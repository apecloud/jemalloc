# Build the syncer image
# includes syncer and configurations.

## docker buildx build injected build-args:
#BUILDPLATFORM — matches the current machine. (e.g. linux/amd64)
#BUILDOS — os component of BUILDPLATFORM, e.g. linux
#BUILDARCH — e.g. amd64, arm64, riscv64
#BUILDVARIANT — used to set build ARM variant, e.g. v7
#TARGETPLATFORM — The value set with --platform flag on build
#TARGETOS - OS component from --platform, e.g. linux
#TARGETARCH - Architecture from --platform, e.g. arm64
#TARGETVARIANT - used to set target ARM variant, e.g. v7

# Use alpine with tag 20230329 is corresponding to "edge" tag (latest release to date is 3.18) as of 20230625
# FROM docker.io/alpine:edge as dist
FROM registry.cn-hangzhou.aliyuncs.com/xuriwuyun/alpine:edge as dist
ARG APK_MIRROR
ARG TARGETARCH

# copy files
COPY  docker/ /jemalloc/

RUN if [ "$TARGETARCH" = "amd64" ]; then \
        mv /jemalloc/lib_amd64 /jemalloc/lib; \
        rm -rf /jemalloc/lib_arm64; \
    elif [ "$TARGETARCH" = "arm64" ]; then \
        mv /jemalloc/lib_arm64 /jemalloc/lib; \
        rm -rf /jemalloc/lib_amd64; \
    else \
        echo "Unsupported architecture: $TARGETARCH"; \
        exit 1; \
    fi

USER 65532:65532
