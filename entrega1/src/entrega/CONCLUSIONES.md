# Conclusiones - Práctica LLMs para Biomedicina

**Nombres:** Valentina García y Constanza Mayer
**Fecha:** 27/3/26

---

## Ejercicio 1: Primera Llamada

### 1. Diferencia entre respuesta sin y con system instruction
La respuesta sin system instruction es completamente técnica y general, como si estuvieras buscando una definición de libro, mientras que la respuesta con system instruction permite adaptar el lenguaje y el tono según lo que se define en este parámetro. Es una respuesta mucho más personalizada, en este caso por ejemplo teniendo empatía con el paciente.

### 2. ¿Pudiste modificar los parámetros internos del modelo? ¿Qué sí controlaste?
No, los parámetros internos del modelo no se pueden modificar, pero sí se puede controlar los parámetros de la API como: el modelo, el system instruction y el prompt.

### 3. ¿Qué pasaría si cambiaras el rol en el system instruction?
Cambiaría la respuesta, ya que el system intruction es lo que me da contexto y el comportamiento para poder responder al prompt.

### 4. ¿Qué system instruction sería útil para tu campo de estudio?
"Sos un ingeniero biomédico especializado en ..." 

---

## Ejercicio 2: Hiperparámetros

### 1. ¿Qué temperature usarías para un informe médico? ¿Y para brainstorming?
Para un informe médico usaría una temperatura muy baja, como 0.0 o 0.1, porque es importante que sea conciso.
Para brainstorming usaría una tempratura alta para obtener variedad de ideas, por ejemplo 1.5 - 2.

### 2. ¿Qué pasó con maxOutputTokens=50? ¿Fue útil?
No, no fue útil ya que al ser un límite muy bajo, la respuesta queda incompleta y no se logra desarrollar la idea. 
(Se obtuvo únicamente "¡Excelente").

### 3. Diferencia entre topP bajo y alto
Con un topP bajo, las respuestas son más precisas y seguras ya que el modelo utiliza las palabras con las probabilidades más altas.
Por el otro lado, un topP alto significa que el modelo considera una mayor variedad de palabras, mostrando respuestas más amplias y detalladas pero menos controladas.

### 4. ¿Las respuestas con temperature=0 fueron idénticas? Implicancias para reproducibilidad
No, las respuestas con temperature=0 no fueron idénticas, aunque sí muy similares en contenido. Esto implica que existe cierta variabilidad en las respuestas y por ende que los resultados de un modelo no siempre son perfectamente reproducibles. 

### 5. Hiperparámetros ideales para un chatbot médico. Justificá.
Para un chatbot médico eligiría una configuración conservadora: con temperature= 0.0 - 0.3 para asegurar respuestas concretas; topP= 0.5 para que sea un poco flexible en el lenguaje pero manteniendo precisión; topK=20 - 30 para evitar que las respuestas sean muy repetitivas; y maxOutputTokens= 800 para una longitud media.

---

## Ejercicio 3: Prompt Engineering

### 1. Ranking de técnicas (peor a mejor) con justificación
1. Zero-shot. Es el más simple porque no podés controlar el formato del output. El modelo no tiene una estructura clara a seguir y por ende responde de forma más libre.
2. Few-shot. La respuesta mejora ya que el modelo imita el formato proporcionado en los ejemplos y responde de forma más ordenada.
3. Chain-of-thought. Fue mejor todavía porque obliga al modelo a razonar paso a paso y esto, además de dar un orden, permite ir siguiendo la lógica y eventualmente identificar puntos débiles.
4. Role + constraints. Es la técnica con mayor calidad ya que además de razonar, el modelo tiene que respetar un rol específico y ciertas reglas estrictas/limitaciones. Con esto se logra un mayor control sobre el output, obteniendo respuestas más precisas y evitando información irrelevante. 

### 2. ¿La respuesta JSON fue clínicamente correcta? Ventajas del output estructurado
Sí, fue clinicamente correcta. La ventaja de un output estrcuturado es que lo vuelve compatible para ser procesado por otros sistemas y además es fácil de leer para el programador.

### 3. ¿El chain-of-thought cambió el diagnóstico o solo el razonamiento?
Sólo cambió el razonamiento. El modelo llegó al mismo diagnóstico pero el chain-of-thought permitió ver paso a paso cómo analizó los datos y cómo llegó a la conclusión.

### 4. ¿Encontraste información incorrecta presentada con confianza? ¿Cómo mitigarlo?
En general, el modelo suele responder con mucha confianza, lo cual puede ser peligroso ya que transmite bastante seguridad aun cuando quizás no tenga toda la información. Esto se podría mitigar obligando al modelo a indicar el nivel de confianza y que diferencie entre diagnóstico probable y diagnsótico confirmado. Además, siempre debe mantenerse la supervisión del médico y no debe reemplazarlo sino apoyarlo en la toma de decisiones.


### 5. Tu diseño ideal de asistente diagnóstico
Usaría una combinación de few-shot, chain-of-thought y role+constraints.
Primero usaría un system instruction donde el modelo tenga el rol de sistema de apoyo a la decisión clíncia y tenga reglas como indicar el nivel de confianza, incluir diagnósticos diferenciales y sugerir estudios confirmatorios. Además, aca le pediría que el output sea en formato JSON para que la información pueda ser integrada en otros sistemas.
Después usaría algunos ejemplos de respuestas para mostrarle el formato y estilo que busco.
Finalmente, implementaría chain-of-thought para que analice los casos con un razonamiento paso a paso y para lograr un diagnóstico más consistente y fácil de revisar.

---

## Reflexión Final

### ¿Qué aprendiste que no esperabas?
Que el output cambia enormemente según cómo definas tu prompt y eso es muy importante para obtener respuestas de calidad. 

### ¿Qué riesgos ves en el uso de LLMs en medicina?
El mayor riesgo es el uso incorrecto de la herramienta. Que lleve a la falta de juicio y por ende afecte el proceso de toma de decisiones. Esto es crítico porque se relaciona directamente con la salud de los pacientes. Se debe estar muy atento a las posibles alucinaciones para no trabajar con información falsa.

### ¿Qué oportunidades ves para tu área de especialización?
Se puede usar por ejemplo para el análisis de imágenes médicas, apoyando al médico en el diagnóstico y colaborando en la toma de decisiones.
