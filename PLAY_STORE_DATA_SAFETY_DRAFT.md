# NeXA ODVIA — Data Safety draft

Estado: borrador interno. No completar Play Console con estas respuestas hasta contrastarlas con la APK release exacta y con NeXA Core.

## Principio
Google Play Data Safety debe reflejar lo que la versión enviada realmente recopila, comparte, transmite y protege. No copiar respuestas genéricas.

## Datos que NeXA puede tratar según el producto actual/proyectado

### Datos personales / contacto
Posibles ejemplos:
- nombre visible del paciente;
- teléfono;
- identificadores del paciente usados por el consultorio;
- datos del usuario/consultorio cuando existan cuentas o licencia.

### Salud / información clínica
Posibles ejemplos:
- historia o notas odontológicas;
- diagnósticos;
- tratamientos;
- fotografías clínicas;
- estudios o documentos clínicos que Chair pueda mostrar en el futuro.

### Fotos
- foto de identificación/perfil;
- fotografías clínicas cuando la función correspondiente exista en la build enviada.

### Mensajes
- texto de recordatorios configurados por el consultorio para WhatsApp.

### Calendario
- datos de eventos de Google Calendar cuando el usuario conecta OAuth.

### Identificadores y datos técnicos
- installation/device ID generado por NeXA;
- versión de app;
- modelo/fabricante con fines de diagnóstico/identificación del dispositivo;
- perfiles/capacidades concedidas;
- estado de conexión.

## Preguntas que deben resolverse con la build release
Para cada tipo de dato:
1. ¿La APK lo recibe?
2. ¿Se queda solo en el dispositivo?
3. ¿Sale del dispositivo hacia Core local?
4. ¿Sale a un servidor/controlador operado por NeXA?
5. ¿Se transmite a Google, WhatsApp u otro tercero por una función iniciada por el usuario?
6. ¿Se almacena?
7. ¿Cuánto tiempo?
8. ¿El usuario puede pedir o ejecutar eliminación?
9. ¿Está cifrado en tránsito?
10. ¿Es necesario para la función principal u opcional?

## Arquitectura que debe reflejarse correctamente
- NeXA Core es la fuente principal de datos clínicos.
- Bridge y Chair son componentes complementarios autorizados.
- No asumir que datos enviados a un Core local del propio consultorio equivalen automáticamente a datos recopilados por el desarrollador; evaluar usando las definiciones vigentes de Play Console.
- Datos que llegan a Google Calendar o WhatsApp deben analizarse también como transferencia a servicios de terceros iniciada por una función del usuario.

## Puntos de riesgo conocidos antes de Play
- DataStore de recordatorios puede contener nombre visible, teléfono y mensaje.
- Estado fotográfico puede contener referencias/tokens y archivos temporales.
- Debe cerrarse el hotfix de limpieza fotográfica antes de release.
- Debe revisarse cifrado/protección adicional de persistencia sensible.
- Deben revisarse logs y backups en build release.

## Google Calendar
La declaración debe ser coherente con la Política de Privacidad ya aprobada para OAuth:
- integración opcional;
- datos usados para mostrar/crear/actualizar/sincronizar eventos;
- sin publicidad, venta o entrenamiento generalizado de IA;
- usuario puede revocar acceso.

## WhatsApp / AccessibilityService
La Data Safety final debe describir cualquier dato que el servicio realmente procese, sin minimizar u ocultar acceso relevante.

## Checklist final
- [ ] Inventario real de datos de APK release.
- [ ] Inventario de transmisiones de red.
- [ ] Inventario de almacenamiento local.
- [ ] Inventario de SDKs de terceros.
- [ ] Revisión de permisos del manifest.
- [ ] Revisión de política pública.
- [ ] Revisión de eliminación/retención.
- [ ] Respuestas de Play Console coinciden con la build.
