# Fronteras comerciales en falla o hurto

Descarga cada día la publicación de XM de fronteras comerciales en falla o hurto
(Resolución CREG 038 de 2014), la guarda en Supabase (PostgreSQL) y la analiza en notebooks.

El esquema SQL base fue compartido por Juan Camilo Jaramillo Tascón.

## Contenido

| Archivo | Qué hace |
| --- | --- |
| `pipeline/schema.sql` | Crea las tablas y vistas en el esquema `fronteras` |
| `pipeline/cargar.py` | Valida un Excel y lo carga en una sola transacción |
| `pipeline/descargar.py` | Revisa XM, descarga lo que falta y lo carga |
| `pipeline/ejecutar.bat` | Corrida diaria para el Programador de tareas de Windows |
| `analisis_falla_hurto.ipynb` | Análisis de las fallas diarias, leído desde Supabase |
| `fronteras.ipynb` | Análisis de las fronteras canceladas por acumulación de fallas |

## Cómo usarlo

```
cd pipeline
python -m venv .venv
.venv\Scripts\pip install -r requirements.txt
copy .env.example .env      # y pega la cadena de conexión de Supabase
.venv\Scripts\python cargar.py --crear-esquema
.venv\Scripts\python descargar.py --desde 2026-10-01
```

`descargar.py` usa la API pública de la biblioteca de archivos de la página de XM. XM no la
documenta para uso automático, así que puede cambiar sin aviso.

El archivo `.env` con la contraseña nunca se sube al repositorio.
