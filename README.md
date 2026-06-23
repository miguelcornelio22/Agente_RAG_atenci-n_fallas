📘 Proyecto RAG – Historial de Fallas SAP
Este proyecto implementa un pipeline RAG (Retrieval-Augmented Generation) para consultar y generar órdenes de trabajo a partir del historial de fallas de equipos industriales.

El flujo está diseñado para:

Ingestar documentos PDF con fallas históricas.

Fragmentar cada falla como un chunk semántico.

Enriquecer cada chunk con metadata útil (equipo, ubicación, criticidad, tipo de falla, solución).

Generar embeddings normalizados para mejorar la similitud semántica.

Almacenar en Elasticsearch con búsqueda híbrida (texto + vector + filtros).

📌 Arquitectura del Pipeline
Enriquecimiento de metadata  
Cada falla se convierte en un Document con atributos adicionales:

equipo_id, nombre_equipo, ubicacion, criticidad, fecha.

tipo_falla (arranque, presión, vibración, sobrecalentamiento, etc.).

solucion.

Esto permite filtrar resultados con precisión y trazabilidad.

Fragmentación semántica  
Se usa RecursiveCharacterTextSplitter para dividir el documento en chunks de 500 caracteres con solapamiento de 50.
Cada chunk corresponde a una falla completa (fecha + descripción + solución).

Embeddings normalizados  
Antes de generar embeddings, se normaliza vocabulario técnico:

“fuga de aceite” → “fuga lubricante”

“caída de tensión” → “problema eléctrico”

“fallo en arranque” → “problema arranque”

Esto mejora la similitud entre fallas que usan términos distintos pero equivalentes.

Almacenamiento híbrido en Elasticsearch  
Se combina búsqueda vectorial con filtros por metadata.
Ejemplo: si el reporte dice “Generador EQA-2004 no arranca”, se filtra por equipo_id=EQA-2004 y tipo_falla=arranque.
Así se evita recuperar fallas irrelevantes.
