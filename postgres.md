#PostgreSQL

##Crear usuario de PostgreSQL 
Es recomendable crear un usuario para la base de datos, que utilizará la aplicación de Ruby on Rails.

<code>
sudo -u postgres createuser -s [username]
</code>

Por ejemplo para crear el usuario <code>userx</code> el comando sería:

<code>sudo -u postgres createuser -s jdoe</code>

Para asignar una sontraseña a  este usuario, se debe acceder a la línea de comandos de PostgreSQL: 

<code>sudo -u postgres psql</code>

En la consola de PostgrSQL, se digita el siguiente comando para establecer una contraseña:

<code>\password [username]</code>

Para el caso del usuario creado es:

<code>\password userx</code>

A continuación se digita la nueva contraseña y se ingresa de nuevo la misma clave para confirmar, seguido a esto se da salida a la consola de PostgreSQL:

<code>\q</code>