# Get Bitnami Docker Image for Wordpress
**The recommended way to get the Bitnami WordPress Docker Image is to pull the prebuilt image from the [Docker Hub Registry](https://hub.docker.com/r/bitnami/wordpress).**

`$ docker pull bitnami/wordpress:latest`

**WordPress requires access to a MySQL or MariaDB database to store information. We'll use the Bitnami [Docker Image for MariaDB](https://github.com/bitnami/bitnami-docker-mariadb) for the database requirements.**

`$ docker pull bitnami/mariadb:latest`
# Deploy wordpess using command line
## 1. Create a network
`$ docker network create wordpress-network`

## 2. Create a volume for MariaDB persistence and create a MariaDB container
```
$ docker volume create --name mariadb_data
$ docker run -d --name mariadb \
  --env ALLOW_EMPTY_PASSWORD=yes \
  --env MARIADB_USER=bn_wordpress \
  --env MARIADB_PASSWORD=bitnami \
  --env MARIADB_DATABASE=bitnami_wordpress \
  --network wordpress-network \
  --volume mariadb_data:/bitnami/mariadb \
  bitnami/mariadb:latest
  ```
## 3. Create volumes for WordPress persistence and launch the container
```
$ docker volume create --name wordpress_data
$ docker run -d --name wordpress \
  -p 8080:8080 -p 8443:8443 \
  --env ALLOW_EMPTY_PASSWORD=yes \
  --env WORDPRESS_DATABASE_USER=bn_wordpress \
  --env WORDPRESS_DATABASE_PASSWORD=bitnami \
  --env WORDPRESS_DATABASE_NAME=bitnami_wordpress \
  --network wordpress-network \
  --volume wordpress_data:/bitnami/wordpress \
  bitnami/wordpress:latest
  ```
  **Now access your application at [https://localhost:8080](https://localhost:8080).**
  
  .<img src="https://scontent.fhan7-1.fna.fbcdn.net/v/t1.15752-9/181499973_842458792974083_6964058063707845327_n.png?_nc_cat=108&ccb=1-3&_nc_sid=ae9488&_nc_ohc=iTVRtQZhbiAAX-6gkeM&_nc_ht=scontent.fhan7-1.fna&oh=2ce0285a0ad672aad0099143db626991&oe=60B9DCD8">
  
  .<img src="https://scontent.fhan7-1.fna.fbcdn.net/v/t1.15752-9/183563557_1079971399499803_1196905899305648690_n.png?_nc_cat=107&ccb=1-3&_nc_sid=ae9488&_nc_ohc=4vfaeXezZbYAX9oSvMk&_nc_ht=scontent.fhan7-1.fna&oh=5ec650d520adbc2f5ecc513d728271a1&oe=60B93A0E">
  
# Deploy wordpress using Docker Compose
**We can run the application in a more convenient way with Docker Compose.**

**The main folder of this repository contains a functional `docker-compose.yml` file. Run the application using it as shown below:**
```
$ sudo apt install docker-compose
$ curl -sSL https://raw.githubusercontent.com/bitnami/bitnami-docker-wordpress/master/docker-compose.yml > docker-compose.yml
$ docker-compose up -d
```
.<img src="https://scontent-hkt1-2.xx.fbcdn.net/v/t1.15752-9/181616110_303527351370295_6971320746211948841_n.png?_nc_cat=111&ccb=1-3&_nc_sid=ae9488&_nc_ohc=kVMFrYythYoAX-sroTO&_nc_ht=scontent-hkt1-2.xx&oh=ded591d4b0be743d97e387e3a42558e6&oe=60BB5386">

.<img src="https://scontent-hkt1-2.xx.fbcdn.net/v/t1.15752-9/180944518_472783833951499_1829735941912541210_n.png?_nc_cat=101&ccb=1-3&_nc_sid=ae9488&_nc_ohc=Ji3Vtd-2aEIAX-EQaN8&tn=epQACHfbLqjx0qY6&_nc_ht=scontent-hkt1-2.xx&oh=b41b2c2bd6b823665a5b0bddcd818275&oe=60B9B622">

# Deploy wordpress on 2 VMs
`Đang cập nhật và bổ sung`
