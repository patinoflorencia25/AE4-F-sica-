# P2 – Memoria de cálculo · Eje II – Fenómenos eléctricos estacionarios (v2)
Caso: F1-01 (sala de servidores de un hospital escuela: fallas por ESD) · Fecha real: 2026-11-18
Estado: REVISAR (desarrollado; falta que Florencia lo revise y pueda explicarlo)
Corresponde a: sección 3 del informe (`P6_borradores/informe_v3.md`) · Versión anterior: `versiones/eje2_v1_plantilla.md`
Notación (igual que el libro y el Eje I): U = energía, E = campo eléctrico, C = 150 pF y V₀ = 15 kV (hipótesis adoptadas en el Eje I).
Procedencia: **[CASO]** dato del Banco · **[NORMA]** valor de una norma, leído a través de una fuente secundaria · **[FABRICANTE]** hoja de datos · **[LIBRO]** Young y Freedman (2009) · **[HIPÓTESIS]** valor que adoptamos · **[CALCULADO]**

## 1. Qué fenómeno ocurre y qué leyes lo explican
En el Eje I el cuerpo quedó cargado como un capacitor (C = 150 pF, V₀ = 15 kV). Ahora la pregunta es **¿por dónde y cuán rápido se descarga?** Eso depende de la resistencia del camino que recorre la carga: persona → calzado → piso → tierra. Si la resistencia es alta, la carga sale despacio y con poca corriente; si es muy baja, sale de golpe y con mucha corriente.

Leyes que usamos (Young y Freedman, 2009):
- **Ley de Ohm:** V = I·R (p. 853).
- **Resistencia de un conductor:** R = ρ·L/A (ecuación 25.10, p. 853); ρ del cobre = 1,72 × 10⁻⁸ Ω·m (tabla 25.1, p. 851).
- **Resistencias en serie:** se suman (sección 26.1, pp. 883–885).
- **Potencia en una resistencia:** P = V·I = I²·R = V²/R (sección 25.5, pp. 863–864).
- **Descarga de un capacitor por una resistencia (circuito R-C):** q = Q₀·e^(−t/RC) (ecuación 26.16) y constante de tiempo τ = R·C (ecuación 26.14), pp. 897–899. Como v = q/C, la tensión también decae así: **v(t) = V₀·e^(−t/RC)**.

## 2. Qué significa cada magnitud (en simple)
| Símbolo | Nombre | Qué es | Unidad |
|---|---|---|---|
| R | resistencia | cuánto "frena" el camino al paso de la corriente | ohm (Ω); 1 MΩ = 10⁶ Ω; 1 GΩ = 10⁹ Ω |
| I | corriente | cantidad de carga que pasa por segundo | ampere (A) |
| τ = R·C | constante de tiempo | tiempo en que la tensión cae a 1/e (≈ 37 %) de su valor inicial | segundo (s) (Ω·F = s) |
| P | potencia | energía por segundo que se convierte en calor en la resistencia | watt (W) |
| R_t | resistencia total del camino | suma de calzado + piso (+ conductor de tierra) | Ω |

## 3. La resistencia del piso: qué sabemos y qué NO sabemos
**El caso F1-01 NO da la resistencia del piso técnico del hospital. Tampoco se midió. Por eso no la inventamos ni la presentamos como dato del hospital.** Lo único que da el caso es la resistencia del calzado: 10⁶ a 10⁹ Ω [CASO].

