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

   Tambien podemos pasar datos a nuestras vistas:

   1. Pasando una variable

   ```php
   return view('user', 'name' => 'John');
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

   ## Cache para nuestras Rutas

   Por defecto Laravel compilan las vistas durante el proceso de solicitud, lo que afecta negativamente al rendimiento, sin embargo el framework nos aporta a traves de la cli Artisan los siguientes comandos:

   ```bash
   $ php artisan view:cache
   ```

   O tambien si queremos borrar el cache de nuestras vistas si estamos en desarrollo:

   ```bash
   $ php artisan view:clear
   ```

   

   





















## Blade template engine

























## Laravel Collective Framework

