# PrimeTime Toran Proxy Docker Image

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