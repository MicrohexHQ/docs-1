# Получить список виртуальных машин в группе

После создания группы виртуальных машин вы можете получить список машин в группе.

Чтобы получить список виртуальных машин:

{% list tabs %}

- Консоль управления
  
  1. Откройте страницу каталога в консоли управления.
  1. Выберите сервис **{{ compute-full-name }}**.
  1. На странице **Виртуальные машины** перейдите на вкладку **Группы виртуальных машин**.
  1. Нажмите на имя нужной группы.
  1. На странице **Обзор** перейдите на вкладку **Список ВМ**.
  
- CLI
  
  {% include [cli-install.md](../../../_includes/cli-install.md) %}
  
  {% include [default-catalogue.md](../../../_includes/default-catalogue.md) %}
  
  1. Посмотрите описание команды CLI для получения списка виртуальных машин:
  
      ```
      $ yc compute instance-group list-instances --help
      ```
  
  1. Получите список групп виртуальных машин в каталоге по умолчанию:
  
      {% include [instance-group-list.md](../../../_includes/instance-groups/instance-group-list.md) %}
  
  1. Выберите `ID` или `NAME` нужной группы, например `first-fixed-group`.
  1. Получите информацию о группе виртуальных машин:
  
      ```
      $ yc compute instance-group list-instances --name first-fixed-group
      ```
  
- API
  
  Воспользуйтесь методом API [listInstances](../../api-ref/InstanceGroup/listInstances.md).
  
{% endlist %}
