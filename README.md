# Assignment: Linear Models, Regularization, and Model Selection on Real Data

------------------------------------------------------------------------

Integrantes:

-   Calle Chambe, Efraín

-   Poma Huamán, Brayan

-   Sánchez Vásquez, Barbara Gabriela

------------------------------------------------------------------------

## **California Housing dataset**

### Differences observed between OLS, Ridge, and Lasso,

**Tabla comparativa de resultados:**

| Modelo    | MSE (test) | R² (test) | α óptimo |
|-----------|------------|-----------|----------|
| **OLS**   | 0.5410     | 0.6122    | –        |
| **Ridge** | 0.5296     | 0.62     | 2.95     |
| **Lasso** | 0.5275     | 0.62     | 0.0020   |

El modelo OLS alcanzó un R² de aproximadamente 0.61 y un MSE de 0.54, mostrando un ajuste aceptable pero con coeficientes de magnitudes variables, sensibles a la multicolinealidad, lo que puede afectar la estabilidad del modelo. Ridge, con un valor de $\alpha$ aproximado de 2.95, redujo ligeramente el MSE a 0.53 y mejoró la generalización mediante la regularización L2, que atenúa la magnitud de los coeficientes sin eliminarlos. Lasso, con $\alpha$ = 0.0020, obtuvo el menor MSE (0.527) y aplicó regularización L1, lo que permitió que algunos coeficientes se aproximaran a cero. Se concluye que Lasso tiene un mejor desempeño predictivo.

### Effect of learning rate on gradient descent,

| Learning Rate | Iteraciones hasta convergencia | MSE entrenamiento | MSE prueba | Intercept | Coeficientes aproximados |
|------------|------------|------------|------------|------------|------------|
| 0.1 | 319 | 0.2613 | 0.27297 | 2.0678 | [0.865, 0.131, -0.321, 0.329, -0.003, -0.042, -0.752, -0.727] |
| 0.5 | 127 | 0.2604 | 0.27092 | 2.0678 | [0.843, 0.120, -0.293, 0.312, -0.007, -0.040, -0.857, -0.829] |

Los resultados muestran que la tasa de aprendizaje influye principalmente en la velocidad de convergencia. Con lr=0.1, el algoritmo necesitó 319 iteraciones para alcanzar un MSE de 0.2613 en entrenamiento (0.27297 en prueba). Con lr=0.5, la convergencia se logró en 127 iteraciones, con un MSE de 0.2604 en entrenamiento (0.27092 en prueba). El incremento de la tasa de aprendizaje permitió entrenar más rápido sin comprometer la precisión final. Los coeficientes obtenidos fueron similares en ambos casos, indicando estabilidad en la solución.

### How k-fold cross-validation influenced the choice of regularization strength.

La validación cruzada k-fold permitió seleccionar de manera óptima los parámetros de regularización ($\alpha$) para Ridge y Lasso, evaluando su desempeño promedio en múltiples particiones del conjunto de entrenamiento. Los valores elegidos, ($\alpha$ $\approx$ 2.95) para Ridge y $\alpha = 0.0020$ para Lasso, lograron un MSE en los datos de prueba de 0.5695 y 0.5710, respectivamente. Este procedimiento garantiza que la elección de la fuerza de regularización no dependa de una única división de los datos, mejorando la generalización del modelo y asegurando un balance adecuado entre sesgo y varianza.

## **Bike Sharing Dataset**

### Differences observed between OLS, Ridge, and Lasso,

**Tabla comparativa de resultados:**

| Modelo    | MSE (test) | R² (test) | α óptimo |
|-----------|------------|-----------|----------|
| **OLS**   | 12211.13   | 0.6122    | –        |
| **Ridge** | 12212.19   | 0.6338   | 0.356    |
| **Lasso** | 12215.97   | 0.6336   | 0.013    |

La diferencia entre OLS, Ridge y Lasso muestra que todos presentan un desempeño similar en términos de MSE y $R^2$. El mejor modelo predictivo por ambas métricas vendria a ser ridge con un MSE de 12212.19 y un $R^2$ de 0.6338

### Effect of learning rate on gradient descent

| Learning Rate | Iteraciones hasta convergencia | MSE entrenamiento | MSE prueba | Intercept | Coeficientes aproximados |
|-----------|-----------|-----------|-----------|-----------|----------------|
| 0.1 | 1000 | \~6105.67 | 6105.67 | 188.547 | [16.388704, 10.426479, 27.738264, 0.498610, 1.179913, -1.777242, 0.689219, -5.776548, -11.307775, -3.768983, 4.216896, 1.679653, -3.983107, -1.867605, -3.309437, -4.789661, -6.570931, -7.203518, -4.024512, 7.562784, 33.948856, 61.727191, 32.014363, 21.198611, 25.191184, 31.769104, 32.203086, 28.131251, 30.898966, 42.506397, 73.807346, 66.026030, 45.309592, 30.351972, 20.669661, 13.670216, 6.232204, -3.674303, -1.054040, 0.089983, 0.912045, 0.713237, 2.121629, 4.541010, 3.418760, -2.576848, -16.807694, -0.478131, 56.605290, -22.011795, -5.644515] |
|  |  |  |  |  |  |
| 0.5 | 500 | \~6105.59 | 6105.59 | 188.547 | [16.485627, 10.557036, 27.820999, 0.474379, 1.125250, -1.878353, 0.577022, -5.901218, -11.454861, -3.911709, 4.089084, 1.586332, -4.068718, -1.930094, -3.302955, -4.783034, -6.564106, -7.196486, -4.016584, 7.570441, 33.955929, 61.734048, 32.019660, 21.202457, 25.194064, 31.771189, 32.204070, 28.131694, 30.899211, 42.506711, 73.808268, 66.027533, 45.312282, 30.355673, 20.673688, 13.674694, 6.237189, -3.675377, -1.054257, 0.088486, 0.911155, 0.711733, 2.122686, 4.540268, 3.416883, -2.579506, -16.807043, -0.478981, 56.659096, -22.010082, -5.644550] |
|  |  |  |  |  |  |

El estudio del efecto de la tasa de aprendizaje sobre el descenso por gradiente indica que tanto una tasa de 0.1 como de 0.5 permiten que el modelo converja a coeficientes muy cercanos a los obtenidos por OLS. Esto evidencia que, para este dataset, el proceso de optimización es estable ante variaciones moderadas en la tasa de aprendizaje, logrando un MSE prácticamente idéntico en los datos de prueba.

### How k-fold cross-validation influenced the choice of regularization strength.
La validación cruzada k-fold permitió seleccionar de manera óptima los parámetros de regularización ($\alpha$) para Ridge y Lasso, evaluando su desempeño promedio en múltiples particiones del conjunto de entrenamiento. Los valores elegidos, $\alpha \approx 0.356$ para Ridge y $\alpha \approx 0.013$ para Lasso, lograron un MSE en los datos de prueba de 12212.19 y 12215.97, respectivamente.