### 3.1 Valores de normas (leídos a través de fuentes secundarias; las normas no se consultaron directamente)
| Qué | Valor | Fuente |
|---|---|---|
| Piso conductivo | menor que 1 × 10⁶ Ω | ANSI/ESD STM7.1, vía In Compliance y Desco |
| Piso disipativo | de 1 × 10⁶ a menos de 1 × 10⁹ Ω | ANSI/ESD STM7.1, vía In Compliance |
| Piso conductivo según ASTM F150 | de 2,5 × 10⁴ a 1 × 10⁶ Ω (el límite inferior se fija por seguridad de las personas) | ASTM F150, vía Interference Technology |
| Persona de pie, sistema calzado + piso (ANSI/ESD S20.20, edición 2014) | menor que 1 × 10⁹ Ω **y** tensión corporal al caminar menor que 100 V pico | S20.20-2014, vía In Compliance |
| Mismo sistema, edición 2007 | alcanzaba con menos de 3,5 × 10⁷ Ω | S20.20-2007, vía In Compliance |
| Sistema de pulsera | menor que 3,5 × 10⁷ Ω | S20.20, vía In Compliance y Desco |
| Para salas de servidores | **no hay una norma oficial** que fije la resistencia del piso; se toma como referencia la industria ESD | In Compliance (nota sobre pisos ESD sin norma específica) |
| Puesta a tierra de protección (Argentina) | máximo 40 Ω (AEA 90364-7-771, ed. 2006; antes 10 Ω) | documento AEA 90364-7-771 |
| Puesta a tierra funcional de UPS (Argentina) | no debe superar 10 Ω | AEA 90364-4 (informe técnico 2019, fragmento leído) |
| Recomendación general de resistencia de tierra | 5 Ω o menos (NFPA e IEEE); "no existe un único umbral reconocido por todas las agencias" | Fluke (blog técnico) |

### 3.2 Valores de fabricantes
| Producto | Resistencia indicada | Otros datos |
|---|---|---|
| 3M, vinilo de la serie 8400 (para pisos técnicos) | conductivo: 2,5 × 10⁴ a 1 × 10⁶ Ω; disipativo: 1 × 10⁶ a 1 × 10⁹ Ω | ensayado según STM7.1 y STM97.1 |
| StaticWorx GroundLock Extreme (apto para instalar sobre piso técnico de centros de datos) | de 2,5 × 10⁴ a 1 × 10⁷ Ω | tensión corporal menor que 100 V (STM97.2) |
| Sikafloor-260 ESD (recubrimiento) | de 2,5 × 10⁴ a 1 × 10⁶ Ω a 23 °C y 50 % de humedad | tensión corporal menor que 30 V; dice no depender de la humedad |
| Talonera conductiva (hoja de datos de un distribuidor) | resistencia mínima a tierra de 1 MΩ | |
| Cordón de pulsera típico (ESD S6.1, vía Desco) | 1 MΩ agregado | |

Advertencia sobre las mediciones: la resistencia se mide con 10 V o 100 V; con 500 V da un valor menor, así que un piso que cumple un límite a una tensión puede no cumplirlo a otra (In Compliance).

### 3.3 Hipótesis que adoptamos [HIPÓTESIS]
| Escenario | R_t del camino persona-tierra | Qué representa | Origen |
|---|---|---|---|
| **A: descarga directa (el evento ESD)** | 1,5 kΩ | resistencia del modelo de cuerpo humano al tocar un equipo | onsemi (2023): HBM de 1,5 kΩ |
| **B: piso conductivo + elemento de 1 MΩ** | 2 × 10⁶ Ω | piso en el límite superior de "conductivo" (1 × 10⁶ Ω) + talonera/calzado de 1 MΩ | normas y fabricantes (3.1 y 3.2) |
| **C (valor de referencia que proponemos)** | **3,5 × 10⁷ Ω** | límite normativo de la pulsera y del sistema calzado + piso en la edición 2007 | norma (3.1) |
| **D: cota superior** | 1 × 10⁹ Ω | límite máximo de S20.20-2014 para calzado + piso, y extremo alto del calzado del caso | norma (3.1) y caso |

**Por qué proponemos C (3,5 × 10⁷ Ω) como valor de referencia:**
1. Es un límite normativo conocido de verificación, así que sirve para decir "si el camino de descarga estuviera justo en el límite, ¿qué pasaría?".
2. Está dentro del rango del calzado del caso (10⁶ a 10⁹ Ω) y entre el piso conductivo y el límite de 10⁹ Ω.
3. **No es la resistencia del piso del hospital**: es una referencia de cálculo. Para saber la resistencia real habría que medirla (por ejemplo, con un megóhmetro según STM7.1 / STM97.1). **No se midió.**
Los escenarios B y D se calculan al lado para mostrar cómo cambia todo.

## 4. Cálculos

