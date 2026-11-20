# Auditoría estadística de un sistema de detección de phishing

Producto integrador de *Estadística aplicada a Seguridad en Tecnologías de la Información*.

- **Grupo:** 061
- **Integrantes:** Bruno Alberto Gonzalez Cuellar, Mikel Eduardo Jonguitud Hernández, Ana Lucia Alonso Martinez
- **Docente:** Dr. Álvaro E. Cordero Franco

## Contenido de la carpeta

| Archivo | Descripción |
|---|---|
| `informe.Rmd` | Código fuente reproducible del análisis completo. |
| `informe.html` | Informe generado a partir del `.Rmd`. |
| `resumen_ejecutivo.pdf` | Resumen de una página: problema, tres hallazgos, recomendación, riesgo y limitación. |
| `presentacion.pdf` | Presentación de 8 a 10 minutos. |
| `data/` | Datos limpios (`datos_limpios.csv`). Se incluye porque la licencia CC BY 4.0 permite redistribuir los datos. |
| `README.md` | Este archivo. |

## Datos

- **Conjunto:** PhiUSIIL Phishing URL Dataset, UCI Machine Learning Repository.
- **Enlace:** <https://archive.ics.uci.edu/dataset/967/phiusiil+phishing+url+dataset>
- **Licencia:** Creative Commons Attribution 4.0 (CC BY 4.0).
- **Fecha de consulta y descarga:** 08-11-2026.
- Si no existe en `data/`, el `.Rmd` descarga el archivo original de forma automática. Si la descarga falla, bájalo desde la página de UCI y coloca el CSV dentro de `data/`.

## Cómo reproducirlo

1. Instala los paquetes (solo una vez):

   ```r
   install.packages(c("tidyverse", "knitr", "rmarkdown", "scales", "ranger"))
   ```

2. Coloca `informe.Rmd` en una carpeta propia y ábrelo en RStudio.
3. Haz **Knit to HTML**. Con el conjunto completo tarda varios minutos; no lo interrumpas.

Al compilar se crean junto al `.Rmd`:

- `informe.html`: el informe.
- `figuras/`: las gráficas en PNG.
- `data/datos_limpios.csv`: los datos limpios.

## Decisiones principales

- Partición estratificada 75/25 con semilla 2026, hecha antes de elegir variables o transformaciones. El conjunto de prueba se usa solo para la evaluación final.
- Phishing es la clase positiva; la codificación de `label` se verifica en el informe (sección 3.3).
- Se excluyen las variables precalculadas con el corpus y las de AUC univariado ≥ 0.95 en entrenamiento, por posible fuga de información (sección 3.5).
- Modelos: regresión logística y bosque aleatorio (`ranger`) sobre la misma partición y las mismas variables.
- Supuesto de trabajo: un ataque omitido cuesta 5 veces una falsa alarma (parámetro `costo_fn` al inicio del `.Rmd`; la sección 7.6 muestra otros costos).
