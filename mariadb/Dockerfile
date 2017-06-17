FROM mariadb
MAINTAINER Spencer Williams <spencer@aninternetpresence.net>

ENV MYSQL_ROOT_PASSWORD=root \
    MYSQL_DATABASE=kohana \
    MYSQL_USER=kohana \
    MYSQL_PASSWORD='kohana' \
    TERM=xterm

EXPOSE 3311

COPY conf.d/* /etc/mysql/conf.d

VOLUME ["/var/lib/mysql"]