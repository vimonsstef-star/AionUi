# Dashboard Tiempos Operativos · Muelle Valencia

Un único archivo `index.html` (sin carpetas `css/` ni `js/`) para analizar `Tiempos Operativos.xlsx`.

## Cómo usar

1. Abre `index.html` en Chrome o Edge (necesita Internet para cargar SheetJS, Chart.js y las fuentes).
2. Al abrirlo verás **datos de ejemplo** (marcados como tales).
3. Pulsa **Cargar Excel** y elige `Tiempos Operativos.xlsx`. Se leen las hojas `BD_LLE_NAC` y `BD_MOV_IQ`. El archivo se procesa en el navegador; no se sube a ningún sitio.

## Qué incluye

- **Resumen**: viajes, % llegada puntual, SSCC movidos, puntos/hora por operario (objetivo 60), tiempo en muelle y plantilla real vs necesaria. Alertas automáticas.
- **Plantilla**: carga media por hora (FR / SU / otras) con operarios presentes vs necesarios; dimensionamiento por turno (Noche 00–08, Mañana 08–16, Tarde 16–24); mapa de calor operario × hora.
- **Tiempo en muelle**: recepción → carga, por temperatura y por tipo de bordereau (descripciones de BD_VIAJES), SSCC sin cargar y sin cargar > 24 h, mediana según hora de recepción. También la mediana recepción → zonaje.
- **Viajes**: puntualidad diaria de salida y llegada, retraso medio por agencia y ranking.
- **Operarios**: recepciones, zonajes y cargas por persona, jornadas, horas, puntos, puntos/h, movimientos/h y comparación con el objetivo.
- **Filtros**: fechas, actividad (todas por defecto, carga + zonaje, carga, zonaje o recepción), turno, operario, temperatura, estado y agencia.
- **Parámetros**: objetivo puntos/h (60), jornada máxima (8 h), inicio del primer turno (00 h), horas efectivas por turno (7), objetivo de tiempo en muelle (12 h) y tolerancia de puntualidad (15 min).
- **Exportar**: informe Excel (Operarios, Turnos, Carga por hora, Tiempo en muelle, Agencias, Alertas) y *Copiar tabla*.

## Cómo se calcula

- **Actividades de BD_MOV_IQ**: recepción (`Fecha de recepción` + `Num. Recep.`), zonaje (`Fecha Zonaje` + `El que reparte en zonas`) y carga (`Fecha Carga Etiq` + `Operador`). Cada línea cuenta como un SSCC.
- **Puntos por SSCC** (tabla H_OPERATIVAS del Canvas ETT vs PRO): recepción 1; zonaje y carga 2 en FR/NR y 4 en SU.
- **Horas de jornada** de un operario: del primer al último escaneo del día (cualquier actividad), con un máximo de 8 h. Es el mismo criterio que la columna HORAS_OP del Canvas.
- **Puntos/hora** = puntos ÷ horas de jornada.
- **Operarios necesarios por hora** = puntos medios de esa hora ÷ objetivo puntos/h.
- **Plantilla necesaria por turno** = puntos/día del turno ÷ (objetivo × horas efectivas).
- **Tiempo en muelle** = Fecha Carga Etiq − Fecha de recepción.
- **Retraso de llegada** = HR_LLE_REAL − HR_LLE_NEGOCIADA (o HR_LLE_PLAN). Las fechas sin año (`31/03 21:00`) toman el año de BD_MOV_IQ.

## Corrección respecto a la versión anterior

El `index.html` anterior cargaba `chart.js@4.4.1/dist/chart.umd.min.js`, archivo que no existe en esa versión, por lo que los gráficos no se mostraban. Ahora se usa `chart.umd.js`.
