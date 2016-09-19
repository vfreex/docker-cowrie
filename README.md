#docker-cowrie

This repo contains Dockerfile and Docker compose file that help you
run [Cowrie][] in Docker containers.

[Cowrie][] is a medium interaction SSH and Telnet honeypot designed
to log brute force attacks and the shell interaction performed by the attacker.

## Usage

### Step 1: Install Docker Engine and Docker Compose

Please make sure you have Docker Engine and Docker Compose installed.

If not, see <https://docs.docker.com/engine/installation/>
and <https://docs.docker.com/compose/install/>.

### Step 2: Clone This Repo

``` sh
cd /path/you/like
git clone https://github.com/vfreex/docker-cowrie.git && cd docker-cowrie

```

### Step 3: Prepare Your Cowrie Docker Image

You can either build the Docker image from the Dockerfile in this repo,
or pull the prebuilt image from Docker Hub:

#### Build by Yourself

Just build it using `docker-compose build`.
The Dockerfile is located at `cowrie/Dockerfile`. Edit it if necessary.

``` sh

docker-compose build

```

#### Pull from Docker Hub

If you don't want to build by yourself, just pull my prebuilt image
from Docker Hub. The repo homepage is at <https://hub.docker.com/r/rayson/cowrie/>.

``` sh
docker-compose pull
```

### Step 4: Run

Before starting a Cowrie container, you may want to edit Cowrie's configuration
file. It is `config/cowrie-config/cowrie.cfg` and will be mounted as
a Docker volume when you start the container.

``` sh
# edit config/cowrie-config/conrie.cfg if necessary
# edit docker-compose.yml to change the port number you want to map

# run in the background
docker-compose up -d

# run in the foreground
# docker-compose up
```
To stop and destroy the container that runs in the background:

``` sh
docker-compose down
```

## Inspect Your Cowrie Container

### Display the status of our container

``` bash
# get container's name and port mapping
docker-compose ps
# get container's detailed information
docker inspect `docker-compose ps -q`
```

### Inspect log and data files

[Cowrie]'s `data` and `log` directorires contain all data
that you are insterested in.
They are mounted as Docker named volumes.

Before inspecting files in those directories,
you should figure out the names of those volumes by running `docker volume ls`:

``` bash
$ docker volume ls
DRIVER              VOLUME NAME
local               cowrie_cowrie-log
local               cowrie_cowrie-data
```

Then obtain the pysical path of your desired volume by ruuning
`docker volume inspect <volume_name>`:

``` bash
$ docker volume inspect cowrie_cowrie-log
[
    {
        "Name": "cowrie_cowrie-log",
        "Driver": "local",
        "Mountpoint": "/var/lib/docker/volumes/cowrie_cowrie-log/_data"
    }
]
```

The "Mountpoint" above is the physical path of the volume.
All files you need are just there.

## Cleanup

If you don't want to use the Docker image anymore,
you can delete the Docker image:

``` sh
docker-compose down --rmi all # will not delete your data volumes

# Be careful: delete all the data volumes (the storage for cowrie logs and data) either
# docker-compose down -v --rmi all
```

## Troubleshoot

### Error occurs when executing `docker-compose`:

```
ERROR: In file './docker-compose.yml' service 'version' doesn't have any configuration options. All top level keys in your docker-compose.yml must map to a dictionary of configuration options.
```
_Solution_ 

Upgrade your docker-compose to 1.6.0+:

``` sh
# Make sure you have pip installed. If not, please install pip:
# apt install python-pip # Debian/Ubuntu
# dnf install python-pip # Fedora
# yum install python-pip # RHEL/CentOS with EPEL

$ pip install -U docker-compose
```

[Cowrie]: https://github.com/micheloosterhof/cowrie
