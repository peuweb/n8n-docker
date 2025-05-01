# n8n-docker

A flexible Docker template for running n8n with support for multiple database types and task runners.

## Features

- Support for multiple databases (SQLite, PostgreSQL, MySQL, MongoDB)
- Task Runners enabled by default for secure code execution
- Basic authentication configuration
- Customizable environment variables
- Easy to set up and run

## Prerequisites

- Docker Engine 20.10.0+
- Docker Compose V2

## Quick Start

1. Set up environment variables:
```bash
cp env.example .env
```

2. Edit the `.env` file with your preferred settings:
- Choose your database type (sqlite, postgresdb, mysqldb, mongodb)
- Set secure passwords
- Configure authentication if needed
- Set your timezone
- Generate and set an encryption key:
  ```bash
  openssl rand -hex 32
  ```

3. Start the application:
```bash
docker compose up -d
```

The n8n interface will be available at: `http://localhost:5678`

## Environment Variables

Check the `env.example` file for a complete template with default values. Below are all available configuration options:

| Variable | Description | Default | Required |
|----------|-------------|---------|----------|
| **Database Settings** ||||
| `N8N_VERSION` | n8n version to use | latest | No |
| `DB_TYPE` | Database type (sqlite, postgresdb, mysqldb, mongodb) | sqlite | Yes |
| `DB_HOST` | Database host | localhost | Yes* |
| `DB_PORT` | Database port | 5432 | Yes* |
| `DB_DATABASE` | Database name | n8n | Yes* |
| `DB_USER` | Database user | root | Yes* |
| `DB_PASSWORD` | Database password | - | Yes* |
| `DB_CONNECTION_URL` | MongoDB connection URL | - | Yes** |
| `DB_SQLITE_PATH` | SQLite database path | /home/node/.n8n/database.sqlite | Yes*** |
| **Task Runners** ||||
| `N8N_RUNNERS_ENABLED` | Enable task runners | true | No |
| `N8N_RUNNERS_MODE` | Runner execution mode (internal/external) | internal | No |
| `N8N_RUNNERS_TIMEOUT` | Maximum task execution time (seconds) | 60 | No |
| `N8N_RUNNERS_MAX_CONCURRENCY` | Maximum concurrent tasks | 5 | No |
| `N8N_RUNNERS_BROKER_PORT` | Task runners broker port | 5679 | No |
| `N8N_RUNNERS_BROKER_LISTEN_ADDRESS` | Broker listen address | 0.0.0.0 | No |
| **Authentication** ||||
| `N8N_BASIC_AUTH_ACTIVE` | Enable basic authentication | false | No |
| `N8N_BASIC_AUTH_USER` | Basic auth username | admin | Yes**** |
| `N8N_BASIC_AUTH_PASSWORD` | Basic auth password | - | Yes**** |
| **General Settings** ||||
| `WEBHOOK_URL` | Base URL for webhooks | http://localhost:5678 | No |
| `N8N_PORT` | Main n8n port | 5678 | No |
| `GENERIC_TIMEZONE` | Application timezone | UTC | No |
| `N8N_ENCRYPTION_KEY` | Encryption key for credentials | - | Yes |

\* Required if using PostgreSQL or MySQL
\** Required if using MongoDB
\*** Required if using SQLite
\**** Required if basic auth is enabled

## Management Commands

Start the application:
```bash
docker compose up -d
```

Stop the application:
```bash
docker compose down
```

View logs:
```bash
docker compose logs -f
```

Restart a service:
```bash
docker compose restart n8n
```

## Volumes

The application uses the following volume:
- `./.n8n:/home/node/.n8n` - Stores n8n data and configurations

## Security Considerations

1. Always change default passwords in production
2. Generate a strong encryption key
3. Enable basic authentication in production
4. Keep your environment variables secure
5. Regularly update the n8n image

## Contributing

Feel free to open issues and pull requests!

## License

This project is licensed under the MIT License - see the LICENSE file for details.
