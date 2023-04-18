**Exercise 1**

```console
rajanssi@lx0-fuxi089:~$ docker container run -d nginx
04697c49009a57ef9356c497e72cd07e4e98904388599d19bd851a5164a0350f
rajanssi@lx0-fuxi089:~$ docker container run -d nginx
f039b1fde6ac51dc3303ff04be29ffcf23b2c946d31e84233cbe41409d35fb79
rajanssi@lx0-fuxi089:~$ docker container run -d nginx
0f667cdb0f5a50ada9bb51ffdd1325682a6ee3fef6964e79d92a39448059daf8
rajanssi@lx0-fuxi089:~$ docker container stop practical_mayer
practical_mayer
rajanssi@lx0-fuxi089:~$ docker container stop eager_panini
eager_panini
rajanssi@lx0-fuxi089:~$ docker ps -a
CONTAINER ID   IMAGE                            COMMAND                  CREATED              STATUS                       PORTS     NAMES
0f667cdb0f5a   nginx                            "/docker-entrypoint.…"   About a minute ago   Up About a minute            80/tcp    silly_aryabhata
f039b1fde6ac   nginx                            "/docker-entrypoint.…"   About a minute ago   Exited (0) 16 seconds ago              practical_mayer
04697c49009a   nginx                            "/docker-entrypoint.…"   About a minute ago   Exited (0) 10 seconds ago              eager_panini
```

**Exercise 2**

```console
rajanssi@lx0-fuxi089:~$ docker images
nginx                               latest         6efc10a0510f   6 days ago      142MB
rajanssi@lx0-fuxi089:~/devops/part1$ docker stop silly_aryabhata
rajanssi@lx0-fuxi089:~/devops/part1$ docker rm silly_aryabhata
rajanssi@lx0-fuxi089:~/devops/part1$ docker rmi nginx:latest
rajanssi@lx0-fuxi089:~/devops/part1$ docker ps -a
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
rajanssi@lx0-fuxi089:~/devops/part1$ docker images
REPOSITORY   TAG       IMAGE ID   CREATED   SIZE
```
