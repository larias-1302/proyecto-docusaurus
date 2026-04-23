---
id: postmortem
title: Postmortem del Sistema de Grama
sidebar_label: Postmortem
---

# Documento Postmortem
---
# 1. Resumen del incidente
Durante la reunión con el cliente, una empresa dedicada a la instalación de grama sintética para canchas deportivas (fútbol, tenis, pádel) y proyectos decorativos, se identificaron múltiples problemas operativos que respaldan la causa raíz descrita en este documento.

El cliente explicó que todos los materiales son importados desde Estados Unidos y se manejan por lotes. Cada lote puede presentar variaciones de color, por lo que no es posible mezclar materiales entre pedidos. Esto implica que una mala asignación de inventario puede afectar directamente la calidad final del proyecto.
En este contexto, uno de los principales riesgos operativos es la asignación incorrecta de productos, ya que utilizar un tipo de grama diferente (por ejemplo, “Grama Premium” en lugar de “Grama Bermuda”) o mezclar lotes distintos genera inconsistencias visibles y reclamos por parte del cliente.

Asimismo, la empresa no cuenta con un sistema centralizado para gestionar inventario, pedidos y cotizaciones, lo que provoca que la información se maneje de forma separada y manual.

---

## Relación con el Incidente y Línea del Tiempo
El incidente presentado en la línea del tiempo refleja directamente esta problemática.

Durante el despliegue del sistema, no se detectaron errores en la asignación de productos. Sin embargo, posteriormente se identificó que el sistema estaba utilizando datos incorrectos, lo que provocó la asignación errónea de tipos de grama y la generación de rutas inválidas.

Esto se traduce en situaciones reales del negocio, donde una mala gestión del inventario o el uso de información incorrecta puede provocar:
* Entrega de productos equivocados
* Diferencias en tonos de grama
* Pérdidas económicas y retrabajo
* El uso de tablas incorrectas (datos de prueba en lugar de producción) representa la falta de control y validación en la información, equivalente a trabajar con registros no actualizados o inconsistentes en la operación diaria.

---
 
## Conclusión
Se observó que la problemática del cliente no es únicamente operativa, sino estructural. El crecimiento del negocio ha superado la capacidad de sus procesos actuales, los cuales siguen siendo manuales y no integrados.

Esto refuerza la necesidad de implementar una solución tecnológica centralizada (como un sistema de catálogo y gestión de procesos), que permita:
* Unificar la información
* Reducir la carga operativa
* Mejorar la coordinación entre áreas
* Evitar futuros incidentes similares

---

# 2. Linea del tiempo (timeline) Incidente de Sincronización de Base de Datos
**Proyecto:** Sistema de Automatización de Pedidos - Empresa de Grama Importada  
**Fecha del Incidente:** 21 de abril de 2026  
**Fecha del Reporte:** 22 de abril de 2026  
**Equipo Responsable:** Estudiantes Ingeniería USAC  
**Estado:** Finalizado / Lecciones Aprendidas

---

## Resumen del Incidente
El 21 de abril, tras el despliegue del nuevo módulo de automatización de procesos, se detectó una anomalía crítica en la integridad de los datos. El sistema realizó asignaciones erróneas de productos, entregando "Grama Premium" (importada) en lugar de "Grama Bermuda". 

Adicionalmente, el **30% de las rutas de instalación** fueron generadas utilizando registros de la base de datos de prueba (*tablas espejo*), lo que derivó en errores de logística y pérdida de recursos en campo.

## Registro Cronológico (Timeline)

| Hora | Evento | Descripción |
| :--- | :--- | :--- |
| **08:00 AM** |  Despliegue | Se inicia la actualización del módulo de base de datos en el servidor de producción. |
| **08:15 AM** |  Confirmación | El sistema de integración continua marca el despliegue como "Exitoso". |
| **09:30 AM** |  Primer Reporte | Logística reporta un cliente inconforme: entrega de producto incorrecto en sitio. |
| **10:05 AM** | Crisis Logística | Se reciben 5 reportes simultáneos de cuadrillas perdidas por direcciones inexistentes. |
| **10:20 AM** |  **Momento Crítico** | Desarrollo identifica que el script lee la **tabla espejo** (pruebas) y no la **tabla maestra** (producción). |
| **10:45 AM** |  Contención | Se apaga el servidor de sincronización para evitar que se sigan corrompiendo pedidos. |
| **11:30 AM** |  Recuperación | Se ejecuta el *rollback* total a la versión previa estable de la base de datos. |
| **12:00 PM** |  Estabilización | Operación restablecida manualmente y validación de datos maestros exitosa. |

---

## 3. Impacto

Una deficiente organización en la distribución de tareas dentro del equipo de desarrollo genera un impacto directo en el avance del proyecto. La falta de una planificación adecuada puede provocar desbalance en la carga de trabajo, duplicación de esfuerzos o retrasos en la implementación de módulos clave.

