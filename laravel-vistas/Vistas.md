# Curso de Laravel desde cero - Vistas

Las **vistas** son otra capa muy importante en toda aplicación, ya que representa de manera visual los datos de la misma, estos pueden representarse en diversos formatos, HTML, JSON, XML, etc, es decir, es la capa de presentación.

En laravel, al igual que en otros frameworks se utilizan algo llamado template engine o motor de plantillas, estos no son mas que un superset de HTML que es el lenguaje de presentación nativo de la web. ¿Que decir esto? Tenemos disponibles las siguientes bondades:

1. **Condicionales.**

2. **Bucles o ciclos.**

3. **Importar plantillas o vistas externas.**

4. **Crear Plantillas.**

5. **Extender Plantillas.**

6. **Extrapolar variables.**

****



## Creando vistas

Las **vistas** se ubican en el directorio de **``resource/views``** con la nomenclatura de ``example.blade.php``, donde **example** es el nombre de nuestra view junto al nombre de nuestro motor de plantillas llamado **[blade 👇](#blade-template-engine)**. Una vista simple puede verse de la siguiente forma:

```html
<!DOCTYPE html>
<html>
    <head>
        <title>Laravel desde cero || Vistas</title>
    </head>
    <body>
        <h1>
            Mi primera vista con laravel
        </h1>
    </body>
</html>
```

Ahora es necesario hacer el retorno de nuestra vista bien sea en un controlador o en una ruta.

1. Desde nuestro closure de ruta

   ```php
   <?php
   
   use Illuminate\Support\Facades\Route;
   
   Route::get('/example-view', function(){
       return view('example');
   });
   ```

   

2. Desde nuestro controlador

   ```php
   <?php
   
   namespace App\Http\Controllers;
   
   use Illuminate\Http\Request;
   
   class MyController extends Controller
   {
       //
       public function example_view(){
           return view('example'); 
       }
   }
   ```

   También podemos pasar datos a nuestras vistas:

   1. Pasando una variable

   ```php
   return view('user', ['name' => 'John']);
   ```

   2. Pasando un arreglo asociativo de valores

   ```php
   return view('user', ['name' => 'John', 'lastname' => 'Wick', 'profile' => 'https://i.ibb.co/Rc5p5nd/image.png', 'description' => 'Me gustan los perros 🐶🐕‍🦺']);
   ```

   Y en nuestra vista realizamos lo siguiente:

   ```php
   <!-- resources/views/users.blade.php -->
   <!DOCTYPE html>
   <html>
       <head>
           <title>Laravel desde cero || Vistas</title>
       	<link rel="stylesheet" href="./css/style.css">
       </head>
       <body>
         <div class="container"> 
   	    <article class="card">
               <img class="card-header" src="https://i.ibb.co/Rc5p5nd/image.png">
               <div class="card-body">
                   <img class="card-avatar" src="https://i.ibb.co/fkfbWTH/image.png" alt="">
                   <h3>{{ $name . ' ' . $lastname }} 💣⚰️</h3>	
                   <p>{{ $description }}</p>
               </div>
       	</article>
         </div>
       </body>
   </html>
   ```

   Puedes copiar este codigo en tu carpeta ```public/css``` y crear un archivo style.css

   ```css
   *, *::before, *::after{
       box-sizing: border-box;
       margin: 0;
       padding: 0;
      font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
    }
   
   body{
       display: flex;
       align-items: center;
       min-height: 100vh;
       background-color: #eee;
       background-image: url('https://images2.alphacoders.com/100/1009975.jpg');
       background-size: cover;
   }
   
    img{
      max-width: 100%;
    }
   
     .container{
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        max-width: 1024px;
        margin: 2rem auto 0 auto;
     }
   
    .card{
        position: relative;
        max-width: 240px;
        background-color: #fff;
        border: 1px solid #eee;
        border-radius: 5px;
        box-shadow: 0 10px 20px rgba(0,0,0,0.09), 0 6px 6px rgba(0,0,0,0.06);
        overflow: hidden;
   }
   
   .card-body{
       padding: 2em;
   }
   
   .card-header{
        min-height: 130px;
        filter: blur(1px);
        object-fit: cover;
   }
   
   .card-avatar{
      position: absolute;
      top: 70px;
      left: 50%;
      transform: translateX(-50%);
      width: 80px;
      height: 80px;
      border-radius: 50%;
      object-fit: cover;
   }
   
    .card-body p{
       font-style: italic;
       line-height: 2.1;
       color: #666;
       font-size: 14px;
   }
   
   h1{
       text-align: center;
       margin: 2rem;
   }
   ```

   ## Compartiendo datos entre Vistas

   Laravel nos permite compartir de manera global datos entre vistas, de esa forma podemos enviar datos comunes que no queremos estar realizando de manera manual en cada retorno.

   Esto lo podemos realizar en nuestro ```AppServiceProvider```, ubicado en la carpeta ``app/Http/Providers``. Aqui el ejemplo:
   
   ```php
	<?php
    namespace App\Providers;

   use Illuminate\Support\Facades\View;  // Es necesario añadir el 			Facade de vista

	class AppServiceProvider extends ServiceProvider
   {
    /**
        * Register any application services.
        *
        * @return void
        */
       public function register()
       {
           //
       }

       /**
        * Bootstrap any application services.
        *
        * @return void
        */
       public function boot()
       {
           //
           View::share('home_title', 'Mi primera app con laravel');
           View::share('fruits', ['grapes' => '🍇', 'watermelon' => '🍉', 'banana' => '🍌', 'strawberry' => '🍓']);
       }
   }
   ```


   Y en nuestro archivo ``welcome.blade.php``, escribimos lo siguiente:

   ```php
   <!DOCTYPE html>
   <html lang="{{ str_replace('_', '-', app()->getLocale()) }}">
       <head>
           <meta charset="utf-8">
           <meta name="viewport" content="width=device-width, initial-scale=1">
   
           <title>Laravel</title>
   
           <!-- Fonts -->
           <link href="https://fonts.googleapis.com/css?family=Nunito:200,600" rel="stylesheet">
   
           <!-- Styles -->
           <style>
               html, body {
                   background-color: #fff;
                   color: #636b6f;
                   font-family: 'Nunito', sans-serif;
                   font-weight: 200;
                   height: 100vh;
                   margin: 0;
               }
   
               .full-height {
                   height: 100vh;
               }
   
               .flex-center {
                   align-items: center;
                   display: flex;
                   justify-content: center;
               }
   
               .position-ref {
                   position: relative;
               }
   
               .top-right {
                   position: absolute;
                   right: 10px;
                   top: 18px;
               }
   
               .content {
                   text-align: center;
               }
   
               .title {
                   font-size: 84px;
               }
   
               .links > a {
                   color: #636b6f;
                   padding: 0 25px;
                   font-size: 13px;
                   font-weight: 600;
                   letter-spacing: .1rem;
                   text-decoration: none;
                   text-transform: uppercase;
               }
   
               .m-b-md {
                   margin-bottom: 30px;
               }
           </style>
       </head>
       <body>
           <div class="flex-center position-ref full-height">
               @if (Route::has('login'))
                   <div class="top-right links">
                       @auth
                           <a href="{{ url('/home') }}">Home</a>
                       @else
                           <a href="{{ route('login') }}">Login</a>
   
                           @if (Route::has('register'))
                               <a href="{{ route('register') }}">Register</a>
                           @endif
                       @endauth
                   </div>
               @endif
   
               <div class="content">
                   <div class="title m-b-md">
                       Laravel
                       <div class="fruits">     
                           @foreach ($fruits as $fruit => $value)
                               <span title="{{ $fruit }}">{{ $value }}</span>
                           @endforeach
                       </div>
                   </div>
   
                   <div class="links">
                       <a href="https://laravel.com/docs">Docs</a>
                       <a href="https://laracasts.com">Laracasts</a>
                       <a href="https://laravel-news.com">News</a>
                       <a href="https://blog.laravel.com">Blog</a>
                       <a href="https://nova.laravel.com">Nova</a>
                       <a href="https://forge.laravel.com">Forge</a>
                       <a href="https://vapor.laravel.com">Vapor</a>
                       <a href="https://github.com/laravel/laravel">GitHub</a>
                   </div>
               </div>
           </div>
       </body>
   </html>
   
   ```

   El resultado sera el siguiente:

   ![image-20200808130625632](C:\Users\Owner\AppData\Roaming\Typora\typora-user-images\image-20200808130625632.png)

   

   ## Cache para nuestras Rutas

   Por defecto Laravel compilan las vistas durante el proceso de solicitud, lo que afecta negativamente al rendimiento, sin embargo el framework nos aporta a través de la cli Artisan los siguientes comandos:

   ```bash
   $ php artisan view:cache
   ```

   O también si queremos borrar el cache de nuestras vistas si estamos en desarrollo:

   ```bash
   $ php artisan view:clear
   ```

   ## Estructura de  directorios común

   Aquí observamos una lista de carpetas basadas en la estructura de nuestra aplicación, esto puede variar según las necesidades. 

   ```bash
   /resources
   ---	/views
   	---- /users
   	|	index.blade.php
   	|	create.blade.php
   	|	edit.blade.php
   	|	show.blade.php
   	---- /posts
   	|	index.blade.php
   	|	create.blade.php
   	|	edit.blade.php
   	|	show.blade.php
   	---- /categories
   	|	index.blade.php
   	|	create.blade.php
   	|	edit.blade.php
   	|	show.blade.php
   ```

   Ahora bien la idea aquí es como accedemos a toda esas vistas desde nuestro controlador o closure de ruta. Esto lo hacemos de la siguiente forma:

   ```php
   return view('users.index'); // si queremos acceder a nuestro index.blade.php
   ```

   De esta forma vemos, que para entrar un directorio de vista, es necesario usar el punto **``(.)``**  .  Luego de esto ya tenemos acceso a dicha ruta.

## Blade template engine

Laravel utiliza el motor de plantillas **Blade** para compilar nuestras vistas en simple HTML. Además este template engine nos permite ejecutar código PHP, lo que es una ventaja ya que utilizamos las características avanzadas del lenguaje.  Así que es momento de comenzar a hacer cosas mas avanzadas con nuestras vistas usando **Blade**.

1. **[Plantillas](#Plantillas)**
2. **[Estructuras de control](#Estructuras-de-control)**
3. **[Formularios](#Formularios)**
4. **[Inclusión de vistas](#Includes)**
5. **[Validaciones](#validaciones)**

	### Plantillas

​	Uno de los tantos beneficios que nos brinda **Laravel** es el de crear plantillas, heredarlas y definir secciones. De esta forma podemos crear plantillas maestras como la base para nuestras vistas. Ejemplo:

```php
<!-- Stored in resources/views/layouts/app.blade.php -->

<html>
    <head>
        <title>App Name - @yield('title')</title>
    </head>
    <body>
        @section('sidebar')
            This is the master sidebar.
        @show

        <div class="container">
            @yield('content')
        </div>
    </body>
</html>
```

Y en nuestras plantillas hijas hacemos lo siguiente:

```php
<!-- Stored in resources/views/posts/show.blade.php -->
@extends('layouts.app')

@section('content')
   <p>Post Content</p>
@endsection
    
@section('sidebar')
   <p>Secondary Content</p>
@endsection 
```

### **Estructuras de control**

​	Como mencionamos al principio, usar un motor de plantillas nos da muchas bondades como bucles, condicionales, incluir vistas, etc.

```php
// Ejemplo de bucle foreach en una vista
@extends('layouts.app')

@section('content')
    @foreach($posts as $post)
        <article class="post">
            <header class="post-header">
                <h3>{{ $post->title }}</h3>
                <img src="{{ $post->thumbnail }}">	
            </header>
            <div class="post-body">
                {{ $post->content }}
            </div>
            <footer class="post-footer">
                <time>{{ $post->date }}</time>
            </footer>
        </article>
    @endforeach
@endsection
```

Ejemplo de uso de una estructura de control condicional:

```php
@extends('layouts.app')
    
@section('content')
    @if (count($records) === 1)
        I have one record!
    @elseif (count($records) > 1)
        I have multiple records!
    @else
        I don't have any records!
  @endif
@endsection
```

Ejemplos de directivas de autenticación.

```php
@auth
    // The user is authenticated...
@endauth

@guest
    // The user is not authenticated...
@endguest
```

Si queremos escribir código php, podemos usar la siguiente directiva:

```php
@php
    //
@endphp
```

### Formularios

​	Es importante que cuando comencemos a utilizar los diferentes métodos HTTP como DELETE, PUT, PATCH entendamos que no son soportados por la especificación de HTML, razón por la cual debemos utilizar un campo oculto llamado ``_method`` para poder realizar dichas peticiones. Laravel nos permite realizar esto a traves de la directiva ``@method`` .

```php
<form action="/foo/bar" method="POST">
    @method('PUT')
    ...
</form>
```

### Includes

​	Podemos importar el contenido de una vista en otra usando la directiva ``@include``:

```php
@include('layouts.header')
    
@include('layouts.footer')
```

### Validaciones

La `@error`directiva se puede utilizar para comprobar rápidamente si existen [mensajes de error de validación](https://laravel.com/docs/7.x/validation#quick-displaying-the-validation-errors) para un atributo determinado. Dentro de una `@error`directiva, puede hacer eco de la `$message`variable para mostrar el mensaje de error:

```php
<!-- /resources/views/post/create.blade.php -->

<label for="title">Post Title</label>

<input id="title" type="text" class="@error('title') is-invalid @enderror">

@error('title')
    <div class="alert alert-danger">{{ $message }}</div>
@enderror
```

Puedes ver ejemplos mas avanzados en la documentación oficial. [Laravel Validation](https://laravel.com/docs/7.x/validation)

## Laravel Collective Framework

