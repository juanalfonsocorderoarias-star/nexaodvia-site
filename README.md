# nexaodvia-site

Sitio público de NeXA ODVIA (`nexaodvia.com`) y documentación interna para mantener coherencia entre Google OAuth, Google Play y las políticas públicas del producto.

## Páginas públicas
- `/` — presentación de NeXA ODVIA.
- `/privacy/` — Política de Privacidad.
- `/terms/` — Términos de uso.
- `/accessibility/` — divulgación sobre Android AccessibilityService.
- `/support/` — soporte.

## Documentos internos
- `OAUTH_CHANGE_GUARD.md` — evita cambios que puedan obligar a re-verificar OAuth sin evaluación previa.
- `GOOGLE_OAUTH_AUDIT_CHECKLIST.md` — auditoría no destructiva de Google Cloud OAuth.
- `PLAY_STORE_COMPLIANCE_GATE.md` — gate completo previo a Google Play.
- `PLAY_STORE_RELEASE_BASELINE.md` — estado técnico Android conocido.
- `PLAY_STORE_ACCESSIBILITY_DECLARATION_DRAFT.md` — borrador de declaración de AccessibilityService.
- `PLAY_STORE_DATA_SAFETY_DRAFT.md` — preparación de Data Safety.
- `PLAY_STORE_HEALTH_DECLARATION_DRAFT.md` — preparación de Health apps declaration.
- `PLAY_STORE_LISTING_DRAFT.md` — borrador de Store Listing.

## Regla OAuth
La preparación de Google Play no debe modificar por defecto la configuración OAuth ya verificada. Cualquier cambio de nombre, logo, URLs, dominios, redirect URIs o scopes se evalúa primero con `OAUTH_CHANGE_GUARD.md`.
