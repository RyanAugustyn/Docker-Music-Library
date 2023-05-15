FROM mysql:latest
EXPOSE 3306
COPY init.sql /docker-entrypoint-initdb.d/

#################################
 MySQL Dockerfile

A breakdown of the recommended MySQL Dockerfile structure.


FROM mysql:latest
ENV MYSQL_ROOT_PASSWORD=root
EXPOSE 3306
COPY init.sql /docker-entrypoint-initdb.d/

 
File Breakdown

Here's a breakdown of each line in the Dockerfile with a brief explanation of its purpose:

FROM mysql:latest

This line sets the base image for the Dockerfile as the latest version of the official MySQL image available on Docker Hub. This means that we are building a new image that is based on the existing MySQL image.

ENV MYSQL_ROOT_PASSWORD=root

This line sets an environment variable called MYSQL_ROOT_PASSWORD to the value root. This variable is used to set the root password for the MySQL server instance that will be running in the container.

EXPOSE 3306

This line exposes port 3306 on the container. Port 3306 is the default port for MySQL, so this line ensures that the container can communicate over this port with other services or containers.

COPY init.sql /docker-entrypoint-initdb.d/

This line copies a file called init.sql from the local directory into the /docker-entrypoint-initdb.d/ directory inside the container. This directory is used by the MySQL image to run initialization scripts when the container starts up. In this case, the init.sql file will be run by the MySQL server instance to create a database and set up any necessary tables or data.