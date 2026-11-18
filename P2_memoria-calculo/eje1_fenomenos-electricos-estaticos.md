# P2 – Memoria de cálculo · Eje I – Fenómenos eléctricos estáticos (v3)
Caso: F1-01 (sala de servidores de un hospital escuela: fallas por ESD) · Fecha real: 2026-11-18
Estado: REVISAR (desarrollado y verificado contra el libro; falta que Florencia lo revise y lo pueda explicar)
Corresponde a: sección 2 del informe (`P6_borradores/informe_v1.md`) · Versiones anteriores conservadas en `versiones/eje1_v1_plantilla.md` y `versiones/eje1_v2.md`
Notación: como en el libro, **U = energía potencial almacenada** y **E = campo eléctrico**. (En P1 v3 la energía de falla figura como "E_falla"; es la misma U_falla de este archivo.)

Código de colores de procedencia: **[CASO]** dato del Banco · **[FUENTE]** dato de bibliografía o ficha técnica · **[HIPÓTESIS]** valor que adoptamos nosotras · **[CALCULADO]**

## 1. Qué fenómeno ocurre y qué ley lo explica
Cuando una persona camina sobre una alfombra (el libro describe justo este caso: en un día seco las fibras de la alfombra son buenos aislantes y la fricción de los zapatos hace que la carga se acumule en el cuerpo, y al tocar un objeto conductor se siente la descarga; Young y Freedman, 2009, pp. 713–714), los materiales se frotan y se transfieren cargas eléctricas (efecto triboeléctrico). El cuerpo queda cargado y, como está aislado del piso por el calzado, la carga se queda ahí. El cuerpo se comporta como un **capacitor**: un objeto que guarda carga y energía. Al tocar un equipo (más a tierra), esa energía se descarga de golpe: es la **descarga electrostática (ESD)**.

Leyes que usamos (Eje I) (Young y Freedman, 2009):
- Definición de capacitancia: C = Q / V_ab, o sea **Q = C · V** (ecuación 24.1, p. 816; el libro usa Q = CV para tensión fija en p. 825)
- Energía almacenada en un capacitor: **U = ½ · C · V²** (ecuación 24.9, p. 824, que también escribe U = Q²/2C = ½·Q·V; p. 825)

## 2. Qué significa cada magnitud (en simple)
| Símbolo | Nombre | Qué es | Unidad |
|---|---|---|---|
| C | capacitancia | cuánta carga puede guardar el cuerpo por cada volt de tensión | farad (F); 1 pF = 10⁻¹² F |
| V | potencial (tensión) | "altura eléctrica" del cuerpo respecto de tierra | volt (V); 1 kV = 10³ V |
| Q | carga | cantidad de carga eléctrica acumulada | coulomb (C); 1 µC = 10⁻⁶ C |
| U | energía almacenada | lo que se libera en la descarga | joule (J); 1 µJ = 10⁻⁶ J |
| U_falla | energía de falla del CI CMOS | energía a partir de la cual el circuito integrado se daña | µJ |

## 3. Valores adoptados y por qué
| Magnitud | Rango del caso [CASO] | Valor adoptado [HIPÓTESIS] | Justificación |
|---|---|---|---|
| C | 100 a 150 pF | **150 pF** | El extremo alto da la descarga más energética: es el caso de diseño más exigente. El modelo de cuerpo humano de componentes (HBM) usa 100 pF [FUENTE: onsemi, AND9059/D]; los ensayos de equipo completo con pistola ESD (IEC 61000-4-2) usan 150 pF [FUENTE: In Compliance Magazine, sin autor ni fecha visibles; verificar]. Por eso 150 pF está dentro de lo que usa la industria. |
| V | 2 a 15 kV "según humedad" | **15 kV** | Extremo alto del rango. Es el caso más desfavorable. Ojo: el caso dice 25 % de humedad en invierno, pero **no dice cuánto vale V a 25 %**; 15 kV es el techo del rango, no un valor medido ni asociado a 25 %. |
| U_falla | 10 a 100 µJ | **10 µJ** | Extremo bajo: representa el componente más sensible. Si el cuerpo supera incluso el límite más alto (100 µJ), la conclusión no depende de esta elección. |

Importante para el coloquio: elegimos el **peor caso** a propósito. Y comprobamos en la sección 6 que la conclusión no cambia si usamos cualquier otro valor del rango.

## 4. Cálculos (con el caso adoptado)

### 4.1 Carga acumulada
**Qué buscamos:** cuánta carga tiene el cuerpo.
**Fórmula:** Q = C · V (se usa porque la capacitancia se define como carga por unidad de tensión).
**Reemplazo:** Q = 150 × 10⁻¹² F · 15 × 10³ V = 2,25 × 10⁻⁶ C
**Resultado:** **Q = 2,25 µC**

