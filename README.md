# tutorial_python_ES
Versión del Tutorial Oficial de Python en español con ajustes para facilitar la impresión "en papel".

El proceso consiste en exportar los archivos LaTex del bloque del tutorial, modificar algunas cuestiones generales (tamaño de la hoja, márgenes, colores, etc.) y luego generar un archivo `pdf` donde impactamos retoques finales.

# Paso a paso para construir el material
## Generar archivos 'base'
1. Crear una copia local del [repositorio oficial de la documentación](https://github.com/python/python-docs-es).
2. Modificar en `conf.py` la entrada 'latex_documents':
̣
```python
latex_documents = [
    ('tutorial/index', 'python-docs-es.tex', u'Documentación de Python en Español',
     _stdauthor, 'manual'),
]
```
3. Hacer un build local
```bash
make build
```
y luego ejecutar
```bash
sphinx-build -j auto -W --keep-going -b latex -d cpython/Doc/build/doctree/tutorial -D language=es . tutorial_latex
```
Si todo fue bien, en la ruta `.../tutorial_latex` tendremos todos los archivos necesarios para continuar el proceso (los mismos que están en este repositorio).

## Ajustes en archivos '.tex'
### python-docs-es.tex

`\documentclass[a5paper,10pt,spanish]{sphinxmanual}` tamaño de la hoja

`
\usepackage{geometry}
\geometry{
 right=20mm
 }` margen para imprimir 

`\title{Tutorial de Python}
\release{3.10}` información que se replica en los encabezados 

Quitamos los capítulos que no nos interesan y el índice se renderiza automáticamente. Eliminar todas las entradas desde la linea `#5678` (capítulos 14 y ss.) en adelante y finalizar el archivo con:
```
(...)
\renewcommand{\indexname}{Índice}
\printindex
\end{document}
```
---

### sphinxmessages.sty

`\renewcommand{\literalblockcontinuedname}{proviene de la página anterior}` texto quiebre de página en bloques de código.

`\renewcommand{\literalblockcontinuesname}{continúa en la próxima página}` texto quiebre de página en bloques de código.

---
### sphinx.sty

`\DeclareBoolOption[false]{verbatimwithframe}` quita recuadro en bloque de sintaxis

---
### sphinxhighlight.sty
En este archivo editamos el coloreado de los distintos elementos del documento. En principio comentamos (`%`) todas las entradas que definen colores específicos. Queda por defecto todo en B & N.

