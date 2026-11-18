# Actividad 13. Servidor Web virtual en Ubuntu


## <div style="background-color: #f5dcd6; color: black; width: 100%; padding: 0px 5px; margin: 0; box-sizing: border-box;">Objetivo de la actividad</div> ##

El objetivo de esta actividad es el almacenamiento de dos páginas web utilizando el mismo servidor web.

1.- Cada página web tendrá un nombre de dominio propio: 

- Página web para clientes → `clientes.angulosmr.local`
- Página web para proveedores → `proveedores.angulosmr.local`

!!! note "Recuerda cambiar la zona DNS por la tuya"

2.Los páginas web compartirán la misma dirección IP y el mismo puerto (80) ya que solo tenemos un servidor web. Es lo que se conoce como configurar servidores virtuales o virtualhosts basados en nombres.

## <div style="background-color: #f5dcd6; color: black; width: 100%; padding: 0px 5px; margin: 0; box-sizing: border-box;">1. Configuración de las máquinas</div> ##

A continuación volvemos a indicar la configuración de las máquinas virtuales

!!! success "Servidor Ubuntu"
    - Debe estar incluida en la `Red Nat Servicios`
    - IP → `192.168.10.5`
    - DNS → `8.8.8.8`

!!! success "Cliente Ubuntu"
    - Debe estar incluida en la `Red Nat Servicios`
    - IP → `192.168.10.140`
    - DNS → `192.168.10.5`


## <div style="background-color: #f5dcd6; color: black; width: 100%; padding: 0px 5px; margin: 0; box-sizing: border-box;">2. Diferencia entre servidores disponibles y activados</div> ##

- **available** → servidores virtuales disponibles.

- **enable** → servidores virtuales activados.

1.- Entra al directorio `/etc/apache2` y lista el contenido. 

2.- Observarás distintos archivos y directorios, entre los cuales están: `sites-available` y `sites-enabled`.

!!! note "sites-available"
    En sites-available tenemos los servidores virtuales disponibles (no están listos para usar).

!!! note "sites-enabled"
    En sites-enabled tendremos los servidores virtuales activados (listos para usar).

La forma de trabajar consiste en crear los archivos de configuración de la página web en el directorio `sitres-available` y, luego, activarlos a través de un enlace simbólico tal y como veremos en el paso 3.

!!! success "Capturas de pantalla"
    Entrega una captura de pantalla del contenido del directorio `/etc/apache2` señalando los dos directorios mencionados en este paso


## <div style="background-color: #f5dcd6; color: black; width: 100%; padding: 0px 5px; margin: 0; box-sizing: border-box;">3. Crear los archivos de configuración de cada sitio web virtual</div> ##

1.- Accede al directorio `/etc/apache2/sites-available` y comprueba que, por defecto, hay dos ficheros.

!!! success "Contesta"
    ¿Cómo se llaman los 2 ficheros de ese directorio?

El fichero que nos interesa es `000-default.conf` que es donde se ubica la configuración del sitio web por defecto. Para crear 2 sitios virtuales necesitamos un archivo de configuración para cada sitio virtual:

1.- Crear una copia de `000-default.conf` y llámala `clientes.conf`.

2.- Crear una copia de `000-default.conf` y llámala `proveedores.conf`.

!!! note "Ficheros de configuración"
    - Los ficheros anteriores servirán para configurar las dos nuevas webs que vamos a crear:
    - Web clientes → `clientes.angulosmr.local`
    - Web proveedores → `proveedores.angulosmr.local`

3.- Comprueba la creación de tus archivos.

!!! success "Capturas de pantalla"
    Entrega una captura de las dos copias creadas


## <div style="background-color: #f5dcd6; color: black; width: 100%; padding: 0px 5px; margin: 0; box-sizing: border-box;">4. Editar los archivos de configuración</div> ##

1.- Editar el fichero `clientes.conf`

2.- Cambiar el nombre de servidor de la línea `ServerName` y modificarla así:
```bash
ServerName clientes.angulosmr.local
```

3.- Modificar la línea que hace referencia al directorio raíz de documentos de la página (es decir el directorio donde crearemos los archivos índex en el paso 4):
```bash
DocumentRoot /var/www/html/clientes/•
```

