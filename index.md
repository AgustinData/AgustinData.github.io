# Caso de estudio: Cyclist 2019

## Agustín Parard Rodriguez

# Introducción

En el contexto actual, donde la movilidad urbana es un factor crucial para las grandes ciudades, los sistemas de bicicletas compartidas han emergido como una solución sostenible y eficiente. Cyclistic, un servicio de bicicletas compartidas en Chicago, ha demostrado ser exitoso en atraer a una amplia gama de usuarios, incluyendo tanto a ciclistas ocasionales como a miembros anuales.

Este informe se centra en analizar los patrones de uso de la empresa ficticia de bicicletas Cyclistic entre estos dos grupos de usuarios. El objetivo principal es comprender cómo los ciclistas ocasionales y los miembros anuales utilizan las bicicletas de manera diferente, con la finalidad de diseñar estrategias de marketing que fomenten la conversión de ciclistas ocasionales en miembros anuales. A través de un análisis detallado de los datos de uso recopilados durante los primeros tres meses de 2019, este informe pretende proporcionar información clave para impulsar el crecimiento y la rentabilidad del servicio.

# **Fase “Preguntar”**

### **Definición del Problema:**

El equipo de Cyclistic y las partes interesadas quieren encontrar la manera de atraer más clientes anuales, ya sea convirtiendo clientes ocasionales en clientes anuales o atrayendo nuevos clientes. Para esto, es esencial conocer la diferencia entre los clientes ocasionales y los anuales, entender sus motivos, y encontrar la manera de convertirlos en clientes anuales, ya que a largo plazo será más rentable.

### **Preguntas Orientadoras:**

¿De qué manera diferente utilizan las bicicletas Cyclistic los miembros anuales y los ciclistas ocasionales?

¿Por qué los ciclistas ocasionales comprarían membresías anuales de Cyclistic?

¿Cómo puede Cyclistic utilizar los medios digitales para influir en los ciclistas ocasionales para que se conviertan en miembros?

### **Partes Interesadas Clave:**

**Lily Moreno (Directora de Marketing):** Diseñará estrategias comerciales enfocadas en convertir a los ciclistas ocasionales en ciclistas anuales.

**Equipo de análisis de marketing:** Utilizará los datos y el análisis para informar la estrategia de marketing.

**Equipo ejecutivo de Cyclistic:** Aprobará las recomendaciones basándose en los hallazgos y análisis realizados por el analista de datos.

## **Declaración de la Tarea Comercial:**

"Analizar las diferencias en el uso del servicio de bicicletas compartidas Cyclistic entre ciclistas ocasionales y miembros anuales. Esta información será utilizada para diseñar estrategias de marketing que conviertan a los ciclistas ocasionales en miembros anuales, aumentando así la rentabilidad y el crecimiento de la empresa."

# Fase “Preparar”

Los datos son brindados por la empresa Motivate International Inc., una empresa no ficticia y bien establecida en el sector de la movilidad compartida. Esto asegura la fiabilidad y precisión de los datos. Estos se encuentran disponibles públicamente y fueron descargados desde el portal de datos abiertos. 

Utilizare el archivo correspondiente a los tres primeros meses del año 2019 (debido a limitaciones técnicas), que contiene información detallada de cada viaje realizado en ese periodo. 
Los datos están organizados en archivos CSV comprimidos en un archivo ZIP llamado `Divvy_Trips_2019_Q1.zip` . Cada fila en el archivo CSV representa un viaje individual e incluye detalles como el ID del viaje, la duración del viaje, las estaciones de inicio y fin, el tipo de usuario (cliente ocasional o miembro anual), y otra información demográfica como el género y el año de nacimiento del usuario.
Para cumplir con los estándares de privacidad de los datos, no se incluyen ningún tipo de información de identificación personal (PII) , como nombre, diereccion, número de tarjeta, etc.

Nota: Aunque el análisis se limita a los datos de los tres primeros meses de 2019 debido a limitaciones técnicas, estos datos proporcionan una muestra representativa y suficiente para identificar patrones de uso y desarrollar estrategias de marketing efectivas.

