# SGE - Sistema de Gestión Empresarial

### 2.1 Requisitos 

- PHP 8.2 o superior
- Composer
- Docker Desktop (con WSL2 habilitado en Windows)

### 2.2 Pasos de instalación

1. Clonar el repositorio:
   ```bash
   git clone <https://github.com/manuela-aguirre/Clase4-SGE>
   cd sge
   ```

2. Instalar las dependencias de PHP con Composer:
   ```bash
   composer install
   ```

3. Copiar el archivo de variables de entorno de ejemplo:
   ```bash
   cp .env
   ```

4. Generar la clave de aplicación:
   ```bash
   php artisan key:generate
   ```

5. Instalar Laravel Sail como dependencia de desarrollo (si el proyecto aún no lo incluye):
  ```bash
   composer require laravel/sail --dev
   php artisan sail:install
   ```
   Durante la instalación se selecciona el servicio `mysql`. Esto genera el archivo `compose.yml` (docker-compose) en la raíz del proyecto.

6. Levantar el entorno de desarrollo con Sail:
   ```bash
   ./vendor/bin/sail up -d
   ```
   - `up` levanta los contenedores definidos en `compose.yml`.
   - `-d` los ejecuta en segundo plano ("detached"), dejando la terminal libre.
   - La primera vez puede tardar varios minutos porque descarga las imágenes de Docker.

7. Verificar que los contenedores quedaron activos:
   ```bash
   docker ps
   ```
   Deben aparecer los servicios `laravel.test` (PHP + servidor web) y `mysql` (base de datos).

8. Ejecutar las migraciones para crear las tablas base (`users`, `sessions`, `failed_jobs`, etc.):
   ```bash
   ./vendor/bin/sail artisan migrate
   ```

9. Acceder a la aplicación en el navegador:
   ```
   http://localhost
   ```
   **Nota:** Sail usa el puerto **80** por defecto, no el 8000. Si el puerto 80 ya está ocupado en el equipo, se puede cambiar la variable `APP_PORT` en el `.env` (ej. `APP_PORT=8080`) y reiniciar con `./vendor/bin/sail down` y `./vendor/bin/sail up -d`.

Para detener el entorno:
```bash
./vendor/bin/sail down
```



## 2.3 Estructura de carpetas

Al ejecutar `composer create-project` (o clonar un proyecto Laravel ya creado), el framework genera la siguiente estructura:

| Carpeta | Función |
|---|---|
| `app/` | Contiene el núcleo de la aplicación: Modelos, Controladores y la lógica de negocio. |
| `bootstrap/` | Archivos que "arrancan" el framework. Casi nunca se modifica. |
| `config/` | Archivos de configuración de Laravel (base de datos, mail, caché, etc.). |
| `database/` | Migraciones, seeders y factories, usados para crear y poblar la base de datos. |
| `public/` | Punto de entrada de la aplicación (`index.php`). Aquí van también CSS, JS e imágenes públicas. |
| `resources/` | Vistas Blade y archivos CSS/JS sin compilar. |
| `routes/` | Definición de todas las rutas (URLs) de la aplicación (`web.php`, `api.php`, etc.). |
| `storage/` | Archivos generados por Laravel: logs, caché y sesiones. |
| `vendor/` | Todas las dependencias instaladas por Composer. No se toca manualmente ni se sube al repositorio. |
| `.env` | Variables de entorno específicas de cada instalación. No se sube al repositorio. |


## 2.4 Variables de entorno

El archivo `.env` contiene las **variables de entorno** de la aplicación: configuraciones que cambian según el entorno donde corre el proyecto (local, pruebas, producción). Es importante porque:

- Separa la configuración del código.
- Permite tener configuraciones distintas en local y en producción.
- **Nunca se sube a GitHub** (debe estar en `.gitignore`).

| Variable | ¿Qué configura? | Ejemplo |
|---|---|---|
| `APP_NAME` | Nombre de la aplicación | `SGE` |
| `APP_ENV` | Entorno de ejecución | `local` |
| `APP_DEBUG` | Modo depuración (muestra errores detallados) | `true` |
| `APP_URL` | URL base de la aplicación | `http://localhost` |
| `DB_CONNECTION` | Motor de base de datos | `mysql` |
| `DB_HOST` | Host de la base de datos | `mysql` (nombre del servicio en Sail) |
| `DB_PORT` | Puerto de conexión a la base de datos | `3306` |
| `DB_DATABASE` | Nombre de la base de datos | `laravel` |
| `DB_USERNAME` | Usuario de la base de datos | `sail` |
| `DB_PASSWORD` | Contraseña del usuario de la base de datos | `password` |

---

## Documentación visual del proyecto

### Captura de pantalla de la landing page

La landing page del sistema está diseñada con los colores caracteristicos de la universidad para transmitir una identidad institucional clara y moderna para la biblioteca universitaria de COTECNOVA.

![![Landing page del sistema](docs/visual/Captura%201.png)

### Cambios visuales realizados

Se realizaron ajustes centrados en dar experiencia visual coherente y profesional para un ERP de biblioteca universitaria:

- Se reforzó la identidad institucional con colores verdes propios de la universidad.
- Se mantuvo una estructura limpia en la landing page con hero section, botones de acción y panel de estadísticas para fácilita el trabajo del bibliotecario.
- Se unificó la estética de login, registro y dashboard con la misma lógica de diseño.
- Se redujo la carga visual y se priorizó una composición sobria con tarjetas, sombras y espacios bien definidos.
- Se incorporó el logo real institucional en los puntos clave de la interfaz para reforzar la identidad de la universidad.
- Se personalizó la navegación y el dashboard para que la experiencia siga siendo uniforme en todo el sistema haciendo más fácil su uso.

### Paleta de colores utilizada

La interfaz usa una paleta verde/blanco inspirada en la identidad institucional de la universidad:

- Verde principal: `#14532d`
- Verde medio: `#15803d`
- Verde claro: `#dcfce7`
- Verde muy claro: `#f0fdf4`
- Fondo general: `#edf8f1`
- Blanco: `#ffffff`
- Texto principal: `#0f172a`
- Texto secundario: `#475569`

### Fuentes y recursos utilizados

- Fuente principal: `Figtree`, importada desde Google Fonts.
- Iconografía: Font Awesome 6 (CDN).
- Logo institucional: imagen localizada en `public/build/images/logo-cotecnova.png`.
- Estilos base: Tailwind + CSS personalizado en Blade y Vite.
- Las pantallas principales y componentes visuales se construyeron con un enfoque de diseño moderno, minimalista y enfocado en ERP académico/bibliotecario.

### Recursos de diseño aplicados

- Bordes redondeados para tarjetas y botones.
- Sombras suaves para profundidad visual.
- Layouts con espacios generosos para una lectura clara.
- El mismo esquema cromático en todas las vistas principales.
- Componentes reutilizables para mantener coherencia entre login, registro, welcome y dashboard.




