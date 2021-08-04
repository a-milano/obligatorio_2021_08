# obligatorio_2021_08

## Intro 

De que se trata el codigo.
Roles
Como usarlo
Cambios en archivos
Condicionales



Cambios realizados:

Archivo ansible.cfg

[defaults]
inventory       = /home/sfeijo/repos/obligatorio_2021_08/hosts/hosts.ini

remote_user = ansible

[privilege_escalation]
become = yes
become_method = sudo

roles_path = /home/sfeijo/repos/obligatorio_2021_08/lamp/roles


## Cambios en roles

# Common

name: ['python3-libselinux', 'python3-libsemanage', 'firewalld']

## esta parte , copia el archivo de configuracion de ntp.Si hubo cambios reinicia el servicio.
- name: Configure ntp file
  template: 
    src: /home/sfeijo/repos/obligatorio_2021_08/lamp/roles/common/templates/ntp.conf.j2 
    dest: /etc/ntp.conf
  tags: ntp
  notify: "Restart ntp"