# Fase “Procesar”

Para realizar la fase de procesamiento y análisis de datos, opté por utilizar RStudio, una herramienta robusta y eficiente para el manejo de grandes volúmenes de datos. A diferencia de Google Sheets o Excel, RStudio me permitió procesar el conjunto de datos de manera óptima. Esta elección fue fundamental para asegurar la precisión y eficiencia en el análisis.

Nota: Durante la elaboración de este proyecto, cometí un pequeño error tipográfico al referirme a la empresa en algunas secciones, utilizando "Cyclist" en lugar de "Cyclistic". Sin embargo, este error no afectó en absoluto el análisis, ya que todos los archivos de datos y procesos utilizados mantenían el nombre correcto, y no hubo ningún impacto en los resultados o conclusiones presentados.

#Instalo y cargo los paquetes necesarios para el análisis
install.packages("tidyverse")
install.packages("lubridate")
install.packages("readr")

library(tidyverse)
library(lubridate)
library(readr)

#Verifico el directorio de trabajo actual
getwd()

```r
[1] "/cloud/project"
```

#Cambio el directorio de trabajo
setwd("/cloud/project/cyclist_2019_Q1")

#Listo los archivos del nuevo directorio de trabajo
list.files()

```r
[1] "Divvy_Trips_2019_Q1.csv"
```

#Cargo el conjunto de datos
trim_2019 <- read.csv("/cloud/project/cyclist_2019_Q1/Divvy_Trips_2019_Q1.csv")

#Resumen de las columnas
glimpse(trim_2019)

```r
Rows: 365,069
Columns: 12
$ trip_id           <int> 21742443, 21742444, 21742445, 21742446, 21742447, 21742448, 21742449, 21…
$ start_time        <chr> "2019-01-01 00:04:37", "2019-01-01 00:08:13", "2019-01-01 00:13:23", "20…
$ end_time          <chr> "2019-01-01 00:11:07", "2019-01-01 00:15:34", "2019-01-01 00:27:12", "20…
$ bikeid            <int> 2167, 4386, 1524, 252, 1170, 2437, 2708, 2796, 6205, 3939, 6243, 6300, 3…
$ tripduration      <chr> "390.0", "441.0", "829.0", "1,783.0", "364.0", "216.0", "177.0", "100.0"…
$ from_station_id   <int> 199, 44, 15, 123, 173, 98, 98, 211, 150, 268, 299, 204, 90, 90, 289, 289…
$ from_station_name <chr> "Wabash Ave & Grand Ave", "State St & Randolph St", "Racine Ave & 18th S…
$ to_station_id     <int> 84, 624, 644, 176, 35, 49, 49, 142, 148, 141, 295, 420, 255, 255, 324, 3…
$ to_station_name   <chr> "Milwaukee Ave & Grand Ave", "Dearborn St & Van Buren St (*)", "Western …
$ usertype          <chr> "Subscriber", "Subscriber", "Subscriber", "Subscriber", "Subscriber", "S…
$ gender            <chr> "Male", "Female", "Female", "Male", "Male", "Female", "Male", "Male", "M…
$ birthyear         <int> 1989, 1990, 1994, 1993, 1994, 1983, 1984, 1990, 1995, 1996, 1994, 1994, …
```

#Observar las primeras filas del nuevo conjunto de datos
head(trim_2019)

