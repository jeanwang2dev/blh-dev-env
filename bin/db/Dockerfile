# MYSQL
FROM mariadb:10.3.30

ENV MYSQL_ROOT_PASSWORD=${MYSQL_ROOT_PASSWORD}
ENV MYSQL_DATABASE=${MYSQL_DATABASE}
ENV MYSQL_USER=${MYSQL_USER}
ENV MYSQL_PASSWORD=${MYSQL_PASSWORD}
ENV MYSQL_INITDB_SKIP_TZINFO=1

# wordpress basic sql to start with
# MYSQL will import the sql file at startup
# COPY distillery_dev_wpdb.sql /docker-entrypoint-initdb.d/