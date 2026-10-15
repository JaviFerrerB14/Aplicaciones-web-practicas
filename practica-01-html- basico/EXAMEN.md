
## 2. Crear la máquina virtual

1. Abrimos VirtualBox.
2. Pulsamos en Nueva.
3. Ponemos el nombre Ubuntu Server.
4. Seleccionamos Linux como sistema operativo y Ubuntu (64-bit).
5. Seleccionamos la ISO que hemos descargado.
6. Si aparece la instalación desatendida, la desactivamos para instalarlo manualmente.
7. Asignamos 2048 MB o 4096 MB de RAM.
8. Ponemos 2 procesadores si tenemos disponibles.
9. Creamos un disco duro virtual VDI de 25 GB.
10. Pulsamos en Finalizar.

## 3. Configurar la red

1. Seleccionamos la máquina virtual.
2. Entramos en Configuración.
3. Vamos al apartado Red.
4. En el adaptador 1 seleccionamos NAT para tener Internet.
5. Guardamos los cambios.

Si necesitamos que el servidor esté en la misma red que nuestro ordenador, podemos utilizar Adaptador puente.

## 4. Iniciar la instalación

1. Iniciamos la máquina virtual.
2. Seleccionamos Try or Install Ubuntu Server.
3. Esperamos a que cargue el instalador.
4. Elegimos el idioma.
5. Seleccionamos la distribución del teclado Spanish.
6. Continuamos con Done.

## 5. Elegir el tipo de instalación

1. Seleccionamos Ubuntu Server.
2. Continuamos con Done.
3. Dejamos la configuración de red por DHCP si queremos que obtenga una IP automáticamente.
4. En Proxy address no ponemos nada.
5. En Ubuntu archive mirror dejamos el que aparece por defecto.
6. Pulsamos Done para continuar.

## 6. Configurar el disco duro

1. Seleccionamos Use an entire disk.
2. Elegimos el disco virtual que hemos creado.
3. Podemos dejar la configuración de almacenamiento por defecto.
4. Pulsamos Done.
5. Confirmamos con Continue.

Esto borrará el contenido del disco seleccionado, por eso debemos comprobar que estamos utilizando el disco virtual.

## 7. Crear el usuario

Rellenamos los datos:

- Your name: Administrador
- Your server's name: ubuntu-server
- Pick a username: usuario
- Choose a password: ponemos una contraseña
- Confirm your password: repetimos la contraseña

Pulsamos Done.

## 8. Instalar OpenSSH

1. Cuando aparezca SSH Setup, marcamos Install OpenSSH server.
2. Dejamos sin marcar la importación de claves SSH si no tenemos ninguna.
3. Pulsamos Done.

OpenSSH nos permite conectarnos al servidor desde otro ordenador.

## 9. Instalar el sistema

1. En Featured Server Snaps no seleccionamos nada si no nos piden instalar paquetes adicionales.
2. Pulsamos Done.
3. Esperamos a que termine la instalación.
4. Seleccionamos Reboot Now.
5. Si nos pide retirar el medio de instalación, quitamos la ISO desde VirtualBox.
6. Pulsamos Enter para continuar.

## 10. Iniciar sesión

Cuando arranque Ubuntu Server introducimos nuestro usuario y contraseña.

La contraseña no se muestra mientras escribimos, pero se está introduciendo correctamente.

## 11. Actualizar Ubuntu Server

Primero actualizamos la lista de paquetes:

bash
sudo apt update


Después actualizamos los paquetes instalados:

bash
sudo apt upgrade -y


## 12. Comprobar la dirección IP

Para ver nuestra IP ejecutamos:

bash
ip a


Para comprobar la puerta de enlace:

bash
ip route


## 13. Comprobar Internet

Probamos la conexión:

bash
ping -c 4 8.8.8.8


Comprobamos que funciona el DNS:

bash
ping -c 4 google.com


Si recibimos respuestas, tenemos conexión.

## 14. Comprobar SSH

Miramos si SSH está funcionando:

bash
sudo systemctl status ssh


Si aparece active (running), significa que está activo.

Si no está instalado:

bash
sudo apt install openssh-server -y


Para iniciarlo:

bash
sudo systemctl enable --now ssh


## 15. Comandos básicos de Ubuntu Server

Ver la carpeta actual:

bash
pwd


Ver archivos y carpetas:

bash
ls


Entrar en una carpeta:

bash
cd nombre_carpeta


Volver a la carpeta anterior:

bash
cd ..


Crear una carpeta:

bash
mkdir prueba


