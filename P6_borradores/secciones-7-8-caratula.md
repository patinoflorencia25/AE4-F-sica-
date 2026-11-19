# UNIVERSIDAD DE LA CUENCA DEL PLATA
**Facultad de Ingeniería y Tecnología**  
**Carrera:** Ingeniería en Sistemas de Información  
**Cátedra:** Física II — Actividad de Evaluación N.º 4 (AE4): Resolución Integradora de Caso Real  
**Período:** Noviembre de 2026  

---

**Título del Proyecto:**  
Diagnóstico electromagnético y diseño de mitigación ante fallas por descarga electrostática (ESD) en la sala de servidores de un hospital escuela (Caso F1-01)

**Integrantes:**  
* Patiño, Florencia Noemí (GitHub: `patinoflorencia25`)
* *[Completar aquí Nombre y Apellido del compañero/a de equipo si corresponde]*

**Docente a cargo:** *[Completar nombre del docente]*  
**Repositorio público del proceso:** https://github.com/patinoflorencia25/AE4-F-sica-

---

# SECCIÓN 7. INTEGRACIÓN Y DECISIÓN PROFESIONAL

## 7.1 Mapa de acoplamientos entre los cinco ejes temáticos
Los fenómenos analizados en la sala de servidores del hospital escuela (Caso F1-01) no operan de forma aislada, sino como una cadena física acoplada donde cada etapa condiciona la siguiente:

* **Eje I (Electrostática) $\rightarrow$ Eje II (Corriente Continua):** La separación triboeléctrica por fricción entre el calzado del operador y el piso técnico acumula una carga neta $Q \approx 300\text{ nC}$ sobre la capacitancia corporal equivalente ($C_{\text{cuerpo}} = 150\text{ pF}$), elevando el potencial a $V_0 = 2000\text{ V}$. El **Eje II** determina la resistencia óhmica óptima de la vía de descarga ($R_{\text{pulsera}} = 1,0\text{ M}\Omega$) que gobierna la constante de tiempo $\tau = R \cdot C = 0,15\text{ ms}$, disipando la energía almacenada ($U = 0,30\text{ mJ}$) de manera controlada sin riesgo de fibrilación ventricular ni daño térmico en el silicio.
* **Eje II / Eje IV $\rightarrow$ Eje III (Magnetismo):** La descarga rápida de corriente impulsiva (en ausencia de limitación resistiva) o los transitorios de conmutación de fuentes generan derivadas temporales de corriente ($\mathrm{d}i/\mathrm{d}t$) que inducen campos magnéticos variables $\vec{B}(t)$. Por la **Ley de Faraday-Lenz** (Eje III), estos flujos variables inducen fuerzas electromotrices parásitas ($\varepsilon_{\text{ind}}$) en los lazos de datos cercanos, provocando corrupción silenciosa de tramas de red o reinicios lógicos.
* **Eje IV (CA y Ondas Electromagnéticas) $\rightarrow$ Eje V (Electrónica):** El arco ESD actúa como una antena dipolar de banda ultraancha que radia energía electromagnética en el rango de decenas de megahertz a gigahertz (Eje IV), acoplándose por diafonía radiada en las pistas de circuito impreso (PCB). El **Eje V** resuelve esta vulnerabilidad mediante etapas de protección hardware (diodos TVS / clamp que limitan sobretensiones antes de perforar el óxido de puerta MOSFET) y un puente hardware-software de monitoreo continuo de humedad relativa mediante conversión analógica-digital (ADC de 10 bits).

---

## 7.2 Evaluación comparativa de alternativas de mitigación ESD

