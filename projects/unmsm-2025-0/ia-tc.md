---
status: to do
deadline: 2025-06-26T00:00
class: ia
---
Desarrollo de software mediante LLMs: uso de al menos 3 modelos fundacionales; fundamentos; aplicación; caso de estudio

- fundamentos del desarrollo de software con LLMs ¿por qué funciona?
- ¿desde cuando es popular?
- patrones comunes de interacción entre llm y usuario

- [lineamientos](pdf/ia-tc.pdf)

---

En junio del 2020 OpenAI lanzó GPT-3, un modelo extenso de lenguaje (LLM) que cambió la expectativa sobre lo que es posible generar con lenguaje natural. Este modelo despertó el interés de muchos investigadores en GitHub Next, quienes hasta ese entonces consideraban a la generación de código de propósito general como algo hipotético. En 2021, OpenAI presentó Codex, una variante de GPT-3 entrenada con alrededor de 159GB de código de 54 millones de repositorios públicos, diseñada para producir no solo lenguaje natural, sino sugerencias de código. Este modelo fue desarrollado en colaboración con GitHub, quienes meses más tarde anunciaron Copilot, una herramienta capaz de ofrecer sugerencias sobre cómo completar cierto código a medida que se escribe. Esta herramienta evolucionó rápidamente: en 2022 salió de la beta y comenzó a integrarse bajo un modelo de suscripción, lo cual extendió su adopción. Para 2023 ya se reportaba que Copilot tenía más de un millón de usuarios profesionales y que algunos usuarios generaban hasta un 35% de su código con la herramienta.

Los LLMs o, concretamente, los transformadores generativos pre-entrenados (GPTs), son redes neuronales profundas capaces de predecir el siguiente token en una secuencia. Esto les permite modelar relaciones complejas entre datos de naturaleza secuencial, tal como texto y código. En la práctica, esto les permite "aprender" sobre sintaxis, convenciones y patrones presentes en múltiples lenguajes de programación. Al integrarse en editores de código, estos son capaces de entender la intención del desarrollador tomando como contexto al código y comentarios existentes. En sus inicios, Copilot funcionaba únicamente como herramienta de autocompletado. Hoy en día, Copilot Chat permite interactuar directamente con el modelo a través de instrucciones en lenguaje natural o *prompts*, incluso sin necesidad de código previo.

El desarrollo basado en *prompts* supone un diálogo iterativo: el **usuario** describe una tarea o requisito de programación en lenguaje natural, y el **asistente** responde con código sugerido, explicaciones o correcciones. Este patrón se materializa en APIs como la de Anthropic, donde se estructuran los mensajes en un arreglo alternante de roles (`user`, `assistant`) y opcionalmente un prompt inicial o `system` para enmarcar el **contexto** o rol de Claude (por ejemplo, “Eres un asistente experto en Python”). La calidad de los resultados se beneficia de prompts claramente estructurados. Anthropic recomienda usar estructuras XML para formalizar 

El uso de plantillas con variables (en `<instructions>`, `<example>`, etc.) permite separar claramente instrucciones, ejemplos y formato deseado, ayudando al modelo a interpretar correctamente cada parte ([docs.anthropic.com](https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/use-xml-tags?utm_source=chatgpt.com "Use XML tags to structure your prompts - Anthropic API")). Además, Anthropic recomienda usar estructuras XML para guiar al modelo en tareas complejas, combinando ejemplos multishot y cadenas de razonamiento (_chain‑of‑thought_) dentro de la misma petición ([docs.anthropic.com](https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/use-xml-tags?utm_source=chatgpt.com "Use XML tags to structure your prompts - Anthropic API")). Este diseño formal reduce errores en la respuesta y permite que la IA genere código más ajustado a la intención del desarrollador. El ciclo sigue así: el usuario envía su prompt (con `system` + `user`), el modelo responde en `assistant`, el usuario evalúa, prueba y refina y puede enviar un nuevo prompt para ajustar o extender la solución, cerrando un lazo iterativo de mejora continua.

---

¿Te parece que este párrafo encaja bien con el tono y nivel académico que buscas?