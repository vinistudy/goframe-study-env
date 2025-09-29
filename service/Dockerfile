FROM ubuntu:24.04

RUN apt-get update && apt-get install -y curl wget git vim ca-certificates && rm -rf /var/lib/apt/lists/*

ARG GO_VERSION=1.25.1

ARG GO_TAR=go${GO_VERSION}.linux-amd64.tar.gz

RUN wget https://golang.google.cn/dl/${GO_TAR} -O /tmp/${GO_TAR} && \
    rm -rf /usr/local/go && \
    tar -C /usr/local -xzf /tmp/${GO_TAR} && \
    rm /tmp/${GO_TAR}

ENV PATH=$PATH:/usr/local/go/bin:/go/bin
ENV GOPATH=/go

RUN go env -w GO111MODULE=on && \
    go env -w GOPROXY=https://goproxy.cn,direct && \
    go env -w GOSUMDB=sum.golang.google.cn

RUN wget -O gf https://github.com/gogf/gf/releases/latest/download/gf_$(go env GOOS)_$(go env GOARCH) && chmod +x gf && ./gf install -y && rm ./gf

RUN mkdir -p /app $GOPATH/bin $GOPATH/pkg $GOPATH/src

WORKDIR /app

CMD ["bash"]