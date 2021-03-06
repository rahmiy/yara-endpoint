# Build stuff
VERSION=v0.1.0
BUILD_TIME=`date +%FT%T%z`
BUILD=`git rev-parse HEAD`
LDFLAGS="-s -w \
	-X main.Version=${VERSION} \
	-X main.BuildID=${BUILD} \
	-X main.BuildDate=${BUILD_TIME}"

YARA_VERSION := v3.7.1
YARA_TAG := yara3.7
GO := $(shell which go)
XGO := $(shell which xgo)
DOCKER := $(shell which docker)
TARGET_DIR := build
OUT_NAME := yep-server

# "yara-rules/x-go-yara"
DOCKER_IMAGE := "x-go-yara"
# DOCKER_BUILD := $(shell docker images | grep $(DOCKER_IMAGE))
DEPS := "https://github.com/VirusTotal/yara/archive/$(YARA_VERSION).tar.gz"


.PHONY: all clean local linux linux-x86 linux-x64 darwin darwin-x86 darwin-x64 windows windows-x86 windows-x64

ifeq ($(GO), "")
	@echo "You must install Go first. Please visit https://golang.org/ and follow the instructions"
	exit 1
endif
ifeq ($(DOCKER), "")
	@echo "You must install Docker first. Please visit https://www.docker.com/ and follow the instructions"
	exit 1
endif
# ifeq ($(DOCKER_BUILD), "")
# 	@echo "Building a docker image to compile Yara-Endpoint"
# 	$(shell docker build "https://github.com/Xumeiquer/xgo.git#:docker/go-latest" -t $(DOCKER_IMAGE))
# endif

all:
	xgo -image $(DOCKER_IMAGE) -tags $(YARA_TAG) -ldflags $(LDFLAGS) -dest build -out $(OUT_NAME) -deps $(DEPS) -targets="linux/*,darwin/*,windows/*" .

linux:
	xgo -image $(DOCKER_IMAGE) -tags $(YARA_TAG) -ldflags $(LDFLAGS) -dest build -out $(OUT_NAME) -deps $(DEPS) -targets="linux/*" .

linux-x86:
	xgo -image $(DOCKER_IMAGE) -tags $(YARA_TAG) -ldflags $(LDFLAGS) -dest build -out $(OUT_NAME) -deps $(DEPS) -targets="linux/386" .

linux-x64:
	xgo -image $(DOCKER_IMAGE) -tags $(YARA_TAG) -ldflags $(LDFLAGS) -dest build -out $(OUT_NAME) -deps $(DEPS) -targets="linux/amd64" .

darwin:
	xgo -image $(DOCKER_IMAGE) -tags $(YARA_TAG) -ldflags $(LDFLAGS) -dest build -out $(OUT_NAME) -deps $(DEPS) -targets="darwin/*" .

darwin-x86:
	xgo -image $(DOCKER_IMAGE) -tags $(YARA_TAG) -ldflags $(LDFLAGS) -dest build -out $(OUT_NAME) -deps $(DEPS) -targets="darwin/386" .

darwin-x64:
	xgo -image $(DOCKER_IMAGE) -tags $(YARA_TAG) -ldflags $(LDFLAGS) -dest build -out $(OUT_NAME) -deps $(DEPS) -targets="darwin/amd64" .

windows:
	xgo -image $(DOCKER_IMAGE) -tags $(YARA_TAG) -ldflags $(LDFLAGS) -dest build -out $(OUT_NAME) -deps $(DEPS) -targets="windows/*" .

windows-x86:
	xgo -image $(DOCKER_IMAGE) -tags $(YARA_TAG) -ldflags $(LDFLAGS) -dest build -out $(OUT_NAME) -deps $(DEPS) -targets="windows/386" .

windows-x64:
	xgo -image $(DOCKER_IMAGE) -tags $(YARA_TAG) -ldflags $(LDFLAGS) -dest build -out $(OUT_NAME) -deps $(DEPS) -targets="windows/amd64" .

local:
	go get -u
	go build -o "$(TARGET_DIR)/$(OUT_NAME)" -ldflags $(LDFLAGS) .

clean:
	rm -rf $(TARGET_DIR)
