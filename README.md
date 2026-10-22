# Orquestador hospitalario directo

Servicio Flask de solo lectura. Con un mismo identificador consulta primero Pacientes y después Laboratorio, y devuelve un JSON consolidado. No modifica datos.

## Variables de entorno

- `PACIENTES_URL`: URL base del servicio de pacientes, por ejemplo `https://servicio-pacientes.onrender.com`. Sin la ruta `/pacientes/1`. Si trae barra final, se elimina.
- `LABORATORIO_URL`: URL base del servicio de laboratorio, del mismo modo, sin `/laboratorio/1`.
- `HTTP_TIMEOUT`: segundos de espera de cada llamada. Si no se define, vale `20`.

## Render

- **Build Command:** `pip install -r requirements.txt`
- **Start Command:** `gunicorn app:app`

En local, `python app.py` escucha en `0.0.0.0` y en el puerto de `PORT` (por defecto `5000`).

## Endpoints

- `GET /` — nombre del servicio y la ruta de atención.
- `GET /atencion/<id>` — `id` entero positivo. Llama a `{PACIENTES_URL}/pacientes/<id>` y luego a `{LABORATORIO_URL}/laboratorio/<id>`.

En Hoppscotch prueba `GET /` y `GET /atencion/1` con un id que exista en ambos servicios. Un id inexistente responde con error JSON e indica el servicio (`pacientes` o `laboratorio`).
