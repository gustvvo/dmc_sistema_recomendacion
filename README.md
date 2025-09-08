# 📌 Sistema de Recomendación Híbrido con MovieLens 100K

## 📖 Introducción
Este proyecto implementa un **sistema de recomendación híbrido** utilizando el dataset **MovieLens 100K**.  
El objetivo es comparar distintos enfoques de recomendación:  
- **Basado en embeddings (colaborativo)**  
- **Híbrido (embeddings + contenido de géneros)**  

y evaluar cuál ofrece mejores resultados en la predicción de ratings y en la calidad de las recomendaciones.

---

## 📊 Dataset
Se utilizó **MovieLens 100K**, un dataset clásico en sistemas de recomendación que contiene:  
- **100.000 ratings** de películas.  
- **943 usuarios** y **1.682 películas**.  
- Metadata de películas: títulos, géneros.  
- Metadata de usuarios: edad, género, ocupación, código postal.  

Fuente: [MovieLens](https://www.kaggle.com/datasets/prajitdatta/movielens-100k-dataset/data)

---

## ⚙️ Metodología

### 1. Análisis exploratorio
- Distribución de ratings (sesgo hacia valores altos).  
- Actividad de usuarios (mayoría con pocas reviews).  
- Popularidad de películas (cola larga: pocas con muchas reviews).  

### 2. Modelo de Embeddings
- Representación de usuarios y películas como vectores.  
- Red neuronal densa para predecir ratings.  
- Entrenamiento con **MSE** y early stopping.

### 3. Modelo Híbrido
- Combina **embeddings** con **contenido de géneros** de cada película.  
- Entrada adicional con vector binario de géneros.  
- Red neuronal con capas densas.  

### 4. Evaluación
- Métricas de error: **RMSE, MAE**.  
- Métricas de ranking: **Precision@K, Recall@K, NDCG@K**.  

---

## 📈 Resultados

### A) Error de predicción
| Modelo       | RMSE   | MAE   |
|--------------|--------|-------|
| Embeddings   | 0.9348 | 0.7344 |
| Híbrido      | 0.9221 | 0.7237 |

➡️ El sistema **híbrido mejora ligeramente** respecto al de embeddings.

### B) Métricas de ranking (ejemplo con K=10)
| Modelo       | Precision@10 | Recall@10 | NDCG@10 |
|--------------|--------------|-----------|----------|
| Embeddings   | 0.215        | 0.132     | 0.186   |
| Híbrido      | 0.227        | 0.141     | 0.193   |

➡️ El híbrido recomienda contenido más relevante en el top-N.

---

## 🎬 Ejemplos de uso

### 1. Predicción de rating para un usuario existente
```python
user_id = 115
title   = "Toy Story (1995)"
pred = predict_rating(hybrid, user_id, title, catalogo, user2idx, item2idx)
print(pred)  # Ejemplo -> 3.32
```

### 2. Top-N recomendaciones para un usuario
```python
recs = recomendar_topn_usuario(hybrid, user_id=115, n=5)
print(recs)
```

Ejemplo de salida:
```
movie_id  title                                  pred_rating
320       Paradise Lost: The Child Murders...    5.0
1536      Aiqing wansui (1994)                  5.0
1189      Prefontaine (1997)                    5.0
1631      Slingshot, The (1993)                 5.0
1398      Anna (1996)                           5.0
```

---


---

## 📂 Estructura del repositorio
```
📂 SistemasRecomendacion
 ┣ 📜 README.md
 ┣ 📜 DMC_SistemasRecomendacion_ML100K.ipynb
 ┗ 📂 data/
     ┣ u.data
     ┣ u.item
     ┗ u.user
```

---

## 📌 Conclusiones
- El sistema **híbrido mejora la calidad de las predicciones** respecto a un modelo puramente colaborativo.  
- El uso de información adicional (géneros, ocupación) enriquece las recomendaciones.  
- Futuras mejoras: incorporar embeddings de texto de descripciones, o información demográfica.  
