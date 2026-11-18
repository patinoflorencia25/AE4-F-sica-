# P4 – Registro de decisiones
Mínimo exigido: 5 entradas fechadas. Se registran solo decisiones realmente tomadas, con su fecha real.

| N.º | Fecha real | Problema | Alternativas consideradas | Decisión | Alternativa descartada | Justificación |
|---|---|---|---|---|---|---|
| 1 | 2026-11-18 | Qué valores adoptar dentro de los rangos del caso para el Eje I (C, V, E_falla) | (a) valores centrales de cada rango; (b) valores del extremo más favorable; (c) valores del extremo más desfavorable | Adoptar C = 150 pF, V = 15 kV y E_falla = 10 µJ (caso más desfavorable), aceptado por Florencia el 2026-11-18 | Valores centrales como valor principal | Un diagnóstico de protección contra ESD se dimensiona con el peor caso. El cálculo muestra además que la conclusión no depende de esta elección (ver decisión 2). Pendiente: Florencia revisa y confirma en sus palabras |
| 2 | 2026-11-18 | Cómo mostrar que la elección de valores no condiciona la conclusión | (a) usar solo un valor; (b) comparar contra todo el rango | Calcular la energía en una grilla de 9 combinaciones (C: 100, 125, 150 pF; V: 2, 8,5, 15 kV) y los umbrales de tensión | Usar un solo valor sin comparar | La consigna pide explicitar hipótesis y su validez; la grilla muestra que en todas las combinaciones E supera 100 µJ (ver P2 Eje I, sección 6) |
| 3 | 2026-11-18 | La resistencia del piso técnico del hospital no figura en el caso | (a) inventar un valor; (b) usar valores de normas y fabricantes como escenarios; (c) dejar el Eje II sin cálculo | Usar escenarios con valores normativos y de fabricantes, sin presentarlos como medición del hospital (pedido de Florencia, 2026-11-18) | Inventar un valor de resistencia del piso | La consigna exige diferenciar datos del caso, fuentes e hipótesis; no hay medición disponible |
| 4 | 2026-11-18 | Qué valor de resistencia total del camino usar como referencia principal en el Eje II | (a) 2×10⁶ Ω (piso conductivo + talonera de 1 MΩ); (b) 3,5×10⁷ Ω (límite normativo de verificación); (c) 1×10⁹ Ω (cota superior) | PROPUESTA de Claude, pendiente de confirmación de Florencia: referencia 3,5×10⁷ Ω, con los escenarios de 2×10⁶ y 1×10⁹ Ω calculados al lado y 1,5 kΩ para la descarga directa | Usar solo 1×10⁹ Ω como único valor | 3,5×10⁷ Ω es un límite de verificación conocido y está dentro del rango del calzado del caso; los otros dos muestran los extremos |

## Uso de IA (para la declaración del Anexo V)
Registrar aquí, con fecha real, qué tareas fueron asistidas por IA y qué se verificó por cuenta propia.
| Fecha real | Tarea asistida por IA | Qué verificó la estudiante |
|---|---|---|
| 2026-11-18 | Lectura de la consigna y del Banco; armado de la estructura del repositorio y de las plantillas | |
| 2026-11-18 | Búsqueda de fuentes (onsemi AND9059/D, NASA NEPP 2020, In Compliance Magazine), cálculos con Python para controlar la aritmética, redacción de la memoria del Eje I y del borrador del informe | Pendiente de completar por Florencia: qué revisó, qué recalculó a mano y qué cambió |
| 2026-11-18 | Búsqueda de normas y fichas técnicas de pisos y puesta a tierra, verificación de ecuaciones en el PDF del libro, cálculos con Python y redacción de la memoria del Eje II | Pendiente de completar por Florencia: qué revisó y recalculó a mano |
