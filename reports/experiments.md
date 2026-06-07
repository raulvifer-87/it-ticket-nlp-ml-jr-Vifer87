# Experiments

## Baseline v0.1 — TF-IDF + LogisticRegression
- **Dataset:** IT Service Ticket Classification (47,837 filas, 8 clases)
- **Texto:** Document | **Label:** Topic_group
- **Split:** train/test 80/20 stratified
- **Modelo:** TF-IDF (ngram 1–2, min_df=2) + LogisticRegression (max_iter=2000)
- **Métricas (test):**
  - **Macro F1:** 0.852
  - **Weighted F1:** 0.8582

### Performance por clase (resumen)
- Mejores: Purchase (F1 0.92), Access (0.89), Storage (0.88)
- Más baja: Administrative rights (F1 0.73) → candidata para error analysis

## Próximo paso
- Confusion matrix + ejemplos de confusiones (error analysis).
- “Human-in-the-loop”: si la confianza del modelo es baja, mandar a revisión humana.

### Nota de error analysis (baseline)
- Principal patrón de error: múltiples categorías se predicen como **Hardware** (catch-all). Confusiones top: HR Support→Hardware (172), Misc→Hardware (142), Admin rights→Hardware (109).
