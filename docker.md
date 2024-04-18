---
layout: default
title: UniTime Docker Installation
---

## How to use

- Download the latest release of UniTime 4.8.126 or later from [UniTime nightly builds](https://builds.unitime.org/) or [UniTime releases](https://github.com/UniTime/unitime/releases/latest).

- Unzip the downloaded distribution, and go to the `docker` folder.

    ```
    unzip unitime-4.8_bld126.zip
    cd docker
    ```

- Build and deploy docker images using the following command:

    ```
    docker-compose build && docker-compose up
    ```

- Once the project has been built and deployed, UniTime should become available at [localhost:8888](http://localhost:8888).

- Log in using `admin` as both user name and password.
  - Other available credentials are listed at [demo.unitime.org](https://demo.unitime.org).

## Additional Notes

- This is a simple installation much like the [online demo](https://demo.unitime.org), with only one web-server and no dedicated solver server.

- All components (OpenJDK 11, Tomcat 9, and MySQL 8.3) are included in one container.

- No HTTPS included, but a reverse-proxy can be used to provide SSL layer.

- Inspired by [vlatka-sinisa/docker-unitime](https://github.com/vlatka-sinisa/docker-unitime)

- See [UniTime Installation](installation) for traditional installation, customization, etc.