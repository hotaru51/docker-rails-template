FROM node:10.15.3-stretch AS node
FROM ruby:2.6.3-stretch

ENV YARN_VERSION=1.13.0
ENV LANG=C.UTF-8

COPY --from=node /usr/local/bin/node /usr/local/bin
COPY --from=node /usr/local/lib/node_modules /usr/local/lib/node_modules
COPY --from=node /opt/yarn-v${YARN_VERSION} /opt/yarn
RUN ln -s /usr/local/lib/node_modules/npm/bin/npm-cli.js /usr/local/bin/npm \
    && ln -s /opt/yarn/bin/yarn /usr/local/bin/yarn

RUN apt-get update \
    && apt-get -y install build-essential \
    mysql-client \
    postgresql-client \
    sqlite3 \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

RUN gem install bundler

COPY Gemfile /tmp/
WORKDIR /tmp
RUN bundle install

RUN mkdir /app
WORKDIR /app