Crear un archivo:

bash
touch archivo.txt


Editar un archivo:

bash
nano archivo.txt


Ver el contenido:

bash
cat archivo.txt


Borrar un archivo:

bash
rm archivo.txt


Borrar una carpeta vacía:

bash
rmdir prueba


Reiniciar el servidor:

bash
sudo reboot


Apagar el servidor:

bash
sudo poweroff


## 16. Instalar Apache (por si lo necesitamos en Aplicaciones Web)

Instalamos Apache:

bash
sudo apt install apache2 -y


Comprobamos su estado:

bash
sudo systemctl status apache2


Lo iniciamos si está parado:

bash
sudo systemctl start apache2


Activamos el inicio automático:

bash
sudo systemctl enable apache2


Comprobamos la IP:

bash
hostname -I


Desde un navegador con acceso a la red del servidor entramos en:

text
http://IP_DEL_SERVIDOR


Si aparece la página de Apache, funciona correctamente.

La carpeta donde se guardan las páginas web es:

text
/var/www/html


Podemos modificar la página principal con:

bash
sudo nano /var/www/html/index.html


Para guardar en nano pulsamos Ctrl + O, Enter y después Ctrl + X.

# Instalación y configuración de MariaDB en Ubuntu Server

## 1. Actualizar Ubuntu Server

Primero actualizamos los repositorios.

bash
sudo apt update


Actualizamos los paquetes instalados.

bash
sudo apt upgrade -y


## 2. Instalar MariaDB

Instalamos el servidor de MariaDB.

bash
sudo apt install mariadb-server -y


Comprobamos que se ha instalado correctamente.

bash
mariadb --version


## 3. Iniciar MariaDB

Iniciamos el servicio.

bash
sudo systemctl start mariadb


Hacemos que se inicie automáticamente al encender Ubuntu.

bash
sudo systemctl enable mariadb


Comprobamos su estado.

bash
sudo systemctl status mariadb


Tiene que aparecer active (running).

Para salir de la pantalla pulsamos Q.

## 4. Configurar la seguridad

Ejecutamos:

bash
sudo mariadb-secure-installation


Seguimos las preguntas que aparecen.

- Contraseña actual de root: pulsamos Enter si utiliza autenticación por socket y no tiene contraseña.
- Cambiar a autenticación unix_socket: podemos mantenerla si ya está configurada.
- Cambiar contraseña de root: no es necesario si usamos autenticación por socket.
- Eliminar usuarios anónimos: Y.
- Desactivar acceso remoto de root: Y.
- Eliminar base de datos test: Y.
- Recargar privilegios: Y.

Las preguntas pueden variar según la versión.

## 5. Entrar en MariaDB

Para entrar ejecutamos:

bash
sudo mariadb


Cuando aparezca:

text
MariaDB [(none)]>


Significa que estamos dentro.

## 6. Ver las bases de datos

sql
SHOW DATABASES;


Nos muestra las bases de datos existentes.

## 7. Crear una base de datos

Creamos una base de datos llamada instituto.

sql
CREATE DATABASE instituto;


Comprobamos que se ha creado.

sql
SHOW DATABASES;


## 8. Seleccionar una base de datos

sql
USE instituto;


A partir de ahora trabajaremos dentro de esta base de datos.

## 9. Crear una tabla

Creamos una tabla llamada alumnos.

sql
CREATE TABLE alumnos (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(50),
    apellido VARCHAR(50),
    edad INT
);


Comprobamos las tablas existentes.

sql
SHOW TABLES;


Para ver la estructura de la tabla:

sql
DESCRIBE alumnos;


## 10. Insertar datos en la tabla

Añadimos un alumno.

sql
INSERT INTO alumnos (nombre, apellido, edad)
VALUES ('Juan', 'Garcia', 18);


Añadimos varios alumnos.

sql
INSERT INTO alumnos (nombre, apellido, edad)
VALUES
('Pedro', 'Lopez', 19),
('Maria', 'Perez', 17),
('Carlos', 'Sanchez', 20);


## 11. Consultar los datos

Para ver todos los alumnos:

sql
SELECT * FROM alumnos;


Para ver solamente los nombres:

sql
SELECT nombre FROM alumnos;


Para buscar alumnos mayores de 18 años:

sql
SELECT * FROM alumnos WHERE edad > 18;


Para ordenar por edad:

sql
SELECT * FROM alumnos ORDER BY edad ASC;


## 12. Modificar datos

Cambiamos la edad del alumno con ID 1.