```r
trip_id          start_time            end_time bikeid tripduration from_station_id
1 21742443 2019-01-01 00:04:37 2019-01-01 00:11:07   2167        390.0             199
2 21742444 2019-01-01 00:08:13 2019-01-01 00:15:34   4386        441.0              44
3 21742445 2019-01-01 00:13:23 2019-01-01 00:27:12   1524        829.0              15
4 21742446 2019-01-01 00:13:45 2019-01-01 00:43:28    252      1,783.0             123
5 21742447 2019-01-01 00:14:52 2019-01-01 00:20:56   1170        364.0             173
6 21742448 2019-01-01 00:15:33 2019-01-01 00:19:09   2437        216.0              98
                    from_station_name to_station_id                to_station_name   usertype
1              Wabash Ave & Grand Ave            84      Milwaukee Ave & Grand Ave Subscriber
2              State St & Randolph St           624 Dearborn St & Van Buren St (*) Subscriber
3                Racine Ave & 18th St           644  Western Ave & Fillmore St (*) Subscriber
4      California Ave & Milwaukee Ave           176              Clark St & Elm St Subscriber
5 Mies van der Rohe Way & Chicago Ave            35        Streeter Dr & Grand Ave Subscriber
6          LaSalle St & Washington St            49        Dearborn St & Monroe St Subscriber
  gender birthyear
1   Male      1989
2 Female      1990
3 Female      1994
4   Male      1993
5   Male      1994
6 Female      1983
```

#Columnas del conjunto de datos
colnames(trim_2019)

```r
[1] "trip_id"           "start_time"        "end_time"          "bikeid"           
 [5] "tripduration"      "from_station_id"   "from_station_name" "to_station_id"    
 [9] "to_station_name"   "usertype"          "gender"            "birthyear"       
```

#Resumen estadístico de cada columna
summary(trim_2019)

```r
trip_id          start_time          end_time             bikeid     tripduration      
 Min.   :21742443   Length:365069      Length:365069      Min.   :   1   Length:365069     
 1st Qu.:21848765   Class :character   Class :character   1st Qu.:1777   Class :character  
 Median :21961829   Mode  :character   Mode  :character   Median :3489   Mode  :character  
 Mean   :21960872                                         Mean   :3429                     
 3rd Qu.:22071823                                         3rd Qu.:5157                     
 Max.   :22178528                                         Max.   :6471                     
                                                                                           
 from_station_id from_station_name  to_station_id   to_station_name      usertype        
 Min.   :  2.0   Length:365069      Min.   :  2.0   Length:365069      Length:365069     
 1st Qu.: 76.0   Class :character   1st Qu.: 76.0   Class :character   Class :character  
 Median :170.0   Mode  :character   Median :168.0   Mode  :character   Mode  :character  
 Mean   :198.1                      Mean   :198.6                                        
 3rd Qu.:287.0                      3rd Qu.:287.0                                        
 Max.   :665.0                      Max.   :665.0                                        
                                                                                         
    gender            birthyear    
 Length:365069      Min.   :1900   
 Class :character   1st Qu.:1975   
 Mode  :character   Median :1985   
                    Mean   :1982   
                    3rd Qu.:1990   
                    Max.   :2003   
                    NA's   :18023  
```

#Ver la estructura del conjunto de datos
str(trim_2019)

```r
'data.frame':	365069 obs. of  12 variables:
 $ trip_id          : int  21742443 21742444 21742445 21742446 21742447 21742448 21742449 21742450 21742451 21742452 ...
 $ start_time       : chr  "2019-01-01 00:04:37" "2019-01-01 00:08:13" "2019-01-01 00:13:23" "2019-01-01 00:13:45" ...
 $ end_time         : chr  "2019-01-01 00:11:07" "2019-01-01 00:15:34" "2019-01-01 00:27:12" "2019-01-01 00:43:28" ...
 $ bikeid           : int  2167 4386 1524 252 1170 2437 2708 2796 6205 3939 ...
 $ tripduration     : chr  "390.0" "441.0" "829.0" "1,783.0" ...
 $ from_station_id  : int  199 44 15 123 173 98 98 211 150 268 ...
 $ from_station_name: chr  "Wabash Ave & Grand Ave" "State St & Randolph St" "Racine Ave & 18th St" "California Ave & Milwaukee Ave" ...
 $ to_station_id    : int  84 624 644 176 35 49 49 142 148 141 ...
 $ to_station_name  : chr  "Milwaukee Ave & Grand Ave" "Dearborn St & Van Buren St (*)" "Western Ave & Fillmore St (*)" "Clark St & Elm St" ...
 $ usertype         : chr  "Subscriber" "Subscriber" "Subscriber" "Subscriber" ...
 $ gender           : chr  "Male" "Female" "Female" "Male" ...
 $ birthyear        : int  1989 1990 1994 1993 1994 1983 1984 1990 1995 1996 ...
```

