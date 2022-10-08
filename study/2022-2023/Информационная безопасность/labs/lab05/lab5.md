---
title: "Лабораторная работа №5"
author: "Липатникова М.С. группа НФИбд-02-19"
subtitle: "Дискреционное разграничение прав в Linux. Исследование влияния дополнительных атрибутов"
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

Изучение механизмов изменения идентификаторов, применения
SetUID- и Sticky-битов. Получение практических навыков работы в консоли с дополнительными атрибутами. Рассмотрение работы механизма
смены идентификатора процессов пользователей, а также влияние бита
Sticky на запись и удаление файлов.

# Выполнение лабораторной работы

Удостоверилась, что установлен gcc (@fig:001). Вошла в систему от имени пользователя guest. Создала программу simpleid.c:

```C
#include <sys/types.h>
#include <unistd.h>
#include <stdio.h>
int
main ()

{

uid_t uid = geteuid ();

gid_t gid = getegid ();

printf ("uid=%d, gid=%d\n", uid, gid);

return 0;

}
```

Скомплилировала программу и убедилась, что файл программы создан:
gcc simpleid.c -o simpleid. Выполнила программу simpleid:
./simpleid. Выполнила системную программу id: id. Полученный результат с данными предыдущего пункта задания совпадает (@fig:002).

![Проверка gcc](1.png){#fig:001 width=100%}

![Работа с программой simpleid](2.png){#fig:002 width=100%}

Усложнила программу, добавив вывод действительных идентификаторов:

```C
#include <sys/types.h>
#include <unistd.h>
#include <stdio.h>
int
main ()

{

uid_t real_uid = getuid ();

uid_t e_uid = geteuid ();

gid_t real_gid = getgid ();

gid_t e_gid = getegid () ;

printf ("e_uid=%d, e_gid=%d\n", e_uid, e_gid);

printf ("real_uid=%d, real_gid=%d\n", real_uid,

real_gid);

return 0;

}
```

Получившуюся программу назвала simpleid2.c. Скомпилировала и запустила simpleid2.c (@fig:003):

gcc simpleid2.c -o simpleid2

./simpleid2

![Работа с программой simpleid2](3.png){#fig:003 width=100%}

От имени суперпользователя выполнила команды (@fig:006):

chown root:guest /home/guest/simpleid2

chmod u+s /home/guest/simpleid2

Выполнила проверку правильности установки новых атрибутов и смены
владельца файла simpleid2: ls -l simpleid2. Запустила simpleid2 и id:

./simpleid2

id

Замечаем, что все совпадает, кроме uid = 0 (@fig:004).

Проделала тоже самое относительно SetGID-бита (@fig:005).

![Работа simpleid2(u+s)](4.png){#fig:004 width=100%}

![Работа simpleid2(g+s)](5.png){#fig:005 width=100%}

![Команды от суперпользователя](6.png){#fig:006 width=100%}

Создала программу readfile.c:

```C
#include <fcntl.h>
#include <stdio.h>
#include <sys/stat.h>
#include <sys/types.h>
#include <unistd.h>

int
main (int argc, char* argv[])

  {

  unsigned char buffer[16];

  size_t bytes_read;

  int i;

  int fd = open (argv[1], O_RDONLY);

  do

  {

    bytes_read = read (fd, buffer, sizeof (buffer));

    for (i =0; i < bytes_read; ++i) printf("%c", buffer[i]);

  }

  while (bytes_read == sizeof (buffer));

  close (fd);

  return 0;

  }
```

Откомпилировала её: gcc readfile.c -o readfile (@fig:007). Сменила владельца у файла readfile.c и изменила права так, чтобы только суперпользователь (root) мог прочитать его, a guest не мог (@fig:009). Проверила, что пользователь guest не может прочитать файл readfile.c (@fig:008). Сменила у программы readfile владельца и установила SetU’D-бит (@fig:009). Проверила, может ли программа readfile прочитать файл readfile.c (может) (@fig:0010). Проверила, может ли программа readfile прочитать файл /etc/shadow (может) (@fig:0010).

![Программа readfile](7.png){#fig:007 width=100%}

![Чтение readfile.c](8.png){#fig:008 width=100%}

![Команды от суперпользователя](9.png){#fig:009 width=100%}

![Чтение с помощью программы readfile](10.png){#fig:0010 width=100%}

Выяснила, установлен ли атрибут Sticky на директории /tmp, для чего
выполнила команду: ls -l / | grep tmp. От имени пользователя guest создала файл file01.txt в директории /tmp со словом test:
echo "test" > /tmp/file01.txt. Просмотрела атрибуты у только что созданного файла и разрешила чтение и запись для категории пользователей «все остальные»:

ls -l /tmp/file01.txt

chmod o+rw /tmp/file01.txt

ls -l /tmp/file01.txt

От пользователя guest2 (не являющегося владельцем) попробовала прочитать файл /tmp/file01.txt: cat /tmp/file01.txt. От пользователя guest2 попробовала дозаписать в файл /tmp/file01.txt слово test2 командой: echo "test2" >> /tmp/file01.txt. Удалось выполнить операцию. Проверила содержимое файла командой: cat /tmp/file01.txt. От пользователя guest2 попробовала записать в файл /tmp/file01.txt слово test3, стерев при этом всю имеющуюся в файле информацию командой: echo "test3" > /tmp/file01.txt.
Удалось выполнить операцию. Проверила содержимое файла командой: cat /tmp/file01.txt. От пользователя guest2 попробовала удалить файл /tmp/file01.txt командой: rm /tmp/fileOl.txt. Не удалось удалить файл (@fig:0011).

![Работа с tmp/file01.txt](11.png){#fig:0011 width=100%}

От суперпользователя выполнила команду, снимающую атрибут t (Sticky-бит) с
директории /tmp: chmod -t /tmp (@fig:0013). От пользователя guest2 проверила, что атрибута t у директории /tmp нет: ls -l / | grep tmp. Повторила предыдущие шаги. Удалось в этот раз удалить файл от имени пользователя, не являющегося его владельцем (@fig:0012). От суперпользователя выполнила команду, вернувший атрибут t (Sticky-бит) в директории /tmp: chmod +t /tmp (@fig:0013).

![Работа с tmp/file01.txt без t](12.png){#fig:0012 width=100%}

![Команды от суперпользователя](13.png){#fig:0013 width=100%}

# Вывод

Изучила механизмы изменения идентификаторов, применения
SetUID- и Sticky-битов. Получила практические навыки работы в консоли с дополнительными атрибутами. Рассмотрела работу механизма
смены идентификатора процессов пользователей, а также влияние бита
Sticky на запись и удаление файлов.

# Список литературы

1. Теоретические материалы курса.
