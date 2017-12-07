# Instalar Ubuntu Server 14.04 en VirtualBox

## Descargar imagen ISO

La imagen ISO de __Ubuntu Server 16.04 LTS__ puede descargarse de la siguiente URL:

[http://releases.ubuntu.com/16.04.3/ubuntu-16.04.3-server-amd64.iso](http://releases.ubuntu.com/16.04.3/ubuntu-16.04.3-server-amd64.iso)

## Crear la Máquina Virtual

En la ventana principal de VirtualBox, pulsamos en el botón _New_:

![img_01][img_01]

Configuramos el nombre y el tipo de la máquina virtual:

* __Name__: ub_server_16.04
* __Type__: Linux
* __Version__: Ubuntu (64-bit)

![img_02][img_02]

La versión de Ubuntu Server está pensada para ejecutar servicios y no trae ningún entorno gráfico instalado, con lo que la cantidad de _memoria RAM_ que le asignemos dependerá del servicio que vayamos a instalar (MySQL, Tomcat, Nginx, ...).

Le asignaremos un memoria de 512MB.

![img_03][img_03]

> __Nota__: Para ampliar/reducir la memoria RAM es necesario que la máquina virtual esté apagada.

Creamos un _disco duro virtual_ que simulará el disco duro de la Máquina Virtual:

![img_04][img_04]

Existen varios formatos para discos duros virtuales:

* __VDI__: es el formato nativo de VirtualBox y es el que se usa en la mayoría de los casos.
* __VMDK__: (_VMware disk format_) es un formato desarrollado por y para Vmware, pero VirtualBox también lo soporta. Este formato hace que exportar Máquinas Virtuales entre distintos entornos de virtualización como  _Vmware Workstation_ sea más fácil.
* __VHD__: es el formato nativo de Microsoft Virtual PC. Este formato es popular en Productos Microsoft.

En este caso usaremos _VDI_, que es la opción que viene configurada por defecto:

![img_05][img_05]

Ahora debemos elegir entre:

* __Asignación dinámica (dinamically allocated)__: el tamaño del fichero del disco duro aumenta a medida que se usa el disco hasta alcanzar el tamaño máximo especificado durante la creación del mismo.
* __Tamaño fijo (Fixed size)__: requiere espacio de almacenamiento físico equivalente al tamaño especificado para el disco duro en el momento de crearlo. El tamaño del fichero del disco duro será  del disco duro virtual y no se modificará.

> __Nota__: El formato _VMDK_ tiene la capacidad adicional de dividir el archivo de almacenamiento en archivos de menos de 2GB cada uno, lo cual resulta muy útil si nuestro sistema de archivos tiene algún límite en cuanto al tamaño de ficheros.

![img_06][img_06]

 Asignamos un tamaño de 16GB a nuestr disco duro y pulsamos en el botón _Create_:

![img_07][img_07]

Vemos cómo se ha creado correctamente la máquina virtual llamada _ub_server_16.04_.

![img_08][img_08]


## Configurar la Máquina Virtual

A continuación veremos cómo configurar distintos aspectos de la máquina virtual como el número de CPUs, el tipo de red, ...

Para acceder al panel de configuración, pulsar botón derecho sobre la máquina virtual y elegir la opción _Settings.._. del menú contextual:

![img_09][img_09]

En la pestaña _Motherboard_ del menú _System_ podemos ver la cantidad de memoria RAM que tiene asignada la máquina virtual:

![img_10][img_10]

> __Nota__: Sólo se puede ampliar/reducir la cantidad de memoria RAM con la máquina virtual apagada.

En la pestaña _Processor_ del menú _System_ podemos ver el número de CPUs que tiene asignada la máquina virtual:

![img_11][img_11]

> __Nota__: Sólo se puede ampliar/reducir el número de CPUs con la máquina virtual apagada.

Existen distintos tipos de configuración de las tarjetas de red:

* __NAT__: es la forma más sencilla que tiene una máquina virtual para acceder a una red externa. Por lo general, no se requiere ninguna configuración en la red, ni en el _equipo anfitrión_ (en inglés _Host_) ni en el _equipo invitado_ (en inglés _Guest_). Por este motivo, __es el modo de red por defecto que usa VirtualBox__.

> Nota: Entiéndase por _equipo anfitrión_ (en inglés _Host_) la máquina donde se encuentra instalado el VirtualBox y _equipo invitado_ (en inglés _Guest_) la máquina virtual.

El _modo NAT_ permite a la máquina virtual comunicarse con el exterior: navegar por internet, descargar ficheros, leer el correo electrónico, ...

En cambio, si desde el _equipo anfitrión_ quisiéramos comunicarnos con algún servicio del _equipo invitado_ (p. ej. SSH, MySQL, ...) necesitaríamos configurar el mapeo de puertos (esto lo veremos más adelante).

En el menú _Network_ podemos ver la configuración de la tarjeta de red:

![img_12][img_12]

En el menú _Storage_ vamos a montar la ISO descargada previamente en la unidad DVD-ROM virtual:

![img_13][img_13]

Seleccionamos la imagen desde el sistema de ficheros:

![img_14][img_14]

Comprobamos que la imagen de Ubuntu Server 16.04 está montada en la unidad DVD-ROM virtual y pulsamos _OK_:

![img_15][img_15]

VirtualBox guarda por defecto las máquinas virtuales creadas en una ubicación que cambia en función del sistema operativo utilizado:

* __Windows__: "C:\Users\<username)>\VirtualBox VMs"

En _Windows_, la máquina virtual creada se encontraría bajo la ruta "C:\Users\<username)>\VirtualBox VMs\ub_server_16.04" y contiene los siguientes ficheros:

![img_16][img_16]

A continuación se detallan los ficheros más importantes:

* __ub_server_16.04.vbox__: fichero de configuración de la máquina virtual.
* __ub_server_16.04.vdi__: fichero de disco duro de la máquina virtual. Vemos que el tamaño de este fichero es de aproximadamente un poco más de 2,5GB, a pesar de haberlo configurado el tamaño del disco a 16GB. Esto es porque lo hemos configurado en modo _asignación dinámica_, es decir, el tamaño del disco crecerá a medida que se vaya llenando (descarga de archivos, instalación de software) hasta un máximo de 16GB.


## Instalación de Ubuntu Server 16.04

Para arrancar la máquina virtual, pulsamos en el boton _Start_:

![img_17][img_17]

Seleccionamos el __idioma__ (nos movemos con los cursores), en este caso _español_ y pulsamos la tecla _Enter_ :

![img_18][img_18]

Seleccionamos _Instalar Ubuntu Server_, que es la opción que viene marcada por defecto, y pulsamos la tecla _Enter_:

![img_19][img_19]

Seleccionamos la __ubicación__, que servirá para fijar la zona horaria donde nos encontramos. En este caso, seleccionamos España, que es la opción que viene marcada por defecto y pulsamos la tecla _Enter_:

![img_20][img_20]

No hace falta realizar una detección de nuestro teclado, marcamos la opción _No_, que es la opción que viene marcada por defecto y pulsamos la tecla _Enter_:

![img_21][img_21]

Seleccionamos la __distribución de teclado__, en este caso _spanish_, que es la opción que viene marcada por defecto, y pulsamos la tecla _Enter_:

> __Nota__: Si la distribucion de teclado que viene marcada por defecto no es  _spanish_, es que __no__ hemos elegido el idioma _español_ en uno de los pasos anteriores. Por lo tanto, debemos movernos con el cursor hasta seleccionar como distribución de teclado  _spanish_. Si no lo hacemos, tendremos una distribución de teclado diferente a la disposición del teclado de nuestro ordenador: cuando pulsemos , por ejemplo, la tecla _ñ_, estaremos insertando en realidad un _;_.

![img_22][img_22]

![img_23][img_23]

Configuramos el __nombre del equipo__, en esta caso escribimos _ubuntu_, que es la opción que viene escrita por defecto, nos movemos con la tecla _Tab_ hasta situarnos en la opción _Continuar_ y pulsamos la tecla _Enter_:

![img_24][img_24]

Durante el proceso de instalación de Ubuntu debemos crear un usuario. Este usuario podrá realizar cualquier tarea que requiera privilegios de administrador a través del comando _sudo_.

Vamos a configurar un usuario con los siguientes datos:

* __Nombre real del usuario__: cfgs.
* __Nombre de usuario para la cuenta__: cfgs.​
* __Password del usuario__: cfgs.

Configuramos el __nombre real del usuario__. En este campo debemos poner el nombre completo del usuario, por ejemplo, Jhon Allen Smith. Es este caso vamos configurarlo a  _cfgs_, nos movemos con la tecla _tabulador_ hasta situarnos en la opción _Continuar_ y pulsamos la tecla _Enter_:

![img_25][img_25]

Configuramos el __nombre de usuario para la cuenta__. Es este caso vamos configurarlo a _cfgs_, nos movemos con la tecla _tabulador_ hasta situarnos en la opción _Continuar_ y pulsamos la tecla _Enter_:

![img_26][img_26]

Configuramos el __password del usuario__. Es este caso vamos configurar el password a _cfgs_, nos movemos con la tecla _tabulador_ hasta situarnos en la opción _Continuar_ y pulsamos la tecla _Enter_:

![img_27][img_27]

Repetimos la misma constraseña que introducimos en el apartado anterior, nos movemos con la tecla _tabulador_ hasta situarnos en la opción _Continuar_ y pulsamos la tecla _Enter_:

![img_28][img_28]

Nos sale un mensaje de aviso indicando que la constraseña elegida tiene menos de 8 caracteres y es considerada una contraseña débil. Nos movemos con la tecla _tabulador_ hasta situarnos en la opción _Sí_ y pulsamos la tecla _Enter_:

![img_29][img_29]

Configuramos la __zona horaria__, en este caso _Atlantic/Canary_. Nos pregunta si esta configuración es correcta. Nos movemos con la tecla _tabulador_ hasta situarnos en la opción _Sí_ y pulsamos la tecla _Enter_:

![img_30][img_30]

En este paso se configura el __particionado del disco__, marcamos la opción _Guiado - utilizar el disco completo y configurar LVM_, que es la opción que viene marcada por defecto y pulsamos la tecla _Enter_:

![img_31][img_31]

Elegimos qué discos queremos particionar. Como sólo configuramos un disco duro cuando creamos la máquina virtual, nos saldrá una opción, en este caso _SCSI3 (0,0,0) (sda) - 17.2 GB ATA VBOX HARDDISK_, que es la opción que viene marcada por defecto y pulsamos la tecla _Enter_:

![img_32][img_32]

Nos indica que debe guardar el esquema de particionado actual en el disco antes de poder configura el Gestor de volúmenes Lógicos. Nos movemos con la tecla _tabulador_ hasta situarnos en la opción _Sí_ y pulsamos la tecla _Enter_:

![img_33][img_33]

Nos indica si queremos utilizar todo el espacio del disco a la hora de particionarlo. Es este caso viene configurado a _16,7 GB_ por defecto, que es el tamaño máximo del disco. Lo dejamos como está. Nos movemos con la tecla _tabulador_ hasta situarnos en la opción _Continuar_ y pulsamos la tecla _Enter_:

![img_34][img_34]

Nos indica las particiones que va a crear en el disco duro y pregunta si queremos escribir los cambios. Nos movemos con la tecla _tabulador_ hasta situarnos en la opción _Sí_ y pulsamos la tecla _Enter_:

![img_35][img_35]

Si todo va bien deberíamos ver la siguiente pantalla __instalando el sistema__:

![img_36][img_36]

Esta pantalla nos permite configurar un proxy HTTP, como no es el caso, lo dejamos en blanco. Nos movemos con la tecla _tabulador_ hasta situarnos en la opción _Continuar_ y pulsamos la tecla _Enter_:

![img_37][img_37]

En esta pantalla nos indica si queremos aplicar actualizaciones frecuentemente. Le indicamos _Sin actualizaciones automáticas_, que es la opción que viene por defecto y pusamos la tecla _Enter_:

![img_38][img_38]

En esta pantalla indicamos los programas que queremos instalar. En principio viene marcada la opción _standard system utilities_, vamos a marcar, además _OpenSSH server_, la cual nos permitirá establecer una conexión remota a la máquina virtual. Para ello, nos movemos con el cursos hasta posicionarnos en la opción que queremos marcar y pulsamos la tecla _Barra espaciadora_ para que quede marcada. A continuación nos movemos con la tecla _tabulador_ hasta situarnos en la opción _Continuar_ y pulsamos la tecla _Enter_:

![img_39][img_39]

En esta pantalla configuramos el __cargador de arranque GRUB__, para ello nos movemos con la tecla _tabulador_ hasta situarnos en la opción _Sí_ y pulsamos la tecla _Enter_:

![img_40][img_40]

¡Listo! Ya hemos finalizado la instalación de Ubuntu Server 16.04 en nuestra máquina virtual. nos movemos con la tecla _tabulador_ hasta situarnos en la opción _Sí_ y pulsamos la tecla _Enter_:

![img_41][img_41]

A continuación se reniciará la máquina virtual. Una vez reiniciada, veremos la siguiente pantalla, solicitando un usuario para acceder a ella:

![img_42][img_42]

Introducimos el usuario y password que configuramos durante el proceso de instalación. En este caso:

* __usuario__: cfgs
* __password__: cfgs

Si todo va bien deberíamos acceder al sistema y ver la siguiente pantalla:

![img_43][img_43]

A continuación escribimos el comando _exit_ para salir del sistema:

```bash
cfgs@ubuntu:$ exit
```
![img_42][img_42]

## Acceso a través de SSH

__SSH__ o __Secure Shell__, es un protocolo de administración remota que permite a un usuario controlar una máquina sin estar físicamente delante de ella.

### Port Forwading

Abrimos la configuración de la VM y vamos al menú _Network-Advanded-Port Forwarding_:

![img_44][img_44]

Creamos una nueva regla que nos permita acceder por SSH a la VM desde nuestro equipo:

* __Name__: SSH
* __Protocol__: TCP
* __Host IP__: vacío
* __Host Port__: 2222
* __Guest IP__: vacío
* __Guest Port__: 22

Lo que estamos haciendo es configurar nuestro equipo para que, cada vez que intentemos conectarnos al puerto 2222, nos redirija el tráfico de red al puerto 22 de nuestra VM.

> __Nota__: Los campos _Host IP_ y _Guest IP_ se dejan vacíos ya que la tarjeta de red se ha configurado en modo _NAT_.

![img_45][img_45]

Descargamos algún cliente SSH para Windows como [PuTTY](http://www.putty.org/) o [MobaXterm](https://mobaxterm.mobatek.net/).

Si utilizamos el cliente _Putty_, para establecer una conexión SSH a la VM:

* __Host Name (or IP address)__: localhost
* __Port__: 2222

Luego pulsamos en el botón _Open_.

![img_46][img_46]

Si todo va bien se nos abrirá una pantalla donde se nos piden las credenciales de un usuario para poder acceder:

* __login as__: cfgs
* __cfgs@localhost's password__: cfgs

![img_47][img_47]

Con esto hemos configurado nuestra VM para poder acceder a través del protocolo SSH.

[img_01]: img/01_instalacion/01.png "Logo Title Text 2"
[img_02]: img/01_instalacion/02.png "Logo Title Text 2"
[img_03]: img/01_instalacion/03.png "Logo Title Text 2"
[img_04]: img/01_instalacion/04.png "Logo Title Text 2"
[img_05]: img/01_instalacion/05.png "Logo Title Text 2"
[img_06]: img/01_instalacion/06.png "Logo Title Text 2"
[img_07]: img/01_instalacion/07.png "Logo Title Text 2"
[img_08]: img/01_instalacion/08.png "Logo Title Text 2"
[img_09]: img/01_instalacion/09.png "Logo Title Text 2"
[img_10]: img/01_instalacion/10.png "Logo Title Text 2"
[img_11]: img/01_instalacion/11.png "Logo Title Text 2"
[img_12]: img/01_instalacion/12.png "Logo Title Text 2"
[img_13]: img/01_instalacion/13.png "Logo Title Text 2"
[img_14]: img/01_instalacion/14.png "Logo Title Text 2"
[img_15]: img/01_instalacion/15.png "Logo Title Text 2"
[img_16]: img/01_instalacion/16.png "Logo Title Text 2"
[img_17]: img/01_instalacion/17.png "Logo Title Text 2"
[img_18]: img/01_instalacion/18.png "Logo Title Text 2"
[img_19]: img/01_instalacion/19.png "Logo Title Text 2"
[img_20]: img/01_instalacion/20.png "Logo Title Text 2"
[img_21]: img/01_instalacion/21.png "Logo Title Text 2"
[img_22]: img/01_instalacion/22.png "Logo Title Text 2"
[img_23]: img/01_instalacion/23.png "Logo Title Text 2"
[img_24]: img/01_instalacion/24.png "Logo Title Text 2"
[img_25]: img/01_instalacion/25.png "Logo Title Text 2"
[img_26]: img/01_instalacion/26.png "Logo Title Text 2"
[img_27]: img/01_instalacion/27.png "Logo Title Text 2"
[img_28]: img/01_instalacion/28.png "Logo Title Text 2"
[img_29]: img/01_instalacion/29.png "Logo Title Text 2"
[img_30]: img/01_instalacion/30.png "Logo Title Text 2"
[img_31]: img/01_instalacion/31.png "Logo Title Text 2"
[img_32]: img/01_instalacion/32.png "Logo Title Text 2"
[img_33]: img/01_instalacion/33.png "Logo Title Text 2"
[img_34]: img/01_instalacion/34.png "Logo Title Text 2"
[img_35]: img/01_instalacion/35.png "Logo Title Text 2"
[img_36]: img/01_instalacion/36.png "Logo Title Text 2"
[img_37]: img/01_instalacion/37.png "Logo Title Text 2"
[img_38]: img/01_instalacion/38.png "Logo Title Text 2"
[img_39]: img/01_instalacion/39.png "Logo Title Text 2"
[img_40]: img/01_instalacion/40.png "Logo Title Text 2"
[img_41]: img/01_instalacion/41.png "Logo Title Text 2"
[img_42]: img/01_instalacion/42.png "Conexión SSH"
[img_43]: img/01_instalacion/43.png "Conexión SSH"
[img_44]: img/01_instalacion/44.png "Conexión SSH"
[img_45]: img/01_instalacion/45.png "Conexión SSH"
[img_46]: img/01_instalacion/46.png "Conexión SSH"
[img_47]: img/01_instalacion/47.png "Conexión SSH"