## Resumen

- **`trip_id`**: Es un entero, lo cual es correcto.
- **`start_time` y `end_time`**: Vemos que son `chr` (carácter), por lo que se debe convertir a un formato de fecha y hora (ymd, hms).
- **`bikeid`**: Es un entero, lo cual es correcto.
- **`tripduration`**: Es de tipo `chr` (carácter), y debe convertirse a numérico.
- **`from_station_id` y `to_station_id`**: Son enteros, lo cual es correcto.
- **`from_station_name` y `to_station_name`**: Son de tipo `chr` (carácter), lo cual es correcto.
- **`usertype`**: Es de tipo `chr` (carácter). Es necesario verificar los valores únicos para asegurarse de que no haya valores inesperados.
- **`gender`**: Es de tipo `chr` (carácter). Es necesario verificar los valores únicos para asegurarse de que no haya valores inesperados.
- **`birthyear`**: Es un entero, lo cual es correcto, pero se ve un año de nacimiento 1898, por lo que habría que investigar valores atípicos.

---

#Verificar los valores únicos en usertype
unique(trim_2019$usertype)

```r
[1] "Subscriber" "Customer"
```

#Verificar los valores únicos en gender
unique(trim_2019$gender)

```r
[1] "Male"   "Female" "" 
```

Podemos observar que al correr el código, este devuelve 3 valores en la columna gender, cuando debería haber 2, male y female.

#Contar el número de entradas con el valor vacío en la columna gender
sum(trim_2019$gender == "") 

```r
[1] 19711
```

19711 es la cantidad de valores vacios en la columna gender. Este valor representa un 5,4% del total de elementos en la columna gender, por lo que decidí mantener estos datos vacios y no eliminarlos ya que no influian significativamente en el resultado.

#Convertir start_time y end_time a formato datetime
trim_2019 <- trim_2019 %>%
mutate(start_time = ymd_hms(start_time),
end_time = ymd_hms(end_time))

#Verificar que las conversiones se realizaron correctamente
summary(trim_2019$start_time)

```r
                      Min.                    1st Qu.                     Median 
"2019-01-01 00:04:37.0000" "2019-01-23 05:26:54.0000" "2019-02-25 07:52:56.0000" 
                      Mean                    3rd Qu.                       Max. 
"2019-02-19 21:43:15.4156" "2019-03-17 16:52:47.0000" "2019-03-31 23:53:48.0000" 
```

#Verificar que las conversiones se realizaron correctamente
summary(trim_2019$end_time)

```r
                      Min.                    1st Qu.                     Median 
"2019-01-01 00:11:07.0000" "2019-01-23 05:49:40.0000" "2019-02-25 08:03:50.0000" 
                      Mean                    3rd Qu.                       Max. 
"2019-02-19 22:00:11.9056" "2019-03-17 17:16:16.0000" "2019-06-17 16:04:35.0000" 
```

#Convertir tripduration a numérico eliminando las comas
trim_2019 <- trim_2019 %>%
mutate(tripduration = as.numeric(gsub(",", "", tripduration)))

#Verificar los valores extremos de tripduration
summary(trim_2019$tripduration)

```r
Min.  1st Qu.   Median     Mean  3rd Qu.     Max. 
      61      326      524     1016      866 10628400 
```

Al ejecutar el código para obtener un resumen estadístico de la columna tripduration, se puede ver un valor extremadamente alto, exactamente 10628400 segundos igual a 123 días. Esto representa un valor ilógico para la duración de un viaje. Tomaremos como medida el valor de un día en segundos (ya que los datos están en esa unidad), ya que un viaje que dure lo mismo o más que un día no reflejaría la realidad, aunque puede darse el caso, es extremadamente improbable. En un día hay 86400 segundos, por lo que ese valor será la referencia para filtrar.

#Cargamos el paquete dplyr para realizar correctamente el filtrado
library(dplyr)

#Número de filas antes del filtrado
initial_rows <- nrow(trim_2019)
initial_rows

