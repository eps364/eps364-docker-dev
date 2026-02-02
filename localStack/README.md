# LocalStack - AWS Cloud Stack

![LocalStack](../images/localstack.svg)

O LocalStack fornece um ambiente de nuvem totalmente funcional que roda em uma única máquina. Ele permite desenvolver e testar aplicações de nuvem (AWS) sem a necessidade de se conectar a um provedor de nuvem real.

## 🚀 Como Usar

### Iniciar o Serviço

```bash
docker compose -f localStack/docker-compose.yml up -d
```

### Parar o Serviço

```bash
docker compose -f localStack/docker-compose.yml down
```

## ☁️ Acesso e Interação

### Versão Gratuita (Padrão)
A versão gratuita do LocalStack **não possui uma interface web local** para visualização de recursos. A interação é feita via linha de comando ou SDKs.

- **Endpoint URL**: `http://localhost:4566`

> **Nota**: Todas as chamadas da AWS CLI ou SDK devem ser direcionadas para este endpoint.

### Interface Web (Recurso Pago)
O LocalStack Pro oferece uma interface web em `https://app.localstack.cloud` que se conecta à sua instância local. Para ativá-la:
1. Obtenha uma **API Key** em uma conta paga do LocalStack.
2. Adicione a chave à variável `LOCALSTACK_API_KEY` no seu arquivo `.env`.
3. Inicie o contêiner. Sua instância local aparecerá no dashboard web.


### Exemplo de Comando com AWS CLI

Para listar os buckets S3 (após configurar a AWS CLI):
```bash
aws --endpoint-url=http://localhost:4566 s3 ls
```

Para criar uma fila SQS:
```bash
aws --endpoint-url=http://localhost:4566 sqs create-queue --queue-name minha-fila-local
```

## 🏗️ Características do Container

- **Imagem**: `localstack/localstack`
- **Container**: `${LOCALSTACK_DOCKER_NAME}` (ex: `localstack-main`)
- **Porta Gateway**: `4566`
- **Portas de Serviços**: `4510-4559`
- **Restart Policy**: `unless-stopped` (implícito no `up -d`)

## 💾 Volumes Persistentes

| Volume | Descrição | Path no Container |
|--------|-----------|-------------------|
| `${LOCALSTACK_VOLUME_DIR}` | Armazena o estado dos serviços da AWS (arquivos S3, itens DynamoDB, etc.) | `/var/lib/localstack` |
| Docker Socket | Permite ao LocalStack criar outros contêineres (ex: para Lambdas) | `/var/run/docker.sock` |

## ⚙️ Configuração via `.env`

As seguintes variáveis no arquivo `.env` controlam o serviço LocalStack:

| Variável | Descrição | Padrão |
|-------------------------|---------------------------------------------------------------------------------|-------------------|
| `LOCALSTACK_DOCKER_NAME`| Nome do contêiner Docker. | `localstack-main` |
| `LOCALSTACK_VOLUME_DIR` | Diretório no host para persistir os dados do LocalStack. | `./localstack/volume` |
| `LOCALSTACK_SERVICES` | Lista de serviços AWS a serem ativados, separados por vírgula. **Importante para performance!** | `s3,sqs,dynamodb,lambda` |
| `LOCALSTACK_API_KEY` | Chave de API para ativar recursos pagos (como a Web UI). | (vazio) |
| `DEBUG` | Ativa logs detalhados para depuração (1 para ativar). | `0` |

### Otimizando com `SERVICES`
Para economizar recursos (CPU/memória), é altamente recomendável especificar apenas os serviços que você precisa na variável `LOCALSTACK_SERVICES`.

**Exemplo de configuração no `.env`:**
```env
LOCALSTACK_SERVICES=s3,sqs,dynamodb,lambda,iam
```

## 🎯 Funcionalidades Principais

- **Emulação de Serviços AWS**: Simula dezenas de serviços, como S3, Lambda, SQS, DynamoDB, IAM, e mais.
- **Desenvolvimento Offline**: Permite que equipes desenvolvam e testem aplicações de nuvem sem acesso à internet ou custos de nuvem.
- **Testes de Integração**: Facilita a execução de testes automatizados em um ambiente consistente e descartável.
- **Depuração Rápida**: Ciclos de feedback mais rápidos, pois tudo roda localmente.

## 🛠️ Comandos Úteis

```bash
# Ver logs do LocalStack
docker logs localstack-main

# Acessar o container
docker exec -it localstack-main bash

# Verificar o status dos serviços (dentro do container)
localstack status services
```

## 🔍 Troubleshooting

### Container não inicia ou serviços não respondem
- **Verifique a variável `SERVICES`**: Uma configuração incorreta ou um serviço com erro pode impedir a inicialização. Tente começar com um serviço simples como `s3`.
- **Verifique os logs**: `docker logs localstack-main` geralmente mostra o erro.
- **Portas em conflito**: Certifique-se de que as portas `4566` e a faixa `4510-4559` não estão em uso.

### "Connection refused" ao usar a AWS CLI
- **Confirme o endpoint**: Certifique-se de que está usando `--endpoint-url=http://localhost:4566` em todos os comandos.
- **Verifique se o container está rodando**: `docker ps | grep localstack`

### Problemas de permissão com o Docker Socket
- Se o LocalStack não consegue iniciar Lambdas, pode ser um problema de permissão no `/var/run/docker.sock`. Verifique as permissões do arquivo no host.

## 📚 Documentação Adicional

- Documentação Oficial do LocalStack
- Configuração do LocalStack
- Referência de Serviços Suportados