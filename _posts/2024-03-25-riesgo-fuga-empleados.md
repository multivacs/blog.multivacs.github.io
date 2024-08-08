---
title: Prediciendo el Riesgo de fuga de Empleados con Machine Learning
description: Sistema que usando Machine Learning con algoritmos de árboles de decisión, calcula la probabilidad de que un empleado abandone la compañía.
author: mario
date: 2024-03-25 11:33:00 +0000
categories: [Data Science, Machine Learning]
tags: [machine learning, data science, tableau, python, riesgo, predictivos]
pin: false
math: false
mermaid: false
image:
  path: assets/img/posts/2024-03-25-riesgo-fuga-empleados/employee-churn.png
  alt: Employee Churn.
---

## Índice

- [Índice](#índice)
- [Introducción](#introducción)
- [Análisis del Problema con Business Analytics](#análisis-del-problema-con-business-analytics)
- [Implementación del Modelo de Machine Learning](#implementación-del-modelo-de-machine-learning)
- [Productivización con Tableau](#productivización-con-tableau)



## Introducción

Cuando un empleado decide abandonar una compañía, es importante saber cuál puede haber sido la causa, si se hubiesen podido implementar medidas preventivas y cuál ha sido el coste asociado, no solo por la pérdida de talento, sino también por el tiempo que requiere encontrar un sustituto.

Es por esto, que durante los últimos años, los modelos de análisis de datos, y más concretamente los modelos predictivos y de riesgo, han sido una herramienta muy útil para este tipo de problemas. 

Recientemente, me inscribí en el curso "Mi primera semana" de Data Science For Business, muy recomendado y con una metodología y enfoque muy prácticos. El objetivo del mismo era crear un sistema con un Dashboard interactivo en Tableau, alimentado con algoritmos de Machine Learning, que permitiese identificar rápidamente las palancas de acción con las que evitar una fuga de empleados.


## Análisis del Problema con Business Analytics

El primer paso en la fase de Business Analytics es identificar en qué punto nos encontramos actualmente, cuantificar el problema y generar _insights_ que nos ayuden a entender mejor el problema. Esta fase nos servirá también para detectar aquellas palancas de acción y KPIs que nos permitan dirigir nuestra solución a la zona de lo realizable _(feasible)_.

En nuestro caso, identificamos de los datos ficticios proporcionados en el curso, una tasa de abandono del 16% de los empleados, que traducido a coste monetario, según cifras de [Center for American Progress](https://www.americanprogress.org/article/there-are-significant-business-costs-to-replacing-employees/), de 2'7M de dólares.

Haciendo un análisis de cúal es el perfil medio que abandona la compañía vemos que los que se encuentran en mayor riesgo son aquellos que:
- No disponen de estudios superiories
- Sin pareja
- Pertenecen al departamento de ventas
- Salarios bajos
- Realizan horas extra

![Business Analytics Estudios](assets/img/posts/2024-03-25-riesgo-fuga-empleados/ba_1.png){: width="434" height="405" }
_Figura 1: Abandonos por estudios_

![Business Analytics Puesto](assets/img/posts/2024-03-25-riesgo-fuga-empleados/ba_3.png){: width="434" height="483" }
_Figura 2: Abandonos por puesto_


Con estos datos sobre la mesa, podemos preguntarnos cuál es ahorro esperado si aplicamos estrategias de retención sobre este primer perfil de riesgo que hemos identificado.
Si nos proponemos el objetivo de reducir en un 30% el porcentaje de abandono sobre el departamento comercial, vemos que podemos retribuir directamente un ahorro de coste de unos 37.000$ 

Pero esto es únicamente una primera estrategia, ya que podemos seguir ahondando en el problema todo lo que queramos, y plantearnos preguntas como ¿Cuál es el coste medio de abandono por año? ¿Cuánto le ha costado a la compañía en el último año? Si aplicamos una estrategia a tres años, en el que cada año reducimos la tasa en un 10%, ¿cuánto habremos ahorrado a la compañía?


## Implementación del Modelo de Machine Learning
Tras identificar el problema y visualizar las posibles soluciones, decidimos implementar una solución técnica, aplicando algoritmos de machine learning para predecir en base al histórico de datos de la compañía, cuál es el riesgo de abandono de un empleado a partir de su perfil.

Para este problema, utilizaremos los árboles de decisión debido a su interpretabilidad, que los hacen idóneos para poder comunicar de manera más fácil las posibles soluciones  aplicar, y cuál es la razón más probable por la que un empleado puede que renuncie.


![Machine Learning Tree](assets/img/posts/2024-03-25-riesgo-fuga-empleados/ml.png){: width="972" height="589" }
_Figura 3: Árbol de decisión_



## Productivización con Tableau
Finalmente, transformamos la salida de este algoritmo en un dashboard interactivo utilizando Tableau.
Podéis consultar el resultado en el siguiente enlace [Dashboard Turnover Risk](https://public.tableau.com/views/DashboardRiesgoFuga/Dashboard1)

![Producto Tableau](assets/img/posts/2024-03-25-riesgo-fuga-empleados/Dashboard.png){: width="972" height="589" }
_Figura 4: Dashboard con Tableau_

> El código fuente utilizado para este curso, es propiedad de [Data Science 4 Business](https://datascience4business.com/).
{: .prompt-tip }