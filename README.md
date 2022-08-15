## DNS dinámico gratuito alojado en AWS
<p align="center">
  <img src="https://github.com/JuanRodenas/Duckdns/blob/main/files/duckdns_logo.png"
       width="700"/>
</p>

### Crear una cuenta en duckdns
[DuckDNS](https://www.duckdns.org)
- Copie el token de su dominio y el dominio creado.

![alt text](https://github.com/JuanRodenas/Duckdns/blob/main/files/token-duckdns.png)

![alt text](https://github.com/JuanRodenas/Duckdns/blob/main/files/Dominio-duckdns.png)


### Creamos los archivos 
Comencemos y hagamos un directorio para colocar sus archivos, muévase a él y haga nuestro script principal:
```
mkdir duckdns && cd duckdns  && vi duck.sh
```
Y pegamos la siguiente línea:
```
echo url="https://www.duckdns.org/update?domains=exampledomain&token=YOUR_TOKEN&ip=" | curl -k -o ~/duckdns/duck.log -K -
```
Pueden ver un ejemplo del archivo en el repositorio o descargarlo de ejemplo:
<a title="duck.sh" href="https://github.com/JuanRodenas/Duckdns/blob/main/duck.sh"><img src="https://github.com/JuanRodenas/Duckdns/blob/main/files/download.jpg" alt="duck.sh" width="120" /></a>


#### Editamos los parámetros de la línea con los datos creados anteriormente
```
- exampledomain=YOUR_DOMAIN.duckdns.org
- YOUR_TOKEN=token de la cuenta
```
- ahora guarde el archivo en `vi` (ESC y luego :wq! luego ENTER).
- Si usas `nano` guarde el archivo (CTRL+O luego CTRL+X).

### Damos permisos de ejecución al archivo y ejecutamos el script
#### 
```
chmod 700 duck.sh && chmod a+x duck.sh
```

#### Damos permisos de ejecución al archivo:
a continuación, usaremos el proceso con `cron` para hacer que el script se ejecute `cada 5 minutos`:
```
crontab-e
```
copia este texto y pégalo en la parte inferior del `crontab`:
```
*/5 * * * * ~/duckdns/duck.sh >/dev/null 2>&1
```
ahora guarde el archivo (CTRL+O luego CTRL+X) y vamos a probar el script:
```
./duck.sh
```
esto simplemente debería volver a un indicador con el porcentaje indicando si es correcto.
![alt text](https://github.com/JuanRodenas/Duckdns/blob/main/files/duckDNS_ejecuci%C3%B3n.jpg)


#### Podemos ver si el último intento fue exitoso indicará `OK` o por lo contrario indicará `KO`.
```
cat duck.log
```
si es `KO`, verifique que su Token y Dominio sean correctos en el `duck.sh` script

![alt text](https://github.com/JuanRodenas/Duckdns/blob/main/files/duckDNS_log.jpg)


### ¿ahora que?
Ahora debemos de configurar el reenvío de puertos en su enrutador para hacer uso de su nuevo nombre DDNS.

Recomendamos [portforward.com](https://portforward.com/) para aprender todo sobre esto.

## Ready!