### 4.2 Energía almacenada
**Qué buscamos:** cuánta energía se puede liberar en la descarga.
**Fórmula:** U = ½ · C · V² (la energía depende del *cuadrado* de la tensión: si V se duplica, U se cuadruplica).
**Reemplazo:** U = ½ · 150 × 10⁻¹² F · (15 × 10³ V)² = ½ · 150 × 10⁻¹² · 2,25 × 10⁸ = 1,6875 × 10⁻² J
**Resultado:** **U = 16,9 mJ = 16 875 µJ**
**Control de unidades:** F · V² = (C/V) · V² = C · V = J ✔.
**Control cruzado:** U = ½ · Q · V = ½ · 2,25 × 10⁻⁶ C · 15 × 10³ V = 1,6875 × 10⁻² J ✔ (da igual).

### 4.3 Comparación con la energía de falla del CI CMOS
**Qué buscamos:** cuántas veces la energía del cuerpo supera lo que daña al componente.
**Cociente:** U / U_falla = 16 875 µJ / 10 µJ = **1 687,5 veces** (con el límite más alto, 100 µJ: 168,75 veces).

### 4.4 Tensión mínima que ya alcanza para dañar
**Qué buscamos:** ¿a qué tensión del cuerpo la energía almacenada iguala la energía de falla?
**Despeje:** de U = ½ · C · V² se obtiene V = √(2 · U_falla / C).
**Reemplazo (150 pF, 10 µJ):** V = √(2 · 10 × 10⁻⁶ J / 150 × 10⁻¹² F) = √(1,333 × 10⁵ V²) = **365 V**
**Control de unidades:** √(J/F) = √(V²) = V ✔.
**Interpretación:** con apenas ~365 V, el cuerpo ya almacena tanta energía como la que daña al componente más sensible. Eso es muy por debajo de los 15 kV adoptados.

### 4.5 Complemento (no lo pide la consigna): ¿a qué distancia salta la chispa?
Según el libro, la rigidez dieléctrica del **aire seco** es alrededor de 3 × 10⁶ V/m, y el propio libro aclara que solo se pueden dar cifras aproximadas (Young y Freedman, 2009, p. 833). E_aire = campo eléctrico máximo antes de que el aire deje de aislar.
**Cálculo (campo uniforme, aproximación):** d = V / E_aire = 15 × 10³ V / 3 × 10⁶ V/m = 5 × 10⁻³ m = **5 mm**.
**Límite:** es un orden de magnitud; en la realidad depende de la forma de los objetos (con puntas salta a mayor distancia). Si no te sirve para el informe, se descarta.

## 5. Interpretación física (para explicarlo con palabras propias)
1. El cuerpo cargado almacena **miles de veces más energía** de la que necesita un circuito integrado para dañarse. Aunque solo una parte de esa energía pase por el componente (depende del camino de la descarga, que es tema del Eje II), la reserva es enorme comparada con el límite.
2. Como U depende de V², **bajar la tensión es lo que más reduce la energía**: reducir V a la mitad baja U a la cuarta parte. Por eso conviene atacar la acumulación de carga (humedad, piso conductivo) o descargar el cuerpo de a poco (pulsera con resistencia).
3. El umbral de daño (365 V) es parecido a lo que se informa para CMOS: **100 a 2 000 V** en el modelo HBM [FUENTE: onsemi, AND9059/D, tabla 1]. Es una coherencia entre nuestro cálculo y un dato externo, no una medición propia.

## 6. Comparación con otros valores del rango
Energía almacenada U = ½·C·V², en µJ. Con V = 8,5 kV (punto medio de 2 a 15 kV; es un valor aritmético para comparar, no un valor medido).

| C \ V | 2 kV | 8,5 kV | 15 kV |
|---|---|---|---|
| 100 pF | 200 | 3 612,5 | 11 250 |
| 125 pF | 250 | 4 515,6 | 14 062,5 |
| 150 pF | 300 | 5 418,8 | **16 875** |

Conclusión de la tabla: **en las 9 combinaciones, la energía almacenada (200 a 16 875 µJ) supera el límite más alto de falla del caso (100 µJ)**; en la combinación más favorable (100 pF y 2 kV) lo supera 2 veces. Es decir, el diagnóstico "el cuerpo cargado puede dañar un CMOS" **no depende** de los valores elegidos.

Tensión umbral V = √(2 · U_falla / C):
| C \ U_falla | 10 µJ | 55 µJ (punto medio) | 100 µJ |
|---|---|---|---|
| 100 pF | 447 V | 1 049 V | 1 414 V |
| 150 pF | 365 V | 856 V | 1 155 V |

Todos los umbrales (365 a 1 414 V) están por debajo del rango del caso (2 a 15 kV).

Lo que sí cambia al variar los valores es **cuánto margen hay**: entre 2 veces y 1 688 veces. Los valores adoptados representan el peor caso para dimensionar la protección con seguridad.

