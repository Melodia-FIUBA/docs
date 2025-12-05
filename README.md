# 🎵 Melodia - Documentación del Proyecto

Este repositorio contiene la documentación técnica de Melodia, una plataforma de streaming de música desarrollada como proyecto académico en FIUBA.

## 🌐 Sitio Desplegado

La documentación está disponible en: **[https://melodia-fiuba.github.io/docs/](https://melodia-fiuba.github.io/docs/)**

## 📚 Contenido

La documentación incluye:

- **Arquitectura**: Visión general del sistema e infraestructura en GCP
- **Roadmap**: Progreso del proyecto por checkpoints
- **Decisiones y Aprendizajes**: ADRs y lecciones aprendidas
- **Contratos de API**: Documentación OpenAPI de los servicios
- **Servicios**: Documentación detallada de cada componente
  - Mobile App (React Native)
  - Admin Backoffice (Next.js)
  - Content Service (Python/Flask)
  - Users Service (Go)
  - Admin Service (Go)

## 🛠️ Desarrollo Local

### Requisitos

- Python 3.11+
- pip

### Instalación

```bash
# Clonar el repositorio
git clone https://github.com/Melodia-FIUBA/docs.git
cd docs

# Crear entorno virtual (opcional pero recomendado)
python -m venv venv
source venv/bin/activate  # Linux/Mac
# o: venv\Scripts\activate  # Windows

# Instalar dependencias
pip install -r requirements.txt
```

### Ejecutar localmente

```bash
# Iniciar servidor de desarrollo
mkdocs serve

# El sitio estará disponible en http://localhost:8000
```

### Construir sitio estático

```bash
mkdocs build
# Los archivos se generan en el directorio 'site/'
```

## 🚀 Deployment

El sitio se despliega automáticamente a GitHub Pages cuando se hace push a la rama `main`.

El workflow de GitHub Actions (`.github/workflows/deploy-docs.yml`) se encarga de:

1. Instalar dependencias
2. Construir el sitio con MkDocs
3. Desplegar a GitHub Pages

## 📁 Estructura del Proyecto

```
docs/
├── mkdocs.yml              # Configuración de MkDocs
├── requirements.txt        # Dependencias de Python
├── README.md              # Este archivo
├── .github/
│   └── workflows/
│       └── deploy-docs.yml # GitHub Action para deployment
└── docs/
    ├── index.md           # Página principal
    ├── architecture.md    # Arquitectura del sistema
    ├── roadmap.md         # Roadmap y checkpoints
    ├── decisions-and-learnings.md  # Decisiones y aprendizajes
    ├── api-contracts.md   # Contratos de API
    ├── known-issues.md    # Problemas conocidos
    ├── services/          # Documentación por servicio
    │   ├── mobile-app.md
    │   ├── admin-backoffice.md
    │   ├── songs-service.md
    │   ├── users-service.md
    │   └── admin-service.md
    ├── assets/
    │   └── diagrams/      # Diagramas e imágenes
    └── openapi/           # Especificaciones OpenAPI
```

## 🤝 Contribuir

Para contribuir a la documentación:

1. Crear una rama desde `main`
2. Realizar los cambios en los archivos `.md`
3. Verificar localmente con `mkdocs serve`
4. Crear un Pull Request

### Convenciones

- Usar español para todo el contenido
- Seguir el formato de Markdown de MkDocs Material
- Utilizar admonitions (`!!! note`, `!!! warning`, etc.) para destacar información
- Incluir diagramas Mermaid cuando sea posible
- Marcar contenido pendiente con `<!-- TODO: descripción -->`

## 📖 Referencias

- [MkDocs](https://www.mkdocs.org/)
- [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/)
- [Mermaid](https://mermaid.js.org/)

## 📄 Licencia

Este proyecto es parte del trabajo práctico de la materia en FIUBA.