```r
[1] 364877
```

#Aplico el filtro
trim_2019 <- trim_2019 %>%
filter(tripduration <= 86400)
filtered_rows  <- nrow(trim_2019) 

```r
[1] 364877
```

#Verificar los valores extremos de tripduration después de la conversión
summary(trim_2019$tripduration)

```r
Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
   61.0   326.0   524.0   769.5   865.0 85984.0 
```

Vemos que el valor máximo es de 85984 segundos, equivale aproximadamente a un día. Es un valor alto considerando un viaje en bicicleta, pero no es totalmente improbable por lo que lo conservaremos.

#Resumen de birthyear
summary(trim_2019$birthyear)

```r
 Min. 1st Qu.  Median    Mean 3rd Qu.    Max.    NA's 
   1900    1975    1985    1982    1990    2003   18023 
```

Como se vio antes, existe una fecha de nacimiento de 1900, lo cual podria tratarse de un error. Tomaremos ese año como filtro. Si hay valores menores a 1900, se los asignara como valores nulos (NA)

#Considerar años de nacimiento menores a 1900 como NA
trim_2019 <- trim_2019 %>%
mutate(birthyear = ifelse(birthyear < 1900, NA, birthyear))

#Verificar el resumen de birthyear después del tratamiento
summary(trim_2019$birthyear)

```r
   Min. 1st Qu.  Median    Mean 3rd Qu.    Max.    NA's 
   1900    1975    1985    1982    1990    2003   17966 
```

Volvió a aparecer un valor alto para la edad de una persona (119 años hasta el 2019). Esta vez el año 1920 será el filtro.

#Considerar años de nacimiento menores a 1920 como NA
trim_2019 <- trim_2019 %>%
mutate(birthyear = ifelse(birthyear < 1920, NA, birthyear))

#Verificar el resumen de birthyear después del tratamiento
summary(trim_2019$birthyear)

```r
 Min. 1st Qu.  Median    Mean 3rd Qu.    Max.    NA's 
   1921    1975    1985    1982    1990    2003   18077
```

Creamos las columnas `day_of_week` y `ride_length`

#Crear la columna day_of_week
trim_2019 <- trim_2019 %>%
mutate(day_of_week = weekdays(start_time))

#Crear la columna ride_length en minutos
trim_2019 <- trim_2019 %>%
mutate(ride_length = as.numeric(difftime(end_time, start_time, units = "mins")))

#Verificar que se hayan creado correctamente las filas
head(trim_2019)

```r
trip_id          start_time            end_time bikeid tripduration from_station_id
1 21742443 2019-01-01 00:04:37 2019-01-01 00:11:07   2167          390             199
2 21742444 2019-01-01 00:08:13 2019-01-01 00:15:34   4386          441              44
3 21742445 2019-01-01 00:13:23 2019-01-01 00:27:12   1524          829              15
4 21742446 2019-01-01 00:13:45 2019-01-01 00:43:28    252         1783             123
5 21742447 2019-01-01 00:14:52 2019-01-01 00:20:56   1170          364             173
6 21742448 2019-01-01 00:15:33 2019-01-01 00:19:09   2437          216              98
                    from_station_name to_station_id                to_station_name   usertype
1              Wabash Ave & Grand Ave            84      Milwaukee Ave & Grand Ave Subscriber
2              State St & Randolph St           624 Dearborn St & Van Buren St (*) Subscriber
3                Racine Ave & 18th St           644  Western Ave & Fillmore St (*) Subscriber
4      California Ave & Milwaukee Ave           176              Clark St & Elm St Subscriber
5 Mies van der Rohe Way & Chicago Ave            35        Streeter Dr & Grand Ave Subscriber
6          LaSalle St & Washington St            49        Dearborn St & Monroe St Subscriber
  gender birthyear day_of_week ride_length
1   Male      1989     Tuesday    6.500000
2 Female      1990     Tuesday    7.350000
3 Female      1994     Tuesday   13.816667
4   Male      1993     Tuesday   29.716667
5   Male      1994     Tuesday    6.066667
6 Female      1983     Tuesday    3.600000
```

