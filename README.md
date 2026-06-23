# 🛠️ Proyecto M4 – Pipeline RAG con Historial de Fallas SAP

Este proyecto implementa un **pipeline RAG (Retrieval-Augmented Generation)** para la gestión de fallas históricas en la industria de hidrocarburos, diseñado con **LangChain**, **Python** y **Elasticsearch**.  
Su objetivo es mejorar la **precisión y relevancia en la recuperación de evidencia técnica**, permitiendo generar órdenes de trabajo más completas y preventivas.

---

## 🌍 Contexto e importancia
La industria de hidrocarburos requiere sistemas confiables para el mantenimiento de equipos críticos.  
El historial de fallas en SAP contiene información valiosa que, si se aprovecha con IA, puede transformar la gestión de mantenimiento:

- **Prevención de incidentes** mediante análisis de patrones históricos.  
- **Optimización de tiempos de respuesta** en órdenes de trabajo.  
- **Mayor trazabilidad** gracias a metadata enriquecida y búsqueda híbrida.  

---

## ⚙️ Arquitectura del sistema

**Componentes principales:**
1. **Ingesta de documentos PDF** con historial de fallas SAP.  
2. **Fragmentación semántica** con `RecursiveCharacterTextSplitter`.  
3. **Enriquecimiento de metadata**: equipo, ubicación, criticidad, fecha, tipo de falla, solución.  
4. **Normalización de texto técnico** para mejorar similitud semántica.  
5. **Embeddings** con `text-embedding-3-large`.  
6. **Almacenamiento híbrido en Elasticsearch** (vector + metadata).  
7. **Recuperación de evidencia relevante** con filtros por equipo y tipo de falla.  
8. **Generación de órdenes de trabajo** con notas preventivas basadas en patrones históricos.  

---

## 🚀 Beneficios del M4
- **Precisión**: recupera únicamente fallas relacionadas con el reporte.  
- **Escalabilidad**: permite añadir más equipos y fallas sin modificar la lógica.  
- **Trazabilidad**: cada chunk incluye metadata completa.  
- **Prevención**: facilita recomendaciones dinámicas para mantenimiento preventivo.  

---

## 📊 Ejemplo de flujo
Un reporte indica: *“El generador EQA-2004 en Planta Lima no arranca y muestra caída de tensión”*.  
El pipeline RAG:  
- Filtra por `equipo_id=EQA-2004` y `tipo_falla=arranque`.  
- Recupera fallas históricas relevantes (ej. arranque y tensión).  
- Genera una orden de trabajo con evidencia técnica y nota preventiva.  

---

## 👨‍💻 Autor
**Miguel – Hidrocarburos del Perú**  
Trabajo académico y técnico para optimizar la gestión de fallas en sistemas industriales mediante IA generativa y RAG.
