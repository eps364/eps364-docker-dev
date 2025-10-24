# WordPress

Docker Compose for a local WordPress development stack (includes MySQL and Redis services to keep the compose self-contained).

Environment variables expected (set in your environment or `.env`):

- WORDPRESS_DB_NAME
- WORDPRESS_DB_USER (optional, defaults to `wordpress`)
- WORDPRESS_DB_PASSWORD
- MYSQL_ROOT_PASSWORD
- WORDPRESS_PORT (optional, default 8000)

Note: For using Redis caching with WordPress you need a Redis plugin in WordPress to use `REDIS_HOST`.

Start:

docker compose -f wordpress/docker-compose.yml up -d
