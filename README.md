# Concesionaria IA - Gestión de Leads de Compra, Venta y Permuta

## Descripción del proyecto

Este proyecto consiste en un ecosistema de automatización con IA para una concesionaria de autos.

El objetivo es recibir consultas comerciales desde un formulario, analizar automáticamente la intención del cliente y dejar una respuesta sugerida para revisión humana.

El sistema permite clasificar leads según tres escenarios principales:

- Compra de vehículo.
- Venta de vehículo a la concesionaria.
- Permuta, donde el cliente quiere comprar un auto y entregar otro como parte de pago.

La automatización no contacta directamente al cliente final. La IA analiza el caso, organiza la información y deja una respuesta sugerida para que una persona del equipo comercial la revise antes de enviarla.

---

## Herramientas utilizadas

- Airtable: base de datos, formulario de entrada y seguimiento de leads.
- n8n: orquestación del flujo automatizado.
- OpenRouter / OpenAI: modelo de IA utilizado por el agente.
- Gmail: envío de notificación interna al equipo comercial.
- GitHub: repositorio del proyecto y documentación.

---

## Estructura general del flujo

El flujo principal funciona de la siguiente manera:

1. El cliente completa un formulario de Airtable.
2. El registro ingresa en la tabla `Consultas Leads` con estado `Pendiente lectura IA`.
3. n8n detecta el nuevo lead mediante un Airtable Trigger.
4. El AI Agent analiza el mensaje y clasifica el escenario.
5. Si corresponde a Compra o Permuta, la IA consulta el stock disponible.
6. n8n actualiza el registro en Airtable con la resolución de la IA.
7. El estado del lead pasa a `Procesado por IA`.
8. Se envía un mail interno al equipo comercial con el resumen del caso.
9. La respuesta queda pendiente de revisión humana antes de contactar al cliente.

---

## Arquitectura del flujo en n8n

El workflow principal está compuesto por los siguientes nodos:

```text
Airtable Trigger
↓
AI Agent
↓
Update Lead - Base
↓
Gmail
