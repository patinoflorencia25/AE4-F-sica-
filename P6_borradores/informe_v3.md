# Informe Técnico Integrador – borrador v3
Caso F1-01 · Fecha real: 2026-11-18 · Estado: borrador parcial (secciones 2 y 3 redactadas; la 3 es nueva en esta versión)
Las ecuaciones están en texto simple; se pasan al editor de ecuaciones al armar el PDF final.

## 0. Carátula y declaraciones — PENDIENTE
(datos, código F1-01, declaración de autoría y de uso de IA según el Anexo V, índice)

## 1. Encuadre del caso — PENDIENTE (base: `P1_ficha-encuadre/ficha-encuadre_v3.md`)

## 2. Eje I — Fenómenos eléctricos estáticos

**Fenómeno y ley.** En la sala de servidores, las personas que hacen mantenimiento caminan sobre una alfombra y se cargan por fricción (efecto triboeléctrico). Como el calzado las aísla del piso, el cuerpo funciona como un capacitor que guarda carga y energía, y las libera de golpe al tocar un equipo: una descarga electrostática (ESD). El libro de la cátedra describe este mismo fenómeno con la alfombra y los zapatos (Young y Freedman, 2009, pp. 713–714). Se usan la definición de capacitancia (ecuación 1) y la energía almacenada en un capacitor (ecuación 2) (Young y Freedman, 2009, pp. 816 y 824):

Q = C · V  (1)

U = ½ · C · V²  (2)

**Magnitudes y datos.** Los rangos son datos orientativos del caso F1-01: capacitancia del cuerpo de 100 a 150 pF, potencial de 2 a 15 kV según la humedad y energía de falla de un CI CMOS de 10 a 100 µJ; la humedad relativa invernal es de 25 %. Como el caso da rangos y no valores únicos, se adopta como hipótesis el caso más desfavorable: C = 150 pF, V = 15 kV y U_falla = 10 µJ. El modelo de cuerpo humano de la industria usa 100 pF (onsemi, 2023), y 150 pF es el valor de los ensayos de equipo completo (esa fuente todavía no se verificó: no citarla hasta ubicar autor y fecha). Los 15 kV son el techo del rango del caso; el caso no indica qué tensión corresponde exactamente a 25 % de humedad.

**Cálculo.** Con la ecuación 1, Q = 150 pF · 15 kV = 2,25 µC. Con la ecuación 2, U = ½ · 150 pF · (15 kV)² = 16,9 mJ, es decir 16 875 µJ, que es 1 688 veces la energía de falla de 10 µJ (169 veces si se usa el límite de 100 µJ). Despejando V de la ecuación 2, la tensión a la que el cuerpo ya almacena 10 µJ es V = √(2U_falla/C) = 365 V, muy inferior a los 15 kV. Además, se calculó la energía para las nueve combinaciones de C (100, 125 y 150 pF) y V (2, 8,5 y 15 kV): en todas supera los 100 µJ, entre 200 y 16 875 µJ (Tabla 1 en la memoria de cálculo).

**Qué influye y efectos.** La energía depende del cuadrado de la tensión: bajar la tensión a la mitad reduce la energía a la cuarta parte. La tensión depende de los materiales (la alfombra aislante acumula carga) y de la humedad: la bibliografía informa para caminar sobre alfombra 35 000 V con 10 a 20 % de humedad y 1 500 V con 65 a 90 % (onsemi, 2023), unas 23 veces menos. La capacitancia cambia con la postura y la cercanía a objetos, por lo que se tomó un valor fijo como simplificación.

**Consecuencia para el sistema de información.** El cuerpo cargado almacena mucha más energía que la necesaria para dañar un CMOS, y el umbral (365 V) es comparable al rango de susceptibilidad de 100 a 2 000 V informado para CMOS (onsemi, 2023). Esto es coherente con que las fallas aparezcan en días secos y tras el mantenimiento, aunque no se midió en el hospital. La decisión de diseño es reducir la tensión que puede acumular el personal antes de tocar los equipos; esto se compara entre las tres alternativas del caso en la sección 7.

**Fuente.** Young y Freedman (2009), capítulo 21 (pp. 713–714), capítulo 24 (pp. 816, 824–825); onsemi (2023).

## 3. Eje II — Fenómenos eléctricos estacionarios

