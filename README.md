# Repositorio Público - Witec

Repositorio con los documentos públicos (PDF y HTML) que Witec publica para sus clientes y usuarios, con control de versiones vía git.

**Sitio publicado:** https://repositorio.witec.id/
**Repo de GitHub:** https://github.com/digiyoid/repositorio-publico-firmoyo

## Cómo está armado

- El sitio se publica con **GitHub Pages**, a partir de la rama `main` (carpeta raíz `/`). Cada `git push` a `main` actualiza el sitio en 1-2 minutos.
- `index.html` es la página principal: lista los documentos agrupados por sección, con el estilo visual de witec.id (colores, tipografías Arimo/DM Sans).
- `CNAME` contiene el dominio personalizado (`repositorio.witec.id`). No lo borres salvo que quieras desvincular el dominio.
- El dominio personalizado apunta por un registro **CNAME en Route 53** (`repositorio` → `digiyoid.github.io`) de la zona `witec.id`.

## Estructura de carpetas

Cada documento vive en su propia carpeta (nombres en minúsculas, sin espacios ni tildes, para que las URLs sean estables):

- `politica-de-privacidad/` — Política de Privacidad
- `declaracion-de-practicas-de-certificacion/` — Declaración de Prácticas de Certificación (DPC)
- `contrato-prestacion-servicios-tipo-F3/` — Contrato de Prestación de Servicios tipo F3

## Cómo agregar o actualizar un documento

1. Colocá el archivo (PDF o HTML) dentro de la carpeta correspondiente (o creá una carpeta nueva con un nombre en minúsculas, sin espacios/tildes/caracteres especiales — eso evita problemas de encoding en las URLs).
2. Actualizá el link en `index.html` dentro del `doc-group` correspondiente, apuntando al nombre real del archivo.
3. Si es una sección nueva, copiá la estructura de un `doc-group` existente (icono, nombre, descripción corta de 1-2 líneas sobre qué define/cubre el documento).
4. Hacé commit y push a `main`.

## Dominio personalizado y HTTPS

- El certificado HTTPS lo emite y renueva GitHub automáticamente (Let's Encrypt). No hace falta hacer nada manualmente en condiciones normales.
- Si en algún momento el navegador muestra un error de certificado al entrar a `https://repositorio.witec.id/` (no es que "expiró": generalmente significa que GitHub no terminó de emitir el certificado para el dominio), la forma de resolverlo es:
  1. En GitHub: `Settings → Pages`, quitar el dominio personalizado (o vía API: `PUT /repos/digiyoid/repositorio-publico-firmoyo/pages` con `{"cname": null}`).
  2. Esperar unos segundos y volver a cargarlo (`{"cname": "repositorio.witec.id"}`).
  3. Esperar 1-2 minutos y confirmar que `https_certificate.state` sea `"approved"` (`GET /repos/digiyoid/repositorio-publico-firmoyo/pages`).
  4. Asegurarse que `https_enforced` esté en `true`.
- El registro DNS (Route 53) no debería necesitar tocarse salvo que cambie el repo o la organización de GitHub.

## Convenciones

- Nombres de archivo y carpetas: minúsculas, con guiones, sin tildes ni caracteres especiales (evita problemas de encoding de URL, sobre todo con archivos que vienen de macOS).
- Cada sección del index lleva un subtítulo corto que resume qué define el documento (no un genérico "PDF").
