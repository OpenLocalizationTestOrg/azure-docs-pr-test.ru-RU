---
title: "aaaHow toouse табличного хранилища Azure из Ruby | Документы Microsoft"
description: "Хранения структурированных данных в облаке hello, с помощью хранилища таблиц Azure, хранилище данных NoSQL."
services: storage
documentationcenter: ruby
author: mmacy
manager: timlt
editor: 
ms.assetid: 047cd9ff-17d3-4c15-9284-1b5cc61a3224
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: 9c77ff9f384a776c9bc075b60b351685c61acc36
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-table-storage-from-ruby"></a>Как toouse табличного хранилища Azure из Ruby
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a>Обзор
В этом руководстве показано, как с помощью распространенных сценариев tooperform hello службы таблиц Azure. образцы Hello записываются с помощью Ruby API hello. Hello сценарии включают **Создание и удаление таблицы, вставка и выполнения запросов к сущностям в таблице**.

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-ruby-application"></a>Создание приложения Ruby
Инструкции toocreate приложении Ruby. в статье [Ruby на направляющие веб-приложения на Виртуальной машине Azure](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).

## <a name="configure-your-application-tooaccess-storage"></a>Настройка вашего приложения tooaccess хранилища
toouse хранилища Azure, понадобится toodownload и используйте hello Ruby azure пакет, который включает в себя набор библиотек удобства, взаимодействующих со службами хранилища REST hello.

### <a name="use-rubygems-tooobtain-hello-package"></a>Используйте RubyGems tooobtain hello пакет
1. Используйте интерфейс командной строки, например **PowerShell** (Windows), **Terminal** (Mac) или **Bash** (Unix).
2. Тип **gem установки azure** в hello команда окна tooinstall hello gem и зависимости.

### <a name="import-hello-package"></a>Импорт пакета hello
Используйте текстовый редактор, добавить следующие toohello вверху hello Ruby файл, куда будет toouse хранилища hello:

```ruby
require "azure"
```

## <a name="set-up-an-azure-storage-connection"></a>Настройка подключения к службе хранилища Azure
Hello модуль azure будет считывать переменные среды hello **AZURE\_ХРАНЕНИЯ\_учетной записи** и **AZURE\_ХРАНЕНИЯ\_доступа\_ключ**сведения, необходимые учетной записи хранилища Azure tooyour tooconnect. Если эти переменные среды не установлены, необходимо указать сведения об учетной записи hello перед использованием **Azure::TableService** с hello, следующий код:

```ruby
Azure.config.storage_account_name = "<your azure storage account>"
Azure.config.storage_access_key = "<your azure storage access key>"
```

tooobtain эти значения из классические или диспетчер ресурсов хранилища учетной записи в hello портала Azure:

