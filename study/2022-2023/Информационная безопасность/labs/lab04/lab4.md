---
title: "Лабораторная работа №4"
author: "Липатникова М.С. группа НФИбд-02-19"
subtitle: "Дискреционное разграничение прав в Linux. Расширенные атрибуты"
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

Получение практических навыков работы в консоли с расширенными атрибутами файлов.

# Выполнение лабораторной работы

От имени пользователя guest определила расширенные атрибуты файла /home/guest/dir1/file командой
lsattr /home/guest/dir1/file1.
Установила командой chmod 600 file на файл file права, разрешающие чтение и запись для владельца файла.
Попробовала установить на файл /home/guest/dir1/file1 расширенный атрибут a от имени пользователя guest:
chattr +a /home/guest/dir1/file. В ответ получила отказ от выполнения операции (@fig:001).

![Проверка расширенных атрибутов](1.png){#fig:001 width=100%}

Зашла на консоль с правами администратора, попробовала установить
расширенный атрибут a на файл /home/guest/dir1/file от имени суперпользователя:
chattr +a /home/guest/dir1/file (@fig:002).

![Действия от суперпользователя](2.png){#fig:002 width=100%}

От пользователя guest проверила правильность установления атрибута:
lsattr file. Выполнила дозапись в файл file слова «test» командой
echo "test" file. После этого выполнила чтение файла file командой
cat file. Убедилась, что слово test было успешно записано в file. Попробовала
удалить файл file либо стереть имеющуюся в нём информацию командой
echo "abcd" > file. Попробовала переименовать файл. Попробовала с помощью команды
chmod 000 file установить на файл file права, например, запрещающие чтение и запись
для владельца файла. Мне удалось успешно выполнить лишь дозапись и чтение файла (@fig:003).

![Действия с атрибутом «a»](3.png){#fig:003 width=100%}

Сняла расширенный атрибут a с файла /home/guest/dirl/file от имени суперпользователя командой
chattr -a /home/guest/dir1/file (@fig:002).

Повторила операции, которые ранее не удавалось выполнить (@fig:004).

![Действия без атрибутов](4.png){#fig:004 width=100%}

Повторив действия по шагам, заменила атрибут «a» атрибутом «i» (@fig:005).

![Действия с атрибутом «i»](5.png){#fig:005 width=100%}

 Наблюдения занесла в таблицу (@fig:006).

![Таблица разрешенных действий](6.png){#fig:006 width=100%}

# Вывод

Получила практические навыки работы в консоли с расширенными атрибутами файлов.

# Список литературы

1. Теоретические материалы курса.