**Fenómeno y ley.** Con el cuerpo cargado (Eje I), la descarga depende de la resistencia del camino persona–calzado–piso–tierra. Esa resistencia no cambia la energía almacenada, sino el tiempo y la corriente de la descarga. Se usan la resistencia de un conductor (ecuación 3), la constante de tiempo de un circuito R-C (ecuación 4), la tensión durante la descarga (ecuación 5) y la potencia en una resistencia (ecuación 6) (Young y Freedman, 2009, pp. 853, 863–864 y 897–899):

R = ρ · L / A  (3)

τ = R · C  (4)

v(t) = V₀ · e^(−t/RC)  (5)

P = V₀² / R  (6)

**Magnitudes y datos.** El caso F1-01 da la resistencia del calzado (10⁶ a 10⁹ Ω) pero **no** la del piso técnico, y no se midió. Por eso no se adopta un valor para el piso del hospital: se calculan escenarios con valores de normas y fabricantes, aclarando que no son mediciones. Escenario A: 1,5 kΩ, resistencia del modelo de cuerpo humano para la descarga directa (onsemi, 2023). Escenario B: 2 × 10⁶ Ω, un piso conductivo (menos de 10⁶ Ω según la norma ANSI/ESD STM7.1) más un elemento de 1 MΩ. Escenario C (referencia): 3,5 × 10⁷ Ω, límite que la norma ESD S20.20 fija para el sistema de pulsera y, en su edición 2007, para el sistema calzado + piso. Escenario D: 10⁹ Ω, límite de S20.20-2014 para calzado + piso, que además exige una tensión corporal menor que 100 V (In Compliance Magazine, s. f.). Los fabricantes de pisos técnicos ESD declaran rangos de 2,5 × 10⁴ a 10⁶ Ω (conductivos) y de 10⁶ a 10⁹ Ω (disipativos) (3M, s. f.; Sika, s. f.). Las normas se leyeron a través de fuentes secundarias. Se usan C = 150 pF y V₀ = 15 kV del Eje I.

**Cálculo.** La constante de tiempo es de 225 ns en el escenario A, 0,30 ms en B, 5,25 ms en C y 150 ms en D. Con la ecuación 5, el cuerpo baja de 15 kV a 100 V en 1,5 ms (B), 26,3 ms (C) y 0,75 s (D). La corriente inicial V₀/R es de 10 A en A, 7,5 mA en B, 0,43 mA en C y 15 µA en D. La potencia inicial (ecuación 6) pasa de 150 kW en A a 112,5 W, 6,43 W y 0,225 W en B, C y D. En todos los casos la energía total disipada es la misma, 16,9 mJ, como en el Eje I (la comprobación P₀·τ/2 lo confirma). El conductor de tierra (cobre de 6 AWG y 10 m, hipótesis) tiene 0,0129 Ω según la ecuación 3, despreciable frente a los megaohms del camino.

**Qué influye y efectos.** La resistencia total es la suma de la del calzado y la del piso, porque están en serie: si el calzado vale 10⁹ Ω, esa resistencia domina aunque el piso sea muy conductor. La resistencia depende además de la humedad, del envejecimiento del piso y de la tensión de medición. Hay un límite inferior de resistencia (2,5 × 10⁴ Ω en ASTM F150) por seguridad eléctrica de las personas.

**Consecuencia para el sistema de información.** Un camino de descarga controlado (megaohms) estira la descarga de nanosegundos a milisegundos y reduce la corriente en varios órdenes de magnitud sin cambiar la energía. Un piso conductivo con puesta a tierra solo protege si el calzado también conduce, por lo que hay que verificar el sistema calzado + piso completo y mantener el límite inferior por seguridad. La resistencia de tierra (5 a 40 Ω según la norma o recomendación) no limita la descarga ESD, pero sí es necesaria para la seguridad de la instalación.

**Limitación.** No hay resistencia medida del piso del hospital; los escenarios son referencias normativas y de fabricantes.

**Fuente.** Young y Freedman (2009), pp. 851, 853, 863–864, 883–885 y 897–899; onsemi (2023); In Compliance Magazine (s. f.); 3M (s. f.); Sika (s. f.).

## 4. Eje III — PENDIENTE
## 5. Eje IV — PENDIENTE
## 6. Eje V — PENDIENTE
## 7. Integración y decisión profesional — PENDIENTE
## 8. Conclusiones, limitaciones y bibliografía — PENDIENTE (bibliografía provisoria en `P5_fuentes/bibliografia.md`)
