# Основы обработки данных с помощью R

## Цель

1.  Развить практические навыки использования языка программирования R для обработки данных
2.  Закрепить знания базовых типов данных языка R
3.  Развить пркатические навыки использования функций обработки данных пакета dplyr -- функции select(), filter(), mutate(), arrange(), group_by()

## Исходные данные

RStudioCloud

## Код программы

```{r}
library(dplyr)
starwars
starwars <- starwars
```

### Задания 1-3

```{r}
# Сколько строк в датафрейме:
starwars %>% nrow()
# Сколько столбцов в датафрейме:
starwars %>% ncol()
# Примерный вид датафрейма:
starwars %>% glimpse()
```

### Задание 4

```{r}
# Количество уникальных рас персонажей: в данных
length(unique(starwars$species))
```

### Задание 5

```{r}
# Самый высокий персонаж
starwars$height[is.na(starwars$height)] <- 0
starwars$name[which.max(starwars$height)]

```

### Задание 6

```{r}
# Все персонажи, ниже 170.
starwars$name[which((starwars$height)<170)]
```

### Задание 7

```{r}
# ИМТ всех перпсонажей
starwars %>%
  mutate(name, bmi = mass/((height/100)^2)) %>%
  select(name:mass, bmi)

```

### Задание 8

```{r}
#10  самых вытянутых персонажей
sort(starwars$height/starwars$mass)

#starwars %>% 
#top_n(starwars, 10)
#top_n(10, starwars$height/starwars$mass)

tibble::as_tibble(starwars) %>%
  group_by(name) %>%
  tally(height/mass) %>%
  top_n(10)
```

### Задание 9

```{r warning=FALSE}
#Средний возраст персонажей каждой расы
starwars$birth_year[is.na(starwars$birth_year)] <- na.exclude(starwars$birth_year)

starwars$species[is.na(starwars$species)] <- "Unknown"

for (x in unique(starwars$species)) {
  print(x)
  print(mean(starwars$birth_year[starwars$species == x]))
}
```

### Задание 10

```{r}
#Самый распространенный цвет глаз персонажей вселенной Звездных войн.
a1 <- c(count(starwars,eye_color))
print (a1[["eye_color"]][which.max(unlist(a1["n"]))])
```

### Задание 11

```{r}
#Средняя длина имени в каждой расе 
require(stringi)
starwars$species[is.na(starwars$species)] <- "Unknown"

for (x in unique(starwars$species)) {
  print(paste(x, ":",mean(stri_length(starwars$name)[starwars$species == x])))
}
```
