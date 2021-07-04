#wordpress
FROM wordpress:5.7.2-php7.4-fpm


# permission solution
RUN apt-get update && apt-get install acl -y
WORKDIR /
COPY setuser.sh /
RUN chmod +x setuser.sh

RUN sed -i '/^exec "\$@"/i cd ../../../' /usr/local/bin/docker-entrypoint.sh
RUN sed -i '/^exec "\$@"/i mv setuser.sh /var/www/html/setuser.sh' /usr/local/bin/docker-entrypoint.sh
RUN sed -i '/^exec "\$@"/i cd /var/www/html' /usr/local/bin/docker-entrypoint.sh
RUN sed -i '/^exec "\$@"/i sh setuser.sh' /usr/local/bin/docker-entrypoint.sh
# RUN sed -i '/^exec "\$@"/i rm -f setuser.sh' /usr/local/bin/docker-entrypoint.sh
# RUN cat /usr/local/bin/docker-entrypoint.sh

# prepare to connect to mailhog 
RUN apt-get update &&\
    apt-get install --no-install-recommends --assume-yes --quiet ca-certificates curl git &&\
    rm -rf /var/lib/apt/lists/*
RUN curl -Lsf 'https://storage.googleapis.com/golang/go1.8.3.linux-amd64.tar.gz' | tar -C '/usr/local' -xvzf -
ENV PATH /usr/local/go/bin:$PATH
RUN go get github.com/mailhog/mhsendmail
RUN cp /root/go/bin/mhsendmail /usr/bin/mhsendmail
RUN echo 'sendmail_path = /usr/bin/mhsendmail --smtp-addr mailhog:1025' > /usr/local/etc/php/php.ini

WORKDIR /var/www/html/

# COPY setuser.sh /var/www/html
# RUN chmod +x /var/www/html/setuser.sh
# # # hacking into wordpress entry file 
# # # and adding my script right before the exit
# RUN sed -i '/^exec "\$@"/i sh /var/www/html/setuser.sh' /usr/local/bin/docker-entrypoint.sh
# WORKDIR /var/www/html/
