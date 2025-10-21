# Primeros Pasos con Rails - Taller Intensivo de 2 Días

Esta guía te ayudará a construir tu primera aplicación Rails en 2 días.

Después de completar este taller, sabrás:

* Cómo crear una aplicación Rails funcional desde cero.
* Los fundamentos de MVC (Modelo, Vista, Controlador).
* Cómo trabajar con base de datos usando Active Record.
* Cómo crear interfaces atractivas con HTML y CSS.
* Lo suficiente para querer seguir aprendiendo Rails.

--------------------------------------------------------------------------------

Introducción
------------

¡Bienvenido a Ruby on Rails! En esta guía intensiva de 2 días, construirás una aplicación web funcional y atractiva. No necesitas experiencia previa con Rails para seguir esta guía, solo conocimientos muy básicos de Ruby.

Rails es un framework web construido para el lenguaje de programación Ruby. Está diseñado para facilitar la programación de aplicaciones web haciendo suposiciones sobre lo que cada desarrollador necesita para comenzar. Te permite escribir menos código mientras logras más que con muchos otros lenguajes y frameworks.

**Estructura del taller:**
- **Día 1 - Sesión Mañana (3 horas):** Configuración, modelo, consola y rutas
- **Día 1 - Sesión Tarde (3 horas):** Controladores, vistas y CRUD básico
- **Día 2 - Sesión Mañana (3 horas):** Estilos CSS y funcionalidades adicionales
- **Día 2 - Sesión Tarde (3 horas):** Toques finales y características avanzadas

### Lo Que Construiremos

Vamos a construir **"Mi Tienda Simple"** - una aplicación de catálogo de productos donde podrás:
- Ver lista de productos
- Agregar nuevos productos
- Editar productos existentes
- Eliminar productos
- Todo con una interfaz visualmente atractiva

Filosofía de Rails
------------------

Rails es software opinado. Asume que hay una "mejor" forma de hacer las cosas y está diseñado para fomentar esa forma. Si aprendes "La Forma Rails" probablemente descubrirás un tremendo aumento en productividad.

La filosofía de Rails incluye dos principios rectores principales:

- **No Te Repitas (DRY):** No escribirás la misma información una y otra vez, nuestro código será más mantenible y menos propenso a errores.
- **Convención Sobre Configuración:** Rails utiliza por defecto un conjunto de convenciones, en lugar de requerir que las definas tú mismo a través de interminables archivos de configuración.

--------------------------------------------------------------------------------

DÍA 1 - SESIÓN MAÑANA (3 horas): Fundamentos
=============================================

Creando Tu Primera Aplicación Rails (15 minutos)
-------------------------------------------------

### Prerrequisitos

Para este proyecto, necesitarás:

* Ruby 3.2 o más reciente
* Rails 8.0 o más reciente
* Un editor de código (VS Code, Sublime, etc.)

TIP: Cualquier comando precedido por un signo de dólar `$` debe ejecutarse en la terminal.

Verifiquemos que tienes la versión correcta de Rails instalada:

```bash
$ rails --version
Rails 8.2.0
```

### Creando la Aplicación

Rails viene con varios comandos para facilitar la vida. `rails new` genera los cimientos de una aplicación Rails nueva para ti.

```bash
$ rails new mi_tienda
```

Después de que tu nueva aplicación sea creada, cambia a su directorio:

```bash
$ cd mi_tienda
```

### Estructura Básica de Directorios

Estos son los directorios más importantes:

| Carpeta | Propósito |
| ------- | --------- |
|app/|Contiene los controladores, modelos, vistas y assets. **Aquí trabajarás principalmente.**|
|config/|Configuración de rutas, base de datos y más.|
|db/|Contiene el esquema de base de datos y las migraciones.|

### Fundamentos de Modelo-Vista-Controlador

El código de Rails se organiza usando la arquitectura MVC:

* **Modelo** - Gestiona los datos (tus tablas de base de datos)
* **Vista** - Lo que ves en el navegador (HTML)
* **Controlador** - Conecta el modelo con la vista

¡Hola, Rails! (10 minutos)
---------------------------

Empecemos creando la base de datos e iniciando el servidor:

```bash
$ bin/rails db:create
$ bin/rails server
```

Esto iniciará un servidor web llamado Puma. Abre http://localhost:3000 en tu navegador. Verás la página de bienvenida de Rails:

¡Funciona!

TIP: Para detener el servidor Rails en cualquier momento, presiona `Ctrl-C` en tu terminal.

### Autocarga en Desarrollo

Una vez que inicies el servidor Rails, los archivos nuevos o cambios a archivos existentes son detectados y automáticamente recargados. Esto te permite enfocarte en construir sin tener que reiniciar tu servidor Rails después de cada cambio.

Creando el Modelo Product (30 minutos)
---------------------------------------

Active Record es una característica de Rails que mapea bases de datos relacionales a código Ruby. Comencemos agregando una tabla de base de datos para productos.

```bash
$ bin/rails generate model Product name:string price:decimal
```

NOTE: Los nombres de modelos son *singulares* (Product), porque un modelo instanciado representa un solo registro en la base de datos.

Verás lo siguiente en tu terminal:

```bash
      invoke  active_record
      create    db/migrate/20240426151900_create_products.rb
      create    app/models/product.rb
      invoke    test_unit
      create      test/models/product_test.rb
      create      test/fixtures/products.yml
```

### Migraciones de Base de Datos

