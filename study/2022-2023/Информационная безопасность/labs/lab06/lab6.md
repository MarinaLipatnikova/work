---
title: "Лабораторная работа №6"
author: "Липатникова М.С. группа НФИбд-02-19"
subtitle: "Мандатное разграничение прав в Linux"
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

Развить навыки администрирования ОС Linux. Получить первое практическое знакомство с технологией SELinux. Проверить работу SELinx на практике совместно с веб-сервером
Apache.

# Выполнение лабораторной работы

Вошла в систему с полученными учётными данными и убедилась, что
SELinux работает в режиме enforcing политики targeted с помощью ко-
манд: getenforce и sestatus. Обратилась с помощью браузера к веб-серверу, запущенному на моем компьютере, и убедилась, что последний работает:
service httpd status (@fig:001).

![Проверка SELinux](1.png){#fig:001 width=100%}

Нашла веб-сервер Apache в списке процессов, его контекст безопасности: httpd_t (ps -eZ | grep httpd)(@fig:002).

![Список процессов: веб-сервер Apache](2.png){#fig:002 width=100%}

Посмотрела текущее состояние переключателей SELinux для Apache с помощью команды: sestatus -b | grep httpd. Обратила внимание, что многие из них находятся в положении «off»(@fig:003).

![Переключатели для Apache](4.png){#fig:003 width=100%}

Посмотрела статистику по политике с помощью команды seinfo, также
определила множество пользователей (8), ролей (14), типов (5002) (@fig:004).

![Статистика по политике](5.png){#fig:004 width=100%}

Определила тип файлов и поддиректорий, находящихся в директории /var/www, с помощью команды: ls -lZ /var/www. Определила тип файлов, находящихся в директории /var/www/html: ls -lZ /var/www/html. Определила круг пользователей, которым разрешено создание файлов в директории /var/www/html (root). Создала от имени суперпользователя html-файл - /var/www/html/test.html, чтобы на странице выводилось слово test. Проверила контекст созданного мной файла (httpd_sys_content_t). Обратилась к файлу через веб-сервер, введя в браузере адрес
http://127.0.0.1/test.html. Убедилась, что файл был успешно отображён (@fig:005).

![Работа в директории /var/www/html](6.png){#fig:005 width=100%}

Изучила справку man httpd_selinux и выяснила, какие контексты файлов определены для httpd. Совпадают с типом файла test.html. Тип httpd_sys_content_t позволяет процессу httpd получить доступ к файлу. Благодаря наличию последнего типа мы получили доступ к файлу при обращении к нему через браузер.

Изменила контекст файла /var/www/html/test.html с
httpd_sys_content_t на (к которому процесс httpd не должен иметь доступа) samba_share_t:

chcon -t samba_share_t /var/www/html/test.html

ls -Z /var/www/html/test.html

Попробовала ещё раз получить доступ к файлу через веб-сервер, введя в
браузере адрес http://127.0.0.1/test.html. Получила сообщение об ошибке:
Forbidden. You don't have permission to access /test.html on this server (@fig:006).

![Изменение контекста](7.png){#fig:006 width=100%}

Файл не был отображён, хотя права доступа позволяют читать этот файл любому пользователю: ls -l /var/www/html/test.html. Это произошло, т.к. мы изменили контекст к которому процесс httpd не должен иметь доступа. Просмотрела log-файлы веб-сервера Apache. Также просмотрела системный лог-файл:
tail /var/log/messages (@fig:007).

![Файл ошибок](8.png){#fig:007 width=100%}

Попробовала запустить веб-сервер Apache на прослушивание ТСР-порта
81 (а не 80, как рекомендует IANA и прописано в /etc/services). Для
этого в файле /etc/httpd/httpd.conf нашла строчку Listen 80 и
заменила её на Listen 81 (@fig:008). Выполнила перезапуск веб-сервера Apache. Сбоя не произошло. Проанализировала лог-файлы: tail -nl /var/log/messages (@fig:009).

![Замена 80-81](9.png){#fig:008 width=100%}

![Перезапуск сервера](10.png){#fig:009 width=100%}

Выполнила команду: semanage port -a -t http_port_t -р tcp 81 (уже существует). После этого проверьте список портов командой: semanage port -l | grep http_port_t
Порт 81 есть в списке. Попробовала запустить веб-сервер Apache ещё раз. Сбоя также нет (@fig:0010).

![Перезапуск сервера](11.png){#fig:0010 width=100%}

Вернула контекст httpd_sys_cоntent__t к файлу /var/www/html/ test.html:
chcon -t httpd_sys_content_t /var/www/html/test.html. После этого попробовала получить доступ к файлу через веб-сервер, введя в браузере адрес http://127.0.0.1:81/test.html. Можно увидеть содержимое файла — слово «test» (@fig:0011).

![Перезапуск сервера - работает](12.png){#fig:0011 width=100%}

Исправила обратно конфигурационный файл apache, вернув Listen 80(@fig:0012).

![Замена 81-80](13.png){#fig:0012 width=100%}

Удалить привязку http_port_t к 81 порту (semanage port -d -t http_port_t -p tcp 81) не получилось, не позволяется.
Удалила файл /var/www/html/test.html: rm /var/www/html/test.html(@fig:0013).

![Удаление](14.png){#fig:0013 width=100%}

# Вывод

Развили навыки администрирования ОС Linux. Получили первое практическое знакомство с технологией SELinux. Проверили работу SELinx на практике совместно с веб-сервером
Apache.

# Список литературы

1. Теоретические материалы курса.
