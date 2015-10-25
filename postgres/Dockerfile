#
# example Dockerfile for https://docs.docker.com/examples/postgresql_service/
#

FROM ubuntu:14.04
MAINTAINER Patrick White whitep@vcu.edu
#MAINTAINER SvenDowideit@docker.com



RUN apt-get update && apt-get install -y python-software-properties software-properties-common postgresql postgresql-contrib postgresql-server-dev-9.3
USER postgres

# Create a PostgreSQL role named ``docker`` with ``docker`` as the password and
# then create a database `docker` owned by the ``docker`` role.
# Note: here we use ``&&\`` to run commands one after the other - the ``\``
#       allows the RUN command to span multiple lines.
RUN    /etc/init.d/postgresql start &&\
    psql --command "CREATE USER patrick WITH SUPERUSER LOGIN;" &&\
    createdb -O patrick twentyeyesdb

# Adjust PostgreSQL configuration so that remote connections to the
# database are possible.
RUN echo "host all  all    0.0.0.0/0  md5" >> /etc/postgresql/9.3/main/pg_hba.conf

# And add ``listen_addresses`` to ``/etc/postgresql/9.3/main/postgresql.conf``
RUN echo "listen_addresses='*'" >> /etc/postgresql/9.3/main/postgresql.conf

# Expose the PostgreSQL port
EXPOSE 5432

# Add VOLUMEs to allow backup of config, logs and databases
VOLUME  ["/etc/postgresql", "/var/log/postgresql", "/var/lib/postgresql"]

# Set the default command to run when starting the container
CMD ["/usr/lib/postgresql/9.3/bin/postgres", "-D", "/var/lib/postgresql/9.3/main", "-c", "config_file=/etc/postgresql/9.3/main/postgresql.conf"]

EXPOSE 5432
CMD ["postgres"]

# pg container
# docker run --name twentyeyes_pg -e POSTGRES_PASSWORD=albatross -d postgres
# app using pg
# docker run --name twentyeyes_web \
# -v /home/workspace/twenteyes_web:/var/www/twentyeyes_web \
# --link twentyeyes_pg:postgres \
# -d docker.io/whitepatrick/twenteyes_web

# available variabls
# POSTGRES_PASSWORD
# POSTGRES_USER
# PGDATA
