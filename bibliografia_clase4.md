# Bibliografía — Clase 4: Regularización y GLMs

**Maestría en Bioinformática y Biología de Sistemas — UNQ**
**Reconocimiento de Patrones en Bioinformática**

---

## Lectura previa recomendada (30 min)

- **Capítulos 3.4 (Ridge), 3.4.2 (Lasso) y 18.4 de "The Elements of Statistical Learning"** (Hastie, Tibshirani, Friedman). PDF gratuito: https://hastie.su.domains/ElemStatLearn/

- **Tibshirani, R. (1996).** *Regression shrinkage and selection via the lasso.* JRSS-B, 58(1), 267–288. El paper original de Lasso. Pesa leer la introducción.

---

## Profundización por tema

### Ridge

- **Hoerl, A. E. & Kennard, R. W. (1970).** *Ridge regression: Biased estimation for nonorthogonal problems.* Technometrics, 12(1), 55–67. El paper fundacional.

### Lasso y Elastic Net

- **Zou, H. & Hastie, T. (2005).** *Regularization and variable selection via the elastic net.* JRSS-B, 67(2), 301–320. El paper original de Elastic Net.

- **Friedman, J., Hastie, T. & Tibshirani, R. (2010).** *Regularization Paths for Generalized Linear Models via Coordinate Descent.* Journal of Statistical Software 33(1). El paper de `glmnet`. Súper práctico.

### Aplicaciones en bioinformática

- **Wu, T. T., Chen, Y. F., Hastie, T., Sobel, E. & Lange, K. (2009).** *Genome-wide association analysis by lasso penalized logistic regression.* Bioinformatics, 25(6), 714–721.

- **Bøvelstad, H. M. et al. (2007).** *Predicting survival from microarray data—a comparative study.* Bioinformatics 23(16), 2080–2087. Compara Ridge, Lasso, etc. en datos de supervivencia.

---

## Videos recomendados (verificados)

- **StatQuest — Regularization Part 1: Ridge (L2) Regression** (~20 min)
  https://www.youtube.com/watch?v=Q81RR3yKn30
  Explicación visual de Ridge.

- **StatQuest — Regularization Part 2: Lasso (L1) Regression** (~9 min)
  https://www.youtube.com/watch?v=NGf0voTMlcs
  Lasso siguiendo Ridge.

- **StatQuest — Ridge vs Lasso Regression, Visualized!!!** (~9 min)
  https://www.youtube.com/watch?v=Xm2C_gTAl8c
  La intuición geométrica L1 vs L2. **Imperdible para entender por qué Lasso selecciona.**

- **StatQuest — Regularization Part 3: Elastic Net Regression** (~5 min)
  https://www.youtube.com/watch?v=1dKRdX9bfIo

- **StatQuest — Ridge, Lasso and Elastic-Net Regression in R** (~17 min)
  https://www.youtube.com/watch?v=ctmNq7FgbvI
  Demo práctica en R. Los conceptos son idénticos para Python.

- **3Blue1Brown — Essence of linear algebra** (serie completa)
  https://www.youtube.com/playlist?list=PLZHQObOWTQDPD3MizzM2xVFitgF8hE_ab
  Para refrescar SVD, matrices y autovalores.

---

## Recursos técnicos

### Documentación de scikit-learn

- `Ridge`: https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.Ridge.html
- `Lasso`: https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.Lasso.html
- `ElasticNet`: https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.ElasticNet.html
- `LogisticRegression`: https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LogisticRegression.html
- Linear models user guide: https://scikit-learn.org/stable/modules/linear_model.html

### En R

- `glmnet`: https://glmnet.stanford.edu/articles/glmnet.html
  El paquete de referencia para regularización en estadística. El propio Hastie es uno de los autores.

### GLMs en general

- **statsmodels** (Python): https://www.statsmodels.org/stable/glm.html
  Más completo que sklearn para inferencia estadística (intervalos de confianza, p-values).

---

## FAQ pedagógico

**1. ¿Por qué Ridge no selecciona variables?**
- La penalización L2 es suave (parábola); el mínimo es interior, no en las "esquinas" del espacio. Por eso los coeficientes se encogen pero nunca son exactamente cero.

**2. ¿Por qué Lasso sí selecciona?**
- La penalización L1 tiene esquinas (rombo en 2D). El óptimo de la suma RSS + λ‖β‖₁ tiende a engancharse en esas esquinas, donde algunos $\beta_j = 0$ exactamente.

**3. ¿Cómo elijo entre Lasso, Ridge y Elastic Net?**
- Si esperás sparsidad fuerte (pocas variables relevantes): **Lasso**.
- Si esperás muchas variables relevantes con multicolinealidad: **Ridge**.
- Si esperás sparsidad PERO con grupos correlacionados: **Elastic Net**.
- En la duda: probá Elastic Net con CV, ajusta `l1_ratio` también.

**4. ¿Tengo que escalar las variables?**
- **Sí, siempre** que uses regularización. Si no, las variables con valores más grandes reciben más penalización (injusto).

**5. ¿C o α?**
- Convención inversa: `Lasso(alpha=...)` y `Ridge(alpha=...)` usan α (mayor = más regularización).
- `LogisticRegression(C=...)` y `SVC(C=...)` usan C = 1/α (mayor = MENOS regularización).
- Mirá siempre la documentación para no confundirte.

**6. ¿Qué pasa si tengo $p > n$ y aplico Ridge?**
- Funciona. La fórmula $(X^T X + \lambda I)^{-1}$ es invertible aunque $X^T X$ sea singular, porque $\lambda I$ "rellena" la diagonal.

**7. ¿Qué pasa con Lasso si $p > n$?**
- Lasso selecciona como máximo $n$ variables (limitación matemática). Para sparsidad más fuerte, eso es bueno; para mantener grupos correlacionados, malo.

**8. ¿Cómo combino regularización con CV anidado?**
- LassoCV/RidgeCV/ElasticNetCV hacen CV interno para elegir $\alpha$. Para tener una estimación honesta del rendimiento, los envolvés en otro CV externo. Esto lo vemos en Clase 6.
