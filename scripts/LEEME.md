# Sincronización automática del stock

Cada par de horas, GitHub descarga los Excel de stock, los lee y actualiza
Supabase. La web no cambia: sigue leyendo de Supabase, pero el dato llega solo.

## Cómo dejar los Excel

Guardar cada archivo en la carpeta de Google Drive compartida, **siempre con el
mismo nombre** (reemplazando el anterior). El enlace de cada archivo no cambia al
reemplazarlo, así que se configura una sola vez.

## Configuración (en GitHub → Settings → Secrets and variables → Actions)

- `SUPABASE_KEY`: la clave **service_role** del proyecto Supabase.
- `FUENTES`: un JSON con el enlace de cada proveedor, por ejemplo:

```json
{
  "gamma": "https://drive.google.com/file/d/AAA/view",
  "lusqtoff": "https://drive.google.com/file/d/BBB/view",
  "omaha": "https://drive.google.com/file/d/CCC/view",
  "kld": "https://drive.google.com/file/d/DDD/view"
}
```

## Resguardos

- Si un archivo trae menos de 10 productos, **no se sube**: se asume que la
  descarga salió mal y se deja el stock anterior.
- Cada proveedor se actualiza por separado: si uno falla, los otros siguen.
- Se puede correr a mano desde la pestaña Actions, botón "Run workflow".
