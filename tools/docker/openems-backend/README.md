# Backend Docker

Container provides an OpenEMS Backend

## Build
Execute the gradle backend build in the root directory via `./gradlew buildBackend`. The resulting fat jar is automatically copied in the right location.

Build the docker image e.g. with `docker build -t phfeustel/openems-backend .`.

## Running
The configuration directory `./config.d` needs to be mounted.
`docker run --name openems-backend --net='host' -v $(pwd)/config.d:/opt/openems-backend/config.d phfeustel/openems-backend:latest`

## Usage
Apache Felix Web Console configuration: http://localhost:8079/system/console/configMgr
