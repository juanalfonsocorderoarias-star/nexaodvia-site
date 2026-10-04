# NeXA ODVIA — PLAY STORE COMPLIANCE GATE

Estado de preparación: **NO PUBLICAR TODAVÍA**.

Objetivo: usar Google Play como canal de distribución y actualización de la APK compartida NeXA Android (Bridge / Chair / Bridge+Chair), empezando por **Internal testing** y manteniendo producción pública cerrada hasta completar todos los controles.

Fecha de referencia de políticas: **4 de octubre de 2026**.

## 0. Baseline actual conocido
Según la última auditoría técnica de Bridge:
- `versionName`: `0.7.0-dev`
- `versionCode`: `19`
- `applicationId`: `com.nexa.bridge.dev`
- `namespace`: `com.nexa.bridge.dev`
- `minSdk`: 26
- `targetSdk`: 35
- `compileSdk`: 35
- firma actual: Android Debug
- no existe todavía firma release comercial
- no existe todavía `applicationId` de producción

Conclusión: **la APK actual no debe enviarse a Google Play como release final**.

## 1. Identidad y distribución
- [ ] Definir `applicationId` de producción definitivo para la APK compartida NeXA Android.
- [ ] Mantener una sola aplicación con perfiles/capacidades Bridge, Chair o ambos; no duplicar apps salvo decisión arquitectónica futura documentada.
- [ ] Crear keystore/firma release protegida y configurar Play App Signing.
- [ ] Mantener separada la clave de carga de la clave administrada por Play cuando corresponda.
- [ ] Definir política de versionado `versionCode` / `versionName`.
- [ ] Generar y validar un Android App Bundle (`.aab`) release.
- [ ] Publicar primero en **Internal testing**.
- [ ] No pasar a Closed/Open testing ni Production hasta que este gate esté completo.

## 2. Target SDK obligatorio
A partir del 31 de agosto de 2026, las apps nuevas y actualizaciones móviles enviadas a Google Play deben apuntar a **Android 16 / API 36 o superior**.

Estado actual conocido: `targetSdk 35`.

- [ ] Migrar `targetSdk` a **36 o superior** antes del primer envío.
- [ ] Migrar `compileSdk` al nivel compatible requerido.
- [ ] Ejecutar regresión completa después de la migración, especialmente cámara, QR, Keystore, TLS, notificaciones, AccessibilityService y comportamiento en segundo plano.
- [ ] Confirmar que el requisito no haya vuelto a cambiar en la fecha exacta del envío.

## 3. AccessibilityService — BLOQUEO DE PUBLICACIÓN
NeXA ODVIA es software odontológico; **no declarar `isAccessibilityTool=true`** mientras su propósito principal no sea asistir a personas con discapacidad.

Antes de enviar una APK que incluya AccessibilityService:
- [ ] Mantener la automatización limitada a un propósito específico y claramente definido: ejecución de secuencias de recordatorios previamente configuradas por el usuario.
- [ ] Mantener la lógica como automatización **determinística basada en reglas definidas por humanos**.
- [ ] No permitir que el servicio inicie, planifique y ejecute decisiones autónomas por sí mismo.
- [ ] Mostrar una **divulgación destacada, separada y dentro de la app** antes de dirigir al usuario a activar AccessibilityService.
- [ ] La divulgación debe explicar qué acceso se utiliza, por qué se necesita y para qué casos prácticos se utilizará.
- [ ] Obtener consentimiento afirmativo del usuario.
- [ ] Diferenciar WhatsApp Personal y WhatsApp Business.
- [ ] No depender de coordenadas absolutas como mecanismo principal de interacción.
- [ ] Fail-safe: si la interfaz, destinatario, mensaje o control esperado no pueden verificarse, detener automático y pasar a flujo supervisado.
- [ ] Mantener un modo supervisado que no dependa de ejecución automática ciega.
- [ ] Completar el formulario de declaración de AccessibilityService en Play Console.
- [ ] Preparar un video real que muestre la función y la divulgación/consentimiento.
- [ ] Si cambia la forma en que NeXA usa AccessibilityService, actualizar la declaración antes de enviar la nueva versión.

Documento asociado: `PLAY_STORE_ACCESSIBILITY_DECLARATION_DRAFT.md`.

## 4. Privacidad y Data Safety
- [ ] Comparar cada respuesta de Data Safety contra el comportamiento real de la APK release y de NeXA Core.
- [ ] Declarar de forma coherente datos de salud, datos personales, fotos, teléfono/mensajes, identificadores de dispositivo y cualquier dato técnico realmente tratado.
- [ ] No declarar como "no recopilado" un dato que salga del dispositivo o llegue a un servicio controlado por NeXA.
- [ ] Separar claramente datos almacenados exclusivamente en infraestructura del consultorio de datos transmitidos a proveedores externos.
- [ ] Confirmar cifrado en tránsito donde corresponda.
- [ ] Confirmar política de eliminación/retención de temporales Bridge/Chair.
- [ ] Revisar logs, backups Android, DataStore, archivos temporales, outbox y cachés.
- [ ] Mantener pública la Política de Privacidad en `nexaodvia.com` y también accesible desde la app cuando corresponda.

