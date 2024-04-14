FROM alpine:3.19

ENV TEX_VERSION=2024
ENV PS1='\[\033[01;32m\]\u\[\033[00m\]:\[\033[01;34m\]\w\[\033[00m\]\$ '
# ${debian_chroot:+($debian_chroot)}
# アップデートや言語設定
# RUN apt-get update
# RUN apt-get -y install locales && \
#     localedef -f UTF-8 -i ja_JP ja_JP.UTF-8
# ENV LANG ja_JP.UTF-8
# ENV LANGUAGE ja_JP:ja
# ENV LC_ALL ja_JP.UTF-8
# ENV TZ JST-9
# ENV TERM xterm

RUN mkdir -p /root/workspace
COPY texlive.profile /root/workspace
COPY tex_requires /root/workspace
COPY .latexmkrc /root
WORKDIR /root/workspace

# git関連とperlのインストール
RUN apk --no-cache add \
    libc6-compat \
    git \
    vim \
    curl \
    tree \
    perl \
    # ca-certificates \
    openssh &&\
    curl -LO http://ftp.jaist.ac.jp/pub/CTAN/systems/texlive/tlnet/install-tl-unx.tar.gz && \
    mkdir install-tl && \
    tar xzf install-tl-unx.tar.gz -C install-tl --strip-components 1 && \
    ./install-tl/install-tl --profile texlive.profile && \
    rm -r install-tl install-tl-unx.tar.gz && \
    cat tex_requires | grep -v "^#" | \
    xargs /usr/local/texlive/${TEX_VERSION}/bin/x86_64-linux/tlmgr install && \
    echo "PS1='"${PS1}"'" > ~/.profile && \
    echo 'PATH="$PATH:/usr/local/texlive/'${TEX_VERSION}'/bin/x86_64-linux"' >> ~/.profile
