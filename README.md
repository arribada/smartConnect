TODO
 - auto generate ssl .keystore file.
 - don't expose db username and pass in the tomcat logs
 - server.war is too big to be kept in github so maybe build it from source. github has a limit of 100mb for a single file, but if build from source it will be broken into many small files.


Install docker:
https://docs.docker.com/install/


Create postgres user and pass files in 
```
.local/postgres_user
.local/postgres_pass
```

To be able to deploy services using `docker stack deploy` and avoid installing docker compose need to enable swarm mode. 
This also allows rolling updates.
```
docker swarm init
```
Deploy the application.
> This will take a while the first time as it needs to download all images.
```
docker stack deploy -c docker-compose.yml smart
```

Check the status.
> Once the `Replicas` column shows `1/1` the application has been deployed.
```
docker stack services smart
```

Access smart connect at 
```
https://localhost:8443/server/connect/home
```

To check the application logs
```
docker service logs -f smart_tomcat
docker service logs -f smart_postgres
```