# Bioinformatica2025
Vamos a realizar un análisis ANOVA para comparar parámetros estructurales entre dos proteínas:
4DUW: Proteína de unión a ADN (Cold shock protein) de Bacillus subtilis
3WIK: Proteína de unión a ARN (Cold shock protein) de Thermotoga maritima
Ambas son proteínas de choque frío (cold shock proteins) pero de diferentes organismos y con diferentes ligandos (ADN vs ARN). El análisis ANOVA nos permitirá determinar si existen diferencias estadísticamente significativas en parámetros como factores B (medida de la movilidad atómica), longitudes de enlace, ángulos o torsion entre estas dos estructuras.
# Base de datos
library(bio3d)
library(ggplot2)
