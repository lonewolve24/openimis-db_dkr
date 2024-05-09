FROM  mcr.microsoft.com/mssql/server:2017-latest
ARG ACCEPT_EULA
ENV ACCEPT_EULA=$ACCEPT_EULA
ARG SA_PASSWORD
ENV SA_PASSWORD=$SA_PASSWORD
ENV DB_USER_PASSWORD=$SA_PASSWORD
ENV DB_NAME=IMIS
ENV DB_USER=IMISUser
RUN mkdir -p /app
COPY script/* /app/
WORKDIR /app

ARG SQL_SCRIPT_URL="/home/lone/Desktop/Openimisfhir/openimis-db_dkr-1.4.0/sql-files-v1.7.0-rc0.zip"
RUN apt-get update && apt-get install unzip -y && rm -rf /var/lib/apt/lists/* && unzip $SQL_SCRIPT_URL -d /app
RUN chmod a+x /app/*.sh
CMD /bin/bash ./entrypoint.sh
