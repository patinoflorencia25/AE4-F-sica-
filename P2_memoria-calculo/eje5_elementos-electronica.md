# Eje V — Elementos de Electrónica
**Caso:** F1-01 — Sala de servidores de un hospital escuela: fallas por descarga electrostática  
**Asignatura:** Física II — Ingeniería en Sistemas de Información (UCP)  
**Versión:** v1  

---

## (a) Fenómeno físico identificado y leyes que lo describen

La placa de red (NIC) quemada y los módulos de memoria dañados en el caso F1-01 evidencian que la energía de la descarga electrostática (Eje I y II) o del pulso acoplado (Ejes III y IV) superó el umbral de ruptura dieléctrica de las compuertas CMOS internas del transceptor Ethernet (PHY). Para proteger la interfaz electrónica sin degradar la transmisión de datos de alta velocidad, se emplean **diodos supresores de tensiones transitorias (TVS — Transient Voltage Suppressor)** en paralelo con las líneas de señal hacia masa de chasis.

Las leyes y principios físicos involucrados son:

1. **Ruptura por avalancha en unión PN (Diodo TVS):**
   En polarización inversa normal ($V < V_{\text{RWM}}$), el diodo TVS presenta una impedancia muy alta y corriente de fuga despreciable ($I_R \sim \mu\text{A}$), siendo transparente para la señal Ethernet. Cuando un pulso ESD supera la tensión de ruptura ($V_{\text{BR}}$), se produce una multiplicación por avalancha en la unión semiconductora que reduce abruptamente su impedancia dinámica ($R_{\text{dyn}}$), recortando (*clamping*) la sobretensión a un valor seguro $V_C$:
   $$V_C = V_{\text{BR}} + I_{\text{PP}} \cdot R_{\text{dyn}}$$
   (Boylestad & Nashelsky, 2009, Cap. 1 y Cap. 16, pp. 1–25, 760–765).
2. **Reactancia capacitiva de la capacidad parásita de unión ($C_j$):**
   Toda unión PN polarizada en inversa posee una capacitancia de agotamiento $C_j$. A altas frecuencias ($f$), esta capacitancia introduce una reactancia en paralelo con la línea de transmisión:
   $$X_C = \frac{1}{2\pi f C_j}$$
   Si $C_j$ es demasiado elevada, atenúa los flancos de la señal digital Ethernet y degrada la integridad de señal.
3. **Filtro pasabajos RC equivalente (compromiso protección vs. ancho de banda):**
   La impedancia característica de la línea diferencial ($Z_0$) y la capacitancia parásita del TVS ($C_{\text{TVS}}$) forman un polo pasabajos con frecuencia de corte a $-3\text{ dB}$:
   $$f_{-3\text{ dB}} = \frac{1}{2\pi R_{\text{eq}} C_{\text{TVS}}}$$
4. **Puente Hardware – Software (acondicionamiento y monitoreo ambiental):**
   Para prevenir las condiciones ambientales que disparan el fenómeno (humedad relativa baja $<30\text{ \%}$), se integra un subsistema embebido basado en microcontrolador (placa *open hardware*) con sensor de humedad/temperatura y etapa de acondicionamiento/conversión analógico-digital (ADC) o bus digital, que genera alertas tempranas en el sistema de monitoreo del hospital.

---

## (b) Magnitudes y datos adoptados

