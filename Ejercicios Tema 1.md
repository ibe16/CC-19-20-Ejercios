# Ejercicios del tema 1 

## Ejercicio 1
> *Buscar una aplicación de ejemplo, preferiblemente propia, y deducir qué patrón es el que usa. ¿Qué habría que hacer para evolucionar a un patrón tipo microservicios?*

En la asignatura DGP (Dirección y Gestión de Proyectos) se realizó una página web y una aplicación Android, cuyo objetivo era mostrar rutas con itirenarios accesibles para los usuarios. Las funciones principales son: mostrar la ruta en un mapa, gestionar rutas (añadir/eliminar) y proporcionar loggin a los usuarios. 

Como arquitectura se uso MVC (Modelo Vista Controlador), aunque debido a las tecnologías que se estaban usando (Firebase y Node.js) quedaba bastante solapados los modelos y el controlador, casi eran lo mismo.

Usando una arquitectura basada en microservicios se habría aprovechado mejor la potencia que ofrece Firebase:
- Microservicio que se encargase de los usuarios 
- Microservicio que gestionase las rutas
- Microservicio que haga el mapa a partir de una ruta
- Microservicio que gestionase el loggin y los tokens asociados a estos


## Ejercicio 2
> *En la aplicación que se ha usado como ejemplo en el ejercicio anterior, ¿podría usar diferentes lenguajes? ¿Qué almacenes de datos serían los más convenientes?*

1. Para cada microservicio se podría haber usado un lenguaje diferente.
2. Como almacén de datos se usó Firebase, que es una base de datos no relacional, ya que ofrece características implimentadas como loggin, notificaciones, notificaciones push, sin necesidad de implementarlas, a parte de un dominio para tu página web. Esto es muy cómodo para desarrollar sitios web rápidamente, pero te deja un poco a merced de sus funcionalidades. Siguiendo la arquitectura de microservicios habría usado una base de datos no relacional, como MongoDB, para almacenar las rutas y sus puntos y una base de datos relacional para los usuarios.


