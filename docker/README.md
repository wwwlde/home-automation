# Docker

## Project Management with Makefile

This `Makefile` helps manage Docker containers for services (`treafik`, `homeassistant`, `cloudflared`).

## Commands

- `make` - Deploy all services.
- `make down` - Stop and remove all containers.
- `make create-dir` - Create the base directory (`/opt/apps`).
- `make deploy` - Deploy services defined in the `DIRS` variable.
