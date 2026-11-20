# PRO vs ETT · Muelle Valencia

Un único `index.html` que compara la productividad de la plantilla propia (PRO) y del personal de ETT a partir del Excel *Canvas ETT vs PRO*.

## Cómo usar

1. Abre `index.html` en Chrome o Edge (necesita Internet para SheetJS, Chart.js y las fuentes).
2. Verás datos de ejemplo marcados como tales.
3. Pulsa **Cargar Excel** y elige el Canvas. Se leen las hojas `FACT`, `H_HORAS` y `H_OPERATIVAS`. El archivo se procesa en el navegador.

## Qué incluye

- **Resumen**: PRO frente a ETT en puntos/h o movimientos/h (botón *Medir en*), con objetivo (60 puntos/h por defecto), horas, puntos y movimientos; peso de ETT en horas, movimientos, puntos y operarios; conclusiones automáticas.
- **Por día**: productividad diaria de cada grupo y horas PRO/ETT con % ETT.
- **Operativas**: reparto de movimientos por operativa en cada grupo, ritmo por operativa y tabla operativa × temperatura con el grupo más rápido.
- **Turnos**: movimientos por hora del día y productividad por turno.
- **Operarios**: ranking individual con objetivo y tabla de detalle.
- **Exportar**: informe Excel (Grupos, Por día, Operativas, Operarios, Conclusiones) y *Copiar tabla*.

## Cómo se calcula

- **Por grupo** (igual que la tabla PT_KPI_GRUPO de CALC): puntos o movimientos de los días con horas en `H_HORAS` ÷ horas de `H_HORAS`. Con filtros de operativa, temperatura o turno, las horas del grupo se reparten entre sus movimientos (columna `HORAS_GRUPO`).
- **Por operario, operativa y turno**: sobre horas de jornada (`HORAS_OP`: primer a último escaneo del día, máximo 8 h).
- Los usuarios con `INDIVIDUAL = NO` suman en su grupo pero no en el ranking.
- El periodo por defecto son los días con horas en `H_HORAS`.

El ritmo por operativa no reproduce la tabla *OPERATIVA / TEMP* de la hoja CALC, que usa otra fórmula.
