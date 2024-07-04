# Flash development

[![Supported PHP Versions][version-img]][version]
[![PHP Total Downloads][icon-php-downloads]][link-php-dockerhub]
[![Nginx Total Downloads][icon-nginx-downloads]][link-nginx-dockerhub]
[![Software License][icon-license]][link-license]

Docker's environment development for PHP (Laravel, Wordpress, Magento...)

## Table of contents

- [Docker Hub](#docker-hub)

## Docker Hub

View Dockerfiles for the latest tags:

- [focela/nginx (Docker Hub)](https://hub.docker.com/r/focela/nginx/)
    - [`1.18`](images/nginx/1.25)
- [focela/php (Docker Hub)](https://hub.docker.com/r/focela/php/)
    - [`8.1-fpm`](images/php/8.1)
    - [`8.2-fpm`](images/php/8.2)
    - [`8.3-fpm`](images/php/8.3)

## Usage

This configuration is intended to be used as a Docker-based development environment for PHP (Laravel, Wordpress,
Magento...)

Folders:

- `images`: Docker images for nginx and php
- `compose`: sample setups with Docker Compose

## Prerequisites

This setup assumes you are running Docker on a computer with at least 6GB of RAM allocated to Docker, a dual-core, and
an SSD hard drive. [Download & Install Docker Desktop](https://www.docker.com/products/docker-desktop).

This configuration has been tested on Mac & Linux. Windows is supported through the use of Docker on WSL.

## Custom CLI Commands

- `bin/bash`: Drop into the bash prompt of your Docker container. The `phpfpm` container should be mainly used to access
  the filesystem within Docker.
- `bin/cli`: Run any CLI command without going into the bash prompt. Ex. `bin/cli ls`
- `bin/docker-compose`: Support V1 (`docker-compose`) and V2 (`docker compose`) docker compose command, and use custom
  configuration files, such as `compose.yml` and `compose.dev.yml`
- `bin/restart`: Stop and then start all containers.
- `bin/setup-ssl`: Generate an SSL certificate for one or more domains. Ex. `bin/setup-ssl domain.test foo.test`
- `bin/setup-ssl-ca`: Generate a certificate authority and copy it to the host.
- `bin/start`: Start all containers, good practice to use this instead of `docker-compose up -d`, as it may contain
  additional helpers.
- `bin/stop`: Stop all project containers.

## Contributing

We encourage and support an active, healthy community of contributors &mdash;
including you! Details are in the [contribution guide](CONTRIBUTING.md) and
the [code of conduct](CODE_OF_CONDUCT.md). The flash-development maintainers keep an eye on
issues and pull requests, but you can also report any negative conduct to
opensource@focela.com. That email list is a private, safe space; even the flash-development
maintainers don't have access, so don't hesitate to hold us to a high
standard.

<hr>

Released under the [MIT License](LICENSE).

[version-img]: https://img.shields.io/badge/PHP-%3E%3D%208-yellow?logo=php&longCache=true

[version]: https://www.php.net/releases/8.0/en.php

[icon-php-downloads]: https://img.shields.io/docker/pulls/focela/php.svg?label=PHP%20pulls

[icon-nginx-downloads]: https://img.shields.io/docker/pulls/focela/nginx.svg?label=Nginx%20pulls

[icon-license]: https://img.shields.io/badge/license-MIT-blue.svg

[link-php-dockerhub]: https://hub.docker.com/r/focela/php/

[link-nginx-dockerhub]: https://hub.docker.com/r/focela/nginx/

[link-license]: https://opensource.org/license/mit