### 4.1 Resistencia total del camino (resistencias en serie)
**Qué buscamos:** la resistencia que "ve" la carga desde el cuerpo hasta la tierra.
**Fórmula:** R_t = R_calzado + R_piso (cuando la carga debe pasar por una después de la otra, las resistencias se suman).
**Ejemplos con datos del caso y de las fuentes:**
- Calzado del extremo bajo del caso + piso en el límite conductivo: R_t = 1 × 10⁶ Ω + 1 × 10⁶ Ω = **2 × 10⁶ Ω** (escenario B).
- Calzado del extremo alto del caso + el mismo piso conductivo: R_t = 1 × 10⁹ Ω + 1 × 10⁶ Ω = **1,001 × 10⁹ Ω**.
**Interpretación:** si el calzado vale 10⁹ Ω, esa resistencia domina y ya está en el límite máximo de la norma. **Un piso conductivo solo ayuda si el calzado también es conductor o disipativo.** Esto es clave para la decisión profesional (sección 7 del informe).

### 4.2 Constante de tiempo τ = R·C
**Qué buscamos:** la escala de tiempo de la descarga.
**Fórmula:** τ = R·C (ecuación 26.14). **Control de unidades:** Ω · F = (V/A)(C/V) = C/A = s ✔.
**Reemplazo con C = 150 pF = 150 × 10⁻¹² F:**
| Escenario | R | τ = R·C |
|---|---|---|
| A (descarga directa) | 1,5 × 10³ Ω | 1,5 × 10³ · 150 × 10⁻¹² = **2,25 × 10⁻⁷ s = 225 ns** |
| B | 2 × 10⁶ Ω | 2 × 10⁶ · 150 × 10⁻¹² = **3 × 10⁻⁴ s = 0,30 ms** |
| C | 3,5 × 10⁷ Ω | 3,5 × 10⁷ · 150 × 10⁻¹² = **5,25 × 10⁻³ s = 5,25 ms** |
| D | 1 × 10⁹ Ω | 1 × 10⁹ · 150 × 10⁻¹² = **0,15 s = 150 ms** |
**Interpretación:** pasar de la descarga directa (225 ns) al camino controlado es "estirar" la descarga: 0,30 ms / 225 ns ≈ 1 300 veces (escenario B), 5,25 ms / 225 ns ≈ 23 000 veces (C) y 150 ms / 225 ns ≈ 670 000 veces (D).

### 4.3 Tiempo para bajar a una tensión segura
**Qué buscamos:** cuánto tarda el cuerpo en bajar de V₀ = 15 kV a una tensión objetivo.
**Despeje:** de v(t) = V₀·e^(−t/RC) se obtiene t = R·C·ln(V₀ / v).
**Dos tensiones objetivo:** 100 V (valor que fija S20.20 para la tensión corporal, vía In Compliance) y 365 V (umbral de daño calculado en el Eje I).
- ln(15 000 / 100) = ln 150 = 5,01 → t₁₀₀ = 5,01 · τ
- ln(15 000 / 365) = 3,72 → t₃₆₅ = 3,72 · τ
| Escenario | τ | t para llegar a 365 V | t para llegar a 100 V |
|---|---|---|---|
| B | 0,30 ms | 1,1 ms | 1,5 ms |
| C | 5,25 ms | 19,5 ms | 26,3 ms |
| D | 150 ms | 0,56 s | 0,75 s |
**Interpretación:** con el escenario B el cuerpo se descarga en un par de milisegundos; con D hace falta casi un segundo, y en ese tiempo la persona sigue caminando y sigue cargándose. La comparación con el tiempo entre pasos (décimas de segundo; es una hipótesis de orden de magnitud, sin fuente) sugiere que en D el cuerpo no alcanza a descargarse entre paso y paso. **Esto es una estimación del modelo, no una medición.**

### 4.4 Corriente inicial de la descarga
**Fórmula:** I₀ = V₀ / R (ley de Ohm, p. 853). **Unidades:** V/Ω = A ✔.
| Escenario | I₀ = 15 000 V / R | Comparada con A (10 A) |
|---|---|---|
| A | 15 000 / 1 500 = **10 A** | — |
| B | 15 000 / 2 × 10⁶ = **7,5 mA** | 1 333 veces menos |
| C | 15 000 / 3,5 × 10⁷ = **0,429 mA** | 23 333 veces menos |
| D | 15 000 / 1 × 10⁹ = **15 µA** | 666 667 veces menos |
**Interpretación:** la resistencia del camino no cambia cuánta energía hay (16,9 mJ, Eje I), sino **con qué rapidez y con qué corriente sale**.

