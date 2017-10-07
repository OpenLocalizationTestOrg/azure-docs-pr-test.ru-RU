---
title: "aaaHow toouse хранилище таблиц (C++) | Документы Microsoft"
description: "Хранения структурированных данных в облаке hello, с помощью хранилища таблиц Azure, хранилище данных NoSQL."
services: cosmos-db
documentationcenter: .net
author: mimig1
manager: jahogg
editor: tysonn
ms.assetid: f191f308-e4b2-4de9-85cb-551b82b1ea7c
ms.service: cosmos-db
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/28/2017
ms.author: mimig
ms.openlocfilehash: 8096fe531427ba4858f7f4cb7f664f941892d1c9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-table-storage-from-c"></a>Как toouse хранилище таблиц из C++
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a>Обзор
В этом руководстве будет показано, как tooperform распространенных сценариев с помощью hello службы хранилища таблиц Azure. Примеры Hello на языке C++ и использовать hello [клиентская библиотека хранилища Azure для C++](https://github.com/Azure/azure-storage-cpp/blob/master/README.md). Hello сценарии включают **Создание и удаление таблицы** и **работа с сущностями таблицы**.

> [!NOTE]
> Это руководство по цели hello клиентская библиотека хранилища Azure для C++ версии 1.0.0 и более поздних версий. Hello рекомендуемое версии клиентской библиотеки хранилища 2.2.0, которая доступна через [NuGet](http://www.nuget.org/packages/wastorage) или [GitHub](https://github.com/Azure/azure-storage-cpp/).
> 
> 

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-c-application"></a>Создание приложения на C++
В этом руководстве будут использоваться компоненты хранилища, которые могут выполняться в приложениях на C++. toodo таким образом, вам потребуется tooinstall hello клиентская библиотека хранилища Azure для C++ и создать учетную запись хранилища Azure в подписке Azure.  

hello tooinstall клиентская библиотека хранилища Azure для C++, можно использовать следующие методы hello:

* **Linux —** следуйте инструкциям hello hello [клиентская библиотека хранилища Azure для C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) страницы.  
* **Windows:** в Visual Studio нажмите **Инструменты > Диспетчер пакетов NuGet > Консоль диспетчера пакетов**. Команда hello введите следующее в hello [консоль диспетчера пакетов NuGet](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) и нажмите клавишу ВВОД.  
  
     Install-Package wastorage

## <a name="configure-your-application-tooaccess-table-storage"></a>Настройка вашего приложения tooaccess хранилище таблиц
Добавьте следующие hello включать инструкции toohello верхней части файла C++ hello место toouse hello хранилища Azure API-интерфейсы tooaccess таблиц:  

```cpp
#include <was/storage_account.h>
#include <was/table.h>
```

## <a name="set-up-an-azure-storage-connection-string"></a>Настройка строки подключения к хранилищу Azure
Клиент хранилища Azure использует хранилища конечные точки toostore соединения строки и учетные данные для доступа к службам данных управления. При запуске клиентского приложения, необходимо указать строку соединения хранения hello в кодировке hello. Имя учетной записи и hello хранилища ключи доступа к хранилищу для учетной записи хранения hello используйте hello, перечисленные в hello [портала Azure](https://portal.azure.com) для hello *AccountName* и *AccountKey* значения. Сведения об учетных записях хранения и ключах доступа см. в статье [Об учетных записях хранения Azure](../storage/common/storage-create-storage-account.md). В этом примере показано, как объявить строки подключения hello toohold статического поля:  

```cpp
// Define hello connection string with your values.
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

tootest приложения на локальном компьютере под управлением Windows, можно использовать hello Azure [эмулятор хранилища](../storage/common/storage-use-emulator.md) , установленная с hello [пакета Azure SDK](https://azure.microsoft.com/downloads/). Эмулятор хранилища Hello — это программа, которая имитирует hello Azure BLOB-объектов, очередей и таблиц служб, доступных на локальном компьютере разработчика. Hello следующем примере показано, как объявить статическое поле toohold hello соединения строки tooyour эмулятора локального хранилища:  

```cpp
// Define hello connection string with Azure storage emulator.
const utility::string_t storage_connection_string(U("UseDevelopmentStorage=true;"));  
```

toostart Здравствуйте эмулятор хранилища Azure, щелкните hello **запустить** или клавишу ключ Windows hello. Начните вводить **эмулятор хранилища Azure**, а затем выберите **эмулятор хранилища Microsoft Azure** hello списке приложений.  

Hello следующие образцы предполагается, что используется один из этих двух методов tooget hello строки подключения к хранилищу.  

## <a name="retrieve-your-connection-string"></a>Получить строку подключения
Можно использовать hello **cloud_storage_account** класса toorepresent сведения об учетной записи хранения. tooretrieve данные из строки подключения к хранилищу hello учетной записи хранилища, можно использовать метод parse hello.

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);
```

Затем следует получить tooa ссылку **cloud_table_client** класса, как она дает возможность ссылаться на объекты для таблиц и сущностей, сохраненными в hello службы хранилища таблиц. Hello следующий код создает **cloud_table_client** объекта с помощью объекта учетной записи хранилища hello, мы получить выше:  

```cpp
// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();
```

## <a name="create-a-table"></a>Создание таблицы
Объект **cloud_table_client** позволяет получить эталонные объекты для таблиц и сущностей. Hello следующий код создает **cloud_table_client** объекта и использует его toocreate новую таблицу.

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);  

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Retrieve a reference tooa table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create hello table if it doesn't exist.
table.create_if_not_exists();  
```

## <a name="add-an-entity-tooa-table"></a>Добавьте таблицу tooa сущности
tooadd таблицу tooa сущности, создайте новый **table_entity** и передать его слишком**table_operation::insert_entity**. Hello следующий код использует имя клиента hello как ключ строки hello и фамилию в качестве ключа секции hello. Вместе секции и ключом строки идентификации сущности hello hello таблицы. Ключи секций сущности с одинаковым ключом секции, которые могут запрашиваться быстрее, чем с различными приветствия, но с помощью различных разделов обеспечивает улучшенную масштабируемость параллельной операции. Дополнительные сведения см. в статье [Производительность хранилища Microsoft Azure и контрольный список масштабируемости](../storage/common/storage-performance-checklist.md).

Hello следующий код создает новый экземпляр **table_entity** с хранимых данных toobe некоторых клиентов система. Здравствуйте, следующий код вызывает метод **table_operation::insert_entity** toocreate **table_operation** объекта tooinsert сущность в таблицу, и связывает hello новая сущность таблицы с ним. Наконец, hello код вызывает метод execute hello на hello **cloud_table** объекта. И новый hello **table_operation** отправляет запрос toohello службы tooinsert hello новый клиент сущности таблицы в таблицу «people» hello.  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Retrieve a reference tooa table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create hello table if it doesn't exist.
table.create_if_not_exists();

// Create a new customer entity.
azure::storage::table_entity customer1(U("Harp"), U("Walter"));

azure::storage::table_entity::properties_type& properties = customer1.properties();
properties.reserve(2);
properties[U("Email")] = azure::storage::entity_property(U("Walter@contoso.com"));

properties[U("Phone")] = azure::storage::entity_property(U("425-555-0101"));

// Create hello table operation that inserts hello customer entity.
azure::storage::table_operation insert_operation = azure::storage::table_operation::insert_entity(customer1);

// Execute hello insert operation.
azure::storage::table_result insert_result = table.execute(insert_operation);
```

## <a name="insert-a-batch-of-entities"></a>Вставка пакета сущностей
Пакет toohello сущностей службы таблиц можно вставить в одну операцию записи. Hello следующий код создает **table_batch_operation** объекта, а затем добавляет три вставить tooit операций. Каждой операции вставки добавляется путем создания нового объекта сущностей задания его значений, и последующего вызова hello вставьте метод hello **table_batch_operation** сущности hello объекта tooassociate с новым операции вставки. Затем **cloud_table.execute** вызывается операция tooexecute hello.  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Define a batch operation.
azure::storage::table_batch_operation batch_operation;

// Create a customer entity and add it toohello table.
azure::storage::table_entity customer1(U("Smith"), U("Jeff"));

azure::storage::table_entity::properties_type& properties1 = customer1.properties();
properties1.reserve(2);
properties1[U("Email")] = azure::storage::entity_property(U("Jeff@contoso.com"));
properties1[U("Phone")] = azure::storage::entity_property(U("425-555-0104"));

// Create another customer entity and add it toohello table.
azure::storage::table_entity customer2(U("Smith"), U("Ben"));

azure::storage::table_entity::properties_type& properties2 = customer2.properties();
properties2.reserve(2);
properties2[U("Email")] = azure::storage::entity_property(U("Ben@contoso.com"));
properties2[U("Phone")] = azure::storage::entity_property(U("425-555-0102"));

// Create a third customer entity tooadd toohello table.
azure::storage::table_entity customer3(U("Smith"), U("Denise"));

azure::storage::table_entity::properties_type& properties3 = customer3.properties();
properties3.reserve(2);
properties3[U("Email")] = azure::storage::entity_property(U("Denise@contoso.com"));
properties3[U("Phone")] = azure::storage::entity_property(U("425-555-0103"));

// Add customer entities toohello batch insert operation.
batch_operation.insert_or_replace_entity(customer1);
batch_operation.insert_or_replace_entity(customer2);
batch_operation.insert_or_replace_entity(customer3);

// Execute hello batch operation.
std::vector<azure::storage::table_result> results = table.execute_batch(batch_operation);
```

Некоторые действия toonote на пакетные операции:  

* Можно выполнять копирование too100 insert, delete, merge, replace, операции insert или merge и вставки или замены в любой комбинации в одном пакете.  
* В него входит только операция hello в пакете hello пакетная операция может быть операцией извлечения.  
* Все сущности в одной пакетной операции должен иметь hello же ключ секционирования.  
* Пакетная операция представляет ограниченный tooa полезных данных 4 МБ.  

## <a name="retrieve-all-entities-in-a-partition"></a>Получение всех сущностей в разделе
таблицы для всех сущностей в секции, используйте tooquery **table_query** объекта. Hello следующий пример кода задает фильтр для сущности, где ключ раздела hello 'Smith'. Этот пример выводит hello поля в каждой сущности в консоли toohello результаты запроса hello.  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Construct hello query operation for all customer entities where PartitionKey="Smith".
azure::storage::table_query query;

query.set_filter_string(azure::storage::table_query::generate_filter_condition(U("PartitionKey"), azure::storage::query_comparison_operator::equal, U("Smith")));

// Execute hello query.
azure::storage::table_query_iterator it = table.execute_query(query);

// Print hello fields for each customer.
azure::storage::table_query_iterator end_of_results;
for (; it != end_of_results; ++it)
{
    const azure::storage::table_entity::properties_type& properties = it->properties();

    std::wcout << U("PartitionKey: ") << it->partition_key() << U(", RowKey: ") << it->row_key()
        << U(", Property1: ") << properties.at(U("Email")).string_value()
        << U(", Property2: ") << properties.at(U("Phone")).string_value() << std::endl;
}  
```

запрос Hello в этом примере переводит все сущности hello, соответствующие условиям фильтра hello. Если вы используете большие таблицы и часто требуется сущностей таблицы toodownload hello, рекомендуется хранить данные в хранилище Azure BLOB-объектов вместо.

## <a name="retrieve-a-range-of-entities-in-a-partition"></a>Получение диапазона сущностей в разделе
Если вы не хотите tooquery все сущности hello в секции, можно указать диапазон, объединяя hello фильтра ключа секции с фильтром ключа строк. Hello следующий пример кода использует два tooget фильтры всех сущностей в разделе «Smith», где начинается с буквы, более ранних, чем 'E' hello алфавита ключ строки hello (имя), а затем выводит результаты запроса hello.  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create hello table query.
azure::storage::table_query query;

query.set_filter_string(azure::storage::table_query::combine_filter_conditions(
    azure::storage::table_query::generate_filter_condition(U("PartitionKey"),
    azure::storage::query_comparison_operator::equal, U("Smith")),
    azure::storage::query_logical_operator::op_and,
    azure::storage::table_query::generate_filter_condition(U("RowKey"), azure::storage::query_comparison_operator::less_than, U("E"))));

// Execute hello query.
azure::storage::table_query_iterator it = table.execute_query(query);

// Loop through hello results, displaying information about hello entity.
azure::storage::table_query_iterator end_of_results;
for (; it != end_of_results; ++it)
{
    const azure::storage::table_entity::properties_type& properties = it->properties();

    std::wcout << U("PartitionKey: ") << it->partition_key() << U(", RowKey: ") << it->row_key()
        << U(", Property1: ") << properties.at(U("Email")).string_value()
        << U(", Property2: ") << properties.at(U("Phone")).string_value() << std::endl;
}  
```

## <a name="retrieve-a-single-entity"></a>Извлечение одной сущности
Можно написать tooretrieve запроса конкретную сущность. Hello следующий код использует **table_operation::retrieve_entity** toospecify hello клиента «Джефф Петров». Этот метод возвращает только одну сущность, а не коллекцию и hello возвращенное значение находится в **table_result**. Указание ключи секций и строк в запросе является hello самый быстрый способ tooretrieve одной сущности из службы таблиц hello.  

```cpp
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Retrieve hello entity with partition key of "Smith" and row key of "Jeff".
azure::storage::table_operation retrieve_operation = azure::storage::table_operation::retrieve_entity(U("Smith"), U("Jeff"));
azure::storage::table_result retrieve_result = table.execute(retrieve_operation);

// Output hello entity.
azure::storage::table_entity entity = retrieve_result.entity();
const azure::storage::table_entity::properties_type& properties = entity.properties();

std::wcout << U("PartitionKey: ") << entity.partition_key() << U(", RowKey: ") << entity.row_key()
    << U(", Property1: ") << properties.at(U("Email")).string_value()
    << U(", Property2: ") << properties.at(U("Phone")).string_value() << std::endl;
```

## <a name="replace-an-entity"></a>Замена сущности
tooreplace сущности, получить его из службы таблиц hello, изменить объект сущности hello и сохранять изменения hello обратно toohello службы таблиц. Hello следующий код позволяет изменить адрес электронной почты и номер телефона существующего клиента. Вместо вызова метода **table_operation::insert_entity** этот код использует **table_operation::replace_entity**. В этом случае toobe сущности hello полностью заменить на сервере hello, пока не изменят hello объекта на сервере hello, так как он был извлечен, в этом случае hello операция завершится ошибкой. Эта ошибка является tooprevent приложение случайно перезаписанный изменения внесены между hello извлечения и обновления приложения другим компонентом. Hello правильной обработки данного сбоя — tooretrieve hello сущность снова, внесенные изменения (если она все еще действует) и затем выполнять другую **table_operation::replace_entity** операции. Hello следующем разделе будет показано, как toooverride это поведение.  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Replace an entity.
azure::storage::table_entity entity_to_replace(U("Smith"), U("Jeff"));
azure::storage::table_entity::properties_type& properties_to_replace = entity_to_replace.properties();
properties_to_replace.reserve(2);

// Specify a new phone number.
properties_to_replace[U("Phone")] = azure::storage::entity_property(U("425-555-0106"));

// Specify a new email address.
properties_to_replace[U("Email")] = azure::storage::entity_property(U("JeffS@contoso.com"));

// Create an operation tooreplace hello entity.
azure::storage::table_operation replace_operation = azure::storage::table_operation::replace_entity(entity_to_replace);

// Submit hello operation toohello Table service.
azure::storage::table_result replace_result = table.execute(replace_operation);
```

## <a name="insert-or-replace-an-entity"></a>Вставка или замена сущности
**table_operation::replace_entity** операции могут завершаться hello объекта было изменено, поскольку он был извлечен из сервера hello. Кроме того, необходимо извлечь hello сущности с hello сервера сначала для **table_operation::replace_entity** toobe успешно. Иногда, тем не менее, вы не знаете Если hello сущность существует на сервере hello и неприменимы hello текущие значения, сохраненные в ней — обновление перезаписывать их все. tooaccomplish это, следует использовать **table_operation::insert_or_replace_entity** операции. Эта операция вставляет сущность hello, если она не существует, или заменяет его, если это так, независимо от того, когда была произведена hello последнего обновления. В следующем примере кода hello, по-прежнему получить сущность customer hello Джефф Смит, но затем сохраняется задней toohello серверу с помощью **table_operation::insert_or_replace_entity**. Все изменения, сделанные сущности toohello между hello операции извлечения и обновления будут перезаписаны.  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Insert-or-replace an entity.
azure::storage::table_entity entity_to_insert_or_replace(U("Smith"), U("Jeff"));
azure::storage::table_entity::properties_type& properties_to_insert_or_replace = entity_to_insert_or_replace.properties();

properties_to_insert_or_replace.reserve(2);

// Specify a phone number.
properties_to_insert_or_replace[U("Phone")] = azure::storage::entity_property(U("425-555-0107"));

// Specify an email address.
properties_to_insert_or_replace[U("Email")] = azure::storage::entity_property(U("Jeffsm@contoso.com"));

// Create an operation tooinsert-or-replace hello entity.
azure::storage::table_operation insert_or_replace_operation = azure::storage::table_operation::insert_or_replace_entity(entity_to_insert_or_replace);

// Submit hello operation toohello Table service.
azure::storage::table_result insert_or_replace_result = table.execute(insert_or_replace_operation);
```

## <a name="query-a-subset-of-entity-properties"></a>Запрос подмножества свойств сущности
Таблицы tooa запроса можно получить только несколько свойств сущности. Hello запрос в hello, следующий код использует hello **table_query::set_select_columns** метод tooreturn только hello адреса электронной почты сущности в таблице hello.  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Define hello query, and select only hello Email property.
azure::storage::table_query query;
std::vector<utility::string_t> columns;

columns.push_back(U("Email"));
query.set_select_columns(columns);

// Execute hello query.
azure::storage::table_query_iterator it = table.execute_query(query);

// Display hello results.
azure::storage::table_query_iterator end_of_results;
for (; it != end_of_results; ++it)
{
    std::wcout << U("PartitionKey: ") << it->partition_key() << U(", RowKey: ") << it->row_key();

    const azure::storage::table_entity::properties_type& properties = it->properties();
    for (auto prop_it = properties.begin(); prop_it != properties.end(); ++prop_it)
    {
        std::wcout << ", " << prop_it->first << ": " << prop_it->second.str();
    }

    std::wcout << std::endl;
}
```

> [!NOTE]
> Запрос нескольких свойств сущности является более эффективной операцией, чем запрос всех свойств.
> 
> 

## <a name="delete-an-entity"></a>Удаление сущности
Сущность можно легко удалить после ее получения. Когда извлекается hello объекта, вызовите **table_operation::delete_entity** с toodelete hello сущности. Затем вызовите hello **cloud_table.execute** метод. Hello следующий код извлекает и удаляет сущность с ключом раздела «Smith» и ключ строки «Джефф».  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create an operation tooretrieve hello entity with partition key of "Smith" and row key of "Jeff".
azure::storage::table_operation retrieve_operation = azure::storage::table_operation::retrieve_entity(U("Smith"), U("Jeff"));
azure::storage::table_result retrieve_result = table.execute(retrieve_operation);

// Create an operation toodelete hello entity.
azure::storage::table_operation delete_operation = azure::storage::table_operation::delete_entity(retrieve_result.entity());

// Submit hello delete operation toohello Table service.
azure::storage::table_result delete_result = table.execute(delete_operation);  
```

## <a name="delete-a-table"></a>Удаление таблицы
Наконец hello, следующий пример кода удаляет таблицу из учетной записи хранения. Таблицы, которая была удалена, будет недоступен toobe повторно создан для определенного периода времени после удаления hello.  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create an operation tooretrieve hello entity with partition key of "Smith" and row key of "Jeff".
azure::storage::table_operation retrieve_operation = azure::storage::table_operation::retrieve_entity(U("Smith"), U("Jeff"));
azure::storage::table_result retrieve_result = table.execute(retrieve_operation);

// Create an operation toodelete hello entity.
azure::storage::table_operation delete_operation = azure::storage::table_operation::delete_entity(retrieve_result.entity());

// Submit hello delete operation toohello Table service.
azure::storage::table_result delete_result = table.execute(delete_operation);
```

## <a name="next-steps"></a>Дальнейшие действия
Теперь, когда вы узнали основы hello хранилища таблицы, выполните следующие дополнительные сведения о хранилище Azure toolearn ссылки.  

* [Обозреватель хранилищ Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md) является бесплатной, отдельное приложение от Майкрософт, позволяющая toowork визуально с помощью данных из хранилища Azure в Windows, macOS и Linux.
* [Как toouse хранилища BLOB-объектов из C++](../storage/blobs/storage-c-plus-plus-how-to-use-blobs.md)
* [Как toouse хранилища очередей из C++](../storage/queues/storage-c-plus-plus-how-to-use-queues.md)
* [Перечисление ресурсов хранилища Azure в C++](../storage/common/storage-c-plus-plus-enumeration.md)
* [Справочник по клиентской библиотеке хранилища для C++](http://azure.github.io/azure-storage-cpp)
* [Документация по службе хранилища Azure](https://azure.microsoft.com/documentation/services/storage/)
