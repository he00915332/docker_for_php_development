FROM php:7.4.16-fpm

COPY ./init_base /var/project

RUN apt-get update && apt-get install -yq libzip-dev zip git libfreetype6-dev \
    libjpeg62-turbo-dev \
    libmcrypt-dev \
    libssl-dev \
    libmemcached-dev \
    libz-dev \
    zlib1g-dev \
    libsqlite3-dev \
    libxml2-dev \
    libcurl3-dev \
    libedit-dev \
    libpspell-dev \
    libldap2-dev \
    unixodbc-dev \
    libpq-dev \
    wget \
    git \
    vim \
    nano \
    sudo \
    cron \
    net-tools \
    iputils-ping \
    procps \
    systemd \
    supervisor \
    nodejs \
    libonig-dev \
    npm

# opcache
RUN docker-php-ext-install opcache

# composer
RUN curl -sS https://getcomposer.org/installer | php
RUN mv composer.phar /usr/local/bin/composer

#docker ext
RUN docker-php-ext-configure zip
RUN docker-php-ext-install mysqli pdo pdo_mysql zip mbstring tokenizer pcntl soap
RUN docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install gd
RUN pecl install memcached \
    && docker-php-ext-enable memcached

# nvm node npm
RUN rm /bin/sh && ln -s /bin/bash /bin/sh
RUN curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.35.2/install.sh | bash
ENV NVM_DIR /root/.nvm
ENV NODE_VERSION v15.14.0
RUN /bin/sh -c ". ~/.bashrc"
RUN . $NVM_DIR/nvm.sh \
    && nvm install $NODE_VERSION \
    && nvm alias default $NODE_VERSION \
    && nvm use default

#timeZone
ENV TZ=Asia/Taipei
RUN ln -snf /usr/share/zoneinfo/${TZ} /etc/localtime && echo ${TZ} > /etc/timezone

RUN npm i -g create-nuxt-app
RUN npm i -g pm2
EXPOSE 3000
ENV HOST 0.0.0.0
WORKDIR /var/project/01WorkSpace/01JSAdways