| Criterio de evaluación | Alternativa A: Piso conductivo / disipativo técnico | Alternativa B: Control activo de humedad relativa ($45\text{–}55\text{ \% HR}$) | Alternativa C: Pulsera antiestática ($1\text{ M}\Omega$) + Tapete + Monitoreo ADC |
| :--- | :--- | :--- | :--- |
| **Mecanismo físico principal** | Drenaje continuo de carga a tierra ($R_{\text{sistema}} < 10^9\text{ }\Omega$ según ANSI/ESD S20.20). | Formación de película molecular de agua adsorbida que incrementa la conductividad superficial. | Limitación de corriente de descarga ($I_{\text{máx}} = 2,0\text{ mA}$) mediante resistor serie de seguridad y bloqueo preventivo. |
| **Inversión inicial (CAPEX)** | Muy alta (obra civil en sala activa, levantamiento de piso técnico y puesta a tierra). | Alta (humidificadores industriales de precisión, sensores y adecuación HVAC). | **Muy baja** (kit ESD certificado por estación + nodo sensor microcontrolado). |
| **Costo operativo (OPEX)** | Bajo (limpieza con productos no aislantes y auditoría anual). | Alto (consumo eléctrico continuo, tratamiento de agua desmineralizada y mantenimiento). | **Muy bajo** (verificación diaria con probador de continuidad). |
| **Efectividad técnica aislada** | Alta, pero ineficaz si el operador utiliza calzado aislante o manipula placas sentado. | Media-alta, pero reduce generación de carga sin garantizar equipotencialidad al tocar el chasis. | **Muy alta** para intervenciones de mantenimiento directo (elimina diferencia de potencial mano-chasis). |
| **Riesgo operativo en hospital** | Requiere parada parcial de sala o logística compleja durante instalación. | Riesgo de condensación local si fallan los lazos de control térmico. | **Nulo** en operación normal; protege al operador ante contacto accidental con $220\text{ V}_{\text{CA}}$. |

### Decisión profesional justificada
Se selecciona una **estrategia escalonada centrada en la Alternativa C (Pulsera antiestática con resistor de seguridad de $1\text{ M}\Omega$ + tapete disipativo conectado a barra equipotencial + sistema electrónico de alerta ambiental con bloqueo por debajo de $30\text{ \% HR}$)** como medida inmediata obligatoria, complementada en una segunda etapa presupuestaria por la **estabilización higrométrica del sistema HVAC en $45\text{ \% HR}$** (Alternativa B).

**Justificación técnica y económica:** El análisis físico demuestra que el evento crítico ocurre exclusivamente durante intervenciones humanas con gabinetes abiertos en días secos invernales. Implementar la Alternativa C resuelve de raíz el problema equipotencial (reduciendo $V_{\text{cuerpo}}$ por debajo del umbral de daño de $100\text{ V}$ en menos de $0,5\text{ ms}$) con una fracción mínima del presupuesto hospitalario, sin interrumpir la disponibilidad de los servidores clínicos y garantizando simultáneamente la seguridad eléctrica del técnico frente a fallas de aislación en red de $220\text{ V}_{\text{CA}}$.

---

## 7.3 Riesgos de implementación e impacto ambiental
* **Riesgos técnicos y de seguridad eléctrica:** El principal riesgo consiste en utilizar una pulsera sin resistor limitador interno de $1\text{ M}\Omega$ o conectarla a una tierra defectuosa; si el técnico tocara accidentalmente un conductor energizado a $220\text{ V}_{\text{CA}}$, una conexión directa a tierra provocaría una electrocución fatal. Asimismo, un falso contacto en el conector banana anularía la protección sin advertencia si no se realiza la prueba de continuidad previa al ingreso.
* **Impacto ambiental y gestión de residuos (RAEE):** Evitar fallas prematuras en placas madre, módulos ECC y controladoras RAID reduce directamente la generación de residuos de aparatos eléctricos y electrónicos (RAEE) hospitalarios y la huella de carbono asociada a la fabricación y transporte de repuestos importados. En caso de optar en el futuro por humidificación evaporativa o ultrasónica, debe evitarse el uso de aditivos químicos biocidas volátiles que puedan corroer contactos dorados o afectar la calidad del aire interior.

---

# SECCIÓN 8. CONCLUSIONES, LIMITACIONES Y BIBLIOGRAFÍA

