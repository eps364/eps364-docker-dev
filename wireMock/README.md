# WireMock Docker Setup

Este diretório contém a configuração Docker para executar o WireMock, uma ferramenta de simulação de APIs HTTP para testes.

## O que é WireMock?

WireMock é uma biblioteca/simulador para APIs HTTP. Ele pode ser usado para testar aplicações que fazem chamadas HTTP, simulando respostas de serviços externos.

## Configuração

A configuração está definida no arquivo `docker-compose.yml`:

- **Imagem**: `wiremock/wiremock:latest` (imagem oficial do WireMock)
- **Porta**: Exposição da porta 8080 do container na porta 8000 do host
- **Volumes**:
  - `./wiremock/__files` mapeado para `/home/wiremock/__files` (para arquivos de resposta)
  - `./wiremock/mappings` mapeado para `/home/wiremock/mappings` (para definições de mapeamentos)
- **Comando**: `--verbose` para logging detalhado

## Como usar

1. Certifique-se de que o Docker está instalado e rodando.

2. Para iniciar o WireMock:
   ```bash
   docker compose up -d
   ```

3. O WireMock estará disponível em `http://localhost:8000`.

4. Para parar:
   ```bash
   docker compose down
   ```

## Adicionando Mapeamentos

Para adicionar mapeamentos personalizados, coloque arquivos JSON na pasta `wiremock/mappings/`. Exemplos:

- `wiremock/mappings/example.json`:
  ```json
  {
    "request": {
      "method": "GET",
      "url": "/api/example"
    },
    "response": {
      "status": 200,
      "jsonBody": {"message": "Hello World"}
    }
  }
  ```

- Arquivos de resposta podem ser colocados em `wiremock/__files/`.

## Verificação

Para verificar se está funcionando, acesse `http://localhost:8000/__admin/` para o painel de administração do WireMock.

## Notas

- A configuração usa a versão mais recente do WireMock. Para uma versão específica, altere `latest` para uma tag como `3.0.1`.
- Os diretórios `wiremock/__files` e `wiremock/mappings` foram criados para persistir configurações.</content>
<parameter name="filePath">/home/emerson/projetos/eps364-docker-dev/wireMock/README.md
