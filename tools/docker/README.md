This directory contains example Dockerfiles

# Docker Compose Setup
Additionally, an example setup via docker compose can be started via `docker compose up`

## Pre-Requisites
### OpenEMS Edge
Execute the gradle edge build in the root directory via `./gradlew buildEdge`. The resulting fat jar is automatically copied in the right location.

### OpenEMS Backend
Execute the gradle backend build in the root directory via `./gradlew buildBackend`. The resulting fat jar is automatically copied in the right location.

### OpenEMS UI
Execute e.g. `ng build -c "openems,openems-backend-prod,prod` in `../../ui` or see `/ui/README.md` and copy the result to `./m` via `cp -rf ../../ui/target/* ./openems-ui/m/`