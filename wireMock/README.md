# WireMock Docker Setup

Este diretório contém a configuração Docker para executar o WireMock, uma ferramenta de simulação de APIs HTTP para testes.

## O que é WireMock?

WireMock é uma biblioteca/simulador para APIs HTTP. Ele pode ser usado para testar aplicações que fazem chamadas HTTP, simulando respostas de serviços externos.

## Configuração

A configuração está definida no arquivo `docker-compose.yml`:

- **Imagem**: `wiremock/wiremock:latest` (imagem oficial do WireMock)
- **Portas**:
  - HTTP: Porta 8080 do container exposta na porta 8000 do host
  - HTTPS: Porta 8443 do container exposta na porta 8443 do host (usa certificado auto-assinado)
- **Volumes**:
  - `./wiremock/__files` mapeado para `/home/wiremock/__files` (para arquivos de resposta)
  - `./wiremock/mappings` mapeado para `/home/wiremock/mappings` (para definições de mapeamentos)
  - `./wiremock/extensions` mapeado para `/home/wiremock/extensions` (para extensões personalizadas)
- **Opções**: `--https-port 8443 --verbose` para habilitar HTTPS na porta 8443 e logging detalhado

## Como usar

1. Certifique-se de que o Docker está instalado e rodando.

2. Para iniciar o WireMock:
   ```bash
   docker compose up -d
   ```

3. O WireMock estará disponível em:
   - **HTTP**: `http://localhost:8000`
   - **HTTPS**: `https://localhost:8443` (aceite o certificado auto-assinado no navegador)

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

Para verificar se está funcionando, acesse o painel de administração do WireMock:
- **HTTP**: `http://localhost:8000/__admin/`
- **HTTPS**: `https://localhost:8443/__admin/` (aceite o certificado auto-assinado)

## Notas

- A configuração usa a versão mais recente do WireMock. Para uma versão específica, altere `latest` para uma tag como `3.0.1`.
- Os diretórios `wiremock/__files`, `wiremock/mappings` e `wiremock/extensions` foram criados para persistir configurações.
- O HTTPS usa um certificado auto-assinado gerado automaticamente pelo WireMock. Em produção ou testes reais, considere fornecer seu próprio keystore via volume ou variável de ambiente.</content>
<parameter name="filePath">/home/emerson/projetos/eps364-docker-dev/wireMock/README.md
