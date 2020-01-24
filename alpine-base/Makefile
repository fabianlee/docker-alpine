OWNER := fabianlee
PROJECT := alpine-base
# matching version used from alpine
VERSION := 3.11.3
OPV := $(OWNER)/$(PROJECT):$(VERSION)

docker-build: 
	sudo docker build -f Dockerfile --build-arg ALPINE_BASE_VERSION=$(VERSION) -t $(OPV) .
	@echo "\n======================="
	@echo "run 'make docker-run' to test"
	@echo "======================="

## cleans docker image
docker-clean: 
	sudo docker image rm $(OPV) | true

#docker-run: 
#	sudo docker run -it --rm --buildarg $(OPV) /bin/sh

## runs container in background
docker-test: 
	sudo docker run -it $(OPV) /bin/sh

## run container in interactive mode
docker-run: 
	sudo docker run -d -it --rm --name $(PROJECT) $(OPV)

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



