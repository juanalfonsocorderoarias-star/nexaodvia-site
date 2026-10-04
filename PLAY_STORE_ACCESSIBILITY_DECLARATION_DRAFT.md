# NeXA ODVIA — AccessibilityService declaration draft

Estado: borrador interno para Play Console. No enviar hasta contrastarlo con la APK release exacta.

## Propósito declarado
NeXA Bridge utiliza Android AccessibilityService únicamente para asistir una secuencia limitada y determinística de recordatorios mediante WhatsApp Personal o WhatsApp Business, configurada previamente por el usuario del consultorio.

NeXA ODVIA no es una herramienta cuyo propósito principal sea asistir a personas con discapacidad y, por tanto, no debe marcarse `isAccessibilityTool=true` mientras su finalidad principal siga siendo la gestión odontológica.

## Flujo que debe mostrar el video de Play Console
1. Usuario abre NeXA Bridge.
2. Usuario entra voluntariamente a la función de recordatorios.
3. Se muestra una divulgación destacada separada que explica por qué se necesita AccessibilityService.
4. Usuario acepta expresamente.
5. Android abre la configuración de accesibilidad para que el propio usuario habilite el servicio.
6. Usuario inicia o deja preparado un flujo de recordatorio configurado previamente.
7. NeXA abre la conversación/flujo correspondiente en WhatsApp Personal o Business.
8. El servicio verifica el contexto de interfaz necesario.
9. Ejecuta únicamente la acción determinística prevista.
10. Si la interfaz no coincide con un estado conocido, la automatización se detiene y exige flujo supervisado.

## Texto base para divulgación destacada dentro de la app
**Uso del servicio de accesibilidad**

NeXA Bridge puede usar el servicio de accesibilidad de Android para completar secuencias de recordatorios por WhatsApp que tú hayas configurado previamente. Durante una tarea activa, NeXA puede leer elementos de la interfaz de WhatsApp necesarios para reconocer el compositor, verificar el mensaje esperado y accionar el control correspondiente.

NeXA no utiliza este acceso para navegar libremente por otras aplicaciones, inventar destinatarios o mensajes, ni tomar decisiones autónomas fuera de las reglas configuradas por el usuario. Si la interfaz no puede verificarse de forma segura, el envío automático se detiene.

Puedes desactivar este permiso en cualquier momento desde la configuración de accesibilidad de Android.

Botones sugeridos:
- `Continuar a ajustes de accesibilidad`
- `Ahora no`

No utilizar un botón ambiguo como `Aceptar` sin contexto.

## Casos de uso que deben declararse
- Reconocer el compositor de WhatsApp durante un flujo de recordatorio iniciado/configurado por el usuario.
- Verificar que el texto esperado esté presente antes de una acción.
- Localizar un control relevante del flujo compatible.
- Ejecutar una acción determinística previamente definida.
- Detectar que la interfaz ya no es compatible y detener el automático.

## Casos de uso que NO deben existir
- Navegación general por el teléfono.
- Lectura de otras aplicaciones sin relación con el flujo declarado.
- Generación autónoma de destinatarios.
- Generación autónoma de decisiones clínicas o administrativas.
- Automatización basada en coordenadas ciegas como mecanismo principal.
- Clics si no se puede validar el contexto.
- Declarar falsamente que NeXA es una herramienta de accesibilidad para discapacidad.

## WhatsApp Personal vs Business
La app debe identificar qué paquete/variante está activa y aplicar compatibilidad específica. Una actualización de WhatsApp que cambie la estructura accesible debe poder desactivar el modo automático hasta ser validada.

## Revisión antes de enviar
- [ ] La implementación real coincide exactamente con esta descripción.
- [ ] La divulgación aparece antes de pedir habilitar AccessibilityService.
- [ ] Existe consentimiento afirmativo.
- [ ] Existe forma de desactivar la función.
- [ ] El video corresponde a la misma build enviada.
- [ ] El manifiesto no declara `isAccessibilityTool=true`.
- [ ] La política pública `/accessibility/` coincide con el comportamiento real.
- [ ] La Privacy Policy describe el uso.
- [ ] Se actualiza el formulario de Play si cambia el uso.
