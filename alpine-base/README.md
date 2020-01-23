# alpine-base

A Docker image for running just about anything within a container, based on Alpine Linux.
This image belongs to a suite of images [documented here][dockeralpine].

Image size is ~20.1 MB.

## Features

This image features:

- [Alpine Linux][alpinelinux]
- [s6][s6] and [s6-overlay][s6overlay]
- [go-dnsmasq][godnsmasq]

## Versions

- `3.11.3`

## Usage

To use this image include `FROM fabianlee/alpine-base:3.11.3` at the top of your `Dockerfile`. Starting from `smebberson/alpine-base` provides you with the ability to easily start any service using s6. s6 will also keep it running for you, restarting it when it crashes.

[Read more about extending this image with your own services](https://github.com/smebberson/docker-alpine/tree/master/#using-services).

### DNS

Alpine Linux does not support the `domain` or `search` directives in `resolv.conf`. This breaks many tools that rely on DNS service discovery, in particular, Kubernetes, Docker Cloud, Consul, Rancher. [You can read more about it](http://gliderlabs.viewdocs.io/docker-alpine/caveats/).

To overcome these issues, `alpine-base` includes the lightweight container-only DNS server [go-dnsmasq][godnsmasq] to resolve these issues.

That means that any image extending this image will now work with [Docker Cloud service discovery and links](https://docs.docker.com/docker-cloud/apps/service-links/) and [Kubernetes service discovery](https://github.com/kubernetes/kubernetes/blob/master/docs/user-guide/services.md#dns).

In some environments, `go-dnsmasq` won't be allowed to bind to port `53`. In this instance, you can set the ENV variable `GO_DNSMASQ_RUNAS` to `root`. While not ideal, that should resolve the issue.

## Example

An example of using this image can be found in [examples/user-alpine](alpinebaseexample).

[alpinebaseexample]: https://github.com/smebberson/docker-alpine/tree/master/examples/user-alpine
[godnsmasq]: https://github.com/janeczku/go-dnsmasq
[dockeralpine]: https://github.com/smebberson/docker-alpine
