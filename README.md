# RMP — Registro Mensual de Producción
### Gaspro Honduras S.A. · Planta AED San Pedro Sula

App web para que el operador de llenado registre la producción diaria de **Oxígeno Líquido (LOX)** y **Nitrógeno Líquido (LIN)**, con envío automático a Google Sheets.

---

## Archivos del proyecto

```
index.html        ← La app completa (un solo archivo)
apps_script.gs    ← Código para Google Apps Script
README.md         ← Este archivo
```

---

## Paso 1 — Subir a GitHub Pages

1. Crea un repositorio nuevo en GitHub (ej. `gaspro-rmp`).
2. Sube los archivos `index.html` y `README.md`.
3. Ve a **Settings → Pages**.
4. En **Source**, selecciona `Deploy from a branch` → rama `main` → carpeta `/ (root)`.
5. Haz clic en **Save**.
6. En unos minutos la app estará disponible en:
   ```
   https://TU_USUARIO.github.io/gaspro-rmp/
   ```

---

## Paso 2 — Configurar Google Sheets

### 2.1 Crear el Google Sheet

1. Crea un nuevo Google Sheet en tu Google Drive.
2. Renombra las pestañas (hojas) con estos nombres **exactos**:
   - `LOX`
   - `LIN`
   - `DESCARGAS`
3. En la fila 1 de cada pestaña agrega estos encabezados:

   **LOX y LIN** (mismos encabezados en ambas):
   | Timestamp | Fecha | Gas | Sección | Tipo_Cilindro | Cantidad |

   **DESCARGAS:**
   | Timestamp | Fecha | Gas | Descarga_lbs | Declarado_lbs | Lugar |

   > ⚠ Si dejas las hojas vacías, el script las llena automáticamente la primera vez.

### 2.2 Instalar el Apps Script

1. En tu Google Sheet, ve a **Extensiones → Apps Script**.
2. Borra el código que aparece por defecto.
3. Copia y pega todo el contenido del archivo `apps_script.gs`.
4. Haz clic en el ícono de **Guardar** (💾).

### 2.3 Publicar como Web App

1. Haz clic en **Implementar → Nueva implementación**.
2. Haz clic en el ícono de engranaje ⚙ junto a "Tipo" y selecciona **Aplicación web**.
3. Configura:
   - **Descripción:** RMP Gaspro (opcional)
   - **Ejecutar como:** Yo (`tu@email.com`)
   - **Quién tiene acceso:** Cualquier usuario
4. Haz clic en **Implementar**.
5. Google pedirá que autorices permisos → acepta todo.
6. **Copia la URL** que termina en `/exec`. Se ve así:
   ```
   https://script.google.com/macros/s/AKfycbxXXXXXXX.../exec
   ```

---

## Paso 3 — Conectar la app con Google Sheets

1. Abre la app en el navegador (`https://TU_USUARIO.github.io/gaspro-rmp/`).
2. Ve a la pestaña **⚙ Configuración**.
3. Pega la URL del Apps Script en el campo correspondiente.
4. Haz clic en **Guardar URL**.

La URL se guarda localmente en el navegador del operador.

---

## Uso diario

1. El operador abre la app desde el celular o tablet.
2. Selecciona la pestaña **O₂ Oxígeno** o **N₂ Nitrógeno**.
3. Elige la **fecha** del día.
4. Ingresa las cantidades de cada tipo de cilindro.
5. Presiona **↑ Enviar LOX/LIN a Google Sheets**.
6. Para descargas de camión-cisterna, usa la pestaña **Descargas**.

---

## Estructura de datos en Google Sheets

### Pestaña LOX / LIN
Cada fila representa **un tipo de cilindro** del día:

| Timestamp | Fecha | Gas | Sección | Tipo_Cilindro | Cantidad |
|---|---|---|---|---|---|
| 2026-06-01T08:30:00Z | 2026-06-01 | LOX | ENVASES INDUSTRIALES | 250M | 120 |
| 2026-06-01T08:30:00Z | 2026-06-01 | LOX | ENVASES MEDICINALES | 300PC | 45 |

### Pestaña DESCARGAS

| Timestamp | Fecha | Gas | Descarga_lbs | Declarado_lbs | Lugar |
|---|---|---|---|---|---|
| 2026-06-01T10:00:00Z | 2026-06-01 | LOX | 21500 | 21341 | AED |

---

## Notas técnicas

- La app funciona con un solo archivo HTML — no requiere Node.js, npm ni build.
- Usa React 18 cargado desde CDN (esm.sh).
- La URL del Apps Script se guarda en `localStorage` del navegador.
- Compatible con Chrome, Firefox, Safari y Edge modernos.
- Optimizada para uso en celular/tablet.
