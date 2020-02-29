# keycloak-postgres-docker-ubuntu

## Start keycloak with Postgres ##

## Create a user defined network
```
docker network create keycloak-network
```
## Run postgres using the above network and local host volume
```
docker run -d --name postgres --net keycloak-network -v path/to/local/host/volume:/var/lib/postgresql/data -e POSTGRES_DB=keycloak -e POSTGRES_USER=keycloak -e POSTGRES_PASSWORD=password postgres
```
## Start keycloak using the created network and bind it to postgres
```
docker run -p 8080:8080 --name keycloak --net keycloak-network -e DB_VENDOR=POSTGRES -e DB_ADDR=postgres -e DB_DATABASE=keycloak -e DB_USER=keycloak -e DB_PASSWORD=password -e KEYCLOAK_USER=admin -e KEYCLOAK_PASSWORD=admin jboss/keycloak
```

## access URL ##
```
http://127.0.0.1:8080/auth
```
