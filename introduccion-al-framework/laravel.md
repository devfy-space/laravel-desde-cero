# Introducción a Laravel

![Laravel introducción al framework - Clase 01 DevFY](https://i.imgur.com/7AeMIhV.jpeg)
<p align="center">
<a href="https://travis-ci.org/laravel/framework"><img src="https://travis-ci.org/laravel/framework.svg" alt="Build Status"></a>
<a href="https://packagist.org/packages/laravel/framework"><img src="https://poser.pugx.org/laravel/framework/d/total.svg" alt="Total Downloads"></a>
<a href="https://packagist.org/packages/laravel/framework"><img src="https://poser.pugx.org/laravel/framework/v/stable.svg" alt="Latest Stable Version"></a>
<a href="https://packagist.org/packages/laravel/framework"><img src="https://poser.pugx.org/laravel/framework/license.svg" alt="License"></a>
</p>

## ¿Que es Laravel?

Laravel es un framework de PHP de codigo abierto creado en el año 2011, catalogado como uno de los mas populares de este año gracias a su facilidad de crear aplicaciones web del lado del backend. Su filosofía es desarrollar código PHP de forma elegante y simple, evitando el "código espagueti".

Laravel intenta eliminar el dolor del desarrollo al facilitar las tareas comunes utilizadas en la mayoría de los proyectos web, como la autenticación, el enrutamiento, las sesiones y el almacenamiento en caché.

## ¿Que es MVC?

Modelo Vista Controlador (MVC) es un estilo de arquitectura de software que separa los datos de una aplicación, la interfaz de usuario, y la lógica de control en tres componentes distintos.

![MVC Architecture](https://upload.wikimedia.org/wikipedia/commons/thumb/a/a0/MVC-Process.svg/1200px-MVC-Process.svg.png)

## ¿Es laravel realmente un framework MVC?

![is really laravel a mvc framework?](https://media-exp1.licdn.com/dms/image/C4E12AQGfyC3OsY3-rg/article-inline_image-shrink_1000_1488/0?e=1601510400&v=beta&t=yGlv438Yrty5TX2-zWXsWP09bFIlzkOcwExRREuLeSA)

Laravel no es un framework MVC, de hecho dejo de serlo hace mucho. [Taylor Otwell](https://twitter.com/taylorotwell?lang=es) el creador de este framework afirma que: 
> "No hay forma de encapsular todos los aspectos de las aplicaciones web robustas en esas 3 letras". ![Taylor Otwell](https://media-exp1.licdn.com/dms/image/C4E12AQEFtWfKmAriPQ/article-inline_image-shrink_1000_1488/0?e=1601510400&v=beta&t=gtZ2lXRCccA05DUBOESyjVSh-2s7I-y-41V4DVkBllc)

Fuente: [Laravel no es MVC](https://www.linkedin.com/pulse/why-laravel-mvc-framework-you-should-forget-kali-dass#:~:text=In%20fact%20although%20Laravel%204,most%20sense%20for%20your%20project.)

## Laravel Vs Symfony
  Mucha gente habla de cual es la diferencia entre estos dos frameworks, cuando en realidad Laravel utilizan varios componentes claves del core de este framework

### Componentes de Symfony usados en Laravel:
  1.  **Cache**
  2.  **Console**
  3.  **ErrorHandler**
  4.  **Filesystem**
  5.  **Finder**
  6.  **HttpFoundation**
  7.  **HttpKernel**
  8.  **Intl**
  9.  **Mime**
  10. **Process**
  11. **Routing**
  12. **VarDumper**

  Fuente: [Proyectos que usan Symfony](https://symfony.com/projects/laravel)

  Sin embargo si hay ciertas diferencias entre las que pueden destacar:

| Diferencia      | Laravel                                 | Symfony                                                      |
| --------------- | --------------------------------------- | ------------------------------------------------------------ |
| ORM             | Eloquent                                | Doctrine                                                     |
| Template Engine | Blade                                   | Twig                                                         |
| Databases       | MySQL, PostgreSQL, SQLite, SQLServer    | MySQL, Oracle, Drizzle, SQLServer, PostgreSQL, SQLite, SAP Sybase SQL Anywhere |
| Ventajas        | Desarrollo rapido y facil de configurar | Framework Robusto y mas usado en entornos enterprise         |


  Fuente: [Stackshare - Diferencias entre laravel y symfony](https://stackshare.io/stackups/laravel-vs-symfony#:~:text=According%20to%20the%20StackShare%20community,stacks%20and%20277%20developer%20stacks.)

  ## Arquitectura del framework Laravel
   Laravel cuenta con una arquitectura bastante organizada y lo suficientemente compleja para atender las necesidades de las aplicaciones mas demandantes 
   y con alta complejidad. Su nucleo se distribuye en Rutas, Vistas, Eloquent ORM, Controladores, Middlewares, Modelos y Migraciones, Requests y Responses.

 ![laravel architecture](https://hackernoon.com/photos/R8aLhmiN8rUgojf5QE8E0wAqhU73-0mkw29ls)

  También cuenta con un sistema de manejo de dependencias o un dependecy management, esto quiere decir que se puede integrar funcionalidades a tu aplicacion 
  facilmente sin la necesidad de crearlas desde cero. Puedes crear tambien tus propios packages o instalar dependencias ya existentes a traves de composer.

  Laravel posee un completo y complejo sistema de autenticación. Un ORM(Object-relational mapping) o una interfaz orientada objetos que nos permite facilmente 
  interactuar con nuestra base de datos. 

  También Posee una CLI nativa del framework llamada Artisan, para gestionar la creación de seeders, migraciones, controladores y modelos. El manejo de cache 
  de rutas y vistas, y la capacidad de levantar un servidor en desarrollo para tu app. Igualmente te brinda la capacidad de crear test unitarios usando la libreria
  PHPUnit.