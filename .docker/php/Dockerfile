FROM php:7.2-fpm

LABEL maintainer "Gift Hlongoane <GiftHl@miway.co.za>"

RUN  apt-get update \
	&& apt-get install -y \
		zip \
		unzip \
		vim \
		wget \
		curl \
		git \
		nodejs \
		moreutils \
		dnsutils \
		zlib1g-dev \
		libicu-dev \
		libmemcached-dev \
		mysql-client \
		libsqlite3-dev \
		libsqlite3-0 \
		libxml2-dev \
		libxslt-dev \
		firebird-dev \
		libtidy-dev \
		libpspell-dev \
		libldb-dev \
		libldap2-dev \
		libc-client-dev \
		libkrb5-dev \
		librecode-dev \
		libpq-dev \
		libxslt-dev \
		# libsnmp-dev \ causes noise
		# libmcrypt-dev \
		libpng-dev \
		# firebird2.5-dev \
		#php7.1-readline \
		#php7.1-phpdbg \
		#php7.1-sybase \
		#php7.1 \
		# php7.1-sqlite3 \
		# php7.1-opcache \
		# php7.1-json \
		# php7.1-xmlrpc \
		# php7.1-curl \
		g++ \
    && rm -rf /var/lib/apt/lists/*

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
RUN composer --version

# Install app dependencies
# COPY ./../ /app
# RUN cd /app && \
#     composer install --no-interaction 
# RUN composer install --no-interaction 

# Set your timezone here
RUN rm /etc/localtime
RUN ln -s /usr/share/zoneinfo/Africa/Johannesburg /etc/localtime
RUN "date"

# Install memcached extension
#RUN git clone https://github.com/php-memcached-dev/php-memcached /usr/src/php/ext/memcached \
#    && cd /usr/src/php/ext/memcached && git checkout -b php7 origin/php7 \
#    && docker-php-ext-configure memcached \
#    && docker-php-ext-install memcached

# Run docker-php-ext-install for available extensions
RUN docker-php-ext-configure ldap --with-libdir=lib/x86_64-linux-gnu
RUN docker-php-ext-configure imap --with-kerberos --with-imap-ssl
RUN docker-php-ext-configure intl \
    && docker-php-ext-install \
	pdo \
	pdo_mysql \
	opcache \
	intl \
	xml \
	xsl \
	mbstring \
	zip \
	mysqli \
	pdo_mysql \
	interbase \
	pdo_sqlite \
	tidy \
	opcache \
	pspell \
	json \
	xmlrpc \
	ldap \
	# php7.1-bz2 \
	# php7.1-cgi \
	imap \
	# php7.1-cli \
	dba \
	# php7.1-dev \
	intl \
	# php7.1-fpm \
	recode \
	# php7.1-odbc \
	# php7.1-gmp \
	# php7.1-common \
	pgsql \
	bcmath \
	# snmp \ causes noise
	soap \
	# mcrypt \
	gd 
	# php7.1-enchant \
	# libphp7.1-embed \
	# tdsodbc \

# install xdebug
RUN pecl install xdebug
RUN docker-php-ext-enable xdebug \
    && echo "error_reporting = E_ALL" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && echo "display_startup_errors = On" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && echo "display_errors = On" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && echo "xdebug.remote_enable = 1" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && echo "xdebug.remote_connect_back = 1" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && echo "xdebug.idekey = \"PHPSTORM\"" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && echo "xdebug.remote_port = 9001" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini

RUN usermod -u 777 www-data
# RUN /bin/sh -c 'cd /app; composer install --no-interaction'
# RUN composer install --no-interaction 
# RUN cd ./app && \
#     composer install --no-interaction 

#  COPY ./ /var/www/html
# RUN composer install --no-dev --no-interaction -o

CMD php-fpm -F
