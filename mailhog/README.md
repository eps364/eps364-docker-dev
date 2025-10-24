# MailHog - Email Testing Tool

MailHog é uma ferramenta de desenvolvimento que intercepta emails enviados pela aplicação, permitindo visualizá-los em uma interface web sem efetivamente enviar os emails para destinatários reais.

## 🚀 Como Usar

### Iniciar o Serviço

```bash
docker compose -f mailhog/docker-compose.yml up -d
```

### Parar o Serviço

```bash
docker compose -f mailhog/docker-compose.yml down
```

## 🌐 Acesso à Interface

- **Interface Web**: http://localhost:8025
- **Servidor SMTP**: localhost:1025

## 📧 Configuração da Aplicação

Configure sua aplicação para enviar emails através do MailHog:

### Configurações SMTP

| Parâmetro | Valor |
|-----------|-------|
| Host SMTP | localhost |
| Porta SMTP | 1025 |
| Usuário | (deixar vazio) |
| Senha | (deixar vazio) |
| Autenticação | Não |
| TLS/SSL | Não |

### Exemplo Spring Boot (application.yml)

```yaml
spring:
  mail:
    host: localhost
    port: 1025
    username: 
    password: 
    properties:
      mail:
        smtp:
          auth: false
          starttls:
            enable: false
```

### Exemplo Node.js (Nodemailer)

```javascript
const nodemailer = require('nodemailer');

const transporter = nodemailer.createTransporter({
  host: 'localhost',
  port: 1025,
  secure: false, // true for 465, false para outras portas
  auth: false
});
```

### Exemplo PHP

```php
// Configuração básica
ini_set('SMTP', 'localhost');
ini_set('smtp_port', 1025);

// Ou usando PHPMailer
$mail = new PHPMailer();
$mail->isSMTP();
$mail->Host = 'localhost';
$mail->Port = 1025;
$mail->SMTPAuth = false;
```

## 🎯 Funcionalidades

### Interface Web
- ✅ Visualização de todos os emails interceptados
- ✅ Busca por remetente, destinatário ou assunto
- ✅ Visualização de HTML e texto simples
- ✅ Download de emails individuais
- ✅ Exclusão de emails
- ✅ API REST para automação

### Características do Container
- **Imagem**: `mailhog/mailhog:latest`
- **Container**: `mailhog`
- **Restart Policy**: always
- **Porta Web UI**: 8025
- **Porta SMTP**: 1025

## 🛠️ Comandos Úteis

```bash
# Ver logs do MailHog
docker logs mailhog

# Testar envio via curl
curl -X POST http://localhost:8025/api/v1/messages \
  -H "Content-Type: application/json" \
  -d '{
    "from": "test@exemplo.com",
    "to": ["destino@exemplo.com"],
    "subject": "Teste",
    "body": "Mensagem de teste"
  }'

# Limpar todos os emails via API
curl -X DELETE http://localhost:8025/api/v1/messages
```

## 🔧 API REST

MailHog fornece uma API REST completa:

| Método | Endpoint | Descrição |
|--------|----------|-----------|
| GET | `/api/v1/messages` | Listar emails |
| GET | `/api/v1/messages/{id}` | Obter email específico |
| DELETE | `/api/v1/messages/{id}` | Deletar email específico |
| DELETE | `/api/v1/messages` | Deletar todos os emails |

### Exemplo de Resposta da API

```json
{
  "items": [
    {
      "ID": "001",
      "from": {"Email": "remetente@exemplo.com"},
      "to": [{"Email": "destino@exemplo.com"}],
      "subject": "Assunto do email",
      "created": "2024-01-01T10:00:00Z",
      "MIME": {
        "Headers": {...},
        "Body": "Conteúdo do email"
      }
    }
  ],
  "count": 1,
  "start": 0,
  "total": 1
}
```

## 🎭 Casos de Uso

### Durante o Desenvolvimento
- Testar templates de email
- Verificar conteúdo de emails automáticos
- Debugar problemas de formatação
- Validar links e imagens

### Em Testes Automatizados
- Verificar se emails foram enviados
- Validar conteúdo via API REST
- Testar fluxos de confirmação por email

## 🔍 Troubleshooting

### Emails não aparecem no MailHog
1. Verifique se a aplicação está configurada para usar `localhost:1025`
2. Confirme que não há firewall bloqueando a porta
3. Verifique os logs: `docker logs mailhog`

### Porta em uso
- Altere a porta no docker-compose.yml se necessário:
  ```yaml
  ports:
    - "8026:8025"  # Web UI na porta 8026
    - "1026:1025"  # SMTP na porta 1026
  ```

### Performance
- MailHog armazena emails em memória - reiniciar o container limpa todos os emails
- Para grandes volumes, considere usar outros interceptadores de email