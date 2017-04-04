# Performance testing

How to create the Example App docker image:
Make sure that in the console you run SBT from, the Docker env variables are set 
If not, set them (for non-native Docker VM, use the `docker-machine env` output)
  
Create a docker image using SBT:
    
    cd services
    sbt example/docker:publishLocal
        
The previous command creates a `pulse/example:0.1-SNAPSHOT` Docker image, which will be used in docker-compose


How to run the stack using the docker-compose:

    cd service
    docker-compose up --force-recreate -d
    cd gatling-load-1
    sbt gatling:testOnly

Dashboard with metrics vizualization (credentials: `admin/admin`):

    http://<DOCKER_HOST>/dashboard/file/dashboard.json
    
Note:
Currently `src/test/resources/gatling.conf` contains the hardcoded Graphite host address.
You need to check if the hardcoded value fits your environment setup, in order to get Gatling metrics collected.

Docker stack is inspired by and mosntly copies this article:
http://mintbeans.com/jvm-monitoring-docker/

The article can be used for the reference.
