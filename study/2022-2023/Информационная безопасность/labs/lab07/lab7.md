---
title: "Лабораторная работа №7"
author: "Липатникова М.С. группа НФИбд-02-19"
subtitle: "Элементы криптографии. Однократное гаммирование"
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

Освоить на практике применение режима однократного гаммирования.

# Выполнение лабораторной работы

Нужно подобрать ключ, чтобы получить сообщение «С Новым Годом,
друзья!». Требуется разработать приложение (@fig:001), позволяющее шифровать и
дешифровать данные в режиме однократного гаммирования. Приложение
должно:
1. Определить вид шифротекста при известном ключе и известном откры-
том тексте.
2. Определить ключ, с помощью которого шифротекст может быть преоб-
разован в некоторый фрагмент текста, представляющий собой один из
возможных вариантов прочтения открытого текста.

Создала 4 функции:
- одна генерирует ключ из ASCII-кодов по количеству букв в сообщении;
- вторая делает шифрование в режиме однократного гаммирования: сначала каждая буква текста и ключа изменяется на число из таблицы символов Unicode, представляющее его позицию, потом это число переводится в 16-ную систему. Далее текст возводится в степень ключа - это зашифрованное сообщение;
- в третьей функции мы можем найти открытый ключ по тексту и зашифрованному тексту;
- в четвертой функции находим открытое собщение из зашифрованного и ключа.

![Программа](1.png){#fig:001 width=100%}


# Вывод

Освоила на практике применение режима однократного гаммирования.

# Список литературы

1. Теоретические материалы курса.
