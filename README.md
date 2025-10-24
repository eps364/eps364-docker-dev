# EPS364 Docker Development Environment

Este repositório contém configurações Docker Compose para ferramentas de desenvolvimento. **NÃO UTILIZAR EM PRODUÇÃO**.

## 🚀 Configuração Inicial

Primeiro, copie o arquivo de exemplo das variáveis de ambiente para criar o seu próprio:

```bash
cp .env.example .env
```

Personalize as variáveis dentro do arquivo `.env` conforme necessário.

## 📁 Estrutura do Projeto

Este repositório está organizado com serviços independentes, cada um em sua própria pasta:

| Pasta | Serviço | Descrição | Porta |
|-------|---------|-----------|-------|
| `postgres/` | PostgreSQL 17 | Banco de dados relacional | 5432 |
| `sonar/` | SonarQube Community | Análise de qualidade de código | 9000 |
| `mailhog/` | MailHog | Interceptador de emails para testes | 8025 (Web UI), 1025 (SMTP) |
| `portainer/` | Portainer | Interface de gerenciamento Docker | 9443 |

## 🏃‍♂️ Como Usar

Cada pasta contém seu próprio `README.md` com instruções específicas do serviço. Para executar qualquer serviço:

```bash
# Padrão geral
docker compose -f '<pasta>/docker-compose.yml' up -d
```

### Links Rápidos
- **PostgreSQL**: [postgres/README.md](postgres/README.md)
- **SonarQube**: [sonar/README.md](sonar/README.md) - http://localhost:9000
- **MailHog**: [mailhog/README.md](mailhog/README.md) - http://localhost:8025
- **Portainer**: [portainer/README.md](portainer/README.md) - https://localhost:9443

## 🛠️ Comandos Úteis

```bash
# Ver todos os contêineres em execução
docker ps

# Ver logs de um contêiner específico
docker logs <container-name>

# Parar todos os serviços
docker compose down

# Limpar volumes não utilizados
docker volume prune
```

## 📋 Pré-requisitos

- Docker
- Docker Compose
- Arquivo `.env` configurado (copie de `.env.example`)