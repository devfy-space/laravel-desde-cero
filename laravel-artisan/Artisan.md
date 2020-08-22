# Curso de Laravel desde cero - **Artisan CLI**

![](D:\cursos\laravel-desde-cero\assets\clase_07.jpg)

La mayoría de frameworks y herramientas como Angular, Vue js, Django, Symfony, Webpack, MySQL, etc. Laravel no es la excepción, utiliza una poderosa ***command-line interface*** (CLI), llamada Artisan, la cual permite interactuar con el framework de una forma mas ágil y rapida. 

Aquí una rápida lista de cosas que se pueden hacer:

1. Gestionar el environment de Nuestra app.
2. Crear Controladores
3. Gestionar las migraciones, seeders y factories de nuestra base de datos.
4. Manejar el cache de nuestras vistas, rutas y nuestra app.
5. Optimizar la app para producción.

Ahora bien, como toda **CLI**, artisan nos trae el siguiente comando para ver toda la lista de instrucciones que nos brinda esta herramienta.

```bash
$ php artisan list
```

##  Iniciando con Artisan

Como toda CLI, Artisan provee su propia help-command tool, la cual nos permite ver toda la información de un comando en particular y sus opciones.

Ejemplo:

```bash
$ php artisan help command-name
```

o también con el flag -h.

```bash
$ php artisan command-name -h
```

Ahora bien, una vez que sabemos como consultar nuestros comandos, es hora de comenzar a probar cosas.

## 1.  Levantar un servidor de desarrollo - Setup a Server 

Laravel nos permite levantar un servidor de desarrollo para ejecutar nuestra app.

```bash
$ php artisan serve 
```

## 2.  Poner la app en modo de mantenimiento

De vez en cuando podemos presentar problemas con la app, para evitar cualquier inconveniente a nuestros usuarios Laravel nos permite poner nuestra app en mantenimiento.

```bash
$ php artisan down
```

O podemos pasar mas opciones a nuestro comando:

```bash
$ php artisan down --message="La app esta en mantenimiento" --allow=192.168.1.110 
```

## 3.  Ver la versión de nuestro framework

```bash
$ php artisan --v
```

## 4.  Trabajar con nuestras base de datos

Con Artisan podemos realizar muchas tareas relacionadas al trabajo de nuestra base de datos, ejemplos de ello:

1. Crear migraciones

   ```bash
   $ php artisan make:migration create_posts_table 
   ```

2. Migrar nuestras tablas

   ```bash
   $ php artisan migrate
   ```

3. Crear Modelos

   ```bash
   $ php artisan make:model
   ```

4. Crear Seeders

   ```bash
   $ php artisan make:seed Post
   ```

5. Crear Factories

   ```bash
   $ php artisan make:factory Post
   ```

Estos comandos los veremos con mas detalles en la clase de Base de Datos del curso.

## 5.  Crear controladores

 1. Controlador basico

    ```bash
    $ php artisan make:controller NameController
    ```

 2. Controlador de accion unica

    ```bash
    $ php artisan make:controller NameController --invokable
    ```

 3. Controlador de Recurso
    
    ```bash
    $ php artisan make:controller --resource
    ```

  4. Controlador con modelo definido

     ```bash
     php artisan make:controller NameController --resource --model=Model
     ```

## 6. Generar una key de nuestra app

Muchas veces cuando desarrollamos apps con laravel es necesario tener la llave de nuestra app, sobre todo en entornos de producción y proteger la integridad de la misma.

```bash
$ php artisan key:generate
```

## 7. Cache

Rutas:

```bash
$ php artisan route:cache
```

Si desea borrar el cache es necesario utilizar:

```bash
$ php artisan route:clear
```

Vistas:

```bash
$ php artisan view:cache
```

Si desea borrar el cache es necesario utilizar:

```bash
$ php artisan view:clear
```



## Tinker

Además de una CLI, laravel también posee un REPL, el cual es como una shell o bash y nos permite interactuar con el ORM Eloquent, eventos, tareas, comandos del sistema.

Entramos a esta shell de la siguiente forma:

```bash
$ php artisan tinker
```

## Publicando archivos de configuración.

La mayoría de los packages que podemos instalar en nuestro framework al igual que componentes nativos como la autenticación, sistema de archivos, correo electrónico, base de datos, tienen la capacidad de generar archivos de configuración en los cuales podemos cambiar ciertos valores y comportamientos que de una u otra forma nos pueden beneficiar a la hora de realizar una tarea en particular.

Por ejemplo:

```bash
$ php artisan vendor:publish --provider="Laravel\Tinker\TinkerServiceProvider"
```

Aqui vemos como Tinker nos permite publicar el archivo de configuración de esta shell y crear cosas como los alias y cambiar diversos mecanismos predeterminados.

Estos se archivos se encuentran en la carpeta **/config**.