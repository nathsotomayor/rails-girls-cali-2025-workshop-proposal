Primeros Pasos con Rails
==========================

Esta guía cubre cómo comenzar a trabajar con Ruby on Rails.

Después de leer esta guía, sabrás:

* Cómo instalar Rails, crear una nueva aplicación Rails y conectar tu aplicación a una base de datos.
* La estructura general de una aplicación Rails.
* Los principios básicos de MVC (Model, View, Controller) y el diseño RESTful.
* Cómo generar rápidamente las piezas iniciales de una aplicación Rails.

--------------------------------------------------------------------------------

Introducción
------------

¡Bienvenido a Ruby on Rails! En esta guía, recorreremos los conceptos principales de la construcción de aplicaciones web con Rails. No necesitas ninguna experiencia previa con Rails para seguir esta guía.

Rails es un framework web construido para el lenguaje de programación Ruby. Rails aprovecha muchas características de Ruby, por lo que **recomendamos encarecidamente** aprender los fundamentos de Ruby para que entiendas algunos de los términos básicos y vocabulario que verás en este tutorial.

- [¿Tienes 30 minutos? ¡Prueba Ruby ahora mismo!](https://try.ruby-lang.org/)
- [Sitio web oficial del lenguaje de programación Ruby](https://www.ruby-lang.org/en/documentation/)
- [Lista de libros gratuitos de programación](https://github.com/EbookFoundation/free-programming-books/blob/main/books/free-programming-books-langs.md#ruby)

Filosofía de Rails
----------------

Rails es un framework de desarrollo de aplicaciones web escrito en el lenguaje de programación Ruby. Está diseñado para hacer que la programación de aplicaciones web sea más fácil al asumir lo que cada desarrollador necesita para comenzar. Te permite escribir menos código mientras logras más que con muchos otros lenguajes y frameworks. Los desarrolladores experimentados de Rails también reportan que hace el desarrollo de aplicaciones web más divertido.

Rails es software con opiniones. Asume que hay una "mejor" manera de hacer las cosas, y está diseñado para fomentar esa manera - y en algunos casos para desalentar alternativas. Si aprendes "La Forma Rails" probablemente descubrirás un tremendo aumento en productividad. Si persistes en traer viejos hábitos de otros lenguajes a tu desarrollo con Rails, e intentas usar patrones que aprendiste en otro lugar, puede que tengas una experiencia menos feliz.

La filosofía de Rails incluye dos principios rectores principales:

- **No Te Repitas (Don't Repeat Yourself):** DRY es un principio de desarrollo de software que establece que "Cada pieza de conocimiento debe tener una representación única, inequívoca y autorizada dentro de un sistema". Al no escribir la misma información una y otra vez, nuestro código es más mantenible, más extensible y con menos errores.
- **Convención Sobre Configuración (Convention Over Configuration):** Rails tiene opiniones sobre la mejor manera de hacer muchas cosas en una aplicación web, y usa como predeterminado este conjunto de convenciones, en lugar de requerir que las definas tú mismo a través de interminables archivos de configuración.

Creando una Nueva Aplicación Rails
------------------------

Vamos a construir un proyecto llamado `store` - una aplicación simple de comercio electrónico que demuestra varias de las características integradas de Rails.

Consejo: Cualquier comando precedido por un signo de dólar `$` debe ejecutarse en la terminal.

### Requisitos Previos

Para este proyecto, necesitarás:

* Una cuenta de GitHub
* Ruby 3.2 o más reciente
* Rails 8.1.0 o más reciente
* Un editor de código

### Creando Tu Ambiente de Desarrollo

Un ambiente de desarrollo es el espacio donde escribes y pruebas tu código antes de ponerlo en producción. Incluye todas las herramientas, librerías y configuraciones necesarias para que tu aplicación funcione correctamente mientras la desarrollas.

Para este proyecto, vamos a usar GitHub Codespaces, que nos proporciona un ambiente de desarrollo completo en la nube, eliminando la necesidad de configurar todo manualmente en tu computadora.

Antes de comenzar, asegúrate de tener lista tu cuenta de GitHub. Si aún no tienes una, puedes crear una siguiendo esta [guía de creación de cuenta en GitHub](https://docs.github.com/es/get-started/start-your-journey/creating-an-account-on-github).

Una vez que tengas tu cuenta, sigue estos pasos para crear tu ambiente de desarrollo:

1. Ingresa al repositorio de plantilla: [store-template](https://github.com/railsgirls-cali/store-template)
2. Haz clic en el botón verde "Use this template" (Usar esta plantilla) y selecciona "Create a new repository" (Crear un nuevo repositorio)
3. Dale un nombre a tu repositorio, por ejemplo `store`, y haz clic en "Create repository" (Crear repositorio)
4. Una vez creado tu repositorio, haz clic en el botón verde "Code" (Código) y selecciona la pestaña "Codespaces"
5. Haz clic en "Create codespace on main" (Crear codespace en main)

GitHub Codespaces creará un ambiente de desarrollo completo en la nube con todo lo necesario para trabajar en tu aplicación Rails. Esto puede tomar unos minutos la primera vez.

Aunque usaremos un ambiente ya configurado, consulta la [Guía de Instalación de Ruby on Rails](https://guides.rubyonrails.org/install_ruby_on_rails.html) si deseas comprender cómo se instalan Ruby y Rails.

Vamos a verificar que la versión correcta de Rails esté instalada. Para mostrar la versión actual, abre una terminal y ejecuta lo siguiente. Deberías ver un número de versión impreso:

```bash
$ rails --version
Rails 8.1.0
```

La versión mostrada debería ser Rails 8.1.0 o superior.

### Creación de Aplicaciones Rails

Rails viene con varios comandos para hacer la vida más fácil. Ejecuta `rails --help` para ver todos los comandos.

Normalmente, cuando se crea una nueva aplicación Rails desde cero, se utiliza el comando `rails new`, que genera todos los cimientos necesarios. Sin embargo, en esta guía no ejecutaremos este comando ya que nuestra plantilla tiene toda esta estructura ya configurada.

Aun así, es útil conocer este proceso. Para crear una aplicación llamada `store` desde cero, ejecutarías:

```bash
$ rails new store
```

Este comando crea la estructura completa de directorios, archivos de configuración, gemas predeterminadas y los archivos iniciales necesarios para trabajar con Rails. Después de creada, cambiarías al directorio de tu aplicación:

```bash
$ cd store
```

Nota: Puedes personalizar lo que Rails genera usando diferentes opciones. Para ver estas opciones, ejecuta `rails new --help`.

### Estructura de Directorios

Echemos un vistazo rápido a los archivos y directorios que se incluyen en una nueva aplicación Rails. Puedes abrir esta carpeta en tu editor de código o ejecutar `ls -la` en tu terminal para ver los archivos y directorios.

| Archivo/Carpeta | Propósito |
| ----------- | ------- |
|app/|Contiene los controllers, models, views, helpers, mailers, jobs y assets para tu aplicación. **Te enfocarás principalmente en esta carpeta durante el resto de esta guía.**|
|bin/|Contiene el script `rails` que inicia tu aplicación y puede contener otros scripts que uses para configurar, actualizar, desplegar o ejecutar tu aplicación.|
|config/|Contiene la configuración de las rutas, base de datos y más de tu aplicación. Esto se cubre con más detalle en [Configurando Aplicaciones Rails](https://guides.rubyonrails.org/configuring.html).|
|config.ru|Configuración de [Rack](https://rack.github.io) para servidores basados en Rack usados para iniciar la aplicación.|
|db/|Contiene el esquema actual de tu base de datos, así como las migrations de la base de datos.|
|Dockerfile|Archivo de configuración para Docker.|
|Gemfile<br>Gemfile.lock|Estos archivos te permiten especificar qué dependencias de gemas son necesarias para tu aplicación Rails. Estos archivos son usados por la gema [Bundler](https://bundler.io).|
|lib/|Módulos extendidos para tu aplicación.|
|log/|Archivos de registro de la aplicación.|
|public/|Contiene archivos estáticos y assets compilados. Cuando tu aplicación está ejecutándose, este directorio será expuesto tal cual.|
|Rakefile|Este archivo localiza y carga tareas que pueden ejecutarse desde la línea de comandos. Las definiciones de tareas están definidas a lo largo de los componentes de Rails. En lugar de cambiar `Rakefile`, deberías agregar tus propias tareas añadiendo archivos al directorio `lib/tasks` de tu aplicación.|
|README.md|Este es un breve manual de instrucciones para tu aplicación. Deberías editar este archivo para decirle a otros qué hace tu aplicación, cómo configurarla, etc.|
|script/|Contiene scripts de un solo uso o de propósito general y [benchmarks](https://github.com/rails/rails/blob/main/railties/lib/rails/generators/rails/benchmark/USAGE).|
|storage/|Contiene bases de datos SQLite y archivos de Active Storage para Disk Service. Esto se cubre en [Descripción General de Active Storage](https://guides.rubyonrails.org/configuring.html/active_storage_overview.html).|
|test/|Pruebas unitarias, fixtures y otros aparatos de prueba. Estos se cubren en [Probando Aplicaciones Rails](https://guides.rubyonrails.org/configuring.html/testing.html).|
|tmp/|Archivos temporales (como caché y archivos pid).|
|vendor/|Un lugar para todo el código de terceros. En una aplicación Rails típica esto incluye gemas vendorizadas.|
|.dockerignore|Este archivo le dice a Docker qué archivos no debe copiar al contenedor.|
|.gitattributes|Este archivo define metadatos para rutas específicas en un repositorio Git. Estos metadatos pueden ser usados por Git y otras herramientas para mejorar su comportamiento. Consulta la [documentación de gitattributes](https://git-scm.com/docs/gitattributes) para más información.|
|.git/|Contiene archivos del repositorio Git.|
|.github/|Contiene archivos específicos de GitHub.|
|.gitignore|Este archivo le dice a Git qué archivos (o patrones) debe ignorar. Consulta [GitHub - Ignorando archivos](https://help.github.com/articles/ignoring-files) para más información sobre cómo ignorar archivos.|
|.kamal/|Contiene secretos de Kamal y hooks de despliegue.|
|.rubocop.yml|Este archivo contiene la configuración para RuboCop.|
|.ruby-version|Este archivo contiene la versión predeterminada de Ruby.|

### Fundamentos de Model-View-Controller

El código de Rails está organizado usando la arquitectura Model-View-Controller (MVC). Con MVC, tenemos tres conceptos principales donde vive la mayoría de nuestro código:

* Model - Administra los datos en tu aplicación. Típicamente, tus tablas de base de datos.
* View - Maneja el renderizado de respuestas en diferentes formatos como HTML, JSON, XML, etc.
* Controller - Maneja las interacciones del usuario y la lógica para cada petición.

<picture class="flowdiagram">
  <source srcset="images/mvc_architecture_dark.jpg" media="(prefers-color-scheme:dark)">
  <img src="images/mvc_architecture_light.jpg">
</picture>

Ahora que tenemos un entendimiento básico de MVC, veamos cómo se usa en Rails.

¡Hola, Rails!
-------------

Comencemos arrancando nuestro servidor Rails por primera vez.

Normalmente, antes de iniciar el servidor, crearías la base de datos ejecutando:

```bash
$ bin/rails db:create
```

Este comando crea inicialmente la base de datos de la aplicación y es parte del flujo habitual al trabajar con Rails. Sin embargo, en nuestro ambiente de GitHub Codespaces, la base de datos ya fue creada automáticamente, así que omitiremos este paso.

En tu terminal, ejecuta el siguiente comando:

```bash
$ bin/rails server
```

Nota: Cuando ejecutamos comandos dentro de un directorio de aplicación, debemos usar `bin/rails`. Esto asegura que se use la versión de Rails de la aplicación.

Esto iniciará un servidor web llamado Puma que servirá archivos estáticos y tu aplicación Rails:

```bash
=> Booting Puma
=> Rails 8.1.0 application starting in development
=> Run `bin/rails server --help` for more startup options
Puma starting in single mode...
* Puma version: 6.4.3 (ruby 3.3.5-p100) ("The Eagle of Durango")
*  Min threads: 3
*  Max threads: 3
*  Environment: development
*          PID: 12345
* Listening on http://127.0.0.1:3000
* Listening on http://[::1]:3000
Use Ctrl-C to stop
```

Cuando ejecutas el servidor en GitHub Codespaces, aparecerá una notificación indicando que tu aplicación está corriendo en un puerto. Codespaces abrirá automáticamente una pestaña de preview dentro del editor para ver tu aplicación. Sin embargo, siempre deberías abrirla en tu navegador haciendo clic en el botón que Codespaces habilita para esto. Verás la página de bienvenida predeterminada de Rails:

![Página de bienvenida de Rails](images/rails_welcome.png)

¡Funciona!

Esta página es la *prueba de humo* para una nueva aplicación Rails, asegurando que todo esté funcionando detrás de escena para servir una página.

Para detener el servidor Rails en cualquier momento, presiona `Ctrl-C` en tu terminal.

### Autoloading en Desarrollo

La felicidad del desarrollador es una filosofía fundamental de Rails y una forma de lograr esto es con la recarga automática de código en desarrollo.

Una vez que inicias el servidor Rails, los archivos nuevos o cambios a archivos existentes se detectan y cargan o recargan automáticamente según sea necesario. Esto te permite enfocarte en construir sin tener que reiniciar tu servidor Rails después de cada cambio.

También puedes notar que las aplicaciones Rails rara vez usan sentencias `require` como puedes haber visto en otros lenguajes de programación. Rails usa convenciones de nomenclatura para requerir archivos automáticamente para que puedas enfocarte en escribir el código de tu aplicación.

Consulta [Autocarga y Recarga de Constantes](https://guides.rubyonrails.org/autoloading_and_reloading_constants.html) para más detalles.

Creando un Model de Base de Datos
-------------------------

Active Record es una característica de Rails que mapea bases de datos relacionales a código Ruby. Ayuda a generar el lenguaje estructurado de consulta (SQL) para interactuar con la base de datos como crear, actualizar y eliminar tablas y registros. Nuestra aplicación está usando SQLite, que es la base de datos predeterminada para Rails.

Comencemos agregando una tabla de base de datos a nuestra aplicación Rails para añadir productos a nuestra tienda simple de comercio electrónico.

```bash
$ bin/rails generate model Product name:string
```

Este comando le dice a Rails que genere un model llamado `Product` que tiene una columna `name` y tipo `string` en la base de datos. Más adelante, aprenderás cómo agregar otros tipos de columnas.

Verás lo siguiente en tu terminal:

```bash
      invoke  active_record
      create    db/migrate/20240426151900_create_products.rb
      create    app/models/product.rb
      invoke    test_unit
      create      test/models/product_test.rb
      create      test/fixtures/products.yml
```

Este comando hace varias cosas. Crea...

1. Una migration en la carpeta `db/migrate`.
2. Un model de Active Record en `app/models/product.rb`.
3. Pruebas y test fixtures para este model.

Nota: Los nombres de los models son *singulares*, porque un model instanciado representa un solo registro en la base de datos (es decir, estás creando un _producto_ para agregar a la base de datos).

### Migrations de Base de Datos

Una _migration_ es un conjunto de cambios que queremos hacer a nuestra base de datos.

Al definir migrations, le estamos diciendo a Rails cómo cambiar la base de datos para agregar, cambiar o eliminar tablas, columnas u otros atributos de nuestra base de datos. Esto ayuda a mantener un registro de los cambios que hacemos en desarrollo (solo en nuestra computadora) para que puedan ser desplegados a producción (¡en vivo, en línea!) de manera segura.

En tu editor de código, abre la migration que Rails creó para nosotros para que podamos ver qué hace la migration. Esto está ubicado en `db/migrate/<timestamp>_create_products.rb`:

```ruby
class CreateProducts < ActiveRecord::Migration[8.1]
  def change
    create_table :products do |t|
      t.string :name

      t.timestamps
    end
  end
end
```

Esta migration le está diciendo a Rails que cree una nueva tabla de base de datos llamada `products`.

Nota: En contraste con el model de arriba, Rails hace los nombres de las tablas de base de datos _plurales_, porque la base de datos contiene todas las instancias de cada model (es decir, estás creando una base de datos de _productos_).

El bloque `create_table` entonces define qué columnas y tipos deben definirse en esta tabla de base de datos.

`t.string :name` le dice a Rails que cree una columna en la tabla `products` llamada `name` y establezca el tipo como `string`.

`t.timestamps` es un atajo para definir dos columnas en tus models: `created_at:datetime` y `updated_at:datetime`. Verás estas columnas en la mayoría de los models de Active Record en Rails y se establecen automáticamente por Active Record al crear o actualizar registros.

### Ejecutando Migrations

Ahora que has definido qué cambios hacer a la base de datos, usa el siguiente comando para ejecutar las migrations:

```bash
$ bin/rails db:migrate
```

Este comando verifica si hay migrations nuevas y las aplica a tu base de datos. Su salida se ve así:

```bash
== 20240426151900 CreateProducts: migrating ===================================
-- create_table(:products)
   -> 0.0030s
== 20240426151900 CreateProducts: migrated (0.0031s) ==========================
```

Consejo: Si cometes un error, puedes ejecutar `bin/rails db:rollback` para deshacer la última migration.

Consola de Rails
-------------

Ahora que hemos creado nuestra tabla de products, podemos interactuar con ella en Rails. Probémoslo.

Para esto, vamos a usar una característica de Rails llamada *console*. La consola es una herramienta útil e interactiva para probar nuestro código en nuestra aplicación Rails.

```bash
$ bin/rails console
```

Se te presentará un prompt como el siguiente:

```irb
Loading development environment (Rails 8.1.0)
store(dev)>
```

Aquí podemos escribir código que se ejecutará cuando presionemos `Enter`. Probemos imprimir la versión de Rails:

```irb
store(dev)> Rails.version
=> "8.1.0"
```

¡Funciona!

Fundamentos de Active Record Model
--------------------------

Cuando ejecutamos el generador de model de Rails para crear el model `Product`, creó un archivo en `app/models/product.rb`. Este archivo crea una clase que usa Active Record para interactuar con nuestra tabla de base de datos `products`.

```ruby
class Product < ApplicationRecord
end
```

Puede que te sorprenda que no haya código en esta clase. ¿Cómo sabe Rails qué define este model?

Cuando se usa el model `Product`, Rails consultará la tabla de base de datos para los nombres y tipos de columnas y generará automáticamente código para estos atributos. Rails nos ahorra escribir este código repetitivo y en su lugar se encarga de ello detrás de escena para que podamos enfocarnos en nuestra lógica de aplicación.

Usemos la consola de Rails para ver qué columnas detecta Rails para el model Product.

Ejecuta:

```irb
store(dev)> Product.column_names
```

Y deberías ver:

```irb
=> ["id", "name", "created_at", "updated_at"]
```

Rails consultó a la base de datos la información de las columnas arriba y usó esa información para definir atributos en la clase `Product` dinámicamente para que no tengas que definir manualmente cada uno de ellos. Este es un ejemplo de cómo Rails hace el desarrollo muy fácil.

### Creando Registros

Podemos instanciar un nuevo registro de Product con el siguiente código:

```irb
store(dev)> product = Product.new(name: "T-Shirt")
=> #<Product:0x000000012e616c30 id: nil, name: "T-Shirt", created_at: nil, updated_at: nil>
```

La variable `product` es una instancia de `Product`. No se ha guardado en la base de datos, y por lo tanto no tiene un ID, created_at, o updated_at timestamps.

Podemos llamar `save` para escribir el registro en la base de datos.

```irb
store(dev)> product.save
  TRANSACTION (0.1ms)  BEGIN immediate TRANSACTION /*application='Store'*/
  Product Create (0.9ms)  INSERT INTO "products" ("name", "created_at", "updated_at") VALUES ('T-Shirt', '2024-11-09 16:35:01.117836', '2024-11-09 16:35:01.117836') RETURNING "id" /*application='Store'*/
  TRANSACTION (0.9ms)  COMMIT TRANSACTION /*application='Store'*/
=> true
```

Cuando se llama `save`, Rails toma los atributos en memoria y genera una consulta SQL `INSERT` para insertar este registro en la base de datos.

Rails también actualiza el objeto en memoria con el `id` del registro de base de datos junto con los timestamps `created_at` y `updated_at`. Podemos ver eso imprimiendo la variable `product`.

```irb
store(dev)> product
=> #<Product:0x00000001221f6260 id: 1, name: "T-Shirt", created_at: "2024-11-09 16:35:01.117836000 +0000", updated_at: "2024-11-09 16:35:01.117836000 +0000">
```

Similar a `save`, podemos usar `create` para instanciar y guardar un objeto Active Record en una sola llamada.

```irb
store(dev)> Product.create(name: "Pants")
  TRANSACTION (0.1ms)  BEGIN immediate TRANSACTION /*application='Store'*/
  Product Create (0.4ms)  INSERT INTO "products" ("name", "created_at", "updated_at") VALUES ('Pants', '2024-11-09 16:36:01.856751', '2024-11-09 16:36:01.856751') RETURNING "id" /*application='Store'*/
  TRANSACTION (0.1ms)  COMMIT TRANSACTION /*application='Store'*/
=> #<Product:0x0000000120485c80 id: 2, name: "Pants", created_at: "2024-11-09 16:36:01.856751000 +0000", updated_at: "2024-11-09 16:36:01.856751000 +0000">
```

### Consultando Registros

También podemos buscar registros de la base de datos usando nuestro model de Active Record.

Para encontrar todos los registros de Product en la base de datos, podemos usar el método `all`. Este es un método de _clase_, por eso podemos usarlo en Product (versus un método de instancia que llamaríamos en la instancia product, como `save` arriba).

```irb
store(dev)> Product.all
  Product Load (0.1ms)  SELECT "products".* FROM "products" /* loading for pp */ LIMIT 11 /*application='Store'*/
=> [#<Product:0x0000000121845158 id: 1, name: "T-Shirt", created_at: "2024-11-09 16:35:01.117836000 +0000", updated_at: "2024-11-09 16:35:01.117836000 +0000">,
 #<Product:0x0000000121845018 id: 2, name: "Pants", created_at: "2024-11-09 16:36:01.856751000 +0000", updated_at: "2024-11-09 16:36:01.856751000 +0000">]
```

Esto genera una consulta SQL `SELECT` para cargar todos los registros de la tabla `products`. Cada registro se convierte automáticamente en una instancia de nuestro model Product de Active Record para que podamos trabajar fácilmente con ellos desde Ruby.

Consejo: El método `all` devuelve un objeto `ActiveRecord::Relation` que es una colección similar a un Array de registros de base de datos con características para filtrar, ordenar y ejecutar otras operaciones de base de datos.

### Filtrando y Ordenando Registros

¿Qué pasa si queremos filtrar los resultados de nuestra base de datos? Podemos usar `where` para filtrar registros por una columna.

```irb
store(dev)> Product.where(name: "Pants")
  Product Load (1.5ms)  SELECT "products".* FROM "products" WHERE "products"."name" = 'Pants' /* loading for pp */ LIMIT 11 /*application='Store'*/
=> [#<Product:0x000000012184d858 id: 2, name: "Pants", created_at: "2024-11-09 16:36:01.856751000 +0000", updated_at: "2024-11-09 16:36:01.856751000 +0000">]
```

Esto genera una consulta SQL `SELECT` pero también agrega una cláusula `WHERE` para filtrar los registros que tienen un `name` que coincida con `"Pants"`. Esto también devuelve un `ActiveRecord::Relation` porque múltiples registros pueden tener el mismo nombre.

Podemos usar `order(name: :asc)` para ordenar los registros por nombre en orden alfabético ascendente.

```irb
store(dev)> Product.order(name: :asc)
  Product Load (0.3ms)  SELECT "products".* FROM "products" /* loading for pp */ ORDER BY "products"."name" ASC LIMIT 11 /*application='Store'*/
=> [#<Product:0x0000000120e02a88 id: 2, name: "Pants", created_at: "2024-11-09 16:36:01.856751000 +0000", updated_at: "2024-11-09 16:36:01.856751000 +0000">,
 #<Product:0x0000000120e02948 id: 1, name: "T-Shirt", created_at: "2024-11-09 16:35:01.117836000 +0000", updated_at: "2024-11-09 16:35:01.117836000 +0000">]
```

### Encontrando Registros

¿Qué pasa si queremos encontrar un registro específico?

Podemos hacer esto usando el método de clase `find` para buscar un solo registro por ID. Llama al método y pasa el ID específico usando el siguiente código:

```irb
store(dev)> Product.find(1)
  Product Load (0.2ms)  SELECT "products".* FROM "products" WHERE "products"."id" = 1 LIMIT 1 /*application='Store'*/
=> #<Product:0x000000012054af08 id: 1, name: "T-Shirt", created_at: "2024-11-09 16:35:01.117836000 +0000", updated_at: "2024-11-09 16:35:01.117836000 +0000">
```

Esto genera una consulta `SELECT` pero especifica un `WHERE` para la columna `id` que coincida con el ID de `1` que se pasó. También agrega un `LIMIT` para devolver solo un registro.

Esta vez, obtenemos una instancia de `Product` en lugar de un `ActiveRecord::Relation` ya que solo estamos recuperando un solo registro de la base de datos.

### Actualizando Registros

Los registros pueden actualizarse de 2 formas: usando `update` o asignando atributos y llamando `save`.

Podemos llamar `update` en una instancia de Product y pasar un Hash de nuevos atributos para guardar en la base de datos. Esto asignará los atributos, ejecutará validaciones y guardará los cambios en la base de datos en una sola llamada de método.

```irb
store(dev)> product = Product.find(1)
store(dev)> product.update(name: "Shoes")
  TRANSACTION (0.1ms)  BEGIN immediate TRANSACTION /*application='Store'*/
  Product Update (0.3ms)  UPDATE "products" SET "name" = 'Shoes', "updated_at" = '2024-11-09 22:38:19.638912' WHERE "products"."id" = 1 /*application='Store'*/
  TRANSACTION (0.4ms)  COMMIT TRANSACTION /*application='Store'*/
=> true
```

Esto actualizó el nombre del producto "T-Shirt" a "Shoes" en la base de datos. Confirma esto ejecutando `Product.all` de nuevo.

```irb
store(dev)> Product.all
```

Verás dos productos: Shoes y Pants.

```irb
  Product Load (0.3ms)  SELECT "products".* FROM "products" /* loading for pp */ LIMIT 11 /*application='Store'*/
=>
[#<Product:0x000000012c0f7300
  id: 1,
  name: "Shoes",
  created_at: "2024-12-02 20:29:56.303546000 +0000",
  updated_at: "2024-12-02 20:30:14.127456000 +0000">,
 #<Product:0x000000012c0f71c0
  id: 2,
  name: "Pants",
  created_at: "2024-12-02 20:30:02.997261000 +0000",
  updated_at: "2024-12-02 20:30:02.997261000 +0000">]
```

Alternativamente, podemos asignar atributos y llamar `save` cuando estemos listos para validar y guardar los cambios en la base de datos.

Cambiemos el nombre "Shoes" de vuelta a "T-Shirt".

```irb
store(dev)> product = Product.find(1)
store(dev)> product.name = "T-Shirt"
=> "T-Shirt"
store(dev)> product.save
  TRANSACTION (0.1ms)  BEGIN immediate TRANSACTION /*application='Store'*/
  Product Update (0.2ms)  UPDATE "products" SET "name" = 'T-Shirt', "updated_at" = '2024-11-09 22:39:09.693548' WHERE "products"."id" = 1 /*application='Store'*/
  TRANSACTION (0.0ms)  COMMIT TRANSACTION /*application='Store'*/
=> true
```

### Eliminando Registros

El método `destroy` puede usarse para eliminar un registro de la base de datos.

```irb
store(dev)> product.destroy
  TRANSACTION (0.1ms)  BEGIN immediate TRANSACTION /*application='Store'*/
  Product Destroy (0.4ms)  DELETE FROM "products" WHERE "products"."id" = 1 /*application='Store'*/
  TRANSACTION (0.1ms)  COMMIT TRANSACTION /*application='Store'*/
=> #<Product:0x0000000125813d48 id: 1, name: "T-Shirt", created_at: "2024-11-09 22:39:38.498730000 +0000", updated_at: "2024-11-09 22:39:38.498730000 +0000">
```

Esto eliminó el producto T-Shirt de nuestra base de datos. Podemos confirmar esto con `Product.all` para ver que solo devuelve Pants.

```irb
store(dev)> Product.all
  Product Load (1.9ms)  SELECT "products".* FROM "products" /* loading for pp */ LIMIT 11 /*application='Store'*/
=>
[#<Product:0x000000012abde4c8
  id: 2,
  name: "Pants",
  created_at: "2024-11-09 22:33:19.638912000 +0000",
  updated_at: "2024-11-09 22:33:19.638912000 +0000">]
```

### Validaciones

Active Record proporciona *validaciones* que te permiten asegurar que los datos insertados en la base de datos cumplan con ciertas reglas.

Agreguemos una validación `presence` al model Product para asegurar que todos los productos deben tener un `name`.

```ruby
class Product < ApplicationRecord
  validates :name, presence: true
end
```

Puedes recordar que Rails recarga automáticamente los cambios durante el desarrollo. Sin embargo, si la consola está ejecutándose cuando haces actualizaciones al código, necesitarás refrescarla manualmente. Así que hagámoslo ahora ejecutando 'reload!'.

```irb
store(dev)> reload!
Reloading...
```

Intentemos crear un Product sin nombre en la consola de Rails.

```irb
store(dev)> product = Product.new
store(dev)> product.save
=> false
```

Esta vez `save` devuelve `false` porque el atributo `name` no fue especificado.

Rails ejecuta automáticamente las validaciones durante las operaciones create, update y save para asegurar entrada válida. Para ver una lista de errores generados por las validaciones, podemos llamar `errors` en la instancia.

```irb
store(dev)> product.errors
=> #<ActiveModel::Errors [#<ActiveModel::Error attribute=name, type=blank, options={}>]>
```

Esto devuelve un objeto `ActiveModel::Errors` que puede decirnos exactamente qué errores están presentes.

También puede generar mensajes de error amigables para nosotros que podemos usar en nuestra interfaz de usuario.

```irb
store(dev)> product.errors.full_messages
=> ["Name can't be blank"]
```

Ahora construyamos una interfaz web para nuestros Products.

Hemos terminado con la consola por ahora, así que puedes salir ejecutando `exit`.

El Viaje de una Petición a Través de Rails
---------------------------------

Para lograr que Rails diga "Hola", necesitas crear como mínimo una _ruta_, un
_controller_ con una _action_, y una _view_. Una ruta mapea una petición a una
action del controller. Una action del controller realiza el trabajo necesario para manejar la
petición, y prepara cualquier dato para la view. Una view muestra datos en un formato
deseado.

En términos de implementación: Las routes son reglas escritas en un
[DSL (Domain-Specific Language)](https://en.wikipedia.org/wiki/Domain-specific_language) de Ruby.
Los controllers son clases Ruby, y sus métodos públicos son actions. Y las views
son templates, generalmente escritos en una mezcla de HTML y Ruby.

Eso es lo breve, pero vamos a recorrer cada uno de estos pasos con
más detalle a continuación.

Routes
------

En Rails, una route es la parte de la URL que determina cómo una petición HTTP
entrante es dirigida al controller y action apropiados para su procesamiento.
Primero, hagamos un repaso rápido sobre URLs y métodos de petición HTTP.

### Partes de una URL

Examinemos las diferentes partes de una URL:

```
https://example.org/products?sale=true&sort=asc
```

En esta URL, cada parte tiene un nombre:

- `https` es el **protocolo**
- `example.org` es el **host**
- `/products` es el **path**
- `?sale=true&sort=asc` son los **query parameters**

### Métodos HTTP y su Propósito

Las peticiones HTTP usan métodos para indicarle al servidor qué acción debe realizar para una
URL dada. Aquí están los métodos más comunes:

- Una petición `GET` le dice al servidor que recupere los datos para una URL dada (ej.,
  cargar una página o buscar un registro).
- Una petición `POST` enviará datos a la URL para procesamiento (usualmente creando
  un nuevo registro).
- Una petición `PUT` o `PATCH` envía datos a una URL para actualizar un registro existente.
- Una petición `DELETE` a una URL le dice al servidor que elimine un registro.

### Routes de Rails

Una `route` en Rails se refiere a una línea de código que empareja un Método HTTP y una
ruta de URL. La route también le dice a Rails qué `controller` y `action` deben responder
a una petición.

Para definir una route en Rails, volvamos a tu editor de código y agrega la
siguiente route a `config/routes.rb`

```ruby
Rails.application.routes.draw do
  get "/products", to: "products#index"
end
```

Esta route le dice a Rails que busque peticiones GET a la ruta `/products`. En este
ejemplo, especificamos `"products#index"` para donde enrutar la petición.

Cuando Rails ve una petición que coincide, enviará la petición al
`ProductsController` y la action `index` dentro de ese controller. Así es
como Rails procesará la petición y devolverá una respuesta al navegador.

Notarás que no necesitamos especificar el protocolo, dominio, o query
params en nuestras routes. Eso es básicamente porque el protocolo y el dominio aseguran que
la petición llegue a tu servidor. Desde ahí, Rails recoge la petición y
sabe qué ruta usar para responder a la petición basándose en qué routes están
definidas. Los query params son como opciones que Rails puede usar para aplicar a la
petición, así que típicamente se usan en el controller para filtrar los datos.

<picture class="flowdiagram">
  <source srcset="images/routing_dark.jpg" media="(prefers-color-scheme:dark)">
  <img src="images/routing_light.jpg">
</picture>

Veamos otro ejemplo. Agrega esta línea después de la route anterior:

```ruby
post "/products", to: "products#create"
```

Aquí, le hemos dicho a Rails que tome peticiones POST a "/products" y las procese
con el `ProductsController` usando la action `create`.

Las routes también pueden necesitar coincidir con URLs con ciertos patrones. Entonces, ¿cómo funciona eso?

```ruby
get "/products/:id", to: "products#show"
```

Esta route tiene `:id` en ella. Esto se llama un `parameter` y captura una
porción de la URL para ser usada luego para procesar la petición.

Si un usuario visita `/products/1`, el param `:id` se establece en `1` y puede ser usado en
la action del controller para buscar y mostrar el registro de Product con un ID de 1.
`/products/2` mostraría Product con un ID de 2 y así sucesivamente.

Los parámetros de route no tienen que ser Integers, tampoco.

Por ejemplo, podrías tener un blog con artículos y coincidir `/blog/hello-world`
con la siguiente route:

```ruby
get "/blog/:title", to: "blog#show"
```

Rails capturará `hello-world` de `/blog/hello-world` y esto puede ser usado
para buscar el post del blog con el título coincidente.

#### Routes CRUD

Hay 4 acciones comunes que generalmente necesitarás para un recurso: Create, Read,
Update, Delete (CRUD). Esto se traduce a 8 routes típicas:

* Index - Muestra todos los registros
* New - Renderiza un formulario para crear un nuevo registro
* Create - Procesa el envío del nuevo formulario, manejando errores y creando el
  registro
* Show - Renderiza un registro específico para visualización
* Edit - Renderiza un formulario para actualizar un registro específico
* Update (completo) - Maneja el envío del formulario de edición, manejando errores y actualizando el registro completo, y típicamente disparado por una petición PUT.
* Update (parcial) - Maneja el envío del formulario de edición, manejando errores y actualizando atributos específicos del registro, y típicamente disparado por una petición PATCH.
* Destroy - Maneja la eliminación de un registro específico

Podemos agregar routes para estas acciones CRUD con lo siguiente:

```ruby
get "/products", to: "products#index"

get "/products/new", to: "products#new"
post "/products", to: "products#create"

get "/products/:id", to: "products#show"

get "/products/:id/edit", to: "products#edit"
patch "/products/:id", to: "products#update"
put "/products/:id", to: "products#update"

delete "/products/:id", to: "products#destroy"
```

#### Routes de Resource

Escribir estas routes cada vez es redundante, así que Rails proporciona un atajo
para definirlas. Para crear todas las mismas routes CRUD, reemplaza las routes anteriores
con esta única línea:

```ruby
resources :products
```

Consejo: Si no quieres todas estas acciones CRUD, puedes especificar exactamente lo que
necesitas. Consulta la [guía de routing](https://guides.rubyonrails.org/routing.html) para más detalles.

### Comando Routes

Rails proporciona un comando que muestra todas las routes a las que tu aplicación responde.

En tu terminal, ejecuta el siguiente comando.

```bash
$ bin/rails routes
```

Verás esto en la salida que son las routes generadas por
`resources :products`

```
      Prefix Verb   URI Pattern                  Controller#Action
    products GET    /products(.:format)          products#index
             POST   /products(.:format)          products#create
 new_product GET    /products/new(.:format)      products#new
edit_product GET    /products/:id/edit(.:format) products#edit
     product GET    /products/:id(.:format)      products#show
             PATCH  /products/:id(.:format)      products#update
             PUT    /products/:id(.:format)      products#update
             DELETE /products/:id(.:format)      products#destroy
```

También verás routes de otras características integradas de Rails como health checks.

Controllers & Actions
---------------------

Ahora que hemos definido routes para Products, implementemos el controller y
las actions para manejar peticiones a estas URLs.

Este comando generará un `ProductsController` con una action index. Como
ya hemos configurado routes, podemos omitir esa parte del generador usando un
flag.

```bash
$ bin/rails generate controller Products index --skip-routes
      create  app/controllers/products_controller.rb
      invoke  erb
      create    app/views/products
      create    app/views/products/index.html.erb
      invoke  test_unit
      create    test/controllers/products_controller_test.rb
      invoke  helper
      create    app/helpers/products_helper.rb
      invoke    test_unit
```

Este comando genera un puñado de archivos para nuestro controller:

* El controller mismo
* Una carpeta de views para el controller que generamos
* Un archivo de view para la action que especificamos al generar el controller
* Un archivo de test para este controller
* Un archivo helper para extraer lógica en nuestras views

Echemos un vistazo al ProductsController definido en
`app/controllers/products_controller.rb`. Se ve así:

```ruby
class ProductsController < ApplicationController
  def index
  end
end
```

Nota: Puede que notes que el nombre del archivo `products_controller.rb` es una versión
con guiones bajos de la Clase que este archivo define, `ProductsController`. Este patrón ayuda
a Rails a cargar automáticamente código sin tener que usar `require` como puedes
haber visto en otros lenguajes.

El método `index` aquí es una Action. Aunque es un método vacío, Rails
por defecto renderizará un template con el nombre coincidente.

La action `index` renderizará `app/views/products/index.html.erb`. Si abrimos
ese archivo en nuestro editor de código, veremos el HTML que renderiza.

```erb
<h1>Products#index</h1>
<p>Find me in app/views/products/index.html.erb</p>
```

### Haciendo Peticiones

Veamos esto en nuestro navegador. Primero, ejecuta `bin/rails server` en tu terminal para
iniciar el servidor Rails. Luego abre la URL de tu Codespace y verás la
página de bienvenida de Rails.

Nota: En GitHub Codespaces, tu aplicación no se ejecuta en `localhost:3000` sino en una URL única generada automáticamente. Para encontrar tu URL, ve a la pestaña "PORTS" (Puertos) en la parte inferior del editor de Codespaces, busca el puerto 3000 en la lista, y copia la URL que aparece en la columna "Forwarded Address". Esta URL tendrá un formato similar a `https://TU-CODESPACE.github.dev`. Usa esta URL cada vez que la guía mencione acceder a la aplicación.

Si abrimos https://TU-CODESPACE.github.dev/products en el navegador, Rails renderizará el
HTML de products index.

Nuestro navegador solicitó `/products` y Rails coincidió esta route con
`products#index`. Rails envió la petición al `ProductsController` y llamó
a la action `index`. Como esta action estaba vacía, Rails renderizó el template coincidente
en `app/views/products/index.html.erb` y lo devolvió a nuestro
navegador. ¡Genial!

Si abrimos `config/routes.rb`, podemos decirle a Rails que la route raíz debe renderizar
la action index de Products agregando esta línea:

```ruby
root "products#index"
```

Ahora cuando visites https://TU-CODESPACE.github.dev, Rails renderizará Products#index.

### Variables de Instancia

Llevemos esto un paso más allá y renderizemos algunos registros de nuestra base de datos.

En la action `index`, agreguemos una consulta de base de datos y asignémosla a una variable
de instancia. Rails usa variables de instancia (variables que comienzan con un @) para
compartir datos con las views.

```ruby
class ProductsController < ApplicationController
  def index
    @products = Product.all
  end
end
```

En `app/views/products/index.html.erb`, podemos reemplazar el HTML con este ERB:

```erb
<%= debug @products %>
```

ERB es la abreviatura de [Embedded Ruby](https://docs.ruby-lang.org/en/master/ERB.html)
y nos permite ejecutar código Ruby para generar dinámicamente HTML con Rails. La
etiqueta `<%= %>` le dice a ERB que ejecute el código Ruby dentro y muestre el valor
devuelto. En nuestro caso, esto toma `@products`, lo convierte a YAML, y muestra el
YAML.

Ahora actualiza https://TU-CODESPACE.github.dev/ en tu navegador y verás que la
salida ha cambiado. Lo que estás viendo son los registros en tu base de datos siendo
mostrados en formato YAML.

El helper `debug` imprime variables en formato YAML para ayudar con la depuración.
Por ejemplo, si no estuvieras prestando atención y escribieras singular `@product`
en lugar de plural `@products`, el helper debug podría ayudarte a identificar que la
variable no se estableció correctamente en el controller.

Consejo: Consulta la [guía de Action View Helpers](https://guides.rubyonrails.org/action_view_helpers.html) para ver
más helpers que están disponibles.

Actualicemos `app/views/products/index.html.erb` para renderizar todos los nombres de nuestros productos.

```erb
<h1>Products</h1>

<div id="products">
  <% @products.each do |product| %>
    <div>
      <%= product.name %>
    </div>
  <% end %>
</div>
```

Usando ERB, este código recorre cada producto en el objeto
`ActiveRecord::Relation` de `@products` y renderiza una etiqueta `<div>` conteniendo el nombre
del producto.

Hemos usado una nueva etiqueta ERB esta vez también. `<% %>` evalúa el código Ruby pero
no muestra el valor devuelto. Eso ignora la salida de `@products.each`
que mostraría un array que no queremos en nuestro HTML.

### Actions CRUD

Necesitamos poder acceder a productos individuales. Esta es la R en CRUD para leer
un recurso.

Ya hemos definido la route para productos individuales con nuestra
route `resources :products`. Esto genera `/products/:id` como una route que
apunta a `products#show`.

Ahora necesitamos agregar esa action al `ProductsController` y definir qué
sucede cuando es llamada.

### Mostrando Productos Individuales

Abre el controller Products y agrega la action `show` así:

```ruby
class ProductsController < ApplicationController
  def index
    @products = Product.all
  end

  def show
    @product = Product.find(params[:id])
  end
end
```

La action `show` aquí define el `@product` *singular* porque está cargando un
único registro de la base de datos, en otras palabras: Muestra este único producto. Usamos
plural `@products` en `index` porque estamos cargando múltiples productos.

Para consultar la base de datos, usamos `params` para acceder a los parámetros de la petición. En este
caso, estamos usando el `:id` de nuestra route `/products/:id`. Cuando visitamos
`/products/1`, el hash params contiene `{id: 1}` lo que resulta en que nuestra action `show`
llame a `Product.find(1)` para cargar el Product con ID de `1` de la
base de datos.

Necesitamos una view para la action show a continuación. Siguiendo las convenciones de nomenclatura de Rails,
el `ProductsController` espera views en `app/views` en una subcarpeta llamada
`products`.

La action `show` espera un archivo en `app/views/products/show.html.erb`. Vamos a
crear ese archivo en nuestro editor y agregar el siguiente contenido:

```erb
<h1><%= @product.name %></h1>

<%= link_to "Back", products_path %>
```

Sería útil que la página index enlazara a la página show para cada producto
para que podamos hacer clic en ellos para navegar. Podemos actualizar la
view `app/views/products/index.html.erb` para enlazar a esta nueva página usando una
etiqueta de anclaje a la ruta para la action `show`.

```erb#6,8
<h1>Products</h1>

<div id="products">
  <% @products.each do |product| %>
    <div>
      <a href="/products/<%= product.id %>">
        <%= product.name %>
      </a>
    </div>
  <% end %>
</div>
```

Actualiza esta página en tu navegador y verás que esto funciona, pero podemos hacer lo mejor.

Rails proporciona métodos helper para generar rutas y URLs. Cuando ejecutas
`bin/rails routes`, verás la columna Prefix. Este prefijo coincide con los
helpers que puedes usar para generar URLs con código Ruby.

```
  Prefix Verb   URI Pattern             Controller#Action
products GET    /products(.:format)     products#index
 product GET    /products/:id(.:format) products#show
```

Estos prefijos de route nos dan helpers como los siguientes:

* `products_path` genera `"/products"`
* `products_url` genera `"https://TU-CODESPACE.github.dev/products"`
* `product_path(1)` genera `"/products/1"`
* `product_url(1)` genera `"https://TU-CODESPACE.github.dev/products/1"`

`_path` devuelve una ruta relativa que el navegador entiende que es para el
dominio actual.

`_url` devuelve una URL completa incluyendo el protocolo, host, y puerto.

Los helpers de URL son útiles para renderizar emails que serán vistos fuera del
navegador.

Combinado con el helper `link_to`, podemos generar etiquetas de anclaje y usar el helper de
URL para hacer esto limpiamente en Ruby. `link_to` acepta el contenido de visualización para el
enlace (`product.name`) y la ruta o URL a la que enlazar para el atributo `href`
(`product`).

Refactoricemos esto para usar estos helpers:

```erb#6
<h1>Products</h1>

<div id="products">
  <% @products.each do |product| %>
    <div>
      <%= link_to product.name, product_path(product.id) %>
    </div>
  <% end %>
</div>
```

### Creando Products

Hasta ahora hemos tenido que crear productos en la consola de Rails, pero hagamos que esto
funcione en el navegador.

Necesitamos crear dos actions para create:

1. El formulario de nuevo producto para recopilar información del producto
2. La action create en el controller para guardar el producto y verificar errores

Comencemos con nuestras actions del controller.

```ruby
class ProductsController < ApplicationController
  def index
    @products = Product.all
  end

  def show
    @product = Product.find(params[:id])
  end

  def new
    @product = Product.new
  end
end
```

La action `new` instancia un nuevo `Product` que usaremos para mostrar
los campos del formulario.

Podemos actualizar `app/views/products/index.html.erb` para enlazar a la action new.

```erb#3
<h1>Products</h1>

<%= link_to "New product", new_product_path %>

<div id="products">
  <% @products.each do |product| %>
    <div>
      <%= link_to product.name, product_path(product.id) %>
    </div>
  <% end %>
</div>
```

Creemos `app/views/products/new.html.erb` para renderizar el formulario para este nuevo
`Product`.

```erb
<h1>New product</h1>

<%= form_with model: @product do |form| %>
  <div>
    <%= form.label :name %>
    <%= form.text_field :name %>
  </div>

  <div>
    <%= form.submit %>
  </div>
<% end %>

<%= link_to "Cancel", products_path %>
```

En esta view, estamos usando el helper `form_with` de Rails para generar un formulario HTML
para crear productos. Este helper usa un *form builder* para manejar cosas como tokens CSRF,
generar la URL basándose en el `model:` proporcionado, e incluso adaptar
el texto del botón de envío al model.

Si abres esta página en tu navegador y ves el código fuente, el HTML del formulario
se verá así:

```html
<form action="/products" accept-charset="UTF-8" method="post">
  <input type="hidden" name="authenticity_token" value="UHQSKXCaFqy_aoK760zpSMUPy6TMnsLNgbPMABwN1zpW-Jx6k-2mISiF0ulZOINmfxPdg5xMyZqdxSW1UK-H-Q" autocomplete="off">

  <div>
    <label for="product_name">Name</label>
    <input type="text" name="product[name]" id="product_name">
  </div>

  <div>
    <input type="submit" name="commit" value="Create Product" data-disable-with="Create Product">
  </div>
</form>
```

El form builder ha incluido un token CSRF para seguridad, configuró el formulario para
soporte UTF-8, estableció los nombres de los campos de entrada e incluso agregó un estado deshabilitado para el
botón de envío.

Porque pasamos una nueva instancia de `Product` al form builder, automáticamente
generó un formulario configurado para enviar una petición `POST` a `/products`, que es
la route predeterminada para crear un nuevo registro.

Para manejar esto, primero necesitamos implementar la action `create` en nuestro
controller.

```ruby#14-26
class ProductsController < ApplicationController
  def index
    @products = Product.all
  end

  def show
    @product = Product.find(params[:id])
  end

  def new
    @product = Product.new
  end

  def create
    @product = Product.new(product_params)
    if @product.save
      redirect_to @product
    else
      render :new, status: :unprocessable_entity
    end
  end

  private
    def product_params
      params.expect(product: [ :name ])
    end
end
```

#### Strong Parameters

La action `create` maneja los datos enviados por el formulario, pero necesitan ser
filtrados por seguridad. Ahí es donde entra en juego el método `product_params`.

En `product_params`, le decimos a Rails que inspeccione los params y asegure que hay una
clave llamada `:product` con un array de parámetros como valor. Los únicos
parámetros permitidos para products es `:name` y Rails ignorará cualquier otro
parámetro. Esto protege nuestra aplicación de usuarios maliciosos que podrían intentar
hackear nuestra aplicación.

#### Manejando Errores

Después de asignar estos params al nuevo `Product`, podemos intentar guardarlo en la
base de datos. `@product.save` le dice a Active Record que ejecute validaciones y guarde el
registro en la base de datos.

Si `save` es exitoso, queremos redirigir al nuevo producto. Cuando
se le da un objeto Active Record a `redirect_to`, Rails genera una ruta para la
action show de ese registro.

```ruby
redirect_to @product
```

Como `@product` es una instancia de `Product`, Rails pluraliza el nombre del model e
incluye el ID del objeto en la ruta para producir `"/products/2"` para la
redirección.

Cuando `save` no es exitoso y el registro no fue válido, queremos re-renderizar
el formulario para que el usuario pueda corregir los datos inválidos. En la cláusula `else`, le decimos
a Rails que `render :new`. Rails sabe que estamos en el controller `Products`, así que
debe renderizar `app/views/products/new.html.erb`. Como hemos establecido la variable `@product`
en `create`, podemos renderizar ese template y el formulario se llenará
con nuestros datos de `Product` aunque no pudo guardarse en la base de datos.

También establecemos el estado HTTP en 422 Unprocessable Entity para decirle al navegador que esta
petición POST falló y que lo maneje en consecuencia.

### Editando Products

El proceso de editar registros es muy similar a crear registros. En lugar de
actions `new` y `create`, tendremos `edit` y `update`.

Implementémoslas en el controller con lo siguiente:

```ruby#23-34
class ProductsController < ApplicationController
  def index
    @products = Product.all
  end

  def show
    @product = Product.find(params[:id])
  end

  def new
    @product = Product.new
  end

  def create
    @product = Product.new(product_params)
    if @product.save
      redirect_to @product
    else
      render :new, status: :unprocessable_entity
    end
  end

  def edit
    @product = Product.find(params[:id])
  end

  def update
    @product = Product.find(params[:id])
    if @product.update(product_params)
      redirect_to @product
    else
      render :edit, status: :unprocessable_entity
    end
  end

  private
    def product_params
      params.expect(product: [ :name ])
    end
end
```

#### Extrayendo Partials

Ya hemos escrito un formulario para crear nuevos productos. ¿No sería bueno si
pudiéramos reutilizarlo para edit y update? Podemos, usando una característica llamada
"partials" que te permite reutilizar una view en múltiples lugares.

Podemos mover el formulario a un archivo llamado `app/views/products/_form.html.erb`. El
nombre del archivo comienza con un guion bajo para denotar que esto es un partial.

También queremos reemplazar cualquier variable de instancia con una variable local, que podemos
definir cuando renderizamos el partial. Haremos esto reemplazando `@product`
con `product`.

También mostremos cualquier error del envío del formulario dentro del formulario.

```erb#1-4
<%= form_with model: product do |form| %>
  <% if form.object.errors.any? %>
    <p class="error"><%= form.object.errors.full_messages.first %></p>
  <% end %>

  <div>
    <%= form.label :name %>
    <%= form.text_field :name %>
  </div>

  <div>
    <%= form.submit %>
  </div>
<% end %>
```

Consejo: Usar variables locales permite que los partials sean reutilizados múltiples veces en la
misma página con un valor diferente cada vez. Esto es útil para renderizar listas
de elementos como una página index.

Para usar este partial en nuestra view `app/views/products/new.html.erb`, podemos
reemplazar el formulario con una llamada render:

```erb#3
<h1>New product</h1>

<%= render "form", product: @product %>
<%= link_to "Cancel", products_path %>
```

La view edit se vuelve casi exactamente lo mismo gracias al partial del formulario.
Creemos `app/views/products/edit.html.erb` con lo siguiente:

```erb#3
<h1>Edit product</h1>

<%= render "form", product: @product %>
<%= link_to "Cancel", @product %>
```

Para aprender más sobre partials de view, consulta la
[Guía de Action View](https://guides.rubyonrails.org/action_view_overview.html).

Ahora podemos agregar un enlace Edit a `app/views/products/show.html.erb`:

```erb#4
<h1><%= @product.name %></h1>

<%= link_to "Back", products_path %>
<%= link_to "Edit", edit_product_path(@product) %>
```

#### Before Actions

Como `edit` y `update` requieren un registro de base de datos existente como `show` podemos
desduplicar esto en un `before_action`.

Un `before_action` te permite extraer código compartido entre actions y ejecutarlo
*antes* de la action. En el código del controller anterior,
`@product = Product.find(params[:id])` está definido en tres métodos diferentes.
Extraer esta consulta a un before action llamado `set_product` limpia nuestro código
para cada action.

Este es un buen ejemplo de la filosofía DRY (Don't Repeat Yourself) en acción.

```ruby#2,8-9,24-25,27-33,36-38
class ProductsController < ApplicationController
  before_action :set_product, only: %i[ show edit update ]

  def index
    @products = Product.all
  end

  def show
  end

  def new
    @product = Product.new
  end

  def create
    @product = Product.new(product_params)
    if @product.save
      redirect_to @product
    else
      render :new, status: :unprocessable_entity
    end
  end

  def edit
  end

  def update
    if @product.update(product_params)
      redirect_to @product
    else
      render :edit, status: :unprocessable_entity
    end
  end

  private
    def set_product
      @product = Product.find(params[:id])
    end

    def product_params
      params.expect(product: [ :name ])
    end
end
```

### Eliminando Products

La última característica que necesitamos implementar es eliminar productos. Agregaremos una
action `destroy` a nuestro `ProductsController` para manejar peticiones `DELETE /products/:id`.

Agregar `destroy` a `before_action :set_product` nos permite establecer la variable
de instancia `@product` de la misma manera que lo hacemos para las otras actions.

```ruby#2,35-38
class ProductsController < ApplicationController
  before_action :set_product, only: %i[ show edit update destroy ]

  def index
    @products = Product.all
  end

  def show
  end

  def new
    @product = Product.new
  end

  def create
    @product = Product.new(product_params)
    if @product.save
      redirect_to @product
    else
      render :new, status: :unprocessable_entity
    end
  end

  def edit
  end

  def update
    if @product.update(product_params)
      redirect_to @product
    else
      render :edit, status: :unprocessable_entity
    end
  end

  def destroy
    @product.destroy
    redirect_to products_path
  end

  private
    def set_product
      @product = Product.find(params[:id])
    end

    def product_params
      params.expect(product: [ :name ])
    end
end
```

Para hacer que esto funcione, necesitamos agregar un botón Delete a
`app/views/products/show.html.erb`:

```erb#5
<h1><%= @product.name %></h1>

<%= link_to "Back", products_path %>
<%= link_to "Edit", edit_product_path(@product) %>
<%= button_to "Delete", @product, method: :delete, data: { turbo_confirm: "Are you sure?" } %>
```

`button_to` genera un formulario con un único botón en él con el texto "Delete".
Cuando este botón se hace clic, envía el formulario que hace una petición `DELETE`
a `/products/:id` que activa la action `destroy` en nuestro controller.

El atributo de datos `turbo_confirm` le dice a la biblioteca JavaScript de Turbo que pregunte al
usuario que confirme antes de enviar el formulario. Profundizaremos más en eso en breve.

Agregando Autenticación
---------------------

Cualquiera puede editar o eliminar productos, lo cual no es seguro. Agreguemos algo de seguridad
requiriendo que un usuario esté autenticado para administrar productos.

Rails viene con un generador de autenticación que podemos usar. Crea models User
y Session y los controllers y views necesarios para iniciar sesión en nuestra
aplicación.

Regresa a tu terminal y ejecuta el siguiente comando:

```bash
$ bin/rails generate authentication
```

Luego migra la base de datos para agregar las tablas User y Session.

```bash
$ bin/rails db:migrate
```

Abre la consola de Rails para crear un User.

```bash
$ bin/rails console
```

Usa el método `User.create!` para crear un User en la consola de Rails. Siéntete libre de
usar tu propio email y contraseña en lugar del ejemplo.

```irb
store(dev)> User.create! email_address: "you@example.org", password: "s3cr3t", password_confirmation: "s3cr3t"
```

Reinicia tu servidor Rails para que cargue la gema `bcrypt` agregada por el
generador. BCrypt se usa para hacer hash seguro de contraseñas para autenticación.

```bash
$ bin/rails server
```

Cuando visites cualquier página, Rails solicitará un nombre de usuario y contraseña. Ingresa
el email y contraseña que usaste al crear el registro User.

Pruébalo visitando https://TU-CODESPACE.github.dev/products/new

Si ingresas el nombre de usuario y contraseña correctos, te permitirá pasar. Tu
navegador también almacenará estas credenciales para futuras peticiones para que no tengas que
escribirlas en cada vista de página.


### Agregando Log Out

Para cerrar sesión en la aplicación, podemos agregar un botón en la parte superior de
`app/views/layouts/application.html.erb`. Este layout es donde colocas HTML que
quieres incluir en cada página como un encabezado o pie de página.

Agrega una pequeña sección `<nav>` dentro del `<body>` con un enlace a Home y un
botón Log out y envuelve `yield` con una etiqueta `<main>`.

```erb#5-8,10,12
<!DOCTYPE html>
<html>
  <!-- ... -->
  <body>
    <nav>
      <%= link_to "Home", root_path %>
      <%= button_to "Log out", session_path, method: :delete if authenticated? %>
    </nav>

    <main>
      <%= yield %>
    </main>
  </body>
</html>
```

Esto mostrará un botón Log out solo si el usuario está autenticado. Cuando
se hace clic, enviará una petición DELETE a la ruta session que cerrará la sesión del
usuario.

### Permitiendo Acceso No Autenticado

Sin embargo, las páginas index y show de productos de nuestra tienda deberían ser accesibles para
todos. Por defecto, el generador de autenticación de Rails restringirá todas las páginas
solo a usuarios autenticados.

Para permitir que los invitados vean productos, podemos permitir acceso no autenticado en nuestro
controller.

```ruby#2
class ProductsController < ApplicationController
  allow_unauthenticated_access only: %i[ index show ]
  # ...
end
```

Cierra sesión y visita las páginas index y show de productos para ver que son accesibles
sin estar autenticado.

### Mostrando Enlaces Solo para Usuarios Autenticados

Como solo los usuarios con sesión iniciada pueden crear productos, podemos modificar la
view `app/views/products/index.html.erb` para mostrar solo el enlace de nuevo producto si
el usuario está autenticado.

```erb
<%= link_to "New product", new_product_path if authenticated? %>
```

Haz clic en el botón Log out y verás que el enlace New está oculto. Inicia sesión en
https://TU-CODESPACE.github.dev/session/new y verás el enlace New en la página index.

Opcionalmente, puedes incluir un enlace a esta route en la barra de navegación para agregar un enlace Login
si no está autenticado.

```erb
<%= link_to "Login", new_session_path unless authenticated? %>
```

También puedes actualizar los enlaces Edit y Delete en la
view `app/views/products/show.html.erb` para mostrarlos solo si está autenticado.

```erb#4,7
<h1><%= @product.name %></h1>

<%= link_to "Back", products_path %>
<% if authenticated? %>
  <%= link_to "Edit", edit_product_path(@product) %>
  <%= button_to "Delete", @product, method: :delete, data: { turbo_confirm: "Are you sure?" } %>
<% end %>
```

Carga de Archivos con Active Storage
--------------------------------

Active Storage es una característica de Rails que hace fácil cargar archivos.

Agreguemos una imagen destacada al
model `Product`.

```ruby#2
class Product < ApplicationRecord
  has_one_attached :featured_image
  validates :name, presence: true
end
```

Luego podemos agregar un campo de carga de archivo a nuestro formulario de producto antes del botón
de envío:

```erb#4-7
<%= form_with model: product do |form| %>
  <%# ... %>

  <div>
    <%= form.label :featured_image, style: "display: block" %>
    <%= form.file_field :featured_image, accept: "image/*" %>
  </div>

  <div>
    <%= form.submit %>
  </div>
<% end %>
```

Agrega `:featured_image` como un parámetro permitido en
`app/controllers/products_controller.rb`

```ruby#3
    # Only allow a list of trusted parameters through.
    def product_params
      params.expect(product: [ :name, :description, :featured_image ])
    end
```

Por último, queremos mostrar la imagen destacada para nuestro producto en
`app/views/products/show.html.erb`. Agrega lo siguiente en la parte superior.

```erb
<%= image_tag @product.featured_image if @product.featured_image.attached? %>
```

Intenta cargar una imagen para un producto y verás la imagen mostrada en la
página show después de guardar.

Consulta la [Descripción General de Active Storage](https://guides.rubyonrails.org/active_storage_overview.html) para más
detalles.

Agregando CSS
-----------------------

CSS es fundamental para construir aplicaciones web, así que aprendamos cómo
usarlos con Rails.

### Propshaft

El pipeline de assets de Rails se llama Propshaft. Toma tu CSS, JavaScript,
imágenes, y otros assets y los sirve a tu navegador. En producción,
Propshaft hace seguimiento de cada versión de tus assets para que puedan ser almacenados en caché para hacer tus páginas más rápidas. Consulta la [guía de Asset Pipeline](https://guides.rubyonrails.org/asset_pipeline.html) para aprender más sobre cómo funciona esto.

Modifiquemos `app/assets/stylesheets/application.css` y agreguemos el siguiente contenido.

```css
body {
  font-family: Arial, Helvetica, sans-serif;
  padding: 1rem;
}

nav {
  justify-content: flex-end;
  display: flex;
  font-size: 0.875em;
  gap: 0.5rem;
  max-width: 1024px;
  margin: 0 auto;
  padding: 1rem;
}

nav a {
  display: inline-block;
}

main {
  max-width: 1024px;
  margin: 0 auto;
}

.alert,
.error {
  color: red;
}

.notice {
  color: green;
}

section.product {
  display: flex;
  gap: 1rem;
  flex-direction: row;
}

section.product img {
  border-radius: 8px;
  flex-basis: 50%;
  max-width: 50%;
}
```

Luego actualizaremos `app/views/products/show.html.erb` para usar estos nuevos estilos.

```erb#1,3,6,18-19
<p><%= link_to "Back", products_path %></p>

<section class="product">
  <%= image_tag @product.featured_image if @product.featured_image.attached? %>

  <section class="product-info">
    <% cache @product do %>
      <h1><%= @product.name %></h1>
      <%= @product.description %>
    <% end %>

    <%= render "inventory", product: @product %>

    <% if authenticated? %>
      <%= link_to "Edit", edit_product_path(@product) %>
      <%= button_to "Delete", @product, method: :delete, data: { turbo_confirm: "Are you sure?" } %>
    <% end %>
  </section>
</section>
```

Actualiza tu página y verás que el CSS ha sido aplicado.

¿Qué Sigue?
------------

¡Felicitaciones por construir tu primera aplicación Rails!

A continuación, sigue la [guía completa Getting Started with Rails](https://guides.rubyonrails.org/getting_started.html) para continuar aprendiendo.

También recomendamos aprender más leyendo otras Guías de Ruby on Rails:
* [Tutorial Sign Up and Settings](sign_up_and_settings.html)
* [Fundamentos de Active Record](active_record_basics.html)
* [Layouts y Renderizado en Rails](layouts_and_rendering.html)
* [Testing de Aplicaciones Rails](testing.html)
* [Depurando Aplicaciones Rails](debugging_rails_applications.html)
* [Asegurando Aplicaciones Rails](security.html)


¡Feliz construcción!
