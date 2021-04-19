# Docker 
Polypheny allows to deploy a mutltitude of different underlying databases (like Cassandra, MonetDB, etc.). Those so-called adapters can be either sources, which only allow to query their data by Polypheny or stores, which also allow to manipulate it.

While some of these adapters can be deployed directly (embedded) in Polypheny itself, others need to be started and configured outside of Polypheny and then connected to it (remote).

This process can be somewhat challenging. 
To ease the access to such adapters, Polypheny offers the ability to manage some adapters via Docker automaticly.

Docker is combination of tools, and allows to manage different preconfigured software packets, so-called containers to be deployed automaticly. Those containers are isolated from the deployant system and can communicate in predefined channels with one another and the managing system.

More information to Docker can be found here: [Link to Docker](https://www.docker.com/)

## Install Docker
To activly use Docker, first one needs to install the appropriate Docker for the running system.

These can be found here:

[Docker Desktop (Windows) ](https://www.docker.com/products/docker-desktop)

[Docker Desktop (Mac) ](https://hub.docker.com/editions/community/docker-ce-desktop-mac?utm_source=docker&utm_medium=webreferral&utm_campaign=dd-smartbutton&utm_location=header)

[Docker Desktop (Linux)](https://hub.docker.com/search?offering=community&operating_system=linux&q=&type=edition)

## Connect Docker to Polypheny
After Docker is started and running on the system, it has to be configured to allow Polypheny to control it.
To achieve this, multiple different methods can be used which can be somewhat dependent on the used system.
For clarity, the two easiest methods are described here.

### TLS Container
Docker exposes a predefined port to the running system. Which in most cases is port 2476, but only allows secured connections.
To quickly generate the needed self-signed certificates to achieve that, a container like [docker-remote-api-tls](https://github.com/kekru/docker-remote-api-tls) can be used.

*Before deploying the tls container make sure to create the path ~/.polypheny/certs if it not exists already.*

Polypheny already comes with a example configuration of this container, which lies in a file called `docker-compose.yml`. 

```
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
```
*For security reason it is highly recommended to change [supersecret] to something different before deploying*


Most Docker installations also install [docker-compose](https://docs.docker.com/compose/), which automates a lot of steps when configuring Docker. 
When docker-compose is installed, one can just start the special container by navigating in the folder of the docker-compose.yml file and execute it by running:

```docker-compose up -d```

If docker-docker compose is not installed but only Docker itself, one can achieve the same by executing following command.

```
docker run -d 
    --restart unless-stopped 
    --name polypheny-connector 
    -p 2376:443 
    -e CREATE_CERTS_WITH_PW=supersecret 
    -e CERT_HOSTNAME=localhost 
    -v ~/.polypheny/certs/localhost:/data/certs 
    -v /var/run/docker.sock:/var/run/docker.sock:ro 
    kekru/docker-remote-api-tls:v0.3.0 
```

*For security reason it is highly recommended to change [supersecret] to something different before deploying*


### Insecure Connection Windows (only development)

When using Windows one can also use a different method to allow Polyheny to connect to Docker. This method should only be used for local debuging and disabled after.

Docker allows to enable insecure local connections by enabling them in the settings.
For this one has to open the Docker Desktop settings and check the box **Allow Insecure Connections**.


## Validate Connection and Deploy Adapter in Polypheny

After configuring Docker correctly, one can start Polypheny and navigate to **Config -> Docker**. 

When the Insecure Connection method was used one has to change the Docker instance settings accordingly. For one the use insecure checkbox has to be checked and second the port has to be changed to 2375.

When the connection was setup correctly it will highlight green and display **Reachable**.

Dont forget to save if any changes where made.


## (Optional) Remote Docker Instance
To allow for a more flexible deployment setup, Polypheny also allows to connect to external Docker instances. 
While the steps to achieve this are mostly identical to the local setup, there are some key differences.

### Enable Docker on Remote Host
It is recommended to use the TLS container for this setup.
First, the CERT_HOSTNAME needs to be exchanged with the ip of the remote host.
Then it can be started and the automaticly generated certificates need to be copied to the client and placed in `~/.polypheny/certs/[ip-of-remote]`.

*One has to make sure to allow the port 2376 of the remote to be accessible from extern.*

When everything is setup correctly the remote can be added in Polypheny by naviating to the Config -> Docker. There a new instance can be created and the ip of the remote needs to be entered.