### 4.5 Potencia máxima y control con la energía del Eje I
**Fórmula:** P₀ = V₀² / R (pp. 863–864). **Unidades:** V²/Ω = W ✔.
| Escenario | P₀ = (15 000 V)² / R |
|---|---|
| A | 2,25 × 10⁸ / 1,5 × 10³ = **150 kW** |
| B | 2,25 × 10⁸ / 2 × 10⁶ = **112,5 W** |
| C | 2,25 × 10⁸ / 3,5 × 10⁷ = **6,43 W** |
| D | 2,25 × 10⁸ / 1 × 10⁹ = **0,225 W** |
**Control de coherencia (conservación de la energía):** la potencia decae como e^(−2t/τ), así que la energía total disipada es P₀·τ/2. Para el escenario A: 150 000 W · 225 × 10⁻⁹ s / 2 = 1,6875 × 10⁻² J = **16,875 mJ**, que coincide con la energía del Eje I (½ · C · V₀²) ✔. Para B, C y D da lo mismo (16,875 mJ): cambia la potencia y el tiempo, no la energía total.
**Interpretación:** en el escenario A hay 150 kW durante unos cientos de nanosegundos; en los demás, entre cientos de watts y fracciones de watt durante milisegundos o décimas de segundo. El pico de A es el tipo de evento que el modelo HBM usa para ensayar daños en circuitos integrados; en un camino controlado la potencia es mucho menor. (No se calculó cuánto soporta un componente concreto.)
**Límite:** esto no dice cuánta energía llega al componente. Eso depende del camino interno del equipo, que el caso no describe.

### 4.6 Resistencia del conductor de tierra y del sistema de puesta a tierra
**Fórmula:** R = ρ·L/A (ecuación 25.10).
**Datos:** ρ del cobre = 1,72 × 10⁻⁸ Ω·m [LIBRO]; L = 10 m [HIPÓTESIS]; conductor de unión de 6 AWG como mínimo (TIA-942, vía Syscom; el área de 13,3 mm² sale del diámetro de 4,115 mm de la tabla AWG: A = π · (4,115 × 10⁻³ / 2)² = 1,33 × 10⁻⁵ m²) [verificar en una hoja de datos].
**Reemplazo:** R = 1,72 × 10⁻⁸ Ω·m · 10 m / 1,33 × 10⁻⁵ m² = **0,0129 Ω**.
**Comparación:** frente a los 2 × 10⁶ Ω del escenario B es una fracción de 6,5 × 10⁻⁹ (despreciable); frente a 3,5 × 10⁷ Ω, de 3,7 × 10⁻¹⁰. Aun sumando una resistencia de tierra de 5 Ω (recomendación general), 5 / 2 × 10⁶ = 2,5 × 10⁻⁶: despreciable.
**Interpretación:** **el cable y la jabalina de tierra no limitan la descarga ESD; la limitan el calzado y el piso.** La puesta a tierra importa por otro motivo: la seguridad ante fallas de la instalación (por eso la AEA fija máximos de 40 Ω y 10 Ω). Los valores de 5, 10 y 40 Ω son límites o recomendaciones, no mediciones del hospital.

### 4.7 Complemento (no lo pide la consigna): por qué hay un límite inferior de resistencia
Si un piso fuera demasiado conductor, una persona que toque un conductor energizado de 220 V (tensión de red; hipótesis para este cálculo) tendría poco freno. Con el límite inferior 2,5 × 10⁴ Ω de ASTM F150: I = V / R = 220 V / 2,5 × 10⁴ Ω = **8,8 mA**. Por eso los pisos ESD no deben tener resistencia demasiado baja. No se compara con umbrales fisiológicos porque no se verificó una fuente confiable para eso; es solo la cuenta de Ohm. Si no te sirve, se descarta.

