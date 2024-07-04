# Changelog

All notable changes to this project will be documented in this file.

This project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## v1.0.0 (04 Jul 2024)

Features:

* New Nginx 1.25 image
* New PHP 8.1, 8.2, 8.3 image
* Add new `bin/bash` drop into the bash prompt of your Docker container
* Add new `bin/cli` run any CLI command without going into the bash prompt
* Add new `bin/docker-compose` support V1 (`docker-compose`) and V2 (`docker compose`) docker compose command, and use
  custom configuration files
* Add new `bin/restart` stop and then start all containers
* Add new `setup-ssl` generate an SSL certificate for one or more domains
* Add new `setup-ssl-ca` generate a certificate authority and copy it to the host
* Add new `start` start all containers
* Add new `stop` stop all project containers
