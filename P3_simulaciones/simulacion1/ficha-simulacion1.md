# P3 – Simulación 1 (v2: propuesta de diseño, NO ejecutada)
Creada: 2026-11-18 · Estado: PENDIENTE (preparada; sin resultados de simulación)
Requisito cubierto: Eje II (descarga R-C). Versión anterior: `ficha-simulacion1_v1_plantilla.md`.

| Campo | Contenido |
|---|---|
| Fenómeno a verificar | Descarga de un capacitor de 150 pF, cargado a 15 kV, por una resistencia (escenario C del Eje II) |
| Objetivo | Comprobar que la tensión decae según v(t) = V₀·e^(−t/RC) y que τ = R·C |
| Herramienta (a decidir) | Falstad Circuit Simulator o QUCS-S, ambas gratuitas. Hay que **comprobar** que la herramienta permita partir con el capacitor cargado (tensión inicial) y que acepte 15 kV; si no, usar una fuente de 15 kV con un interruptor |
| Circuito o modelo | Capacitor C en serie con resistencia R; el capacitor parte con V₀. Se mide la tensión en el capacitor en función del tiempo |
| Parámetros | C = 150 pF · R = 3,5 × 10⁷ Ω · V₀ = 15 kV · tiempo de simulación 0 a 30 ms |
| Cálculo analítico (resultados esperados) | τ = R·C = 5,25 ms · v(τ) = V₀·e⁻¹ = 5 518 V · v(2τ) = 2 030 V · v(26,3 ms) = 100 V · corriente inicial I₀ = V₀/R = 0,429 mA |
| Resultado de la simulación | (solo se completa después de ejecutarla) |
| Comparación | |
| Error relativo % (= valor absoluto de (simulado − analítico) ÷ analítico × 100) | |
| Captura de pantalla (archivo) | |
| Archivo nativo / enlace del proyecto | |
| Limitaciones del modelo | R y C constantes e ideales; no incluye humedad, geometría del cuerpo ni capacitancias parásitas |
| Fecha real de ejecución | |
| Variante opcional | R = 2 × 10⁶ Ω (τ = 0,30 ms) y R = 10⁹ Ω (τ = 150 ms) para comparar escenarios |

Nota para el informe: el error esperado es muy chico porque el simulador usa la misma ecuación; si el error es 0, hay que decirlo y explicarlo (como en el informe de referencia de Braian), y no inventar una diferencia.
