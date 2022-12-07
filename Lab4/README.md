# Основы обработки данных с помощью R

## Цель

1. Зекрепить практические навыки использования языка программирования R для обработки данных
2. Закрепить знания основных функций обработки данных экосистемы tidyverse языка R
3. Развить практические навыки использования функций обработки данных пакета dplyr – функции
select(), filter(), mutate(), arrange(), group_by()

## Исходные данные

RStudioCloud

## Код программы

```{r}
install.packages('nycflights13')
install.packages("dplyr")
```

### Задания 1-3

```{r}
library(nycflights13)
library(dplyr)

#Сколько встроенных в пакет nycflights13 датафреймов?
numb_of_df <- ls("package:nycflights13")
length(numb_of_df)

# Сколько строк в каждом датафрейме?
# Сколько столбцов в каждом датафрейме?
rows <- c(dim(airlines)[1], dim(airports)[1], dim(flights)[1], dim(planes)[1], dim(weather)[1])
columns <- c(dim(airlines)[2], dim(airports)[2], dim(flights)[2], dim(planes)[2], dim(weather)[2])
DF_struct <- data.frame(Dataframe = numb_of_df, Rows = rows, Columns = columns)

DF_struct
```

### Задание 4

```{r}
# Как просмотреть примерный вид датафрейма?
library(nycflights13)
glimpse(flights)
```

### Задание 5

```{r}
# Сколько компаний-перевозчиков (carrier) учитывают эти наборы данных (представлено в наборах данных)?
count(select(flights %>%
               group_by(carrier) %>%
               summarise(N = n()
                         )
             )
      )
```

### Задание 6

```{r}
# Сколько рейсов принял аэропорт John F Kennedy Intl в мае?
count(filter(flights,origin=='JFK', month == 5))
```

### Задание 7

```{r}
# Какой самый северный аэропорт?
airports$name[which.max(airports$lat)]
max(airports$lat)
```

### Задание 8

```{r}
# Какой аэропорт самый высокогорный (находится выше всех над уровнем моря)?
airports$name[which.max(airports$alt)]
```

### Задание 9

```{r}
# Какие бортовые номера у самых старых самолетов?
library(nycflights13)
#glimpse(planes)
select(planes,tailnum, -(year)) %>% top_n(10)
```

### Задание 10

```{r}
# Какая средняя температура воздуха была в сентябре в аэропорту John F Kennedy Intl (в градусах Цельсия).
library(nycflights13)
#glimpse(weather)
w <- filter(weather,origin=='JFK', month == 9)
(5/9)*(mean(w$temp)-32)
```

### Задание 11

```{r}
# Самолеты какой авиакомпании совершили больше всего вылетов в июне?
library(dplyr)
library(nycflights13)
flights.j <- flights %>%
  filter(month == 5) %>%
  group_by(carrier) %>%
  summarise(N = n())
select(arrange(flights.j,desc(N)) %>% top_n(1),carrier)

```

### Задание 12

```{r}
# Самолеты какой авиакомпании задерживались чаще других в 2013 году?
flights.2013 <- flights %>% 
  filter(year == 2013) %>%
  filter(dep_delay>0) %>%
  group_by(carrier) %>% 
  summarise(N = n())
select(arrange(flights.2013,desc(N)) %>% top_n(1),carrier)
```
