FROM hhvm/hhvm:latest

ADD server.ini /etc/hhvm/server.ini
RUN touch /etc/hhvm/site.ini

EXPOSE 9000

CMD ["/usr/bin/hhvm", "--mode", "server", "-d", "hhvm.server.type=fastcgi", "-c", "/etc/hhvm/server.ini", "-c", "/etc/hhvm/site.ini"]
