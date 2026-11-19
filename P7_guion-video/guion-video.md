# P7 – Guion de la video-defensa (máx. 3 min, individual, cámara encendida)
Estado: PENDIENTE (estructura; se redacta cuando haya resultados). Es una síntesis argumentada, no una lectura del informe.

| Bloque | Qué decir | Tiempo orientativo |
|---|---|---|
| 1. Caso en una frase | | ~20 s |
| 2. Acoplamiento entre ejes más relevante | | ~60 s |
| 3. Decisión profesional y por qué se descartó la otra alternativa | | ~60 s |
| 4. Una limitación de mi propio trabajo | | ~30 s |
# Guion de Video-Defensa (Duración objetivo: 2 min 50 s – 3 min 00 s)
**Caso:** F1-01 — Sala de servidores de un hospital escuela: fallas por descarga electrostática  

---

### 1. Presentación del caso y pregunta guía (0:00 – 0:40 | ~40 seg)
> "Hola, soy Florencia Patiño, estudiante de Ingeniería en Sistemas de Información, y presento la resolución del Caso F1-01 de Física II: fallas intermitentes y reinicios no planificados en la sala de servidores de un hospital escuela.  
> El problema aparece tras intervenciones técnicas en días secos de invierno, sin disparos en las protecciones térmicas ni daños visibles. Nuestra pregunta guía fue: **¿cómo cuantificar el mecanismo físico de las descargas electrostáticas (ESD) a través de los cinco ejes de la materia y qué solución de ingeniería garantiza la continuidad operativa del hospital con mayor viabilidad técnica y económica?**"

### 2. Recorrido por los 5 ejes de cálculo (0:40 – 1:45 | ~65 seg)
> "Para responderla, modelamos la cadena física completa:  
> * En el **Eje I (Electrostática)**, calculamos que la fricción del operador en un ambiente seco ($HR < 30\text{ \%}$) acumula una carga de $300\text{ nC}$ sobre una capacitancia corporal de $150\text{ pF}$, generando un potencial de $2000\text{ V}$ y una energía de $0,30\text{ mJ}$, suficiente para perforar el óxido de puerta de circuitos integrados.  
> * En el **Eje II (Corriente Continua)**, demostramos que intercalar una pulsera antiestática con resistencia de $1,0\text{ M}\Omega$ establece una constante de tiempo $\tau = 0,15\text{ ms}$ y limita la corriente pico a $2,0\text{ mA}$, drenando la carga en menos de $0,75\text{ ms}$ sin riesgo de electrocución frente a red de $220\text{ V}$.  
> * En el **Eje III (Magnetismo)**, aplicamos la Ley de Faraday-Lenz para mostrar cómo una descarga rápida sin limitar genera variaciones de flujo magnético que inducen tensiones parásitas en los buses de datos cercanos.  
> * En el **Eje IV (CA y Ondas Electromagnéticas)**, caracterizamos el pulso ESD como una fuente radiada de banda ultraancha que acopla ruido de alta frecuencia en pistas sin blindaje.  
> * Finalmente, en el **Eje V (Electrónica)**, diseñamos la doble barrera de protección: diodos TVS de sujeción rápida en hardware y un nodo de monitoreo ambiental con microcontrolador."

### 3. Validación mediante simulación (1:45 – 2:25 | ~40 seg)
> "Validamos los modelos con tres simulaciones digitales. En **Tinkercad Circuits** *(mostrar en pantalla la captura de Tinkercad con el Monitor Serie)*, implementamos el subsistema del Eje V con un Arduino Uno, un sensor analógico de humedad relativa y lógica de alarma. Verificamos que, al descender la humedad por debajo del umbral crítico del $30\text{ \%}$, el conversor ADC de $10\text{ bits}$ dispara la alerta roja y bloquea el mantenimiento preventivo, con un error de cuantización menor al $0,1\text{ \%}$ respecto al cálculo analítico."

### 4. Decisión profesional fundamentada (2:25 – 3:00 | ~35 seg)
> "Como decisión profesional, tras comparar el costo y la viabilidad de instalar un piso conductivo técnico frente a la humidificación industrial y el control equipotencial directo, recomendamos implementar de inmediato el **protocolo de pulsera antiestática de $1\text{ M}\Omega$, tapete disipativo y bloqueo automático por baja humedad**, complementado en una segunda etapa por el ajuste HVAC al $45\text{ \% HR}$. Esta solución elimina el riesgo ESD sin detener los servidores críticos del hospital y con una fracción mínima de inversión. Muchas gracias."
