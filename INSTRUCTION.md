# Django Todolist — Docker Compose

This project runs a Django Todolist application and a MySQL database using Docker Compose.

## Prerequisites

- Docker installed
- Docker Compose installed
- Docker Desktop running (if applicable)

## Build and Run

Clone the repository and navigate to the project directory.

Build and start both containers:

```bash
docker compose up --build
```

To run containers in detached mode:

```bash
docker compose up -d --build
```

Docker Compose will:
1. Build the Django application image.
2. Start the MySQL container.
3. Wait until MySQL is healthy.
4. Run Django database migrations automatically.
5. Start the Django development server.

## Access the Application

Open the following URL in your browser:

http://localhost:8080

## Check Running Containers

```bash
docker compose ps
```

## View Container Logs

View logs from both containers:

```bash
docker compose logs
```

Follow logs in real time:

```bash
docker compose logs -f
```

View only Django logs:

```bash
docker compose logs web
```

## Stop Containers

Stop and remove the containers and Compose network:

```bash
docker compose down
```

The MySQL database volume will be preserved.

## Restart Containers

```bash
docker compose up -d
```

## Persistent MySQL Storage

MySQL data is stored in a named Docker volume called `mysql_data`, mounted at `/var/lib/mysql`.

This ensures that user accounts and todo tasks remain available after containers are stopped or recreated.

To remove containers and database volumes:

```bash
docker compose down -v
```

**Warning:** This command deletes the persistent MySQL database data.

## Verify Data Persistence

1. Start the application with `docker compose up -d --build`.
2. Open http://localhost:8080.
3. Register or log in and create a todo task.
4. Stop the containers using `docker compose down`.
5. Restart them using `docker compose up -d`.
6. Open the application again and verify that the todo task still exists.

## Database Configuration

The application uses MySQL 8.0.

The database connection is configured through environment variables in `docker-compose.yml`.

The Django service connects to MySQL using the Compose service hostname `db` and port `3306`.

Database migrations are executed automatically when the Django container starts.
