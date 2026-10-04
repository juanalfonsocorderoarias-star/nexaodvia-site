# NeXA ODVIA — OAuth Change Guard

Estado base: Google OAuth ya autorizado/verificado para la configuración actualmente publicada.

## Regla principal
No cambiar en Google Cloud Console sin una revisión previa:

- nombre de la aplicación;
- logo/icono de la pantalla de consentimiento;
- homepage configurada;
- URL de Política de Privacidad;
- URL de Términos si está declarada;
- dominios autorizados;
- redirect URIs/orígenes autorizados;
- scopes sensibles o restringidos solicitados.

Google indica que cambiar detalles de branding como logo, nombre, homepage, Privacy Policy URI o dominios autorizados crea un estado de **Draft Branding** que debe volver a verificarse/publicarse antes de sustituir el branding ya publicado.

## Cambios web que no tocan la configuración OAuth
Se puede mantener actualizado el contenido de las páginas existentes en `nexaodvia.com` siempre que:

- no se modifique la URL configurada en OAuth;
- el contenido siga representando correctamente la app;
- no se contradiga el uso real de datos de Google;
- no se amplíen los scopes en el código;
- se mantenga la información exigida por Google API Services User Data Policy / Limited Use.

Actualizar el texto servido por una URL ya configurada no equivale por sí mismo a editar el campo de branding en Google Cloud. Aun así, el texto publicado debe continuar siendo preciso y coherente con el producto.

La URL OAuth de privacidad debe seguir siendo la misma página pública que enlaza la homepage.

## Baseline que debe conservarse
- Dominio: `nexaodvia.com`
- Homepage: conservar la URL ya aprobada en Google Cloud.
- Política de privacidad: conservar la URL ya aprobada en Google Cloud.
- Google Calendar: uso opcional autorizado por OAuth.
- No usar datos de Google para publicidad, venta de datos, scoring crediticio o entrenamiento de modelos de IA generalizados.
- No añadir scopes de Google para funciones de Bridge, Chair, WhatsApp o Google Play que no los necesitan.

## Preparar Google Play NO exige cambiar OAuth
El alta de la app Android en Play Console debe tratarse como un flujo separado. Por sí sola no justifica cambiar:
- OAuth app name;
- logo OAuth;
- homepage OAuth;
- privacy URI;
- authorized domains;
- redirect URIs;
- scopes de Google Calendar.

Si Play Store necesita mostrar una marca, descripción o recursos gráficos, primero se intenta mantenerlos coherentes con la identidad OAuth ya aprobada sin editar OAuth.

## Antes de cualquier cambio futuro en Google Cloud
1. Revisar la configuración publicada en OAuth Branding y Data Access.
2. Comparar scopes actuales contra cualquier scope nuevo propuesto.
3. Si solo cambia contenido legal en la misma URL, mantener los campos OAuth intactos.
4. Si cambia nombre, logo, URL, dominio, redirect URI o scopes, evaluar re-verificación antes de guardar/publicar el cambio.
5. No desplegar cambios OAuth destructivos durante una verificación en curso.
6. No pulsar `Publish branding` ni iniciar una nueva verificación sin comprobar primero el impacto.

## Auditoría no destructiva
Usar `GOOGLE_OAUTH_AUDIT_CHECKLIST.md`. La primera auditoría debe ser solo lectura y registrar el estado publicado actual antes de decidir cualquier cambio.

## Google Play
Este documento no sustituye el `PLAY_STORE_COMPLIANCE_GATE`. AccessibilityService, Data Safety, Health Declaration, firma release, package de producción y target SDK se revisan aparte antes del primer envío a Play.
