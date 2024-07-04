args = `arg="$(filter-out $(firstword $(MAKECMDGOALS)),$(MAKECMDGOALS))" && echo $${arg:-${1}}`

%:
	@:

.PHONY: help
help: ## Print help
	@awk 'BEGIN {FS = ":.*##"; printf "\nUsage:\n  make \033[36m<target>\033[0m\n\nTargets:\n"} /^[a-zA-Z_-]+:.*?##/ { printf "  \033[36m%-10s\033[0m %s\n", $$1, $$2 }' $(MAKEFILE_LIST)

.PHONY: bash
bash: ## Drop into the bash prompt of your Docker container
	@./bin/bash

.PHONY: cli
cli: ## Run any CLI command without going into the bash prompt
	@./bin/cli $(call args)

.PHONY: docker-compose
docker-compose: ## Support V1 (`docker-compose`) and V2 (`docker compose`) docker compose command, and use custom configuration files
	@./bin/docker-compose

.PHONY: restart
restart: ## Stop and then start all containers
	@./bin/restart $(call args)

.PHONY: setup-ssl
setup-ssl: ## Generate an SSL certificate for one or more domains
	@./bin/setup-ssl $(call args)

.PHONY: setup-ssl-ca
setup-ssl-ca: ## Generate a certificate authority and copy it to the host
	@./bin/setup-ssl-ca

.PHONY: start
start: ## Start all containers
	@./bin/start $(call args)

.PHONY: stop
stop: ## Stop all project containers
	@./bin/stop $(call args)
