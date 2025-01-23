# n8n instalacao vps via Easy Panel

# Instalaçao dos bancos de dados

- Postgres
- Redis

# Instalaçao do n8n

1. **Instale o editor**

```json
{
  "services": [
    {
      "type": "app",
      "data": {
        "projectName": "n8n_start",
        "serviceName": "n8n_start",
        "source": {
          "type": "image",
          "image": "n8nio/n8n:latest"
        },
        "domains": [
          {
            "host": "$(EASYPANEL_DOMAIN)",
            "port": 5678
          }
        ],
        "env": "N8N_ENCRYPTION_KEY=qwSYwLlijZOh+FaBHrK0tfGzxG6W/J4O",
         "deploy": {
                  "replicas": 1,
                  "command": "n8n start",
                  "zeroDowntime": true
        },
        "mounts": []
      }
    }
  ]
}
```

1. Instale o webhook

```json
{
  "services": [
    {
      "type": "app",
      "data": {
        "projectName": "n8n_webhook",
        "serviceName": "n8n_webhook",
        "source": {
          "type": "image",
          "image": "n8nio/n8n:latest"
        },
        "domains": [
          {
            "host": "$(EASYPANEL_DOMAIN)",
            "port": 5678
          }
        ],
        "env": "N8N_ENCRYPTION_KEY=qwSYwLlijZOh+FaBHrK0tfGzxG6W/J4O",
         "deploy": {
          "replicas": 1,
          "command": "n8n webhook",
          "zeroDowntime": true
        },
        "mounts": []
      }
    }
  ]
}
```

1. Instale o worker

```json
{
  "services": [
    {
      "type": "app",
      "data": {
        "projectName": "n8n_worker",
        "serviceName": "n8n_worker",
        "source": {
          "type": "image",
          "image": "n8nio/n8n:latest"
        },
        "domains": [
          {
            "host": "$(EASYPANEL_DOMAIN)",
            "port": 5678
          }
        ],
        "env": "N8N_ENCRYPTION_KEY=qwSYwLlijZOh+FaBHrK0tfGzxG6W/J4O",
         "deploy": {
          "replicas": 1,
          "command": "n8n worker --concurrency=10",
          "zeroDowntime": true
        },
        
        "mounts": []
      }
    }
  ]
}
```

### Variáveis de ambiente

Alterar as credencais do Postgres e Redis.
```
### Você pode criar a sua própria Encryption Key
N8N_ENCRYPTION_KEY = qwSYwLlijZOh+FaBHrK0tfGzxG6W/J4O

### Banco de Dados - Coloque suas credenciais ###
DB_TYPE=postgresdb
DB_POSTGRESDB_DATABASE=database
DB_POSTGRESDB_HOST=n8n_postgres
DB_POSTGRESDB_PORT=5432
DB_POSTGRESDB_USER=postgres
DB_POSTGRESDB_PASSWORD=d5a2837c7e6ef4ed245a

### Redis - Configurações ###
QUEUE_BULL_REDIS_HOST=n8n_redis
QUEUE_BULL_REDIS_PORT=6379
QUEUE_BULL_REDIS_DB=2
QUEUE_BULL_REDIS_USER=default
QUEUE_BULL_REDIS_PASSWORD=1e382732350a69760a4e

### Configurações Gerais ###
NODE_FUNCTION_ALLOW_EXTERNAL=moment,lodash,moment-with-locales
EXECUTIONS_DATA_PRUNE=true
EXECUTIONS_DATA_MAX_AGE=336
GENERIC_TIMEZONE=America/Sao_Paulo
TZ=America/Sao_Paulo
EXECUTIONS_MODE=queue
N8N_HOST=https://$(PRIMARY_DOMAIN)
N8N_EDITOR_BASE_URL=https://$(PRIMARY_DOMAIN)
N8N_PROTOCOL=https
NODE_ENV=production
WEBHOOK_URL=https://$(PRIMARY_DOMAIN)

### Configuração de E-mail Para recuperação da senha ###
N8N_EMAIL_MODE=smtp
N8N_SMTP_HOST=smtp.hostinger.com
N8N_SMTP_PORT=465
N8N_SMTP_USER=seu_email@gmail.com
N8N_SMTP_PASS=123455
N8N_SMTP_SENDER=Seu Nome <seu_email@gmail.com>
N8N_SMTP_SSL=true
```
