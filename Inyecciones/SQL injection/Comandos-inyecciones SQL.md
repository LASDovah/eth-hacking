**Crear Base de datos**
```sql
CREATE DATABASE youtube;
```
**Ver Base de datos creadas**
```sql
SHOW DATABASE ;
```
**Eliminar Base de datos**
```sql
DROP DATABASE youtube;
```
---
**Ingresar a la DB**
```sql
USE youtube;
```
**Crear tabla**
```sql
CREATE TABLE users(id NOT NULL AUTO_INCREMENT PRIMARY KEY, username VARCHAR(32), password VARCHAR(32));
```
**Ver los atributos de la tabla**
```sql
DESCRIBE users;
```
**Insertar un valor**
```sql
INSERT INTO users(username, password) values('admin','admin123');
```
![db basica](https://github.com/LASDovah/vulnerability-pentest/assets/163781606/8a15a33b-18c0-4d42-a3e5-ac55a66d7f73)

**Modificar un valor insertado**
```sql
UPDATE users SET username='admin_user' WHERE username = 'admin';
#Se coloca primero el usuario a modificar y a lo ultimo el nombre creado
```
**Ver * el contenido insertado dentro de la tabla**
```sql
SELECT * FROM users;
```
**Eliminar Tabla COMPLETA**
```sql
DROP TABLE usuarios;
```
**Eliminar FILA completa de una tabla**
```sql
DELETE FROM users WHERE id = 3;
//Esto elimina la fila con id igual a 3 de la tabla users
```
**Eliminar COLUMNA completa de una tabla**
```sql
ALTER TABLE users DROP COLUMN subscription;
//Elimina la columna completa de subscription
```