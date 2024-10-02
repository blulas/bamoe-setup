# Kogito and Infrastructure services

To allow a quick setup of all services required to run this demo, we provide a docker compose template that starts the following services:

- Postgresql: 5432
- PgAdmin: 8055
- Keycloak: 8480
- BAMOE Canvas: 9090
- BAMOE Management Console: 8280
- BAMOE Task Console: 8380

## Starting the services

Use the `startServices.sh` passing the docker profile you want to use as an argument. If no profile is provided the script will default to `infra`*

Eg:

```shell
sh startServices.sh infra
```

Once the services are started (depending on the profile), the following ports will be assigned on your local machine:

- Postgresql: 5432
- PgAdmin: 8055
- Kogito Management Console: 8280
- Kogito Task Console: 8380
- Keycloak: 8480

## Stopping and removing volume data

To stop all services, simply run:

```shell
docker compose stop
```

or

```shell
docker compose down
```

to stop the services and remove the containers
docker-compose -f docker-compose-postgresql.yml stop

For more details please check the Docker Compose documentation.

```shell
docker compose --help
```
