# F7. Корпоративная защита от внутренних угроз информационной безопасности

## Задания (Модуль Г)
**Задание 1**: Настройка сетевого окружения и компонентов систем 
С помощью технологии виртуальных машин VMWare для выполнения задания смоделирована корпоративная сеть организации на 2 филиалах. Необходимо самостоятельно настроить соединения между виртуальными машинами используя сетевые интерфейсы. При выполнении заданий необходимо ключевые настройки (установка паролей, настройки соединения с БД, компрометация, скриншоты работоспособной сети ViPNet и аналогичные) или указанные моменты в задании подтверждать скриншотами. Скриншоты необходимо сохранить на
рабочем столе в папке «Модуль InfoTeCS». Формат названия скриншотов: ITCS1-2-1.jpg (задание 1.2, скриншот 1). Можно добавить комментарий (ITCS-1-2-1-Coordinator).

Делать лишние скриншоты установки ПО нет необходимости, только скриншоты работоспособности! В ходе выполнения данного задания нужно установить основное ПО VipNet на
рабочие станции будущей защищенной сети.

Доступ на все Windows 10: **2003**
Все пароли пользователей в сети ViPNet сделать **xxXX2233**
Все пароли администраторов в сети ViPNet сделать **xxXX2233**.
В случае изменения паролей обязательно отразить это в отчете!

Перед установкой ПО ViPNet необходимо настроить сеть в соответствии со схемой. Необходимо записать все IP адреса, логины и пароли в текстовый файл vipnet.txt на рабочем столе хост-компьютера, где развернута сеть 1. Все дистрибутивы, лицензии и документация находятся на хост машине в папке D:\ViPNet на жестком диске (D).



## Решение заданий
Для начала разберемся, что мы имеем на данный момент. Нам доступно различное программное обеспечение ViPNet, в добавок имеется некоторый набор iso-образов ОС – Ubuntu и Windows 10. Плюс, ко всему ПО есть лицензии.

2 ----

Также под все хосты в представленных на схеме 3-х подсетях были сделаны папки, где будут расположены виртуальные машины. Предполагается, что сеть мы строим с нуля:

3 ----

Таблица с кратким описанием сетевых параметров хостов:

таблица ----

В качестве системы виртуализации был выбран VMware. Соответственно, всем виртуальным машинам впоследствии необходимо выдать и правильно настроить сетевые адаптеры. В нашем случае, вся настройка сетевых параметров будет производиться непосредственно на самих виртуальных машинах. Это означает, что конфигурировать сетевые адаптеры в VMware, не нужно. Сразу распределим сетевые интерфейсы:
- VMnet1 - Выход в Интернет (условный выход)
- VMnet2 - Подсеть ЦентрОфис
- VMnet3 - Подсеть Филиал
- VMnet4 - подсеть Межсеть

Теперь необходимо установить виртуальные хосты в те папки, что мы создали ранее. Создаем 9 вируальных машин на базе Windows 10 (версия Pro, но можно и более простые). Когда машины будут созданы, необходимо прокинуть общую папку с хоста на виртуальные машины (может быть и такое, что папки нельзя будет создать сразу для всех, отключить из одной ВМ и подключить в другую нам ничего не мешает).

4 ----

Перейдем на V-1-DB. Здесь будет установлен SQL Express Server. Создаем на диске C:\ папку SQLServer (C:\SQLServer). Разархивируем зарание на хосте архив с ViPNet Administrator 4.x. Теперь, находясь на V-1-DB можно беспрепятсвенно получить доступ к установщику SQL Server (Путь до файла: \\vmware-host\Shared Folders\ViPNet\ViPNet Administrator 4.x\1. ViPNet Administrator 4.6.4 NEW\1. Программное обеспечение\Центр управления сетью\Server Install\Packages\SqlExpress2014)

5 ----

Нам необходимо установить SQLEXPR_x64_ENU в C:\SQLServer. Далее у нас появится окно мастера установки. Необходимо выбрать New SQL Server stand-alone installation or add features to an existing installation. Далее показаны скриншоты того, что нужно поменять в параметрах установки:

