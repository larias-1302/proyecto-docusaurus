---
id: acuerdos
title: Acuerdos del proyecto
sidebar_label: Acuerdos
---

---
# Acta de Acuerdos y Trade-offs: Reunión de Junta Directiva

Tras la sesión de la Junta Directiva enfocada en la profesionalización del negocio de grama sintética, se definieron las prioridades estratégicas y los sacrificios técnicos necesarios para garantizar una implementación rápida y efectiva.

---

## 1. Acuerdos Alcanzados

| ID | Acuerdo | Descripción |
| :--- | :--- | :--- |
| **AC-01** | **Priorización del Módulo de Gestión de Personal** | Se determinó que el recurso más crítico es el equipo de instaladores. El sistema se enfocará primero en la asignación de cuadrillas y control de asistencia en las obras de grama. |
| **AC-02** | **Optimización del Flujo de Datos de Clientes** | Se acordó implementar un módulo ágil de captura de prospectos y seguimiento de quejas para mejorar la respuesta comercial y evitar la pérdida de contratos. |
| **AC-03** | **Postergación del Módulo de Catálogo e Inventario** | Debido a la complejidad logística de los rollos y materiales, se decidió dejar el catálogo detallado y la gestión de precios automatizada para una actualización futura. |

---

## 2. Trade-offs (Análisis de Concesiones)

El equipo de directivos evaluó los siguientes intercambios estratégicos para viabilizar el proyecto en el corto plazo:

### A. Control Operativo vs. Control de Almacén
* **Decisión:** Enfocar los esfuerzos en la gestión del personal de campo.
* **Trade-off:** Se aceptó seguir manejando el inventario de grama sintética de forma manual temporalmente. Se priorizó saber *quién* está en la obra y *qué* opina el cliente, sacrificando la precisión automatizada de las existencias en bodega.

### B. Velocidad de Entrega vs. Robustez Técnica
* **Decisión:** Utilizar un sistema de almacenamiento de datos simplificado (archivos planos o estructuras ligeras) en lugar de una base de datos relacional compleja.
* **Trade-off:** Se gana rapidez en el desarrollo y menor costo inicial, pero se asume el riesgo de una migración de datos más laboriosa en el futuro cuando el sistema crezca y requiera una base de datos profesional.

### C. Agilidad Comercial vs. Estandarización de Precios
* **Decisión:** Implementar un registro rápido de datos de clientes y necesidades.
* **Trade-off:** Al no incluir el módulo de catálogo y precios en esta fase, las cotizaciones seguirán dependiendo del criterio manual del vendedor. Se aceptó este margen de error para priorizar que ningún cliente se quede sin atención o seguimiento.

---

## 3. Conclusión de la Sesión
La junta directiva concluye que la urgencia principal radica en el **control del capital humano** y la **satisfacción del cliente**. Aunque el catálogo y la base de datos son necesarios para la visión a largo plazo, su complejidad técnica justifica su exclusión de la fase inicial para asegurar que el sistema sea adoptado de inmediato por el equipo.
