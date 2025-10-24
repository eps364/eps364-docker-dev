# Grafana Docker Setup

Grafana is an open-source analytics and monitoring platform that allows you to query, visualize, alert on, and understand your metrics.

## Quick Start

Start Grafana:
```bash
docker compose up -d
```

Stop Grafana:
```bash
docker compose down
```

## Access

- **URL**: http://localhost:3002
- **Default Username**: admin
- **Default Password**: admin123 (configured in .env)

⚠️ **Note**: Port 3000 is typically used by VS Code extensions. This setup uses port 3002.

⚠️ **Important**: Change the default password for production environments!

## Configuration

All configuration is managed through the `.env` file:

- `GRAFANA_PORT`: Port to expose Grafana (default: 3002)
- `GRAFANA_ADMIN_USER`: Admin username (default: admin)
- `GRAFANA_ADMIN_PASSWORD`: Admin password (default: admin123)
- `GRAFANA_INSTALL_PLUGINS`: Comma-separated list of plugins to install

## Data Persistence

Data is persisted in Docker volumes:
- `grafana_data`: Stores dashboards, users, and other Grafana data
- `grafana_config`: Stores configuration files

## Common Datasources

Grafana supports many datasources including:
- Prometheus
- InfluxDB
- PostgreSQL
- MySQL
- Elasticsearch
- And many more...

## Example Use Cases

- Application monitoring
- Infrastructure metrics
- Business analytics
- Log aggregation visualization
- IoT data visualization

## Documentation

- [Official Grafana Documentation](https://grafana.com/docs/grafana/latest/)
- [Grafana Plugins](https://grafana.com/grafana/plugins/)
