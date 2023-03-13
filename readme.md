
## Link do YouTube
Para o curso completo de 1 hora, assista ao youtube:
https://www.youtube.com/watch?v=6YZvp2GwT0A

# Instalação
## Crie a imagem do Jenkins BlueOcean Docker
```
docker build -t myjenkins-blueocean:2.332.3-1 .
```

## Criar a rede 'jenkins'
```
docker network create jenkins
```

## Execute o Container
### MacOS / Linux
```
docker run --name jenkins-blueocean --restart=on-failure --detach \
  --network jenkins --env DOCKER_HOST=tcp://docker:2376 \
  --env DOCKER_CERT_PATH=/certs/client --env DOCKER_TLS_VERIFY=1 \
  --publish 8080:8080 --publish 50000:50000 \
  --volume jenkins-data:/var/jenkins_home \
  --volume jenkins-docker-certs:/certs/client:ro \
  myjenkins-blueocean:2.332.3-1
```

### Windows
```
docker run --name jenkins-blueocean --restart=on-failure --detach `
  --network jenkins --env DOCKER_HOST=tcp://docker:2376 `
  --env DOCKER_CERT_PATH=/certs/client --env DOCKER_TLS_VERIFY=1 `
  --volume jenkins-data:/var/jenkins_home `
  --volume jenkins-docker-certs:/certs/client:ro `
  --publish 8080:8080 --publish 50000:50000 myjenkins-blueocean:2.332.3-1
```


## Obter a senha
```
docker exec jenkins-blueocean cat /var/jenkins_home/secrets/initialAdminPassword
```

## Conecte-se ao Jenkins
```
https://localhost:8080/
```

## Referência de instalação:
https://www.jenkins.io/doc/book/installing/docker/


## contêiner alpine/socat para encaminhar o tráfego do Jenkins para o Docker Desktop na máquina host

https://stackoverflow.com/questions/47709208/how-to-find-docker-host-uri-to-be-used-in-jenkins-docker-plugin
```
docker run -d --restart=always -p 127.0.0.1:2376:2375 --network jenkins -v /var/run/docker.sock:/var/run/docker.sock alpine/socat tcp-listen:2375,fork,reuseaddr unix-connect:/var/run/docker.sock
docker inspect <container_id> | grep IPAddress
```

## Usando meu agente Jenkins Python
```
docker pull devopsjourney1/myjenkinsagents:python
```
