# ChibiMania — Tienda E-Commerce 

Aplicación web de comercio electrónico desarrollada en PHP con integración a base de datos MySQL. Permite a los usuarios explorar un catálogo de productos (manga/anime), ver el detalle de cada artículo y realizar pagos mediante PayPal.

---

## Descripción

ChibiMania tienda online Multiversatil. El sistema gestiona el catálogo de productos desde una base de datos relacional y presenta la información de forma dinámica al usuario. Incluye un flujo completo desde la vista del catálogo hasta el checkout con integración de PayPal.

---

## Tecnologías utilizadas

| Tecnología | Uso |
|---|---|
| PHP 8 | Lógica del servidor y renderizado dinámico |
| MySQL / MariaDB | Base de datos relacional |
| PDO | Conexión segura a la base de datos |
| Bootstrap 5 | Diseño responsive y componentes UI |
| PayPal SDK (JS) | Procesamiento de pagos |
| HTML / CSS | Estructura y estilos personalizados |

---

## Estructura del proyecto

```
├── pagina/
│   ├── index.php          # Catálogo principal de productos
│   ├── details.php        # Vista detallada de un producto
│   ├── checkout.php       # Página de pago con PayPal
│   ├── config/
│   │   ├── config.php     # Constantes globales (token, moneda)
│   │   └── database.php   # Clase de conexión PDO a MySQL
│   ├── css/
│   │   └── index.css      # Estilos personalizados
│   └── images/            # Imágenes del sitio y productos
│       └── productos/     # Imágenes por ID de producto
└── BD integracion/
    └── productos.sql      # Script SQL para crear e insertar datos
```

---

## Base de datos

Base de datos: `tienda_online`  
Tabla principal: `productos`

| Campo | Tipo | Descripción |
|---|---|---|
| `id` | INT | Identificador único del producto |
| `nombre` | VARCHAR(200) | Nombre del producto |
| `descripcion` | TEXT | Descripción detallada |
| `precio` | DECIMAL(10,2) | Precio base en USD |
| `descuento` | TINYINT | Porcentaje de descuento (0–100) |
| `id_categoria` | INT | Categoría del producto |
| `activo` | INT | 1 = visible en tienda, 0 = oculto |

---

## Funcionalidades

- **Catálogo dinámico:** Los productos se cargan desde MySQL y se muestran en tarjetas con imagen, nombre y precio.
- **Vista de detalle:** Cada producto tiene su propia página con descripción, precio, descuento aplicado y galería de imágenes.
- **URLs seguras:** Los links de detalle usan tokens HMAC-SHA1 para evitar accesos manipulados.
- **Descuentos:** Si un producto tiene descuento asignado, se muestra el precio original tachado y el precio final con el porcentaje.
- **Checkout con PayPal:** Integración con el SDK de PayPal para procesar pagos en USD.
- **Diseño responsive:** Adaptable a dispositivos móviles mediante Bootstrap 5.

---

## Instalación y configuración

### Requisitos
- PHP 8+
- MySQL / MariaDB
- Servidor local: XAMPP, WAMP o similar

### Pasos

1. Clona o descarga el repositorio.
2. Copia la carpeta `pagina/` dentro de `htdocs/` (XAMPP) o el directorio raíz de tu servidor.
3. Importa el archivo `BD integracion/productos.sql` en phpMyAdmin o desde la terminal:
   ```bash
   mysql -u root -p < "BD integracion/productos.sql"
   ```
4. Verifica la configuración de conexión en `pagina/config/database.php`:
   ```php
   private $hostname = "localhost";
   private $database = "tienda_online";
   private $username = "root";
   private $password = "";
   ```
5. Accede desde el navegador a `http://localhost/pagina/`.

---

## Agregar productos con imagen

Las imágenes de productos deben guardarse en:
```
pagina/images/productos/{id_producto}/principal.png
```
Si no existe imagen, se muestra una imagen por defecto (`no-photo.png`).
