# Análisis ANOVA de proteínas de choque frío
**Análisis comparativo de parámetros estructurales mediante ANOVA**

Se realizó un análisis de varianza (ANOVA) para evaluar diferencias estadísticamente significativas en los parámetros estructurales de dos proteínas homólogas de choque frío:

1. **Muestras de estudio**:
   - 4DUW: Cold shock protein de *Bacillus subtilis* (unión a ADN)
   - 3WIK: Cold shock protein de *Thermotoga maritima* (unión a ARN)

2. **Parámetros analizados**:
   - Factores de temperatura atómica (B-factors)
   - Geometría molecular (longitudes de enlace, ángulos de torsión)

4. **Enfoque metodológico**:
   - Diseño experimental unifactorial
   - Contraste de hipótesis con α=0.05
   - Pruebas post-hoc de Tukey para comparaciones múltiples

Este análisis permite cuantificar objetivamente las adaptaciones estructurales asociadas a diferencias funcionales y evolutivas entre estas proteínas relacionadas.

Los datos se obtuvieron directamente del Protein Data Bank (PDB):

4DUW: https://www.rcsb.org/structure/4DUW

3WIK: https://www.rcsb.org/structure/3WIK
## Paquetes 
```
# Instalar paquetes (si no están instalados)
if (!require("bio3d")) install.packages("bio3d")
if (!require("ggplot2")) install.packages("ggplot2")

# Cargar librerías
library(bio3d)    # Para manejar estructuras PDB
library(ggplot2)  # Para gráficos
```
## Descarga de datos 
```
# Descargar estructuras PDB
pdb_4duw <- read.pdb("4DUW")  # Proteína de B. subtilis (4DUW)
pdb_3wik <- read.pdb("3WIK")  # Proteína de T. maritima (3WIK)

# Extraer factores B (Cα backbone)
bfactor_4duw <- pdb_4duw$atom[pdb_4duw$calpha, "b"]
bfactor_3wik <- pdb_3wik$atom[pdb_3wik$calpha, "b"]
```
## Procesamiento de datos 
```
# Crear dataframe para ANOVA
data <- data.frame(
  bfactor = c(bfactor_4duw, bfactor_3wik),
  protein = factor(rep(c("4DUW", "3WIK"), 
                   times = c(length(bfactor_4duw), length(bfactor_3wik))))
```
## Visualización (Boxplot)
```
ggplot(data, aes(x = protein, y = bfactor, fill = protein)) +
  geom_boxplot() +
  labs(title = "Comparación de Factores B entre 4DUW y 3WIK",
       x = "Proteína",
       y = "Factor B") +
  theme_minimal()
```
![image](https://github.com/user-attachments/assets/13137930-c11c-4019-8487-9e2b9ecd5cc8)
**Análisis Comparativo de Factores B: Estructuras 4DUW vs 3WIK**

## Interpretación del boxplot (Factores B: 4DUW vs 3WIK):**

1. **Diferencias clave**:
   - 3WIK muestra mayor movilidad atómica (mediana más alta)
   - 4DUW tiene valores más consistentes (caja más compacta)

2. **Implicaciones**:
   - La proteína termófila (3WIK) es más flexible
   - Posibles adaptaciones a diferentes temperaturas ambientales

Las diferencias observadas en los factores B reflejan adaptaciones estructurales distintivas entre estos homólogos evolutivos, posiblemente relacionadas con sus diferentes entornos fisiológicos y mecanismos de unión a ácidos nucleicos.
## Pruebas de Normalidad (Shapiro-Wilk) 
```
shapiro_4duw <- shapiro.test(bfactor_4duw)
shapiro_3wik <- shapiro.test(bfactor_3wik)

print(paste("Shapiro-Wilk para 4DUW: p-value =", shapiro_4duw$p.value))
print(paste("Shapiro-Wilk para 3WIK: p-value =", shapiro_3wik$p.value))
```
