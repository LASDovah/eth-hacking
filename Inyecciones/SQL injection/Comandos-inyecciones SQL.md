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
CREATE TABLE users(id NOT NULL AUTO_INCREMENT PRIMARY KEY, username VARCHAR(32), password(32));
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
#Se colocar
```
**Eliminar Tabla**
```sql
UPDATE users SET username='admin_user' WHERE username = 'admin';
#Se colocar
```
---
