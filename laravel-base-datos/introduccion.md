# Curso de Laravel desde cero - Base de datos

![Fundamentos de base de datos](../assets/clase_08_01.jpg)

La capa de persistencia o almacenamiento de Datos es increíblemente importante en cualquier aplicación, ya que aquí estará guardada la información que dispone nuestra app.  Antes de iniciar con el manejo de base de datos con Laravel es necesario tener los siguientes fundamentos.

1. ¿Que es una base de datos?
2. ¿Bases de datos SQL y NoSQL?
3. ¿Bases de datos relacionales?
4.  ¿Que es un SGBD ó DBMS?
5. ¿Que es un ORM?

Estos conocimientos nos llevaran a una mejor productividad a la hora de trabajar con los diferentes gestores de base de datos con laravel, en este curso usaremos MySQL, PostgresSQL y MongoDB. 

## ¿Que es una base de datos?

_**Disclaimer:**_ Este curso no pretende ser un curso de base de datos definitivo, pero veremos ciertos aspectos fundamentales que son necesarios para el trabajo con este framework.

Una base de datos es un conjunto de información organizada, de un mismo contexto, estructurados y que están almacenados para su posterior uso. 

Existen diferentes tipos de base de datos, entre los mas comunes están las relacionales o SQL, y las bases de datos NoSQL o no relacionales.

## Bases de datos relacionales

Las bases de datos relacionales son aquellas que como su nombre lo indica utiliza un esquema basado en relaciones entre entidades a las cuales se les denomina tablas, conformadas por filas, llamadas registros y columnas, llamadas campos. Y que hoy en día son ampliamente usadas por su consistencia, estructura, perfectas para transacciones, atomicidad, madurez y sobre todo por su fácil aplicación en casi cualquier problema. 

## Bases de datos no relacionales (NoSQL)

Las bases de datos NoSQL, a diferencia de su contraparte no se basan únicamente en tablas, sino en colecciones, documentos, clave-valor, multivalor, grafos, etc. Hoy en día han alcanzado gran popularidad por su escalibilidad, usos en Big Data, versatilidad pero menos maduro y probado que las relacionales.

## ¿Qué es un sistema SGBD?

Si bien un Sistema gestor de base de datos no es un BD en si, van de la mano ya que es un software que nos permite administrar, almacenar y manipular nuestras bases de datos. Además nos brinda características como seguridad, gestión de roles, manejo de concurrencia, capacidad de acceso, etc.

Entre los mas populares tenemos:

### RDBMS o Sistemas gestores de base de datos relacionales

1. MySQL
2. PostgresSQL
3. Oracle DB
4. SQL Server
5. DB2
6. SQLite

### NoSQL DBMS

1. MongoDB
2. Cassandra
3. Neo4j
4. Redis

##  ¿Qué es un ORM?

Normalmente al usar un framework de backend, estos nos proporcionan diversas opciones para el trabajo con las bases de datos, un ejemplo de ello son los ORM (Object Relational Mapping), el cual nos permite el uso de los diversos métodos como  SELECT, INSERT, UPDATE y DELETE, sin la necesidad de usar SQL, solo una capa de interfaz orientada o objetos que permite una mayor legibilidad. En laravel usamos **Eloquent**.



