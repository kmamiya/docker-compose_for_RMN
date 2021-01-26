FROM ruby:2.6.3

ARG USER_ID=1000
ARG USER_GROUP_ID=1000
ARG USER_NAME=worker
ARG APP_NAME=rails_app

ENV NODEJS_VERSION 14.15.4
ENV NODEJS_PATH /usr/local/node-v${NODEJS_VERSION}-linux-x64
ENV PATH ${NODEJS_PATH}/bin:${PATH}

RUN groupadd -g $USER_GROUP_ID $USER_NAME \
  && useradd -u $USER_ID -g $USER_NAME -m $USER_NAME \
  \
  && wget https://nodejs.org/dist/v${NODEJS_VERSION}/node-v${NODEJS_VERSION}-linux-x64.tar.xz \
  && tar xfJ node-v${NODEJS_VERSION}-linux-x64.tar.xz -C /usr/local \
  && rm node-v${NODEJS_VERSION}-linux-x64.tar.xz \
  && node --version \
  \
  && apt-get update && apt-get -y install apt-transport-https \
  && wget -O - https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - \
  && echo 'deb https://dl.yarnpkg.com/debian/ stable main' >> /etc/apt/sources.list.d/yarn.list \
  && apt-get update && apt-get -y install yarn \
  && yarn --version

VOLUME /mnt/${APP_NAME}
VOLUME ${NODEJS_PATH}

USER ${USER_NAME}

WORKDIR /mnt/${APP_NAME}
