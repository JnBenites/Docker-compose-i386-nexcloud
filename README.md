# docker-compose-i386-nexcloud
A simple docker-compose YML for  quickly running  on i368 machines

```
version: '2'
services:
  nextcloud:
    image: i386/nextcloud
    restart: always
    container_name: nextcloud
    hostname: nextcloud
    environment:
      - MYSQL_DATABASE=nextcloud
      - MYSQL_USER=user
      - MYSQL_PASSWORD=pass
      - MYSQL_HOST=mariadb-nextcloud
    depends_on:
      - mariadb-nextcloud
    ports:
      - 8081:80
    links:
      - mariadb-nextcloud
    volumes:
      - ./nextcloud/html/custom_apps:/var/www/html/custom_apps
      - ./nextcloud/html/config:/var/www/html/config
      - ./nextcloud/html/data:/var/www/html/data
      - ./nextcloud/html/themes:/var/www/html/themes
  mariadb-nextcloud:
    image: mariadb:10.0.35
    command: --transaction-isolation=READ-COMMITTED --binlog-format=ROW
    restart: always
    container_name: mariadb-nextcloud
    hostname: mariadb-nextcloud
    volumes:
      - ./nextcloud/mysql:/var/lib/mysql
    environment:
      - MYSQL_ROOT_PASSWORD=passroot
      - MYSQL_PASSWORD=pass
      - MYSQL_DATABASE=nextcloud
      - MYSQL_USER=user
```
