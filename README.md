Trabajo Práctico – Administración de Sistemas Linux con Vagrant

Equipo 14 – Brazi & Bearzotti
Entrega Final

0. Máquinas virtuales e IPs

Se prepararon dos máquinas virtuales con una distribución GNU/Linux Jammy’s/64.
A cada VM se le identificó su dirección IP, la cual se registró en el archivo solicitado en la presentación.
Además, cada dirección IP fue guardada dentro del repositorio local de cada máquina para facilitar la comprobación del funcionamiento.

1. Configuración inicial y repositorio

Se creó un repositorio nuevo con el nombre indicado: practica-linux-brazi-bearzotti-equipo14, y se clonó en las dos VMs.
Las capturas de pantalla se almacenan dentro del repositorio, organizadas en un directorio principal y subdivididas según cada VM.
Para revisar la estructura del proyecto, se instaló la herramienta tree.

2. Fastfetch

Desde la primera máquina (brazi) se generó el archivo con la información del sistema utilizando fastfetch, y se subió al repositorio.
En la VM de bearzotti se realizó un pull para incorporar ese archivo, agregar su propia información y volver a subir los cambios.

3. Gestión de permisos

En cada VM se creó el directorio /home/vagrant/(Alumno)_espacio/, donde la X varía según corresponda.
Dentro de ese directorio se generaron los archivos privado.txt y publico.txt aplicando los permisos indicados:

chmod 600 para el archivo privado

chmod 644 para el archivo público

También se creó el grupo equipotrabajo y luego los usuarios utilizando:
sudo useradd -m -s /bin/bash -G equipotrabajo estudianteX
(x = 1, 2 o 3).

A continuación se configuró un directorio colaborativo, creando archivos desde cada usuario y ajustando el grupo propietario para permitir que todos los integrantes del grupo equipotrabajo puedan modificarlos.
Se añadió al repositorio un archivo con la información de cada usuario y sus grupos, así como un archivo de verificación donde todos los usuarios dejaron sus datos de permisos.

4. LVM

Primero se identificó la unidad disponible mediante lsblk.
A partir de esa unidad se creó el PV, luego el VG y finalmente la LV asignándole el espacio correspondiente.
Se dio formato ext4, se creó el punto de montaje, se montó la LV y se añadió al fstab.
La configuración se verificó con los comandos: pvscan, vgscan y lvscan.

5. Gestión de archivos y directorios

Dentro del punto de montaje de la LVM se generó la estructura de directorios utilizando:
mkdir -p /lvm_sotrage_BruchesUserX/{proyectos/{activos,archivados},respaldos,temporales}

Con el bucle proporcionado se crearon 10 archivos en la carpeta temporales.
Posteriormente:

Los archivos 01–05 se copiaron a activos

Los archivos 06–08 se movieron a archivados

Los archivos 09 y 10 se copiaron a respaldo y se eliminaron de temporales

6. Contenedores

Se actualizaron los paquetes e instalaron docker y docker-compose, ya que no venían incluidos en el entorno de Vagrant.
El archivo docker-compose.yml fue transcripto manualmente por problemas de identación al copiarlo directamente.
Luego se ejecutó para revisar los logs y detectar errores tanto en el compose como en prometheus.yml.
Tras las correcciones necesarias, quedó funcionando.
El informe de los errores detectados se encuentra dentro del directorio contenedores.

7. Servidor LAMP (BONUS)

Se actualizaron los paquetes e instalaron las dependencias necesarias para el funcionamiento del servidor LAMP.
Se crearon los archivos index.html, info.php y test_db.php en el directorio correspondiente.
Finalmente, se accedió a la VM desde el navegador usando su IP, se tomaron las capturas y se realizaron todas las verificaciones indicadas.


Aclaración final, nos quedaron archivos por fuera de la carpeta Proyecto los cuales decidimos no eliminar por no estar seguros de que altere algo dentro del git, dentro de nuestras vms no aparecían, solamente la carpeta nombrada anteriormente.
