This directory contains an example docker-compose setup based on Dockerfiles for the single components.

# Docker Compose Setup
The docker compose can be started via `docker compose up`; see the following pre-requisites in the next paragraph.

## Pre-Requisites
### OpenEMS Edge
Execute the gradle edge build in the root directory via `./gradlew buildEdge`. The resulting fat jar is automatically copied in the right location for the Dockerfile.

### OpenEMS Backend
Execute the gradle backend build in the root directory via `./gradlew buildBackend`. The resulting fat jar is automatically copied in the right location for the Dockerfile.

### OpenEMS UI
Execute e.g. `ng build -c "openems,openems-backend-prod,prod"` in `../../ui` or see `/ui/README.md` and copy the result to `./m`; e.g. via `cp -rf ../../ui/target/* ./openems-ui/m/`

# Road towards a (production-ready) cloud-native deployment
The following areas need discussion and decisions to reach a production-ready setup.

## Architecture in General
- Is the integration Edge<->Backend via [web sockets](https://openems.github.io/openems.io/openems/latest/component-communication/index.html) the right choice?
    - Traffic volume?
    - Connection handling?
    - Recovery on failure?
    - Can we assume that the internet connection on the Edge is stable enough for a permanent websocket connection.
- Which grade of automatisation in build, deployment and operations do we want to achieve?

## Configuration Management
- At the moment the configuration is *synchronized* via a mounted volume. I.e. config changes by the running system are written back -> potential for conflict: 
  - How should the configuration versioning happen? 
  - Which parts of the configuration should be packed into the deployment package /  injected on start-up / modifiable without restart?
- How to handle secrets and their exchange?
- Is there bespoke configuration per customer on the Edge and where is it stored?

## Ownership
- Who is responsible for the operation of the Edge installations?

## Multi-Tenancy
- Should different Edge installations be separated and/or grouped into different backends/InfluxDBs?

### Separation Options
- By AWS account per customer
- Separated Deployments: e.g. DB + backend instance per customer
- Multiple DBs in one instance
- Influx DB with different orgs/buckets
- Request Based / data entry separation

## Build & Deploy
- Where to build? (GitLab?)
- Where to store artifacts? (ECR, GitLab)

## Runtime / Deployment strategy

### Update rollout in general
- How may versions need to kept running in parallel?
    - Are all changes in OpenEMS components backwards compatible; e.g. new Backend but old Edge versions out in the wild
- What's the release strategy and pace for the different components?

### Backend
- Container-based like: 
  - AWS Fargate + manual load balancing etc.
  - AWS App Runner
- AWS Elastic Beanstalk 


### Influx DB
- Managed Service:
  - InfluxDB Cloud (Hosting from influxdata)
  - AWS InfluxDB Cloud (Marketplace)
- Self-hosted in a container
  - Where to store the data and config?

### UI
- Container-based: nginx in AWS Fargate
- AWS S3 + CloudFront
- AWS Amplify

### Edge
- Direct installations on device's OS?
- Containerization strategy?

## Monitoring & Alarming
- Which components need to be monitored? Where to we need metrics?
- What is worth alarming?
- Enable Structured & JSON logging

## Networking
###  Network Separation
- How many sub-segments should exist?
- Which functionality should be exposed?  

### Layering & Security
- Circle-the-wagons setup and/or zero-trust
- Where to terminate encrypted endpoints?
- Which components are integrated via secure connections?

## IAM 
- Which user, rights & roles are needed?
  - Are external end-users managed or only internal ones?
- Where should they be managed? (odoo seems kind of random)