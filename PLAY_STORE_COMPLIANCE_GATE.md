# NeXA ODVIA — PLAY STORE COMPLIANCE GATE

No publicar NeXA Bridge/Chair en Google Play hasta completar y documentar este control.

## Identidad y distribución
- [ ] Definir `applicationId` de producción.
- [ ] Configurar firma release y Play App Signing.
- [ ] Confirmar target SDK exigido por Google Play en la fecha de envío.
- [ ] Generar y validar AAB release.
- [ ] Mantener canal de pruebas internas antes de producción.

## AccessibilityService
- [ ] No declarar `isAccessibilityTool=true` salvo que el propósito principal de la aplicación cambie realmente a una herramienta de accesibilidad.
- [ ] Mostrar divulgación destacada dentro de la app antes de habilitar el servicio.
- [ ] Obtener consentimiento afirmativo del usuario.
- [ ] Limitar la automatización a reglas determinísticas configuradas por el usuario.
- [ ] Diferenciar WhatsApp Personal y WhatsApp Business.
- [ ] Fail-safe: si la interfaz no se reconoce de forma segura, detener automático y pasar a flujo supervisado.
- [ ] Completar AccessibilityService declaration en Play Console.
- [ ] Preparar video de demostración del uso real.

## Privacidad y salud
- [ ] Revisar Data Safety contra el comportamiento real de la APK y Core.
- [ ] Completar Health apps declaration si corresponde por las funciones clínicas.
- [ ] Confirmar que Política de Privacidad pública coincide con el producto final.
- [ ] Confirmar eliminación/limpieza de datos temporales Bridge/Chair.
- [ ] Revisar logs, backups, temporales y almacenamiento local.

## Google OAuth
- [ ] No cambiar nombre, logo, URLs, dominios, redirect URIs o scopes sin revisar `OAUTH_CHANGE_GUARD.md`.
- [ ] Confirmar que los scopes de Google Calendar siguen siendo los ya aprobados y mínimos necesarios.
- [ ] Mantener la misma URL pública de Política de Privacidad aprobada.

## Estado
Pendiente de ejecución antes del primer envío a Google Play.
