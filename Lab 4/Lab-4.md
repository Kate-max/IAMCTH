## Цель работы

1.  Зекрепить практические навыки использования языка программирования R
    для обработки данных
2.  Закрепить знания основных функций обработки данных экосистемы
    tidyverse языка R
3.  Развить пркатические навыки использования функций обработки данных
    пакета dplyr – функции select(), filter(), mutate(), arrange(),
    group\_by()

RStudioCloud

### Подготовка данных

    #install.packages('nycflights13')
    #install.packages("dplyr")

## Задания

    library(nycflights13)
    library(dplyr)
    #1. Сколько встроенных в пакет nycflights13 датафреймов?
    data(package = "nycflights13")
    #2. Сколько строк в каждом датафрейме?
    #3. Сколько столбцов в каждом датафрейме?
    print ("flights: ")

    ## [1] "flights: "

    dim(flights)

    ## [1] 336776     19

    print ("weather: ")

    ## [1] "weather: "

    dim(weather)

    ## [1] 26115    15

    print ("planes: ")

    ## [1] "planes: "

    dim(planes)

    ## [1] 3322    9

    print ("airports: ")

    ## [1] "airports: "

    dim(airports)

    ## [1] 1458    8

    print ("airlines: ")

    ## [1] "airlines: "

    dim(airlines)

    ## [1] 16  2

    #4. Как просмотреть примерный вид датафрейма?
    library(nycflights13)
    glimpse(flights)

    ## Rows: 336,776
    ## Columns: 19
    ## $ year           <int> 2013, 2013, 2013, 2013, 2013, 2013, 2013, 2013, 2013, 2…
    ## $ month          <int> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1…
    ## $ day            <int> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1…
    ## $ dep_time       <int> 517, 533, 542, 544, 554, 554, 555, 557, 557, 558, 558, …
    ## $ sched_dep_time <int> 515, 529, 540, 545, 600, 558, 600, 600, 600, 600, 600, …
    ## $ dep_delay      <dbl> 2, 4, 2, -1, -6, -4, -5, -3, -3, -2, -2, -2, -2, -2, -1…
    ## $ arr_time       <int> 830, 850, 923, 1004, 812, 740, 913, 709, 838, 753, 849,…
    ## $ sched_arr_time <int> 819, 830, 850, 1022, 837, 728, 854, 723, 846, 745, 851,…
    ## $ arr_delay      <dbl> 11, 20, 33, -18, -25, 12, 19, -14, -8, 8, -2, -3, 7, -1…
    ## $ carrier        <chr> "UA", "UA", "AA", "B6", "DL", "UA", "B6", "EV", "B6", "…
    ## $ flight         <int> 1545, 1714, 1141, 725, 461, 1696, 507, 5708, 79, 301, 4…
    ## $ tailnum        <chr> "N14228", "N24211", "N619AA", "N804JB", "N668DN", "N394…
    ## $ origin         <chr> "EWR", "LGA", "JFK", "JFK", "LGA", "EWR", "EWR", "LGA",…
    ## $ dest           <chr> "IAH", "IAH", "MIA", "BQN", "ATL", "ORD", "FLL", "IAD",…
    ## $ air_time       <dbl> 227, 227, 160, 183, 116, 150, 158, 53, 140, 138, 149, 1…
    ## $ distance       <dbl> 1400, 1416, 1089, 1576, 762, 719, 1065, 229, 944, 733, …
    ## $ hour           <dbl> 5, 5, 5, 5, 6, 5, 6, 6, 6, 6, 6, 6, 6, 6, 6, 5, 6, 6, 6…
    ## $ minute         <dbl> 15, 29, 40, 45, 0, 58, 0, 0, 0, 0, 0, 0, 0, 0, 0, 59, 0…
    ## $ time_hour      <dttm> 2013-01-01 05:00:00, 2013-01-01 05:00:00, 2013-01-01 0…

    #5. Сколько компаний-перевозчиков (carrier) учитывают эти наборы данных (представлено в наборах данных)?
    library(dplyr)
    library(nycflights13)
    flights.1 <- flights %>% 
      group_by(carrier) %>% 
      summarise(N = n())
    count(select(flights.1,carrier))

    ## # A tibble: 1 × 1
    ##       n
    ##   <int>
    ## 1    16

    #6. Сколько рейсов принял аэропорт John F Kennedy Intl в мае?
    count(filter(flights,origin=='JFK', month == 5))

    ## # A tibble: 1 × 1
    ##       n
    ##   <int>
    ## 1  9397

    #7. Какой самый северный аэропорт?
    airports$name[which.max(airports$lat)]

    ## [1] "Dillant Hopkins Airport"

    #8. Какой аэропорт самый высокогорный (находится выше всех над уровнем моря)?
    airports$name[which.max(airports$alt)]

    ## [1] "Telluride"

    #9. Какие бортовые номера у самых старых самолетов?
    library(nycflights13)
    #glimpse(planes)
    select(planes,tailnum, -(year)) %>% top_n(10)

    ## # A tibble: 10 × 1
    ##    tailnum
    ##    <chr>  
    ##  1 N994DL 
    ##  2 N995AT 
    ##  3 N995DL 
    ##  4 N996AT 
    ##  5 N996DL 
    ##  6 N997AT 
    ##  7 N997DL 
    ##  8 N998AT 
    ##  9 N998DL 
    ## 10 N999DN

    #10. Какая средняя температура воздуха была в сентябре в аэропорту John F Kennedy Intl (в градусах Цельсия).
    library(nycflights13)
    #glimpse(weather)
    w <- filter(weather,origin=='JFK', month == 9)
    (5/9)*(mean(w$temp)-32)

    ## [1] 19.38764

    #11. Самолеты какой авиакомпании совершили больше всего вылетов в июне?
    library(dplyr)
    library(nycflights13)
    flights.2 <- flights %>% 
      filter(month == 5) %>%
      group_by(carrier) %>% 
      summarise(N = n())
    select(arrange(flights.2,desc(N)) %>% top_n(1),carrier)

    ## # A tibble: 1 × 1
    ##   carrier
    ##   <chr>  
    ## 1 UA

    #12. Самолеты какой авиакомпании задерживались чаще других в 2013 году?
    flights.3 <- flights %>% 
      filter(year == 2013) %>%
      filter(dep_delay>0) %>%
      group_by(carrier) %>% 
      summarise(N = n())
    select(arrange(flights.3,desc(N)) %>% top_n(1),carrier)

    ## # A tibble: 1 × 1
    ##   carrier
    ##   <chr>  
    ## 1 UA
