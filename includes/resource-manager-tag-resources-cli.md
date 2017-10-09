использовать tooadd группу ресурсов тег tooa **набор групп azure**. Если группа ресурсов hello не имеет существующие теги, передайте тег hello.

```azurecli
azure group set -n tag-demo-group -t Dept=Finance
```

При этом обновляются все теги. Если вы хотите tooadd группу ресурсов tooa тег с существующие теги, передайте все теги hello. 

```azurecli
azure group set -n tag-demo-group -t Dept=Finance;Environment=Production;Project=Upgrade
```

Ресурсы не унаследуют теги в группе ресурсов. использовать tooadd ресурс tooa тег **набор ресурсов azure**. Передайте hello номер версии API для hello тип ресурса, который вы добавляете тег hello. При необходимости tooretrieve hello API версии используйте следующую команду с поставщиком ресурсов hello для типа hello установки hello:

```azurecli
azure provider show -n Microsoft.Storage --json
```

В результатах hello поиск нужного типа ресурса hello.

```azurecli
"resourceTypes": [
{
  "resourceType": "storageAccounts",
  ...
  "apiVersions": [
    "2016-01-01",
    "2015-06-15",
    "2015-05-01-preview"
  ]
}
...
```

Теперь укажите эту версию API, имя группы ресурсов, имя ресурса, тип ресурса и значение тега в качестве параметров.

```azurecli
azure resource set -g tag-demo-group -n storagetagdemo -r Microsoft.Storage/storageAccounts -t Dept=Finance -o 2016-01-01
```

Существующие теги находятся непосредственно в ресурсах и группах ресурсов. существующие теги hello toosee получить группу ресурсов и его ресурсы с **Показать группу azure**.

```azurecli
azure group show -n tag-demo-group --json
```

Которая возвращает метаданные о hello группы ресурсов, включая любые теги, примененные tooit.

```azurecli
{
  "id": "/subscriptions/4705409c-9372-42f0-914c-64a504530837/resourceGroups/tag-demo-group",
  "name": "tag-demo-group",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "location": "southcentralus",
  "tags": {
    "Dept": "Finance",
    "Environment": "Production",
    "Project": "Upgrade"
  },
  ...
}
```

Просмотр hello тегов для определенного ресурса с помощью **Показать ресурсов azure**.

```azurecli
azure resource show -g tag-demo-group -n storagetagdemo -r Microsoft.Storage/storageAccounts -o 2016-01-01 --json
```

tooretrieve использовать все ресурсы hello со значением тега:

```azurecli
azure resource list -t Dept=Finance --json
```

Используйте для всех групп ресурсов hello со значением тега tooretrieve:

```azurecli
azure group list -t Dept=Finance
```

Можно просматривать существующие теги hello в вашей подписке на hello следующую команду:

```azurecli
azure tag list
```