Abre la migración en `db/migrate/<timestamp>_create_products.rb`:

```ruby
class CreateProducts < ActiveRecord::Migration[8.2]
  def change
    create_table :products do |t|
      t.string :name
      t.decimal :price

      t.timestamps
    end
  end
end
```

Esta migración le dice a Rails que cree una tabla `products` con columnas `name`, `price`, `created_at` y `updated_at`.

Vamos a mejorar esto. Modifica la línea de `price` para especificar precisión:

```ruby
t.decimal :price, precision: 10, scale: 2
```

### Ejecutando Migraciones

Ahora ejecuta la migración para crear la tabla:

```bash
$ bin/rails db:migrate
```

### Agregando Validaciones

Abre el archivo `app/models/product.rb` y agrégale validaciones:

```ruby
class Product < ApplicationRecord
  validates :name, presence: true
  validates :price, presence: true, numericality: { greater_than_or_equal_to: 0 }
end
```

Consola de Rails (25 minutos)
------------------------------

La consola es una herramienta interactiva para probar tu código Rails.

```bash
$ bin/rails console
```

### Creando Registros

Crea algunos productos de ejemplo:

```ruby
# Crear productos
Product.create(name: "Camiseta", price: 25.99)
Product.create(name: "Pantalones", price: 45.50)
Product.create(name: "Zapatos", price: 89.99)

# Ver todos los productos
Product.all

# Contar productos
Product.count
```

### Consultando Registros

```ruby
# Encontrar todos
Product.all

# Encontrar por ID
Product.find(1)

# Buscar por nombre
Product.where(name: "Camiseta")

# Ordenar por precio
Product.order(price: :asc)
```

### Actualizando Registros

```ruby
product = Product.find(1)
product.update(price: 29.99)
```

### Eliminando Registros

```ruby
product = Product.find(1)
product.destroy
```

Para salir de la consola, escribe `exit`.

Creando Rutas (20 minutos)
---------------------------

Las rutas le dicen a Rails qué hacer cuando alguien visita una URL.

Abre `config/routes.rb` y reemplaza el contenido con:

```ruby
Rails.application.routes.draw do
  root "products#index"
  resources :products
end
```

La línea `resources :products` crea automáticamente todas las rutas necesarias para operaciones CRUD.

Para ver todas las rutas:

```bash
$ bin/rails routes
```

Verás algo así:

```
      Prefix Verb   URI Pattern                  Controller#Action
    products GET    /products(.:format)          products#index
             POST   /products(.:format)          products#create
 new_product GET    /products/new(.:format)      products#new
edit_product GET    /products/:id/edit(.:format) products#edit
     product GET    /products/:id(.:format)      products#show
             PATCH  /products/:id(.:format)      products#update
             DELETE /products/:id(.:format)      products#destroy
```

Creando el Controlador (20 minutos)
------------------------------------

El controlador es el cerebro de tu aplicación.

```bash
$ bin/rails generate controller Products index --skip-routes
```

Abre `app/controllers/products_controller.rb` y reemplaza todo con:

```ruby
class ProductsController < ApplicationController
  before_action :set_product, only: %i[ show edit update destroy ]

  def index
    @products = Product.all.order(created_at: :desc)
  end

  def show
  end

  def new
    @product = Product.new
  end

  def create
    @product = Product.new(product_params)
    if @product.save
      redirect_to products_path, notice: "Producto creado exitosamente."
    else
      render :new, status: :unprocessable_entity
    end
  end

  def edit
  end

  def update
    if @product.update(product_params)
      redirect_to products_path, notice: "Producto actualizado."
    else
      render :edit, status: :unprocessable_entity
    end
  end

  def destroy
    @product.destroy
    redirect_to products_path, notice: "Producto eliminado."
  end

  private

  def set_product
    @product = Product.find(params[:id])
  end

  def product_params
    params.require(:product).permit(:name, :price)
  end
end
```

**PAUSA - Fin de Sesión Mañana Día 1**

--------------------------------------------------------------------------------

DÍA 1 - SESIÓN TARDE (3 horas): Vistas y CRUD
==============================================

Creando las Vistas (50 minutos)
--------------------------------

### Vista Principal (Index)

Crea el archivo `app/views/products/index.html.erb`:

```erb
<div class="container">
  <div class="header">
    <h1>🛍️ Mi Tienda</h1>
    <%= link_to "Nuevo Producto", new_product_path, class: "btn-primary" %>
  </div>

  <% if notice %>
    <div class="notice"><%= notice %></div>
  <% end %>

  <% if @products.empty? %>
    <div class="empty-state">
      <p>No hay productos aún</p>
      <p>Comienza agregando tu primer producto</p>
    </div>
  <% else %>
    <div class="products-grid">
      <% @products.each do |product| %>
        <div class="product-card">
          <h3><%= product.name %></h3>
          <p class="price">$<%= number_with_precision(product.price, precision: 2) %></p>
          <div class="card-actions">
            <%= link_to "Ver", product_path(product), class: "btn-view" %>
            <%= link_to "Editar", edit_product_path(product), class: "btn-edit" %>
            <%= button_to "Eliminar", product_path(product), method: :delete,
                data: { turbo_confirm: "¿Estás seguro?" }, class: "btn-delete" %>
          </div>
        </div>
      <% end %>
    </div>
  <% end %>
</div>
```

### Formulario Reutilizable

Crea `app/views/products/_form.html.erb`:

