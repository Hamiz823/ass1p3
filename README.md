Assignment 1
Part#3

I#1:
viru@viru:~/Desktop/ass1p3$ sudo docker volume create my_volume
my_volume
viru@viru:~/Desktop/ass1p3$ sudo docker volume ls
DRIVER    VOLUME NAME
local     my_volume

I#2
viru@viru:~$ docker run -d -p 8080:80 -v my_volume:/usr/share/nginx/html nginx
706fbfdd1d75d1cd59610475545432948068ca3e5d2e6b2075b477299ab2fec4

 docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED         STATUS         PORTS                                   NAMES
706fbfdd1d75   nginx     "/docker-entrypoint.…"   5 minutes ago   Up 5 minutes   0.0.0.0:8080->80/tcp, :::8080->80/tcp   lucid_hofstadter


viru@viru:~$ nano index.html
viru@viru:~$ docker cp index.html lucid_hofstadter:/usr/share/nginx/html
Preparing to copy...
Copying to container - 2.048kB
Successfully copied 2.048kB to lucid_hofstadter:/usr/share/nginx/html


viru@viru:~$ docker stop lucid_hofstadter
lucid_hofstadter
viru@viru:~$ docker rm lucid_hofstadter
lucid_hofstadter


viru@viru:~$ docker run -d -p 8081:80 -v my_volume:/usr/local/apache2/htdocs httpd
Unable to find image 'httpd:latest' locally
latest: Pulling from library/httpd
f1f26f570256: Already exists
a6b093ae1967: Pull complete
6b400bbb27df: Pull complete
d9833ead928a: Pull complete
ace056404ed3: Pull complete
Digest: sha256:f3e9eb9acace5bbc13c924293d2247a65bb59b8f062bcd98cd87ee4e18f86733
Status: Downloaded newer image for httpd:latest
1c5d84a6eae0fd0108d61a31caa74b79624a12923f861626c779b7cea9038c6a

viru@viru:~$ docker ps
CONTAINER ID   IMAGE     COMMAND              CREATED         STATUS         PORTS                                   NAMES
1c5d84a6eae0   httpd     "httpd-foreground"   7 seconds ago   Up 5 seconds   0.0.0.0:8081->80/tcp, :::8081->80/tcp   relaxed_snyder

viru@viru:~$ nano about.html
viru@viru:~$ docker cp about.html relaxed_snyder:/usr/local/apache2/htdocs
Preparing to copy...
Copying to container - 2.048kB
Successfully copied 2.048kB to relaxed_snyder:/usr/local/apache2/htdocs


viru@viru:~$ docker stop relaxed_snyder
relaxed_snyder
viru@viru:~$ docker rm relaxed_snyder
relaxed_snyder


viru@viru:~$ docker run --rm -v my_volume:/data alpine ls -l /data
Unable to find image 'alpine:latest' locally
latest: Pulling from library/alpine
63b65145d645: Pull complete
Digest: sha256:ff6bdca1701f3a8a67e328815ff2346b0e4067d32ec36b7992c1fdc001dc8517
Status: Downloaded newer image for alpine:latest
total 12
-rw-r--r--    1 root     root           497 Dec 13 15:53 50x.html
-rw-rw-r--    1 1000     1000            16 Mar 26 17:52 about.html
-rw-rw-r--    1 1000     1000            29 Mar 26 17:27 index.html


viru@viru:~$ docker volume rm my_volume
my_volume
