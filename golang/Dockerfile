ARG GO_VERSION=1.16

FROM golang:${GO_VERSION} as builder

RUN go install github.com/go-delve/delve/cmd/dlv@latest

ARG GO_VERSION=1.16

FROM golang:${GO_VERSION}

RUN apt-get update && apt-get install -y --no-install-recommends \
            ca-certificates curl \
            build-essential gcc g++ \
            tzdata zip unzip vim wget \
            git openssh-client bash net-tools sudo \
    # Clean up
        && apt-get autoremove -y \
        && apt-get clean -y \
        && rm -rf /var/lib/apt/lists/*

COPY --from=builder /go/bin/dlv /usr/local/bin/dlv
