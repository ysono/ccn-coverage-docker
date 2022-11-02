This repo allows you to run the `ccn-coverage` project in `docker compose`.

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
docker compose run --rm \
  -v "$PWD/mongo-data-init:/mongo-data-init" \
  mongo \
  /mongo-data-init/initialize.sh

docker compose build
```

## Running for dev

```sh
docker compose up -d

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
docker compose \
  -f docker-compose.yaml \
  -f docker-compose.override.release.yaml \
  build

docker compose \
  -f docker-compose.yaml \
  -f docker-compose.override.release.yaml \
  up -d

# The workflow for dev is applicable here too (build, up, logs, down).
# Until you bring down the containers, remember to specify the same yaml files in the same order: `docker compose -f <ditto> -f <ditto> <your_command ...>`.
```

## Troubleshooting

If stuck, try `down`, `build`, then `up`.
1. `docker compose <...> down`
1. `docker ps -a`. This lists all containers (exited or running). You might want to kill some or all of them. `docker rm <name or id of container>`.
1. `docker compose <...> build`
1. `docker compose <...> up -d`
