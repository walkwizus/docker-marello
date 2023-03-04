
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