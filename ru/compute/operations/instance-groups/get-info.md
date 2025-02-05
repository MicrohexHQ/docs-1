# Получить информацию о группе виртуальных машин

После создания группы виртуальных машин вы можете получить основную информацию о группе.

Пользовательские [метаданные](../../concepts/vm-metadata.md), которые были переданы при создании или изменении группы, можно получить только с помощью CLI или API.

Чтобы получить информацию о группе виртуальных машин:

{% list tabs %}

- Консоль управления
  
  1. Откройте страницу каталога в консоли управления.
  1. Выберите сервис **{{ compute-full-name }}**.
  1. На странице **Виртуальные машины** перейдите на вкладку **Группы виртуальных машин**.
  1. Нажмите на имя нужной группы.
  
- CLI
  
  {% include [cli-install.md](../../../_includes/cli-install.md) %}
  
  {% include [default-catalogue.md](../../../_includes/default-catalogue.md) %}
  
  1. Посмотрите описание команды CLI для получения информации о группе виртуальных машин:
  
      ```
      $ yc compute instance-group get --help
      ```
  
  1. Получите список групп виртуальных машин в каталоге по умолчанию:
  
      {% include [instance-group-list.md](../../../_includes/instance-groups/instance-group-list.md) %}
  
  1. Выберите `ID` или `NAME` нужной группы, например `first-fixed-group`.
  1. Получите информацию о группе виртуальных машин:
  
      ```
      $ yc compute instance-group get --name first-fixed-group
      ```
  
- API
  
  Воспользуйтесь методом API [get](../../api-ref/InstanceGroup/get.md).
  
  Список доступных групп запрашивайте методом [listInstances](../../api-ref/InstanceGroup/listInstances.md).
  
{% endlist %}
