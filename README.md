# Repository for configuring compose files for using Docker in the development environment
Not using in the production

## Docker Compose Commands

---

### Start the PostgreSQL Service
<img src="images/postgresql_logo.svg" alt="PostgreSQL Logo" width="200">

To start the PostgreSQL service using the `docker-compose.postgres.yml` file, run the following command:

```bash
docker compose -f 'docker-compose/postgres.yml' up -d --build
```

To power off the PostgreSQL service
```bash
docker compose -f 'docker-compose/postgres.yml' down
```

---

### Start the SonarQube
<img src="images/sonar_logo.png" alt="Sonar Logo" width="200">

To start the SonarQube

```bash
docker compose -f 'docker-compose/sonar.yml' up -d --build
```

To power off the SonarQube

```bash
docker compose -f 'docker-compose/sonar.yml' down
```

Local Access (http://localhost:9000/)
user: admin | passowrd: admin

