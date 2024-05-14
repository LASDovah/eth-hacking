![[What is a SQL injection.webp]]
### Introducción 
Las bases de datos en el back-end: Estas bases de datos se utilizan para:
+ Almacenar y recuperar datos relacionados con la aplicación web.
+ Desde >> Contenido web real hasta la información y el contenido del usuario.

La inyección SQL se refiere a ataques contra base de datos relacionales como MySQL 
(mientras que las inyecciones contra bases de datos no relacionales, como MongoDB, son la inyección NoSQL).
### Inyección SQL (SQLi)

Vulnerabilidades por inyección dentro de las aplicaciones web:
+ Inyección HTTP,
+ Inyección de código,
+ Inyección de comandos.
La inyección SQL es una vulnerabilidad de seguridad que ocurre cuando los datos ingresados por el usuario son maliciosamente manipulados para alterar el comportamiento de una consulta SQL enviada a la base de datos. Esto puede permitir a un atacante ejecutar comandos SQL no autorizados y potencialmente obtener acceso a datos sensibles o manipular la base de datos de manera no deseada.
###### Obtener una inyección SQL >
1. Inyectar código SQL
2. Subvertir la lógica de aplicación web cambiando la consulta original o ejecutando una completamente nueva.
Primero, el atacante debe inyectar código SQL fuera de los límites de entrada del usuario esperados, por lo que no se ejecuta como simple entrada de usuario. **En el caso más básico, esto se hace inyectando una sola cita( ') o una doble cotización ( ")** para escapar de los límites de la entrada del usuario e inyectar datos directamente en la consulta.
![[Pasted image 20240514115532.png]]

----
#### Consultas SQL 
Interacción con la base de datos, comandos:
+ SELECT > Se utiliza para recuperar datos de una o varias tablas. Permite especificar las columnas que se desean recuperar, así como también se pueden aplicar condiciones y ordenamientos.
+ INSERT > Se utiliza para agregar nuevos registros a una tabla.
+ UPDATE > Se utiliza para modificar los datos existentes de una tabla.
+ DELETE > Se utiliza para eliminar registros de una tabla.
+ CREATE > Se utiliza para crear nuevas tablas, índices o vistas de la base de datos.
+ DROP > Se utiliza para eliminar tablas, índices o vistas en la base de datos.
+ ALTER > Se utiliza para modificar la estructura de una tabla existente, como agregar o eliminar columnas.
+ TRUNCATE > Se utiliza para eliminar todos los registros de una tabla sin eliminar la estructura de la tabla misma.
+ GRANT > Se utiliza para otorgar privilegios a usuarios o roles sobre objetos de la base de datos.
+ REVOKE > Se utiliza para revocar privilegios otorgados previamente.
#### Interacción con la base de datos, consultas:
+ Consultas apiladas (Subqueries) > Las consultas apiladas, también conocidas como subconsultas o subqueries, son consultas SQL anidadas dentro de otras consultas. Estas subconsultas se ejecutan primero y luego el resultado se utiliza como parte de la consulta principal. Las subconsultas pueden aparecer en diferentes partes de una consulta SQL, como en la cláusula WHERE, FROM o SELECT.

+ Consultas de unión (UNION) > Las consultas de unión se utilizan para combinar los resultados de dos o más consultas en un solo conjunto de resultados. Las consultas de unión requieren que todas las consultas tengan la misma cantidad de columnas y tipos de datos. Los resultados de cada consulta se apilan uno encima del otro en el conjunto de resultados final.

+ Consultas basadas en tiempo (DATE/TIME) >
 **Funciones de fecha y hora**: SQL proporciona una variedad de funciones para trabajar con datos de fecha y hora, como `CURRENT_DATE`, `CURRENT_TIME`, `NOW()`, `DATE()`, `TIME()`, etc., que te permiten obtener la fecha y hora actuales, extraer partes específicas de una fecha o realizar cálculos con fechas.
	- **Filtrado por fecha**: Puedes usar cláusulas como `WHERE` para filtrar datos basados en fechas. Por ejemplo, puedes buscar registros que estén después o antes de una fecha específica, dentro de un rango de fechas o en un día de la semana determinado.

+ Consultas Booleanas >
	- **Filtrado condicional (CASE)**: La expresión `CASE` en SQL permite realizar operaciones condicionales, similar a las declaraciones `if-else` en otros lenguajes de programación. Puedes usar `CASE` para evaluar condiciones y devolver valores basados en esas condiciones.
	- **Operadores lógicos**: SQL utiliza operadores lógicos como `AND`, `OR` y `NOT` para combinar condiciones en las cláusulas `WHERE`. Estos operadores te permiten realizar consultas más complejas que involucran múltiples condiciones booleanas.
---
### Diferencia entre DB y DBMS.
//Base de datos (DB) y Sistema de Gestión de Base de Datos (DBMS).
1. Base de datos (DB):
+ Una base de datos es una colección organizada de datos que están estructurados y almacenados de manera que puedan ser fácilmente accedidos, gestionados y actualizados.
+ Puede ser simplemente un conjunto de archivos que contienen datos estructurados, organizados de acuerdo con un modelo de datos específico (modelo relacional).
+ Contenedor de datos organizado, no tiene la capacidad de gestionar, acceder y manipular datos que proporciona un DBMS.
2. Sistema de Gestión de Base de Datos (DBMS):
+ Es un software que proporciona una interfaz para definir, crear, manipular y consultar base de datos.
+ Es responsable de la administración y gestión de la base de datos, incluyendo aspectos como la seguridad, la integridad, la concurrencia y el rendimiento de la base de datos. 

En la similitud Tier 2 y el DBMS, hay una relación estrecha ya que la Tier 2 generalmente esta compuesta por el servidor de base de datos y su software, que es el DBMS. Es decir, la Tier 2 incluye el componente que gestiona y manipula los datos de la base de datos, que es proporcionado por el DBMS. Por lo tanto, en muchos casos, la Tier 2 y el DBMS se consideran como componentes interrelacionados en una arquitectura de sistema que utiliza bases de datos.

---
## Sistema de Gestión de Base de datos (DBMS)
+ Crear, definir, organizar y administrar base de datos.
+ Varios tipos de DBMS fueron diseñados con el tiempo, tales como tiendas de archivos, Relational DBMS (RDBMS), NoSQL, Graph y Key/Value.

##### Arquitectura DBMS
USER - TIER 1 - TIER 2 - DBMS - User/ DB-Administrador

User > Representa las personas o sistemas que interactúan directamente con la aplicación.
TIER 1 > Capa que actúa como frontend o la interfaz de usuario del sistema. 
+ Recibe las solicitudes de los usuarios, procesarlas y enviarlas al nivel de back-end (Tier 2) para su procesamiento.
+ Puede incluir servicios como autenticación de usuarios , enrutamiento de solicitudes, validación de datos, etc.
TIER 2 > Capa que actúa como back-end o la capa de datos del sistema.
+ Compuesta por el servidor de la base de datos y su software (DBMS).
+ Es responsable de almacenar y gestionar los datos de la base de datos, ejecutar consultas, realizar operaciones de lectura y escritura, gestionar transacciones, etc.
+ Puede incluir múltiples servidores de base de datos para distribuir la carga de trabajo y mejorar el rendimiento.
DBMS (Sistema de Gestión de Bases de Datos) > Software que administra y gestiona la DB.
+ Proporciona una interfaz para: Definir - Crear - Manipular y Consultar los datos en la DB.
+ Gestiona aspectos como la seguridad, la integridad, la concurrencia y el rendimiento de la base de datos.
+ Ejemplos populares de DBMS incluyen MySQL, PostgreSQL, Oracle Database, SQL Server, MongoDB, etc.
Administrador de la base de datos (Database Administrator) > Administra y mantiene la DB.
+ Su tarea puede incluir la instalación y configuración del DBMS, la optimización del rendimiento, la realización de copias de seguridad y recuperación, la gestión de usuarios y permisos, la monitorización del sistema, etc.

En otras palabras, en la arquitectura mencionada arriba, los usuarios interactúan con la aplicación a través de la capa de frontend (Tier 1), que luego envía solicitudes backend (Tier 2) para su procesamiento mediante el DBMS.
`nota: es posible alojar el servidor de la aplicación, así como el DBMS en el mismo host. Sin embargo, las bases de datos con grandes cantidades de datos que soportan a muchos usuarios suelen estar alojadas por separado para mejorar el rendimiento y la escalabilidad.`
