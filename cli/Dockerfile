FROM ubuntu:latest

RUN apt update && apt install -y curl
RUN curl -s https://packagecloud.io/install/repositories/sensu/stable/script.deb.sh | bash
RUN apt install -y sensu-go-cli

ARG user
ARG pw
ARG backendurl
RUN echo admin $user $backendurl && curl -s $backendurl/version
RUN sensuctl configure -n --username $user --password $pw --url $backendurl