# Dashboard Tiempos Operativos · Muelle Valencia

Un único archivo `index.html` (sin carpetas `css/` ni `js/`) para analizar `Tiempos Operativos.xlsx`.

## Cómo usar

1. Abre `index.html` en Chrome o Edge (necesita Internet para cargar SheetJS, Chart.js y las fuentes).
2. Al abrirlo verás **datos de ejemplo** (marcados como tales).
3. Pulsa **Cargar Excel** y elige `Tiempos Operativos.xlsx`. Se leen las hojas `BD_LLE_NAC` y `BD_MOV_IQ`. El archivo se procesa en el navegador; no se sube a ningún sitio.

## Qué incluye

- **Resumen**: viajes, % llegada puntual, SSCC zonados, SSCC/hora por operador, mediana recepción→zonaje y plantilla real vs necesaria. Alertas automáticas ordenadas por gravedad.
- **Plantilla**: carga media por hora del día (FR / SU / otras) con operadores presentes vs necesarios; dimensionamiento por turno (Noche 00–08, Mañana 08–16, Tarde 16–24); mapa de calor operador × hora.
- **Recepción → Zonaje**: distribución de tiempos, mediana / P90 / % en objetivo por temperatura, pendientes de zonaje y mediana por hora.
- **Viajes**: puntualidad diaria de salida y llegada, retraso medio por agencia y ranking de agencias.
- **Operadores**: SSCC por hora activa, comparación con el objetivo, mediana de zonaje y estado.
- **Filtros**: rango de fechas, turno, operador, temperatura, estado de etiqueta y agencia.
- **Parámetros**: objetivo de zonaje (min), tolerancia de puntualidad (min), objetivo SSCC/h (60 por defecto, el de la delegación; vacío = mediana del equipo), inicio del primer turno (00 h por defecto; los tres turnos son de 8 h) y horas efectivas por turno. Se guardan en el navegador.
- **Exportar**: informe Excel con hojas Operadores, Turnos, Carga por hora, Agencias y Alertas; botón *Copiar tabla* para pegar en Excel.
- Tema claro / oscuro y vista móvil.

## Cómo se calcula

- **Hora de actividad**: la de *Fecha Zonaje* (o la de recepción si aún no está zonado).
- **Horas activas** de un operador: horas de reloj distintas en las que hizo al menos un zonaje.
- **Operadores necesarios por hora** = SSCC medios de esa hora ÷ objetivo SSCC/h.
- **Plantilla necesaria por turno** = SSCC/día del turno ÷ (objetivo SSCC/h × horas efectivas).
- **Retraso de llegada** = HR_LLE_REAL − HR_LLE_NEGOCIADA (o HR_LLE_PLAN si no hay negociada). Si solo hay hora, se corrige el cruce de medianoche.
- **Puntual** = retraso ≤ tolerancia.

## Columnas esperadas

**BD_LLE_NAC**: F.VIAJE, NOM_VIAJE, COD_VIAJE, HR_SAL_PLAN, HR_SAL_REAL, AGENCIA EXPEDIDORA, HR_LLE_NEGOCIADA, HR_LLE_PLAN, HR_LLE_REAL

**BD_MOV_IQ**: Etiqueta SSCC, Cat Temp, Fecha de recepción, Fecha Zonaje, Estado Etiqueta, Operador, Num Paquete Pos., Num Tot Pal Pos, Tipo Bord, Descr. Bord., Agencia expedidiora, Agencia proprietaria

Se toleran acentos, mayúsculas, puntos y guiones bajos en los nombres de columna. Las fechas pueden venir como fecha de Excel, `dd/mm/aaaa hh:mm`, `aaaa-mm-dd hh:mm` o solo `hh:mm`.

## Corrección respecto a la versión anterior

El `index.html` anterior cargaba `chart.js@4.4.1/dist/chart.umd.min.js`, archivo que no existe en esa versión, por lo que los gráficos no se mostraban. Ahora se usa `chart.umd.js`.
