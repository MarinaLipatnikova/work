---
title: "Лабораторная работа №1"
author: "Липатникова М.С. группа НФИбд-02-19"
subtitle: "Установка и конфигурация операционной системы на виртуальную машину"
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

Целью данной работы является приобретение практических навыков установки операционной системы на виртуальную машину, настройки минимально необходимых для дальнейшей работы сервисов.

# Выполнение лабораторной работы

Создала новую виртуальную машину(Машина->Создать). Указала имя виртуальной машины (логин в дисплейном классе), тип операционной системы — Linux, RedHat (@fig:001).

![Новая машина](1.png){#fig:001 width=100%}

Указала размер основной памяти виртуальной машины (@fig:002) — 2048 МБ.

![Размер памяти](2.png){#fig:002 width=100%}

Задала конфигурацию жёсткого диска — загрузочный, VDI (VirtualBox Disk Image), динамический виртуальный диск (@fig:003).

![Конфигурация жёсткого диска](3.png){#fig:003 width=100%}

Задала размер диска — 40 ГБ (@fig:004).

![Размер диска](4.png){#fig:004 width=100%}

Добавила новый привод оптических дисков и выбрала образ операционной системы (Настройки->Носители)(@fig:005).

![Образ ОС](5.png){#fig:005 width=100%}

Запустила виртуальную машину, выбрала English в качестве языка интерфейса и перешла к настройкам установки операционной системы. Поменяла раскладку клавиатуры
(добавила русский язык, задала комбинацию клавиш для переключения между раскладками клавиатуры) (@fig:006).

![Общие настройки](6.png){#fig:006 width=100%}

В разделе выбора программ указала в качестве базового окружения Server with GUI, а в качестве дополнения — Development Tools (@fig:007).

![Раздел выбора программ](7.png){#fig:007 width=100%}

Отключила KDUMP (@fig:008).

![KDUMP](8.png){#fig:008 width=100%}

Место установки ОС оставила без изменения. Включила сетевое соединение и в качестве имени узла указала mslipatnikova.localdomain (@fig:009).

![Сетевое соединение](9.png){#fig:009 width=100%}

Установила пароль для root и пользователя с правами администратора (@fig:0010).

![Пользователь и пароль](10.png){#fig:0010 width=100%}

В меню Устройства виртуальной машины подключила образ диска дополнений гостевой ОС (@fig:0011).

![Раздел выбора программ](11.png){#fig:0011 width=100%}

После загрузки дополнений нажала Return или Enter и перезагрузила виртуальную машину.

# Домашнее задание

Получила следующую информацию с помощью команды dmesg | grep -i "то, что ищем"

1. Версия ядра Linux (Linux version) (@fig:0012): Linux version 5.14.0-70.13.1.el9_0.x86_64 (gcc (GCC) 11.2.120220127 (Red Hat 11.2.1-9), GNU ld version 2.35.2-17.el9)

![Версия ядра Linux](12.png){#fig:0012 width=100%}

2. Частота процессора (Detected Mhz processor) 3382.402 МГц(@fig:0013).

![Частота процессора](13.png){#fig:0013 width=100%}

3. Модель процессора (CPU0) (@fig:0014): 11th Gen Intel(R) Core(TM) i7-11370H @3.30GHz (family: 0x6, model: 0x8c, stepping: 0x1).

![Модель процессора](14.png){#fig:0014 width=100%}

4. Объем доступной оперативной памяти (Memory available) (@fig:0015): 260860K/2096696K.

![Объем доступной оперативной памяти](15.png){#fig:0015 width=100%}

5. Тип обнаруженного гипервизора (Hypervisor detected) (@fig:0016): KVM.

![Тип обнаруженного гипервизора](16.png){#fig:0016 width=100%}

6. Тип файловой системы корневого раздела (@fig:0017): XFS.

![Тип файловой системы корневого раздела](17.png){#fig:0017 width=100%}

7. Последовательность монтирования файловых систем (@fig:0018):

- Set up automount Arbitrary Executable File Formats File System Automount Point

- Mounting Huge Pages File System

- Mounting POSIX Message Queue File System

- Mounting Kernel Debug File System

- Mounting Kernel Trace File System

- Starting Remount Root and Kernel File Systems

![Последовательность монтирования файловых систем](18.png){#fig:0018 width=100%}

# Контрольные вопросы

1. Какую информацию содержит учётная запись пользователя?

Учётные записи представляют собой средства идентификации пользователей и проверки их подлинности. Учётные записи пользователей имеют несколько компонентов. Первый компонент — имя пользователя. Второй — пароль, а затем идёт информация об управлении доступом.

2. Укажите команды терминала и приведите примеры:

– для получения справки по команде: man

– для перемещения по файловой системе: cd

– для просмотра содержимого каталога: ls

– для определения объёма каталога: df

– для создания / удаления каталогов / файлов: mkdir/touch(echo), rmdir/rm

– для задания определённых прав на файл / каталог: chmod

– для просмотра истории команд: history

3. Что такое файловая система? Приведите примеры с краткой характеристикой.

Файловая система – это инструмент, позволяющий операционной системе и программам обращаться к нужным файлам и работать с ними.
- FAT32. Благодаря отсутствию шифрования, современных систем защиты информации и журнала данных, накопители с файловой системой FAT32 могут работать быстрее, но только с единичными файлами. Работа с массивом небольших файлов может затянуться надолго. Причиной является иерархическая структура, которая подразумевает многоуровневый доступ к файлам, в отличие от бинарного дерева, где доступ к файлам открывается напрямую, независимо от других. 
- NTFS. Структура системы хранения данных имеет вид бинарного дерева. В отличие от иерархической, как у FAT32, доступ к информации осуществляется по запросу, а поиск ведется по названию файла. При этом система имеет каталог, отсортированный по названиям. Массив делится на 2 части и отсекается та, в которой данного файла не будет, оставшаяся часть также делиться на 2, и так далее до тех пор, пока не будет найден нужный файл. 
- ReFS. Файловая система ReFS отличается высокой степенью надежности хранения файлов и легким их восстановлением в случае сбоя. 
- ZFS. Файловая система, разработанная для систем хранения данных. Главная ее черта – отказоустойчивость. Данные с которыми ведется работа копируются в служебный сектор. Его объем должен быть равен области хранения.

4. Как посмотреть, какие файловые системы подмонтированы в ОС?

Для монтирования и размонтирования файловых систем используются программы mount и umount. Информация о файловых системах и точках монтирования находится в файле /etc/fstab.

5. Как удалить зависший процесс?

Команда killall в Linux предназначена для «убийства» всех процессов, имеющих одно и то же имя.

# Вывод

Приобрела практические навыки установки операционной системы на виртуальную машину, настройки минимально необходимых для дальнейшей работы сервисов.

# Список литературы

1. Теоретические материалы курса.
