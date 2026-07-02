*This project has been created as part of the 42 curriculum by asmafrid.*

## Description

Inception is a system administration project that uses Docker to set up a small infrastructure of services inside a virtual machine. The project deploys a WordPress website served by NGINX with TLS, backed by a MariaDB database, all running in separate Docker containers orchestrated with Docker Compose.

## Project Description

### Design Choices

**Virtual Machines vs Docker**
A Virtual Machine emulates an entire operating system, requiring significant resources. Docker containers share the host OS kernel, making them lighter and faster to start. In this project, Docker runs *inside* a VM as required by the subject.

**Secrets vs Environment Variables**
Environment variables (via `.env` file) are used to store credentials. The `.env` file is gitignored to prevent credentials from being exposed in the repository.

**Docker Network vs Host Network**
A custom bridge network (`inception`) is used instead of the host network. This isolates containers from the host and allows them to communicate using container names as hostnames (e.g., `mariadb:3306`, `wordpress:9000`).

**Docker Volumes vs Bind Mounts**
Named volumes with local driver are used to persist data for MariaDB and WordPress. Data is stored at `/home/asmafrid/data/` on the host machine.

## Instructions

### Prerequisites
- VirtualBox with Debian 12 VM
- Docker and Docker Compose installed in the VM
- `asmafrid.42.fr` added to `/etc/hosts` pointing to `127.0.0.1`

### Run the project
```bash
make
```

### Stop the project
```bash
make down
```

### Full clean rebuild
```bash
make re
```

## Resources

- [Docker Documentation](https://docs.docker.com)
- [NGINX Documentation](https://nginx.org/en/docs/)
- [WordPress CLI](https://wp-cli.org/)
- [MariaDB Documentation](https://mariadb.com/kb/en/)
- [PHP-FPM Configuration](https://www.php.net/manual/en/install.fpm.configuration.php)

**AI Usage:** Claude (claude.ai) was used to assist with debugging Docker networking issues, PHP-FPM configuration, and entrypoint script logic. All generated code was tested, understood, and verified before use.
