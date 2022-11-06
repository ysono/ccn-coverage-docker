This repo enables you to run the `ccn-coverage` project in docker.

## Prerequisites

You have checked out `ccn-coverage`-related git repos as follows:

```
foo/
├── ccn-coverage-api/
├── ccn-coverage-vis/
├── ccn-coverage-docker/ (this repo)
```

All commands below must be executed while you have `cd`'d to this directory.

## Setting up for the first time

```sh
# Dump the test mongo data.
docker compose run --rm \
  -v "${PWD}/../mongo-data-mock:/mongo-data-mock" \
  mongo \
  /mongo-data-mock/initialize.sh
```

## Running for development

```sh
docker compose up --build -d

# Follow logs in order to infer when the containers are ready. (Docker cannot inform application logic readiness.)
docker compose logs -f api
docker compose logs -f vis

# Open the app on your browser at this address.
curl localhost:8000

# When done
docker compose down
```

## Running the "release" versions of containers

```sh
docker compose -f docker-compose.yaml -f docker-compose.override.release.yaml \
  up --build -d

# The workflow for dev is applicable here too (up, logs, down).
# Until you bring down the containers, remember to specify the same yaml files in the same order.
```

## Troubleshooting

If stuck, try `down` then `up`.
1. `docker compose [...] down`
1. `docker ps -a`. This lists all containers (exited or running). You might want to kill some or all of them. `docker rm <name or id of container>`.
1. `docker compose [...] up --build -d`