```erb
<%= form_with(model: product, class: "product-form") do |form| %>
  <% if product.errors.any? %>
    <div class="errors">
      <h3>Se encontraron errores:</h3>
      <ul>
        <% product.errors.full_messages.each do |message| %>
          <li><%= message %></li>
        <% end %>
      </ul>
    </div>
  <% end %>

  <div class="form-group">
    <%= form.label :name, "Nombre del producto" %>
    <%= form.text_field :name, placeholder: "Ej: Camiseta básica", class: "form-input" %>
  </div>

  <div class="form-group">
    <%= form.label :price, "Precio" %>
    <%= form.number_field :price, step: 0.01, placeholder: "0.00", class: "form-input" %>
  </div>

  <div class="form-actions">
    <%= form.submit class: "btn-submit" %>
    <%= link_to "Cancelar", products_path, class: "btn-cancel" %>
  </div>
<% end %>
```

### Vista para Nuevo Producto

Crea `app/views/products/new.html.erb`:

```erb
<div class="container">
  <div class="form-container">
    <h1>Nuevo Producto</h1>
    <%= render "form", product: @product %>
  </div>
</div>
```

### Vista para Editar Producto

Crea `app/views/products/edit.html.erb`:

```erb
<div class="container">
  <div class="form-container">
    <h1>Editar Producto</h1>
    <%= render "form", product: @product %>
  </div>
</div>
```

### Vista para Ver Producto Individual

Crea `app/views/products/show.html.erb`:

```erb
<div class="container">
  <div class="product-detail">
    <h1><%= @product.name %></h1>
    <p class="price-large">$<%= number_with_precision(@product.price, precision: 2) %></p>

    <div class="detail-meta">
      <p><strong>Creado:</strong> <%= @product.created_at.strftime("%d/%m/%Y %H:%M") %></p>
      <p><strong>Actualizado:</strong> <%= @product.updated_at.strftime("%d/%m/%Y %H:%M") %></p>
    </div>

    <div class="detail-actions">
      <%= link_to "← Volver", products_path, class: "btn-back" %>
      <%= link_to "Editar", edit_product_path(@product), class: "btn-edit" %>
      <%= button_to "Eliminar", product_path(@product), method: :delete,
          data: { turbo_confirm: "¿Estás seguro?" }, class: "btn-delete" %>
    </div>
  </div>
</div>
```

Probando la Aplicación (10 minutos)
------------------------------------

Inicia tu servidor:

```bash
$ bin/rails server
```

Visita http://localhost:3000 y prueba:

1. Ver la lista de productos
2. Crear un nuevo producto
3. Ver un producto individual
4. Editar un producto
5. Eliminar un producto

Agregando Estilos CSS Básicos (60 minutos)
-------------------------------------------

Abre `app/assets/stylesheets/application.css` y reemplaza todo con:

```css
/* Reset y Base */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  min-height: 100vh;
  padding: 2rem 1rem;
  color: #333;
}

/* Container */
.container {
  max-width: 1200px;
  margin: 0 auto;
}

/* Header */
.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background: white;
  padding: 1.5rem 2rem;
  border-radius: 15px;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
  margin-bottom: 2rem;
}

.header h1 {
  color: #667eea;
  font-size: 2rem;
}

/* Botones */
.btn-primary, .btn-submit {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  padding: 0.75rem 1.5rem;
  text-decoration: none;
  border-radius: 25px;
  border: none;
  font-weight: 600;
  cursor: pointer;
  transition: transform 0.2s;
  display: inline-block;
}

.btn-primary:hover, .btn-submit:hover {
  transform: translateY(-2px);
}

.btn-view, .btn-edit, .btn-delete, .btn-cancel, .btn-back {
  padding: 0.5rem 1rem;
  text-decoration: none;
  border-radius: 8px;
  font-size: 0.875rem;
  border: none;
  cursor: pointer;
  transition: all 0.2s;
  display: inline-block;
  font-weight: 500;
}

.btn-view {
  background: #4299e1;
  color: white;
}

.btn-edit {
  background: #48bb78;
  color: white;
}

.btn-delete {
  background: #f56565;
  color: white;
}

.btn-cancel, .btn-back {
  background: #e2e8f0;
  color: #4a5568;
}

/* Notificaciones */
.notice {
  background: #48bb78;
  color: white;
  padding: 1rem 1.5rem;
  border-radius: 10px;
  margin-bottom: 1.5rem;
  text-align: center;
  animation: slideDown 0.3s;
}

@keyframes slideDown {
  from {
    opacity: 0;
    transform: translateY(-20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

/* Estado Vacío */
.empty-state {
  background: white;
  padding: 4rem 2rem;
  border-radius: 15px;
  text-align: center;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
}

.empty-state p:first-child {
  font-size: 1.5rem;
  color: #667eea;
  margin-bottom: 0.5rem;
}

/* Grid de Productos */
.products-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
  gap: 1.5rem;
}

/* Tarjeta de Producto */
.product-card {
  background: white;
  border-radius: 15px;
  padding: 1.5rem;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
  transition: transform 0.2s;
}

.product-card:hover {
  transform: translateY(-5px);
}

.product-card h3 {
  color: #2d3748;
  margin-bottom: 0.5rem;
  font-size: 1.25rem;
}

.product-card .price {
  color: #667eea;
  font-size: 1.5rem;
  font-weight: 700;
  margin: 1rem 0;
}

.card-actions {
  display: flex;
  gap: 0.5rem;
  flex-wrap: wrap;
  padding-top: 1rem;
  border-top: 1px solid #e2e8f0;
}

/* Formularios */
.form-container {
  background: white;
  padding: 2rem;
  border-radius: 15px;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
  max-width: 600px;
  margin: 0 auto;
}

.product-form {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
}

.form-group {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
}

.form-group label {
  color: #2d3748;
  font-weight: 600;
}

.form-input {
  padding: 0.75rem;
  border: 2px solid #e2e8f0;
  border-radius: 8px;
  font-size: 1rem;
  transition: border-color 0.2s;
}

.form-input:focus {
  outline: none;
  border-color: #667eea;
}

.form-actions {
  display: flex;
  gap: 1rem;
  margin-top: 1rem;
}

/* Errores */
.errors {
  background: #fed7d7;
  border-left: 4px solid #f56565;
  padding: 1rem;
  border-radius: 8px;
  margin-bottom: 1rem;
}

.errors h3 {
  color: #742a2a;
  margin-bottom: 0.5rem;
}

.errors ul {
  list-style-position: inside;
  color: #742a2a;
}

/* Detalle de Producto */
.product-detail {
  background: white;
  padding: 2rem;
  border-radius: 15px;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
  text-align: center;
}

.product-detail h1 {
  color: #2d3748;
  margin-bottom: 1rem;
}

.price-large {
  color: #667eea;
  font-size: 3rem;
  font-weight: 700;
  margin: 2rem 0;
}

.detail-meta {
  background: #f7fafc;
  padding: 1rem;
  border-radius: 8px;
  margin: 2rem 0;
}

.detail-meta p {
  color: #4a5568;
  margin: 0.5rem 0;
}

.detail-actions {
  display: flex;
  gap: 1rem;
  justify-content: center;
  flex-wrap: wrap;
}

/* Responsive */
@media (max-width: 768px) {
  .header {
    flex-direction: column;
    gap: 1rem;
  }

  .products-grid {
    grid-template-columns: 1fr;
  }

  .form-actions {
    flex-direction: column;
  }
}
```

