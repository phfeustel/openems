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

# Road towards a (production-ready) cloud-native deployment
The following areas need discussion and decisions

## Architecture in General
- Is the integration Edge<->Backend via [Websockets](https://openems.github.io/openems.io/openems/latest/component-communication/index.html) the right choice?
    - Traffic volume?
    - Connection handling?
    - Recovery on failure?
- Which grade of automatisation in build, deployment and operations do we want to achieve?

## Configuration Management
- At the moment the configuration is *synchronized* (on config changes in the running system it's written back) via a mounted volume: How should the configuration versioning happen? Which parts of the configuration should be backed into the deployment package, injected on start-up, modifiable without restart?
- How to handle secrets and their exchange?

## Ownership
- Who is responsible for the operation of the Edge installations?

## Multi-Tenancy
- Should different Edge installations be separated and/or grouped into different backends/influx DBs

### Separation Options
- AWS account
- Separated Deployments: e.g. DB + backend instance per customer
- Multiple DBs in one instance
- Influx DB Different orgs/buckets
- Request Based / data entry separation

## Build & Depoly
- Where to build? (GitLab?)
- Where to store artifacts? (ECR, GitLab)

## Runtime / Deployment strategy

### Update rollout in general
- How may versions need to kept running in parallel?
    - Are all changes in OpenEMS components backwards compatible (e.g. new Backend but old Edge versions out there)

### Backend
- Container-based like: AWS Fargate 
- AWS App Runner

### UI
- Container-based: Nginx in AWS Fargate
- S3 + CloudFront
- Amplify

### Edge
- Direkt installations on devices
- Containerization strategy?

## Monitoring & Alarming
- Which components need to be monitored / tracked?
- What is worth alarming?
- Structured & JSON logging

## Networking
###  Network Separation
- How many sub-segments should exist
- Which functionality should be exposed  

### Layering & Security
- Circle-the-wagons setup and/or zero-trust
- Where to terminate encrypted endpoints?

## IAM 
- Which user, rights & roles are needed?
  - Are external end-users managed or only internal ones?
- Where should they be managed? (odoo seems kind of random)