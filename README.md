# Basic Docker Commands


## Remove all containers
* Ubuntu
```
docker rm -f $(docker ps -a -q)
```

* Window
```
$containers = docker ps -a -q
foreach ($container in $containers) { docker rm $container -f }
```

## Remove all images unused
```
docker image prune -a
```

## Remove all images
* Ubuntu
```
docker rmi -f $(docker images -q)
```

* Window
```
$images = docker images -a -q
foreach ($image in $images) { docker image rm $image -f }
```

## Save docker images and load docker images from file .tar
```
docker save -o [path]/<file_name>.tar images_name:tag new_images_name:tag

docker load -i [path]/<file_name>.tar
```

## Search an image 
```
docker search <key>
```

## Build an image from container
```
docker commit [OPTIONS] CONTAINER [REPOSITORY[:TAG]]

docker commit -m "upload" c3f279d17e0a  <your_docker_hub>/new-repo:tagname

docker push <your_docker_hub>/new-repo:tagname
```

## Push an Image to docker hub
```
docker push IMAGE [REPOSITORY[:TAG]]

docker tag local-image:tagname new-repo:tagname

docker push <your_docker_hub>/new-repo:tagname
```

## Pull an image
```
docker pull <repository>
```

## Run an image as container
```
docker run [OPTIONS] IMAGE [COMMAND] [ARG...]

docker run --name=mysqlCon -p 3306:3306 -d -e MYSQL_ROOT_HOST=% -e MYSQL_ROOT_PASSWORD=123456 mysql/mysql-server:5.7
```

## Show logs a container
```
docker logs [container name]
```

## SH into a container
```
docker exec [OPTIONS] CONTAINER COMMAND [ARG...]

sudo docker exec -it <container_id> sh

sudo docker exec -it mysqlCon mysql -uroot -p
```

## Remove an Image
```
docker rmi [OPTIONS] IMAGE [IMAGE...]

docker rmi -f <your_docker_hub>/test:v1
```

## Show containers
```
docker ps # containers are running

docker ps -a # show all
```

## Stop/Start/Restart/Remove a container
```
docker container start/stop/restart/rm [container id]
```

## Stop/remove all containers
```
docker stop/rm $(docker ps -a -q)
```

## Remove all Images
```
docker rmi -f $(docker images -a -q)
```

#  Volume commands

## Basic command
```
docker volume create [volume name]      T???o m???ng m???i
docker volume inspect  [volume name]    Xem chi ti???t m???ng
docker volume ls                        Hi???n th??? nh???ng m???ng ??ang c??
docker volume rm     [volume name]      X??a volume
docker volume prune                     X??a to??n b??? volumn
```

## Tao mot volume mysql_data sau do tao mot container mysql luu du lieu vao day
```
docker volume create mysql_data
docker container run --name mysql -v mysql_data:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=123456 -p 3306:3306 -d mysql:5.7
```

#  Networks

## Basic command
```
docker network create       [nerwork name]       T???o m???ng m???i
docker network inspect      [nerwork name]       Xem chi ti???t m???ng
docker network ls                                Hi???n th??? nh???ng m???ng ??ang c??
docker network rm           [nerwork name]       X??a m???ng
docker network prune                             X??a ?????ng lo???t c??c m???ng kh??ng s??? d???ng
docker network connect      [nerwork name]       T???o k???t n???i m???ng
docker network disconnect   [nerwork name]       Ng???t k???t n???i m???ng
```

## T???o 1 m???ng l???p C, tao 2 container su dung lop mang do, roi kiem tra ket noi giua 2 con container
```
docker network create --subnet 192.168.1.0/24 network1
docker run -itd --name=container1  --network network1 busybox
docker run -itd --name=container2  --network network1 busybox

docker attach container1
ping 192.168.1.3
```
