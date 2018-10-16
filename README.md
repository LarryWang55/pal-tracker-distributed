# pal-tracker-distributed

This is the second codebase.

curl -i -XPOST -H"Content-Type: application/json" localhost:8081/allocations -d"{\"projectId\": 1, \"userId\": 1, \"firstDay\": \"2015-05-17\", \"lastDay\": \"2015-05-18\"}"

curl -i -XPOST -H"Content-Type: application/json" localhost:8082/stories -d"{\"projectId\": 1, \"name\": \"Find some reeds\"}"

curl -i -XPOST -H"Content-Type: application/json" localhost:8084/time-entries/ -d"{\"projectId\": 1, \"userId\": 1, \"date\": \"2015-05-17\", \"hours\": 6}"

cf create-service SERVICE PLAN SERVICE_INSTANCE [-c PARAMETERS_AS_JSON] [-t TAGS]

cf create-service p-service-registry standard tracker-service-registry

cf create-service p-mysql 100mb tracker-allocations-database
cf create-service p-mysql 100mb tracker-backlog-database
cf create-service p-mysql 100mb tracker-registration-database
cf create-service p-mysql 100mb tracker-timesheets-database

cf push APP_NAME [-b BUILDPACK_NAME] [-c COMMAND] [-f MANIFEST_PATH | --no-manifest] [--no-start]
   [-i NUM_INSTANCES] [-k DISK] [-m MEMORY] [-p PATH] [-s STACK] [-t HEALTH_TIMEOUT] [-u (process | port | http)]
   [--no-route | --random-route | --hostname HOST | --no-hostname] [-d DOMAIN] [--route-path ROUTE_PATH] [--var KEY=VALUE]... [--vars-file VARS_FILE_PATH]...

cf push tracker-allocations -p applications/allocations-server/build/libs/allocations-server.jar
cf push tracker-backlog -p applications/backlog-server/build/libs/backlog-server.jar
cf push tracker-registration -p applications/registration-server/build/libs/registration-server.jar
cf push tracker-timesheets -p applications/timesheets-server/build/libs/timesheets-server.jar

cf bind-service APP_NAME SERVICE_INSTANCE [-c PARAMETERS_AS_JSON] [--binding-name BINDING_NAME]

cf bind-service tracker-allocations tracker-allocations-database
cf bind-service tracker-backlog tracker-backlog-database
cf bind-service tracker-registration tracker-registration-database
cf bind-service tracker-timesheets tracker-timesheets-database


cd ~/workspace/assignment-submission
./gradlew cloudNativeDeveloperDistributedSystemDeployment \
    -PregistrationServerUrl=https://tracker-registration.apps.pikes.pal.pivotal.io/ \
    -PbacklogServerUrl=https://tracker-backlog.apps.pikes.pal.pivotal.io/ \
    -PallocationsServerUrl=https://tracker-allocations.apps.pikes.pal.pivotal.io/ \
    -PtimesheetsServerUrl=https://tracker-timesheets.apps.pikes.pal.pivotal.io/

    curl https://spring-cloud-broker.${APPS_DOMAIN}/info
    curl https://spring-cloud-broker.${APPS_DOMAIN}/info

    curl https://spring-cloud-broker.apps.evans.pal.pivotal.io/info | jq

    1.3.3.RELEASE
    org.springframework.cloud:spring-cloud-commons:1.3.3.RELEASE

./gradlew cloudNativeDeveloperDistributedSystemWithServiceDiscovery \
    -PregistrationServerUrl=https://tracker-registration.apps.pikes.pal.pivotal.io/ \
    -PbacklogServerUrl=https://tracker-backlog.apps.pikes.pal.pivotal.io/ \
    -PallocationsServerUrl=https://tracker-allocations.apps.pikes.pal.pivotal.io/ \
    -PtimesheetsServerUrl=https://tracker-timesheets.apps.pikes.pal.pivotal.io/