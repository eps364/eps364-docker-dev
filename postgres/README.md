# PostgreSQL 17 - Development Database

<img src="../images/postgresql_logo.png" alt="PostgreSQL Logo" width="200">

Este serviço fornece uma instância do PostgreSQL 17 para desenvolvimento local com configuração em português brasileiro.

## 🚀 Como Usar

### Iniciar o Serviço

```bash
docker compose -f postgres/docker-compose.yml up -d
```

### Parar o Serviço

```bash
docker compose -f postgres/docker-compose.yml down
```

## 📊 Informações de Conexão

As credenciais padrão (configuráveis no arquivo `.env`):

| Parâmetro | Valor Padrão | Variável de Ambiente |
|-----------|--------------|---------------------|
| Host | localhost | `POSTGRES_HOST` |
| Porta | 5432 | `POSTGRES_PORT` |
| Usuário | postgres | `POSTGRES_USER` |
| Senha | postgres | `POSTGRES_PASSWORD` |
| Database | dev | `POSTGRES_DB` |

## 🔧 Configurações

### Características do Container

- **Imagem**: `postgres:17`
- **Container**: `postgres-17`
- **Encoding**: UTF-8
- **Locale**: pt-br.UTF-8
- **Restart Policy**: always
- **Network**: `postgres-network`

### Volumes

- `postgres_data`: Persistência dos dados do banco (`/var/lib/postgresql/data`)

## 🛠️ Comandos Úteis

```bash
# Conectar ao PostgreSQL via psql
docker exec -it postgres-17 psql -U postgres -d dev

# Ver logs do container
docker logs postgres-17

# Executar backup
docker exec postgres-17 pg_dump -U postgres dev > backup.sql

# Restaurar backup
docker exec -i postgres-17 psql -U postgres -d dev < backup.sql
```

## 🔍 Troubleshooting

### Container não inicia
1. Verifique se a porta 5432 não está sendo usada por outro processo
2. Confirme se o arquivo `.env` está configurado corretamente
3. Verifique os logs: `docker logs postgres-17`

### Conectividade
- Certifique-se de que o container está em execução: `docker ps`
- Teste a conexão: `docker exec postgres-17 pg_isready`

## 📝 Variáveis de Ambiente

Configure no arquivo `.env` na raiz do projeto:

```bash
POSTGRES_USER=postgres
POSTGRES_PASSWORD=postgres
POSTGRES_DB=dev
POSTGRES_HOST=localhost
POSTGRES_PORT=5432
```