# Simple Docker
## Contents
  1.1. [Готовый докер](#part-1-готовый-докер) \
  1.2. [Операции с контейнером](#part-2-операции-с-контейнером) \
  1.3. [Мини веб-сервер](#part-3-мини-веб-сервер) \
  1.4. [Свой докер](#part-4-свой-докер) \
  1.5. [Dockle](#part-5-dockle) \
  1.6. [Базовый Docker Compose](#part-6-базовый-docker-compose)

## Part 1. Готовый докер

В качестве конечной цели своей небольшой практики вы сразу выбрали написание докер образа для собственного веб сервера, а потому в начале вам нужно разобраться с уже готовым докер образом для сервера.
Ваш выбор пал на довольно простой **nginx**.

**== Задание ==**

**Взять официальный докер образ с **nginx** и выкачать его при помощи `docker pull`**

<img width="1303" alt="pull nginx" src="https://user-images.githubusercontent.com/89585637/223464236-01088090-2d04-45e4-a514-33c99e83710f.png">

**Проверить наличие докер образа через `docker images`**

<img width="1200" alt="docker images" src="https://user-images.githubusercontent.com/89585637/223673191-6a072e72-b6f9-43ae-b5a0-4786aed91ebb.png">

**Запустить докер образ через `docker run -d [image_id|repository]`**

<img width="1256" alt="docker run " src="https://user-images.githubusercontent.com/89585637/223464592-26d9dbc1-828d-4d46-98c3-fa9cd3d73c56.png">

##### Проверить, что образ запустился через `docker ps`
##### Посмотреть информацию о контейнере через `docker inspect [container_id|container_name]`

<img width="1808" alt="docker inspect" src="https://user-images.githubusercontent.com/89585637/223464788-9464e193-1da7-4cd3-862e-1fba7e03c6af.png">

##### По выводу команды определить и поместить в отчёт размер контейнера, список замапленных портов и ip контейнера
Размер контейнера (с флагом -s, в kB));

<img width="1621" alt="docker inspect(1)" src="https://user-images.githubusercontent.com/89585637/223464933-a51d410a-cab3-43b9-8e41-2fb0722a1d02.png">
<img width="1711" alt="docker inspect(2)" src="https://user-images.githubusercontent.com/89585637/223464975-4ec26e6f-ac18-4b8b-b823-0532b21e79bc.png">

##### Остановить докер образ через `docker stop [container_id|container_name]`

<img width="1652" alt="docker stop" src="https://user-images.githubusercontent.com/89585637/223465057-1a5ed93b-3230-462a-8fea-6c443cf89546.png">

##### Проверить, что образ остановился через `docker ps`

<img width="1679" alt="docker ps" src="https://user-images.githubusercontent.com/89585637/223465112-0962d31f-4f45-4581-8fa8-7bb65dcb25e5.png">

##### Запустить докер с замапленными портами 80 и 443 на локальную машину через команду *run*

<img width="1788" alt="ports" src="https://user-images.githubusercontent.com/89585637/223465434-2a1c2aee-65da-4162-8cda-bdf64af5d807.png">

##### Проверить, что в браузере по адресу *localhost:80* доступна стартовая страница **nginx**

<img width="1963" alt="localhost" src="https://user-images.githubusercontent.com/89585637/223465232-3a3ad8f0-d478-4ffe-a3a1-8691a0fbee2a.png">
<img width="2287" alt="443" src="https://user-images.githubusercontent.com/89585637/223465277-31fb0e8c-8539-4f2c-8405-2d886793a8ba.png">

##### Перезапустить докер контейнер через `docker restart [container_id|container_name]`
**Проверить любым способом, что контейнер запустился**

<img width="1690" alt="docker restart" src="https://user-images.githubusercontent.com/89585637/223465574-e5815912-22e5-4b3b-bdd5-248ca6c26f79.png">


## Part 2. Операции с контейнером

Докер образ и контейнер готовы. Теперь можно покопаться в конфигурации **nginx** и отобразить статус страницы.

**== Задание ==**

##### Прочитать конфигурационный файл *nginx.conf* внутри докер образа через команду *exec*

<img width="1160" alt="Снимок экрана 2023-03-08 в 12 25 54" src="https://user-images.githubusercontent.com/89585637/223674720-3179b478-b882-4fd4-b662-ecfce97eaa97.png">

##### Создать на локальной машине файл *nginx.conf*

![image](https://user-images.githubusercontent.com/89585637/223537426-7c7a39e3-3f90-4f07-bb87-98ffd86da2ab.png)

##### Настроить в нем по пути */status* отдачу страницы статуса сервера **nginx**
##### Скопировать созданный файл *nginx.conf* внутрь докер образа через команду `docker cp`

![image](https://user-images.githubusercontent.com/89585637/223535469-022ebd6d-df63-40fb-8594-c32c5e6267f1.png)

##### Перезапустить **nginx** внутри докер образа через команду *exec*

![image](https://user-images.githubusercontent.com/89585637/223536245-6e244320-80a3-4e9f-a854-a794ff5993d2.png)

##### Проверить, что по адресу *localhost:80/status* отдается страничка со статусом сервера **nginx**

![image](https://user-images.githubusercontent.com/89585637/223537344-0ad3f821-81c8-4ebe-8cfb-0e87626c7109.png)

##### Экспортировать контейнер в файл *container.tar* через команду *export*
##### Остановить контейнер

![image](https://user-images.githubusercontent.com/89585637/223535732-bb8a0939-246d-4cec-8621-b9d1dd9aad40.png)

##### Удалить образ через `docker rmi [image_id|repository]`, не удаляя перед этим контейнеры
##### Импортировать контейнер обратно через команду *import*

![image](https://user-images.githubusercontent.com/89585637/223535822-b74b7559-1cea-401c-b29f-fc27d6724a09.png)

##### Запустить импортированный контейнер

![image](https://user-images.githubusercontent.com/89585637/223535881-409f6b75-e79c-430a-b8f3-2ab99a776015.png)

<img width="1451" alt="localhost status" src="https://user-images.githubusercontent.com/89585637/223676573-21f794c9-c829-4e18-bf22-bc003e6229e8.png">

## Part 3. Мини веб-сервер

Настало время немного оторваться от докера, чтобы подготовиться к последнему этапу. Настало время написать свой сервер.

**== Задание ==**

![image](https://user-images.githubusercontent.com/89585637/223534328-d34a873d-9774-4250-8c21-292a7c1c4ce0.png)

![image](https://user-images.githubusercontent.com/89585637/223536786-fa1471fc-3b57-4528-a156-21548766a233.png)

##### Написать мини сервер на **C** и **FastCgi**, который будет возвращать простейшую страничку с надписью `Hello World!`

![image](https://user-images.githubusercontent.com/89585637/223534177-e5ce0ec9-121e-4722-b262-5ebd6307c0b8.png)

##### Запустить написанный мини сервер через *spawn-cgi* на порту 8080

![image](https://user-images.githubusercontent.com/89585637/223536562-1ea6feaa-6585-4c4c-949e-074a1d544443.png)

![image](https://user-images.githubusercontent.com/89585637/223534569-35a0964b-825f-4327-94ff-fab726dd302e.png)

##### Написать свой *nginx.conf*, который будет проксировать все запросы с 81 порта на *127.0.0.1:8080*

![image](https://user-images.githubusercontent.com/89585637/223534413-74d7fed2-c18e-4608-bbc6-edb19a0df1bd.png)

##### Проверить, что в браузере по *localhost:81* отдается написанная вами страничка

![image](https://user-images.githubusercontent.com/89585637/223534800-8583eec8-6967-400b-a5ba-6b72b6bb9c65.png)

![image](https://user-images.githubusercontent.com/89585637/223534475-3a5ea697-e075-4e3f-b552-49760e70fee6.png)

## Part 4. Свой докер

Теперь всё готово. Можно приступать к написанию докер образа для созданного сервера.

**== Задание ==**

*При написании докер образа избегайте множественных вызовов команд RUN*

#### Написать свой докер образ, который:
##### 1) собирает исходники мини сервера на FastCgi из [Части 3](#part-3-мини-веб-сервер)
##### 2) запускает его на 8080 порту
##### 3) копирует внутрь образа написанный *./nginx/nginx.conf*
##### 4) запускает **nginx**.
_**nginx** можно установить внутрь докера самостоятельно, а можно воспользоваться готовым образом с **nginx**'ом, как базовым._

##### Собрать написанный докер образ через `docker build` при этом указав имя и тег
docker build -f Dockerfile -t my_docker_image:task4 "../"

![image](https://user-images.githubusercontent.com/89585637/223532803-b1bce28a-4da5-40dc-8d32-95ee3db09588.png)

##### Проверить через `docker images`, что все собралось корректно

##### Запустить собранный докер образ с маппингом 81 порта на 80 на локальной машине и маппингом папки *./nginx* внутрь контейнера по адресу, где лежат конфигурационные файлы **nginx**'а (см. [Часть 2](#part-2-операции-с-контейнером))
docker run --name my_docker_container -p 80:81 -v $(pwd)/../nginx/nginx.conf:/etc/nginx/nginx.conf -dt my_docker_image:task4

![image](https://user-images.githubusercontent.com/89585637/223533110-bbbd1a66-00d4-4ebf-88e1-6e485b3d55ed.png)

##### Проверить, что по localhost:80 доступна страничка написанного мини сервера
##### Дописать в *./nginx/nginx.conf* проксирование странички */status*, по которой надо отдавать статус сервера **nginx**

![image](https://user-images.githubusercontent.com/89585637/223533865-9d5b2c50-3d94-400d-8121-fba0e7401314.png)

##### Перезапустить докер образ
*Если всё сделано верно, то, после сохранения файла и перезапуска контейнера, конфигурационный файл внутри докер образа должен обновиться самостоятельно без лишних действий*
##### Проверить, что теперь по *localhost:80/status* отдается страничка со статусом **nginx**

![image](https://user-images.githubusercontent.com/89585637/223533548-cdbe449a-e1c2-4c33-ae52-d0efdaa42c0c.png)


## Part 5. **Dockle**

После написания контейнера никогда не будет лишним проверить его на безопасность.

**== Задание ==**

##### Просканировать контейнер из предыдущего задания через `dockle [container_id|container_name]`
##### Исправить контейнер так, чтобы при проверке через **dockle** не было ошибок и предупреждений
ДО:
dockle my_docker_image:task4

![image](https://user-images.githubusercontent.com/89585637/223532622-051354e1-b265-468f-8d80-b6f8a79bb3de.png)

![image](https://user-images.githubusercontent.com/89585637/223525701-3a0bd2ce-2c12-4cc8-a234-2ff7efc063d0.png)

ПОСЛЕ:
docker build -f Dockerfile_task5 -t my_docker_image:task5 "../"
docker run --name my_docker_container -p 80:81 -v $(pwd)/../nginx/nginx.conf:/etc/nginx/nginx.conf -dt my_docker_image:task5

![image](https://user-images.githubusercontent.com/89585637/223525789-c578b14e-7450-4f4e-99e2-9fc9918ed611.png)
![image](https://user-images.githubusercontent.com/89585637/223525752-c03ae8f8-cbe8-47d2-8110-1a3eb4109826.png)

## Part 6. Базовый **Docker Compose**

Вот вы и закончили вашу разминку. А хотя погодите...
Почему бы не поэкспериментировать с развёртыванием проекта, состоящего сразу из нескольких докер образов?

**== Задание ==**

##### Написать файл *docker-compose.yml*, с помощью которого:
##### 1) Поднять докер контейнер из [Части 5](#part-5-инструмент-dockle) _(он должен работать в локальной сети, т.е. не нужно использовать инструкцию **EXPOSE** и мапить порты на локальную машину)_
##### 2) Поднять докер контейнер с **nginx**, который будет проксировать все запросы с 8080 порта на 81 порт первого контейнера
##### Замапить 8080 порт второго контейнера на 80 порт локальной машины


##### Остановить все запущенные контейнеры
docker ps -q | xargs docker stop

![image](https://user-images.githubusercontent.com/89585637/223525422-a92e718c-3b61-4377-90e4-85bbdb152386.png)

##### Собрать и запустить проект с помощью команд `docker-compose build` и `docker-compose up`
##### Проверить, что в браузере по *localhost:80* отдается написанная вами страничка, как и ранее

![image](https://user-images.githubusercontent.com/89585637/223525233-f872dfde-5899-45bb-b556-ec281e095adf.png)
![image](https://user-images.githubusercontent.com/89585637/223532394-811fc3b7-dc5e-4485-99f5-2e49f772b346.png)

