# SIGEM — Sistema Integral de Gestión de Mesas de Examen

Aplicación web del sistema de gestión de mesas de examen.

## Archivos principales

- `index.html`: aplicación web actual. En esta versión los datos se guardan en el navegador mediante `localStorage`.
- `sistema_examenes.sql`: dump histórico de MariaDB/MySQL.
- `supabase/`: documentación y snapshot estructural del esquema Supabase activo.

## Supabase

El proyecto Supabase asociado es `arielito` (ref: `rommwpcuzwlbwogjqkjg`).

Consultar [supabase/README.md](supabase/README.md) para el estado del proyecto, las tablas, las migraciones registradas y las precauciones de seguridad. El archivo [supabase/schema.sql](supabase/schema.sql) es un snapshot de referencia sin filas ni credenciales; no es una migración para ejecutar sobre producción.

## Estado de integración

La aplicación `index.html` todavía no está conectada a Supabase: sigue utilizando `localStorage`. Este commit incorpora documentación y estructura de base de datos, no modifica el inicio de sesión ni sincroniza datos.

## Seguridad

- No subir `.env`, tokens, service-role keys, contraseñas, DNI ni exportaciones con datos reales.
- La clave publishable puede utilizarse en un cliente web; la service-role key nunca debe exponerse en el navegador.
- Mantener RLS habilitado y probar las políticas con cada cambio de esquema o autenticación.
