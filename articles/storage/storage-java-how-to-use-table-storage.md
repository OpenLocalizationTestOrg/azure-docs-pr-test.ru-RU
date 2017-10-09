---
title: "aaaHow toouse хранилище таблиц из Java | Документы Microsoft"
description: "Хранения структурированных данных в облаке hello, с помощью хранилища таблиц Azure, хранилище данных NoSQL."
services: storage
documentationcenter: java
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 45145189-e67f-4ca6-b15d-43af7bfd3f97
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: f72cac3fc10cf0aef74780b84c515d93d715d787
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-table-storage-from-java"></a>Как toouse хранилище таблиц из Java
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a>Обзор
В этом руководстве будет показано, как tooperform распространенных сценариев использования hello службы хранилища таблиц Azure. Hello примеры написаны на Java и использовать hello [пакет SDK хранилища Azure для Java][Azure Storage SDK for Java]. Hello сценарии включают **создание**, **вывод**, и **удаление** таблиц, а также **Вставка**,  **запрос**, **изменение**, и **удаление** сущностей в таблице. Дополнительные сведения о таблицах см. в разделе hello [дальнейшие действия](#Next-Steps) раздела.

Примечание. Пакет SDK доступен для разработчиков, которые используют хранилище Azure на устройствах под управлением Android. Дополнительные сведения см. в разделе hello [пакет SDK хранилища Azure для Android][Azure Storage SDK for Android].

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-java-application"></a>Создание приложения Java
В этом руководстве будут использоваться компоненты хранилища, которые могут быть вызваны локально в приложении Java или в коде, работающем в веб-роли или рабочей роли в Azure.

toodo таким образом, вам потребуется tooinstall hello Java Development Kit (JDK) и создать учетную запись хранилища Azure в подписке Azure. Как только вы делали, вам потребуется tooverify, разработки система удовлетворяет минимальным требованиям hello и зависимости, которые указаны в hello [пакет SDK хранилища Azure для Java] [ Azure Storage SDK for Java] репозитория в GitHub. Если компьютер соответствует этим требованиям, можно выполнить hello инструкции по загрузке и установке hello библиотеки хранилища Azure для Java в вашей системе из этого репозитория. После завершения этих задач можно будет toocreate приложения Java, использующего hello примеры в этой статье.

## <a name="configure-your-application-tooaccess-table-storage"></a>Настройка хранилища таблицы tooaccess приложения
Добавьте следующие начало toohello инструкции импорта файла Java hello, место таблиц tooaccess API-интерфейсов хранилища Microsoft Azure toouse hello:

```java
// Include hello following imports toouse table APIs
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.table.*;
import com.microsoft.azure.storage.table.TableQuery.*;
```

## <a name="set-up-an-azure-storage-connection-string"></a>Настройка строки подключения к хранилищу Azure
Клиент хранилища Azure использует хранилища конечные точки toostore соединения строки и учетные данные для доступа к службам данных управления. При работе в клиентском приложении, необходимо указать строку соединения хранения hello в hello следующая формата, используя hello имя учетной записи и hello первичный ключ доступа для учетной записи хранения hello, перечисленные в hello [портал Azure](https://portal.azure.com)для hello *AccountName* и *AccountKey* значения. В этом примере показано, как объявить строки подключения hello toohold статического поля:

```java
// Define hello connection-string with your values.
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key";
```

Эта строка в приложения, запущенного в рамках роли в Microsoft Azure, могут храниться в файле конфигурации службы hello, *ServiceConfiguration.cscfg*и можно осуществить с помощью toohello вызова  **RoleEnvironment.getConfigurationSettings** метод. Ниже приведен пример получения строки подключения hello из **параметр** элемента с именем *StorageConnectionString* в файле конфигурации службы hello:

```java
// Retrieve storage account from connection-string.
String storageConnectionString =
    RoleEnvironment.getConfigurationSettings().get("StorageConnectionString");
```

Hello следующие образцы предполагается, что используется один из этих двух методов tooget hello строки подключения к хранилищу.

## <a name="how-to-create-a-table"></a>Практическое руководство. Создание таблицы
Объект **CloudTableClient** позволяет ссылаться на объекты таблиц и сущностей. Hello следующий код создает **CloudTableClient** объекта и использует его toocreate новый **CloudTable** объект, который представляет таблицу с именем «пользователи». (Примечание: существуют дополнительные способы toocreate **CloudStorageAccount** объектов; Дополнительные сведения см. в разделе **CloudStorageAccount** в hello [Azure SDK Справочник по клиентской хранилища].)

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create hello table if it doesn't exist.
    String tableName = "people";
    CloudTable cloudTable = tableClient.getTableReference(tableName);
    cloudTable.createIfNotExists();
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-list-hello-tables"></a>Как: список таблиц hello
список таблиц, вызов hello tooget **CloudTableClient.listTables()** tooretrieve метод итерируемого перечень имен таблиц.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Loop through hello collection of table names.
    for (String table : tableClient.listTables())
    {
        // Output each table name.
        System.out.println(table);
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-add-an-entity-tooa-table"></a>Способ: добавьте таблицу tooa сущности
Сущности сопоставляют объекты tooJava, используя пользовательский класс, реализующий **TableEntity**. Для удобства hello **TableServiceEntity** класс реализует **TableEntity** и использует отражение toomap свойства с именем toogetter и задание значения для hello свойства. tooadd таблицу tooa сущности сначала создать класс, определяющий hello свойства сущности. Hello следующий код определяет класс сущностей, который использует имя клиента hello как ключ строки hello и фамилию в качестве ключа секции hello. Вместе секции и ключом строки идентификации сущности hello hello таблицы. Сущности с одинаковым ключом секции могут выполняться быстрее, чем с разными ключами секционирования приветствия.

```java
public class CustomerEntity extends TableServiceEntity {
    public CustomerEntity(String lastName, String firstName) {
        this.partitionKey = lastName;
        this.rowKey = firstName;
    }

    public CustomerEntity() { }

    String email;
    String phoneNumber;

    public String getEmail() {
        return this.email;
    }

    public void setEmail(String email) {
        this.email = email;
    }

    public String getPhoneNumber() {
        return this.phoneNumber;
    }

    public void setPhoneNumber(String phoneNumber) {
        this.phoneNumber = phoneNumber;
    }
}
```

Табличные операций, включающие сущности, требуют объект **TableOperation** . Этот объект определяет toobe операции hello выполнена на сущность, которая может выполняться с **CloudTable** объекта. Hello следующий код создает новый экземпляр hello **CustomerEntity** класса хранимых данных toobe некоторых клиентов система. Здравствуйте, следующий код вызывает метод **TableOperation.insertOrReplace** toocreate **TableOperation** объекта tooinsert сущность в таблицу, и связывает hello новые **CustomerEntity**с ним. Наконец, код hello вызывает hello **выполнение** метод hello **CloudTable** указание таблицы «people» hello и новый hello объекта **TableOperation**, которая затем отправляет запрос toohello хранилища службы tooinsert hello новой сущности customer в таблицу «люди» hello, или заменяет сущность hello в том случае, если он уже существует.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a new customer entity.
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.setEmail("Walter@contoso.com");
    customer1.setPhoneNumber("425-555-0101");

    // Create an operation tooadd hello new customer toohello people table.
    TableOperation insertCustomer1 = TableOperation.insertOrReplace(customer1);

    // Submit hello operation toohello table service.
    cloudTable.execute(insertCustomer1);
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-insert-a-batch-of-entities"></a>Практическое руководство. Вставка пакета сущностей
Пакет службы таблиц toohello сущностей можно вставить в одну операцию записи. Hello следующий код создает **TableBatchOperation** объекта, а затем добавляет три вставить tooit операций. Каждой операции вставки добавляется путем создания нового объекта сущностей, задание его значения и последующего вызова hello **вставить** метод hello **TableBatchOperation** объекта tooassociate hello сущности с новым операции вставки. Здравствуйте, затем код вызывает метод **выполнение** на hello **CloudTable** указание таблицы «people» hello и hello объекта **TableBatchOperation** объекта, который отправляет пакет hello таблицы Служба хранилища toohello операций в одном запросе.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Define a batch operation.
    TableBatchOperation batchOperation = new TableBatchOperation();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a customer entity tooadd toohello table.
    CustomerEntity customer = new CustomerEntity("Smith", "Jeff");
    customer.setEmail("Jeff@contoso.com");
    customer.setPhoneNumber("425-555-0104");
    batchOperation.insertOrReplace(customer);

    // Create another customer entity tooadd toohello table.
    CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
    customer2.setEmail("Ben@contoso.com");
    customer2.setPhoneNumber("425-555-0102");
    batchOperation.insertOrReplace(customer2);

    // Create a third customer entity tooadd toohello table.
    CustomerEntity customer3 = new CustomerEntity("Smith", "Denise");
    customer3.setEmail("Denise@contoso.com");
    customer3.setPhoneNumber("425-555-0103");
    batchOperation.insertOrReplace(customer3);

    // Execute hello batch of operations on hello "people" table.
    cloudTable.execute(batchOperation);
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

Некоторые действия toonote на пакетные операции:

* Можно выполнять копирование too100 insert, delete, merge, replace, insert или merge и вставки или замены в любой комбинации в одном пакете.
* В него входит только операция hello в пакете hello пакетная операция может быть операцией извлечения.
* Все сущности в одной пакетной операции должен иметь hello же ключ секционирования.
* Пакетная операция представляет полезные данные ограниченного tooa 4 МБ.

## <a name="how-to-retrieve-all-entities-in-a-partition"></a>Практическое руководство. Получение всех сущностей в разделе
tooquery таблицы для сущностей из секции, можно использовать **TableQuery**. Вызовите **TableQuery.from** toocreate запроса на определенной таблице, которая возвращает тип, заданный результат. Hello следующий код задает фильтр для сущности, где ключ раздела hello 'Smith'. **TableQuery.generateFilterCondition** — это вспомогательный метод toocreate фильтры для запросов. Вызовите **где** hello ссылки, возвращенные hello **TableQuery.from** метод tooapply hello фильтра toohello запроса. Если hello запрос выполняется с помощью вызова слишком**выполнение** на hello **CloudTable** он возвращает **итератор** с hello **CustomerEntity**указан тип результата. Затем можно использовать hello **итератор** возвращается в для каждого цикла tooconsume hello результатов. Этот код выводит hello поля в каждой сущности в консоли toohello результаты запроса hello.

```java
try
{
    // Define constants for filters.
    final String PARTITION_KEY = "PartitionKey";
    final String ROW_KEY = "RowKey";
    final String TIMESTAMP = "Timestamp";

    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a filter condition where hello partition key is "Smith".
    String partitionFilter = TableQuery.generateFilterCondition(
        PARTITION_KEY,
        QueryComparisons.EQUAL,
        "Smith");

    // Specify a partition query, using "Smith" as hello partition key filter.
    TableQuery<CustomerEntity> partitionQuery =
        TableQuery.from(CustomerEntity.class)
        .where(partitionFilter);

    // Loop through hello results, displaying information about hello entity.
    for (CustomerEntity entity : cloudTable.execute(partitionQuery)) {
        System.out.println(entity.getPartitionKey() +
            " " + entity.getRowKey() +
            "\t" + entity.getEmail() +
            "\t" + entity.getPhoneNumber());
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-retrieve-a-range-of-entities-in-a-partition"></a>Практическое руководство. Получение диапазона сущностей в разделе
Если вы не хотите tooquery все сущности hello в секции, можно указать диапазон с помощью операторов сравнения в фильтре. Здравствуйте, следующий код объединяет два фильтрует tooget всех сущностей в разделе «Smith» где ключ строки hello (имя) начинается с буквы вверх too'E "hello алфавита. Затем он выводит результаты запроса hello. При использовании таблицы добавлены toohello hello сущностей в пакете hello вставить данного руководства, возвращаются только две сущности, это время (Бен и Юлия Smith); Джефф Smith не включается.

```java
try
{
    // Define constants for filters.
    final String PARTITION_KEY = "PartitionKey";
    final String ROW_KEY = "RowKey";
    final String TIMESTAMP = "Timestamp";

    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a filter condition where hello partition key is "Smith".
    String partitionFilter = TableQuery.generateFilterCondition(
        PARTITION_KEY,
        QueryComparisons.EQUAL,
        "Smith");

    // Create a filter condition where hello row key is less than hello letter "E".
    String rowFilter = TableQuery.generateFilterCondition(
        ROW_KEY,
        QueryComparisons.LESS_THAN,
        "E");

    // Combine hello two conditions into a filter expression.
    String combinedFilter = TableQuery.combineFilters(partitionFilter,
        Operators.AND, rowFilter);

    // Specify a range query, using "Smith" as hello partition key,
    // with hello row key being up toohello letter "E".
    TableQuery<CustomerEntity> rangeQuery =
        TableQuery.from(CustomerEntity.class)
        .where(combinedFilter);

    // Loop through hello results, displaying information about hello entity
    for (CustomerEntity entity : cloudTable.execute(rangeQuery)) {
        System.out.println(entity.getPartitionKey() +
            " " + entity.getRowKey() +
            "\t" + entity.getEmail() +
            "\t" + entity.getPhoneNumber());
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-retrieve-a-single-entity"></a>Практическое руководство. Извлечение одной сущности
Можно написать tooretrieve запроса конкретную сущность. Hello следующий код вызывает **TableOperation.retrieve** с секции ключ и строку параметров ключа toospecify hello клиентом «Джефф Smith», вместо создания **TableQuery** и использование фильтров toodo hello одинаково. Во время выполнения получить hello, операция возвращает только одну сущность, а не коллекцию. Hello **getResultAsType** метод приводит hello результат toohello тип цели назначения hello, **CustomerEntity** объекта. Если этот тип несовместим с типом hello hello запросе указано, будет вызвано исключение. Значение NULL возвращается, если ни одна сущность не подходит по ключам раздела и строки. Указание ключи секций и строк в запросе является hello самый быстрый способ tooretrieve одной сущности из службы таблиц hello.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Retrieve hello entity with partition key of "Smith" and row key of "Jeff"
    TableOperation retrieveSmithJeff =
        TableOperation.retrieve("Smith", "Jeff", CustomerEntity.class);

    // Submit hello operation toohello table service and get hello specific entity.
    CustomerEntity specificEntity =
        cloudTable.execute(retrieveSmithJeff).getResultAsType();

    // Output hello entity.
    if (specificEntity != null)
    {
        System.out.println(specificEntity.getPartitionKey() +
            " " + specificEntity.getRowKey() +
            "\t" + specificEntity.getEmail() +
            "\t" + specificEntity.getPhoneNumber());
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-modify-an-entity"></a>Практическое руководство. Изменение сущности
toomodify сущности, получить его из службы таблиц hello, сделать объект сущности toohello изменения и сохранить изменения hello задней toohello службы таблиц с помощью операции слияния или замены. Hello следующий код позволяет изменить номер телефона существующего клиента. Вместо вызова метода **TableOperation.insert** как мы делали tooinsert, этот код вызывает **TableOperation.replace**. Hello **CloudTable.execute** метод вызывает службу hello таблицы и сущности hello заменяется первоначально другое приложение его hello времени с момента получения данного приложения, его. Когда это происходит, возникает исключение и hello сущности необходимо извлечь, изменения и снова сохранить. Этот оптимистичный шаблон повторения в случае конфликтов широко применяется в системе распределенного хранения.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Retrieve hello entity with partition key of "Smith" and row key of "Jeff".
    TableOperation retrieveSmithJeff =
        TableOperation.retrieve("Smith", "Jeff", CustomerEntity.class);

    // Submit hello operation toohello table service and get hello specific entity.
    CustomerEntity specificEntity =
        cloudTable.execute(retrieveSmithJeff).getResultAsType();

    // Specify a new phone number.
    specificEntity.setPhoneNumber("425-555-0105");

    // Create an operation tooreplace hello entity.
    TableOperation replaceEntity = TableOperation.replace(specificEntity);

    // Submit hello operation toohello table service.
    cloudTable.execute(replaceEntity);
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-query-a-subset-of-entity-properties"></a>Практическое руководство. Запрос подмножества свойств сущности
Таблицы tooa запроса можно получить только несколько свойств сущности. Этот метод, который называется "проекцией", снижает потребление пропускной способности и может повысить производительность запросов, особенно для крупных сущностей. Hello запрос в hello, следующий код использует hello **выберите** метод tooreturn только hello адреса электронной почты сущности в таблице hello. Hello результаты проецируются в коллекцию **строка** с помощью hello **EntityResolver**, который does hello преобразование типов сущностей hello, возвращенный от сервера hello. Дополнительные сведения о проекции см. в записи блога [Azure Tables: Introducing Upsert and Query Projection][Azure Tables: Introducing Upsert and Query Projection] (Таблицы Azure: введение в Upsert и проекции в запросах). Обратите внимание, что проекции не поддерживается эмуляторе hello локального хранилища, поэтому этот код выполняется только при использовании учетной записи для службы таблиц hello.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Define a projection query that retrieves only hello Email property
    TableQuery<CustomerEntity> projectionQuery =
        TableQuery.from(CustomerEntity.class)
        .select(new String[] {"Email"});

    // Define a Entity resolver tooproject hello entity toohello Email value.
    EntityResolver<String> emailResolver = new EntityResolver<String>() {
        @Override
        public String resolve(String PartitionKey, String RowKey, Date timeStamp, HashMap<String, EntityProperty> properties, String etag) {
            return properties.get("Email").getValueAsString();
        }
    };

    // Loop through hello results, displaying hello Email values.
    for (String projectedString :
        cloudTable.execute(projectionQuery, emailResolver)) {
            System.out.println(projectedString);
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-insert-or-replace-an-entity"></a>Как вставлять и заменять сущности
Часто возникает необходимость tooadd tooa сущности таблицы, не зная, если он уже существует в таблице hello. Операция вставки или замены позволяет toomake одного запроса, который будет вставлять hello сущности, если он не существует, или замените hello один существующий, если он не. Основываясь на предыдущих примерах, hello следующий код вставляет или заменяет сущность hello для «Уолтер Harp». После создания новой сущности, этот код вызывает hello **TableOperation.insertOrReplace** метод. Затем этот код вызывает **выполнение** на hello **CloudTable** объекта с помощью вставки таблицы и hello hello или заменить таблицу операцию, так как параметры hello. в сущности, tooupdate hello **TableOperation.insertOrMerge** можно метода. Обратите внимание, что вставки или replace не поддерживается на эмулятор локального хранилища hello, поэтому этот код выполняется только при использовании учетной записи для службы таблиц hello. Дополнительные сведения об операциях "вставка или замена" и "вставка или объединение" см. в записи блога [Azure Tables: Introducing Upsert and Query Projection][Azure Tables: Introducing Upsert and Query Projection] (Таблицы Azure: введение в Upsert и проекции в запросах).

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a new customer entity.
    CustomerEntity customer5 = new CustomerEntity("Harp", "Walter");
    customer5.setEmail("Walter@contoso.com");
    customer5.setPhoneNumber("425-555-0106");

    // Create an operation tooadd hello new customer toohello people table.
    TableOperation insertCustomer5 = TableOperation.insertOrReplace(customer5);

    // Submit hello operation toohello table service.
    cloudTable.execute(insertCustomer5);
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-delete-an-entity"></a>Практическое руководство. Удаление сущности
Сущность можно легко удалить после ее получения. Когда извлекается hello объекта, вызовите **TableOperation.delete** с toodelete hello сущности. Затем вызовите **выполнение** на hello **CloudTable** объекта. Привет, следующий код извлекает и удаляет сущность «клиент».

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create an operation tooretrieve hello entity with partition key of "Smith" and row key of "Jeff".
    TableOperation retrieveSmithJeff = TableOperation.retrieve("Smith", "Jeff", CustomerEntity.class);

    // Retrieve hello entity with partition key of "Smith" and row key of "Jeff".
    CustomerEntity entitySmithJeff =
        cloudTable.execute(retrieveSmithJeff).getResultAsType();

    // Create an operation toodelete hello entity.
    TableOperation deleteSmithJeff = TableOperation.delete(entitySmithJeff);

    // Submit hello delete operation toohello table service.
    cloudTable.execute(deleteSmithJeff);
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-delete-a-table"></a>Практическое руководство. Удаление таблицы
Наконец, hello следующий код удаляет таблицы из учетной записи хранилища. Таблицы, который был удален будет недоступным toobe повторно в течение заданного времени, после удаления hello, обычно менее 40 секунд.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Delete hello table and all its data if it exists.
    CloudTable cloudTable = tableClient.getTableReference("people");
    cloudTable.deleteIfExists();
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```
[!INCLUDE [storage-check-out-samples-java](../../includes/storage-check-out-samples-java.md)]

## <a name="next-steps"></a>Дальнейшие действия

* [Обозреватель хранилищ Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md) является бесплатной, отдельное приложение от Майкрософт, позволяющая toowork визуально с помощью данных из хранилища Azure в Windows, macOS и Linux.
* [Пакет SDK службы хранилища Azure для Java][Azure Storage SDK for Java]
* [Azure SDK Справочник по клиентской хранилища][Azure SDK Справочник по клиентской хранилища]
* [REST API службы хранилища Azure][Azure Storage REST API]
* [Блог рабочей группы службы хранилища Azure][Azure Storage Team Blog]

Дополнительные сведения см. также: hello [центра разработчиков Java](/develop/java/).

[Azure SDK for Java]: http://go.microsoft.com/fwlink/?LinkID=525671
[Azure Storage SDK for Java]: https://github.com/azure/azure-storage-java
[Azure Storage SDK for Android]: https://github.com/azure/azure-storage-android
[Azure SDK Справочник по клиентской хранилища]: http://dl.windowsazure.com/storage/javadoc/
[Azure Storage REST API]: https://msdn.microsoft.com/library/azure/dd179355.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
[Azure Tables: Introducing Upsert and Query Projection]: http://blogs.msdn.com/b/windowsazurestorage/archive/2011/09/15/windows-azure-tables-introducing-upsert-and-query-projection.aspx
