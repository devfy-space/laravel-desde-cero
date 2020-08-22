# Curso de Laravel desde Cero - Controladores

![]()

## 1. ¿Qué son los Controladores?

Los controladores forman parte de la capa estructural de un framewok, dentro del patron **MVC** son los encargados de la logica y funciona de intermediarios entre nuestras vistas y modelos. Como ya sabemos **Laravel** no implementa del todo esta filosofia, y dentro de este framework es solo una capa mas, obviamente tiene mucha importancia, y se utilizan para asignar a nuestras rutas y manejar de mejor manera todo la logica necesaria que estas requieren. Al desarrollar aplicaciones **CRUD** y monolitos estos cobran mucho protagonismo y son la base estructural de dicha aplicación.

Ahora que nos dice la documetación oficial de Laravel:

> En lugar de definir toda su lógica de manejo de solicitudes como closures en su archivo de rutas, es posible que desee organizar este comportamiento utilizando clases de Controlador. Los controladores pueden agrupar la lógica de manejo de solicitudes relacionadas en una sola clase.

Como vemos aqui, **Laravel** claramente nos confirma que los Controladores se usa unicamente para nuestra capa HTTP, osea para agrupar la logica de las solicitudes que se realizan a nuestra app, en vez de manejarlas unicamente usando funciones de cierre o closures en nuestro archivo de rutas.

## 2. ¿Dónde ubicamos nuestros controladores?

Los controladores están ubicados en el directorio ``app/Http/Controllers/``. La estructura es algo asi:

```
app/
	*--Console
	*--Exceptions
	*--Http
		*--Controllers
			*--Controller.php
		*--Middleware
		Kernel.php
	*--Providers
```

## 3. Iniciando con nuestros controladores

Primero nos dirigimos a nuestra carpeta de controladores, donde crearemos el siguiente controller llamado ProductController, por convención se tiende a utilizar esta nomenclatura donde el nombre de nuestro controlador inicia con mayúscula y concatenado a la palabra **"Controller"**.

Luego creamos nuestro controlador usando la siguiente estructura.

```php
<?php

namespace App\Http\Controllers; // esto nos indica donde va a estar ubicado nuestro controlador
/**
	Aqui indicamos que estamos usando la clase Controller ubicada en el namespace "App\Http\Controllers"
**/
use App\Http\Controllers\Controller; 

class ProductController extends Controller // declaracion de nuestra clase 
{
    public function show() // metodo de nuestro clase
    {
        return 'Mi primer Controlador con laravel'; // retorno de nuestro controlador
    }
}
```

Palabras claves:

**Namespace:** Un espacio de nombres es un contenedor abstracto en el que un grupo de uno o más identificadores únicos de una clase pueden existir.

**Class:** Es una plantilla para la creación de objetos de datos según un modelo predefinido. Las clases se utilizan para representar entidades o conceptos, como los sustantivos en el lenguaje.

**Method:** Un método define el comportamiento de los objetos que se crean a partir de la clase.

## 4. ¿Como ejecutamos nuestros controladores?

Para trabajar con nuestros controladores es necesario ir a nuestro archivo de rutas y asignar una ruta a dicho controller. Ejemplo

```php
Route::get('/product', 'ProductController@show'); // Es necesario especificar el metodo al cual queremos acceder
```

## 5. Controladores de acción única

Laravel tambien nos permite definir controladores que solo tengan un unico comportamiento, una sola acción. Aqui el siguiente ejemplo.

```php
<?php

namespace App\Http\Controllers;

use App\Http\Controllers\Controller;

class ShowProfile extends Controller
{
    /**
     * Show the profile for the given user.
     *
     * @param  int  $id
     * @return View
     */
    public function __invoke($id)
    {
        return "Editar Perfil de Usuario id: {$id}" ;
    }
}
```

Y en nuestro ``web.php``:

```php
Route::get('user/{id}', 'ShowProfile'); // como vemos no es necesario especificar el metodo de acción
```



## Resource Controllers

Laravel tiene la capacidad de generar controladores que utilizan el esquema **REST**, de esa forma ya tenemos la base para realizar nuestro CRUD.

para obtener este tipo de controlador es necesario usar **Artisan**

```bash
$ php artisan make:controller ProductController --resource
```

luego inspeccionamos nuestras rutas con ``php artisan route:list`` y obtendremos el siguiente resultado:

| Verb      | URI                        | Action  | Route Name       |
| :-------- | :------------------------- | :------ | :--------------- |
| GET       | `/products`                | index   | products.index   |
| GET       | `/products/create`         | create  | products.create  |
| POST      | `/products`                | store   | products.store   |
| GET       | `/products/{product}`      | show    | products.show    |
| GET       | `/products/{product}/edit` | edit    | products.edit    |
| PUT/PATCH | `/products/{product}`      | update  | products.update  |
| DELETE    | `/products/{product}`      | destroy | products.destroy |

Para ver el efecto necesitamos asignar nuestra ruta al controlador.

```php
Route::resource('photos', 'ProductController');
```

## 7. Como generamos nuestros Controladores

Gracias a la **CLI** nativa de **Laravel**, Artisan, podemos generar el esqueleto o estructura de nuestros controladores, los comandos disponibles son:

 1. Controlador básico

    ```bash
    $ php artisan make:controller NameController
    ```

 2. Controlador de acción única

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

     
