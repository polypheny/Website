---
layout: plain
title: Docker-based data store deployment
---

Polypheny-DB supports a multitude of different underlying data stores (like Cassandra, MonetDB, etc.). Polypheny-Db connects to these databases using data store adapters. While some of these adapters can be deployed directly (embedded) in Polypheny-DB itself, others need to be deployed and configured outside Polypheny-DB and then connected to it (remote).

This process can be somewhat challenging. Polypheny-DB, therefore, offers the ability to deploy and mang some adapters directly from Polypheny-DB using Docker. This massively simplifies the setup of a data store. 

Docker allows the automated setup and execution of preconfigured software packets, so-called containers. These containers are isolated from the host system.

More information about Docker can be found [here](https://www.docker.com/).

## Install Docker
Docker is available for all major operating systems. 

[Docker Desktop (Windows) ](https://www.docker.com/products/docker-desktop)

[Docker Desktop (Mac)](https://hub.docker.com/editions/community/docker-ce-desktop-mac?utm_source=docker&utm_medium=webreferral&utm_campaign=dd-smartbutton&utm_location=header)

[Docker Engine (Linux)](https://hub.docker.com/search?offering=community&operating_system=linux&q=&type=edition)


## Connect Docker with Polypheny-DB
The easiest approach to setup Docker with Polypheny-DB is by using the [docker-remote-api-tls](https://github.com/kekru/docker-remote-api-tls) container. This Container exposes the Docker Remote API. The API is secure and requires clients to authenticate using a TLS client certificat. The required certificate is created by the container on start up. 

Before deploying the connector container, make sure that the `~/.polypheny/certs` folder exists.
{:.note title="Attention"}

### Using Docker Compose
Polypheny-DB comes with a Docker compose file containing an example configuration of this container. The `docker-compose.yml` file can be found in the root directory of Polypheny-DB. 

~~~yml
# file: `docker-compose.yml`
version: "3.4"
services:
    remote-api:
        image: kekru/docker-remote-api-tls:v0.3.0
        restart: unless-stopped
        container_name: polypheny-connector
        ports:
            - 2376:443
        environment:
            - CREATE_CERTS_WITH_PW=supersecret
            - CERT_HOSTNAME=localhost
        volumes:
            - ~/.polypheny/certs/localhost:/data/certs
            - /var/run/docker.sock:/var/run/docker.sock:ro
~~~

*For security reason it is highly recommended changing [supersecret] to something more secure.*

When running docker-compose using `sudo`, make sure to replace `~/.polypheny/certs/localhost` with the absolut path: `/home/[user]/.polypheny/certs/localhost`
{:.note title="Attention"}

Most Docker installations also install [docker-compose](https://docs.docker.com/compose/), which automates a lot of steps when configuring Docker. 
When docker-compose is installed, one can just start the special container by navigating in the folder of the docker-compose.yml file and execute it by running:

~~~
docker-compose up -d
~~~


### Using Docker Run
Instead of using docker-compose, it is also possible to start the container using the following Docker run command:

~~~bash
docker run -d \
    --restart unless-stopped \
    --name polypheny-connector \
    -p 2376:443 \
    -e CREATE_CERTS_WITH_PW=supersecret \
    -e CERT_HOSTNAME=localhost \
    -v ~/.polypheny/certs/localhost:/data/certs \
    -v /var/run/docker.sock:/var/run/docker.sock:ro \
    kekru/docker-remote-api-tls:v0.3.0
~~~

*For security reason it is highly recommended changing [supersecret] to something different before deploying.*

When running Docker using `sudo`, `~/.polypheny/certs/localhost` should be replaced with `/home/[user]/.polypheny/certs/localhost`.
{:.note title="Attention"}


## Validate Connection and Deploy Data Stores
After configuring Docker correctly, one can start Polypheny-DB and navigate to **Config -> Docker**. When the connection has been set up correctly, it will be highlighted green and display **Reachable**. Do not forget to save, after making changes.


## (Optional) Docker on Remote Hosts
To allow for a more flexible deployment setup, Polypheny-DB also allows Docker installations running on other machines. The necessary steps tp connect to a remote docker instance are mostly identical to the local setup.

Before starting the connector container (using compose or the run command) on the remote system, make sure to change the CERT_HOSTNAME to the IP address or hostname of the remote system. After starting the connector container, copy the generated certificates to `~/.polypheny/certs/[ip-of-remote]` on the system Polypheny-DB is running on.

Make sure that port 2376 on the remote system is accessible from the machine Polypheny-DB is running on.
{:.note title="Attention"}

When everything has been set up correctly, the remote can be added in the UI by navigating to **Config** -> **Docker**. To connect to the remote host, add a new instance using the IP address of the machine the remote docker instance is running on.


## Troubleshooting
* **Starting the connector container fails. No certificates in the `~/.polypheny/certs/` folder.**
  
  If there is already a **localhost** or **[ip-of-remote]** folder, try deleting it and run `docker-compose up -d` or execute the Docker run command again. 
  When using a Unix operating system, one can also try to set the access rights to the certs folder:
  ```
  sudo chmod -R 770 .polypheny/certs/
  sudo chown -R ubuntu:docker .polypheny/certs/
  ```