Mejorando Mensajes de Validación (20 minutos)
----------------------------------------------

Rails tiene mensajes de validación en inglés por defecto. Vamos a personalizarlos.

Abre `app/models/product.rb` y actualiza:

```ruby
class Product < ApplicationRecord
  validates :name, presence: { message: "no puede estar en blanco" }
  validates :price, presence: { message: "no puede estar en blanco" },
                    numericality: { greater_than_or_equal_to: 0,
                                    message: "debe ser mayor o igual a 0" }
end
```

**PAUSA - Fin de Sesión Tarde Día 1**

--------------------------------------------------------------------------------

DÍA 2 - SESIÓN MAÑANA (3 horas): Mejoras Visuales
==================================================

Agregando Más Información a los Productos (40 minutos)
-------------------------------------------------------

Vamos a agregar un campo de descripción a nuestros productos.

### Crear la Migración

```bash
$ bin/rails generate migration AddDescriptionToProducts description:text
```

Ejecuta la migración:

```bash
$ bin/rails db:migrate
```

### Actualizar el Modelo

En `app/models/product.rb`:

```ruby
class Product < ApplicationRecord
  validates :name, presence: { message: "no puede estar en blanco" }
  validates :price, presence: { message: "no puede estar en blanco" },
                    numericality: { greater_than_or_equal_to: 0,
                                    message: "debe ser mayor o igual a 0" }
  validates :description, length: { maximum: 500 }
end
```

### Actualizar el Controlador

En `app/controllers/products_controller.rb`, actualiza `product_params`:

```ruby
def product_params
  params.require(:product).permit(:name, :price, :description)
end
```

### Actualizar el Formulario

En `app/views/products/_form.html.erb`, agrega después del campo de precio:

```erb
<div class="form-group">
  <%= form.label :description, "Descripción (opcional)" %>
  <%= form.text_area :description, rows: 4,
      placeholder: "Describe tu producto...", class: "form-input" %>
</div>
```

### Actualizar las Vistas

En `app/views/products/index.html.erb`, actualiza la tarjeta de producto:

```erb
<div class="product-card">
  <h3><%= product.name %></h3>
  <% if product.description.present? %>
    <p class="description"><%= truncate(product.description, length: 100) %></p>
  <% end %>
  <p class="price">$<%= number_with_precision(product.price, precision: 2) %></p>
  <div class="card-actions">
    <%= link_to "Ver", product_path(product), class: "btn-view" %>
    <%= link_to "Editar", edit_product_path(product), class: "btn-edit" %>
    <%= button_to "Eliminar", product_path(product), method: :delete,
        data: { turbo_confirm: "¿Estás seguro?" }, class: "btn-delete" %>
  </div>
</div>
```

En `app/views/products/show.html.erb`, agrega después del título:

```erb
<% if @product.description.present? %>
  <div class="description-box">
    <p><%= @product.description %></p>
  </div>
<% end %>
```

### Actualizar los Estilos

Agrega al final de `app/assets/stylesheets/application.css`:

```css
/* Descripción */
.product-card .description {
  color: #4a5568;
  margin: 0.75rem 0;
  line-height: 1.5;
  font-size: 0.9rem;
}

.description-box {
  background: #f7fafc;
  padding: 1.5rem;
  border-radius: 10px;
  margin: 1.5rem 0;
  line-height: 1.8;
  color: #4a5568;
}
```

