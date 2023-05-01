# Apache AGE on PostgreSQL
### Source:
https://hub.docker.com/search?q=sorrell%2Fapache-age

### This is an image to build the Apache AGE on the official PostgreSQL 11 Docker image.
```sudo docker pull sorrell/apache-age```

### Running the container:
```sudo docker run --name postgres-docker -e POSTGRES_PASSWORD=postgres -p 5432:5432 -d sorrell/apache-age```

What this does:
- it pulls the "sorrell/apache-age" Docker image from Docker Hub,
- sets the POSTGRES_PASSWORD environment variable value to postgres,
- names (--name) the Docker container to be postgres-docker ,
- maps container’s internal 5432 (right of :) port to external 5432 port, so we’ll be able to enter it from outside,
- and enables to run the Docker container in the background (-d).

In the above command, replace 5432 on the host with a different port if needed (5433:5432).

To access the database in command line inside the container, use:
```sudo docker exec -it postgres-docker bash```
Once inside the container, then run:

```root@imageid:/# psql -U postgres```

### Connect to your containerized Postgres instance using pgAdmin and create a new database (dbgraph1).
### Loading AGE
```
CREATE EXTENSION age;
LOAD 'age';
SET search_path = ag_catalog, "$user", public;
```
### Using AGE
First you will need to create a graph:
```SELECT create_graph('my_graph_name');```

To execute Cypher queries, you will need to wrap them in the following syntax:
```
SELECT * from cypher('my_graph_name', $$
  CypherQuery
$$) as (a agtype);
```
### See more:
https://hub.docker.com/r/sorrell/apache-age

### ***************************************************
# age-viewer:

### Pull apache-age-viewer:
```sudo docker pull sorrell/apache-age-viewer```

### Run apache-age-viewer:
```
sudo docker run \
    --publish=3001:3001 \
    --name=agviewer \
    sorrell/apache-age-viewer
```
### Access the site from a browser: URL:3001
### age-viewer will require a connection to access the database:
- Database Type: Postgres AGE
- Connect URL
- Database Name: dbgraph1
- Graph Path: graph1
- Username:
- Password:

