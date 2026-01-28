# Luminosidad Estelar: Modelos Lineales y Polinomiales para Regresión

## Descripción del Proyecto

Este proyecto implementa algoritmos de regresión lineal y polinomial desde los primeros principios para modelar la luminosidad estelar en función de la masa y temperatura. La implementación se realiza sin utilizar bibliotecas de aprendizaje automático de alto nivel, desarrollando explícitamente las funciones de hipótesis, pérdida y optimización mediante descenso de gradiente.

El problema estudiado se inspira en la relación masa-luminosidad de estrellas en la secuencia principal, donde la luminosidad crece de manera no lineal con la masa estelar, y la temperatura introduce efectos adicionales de interacción.

## Contexto

Este trabajo se desarrolla en el marco de un Bootcamp de Aprendizaje Automático de cuatro semanas, integrado en un curso sobre Transformación Digital y Arquitectura Empresarial. El proyecto aborda el aprendizaje automático como una capacidad arquitectónica fundamental en sistemas empresariales modernos, donde la inteligencia se considera un atributo de calidad de primer nivel junto con escalabilidad, disponibilidad, seguridad y rendimiento.

## Estructura del Repositorio

```
/
├── README.md
├── Part1_dataset_one_feature.ipynb
└── Part2_dataset_two_features.ipynb
```

## Contenido de los Notebooks

### Part1_dataset_one_feature.ipynb

Implementación de regresión lineal simple para modelar la luminosidad estelar en función de la masa:

**Modelo:** L̂ = w · M + b

**Contenido:**
- Visualización y análisis exploratorio del conjunto de datos (M vs L)
- Implementación de la función de predicción y cálculo del error cuadrático medio (MSE)
- Visualización de la superficie de costo J(w,b) en 3D y contornos
- Derivación e implementación de gradientes ∂J/∂w y ∂J/∂b
- Descenso de gradiente no vectorizado (con bucle explícito)
- Descenso de gradiente vectorizado (usando operaciones NumPy)
- Análisis de convergencia con gráficos de pérdida vs iteraciones
- Experimentos con tres tasas de aprendizaje diferentes
- Visualización del ajuste final y análisis de residuos
- Respuestas a preguntas conceptuales sobre el significado astrofísico de los parámetros

**Resultados principales:**
- Modelo óptimo: w ≈ 19.3 L☉/M☉, b ≈ -11.5 L☉
- MSE final: ~2.31
- Se identifican errores sistemáticos evidenciando la inadecuación del modelo lineal

### Part2_dataset_two_features.ipynb

Implementación de regresión polinomial con ingeniería de características para capturar efectos no lineales:

**Modelo:** L̂ = X · w + b

**Características consideradas:** X = [M, T, M², M·T]

**Contenido:**
- Visualización del conjunto de datos con temperatura codificada por color
- Construcción de matriz de diseño con características polinomiales
- Implementación vectorizada de MSE y gradientes
- Descenso de gradiente con análisis de convergencia
- Experimento de selección de características comparando tres modelos:
  - M1: X = [M, T]
  - M2: X = [M, T, M²]
  - M3: X = [M, T, M², M·T]
- Análisis del costo en función del coeficiente de interacción M·T
- Demostración de inferencia con predicción de luminosidad para nuevas estrellas

**Resultados principales:**
- Modelo M3 muestra el mejor ajuste con MSE mínimo
- El término de interacción M·T resulta significativo para capturar la física del problema
- Las predicciones son confiables dentro del rango de entrenamiento

## Conjunto de Datos

**Parte I (una característica):**
- M: [0.6, 0.8, 1.0, 1.2, 1.4, 1.6, 1.8, 2.0, 2.2, 2.4] M☉
- L: [0.15, 0.35, 1.00, 2.30, 4.10, 7.00, 11.2, 17.5, 25.0, 35.0] L☉

**Parte II (dos características):**
- M: [0.6, 0.8, 1.0, 1.2, 1.4, 1.6, 1.8, 2.0, 2.2, 2.4] M☉
- T: [3800, 4400, 5800, 6400, 6900, 7400, 7900, 8300, 8800, 9200] K
- L: [0.15, 0.35, 1.00, 2.30, 4.10, 7.00, 11.2, 17.5, 25.0, 35.0] L☉

## Implementación Técnica

### Bibliotecas Permitidas
- Python estándar
- NumPy (operaciones matriciales y vectoriales)
- Matplotlib (visualización únicamente)

### Restricciones
No se utilizan bibliotecas de aprendizaje automático de alto nivel como:
- scikit-learn
- statsmodels
- TensorFlow/PyTorch
- Bibliotecas de regresión u optimización predefinidas

### Características Técnicas
- Implementación desde primeros principios de todas las funciones
- Vectorización completa usando NumPy para eficiencia computacional
- Cálculo explícito de gradientes mediante derivación matemática
- Optimización mediante descenso de gradiente con tasa de aprendizaje configurable

## Evidencia de Ejecución en AWS SageMaker

![image-example](Images/image.png)

### Procedimiento de Carga

Los notebooks fueron cargados exitosamente a AWS SageMaker mediante el siguiente procedimiento:

1. Acceso a la consola de AWS SageMaker Studio
2. Uso de dominio existente de SageMaker 
3. Lanzamiento de un entorno de Jupyter Notebook
4. Carga de los archivos `.ipynb` mediante la interfaz de SageMaker
5. Selección del kernel Python 3 para ejecución

### Ejecución en la Nube

Ambos notebooks fueron ejecutados exitosamente en AWS SageMaker sin errores:

- **Part1_dataset_one_feature.ipynb**: Todas las celdas ejecutadas correctamente
- **Part2_dataset_two_features.ipynb**: Todas las celdas ejecutadas correctamente

### Capturas de Pantalla



### Comparación: Ejecución Local vs SageMaker

**Similitudes:**
- Ambos entornos ejecutan el código de manera idéntica
- Los resultados numéricos son consistentes entre plataformas
- Las visualizaciones se renderizan correctamente en ambos casos

**Diferencias observadas:**
- SageMaker proporciona un entorno preconfigurado con todas las bibliotecas necesarias
- La infraestructura en la nube permite escalabilidad para conjuntos de datos mayores
- El entorno local requiere instalación manual de dependencias


## Resultados y Conclusiones

### Regresión Lineal
El modelo lineal proporciona una primera aproximación, pero presenta limitaciones fundamentales:
- No captura la verdadera relación no lineal L ∝ M^α
- Presenta errores sistemáticos con patrón en "U"
- Limitado para extrapolación fuera del rango de entrenamiento

### Regresión Polinomial
El modelo polinomial con características de interacción mejora significativamente el ajuste:
- Captura efectos no lineales mediante el término M²
- El término de interacción M·T es físicamente significativo
- Mejor capacidad predictiva dentro del rango de entrenamiento
- Requiere precaución en extrapolación

### Significado Astrofísico
Los modelos desarrollados reflejan aspectos fundamentales de la física estelar:
- La relación masa-luminosidad en estrellas de secuencia principal
- El efecto de la temperatura efectiva en la emisión radiativa
- La naturaleza no lineal de los procesos de fusión nuclear

## Requisitos del Sistema

- Python 3.8+
- NumPy 1.20+
- Matplotlib 3.3+
- Jupyter Notebook / JupyterLab
- AWS SageMaker 

## Autor
Maria Juliana Rodriguez Caicedo
Escuela Colombiana De Ingenieria Julio Garavito

