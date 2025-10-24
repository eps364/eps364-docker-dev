# Apache (httpd)

Simple Apache (httpd) service.

Structure inside `apache/`:

- `www/` (place site static files here)
- `conf/httpd.conf` (optional custom config mounted into container)

Environment variables:

- APACHE_PORT (default 8080)

Start:

docker compose -f apache/docker-compose.yml up -d
