FROM php:7.1-fpm

#ADD sources.list /etc/apt/sources.list

RUN apt-get update \
    && apt-get install -y wget python2.7 python2.7-dev python-pip libmysqlclient-dev libxml2-dev libxslt1-dev mysql-client cron supervisor rsyslog libzip-dev libjpeg62-turbo-dev libpng12-dev libfreetype6-dev git libssl-dev pkg-config libmcrypt-dev

# Install modules
#RUN pecl install redis
    #&& docker-php-ext-enable redis
#RUN pecl install swoole && docker-php-ext-enable swoole
#RUN pecl install xdebug && docker-php-ext-enable xdebug
#RUN pecl install mongodb && docker-php-ext-enable mongodb
#RUN docker-php-ext-install zip pdo_mysql mysql mysqli gd bcmath mcrypt

RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/
RUN docker-php-ext-install -j$(nproc) gd

#ADD php-fpm.conf    /usr/local/etc/php-fpm.conf

RUN mkdir -p /var/log/supervisor

RUN pip install -U pip setuptools -i http://pypi.douban.com/simple
RUN pip install beautifulsoup4 MySQL-python requests lxml html5lib python-dotenv -i http://pypi.douban.com/simple --trusted-host pypi.douban.com

ADD composer.phar    /usr/local/bin/composer

#COPY ./package/node-v6.10.1-linux-x64.tar.xz /root/

#RUN tar -Jxf /root/node-v6.10.1-linux-x64.tar.xz -C /root/ && \
#    mv /root/node-v6.10.1-linux-x64 /usr/local/node && \
#    rm -rf /root/node-v6.10.1-linux-x64.tar.xz
    #echo 'export NODE_HOME=/usr/local/node' >> ~/.profile && \
    #echo 'export PATH=$PATH:$NODE_HOME/bin' >> ~/.profile
    #sh source ~/.profile
ENV NODE_HOME /usr/local/node
ENV PATH $PATH:$NODE_HOME/bin

RUN docker-php-ext-install zip pdo_mysql mysqli bcmath mcrypt
# JPEG Support enable
RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd
#RUN pecl install swoole && docker-php-ext-enable swoole
RUN pecl install mongodb && docker-php-ext-enable mongodb
#RUN pecl install yac-2.0.2 && docker-php-ext-enable yac
#RUN pecl install redis && docker-php-ext-enable redis
#RUN pecl install inotify && docker-php-ext-enable inotify
# pecl install <package> for error : No releases available for package "pecl.php.net/redis" 暂时无法解决
RUN wget http://pecl.php.net/get/redis && pecl install -O redis && docker-php-ext-enable redis
RUN wget http://pecl.php.net/get/xdebug && pecl install -O xdebug && docker-php-ext-enable xdebug
RUN wget http://pecl.php.net/get/swoole && pecl install -O swoole && docker-php-ext-enable swoole
#CMD ["/usr/bin/supervisord"]
#CMD ["sh -c source ~/.profile"]

#RUN tar -Jxf /root/node-v6.10.1-linux-x64.tar.xz -C /root/ && \
#    mv /root/node-v6.10.1-linux-x64 /usr/local/node && \
#    rm -rf /root/node-v6.10.1-linux-x64.tar.xz
    #echo 'export NODE_HOME=/usr/local/node' >> ~/.profile && \
    #echo 'export PATH=$PATH:$NODE_HOME/bin' >> ~/.profile
    #sh source ~/.profile
ENV NODE_HOME /usr/local/node
ENV PATH $PATH:$NODE_HOME/bin

RUN wget -P /root/ https://npm.taobao.org/mirrors/node/v8.9.3/node-v8.9.3-linux-x64.tar.xz
#COPY ./package/node-v8.9.3-linux-x64.tar.xz /root/
RUN tar -Jxf /root/node-v8.9.3-linux-x64.tar.xz -C /root/ && \
    mv /root/node-v8.9.3-linux-x64 /usr/local/node && \
    rm -rf /root/node-v8.9.3-linux-x64.tar.xz
    #echo 'export NODE_HOME=/usr/local/node' >> ~/.profile && \
    #echo 'export PATH=$PATH:$NODE_HOME/bin' >> ~/.profile
    #sh source ~/.profile
ENV NODE_HOME /usr/local/node
ENV PATH $PATH:$NODE_HOME/bin
RUN npm install -g cnpm --registry=https://registry.npm.taobao.org
RUN wget https://phar.phpunit.de/phpunit.phar \
    && chmod +x phpunit.phar \
    && mv phpunit.phar /usr/local/bin/phpunit
RUN docker-php-ext-install pcntl
ADD php.ini  /usr/local/etc/php/php.ini
RUN npm install --global gulp

WORKDIR /var/www