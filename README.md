** Moodle**

## Instal·lació i configuració d'aplicacions web

Per instal·lar una aplicació web hem de baixar el seu codi font i portar-lo al directori arrel del nostre servidor d'aplicacions, en el nostre cas, apache2. Quan instal·lem apache2 es crea una carpeta a `/var/www/html` on, per defecte, el servidor web utilitza com a directori arrel.

Llavors, si portem la nostra aplicació al directori `/var/www/html` tindrem accés a la nostra aplicació mitjançant l'adreça `http://localhost`.

---

## Instal·lació d'apache2, mysql i algunes llibreries al contenidor

### Actualització de la màquina
```bash
sudo apt update
sudo apt upgrade
```

### Instal·lació del servidor web apache2
```bash
sudo apt install -y apache2
```

### Instal·lació del servidor de bases de dades mysql-server
```bash
sudo apt install -y mysql-server
```

### Instal·lació d'algunes llibreries de PHP
```bash
sudo apt install -y php libapache2-mod-php
sudo apt install -y php-fpm php-common php-mbstring php-xmlrpc php-soap php-gd php-xml php-intl php-mysql php-cli php-ldap php-zip php-curl
```

### Reiniciem el servidor apache2
```bash
sudo systemctl restart apache2
```

---

## Configuració de MySQL

### Accedim a la consola de MySQL
Des d'un terminal on siguem root hem d'executar la següent comanda:
```bash
sudo mysql
```

### Creació de la base de dades
Un cop dins la consola de MySQL executem les comandes per a crear la base de dades.
```sql
CREATE DATABASE bbdd;
```

### Creació d'un usuari
Tingueu en compte que s'haurà d'identificar la IP des de la qual s'accedirà a la base de dades, en aquest cas, `localhost`.
```sql
CREATE USER 'usuario'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
```

### Donem privilegis a l'usuari
```sql
GRANT ALL ON bbdd.* to 'usuario'@'localhost';
```

### Sortim de la base de dades
```bash
exit
```

### Probem la connexió a la base de dades
Des d'un terminal amb un usuari sense privilegis hem de ser capaços de connectar introduïnt la nostra contrassenya.
```bash
mysql -u usuario -p
```

---

## Descarreguem els fitxers de l'aplicació web

Anem al directori `/var/www/html` i descomprimim allà els fitxers de l'aplicació web. Heu de substituir `app-web.zip` pel nom del vostre fitxer que heu descarregat amb l'aplicació web i el nom de la carpeta `app-web` per la carpeta que us ha creat.

```bash
sudo cp ~/Baixades/app-web.zip /var/www/html
```

### Aneu al directori `/var/www/html`
```bash
cd /var/www/html
```

### Descomprimiu el fitxer que heu baixat
```bash
sudo unzip app-web.zip
```

### Copieu els fitxers a la carpeta `/var/www/html`
```bash
sudo cp -R app-web/. /var/www/html
```

### Eliminem la carpeta creada quan hem fet l'unzip
```bash
sudo rm -rf app-web/
```

### Eliminem el fitxer `index.html` de l'apache2
```bash
sudo rm -rf /var/www/html/index.html
```

---

## Aplicació de permisos a les nostres aplicacions web

Un cop descomprimits els fitxers de l'aplicació web al directori `/var/www/html`, apliquem els següents permisos:

```bash
cd /var/www/html
sudo chmod -R 775 .
sudo chown -R usuario:www-data .
```

---

## Accedim al navegador per veure que tot funciona

Poseu la direcció `http://localhost` al navegador web i configureu la cloud.

Si tot ha anat bé i heu seguit el manual, us apareixerà l'instal·lador de l'aplicació web que heu baixat i us demanarà crear un usuari admin i la informació de la base de dades.

### La informació que heu de posar (si no heu modificat la informació del manual) és la següent:
- **Usuari**: `usuario`
- **Contrasenya**: `password`
- **Base de dades**: `bbdd`
- **Domini**: `localhost`



