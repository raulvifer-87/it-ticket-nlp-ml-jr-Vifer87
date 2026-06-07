# EDA (snapshot) — IT Ticket NLP

## Datos
- **Texto:** `Document`
- **Etiqueta (label):** `Topic_group`
- **Tamaño:** **47,837 filas**, **2 columnas**
- **# clases:** **8**

## Distribución de clases (Top)
| Clase | % |
|---|---:|
| Hardware | 28.47% |
| HR Support | 22.82% |
| Access | 14.89% |
| Miscellaneous | 14.76% |
| Storage | 5.81% |
| Purchase | 5.15% |
| Internal Project | 4.43% |
| Administrative rights | 3.68% |

**Nota:** hay desbalance (clases dominantes como Hardware/HR Support). Por eso usaremos **Macro F1** como métrica principal.

## Longitud del texto (caracteres)
- count: 47,837
- mean: 291.87
- 25%: 110
- 50% (mediana): 175
- 75%: 304
- max: 7015

**Nota:** existen tickets muy largos (outliers). Se evaluará si afectan el modelo o si conviene truncar/normalizar.

## Calidad de datos
- missing text: **0%**
- empty text: **0%**
- duplicates (Document+Topic_group): **0%**

## Hipótesis iniciales
- H1: El **desbalance de clases** hará que accuracy no sea suficiente → **Macro F1** será clave.
- H2: Tickets cortos/genéricos tenderán a confundirse entre categorías cercanas (ej. Access vs Administrative rights).
- H3: Algunas categorías se solapan semánticamente → el **error analysis** (confusion matrix + ejemplos) será importante.
