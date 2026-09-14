# Sistema de Alerta Temprana para Defensa Civil — Sur Tucumano

Proyecto integrador — Programación IV (TUP)
Docente: Ing. Marchese Rosana Soledad / TUP Albornoz Lucas Ariel — Comisión C11

## Descripción

Sistema web para la gestión y difusión de alertas tempranas por parte de Defensa
Civil (u otro organismo) en el sur de Tucumán. Los organismos cargan alertas
asociadas a una o más zonas geográficas, y los vecinos suscriptos a esas zonas
reciben una notificación (por email, en esta primera versión) cuando se emite
una alerta que los afecta.

El proyecto toma como referencia el modelo de "Alerta California" (CalAlerts),
un sistema de suscripción voluntaria por zona, y responde a la Ley Provincial
9.775 (creación del SAEC) y a la ley aprobada el 30/07/2026 que designa a la
Dirección de Defensa Civil como autoridad de aplicación y crea el Departamento
de Monitoreo y Alerta Temprana.

Ver `docs/dominio-propuesto.pdf` para la explicación completa del dominio, el
modelo de datos y los endpoints previstos.

## Estructura del proyecto

```
backend/     # API REST (FastAPI + SQLAlchemy)
frontend/    # Cliente web
docs/        # Documentación del proyecto (DER, dominio, etc.)
```

## Estado actual

- [x] Definición del dominio y modelo relacional (TP0)
- [x] Repositorio y estructura de carpetas (TP1)
- [ ] Implementación del backend
- [ ] Implementación del frontend

## Endpoints REST previstos

- `/alertas`
- `/zonas` (incluye consulta pública de alertas activas por zona)
- `/organismos`
- `/niveles-alerta`
- `/suscriptores`
- `/reportes/cobertura`

## Autor

Maxi — Tecnicatura Universitaria en Programación
