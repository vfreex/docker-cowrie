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

[Cowrie]: https://github.com/micheloosterhof/cowrie
