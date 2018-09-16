FROM centos:latest
RUN set -x \
        && cd /home \
        && yum install -y wget \
        && wget http://am1.php.net/distributions/php-7.2.2.tar.gz \
        && tar zxvf php-7.2.2.tar.gz \
        && cd php-7.2.2 \
        && yum install -y make gcc gcc-c++ libxml2 libxml2-devel autoconf libjpeg libjpeg-devel libpng libpng-devel freetype freetype-devel zlib zlib-devel glibc glibc-devel glib2 glib2-devel curl curl-devel libxslt-devel openssl-devel \
        && ./configure --prefix=/usr/local/php --with-curl --with-freetype-dir --with-gd --with-gettext --with-iconv-dir --with-kerberos --with-libdir=lib64 --with-libxml-dir  --with-pdo-mysql --with-mysqli --with-openssl --with-pcre-regex --with-pdo-mysql --with-pdo-sqlite --with-pear --with-png-dir --with-xmlrpc --with-xsl --with-zlib --enable-fpm --enable-bcmath --enable-libxml --enable-inline-optimization --enable-gd-native-ttf --enable-mbregex --enable-mbstring --enable-opcache --enable-pcntl --enable-sockets --enable-sysvsem --enable-xml --enable-zip \
        && make \
        && make install \
        && cp php.ini-development /usr/local/php/lib/php.ini \
        && cp /usr/local/php/etc/php-fpm.conf.default /usr/local/php/etc/php-fpm.conf \
        && cp sapi/fpm/init.d.php-fpm /etc/init.d/php-fpm \
        && cp /usr/local/php/etc/php-fpm.d/www.conf.default /usr/local/php/etc/php-fpm.d/www.conf \
        && groupadd www \
        && useradd www -g www \
        && rm -rf /home/php-7.2.2 \
        && cd /home \
        && wget https://github.com/edenhill/librdkafka/archive/v0.11.5.tar.gz \
        && tar zxvf v0.11.5.tar.gz \
        && cd librdkafka-0.11.5 \
        && ./configure \
        && make \
        && make install \
        && cd /home \
        && rm -rf /home/librdkafka-0.11.5 \
        && wget https://github.com/arnaud-lb/php-rdkafka/archive/3.0.5.tar.gz \
        && tar zxvf 3.0.5.tar.gz \
        && cd php-rdkafka-3.0.5 \
        && /usr/local/php/bin/phpize \
        && ./configure  --with-php-config=/usr/local/php/bin/php-config \
        && make \
        && make install \
        && sed -i '/;extension=shmop/a\extension=rdkafka' /usr/local/php/php.ini \
        && cd /home \
        && rm -rf /home/php-rdkafka-3.0.5\
        && yum remove -y -nodeps make gcc gcc-c++ libxml2 libxml2-devel autoconf libjpeg libjpeg-devel libpng libpng-devel freetype freetype-devel zlib zlib-devel glibc glibc-devel glib2 glib2-devel curl curl-devel libxslt-devel openssl-devel\
        && yum clean all \
        && rm -rf /tmp/* \
        && /usr/local/php/bin/php -v
ENTRYPOINT ["/usr/local/php/sbin/php-fpm" " -F"]