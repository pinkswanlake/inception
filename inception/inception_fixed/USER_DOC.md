# User Documentation — Inception

## What services are provided?

This stack runs three services:
- **NGINX** — Web server with TLS (HTTPS only, port 443)
- **WordPress + PHP-FPM** — The website and content management system
- **MariaDB** — The database storing all WordPress content

## Start the project

```bash
cd /home/asmafrid/inception
make
```

## Stop the project

```bash
make down
```

## Access the website

Open a browser and go to:
```
https://asmafrid.42.fr
```

## Access the WordPress admin panel

```
https://asmafrid.42.fr/wp-admin
```

Login with:
- Username: `asmafrid42`
- Password: defined in `srcs/.env` as `WP_ADMIN_PASSWORD`

## Credentials

All credentials are stored in `srcs/.env`. This file is not committed to git for security reasons.

| Variable | Purpose |
|---|---|
| MYSQL_ROOT_PASSWORD | MariaDB root password |
| MYSQL_USER / MYSQL_PASSWORD | WordPress DB user |
| WP_ADMIN / WP_ADMIN_PASSWORD | WordPress admin login |
| WP_USER / WP_USER_PASSWORD | WordPress regular user |

## Check services are running

```bash
docker ps
```

All three containers (`nginx`, `wordpress`, `mariadb`) should show status `Up`.

To check logs:
```bash
docker logs nginx
docker logs wordpress
docker logs mariadb
```
