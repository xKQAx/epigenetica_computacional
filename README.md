# Epigenética Computacional — Proyecto de Grado

Análisis de metilación del ADN a partir de datos públicos de NCBI GEO,
implementado en Python con notebooks Jupyter compatibles con Jupytext.

---

## Requisitos

- Python 3.8 o superior
- pip

---

## Instalación en Windows

Clonar el repositorio e instalar las dependencias:

```bash
git clone https://github.com/xKQAx/epigenetica_computacional.git
cd epigenetica_computacional
pip install -r requirements.txt
```

## Instalación en Ubuntu / Debian

En sistemas Linux con Python administrado por el sistema operativo,
es necesario usar un entorno virtual antes de instalar las dependencias.

```bash
# Clonar el repositorio
git clone https://github.com/xKQAx/epigenetica_computacional.git
cd epigenetica_computacional

# Instalar dependencias del sistema si no están disponibles
sudo apt install python3-full python3-venv -y

# Crear y activar el entorno virtual
python3 -m venv venv_tarea1
source venv_tarea1/bin/activate

# Instalar las dependencias del proyecto
pip install -r requirements.txt
```

El entorno virtual debe activarse cada vez que se abra una terminal nueva
antes de ejecutar el notebook:

```bash
source venv_tarea1/bin/activate
```

---

## Estructura del proyecto

```
epigenetica_computacional/
├── requirements.txt
├── README.md
├── notebooks/
│   ├── tarea1_fenodata_GSE116378.ipynb
│   └── tarea1_fenodata_GSE116378.py
├── data_geo/
│   └── GSE116378_family.soft.gz
└── resultados/
    └── GSE116378_phenodata.csv
```

---

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