Agregando Búsqueda de Productos (30 minutos)
---------------------------------------------

### Actualizar el Controlador

En `app/controllers/products_controller.rb`, modifica el método `index`:

```ruby
def index
  @products = Product.all.order(created_at: :desc)

  if params[:search].present?
    @products = @products.where("name LIKE ? OR description LIKE ?",
                                "%#{params[:search]}%",
                                "%#{params[:search]}%")
  end
end
```

### Actualizar la Vista Index

En `app/views/products/index.html.erb`, agrega después del header:

```erb
<div class="search-box">
  <%= form_with url: products_path, method: :get, class: "search-form" do %>
    <%= text_field_tag :search, params[:search],
        placeholder: "🔍 Buscar productos...",
        class: "search-input" %>
    <%= submit_tag "Buscar", class: "btn-search" %>
    <% if params[:search].present? %>
      <%= link_to "Limpiar", products_path, class: "btn-clear" %>
    <% end %>
  <% end %>
</div>
```

### Agregar Estilos para Búsqueda

```css
/* Búsqueda */
.search-box {
  background: white;
  padding: 1rem;
  border-radius: 15px;
  box-shadow: 0 5px 20px rgba(0, 0, 0, 0.1);
  margin-bottom: 2rem;
}

.search-form {
  display: flex;
  gap: 0.5rem;
  align-items: center;
}

.search-input {
  flex: 1;
  padding: 0.75rem 1rem;
  border: 2px solid #e2e8f0;
  border-radius: 8px;
  font-size: 1rem;
}

.search-input:focus {
  outline: none;
  border-color: #667eea;
}

.btn-search {
  background: #667eea;
  color: white;
  padding: 0.75rem 1.5rem;
  border: none;
  border-radius: 8px;
  font-weight: 600;
  cursor: pointer;
}

.btn-clear {
  background: #e2e8f0;
  color: #4a5568;
  padding: 0.75rem 1rem;
  border-radius: 8px;
  text-decoration: none;
  font-weight: 500;
}
```

Agregando Categorías (50 minutos)
----------------------------------

### Crear Migración

```bash
$ bin/rails generate migration AddCategoryToProducts category:string
```

Ejecuta la migración:

```bash
$ bin/rails db:migrate
```

### Actualizar el Modelo

En `app/models/product.rb`:

```ruby
class Product < ApplicationRecord
  CATEGORIES = ["Ropa", "Electrónica", "Hogar", "Deportes", "Otros"]

  validates :name, presence: { message: "no puede estar en blanco" }
  validates :price, presence: { message: "no puede estar en blanco" },
                    numericality: { greater_than_or_equal_to: 0,
                                    message: "debe ser mayor o igual a 0" }
  validates :description, length: { maximum: 500 }
  validates :category, inclusion: { in: CATEGORIES }, allow_blank: true
end
```

### Actualizar el Controlador

```ruby
def product_params
  params.require(:product).permit(:name, :price, :description, :category)
end
```

### Actualizar el Formulario

En `app/views/products/_form.html.erb`:

```erb
<div class="form-group">
  <%= form.label :category, "Categoría" %>
  <%= form.select :category, Product::CATEGORIES,
      { include_blank: "Selecciona una categoría" },
      { class: "form-input" } %>
</div>
```

### Actualizar las Vistas

En `app/views/products/index.html.erb`, actualiza la tarjeta:

```erb
<div class="product-card">
  <% if product.category.present? %>
    <span class="category-badge"><%= product.category %></span>
  <% end %>
  <h3><%= product.name %></h3>
  <!-- resto del contenido -->
</div>
```

En `app/views/products/show.html.erb`:

```erb
<% if @product.category.present? %>
  <span class="category-badge-large"><%= @product.category %></span>
<% end %>
```

### Estilos para Categorías

```css
/* Categorías */
.category-badge {
  display: inline-block;
  background: #edf2f7;
  color: #4a5568;
  padding: 0.25rem 0.75rem;
  border-radius: 20px;
  font-size: 0.75rem;
  font-weight: 600;
  margin-bottom: 0.5rem;
}

.category-badge-large {
  display: inline-block;
  background: #edf2f7;
  color: #4a5568;
  padding: 0.5rem 1.5rem;
  border-radius: 25px;
  font-size: 0.9rem;
  font-weight: 600;
  margin-bottom: 1rem;
}
```

Agregando Filtros por Categoría (30 minutos)
---------------------------------------------

### Actualizar el Controlador

```ruby
def index
  @products = Product.all.order(created_at: :desc)

  if params[:search].present?
    @products = @products.where("name LIKE ? OR description LIKE ?",
                                "%#{params[:search]}%",
                                "%#{params[:search]}%")
  end

  if params[:category].present?
    @products = @products.where(category: params[:category])
  end
end
```

### Actualizar la Vista

En `app/views/products/index.html.erb`, después de la búsqueda:

```erb
<div class="filters">
  <%= link_to "Todas", products_path,
      class: "filter-btn #{params[:category].nil? ? 'active' : ''}" %>
  <% Product::CATEGORIES.each do |cat| %>
    <%= link_to cat, products_path(category: cat),
        class: "filter-btn #{params[:category] == cat ? 'active' : ''}" %>
  <% end %>
</div>
```

### Estilos para Filtros

