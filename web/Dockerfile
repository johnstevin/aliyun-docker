FROM php:5.6-fpm

ADD sources.list /etc/apt/sources.list

RUN apt-get update \
    && apt-get install -y wget python2.7 python2.7-dev python-pip libmysqlclient-dev libxml2-dev libxslt1-dev mysql-client cron supervisor rsyslog libzip-dev libjpeg62-turbo-dev libpng12-dev libfreetype6-dev git libssl-dev pkg-config libmcrypt-dev

# Install modules
RUN pecl install redis && docker-php-ext-enable redis \
    && pecl install swoole && docker-php-ext-enable swoole \
    && pecl install xdebug && docker-php-ext-enable xdebug \
    && pecl install mongodb && docker-php-ext-enable mongodb \
    && docker-php-ext-install zip pdo_mysql mysql mysqli gd bcmath mcrypt

RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/
RUN docker-php-ext-install gd

#ADD php-fpm.conf    /usr/local/etc/php-fpm.conf

RUN mkdir -p /var/log/supervisor

RUN pip install -U pip setuptools -i http://pypi.douban.com/simple
RUN pip install beautifulsoup4 MySQL-python requests lxml html5lib python-dotenv -i http://pypi.douban.com/simple --trusted-host pypi.douban.com

ADD composer.phar    /usr/local/bin/composer

COPY ./package/node-v6.10.1-linux-x64.tar.xz /root/

RUN tar -Jxf /root/node-v6.10.1-linux-x64.tar.xz -C /root/ && \
    mv /root/node-v6.10.1-linux-x64 /usr/local/node && \
    rm -rf /root/node-v6.10.1-linux-x64.tar.xz
    #echo 'export NODE_HOME=/usr/local/node' >> ~/.profile && \
    #echo 'export PATH=$PATH:$NODE_HOME/bin' >> ~/.profile
    #sh source ~/.profile
ENV NODE_HOME /usr/local/node
ENV PATH $PATH:$NODE_HOME/bin

ADD php.ini          /usr/local/etc/php/php.ini

CMD ["/usr/bin/supervisord"]
#CMD ["sh -c source ~/.profile"]

WORKDIR /var/www