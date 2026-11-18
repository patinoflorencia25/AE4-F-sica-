# Informe Técnico Integrador – borrador v1
Caso F1-01 · Fecha real: 2026-11-18 · Estado: borrador parcial (solo la sección 2 está redactada)
Las ecuaciones están en texto simple; se pasan al editor de ecuaciones al armar el PDF final.

## 0. Carátula y declaraciones — PENDIENTE
(datos, código F1-01, declaración de autoría y de uso de IA según el Anexo V, índice)

## 1. Encuadre del caso — PENDIENTE (base: `P1_ficha-encuadre/ficha-encuadre_v3.md`)

## 2. Eje I — Fenómenos eléctricos estáticos

**Fenómeno y ley.** En la sala de servidores, las personas que hacen mantenimiento caminan sobre una alfombra y se cargan por fricción (efecto triboeléctrico). Como el calzado las aísla del piso, el cuerpo funciona como un capacitor que guarda carga y energía, y las libera de golpe al tocar un equipo: una descarga electrostática (ESD). Se usan la definición de capacitancia (ecuación 1) y la energía almacenada en un capacitor (ecuación 2):

Q = C · V  (1)

E = ½ · C · V²  (2)

**Magnitudes y datos.** Los rangos son datos orientativos del caso F1-01: capacitancia del cuerpo de 100 a 150 pF, potencial de 2 a 15 kV según la humedad y energía de falla de un CI CMOS de 10 a 100 µJ; la humedad relativa invernal es de 25 %. Como el caso da rangos y no valores únicos, se adopta como hipótesis el caso más desfavorable: C = 150 pF, V = 15 kV y E_falla = 10 µJ. El modelo de cuerpo humano de la industria usa 100 pF (onsemi, 2023), y 150 pF es el valor de los ensayos de equipo completo (verificar la fuente antes de citarla). Los 15 kV son el techo del rango del caso; el caso no indica qué tensión corresponde exactamente a 25 % de humedad.

**Cálculo.** Con la ecuación 1, Q = 150 pF · 15 kV = 2,25 µC. Con la ecuación 2, E = ½ · 150 pF · (15 kV)² = 16,9 mJ, es decir 16 875 µJ, que es 1 688 veces la energía de falla de 10 µJ (169 veces si se usa el límite de 100 µJ). Despejando V de la ecuación 2, la tensión a la que el cuerpo ya almacena 10 µJ es V = √(2E/C) = 365 V, muy inferior a los 15 kV. Además, se calculó la energía para las nueve combinaciones de C (100, 125 y 150 pF) y V (2, 8,5 y 15 kV): en todas supera los 100 µJ, entre 200 y 16 875 µJ (Tabla 1 en la memoria de cálculo).

**Qué influye y efectos.** La energía depende del cuadrado de la tensión: bajar la tensión a la mitad reduce la energía a la cuarta parte. La tensión depende de los materiales (la alfombra aislante acumula carga) y de la humedad: la bibliografía informa para caminar sobre alfombra 35 000 V con 10 a 20 % de humedad y 1 500 V con 65 a 90 % (onsemi, 2023), unas 23 veces menos. La capacitancia cambia con la postura y la cercanía a objetos, por lo que se tomó un valor fijo como simplificación.

**Consecuencia para el sistema de información.** El cuerpo cargado almacena mucha más energía que la necesaria para dañar un CMOS, y el umbral (365 V) es comparable al rango de susceptibilidad de 100 a 2 000 V informado para CMOS (onsemi, 2023). Esto es coherente con que las fallas aparezcan en días secos y tras el mantenimiento, aunque no se midió en el hospital. La decisión de diseño es reducir la tensión que puede acumular el personal antes de tocar los equipos; esto se compara entre las tres alternativas del caso en la sección 7.

**Fuente.** Young y Freedman (2009), capítulos 23 y 24 (verificar); onsemi (2023).

## 3. Eje II — PENDIENTE
## 4. Eje III — PENDIENTE
## 5. Eje IV — PENDIENTE
## 6. Eje V — PENDIENTE
## 7. Integración y decisión profesional — PENDIENTE
## 8. Conclusiones, limitaciones y bibliografía — PENDIENTE (bibliografía provisoria en `P5_fuentes/bibliografia.md`)