#Resumen estadístico de ride_length y day_of_week
summary(trim_2019$ride_length)

```r
 Min.  1st Qu.   Median     Mean  3rd Qu.     Max. 
   1.017    5.433    8.733   12.826   14.417 1433.067 
```

#Resumen estadístico de ride_length y day_of_week
summary(trim_2019$day_of_week)

```r
   Length     Class      Mode 
   364877 character character 
```

#Contar las ocurrencias de cada día de la semana
table(trim_2019$day_of_week)

```r
 Friday    Monday  Saturday    Sunday  Thursday   Tuesday Wednesday 
    63018     50383     35257     27977     66872     60978     60392 
```

# Fase **“Analizar”**

#Calcular la media de ride_length
mean_ride_length <- mean(trim_2019$ride_length, na.rm = TRUE)

#Ver los resultados
mean_ride_length

```r
[1] 12.82654
```

#Calcular la máxima ride_length
max_ride_length <- max(trim_2019$ride_length, na.rm = TRUE)

#Ver los resultados
max_ride_length

```r
[1] 1433.067
```

#Calcular la moda de day_of_week
mode_day_of_week <- as.character(names(sort(table(trim_2019$day_of_week), decreasing = TRUE)[1]))
mode_day_of_week

```r
[1] "Thursday"
```

#Calcular la ride_length promedio para miembros y pasajeros ocasionales
avg_ride_length_by_user <- trim_2019 %>%
group_by(usertype) %>%
summarize(avg_ride_length = mean(ride_length, na.rm = TRUE))

#Ver los resultados
print(avg_ride_length_by_user)

```r
# A tibble: 2 × 2
  usertype   avg_ride_length
  <chr>                <dbl>
1 Customer              35.3
2 Subscriber            11.3
```

#Calcular la ride_length promedio por día de la semana
avg_ride_length_by_day <- trim_2019 %>%
group_by(day_of_week) %>%
summarize(avg_ride_length = mean(ride_length, na.rm = TRUE)) %>%
arrange(match(day_of_week, c("Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday", "Sunday")))

#Ver los resultados
print(avg_ride_length_by_day)

```r
# A tibble: 7 × 2
  day_of_week avg_ride_length
  <chr>                 <dbl>
1 Monday                 11.9
2 Tuesday                12.4
3 Wednesday              12.1
4 Thursday               12.0
5 Friday                 12.3
6 Saturday               16.9
7 Sunday                 15.0
```

#Calcular la cantidad de viajes por día de la semana
trip_count_by_day <- trim_2019 %>%
group_by(day_of_week) %>%
summarize(trip_count = n())

#Ver los resultados
print(trip_count_by_day)

```r
# A tibble: 7 × 2
  day_of_week trip_count
  <chr>            <int>
1 Friday           63018
2 Monday           50383
3 Saturday         35257
4 Sunday           27977
5 Thursday         66872
6 Tuesday          60978
7 Wednesday        60392
```

#Crear una visualización para la cantidad de viajes por día de la semana
ggplot(trip_count_by_day, aes(x = day_of_week, y = trip_count, fill = day_of_week)) +
geom_bar(stat = "identity") +
labs(title = "Cantidad de Viajes por Día de la Semana",
x = "Día de la Semana",
y = "Cantidad de Viajes") +
theme_minimal()

![cantidad viajes x dof.png](Caso%20de%20estudio%20Cyclist%202019%20ae13c39c1d684b1ca0dbe64d8b0353aa/cantidad_viajes_x_dof.png)

#Calcular la cantidad de cada tipo de usuario
user_counts <- trim_2019 %>%
group_by(usertype) %>%
summarize(count = n())

#Ver los resultados
print(user_counts)

```r
# A tibble: 2 × 2
  usertype    count
  <chr>       <int>
1 Customer    23095
2 Subscriber 341782
```

#Calcular la cantidad de viajes por día de la semana y tipo de usuario
trip_count_by_day_user <- trim_2019 %>%
group_by(day_of_week, usertype) %>%
summarize(trip_count = n())

