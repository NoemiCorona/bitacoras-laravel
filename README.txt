Guía de Instalación: Laravel con PostgreSQL

##  Prerrequisitos
- Windows 10/11
- XAMPP instalado
- PHP 8.2+

## 🔧 Instalación de Composer

### 1. Descargar e instalar Composer
cmd
# Descargar el instalador
php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"

# Verificar el instalador
php -r "if (hash_file('sha384', 'composer-setup.php') === 'dac665fdc30fdd8ec78b38b9800061b4150413ff2e3b6f88543c636f7cd84f6db9189d43a81e5503cda447da73c7e5b6') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"

# Ejecutar instalación
php composer-setup.php
php -r "unlink('composer-setup.php');"


### 2. Mover Composer a PATH del sistema
cmd
mv composer.phar C:\xampp\php\composer.phar

# Crear archivo batch
echo @php "%~dp0composer.phar" %*> C:\xampp\php\composer.bat


### 3. Verificar instalación
cmd
composer --version


## Creación de Proyecto Laravel

### 1. Crear nuevo proyecto
cmd
cd C:\xampp\htdocs
composer create-project laravel/laravel bitacoras


### 2. Acceder al proyecto
cmd
cd bitacoras


##  Configuración de Base de Datos PostgreSQL

### 1. Configurar archivo .env
env
DB_CONNECTION=pgsql
DB_HOST=127.0.0.1
DB_PORT=5432
DB_DATABASE=db_denso_bitacora_UUID
DB_USERNAME=postgres
DB_PASSWORD=tu_password


### 2. Generar clave de aplicación
cmd
php artisan key:generate


##  Migraciones y Modelos

### 1. Crear migración para bitácoras
cmd
php artisan make:migration create_bitacoras_table

### 2. Configurar migración (database/migrations/*_create_bitacoras_table.php)
php
Schema::create('bitacoras', function (Blueprint $table) {
    $table->id();
    $table->string('accion');
    $table->text('descripcion')->nullable();
    $table->string('modulo');
    $table->foreignId('user_id')->constrained()->onDelete('cascade');
    $table->timestamps();
});


### 3. Ejecutar migraciones
cmd
php artisan migrate


### 4. Crear modelo
cmd
php artisan make:model Bitacora


## 🚀 Ejecutar Servidor de Desarrollo

### 1. Iniciar servidor
cmd
php artisan serve


### 2. Acceder a la aplicación
Abrir navegador en: `http://localhost:8000`

# Verificar instalación
cmd
php artisan --version
composer --version
php --version


### Verificar base de datos
cmd
php artisan migrate:status

##Estructura del Proyecto
bitacoras/
├── app/Models/Bitacora.php
├── database/migrations/
├── routes/web.php
├── resources/views/
└── .env
