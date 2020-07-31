# Curso de Laravel desde cero - Instalación en Linux 💪🧠🔥🔥🔥

![Windows and Linux - Devfy](https://i.imgur.com/L3F0jtr.jpeg)

En esta clase te explicaremos como instalar el framework Laravel en tu sistema Linux Ubuntu-like distribution **(Distribución basada en Ubuntu Linux)** llamada Elementary OS. No te preocupes aunque lo hagamos formalmente en esta versión se colocara como hacerlo en otras distribuciones populares de Linux como Arch Linux, Fedora y CentOS.

## Requisitos para instalar son:

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

## Instalación de Composer

Primero es necesario tener instalado el package manager de php **Composer**, puedes ir a su sitio web oficial en este enlace **[getcomposer.org](https://getcomposer.org)**.

![upload.wikimedia.org/wikipedia/commons/thumb/2/...](https://upload.wikimedia.org/wikipedia/commons/thumb/2/26/Logo-composer-transparent.png/200px-Logo-composer-transparent.png)

1. **Instalación de dependencias**	

​	Para instalar **composer**, es necesario tener instalado curl para descargar el package, **php-cli** para correr el instalador, **php-mbstring** para funcionalidades de la biblioteca y **unzip** para descomprimir paquetes.

​	Primero asegúrate de tener actualizada la cache del administrador de paquetes:

```bash
$ sudo apt update
```

Luego:

```bash
$ sudo apt install curl php-cli php-mbstring unzip
```

2. **Descarga e Instalación usando curl**

   Asegúrese de posicionarse en su directorio de inicio y recupere el instalador usando **curl**

 ```bash
$ cd ~
$ curl -sS https://getcomposer.org/installer -o composer-setup.php
 ```

   A continuación, verifique que el instalador coincida con el hash SHA-384 para el instalador más reciente encontrado en la página **[Composer Public Keys/Signatures](https://composer.github.io/pubkeys.html)**. Copie el hash de esa página y almacénelo como variable de shell:

```bash
$ HASH=yourhashcode
```

Asegúrese de sustituir el hash más reciente por el valor resaltado.

Ahora, ejecute el siguiente script PHP para verificar que el script de instalación se ejecute de forma segura:

```bash
$ php -r "if (hash_file('SHA384', 'composer-setup.php') === '$HASH') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
```

Para instalar composer a nivel global, utilice el siguiente comando que lo descargará e instalará en todo el sistema como un comando llamado `composer`, en `/usr/local/bin`:

```bash
$ sudo php composer-setup.php --install-dir=/usr/local/bin --filename=composer
```

Si el hash es correcto, debería obtener el siguiente resultado:

Finalizando, ejecute **composer** en su terminal y obtendrá el siguiente resultado:

```
Output
   ______
  / ____/___  ____ ___  ____  ____  ________  _____
 / /   / __ \/ __ `__ \/ __ \/ __ \/ ___/ _ \/ ___/
/ /___/ /_/ / / / / / / /_/ / /_/ (__  )  __/ /
\____/\____/_/ /_/ /_/ .___/\____/____/\___/_/
                    /_/
Composer version x.x.x

Usage:
  command [options] [arguments]

Options:
  -h, --help                     Display this help message
  -q, --quiet                    Do not output any message
  -V, --version                  Display this application version
      --ansi                     Force ANSI output
      --no-ansi                  Disable ANSI output
  -n, --no-interaction           Do not ask any interactive question
      --profile                  Display timing and memory usage information
      --no-plugins               Whether to disable plugins.
  -d, --working-dir=WORKING-DIR  If specified, use the given directory as working directory.
  -v|vv|vvv, --verbose           Increase the verbosity of messages: 1 for normal output, 2 for more verbose output and 3 for debug
. . .
```



## Instalación en Apache 2

Para comenzar a desarrollar con **Laravel** no es necesario tener instalado Apache, sin embargo en esta guía colocaremos nuestra app en este servidor web para no tener que estar levantando un servidor con el comando **php artisan serve** cada vez que utilizamos este framework, además tenemos la comodidad de crear vhost(virtual host) y tener nuestro propio dominio personalizado en nuestro sistema.

Para instalar apache2 es necesario utilizar el siguiente comando:

```bash
$ sudo apt install apache2 
```

Una vez instalado, podemos comprobar que apache ya esta activo realizando las siguientes pruebas:

 1. Ingresando al browser con la siguiente url y obtener el siguiente resultado:

    ```
    http://localhost
    ```

​       ![](https://ubuntucommunity.s3.dualstack.us-east-2.amazonaws.com/optimized/2X/7/771159b35c97e429247aac754ad44bf06cc1efa8_2_690x461.png)

 2. Usando **systemctl**:

    ```bash
    $ sudo systemctl status apache2
    ```

    Debemos obtener algo parecido a este resultado:

    ```
    Output
    ● apache2.service - The Apache HTTP Server
         Loaded: loaded (/lib/systemd/system/apache2.service; enabled; vendor preset: enabled)
         Active: active (running) since Thu 2020-07-31 22:36:30 UTC;
           Docs: https://httpd.apache.org/docs/2.4/
       Main PID: 29435 (apache2)
          Tasks: 55 (limit: 1137)
         Memory: 8.0M
         CGroup: /system.slice/apache2.service
                 ├─29435 /usr/sbin/apache2 -k start
                 ├─29437 /usr/sbin/apache2 -k start
                 └─29438 /usr/sbin/apache2 -k start
    ```

 3. Buscando el directorio apache2 en nuestro sistema:

    ```bash
    $ cd /etc/apache2 && ls
    ```

Mas información en:

[Instalación de Apache 2 - digitalocean](https://www.digitalocean.com/community/tutorials/how-to-install-the-apache-web-server-on-ubuntu-20-04-es)

## Instalación de Laravel con composer

Una vez que tengamos instalado tanto composer como apache, procedemos a instalar laravel en nuestro sistema con el comando:

```bash
$ composer create-project --prefer-dist laravel/laravel yourapp-name
```

 Recuerda siempre tener cargados los modulos de php anteriormente mencionados, accede pulsando la manito [👆](#Requisitos para instalar son:) 😊.

Finalmente puedes usar laravel con el siguiente comando:

```bash
$ php artisan serve
```

![laravel - php artisan serve](https://i.ibb.co/q0GXLkP/image.png)

Sin embargo, como ya mencionamos antes no utlizaremos este setup para trabajar, sino que nos dirigeremos a nuestro directorio  **_/var/www_** que es el directorio root por defecto que usa apache para localizar nuestros sitios, no importa esto lo puedes cambiar y modificar segun tus necesidades 👌.

Asi que debemos hacer el siguiente comando, tomando en cuenta que ya laravel esta instalado, simplemente moveremos la carpeta:

```bash
$ cd mv yourapp-name /var/www
```

###### No olvides darle permisos a toda tu carpeta public y establecer como dueño de ese directorio. Para hacer eso necesitas, ```chmod -R yourapp-name/public && chown -R $USER:$USER /var/www/yourapp-name```

Una vez hecho esta sentencia, nos vamos a nuestro browser y vamos a la siguiente dirección:

```bash
http://localhost/yourapp-name/public
```

Esto es feo,  ¿no? 🤔. Nosotros como en la seria anterior,  **[instalación-laravel-windows](https://github.com/devfy-space/laravel-desde-cero/blob/master/instalacion-configuracion/windows.md)** creamos un virtual host en apache para nuestro sitio y utilizamos  el dominio de nuestra preferencia, recuerden, pueden utilizar el nombre que mejor les parezca, obviamente sin violar las reglas de un dominio valido.

Asi que, nos iremos a nuestro directorio apache2, y haremos el setup de nuestra:

 ```bash
$ cd /etc/apache2/sites-available
 ```

Luego de eso copiamos el archivo base de configuración a nuestro nuevo site y editarlo:

```bash
$ sudo cp 000-default.conf yourapp-name.conf && nano yourapp-name.conf
```

Deberias tener algo similar a esto, obviamente con tus modificaciones a los nombres del sitio, etc.

```bash
<VirtualHost *:80>
    ServerAdmin webmaster@localhost
    ServerName your_domain
    ServerAlias www.your_domain
    DocumentRoot /var/www/your_domain
    <Directory /var/www/your_domain>
    	Options -Indexes +FollowSymLinks
    	Require all granted
    	AllowOverride All
    </Directory>
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```

Una vez creado el vhost es necesario ir otra vez a nuestro bash y correr el comando:

```bash
$ sudo a2ensite yourapp-name.conf
```

Ahora, esto no sera suficiente para hacer lo que queremos, necesitamos primero reiniciar nuestro apache.

```bash
$ sudo systemctl restart apache2
```

Finalmente puedes acceder en tu navegador a tu nuevo sitio y listo!!. Si te gusto esta guía de instalación, no dudes en suscribirte a nuestro **[canal de youtube](https://bit.ly/30bmtAp)** y dar una manito arriba a este tutorial 👍, te lo agradecería!!❤️😁. 

**[Pulsa aqui para acceder al playlist del curso](https://www.youtube.com/playlist?list=PLc64KFB8u6VSmNoZP1xGcOHlCRgLFNMka)**

