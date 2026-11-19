# Eje IV — Corriente Alterna y Ondas Electromagnéticas
**Caso:** F1-01 — Sala de servidores de un hospital escuela: fallas por descarga electrostática  
**Asignatura:** Física II — Ingeniería en Sistemas de Información (UCP)  
**Versión:** v1  

---

## (a) Fenómeno físico identificado y leyes que lo describen

Aunque la descarga electrostática (ESD) se origina en una acumulación de carga estática (Eje I) y se drena como una corriente transitoria (Eje II), su **variación extremadamente rápida en el tiempo** (flancos de subida del orden de sub-nanosegundos a nanosegundos) genera un espectro de componentes de alta frecuencia que se comportan como señales de corriente alterna de banda ancha y dan lugar a **radiación electromagnética**.

Las leyes físicas fundamentales que rigen este fenómeno son:

1. **Ecuaciones de Maxwell (forma integral / conceptual en el vacío y aire):**
   - **Ley de Faraday-Maxwell:** Un campo magnético variable en el tiempo induce un campo eléctrico rotacional ($\oint \vec{E} \cdot d\vec{l} = -\frac{d\Phi_B}{dt}$).
   - **Ley de Ampère-Maxwell:** Una corriente de conducción y una corriente de desplazamiento ($\varepsilon_0 \frac{d\Phi_E}{dt}$) generan un campo magnético rotacional ($\oint \vec{B} \cdot d\vec{l} = \mu_0 I + \mu_0 \varepsilon_0 \frac{d\Phi_E}{dt}$).
   - El acoplamiento mutuo entre $\vec{E}(t)$ y $\vec{B}(t)$ variables produce una **onda electromagnética** que se propaga a la velocidad de la luz $c = \frac{1}{\sqrt{\mu_0 \varepsilon_0}} \approx 3,00 \times 10^8\text{ m/s}$ (Young & Freedman, 2009, Cap. 32, pp. 1093–1097).
2. **Relación frecuencia – longitud de onda:**
   $$\lambda = \frac{c}{f}$$
3. **Ancho de banda equivalente de un pulso transitorio (aproximación de tiempo de subida):**
   Para un pulso con tiempo de subida $t_r$ (entre el 10 % y el 90 % de su amplitud pico), el contenido espectral significativo se extiende hasta una frecuencia máxima efectiva (frecuencia de corte o *knee frequency*):
   $$f_{\max} \approx \frac{0,35}{t_r}$$
4. **Condición de radiación eficiente (criterio de antena):**
   Un conductor, estructura metálica o cable de red actúa como antena radiante o receptora eficiente cuando su longitud física $L$ es comparable a una fracción significativa de la longitud de onda ($\lambda$), típicamente a partir de $L \ge \frac{\lambda}{10}$ (y máxima eficiencia en resonancia de cuarto de onda $L = \frac{\lambda}{4}$ o media onda $L = \frac{\lambda}{2}$).

---

## (b) Magnitudes y datos adoptados

| Magnitud / Parámetro | Símbolo | Valor adoptado | Fuente / Justificación |
| :--- | :---: | :---: | :--- |
| Velocidad de propagación en aire | $c$ | $3,00 \times 10^8\text{ m/s}$ | Constante física fundamental (Young & Freedman, 2009, p. 1097). |
| Tiempo de subida del pulso ESD (Descarga por Contacto) | $t_r$ | $0,8\text{ ns}$ ($0,8 \times 10^{-9}\text{ s}$) | Parámetro normalizado de forma de onda ESD según IEC 61000-4-2 ($0,7\text{ ns}$ a $1\text{ ns}$). |
| Tiempo de subida alternativo (Descarga en Aire / escenario lento) | $t_{r,\text{lento}}$ | $5,0\text{ ns}$ ($5,0 \times 10^{-9}\text{ s}$) | Rango representativo de descargas en aire de menor pendiente (estimación técnica). |
| Longitud típica de latiguillos UTP (*patch cords*) en el rack | $L_{\text{patch}}$ | $1,5\text{ m}$ | Dato típico de cableado estructurado en gabinetes de servidores. |
| Altura estándar de un rack de servidores (42U) | $H_{\text{rack}}$ | $2,0\text{ m}$ | Dimensión mecánica estándar de gabinetes de telecomunicaciones (EIA-310). |
| Frecuencia fundamental de operación de Ethernet 1000BASE-T | $f_{\text{ETH}}$ | $125\text{ MHz}$ (ancho de banda efectivo hasta $100\text{ MHz}$ por par) | Especificación IEEE 802.3ab (Gigabit Ethernet sobre par trenzado). |

---

## (c) Resolución cuantitativa

### 1. Frecuencia máxima del espectro del pulso ESD ($f_{\max}$)
Aplicando la relación entre tiempo de subida y ancho de banda espectral para el pulso normalizado ($t_r = 0,8\text{ ns}$):

$$f_{\max} = \frac{0,35}{t_r} = \frac{0,35}{0,8 \times 10^{-9}\text{ s}} = 4,375 \times 10^8\text{ Hz} = 437,5\text{ MHz}$$

Para el escenario de descarga más lenta ($t_{r,\text{lento}} = 5,0\text{ ns}$):

