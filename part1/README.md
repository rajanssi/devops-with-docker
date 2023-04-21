**Exercise 1.1**

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

**Exercise 1.2**

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

**Exercise 1.3**
```console
rajanssi@lx0-fuxi089:~/devops/part1$ docker run -it -d devopsdockeruh/simple-web-service:ubuntu
rajanssi@lx0-fuxi089:~$ docker container ls
CONTAINER ID   IMAGE                                      COMMAND                 CREATED         STATUS         PORTS     NAMES
66558655fb17   devopsdockeruh/simple-web-service:ubuntu   "/usr/src/app/server"   8 seconds ago   Up 7 seconds             exciting_jackson
rajanssi@lx0-fuxi089:~$ docker exec -it exciting_jackson bash
root@66558655fb17:/usr/src/app# ls
server  text.log
root@66558655fb17:/usr/src/app# tail -f ./text.log 
2023-04-18 09:01:43 +0000 UTC
Secret message is: 'You can find the source code here: https://github.com/docker-hy'
```

**Exercise 1.4**
```console
rajanssi@lx0-fuxi089:~$ docker run -d ubuntu sh -c "while true; do echo 'Input website:'; read website; echo 'Searching..'; sleep 1; curl http://helsinki.fi  ; done"
rajanssi@lx0-fuxi089:~$ docker container ls
CONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS          PORTS     NAMES
994100d45567   ubuntu    "sh -c 'while true; …"   55 seconds ago   Up 54 seconds             angry_davinci
rajanssi@lx0-fuxi089:~$ docker exec -it angry_davinci bash
root@994100d45567:/# apt-get -y update; apt-get -y install curl
...
root@994100d45567:/# exit
rajanssi@lx0-fuxi089:~$ docker attach angry_davinci
Input website:
Searching..
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   169  100   169    0     0   7058      0 --:--:-- --:--:-- --:--:--  7347
<html>
<head><title>301 Moved Permanently</title></head>
<body>
<center><h1>301 Moved Permanently</h1></center>
<hr><center>nginx/1.20.1</center>
</body>
</html>

```

**Exercise 1.5**
```console
rajanssi@lx0-fuxi089:~$ docker run -d devopsdockeruh/simple-web-service:alpine
Unable to find image 'devopsdockeruh/simple-web-service:alpine' locally
alpine: Pulling from devopsdockeruh/simple-web-service
ba3557a56b15: Pull complete 
1dace236434b: Pull complete 
4f4fb700ef54: Pull complete 
Digest: sha256:dd4d367476f86b7d7579d3379fe446ae5dfce25480903fb0966fc2e5257e0543
Status: Downloaded newer image for devopsdockeruh/simple-web-service:alpine
0b54c9b572cad154e97b872ee64d67d106d0a5a278017c9083631252e8c8a769
rajanssi@lx0-fuxi089:~$ docker container ls
CONTAINER ID   IMAGE                                      COMMAND                 CREATED         STATUS         PORTS     NAMES
0b54c9b572ca   devopsdockeruh/simple-web-service:alpine   "/usr/src/app/server"   8 seconds ago   Up 7 seconds             relaxed_mcclintock
rajanssi@lx0-fuxi089:~$ docker images
REPOSITORY                          TAG       IMAGE ID       CREATED       SIZE
ubuntu                              latest    08d22c0ceb15   6 weeks ago   77.8MB
devopsdockeruh/simple-web-service   ubuntu    4e3362e907d5   2 years ago   83MB
devopsdockeruh/simple-web-service   alpine    fd312adc88e0   2 years ago   15.7MB
rajanssi@lx0-fuxi089:~$ docker exec -it relaxed_mcclintock sh
/usr/src/app # ls
server    text.log
/usr/src/app # tail -f ./text.log 
Secret message is: 'You can find the source code here: https://github.com/docker-hy'
```

**Exercise 1.6**
```console
rajanssi@lx0-fuxi089:~$ docker run -it devopsdockeruh/pull_exercise
Unable to find image 'devopsdockeruh/pull_exercise:latest' locally
latest: Pulling from devopsdockeruh/pull_exercise
8e402f1a9c57: Pull complete 
5e2195587d10: Pull complete 
6f595b2fc66d: Pull complete 
165f32bf4e94: Pull complete 
67c4f504c224: Pull complete 
Digest: sha256:7c0635934049afb9ca0481fb6a58b16100f990a0d62c8665b9cfb5c9ada8a99f
Status: Downloaded newer image for devopsdockeruh/pull_exercise:latest
Give me the password: basics
You found the correct password. Secret message is:
"This is the secret message"
```

**Exercise 1.7**
```dockerfile
FROM ubuntu:20.04

WORKDIR /usr/src/app

COPY curler.sh .

RUN apt-get update && apt-get install -y curl

CMD ./curler.sh
```

**Exercise 1.8**
```Dockerfile
FROM devopsdockeruh/simple-web-service:alpine

CMD server
```
