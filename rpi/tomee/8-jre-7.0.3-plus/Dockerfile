FROM hypriot/rpi-java
MAINTAINER Roberto Cortez <radcortez@yahoo.com>

ENV PATH /usr/local/tomee/bin:$PATH
RUN mkdir -p /usr/local/tomee

WORKDIR /usr/local/tomee

RUN set -x \
    && apt-get update \
    && apt-get install curl \
	&& curl -fSL https://repo1.maven.org/maven2/org/apache/tomee/apache-tomee/7.0.3/apache-tomee-7.0.3-plus.tar.gz -o tomee.tar.gz \
	&& tar -zxf tomee.tar.gz \
	&& mv apache-tomee-plus-7.0.3/* /usr/local/tomee \
	&& rm -Rf apache-tomee-plus-7.0.3 \
	&& rm bin/*.bat \
	&& rm tomee.tar.gz*

EXPOSE 8080
CMD ["catalina.sh", "run"]
