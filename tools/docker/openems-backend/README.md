# Backend Docker

Container provides an OpenEMS Backend

## Running
The configuration directory `./config.d` needs to be mounted.
`docker run --name openems-backend --net='host' -v $(pwd)/config.d:/opt/openems-backend/config.d phfeustel/openems-backend:latest`

## Usage
Apache Felix Web Console configuration: http://localhost:8079/system/console/configMgr