Documento asociado: `PLAY_STORE_DATA_SAFETY_DRAFT.md`.

## 5. Apps de salud / odontología
Google Play exige que las apps de salud o medicina completen la **Health apps declaration** y publiquen una política de privacidad que explique el tratamiento de datos personales y sensibles.

- [ ] Clasificar correctamente la función real de NeXA; no declarar funciones diagnósticas o terapéuticas que la app no realiza.
- [ ] Describir NeXA como software de gestión odontológica / información clínica según las categorías que Play Console muestre en el formulario vigente.
- [ ] Revisar si alguna función futura convierte una parte del producto en funcionalidad médica regulada.
- [ ] Si no existe una función médica regulada, mantener un descargo claro de que NeXA no sustituye criterio, diagnóstico ni decisión clínica profesional.
- [ ] Completar Health apps declaration usando solamente funciones presentes en la versión enviada.

Documento asociado: `PLAY_STORE_HEALTH_DECLARATION_DRAFT.md`.

## 6. Google OAuth — NO ROMPER LO YA VERIFICADO
- [ ] No cambiar nombre, logo, homepage, Privacy Policy URI, Terms URI declarada, dominios autorizados, redirect URIs/orígenes o scopes sin revisar primero `OAUTH_CHANGE_GUARD.md`.
- [ ] Mantener la misma URL pública de Política de Privacidad ya usada por OAuth.
- [ ] Confirmar que los scopes de Google Calendar de la app release sean exactamente los ya aprobados y el mínimo necesario.
- [ ] No añadir scopes nuevos solamente por publicar en Play.
- [ ] La publicación en Google Play y la verificación OAuth se consideran procesos separados: preparar Play no debe modificar Google Cloud OAuth salvo necesidad demostrada.

## 7. Seguridad Android antes del AAB
- [ ] Cerrar P0 de limpieza de fotografías temporales.
- [ ] Revisar cifrado/protección de datos sensibles persistidos en Android.
- [ ] Confirmar limpieza completa al revocar Core/dispositivo.
- [ ] Confirmar que no haya nombres, teléfonos, mensajes, fotos, diagnósticos o tokens sensibles en logs.
- [ ] Mantener backups/transferencia Android desactivados si contienen estado sensible.
- [ ] Revisar exported components, intents, deep links y permisos efectivos del manifest release.
- [ ] Confirmar que Chair no persista historia clínica completa de forma independiente.

## 8. Sistema de tareas / Chair
Antes de habilitar Chair como segundo ejecutor:
- [ ] Persistencia durable de tareas Hub.
- [ ] Rehidratación después de reiniciar Core.
- [ ] Claim / lease / renew / release o mecanismo equivalente de ownership global.
- [ ] Idempotencia global demostrada.
- [ ] Sesiones clínicas Chair con expiración/revocación y limpieza local.

## 9. Store listing
- [ ] Nombre público coherente con la marca OAuth ya verificada.
- [ ] Descripción corta y completa sin promesas clínicas engañosas.
- [ ] Categoría correcta.
- [ ] Email de soporte activo.
- [ ] URL de privacidad activa.
- [ ] Capturas reales de la versión enviada.
- [ ] Icono, feature graphic y recursos finales.
- [ ] No mostrar funciones que todavía no estén en la build enviada.

Documento asociado: `PLAY_STORE_LISTING_DRAFT.md`.

## 10. Pruebas mínimas antes de Internal testing
- [ ] Unit tests y lint release.
- [ ] Pruebas instrumentadas actuales.
- [ ] Samsung/tablet: Bridge + Chair según capacidades concedidas.
- [ ] Teléfono: regresión Bridge.
- [ ] WhatsApp Personal.
- [ ] WhatsApp Business.
- [ ] Versión de WhatsApp conocida/compatible.
- [ ] Interfaz no reconocida => automático se detiene.
- [ ] Cámara/QR/foto.
- [ ] Emparejamiento, revocación y reconexión.
- [ ] Pérdida y recuperación de red local.
- [ ] Actualización sobre una build de prueba anterior usando la misma identidad release.

## 11. Gate final
Solo crear envío a Google Play cuando:
1. todos los puntos P0 estén cerrados;
2. `targetSdk >= 36`;
3. exista identidad/firma release definitiva;
4. Data Safety y Health Declaration coincidan con la build;
5. AccessibilityService tenga divulgación, consentimiento, declaración y video preparados;
6. OAuth no haya sido modificado de forma que fuerce una nueva verificación no completada;
7. la política pública coincida con el producto real.

**Estado actual: PREPARACIÓN — NO ENVIAR A PLAY TODAVÍA.**
