FROM ubuntu:latest
MAINTAINER kentakuma<hogehogehoge@gmail.com>

# 基本的パッケージを導入

ENV TERM $TERM:xterm
RUN apt-get update
RUN apt-get install -y build-essential wget curl git
RUN apt-get install -y libffi-dev
RUN apt-get install -y zlib1g-dev libssl-dev libreadline-dev libyaml-dev libxml2-dev libxslt-dev
RUN apt-get install -y sqlite3 libsqlite3-dev
RUN apt-get clean

#ruby-buildの導入
RUN git clone https://github.com/sstephenson/ruby-build.git .ruby-build
RUN .ruby-build/install.sh
RUN rm -fr .ruby-build

# ruby　2.2.1のインストール
RUN ruby-build 2.2.1 /usr/local

# bundlerの導入
RUN gem update --system
RUN gem install bundler --no-rdoc --no-ri

# railsコマンドを実行したときのエラー抑止用
RUN apt-get install -y software-properties-common

RUN add-apt-repository ppa:ubuntu-toolchain-r/test
RUN apt-get update
RUN apt-get install -y gcc-4.9 g++-4.9
RUN update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-4.9 100 --slave /usr/bin/g++ g++ /usr/bin/g++-4.9

RUN gem install libv8 -v '3.16.14.11' -- --with-system-v8
RUN bundle config build.libv8 --with-system-v8

# railsのインストール
RUN gem install rails --version="~> 4.2.3" --no-ri --no-rdoc


RUN mkdir ~/workspace
EXPOSE 3000
VOLUME /home/rails/workspace
