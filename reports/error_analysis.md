# Error Analysis — IT Ticket NLP (Baseline v0.1)

## Contexto
- Modelo: **TF-IDF (1–2 grams, min_df=2) + LogisticRegression**
- Métricas (test): **Macro F1 = 0.852**, **Weighted F1 = 0.8582**
- Clases: 8 (Hardware, HR Support, Access, Miscellaneous, Storage, Purchase, Internal Project, Administrative rights)

## Top confusiones (fuera de la diagonal)
Las confusiones más frecuentes del baseline (conteos) son:

1) **HR Support → Hardware**: 172  
2) **Miscellaneous → Hardware**: 142  
3) **Administrative rights → Hardware**: 109  
4) **Hardware → HR Support**: 106  
5) **Access → Hardware**: 97  
6) **Hardware → Miscellaneous**: 74  
7) **Miscellaneous → HR Support**: 74  
8) **HR Support → Miscellaneous**: 55  
9) **Storage → Hardware**: 52  
10) **Purchase → Hardware**: 46  

## Interpretación (qué significa en negocio)
- **Hardware funciona como “catch-all”**: muchas categorías terminan prediciéndose como Hardware (ej. HR Support, Misc, Admin rights, Access).  
  → En operación, esto causaría **sobrecarga del equipo de Hardware** y tickets mal enroutados.
- Hay **solapamiento semántico** entre áreas (ej. HR Support ↔ Hardware, Hardware ↔ Misc).  
  → El texto puede contener términos comunes (“issue”, “request”, “support”) que el modelo no separa bien.
- **Administrative rights** es una clase más difícil (F1 más bajo) y se confunde sobre todo con Hardware.  
  → Probablemente requiere señales más específicas (keywords como “admin”, “privileges”, “rights”, “permissions”).

## Acciones recomendadas (próximos experimentos)
1) **Modelo alterno**: probar **LinearSVC** (suele mejorar en texto con TF-IDF).
2) **Balanceo**: probar `class_weight="balanced"` para reducir sesgo hacia clases grandes (como Hardware).
3) **Features de texto**:
   - añadir **char n-grams** (ej. 3–5) o combinar word+char para capturar variaciones/typos.
   - revisar `min_df` y regularización (`C`) para mejorar separación.
4) **Human-in-the-loop**: si la “confianza” es baja (probabilidad máxima < umbral), mandar a revisión humana en vez de enrutar mal.
5) **Segmentación ligera** (si se requiere): primer paso “Hardware vs No-Hardware”, luego clasificar el resto (enrutamiento jerárquico).
