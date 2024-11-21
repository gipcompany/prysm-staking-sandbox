FROM ubuntu:24.04

RUN apt update
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y software-properties-common
RUN add-apt-repository -y ppa:ethereum/ethereum
RUN apt install -y ethereum
RUN apt install -y curl gnupg

RUN apt install -y ruby
RUN gem install foreman

EXPOSE 4000 7500 8545 8551
