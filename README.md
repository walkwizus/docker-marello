# <p align="center">walkwizus/docker-marello</p>

Docker environment for Marello Application inspired by the awesome [Mark Shust's Docker for Magento](https://github.com/markshust/docker-magento)

## 🛠️ Setup Project

```bash
mkdir ~/Sites/marello
cd $_
curl -s https://raw.githubusercontent.com/walkwizus/docker-marello/master/lib/template | bash

# Clone Marello repository
git clone https://github.com/marellocommerce/marello-application.git src

# Marello EE
# git clone https://github.com/marellocommerce/marello-application-ee.git

bin/start --no-dev
bin/copytocontainer --all
bin/composer install
```
### Configuration values

| Configuration | Value |
| -------- | -------- |
| database_driver | pdo_mysql |
| database_host | db |
| database_port | 3306 | 
| database_name | marello |
| database_user | marello |
| database_password | marello |
| database_server_version | null |
| database_driver_options | { } |
| mailer_dsn | mailcatcher |
| websocket_bind_address | 0.0.0.0 |
| websocket_bind_port | 8080 |
| websocket_frontend_host | '*' |
| websocket_frontend_port | 8080 |
| websocket_frontend_path | '' |
| websocket_backend_host | '*' |
| websocket_backend_port | 8080 |
| websocket_backend_path | '' |
| websocket_backend_transport | tcp |
| websocket_backend_ssl_context_options | { } |
| search_engine_name | orm |
| search_engine_host | 127.0.0.1 |
| search_engine_port | null |
| search_engine_index_prefix | oro_search |
| search_engine_username | null |
| search_engine_password | null |
| search_engine_ssl_verification | null |
| search_engine_ssl_cert | null |
| search_engine_ssl_cert_password | null |
| search_engine_ssl_key | null |
| search_engine_ssl_key_password | null |
| search_engine_dsn | orm |
| web_backend_prefix | '' |
| session_handler | session.handler.native_file |
| installed | null |
| secret | ThisTokenIsNotSoSecretChangeIt |
| message_queue_transport | dbal |
| message_queue_transport_config | null |
| enable_price_sharding | null |
| deployment_type | null |
| liip_imagine.jpegoptim.binary | null |
| liip_imagine.pngquant.binary | null |

### Finish installation

```bash
bin/copyfromcontainer composer.lock
bin/restart
bin/console oro:install
bin/console oro:assets:install

# Setup SSL cert
bin/setup-ssl www.marello.local
open https://www.marello.local
```

## Usage

- `bin/bash`: Drop into the bash prompt of your Docker container. The phpfpm container should be mainly used to access the filesystem within Docker.
- `bin/cli`: Run any CLI command without going into the bash prompt. Ex. bin/cli ls
- `bin/clinotty`: Run any CLI command with no TTY. Ex. bin/clinotty chmod u+x bin/console
- `bin/cliq`: The same as `bin/cli`, but pipes all output to `/dev/null`. Useful for a quiet CLI, or implementing long-running processes.
- `bin/composer`: Run the composer binary. Ex. `bin/composer install`
- `bin/console`: Run the Symfony Console. Ex: `bin/console cache:clean`
- `bin/copyfromcontainer`: Copy folders or files from container to host. Ex. `bin/copyfromcontainer vendor`
- `bin/copytocontainer`: Copy folders or files from host to container. Ex. `bin/copytocontainer --all`
- `bin/docker-compose`: Support V1 (docker-compose) and V2 (docker compose) docker compose command, and use custom configuration files, such as `compose.yml` and `compose.dev.yml`
- `bin/fixowns`: This will fix filesystem ownerships within the container.
- `bin/fixperms`: This will fix filesystem permissions within the container.
- `bin/mysql`: Run the MySQL CLI with database config from `env/db.env`. Ex. `bin/mysql -e "EXPLAIN oro_config"`
- `bin/node`: Run the node binary. Ex. `bin/node --version`
- `bin/npm`: Run the npm binary. Ex. `bin/npm install`
- `bin/redis`: Run a command from the redis container. Ex. `bin/redis redis-cli monitor`
- `bin/remove`: Remove all containers.
- `bin/removeall`: Remove all containers, networks, volumes, and images, calling bin/stopall before doing so.
- `bin/removevolumes`: Remove all volumes.
- `bin/restart`: Stop and then start all containers.
- `bin/root`: Run any CLI command as root without going into the bash prompt. Ex `bin/root apt-get install nano`
- `bin/rootnotty`: Run any CLI command as root with no TTY. Ex `bin/rootnotty chown -R app:app /var/www/html`
- `bin/setup-ssl`: Generate an SSL certificate for one or more domains. Ex. `bin/setup-ssl marello.test foo.test`
- `bin/setup-ssl-ca`: Generate a certificate authority and copy it to the host.
- `bin/start`: Start all containers, good practice to use this instead of `docker-compose up -d`, as it may contain additional helpers.
- `bin/status`: Check the container status.
- `bin/stop`: Stop all project containers.
- `bin/stopall`: Stop all docker running containers
- `bin/update`: Update your project to the most recent version of `docker-marello`.