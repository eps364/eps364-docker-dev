# 📖 Índice da Documentação - EPS364 Docker Environment

Este arquivo serve como índice central para toda a documentação do projeto.

## 📂 Estrutura da Documentação

```
eps364-docker-dev/
├── README.md                    # 📋 Documentação principal
├── .env.example                 # ⚙️  Variáveis de ambiente
├── images/
│   ├── README.md               # 🎨 Documentação dos ícones SVG
│   ├── preview.html            # 👁️  Visualizador de ícones
│   └── *.svg                   # 🖼️  Ícones dos serviços
├── postgres/
│   └── README.md               # 🐘 PostgreSQL 17
├── keycloak/
│   └── README.md               # 🔐 Keycloak IAM
├── mailhog/
│   └── README.md               # 📧 MailHog
├── portainer/
│   └── README.md               # 🐳 Portainer
├── sonar/
│   └── README.md               # 📊 SonarQube
├── grafana/
│   └── README.md               # 📈 Grafana
├── localStack/
│   └── README.md               # ☁️ LocalStack
├── graylog/
│   └── README.md               # 📝 Graylog
└── mockoon/
    └── README.md               # 🎭 Mockoon
```

## 🚀 Links Rápidos

### Principal
- [README Principal](README.md) - Visão geral e configuração inicial
- [Variáveis de Ambiente](.env.example) - Configurações do sistema

### Serviços Docker
- [PostgreSQL](postgres/README.md) - Banco de dados (porta 5432)
- [Keycloak](keycloak/README.md) - Autenticação (porta 8080)  
- [MailHog](mailhog/README.md) - Email testing (portas 8025/1025)
- [Portainer](portainer/README.md) - Docker UI (porta 9443)
- [SonarQube](sonar/README.md) - Code quality (porta 9000)
- [Grafana](grafana/README.md) - Monitoring & Analytics (porta 3002)
- [Graylog](graylog/README.md) - Log Management (porta 9000)
- [Mockoon](mockoon/README.md) - API mock server (porta 3000)

### Recursos Visuais
- [Ícones SVG](images/README.md) - Documentação técnica dos ícones
- [Visualizador](images/preview.html) - Preview dos ícones (abrir no navegador)

## 🔍 Navegação por Categoria

### Por Tipo de Serviço
- **Banco de Dados**: PostgreSQL
- **Segurança**: Keycloak  
- **Comunicação**: MailHog
- **Gerenciamento**: Portainer
- **Qualidade**: SonarQube
- **Monitoramento**: Grafana
- **Logs**: Graylog
- **Mocks**: Mockoon

### Por Nível de Complexidade
- **Básico**: PostgreSQL, MailHog
- **Intermediário**: Portainer, SonarQube, Mockoon  
- **Avançado**: Keycloak

### Por Dependências
- **Independentes**: MailHog, Portainer, Mockoon
- **Com PostgreSQL**: SonarQube, Keycloak
- **Standalone**: PostgreSQL

## 📋 Checklist de Configuração

### Pré-requisitos
- [ ] Docker instalado (v20.10+)
- [ ] Docker Compose instalado (v2.0+)
- [ ] Git instalado
- [ ] 4GB+ RAM disponível
- [ ] 10GB+ espaço em disco

### Configuração Inicial  
- [ ] Repositório clonado
- [ ] Arquivo `.env` criado (copiar de `.env.example`)
- [ ] Variáveis de ambiente ajustadas
- [ ] Portas verificadas (sem conflitos)

### Validação
- [ ] Serviços iniciam sem erro
- [ ] Interfaces web acessíveis  
- [ ] Health checks passando
- [ ] Logs sem erros críticos

## 🆘 Ajuda e Suporte

### Problemas Comuns
1. **Porta em uso**: Verificar com `netstat -tulpn | grep :<porta>`
2. **Container não inicia**: Verificar logs com `docker logs <container>`
3. **Sem espaço em disco**: Limpar com `docker system prune -f`
4. **Permissões**: Verificar se usuário está no grupo docker

### Comandos de Diagnóstico
```bash
# Status geral
docker ps -a
docker compose ps

# Uso de recursos  
docker stats
docker system df

# Limpeza
docker system prune -f
docker volume prune -f
```

### Documentação Adicional
- [Docker Official Docs](https://docs.docker.com/)
- [Docker Compose Reference](https://docs.docker.com/compose/)
- [PostgreSQL Documentation](https://www.postgresql.org/docs/)
- [Keycloak Documentation](https://www.keycloak.org/documentation)

---

**Última atualização**: Outubro 2024  
**Versão**: 1.0  
**Ambiente**: Desenvolvimento Local