#Ordenar los días de la semana
trip_count_by_day_user$day_of_week <- factor(trip_count_by_day_user$day_of_week,
levels = c("Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday", "Sunday"))

#Crear una visualización de barras apiladas para visualizar el uso por tipo de usuario en diferentes días de la semana
ggplot(trip_count_by_day_user, aes(x = day_of_week, y = trip_count, fill = usertype)) +
geom_bar(stat = "identity", position = "stack") +
labs(title = "Cantidad de Viajes por Día de la Semana y Tipo de Usuario",
x = "Día de la Semana",
y = "Cantidad de Viajes") +
theme_minimal()

![customer vs subs 2.png](Caso%20de%20estudio%20Cyclist%202019%20ae13c39c1d684b1ca0dbe64d8b0353aa/customer_vs_subs_2.png)

#Crear la columna month
trim_2019 <- trim_2019 %>%
mutate(month = format(start_time, "%B"))

#Verificar las primeras filas para asegurarse de que la columna se ha creado correctamente
head(trim_2019)

```r
trip_id          start_time            end_time bikeid tripduration from_station_id
1 21742443 2019-01-01 00:04:37 2019-01-01 00:11:07   2167          390             199
2 21742444 2019-01-01 00:08:13 2019-01-01 00:15:34   4386          441              44
3 21742445 2019-01-01 00:13:23 2019-01-01 00:27:12   1524          829              15
4 21742446 2019-01-01 00:13:45 2019-01-01 00:43:28    252         1783             123
5 21742447 2019-01-01 00:14:52 2019-01-01 00:20:56   1170          364             173
6 21742448 2019-01-01 00:15:33 2019-01-01 00:19:09   2437          216              98
                    from_station_name to_station_id                to_station_name   usertype
1              Wabash Ave & Grand Ave            84      Milwaukee Ave & Grand Ave Subscriber
2              State St & Randolph St           624 Dearborn St & Van Buren St (*) Subscriber
3                Racine Ave & 18th St           644  Western Ave & Fillmore St (*) Subscriber
4      California Ave & Milwaukee Ave           176              Clark St & Elm St Subscriber
5 Mies van der Rohe Way & Chicago Ave            35        Streeter Dr & Grand Ave Subscriber
6          LaSalle St & Washington St            49        Dearborn St & Monroe St Subscriber
  gender birthyear day_of_week ride_length   month
1   Male      1989     Tuesday    6.500000 January
2 Female      1990     Tuesday    7.350000 January
3 Female      1994     Tuesday   13.816667 January
4   Male      1993     Tuesday   29.716667 January
5   Male      1994     Tuesday    6.066667 January
6 Female      1983     Tuesday    3.600000 January
```

#Calcular la cantidad de viajes por mes y tipo de usuario
trip_count_by_month_user <- trim_2019 %>%
group_by(month, usertype) %>%
summarize(trip_count = n())

