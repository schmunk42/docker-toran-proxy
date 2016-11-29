# PrimeTime Toran Proxy Docker Image

:whale: https://hub.docker.com/r/schmunk42/toran-proxy/
:octocat: https://github.com/schmunk42/docker-toran-proxy

### Features

- non-priviliged user (alpha)
- environment based configuration
- ssh for git proxy
- automatically sets up location for mirrors
- generates mirror urls for toran config
- cron set to run every minute
- based on phusion-baseimage
- installs github oauth token
- add custom public key through environment variable

### Environment Variables
Key  | Value | Default
------------- | ------------- | -------------
SECRET  | Secret | **RandomString**
TORAN_SCHEME  | Protocol | http
TORAN_HTTP_PORT  | HTTP Port | 80
TORAN_HTTPS_PORT  | HTTPS Port | 443
TORAN_HOST | Hostname | **ChangeMe**
TORAN_BASE_URL | Base URL | **NULL**
GITHUB_OAUTH | Github OAuth | **ChangeMe**
PUB_KEY | Public key for Alpha user | **NULL**


### Usage

Run a container from the image

    docker run \
        -e TORAN_HOST=docker.local \
        -e SECRET=secret \
        -e GITHUB_OAUTH=1ab2c \
        -p 80 \
        schmunk42/toran-proxy

        
### docker-compose
        
Mount `defaults.yml`

    toran:
      image: schmunk42/toran-proxy:1.4.0
      environment:
        VIRTUAL_HOST: toran.example.com
        TORAN_HOST: toran.example.com
        CERT_NAME: default
        TORAN_SCHEME: https
        SECRET: <INSERT_SECRET>_
        GITHUB_OAUTH: <YOUR_TOKEN>
      ports:
        - '8380:80'
      restart: always
      volumes:
        - ./custom/init.sh:/root/init.sh
        - ./custom/auth.json:/var/www/toran/app/toran/composer/auth.json
        - ./custom/config.yml:/var/www/toran/app/toran/config.yml
        - ./custom/defaults.yml:/var/www/toran/app/config/defaults.yml
        - ./persist/toran/mirrors:/home/alpha/mirrors
        - ./persist/toran/app/cache:/var/www/toran/app/cache
        - ./persist/toran/cache:/var/www/toran/app/toran/cache
      command: bash /root/init.sh
