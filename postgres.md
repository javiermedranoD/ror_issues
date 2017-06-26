# Usar PostgreSQL en Ruby on Rails

## Crear usuario de PostgreSQL
Es recomendable crear un usuario para la base de datos, que utilizará la aplicación de Ruby on Rails.

<code>
sudo -u postgres createuser -s [username]
</code>

Por ejemplo para crear el usuario <code>userx</code> el comando sería:

<code>sudo -u postgres createuser -s userx</code>

Para asignar una sontraseña a  este usuario, se debe acceder a la línea de comandos de PostgreSQL:

<code>sudo -u postgres psql</code>

En la consola de PostgrSQL, se digita el siguiente comando para establecer una contraseña:

<code>\password [username]</code>

Para el caso del usuario creado es:

<code>\password userx</code>

A continuación se digita la nueva contraseña y se ingresa de nuevo la misma clave para confirmar, seguido a esto se da salida a la consola de PostgreSQL:

<code>\q</code>

## Configurar la aplicación
Luego de crear las credenciales necesarias para utilizar PostgreSQL, es necesario configurar la nueva aplicación, para esto de debe utilizar la opción `-d postgresql` en el generador de rails que se ejecuta en la terminal:

`rails new myapp -d postgresql`

Con esto se indica que la nueva aplicación hará uso de PostgreSQL, como motor de base de datos.

Ruby on Rails creará toda la estructura de carpetas y archivos necesarios para iniciar el desarrollo de la aplicación, terminado el proceso de procede a modificar la información de acceso a la base de datos desde la aplicación:

`cd myapp`

Editar el archivo `config/database.yml`

En este archivo se deben modificar las credenciales de acceso para una conexión exitosa.

Se debe borrar `#` de la linea `#username:` y luego de los dos punto escribir el usuario creado para postgres anteriormente.

`username: userx`

De igual forma se debe habilitar la línea de `#password:`  con el password elegido para el usuario creado

`password: new_pass00`

Guardar los cambios y salir.

En la terminal es necesario ejecutar `bundle install` con el fin de instalar tanto la gema de PostgreSQL como todos los demás componentes y gemas requeridas para la aplicación.

## Creación de la base de datos desde Rails
El paso a seguir es ejecutar `rails db:create` con el fin de crear la base de datos a ejecutar, la salida en la terminal luego de ejecutar este comando, deberìa verse así:

`Created database 'myapp_development` lo que confirma la correcta creación de la base de datos.

### Otras tareas que involucran la base de datos `rails db:*`
Rails provee herramientas que facilitan el trabajo con la base de datos, provistas dentro del comando `rails db:*`

+ `rails db:create` => Crea la base de datos para el actual ambiente de desarrollo, por defecto se crean para `development` y `test`
+ `rails db:create:all` => Crea las bases para **todos** los ambientes de desarrollo
+ `rails db:drop` => Elimina la base de datos para el actual ambiente de desarrollo, por defecto se aplican para `development` y `test`
+ `rails db:drop:all` => Elimina las bases para **todos** los ambientes de desarrollo
+ `rails db:migrate` => Ejecuta las migraciones que aún no han sido realizadas en el actual ambiente de desarrollo.
+ `rails db:migrate:rollback` => Deshace los cambios realizados en la última migración ejecutada.
+ `rails db:seed` => Ejecuta el archivo *db/seeds.rb*, lo que permite poblar la base de datos con datos incluídos previamente por el usuario, en el archivo **seeds.rb**.
+ `rails db:schema:load` =>  Carga el esquema de la base de datos sin necesidad de ejecutar todas las migraciones, **solo debería usarse para poner una aplicación en producción desde cero**
+ `rails db:setup` => Ejecuta **db:schema:load** y luego **db:seed**.
+ `rails db:reset` => Ejecuta **db:drop** y luego **db:setup**.
