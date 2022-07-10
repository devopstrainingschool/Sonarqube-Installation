# sonarqube-installation
## Install docker engine
https://github.com/devopstrainingschool/docker-installation

## Install docker-compose
https://github.com/devopstrainingschool/Docker-compose-installation/blob/master/README.md

## Create a docker-compose.yaml file 
```
touch docker-compose.yaml
```
## vim inside the file
```
vi docker-compose.yaml
```
## Click on i , paste and save this content

```

version: "3"

services:
  sonarqube:
    image: sonarqube:community
    depends_on:
      - db
    environment:
      SONAR_JDBC_URL: jdbc:postgresql://db:5432/sonar
      SONAR_JDBC_USERNAME: sonar
      SONAR_JDBC_PASSWORD: sonar
    volumes:
      - sonarqube_data:/opt/sonarqube/data
      - sonarqube_extensions:/opt/sonarqube/extensions
      - sonarqube_logs:/opt/sonarqube/logs
    ports:
      - "9000:9000"
  db:
    image: postgres:12
    environment:
      POSTGRES_USER: sonar
      POSTGRES_PASSWORD: sonar
    volumes:
      - postgresql:/var/lib/postgresql
      - postgresql_data:/var/lib/postgresql/data

volumes:
  sonarqube_data:
  sonarqube_extensions:
  sonarqube_logs:
  postgresql:
  postgresql_data:
  ```
  ## run this command:
  ```
  sysctl -w vm.max_map_count=262144
  ```
## Finally run 
```
docker-compose up -d
```
## sonarqube is accessible on port 9000
### http://ipaddress:9000
