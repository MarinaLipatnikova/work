---
title: "Лабораторная работа №5"
author: |
  Липатникова Марина Сергеевна
date: "08.10.2022, Moscow"
output:
  beamer_presentation: default
  slidy_presentation: default
  ioslides_presentation: default
  powerpoint_presentation: default
subtitle: Дискреционное разграничение прав в Linux. Исследование влияния дополнительных атрибутов
lang: ru-RU
institute: |
  RUDN University, Moscow, Russian Federation
toc: false
slide_level: 2
theme: metropolis
header-includes:
- \metroset{progressbar=frametitle,sectionpage=progressbar,numbering=fraction}
- \makeatletter
- \beamer@ignorenonframefalse
- \makeatother
aspectratio: 43
section-titles: yes
---

## Цель работы

Изучение механизмов изменения идентификаторов, применения
SetUID- и Sticky-битов. Получение практических навыков работы в консоли с дополнительными атрибутами. Рассмотрение работы механизма
смены идентификатора процессов пользователей, а также влияние бита
Sticky на запись и удаление файлов.

## Выполнение лабораторной работы

![Работа с программой simpleid](2.png){width=50%}

## Выполнение лабораторной работы

![Работа с программой simpleid2](3.png){width=50%}

## Выполнение лабораторной работы


![Работа simpleid2(u+s)](4.png){width=40%}

![Работа simpleid2(g+s)](5.png){width=40%}

![Команды от суперпользователя](6.png){width=50%}

## Выполнение лабораторной работы

![Программа readfile](7.png){width=40%}

## Выполнение лабораторной работы

![Чтение readfile.c](8.png)

![Команды от суперпользователя](9.png)

## Выполнение лабораторной работы

![Чтение с помощью программы readfile](10.png){width=40%}

## Выполнение лабораторной работы

![Работа с tmp/file01.txt](11.png){width=50%}

## Выполнение лабораторной работы

![Работа с tmp/file01.txt без t](12.png){width=50%}

![Команды от суперпользователя](13.png){width=50%}

## Результат выполнения работы

Изучила механизмы изменения идентификаторов, применения
SetUID- и Sticky-битов. Получила практические навыки работы в консоли с дополнительными атрибутами. Рассмотрела работу механизма
смены идентификатора процессов пользователей, а также влияние бита
Sticky на запись и удаление файлов.

## Список литературы

1. Теоретические материалы курса.
