# Ficha de Simulación 3 — Eje V (Elementos de Electrónica: Puente Hardware-Software)
**Caso:** F1-01 — Sala de servidores de un hospital escuela: fallas por descarga electrostática  
**Herramienta:** Tinkercad Circuits (simulación de microcontrolador ATmega328P / Arduino Uno, ADC de 10 bits y lógica de alarma)  
**Enlace nativo al proyecto:** https://www.tinkercad.com/things/gDgBRy89K13/editel?returnTo=%2Fdashboard&sharecode=FqWBZPOgFILbqx6mEN2MSEkGP1gdXMGZWuCFRkOmVik  
**Captura de evidencia:** `sim3_eje5_tinkercad.png`  

---

## (i) Descripción del montaje simulado
Se implementó el subsistema electrónico de monitoreo ambiental propuesto en el Eje V. Un transductor analógico lineal de humedad relativa ($0\text{ V} \rightarrow 0\text{ \% HR}$ a $5,0\text{ V} \rightarrow 100\text{ \% HR}$) ingresa al canal analógico `A0` (ADC de $10\text{ bits}$, $V_{\text{ref}} = 5,0\text{ V}$) del microcontrolador. El firmware en C evalúa el umbral crítico invernal del caso F1-01 ($HR < 30\text{ \%}$), activando una salida digital de bloqueo/alarma (LED rojo en pin `D9`) y reportando la telemetría por puerto serie.

---

## (ii) Tabla de parámetros cargados

| Parámetro | Valor cargado en simulador | Unidad | Observación |
| :--- | :---: | :---: | :--- |
| Tensión de referencia del ADC ($V_{\text{ref}}$) | $5,00$ | $\text{V}$ | Alimentación regulada de placa |
| Resolución del conversor ADC ($N$) | $10$ | $\text{bits}$ | $1024$ niveles discretos ($0$ a $1023$) |
| Rango del sensor simulado | $0,00\text{ a }5,00$ | $\text{V}$ | Equivalente a $0\text{ \%}$ a $100\text{ \% HR}$ |
| Punto de prueba 1: Condición extrema seca | $0,00$ | $\text{V}$ | Corresponde a $HR = 0,0\text{ \%}$ (disparo de alarma) |
| Punto de prueba 2: Umbral crítico de disparo | $1,50$ | $\text{V}$ | Corresponde a $HR = 30,0\text{ \%}$ |
| Punto de prueba 3: Condición segura | $3,90$ | $\text{V}$ | Corresponde a $HR = 78,0\text{ \%}$ (LED verde activo) |
| Resistencias limitadoras de LEDs | $220$ | $\text{ }\Omega$ | Corriente de salida $\approx 13,6\text{ mA}$ por pin |

---

## (iii) Resultados: Analítico vs. Simulado y Error Relativo

| Magnitud evaluada | Resultado Analítico | Resultado Simulado (Monitor Serie) | Error Relativo (%) |
| :--- | :---: | :---: | :---: |
| Código ADC a $HR = 0,0\text{ \%}$ ($V_{\text{in}} = 0,00\text{ V}$) | $0$ | $0$ | $0,00\text{ \%}$ |
| Código ADC en umbral $HR = 30,0\text{ \%}$ ($V_{\text{in}} = 1,50\text{ V}$) | $306,90 \rightarrow 307$ | $307$ | $0,00\text{ \%}$ (discretizado) / $0,03\text{ \%}$ (ideal continuo) |
| Código ADC a $HR = 78,0\text{ \%}$ ($V_{\text{in}} = 3,90\text{ V}$) | $797,94 \rightarrow 798$ | $798$ | $0,00\text{ \%}$ (discretizado) / $0,01\text{ \%}$ (ideal continuo) |
| Estado de salida digital ($HR < 30,0\text{ \%}$) | Alarma ACTIVA (`D9 = HIGH`) | `ALERTA ESD` (`D9` encendido) | $0,00\text{ \%}$ |

---

## (iv) Explicación de la discrepancia
La diferencia mínima ($0,01\text{ \%}$ a $0,03\text{ \%}$ respecto al valor continuo ideal) se debe exclusivamente al **error de cuantización propio de un ADC de $10\text{ bits}$**, cuyo paso mínimo es $\Delta V_{\text{LSB}} = \frac{5,0\text{ V}}{1024} \approx 4,88\text{ mV}$ ($\pm 0,5\text{ LSB} \approx \pm 0,05\text{ \% HR}$). Asimismo, el simulador asume una fuente de referencia ideal de $5,00\text{ V}$ sin ruido térmico ni caída por carga en los reguladores, lo cual en una implementación física real se mitiga mediante un capacitor de desacople de $100\text{ nF}$ en el pin `AREF` y promediado móvil de muestras en el firmware.