## 8.1 Conclusiones
1. **Validación cuantitativa del diagnóstico:** La modelización física demostró que una condición invernal de baja humedad relativa ($HR < 30\text{ \%}$) permite acumular potenciales electrostáticos del orden de $2,0\text{ kV}$ sobre el cuerpo humano ($C \approx 150\text{ pF}$), superando ampliamente la rigidez dieléctrica de los óxidos de puerta de los circuitos integrados modernos ($< 100\text{ V}$).
2. **Eficacia del control resistivo de descarga:** Incorporar una resistencia serie de $1,0\text{ M}\Omega$ (Eje II) controla la constante de tiempo de descarga en $\tau = 0,15\text{ ms}$ y limita la corriente pico a $2,0\text{ mA}$, logrando tanto la integridad de los semiconductores como la seguridad fisiológica del operador.
3. **Necesidad de protección multinivel (conducida y radiada):** El acoplamiento magnético por variación rápida de corriente (Eje III) y la radiación electromagnética de banda ancha del arco ESD (Eje IV) confirman que el blindaje de gabinetes, la continuidad de masa y los diodos de sujeción rápida TVS en puertos de E/S (Eje V) son indispensables para evitar reinicios lógicos y errores silenciosos de memoria.
4. **Integración hardware-software:** La simulación del nodo sensor con ADC de $10\text{ bits}$ (Eje V) verificó que es viable automatizar una alerta temprana preventiva con error de cuantización inferior al $0,1\text{ \%}$, trasladando los principios de la Física II a una solución de ingeniería aplicable en sistemas de información reales.

## 8.2 Limitaciones del modelo y trabajos futuros
* **Simplificaciones del modelo:** El análisis electrostático asumió una capacitancia corporal constante de $150\text{ pF}$ (modelo HBM estándar), sin considerar variaciones por postura, proximidad a racks metálicos ni geometría tridimensional exacta de la sala. De igual modo, el transductor en la simulación de Tinkercad se modeló como idealmente lineal sin histéresis térmica.
* **Trabajos futuros:** Como extensión práctica se propone validar en campo la resistencia a tierra del piso y de las pulseras mediante un megóhmetro calibrado según norma ANSI/ESD S20.20, e integrar el nodo sensor desarrollado en el Eje V con el sistema de monitoreo institucional del hospital (vía protocolo SNMP o MQTT) para registrar históricos de humedad y temperatura en tiempo real.

## 8.3 Referencias bibliográficas (Formato APA 7)
* ANSI/ESD Association. (2021). *ANSI/ESD S20.20-2021: Protection of Electrical and Electronic Parts, Assemblies and Equipment (Excluding Electrically Initiated Explosive Devices)*. ESD Association.
* Halliday, D., Resnick, R., & Walker, J. (2018). *Fundamentos de Física* (10.ª ed., Vol. 2). Grupo Editorial Patria.
* JEDEC Solid State Technology Association. (2014). *JS-001-2014: Electrostatic Discharge Sensitivity Testing - Human Body Model (HBM)*. JEDEC & ESDA Joint Standard.
* Ott, H. W. (2009). *Electromagnetic Compatibility Engineering*. John Wiley & Sons.
* Sadiku, M. N. O. (2018). *Elementos de electromagnetismo* (7.ª ed.). Oxford University Press.
* Serway, R. A., & Jewett, J. W. (2019). *Física para ciencias e ingeniería* (10.ª ed., Vol. 2). Cengage Learning.

---

## ANEXO V — DECLARACIÓN DE AUTORÍA Y USO DE INTELIGENCIA ARTIFICIAL

Quienes suscriben declaran que el presente informe técnico y su correspondiente repositorio de proceso constituyen una producción original elaborada para la Actividad de Evaluación N.º 4 de la asignatura Física II.

En cumplimiento con las pautas de integridad académica de la cátedra, se informa que se utilizaron herramientas de Inteligencia Artificial generativa (Claude y Google Gemini) exclusivamente como asistentes de apoyo metodológico para: (a) estructuración de plantillas en Markdown del portafolio en GitHub, (b) verificación cruzada de despejes algebraicos y sintaxis en C++ para la simulación del microcontrolador, y (c) revisión de estilo y redacción técnica. Todos los planteos físicos, criterios de ingeniería, selección de parámetros, ejecución de simulaciones en PhET, Falstad y Tinkercad, validación de resultados y decisiones profesionales fueron realizados, verificados y defendidos de manera autónoma por los autores.
