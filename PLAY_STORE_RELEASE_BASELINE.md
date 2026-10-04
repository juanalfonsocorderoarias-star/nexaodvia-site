# NeXA ODVIA — Android release readiness baseline

Fuente: última auditoría Bridge disponible antes de preparar Google Play.
Fecha de referencia: 4 de octubre de 2026.

## Build actual conocido
- `versionName`: `0.7.0-dev`
- `versionCode`: `19`
- `namespace`: `com.nexa.bridge.dev`
- `applicationId`: `com.nexa.bridge.dev`
- `minSdk`: 26
- `targetSdk`: 35
- `compileSdk`: 35
- Java/Kotlin target: 17
- firma: Android Debug
- release signing: no configurada

## Permisos actuales conocidos
- INTERNET
- CAMERA
- POST_NOTIFICATIONS
- permiso interno AndroidX para receptores no exportados

No se observaron permisos amplios de contactos, ubicación, micrófono, SMS, llamadas o almacenamiento general en la build auditada.

## Arquitectura Android conocida
- una sola app/módulo actual;
- perfiles efectivos BRIDGE / CHAIR / combinación;
- capacidades concedidas por Core;
- HTTPS local y pinning;
- identidad ECDSA en Android Keystore;
- WhatsApp Personal/Business con flujo supervisado y automático por AccessibilityService;
- CameraX para QR/fotografía;
- Chair clínico todavía no implementado en la build auditada.

## Bloqueadores de release conocidos
### P0
- limpieza incompleta de fotografías temporales en cancelar/revocar;
- Hub pierde tareas al reiniciar Core;
- falta arbitraje global claim/lease antes de incorporar Chair como segundo ejecutor.

### P1 / hardening
- polling/heartbeat en segundo plano requiere revisión;
- nonces Hub no durables;
- datos sensibles persistidos localmente requieren revisión de protección/cifrado;
- pruebas instrumentadas/físicas de la build actual pendientes.

## Bloqueadores específicos de Google Play
- `targetSdk 35` ya no cumple para un nuevo envío móvil en octubre de 2026; se requiere API 36 o superior.
- `applicationId` actual contiene `.dev` y no debe fijarse en producción sin decisión explícita.
- firma debug no es válida como identidad comercial definitiva.
- AccessibilityService exige declaración, divulgación y consentimiento.
- Data Safety y Health apps declaration deben completarse con la build final.

## Estrategia recomendada
1. Cerrar hotfix P0 fotográfico.
2. Hacer durables las tareas Hub.
3. Implementar arbitraje/ownership antes de Chair ejecutor.
4. Definir identidad Android de producción.
5. Subir target/compile SDK y probar.
6. Configurar firma release / Play App Signing.
7. Generar AAB.
8. Completar declaraciones Play con evidencia de la build.
9. Internal testing.
10. Solo después evaluar distribución más amplia.

## Regla OAuth
Nada de lo anterior requiere por sí mismo cambiar Google OAuth. Mantener separado el trabajo de Play Store de la configuración OAuth ya verificada.