## 5. Interpretación física (para explicarlo con palabras propias)
1. La resistencia **no cambia la energía** que guarda el cuerpo; cambia **cuánto tarda en salir** y **con qué corriente**. Es como vaciar un tanque: la cantidad de agua es la misma, pero un caño ancho la tira de golpe y uno angosto la deja salir de a poco.
2. Una descarga directa (1,5 kΩ) dura nanosegundos y llega a 10 A; un camino de megaohms la estira a milisegundos y baja la corriente a miliamperes o menos.
3. La resistencia **del calzado** está en serie con la del piso: si el calzado es muy resistivo, un piso excelente no alcanza.
4. La resistencia **de la tierra** (ohms) es minúscula frente a la del camino ESD (megaohms).

## 6. Qué influye y efectos
- **Humedad:** un piso o recubrimiento común puede conducir menos con aire seco (hipótesis general; no hay una fuente específica leída para esto). Un fabricante (Sika) dice que su producto no depende de la humedad, y los fabricantes miden a 12–50 % de humedad según el ensayo; la resistencia declarada es de laboratorio, no la del hospital.
- **Tensión de medición:** un mismo piso mide menos resistencia a 500 V que a 10 o 100 V.
- **Materiales y geometría:** R aumenta con la longitud del camino y con la resistividad, y baja con la sección (R = ρL/A). Un piso técnico tiene paneles, pedestales y uniones: cada contacto suma resistencia.
- **Envejecimiento, limpieza y ceras** pueden subir la resistencia del piso con el tiempo (por eso hay que verificar periódicamente).
- **Relación con otros ejes:** una descarga rápida (τ chico) tiene corriente alta y variación rápida, lo que importa para el Eje III (campo magnético) y el Eje IV (contenido de alta frecuencia).

## 7. Consecuencia para el sistema de información (decisión de diseño)
- El piso conductivo con puesta a tierra **reduce** la resistencia del camino, pero hay que **verificar el sistema completo calzado + piso** (resistencia y tensión corporal al caminar), no solo el piso.
- Hay que **mantener un límite inferior** de resistencia por seguridad eléctrica.
- La puesta a tierra debe cumplir la norma local; con 5 a 10 Ω el efecto sobre la ESD es despreciable, pero es necesaria para seguridad.
- Esto alimenta la decisión de la sección 7: piso conductivo vs. control de humedad vs. pulsera antiestática.

## 8. Limitaciones
- **No hay resistencia medida del piso del hospital**: los escenarios B, C y D son referencias normativas o de fabricantes, no mediciones.
- Las normas ANSI/ESD, ASTM F150 e IEC 61340 no se consultaron directamente: sus valores vienen de fuentes secundarias (In Compliance, Desco, Interference Technology). Hay que contrastarlos con el texto de la norma si se puede.
- El modelo usa una sola R y un solo C constantes (circuito R-C simple); en la realidad, la resistencia depende de la tensión y de la humedad, y el cuerpo es una distribución de capacitancias.
- No se calculó cuánta energía llega al componente.
- La comparación con el tiempo entre pasos es solo un orden de magnitud.

## 9. Para el coloquio (preguntas posibles)
1. *¿Por qué el valor de 3,5 × 10⁷ Ω?* Es un límite normativo de verificación; lo usamos como referencia, no como dato medido del hospital.
2. *¿La resistencia cambia la energía de la descarga?* No: es siempre ½CV² = 16,9 mJ; cambia la potencia y el tiempo (τ = RC).
3. *¿Por qué no alcanza con un piso conductivo?* Porque el calzado está en serie y suma; si es de 10⁹ Ω, domina.
4. *¿Qué mediría en el hospital?* La resistencia del sistema calzado + piso y la tensión corporal al caminar, con los ensayos STM97.1 y STM97.2.

## 10. Fuentes (ver `P5_fuentes/fuentes.md`)
Young y Freedman (2009), pp. 851, 853, 863–864, 883–885, 897–899 (verificadas en el PDF). Normas y fabricantes: ver tablas 3.1 y 3.2 y P5. onsemi (2023) para la resistencia del modelo de cuerpo humano.

## 11. Historial
| Versión | Fecha real | Qué cambió |
|---|---|---|
| v1 | 2026-11-18 | Plantilla (conservada en `versiones/eje2_v1_plantilla.md`) |
| v2 | 2026-11-18 | Eje II desarrollado: valores normativos, de fabricantes e hipótesis separados; cuatro escenarios; cálculos de R_t, τ, tiempo de descarga, corriente, potencia y conductor de tierra |
