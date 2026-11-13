# Entregable Laboratorio 1: Benchmarking de Serving Local y Cuantización

- **Curso:** LLMOps, Serving Local y Arquitecturas RAG
- **Estudiante:** Jose Sebastian Fernandez
- **Hardware Utilizado:** CPU: Intel Core i5-1235U.  RAM: 16 GB.  GPU: Intel Iris Xe integrada  Windows 11 .
- **Fecha:** 12 de noviembre de 2026

---

## Análisis Técnico de Resultados

### 1. Impacto en Memoria (MEM USAGE y KV Cache)
> ¿Cuál fue la diferencia exacta en MB/GB de RAM consumida entre `q4_K_M` y `q8_0` al ejecutar `docker stats`? ¿Por qué el consumo en ejecución supera el tamaño del archivo en disco?

**Respuesta:**
Q4_K_M consumió 1.558 GiB y Q8_0 consumió 2.2 GiB. La diferencia fue de 0.642 GiB (aproximadamente 657 MiB).

El consumo supera el tamaño del modelo en disco porque también utiliza memoria para procesamiento, buffers y KV Cache, que almacena información de los tokens. En las pruebas se utilizó un contexto de 2048 tokens.

---

### 2. Ancho de Banda de Memoria y Velocidad (TPS)
> En inferencia sobre CPU, el cuello de botella suele ser el ancho de banda de la memoria RAM. ¿En qué porcentaje aumentó la velocidad (TPS) al pasar de 8 bits a 4 bits?

**Respuesta:**
Q4_K_M alcanzó 15.37 TPS y Q8_0 obtuvo 10.36 TPS. Al pasar de 8 bits a 4 bits, la velocidad aumentó aproximadamente 48.3 %, gracias a la reducción del tamaño de los pesos y del tráfico de memoria.

---

### 3. Latencia Inicial (TTFT) y Fase Prefill
> ¿Por qué el `TTFT (ms)` es significativamente más alto en el Prompt Largo que en el Prompt Corto?

**Respuesta:**
El prompt largo necesita más tiempo de procesamiento durante la fase Prefill, porque el modelo debe analizar más tokens antes de generar su primera respuesta. Por eso su TTFT es mayor.

---

### 4. Calidad vs. Eficiencia en `resultados_benchmark.md`
> Revisando las 6 respuestas completas generadas, ¿hubo alguna degradación perceptible en la lógica del código Python o en el razonamiento generado por el modelo de 4 bits frente al de 8 bits?

**Respuesta:**
Q4 ofrece menor consumo de memoria y mayor velocidad. Para determinar si perdió calidad frente a Q8, es necesario comparar las seis respuestas completas, especialmente el código Python y el razonamiento arquitectónico.

---
*Nota: Adjuntar junto con este documento los archivos generados `resultados_benchmark.csv` y `resultados_benchmark.md`.*