```css
/* Filtros */
.filters {
  display: flex;
  gap: 0.75rem;
  margin-bottom: 2rem;
  flex-wrap: wrap;
}

.filter-btn {
  background: white;
  color: #4a5568;
  padding: 0.5rem 1.25rem;
  border-radius: 20px;
  text-decoration: none;
  font-weight: 500;
  font-size: 0.9rem;
  transition: all 0.2s;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.05);
}

.filter-btn:hover {
  transform: translateY(-2px);
}

.filter-btn.active {
  background: #667eea;
  color: white;
}
```

**PAUSA - Fin de Sesión Mañana Día 2**

--------------------------------------------------------------------------------

DÍA 2 - SESIÓN TARDE (3 horas): Toques Finales
===============================================

Agregando Contador de Productos (20 minutos)
---------------------------------------------

### Actualizar el Controlador

```ruby
def index
  all_products = Product.all
  @total_count = all_products.count
  @total_value = all_products.sum(:price)

  @products = all_products.order(created_at: :desc)

  if params[:search].present?
    @products = @products.where("name LIKE ? OR description LIKE ?",
                                "%#{params[:search]}%",
                                "%#{params[:search]}%")
  end

  if params[:category].present?
    @products = @products.where(category: params[:category])
  end
end
```

### Actualizar la Vista

En `app/views/products/index.html.erb`, después de los filtros:

```erb
<div class="stats">
  <div class="stat-card">
    <div class="stat-number"><%= @total_count %></div>
    <div class="stat-label">Productos</div>
  </div>
  <div class="stat-card">
    <div class="stat-number">$<%= number_with_precision(@total_value, precision: 2) %></div>
    <div class="stat-label">Valor Total</div>
  </div>
  <div class="stat-card">
    <div class="stat-number"><%= @products.count %></div>
    <div class="stat-label">Mostrando</div>
  </div>
</div>
```

### Estilos para Estadísticas

```css
/* Estadísticas */
.stats {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
  gap: 1rem;
  margin-bottom: 2rem;
}

.stat-card {
  background: white;
  padding: 1.5rem;
  border-radius: 15px;
  text-align: center;
  box-shadow: 0 5px 20px rgba(0, 0, 0, 0.08);
}

.stat-number {
  font-size: 2rem;
  font-weight: 700;
  color: #667eea;
  margin-bottom: 0.5rem;
}

.stat-label {
  color: #718096;
  font-size: 0.875rem;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.05em;
}
```

Mejorando el Layout General (40 minutos)
-----------------------------------------

### Crear un Layout Personalizado

En `app/views/layouts/application.html.erb`, envuelve el yield con navegación:

```erb
<!DOCTYPE html>
<html>
  <head>
    <title>Mi Tienda</title>
    <meta name="viewport" content="width=device-width,initial-scale=1">
    <%= csrf_meta_tags %>
    <%= csp_meta_tag %>

    <%= stylesheet_link_tag "application", "data-turbo-track": "reload" %>
  </head>

  <body>
    <nav class="navbar">
      <div class="nav-container">
        <%= link_to "🛍️ Mi Tienda", root_path, class: "nav-brand" %>
        <div class="nav-links">
          <%= link_to "Productos", products_path, class: "nav-link" %>
          <%= link_to "Nuevo Producto", new_product_path, class: "nav-link" %>
        </div>
      </div>
    </nav>

    <main>
      <%= yield %>
    </main>

    <footer class="footer">
      <p>Mi Tienda © <%= Date.today.year %> - Hecho con Rails</p>
    </footer>
  </body>
</html>
```

### Estilos para Navegación y Footer

```css
/* Navegación */
.navbar {
  background: white;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
  margin-bottom: 2rem;
  position: sticky;
  top: 0;
  z-index: 100;
}

.nav-container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 1rem 2rem;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.nav-brand {
  font-size: 1.5rem;
  font-weight: 700;
  color: #667eea;
  text-decoration: none;
}

.nav-links {
  display: flex;
  gap: 1.5rem;
}

.nav-link {
  color: #4a5568;
  text-decoration: none;
  font-weight: 500;
  transition: color 0.2s;
}

.nav-link:hover {
  color: #667eea;
}

/* Footer */
.footer {
  text-align: center;
  padding: 2rem;
  color: white;
  margin-top: 3rem;
}

.footer p {
  opacity: 0.9;
}
```

Agregando Animaciones (30 minutos)
-----------------------------------

Actualiza los estilos para agregar animaciones:

```css
/* Animaciones */
.product-card {
  animation: fadeInUp 0.3s ease-out;
}

@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.product-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 15px 40px rgba(0, 0, 0, 0.15);
}

.btn-primary:hover,
.btn-submit:hover,
.btn-view:hover,
.btn-edit:hover {
  transform: scale(1.05);
}

.btn-delete:hover {
  transform: scale(1.05);
  background: #e53e3e;
}
```

Mejorando Mensajes de Confirmación (20 minutos)
------------------------------------------------

Actualiza los botones de eliminar para tener mejores confirmaciones:

En `app/views/products/index.html.erb`:

```erb
<%= button_to "Eliminar", product_path(product), method: :delete,
    data: { turbo_confirm: "¿Estás seguro de eliminar '#{product.name}'?" },
    class: "btn-delete" %>
```

En `app/views/products/show.html.erb`:

```erb
<%= button_to "Eliminar", product_path(@product), method: :delete,
    data: { turbo_confirm: "¿Estás seguro de eliminar este producto? Esta acción no se puede deshacer." },
    class: "btn-delete" %>
```

