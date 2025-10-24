# Portainer CE - Docker Management Interface

![Portainer](../images/portainer.svg)

Portainer é uma interface de gerenciamento leve que permite gerenciar facilmente ambientes Docker, containers, imagens, volumes e redes através de uma interface web intuitiva.

## 🚀 Como Usar

### Iniciar o Serviço

```bash
docker compose -f portainer/docker-compose.yml up -d
```

### Parar o Serviço

```bash
docker compose -f portainer/docker-compose.yml down
```

## 🌐 Acesso à Interface Web

- **URL**: https://localhost:9443
- **Protocolo**: HTTPS (com certificado auto-assinado)

> **Nota**: Você verá um aviso sobre certificado não confiável - isso é normal para desenvolvimento local.

## 🛠️ Configuração Inicial

### 1. Primeiro Acesso
1. Navegue até https://localhost:9443
2. Aceite o certificado auto-assinado no navegador
3. Crie um usuário administrador:
   - **Username**: admin (ou outro de sua escolha)
   - **Password**: Use uma senha forte
4. Clique em "Create user"

### 2. Conectar ao Docker Local
1. Selecione **"Get Started"**
2. O Portainer detectará automaticamente o ambiente Docker local
3. Será redirecionado para o dashboard principal

## 🏗️ Características do Container

- **Imagem**: `portainer/portainer-ce:latest`
- **Container**: `portainer`
- **Porta**: 9443 (HTTPS)
- **Restart Policy**: always
- **SSL**: Habilitado por padrão

## 💾 Volumes Persistentes

| Volume | Descrição | Path no Container |
|--------|-----------|-------------------|
| `portainer_data` | Dados do Portainer (usuários, configurações) | `/data` |
| Docker Socket | Acesso ao Docker daemon | `/var/run/docker.sock` |

## 🎯 Funcionalidades Principais

### Dashboard
- ✅ Visão geral de containers, imagens, volumes e redes
- ✅ Estatísticas de uso de recursos
- ✅ Status dos serviços Docker

### Gerenciamento de Containers
- ✅ Listar, iniciar, parar e remover containers
- ✅ Visualizar logs em tempo real
- ✅ Executar comandos dentro de containers
- ✅ Monitorar estatísticas de performance

### Gerenciamento de Imagens
- ✅ Listar imagens locais
- ✅ Pull/Push de imagens de registries
- ✅ Build de imagens via Dockerfile
- ✅ Remover imagens não utilizadas

### Docker Compose
- ✅ Implantar stacks via Docker Compose
- ✅ Editar e atualizar stacks existentes
- ✅ Gerenciar variáveis de ambiente

### Usuários e Acesso
- ✅ Gerenciamento de usuários (CE limitado)
- ✅ Controle de acesso baseado em roles
- ✅ Autenticação local

## 📊 Interface Web - Seções Principais

| Seção | Descrição |
|-------|-----------|
| **Home** | Dashboard com overview geral |
| **App Templates** | Templates prontos para aplicações |
| **Stacks** | Gerenciamento de Docker Compose |
| **Containers** | Lista e gerenciamento de containers |
| **Images** | Gerenciamento de imagens Docker |
| **Networks** | Configuração de redes Docker |
| **Volumes** | Gerenciamento de volumes |
| **Events** | Log de eventos do Docker |
| **Host** | Informações do sistema host |
| **Users** | Gerenciamento de usuários |

## 🛠️ Comandos Úteis

```bash
# Ver logs do Portainer
docker logs portainer

# Acessar container do Portainer
docker exec -it portainer sh

# Backup dos dados do Portainer
docker run --rm -v portainer_portainer_data:/data -v $(pwd):/backup alpine tar czf /backup/portainer_backup.tar.gz -C /data .

# Restaurar backup
docker run --rm -v portainer_portainer_data:/data -v $(pwd):/backup alpine tar xzf /backup/portainer_backup.tar.gz -C /data
```

## 🔐 Segurança

### Certificado SSL
- Portainer gera automaticamente certificados auto-assinados
- Para produção, configure certificados válidos
- Localização: `/data/portainer.crt` e `/data/portainer.key`

### Acesso Restrito
- Configure firewall para restringir acesso à porta 9443
- Use senhas fortes para usuários administrativos
- Considere usar autenticação externa (LDAP/OAuth)

## 🔍 Troubleshooting

### Container não inicia
- Verifique se a porta 9443 está disponível
- Confirme permissões do Docker socket
- Veja os logs: `docker logs portainer`

### Erro de conexão Docker
- Verifique se o Docker daemon está executando
- Confirme se o volume do socket está montado corretamente
- Tente reiniciar o container: `docker restart portainer`

### Problema com certificado SSL
- Limpe dados do navegador para localhost:9443
- Reinicie o container para regenerar certificados
- Use modo incógnito para teste

### Esqueceu a senha
```bash
# Resetar senha do admin
docker exec -it portainer /portainer --admin-password='novaSenha123'
```

## 📋 Limitações da Versão CE

- **Usuários**: Limitado a poucos usuários
- **Environments**: Um ambiente Docker por instância
- **RBAC**: Controle de acesso básico
- **Support**: Comunidade apenas

Para recursos avançados, considere o Portainer Business Edition.
