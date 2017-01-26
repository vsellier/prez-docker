# Test like acceptance

## PLF configuration

* Uncompress a plf binary on the ``plf`` directory
* Configure the plf instance
** Install the postgresql jdbc driver
```
# cd plf
# ./addon install --unstable exo-jdbc-driver-postgresql
```
** Configure the tomcat datasources
*** Edit the ``conf/server.xml`` file
*** Set the datasources properties to :
```
username="plf" password="plf" driverClassName="org.postgresql.Driver" url="jdbc:postgresql://db:5432/plf"
```

The username, password, and url match the values declare on the ``docker-compose.yml`` file

```
  postgresql:
    image: postgres:9.4
    volumes:
      - $PWD/data/postgresql:/var/lib/postgresql/data
    environment:
      - POSTGRES_USER=plf  # <-- user name to use
      - POSTGRES_PASSWORD=plf  # <-- password to use
...
  plf:
...
    ports:
      - 8080:8080  # <-- plf will be accessible on localhost:8080
    links:
      - postgresql:db  # <container name>:<visible name inside the container>
      - mongo:mongo
      - elasticsearch:elasticsearch

```

*** Copy this content to the plf/gatein/conf/exo.properties
```
chat.dbServerHost=mongo
chat.dbServerPort=27017
exo.es.embedded.enabled=false
exo.es.search.server.url=http://elasticsearch:9200
exo.es.index.server.url=http://elasticsearch:9200
```

## PLF startup

```
# docker-compose up
```

It starts 4 container ``elasticsearch``, ``mongo``, ``postgresql`` and ``plf``. The binaries are read from the ``plf`` directory
The containers data is wrote on the ``data`` directory. It configured via the ``volumes`` sections on the dockerfile.

