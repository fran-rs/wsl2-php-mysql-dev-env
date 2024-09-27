# Guía de Instalación de PHP y MySQL en WSL2
Esta guía te llevará a través del proceso de instalación de PHP, MySQL y Apache en tu entorno WSL2, así como la configuración de un usuario en MySQL y ajustes de PHP.

## Requisitos Previos
Asegúrate de tener WSL2 instalado y actualizado en tu sistema Windows. También necesitas tener instalado un sistema operativo basado en Ubuntu y una terminal abierta.

## Pasos de Instalación
1. Actualizar el Sistema
Actualiza los repositorios de paquetes y los paquetes instalados:


```bash
sudo apt update
sudo apt upgrade
```

2. Instalar PHP
Instala PHP y verifica la instalación:

```bash
sudo apt install php
php -v
```

3. Instalar MySQL y reiniciar servicio
Instala el servidor MySQL:

```bash
sudo apt install mysql-server
```
```bash
sudo service mysql start
```
Configurar un Usuario de MySQL
Inicia sesión como root en MySQL:


```bash
sudo mysql -u root
```
Crea un nuevo usuario y asigna privilegios:

```sql

CREATE USER 'lucy'@'localhost' IDENTIFIED BY 'lucilu.';
FLUSH PRIVILEGES;

GRANT ALL PRIVILEGES ON *.* TO 'lucy'@'localhost';
FLUSH PRIVILEGES;

GRANT GRANT OPTION ON *.* TO 'lucy'@'localhost';
FLUSH PRIVILEGES;
```
Verifica la conexión con el nuevo usuario:

```bash
mysql -u lucy -p
```
4. Instalar Apache
Instala el servidor web Apache:

```bash

sudo apt install apache2
Puedes verificarlo ingresando a http://localhost en tu navegador.
```
5. Instalar PHP para Apache
Instala el módulo de PHP para Apache:

```bash

sudo apt install libapache2-mod-php
6. Instalar la Extensión de MySQL para PHP
Instala la extensión de MySQL para que PHP pueda comunicarse con MySQL:
```

```bash
sudo apt install php-mysql
```
7. Reiniciar Apache
Reinicia el servicio de Apache para aplicar los cambios:


```bash
sudo service apache2 restart
```
8. Instalar phpMyAdmin
Habilita el módulo de reescritura en Apache:


```bash
sudo a2enmod rewrite
```
9. Instalar TablePlus
Si deseas utilizar una interfaz gráfica, puedes instalar TablePlus y crear una nueva conexión:

* Presiona + para agregar una conexión.
* Selecciona MySQL.
* Completa los campos:
    * Name: Cualquier nombre que prefieras.
    * Host: localhost
    * Port: 3306
    * Username: lucy
    * Password: lucilu.
* Presiona Test para verificar la conexión y luego OK y Connect.

10. Aumentar la Capacidad de PHP
Para aumentar el tamaño máximo de las cargas y las solicitudes POST, edita el archivo de configuración de PHP:

```bash
sudo vim /etc/php/8.1/apache2/php.ini
```

* Buscar y Modificar las Configuraciones
    * Buscar post_max_size:

        Presiona / para iniciar la búsqueda.
        Escribe post_max_size y presiona Enter.
    * Entrar en Modo de Edición:

        Una vez que encuentres la línea, presiona i para entrar en el modo de inserción.
    * Modificar el Valor:

        Cambia el valor a 100M, así:

        post_max_size = 100M
    * Buscar upload_max_filesize:

        Presiona / nuevamente, escribe upload_max_filesize y presiona Enter.
        Entrar en Modo de Edición y Modificar:

        Presiona i para editar y cambia el valor a 100M:

        upload_max_filesize = 100M
    * Guardar y Salir:

        Presiona Esc para salir del modo de inserción.
        Mantén presionado Shift y presiona Z dos veces (Shift + ZZ) para guardar los cambios y salir del editor.
11. Reiniciar Apache Nuevamente
Reinicia Apache para aplicar los cambios:

```bash
sudo service apache2 restart
```
11. Reiniciar Apache Nuevamente
Reinicia Apache para aplicar los cambios:

```bash
sudo service apache2 restart
```
12. Crear un Archivo PHP para Verificar la Instalación
Crea un archivo info.php para verificar la instalación de PHP:

```bash
sudo vim info.php
Agrega el siguiente código:
```
```php
<?php
phpinfo();
```
Guarda y cierra el archivo como antes.

13. Verificar la Instalación
Puedes verificar que PHP está funcionando correctamente visitando http://localhost/info.php en tu navegador.

14. Listar Archivos y Ver Contenido de index.html
Para verificar archivos en tu directorio actual:

```bash
ls
cat index.html
```
