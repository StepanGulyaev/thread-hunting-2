# Лабораторная работа №3
Гуляев Степан БИСО-01-20

## Цель работы

1.  Зекрепить практические навыки использования языка программирования R
    для обработки данных
2.  Закрепить знания основных функций обработки данных экосистемы
    tidyverse языка R
3.  Развить пркатические навыки использования функций обработки данных
    пакета dplyr – функции select(),filter(),mutate(), arrange(),
    group_by()

## Исходные данные

1.  ОС Windows 10
2.  Интерпретатор R v-4.3.1
3.  RStudio Desktop
4.  dplyr
5.  nycflights13

## Задание

Проанализировать встроенные в пакет nycflights13 наборы данных с помощью
языка R и ответить на вопросы

## Ход работы

### Установка dplyr

Выполним install.packages(“dplyr”), а затем добавим библиотеку:

``` r
library(dplyr)
```

    Warning: пакет 'dplyr' был собран под R версии 4.3.1


    Присоединяю пакет: 'dplyr'

    Следующие объекты скрыты от 'package:stats':

        filter, lag

    Следующие объекты скрыты от 'package:base':

        intersect, setdiff, setequal, union

### Установка nycflights13

Выполним install.packages(“nycflights13”), а затем добавим библиотеку:

``` r
library(nycflights13)
```

    Warning: пакет 'nycflights13' был собран под R версии 4.3.1

### Выполнение заданий

#### 1. Сколько встроенных в пакет nycflights13 датафреймов?

``` r
help(package="nycflights13")
```

Пять: airlines, airports, flights, planes, weather.

#### 2. Сколько строк в каждом датафрейме?

``` r
airlines %>% nrow()
```

    [1] 16

``` r
airports %>% nrow()
```

    [1] 1458

``` r
flights %>% nrow()
```

    [1] 336776

``` r
planes %>% nrow()
```

    [1] 3322

``` r
weather %>% nrow()
```

    [1] 26115

#### 3. Сколько столбцов в каждом датафрейме?

``` r
airlines %>% ncol()
```

    [1] 2

``` r
airports %>% ncol()
```

    [1] 8

``` r
flights %>% ncol()
```

    [1] 19

``` r
planes %>% ncol()
```

    [1] 9

``` r
weather %>% ncol()
```

    [1] 15

#### 4. Как просмотреть примерный вид датафрейма?

``` r
weather %>% glimpse()
```

    Rows: 26,115
    Columns: 15
    $ origin     <chr> "EWR", "EWR", "EWR", "EWR", "EWR", "EWR", "EWR", "EWR", "EW…
    $ year       <int> 2013, 2013, 2013, 2013, 2013, 2013, 2013, 2013, 2013, 2013,…
    $ month      <int> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1,…
    $ day        <int> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1,…
    $ hour       <int> 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 13, 14, 15, 16, 17, 18, …
    $ temp       <dbl> 39.02, 39.02, 39.02, 39.92, 39.02, 37.94, 39.02, 39.92, 39.…
    $ dewp       <dbl> 26.06, 26.96, 28.04, 28.04, 28.04, 28.04, 28.04, 28.04, 28.…
    $ humid      <dbl> 59.37, 61.63, 64.43, 62.21, 64.43, 67.21, 64.43, 62.21, 62.…
    $ wind_dir   <dbl> 270, 250, 240, 250, 260, 240, 240, 250, 260, 260, 260, 330,…
    $ wind_speed <dbl> 10.35702, 8.05546, 11.50780, 12.65858, 12.65858, 11.50780, …
    $ wind_gust  <dbl> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, 20.…
    $ precip     <dbl> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,…
    $ pressure   <dbl> 1012.0, 1012.3, 1012.5, 1012.2, 1011.9, 1012.4, 1012.2, 101…
    $ visib      <dbl> 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10,…
    $ time_hour  <dttm> 2013-01-01 01:00:00, 2013-01-01 02:00:00, 2013-01-01 03:00…

#### 5. Сколько компаний-перевозчиков (carrier) учитывают эти наборы данных (представлено в наборах данных)?

``` r
airlines %>% distinct(carrier) %>% n_distinct()
```

    [1] 16

#### 6. Сколько рейсов принял аэропорт John F Kennedy Intl в мае?

``` r
flights %>% filter(month == 5 & dest == as.character(airports %>% filter(name == "John F Kennedy Intl") %>% select(faa)))  %>% nrow()
```

    [1] 0

#### 7. Какой самый северный аэропорт?

``` r
airports %>% filter(lat == max(lat))
```

    # A tibble: 1 × 8
      faa   name                      lat   lon   alt    tz dst   tzone
      <chr> <chr>                   <dbl> <dbl> <dbl> <dbl> <chr> <chr>
    1 EEN   Dillant Hopkins Airport  72.3  42.9   149    -5 A     <NA> 

#### 8. Какой аэропорт самый высокогорный (находится выше всех над уровнем моря)?

``` r
airports %>% filter(alt == max(alt))
```

    # A tibble: 1 × 8
      faa   name        lat   lon   alt    tz dst   tzone         
      <chr> <chr>     <dbl> <dbl> <dbl> <dbl> <chr> <chr>         
    1 TEX   Telluride  38.0 -108.  9078    -7 A     America/Denver

#### 9. Какие бортовые номера у самых старых самолетов?

``` r
planes %>% arrange(year) %>% head(5) %>% select(tailnum)
```

    # A tibble: 5 × 1
      tailnum
      <chr>  
    1 N381AA 
    2 N201AA 
    3 N567AA 
    4 N378AA 
    5 N575AA 

#### 10. Какая средняя температура воздуха была в сентябре в аэропорту John F Kennedy Intl (в градусах Цельсия).

``` r
faa_kennedy <- airports %>% filter(name == "John F Kennedy Intl") %>% select(faa)

weather %>% filter(origin == as.character(faa_kennedy) & month == 9) %>% summarize(avg_temp_celsius = mean((temp - 32)*5/9 , na.rm = TRUE))
```

    # A tibble: 1 × 1
      avg_temp_celsius
                 <dbl>
    1             19.4

#### 10. Какая средняя температура воздуха была в сентябре в аэропорту John F Kennedy Intl (в градусах Цельсия).

``` r
faa_kennedy <- airports %>% filter(name == "John F Kennedy Intl") %>% select(faa)

weather %>% filter(origin == as.character(faa_kennedy) & month == 9) %>% summarize(avg_temp_celsius = mean((temp - 32)*5/9 , na.rm = TRUE))
```

    # A tibble: 1 × 1
      avg_temp_celsius
                 <dbl>
    1             19.4

#### 11. Самолеты какой авиакомпании совершили больше всего вылетов в июне?

``` r
flights %>% filter(month == 6) %>% group_by(carrier) %>% summarize(total_flights = n()) %>% arrange(desc(total_flights)) %>% head(1)
```

    # A tibble: 1 × 2
      carrier total_flights
      <chr>           <int>
    1 UA               4975

#### 12. Самолеты какой авиакомпании задерживались чаще других в 2013 году?

``` r
flights %>% filter(year == 2013) %>% group_by(carrier) %>% summarize(total_delay = sum(arr_delay > 0,na.rm = TRUE)) %>% arrange(desc(total_delay)) %>% head(1)
```

    # A tibble: 1 × 2
      carrier total_delay
      <chr>         <int>
    1 EV            24484

## Оценка результата

В результате лабораторной работы мы выполнили задания с использованием
dplyr на данных из пакета nycflights13

## Вывод

Мы научились работать с пакетом dplyr для языка R с новыми наборами
данных
