FROM mysql:latest

ENV MYSQL_ROOT_PASSWORD=rootpwd
ENV MYSQL_DATABASE=db_name
ENV MYSQL_USER=db_username
ENV MYSQL_PASSWORD=db_pw

COPY *.sh /docker-entrypoint-initdb.d/
COPY *.sql /docker-entrypoint-initdb.d/