# Corpus de datos de los Bienes de Interés Cultural de Canarias en los proyectos Wikimedia

Este repositorio contiene un conjunto de datos que se ha denominado *Corpus de datos de los Bienes de Interés Cultural de Canarias en los proyectos Wikimedia*. Concretamente contiene datos de los bienes de interés cultural de Canarias extraídos con la herramienta WikiCorpus de Wikipedia en español, Wikidata y Wikimedia Commons.

Su objetivo principal ha sido el análisis de los datos curados para la investigación del trabajo de fin de máster *Estado del conocimiento libre sobre el patrimonio cultural de Canarias en Wikipedia, Wikimedia Commons y Wikidata. Los Bienes de Interés Cultural de Canarias en los Proyectos Wikimedia*.

Este repositorio contiene tres archivos CSV:

  - `datos_preliminares.csv`
  - `qid_bics_wikidata.csv`
  - `corpus_bics_wikidata_commons_eswiki.csv`

A continuación se describe cada archivo y columna de los datos que componen cada conjunto de datos.

## `datos_preliminares.csv`

Elementos de los bienes de interés cultural de Canarias disponibles en Wikidata. Fueron extraídos a partir del Wikidata Query Service con la siguiente consulta SPARQL:

```sparql
SELECT ?bic ?bic_denominacion ?eswiki_titulo ?eswiki_url ?id_bic ?id_bic_canarias WHERE {
  ?location (wdt:P31/(wdt:P279*)) wd:Q2074737;
    (wdt:P131+) ?province.
  ?bic (wdt:P1435/(wdt:P279*)) wd:Q23712;
    (wdt:P131+) ?location;
    rdfs:label ?bic_denominacion.
  FILTER((LANG(?bic_denominacion)) = "es")
  OPTIONAL {
    ?eswiki_url schema:about ?bic;
      schema:isPartOf <https://es.wikipedia.org/>;
      schema:name ?eswiki_titulo.
  }
  OPTIONAL { ?bic wdt:P808 ?id_bic. }
  OPTIONAL { ?bic wdt:P7006 ?id_bic_canarias. }
  VALUES ?province {
    wd:Q95080
    wd:Q99976
  }
}
ORDER BY (?bic)
```

Se compone de las siguientes columnas:

  - `bic`. URL del elemento.
  - `bic_denominación`. Etiqueta en español del elemento.
  - `eswiki_titulo`. Título del artículo en Wikipedia en español, si tiene artículo.
  - `eswiki_url`. URL del artículo en Wikipedia en español, si tiene artículo.
  - `id_bic`. Identificador de bien de interés cultural (P808).
  - `id_bic_canarias`. Identificador de bien de interés cultural de Canarias (P7006).

## `qid_bics_wikidata`

Identificadores de los elementos extraídos de Wikidata para su posterior uso en la herramienta que extrajo los datos de `corpus_bics_wikidata_commons_eswiki.csv`.

  - `id`. Identificador numérico.
  - `qid`. Identificador del elemento de Wikidata (se obtuvo tras haber limpiado la URL del campo `bic` en `datos_preliminares` con una expresión regular).

## `corpus_bics_wikidata_commons_eswiki.csv`

Conjunto de los diversos datos extraídos de Wikidata, Wikimedia Commons y Wikipedia en español a partir de la herramienta WikiCorpus. Se compone de 32 columnas de datos.

  - `id`. Identificador numérico para cada fila.
  - `articulo`. Titulo del artículo en Wikipedia en español, si tiene artículo.
  - `tamano_bytes`. Tamaño del artículo en bytes.
  - `tamano_palabras`. Tamaño del artículo en palabras (solo el texto, no cuenta la sintaxis).
  - `fecha_creacion`. Fecha de creación del artículo.
  - `id_creacion`. Identificador (oldid) de la primera versión del artículo.
  - `url_creacion`. URL de la primera versión del artículo.
  - `fecha_ultima_revision`. Fecha de la última revisión del artículo.
  - `id_ultima_revision`. Identificador (oldid) de la última revisión del artículo.
  - `url_ultima_revision`. URL de la última revisión del artículo.
  - `editores_anonimos`. Cantidad de editores anónimos (sin registrar) que han editado el artículo.
  - `editores_registrados`. Cantidad de editores registrados que han editado el artículo.
  - `editor_principal`. Editor que más ediciones ha realizado en el artícuo.
  - `discusion`. Título de la página de discusión del artículo (con el espacio de nombres incluído), si tiene página de discusión.
  - `discusion_tamanho_bytes`. Tamaño de la página de discusión del artículo en bytes.
  - `discusion_tamanho_palabras`. Tamaño de la página de discusión del artículo en palabras.
  - `enlaces_a`. Cantidad de enlaces a otras páginas.
  - `enlaces_de`. Cantidad de enlaces al artículo.
  - `imagenes_cantidad`. Cantidad de imágenes en el artículo.
  - `referencias`. Cantidad de referencias en el artículo.
  - `bibliografía`. Cantidad de obras en la bibliografía.
  - `wikidata_id`. Identificador del elemento de Wikidata.
  - `wikidata_etiquetas`. Cantidad de etiquetas del elemento de Wikidata.
  - `wikidata_descripciones`. Cantidad de descripciones del elemento de Wikidata.
  - `wikidata_declaraciones`. Cantidad de declaraciones del elemento de Wikidata.
  - `wikidata_declaraciones_P143`. Cantidad de declaraciones del elemento de Wikidata con una referencia marcada por la propiedad P143.
  - `wikidata_declaraciones_referencias`. Cantidad de declaraciones del elemento de Wikidata con referencias (incluye las marcadas con la P143).
  - `wikidata_identificadores_externos`. Cantidad de identificadores externos del elemento de Wikidata.
  - `wikidata_interwiki`. Cantidad de enlaces interwiki (enlaces a otros proyectos Wikimedia) del elemento de Wikidata.
  - `commons_categoria`. Categoría del elemento en Wikimedia Commons, si tiene.
  - `commons_archivos`. Cantidad de archivos en la categoría de Wikimedia Commons (nivel de recursión 3).
  - `commons_subcats`. Cantidad de subcategorías en la categoría de Wikimedia Commons (nivel de recursión 3).

## Licencia

El *Corpus de datos de los Bienes de Interés Cultural de Canarias en los proyectos Wikimedia* está disponible bajo la **Open Data Commons Public Domain Dedication and License (PDDL)**: https://opendatacommons.org/licenses/pddl/
