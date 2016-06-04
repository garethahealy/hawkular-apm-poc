[![Build Status](https://travis-ci.org/garethahealy/hawkular-poc.svg?branch=master)](https://travis-ci.org/garethahealy/hawkular-poc)

# hawkular-poc
PoC around Hawkluar monitoring
- http://www.hawkular.org

## Running Hawkular
Firstly, clone the docker repo, which is based on https://github.com/jboss-dockerfiles/hawkular:
- git clone https://github.com/garethahealy/hawkular.git

Secondly, update hawkular/hawkular-aio/custom.properties to contain the correct IP of your docker host:
- cd hawkular/hawkular-aio
- vi custom.properties

Thirdly, build it:
- docker build --tag jboss/hawkular11 .

Now run it:
- docker run -p 8080:8080 --name hawkular -v /tmp/hawkular:/opt/data jboss/hawkular11

Once hawkular has started, you can access it via: http://{docker host}:8080/hawkular-ui.

On first login, you will need to create a user account as per:
- U: admin
- P: Admin123!

## Running Camel example
The Camel example is based on https://github.com/fabric8io/ipaas-quickstarts/tree/master/quickstart/cdi/camel-jetty
- cd fabric8io-quickstart-camel-jetty
- mvn -Pf8-build
- docker run -p 9102:8080 --name camel-jetty fabric8/cdi-camel-jetty:2.2.28

Update JAVA_OPTS located in the camel-jetty/pom.xml, so that camel-jetty can see the BTM docker container, as per:
- <JAVA_OPTIONS>-javaagent:/deployments/bin/hawkular-btm-agent-rest-0.7.4.Final.jar -Dhawkular-btm.base-uri=http://172.17.0.2:8080/hawkular/btm -Dhawkular-btm.config.refresh=10 -Dhawkular-btm.username=admin -Dhawkular-btm.password=Admin123! -Dhawkular-btm.tenantId=d189128c-2a7b-11e6-b67b-9e71128cae77 -Dhawkular-btm.log.level=FINEST</JAVA_OPTIONS>

Test by hitting: http://{docker host}:9102/camel/hello?name=gareth







