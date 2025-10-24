# Graylog Docker Setup

Graylog is a leading centralized log management solution for capturing, storing, and enabling real-time analysis of terabytes of machine data.

## Quick Start

Start Graylog (includes MongoDB and Elasticsearch):
```bash
docker compose up -d
```

Stop Graylog:
```bash
docker compose down
```

## Access

- **URL**: http://localhost:9000
- **Default Username**: admin
- **Default Password**: admin (configured as SHA2 hash in .env)

⚠️ **Important**: Change the default credentials for production environments!

## Architecture

This setup includes three services:

1. **MongoDB**: Stores Graylog metadata (users, streams, dashboards)
2. **Elasticsearch**: Stores and indexes log messages
3. **Graylog**: Main application server with web interface

## Ports

- `9000`: Graylog web interface and REST API
- `1514`: Syslog TCP/UDP
- `12201`: GELF TCP/UDP (Graylog Extended Log Format)

## Configuration

All configuration is managed through the `.env` file.

### Changing the Root Password

To generate a new password hash:
```bash
echo -n "yourpassword" | sha256sum
```

Then update `GRAYLOG_ROOT_PASSWORD_SHA2` in the `.env` file.

### Password Secret

The `GRAYLOG_PASSWORD_SECRET` must be at least 16 characters. Generate a secure one:
```bash
pwgen -N 1 -s 96
```

## Data Persistence

Data is persisted in Docker volumes:
- `graylog_mongodb_data`: MongoDB data
- `graylog_elasticsearch_data`: Elasticsearch indices
- `graylog_data`: Graylog data and configuration

## Input Configuration

After starting Graylog, you need to configure inputs to receive logs:

1. Go to System → Inputs
2. Select an input type (e.g., GELF UDP, Syslog UDP)
3. Click "Launch new input"
4. Configure and save

## Common Input Types

- **GELF**: Graylog Extended Log Format (recommended)
- **Syslog**: Standard syslog protocol
- **Raw/Plaintext**: Simple text input
- **Beats**: For Filebeat, Metricbeat, etc.

## Example: Sending Logs

### Using GELF with Docker:
```bash
docker run --log-driver=gelf --log-opt gelf-address=udp://localhost:12201 \
  your-image
```

### Using netcat:
```bash
echo '{"version":"1.1","host":"example.com","short_message":"Hello Graylog"}' | \
  nc -u -w1 localhost 12201
```

## Resource Requirements

- **Minimum**: 4GB RAM
- **Recommended**: 8GB+ RAM for production

Elasticsearch is memory-intensive. Adjust `ES_JAVA_OPTS` in docker-compose.yml if needed.

## Troubleshooting

If Graylog doesn't start:
1. Check if all containers are running: `docker compose ps`
2. View logs: `docker compose logs graylog`
3. Ensure ports are not already in use
4. Wait for Elasticsearch to be ready (can take 1-2 minutes)

## Documentation

- [Official Graylog Documentation](https://docs.graylog.org/)
- [Graylog REST API](https://docs.graylog.org/docs/rest-api)
- [Input Types](https://docs.graylog.org/docs/sending-data)
