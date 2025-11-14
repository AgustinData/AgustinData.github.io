# 📈 Análisis de Datos de Viajes - Caso de Estudio Cyclistic

## Resumen Ejecutivo
Este proyecto se centra en el servicio de bicicletas compartidas Cyclistic de Chicago. El objetivo principal es analizar las **diferencias en los patrones de uso** entre **Miembros Anuales** (Subscribers) y **Ciclistas Ocasionales** (Customers) para desarrollar estrategias de marketing dirigidas a **convertir clientes ocasionales en miembros anuales**.

---

## 🔬 Metodología y Herramientas

El análisis se basó en el marco de trabajo *Ask, Prepare, Process, Analyze, Share, Act* (Preguntar, Preparar, Procesar, Analizar, Actuar).

| Fase | Tarea Clave | Habilidades y Herramientas |
| :--- | :--- | :--- |
| **Preparación y Procesamiento** | Carga y limpieza de datos brutos del Q1 de 2019. Se manejaron inconsistencias de formato de fecha/hora, valores atípicos en la duración de los viajes (`tripduration`), y valores extremos en la edad. | **RStudio**, Paquetes `tidyverse`, `lubridate`, Manejo de `NA`s y *Outliers*. |
| **Análisis** | Cálculo de la duración promedio de viajes (`ride_length`), análisis de uso por día de la semana (`day_of_week`) y visualización de la demanda mensual por tipo de usuario. | Agrupación (`group_by`), Resumen estadístico, `ggplot2` (Visualización). |

---

## 🔑 Descubrimientos e Insights Clave

Los datos revelan una diferencia fundamental en el comportamiento de los usuarios:

* **Uso Ocasional vs. Rutinario:** Los **Clientes Ocasionales** tienen una duración promedio de viaje significativamente mayor (**35.3 minutos**) que los **Miembros Anuales** (**11.3 minutos**).
    * **Insight:** Esto sugiere que los Miembros Anuales usan el servicio para trayectos cortos y rutinarios (trabajo), mientras que los Clientes Ocasionales lo usan para actividades recreativas (viajes largos, fines de semana).
* **Demanda por Día:** Los Miembros Anuales dominan el uso durante los **días de la semana**, mientras que los Clientes Ocasionales muestran un pico de uso notable en los **fines de semana** (especialmente el sábado).
* **Aumento Estacional:** Ambos grupos experimentan un fuerte aumento en la demanda en **Marzo**, anticipando la temporada alta de primavera/verano.

## 💡 Recomendaciones de Negocio (Fase Actuar)

1.  **Programa de Lealtad:** Implementar un sistema de seguimiento para Clientes Ocasionales. Ofrecer un **descuento anual** o un **primer mes gratis** después de que el usuario alcance un número determinado de viajes.
2.  **Campaña de Fines de Semana:** Desarrollar una campaña de marketing específica para los fines de semana, destacando cómo la membresía anual puede reducir el costo de los viajes recreativos.
3.  **Promoción Estacional:** Lanzar promociones y descuentos al comienzo de la primavera (ej. **Marzo**) para capitalizar el aumento natural de clientes ocasionales.

---

## 📊 Documentación y Visualizaciones

El informe técnico completo, que incluye el código R y todas las visualizaciones generadas, se encuentra disponible en:

[**Ver Análisis Completo (index.md)**](index.md)
