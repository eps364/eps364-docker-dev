# Portainer

O Portainer é uma interface de gerenciamento leve que permite gerenciar facilmente seus diferentes ambientes Docker (hosts Docker ou clusters Swarm).

## Como Usar

### 1. Iniciar o Serviço

Para iniciar o contêiner do Portainer, execute o seguinte comando a partir da raiz do projeto:

```bash
docker compose -f 'portainer/docker-compose.yml' up -d
```

### 2. Configuração Inicial

1.  Abra seu navegador web e navegue até **https://localhost:9443**.
2.  Você provavelmente verá um aviso do navegador sobre um certificado auto-assinado. Isso é esperado. Prossiga para o site (por exemplo, no Chrome, clique em "Avançado" e depois em "Prosseguir para localhost (não seguro)").
3.  Na primeira tela, você será solicitado a criar um usuário administrador. Escolha um nome de usuário e uma senha forte.
4.  Clique em "Criar usuário".

### 3. Conectar ao Seu Ambiente Docker

1.  Após criar o usuário, você será solicitado a conectar o Portainer a um ambiente Docker.
2.  Selecione a opção **Docker** e clique em **Conectar**. O Portainer se conectará automaticamente ao ambiente Docker local através do socket Docker (`/var/run/docker.sock`) que foi montado como volume.
3.  Você será então redirecionado para o painel, onde poderá ver e gerenciar todos os seus contêineres em execução, imagens, volumes e redes.

### 4. Parar o Serviço

Para parar o contêiner do Portainer, execute o seguinte comando:

```bash
docker compose -f 'portainer/docker-compose.yml' down
```