Agregando Página de Inicio Atractiva (30 minutos)
--------------------------------------------------

### Crear Controlador Pages

```bash
$ bin/rails generate controller Pages home --skip-routes
```

### Actualizar Rutas

En `config/routes.rb`:

```ruby
Rails.application.routes.draw do
  root "pages#home"
  resources :products
end
```

### Crear Vista Home

En `app/views/pages/home.html.erb`:

```erb
<div class="hero">
  <div class="hero-content">
    <h1>🛍️ Bienvenido a Mi Tienda</h1>
    <p class="hero-subtitle">Gestiona tu catálogo de productos de forma simple y elegante</p>
    <div class="hero-actions">
      <%= link_to "Ver Productos", products_path, class: "btn-hero-primary" %>
      <%= link_to "Agregar Producto", new_product_path, class: "btn-hero-secondary" %>
    </div>
  </div>

  <div class="features">
    <div class="feature-card">
      <div class="feature-icon">📦</div>
      <h3>Gestión Completa</h3>
      <p>Crea, edita y elimina productos fácilmente</p>
    </div>
    <div class="feature-card">
      <div class="feature-icon">🔍</div>
      <h3>Búsqueda Rápida</h3>
      <p>Encuentra productos al instante</p>
    </div>
    <div class="feature-card">
      <div class="feature-icon">🏷️</div>
      <h3>Categorías</h3>
      <p>Organiza por categorías</p>
    </div>
  </div>
</div>
```

### Estilos para la Página de Inicio

```css
/* Hero Section */
.hero {
  text-align: center;
  padding: 3rem 1rem;
}

.hero-content {
  background: white;
  padding: 3rem 2rem;
  border-radius: 20px;
  box-shadow: 0 20px 60px rgba(0, 0, 0, 0.2);
  margin-bottom: 3rem;
}

.hero-content h1 {
  font-size: 3rem;
  color: #667eea;
  margin-bottom: 1rem;
}

.hero-subtitle {
  font-size: 1.25rem;
  color: #4a5568;
  margin-bottom: 2rem;
}

.hero-actions {
  display: flex;
  gap: 1rem;
  justify-content: center;
  flex-wrap: wrap;
}

.btn-hero-primary,
.btn-hero-secondary {
  padding: 1rem 2rem;
  border-radius: 30px;
  text-decoration: none;
  font-weight: 600;
  font-size: 1.1rem;
  transition: all 0.3s;
}

.btn-hero-primary {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
}

.btn-hero-secondary {
  background: white;
  color: #667eea;
  border: 2px solid #667eea;
}

.btn-hero-primary:hover {
  transform: scale(1.05);
  box-shadow: 0 10px 30px rgba(102, 126, 234, 0.4);
}

.btn-hero-secondary:hover {
  background: #667eea;
  color: white;
  transform: scale(1.05);
}

/* Features */
.features {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 2rem;
  max-width: 900px;
  margin: 0 auto;
}

.feature-card {
  background: white;
  padding: 2rem;
  border-radius: 15px;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
  transition: transform 0.3s;
}

.feature-card:hover {
  transform: translateY(-10px);
}

.feature-icon {
  font-size: 3rem;
  margin-bottom: 1rem;
}

.feature-card h3 {
  color: #2d3748;
  margin-bottom: 0.5rem;
}

.feature-card p {
  color: #718096;
}

/* Responsive Hero */
@media (max-width: 768px) {
  .hero-content h1 {
    font-size: 2rem;
  }

  .hero-subtitle {
    font-size: 1rem;
  }

  .features {
    grid-template-columns: 1fr;
  }
}
```

Prueba Final y Revisión (30 minutos)
-------------------------------------

### Checklist de Funcionalidades

Abre tu aplicación y verifica que todo funcione:

- [ ] Página de inicio atractiva
- [ ] Navegación funcional
- [ ] Ver lista de productos
- [ ] Crear nuevo producto con todos los campos
- [ ] Ver detalle de producto individual
- [ ] Editar producto existente
- [ ] Eliminar producto con confirmación
- [ ] Búsqueda de productos funcional
- [ ] Filtros por categoría
- [ ] Estadísticas de productos
- [ ] Validaciones funcionando
- [ ] Mensajes de error claros
- [ ] Diseño responsive (probar en móvil)
- [ ] Animaciones suaves

### Crear Datos de Prueba

Abre la consola de Rails y crea productos de ejemplo:

```bash
$ bin/rails console
```

```ruby
Product.create([
  { name: "Camiseta Básica", price: 19.99, description: "Camiseta de algodón 100%", category: "Ropa" },
  { name: "Laptop HP", price: 899.99, description: "Laptop para trabajo y estudio", category: "Electrónica" },
  { name: "Balón de Fútbol", price: 29.99, description: "Balón profesional", category: "Deportes" },
  { name: "Lámpara LED", price: 45.50, description: "Iluminación moderna", category: "Hogar" },
  { name: "Audífonos Bluetooth", price: 79.99, description: "Audio de alta calidad", category: "Electrónica" }
])
```

Optimizaciones Finales (20 minutos)
------------------------------------

### Mejorar los Mensajes Flash

Actualiza `app/views/layouts/application.html.erb`:

```erb
<% if notice %>
  <div class="flash-notice"><%= notice %></div>
<% end %>
<% if alert %>
  <div class="flash-alert"><%= alert %></div>
<% end %>
```

