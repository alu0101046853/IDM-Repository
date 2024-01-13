# Despliegue de Hadoop usando Ansible

Como paso previo ejecutamos el playbook [ovirt-install](./ovirt-install-playbook.yml) para poder instalar las dependencias para poder crear máquinas en oVirt automáticamente.

- 1º: Ejecutamos el playbook de [crear-ovejas](./crear-ovejas-playbook.yml) para crear las máquinas a configurar. Al ejecutarlo configuramos el [inventario](./hosts) ansible y el archivo /etc/hosts con las máquinas configuradas.

- 2º: Ejecutamos el playbook de [host-configuration](./hosts-configuration-playbook.yml) para configurar los nombres de los host en las máquinas de Hadoop.

- 3º: Ejecutamos el playbook de [create-user-hadoop](./create-user-hadoop-playbook.yml) para crear el usuario Hadoop en todas las máquinas y setear las claves públicas para poder hacer ssh sin contraseña.

Cambiamos al usuario hadoop en nuestra máquina ansible para poder ejecutar los playbooks como este usuario.

- 4º: Ejecutamos el playbook de [hadoop-install](./hadoop-install.playbook.yml) para instalar hadoop y Java en las máquinas Hadoop.

- 5º: Ejecutamos el playbook de [java-configuration](./java-configuration-playbook.yml) para configurar las variables de entorno.

- 6º: Ejecutamos el playbook de [hadoop-configuration](./hadoop-conf-playbook.yml) para configurar todo lo básico del namenode y datanodes de hadoop.

- 7º: Ejecutamos el playbook de [yarn-map-conf](./yarn-map-conf-playbook.yml) para acabar de configurar los ficheros mapred-sites y yarn-site.

Por último quedaría ejecutar el comando ```hdfs namenode -format``` y el comando ```start-all.sh```  en el **namenode** para arrancar todos los servicios hadoop.

Existe la posibilidad de borrar todas las máquinas con el playbook [borrar-ovejas](./borrar-ovejas-playbook.yml).