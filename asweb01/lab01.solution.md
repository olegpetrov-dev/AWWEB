# Лабораторная работа №1. Контейнеризация. Отчет.

Данная лабораторная работа знакомит с основами контейнеризации и подготавливает рабочее место
для выполнения следующих лабораторных работ.

## Подготовка

&#9745; Скачайте и установите [Docker Desktop](https://www.docker.com/products/docker-desktop/).

## Выполнение

Создайте папку `asweb01`.

Создайте файл `Dockerfile` со следующим содержимым:

```dockerfile
FROM debian:latest
COPY ./site/ /var/www/html/
CMD ["sh", "-c", "echo hello from $HOSTNAME"]
```

В папке asweb01 создайте папку `site`. В новой папке создайте файл `index.html` с каким-либо
содержимым.

## Запуск и тестирование

Откройте терминал в папке `asweb01` и выполните команду:

```bash
docker build -t asweb01 .
```

_Сколько времени создавался образ?_
```bash
PS F:\1Учеба\USM\3 Курс\ASWEB\labs> cd .\asweb01\
PS F:\1Учеба\USM\3 Курс\ASWEB\labs\asweb01> docker build -t asweb01 .
[+] Building 16.6s (7/7) FINISHED 
```

Выполните команду для запуска контейнера:

```bash
docker run --name asweb01 asweb01
```

_Что было выведено в консоли?_
```bash
PS F:\1Учеба\USM\3 Курс\ASWEB\labs\asweb01> docker run --name asweb01 asweb01
hello from 5c1e13a7a9b9
```

Удалите контейнер и запустите снова, выполнив команды:

```bash
docker rm asweb01
docker run -ti --name asweb01 asweb01 bash
```

В открывшемся окне выполните команды:

```bash
cd /var/www/html/
ls -l
```

_Что выводится на экране?_

```bash
PS F:\1Учеба\USM\3 Курс\ASWEB\labs\asweb01> docker run -ti --name asweb01 asweb01 bash
root@1dfa7f40b42d:/# cd /var/www/html/
root@1dfa7f40b42d:/var/www/html# ls -l
total 4
-rwxr-xr-x 1 root root 750 Dec 16 16:26 index.html
```

&#9745; Закройте окно командой `exit`.
