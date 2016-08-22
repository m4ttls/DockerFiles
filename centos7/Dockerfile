FROM centos:7

MAINTAINER m4ttls <m4ttls@hotmail.com.ar>

# Install core RPMs
RUN yum -y install \
  java-1.8.0-openjdk \
  java-1.8.0-openjdk-devel \
  wget

RUN wget http://repo1.maven.org/maven2/org/eclipse/jetty/jetty-distribution/9.3.11.v20160721/jetty-distribution-9.3.11.v20160721.tar.gz
RUN tar zxvf jetty-distribution-9.3.11.v20160721.tar.gz -C /opt/
RUN mv /opt/jetty-distribution-9.3.11.v20160721/ /opt/jetty
RUN useradd -m jetty
RUN chown -R jetty:jetty /opt/jetty/
RUN ln -s /opt/jetty/bin/jetty.sh /etc/init.d/jetty
RUN chkconfig --add jetty
RUN chkconfig --level 345 jetty on
RUN touch /etc/default/jetty
RUN echo 'JETTY_HOME=/opt/jetty' >> /etc/default/jetty
RUN echo 'JETTY_USER=jetty' >> /etc/default/jetty
RUN echo 'JETTY_PORT=8080' >> /etc/default/jetty
RUN echo $(hostname -I | cut -d" " -f 1)
RUN echo 'JETTY_HOST='$(hostname -I | cut -d" " -f 1) >> /etc/default/jetty
RUN echo 'JETTY_LOGS=/opt/jetty/logs/' >> /etc/default/jetty
RUN service jetty start

# Create the data dir.
RUN mkdir /data

# Define working directory.
WORKDIR /data

# Open port 8080 for app
EXPOSE 8080

# Expose our source directory.
VOLUME ["/lakaut", "/data"]

# COPY ./config/build-serve.sh /
# ENTRYPOINT ["/build-serve.sh"]
