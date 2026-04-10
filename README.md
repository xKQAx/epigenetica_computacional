# Epigenética Computacional — Proyecto de Grado

Análisis de metilación del ADN a partir de datos públicos de NCBI GEO,
implementado en Python con notebooks Jupyter compatibles con Jupytext.

---

## Requisitos

- Python 3.8 o superior
- pip

## Instalación

Clonar el repositorio y instalar las dependencias:

```bash
git https://github.com/xKQAx/epigenetica_computacional.git
cd epigenetica_computacional
pip install -r requirements.txt
```

## Estructura del proyecto
epigenetica_computacional/
├── requirements.txt
├── README.md
├── notebooks/
│   ├── tarea1_fenodata_GSE116378.ipynb
│   └── tarea1_fenodata_GSE116378.py
├── data_geo/
│   └── GSE116378_series_matrix.txt.gz
└── resultados/
└── GSE116378_phenodata.csv

## Tareas

### Tarea 1 — Extracción de datos fenotípicos

Descarga y extrae los metadatos clínicos del dataset GSE116378
desde NCBI GEO, equivalente al `phenoData` de R con GEOquery.

**Dataset:** GSE116378 — DUTCHSCZ  
**Plataforma:** Illumina HumanMethylation450 BeadChip  
**Muestras:** 64 (49 controles, 15 pacientes con esquizofrenia)

**Ejecutar el notebook:**

```bash
jupyter notebook notebooks/tarea1_fenodata_GSE116378.ipynb
```

**O ejecutar como script Python plano:**

```bash
python notebooks/tarea1_fenodata_GSE116378.py
```

**Salida generada:** `resultados/GSE116378_phenodata.csv`

**Exportar notebook a Python plano con Jupytext:**

```bash
python -m jupytext --to py:percent notebooks/tarea1_fenodata_GSE116378.ipynb
```

---

## Dataset

- **Fuente:** https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE116378
- **Referencia:** Boks MP et al. NPJ Schizophr. 2018 Aug 21;4(1):16. PMID: 30131491

---

## Nota

La carpeta `data_geo/` se genera automáticamente al ejecutar el notebook.
No es necesario descargar los archivos manualmente.