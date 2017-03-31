[![Build Status](https://travis-ci.org/garethahealy/hawkular-apm-poc.svg?branch=master)](https://travis-ci.org/garethahealy/hawkular-apm-poc)
[![License](https://img.shields.io/hexpm/l/plug.svg?maxAge=2592000)]()

# hawkular-apm-poc
PoC around Hawkluar APM monitoring
- http://www.hawkular.org

## Running Hawkular APM
To run hawkular apm, you can use the following repo, which contains all the needed Dockerfiles:

    git clone https://github.com/garethahealy/hawkular-aio-docker.git
    cd hawkular-aio-docker
    cd hawkular-apm
    docker-compose up

Once the docker container has started, you can then log into apm:

    http://{docker host}:8081/hawkular-ui/apm/

The docker image auto-generates a user/password, which is printed out at the begining of the start script, i.e.:

    hawkular-apm_1  | ------------------------------------
    hawkular-apm_1  | ATTENTION ATTENTION ATTENTION ATTENTION
    hawkular-apm_1  | We automatically created an admin user for you to access the Hawkular APM web interface:
    hawkular-apm_1  | Username: adminzkR0f-B
    hawkular-apm_1  | Password: lzyVsCy-tD2e3Uumo
    hawkular-apm_1  | ------------------------------------
    
## Running Camel example
The cdi-simple-jetty example is based on:

    https://github.com/fabric8io/ipaas-quickstarts/tree/cc3eb91c365936e40b759d321974329167073bc3/archetypes/cdi-camel-http-client-archetype 

The APM instrumentation config is located in:

    cdi-simple-jetty/src/main/hawt-app/apmconfig/jvm
    
And the APM runtime config, which sets where the APM server is located, is:

    cdi-simple-jetty/src/main/hawt-app/bin/setenv.sh
    
Once it is built, you can run the example by:

    cd cdi-simple-jetty/target/hawt-app/bin
    ./run.sh
    
You can then go to:

    http://localhost:8080/camel/hello?name=bob









