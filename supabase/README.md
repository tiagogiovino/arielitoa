# Supabase – SIGEM

Proyecto Supabase vinculado: **arielito**  
Project ref: `rommwpcuzwlbwogjqkjg`

## Contenido de esta carpeta

- `schema.sql`: snapshot estructural de las tablas y relaciones de `public`, sin datos personales ni credenciales. Es de referencia; no ejecutarlo sobre la base de producción.
- `README.md`: documentación de la configuración y del estado conocido del proyecto.

## Estado comprobado el 2026-11-11

El proyecto activo contiene las tablas `aula`, `materia`, `docente`, `alumno`, `preceptor`, `acceso_docente`, `acceso_preceptor`, `mesa`, `correlativa`, `inscripcion`, `nota`, `comprobante`, `registro_ingresos_alumnos`, `usuarios`, `validacion_ingreso` y `sigem_perfiles`.

RLS está habilitado en todas las tablas públicas. Hay políticas por rol para alumnos, docentes y preceptores. Las tablas heredadas `usuarios`, `acceso_docente` y `acceso_preceptor` tienen políticas de bloqueo para impedir el acceso directo a las credenciales antiguas. La columna antigua de contraseña de `preceptor` fue eliminada.

El esquema privado `private` contiene funciones auxiliares de autorización:
- `private.sigem_rol()`
- `private.sigem_id_alumno()`
- `private.sigem_id_docente()`
- `private.sigem_id_preceptor()`

También existe el trigger `trg_validar_correlativas` sobre `inscripcion`, que valida las materias correlativas antes de inscribir.

## Historial de migraciones aplicado en Supabase

El proyecto informa estas migraciones como aplicadas:

1. `20261111181345_sigem_initial_schema_and_seed`
2. `20261111181407_sigem_remove_legacy_plaintext_preceptor_passwords`
3. `20261111181643_sigem_auth_profiles_and_role_rls`

La API de administración de Supabase devuelve las versiones y nombres, pero no el contenido SQL original de esos archivos. Por eso no se inventan archivos de migración con esos nombres: el snapshot de `schema.sql` documenta la estructura que está activa.

## Configuración local

1. Instalar Supabase CLI y autenticarla.
2. Enlazar el directorio local con el proyecto usando el project ref indicado arriba.
3. Recuperar el esquema real y las migraciones con Supabase CLI antes de generar migraciones nuevas.
4. Revisar los cambios y probarlos en un entorno de desarrollo antes de aplicarlos a producción.

No guardar archivos `.env`, tokens de acceso, service-role keys, contraseñas, DNI ni exportaciones con datos reales en Git.

## Autenticación y aplicación web

El repositorio todavía contiene una versión web que usa `localStorage`; subir la documentación de Supabase no conecta automáticamente la aplicación a la base. La integración de inicio de sesión y consultas debe hacerse como un cambio separado, con la clave publishable en configuración pública y nunca con la service-role key en el navegador.

**Importante:** el esquema de autenticación nombre completo + DNI como contraseña inicial no se da por implementado. No se deben crear usuarios ni publicar DNI como contraseñas desde este repositorio.
