# Laravel-docker con base de datos para pruebas y phpmyadmin

## Requerimientos

- Docker-compose

---

## Instalación

- Copiar los archivos al directorio raíz del proyecto.
- Modificar el archivo .env dejando "DB_HOST=db".

```env
DB_HOST=db
```

- Modificar el archivo phpunit.xml colocando las siguientes lineas. (Remplazar "base de datos" con el nombre de la base de datos utilizada en producción).

```xml
<server name="DB_CONNECTION" value="mysql"/>
<server name="DB_DATABASE" value="<<base de datos>>_tests"/>
<server name="DB_HOST" value="db-tests"/>
```

-   IMPORTANTE: agregar el sufijo \_tests despues del nombre de la base de datos.

## Ejecución

```bash
docker-compose build app
docker-compose up -d
docker-compose exec app composer install
docker-compose exec app php artisan migrate
```

- Ir a localhost:8000 y comprobar que funciona.

---

## Abrir phpmyadmin

- Ir a localhost:8081 y usar el usuario root y la contraseña usada en el .env.

---

## Correr pruebas

```bash
docker-compose exec app php artisan test
```

---

## Exportar base de datos

- Remplazar las variables con las usadas en el .env.

```bash
docker-compose exec db /usr/bin/mysqldump   -u <<user> --host=db --password=<<password>> <<base_de_datos>> > backup.sql
```
