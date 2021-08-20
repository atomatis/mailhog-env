# Mailhog environment

## Dependencies

- [Traefik environment](https://github.com/atomatis/traefik-env)

## Installation

```bash
cp .env.dist .env
sed -i "" "s#CHANGE_ME#REPLACE_THIS_BY_YOUR_LOCAL_DOMAIN#g" .env
```

**Create docker network**
```bash
docker network create smtp
```

**Run Mailhog container**

```bash
docker-compose up -d
```

## Usage

**Access to Mailhog dashboard:**

```mailhog.REPLACE_THIS_BY_YOUR_LOCAL_DOMAIN``` on our favorite browser (it's Firefox ofc).

Or use [localhost](localhost:8080).

**Docker-compose example:**

```yaml
# docker-compose.yaml

services:
  my-web-server:
    image: php-apache
    ports:
      - 80
    # Required
    networks:
      - smtp
    /.../
    
# Required
networks:
  proxy:
    external:
      name: smtp
```

And target mail server with ```smtp://mail-tester:25``` on your configuration.
