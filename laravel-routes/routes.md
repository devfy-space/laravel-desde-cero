# Curso de Laravel desde cero - Rutas

![laravel routing](https://i.ibb.co/7j4kWzD/image.png)

En esta guía hablaremos acerca de como crear, manejar y validar rutas con Laravel. El routing o **Enrutamiento** es uno de los aspectos mas fundamentales a la hora de desarrollar aplicaciones ya que nos permite controlar el flujo de peticiones que se realizan a nuestro aplicación y se encarga de decidir que se hará cuando el usuario solicite dicha ruta.

Por ejemplo, ¿Que haremos cuando un **usuario** solicite la ruta  "_/usuarios_" ? . Podemos enviar una vista con todos los usuarios existentes, podemos hacer el output de query a la base de datos en un formato legible como **JSON**, etc. También puede suceder que nuestras rutas no necesite estar actualizando constantemente el estado de nuestra aplicación, sino que solamente pueden devolver una vista estática de la pagina web de tu negocio o sitio web personal. En pocas palabras, se pueden realizar muchas cosas, ¿no?. Ahora, ¿Cómo iniciamos a crear rutas con **laravel**?

## Primero lo Primero, ¿Donde se encuentran las rutas?

A partir de Laravel 5, todas las rutas se definían en un único archivo llamado `routes.php` que se encontraba en `app/Http`. Pero, **a partir de Laravel 5.3, los routes tienen su propia carpeta en la raíz del proyecto** para llevar una mejor organización, llamada **`routes/`**.

En las ultimas versiones de **Laravel** las rutas se pueden encontrar en:

- `routes/api.php`: En este archivo se definen todas las rutas de las APIs que puede llegar a tener nuestra aplicación.
- `routes/channels.php`: Aquí definimos los canales transmisión de eventos. Por ejemplo, cuando realizamos notificaciones en tiempo real.
- `routes/console.php`: En el archivo de rutas `console.php` definimos comandos de consola que pueden interactuar con el usuario u otro sistema.
- `routes/web.php`: En este archivo de rutas es donde definimos todas las rutas de nuestra aplicación web que pueden ser ingresadas por la barra de direcciones del navegador.

En este curso solo usaremos el archivo **web.php**, el cual nos basta para realizar lo que necesitamos.

Si vamos a nuestro bash, y listamos nuestro directorio de rutas, podríamos ver algo así:

```bash
$ yotmanr@localhost /var/www/laravel-desde-cero.io (*master) > ls routes/
	|---* api.php
	|---* channels.php
	|---* console.php
	|---* web.php
```

Fuente: **[laraveltips.com/que-son-los-routes-en-laravel](https://www.laraveltip.com/que-son-los-routes-en-laravel/)**

## Métodos HTTP disponibles en nuestras rutas

Es importante entender que el 100% de los frameworks de backend, utilizan gran parte de los verbos HTTP o mejor conocido como métodos, de los cuales mayormente se usan :

 1. **GET**

 2. **POST**

 3. **PUT**

 4. **DELETE**

 5. **PATCH**

 6. **OPTIONS**

¿Pero porque se usan?

Si vienes del mundo de HTML, probablemente conozcas los formularios, los cuales nos permiten enviar y recibir datos en el servidor. HTML permite solo dos métodos HTTP que son POST y GET ó enviar y recibir. No obstante cuando desarrollamos aplicaciones necesitamos un poco mas que estos dos simples métodos, sobre todo cuando se emplea la arquitectura **REST** la cual emplea los verbos HTTP como la forma en la que nuestra aplicación, envía, recibe, actualiza o elimina recursos o datos.

## Ejemplos Básicos de Rutas

Entrando a nuestro bash abrimos con nano nuestro archivo **web.php**.

```bash
$ /var/www/laravel-desde-cero.io/routes -> nano web.php
```

```php
use Illuminate\Support\Facades\Route;

Route::get('/', function(){
	return view('welcome');
});
```

Como vemos en este archivo, tenemos una sola ruta, la ruta raíz de nuestra app, en la cual se retorna la vista **welcome**. Este es un ejemplo de ruta estática.

Aquí no solo podemos retornar vistas, sino que también podemos mostrar datos en texto plano, JSON, asignar a un controlador, etc. 

```php
use Illuminate\Support\Facades\Route;

Route::get('/my-first-route-with-laravel', function(){
	return 'Mi primera ruta con laravel';
});

// También podemos retornar JSON

Route::get('/users', function(){
    $users = ['John', 'Ana', 'Carlos', 'Mary', 'Albert'];
   return response()->json($users);
});

```

### Parámetros de Ruta (Requeridos)

También se pueden pasar parámetros que permitan devolver una respuesta dinámica a la información que solicita el usuario.

```php
use Illuminate\Support\Facades\Route;

Route::get('/user/{name}', function($name){ // pasamos el parametro a nuestro closure
    return $name;
});

// Podemos hacer una busqueda por {id} del usuario

Route::get('/user/{id}', function($id){
    $users = [
        ['id' => 1, 'name' => 'Dennis', 'lastname' => 'Ritchie',  'age'  => 40, 'ocupation' => 'Programmer'],
        ['id' => 2, 'name' => 'Ada',    'lastname' => 'Lovelace', 'age'  => 20, 'ocupation' => 'UI/UX Designer'],
        ['id' => 3, 'name' => 'Linux',  'lastname' => 'Torvalds', 'age'  => 50, 'ocupation' => 'Member of LSF']
    ];
        
    foreach($users as $user){
        if($user['id'] == $id){
            return response()->json($user);
        }
    }
    
    return view('404', compact('id'));
});

```

### Parámetros de Ruta (Opcionales)

Algo mas que se puede hacer con nuestras rutas es pasar parámetros opcionales, en los que el usuario puede o no solicitar una **URI** especifica.

```php
use Illuminate\Support\Facades\Route;

Route::get('user/{name?}', function ($name = null) {
    return $name;
});

Route::get('user/{name?}', function ($name = 'John') {
    return $name;
});
```

### Pasando múltiples parámetros

```php
/**
 Aqui podemos buscar usuarios pasando su nombre y opcionalmente su id, de tal manera que si hay usuarios que concidan con el mismo nombre, estos puedan distinguirse por su id único.
**/

Route::get('/user/{name}/{id?}', function($name, $id = null){
    $users = [
        ['id' => 1, 'name' => 'Steve', 'lastname' => 'Wozniak', 'nickname' => 'WOZ'],
        ['id' => 2, 'name' => 'Steve', 'lastname' => 'Jobs', 'nickname' => 'JOBS'],
    ];
        
    foreach($users as $user){
        if(strtolower($user['name']) == $name) {
            if($user['id'] == $id){
                return response()->json($user);
            }
            print_r(json_encode($user, JSON_PRETTY_PRINT)  . "<br>");
        }
    }    
});
```

Este ultimo ejemplo es una aplicación práctica de esta característica.

### Métodos de rutas disponibles

Tenemos diferentes métodos que podemos usar en **laravel** para recibir solicitudes de los usuarios.

```php
Route::get($uri, $callback);
Route::post($uri, $callback);
Route::put($uri, $callback);
Route::patch($uri, $callback);
Route::delete($uri, $callback);
Route::options($uri, $callback);
```

## Validando Rutas

Uno de los tantos beneficios que nos ofrece **Laravel** es que podemos validar o filtrar las peticiones de nuestros usuarios y de esa forma podemos evitar comportamientos no esperados. Aquí el siguiente ejemplo:

```php
use Illuminate\Support\Facades\Route;

Route::get('user/{name}', function ($name) {
    
})->where('name', '[A-Za-z]+'); // validar solo caracteres alfabeticos

Route::get('user/{id}', function ($id) {
    
})->where('id', '[0-9]+'); // validar solo caracteres númericos

Route::get('user/{id}/{name}', function ($id, $name) {
    
})->where(['id' => '[0-9]+', 'name' => '[a-z]+']); // validar multiples parametros
```

También podemos validar nuestras rutas de manera global en nuestro ```RouteServiceProvider```.

```php
/**
 * Define your route model bindings, pattern filters, etc.
 *
 * @return void
 */
public function boot()
{
    Route::pattern('id', '[0-9]+');

    parent::boot();
}
```



## Pasando datos en nuestras rutas

Laravel nos permite pasar datos de nuestras rutas a vistas utilizando la función ```compact```.

```php
use Illuminate\Support\Facades\Route;

Route::get('/products', function(){
    
   $products_array = [
      	['id' => 001, 'name' => 'computer',  'price' => '1270.00$', 'stock' => 50],
       	['id' => 002, 'name' => 'headset',   'price' => '55.40$',   'stock' => 20],
       	['id' => 003, 'name' => 'webcam',    'price' => '120.00$',  'stock' => 30],
       	['id' => 004, 'name' => 'smartphone', 'price' => '650.$',    'stock' => 10]
   ];
    
   $products = json_encode($products_array);
   
   return view('products', compact('products'));
});
```

En nuestra vista ```products.blade.php```,  mostramos los productos de la siguiente forma.

```php
{{
    $products
}}
```

Obtendremos el siguiente resultado:

![products view](https://i.ibb.co/2jHw25p/image.png)



## Named Routes o Rutas con nombre

Esta característica nos permite darle nombres a nuestras rutas y agilizar de cierta manera el uso de nuestras rutas tanto en controladores como en vistas. en clases posteriores veras sus beneficios.

```php
use Illuminate\Support\Facades\Route;

Route::get('user/profile', function () {
    //
})->name('profile');
```

Igualmente lo hacemos al asignar nuestras rutas a nuestros controladores

```php
Route::get('user/profile', 'UserProfileController@show')->name('profile');
```

## Nested Routes o Rutas anidadas

Un ejemplo básico de esto es un restaurante, donde existen clientes y pedidos, las rutas anidadas nos permiten saber que pedido pertenece a un cliente. Ejemplo:

```php
use Illuminate\Support\Facades\Route;

Route::get('clientes.pedidos', function () {
    //
});
```



## Como inspeccionar tus rutas

Para saber que rutas están disponibles en nuestra aplicación es necesario utilizar artisan. 

```bash
$ php artisan route:list
```

![](https://i.ibb.co/xh1Xsq5/bash.jpg)



## Conclusión

Ya vimos toda la cantidad de cosas que podemos hacer con las rutas de laravel, en posteriores clases estaremos hablando cosas mas avanzadas de routing, como route model binding, middlewares, groups, namespaces, etc.

Puedes acceder a la documentación oficial de **Laravel**, pulsando aquí en la manito [👉](https://laravel.com/docs/7.x/routing).

Y no olvides **[acceder al playlist del curso](https://www.youtube.com/playlist?list=PLc64KFB8u6VSmNoZP1xGcOHlCRgLFNMka)** 👀