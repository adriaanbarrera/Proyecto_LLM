# Asistente Experto en Física de 2º de Bachillerato
 
Agente conversacional basado en RAG que responde preguntas sobre Física de 2º de Bachillerato, usando documentos encontrados en la web como base de conocimiento y manteniendo memoria de conversación entre turnos.
 
---
 
## Descripción
 
El asistente es capaz de:
- Responder preguntas teóricas sobre los temas del material de estudio
- Plantear y resolver ejercicios y exámenes tipo al nivel de 2º de Bachillerato
- Mantener el contexto de la conversación 
- Reconocer cuándo una pregunta está fuera de su dominio y comunicarlo claramente

 
---
 
## Tecnologías utilizadas
 
| Componente | Tecnología |
|---|---|
| LLM | Google Gemini 2.0 Flash |
| Embeddings | sentence-transformers/paraphrase-multilingual-MiniLM-L12-v2 (HuggingFace) |
| Base de datos vectorial | ChromaDB |
| Framework agente | LangChain + LangGraph |
| Entorno de ejecución | Google Colab |
 
---
 
## Documentos utilizados
 
- `apuntes_fisica.pdf` — Apuntes teóricos de Física de 2º de Bachillerato
- `ejercicios_resueltos.pdf` — Problemas y ejercicios resueltos por temas
- `formulario.pdf` — Formulario de referencia con fórmulas y constantes
 
---
 
## Cómo ejecutar
 
### Requisitos previos
- Cuenta de Google
- API key de Google Gemini (gratuita en [aistudio.google.com](https://aistudio.google.com))
### Pasos
 
1. Abre `asistente_experto.ipynb` en [Google Colab](https://colab.research.google.com)
2. En el panel izquierdo, clic en el icono 🔑 (Secrets)
3. Añade un nuevo secret con nombre `GEMINI_API` y pega tu clave. Activa el toggle "Acceso al notebook"
4. Sube tus PDFs a `/content/` arrastrándolos al panel de archivos 📁
6. Ejecuta todas las celdas en orden: **Entorno de ejecución → Ejecutar todo**
 
---
 
## Justificación del System Prompt
 
Se diseñó un prompt con **dos modos de respuesta diferenciados**:
 
**Modo teoría:** el agente responde únicamente con información del contexto recuperado de ChromaDB. Esto garantiza que no invente conceptos ni datos fuera del material de estudio, lo cual es crítico en un contexto educativo donde la precisión importa.
 
**Modo ejercicios:** el agente usa su conocimiento propio de física de bachillerato para plantear y resolver problemas. Esta decisión se tomó porque los documentos originales no contenían suficientes ejercicios prácticos, y forzar al agente a limitarse al contexto lo hacía inútil para una de las funciones más valiosas de un asistente de estudio.
 
Adicionalmente, se añadieron reglas explícitas para que el agente **nunca haga referencia al documento o al contexto interno** en sus respuestas, logrando una experiencia más natural para el usuario final.
 
Esta separación entre recuperación de conocimiento documental y generación de ejercicios refleja un patrón habitual en sistemas RAG de producción, donde los embeddings y el LLM tienen roles claramente diferenciados.
 
