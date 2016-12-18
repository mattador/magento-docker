Magento 1 and 2 Docker Development stack
========================================

I created this custom build in my quest to reduce the painful memory/cpu overhead I experienced while developing Magento 2 applications on a traditional Vagrant/VirtualBox stack. There are plenty of Magento specific builds available on Docker Hub, but they all currently use Docker Toolbox, where as I wanted to use native docker for MacOSX. Additionally, none of the builds that I looked at included Redis for Magento session/cache storage, which was critical for me at the time. I took some inspiration from parts of [Laradock](https://github.com/laradock/laradock).

The dev stack comprises of 4 Debian-based images:

- Apache
- MySQL 5.7
- Redis
- PHP 7 (with all Magento 1 and 2 required extensions)

Basic instructions
==================

- Set up your working project directory into 2 sub folders: docker and html
- Checkout this repository into the docker directory
- Edit docker-composer.yml to suit your needs, defining which directories are shared with which containers and of course remember to include your chosen MySQL credentials.
- From the docker directory execute: ```docker-compose up -d apache2 mysql php-fpm redis```
- Import your database and configure Magento, referencing 'mysql' and 'redis' as the mysql and redis server hosts respectfully. Watch out for potential port conflicts if you have previously installed MySQL server using Homebrew etc.

Cleaning up
===========
You can stop and remove all containers easily using:
`docker rm $(docker ps --no-trunc -aq)`

Images can also be removed if needed using:
`docker rmi $(docker images -q)`

