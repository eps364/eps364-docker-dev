# Mockoon - API Mock Server

Mockoon e uma ferramenta para simular APIs HTTP durante o desenvolvimento e testes.

## Como usar

### Iniciar o servico

```bash
docker compose -f mockoon/docker-compose.yml up -d
```

### Parar o servico

```bash
docker compose -f mockoon/docker-compose.yml down
```

## Endpoint de teste

Com a configuracao padrao, a API ficara disponivel em:

- http://localhost:8080/products (GET)
- http://localhost:8080/products/:id (GET)
- http://localhost:8080/products (POST)
- http://localhost:8080/products/:id (PUT)
- http://localhost:8080/products/:id (DELETE)

Exemplo de resposta:

```json
{
  "id": 1,
  "name": "Produto 1",
  "price": 99.9,
  "stock": 10,
  "active": true
}
```

## Estrutura

- `docker-compose.yml`: definicao do container Mockoon
- `data/mockoon-data.json`: ambiente de mock carregado pelo Mockoon CLI
- `data/sellerCenter.json`: ambiente SellerCenter de referencia (rota consolidada em `mockoon-data.json` para uso na porta 8080)

## Personalizacao

1. Abra o Mockoon Desktop e exporte seu ambiente como JSON.
2. Substitua o arquivo `mockoon/data/mockoon-data.json` pelo export.
3. Reinicie o container:

```bash
docker compose -f mockoon/docker-compose.yml up -d --force-recreate
```

## Variaveis opcionais

- `MOCKOON_IMAGE` (default: `mockoon/cli:latest`)
- `MOCKOON_NAME` (default: `mockoon`)
- `MOCKOON_PORT` (default: `8080`)
