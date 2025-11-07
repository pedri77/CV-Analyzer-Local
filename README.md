# CV Experience Scorer
MVP para evaluar experiencia desde CVs (PDF/DOCX/TXT), extraer empresas, tecnologías, skills y generar Excel.
## Cómo usar
1) `pip install -r requirements.txt`
2) `python app/gradio_app.py` → UI web local
3) Procesado en lote: `python scripts/demo_batch.py --input data/raw --out outputs/excel/CV_valuation_batch.xlsx`
