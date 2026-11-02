# Actividad 10. Escritorio remoto en Servidor Windows #

Vamos a configurar y utilizar el servicio de conexión por Escritorio Remoto a un servidor Windows. La conexión la realizaremos desde los **clientes Windows y Ubuntu**. 

!!! warning "Servicio DNS activo"
    Para poder completar la actividad actual exitosamente deberás tener el servicio DNS del servidor Ubuntu operando adecuadamente


## <div style="background-color: #f5dcd6; color: black; width: 100%; padding: 0px 5px; margin: 0; box-sizing: border-box;">1. Configuración previa de los equipos</div> ##

Para poder realizar la actividad adecuadamente debemos configurar las máquinas virtuales para que tengan la información correspondientes:

- Configurar la red NAT como `192.168.10.0/24` y llamarla `RedNatServicios`
- Asignar a las máquinas virtuales la red Nat anterior.
- Asignar las siguientes configuraciones:

| Configuración     | Servidor Windows   | Cliente Ubuntu | Cliente Windows |
| ------------------|-------------------|----------------|-----------------|
| IP                | 192.168.10.6      | 192.168.10.140 | 192.168.10.141  |
| IP servidor DNS   | 192.168.10.6      | 192.168.10.6   | 192.168.10.6    |


## <div style="background-color: #f5dcd6; color: black; width: 100%; padding: 0px 5px; margin: 0; box-sizing: border-box;">2. Activar el escritorio remoto en el servidor Windows</div> ##

1.- En el servidor Windows, en `administrador del servidor → servidor local`, habilitar el escritorio remoto.


!!! warning "Acceso remoto activado"
    - Por defecto la administración remota está habilitada. Comprobar que sea así.
    - Habilitar también la opción: `Escritorio remoto`

<img src="../images/ud04/actividad10/act10_04.png" width="100%">

## <div style="background-color: #f5dcd6; color: black; width: 100%; padding: 0px 5px; margin: 0; box-sizing: border-box;">3. Acceder al servidor Windows desde el cliente Windows con la IP</div> ##

1.- En el cliente Windows, abrir la aplicación de escritorio remoto.

2.- Introducir la IP del servidor al que queremos acceder y, a continuación, el usuario y contraseña del servidor.

3.- Si es la primera conexión nos aparece una pestaña de este tipo. Aceptamos el certificado del servidor. Nos tiene que aparecer el escritorio del servidor.

<img src="../images/ud04/actividad10/act10_01.png" width="40%">

!!! success "Capturas de pantalla"
    Entrega una captura de pantalla de la conexión al servidor desde el cliente (administrador del servidor visible)

4.- Desde el cliente Windows, realiza una tarea de administración del servidor : cambia su servidor DNS secundario al `1.1.1.1`. 

!!! success "Capturas de pantalla"
    Entrega una captura de pantalla con los cambios de DNS de servidor.


## <div style="background-color: #f5dcd6; color: black; width: 100%; padding: 0px 5px; margin: 0; box-sizing: border-box;">4. Acceder al servidor Windows desde el cliente Windows con el nombre de dominio</div> ##

!!! warning "¿Tienes activado el servicio DNS?"
    Recuerda que solo te funcionará si tienes el DNS bien configurado en tu servidor Windows. Compruébalo haciendo, desde el cliente, una consulta nslookup tipo A al nombre de tu servidor.

1.- La conexión deberás hacerla indicando: `Nombre del servidor + tu zona DNS`

<img src="../images/ud04/actividad10/act10_06.png" width="100%">    

!!! success "Capturas de pantalla"
    Entrega una captura de pantalla con la consulta nslookup

1.- En el cliente Windows, abrir la aplicación de escritorio remoto. En lugar de la IP introducir el nombre de dominio FQDN del servidor.

!!! success "Capturas de pantalla"
    Entrega una captura de pantalla de la conexión al servidor desde el cliente mostrando el servidor.
    
2.- Apaga el cliente Windows.


## <div style="background-color: #f5dcd6; color: black; width: 100%; padding: 0px 5px; margin: 0; box-sizing: border-box;">5. Acceder al servidor Windows desde el cliente Ubuntu</div> ##

1.- En el cliente Ubuntu, abrir el programa **Remmina** e introducir la IP del servidor Windows. Te pedirá confirmar que te fías del certificado del servidor. 

!!! note "Remmina"
    Remmina es un cliente de acceso remoto **RDP** que viene instalado por defecto en Ubuntu

<img src="../images/ud04/actividad10/act10_07.png" width="15%" style="border: 5px solid #3498db; border-radius: 8px">

2.- A continuación poner el usuario y contraseña del servidor Windows.

!!! success "Capturas de pantalla"
    Entrega una captura de pantalla de la conexión al servidor desde el cliente (administrador del servidor visible)

<img src="../images/ud04/actividad10/act10_08.png" width="100%" style="border: 5px solid #3498db; border-radius: 8px">




