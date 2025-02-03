# Define the base directory
BASE_DIR := /opt/apps

# List of directories to deploy
DIRS := treafik homeassistant cloudflared

# Target to create the BASE_DIR if it does not exist
.PHONY: create-dir
create-dir:
	@echo "Checking if directory $(BASE_DIR) exists..."
	@if [ ! -d "$(BASE_DIR)" ]; then \
		echo "Directory $(BASE_DIR) does not exist. Creating..."; \
		mkdir -p $(BASE_DIR); \
	else \
		echo "Directory $(BASE_DIR) already exists."; \
	fi

# Target to deploy services
.PHONY: deploy
deploy: create-dir
	@cd $(BASE_DIR) && \
	$(foreach dir,$(DIRS), \
		if [ -f "$(BASE_DIR)/$(dir)/docker-compose.yml" ]; then \
			echo "Starting project in $(dir)"; \
			docker compose --env-file "$(BASE_DIR)/$(dir)/.env" -f "$(BASE_DIR)/$(dir)/docker-compose.yml" up -d; \
		fi; \
	)

# Target to stop and remove all containers, networks, and volumes
.PHONY: down
down:
	@echo "Stopping and removing all containers..."
	@for dir in $(DIRS); do \
		if [ -f "$(BASE_DIR)/$$dir/docker-compose.yml" ]; then \
			echo "Stopping containers in $$dir"; \
			docker compose -f "$(BASE_DIR)/$$dir/docker-compose.yml" down; \
		fi; \
	done

# Default target
.PHONY: all
all: deploy
