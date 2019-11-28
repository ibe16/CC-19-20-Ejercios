# Ejercicios Tema 3

## Ejercicio 1
> Buscar alguna demo interesante de Docker y ejecutarla localmente, o en su defecto, ejecutar la imagen anterior y ver cómo funciona y los procesos que se llevan a cabo la primera vez que se ejecuta y las siguientes ocasiones.

Se ha ejecutado la imagen que se proporciona de ejemplo. La primera vez que la ejecutamos obtenemos la siguiente salida:

```bash
irene@irene:~$ docker run --rm jjmerelo/docker-daleksay -f smiling-octopus Hola
Unable to find image 'jjmerelo/docker-daleksay:latest' locally
latest: Pulling from jjmerelo/docker-daleksay
0a8490d0dfd3: Pull complete 
aac9fee8ebfb: Pull complete 
c951ce7a8ac7: Pull complete 
ab590fdbfbc0: Pull complete 
08ad84f33a7b: Pull complete 
Digest: sha256:9e2b66e742f80dd7422e48d69c0cf9a01afc9c2d50a6c2185fd37c3519a984ff
Status: Downloaded newer image for jjmerelo/docker-daleksay:latest

```
Lo que quiere decir que:
1. No encuentra la imagen localmente
2. Usamos el tag por defecto `latest` por lo que se descarga la última versión disponible
3. Hace un pull del repositorio ```jjmerelo/docker-daleksay``` alojado en DockerHub
4. Se descarga la nueva imagen
5. Se ejecuta

Cuando la ejecutamos una segunda vez simplemente se muestra la salida del programa, en este caso el pulpo diciendo algo.

## Ejercicio 2
> Tomar algún programa simple, “Hola mundo” impreso desde el intérprete de línea de órdenes, y comparar el tamaño de las imágenes de diferentes sistemas operativos base, Fedora, CentOS y Alpine, por ejemplo.

```bash

REPOSITORY                 TAG                 IMAGE ID            CREATED             SIZE

fedora                     latest              f0858ad3febd        4 weeks ago         194MB
alpine                     latest              965ea09ff2eb        5 weeks ago         5.55MB
centos                     latest              0f3e07c0138f        8 weeks ago         220MB

```

Podemos ver que la imagen de `Alpine` es la más pequeña de todas. De hecho, en su repositorio de DockerHub pone:
> Alpine Linux is a Linux distribution built around musl libc and BusyBox. The image is only 5 MB in size and has access to a package repository that is much more complete than other BusyBox based images. This makes Alpine Linux a great image base for utilities and even production applications. Read more about Alpine Linux here and you can see how their mantra fits in right at home with Docker images.

Es decir, tiene lo mínimo y necesario para funcionar, está pensada para ser pequeña y eficiente.

## Ejercicio 3
> Crear a partir del contenedor anterior una imagen persistente con commit.

Haremos commit a partir del contenedor de `centos` anterior.

```bash
$ docker commit b51da1a69915 centos-prueba
sha256:b9639820f364bdef6b372e743e4d352ade2302e7636c8653f015872d0093ba58

$ docker images
REPOSITORY                 TAG                 IMAGE ID            CREATED             SIZE
centos-prueba              latest              b9639820f364        14 seconds ago      220MB
```

## Ejercicio 4
> Examinar la estructura de capas que se forma al crear imágenes nuevas a partir de contenedores que se hayan estado ejecutando.

Capas de la imagen del ejercicio anterior `centos-prueba` creada a partir de la imagen base de `centos`.

```json
"rootfs": {
    "type": "layers",
    "diff_ids": [
      "sha256:9e607bb861a7d58bece26dd2c02874beedd6a097c1b6eca5255d5eb0d2236983",
      "sha256:3245ce9924174a4e549201eacbd60ed23b123db8d099819f15f3c584e6069b0f"
    ]
  }

```

## Ejercicio 5
> Crear un volumen y usarlo, por ejemplo, para escribir la salida de un programa determinado.

```bash
$ docker volume create test-volume
test-volume
$ docker run -it --rm -v test-volume:/prueba centos /bin/bash
[root@472bb9a34052 /]# ls -R / | wc
  95935   89275 1358292
[root@472bb9a34052 /]# exit
$ docker volume inspect test-volume
[
    {
        "CreatedAt": "2019-11-27T03:08:56+01:00",
        "Driver": "local",
        "Labels": {},
        "Mountpoint": "/var/lib/docker/volumes/test-volume/_data",
        "Name": "test-volume",
        "Options": {},
        "Scope": "local"
    }
]

```

## Ejercicio 6
> Usar un miniframework REST para crear un servicio web y introducirlo en un contenedor, y componerlo con un cliente REST que sea el que finalmente se ejecuta y sirve como “frontend”.


## Ejercicio 7
> Reproducir los contenedores creados anteriormente usando un Dockerfile.

## Ejercicio 8
> Crear con docker-machine una máquina virtual local que permita desplegar contenedores y ejecutar en él contenedores creados con antelación.