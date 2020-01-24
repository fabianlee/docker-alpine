OWNER := fabianlee
PROJECT := alpine-apache
VERSION := $(shell cat VERSION)
OPV := $(OWNER)/$(PROJECT):$(VERSION)
EXPOSED_PORT := 8080

## builds docker image
docker-build: version-exists
	## use template to construct actual index.html containing version
	cp root/var/www/localhost/htdocs/index.html.template root/var/www/localhost/htdocs/index.html
	sed -i 's/$${VERSION}/$(VERSION)/g' root/var/www/localhost/htdocs/index.html
	## now build docker image
	sudo docker build -f Dockerfile --build-arg APACHE2_VERSION="$(VERSION)" -t $(OPV) .

## make sure we have file containing version
version-exists:
	test -f VERSION

## cleans docker image
clean: version-exists
	sudo docker image rm $(OPV) | true

## runs container in background
docker-test: version-exists
	sudo docker run -it -p $(EXPOSED_PORT):80 $(OPV) /bin/sh

## run container in interactive mode
docker-run: version-exists
	sudo docker run -d -it --rm --name $(PROJECT) -p $(EXPOSED_PORT):80 $(OPV)

## get to console of running container
docker-ssh:
	sudo docker exec -it $(PROJECT) /bin/sh

## tails docker logs
docker-logs:
	sudo docker logs -f $(PROJECT)

## stops container running in background
docker-stop:
	sudo docker stop $(PROJECT)

## pushes to docker hub
docker-push:
	sudo docker push $(OPV)
