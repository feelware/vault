# Expo final

## Codificación

### Objetivo

El objetivo de la codificación es asegurar que las especificaciones de diseño se implementen correctamente en el código, garantizando que este sea funcional, mantenible y cumpla con los estándares definidos. Además, se busca que el software sea escalable y fácil de adaptar a cambios futuros, lo que reduce significativamente los errores en fases posteriores del desarrollo, como pruebas o integración.

### Entrada

Las entradas esenciales para el proceso de codificación incluyen las especificaciones de programas, que definen el comportamiento y los requisitos funcionales del software; la documentación de programas, que detalla el funcionamiento e interacción de los componentes; y el listado de código, que actúa como referencia para asegurar la alineación con las especificaciones y estándares. También se incluyen los programas ejecutables, que permiten verificar la funcionalidad antes de la implementación final, y los diagramas de flujo, que ilustran la lógica del programa y facilitan la comprensión del proceso.

### Proceso

El proceso de codificación se compone de diversas actividades clave para garantizar la calidad del código. Estas incluyen la implementación de controles de integridad para asegurar que los datos y archivos sean correctos y consistentes, reglas de autorización para proteger el acceso no autorizado, auditorías de rastreo para monitorear el uso del sistema, y procedimientos de seguridad para prevenir vulnerabilidades. Además, se debe cumplir con la metodología adoptada, garantizar la correcta implementación según el diseño, y asegurar que el código sea fácil de mantener y modificar en el futuro. También es crucial establecer procedimientos operativos que faciliten la administración del software a lo largo de su ciclo de vida.

### Salidas

Como resultado de la codificación, se obtiene un listado de defectos encontrados, el cual incluye detalles sobre la ubicación, gravedad y posibles soluciones de los errores detectados. Este listado no solo permite la corrección inmediata de los errores, sino que también es útil para ajustar el proceso de desarrollo y prevenir fallos similares en el futuro. Además, es una herramienta valiosa para realizar análisis retrospectivos y mejorar las prácticas de desarrollo.

### Lista de Verificación (Checklist)

![](../../utilities/attachments/Pasted%20image%2020241204225012.png)

### Métricas

Durante la codificación, se utilizan diversas métricas para evaluar la calidad del software. La **complejidad ciclomática** mide la cantidad de caminos lineales independientes en el código, ayudando a identificar secciones que podrían ser difíciles de mantener o propensas a errores. La **densidad de defectos** calcula el número de defectos por cada 1,000 líneas de código, lo que permite identificar áreas que requieren más atención. Finalmente, la **cobertura de pruebas** mide el porcentaje de código ejecutado durante las pruebas, asegurando que una parte significativa del código haya sido probada, lo que ayuda a reducir la probabilidad de defectos no detectados.

### Involucrados

El proceso de codificación involucra a dos equipos clave: el equipo de ingeniería y el de aseguramiento de la calidad del software. El **gerente de proyecto** supervisa el progreso del proyecto y garantiza que se cumplan los plazos establecidos. El **grupo de programación**, compuesto por los desarrolladores, es responsable de implementar las soluciones técnicas de acuerdo con las especificaciones y estándares de codificación. En el equipo de aseguramiento de la calidad, el **líder de calidad** coordina las actividades de control de calidad, mientras que los **analistas de calidad** realizan pruebas y validaciones, detectando defectos y colaborando con los desarrolladores para asegurar que el software sea seguro, funcional y libre de errores.

---

## Pruebas del Sistema

### Objetivo

El objetivo de la fase de pruebas del sistema es validar que el sistema completo cumpla con los requisitos especificados, asegurando su correcto funcionamiento y la integración adecuada de todos los módulos. Esta fase busca garantizar que el sistema esté completamente preparado para ser entregado al usuario final, cumpliendo con los estándares de calidad previamente establecidos. Al final de esta etapa, se debe certificar que todas las funcionalidades del sistema han sido correctamente implementadas y verificadas, proporcionando la confianza de que el producto es estable y fiable.

### Entrada

