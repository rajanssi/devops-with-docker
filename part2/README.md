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
