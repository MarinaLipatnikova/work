---
title: "Лабораторная работа №3"
author: "Липатникова М.С. группа НФИбд-02-19"
subtitle: "Дискреционное разграничение прав в Linux. Два пользователя"
output:
  word_document: default
  pdf_document: default
toc-title: Содержание
toc: yes
toc_depth: 2
lof: yes
fontsize: 12pt
linestretch: 1.5
papersize: a4paper
documentclass: scrreprt
polyglossia-lang: russian
polyglossia-otherlangs: english
mainfont: PT Serif
romanfont: PT Serif
sansfont: PT Sans
monofont: PT Mono
mainfontoptions: Ligatures=TeX
romanfontoptions: Ligatures=TeX
sansfontoptions: Ligatures=TeX,Scale=MatchLowercase
monofontoptions: Scale=MatchLowercase
indent: yes
pdf-engine: lualatex
header-includes:
- \linepenalty=10
- \interlinepenalty=0
- \hyphenpenalty=50
- \exhyphenpenalty=50
- \binoppenalty=700
- \relpenalty=500
- \clubpenalty=150
- \widowpenalty=150
- \displaywidowpenalty=50
- \brokenpenalty=100
- \predisplaypenalty=10000
- \postdisplaypenalty=0
- \floatingpenalty = 20000
- \raggedbottom
- \usepackage{float}
- \floatplacement{figure}{H}
---

# Цель работы

Получение практических навыков работы в консоли с атрибутами файлов для групп пользователей.

# Выполнение лабораторной работы

В установленной операционной системе создала в предыдущей л/р учётную запись  пользователя guest (используя учётную запись администратора): useradd guest. Задала пароль для пользователя guest (использую учётнуя запись администратора): passwd guest. Аналогично создала второго пользователя. Добавила пользователя guest2 в группу guest: gpasswd -a guest2 guest (@fig:001).

![Создание второго пользователя](1.png){#fig:001 width=100%}

Осуществила вход в систему от двух пользователей на двух разных консолях: guest на первой консоли и guest2 на второй консоли. Для обоих пользователей командой pwd определила директорию, в которой нахожусь: /home/mslipatnikova. Совпадает с приглашениями командной строки. Уточнила имя моих пользователей (guest, guest2), их группу и кто входит в неё, к каким группам принадлежит пользователь (guest: guest, guest2: guest2 guest). Определила командами groups guest и groups guest2, в какие группы входят пользователи guest и guest2. Совпадает вывод команды groups с выводом команд id -Gn и id -G (@fig:002)(@fig:003).

![Определение пользователя](2.png){#fig:002 width=100%}

![Определение второго пользователя](3.png){#fig:003 width=100%}

Сравнив полученную информацию с содержимым файла /etc/group, просмотрев файл командой cat /etc/group, получила совпадение. От имени пользователя guest2 выполнила регистрацию пользователя guest2 в группе guest командой newgrp guest(@fig:004).

![Файл /etc/group и регистрация в группе](4.png){#fig:004 width=100%}

От имени пользователя guest изменила права директории /home/guest, разрешив все действия для пользователей группы: chmod g+rwx /home/guest (@fig:005).

![Права доступа в домашней директории guest](5.png){#fig:005 width=100%}

От имени пользователя guest сняла с директории /home/guest/dir1 все атрибуты командой chmod 000 dirl и проверила правильность снятия атрибутов: ls -l (@fig:006).

![Права на dir1](6.png){#fig:006 width=100%}


Меняя атрибуты у директории dir1 и файла file1 от имени пользователя guest и делая проверку от пользователя guest2, заполнила таблицу,определив опытным путём, какие операции разрешены, а какие нет. Если операция разрешена, занесла в таблицу знак «+», если не разрешена, знак «-» (@fig:009)(@fig:0010). Команды для проверки (@fig:007)(@fig:008).

![Команды для проверки guest2](7.png){#fig:007 width=100%}

![Команды для проверки guest](8.png){#fig:008 width=100%}

![Установленные права и разрешённые действия для групп](10.png){#fig:009 width=100%}

![Установленные права и разрешённые действия для групп](11.png){#fig:0010 width=100%}

Сравнила таблицу из лабораторной работы No 2 и данную таблицу, главное отличие - невозможность у группы менять артибуты файла, созданного первом пользователем.

На основании заполненной таблицы определила те или иные минимально необходимые права для выполнения пользователем guest2 операций внутри директории dir1 и заполнила таблицу(@fig:0011).

![Минимальные права для совершения операций от имени пользователей входящих в группу](12.png){#fig:0011 width=100%}

# Вывод

Получила практические навыки работы в консоли с атрибутами файлов для групп пользователей.

# Список литературы

1. Теоретические материалы курса.
