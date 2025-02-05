# AWS Command Line Interface (AWS CLI)

[AWS CLI](https://aws.amazon.com/ru/cli/) — это интерфейс командной строки для работы с сервисами AWS. Общий [порядок вызова команд](https://docs.aws.amazon.com/cli/latest/reference/) смотрите в официальной документации Amazon.

Для работы с {{ objstorage-full-name }} с помощью AWS CLI вы можете использовать следующие наборы команд:
- [s3api](https://docs.aws.amazon.com/cli/latest/reference/s3api/index.html) — команды, соответствующие операциям в REST API. Перед использованием ознакомьтесь с [перечнем поддерживаемых операций](../s3/api-ref/index.md).
- [s3](https://docs.aws.amazon.com/cli/latest/reference/s3/index.html) — дополнительные команды, упрощающие работу с большим количеством объектов.


## Подготовка к работе {#preparations}

{% include [storage-s3-http-api-preps](../_includes_service/storage-s3-http-api-preps.md) %}

## Установка {#installation}

Для установки AWS CLI воспользуйтесь [инструкцией](https://docs.aws.amazon.com/cli/latest/userguide/installing.html) на сайте разработчика.

## Настройка {#setup}

Для настройки AWS CLI используйте команду `aws configure`. Команда запросит значения для следующих параметров:

1. `AWS Access Key ID` — введите идентификатор ключа, который вы получили при генерации статического ключа.
1. `AWS Secret Access Key` — введите секретный ключ, который вы получили при генерации статического ключа.
1. `Default region name` — введите значение `ru-central1`.

   {% note info %}

   Для работы с Yandex Object Storage всегда указывайте регион — `ru-central1`. Другие значения региона могут привести к ошибке авторизации.

   {% endnote %}
1. Значения остальных параметров оставьте без изменений.

### Конфигурационные файлы {#config-files}

В результате своей работы команда `aws configure` сохранит настройки в файлах:

- Статический ключ в `.aws/credentials` в формате:
    ```
    [default]
                aws_access_key_id = id
                aws_secret_access_key = secretKey
    ```

- Регион по умолчанию в `.aws/config` в формате:
    ```
    [default]
                region=ru-central1
    ```


## Особенности {#specifics}

При использовании AWS CLI для работы с {{ objstorage-name }} учитывайте следующие особенности этого инструмента:
- AWS CLI работает с {{ objstorage-name }} как с иерархической файловой системой и ключи объектов имеют вид пути к файлу.
- При запуске команды `aws` для работы с {{ objstorage-name }} обязателен параметр `--endpoint-url`, поскольку по умолчанию клиент настроен на работу с серверами Amazon.
- При работе в macOS, в некоторых случаях требуется запуск вида:
    ```
    export PYTHONPATH=/Library/Python/2.7/site-packages; aws --endpoint-url=https://storage.yandexcloud.net s3 ls
    ```


## Примеры операций {#aws-cli-examples}

### Создать бакет

   ```bash
   aws --endpoint-url=https://storage.yandexcloud.net s3 mb s3://bucket-name
   ```

{% note info %}

При создании бакета помните об [ограничениях на имя](../concepts/bucket.md#naming).

{% endnote %}

### Загрузить объекты

Загрузить объекты можно разными способами, например:

- Загрузить все объекты из локальной директории:
   ```bash
   aws --endpoint-url=https://storage.yandexcloud.net \
       s3 cp --recursive local_files/ s3://bucket-name/path_style_prefix/
   ```
- Загрузить объекты, описанные в фильтре `--include`, и пропустить объекты, описанные в фильтре`--exclude`:
   ```bash
   aws --endpoint-url=https://storage.yandexcloud.net \
       s3 cp --recursive --exclude "*" --include "*.log" \
       local_files/ s3://bucket-name/path_style_prefix/
   ```
- Загрузить объекты по одному, запуская для каждого объекта команду следующего вида:
   ```bash
   aws --endpoint-url=https://storage.yandexcloud.net \
       s3 cp testfile.txt s3://bucket-name/path_style_prefix/textfile.txt
   ```

### Получить список объектов

   ```bash
   aws --endpoint-url=https://storage.yandexcloud.net \
       s3 ls --recursive s3://bucket-name
   ```

### Удалить объекты

Удалить объекты можно разными способами, например:

- Удалить все объекты с заданным префиксом.
   ```bash
   aws --endpoint-url=https://storage.yandexcloud.net \
       s3 rm s3://bucket-name/path_style_prefix/ --recursive
   ```
- Удалить объекты, описанные в фильтре `--include`, и пропустить объекты, описанные в фильтре`--exclude`:
   ```bash
   aws --endpoint-url=https://storage.yandexcloud.net \
       s3 rm s3://bucket-name/path_style_prefix/ --recursive \
       --exclude "*" --include "*.log"
   ```
- Удалить объекты по одному, запуская для каждого объекта команду следующего вида:
   ```bash
   aws --endpoint-url=https://storage.yandexcloud.net \
       s3 rm s3://bucket-name/path_style_prefix/textfile.txt
   ```

### Получить объект

   ```bash
   aws --endpoint-url=https://storage.yandexcloud.net \
       s3 cp s3://bucket-name/textfile.txt textfile.txt
   ```

