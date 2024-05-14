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
