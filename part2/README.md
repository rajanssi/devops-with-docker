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
