# Epigenética Computacional — Proyecto de Grado

Metaanálisis de metilación del ADN en esquizofrenia a partir de datos
públicos de NCBI GEO, implementado en Python con notebooks Jupyter
compatibles con Jupytext.

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
│   ├── tarea1_fenodata_todos_datasets.ipynb
│   └── tarea1_fenodata_todos_datasets.py
├── data_geo/
│   ├── GSE116378_family.soft.gz
│   ├── GSE116379_family.soft.gz
│   ├── GSE80417_family.soft.gz
│   ├── GSE84727_family.soft.gz
│   ├── GSE152027_family.soft.gz
│   └── GSE147221_family.soft.gz
└── resultados/
    ├── GSE116378_phenodata.csv
    ├── GSE116379_phenodata.csv
    ├── GSE80417_phenodata.csv
    ├── GSE84727_phenodata.csv
    ├── GSE152027_phenodata.csv
    ├── GSE147221_phenodata.csv
    └── metaanalisis_phenodata_combinado.csv
```

---

## Datasets del metaanálisis

Todos los datasets usan sangre completa como tejido y la plataforma
Illumina HumanMethylation450 BeadChip (450K). Fuente: NCBI GEO.

| Código GEO | Autores | Año | Cohorte | Casos (SCZ) | Controles |
|------------|---------|-----|---------|-------------|-----------|
| GSE116378 | Boks et al. | 2018 | DUTCHSCZ — sangre | 15 | 49 |
| GSE116379 | Boks et al. | 2018 | DUTCHSCZ — hambruna prenatal | ~100 | ~53 |
| GSE80417 | Hannon et al. | 2016 | UCL — Londres | 353 | 322 |
| GSE84727 | Hannon et al. | 2016 | Aberdeen — Escocia | 414 | 433 |
| GSE152027 | Hannon et al. | 2021 | IoPPN + FEP | 290 (+307 FEP) | 203 |
| GSE147221 | Hannon et al. | 2021 | Dublin | 364 | 349 |

---

## Tarea 1 — Extracción de datos fenotípicos

### Qué hace el notebook

El notebook descarga cada dataset directamente desde los servidores
de NCBI GEO y extrae los metadatos clínicos de cada muestra, sin
necesidad de descargar manualmente los archivos de metilación
(que pesan entre 130 MB y 220 MB cada uno).

En R con GEOquery, este proceso sería equivalente a:

```r
gse <- getGEO("GSE116378")
pheno <- pData(phenoData(gse[[1]]))
```

En Python, GEOparse realiza el mismo proceso descargando el archivo
SOFT de cada dataset, que contiene la estructura completa de metadatos
de todas las muestras.

### Sobre el CSV combinado

El archivo `metaanalisis_phenodata_combinado.csv` une los phenoData
de los 6 datasets en una sola tabla. Dado que cada grupo de autores
registró sus variables clínicas con nombres propios, algunas columnas
solo tienen datos en ciertos datasets y aparecen como NaN (equivalente
a NA en R) en los demás. Esto es el comportamiento esperado y correcto,
no indica mezcla de datos, sino diferencias en las variables reportadas
por cada estudio. Las dos primeras columnas, `gse_id` y `referencia`,
permiten identificar en todo momento a qué dataset pertenece cada fila.

Por ejemplo, la columna `famine_exposure` solo tendrá datos en
GSE116379 (Boks et al., estudio de hambruna prenatal), mientras que
`Smoking` o `smoking_status` pueden aparecer en los datasets de Hannon.

### Ejecutar el notebook

```bash
jupyter notebook notebooks/tarea1_fenodata_todos_datasets.ipynb
```

### O ejecutar como script Python plano

```bash
python notebooks/tarea1_fenodata_todos_datasets.py
```

### Exportar notebook a Python plano con Jupytext

```bash
python -m jupytext --to py:percent notebooks/tarea1_fenodata_todos_datasets.ipynb
```

---

## Referencias

- Boks MP et al. NPJ Schizophr. 2018;4(1):16. PMID: 30131491
  https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE116378
  https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE116379

- Hannon E et al. Genome Biol. 2016;17(1):176. PMID: 27549193
  https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE80417
  https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE84727

- Hannon E et al. eLife. 2021. PMID: 33646118
  https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE152027
  https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE147221

---

## Nota

La carpeta `data_geo/` se genera automáticamente al ejecutar el notebook.
Los archivos SOFT descargados pueden conservarse para evitar
descargarlos nuevamente en ejecuciones futuras: GEOparse detecta
si el archivo ya existe y lo carga desde disco sin repetir la descarga.
