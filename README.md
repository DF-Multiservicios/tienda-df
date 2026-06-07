# 🚀 Guía de DF Multiservicios - Publicación y Gestión del E-commerce

Esta carpeta contiene la versión definitiva de tu sitio web optimizado para **GitHub Pages** y diseñado en **Negro y Naranja**.

---

## 🆕 Últimas Novedades y Mejoras
1. **Solo el precio final**: Eliminamos el "precio original" tachado de la tienda. Ahora solo se muestra el precio final con el margen de ganancia aplicado, logrando un diseño más limpio y directo.
2. **Productos manuales funcionando correctamente**: La base de datos local y el scraper se comunican de forma fluida. Ahora tus productos en `data/productos_manuales.json` se fusionarán automáticamente.
3. **Precios manuales más flexibles**: El sistema de excepciones de precios en `data/precios_manuales.json` ya no requiere que escribas el nombre exacto de forma estricta. Admite minúsculas/mayúsculas indiferentemente y realiza búsquedas de palabras clave (coincidencias parciales), facilitando su edición.
4. **Actualización automática instantánea en GitHub**: Añadimos un disparador al workflow. Cada vez que subas cambios en tus archivos de configuración (`productos_manuales.json`, `precios_manuales.json` o `scraper.py`), GitHub ejecutará el scraper inmediatamente y actualizará la página web en menos de un minuto.

---

## 📂 Estructura del Proyecto

```text
/GITHUB
├── .github/workflows/actualizar-inventario.yml # Ejecución en push y diaria a las 00:00 UTC
├── assets/
│   ├── css/style.css                          # Estilos de fondo y efectos (Negro/Naranja)
│   └── js/main.js                             # Catálogo interactivo (Solo muestra el precio final)
├── data/
│   ├── productos.json                          # Catálogo final compilado (No editar a mano)
│   ├── productos_manuales.json                 # Tus productos personalizados (¡Agrégalos aquí!)
│   └── precios_manuales.json                   # Excepciones de precios (Coincidencia flexible)
├── images/
│   ├── logo.jpeg                              # Logotipo de la empresa
│   └── ...                                    # Fotos de los servicios y productos
├── index.html                                 # Página web principal (Sin formulario de contacto)
├── scraper.py                                 # Script de Python con coincidencia flexible y mezcla manual
└── README.md                                  # Esta guía de uso
```

---

## ☁️ 1. Cómo aplicar los cambios por primera vez en GitHub

Para subir esta nueva versión mejorada a tu repositorio existente de GitHub, abre la consola en la carpeta `C:\Users\PC\Desktop\GITHUB` y ejecuta los siguientes comandos:

```bash
# 1. Registrar todos los archivos modificados
git add .

# 2. Crear un punto de restauración con los cambios de diseño y flujo
git commit -m "Actualizacion: sin precio original y auto-ejecucion en push"

# 3. Subir los archivos a tu repositorio en GitHub
# (Esto cargará el nuevo workflow, el index.html sin formulario y el main.js sin precio original)
git push origin main
```

Una vez subido, ¡tu sitio web se actualizará con el nuevo diseño!

---

## 🛍️ 2. Cómo agregar y modificar productos (Flujo de Trabajo)

### A) Agregar tus productos propios (Manuales)
1. Abre el archivo [data/productos_manuales.json](file:///C:/Users/PC/Desktop/GITHUB/data/productos_manuales.json) en tu editor.
2. Añade tus artículos respetando el formato (puedes copiar y pegar el bloque de ejemplo para agregar más):
   ```json
   {
     "name": "Nombre de tu producto o servicio",
     "original_price": 450.00,
     "price_with_margin": 540.00,
     "image": "images/tu-foto.jpeg", 
     "category": "Periféricos",
     "specs": "Descripción corta o especificaciones"
   }
   ```
3. Guarda el archivo.

### B) Modificar precios del proveedor (Socio Vip)
Si quieres fijar un precio personalizado para un producto de Visão Vip:
1. Abre [data/precios_manuales.json](file:///C:/Users/PC/Desktop/GITHUB/data/precios_manuales.json).
2. Escribe una palabra clave o parte del nombre del producto y su precio final:
   ```json
   {
     "descripciones_manuales": {
       "Precision 7780": 4200.00,
       "Radeon RX580": 110.00
     }
   }
   ```
   *Nota: Gracias al nuevo buscador flexible, el scraper aplicará el precio `4200.00` a cualquier producto del proveedor que contenga "Precision 7780" en su nombre, sin importar mayúsculas o espacios.*

### C) Aplicar los cambios en Internet
Gracias a la nueva automatización, solo debes subir tus archivos editados a GitHub. La web se encargará del resto:
```bash
git add .
git commit -m "Edicion de productos y precios manuales"
git push origin main
```
Al hacer `git push`, GitHub Actions detectará la modificación de tus archivos de datos, ejecutará el script `scraper.py` en la nube, y actualizará la tienda online automáticamente.

---

## 🖼️ 3. Cambiar Imágenes y Logotipo

- **Logo**: Reemplaza el archivo `images/logo.jpeg` con tu nueva imagen en formato JPEG con el nombre exacto `logo.jpeg`.
- **Fotos de productos manuales**: Pega la imagen en la carpeta `images/` (ej. `mi-antena.jpeg`) y colócala en el campo `"image"` de tu producto manual en el JSON: `"images/mi-antena.jpeg"`.
- **Subir cambios**: Guarda y ejecuta `git push origin main` para subirlas a internet.
