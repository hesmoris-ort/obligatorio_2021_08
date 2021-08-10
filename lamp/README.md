# instalación y configuración de LAMP - Para CentOS y Ubuntu
-------------------------------------------

Este libro de trabajos está desarrollado y probado con Ansible 2.9.6

A través de este libro de trabajo podemos instalar y configurar los servicios LAMP, en servidores CentOS y Ubuntu

En el libro de tareas “site.yml” a través de roles:
-	Se lanzan las tareas básicas de configuración para todos los equipos.
-	Se instala y configuran los servicios de servidor web, para los equipos que estén dentro del grupo “webserbers”.
-	Se instala y configuran los servicios de servidor de base de datos, para los equipos que estén dentro del grupo “dbserbers”

Se definen los grupos “webserbers” y “dbserbers”, de acuerdo con los roles que en ellos se quiera instalar. De igual modo, si se cargan otros grupos en el inventario, se analizará la distribución y se ejecutaran sobre ellos, las tareas básicas, siempre que sean CentOS o Ubuntu, y se ejecute la tarea sin etiquetas.

Es posible ejecutar la tarea con la cantidad de equipos que se quiera, cargados en el archivo “hosts”; para los roles de servidor web y servidor de base de datos, es necesario que estén dentro de los grupos que corresponden.
Es necesario que se definan en el inventario:
-	Los equipos que pertenecerán al grupo “dbservers”
-	Los equipos que pertenecerán al grupo “webservers”
-	Además, para la aplicación, debe indicarse, cuál será la dirección ip del servidor de base de datos en la variable “ipdb”

La tarea se puede ejecutar con el siguiente comando:
_ ansible-playbook site.yml

También es posible la ejecución de las tareas, a través de las etiquetas, que son las siguientes:
-	     basic
-	     web
-	     db

Las etiquetas, aplican a cada uno de los roles y grupos de equipos, un ejemplo de la ejecución es el siguiente:

_ ansible-playbook site.yml --tags db

Las tareas básicas son requeridas para las demás, ya que se considera que hay programas instalados y activados, que son requeridos.



# Requerimientos

Son requeridos para los trabajos, los módulos de ansible:
-	ansible.posix
-	community.general
-	community.mysql

Dadas las definiciones en el archivo “ansible.cfg”, se requiere crear la carpeta “ansible”, que contenga dentro las carpetas “log” y “tmp”, en el “home” del usuario que ejecutara las tareas. Dentro de la misma se debe colocar la carpeta “lamp”, del repositorio, con todo su contenido.
De acuerdo con las indicaciones, en la documentación de Ansible, después de copiar el repositorio al equipo “bastion” ansible, se deben modificar los permisos del archivo a “660” o “600”, como también deben quitarse los permisos sobre la carpeta, para “otros”, cambiando los permisos a “770” o “700”

Los clientes requieren tener un usuario con nombre “ansible”, el mismo debe ser “sudoers” y poder escalar permisos, sin necesidad de contraseña. 
Se debe configurar el acceso del equipo bastión a los clientes, sin necesidad de uso de contraseña. Puede ser a través de una llave del usuario con el que se ejecuten las tareas en el equipo bastión o cargando un certificado.


# Pruebas realizadas

Para el desarrollo de la tarea como los roles, se utilizó como bastión un equipo Windows con WSL (Ubuntu 20.04 LTS)
Para poder trabajar correctamente es necesario habilitar el sistema de permisos en WSL.
Para habilitarlo dejo el siguiente enlace:
https://community.dataquest.io/t/chmod-not-working/364329
Se utilizo ansible 2.9.6.
Los equipos clientes con los que realizaron pruebas fueron:
-	CentOS 8.4
-	Ubuntu 20.04 Server 
