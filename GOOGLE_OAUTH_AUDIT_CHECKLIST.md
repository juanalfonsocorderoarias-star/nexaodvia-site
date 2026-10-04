# NeXA ODVIA — GOOGLE OAUTH AUDIT CHECKLIST

Objetivo: auditar el estado ya aprobado de Google OAuth **sin modificar la configuración publicada**.

## Regla de oro
Durante esta auditoría no pulsar Guardar/Publicar/Verificar ni editar Branding, Audience, Data Access o Clients salvo que exista un problema demostrado y se haya evaluado el impacto sobre la verificación existente.

## 1. Branding — SOLO LECTURA
Registrar exactamente lo que muestra Google Cloud:
- Estado de branding: Published / Verified / equivalente vigente.
- App name.
- Logo.
- User support email.
- Homepage URI.
- Privacy Policy URI.
- Terms of Service URI, si está configurada.
- Authorized domains.
- Developer contact information.

### Baseline que no debe cambiar por preparar Google Play
- Dominio: `nexaodvia.com`.
- Mantener las mismas URLs ya aprobadas para homepage y privacidad.
- Mantener el mismo nombre/logo ya publicado mientras no exista una razón real para re-verificar branding.

## 2. Audience — SOLO LECTURA
Registrar:
- User type / Audience.
- Publishing status.
- Si existen test users.
- Si hay límites o advertencias activas.

No cambiar Audience por el simple hecho de publicar la app Android.

## 3. Data Access — SOLO LECTURA
Registrar todos los scopes declarados actualmente:
- scope URI exacta;
- clasificación actual (non-sensitive / sensitive / restricted);
- justificación registrada;
- estado de verificación.

Comparar luego estos scopes con el código real de NeXA Calendar.

### Regla
No añadir scopes para Chair, Bridge, Play Store, WhatsApp ni AccessibilityService. Esas funciones no justifican ampliar permisos de Google Calendar.

## 4. OAuth Clients — SOLO LECTURA
Para cada cliente:
- tipo de cliente;
- nombre;
- client ID (se puede registrar internamente, nunca publicar secretos);
- redirect URIs;
- JavaScript origins, si aplican;
- cliente usado por producción vs DEV.

### Secretos
- No subir client secrets, tokens OAuth ni credenciales a este repositorio público.
- No copiar secretos a issues, PRs, capturas públicas o documentación web.

## 5. Dominio
Confirmar:
- `nexaodvia.com` sigue siendo dominio autorizado;
- propiedad del dominio verificada en Search Console con una cuenta asociada al proyecto OAuth;
- homepage y privacy policy siguen siendo públicas por HTTPS;
- no hay redirecciones a dominios no autorizados.

## 6. Resultado esperado
La auditoría debe terminar con uno de estos estados:

### A — SIN CAMBIOS
Todo coincide con la configuración aprobada. No se toca Google Cloud.

### B — CAMBIO WEB SEGURO
Solo se actualiza el contenido de páginas públicas manteniendo las mismas URLs y sin cambiar scopes ni branding configurado.

### C — CAMBIO OAUTH REQUIERE EVALUACIÓN
Se detecta necesidad de cambiar nombre, logo, URL, dominio, redirect URI o scopes. No publicar ese cambio hasta evaluar re-verificación.

## 7. Evidencia a conservar
Guardar capturas o notas internas de:
- Branding publicado;
- Data Access/scopes;
- Audience;
- Clients/redirect URIs sin exponer secretos;
- fecha de la revisión.

Estado: pendiente de auditoría visual en Google Cloud Console. La preparación de Google Play puede continuar en paralelo sin modificar OAuth.
