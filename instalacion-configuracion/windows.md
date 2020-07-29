# Instalación y Configuración de Laravel - Windows 10

![Windows and Linux - Devfy](https://i.imgur.com/L3F0jtr.jpeg)

 

En esta clase estaremos instalando Laravel en la plataforma Windows 10, los requisitos necesarios para el desarrollo de esta clase son: 

- **PHP >= 7.2.5** como minimo
- **BCMath PHP Extension**
- **Ctype PHP Extension**
- **Fileinfo PHP extension**
- **JSON PHP Extension**
- **Mbstring PHP Extension**
- **OpenSSL PHP Extension**
- **PDO PHP Extension**
- **Tokenizer PHP Extension**
- **XML PHP Extension**
- **Composer**

Para comprobar que versión tenemos instalado en nuestra máquina windows, es necesario ir a nuestro símbolo del sistema CMD, y correr el comando **```php -v```** .

En este caso estamos usando xampp el cual es kit de desarrollo que viene con el stack **LAMP** (Linux, Apache, MySQL y PHP)

![Windows CMD](https://i.ibb.co/pdgfqkG/cmd.jpg)

Luego de verificar que contamos que con la versión de php adecuada debemos asegurarnos de contar con las extensiones anteriormente mencionadas, las cuales esta contenidas en nuestro archivo php.ini, el cual podemos ubicar con el siguiente comando **```php --ini```**. Como vemos el archivo se encuentra en **c:\xampp\php\php.ini**.

![Windows cmd](https://i.ibb.co/Mhb5Jsc/cmd.jpg)

Ahora entrando al archivo **php.ini** vemos que extensiones tenemos cargadas, si necesitas alguna de estas extensiones la puedes habilitar eliminando el **";"** .

![vscode](https://i.ibb.co/BHk2bft/vscode.jpg)



Una vez que todo esto esta OK, procedemos a instalar laravel.

Tenemos dos opciones para instalar laravel en Windows:

1. Utilizando el laravel installer. Para ello es necesario tener composer añadido a nuestro **$PATH** en windows:

   ![environment variables](https://i.ibb.co/2nN9DbN/environment-variables.jpg)

   Luego de verificar que composer esta correctamente configurado en nuestro sistema procedemos **`composer global require laravel/installer`** y luego de haberse instalado, utilizamos el comando;
   ```bash
   	laravel new project-name
   ```

2. Utilizando el comando Composer create-project 

   ```bash
   composer create-project --prefer-dist laravel/laravel blog
   ```




Finalmente de haber sido instalado todas las dependencias, escribimos el comando:

```bash
php artisan serve
```

Una vez levantado el servidor de desarrollo vamos a nuestro navegador en la dirección [localhost:8000](https://localhost:8000)

![laravel - php artisan serve](https://i.ibb.co/q0GXLkP/image.png)



## Creación de virtual host en apache

Laravel esta efectivamente configurado en nuestra máquina, ahora crearemos un virtual site en nuestro servidor local para poder acceder a nuestra app desde el navegador con una url personalizada y que incluso puede sobreescribir dominios publicos de internet.

Primero procedemos a ir a nuestra carpeta **apache** en nuestro xampp o wampp, la ruta al archivo de host virtual es **carpeta-instalacion\apache\conf\extra\httpd-vhosts.conf**:

Ejemplo:

```bash
<VirtualHost *:80>
    ServerAdmin  soporte@misitioweb.io
    DocumentRoot "D:\aplicaciones\www\misitioweb.com"
    ServerName   misitioweb
    ServerAlias  www.misitioweb.com

    <Directory "D:\aplicaciones\www\misitioweb.com">
        Options -Indexes +FollowSymLinks
        Require all granted
        AllowOverride All
    </Directory>

    ErrorLog    "logs/misitioweb-error.log"
    CustomLog   "logs/misitioweb-access.log" common
</VirtualHost>
```

En mi caso escribi lo siguiente:

![apache virtual host](https://i.ibb.co/DwXN1xR/image.png)

Una vez creado nuestro site, es necesario modificar los dns de nuestro sistema local, los cuales estan ubicados en **C:\Windows\System32\drivers\etc**, proceder a editar el archivo y agregar las siguientes lineas

```bash
// Curso de Laravel

127.0.0.1 laravel-desde-cero.io
```



Finalmente se procede a reiniciar el servidor de apache de nuestro xampp o wampp e ir al navegador y acceder a nuestro sitio web.