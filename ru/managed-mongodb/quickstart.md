# Как начать работать с {{ mmg-short-name }}


Чтобы воспользоваться сервисом, нужно создать кластер и подключиться к СУБД:

1. Чтобы создать кластер баз данных, понадобится только доступный вам каталог в Яндекс.Облаке. Если у вас уже есть каталог в Яндекс.Облаке, откройте страницу этого каталога в консоли управления. Если каталога еще нет, создайте его:

    {% include [create-folder](../_includes/create-folder.md) %}

2. Создайте виртуальную машину (на основе [Linux](../compute/quickstart/quick-create-linux.md) или [Windows](../compute/quickstart/quick-create-windows.md)), с которой вы будете обращаться к кластеру БД. Если вы планируете подключаться к базе данных извне Облака, запросите внешние IP-адреса для хостов при создании кластера.

   1. Чтобы подключаться изнутри Облака, создайте виртуальную машину в той же сети, что и кластер БД (на основе [Linux](../compute/quickstart/quick-create-linux.md) или [Windows](../compute/quickstart/quick-create-windows.md))
   1. Чтобы подключаться к кластеру через интернет, запросите внешние IP-адреса для хостов при создании кластера.

1. В [консоли управления]({{ link-console-main }}) выберите каталог, в котором нужно создать кластер БД.
1. Выберите сервис **{{ mmg-name }}**.
1. Нажмите кнопку **Создать кластер** и выберите нужную СУБД.
1. Задайте параметры кластера и нажмите кнопку **Создать кластер**. Процесс подробно рассмотрен в разделе [{#T}](operations/cluster-create.md).
1. Когда кластер будет готов к работе, его статус на панели {{ mmg-short-name }} сменится на **RUNNING**.
1. Чтобы подключиться к серверу БД, необходим SSL-сертификат. Подготовить все нужные аутентификационные данные можно, например, так:

    ```bash
    $ mkdir ~/.mongodb
    $ wget "https://storage.yandexcloud.net/cloud-certs/CA.pem" -O ~/.mongodb/CA.pem
    ```
 
 1. Теперь подключитесь к кластеру:
 
    ```bash
    $ mongo --norc \
            --ssl \
            --sslCAFile ~/.mongodb/CA.pem \
            --ipv6 \
            --host 'rs01/<адрес хоста 1>:27018,<адрес хоста 2>:27018,<адрес хоста N>:27018' \
            -u <имя пользователя> \
            -p <пароль пользователя> \
            <имя БД>
    ```