$$f_{\max,\text{lento}} = \frac{0,35}{5,0 \times 10^{-9}\text{ s}} = 7,0 \times 10^7\text{ Hz} = 70\text{ MHz}$$

### 2. Longitud de onda asociada a la frecuencia máxima ($\lambda_{\min}$)
Para $f_{\max} = 437,5\text{ MHz}$:

$$\lambda_{\min} = \frac{c}{f_{\max}} = \frac{3,00 \times 10^8\text{ m/s}}{4,375 \times 10^8\text{ Hz}} \approx 0,686\text{ m} \quad (68,6\text{ cm})$$

### 3. Evaluación de eficiencia de radiación / recepción en la sala de servidores
Calculamos el umbral mínimo de longitud para radiación/recepción eficiente ($\lambda_{\min}/10$) y la longitud de resonancia de cuarto de onda ($\lambda_{\min}/4$):

$$L_{\text{umbral}} = \frac{\lambda_{\min}}{10} = \frac{0,686\text{ m}}{10} = 0,0686\text{ m} \quad (6,86\text{ cm})$$

$$L_{\text{res},\lambda/4} = \frac{\lambda_{\min}}{4} = \frac{0,686\text{ m}}{4} = 0,1715\text{ m} \quad (17,15\text{ cm})$$

**Interpretación de resultados:**
- El pulso de ESD no es una corriente continua lenta: contiene energía espectral significativa desde bajas frecuencias hasta **$437,5\text{ MHz}$** (banda VHF/UHF).
- A esa frecuencia, la longitud de onda es de apenas **$68,6\text{ cm}$**. Cualquier conductor o ranura metálica mayor a **$6,9\text{ cm}$** (como un *patch cord* de $1,5\text{ m}$, el brazo del técnico, una herramienta metálica o la apertura de la puerta de un rack de $2\text{ m}$) supera ampliamente el umbral $\lambda/10$ y actúa como **antena emisora y receptora eficiente**.
- Además, el espectro de la descarga ($0$ a $437,5\text{ MHz}$) solapa directamente la banda de trabajo de la interfaz Ethernet ($100\text{--}125\text{ MHz}$), lo que explica la inyección de ruido radiado directamente en los puertos de la placa de red (NIC) incluso sin contacto directo sobre el conector RJ45.

---

## (d) Características influyentes y efectos

1. **Tiempo de subida del pulso ($t_r$):** Es el factor determinante. A menor tiempo de subida (descargas metálicas rápidas o baja impedancia de contacto), mayor es el contenido de alta frecuencia ($f_{\max} \propto 1/t_r$) y más corta es la longitud de onda, haciendo que pistas cortas de circuito impreso (PCB) se comporten como antenas receptoras.
2. **Aberturas y ranuras en gabinetes (Jaula de Faraday imperfecta):** Un rack metálico cerrado atenúa el campo electromagnético incidente; sin embargo, si la puerta está abierta durante el mantenimiento (condición exacta reportada en el caso F1-01) o presenta ranuras de ventilación mayores a $\lambda/10 \approx 6,9\text{ cm}$, el blindaje electromagnético pierde efectividad y las ondas penetran hacia las placas de red y módulos de memoria.
3. **Acoplamiento con otros ejes y entorno:**
   - Condiciona directamente al **Eje V**, ya que el frente de onda de alta frecuencia exige que los dispositivos de protección en la entrada de la placa de red (diodos TVS) tengan tiempos de respuesta menores a $1\text{ ns}$ y baja inductancia parásita de montaje.
   - Desde el punto de vista de **compatibilidad electromagnética (EMC)**, el evento genera interferencia electromagnética radiada (EMI) que puede corromper tramas de datos o provocar reinicios espúreos en equipamiento clínico conectado en red dentro del hospital escuela.

---

## (e) Consecuencia para el Sistema de Información

1. **Continuidad de puesta a tierra equipotencial en múltiples puntos:** Para altas frecuencias ($>100\text{ MHz}$), un cable largo de tierra presenta alta reactancia inductiva ($X_L = 2\pi f L$) y deja de ser equipotencial. Se exige vincular todas las partes metálicas del rack (puertas, paneles laterales, bastidor) mediante trenzas cortas de cobre de baja inductancia a la barra de tierra de telecomunicaciones (norma ANSI/TIA-607).
2. **Protocolo operativo de gabinete cerrado y cableado apantallado:** Mantener cerradas las puertas metálicas de los racks fuera de las intervenciones puntualizadas y utilizar cableado estructurado apantallado (**F/UTP o S/FTP Cat6A**) con conectores RJ45 blindados correctamente aterrizados en ambos extremos (o según topología del fabricante) para mitigar el acoplamiento radiado sobre los pares diferenciales.

---

## (f) Fundamentación bibliográfica (APA 7)

- Young, H. D., & Freedman, R. A. (2009). *Física universitaria con física moderna* (12.ª ed., Vol. 2, Cap. 32: Ondas electromagnéticas, pp. 1093–1105). Pearson Educación.
- International Electrotechnical Commission. (2008). *IEC 61000-4-2: Electromagnetic compatibility (EMC) — Part 4-2: Testing and measurement techniques — Electrostatic discharge immunity test* (2.ª ed.). IEC.
