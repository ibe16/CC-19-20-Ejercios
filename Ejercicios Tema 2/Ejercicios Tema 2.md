# Ejercicios del tema 2 

## Ejercicio 1
>Instalar alguno de los entornos virtuales de node.js (o de cualquier otro lenguaje con el que se esté familiarizado) y, con ellos, instalar la última versión existente, la versión minor más actual de la 4.x y lo mismo para la 0.11 o alguna impar (de desarrollo).

1. Descargar y ejecutar el ```install scrip```

```curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.0/install.sh | bash```

2. Verificar la instalación

```command -v nvm```

3. Usar ```nvm remote-ls``` para ver las versiones
4. Instalar las que interesen

```nvm install v12.13.0``` 

```nvm install v0.11.16 ```

## Ejercicio 2
> Crear una descripción del módulo usando package.json. En caso de que se trate de otro lenguaje, usar el método correspondiente.

1. Ejecutar ```npm init``` para crear un package.json por defecto.

```json
{
  "name": "Prueba",
  "version": "1.0.0",
  "description": "Package json de prueba para el ejercicio 2",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "repository": {
    "type": "git",
    "url": "https://github.com/ibe16/CC-19-20-Ejercicios"
  },
  "author": "@ibe16",
  "license": "ISC",
  "bugs": {
    "url": "https://github.com/ibe16/CC-19-20-Ejercicios/issues"
  },
  "homepage": "https://github.com/ibe16/CC-19-20-Ejercicios"
}
```

2. Vamos a añadir algunas dependencias al package.json
    1. ```npm install docco grunt-docco --save-dev```
    2. ``` npm install sqlite --save-dev```

3. Dependencias actuales
```json
  "devDependencies": {
    "docco": "^0.8.0",
    "grunt": "^1.0.4",
    "grunt-docco": "^0.5.0",
    "sqlite": "^3.0.3"
  }
```

## Ejercicio 3
> Descargar el repositorio de ejemplo anterior, instalar las herramientas necesarias (principalmente Scala y sbt) y ejecutar el ejemplo desde sbt. Alternativamente, buscar otros marcos para REST en Scala tales como Finatra o Scalatra y probar los ejemplos que se incluyan en el repositorio.

Seguimos las instrucciones que se proporcionan en el [repositorio](https://github.com/JJ/spray-test) y vemos que todo funciona, se ejecutan los test y se realizan algunos ejemplos de funcionamiento.

## Ejercicio 4
> Para la aplicación que se está haciendo, escribir una serie de aserciones y probar que efectivamente no fallan. Añadir tests para una nueva funcionalidad, probar que falla y escribir el código para que no lo haga. A continuación, ejecutarlos desde mocha (u otro módulo de test de alto nivel), usando descripciones del test y del grupo de test de forma correcta. Si hasta ahora no has subido el código que has venido realizando a GitHub, es el momento de hacerlo, porque lo vamos a necesitar un poco más adelante.

Como ejemplo se pueden consultar los [test](https://github.com/ibe16/CC-19-20-Proyecto/tree/master/tests) realizados para el microservicio ```Notifier```.

## Ejerucicio 5
>1. Darse de alta. Muchos están conectados con GitHub por lo que puedes usar directamente el usuario ahí. A través de un proceso de autorización, acceder al contenido e incluso informar del resultado de los tests.
>2. Activar el repositorio en el que se vaya a aplicar la integración continua. Travis permite hacerlo directamente desde tu configuración; en otros se dan de alta desde la web de GitHub.
>3. Crear un fichero de configuración para que se ejecute la integración y añadirlo al repositorio.

Después de darse de alta en TravisCI y activar la CI para el repositorio del proyecto, el archivo de configuración creado es el siguiente:
```yml
#Lenguaje de programación
language: python

#Distintas versiones para hacer la prueba
python:
  - "3.4"
  - "3.5"
  - "3.6"
  - "3.6.8" 
  - "3.7"
  - "3.8"
  - "3.8-dev"

#Instalar las dependencias necesarias
install:
  - pip install -r requirements.txt

#Ejecutar los test unitarios y de cobertura
script:
  - invoke test
  - invoke coverage

#Enviar resultados test de cobertura a codecov
after_success:
  - codecov
```
