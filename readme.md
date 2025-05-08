# Greenlight API

Greenlight is a RESTful API service for managing movie information, built with Go. This project implements a production-ready backend service with authentication, permission-based authorization, rate limiting, and more.

## Features

- RESTful API endpoints for movie data management (CRUD operations)
- User authentication and management
- Request filtering, sorting, and pagination
- Full-text search capabilities
- Rate limiting
- Metrics tracking
- PostgreSQL database integration
- Email sending functionality

## API Endpoints

| Method | URL Pattern | Action |
|--------|-------------|--------|
| GET | /v1/healthcheck | Show application health and version information |
| GET | /v1/movies | Show the details of all movies |
| POST | /v1/movies | Create a new movie |
| GET | /v1/movies/:id | Show the details of a specific movie |
| PATCH | /v1/movies/:id | Update the details of a specific movie |
| DELETE | /v1/movies/:id | Delete a specific movie |
| POST | /v1/users | Register a new user |
| PUT | /v1/users/activated | Activate a specific user |
| PUT | /v1/users/password | Update the password for a specific user |
| POST | /v1/tokens/authentication | Generate a new authentication token |
| POST | /v1/tokens/password-reset | Generate a new password-reset token |
| GET | /debug/vars | Display application metrics |

## Getting Started

### Prerequisites

- Go 1.19 or higher
- PostgreSQL 12 or higher

### Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/yourusername/greenlight.git
   cd greenlight
   ```

2. Install dependencies:
   ```bash
   go mod download
   ```

3. Set up the PostgreSQL database:
   ```bash
   # Create the database
   createdb greenlight
   
   # Run migrations (once the application is built)
   ./greenlight -db-migrate
   ```

4. Configure environment variables (see Configuration section below)

5. Build and run the application:
   ```bash
   make build
   ./bin/greenlight
   ```

### Example API Usage

Fetch a specific movie:
```bash
curl -H "Authorization: Bearer RIDBIAE3AMMK57T6IAEBUGA7ZQ" localhost:4000/v1/movies/1
```

Response:
```json
{
    "movie": {
        "id": 1,
        "title": "Moana",
        "year": 2016,
        "runtime": "107 mins",
        "genres": [
            "animation",
            "adventure"
        ],
        "version": 1
    }
}
```

## Configuration

The application can be configured using environment variables or command line flags:

| Setting | Environment Variable | Command Line Flag | Default |
|---------|----------------------|------------------|---------|
| Server port | PORT | -port | 4000 |
| Environment | ENV | -env | development |
| Database DSN | DB_DSN | -db-dsn | postgres://greenlight:password@localhost/greenlight |
| Database max open conns | DB_MAX_OPEN_CONNS | -db-max-open-conns | 25 |
| Database max idle conns | DB_MAX_IDLE_CONNS | -db-max-idle-conns | 25 |
| Database max idle time | DB_MAX_IDLE_TIME | -db-max-idle-time | 15m |
| SMTP host | SMTP_HOST | -smtp-host | smtp.mailtrap.io |
| SMTP port | SMTP_PORT | -smtp-port | 25 |
| SMTP username | SMTP_USERNAME | -smtp-username | - |
| SMTP password | SMTP_PASSWORD | -smtp-password | - |
| SMTP sender | SMTP_SENDER | -smtp-sender | Greenlight <no-reply@greenlight.example.com> |


```

## Development

### Running Tests

```bash
go test -v ./...
```

### Using Make

Several Make commands are available for development:

```bash
# Build the application
make build

# Run all tests
make test

# Lint the code
make lint

# Clean build artifacts
make clean
```

## License

This project is licensed under the MIT License - see the LICENSE file for details.