## 7. Efecto de la humedad y los materiales (qué influye)
- Los materiales aislantes (alfombra, calzado) acumulan carga; los conductores (metal, piso conductivo) la reparten o la llevan a tierra.
- La humedad hace que las superficies sean parcialmente conductoras y la carga se disipa [FUENTE: onsemi, AND9059/D]. El libro coincide: dice que las fibras de la alfombra son buenos aislantes "en un día seco" (Young y Freedman, 2009, p. 713) y propone como soluciones fibras conductoras en la alfombra o un tratamiento antiestático (p. 714).
- Tabla de tensiones típicas [FUENTE: onsemi, AND9059/D; coincide con el boletín NASA NEPP 2020]: caminar sobre alfombra, 35 000 V a 10–20 % de humedad vs. 1 500 V a 65–90 %; sobre piso vinílico, 12 000 V vs. 250 V. Es decir, 23 veces y 48 veces menos con aire húmedo (cálculos: 35 000/1 500 = 23,3 y 12 000/250 = 48).
- Nota: el rango del caso llega a 15 kV, y la literatura da 35 kV para alfombra y humedad muy baja. Usamos el rango del caso porque es el dato oficial; la literatura indica que valores de esa magnitud son realistas.

## 8. Relación con las fallas del hospital
Las fallas (3 memorias y 1 placa de red en 6 meses) ocurren en días secos y después del mantenimiento. Es coherente con: aire seco → más carga acumulada (V alta) → U enorme respecto de U_falla → daño al tocar los módulos. El mantenimiento implica contacto directo con módulos y placas, que es cuando se produce la descarga. Esto es una explicación compatible con los datos, **no una medición** en ese hospital.

## 9. Consecuencia para el sistema de información (decisión de diseño)
- Hay que evitar que el cuerpo llegue a decenas de volts de diferencia con el equipo, no solo a miles: el umbral de daño es de cientos de volts.
- Esto se evalúa en la decisión profesional (sección 7 del informe) comparando piso conductivo con tierra, control de humedad y pulsera antiestática.
- Dato útil para esa comparación: onsemi indica que no conviene descargar con camino de muy baja resistencia; se usa un camino de alta resistencia (del orden de 1 MΩ) para evitar una descarga brusca [FUENTE: onsemi, AND9059/D]. Se desarrolla en el Eje II.

## 10. Limitaciones
- No hay mediciones en el hospital: todo es modelo con datos orientativos del caso.
- La energía almacenada no es la energía que llega al componente; depende del camino (Eje II).
- El modelo del cuerpo como capacitor fijo es una simplificación: C cambia con la postura y la cercanía a objetos.
- Los rangos del Banco son orientativos.

## 11. Fuentes y verificación contra el libro (hecha el 2026-11-18 con el PDF adjunto)
Libro: Young y Freedman, *Física universitaria con física moderna*, vol. 2, 12.ª ed., Pearson Educación, México, 2009. Páginas = **numeración impresa del libro** (en el visor del PDF, página = impresa − 682).

| Qué se usa | Dónde está en el libro |
|---|---|
| Carga por fricción con la alfombra, descarga al tocar un conductor | Cap. 21, introducción (p. 709) y pp. 713–714 |
| Potencial eléctrico = energía potencial por unidad de carga (volts = J/C) | Cap. 23, sección 23.2 (p. 789) |
| Capacitor, capacitancia C = Q/V_ab (ecuación 24.1) | Cap. 24, sección 24.1 (p. 816) |
| Energía almacenada: W = Q²/2C (24.8) y U = Q²/2C = ½CV² = ½QV (24.9) | Cap. 24, sección 24.3 (pp. 824–825) |
| Rigidez dieléctrica del aire seco ≈ 3 × 10⁶ V/m | Cap. 24, sección 24.4 (p. 833) |

Otras fuentes: onsemi (2023), AND9059/D (HBM 100 pF; tabla de tensiones por humedad; CMOS 100–2 000 V); NASA NEPP (2020) (misma tabla; solo fragmentos leídos).

**Qué dice el libro y qué NO dice (para el coloquio):** el libro respalda las fórmulas, el concepto de capacitor, la carga por fricción con alfombra y la rigidez del aire. **No** trae los valores de 100–150 pF del cuerpo humano, ni los kV según la humedad, ni la energía de falla de un CMOS: esos vienen del caso F1-01 y de onsemi.

## 12. Historial
| Versión | Fecha real | Qué cambió |
|---|---|---|
| v1 | 2026-11-18 | Plantilla (conservada en `versiones/eje1_v1_plantilla.md`) |
| v2 | 2026-11-18 | Eje I desarrollado con C = 150 pF, V = 15 kV, U_falla = 10 µJ; comparación con el rango (conservada en `versiones/eje1_v2.md`) |
| v3 | 2026-11-18 | Verificado contra el libro: páginas exactas; símbolo U para la energía (E queda para el campo eléctrico); se aclara la rigidez del aire (aire seco, aproximada) |
