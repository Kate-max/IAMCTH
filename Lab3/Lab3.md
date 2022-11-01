# Основы обработки данных с помощью R.

## Цель:

1.  Развить практические навыки использования языка программирования R для обработки данных.
2.  Закрепить знания базовых типов данных языка R.
3.  Развить пркатические навыки использования функций обработки данных пакета dplyr -- функции select(), filter(), mutate(), arrange(), group_by().

## Исходные данные:

RStudioCloud

## Код программы:

```{r}
install.packages("dplyr")
```

```{r}
library(dplyr) # for functions
starwars <- starwars
```

```{r} 
# 1. Сколько строк в датафрейме?
starwars %>% nrow()
# 2. Сколько столбцов в датафрейме?
starwars %>% ncol()
# 3. Как просмотреть примерный вид датафрейма?
starwars %>% glimpse()
```

```{r} 
# 4. Сколько уникальных рас персонажей (species) представлено в данных?
length(unique(starwars$species))
```

```{r}
# 5. Найти самого высокого персонажа.
starwars$height[is.na(starwars$height)] <- 0
max(starwars$height)
starwars$name[which.max(starwars$height)]
```
```{r}
# 6. Найти всех персонажей ниже 170
starwars$name[which ((starwars$height)<170)]
```


```{r} 
# 7. Подсчитать ИМТ (индекс массы тела) для всех персонажей.
starwars %>% 
  mutate(name, bmi = mass / ((height / 100)  ^ 2)) %>%
  select(name:mass, bmi)
```

```{r}
# 8. Найти 10 самых “вытянутых” персонажей.
tibble::as_tibble(starwars) %>%
  group_by(name) %>%
  tally(height/mass) %>%
  top_n(10)

```

```{r}
# 9. Найти средний возраст персонажей каждой расы вселенной Звездных войн.
starwars$birth_year[is.na(starwars$birth_year)] <- na.exclude(starwars$birth_year)

starwars$species[is.na(starwars$species)] <- "Unknown"

for (x in unique(starwars$species)) {
  print(x)
  print(mean(starwars$birth_year[starwars$species == x]))
}
```

```{r}
# 10. Найти самый распространенный цвет глаз персонажей вселенной Звездных войн.
a1 <- c(count(starwars,eye_color))
print (a1[["eye_color"]][which.max(unlist(a1["n"]))])
```

```{r}
# 11. Подсчитать среднюю длину имени в каждой расе вселенной Звездных войн.
require(stringi)
starwars$species[is.na(starwars$species)] <- "Unknown"

for (x in unique(starwars$species)) {
  print(paste(x, ":",mean(stri_length(starwars$name)[starwars$species == x])))
}
```

