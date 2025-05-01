# n8n-docker

A flexible Docker template for running n8n with support for multiple database types and task runners.

## Features

- Support for multiple databases (SQLite, PostgreSQL, MySQL, MongoDB)
- Flexible network configuration
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

## Network Modes

This template supports different network modes depending on your operating system:

### Bridge Mode (Default, recommended for all systems)
```bash
# Start with bridge mode
docker compose --profile bridge-mode up -d
```
- Uses Docker's default bridge networking
- Ports are mapped from the container to the host
- Works on all operating systems (Linux, macOS, Windows)
- Configure using port mappings in the `ports` section

### Host Mode (Linux only)
```bash
# Start with host mode (Linux only)
docker compose up -d
```
- Only fully supported on Linux systems
- Container uses the host's network directly
- Ports are managed by environment variables (`N8N_PORT` and `N8N_RUNNERS_BROKER_PORT`)
- Not recommended for macOS or Windows users
- Useful for specific network requirements or performance on Linux

> **Note**: On macOS and Windows, the host network mode is not fully supported due to the way Docker is implemented on these systems. Please use bridge mode instead.

## Environment Variables

Check the `env.example` file for a complete template with default values. Below are all available configuration options:

| Variable | Description | Default | Required |
|----------|-------------|---------|----------|
| **Network & Port Settings** ||||
| `NETWORK_MODE` | Docker network mode (bridge, host) | bridge | No |
| `N8N_PORT` | Main n8n port (used in both network modes) | 5678 | No |
| `N8N_RUNNERS_BROKER_PORT` | Task runners broker port (used in both network modes) | 5679 | No |
| **General Settings** ||||
| `N8N_VERSION` | n8n version to use | latest | No |
| `WEBHOOK_URL` | Base URL for webhooks | http://localhost:5678 | No |
| `GENERIC_TIMEZONE` | Application timezone | UTC | No |
| `N8N_ENCRYPTION_KEY` | Encryption key for credentials | - | Yes |
| **Security Settings** ||||
| `N8N_ENFORCE_SETTINGS_FILE_PERMISSIONS` | Enforce secure file permissions on settings files | true | No |
| **Database Settings** ||||
| `DB_TYPE` | Database type (sqlite, postgresdb, mysqldb, mongodb) | sqlite | Yes |
| **PostgreSQL Settings** ||||
| `DB_POSTGRESDB_HOST` | PostgreSQL host | postgres | Yes* |
| `DB_POSTGRESDB_PORT` | PostgreSQL port | 5432 | Yes* |
| `DB_POSTGRESDB_DATABASE` | PostgreSQL database name | n8n | Yes* |
| `DB_POSTGRESDB_USER` | PostgreSQL user | postgres | Yes* |
| `DB_POSTGRESDB_PASSWORD` | PostgreSQL password | - | Yes* |
| **MySQL Settings** ||||
| `DB_MYSQLDB_HOST` | MySQL host | mysql | Yes** |
| `DB_MYSQLDB_PORT` | MySQL port | 3306 | Yes** |
| `DB_MYSQLDB_DATABASE` | MySQL database name | n8n | Yes** |
| `DB_MYSQLDB_USER` | MySQL user | root | Yes** |
| `DB_MYSQLDB_PASSWORD` | MySQL password | - | Yes** |
| **MongoDB Settings** ||||
| `DB_MONGODB_CONNECTION_URL` | MongoDB connection URL | - | Yes*** |
| **SQLite Settings** ||||
| `DB_SQLITE_PATH` | SQLite database path | /home/node/.n8n/database.sqlite | Yes**** |
| **Task Runners** ||||
| `N8N_RUNNERS_ENABLED` | Enable task runners | true | No |
| `N8N_RUNNERS_MODE` | Runner execution mode (internal/external) | internal | No |
| `N8N_RUNNERS_TIMEOUT` | Maximum task execution time (seconds) | 60 | No |
| `N8N_RUNNERS_MAX_CONCURRENCY` | Maximum concurrent tasks | 5 | No |
| `N8N_RUNNERS_BROKER_LISTEN_ADDRESS` | Broker listen address | 0.0.0.0 | No |
| **Authentication** ||||
| `N8N_BASIC_AUTH_ACTIVE` | Enable basic authentication | false | No |
| `N8N_BASIC_AUTH_USER` | Basic auth username | admin | Yes**** |
| `N8N_BASIC_AUTH_PASSWORD` | Basic auth password | - | Yes**** |

\* Required if using PostgreSQL (DB_TYPE=postgresdb)
\** Required if using MySQL (DB_TYPE=mysqldb)
\*** Required if using MongoDB (DB_TYPE=mongodb)
\**** Required if using SQLite (DB_TYPE=sqlite)

## Management Commands

Start the application (recommended way):
```bash
docker compose --profile bridge-mode up -d
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