| Magnitud / Parámetro | Símbolo | Valor adoptado | Fuente / Justificación |
| :--- | :---: | :---: | :--- |
| Tensión pico de descarga ESD (contacto / aire severo) | $V_{\text{ESD}}$ | $8\text{ kV}$ / $15\text{ kV}$ | Datos del caso F1-01 (2 a 15 kV) y nivel 4 de IEC 61000-4-2 ($8\text{ kV}$ contacto). |
| Corriente pico del pulso ESD a $8\text{ kV}$ (IEC 61000-4-2) | $I_{\text{PP}}$ | $30\text{ A}$ | Especificación estándar de forma de onda IEC 61000-4-2 ($3,75\text{ A/kV}$). |
| Tensión máxima inversa de trabajo del TVS (línea Ethernet) | $V_{\text{RWM}}$ | $3,3\text{ V}$ | Hoja de datos típica de matriz TVS para Ethernet (ej. Semtech RClamp0524P / Littelfuse SP3012). |
| Tensión de ruptura inversa del TVS | $V_{\text{BR}}$ | $4,0\text{ V}$ (mín.) | Hoja de datos de matriz TVS de baja capacitancia para interfaces de alta velocidad. |
| Resistencia dinámica del TVS en conducción de avalancha | $R_{\text{dyn}}$ | $0,35\text{ }\Omega$ | Parámetro típico de hoja de datos para TVS de protección ESD de líneas de datos. |
| Capacitancia parásita típica del TVS por línea (línea a tierra) | $C_{\text{TVS}}$ | $0,5\text{ pF}$ ($0,5 \times 10^{-12}\text{ F}$) | Hoja de datos de arreglo TVS ultra-baja capacitancia para Gigabit Ethernet. |
| Capacitancia de un diodo Zener/TVS estándar de potencia (comparación) | $C_{\text{TVS,std}}$ | $150\text{ pF}$ ($1,5 \times 10^{-10}\text{ F}$) | Valor típico de diodos TVS convencionales de alimentación (no aptos para datos). |
| Impedancia de carga equivalente por conductor respecto a referencia | $R_{\text{eq}}$ | $50\text{ }\Omega$ | Mitad de la impedancia diferencial de $100\text{ }\Omega$ del par trenzado Cat6A. |
| Frecuencia fundamental de señal 1000BASE-T | $f_{\text{ETH}}$ | $125\text{ MHz}$ | Estándar IEEE 802.3ab (Gigabit Ethernet). |
| Resolución ADC y tensión de referencia del nodo de monitoreo | $N_{\text{bits}}, V_{\text{ref}}$ | $10\text{ bits}$ ($1024\text{ niveles}$), $5,0\text{ V}$ | Arquitectura estándar AVR (Arduino Uno / ATmega328P) para telemetría ambiental. |

---

## (c) Resolución cuantitativa

### 1. Tensión de sujeción (*clamping voltage*) del TVS ante un pulso ESD de $8\text{ kV}$ ($I_{\text{PP}} = 30\text{ A}$)
Cuando el pulso ESD ingresa por el puerto RJ45, el diodo TVS entra en avalancha en menos de $1\text{ ns}$ y fija la tensión residual que llega al chip PHY de la placa de red:

$$V_C = V_{\text{BR}} + I_{\text{PP}} \cdot R_{\text{dyn}} = 4,0\text{ V} + (30\text{ A} \cdot 0,35\text{ }\Omega) = 4,0\text{ V} + 10,5\text{ V} = 14,5\text{ V}$$

*(Nota: Con el transformador de aislamiento Ethernet colocado antes o después según topología, la energía residual que alcanza el silicio se reduce en más de tres órdenes de magnitud frente a los $8\,000\text{ V}$ incidentes, manteniéndose dentro de la tolerancia de transitorios cortos del transceptor).*

### 2. Verificación del impacto de la capacidad parásita ($C_{\text{TVS}}$) sobre la señal Ethernet
Calculamos la reactancia capacitiva a $f_{\text{ETH}} = 125\text{ MHz}$ y la frecuencia de corte del enlace:

**Caso A: Diodo TVS de ultra-baja capacitancia ($C_{\text{TVS}} = 0,5\text{ pF}$):**

$$X_{C,\text{baja}} = \frac{1}{2\pi \cdot (125 \times 10^6\text{ Hz}) \cdot (0,5 \times 10^{-12}\text{ F})} \approx 2\,546,5\text{ }\Omega$$

$$f_{-3\text{ dB,baja}} = \frac{1}{2\pi \cdot 50\text{ }\Omega \cdot (0,5 \times 10^{-12}\text{ F})} \approx 6,37 \times 10^9\text{ Hz} = 6,37\text{ GHz}$$

**Caso B: Diodo TVS estándar de alimentación ($C_{\text{TVS,std}} = 150\text{ pF}$):**

$$X_{C,\text{std}} = \frac{1}{2\pi \cdot (125 \times 10^6\text{ Hz}) \cdot (150 \times 10^{-12}\text{ F})} \approx 8,49\text{ }\Omega$$

$$f_{-3\text{ dB,std}} = \frac{1}{2\pi \cdot 50\text{ }\Omega \cdot (150 \times 10^{-12}\text{ F})} \approx 2,12 \times 10^7\text{ Hz} = 21,2\text{ MHz}$$

**Interpretación de resultados:**
- Con el TVS especializado ($0,5\text{ pF}$), la reactancia a $125\text{ MHz}$ es de **$2\,546,5\text{ }\Omega$** (mucho mayor que los $50\text{ }\Omega$ de la línea, por lo que casi no deriva señal útil a masa) y el ancho de banda de corte es de **$6,37\text{ GHz}$**, dejando pasar sin distorsión la señal Gigabit Ethernet.
- Si por error de diseño se utilizara un diodo de protección común ($150\text{ pF}$), su reactancia caerían a **$8,49\text{ }\Omega$** y recortaría el ancho de banda a **$21,2\text{ MHz}$**, bloqueando la comunicación de red.