![Descripción de la imagen](https://lh7-rt.googleusercontent.com/docsz/AD_4nXetF3vJf2ETGMx6P7PiZSqSMd7UamPlclSiP90tN1im7xPSyOyLnRBD6lzvwFBqF2maNwQ-RQFP02BtIMHSYnaiN147zu0yWBQKE4wO-zQpV53o3BIRrNpRbBaS1Z_JDg7AHp6xGQ?key=c0F-wb2xdPICaYdeQn-Vv90A)

## Tendrás que iniciar sesión

---

![Descripción de la imagen](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeFxm9MFiLJsECld1yWmbXjISgNhF6yJ_FcEMqvp5FcFxTti7pXgwm_dgs7htq6atkro0aW7X1O9ptQT2aiXHMDe4nC6bBQNMTrl6wlO0aEd3dda_61hImNzELzGeqIUUhWlgEgWw?key=c0F-wb2xdPICaYdeQn-Vv90A)

## Cambia el nombre de tu Moodle y ajusta tu zona horaria

![Descripción de la imagen](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfOdOLT9Qyv7Vyz22BcbytvyLYtG21p3_X7YmeYPl9sqJuc-O_Jxdo_vYajqGFgR3TqFyIAJMAuSAbPjBqxQYAfNqR3APPVEpqgFKfRsDMQSzgIJrDf_ydHyoaxP21M6B40w6bESA?key=c0F-wb2xdPICaYdeQn-Vv90A)

## Configura el idioma de tu Moodle

![Descripción de la imagen](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdp1hQ45Cdj9x4qfmEun60U57c5nXDLPBoL0fFhDDI5GcCnvJHC7md_y3YQG0AN0r73Xu_ZUtmIBqm3uHjPOieU_DLWnjcddZxnGcYnCsVvrJaEwf_wbAsSupJ2xNWyrFqazQqoog?key=c0F-wb2xdPICaYdeQn-Vv90A)

## Políticas de seguridad

Dirígete a **Administración del sitio > Seguridad > Políticas de seguridad del sitio** para actualizar las políticas de contraseña conforme a tus necesidades.

---

## Creación de usuario y cursos

![Descripción de la imagen](https://lh7-rt.googleusercontent.com/docsz/AD_4nXe4BZ6oRgZ8KNxmpy3JPcZgdIcmwzcugxqA4vJgAoUitjuy8IbaLc4PZA9kRf1994E760ST8Nde9xBwL5C5lq11_LEL5EA0kQgAbUtLNfqruLtoW8ljVz3G0cCvLINE1oHSaa1b6w?key=c0F-wb2xdPICaYdeQn-Vv90A)

Crea un usuario con el nombre que desees (por ejemplo, "A"). Luego, genera los cursos necesarios, asegurando incluir al menos tres temas en cada uno y agregando actividades propias.

---

![Descripción de la imagen](https://lh7-rt.googleusercontent.com/docsz/AD_4nXd3eAhul9zUW-rJu8Fv5bgF9ditKzxaZSEa_MV0xzU-XpuF8oP2v6GHyL-mKFh_ATN4-tQaDjcb21YHk-YGJOrzkpgbnqutfCR8D8ns8t8uibmAN8XOe9Vrp6FXsMw0xmkTWIcP?key=c0F-wb2xdPICaYdeQn-Vv90A)

Asegúrate de incluir actividades personalizadas para completar los cursos.

---

## Creación de usuarios

![Descripción de la imagen](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeCdnF-hRiUJd28Nd-4OM2LA8FXnhwREjxH3xg45MIVb1tD5Sk9i9yKbisjXE_wYaNBqFlSzAR0C1d49VdM7zNZhdC8F6VTEi7lpsS9z4s-VwKbiKdPq-iEuHSvMsDjCgrK0hYL_g?key=c0F-wb2xdPICaYdeQn-Vv90A)

Dirígete a **Administració del lloc > Usuaris > Comptes > Afegeix un usuari** y rellena los datos: nombre, apellido, correo y contraseña.

---

## Creación y eliminación de usuarios

![Descripción de la imagen](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdxX2e9VmCvrubdXaKdTZux8-vpn8rwXXzDXaHlMy1z85U8RPUTl7ptSHXJUhp0d2HdXhjg3mENRKpANBn-b9laMc4a9R2Yr0OOhcRopxgYctdOldeDAIdVM-HAv9DXMs19yMBM?key=c0F-wb2xdPICaYdeQn-Vv90A)

Crea alrededor de 10 usuarios por curso para "A" y "B".

---

![Descripción de la imagen](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfz7i2D-Xne2IP_3HTqMx-TErkYIvDWf1VxmSRjf8p97gUreUkPSkDT2V1OzUf89PwIXAiZE52F9irVwiMchNBPkJL9D0ePPZxoC1rGoVohQk0Kj_nGD0OlKV2u2QV8PPmmKBB-yQ?key=c0F-wb2xdPICaYdeQn-Vv90A)

Dirígete a **Administració del lloc > Usuaris > Accions amb usuaris en bloc** para eliminar a dos usuarios mediante la opción "eliminar de la selección".

---

## Inscripción de usuarios en los cursos

![Descripción de la imagen](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdZ18rz1MxMxhOLPozO7Pa7FUHSy4B-N7VM9SPmf5BXCFO6mQoydU2ToUz7Q6c3v4-JLo3NQpwe1qAj67LLzhfNfnf8vdGe0TadylG1vT8aNP2cksiJkbGFOxdosxaFsg5OtaZP?key=c0F-wb2xdPICaYdeQn-Vv90A)

En el curso "A", la inscripción no debe ser posible. En el curso "B", debe requerir registro manual. Asigna a "Bob" como profesor y al resto como estudiantes.

---

## Personalización de Moodle

![Descripción de la imagen](https://lh7-rt.googleusercontent.com/docsz/AD_4nXc6epNAOCMtWhe6cpZIrPBhETUIuzeVSSG8F7_Gt6Q5GrMOYvGX_yFtMs7PahgxRywRuvh185JQR_XzC4TOAH1AOgiCHNHhepZdFza8xO1crZBsQjKGMp5c5yGFTWJXwUOXm0Ur9g?key=c0F-wb2xdPICaYdeQn-Vv90A)

Accede a **Administración del sitio > Conectores > Instalar complemento** para modificar la apariencia de tu Moodle.
