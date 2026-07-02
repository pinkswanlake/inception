# Developer Documentation — Inception

## Prerequisites

- VirtualBox installed on host machine
- Debian 12 VM running inside VirtualBox
- Docker installed: `sudo apt-get install -y docker.io`
- Docker Compose installed: `sudo apt-get install -y docker-compose`
- Domain added to `/etc/hosts`: `127.0.0.1 asmafrid.42.fr`

## Project Structure

```
inception/
├── Makefile
├── README.md
├── USER_DOC.md
├── DEV_DOC.md
└── srcs/
    ├── .env
    ├── docker-compose.yml
    └── requirements/
        ├── mariadb/
        │   ├── Dockerfile
        │   ├── conf/my.cnf
        │   └── tools/init.sh
        ├── nginx/
        │   ├── Dockerfile
        │   ├── conf/nginx.conf
        │   └── tools/init.sh
        └── wordpress/
            ├── Dockerfile
            └── tools/init.sh
```

## Configuration Files

- `srcs/.env` — All environment variables and credentials (not committed to git)
- `srcs/docker-compose.yml` — Service definitions, volumes, and network

## Build and Launch

```bash
cd /home/asmafrid/inception
make
```

This will:
1. Create data directories at `/home/asmafrid/data/`
2. Build all three Docker images from their Dockerfiles
3. Start all containers in detached mode

## Useful Commands

```bash
# Start everything
make

# Stop containers (keep volumes)
make down

# Stop and remove volumes
make clean

# Full clean including data directories
make fclean

# Clean rebuild
make re

# Check running containers
docker ps

# View logs
docker logs mariadb
docker logs wordpress
docker logs nginx

# Get shell inside a container
docker exec -it mariadb bash
docker exec -it wordpress bash
docker exec -it nginx bash
```

## Data Persistence

Volume data is stored at:
- MariaDB: `/home/asmafrid/data/mariadb`
- WordPress: `/home/asmafrid/data/wordpress`

These directories persist even when containers are stopped or removed (unless `make fclean` is run).

## Network

All containers communicate via the `inception` bridge network. Container names serve as hostnames:
- WordPress connects to MariaDB at `mariadb:3306`
- NGINX proxies PHP requests to WordPress at `wordpress:9000`
