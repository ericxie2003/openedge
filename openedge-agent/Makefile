TAG?=latest
SRC=$(wildcard *.go)

all: openedge-agent package.tar.gz

openedge-agent: $(SRC)
	@echo "BUILD $@"
	@go build ${GOFLAG} .

package.tar.gz: openedge-agent
	install -d -m 0755 __package/bin
	cp $< __package/bin
	cp package.yml __package/
	tar czvf $@ -C __package bin package.yml
	rm -rf __package

image: openedge-agent
	@echo "IMAGE $<"
	docker build -t $(IMAGE_PREFIX)$<$(IMAGE_SUFFIX):$(TAG) .

.PHONY: clean
clean:
	rm -f openedge-agent package.tar.gz

.PHONY: rebuild
rebuild: clean all
