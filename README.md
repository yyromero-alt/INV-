# WMS Control por Serial

Aplicación web para controlar ingresos, ubicación, reubicación, salidas individuales y salidas múltiples por serial, usando Google Sheets como base de datos compartida.

## Archivos

- `index.html`: aplicación web completa.
- `Code.gs`: backend Google Apps Script.
- `plantilla_ingreso_masivo.csv`: plantilla para carga masiva de ingresos.

## Configuración del HTML

Abra `index.html` y busque:

```javascript
const API_URL='PEGAR_AQUI_URL_DE_APPS_SCRIPT';
```

Reemplácelo por la URL de su implementación web de Apps Script:

```javascript
const API_URL='https://script.google.com/macros/s/SU_ID/exec';
```

No publique claves privadas ni tokens en GitHub.

## Configuración de Google Apps Script

1. Cree o abra el Google Sheet asociado.
2. Abra **Extensiones → Apps Script**.
3. Pegue el contenido de `Code.gs`.
4. Verifique el valor de `SPREADSHEET_ID`.
5. Ejecute `crearHoja` una vez y autorice los permisos.
6. Publique como **Aplicación web**.
7. Configure **Ejecutar como: Yo**.
8. Configure el acceso según sus usuarios.
9. Copie la URL `/exec` y colóquela en `index.html`.
10. En cada modificación del backend, publique una nueva versión desde **Administrar implementaciones**.

## Funciones incluidas

- Ingreso manual.
- Carga masiva CSV/plano.
- Búsqueda por serial, referencia o descripción.
- Reubicación de productos activos.
- Salida individual.
- Salida múltiple con un mismo documento y destino.
- Inventario filtrable.
- Historial de salidas.
- Exportación a Excel.

## Publicar en GitHub Pages

1. Cree un repositorio, preferiblemente privado si el proyecto contiene información interna.
2. Suba `index.html`, `Code.gs`, `plantilla_ingreso_masivo.csv` y este README.
3. En GitHub abra **Settings → Pages**.
4. Seleccione la rama principal y la carpeta `/root`.
5. Guarde y espere la URL de GitHub Pages.

GitHub Pages publica el HTML, pero no ejecuta `Code.gs`; el Apps Script debe permanecer publicado como aplicación web independiente.

## Formato de carga masiva

El archivo CSV debe utilizar exactamente estos encabezados:

```csv
Serial,Referencia,Descripcion,Cantidad,Zona,Pasillo,Nivel,Observaciones
```

Los seriales deben conservarse como texto, especialmente si son largos o empiezan por cero. En Excel, importe la columna Serial como **Texto** para evitar que se convierta en notación científica o pierda ceros iniciales.

## Seguridad

Si el repositorio es público, no incluya IDs sensibles, claves, tokens ni datos reales de inventario. Para uso empresarial, restrinja el acceso del Apps Script a usuarios autorizados de Google Workspace y considere mantener el repositorio privado.
