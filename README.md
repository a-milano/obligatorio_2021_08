# obligatorio_2021_08

## Intro 

El código se trata de la instalación de distintos paquetes en servidores Linux, a partir de diferentes roles configurables.
Estos roles fueron creados con el propósito de poder ser usados tanto para distribuciones de Debian como de Redhat.
El objetivo de usar roles es que el código sea escalable y adaptable a los requerimientos necesarios. En caso de necesitar implementar una nueva funcionalidad, no es necesario modificar el código, si no agregar un nuevo rol e invocarlo desde el playbook principal.
Cada rol contiene archivos de

Para poder utilizar este playbook se debe ejecutar el archivo site.yml, desde este archivo se referencia a los diferentes roles.
	# ansible-playbook site.yml

Archivo de configuración:
ansible.cfg, en este archivo se encuentran los parámetros de configuración generales, como ser ubicación de archivo de inventario, ubicación de roles, usuario remoto y escalación de privilegios de usuario.

Cambios realizados en los archivos:
## Cambios en roles
# Common
En este archivo se realizo corrección de sintaxis, corrección de nombres de paquetes según la distro y se aplicó condicionales teniendo que hacer para este ultimo punto el agregado del siguiente código:
when: ansible_facts['os_family'] == "Debian"
when: ansible_facts['os_family'] == "RedHat"
Este código se agrega al final de cada play dependiendo de la tarea que corresponda.
Para realizar la instalación de las dependencias en vez de usar with_items, se utilizó una lista:
name: ['python3-libselinux', 'python3-libsemanage', 'firewalld'].
Se utiliza un archivo handler para reiniciar el servicio ntp (chronyd).
También desde este rol se llama a un archivo template el cual copia la configuración del servicio a los servidores.


	#DB
En este rol se realizó corrección de sintaxis, se corrigió nombre de paquetes, se agregó el uso de variables las cuales se definen en el playbook principal, en el archivo site.yml.
En este rol se adapto el uso de condicionales para los casos que son necesarios.
Al igual que en el rol common, se utiliza handler para reiniciar la base de datos y un template para copiar la configuración de  mysql a los servidores.


#WEB
Este rol cuenta con tres archivos, uno principal (main), uno de configuración (copy_code.yml) y otro de instalación (install_httpd.yml). Desde el archivo principal se ejecutan los otros dos.
	En este rol se realizó corrección de sintaxis, se corrigió nombre de paquetes.
En este rol se adaptó el uso de condicionales para los casos que son necesarios.
Al igual que en el rol common, se utiliza un template para copiar la estructura del sitio a los servidores.
