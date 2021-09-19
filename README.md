# Dockerfiles for drupal

This repository contains dockerfiles for various php versions, together with apache, ssh and tools useful for debugging. They are not meant to be used for production hosting.

The docker container comes with 2 services, apache on 80 and ssh on 22. You will need to map your local installation to /var/www.

## Logins / Passwords

    ssh    : root:root

The container contains

  * apache 2
  * php with some extensions
  * composer
  * ssh
  * git
  * imagemagick

## Available php versions:

  * 5.6
  * 7.1
  * 7.2
  * 7.3
  * 7.4
  * 8.0

## Building the docker container:

```
cd php
docker build -t factorial-io/drupal-docker:php-<version>  -f Dockerfile.php-<version> .
cd ../php-xdebug
docker build \
  --build-arg BASE_IMAGE_TAG=php-<version> \
  -t factorial-io/drupal-docker:php-<version>-xdebug  \
  -f Dockerfile.php-<version> \
  .
cd ../php-wkhtmltopdf
docker build \
  --build-arg TARGETARCH=<amd64|arm64> \
  --build-arg BASE_IMAGE_TAG=php-<version> \
  -t factorial-io/drupal-docker:php-<version>-wkhtmltopdf \
  -f Dockerfile.php-<version> \
  .

```

Using the build script:

```
# Build all images locally for the local native docker.
sh build.sh native
# Build all images using a registered muti-arch builder. Images will be pushed to the docker registry. (Log in first!)
sh build.sh both
# Build only php-7.4 and tag the images with the suffix test
sh build.sh native test 74
```