sql
UPDATE alumnos
SET edad = 20
WHERE id = 1;


Comprobamos el cambio.

sql
SELECT * FROM alumnos;


## 13. Eliminar datos

Eliminamos un alumno.

sql
DELETE FROM alumnos WHERE id = 1;


Comprobamos que se ha eliminado.

sql
SELECT * FROM alumnos;


Importante: utilizar WHERE para no borrar todos los registros.

## 14. Crear un usuario en MariaDB

Creamos un usuario llamado usuario1.

sql
CREATE USER 'usuario1'@'localhost'
IDENTIFIED BY 'ClaveSegura123!';


Le damos permisos sobre la base de datos instituto.

sql
GRANT ALL PRIVILEGES ON instituto.* TO 'usuario1'@'localhost';


Comprobamos los permisos.

sql
SHOW GRANTS FOR 'usuario1'@'localhost';


## 15. Salir de MariaDB

sql
EXIT;


## 16. Entrar con el usuario creado

Desde la terminal de Ubuntu ejecutamos:

bash
mariadb -u usuario1 -p


Introducimos la contraseña.

Seleccionamos la base de datos.

sql
USE instituto;


Comprobamos que podemos consultar los datos.

sql
SELECT * FROM alumnos;


## 17. Cambiar la contraseña de un usuario

Entramos como administrador:

bash
sudo mariadb


Cambiamos la contraseña:

sql
ALTER USER 'usuario1'@'localhost'
IDENTIFIED BY 'NuevaClave123!';


## 18. Eliminar una tabla

sql
DROP TABLE alumnos;


Este comando elimina la tabla y todos sus datos.

## 19. Eliminar una base de datos

sql
DROP DATABASE instituto;


Cuidado porque elimina toda la base de datos y sus tablas.

## 20. Hacer una copia de seguridad

Salimos de MariaDB:

sql
EXIT;


Desde la terminal de Ubuntu ejecutamos:

bash
sudo mariadb-dump instituto > copia_instituto.sql


Esto crea una copia de seguridad de la base de datos.

## 21. Restaurar una copia de seguridad

Si la base de datos no existe, primero la creamos.

bash
sudo mariadb -e "CREATE DATABASE instituto;"


Restauramos la copia:

bash
sudo mariadb instituto < copia_instituto.sql


Si la base de datos ya existe, no hace falta volver a crearla.

## 22. Reiniciar MariaDB

bash
sudo systemctl restart mariadb


Para detener el servicio:

bash
sudo systemctl stop mariadb


Para volver a iniciarlo:

bash
sudo systemctl start mariadb


## 23. Instalar PHP para conectar con MariaDB

Si necesitamos utilizar MariaDB con Apache y PHP:

bash
sudo apt install php php-mysql libapache2-mod-php -y


Reiniciamos Apache.

bash
sudo systemctl restart apache2


Comprobamos la versión de PHP.

bash
php -v


## 24. Instalar phpMyAdmin (opcional)

Si el examen pide administrar MariaDB desde el navegador:

bash
sudo apt install phpmyadmin -y


Durante la instalación seleccionamos apache2 si aparece la opción y seguimos el asistente de configuración.

Si phpMyAdmin queda correctamente configurado, podemos acceder desde el navegador:

text
http://IP_DEL_SERVIDOR/phpmyadmin


Entramos con el usuario y contraseña de MariaDB.

Si la página no aparece, tendremos que revisar la integración de phpMyAdmin con Apache.

---

# Resumen de comandos importantes

| Comando | Función |
|---|---|
| sudo apt install mariadb-server -y | Instalar MariaDB |
| sudo systemctl status mariadb | Ver estado |
| sudo mariadb | Entrar como administrador |
| SHOW DATABASES; | Ver bases de datos |
| CREATE DATABASE nombre; | Crear base de datos |
| USE nombre; | Seleccionar base de datos |
| SHOW TABLES; | Ver tablas |
| DESCRIBE tabla; | Ver estructura |
| SELECT * FROM tabla; | Consultar datos |
| INSERT INTO | Insertar datos |
| UPDATE | Modificar datos |
| DELETE FROM | Eliminar registros |
| CREATE USER | Crear usuario |
| GRANT | Dar permisos |
| DROP TABLE | Eliminar tabla |
| DROP DATABASE | Eliminar base de datos |
| EXIT; | Salir de MariaDB |

*Importante:* los comandos que empiezan por sudo se ejecutan en la terminal de Ubuntu. Los comandos SQL se ejecutan dentro de MariaDB y normalmente terminan en punto y coma