#Ordenar los meses
trip_count_by_month_user$month <- factor(trip_count_by_month_user$month,
levels = [month.name](http://month.name/))

#Ver los resultados
print(trip_count_by_month_user)

```r
# A tibble: 6 × 3
# Groups:   month [3]
  month    usertype   trip_count
  <fct>    <chr>           <int>
1 February Customer         2627
2 February Subscriber      93522
3 January  Customer         4591
4 January  Subscriber      98601
5 March    Customer        15877
6 March    Subscriber     149659
```

#Crear una visualización para la cantidad de viajes por mes y tipo de usuario
ggplot(trip_count_by_month_user, aes(x = month, y = trip_count, fill = usertype)) +
geom_bar(stat = "identity", position = "stack") +
labs(title = "Cantidad de Viajes por Mes y Tipo de Usuario",
x = "Mes",
y = "Cantidad de Viajes") +
theme_minimal() +
theme(axis.text.x = element_text(angle = 45, hjust = 1))

![88ef08e2-e2f5-4a67-afd3-29b32d211fe3.png](Caso%20de%20estudio%20Cyclist%202019%20ae13c39c1d684b1ca0dbe64d8b0353aa/88ef08e2-e2f5-4a67-afd3-29b32d211fe3.png)

#Filtrar los datos para obtener solo a los clientes ocasionales
casual_customers <- trim_2019 %>%
filter(usertype == "Customer")

#Contar la cantidad de viajes por sexo
gender_count <- casual_customers %>%
group_by(gender) %>%
summarize(count = n())

#Ver los resultados
print(gender_count)

```r
# A tibble: 3 × 2
  gender   count
  <chr>    <int>
1 ""       17171
2 "Female"  1872
3 "Male"    4052
```

Como deberían haber 2 valores en la comuna `gender` pero hay 3, filtramos los valores vacíos que anteriormente decidimos conservar por ser estos un pequeño porcentaje.

#Filtrar los valores vacíos en la columna gender
gender_count_filtered <- gender_count %>%
filter(gender != "")

#Crear un gráfico de barras para visualizar el uso por sexo, excluyendo valores vacíos
ggplot(gender_count_filtered, aes(x = gender, y = count, fill = gender)) +
geom_bar(stat = "identity") +
labs(title = "Cantidad de Viajes por Sexo - Clientes Ocasionales",
x = "Sexo",
y = "Cantidad de Viajes") +
theme_minimal()

![1a84b11d-79d3-4430-a2c7-61848bcac38c.png](Caso%20de%20estudio%20Cyclist%202019%20ae13c39c1d684b1ca0dbe64d8b0353aa/1a84b11d-79d3-4430-a2c7-61848bcac38c.png)

# Fase “Actuar”

## Descubrimientos

- El jueves es el día con más viajes, y globalmente, los días de la semana con más tránsito son martes y jueves.
- El recorrido promedio es de 12.8 minutos.
- El recorrido promedio para clientes ocasionales es de 35.3 minutos, mientras que para los clientes anuales es de 11.3 minutos. Esto sugiere que los clientes ocasionales utilizan el servicio más para actividades recreativas, mientras que los clientes anuales probablemente lo usen de manera más rutinaria, como para ir al trabajo, lo que explica un tiempo de viaje más corto.
- Hay 341,782 clientes anuales y 23,095 clientes ocasionales, lo que representa el 6.76% de clientes ocasionales.
- Los clientes anuales utilizan el servicio más durante la semana, con un notable descenso en los fines de semana, lo que refuerza la hipótesis de que lo usan principalmente para ir al trabajo. Por otro lado, los clientes ocasionales muestran un patrón opuesto, con un mayor uso durante los fines de semana, especialmente los sábados.
- Tanto los clientes ocasionales como los anuales muestran un uso similar en enero y febrero, pero experimentan un fuerte aumento en marzo, posiblemente debido a la mejora del clima.*
- Hay más del doble de hombres que mujeres entre los clientes ocasionales.

* Un análisis basado en un solo trimestre, como el realizado en este estudio, puede proporcionar una visión útil de los patrones de uso a corto plazo, pero tiene limitaciones importantes cuando se trata de capturar la variabilidad estacional a lo largo de un año completo. La demanda de un servicio de bicicletas compartidas está fuertemente influenciada por las condiciones climáticas, que varían significativamente entre estaciones. Durante el invierno, la menor demanda podría no reflejar la actividad durante los meses más cálidos, como el verano, cuando el uso del servicio podría aumentar considerablemente.

## Recomendaciones

- Registrar la cantidad de viajes que hace cada cliente ocasional, esto con el fin de enfatizar un descuento anual, con algún descuento adicional los primeros meses (o el primer mes gratis por ejemplo), al llegar a cierta cantidad de viajes, o de tiempo transcurrido utilizando el servicio.
- Implementar un descuento en el comienzo de la primavera, para aprovechar la llegada de clientes ocasionales que van a usar las bicicletas en los meses más cálidos.
- Impulsar una campaña de marketing en aquellas estaciones de bicicletas que son más concurridas por los clientes ocasionales.
- Desarrollar una campaña de marketing específica durante los fines de semana, cuando los clientes ocasionales están más activos, destacando los beneficios de una membresía anual.