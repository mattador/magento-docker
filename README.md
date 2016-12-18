Magento 1 and 2 Docker Development stack
========================================

I created this build in my quest to reduce the painful memory/cpu overhead I experienced while developing Magento 2 applications on a traditional Vagrant/VirtualBox stack.

There are plenty of Magento specific builds available on Docker Hub, but none of the ones I looked into included redis for session/cache storage which was critical for me.
 
Laradock actually fulfilled about 80% of what I wanted (albeit full of unnecessary bells and whistles), so it made sense to use it as a reference for my own trimmed down version.

The dev stack comprises of 4 Debian-based images:

-Apache
-MySQL 5.7
-Redis
-PHP 7 (with all Magento 1 and 2 required extensions)



Basic instructions
==================

I like to set up my working project directory into 2 sub folders:
-docker
-html

+Edit docker-composer.yml to suit your needs, defining which directories are shared with which containers and of course remember to include your chosen MySQL credentials.
+From the docker directory simple execute:
`docker-compose up -d apache2 mysql php-fpm redis`
+Import your database and then configure Magento, using 'mysql' and 'redis' as the mysql and redis server hosts respectfully. Watch out for potential port conflicts if you have installed MySQL server using Homebrew or other means.

Cleaning up
===========
You can stop and remove all containers easily using:
`docker rm $(docker ps --no-trunc -aq)`

Images can also be removed if needed using:
`docker rmi $(docker images -q)`