### Estilos para Flash Messages

```css
/* Flash Messages */
.flash-notice,
.flash-alert {
  position: fixed;
  top: 20px;
  right: 20px;
  padding: 1rem 1.5rem;
  border-radius: 10px;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
  z-index: 1000;
  animation: slideInRight 0.3s;
}

.flash-notice {
  background: #48bb78;
  color: white;
}

.flash-alert {
  background: #f56565;
  color: white;
}

@keyframes slideInRight {
  from {
    opacity: 0;
    transform: translateX(100px);
  }
  to {
    opacity: 1;
    transform: translateX(0);
  }
}
```

--------------------------------------------------------------------------------

¡FELICITACIONES! 🎉
====================

Has completado tu primera aplicación Rails en 2 días. Ahora tienes:

✅ Una aplicación completamente funcional
✅ Operaciones CRUD completas
✅ Interfaz hermosa y profesional
✅ Búsqueda y filtros
✅ Validaciones y mensajes de error
✅ Diseño responsive
✅ Animaciones suaves

¿Qué Aprendiste?
----------------

1. **Estructura MVC**: Cómo Rails organiza el código en Modelos, Vistas y Controladores
2. **Active Record**: Trabajar con bases de datos de forma intuitiva
3. **Rutas RESTful**: Cómo Rails maneja las URLs
4. **Vistas con ERB**: Crear interfaces dinámicas mezclando HTML y Ruby
5. **Validaciones**: Asegurar la integridad de los datos
6. **CSS**: Diseñar interfaces atractivas
7. **Helpers de Rails**: Usar `link_to`, `form_with`, y otros helpers

Próximos Pasos Recomendados
----------------------------

Ahora que dominas los fundamentos, puedes:

### 1. Agregar Más Funcionalidades

- **Imágenes de Productos**: Usar Active Storage para subir fotos
- **Usuarios y Autenticación**: Solo usuarios registrados pueden crear/editar
- **Comentarios o Reseñas**: Permitir calificaciones de productos
- **Carrito de Compras**: Agregar funcionalidad de e-commerce
- **Stock/Inventario**: Controlar la cantidad disponible

### 2. Mejorar la Aplicación Existente

- **Paginación**: Mostrar 10 productos por página
- **Ordenamiento**: Ordenar por precio, nombre, fecha
- **Tags/Etiquetas**: Sistema de etiquetas para productos
- **Exportar a CSV**: Descargar catálogo completo
- **Dashboard**: Página con estadísticas y gráficos

### 3. Aprender Más sobre Rails

- **Guía Oficial**: Revisa https://guides.rubyonrails.org/es/ para profundizar
- **Action Text**: Agregar editor de texto enriquecido
- **Action Mailer**: Enviar correos electrónicos
- **Active Job**: Tareas en segundo plano
- **Tests**: Escribir pruebas para tu código

### 4. Desplegar tu Aplicación

Comparte tu aplicación con el mundo:

- **Heroku**: Hosting gratuito para comenzar
- **Render**: Alternativa moderna y gratuita
- **Fly.io**: Despliegue global rápido

Recursos Adicionales
---------------------

### Documentación Oficial
- **Rails Guides**: https://guides.rubyonrails.org/es/
- **Ruby Docs**: https://ruby-doc.org/
- **API Reference**: https://api.rubyonrails.org/

### Comunidad
- **Stack Overflow**: Para preguntas específicas
- **Reddit r/rails**: Comunidad activa de Rails
- **Discord Rails**: Chats en tiempo real

### Tutoriales
- **Rails Tutorial de Michael Hartl**: Tutorial completo gratuito
- **GoRails**: Videos tutoriales (algunos gratuitos)
- **Railscasts**: Screencasts clásicos

Ejercicios de Práctica
-----------------------

Si quieres seguir practicando antes de continuar:

1. **Duplica la Aplicación**: Crea una tienda de libros con título, autor, y año
2. **Cambia los Colores**: Personaliza el esquema de colores
3. **Agrega Validaciones**: Precio mínimo, nombre único
4. **Crea Más Categorías**: Agrega subcategorías
5. **Mejora la Búsqueda**: Búsqueda por rango de precio

Mensaje Final
-------------

¡Felicitaciones por completar este taller intensivo! Lo que has logrado en 2 días es impresionante:

- Has creado una aplicación web real y funcional
- Comprendes los fundamentos de Rails y MVC
- Puedes crear, leer, actualizar y eliminar datos
- Has construido una interfaz atractiva
- Sabes cómo buscar y filtrar información

**Lo más importante**: Has experimentado la productividad y el placer de desarrollar con Rails. Esta es solo la punta del iceberg. Rails tiene muchísimo más que ofrecer, y ahora tienes las bases para seguir aprendiendo.

Recuerda: **todos los grandes desarrolladores comenzaron exactamente donde estás tú ahora**. Sigue practicando, sigue construyendo, y sigue aprendiendo.

### ¿Qué Sigue?

No dejes que termine aquí. Tu próximo paso debería ser:

1. **Terminar de leer** - La guía completa original
2. **Construir algo propio** - Una idea que te apasione
3. **Unirte a la comunidad** - Comparte tu progreso, haz preguntas
4. **Seguir aprendiendo** - Cada día un poco más

**¡El viaje apenas comienza! 🚀**

---

*Este taller fue diseñado con ❤️ para personas que quieren descubrir la magia de Rails.*

*Basado en la guía oficial de Rails*
