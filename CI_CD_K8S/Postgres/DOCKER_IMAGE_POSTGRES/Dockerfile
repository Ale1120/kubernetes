FROM ubuntu:16.04
MAINTAINER Josue

RUN apt-get update
RUN apt-get install locales
RUN echo "LANG=\"en_US.UTF-8\"" > /etc/default/locale
RUN locale-gen en_US.UTF-8

ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

RUN apt-get install -y build-essential openssl libreadline6 libreadline6-dev curl git-core zlib1g zlib1g-dev libssl-dev libyaml-dev libsqlite3-dev sqlite3 libxml2-dev libxslt-dev autoconf libc6-dev $
RUN apt-get update \
  && apt-get install -y wget \
  && rm -rf /var/lib/apt/lists/*
RUN apt-get install -y tar
RUN apt-get install libreadline6 libreadline6-dev
RUN apt-get install -y --reinstall sed
RUN apt-get update && apt-get upgrade -y && apt-get install -y build-essential
RUN wget https://ftp.postgresql.org/pub/source/v10.3/postgresql-10.3.tar.gz
RUN tar xvfz postgresql-10.3.tar.gz

WORKDIR /postgresql-10.3

RUN sed -i "s/NAMEDATALEN 64/NAMEDATALEN 1024/g" src/include/pg_config_manual.h
RUN ./configure
RUN make
RUN make install

COPY docker-entrypoint.sh ../usr/local/bin/

RUN ln -s ../usr/local/bin/docker-entrypoint.sh /

ENTRYPOINT ["docker-entrypoint.sh"]

EXPOSE 5432

CMD ["postgres"]
