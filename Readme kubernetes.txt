52.168.121.49 


40.117.169.4  ( installed docker engine)
docker / Docker@12345


52.234.142.248  ( trainer's master node)

sudo -i 
systemctl status docker
docker ps -a
docker images
docker info
docker inspect
docker pull mysql  ( from docker hub - registry)
docker search httpd --filter starts=3000
docker search nginx --limit=5 -f stars=50 -f is-official=true
docker rmi c899fcc3f3d8  ( remove image )
docker tag haproxy:latest hapoxy:chickenrice
docker rmi haproxy:chickenrice ( untag)

docker container create --name=hucklee httpd
docker start/stop/rm  pause/unpause container name

Web Site
docker run -d --name=hucklee2 httpd
docker inspect hucklee2 | grep -i ipaddr   --- curl 172.17.0.5

firewall --> iptables 
docker run -d --name=hucklee2-web1 -p 8080:80 httpd

docker exec -it hucklee2-web1 bash ( login into container )

docker rm -f $(docker ps -a -q) ---!!!!!remove all containers


SQL
docker run -d --name=hucklee-db1 -e MYSQL_ROOT_PASSWORD=123 -e MYSQL_DATABASE=spgroup mysql
mysql -u root -p  ( keyin password)
show databases;  ( check databases)
use spgroup
create table emp ( name varchar(20))
insert into emp values("sam")

mkdir /hucklee-db1
docker run -d --name=hucklee-db1 -v /hucklee-db1:/var/lib/mysql  -p 3308:3306 -e MYSQL_ROOT_PASSWORD=123 -e MYSQL_DATABASE=spgroup mysql  ---- bind/mount
mysql default port = 3306

docker volume create hucklee-db1
docker run -d --name=hucklee-db2 -v hucklee-db2:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=123 -e MYSQL_DATABASE=spgroup mysql 


Docker File  
FROM
MAINTAINER
LABEL
COPY
ENV -- container creation
ARG --- image creation

CMD  --- start service
ENTRYPOINT --- start service

Create image from docker file
docker build . -f one.df -t hucklee/spgroup:webserverv1.0
docker login
docker push hucklee/spgroup:webserverv1.0