1. Войдите в toohello [портал Azure](https://portal.azure.com).
2. Перейдите toohello необходимом toouse учетной записи хранилища.
3. В колонке параметров hello на hello вправо, щелкните **клавиши доступа**.
4. В колонке ключи hello доступа, отображается вы увидите ключ доступа hello 1 и ключ доступа 2. Можно использовать любой из них.
5. Щелкните hello скопировать значок toocopy hello ключа toohello буфер обмена.

Эти значения из классической хранилища учетной записи в классический портал Azure hello tooobtain:

1. Войдите в toohello [классический портал Azure](https://manage.windowsazure.com).
2. Перейдите toohello необходимом toouse учетной записи хранилища.
3. Нажмите кнопку **УПРАВЛЕНИЕ КЛЮЧАМИ доступа** hello нижней части панели навигации hello.
4. В диалоговом окне всплывающих hello вы увидите имя учетной записи хранения hello, первичный ключ доступа и вторичный ключ доступа. Клавиша доступа можно использовать hello первичной или вторичной hello.
5. Щелкните hello скопировать значок toocopy hello ключа toohello буфер обмена.

## <a name="create-a-table"></a>Создание таблицы
Hello **Azure::TableService** объектов позволяет работать с таблицами и сущностями. toocreate таблицы, используйте hello **создания\_table()** метод. Hello следующий пример создает таблицу или отпечатков hello ошибки, если оно назначено.

```ruby
azure_table_service = Azure::TableService.new
begin
    azure_table_service.create_table("testtable")
rescue
    puts $!
end
```

## <a name="add-an-entity-tooa-table"></a>Добавьте таблицу tooa сущности
tooadd сущности, сначала создать хэш-объект, определяющий свойства сущности. Обратите внимание, что для каждой сущности необходимо указать **PartitionKey** и **RowKey**. Это hello уникальные идентификаторы объектов и значений, которые могут запрашиваться гораздо быстрее, чем другие свойства. Хранилище Azure использует **PartitionKey** tooautomatically распределения сущностей таблицы hello по многим узлам хранилища. Здравствуйте сущности с одинаковым **PartitionKey** хранятся на hello того же узла. Hello **RowKey** hello уникальным идентификатором hello сущности внутри раздела hello, он принадлежит.

```ruby
entity = { "content" => "test entity",
    :PartitionKey => "test-partition-key", :RowKey => "1" }
azure_table_service.insert_entity("testtable", entity)
```

## <a name="update-an-entity"></a>Обновление сущности
Существует несколько методов, доступных tooupdate существующей сущности.

* **update\_entity():** обновляет имеющуюся сущность путем ее замены.
* **Слияние\_entity():** обновляет существующую сущность, объединив новых значений свойств в hello существующей сущности.
* **insert\_or\_merge\_entity():** обновляет имеющуюся сущность путем ее замены. Если сущность не существует, будет вставлена новая сущность.
* **Вставить\_или\_заменить\_entity():** обновляет существующую сущность, объединив новых значений свойств в hello существующей сущности. Если сущность не существует, будет вставлена новая сущность.

Hello ниже приведен пример обновления сущности, используя **обновление\_entity()**:

```ruby
entity = { "content" => "test entity with updated content",
    :PartitionKey => "test-partition-key", :RowKey => "1" }
azure_table_service.update_entity("testtable", entity)
```

С **обновление\_entity()** и **слияния\_entity()**, если сущности hello, обновление которого не существует, операция обновления hello завершается с ошибкой. Поэтому если вы хотите toostore сущности независимо от того, является ли он уже существует, следует использовать **вставить\_или\_заменить\_entity()** или **вставить\_или \_слияния\_entity()**.

## <a name="work-with-groups-of-entities"></a>Работа с группами сущностей
Иногда он делает toosubmit смысле несколько операций друг с другом в tooensure пакета atomic обработки сервером hello. tooaccomplish, сначала необходимо создать **пакета** объекта, а затем использовать hello **выполнение\_batch()** метод **TableService**. Hello ниже приведен пример отправки две сущности с RowKey 2 и 3 в пакете. Обратите внимание что он только работает для сущностей с hello же PartitionKey.

```ruby
azure_table_service = Azure::TableService.new
batch = Azure::Storage::Table::Batch.new("testtable",
    "test-partition-key") do
    insert "2", { "content" => "new content 2" }
    insert "3", { "content" => "new content 3" }
end
results = azure_table_service.execute_batch(batch)
```

## <a name="query-for-an-entity"></a>Запрос сущности
сущности в таблице, используйте hello tooquery **получить\_entity()** метод путем передачи имени таблицы hello, **PartitionKey** и **RowKey**.

```ruby
result = azure_table_service.get_entity("testtable", "test-partition-key",
    "1")
```

## <a name="query-a-set-of-entities"></a>Запрос набора сущностей
tooquery набора сущностей в таблице, создать хэш-объект запроса и использовать hello **запроса\_entities()** метод. Hello следующем примере показано получение всех сущностей hello hello же **PartitionKey**:

```ruby
query = { :filter => "PartitionKey eq 'test-partition-key'" }
result, token = azure_table_service.query_entities("testtable", query)
```

> [!NOTE]
> Если результирующий набор hello слишком велик для tooreturn одного запроса, токен продолжения будут возвращены которого производится tooretrieve последующих страницах.
>
>

## <a name="query-a-subset-of-entity-properties"></a>Запрос подмножества свойств сущности
Таблицы tooa запроса можно получить только несколько свойств сущности. Этот метод, который называется "проекцией", снижает потребление пропускной способности и может повысить производительность запросов, особенно для крупных сущностей. Предложение select используется hello и передайте hello имена hello свойства toobring через toohello клиента.

```ruby
query = { :filter => "PartitionKey eq 'test-partition-key'",
    :select => ["content"] }
result, token = azure_table_service.query_entities("testtable", query)
```

## <a name="delete-an-entity"></a>Удаление сущности
toodelete сущности, используйте hello **удаление\_entity()** метод. Вы должны toopass в качестве имени hello hello таблица, содержащая сущность hello, hello PartitionKey и RowKey hello сущности.

```ruby
azure_table_service.delete_entity("testtable", "test-partition-key", "1")
```

## <a name="delete-a-table"></a>Удаление таблицы
toodelete таблицы, используйте hello **удаление\_table()** метод и передайте имя hello hello toodelete таблицу.

```ruby
azure_table_service.delete_table("testtable")
```

## <a name="next-steps"></a>Дальнейшие действия

* [Обозреватель хранилищ Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md) является бесплатной, отдельное приложение от Майкрософт, позволяющая toowork визуально с помощью данных из хранилища Azure в Windows, macOS и Linux.
* [пакетов SDK Azure для Ruby](http://github.com/WindowsAzure/azure-sdk-for-ruby) на веб-сайте GitHub

