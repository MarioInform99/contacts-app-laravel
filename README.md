# Proyectos de Laravel

Iniciaremos proyectos de pruebas para conocer bastante bien el framework

## Instalaciones necesarias

Una de las instalaciones necesarias para crear nuestro entorno servidor con <b>XAMP</b>, <b>VSCode</b> y <b>Git Bash</b>. Los anteriores programas son instalaciones necesarias para entornos Windows y Linux, acontinuación instalamos <i>composer</i> es un gestor de paquetes de php como npm, a la hora de instalar composer debemos de tener las variables de entornos de PHP predefinido, la ruta de XAMPP para el php.
NodeJS y npm instalamos la ultima version, por problemas de compatibilidad en Vue JS, para evitar dichos problemas instalamos siempre la ultima version de node y npm, aunque pueden tener fallos de seguridad.

Instalacion de Linux-Ubuntu.
Composer actualizamos y ejecutamos los paquetes necesarios.

```bash
apt-get install curl
curl -sS https:://getcomposer.org/installer -o composer-setup

```

Esto nos trae un paquete .php ejecutamos el archivo <i>php composer-setup.php --install-dir="/usr/local/bin" filename=composer</i> le decimos que lo llevamos al un punto de desarrollo.

## Creacion de proyecto Laravel

Creamos un proyecto para verificar que todos nos funciona correctamente. El comando que usaremos es el siguiente.

```bash
composer create-project laravel/laravel <name_project>
```

Creamos la base de datos para la app de laravel. Para iniciar Laravel este framework tiene un CLI en el archivo artisan. Ejecutamos el siguiente comando.

```bash
php artisan serve

```

## Configuramos VSCode

Instalamos MySQL un extension e instalamos la version 4.5.12 que es la gratuita. Añadimos la conexion para conectarnos a la base de datos que nos proporciona XAMPP.

## Enrutamiento

El archivo principal donde cargamos el template y la rutas la encontramos en <i>routes/web.php</i> Route::get('',function) es una clase de Route y usamos una función o metodo llamado get le pasamos una función que define lo que vamos hacer, cuando realizamos esa peticion a esa ruta.

Con la clase Route podemos realizar peticiones HTTP (post,put,delete,etc...). Asociar una accion a una ruta.

Para comprobar el metodo POST hacemos con <i>curl</i> una petición con el siguiente comando.
-X es el metodo de peticion y -d data

```bash
curl -X POST -d "data=test" http://localhost:8000/ruta/post
```

### Ejercicios 1 (enrutamiento)

El ejercicio trata de realizar diferentes tipos de peticiones HTTP para trabajar con el enrutamiento de Laravel.
Debemos de clonar nuestro repositorio, copia el .env.example y cambiamos su nombre a .env, posteriormente ejecutamos <i>php artisan key:generate</i> pero antes de todo esto usaremos <i>composer install</i>.
Este es el resultado del código que hemo realizado ante peticiones HTTP, para realizar las pruebas del archivo disponemos de archivos de que realizar pruebas TestCase

```bash

// Ejercicio 1 peticiones http

Route::get('/ejercicio1', function () {
    return "GET OK";
});
//POST se usa para enviar una entidad a un recurso especifico.
Route::post('/ejercicio1', function () {
    return "POST OK";
});

//PUT reemplazar todas la representaciones del recurso de destio
Route::put('/ejercicio1', function () {
    return "PUT OK";
});

//PATCH es usado para aplicar modificaciones parciales a un recurso
Route::patch('/ejercicio1',function(){
    return "PATCH OK";
});

//DELETE borra el recurso
Route::delete('/ejercicio1', function () {
    return 'DELETE OK';
});
```

La ejecución de las pruebas para la comprobación del enrutamiento son las siguientes, los archivos tienen que estar en la carpeta Tests y heredar las clases TestCase.php y CreatesApplication.php

```bash
php artisan test --filter <nombre_del_archivo>
```

## Migraciones (artisan)

Las migraciones es una funcionalidad del framework para que el código SQL sea más accesible y mantenible. Las migraciones crea tablas, dichas migraciones las podemos encontrar en el archivo <i>database/migrations</i>. Para crear la base de datos usa un ORM usa funciones php para implementar a SQL.
Para crear migraciones usaremos artisan una herramienta de comandos.

```bash
php artisan route:list

php artisan migrate --help
```

Para realizar las creaciones de tablas a la base de datos, tenemos un archivo llamado .env para añadir las configuraciones al servidor y base de datos. Laravel nos ejecutara las migraciones.
Ejecutamos el siguiente comando para crear todas las tablas de pruebas que tiene nuestra app

```bash
php artisan migrate
```

