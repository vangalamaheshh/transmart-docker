FROM     tomcat:7-jre8
MAINTAINER Alexander De Leon <me@alexdeleon.name>

#Declare environment variables

ENV POSTGRESQL_HOST postgres
ENV POSTGRESQL_PORT 5432
ENV POSTGRESQL_DB transmart
ENV POSTGRESQL_USER postgres
ENV POSTGRESQL_PASSWORD ''

# Install dependencies
RUN apt-get update && apt-get -y install build-essential postgresql php5 sudo rsync supervisor r-base libcairo2-dev

#Install R dependencies
#RUN R CMD BATCH ../scripts/install_r_packages.R


# Install transmartApp WAR
RUN rm -rf /usr/local/tomcat/webapps/ROOT
ADD https://ci.transmartfoundation.org/browse/DEPLOY-TRAPP-14/artifact/shared/transmart.war/transmart.war /usr/local/tomcat/webapps/ROOT.war


# Create config files for transmartApp
ADD config/BuildConfig.groovy /root/.grails/transmartConfig/BuildConfig.groovy
ADD config/Config.groovy /root/.grails/transmartConfig/Config.groovy
ADD config/DataSource.groovy /root/.grails/transmartConfig/DataSource.groovy

# Create supervisor config
COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf

# Ports
# tomcat/transmart
EXPOSE 8080
#postgresql
EXPOSE 5432
#solr
EXPOSE 8983
#rserver
EXPOSE 6311
CMD ["/usr/bin/supervisord"]
