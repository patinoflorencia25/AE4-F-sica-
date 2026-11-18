# P4 – Registro de decisiones
Mínimo exigido: 5 entradas fechadas. Se registran solo decisiones realmente tomadas, con su fecha real.

| N.º | Fecha real | Problema | Alternativas consideradas | Decisión | Alternativa descartada | Justificación |
|---|---|---|---|---|---|---|
| 1 | 2026-11-18 | Qué valores adoptar dentro de los rangos del caso para el Eje I (C, V, E_falla) | (a) valores centrales de cada rango; (b) valores del extremo más favorable; (c) valores del extremo más desfavorable | Adoptar C = 150 pF, V = 15 kV y E_falla = 10 µJ (caso más desfavorable), aceptado por Florencia el 2026-11-18 | Valores centrales como valor principal | Un diagnóstico de protección contra ESD se dimensiona con el peor caso. El cálculo muestra además que la conclusión no depende de esta elección (ver decisión 2). Pendiente: Florencia revisa y confirma en sus palabras |
| 2 | 2026-11-18 | Cómo mostrar que la elección de valores no condiciona la conclusión | (a) usar solo un valor; (b) comparar contra todo el rango | Calcular la energía en una grilla de 9 combinaciones (C: 100, 125, 150 pF; V: 2, 8,5, 15 kV) y los umbrales de tensión | Usar un solo valor sin comparar | La consigna pide explicitar hipótesis y su validez; la grilla muestra que en todas las combinaciones E supera 100 µJ (ver P2 Eje I, sección 6) |

## Uso de IA (para la declaración del Anexo V)
Registrar aquí, con fecha real, qué tareas fueron asistidas por IA y qué se verificó por cuenta propia.
| Fecha real | Tarea asistida por IA | Qué verificó la estudiante |
|---|---|---|
| 2026-11-18 | Lectura de la consigna y del Banco; armado de la estructura del repositorio y de las plantillas | |
| 2026-11-18 | Búsqueda de fuentes (onsemi AND9059/D, NASA NEPP 2020, In Compliance Magazine), cálculos con Python para controlar la aritmética, redacción de la memoria del Eje I y del borrador del informe | Pendiente de completar por Florencia: qué revisó, qué recalculó a mano y qué cambió |
