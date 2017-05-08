FROM hypriot/rpi-java
MAINTAINER Roberto Cortez <radcortez@yahoo.com>

ENV PATH /usr/local/tomee/bin:$PATH
RUN mkdir -p /usr/local/tomee

WORKDIR /usr/local/tomee

RUN set -x \
    && apt-get update \
    && apt-get install curl \
	&& curl -fSL https://s3-eu-west-1.amazonaws.com/jgallimore/tomee-70x-with-metrics-1.0-MB.7-SNAPSHOT.tar.gz -o tomee.tar.gz \
	&& tar -zxf tomee.tar.gz \
	&& mv apache-tomee/* /usr/local/tomee \
	&& rm -Rf apache-tomee \
	&& rm bin/*.bat \
	&& rm -Rf webapps/* \
	&& rm tomee.tar.gz* \
  && printf "<tomee>\n\t<Resource id=\"ElasticSearchClient\" class-name=\"com.tomitribe.tomee.metrics.core.elasticsearch.ElasticSearchFastEventDataStore\">\n\t\tcollectors = http://pi-elastic-01:9200\n\t\tperiod = 1000\n\t</Resource>\n\t<Resource id=\"MetricsService\" class-name=\"com.tomitribe.tomee.metrics.core.service.MetricsService\">\n\t\tdataStore = ElasticSearchClient\n\t</Resource>\n</tomee>" > /usr/local/tomee/conf/tomee.xml

EXPOSE 8080
CMD ["catalina.sh", "run"]