### 3. Puente Hardware – Software: Resolución del ADC para alarma de baja humedad ($HR < 30\text{ \%}$)
Para un sensor analógico de humedad relativa lineal ($0\text{ V} \rightarrow 0\text{ \% HR}$ a $5,0\text{ V} \rightarrow 100\text{ \% HR}$) conectado a un ADC de $10\text{ bits}$ ($V_{\text{ref}} = 5,0\text{ V}$):

$$\Delta V_{\text{LSB}} = \frac{V_{\text{ref}}}{2^{10}} = \frac{5,0\text{ V}}{1024} \approx 4,88\text{ mV/paso} \quad (\text{equivale a } 0,098\text{ \% HR por paso})$$

El umbral crítico del caso F1-01 ($HR = 30\text{ \%}$, donde el riesgo de triboelectricidad invernal se dispara) corresponde a una tensión de entrada de $V_{\text{umbral}} = 1,50\text{ V}$ y un código digital de:

$$\text{Código}_{\text{ADC}} = \text{round}\left(\frac{1,50\text{ V}}{5,0\text{ V}} \times 1024\right) = 307$$

Cuando la lectura cae por debajo del código `307` ($<30\text{ \% HR}$), el microcontrolador activa una alerta visual/sonora en la sala y envía una trama serie/MQTT al servidor de monitoreo antes de habilitar tareas de mantenimiento.

---

## (d) Características influyentes y efectos

1. **Inductancia parásita de pistas (layout de PCB):** A velocidades de flanco sub-nanosegundo ($t_r = 0,8\text{ ns}$), una pista de apenas $1\text{ cm}$ entre el conector RJ45 y el diodo TVS posee una inductancia parásita $L_{\text{pista}} \approx 8\text{--}10\text{ nH}$. Durante el flanco de corriente ($\frac{dI}{dt} \approx \frac{30\text{ A}}{0,8\text{ ns}} = 3,75 \times 10^{10}\text{ A/s}$), se genera una sobretensión inductiva adicional $V_L = L_{\text{pista}} \frac{dI}{dt} \approx 300\text{ V}$ si el TVS no está ubicado inmediatamente junto al conector.
2. **Temperatura de unión:** Un aumento de temperatura ambiente incrementa levemente la tensión de ruptura $V_{\text{BR}}$ (coeficiente térmico positivo en diodos de avalancha $>5\text{ V}$) y la corriente de fuga inversa $I_R$, aunque dentro del rango climatizado de una sala de servidores ($18\text{--}24\text{ }^\circ\text{C}$) su efecto es despreciable.
3. **Efecto sobre el sistema y el ambiente:** La protección electrónica correcta evita el reemplazo prematuro de placas de red y servidores completos (reduciendo residuos electrónicos — RAEE — y costos de indisponibilidad hospitalaria).

---

## (e) Consecuencia para el Sistema de Información

1. **Especificación técnica de hardware de red:** Exigir en los pliegos de adquisición de placas de red y switches de acceso del hospital que cuenten con protección ESD integrada o externa certificada bajo **IEC 61000-4-2 Nivel 4 ($\pm 8\text{ kV}$ contacto / $\pm 15\text{ kV}$ aire)** implementada con arreglos TVS de ultra-baja capacitancia ($C_j < 1\text{ pF}$).
2. **Monitoreo automatizado integrado al flujo de mantenimiento:** Implementar un nodo sensor de humedad y temperatura en el rack conectado al sistema de gestión de infraestructura (DCIM / Zabbix / Nagios del hospital) que bloquee o alerte automáticamente las órdenes de mantenimiento físico cuando la humedad relativa descienda por debajo del $35\text{--}40\text{ \%}$, articulando la prevención física con el control operativo de Sistemas de Información.

---

## (f) Fundamentación bibliográfica (APA 7)

- Boylestad, R. L., & Nashelsky, L. (2009). *Electrónica: Teoría de circuitos y dispositivos electrónicos* (10.ª ed., Cap. 1: Diodos semiconductores, pp. 1–45; Cap. 16: Otros dispositivos de dos terminales, pp. 760–766). Pearson Educación.
- International Electrotechnical Commission. (2008). *IEC 61000-4-2: Electromagnetic compatibility (EMC) — Part 4-2: Testing and measurement techniques — Electrostatic discharge immunity test* (2.ª ed.). IEC.