Disponemos de una tabla como copia de seguridad llamada <i>migrations</i>, por ejemplo quiero borrar una tabla

```bash
php artisan migrate:rollback --step 1
```

Y si me quisiera volver a tener esa tabla realizare

```bash
php artisan migrate
```

## Autenticación

Creamos los formularios de registros y las rutas. Para instalar los paquetes instalaremos paquetes UI. Esto nos genera automaticamente archivos de bootstrap, la carpeta <i>vendor</i> es donde nos mete todas la dependencias.
Para ver la documentación de este paquete debemos de buscar en google <i>laravel/ui</i>

```bash
composer require laravel/ui
```

Una vez realizado la instalacion de laravel/ui dispondremos de un nuevo comando en <i>artisan</i> llamado <i>ui</i>.
Vamos a decirle que cree nuestras vistas con bootstrap, y tambien que nos cree los formularios de registro y login automaticamente

```bash
php artisan ui bootstrap
#Crea las vistas de los formularios de login y registro
php artisan ui bootstrap --auth
```

Ahora tenemos que ejecutar "npm install && npm run dev" para que nos instale las dependencias de vistas de javascript o cualquier "cosa".
En Laravel 9.x Vite a reemplazado a Laravel Mix, es decir que los compresores de paquetes de webpack debemos de migrarlos usando <i>npm install --save-dev laravel-mix</i>, una vez realizado dicha instalación debemos de actualizar o modificar el archivo package.json

```diff
  "scripts": {
-     "dev": "vite",
-     "build": "vite build"
+     "dev": "npm run development",
+     "development": "mix",
+     "watch": "mix watch",
+     "watch-poll": "mix watch -- --watch-options-poll=1000",
+     "hot": "mix watch --hot",
+     "prod": "npm run production",
+     "production": "mix --production"
  }
```

Una vez realizado esto ejecutaremos <i>npm install && npm run dev</i> y cuando hallamos terminado de ejecutar dicho comando, tendremos que volver a ejecutar <i>npm run dev</i>.
Esto ejecuta el Webpack mix, esto es un module que crea un solo archivo que mete todo el css o js en un archivo.

Ya realizados los pasos, el tema de la autenticación y del login ya estaría realizado por laravel. Las vistas las podemos encontrar en la carpeta <i>resources/views/auth</i>

## Cambiar de tema - Webpack Mix.

Usaremos el tema de bootswatch llamado Darkly. Las version de Bootstrap ha se der la 5.x.x. Instalamos boootswatch <i>npm install bootswatch</i>, ejecutamos npm install && npm run dev para que se nos instale todos los modulos.
Una vez realizada la instalación, nos iremos a la archivo <b>app.scss</b> que lo encontraremos en <i>resources/sass/</i>. Añadiremos esto:

```diff
- // Bootstrap
- //@import '~bootstrap/scss/bootstrap';
+ // Your variable overrides go here, e.g.:
+ // $h1-font-size: 3rem;

+ @import "~bootswatch/dist/darkly/variables";
+ @import "~bootstrap/scss/bootstrap";
+ @import "~bootswatch/dist/darkly/bootswatch";

```

Para compilar todo, a la hora de realizar cambios en los temas, js, css, etc. Debemos de usar <i>npm run dev</i>

Nos dirijimos a la carpeta <i>resources/sass/\_variables.scss</i> modificamos el <i>body-bg:</i> a el valor <b>#ff0000</b>, solamente para hacer una pruebas.

Para compilar automaticamente usaremos, a la hora de modificar cualquier tipo de archivo este comando te lo compilar automaticamente.

```bash
npm run watch
```

Modificamos el <i>navbar</i> de nuestra app, nos ubicaremos en <i>resources/layouts/app.blade.php</i>. Y modificaremos la clase de <i>navbar-ligth</i> a <b>navbar-dark</b> y <i>bg-white</i> a <b>bg-dark</b>.

NOTA: Layout, especificas donde introduces el contenido.

## Bundles de CSS y JS Laravel.

Editaremos el welcome.bladel.php y añadiremos nuestro propio html. Extendemos el layout, usando una directiva de blade, @section(''). Ahora usarmeos @extends, esta definia una vista secundaria para especificar el diseño que hereda
@extends('layouts.app')
@section('content')

---

@endsection
NOTA: Blade es un preprocesador de html.

Ahora introduciremos una img, crearemos una carpeta llamada img y esta la meteremos en la carpeta <i>resources</i>.
Introducimos la imagen a traves del css, esto lo añadiremos app.css.

```diff
+  .navbar img {
+     width: 1.2rem;
+  }

+  .welcome {
+     background: url('/img/background.jpg');
+     background-position: center center;
+     background-size: cover;
+  }
```

