**Exercise 2.1**

```yml
version: '3.8'

services:
    simple-web-service:
      image: devopsdockeruh/simple-web-service
      build: .
      volumes:
        - ./text.log:/usr/src/app/text.log
      container_name: simple-web-service
```

**Exercise 2.2**

```yml
version: '3.8'

services:
    simple-web-service:
      image: devopsdockeruh/simple-web-service
      build: .
      ports:
        - 8080:8080
      command: ["server"]
      container_name: simple-web-service
```

**Exercise 2.3**
```yml
version: '3.8'

services:
    example-frontend:
      image: example-frontend
      ports:
        - 5000:5000
      command: ["serve", "-s", "-l", "5000", "build"]
      container_name: frontend

    example-backend:
      image: example-backend
      ports:
        - 8080:8080
      environment:
        - REQUEST_ORIGIN=http://localhost:5000
      command: ./server
      container_name: backend
```

**Exercise 2.4**
```yml
version: '3.8'

services:
    example-frontend:
      image: example-frontend
      ports:
        - 5000:5000
      command: ["serve", "-s", "-l", "5000", "build"]
      container_name: frontend

    example-backend:
      image: example-backend
      ports:
        - 8080:8080
      environment:
        - REQUEST_ORIGIN=http://localhost:5000
        - REDIS_HOST=redis
      command: ./server
      container_name: backend

    redis:
      image: redis
      container_name: redis
```

**Exercise 2.5**
```console
rajanssi@lx0-fuxi089:~$ docker compose up --scale compute=3
```

**Exercise 2.6**
```yml
version: '3.8'

services:
    example-frontend:
      image: example-frontend
      ports:
        - 5000:5000
      command: ["serve", "-s", "-l", "5000", "build"]
      container_name: frontend

    example-backend:
      image: example-backend
      ports:
        - 8080:8080
      environment:
        - REQUEST_ORIGIN=http://localhost:5000
        - REDIS_HOST=redis
        - POSTGRES_HOST=postgres
        - POSTGRES_USER=postgres
        - POSTGRES_PASSWORD=postgres
        - POSTGRES_DATABASE=postgres
      command: ./server
      container_name: backend

    redis:
      image: redis
      container_name: redis

    postgres:
      image: postgres:13.2-alpine
      restart: unless-stopped
      environment:
        POSTGRES_PASSWORD: postgres
      container_name: postgres
```
**Exercise 2.7**
```yml
version: '3.8'

services:
    example-frontend:
      image: example-frontend
      ports:
        - 5000:5000
      command: ["serve", "-s", "-l", "5000", "build"]
      container_name: frontend

    example-backend:
      image: example-backend
      ports:
        - 8080:8080
      environment:
        - REQUEST_ORIGIN=http://localhost:5000
        - REDIS_HOST=redis
        - POSTGRES_HOST=postgres
        - POSTGRES_USER=postgres
        - POSTGRES_PASSWORD=postgres
        - POSTGRES_DATABASE=postgres
      command: ./server
      container_name: backend

    redis:
      image: redis
      container_name: redis

    postgres:
      image: postgres:13.2-alpine
      restart: unless-stopped
      environment:
        POSTGRES_PASSWORD: postgres
      container_name: postgres
      volumes:
      - type: bind
        source: ./database
        target: /var/lib/postgresql/data

volumes:
  database:
```

**Exercise 2.8**
```yml
version: '3.8'

services:
    example-frontend:
      image: example-frontend
      ports:
        - 5000:5000
      command: ["serve", "-s", "-l", "5000", "build"]
      container_name: frontend

    example-backend:
      image: example-backend
      ports:
        - 8080:8080
      environment:
        - REDIS_HOST=redis
        - POSTGRES_HOST=postgres
        - POSTGRES_USER=postgres
        - POSTGRES_PASSWORD=postgres
        - POSTGRES_DATABASE=postgres
      command: ./server
      container_name: backend

    proxy:
      image: nginx:latest
      volumes:
        - type: bind
          source: ./nginx.conf
          target: /etc/nginx/nginx.conf
      ports:
        - 80:80
      container_name: proxy

    redis:
      image: redis
      container_name: redis

    postgres:
      image: postgres:13.2-alpine
      restart: unless-stopped
      environment:
        POSTGRES_PASSWORD: postgres
      container_name: postgres
      volumes:
      - type: bind
        source: ./database
        target: /var/lib/postgresql/data
```

