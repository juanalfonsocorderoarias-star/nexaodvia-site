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

Cambios en estos elementos pueden requerir nueva verificación de marca o de scopes.

## Cambios web que normalmente son seguros
Se puede mantener actualizado el contenido de las páginas existentes en `nexaodvia.com` siempre que:

- no cambie la URL configurada en OAuth;
- no se contradiga el uso real de datos de Google;
- no se amplíen los scopes en el código;
- se mantenga la información exigida por Google API Services User Data Policy / Limited Use.

La URL OAuth de privacidad debe seguir siendo la misma página pública que enlaza la homepage.

## Baseline que debe conservarse
- Dominio: `nexaodvia.com`
- Homepage: conservar la URL ya aprobada en Google Cloud.
- Política de privacidad: conservar la URL ya aprobada en Google Cloud.
- Google Calendar: uso opcional autorizado por OAuth.
- No usar datos de Google para publicidad, venta de datos, scoring crediticio o entrenamiento de modelos de IA generalizados.

## Antes de cualquier cambio futuro
1. Revisar la configuración publicada en Google Cloud OAuth Branding y Data Access.
2. Comparar scopes actuales contra los nuevos.
3. Si solo cambia contenido legal en la misma URL, mantener las rutas OAuth intactas.
4. Si cambia nombre, logo, URL, dominio, redirect URI o scopes, evaluar re-verificación antes de publicar el cambio.
5. No desplegar cambios OAuth destructivos durante una verificación en curso.

## Google Play
Este documento no sustituye el `PLAY STORE COMPLIANCE GATE`. AccessibilityService, Data Safety, Health Declaration, firma release, package de producción y target SDK se revisan aparte antes del primer envío a Play.
