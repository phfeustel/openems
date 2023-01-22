
## Build
Execute the gradle edge build in the root directory via `./gradlew buildEdge`. The resulting fat jar is automatically copied in the right location.

Build the docker image e.g. with `docker build -t phfeustel/openems-edge .`.

## Running
The configuration directory `./config.d` needs to be mounted.
`docker run --name openems-egde --net='host' -v $(pwd)/config.d:/opt/openems-edge/config.d phfeustel/openems-edge:latest`