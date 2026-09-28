# Bitácora de desarrollo

Proyecto: Sistema de Alerta Temprana para Defensa Civil (sur tucumano)
Materia: Metodología de Sistemas II
Repositorio: [<link al repo en GitHub>](https://github.com/MaxiPalomino02/Alerta-temprana-defensa-civil)

---

## 28/09/2026 - Patrón Observer

**Qué hice:** elegí e implementé el patrón Observer (familia de Comportamiento) para manejar las reacciones que se disparan cuando Defensa Civil emite una alerta.

**Problema identificado:** al emitir una alerta tienen que pasar varias cosas: enviar el email a los suscriptores de cada zona, registrar la auditoría de la emisión y, a futuro, sumar otros canales (SMS, push, Flood Hub API). Si `emitir_alerta()` llama directamente a cada una, la emisión queda mezclada con las reacciones y hay que modificar esa función cada vez que se agrega una nueva. Es el mismo problema de fragilidad que muestra la Unidad 4 con `reservarTurno()`.

**Por qué Observer y no otro:**
- **Strategy:** sirve para elegir un algoritmo entre varios. Acá no se elige una reacción, se disparan varias a la vez.
- **Facade:** simplifica el acceso a varios módulos, pero seguiría llamando a cada reacción una por una, sin desacoplarlas.
- **Command:** encapsula acciones para encolarlas o deshacerlas, y el proyecto no tiene ese requisito.
- **State:** encaja con el ciclo de vida de la alerta (activa/cerrada), pero no resuelve el disparo de reacciones.
- **Observer:** según la matriz de la Unidad 4, "un evento debe disparar múltiples reacciones desacopladas" se resuelve con Observer. Cumple Open/Closed (se agregan observadores sin tocar el servicio) y Single Responsibility (el servicio solo emite la alerta).

**Costo (trade-off):** más clases e indirección, y un flujo menos obvio al leer el código. Se justifica porque ya existen al menos tres reacciones reales (email a suscriptores, registro de auditoría y confirmación de envío). Con una sola reacción habría sido sobreingeniería (YAGNI).

**Implementación:**
- `app/services/eventos.py`: interfaz `ObservadorAlerta` y `PublicadorAlertas` (el sujeto).
- `app/services/observadores.py`: `NotificadorEmailSuscriptores` y `RegistroAuditoria`.
- `app/services/alertas_service.py`: `AlertasService.emitir_alerta()` publica el evento sin conocer a los observadores.
- `tests/test_observer_alertas.py`: tests de notificación múltiple, aislamiento de fallos y desuscripción.

**Evidencia:** <link al commit o PR en GitHub>

