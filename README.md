#docker-cowrie

Dockerfile and docker-compose file to run [Cowrie][] in Docker.
[Cowrie][] is a medium interaction SSH and Telnet honeypot designed to log brute force attacks and the shell interaction performed by the attacker.

## Usage

Suppose you have Docker Engine and Docker Compose installed.
If not, see <https://docs.docker.com/engine/installation/> and <https://docs.docker.com/compose/install/>.

``` bash
# clone this repo
git clone https://github.com/vfreex/docker-cowrie.git
cd docker-cowrie

# edit config/cowrie-config/conrie.cfg if necessary
# edit docker-compose.yml to change the port number you want to map

# run (suppose you have Docker installed)
docker-compose up
# run in the backgroud
# docker-compose up -d
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

[Cowrie]'s `data` and `log` directorires are mounted as Docker volumes.

Before inspecting files in those directories,
you should get the names of those volumes by running `docker volume ls`:

``` bash
$ docker volume ls
DRIVER              VOLUME NAME
local               cowrie_cowrie-log
local               cowrie_cowrie-data
```

Then obtain the path of desired volume by `docker volume inspect <volume_name>`:

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

The "Mountpoint" above is the physical path of the volume. All files you need are there.


[Cowrie]: https://github.com/micheloosterhof/cowrie