Esto no se nos va a compilar con el WebPack Mix, asi que tendremos que decirle que nos los compile. Introducimos las siguiente linea. Le estamos diciendo que de css, el archivo app.css mete todo lo que tenga en 'public/css' y de la imagen, que copie dicha imagen y la introduzca en 'public/img'

```diff
const mix = require('laravel-mix');


mix.js('resources/js/app.js', 'public/js')
    .sass('resources/sass/app.scss', 'public/css')
+   .css('resources/css/app.css','public/css')
+   .copy('resources/img','public/img')
    .sourceMaps();

```

<p align="center"><a href="https://laravel.com" target="_blank"><img src="https://raw.githubusercontent.com/laravel/art/master/logo-lockup/5%20SVG/2%20CMYK/1%20Full%20Color/laravel-logolockup-cmyk-red.svg" width="400"></a></p>

<p align="center">
<a href="https://travis-ci.org/laravel/framework"><img src="https://travis-ci.org/laravel/framework.svg" alt="Build Status"></a>
<a href="https://packagist.org/packages/laravel/framework"><img src="https://img.shields.io/packagist/dt/laravel/framework" alt="Total Downloads"></a>
<a href="https://packagist.org/packages/laravel/framework"><img src="https://img.shields.io/packagist/v/laravel/framework" alt="Latest Stable Version"></a>
<a href="https://packagist.org/packages/laravel/framework"><img src="https://img.shields.io/packagist/l/laravel/framework" alt="License"></a>
</p>

## About Laravel

Laravel is a web application framework with expressive, elegant syntax. We believe development must be an enjoyable and creative experience to be truly fulfilling. Laravel takes the pain out of development by easing common tasks used in many web projects, such as:

-   [Simple, fast routing engine](https://laravel.com/docs/routing).
-   [Powerful dependency injection container](https://laravel.com/docs/container).
-   Multiple back-ends for [session](https://laravel.com/docs/session) and [cache](https://laravel.com/docs/cache) storage.
-   Expressive, intuitive [database ORM](https://laravel.com/docs/eloquent).
-   Database agnostic [schema migrations](https://laravel.com/docs/migrations).
-   [Robust background job processing](https://laravel.com/docs/queues).
-   [Real-time event broadcasting](https://laravel.com/docs/broadcasting).

Laravel is accessible, powerful, and provides tools required for large, robust applications.

## Learning Laravel

Laravel has the most extensive and thorough [documentation](https://laravel.com/docs) and video tutorial library of all modern web application frameworks, making it a breeze to get started with the framework.

If you don't feel like reading, [Laracasts](https://laracasts.com) can help. Laracasts contains over 2000 video tutorials on a range of topics including Laravel, modern PHP, unit testing, and JavaScript. Boost your skills by digging into our comprehensive video library.

## Laravel Sponsors

We would like to extend our thanks to the following sponsors for funding Laravel development. If you are interested in becoming a sponsor, please visit the Laravel [Patreon page](https://patreon.com/taylorotwell).

### Premium Partners

-   **[Vehikl](https://vehikl.com/)**
-   **[Tighten Co.](https://tighten.co)**
-   **[Kirschbaum Development Group](https://kirschbaumdevelopment.com)**
-   **[64 Robots](https://64robots.com)**
-   **[Cubet Techno Labs](https://cubettech.com)**
-   **[Cyber-Duck](https://cyber-duck.co.uk)**
-   **[Many](https://www.many.co.uk)**
-   **[Webdock, Fast VPS Hosting](https://www.webdock.io/en)**
-   **[DevSquad](https://devsquad.com)**
-   **[Curotec](https://www.curotec.com/services/technologies/laravel/)**
-   **[OP.GG](https://op.gg)**
-   **[WebReinvent](https://webreinvent.com/?utm_source=laravel&utm_medium=github&utm_campaign=patreon-sponsors)**
-   **[Lendio](https://lendio.com)**

## Contributing

Thank you for considering contributing to the Laravel framework! The contribution guide can be found in the [Laravel documentation](https://laravel.com/docs/contributions).

## Code of Conduct

In order to ensure that the Laravel community is welcoming to all, please review and abide by the [Code of Conduct](https://laravel.com/docs/contributions#code-of-conduct).

## Security Vulnerabilities

If you discover a security vulnerability within Laravel, please send an e-mail to Taylor Otwell via [taylor@laravel.com](mailto:taylor@laravel.com). All security vulnerabilities will be promptly addressed.

## License

The Laravel framework is open-sourced software licensed under the [MIT license](https://opensource.org/licenses/MIT).
