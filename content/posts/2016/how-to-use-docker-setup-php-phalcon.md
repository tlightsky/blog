---
layout: post
title:  "如何用docker快速搭建phalcon运行环境"
date:   2016-03-14 09:51:02
categories: phalcon php docker
---

使用docker的话还是相对比较简单的，
不过找了下docker hub上的现有image，排名靠前的[eboraas/phalcon][eboraas/phalcon]出现了thread-safe的错误提示用不了
只好自己动手了。

基于之前的laravel docker的[Dockerfile][Dockerfile]改了改：


```dockerfile
FROM centurylink/apache-php:latest
MAINTAINER Derek Myers <arcticpro@gmail.com>

# Install packages
RUN apt-get update && \
 DEBIAN_FRONTEND=noninteractive apt-get -y upgrade && \
 DEBIAN_FRONTEND=noninteractive apt-get -y install supervisor pwgen && \
 apt-get -y install mysql-client libmcrypt4 php5-mcrypt php5-json php5-curl php5-cli

# Override default apache conf
ADD apache.conf /etc/apache2/sites-enabled/000-default.conf

# Enable apache rewrite module
RUN a2enmod rewrite

# Enable php mcrypt module
RUN php5enmod mcrypt

# Configure /app folder
RUN mkdir -p /app && rm -fr /var/www/html && ln -s /app/public /var/www/html

#-----------------------------------------

# This is no longer available by default in jessie's apache2
RUN /usr/sbin/a2enmod socache_shmcb || true

# Note: "default" is enabled in the default installation, and "default-ssl" is enabled in the eboraas/apache image, so no need to recreate the symlinks here, just copy the new site definitions into place
# ADD default /etc/apache2/sites-available/
# ADD default-ssl /etc/apache2/sites-available/

# WORKDIR /tmp
# Run build process on one line to avoid generating bloat via intermediate images
RUN /usr/bin/apt-get update && apt-get -y install git php5-dev libpcre3-dev gcc make && \
    /usr/bin/git clone git://github.com/phalcon/cphalcon.git && \
    cd cphalcon/build/ && \
    ./install && \
    cd /tmp && \
    /bin/rm -rf /tmp/cphalcon/ && \
    /usr/bin/apt-get -y purge git php5-dev libpcre3-dev gcc make && apt-get -y autoremove && apt-get clean
RUN /bin/echo 'extension=phalcon.so' >/etc/php5/mods-available/phalcon.ini
RUN /usr/sbin/php5enmod phalcon
WORKDIR /app/public/
RUN /bin/echo '<html><body><h1>It works!</h1></body></html>' > /app/public/index.html

EXPOSE 80
EXPOSE 443

CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]
```


[eboraas/phalcon]:  https://hub.docker.com/r/eboraas/phalcon/
[Dockerfile]:       https://hub.docker.com/r/dmyers/laravel/~/dockerfile/
