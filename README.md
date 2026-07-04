# AppSalon

Sistema de gestión de citas para una barbería/salón. Permite a los usuarios registrarse, elegir servicios y agendar una cita.

> **Nota:** Proyecto académico realizado como parte del curso "Desarrollo Web Completo con HTML5, CSS3, JS, PHP y MySQL" (Udemy).

## Stack

- **Backend:** PHP 8, MVC propio (Router, Controllers, Models, Active Record)
- **Base de datos:** MySQL
- **Frontend:** SCSS (Sass), JavaScript
- **Envío de emails:** PHPMailer + Mailtrap (SMTP de testing)
- **Variables de entorno:** vlucas/phpdotenv
- **Build:** Gulp + Sharp (optimización/conversión de imágenes)
- **Gestión de dependencias:** Composer (PHP) + NPM (assets)

## Requisitos

- PHP >= 8.0
- Composer
- Node.js + NPM
- MySQL

## Instalación

1. Cloná el repo:

```bash
git clone https://github.com/lucas99morel/appsalon.git
cd appsalon
```

2. Instalá dependencias:

```bash
composer install
npm install
```

3. Creá la base de datos importando el schema (incluye seeds):

```bash
mysql -u root -p --default-character-set=utf8mb4 < schema.sql
```

4. Copiá el archivo de variables de entorno de ejemplo y completá tus credenciales:

```cmd
copy .env.example .env
```

Editá `.env` con tus credenciales de MySQL y de Mailtrap:

```env
DB_HOST=localhost
DB_NAME=appsalon_mvc_php
DB_USER=tu_usuario
DB_PASS=tu_password

MAIL_HOST=smtp.mailtrap.io
MAIL_PORT=2525
MAIL_USERNAME=tu_usuario_mailtrap
MAIL_PASSWORD=tu_password_mailtrap
```

> **Nota:** Mailtrap es un servicio gratuito para testing de emails (no envía correos reales). Creá tu propia cuenta en [mailtrap.io](https://mailtrap.io), armá un inbox, y usá esas credenciales SMTP.

5. Compilá los assets (CSS, JS, imágenes):

```bash
npm run dev
```

Esto corre `js → css → imagenes` y deja Gulp en modo watch sobre `src/scss`, `src/js` y `src/img`, generando todo en `public/build`.

6. Levantá un servidor apuntando a `public/` como document root:

```bash
php -S localhost:3000 -t public
```

## Usuarios de prueba (seeds)

El `schema.sql` incluye dos usuarios ya confirmados para probar la app sin tener que registrarte:

| Rol      | Email              | Password   |
|----------|---------------------|------------|
| Admin    | correo@correo.com   | password   |
| Cliente  | ana@correo.com      | password   |


## Estructura
```
AppSalon/
├── classes/
│   └── Email.php          # Envío de correos (confirmación, recuperar password)
├── controllers/            # Controladores MVC
├── includes/
│   ├── app.php              # autoload, dotenv, conexión BD
│   ├── database.php          # Conexión mysqli (usa variables de .env)
│   └── funciones.php
├── models/                   # Modelos (Active Record)
├── public/                    # Document root — index.php, assets compilados
│   └── build/                  # CSS, JS e imágenes generados por Gulp
├── src/
│   ├── scss/
│   ├── js/
│   └── img/
├── views/                       # Vistas (templates)
├── vendor/                       # Dependencias de Composer
├── node_modules/
├── Router.php                     # Enrutador de la app
├── composer.json
├── package.json
├── gulpfile.js
├── schema.sql                      # Script de creación de la BD + seeds
├── .env.example                     # Plantilla de variables de entorno
└── .env                               # Variables reales (no se sube al repo)
```

## Notas

- Las variables de entorno se cargan en `includes/app.php` vía `phpdotenv`, antes de conectarse a la BD o instanciar PHPMailer.
- Las imágenes se procesan automáticamente a `.jpg`, `.webp` y `.avif` vía Sharp; los `.svg` se copian tal cual.
