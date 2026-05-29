# casiriorg.github.io

Sitio web y documentación de [CASIRI](https://casiriorg.github.io) — Corporation for Aerospace Initiatives, Research and Innovation.

Construido con [MkDocs Material](https://squidfunk.github.io/mkdocs-material/).

## Estructura

```
casiriorg.github.io/
├── docs/
│   ├── index.md                          # Homepage principal
│   ├── projects/
│   │   └── index.md                      # Índice de proyectos
│   ├── docs/
│   │   └── qiskit-data-reuploading/
│   │       ├── index.md                  # Intro del proyecto QDR
│   │       └── api.md                    # API autodoc (mkdocstrings)
│   ├── assets/
│   │   ├── logo.svg
│   │   └── custom.css
│   └── overrides/                        # Plantillas MkDocs custom
├── .github/
│   └── workflows/
│       └── deploy-docs.yml               # CI/CD → GitHub Pages
├── mkdocs.yml
└── requirements.txt
```

## Desarrollo local

```bash
pip install -r requirements.txt

# Clonar el repo de código fuente para autodoc
git clone --depth=1 https://github.com/Carlosandp/qiskit-data-reuploading.git \
  qiskit-data-reuploading-src
cd qiskit-data-reuploading-src && pip install -e . && cd ..

# Servidor local con hot-reload
mkdocs serve
```

El sitio queda disponible en `http://localhost:8000`.

## Deployment

El sitio se despliega automáticamente vía GitHub Actions:
- Al hacer push a `main`
- Manualmente desde la pestaña **Actions → Deploy CASIRI Docs → Run workflow**

Configurar en GitHub: **Settings → Pages → Source: GitHub Actions**
