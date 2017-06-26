# Migraciones
Las migraciones permiten la modificación del esquema de la base de datos a través del tiempo, de una forma sencilla y segura. Cada nueva migración se puede considerar como una versión diferente de la base de datos.  

Un ejemplo de migración

````
class CreateProducts < ActiveRecord::Migration
  def change
    create_table :products do |t|
      t.string :name
      t.text :description
      t.timestamps null: false
    end
  end
end
````
Esta migración añade una tabla llamada **products** con una columna cadena de caractéres llamada *name* y una columna de texto llamada *description*. Una columna de clave primaria llamada *id* será también añadida implicitamente, como la clave primaria por defecto para todos los modelos Active Record. Los macro timestamps añaden dos columnas, *created_at* y *updated_at*. Estas columnas especiales son automaticamemente administradas por Active Record si existen.

## Crear una migración

Las migraciones pueden ser creadas de manera independiente por el usuario (por ejemplo cuando se debe modificar una tabla ya creada) ó de manera automática por Rails (Cuando se crean los modelos, rails automáticamente crea una migración).

### Un modelo y su migración
Al crear el siguiente modelo desde la línea de comandos

`rails g model Banco codigo:string nombre:string`

Ruby on Rails crea una migración que se encuentra en un archivo *20170626204240_create_bancos.rb*,
ubicado en la carpeta *db/migrate*, el contenido creado con la migración es el siguiente:
````
class CreateBancos < ActiveRecord::Migration[5.0]
  def change
    create_table :bancos do |t|
      t.string :codigo
      t.string :nombre

      t.timestamps
    end
  end
end
````
Para hacer efectiva esta migración en la base de datos, se debe ejecutar en la terminal `rails db:migrate`

### Crear migración independiente
Si se requiere modificar, eliminar o crear un elemento de las tablas o tablas como tal, se debe ejecutar una migración de acuerdo a las necesidades. Para este caso se agregará un campo *tipo* a la tabla "bancos", creada por el modelo *Banco* y su migración.

La convención en general para agregar nuevos campos a una tabla ya existente utilizando generadores es: `rails g migration AddNombredeMigrationToTabla campo1:tipo campo2:tipo`

`rails g migration AddCampoTipoToBancos tipo:string`

Tras ejecutar la migración en la terminal debe mostrar el resultado
~~~
rails db:migrate                                  
== 20170626211225 AddCampoTipoToBancos: migrating =============================
-- add_column(:bancos, :tipo, :string)
   -> 0.0011s
== 20170626211225 AddCampoTipoToBancos: migrated (0.0011s) ====================
~~~
