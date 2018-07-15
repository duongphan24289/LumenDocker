FROM centos:latest
MAINTAINER MrPhan <duong.pv@neo-lab.vn>

# add user
ARG AGENT_ID=1000
RUN adduser -s /bin/sh -u ${AGENT_ID} apache

RUN yum clean all
RUN yum -y update

RUN rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
RUN rpm -Uvh http://rpms.famillecollet.com/enterprise/remi-release-7.rpm

RUN yum --enablerepo=remi-php70 install php php-devel php-gd php-xml php-mbstring php-opcache php-mcrypt php-mysqlnd -y

RUN yum install -y nano
RUN yum install -y vim

# Install Composer
RUN  curl -sS https://getcomposer.org/installer | php && mv composer.phar /usr/local/bin/composer

# Clear yum cache
RUN yum clean all

RUN mkdir -p /var/www/html/keirin_api
RUN chmod -R 755 /var/www/html/keirin_api

# config virtual host
ADD keirin-test.conf /etc/httpd/conf.d
# workspace
WORKDIR /var/www/html/keirin_api/
# for web
EXPOSE 80
EXPOSE 443

CMD /usr/sbin/httpd -DFOREGROUND