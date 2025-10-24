# MySQL

Docker Compose for MySQL service.

Environment variables expected (set in your environment or `.env`):

- MYSQL_ROOT_PASSWORD
- MYSQL_DATABASE
- MYSQL_USER
- MYSQL_PASSWORD
- MYSQL_PORT (optional, default 3306)

Start:

docker compose -f mysql/docker-compose.yml up -d
