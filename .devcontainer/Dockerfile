ARG TEX_VERSION=2024

FROM amd64/alpine:3.19.3 AS builder

ARG TEX_VERSION

RUN mkdir -p /root/workspace
COPY texlive.profile /root/workspace
WORKDIR /root/workspace

RUN apk --no-cache add \
    libc6-compat \
    perl \
    curl &&\
    curl -LO http://ftp.jaist.ac.jp/pub/CTAN/systems/texlive/tlnet/install-tl-unx.tar.gz && \
    mkdir install-tl && \
    tar xzf install-tl-unx.tar.gz -C install-tl --strip-components 1 && \
    ./install-tl/install-tl --profile texlive.profile && \
    rm -r install-tl install-tl-unx.tar.gz


FROM alpine:3.19.3

ARG TEX_VERSION
ARG GLIBC_VERSION=2.34-r0


COPY --from=multiarch/qemu-user-static:latest /usr/bin/qemu-aarch64-static /usr/bin/
COPY --from=builder /usr/local/texlive/ /usr/local/texlive/
COPY .latexmkrc /root
COPY tex_requires /root

WORKDIR /root

ENV PS1='\[\033[01;32m\]\u\[\033[00m\]:\[\033[01;34m\]\w\[\033[00m\]\$ ' \
    PATH="/usr/local/texlive/${TEX_VERSION}/bin/x86_64-linux:${PATH}"

RUN apk --no-cache add \
    git \
    vim \
    curl \
    tree \
    perl \
    # openssl \
    # ca-certificates \
    openssh-client &&\
    echo "PS1='"${PS1}"'" > ~/.profile

RUN if [ "$(uname -m)" = "aarch64" ]; then \
        curl -L -o /etc/apk/keys/sgerrand.rsa.pub https://alpine-pkgs.sgerrand.com/sgerrand.rsa.pub && \
        curl -sLO https://github.com/sgerrand/alpine-pkg-glibc/releases/download/${GLIBC_VERSION}/glibc-${GLIBC_VERSION}.apk && \
        curl -sLO https://github.com/sgerrand/alpine-pkg-glibc/releases/download/${GLIBC_VERSION}/glibc-bin-${GLIBC_VERSION}.apk && \
        apk add --no-cache --force-overwrite \
        xz\
        glibc-${GLIBC_VERSION}.apk \
        glibc-bin-${GLIBC_VERSION}.apk && \
        rm glibc-${GLIBC_VERSION}.apk && \
        rm glibc-bin-${GLIBC_VERSION}.apk && \
        rm -rf /var/cache/apk/*; \
    else \
        apk add --no-cache libc6-compat; \
    fi && \
    cat tex_requires | grep -v "^#" | \
    xargs /usr/local/texlive/${TEX_VERSION}/bin/x86_64-linux/tlmgr install