Esto repercute principalmente en el incumplimiento de los tiempos establecidos, ya que una mala estimación del esfuerzo requerido para cada módulo dificulta la correcta integración del sistema en las etapas finales. Un retraso en el sistema también implica que la empresa no pueda utilizar el sistema en el tiempo estipulado y retrase en ciertos aspectos la productividad de la empresa y la organización de tiempos del área administrativa.

Asimismo, no considerar desde el inicio fases importantes como pruebas, validación y presentación de módulos incrementa el riesgo de errores en etapas avanzadas del desarrollo. La ausencia de documentación clara sobre el funcionamiento de cada componente del sistema complica la identificación y solución de fallas, afectando la calidad del producto final.

En consecuencia, estos factores no solo impactan en el tiempo de entrega, sino también en la eficiencia del equipo y en la mantenibilidad del sistema desarrollado.

## 4. Causa Raíz

Para identificar el origen del incidente en la gestión de proyectos de grama sintética, se aplicó la técnica de los **"5 Porqués"**, permitiendo desglosar el problema desde el síntoma superficial hasta la falla estructural del negocio.

### Análisis de los 5 Porqués

1. **¿Por qué hubo un retraso crítico en la entrega de la obra y errores en la facturación al cliente?**
   Porque los datos de inventario de rollos de grama y la disponibilidad del equipo de instalación no estaban sincronizados al momento de generar la orden.

2. **¿Por qué la información de inventario y personal no estaba sincronizada?**
   Porque cada área maneja su propia información en archivos locales e independientes, lo que genera duplicidad y datos contradictorios.

3. **¿Por qué se utilizan archivos locales independientes para áreas tan críticas?**
   Porque el flujo de trabajo actual depende de procesos manuales y herramientas no integradas que no permiten el flujo de datos en tiempo real entre el catálogo de precios y la asignación de personal.

4. **¿Por qué no existe una comunicación automatizada entre el catálogo, los precios y el personal?**
   Porque el negocio ha crecido a una escala medio-grande, pero los procesos administrativos siguen operando bajo una estructura artesanal diseñada para proyectos pequeños.

5. **¿Por qué los procesos siguen siendo artesanales a pesar del crecimiento del negocio? (Causa Raíz)**
   Debido a la **ausencia de un sistema de gestión profesional (ERP/Software Centralizado)** diseñado para integrar de forma modular el manejo de personal, facturación, quejas de clientes, catálogo y precios. La falta de una infraestructura tecnológica unificada impide la escalabilidad y el control de calidad en proyectos de gran envergadura.

---

**Conclusión del Análisis:**
El incidente no fue un error humano aislado, sino una consecuencia inevitable de la desconexión sistémica. La falta de una plataforma centralizada de gestión profesional impide que las áreas críticas del negocio (como la colocación de grama y el manejo de precios) se comuniquen, resultando en ineficiencias operativas y pérdida de control sobre la rentabilidad del proyecto.
 
## Acciones tomadas para solucionarlo
Durante el incidente, el equipo tomó medidas inmediatas para reducir el impacto generado por la falta de sincronización entre las áreas del negocio. Como primer acción, se decidió suspender temporalmente la generación automática de órdenes y facturación, con el objetivo de evitar la propagación de errores en los datos.
Posteriormente, se optó por implementar un control manual provisional, en el cual se verificaba la disponibildad de invetario de rollos grama y la asignación del personal antes de confirmar pedido o proyecto. De manera simultanea, el equipo técnico realizó una revisión de los archivos loclaes utilizados por cada área, con el fin de identificar inconsistencias en la información y unificar los datos más relevantes en un solo registro temporal.
Asimismo, se estableció una comunicación directa entre las áreas involucradas (inventario, facturación y asignación de personal), permitiendo coordinar las actividades de forma más controlada mientras se solucionaba el problema. Finalmente, una vez corregidas las inconsistencias más críticas, se validó la información actualizada y se reanudó el flujo de trabajo, asegurando que las operaciones continuaran de manera más ordenada hasta la implementación de una solución definitiva.

## Acciones a futuro
Las acciones que se tomaran en el futuro a base de las conclusiones finales de la reunión, se basa em seguir con el plan original de la creación del sistema ya con las ideas más ordenadas. Al finalizar la implementación del programa se seguira actualizando para terminar de implementar cualquier aspecto a mejorar, tomando en cuenta los comentarios de los clientes y los errores que podrían presentarse a lo largo de el uso.

Ademas de ello, se estará convocando a diferentes reuniones para el correcto seguimiento del proyecto, asi se podrá compartir el avance y se resolvera dudas que se podrían generar al lo largo del tiempo, por ultimo se tendrá una comunicación con el cliente por cualquier modificación, de parte del equipo o del cliente.