Para iniciar la fase de pruebas, se requiere recibir las especificaciones funcionales y no funcionales del sistema, que detallan los requisitos y comportamientos esperados del mismo. Además, se deben contar con los casos de prueba diseñados previamente, los cuales cubren las funcionalidades y flujos críticos del sistema. También se necesitan los entregables del desarrollo, como el código fuente, configuraciones y otros artefactos que serán evaluados. El plan de pruebas, que incluye la priorización de las pruebas y los criterios de aceptación, es otro elemento crucial, pues establece cómo y en qué orden se realizarán las pruebas, asegurando que se alineen con los objetivos del proyecto.

### Proceso

El proceso de pruebas comienza con la **preparación del entorno de pruebas**, donde se configura el hardware y software necesarios para replicar las condiciones reales de uso del sistema. Esta fase también incluye la verificación de que todos los datos y herramientas requeridas para ejecutar las pruebas estén disponibles. Posteriormente, se ejecutan las **pruebas funcionales**, que tienen como objetivo verificar que cada funcionalidad del sistema cumpla con los requisitos especificados, validando los flujos de trabajo clave desde el punto de vista del usuario final. En paralelo, se realizan **pruebas de integración** para asegurar que los diferentes módulos y componentes del sistema interactúen correctamente entre sí. Además, se llevan a cabo **pruebas de rendimiento** para evaluar el comportamiento del sistema bajo distintas condiciones de carga, verificando aspectos como la velocidad, capacidad de respuesta y estabilidad. A lo largo de estas pruebas, se debe **documentar los resultados**, registrando los fallos encontrados y generando reportes detallados para su análisis y resolución. Este proceso es fundamental para garantizar que todas las funciones del sistema estén correctamente validadas antes de su implementación.

### Salidas

Al finalizar la fase de pruebas, se generan varios entregables clave. Uno de los más importantes es el **reporte de pruebas**, un documento detallado que incluye los resultados de todas las pruebas realizadas, los fallos identificados y su gravedad. Este reporte sirve como base para la toma de decisiones y la priorización de correcciones. Además, se crea un **registro de defectos**, una lista priorizada de errores detectados durante las pruebas, que incluye información sobre la ubicación del defecto, su causa y el estado de su corrección. Tras la resolución de los defectos críticos, el **sistema validado** es el producto final que ha superado las pruebas esenciales y está listo para su despliegue o para ser sometido a la fase de **pruebas de aceptación del usuario**. Finalmente, cualquier defecto o mejora detectada se refleja en la **actualización del backlog**, lo que permite incluirlas en iteraciones posteriores para su corrección.

### Lista de Verificación (Checklist)

![](../../utilities/attachments/Pasted%20image%2020241204225030.png)

### Métricas

Durante la fase de pruebas, se utilizan varias métricas para evaluar la efectividad del proceso. El **porcentaje de cobertura de pruebas** mide la cantidad de funcionalidades y casos de uso que han sido verificados mediante las pruebas realizadas. Este indicador es crucial para garantizar que se cubran todas las funcionalidades críticas del sistema y reducir la posibilidad de defectos en producción. La **tasa de defectos por iteración** permite analizar el número de defectos encontrados durante una iteración específica del desarrollo o las pruebas, lo que ayuda a identificar fases con alta incidencia de errores y a enfocar los esfuerzos en mejorar los procesos de calidad. Además, el **tiempo promedio de resolución de defectos** es una métrica que mide la eficiencia del equipo en la identificación, documentación, asignación y corrección de los defectos. Esta métrica permite identificar áreas donde el proceso puede optimizarse, y su reducción indica que el equipo está resolviendo los problemas de manera ágil y efectiva.

### Involucrados

En la fase de pruebas, el equipo de ingeniería juega un papel fundamental, con los **desarrolladores de software** encargados de corregir los errores identificados durante las pruebas y ajustar las funcionalidades según los hallazgos. Los **arquitectos de software** también están involucrados, ya que deben evaluar problemas estructurales o de integración que puedan surgir durante las pruebas. Además, el equipo de **aseguramiento de la calidad de software** es crucial para el éxito de las pruebas. Los **analistas de calidad** diseñan y actualizan los casos de prueba según los cambios realizados en el sistema, mientras que los **ingenieros de pruebas** son responsables de automatizar pruebas y ejecutar los casos de prueba manuales, evaluando el sistema en diferentes escenarios para asegurar su calidad y rendimiento.
