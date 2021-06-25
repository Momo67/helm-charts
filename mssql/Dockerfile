FROM ubuntu:20.04

LABEL maintener="Maurice Pittet <maurice.pittet@lausanne.ch>"

ENV SA_PASSWORD=Kr54Fd6c
ENV ACCEPT_EULA=Y

# Dépots, mises à jour et installs
ARG DEBIAN_FRONTEND=noninteractive
RUN apt-get update && apt-get install --assume-yes apt-utils
RUN (apt-get update && apt-get upgrade -y -q && apt-get dist-upgrade -y -q && apt-get -y -q autoclean && apt-get -y -q autoremove)
RUN apt-get install -y wget gnupg software-properties-common apt-transport-https

RUN wget -qO- https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
RUN add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/18.04/mssql-server-2019.list)"
RUN add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/19.10/prod.list)"
RUN apt-get update && apt-get install -y mssql-server
#RUN ACCEPT_EULA=Y apt-get update && apt-get install -y mssql-tools unixodbc-dev
RUN ACCEPT_EULA=Y apt-get update && apt-get install -y mssql-tools
RUN apt-get install -y locales && echo "en_US.UTF-8 UTF-8" > /etc/locale.gen && locale-gen

EXPOSE 1433

CMD [ "/opt/mssql/bin/sqlservr" ]

