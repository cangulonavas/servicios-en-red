# Actividad 12. Servidor Web básico en Ubuntu


## <div style="background-color: #f5dcd6; color: black; width: 100%; padding: 0px 5px; margin: 0; box-sizing: border-box;">Objetivo de la actividad</div> ##

Vamos a instalar un servidor web en nuestro servidor Ubuntu y levantaremos una página web de prueba.

!!! success "Requisitos"
    - Servidor Ubuntu → **Red NAT Servicios** con **IP manual** → `192.168.10.5`
    - Cliente Ubuntu → **Red NAT Servicios** con **IP manual** → `192.168.10.140`


## <div style="background-color: #f5dcd6; color: black; width: 100%; padding: 0px 5px; margin: 0; box-sizing: border-box;">1. Instalar Apache2 en tu servidor Linux</div> ##

1.- Instala el paquete del servidor Apache en Ubuntu con el siguiente comando:
```bash
sudo apt update
sudo apt install apache2
```

2.- Desde tu **cliente Ubuntu**, prueba acceder con el navegador a través de la URL:
```bash
http://192.168.10.5
```

!!! success "Página de presentación de Apache"
    Si todo funciona bien te aparecerá una página web de presentación de Apache. En este caso el servidor web funciona, solo queda configurar tu página web.


## <div style="background-color: #f5dcd6; color: black; width: 100%; padding: 0px 5px; margin: 0; box-sizing: border-box;">2. Personalizar tu página web</div> ##

La carpeta donde se guardan los archivos de tu página web es `/var/www/html`. 

1.- Accede a la carpeta anterior y comprueba que tienes un archivo dentro llamado `index.html`.

!!! warning "Archivo index.html"
    **Lee detenidamenete** el archivo `index.html`. Este es el primer archivo que se ejecuta cuando accedemos a una página web a través de un navegador. Contiene código en lenguaje HTML. 
    
2.- Ahora vamos a editar el archivo `index.html` para personalizar nuestra página web:
```bash
sudo joe index.html
```

3.- Realiza una copia del fichero `index.html` para evitar machacar su contenido.

4.- Sustituye el contenido del archivo por el siguiente código en HTML.
```
<html>
    <head>
        <meta charset="utf-8">
        <title>Página web de Servicios en Red</title>
    </head>
    <body>
        <h1>Bienvenido a la página web de Servicios en Red</h1>
        <h3>IES Camp de Morvedre</h3>
        <h4>Carlos Angulo</h4>
    </body>
</html>
```

!!! note "Tu página web"
    - Recuerda cambiar `Carlos Angulo` por tu nombre
    - También puedes crear tu propia página con IA. Solicita un diseño tuyo personal pero tu nombre debe aparecer.


5.- Desde el navegador del cliente, vuelve a acceder a tu página web y observa el resultado.

!!! success "Captura de pantalla"
    Realiza captura de pantalla de tu navegador web    

!!! Success "Contesta a las siguientes preguntas"
    1.- ¿Dónde aparece el texto que has puesto entre las marcas `<title>` y `</title>`?

    2.- ¿Dónde aparece el texto que has puesto entre las marcas `<h1>` y `</h1>`?


## <div style="background-color: #f5dcd6; color: black; width: 100%; padding: 0px 5px; margin: 0; box-sizing: border-box;">3. Archivo de configuración de Apache y arranque del servicio</div> ##

!!! note "Archivos de configuración de Apache"
    - Los archivos de configuración de apache2 se encuentran en la carpeta `/etc/apache2`
    - El archivo principal de configuración es `apache2.conf`


!!! note "Configuración básica"
    Los valores que hay por defecto funcionan bien en la mayoría de situaciones.

1.- Añade la siguiente linea a tu fichero index.html tras la línea ` <h3>IES Camp de Morvedre</h3>`
```
<h2>Sistemas Microinformáticos y Redes</h2>
```

2.- Reinicia el servidor web:
```bash
service apache2 restart
service apache2 status
```

!!! success "Conteta a las siguientes preguntas"
    3.- ¿Has tenido que reiniciar el servicio Apache para observar tu página web modificada?


3.2 Prueba la ejecución de esos comandos.

!!! success "Captura de pantalla"
    Realiza captura de pantalla del reinicio y estado de tu servidor Apache


## <div style="background-color: #f5dcd6; color: black; width: 100%; padding: 0px 5px; margin: 0; box-sizing: border-box;">4. Acceder a la página web por su URL</div> ##

Hasta ahora, para acceder al servidor web desde cualquier cliente de la intranet, has puesto la dirección IP del servidor. Sin embargo, sería deseable acceder a la página web por un nombre, por ejemplo `www.angulosmr.com`

Para ello necesitamos convertir el nombre de dominio en dirección IP, es decir tener el servicio DNS instalado en nuestro servidor y bien configurado.

!!! warning "Servidor DNS activado"
    - Si no tienes el DNS hecho en tu máquina, vuelve a hacerlo con la actividad correspondiente
    
1.- Si tienes el DNS funcionando en tu máquina solo tienes que editar el archivo de base de datos de la zona directa.
    
2.- Una vez hecho eso reinicia el servicio bind
```bash
service bind9 restart
service bind9 status
```

3.-Si todo está correcto pasa a comprobar el funcionamiento del DNS. Asegúrate que tu cliente tiene configurado el servidor `192.168.10.6` como DNS (en los parámetros de red).

4.- En el cliente, accede al archivo `/etc/resolv.conf` 

5.- Donde pone `nameserver 127.0.0.53` sustituye la IP del bucle local por la IP de tu servidor DNS `192.168.10.5` y guarda el archivo.

6.- Realiza una consulta **nslookup CNAME** a tu página web `www.angulosmr.local`

7.- Ahora ya puedes acceder a tu página web por su URL.

!!! note "Limpia la caché"
    Se recomienda limpiar la caché DNS local de tu cliente Ubuntu con la siguiente sentencia:
    ```bash
    sudo resolvectl flush-caches
    ```

!!! success "Captura de pantalla"
    Realiza captura de pantalla del navegador con el servidor web funcionando y conectando a través de tu URL `http://www.angulosmr.local`
