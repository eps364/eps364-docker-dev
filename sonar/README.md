# SonarQube Community - Code Quality Analysis

<img src="../images/sonar_logo.png" alt="SonarQube Logo" width="200">

Este serviço fornece uma instância do SonarQube Community Edition para análise de qualidade de código, incluindo um banco PostgreSQL dedicado.

## 🚀 Como Usar

### Iniciar o Serviço

```bash
docker compose -f sonar/docker-compose.yml up -d
```

### Parar o Serviço

```bash
docker compose -f sonar/docker-compose.yml down
```

## 🌐 Acesso à Interface Web

- **URL**: http://localhost:9000
- **Usuário padrão**: admin
- **Senha padrão**: admin

> **Importante**: Altere a senha padrão no primeiro acesso!

## 🏗️ Arquitetura do Serviço

### SonarQube Container
- **Imagem**: `sonarqube:8.8-community`
- **Porta**: 9000
- **Dependência**: Banco PostgreSQL interno

### PostgreSQL Container (Interno)
- **Imagem**: `postgres:13`
- **Usuário**: sonar
- **Senha**: sonar
- **Database**: sonarqube

## 💾 Volumes Persistentes

| Volume | Descrição | Path no Container |
|--------|-----------|-------------------|
| `sonarqube_data` | Dados do SonarQube | `/opt/sonarqube/data` |
| `sonarqube_conf` | Configurações | `/opt/sonarqube/conf` |
| `sonarqube_extensions` | Plugins e extensões | `/opt/sonarqube/extensions` |
| `postgres_data` | Dados do PostgreSQL | `/var/lib/postgresql/data` |

## 🔧 Configuração Inicial

### 1. Primeiro Acesso
1. Acesse http://localhost:9000
2. Faça login com `admin/admin`
3. Altere a senha quando solicitado

### 2. Criar um Projeto
1. Clique em "Create Project"
2. Escolha "Manually"
3. Configure o nome e key do projeto
4. Gere um token de acesso

### 3. Analisar Código
```bash
# Exemplo com Maven
mvn sonar:sonar \
  -Dsonar.projectKey=meu-projeto \
  -Dsonar.host.url=http://localhost:9000 \
  -Dsonar.login=<seu-token>

# Exemplo com SonarScanner CLI
sonar-scanner \
  -Dsonar.projectKey=meu-projeto \
  -Dsonar.sources=. \
  -Dsonar.host.url=http://localhost:9000 \
  -Dsonar.login=<seu-token>
```

## 📊 Recursos do SonarQube Community

- ✅ Análise de bugs, vulnerabilidades e code smells
- ✅ Métricas de cobertura de código
- ✅ Análise de duplicação de código
- ✅ Suporte para 25+ linguagens
- ✅ Interface web intuitiva
- ❌ Análise de branches (apenas Edition paga)
- ❌ Pull Request decoration (apenas Edition paga)

## 🛠️ Comandos Úteis

```bash
# Ver logs do SonarQube
docker logs sonar-sonarqube-1

# Ver logs do PostgreSQL
docker logs sonar-db-1

# Acessar container do SonarQube
docker exec -it sonar-sonarqube-1 bash

# Backup do banco de dados
docker exec sonar-db-1 pg_dump -U sonar sonarqube > sonarqube_backup.sql
```

## 🔍 Troubleshooting

### Container não inicia
- Verifique se há memória suficiente (mín. 2GB recomendado)
- Confirme se a porta 9000 está disponível
- Aguarde alguns minutos - o SonarQube demora para inicializar

### Problemas de Performance
- Aumente a memória disponível no Docker
- Configure `vm.max_map_count` no host: `sudo sysctl -w vm.max_map_count=524288`

### Erro de Conexão com Banco
- Verifique se o container do PostgreSQL está em execução
- Confirme os logs: `docker logs sonar-db-1`

## 🌍 Linguagens Suportadas

Java, JavaScript/TypeScript, C#, Python, PHP, Go, Kotlin, Ruby, Scala, Swift, Objective-C, C/C++, XML, HTML, CSS, YAML, Docker, Terraform, CloudFormation, e mais.