**Exercise 2.9**
Backend REQUEST_ORIGIN was changed from http://localhost:5000 to http://localhost.

Backend:
```Dockerfile
FROM golang:1.16

EXPOSE 8080

WORKDIR /usr/src/app

COPY . .

RUN go build

ENV REQUEST_ORIGIN=http://localhost

CMD ["./server"]
```
Frontend:
```Dockerfile
FROM node:16

EXPOSE 5000

WORKDIR /usr/src/app

COPY . .

RUN npm install

RUN REACT_APP_BACKEND_URL=http://localhost:8080 npm run build

RUN npm install -g serve

CMD ["serve", "-s", "-l", "5000", "build"]
```
Compose:
```yml
version: '3.8'

services:
    example-frontend:
      image: example-frontend
      ports:
        - 5000:5000
      command: ["serve", "-s", "-l", "5000", "build"]
      container_name: frontend

    example-backend:
      image: example-backend
      ports:
        - 8080:8080
      environment:
        - REDIS_HOST=redis
        - POSTGRES_HOST=postgres
        - POSTGRES_USER=postgres
        - POSTGRES_PASSWORD=postgres
        - POSTGRES_DATABASE=postgres
      command: ./server
      container_name: backend

    proxy:
      image: nginx:latest
      volumes:
        - type: bind
          source: ./nginx.conf
          target: /etc/nginx/nginx.conf
      ports:
        - 80:80
      container_name: proxy

    redis:
      image: redis
      container_name: redis

    postgres:
      image: postgres:13.2-alpine
      restart: unless-stopped
      environment:
        POSTGRES_PASSWORD: postgres
      container_name: postgres
      volumes:
      - type: bind
        source: ./database
        target: /var/lib/postgresql/data
```

** Exercise 2.10 **
Compose:
```yml
version: '3.8'

services:
    example-frontend:
      image: example-frontend
      command: ["serve", "-s", "-l", "5000", "build"]
      container_name: frontend

    example-backend:
      image: example-backend
      environment:
        - REDIS_HOST=redis
        - POSTGRES_HOST=postgres
        - POSTGRES_USER=postgres
        - POSTGRES_PASSWORD=postgres
        - POSTGRES_DATABASE=postgres
      command: ./server
      container_name: backend

    proxy:
      image: nginx:latest
      volumes:
        - type: bind
          source: ./nginx.conf
          target: /etc/nginx/nginx.conf
      ports:
        - 80:80
      container_name: proxy

    redis:
      image: redis
      container_name: redis

    postgres:
      image: postgres:13.2-alpine
      restart: unless-stopped
      environment:
        POSTGRES_PASSWORD: postgres
      container_name: postgres
      volumes:
      - type: bind
        source: ./database
        target: /var/lib/postgresql/data
```
Frontend:
```Dockerfile
FROM node:16

EXPOSE 5000

WORKDIR /usr/src/app

COPY . .

RUN npm install

RUN REACT_APP_BACKEND_URL=http://localhost/api npm run build

RUN npm install -g serve

CMD ["serve", "-s", "-l", "5000", "build"]
```

```console
rajanssi@DESKTOP-CPO38BA:~/devops-with-docker/part2$ docker run -it --rm --network host networkstatic/nmap localhost
Starting Nmap 7.92 ( https://nmap.org ) at 2023-06-11 18:51 UTC
Nmap scan report for localhost (127.0.0.1)
Host is up (0.0000020s latency).
Not shown: 999 closed tcp ports (reset)
PORT   STATE SERVICE
80/tcp open  http

Nmap done: 1 IP address (1 host up) scanned in 0.17 seconds
```
