## Цель работы

1.  Зекрепить практические навыки использования языка программирования R
    для обработки данных
2.  Закрепить знания основных функций обработки данных экосистемы
    tidyverse языка R
3.  Закрепить навыки исследования метаданных DNS трафика

RStudioCloud \### Подготовка данных

## Задания

    ## [1] 123352

    ## [1] "Отношение участников обмена внутри сети и участников обращений к внешним ресурсам: "

    ## [1] 0.9625458

    ## Selecting by N

    ## # A tibble: 10 × 1
    ##    ip_host        
    ##    <chr>          
    ##  1 10.10.117.210  
    ##  2 192.168.202.93 
    ##  3 192.168.202.103
    ##  4 192.168.202.76 
    ##  5 192.168.202.97 
    ##  6 192.168.202.141
    ##  7 10.10.117.209  
    ##  8 192.168.202.110
    ##  9 192.168.203.63 
    ## 10 192.168.202.106

    ## Selecting by N

    ## # A tibble: 15 × 1
    ##    query          
    ##    <chr>          
    ##  1 dropbox.com    
    ##  2 apple.com      
    ##  3 sorbs.net      
    ##  4 google.com     
    ##  5 hec.net        
    ##  6 microsoft.com  
    ##  7 fireeye.com    
    ##  8 org.localdomain
    ##  9 ahbl.org       
    ## 10 apews.org      
    ## 11 nszones.com    
    ## 12 spamcop.net    
    ## 13 spamhaus.org   
    ## 14 spamrats.com   
    ## 15 tornevall.org

    ##     query                 N          
    ##  Length:397         Min.   :  1.000  
    ##  Class :character   1st Qu.:  1.000  
    ##  Mode  :character   Median :  1.000  
    ##                     Mean   :  3.108  
    ##                     3rd Qu.:  2.000  
    ##                     Max.   :104.000

    ## # A tibble: 428,292 × 3
    ## # Groups:   dns.4$query [5,176]
    ##    ip_host        query                                                  dns.4…¹
    ##    <chr>          <chr>                                                  <chr>  
    ##  1 192.168.202.76 "HPE8AA67"                                             "HPE8A…
    ##  2 192.168.202.76 "HPE8AA67"                                             "HPE8A…
    ##  3 192.168.202.76 "HPE8AA67"                                             "HPE8A…
    ##  4 192.168.202.76 "WPAD"                                                 "WPAD" 
    ##  5 192.168.202.76 "WPAD"                                                 "WPAD" 
    ##  6 192.168.202.76 "WPAD"                                                 "WPAD" 
    ##  7 192.168.202.89 "EWREP1"                                               "EWREP…
    ##  8 192.168.202.89 "EWREP1"                                               "EWREP…
    ##  9 192.168.202.89 "EWREP1"                                               "EWREP…
    ## 10 192.168.202.89 "*\\x00\\x00\\x00\\x00\\x00\\x00\\x00\\x00\\x00\\x00\… "*\\x0…
    ## # … with 428,282 more rows, and abbreviated variable name ¹​`dns.4$query`

    ## [1] 73
