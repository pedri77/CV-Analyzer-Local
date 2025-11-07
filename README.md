# CV Experience Scorer
MVP para evaluar experiencia desde CVs (PDF/DOCX/TXT), extraer empresas, tecnologías, skills y generar Excel.

## Cómo usar
1) `pip install -r requirements.txt`
2) `python app/gradio_app.py` → UI web local
3) Procesado en lote: `python scripts/demo_batch.py --input data/raw --out outputs/excel/CV_valuation_batch.xlsx`

## Uso rápido

Procesar un archivo:
```
python cv_analyzer.py --input "samples/CV_Juan.pdf" --out "resultados"
```

Procesar una carpeta con varios CVs:
```
python cv_analyzer.py --input "./samples" --out "./resultados"
```

Ver solo por pantalla (sin exportar):
```
python cv_analyzer.py --input "CV_Ana.docx" --no-save
```

Parámetros útiles:
```
python cv_analyzer.py --help
```

## Salidas

resultados/cv_analysis.csv — tabla consolidada

resultados/json/<nombre>.json — detalle por CV

Campos principales: filename, name_guess, email, phone, linkedin, github, years_experience, skills_hard_found, skills_soft_found, education_level, certifications_found, languages_found, score_total, score_breakdown.

## Estrategias de análisis

Extracción de texto: PDF (PyMuPDF), DOCX (python-docx), TXT.

Contacto: email, teléfono, LinkedIn, GitHub via regex.

Experiencia: busca rangos de fechas ("ene 2020 – mar 2022", "2018-Actual", etc.), calcula años acumulados; si falla, estima desde el año más antiguo encontrado.

Habilidades: match por presencia (normalizado a minúsculas) contra listas técnicas/soft/ciber. Evita duplicados y cuenta cobertura.

Educación: detecta grado, máster, doctorado, ingeniería, etc. Asigna nivel.

Certificaciones: detecta CISSP, CISM, CEH, OSCP, CompTIA Security+, AZ-500, SC-200, etc.

Idiomas: español, inglés, francés, alemán, italiano, portugués; detecta niveles C1, B2, nativo, etc.

Puntuación: ponderaciones configurables (ver config.yaml).

## Notas y mejoras futuras

Añadir fuzzy matching para skills (rapidfuzz) y normalización de sinónimos.

Extraer organizaciones/roles con patrones adicionales (NER local: spaCy offline).

Detector de brechas (meses sin empleo) y cálculo por posición.

Exportación adicional a Excel (XLSX) con formato y filtros.
