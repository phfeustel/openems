
# Docker 

## Build
This `Dockerfile` expects a build of `openems-ui` in the `./m` folder.

Execute e.g. `ng build -c "openems,openems-backend-prod,prod` in `../../../ui` or see `/ui/README.md` and copy the result to `./m` via `cp -rf ../../../ui/target/* ./m/`