4.- Realiza cambios similares en el fichero `proveedores.conf`


## <div style="background-color: #f5dcd6; color: black; width: 100%; padding: 0px 5px; margin: 0; box-sizing: border-box;">5. Crear un enlace simbólico</div> ##

No es suficiente crear los ficheros de configuración de cada sitio web. Además hay que crear un enlace simbólico a estos ficheros dentro del directorio para activarlos. 

1.- Accede al siguiente directorio:
```bash
/etc/apache2/sites-enabled
```

2.- Crear de los enlace simbólico a los ficheros de configuración en `sites-enabled` con estos comandos:
```bash
sudo a2ensite clientes.conf
sudo a2ensite proveedores.conf
```

!!! succeso "Contesta las siguientes preguntas"
    - ¿Qué nos contesta la consola cuando ejecutamos los anteriores comandos?
    - ¿Qué ves después de haber creado los enlaces si ejecutas `ls`? 
    
!!! success "Captura de pantalla"
    Realuza una captura de lo mostrado anteriormente

3.- Ahora sólo tendremos que recargar la configuración para que Apache tome en cuenta los cambios.
```bash
$service apache2 reload
```

## <div style="background-color: #f5dcd6; color: black; width: 100%; padding: 0px 5px; margin: 0; box-sizing: border-box;">6. Crear un directorio y el archivo index.html para cada sitio web</div> ##

1.- Creamos un directorio para cada sitio web virtual en `/var/www/html`
    - crear un directorio clientes
    - crear un directorio proveedores

!!! note "¿Qué son estos directorios?"
    Son los directorios que hemos mencionado en el archivos de configuración. Por ejemplo, en `clientes.conf` hemos añadido la ruta `DocumentRoot /var/www/html/clientes/`

2.- Copiamos el fichero `/var/www/html/index.html` a los distintos directorios.

!!! note "La copia también se tiene que llamar index.html"

3.- Modificamos el fichero `index.html` para que dé un mensaje de bienvenida apropiado:
```bash
<html>
    <head>
        <meta charset=”utf-8”>
        <title>Web clientes</title>
    </head>
    <body>
        <h1> Bienvenidos a la web clientes de mi empresa</h1>
    </body>
</html>
```

4.- Repetimos la operación para proveedodres en el archivo `/var/www/html/proveedores/índex.html` 

5.- Modifica el archivo anterior para que dé un mensaje de bienvenida apropiado: 

`Bienvenidos a la web proveedores de miempresa`

6.- Reiniciamos el servicio apache:
```bash
service apache2 restart
service apache2 status
```

## <div style="background-color: #f5dcd6; color: black; width: 100%; padding: 0px 5px; margin: 0; box-sizing: border-box;">7. Configuraicón del DNS</div> ##

Ahora vamos a modificar los archivos de configuración del DNS:

!!! note "Indica tu zona"
    Recuerda que debes indicar tu zona DNS en lugar de `angulosmr.local`.

1.- Para que resuelva los nuevos nombres de host: `clientes.angulosmr.local` y `proveedores.angulosmr.local`, crearemos dos alias en el archivo de configuración que apunten a la IP de tu servidor.

2.- Recuerda indicar la IP de tu servidor en el archivo `/etc/resolv.conf` para que la resolución se haga con éxito.


!!! warning "prueba con nslookup"
    Antes que nada, prueba tu DNS con una consulta nslookup a `clientes.angulosmr.local` y `proveedores.angulosmr.local`

!!! success "Entregas"

    1.- Responde a todas las preguntas

    2.- Capturas de pantalla de los archivos de configuración del DNS bind9.

    3.- Captura de pantalla de las consultas nslookup a `clientes.angulosmr.local` y `proveedores.angulosmr.local`

    4.- Capturas de pantalla del contenido de los archivos de configuración 
    
    - Fichero de configuración de clientes → `/etc/apache2/sites-available/clientes.conf` 
    - Fichero de configuración de proveedores → `/etc/apache2/sites-available/proveedores.conf`

    5.- Captura de la creación de los enlaces simbólicos.

    6.- Dos capturas de pantalla del cliente accediendo a cada una de las páginas web.



