---
title: "Как использовать хранилище таблиц Azure из Java | Документация Майкрософт"
description: "Хранение структурированных данных в облаке в хранилище таблиц Azure (хранилище данных NoSQL)."
services: cosmos-db
documentationcenter: java
author: mimig1
manager: jhubbard
editor: tysonn
ms.assetid: 45145189-e67f-4ca6-b15d-43af7bfd3f97
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 11/03/2017
ms.author: mimig
ms.openlocfilehash: 6862475e05f49c7da823bcfb70f30ee484131d12
ms.sourcegitcommit: f1c1789f2f2502d683afaf5a2f46cc548c0dea50
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/18/2018
---
# <a name="how-to-use-azure-table-storage-from-java"></a>Как использовать хранилище таблиц Azure из Java
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-tip-include](../../includes/storage-table-cosmos-db-tip-include.md)]

## <a name="overview"></a>Обзор
В этом руководстве показано, как реализовать типичные сценарии с использованием службы табличного хранилища Azure. Примеры написаны на Java и используют [пакет SDK службы хранилища Azure для Java][Azure Storage SDK for Java]. Рассматриваются сценарии **создания**, **перечисления** и **удаления** таблиц, а также **вставки**, **запроса**, **изменения** и **удаления** сущностей в таблице. Дополнительные сведения о таблицах см. в разделе [Дальнейшие действия](#Next-Steps).

> [!NOTE]
> Пакет SDK доступен разработчикам, использующим хранилище Azure на устройствах Android. Дополнительные сведения см. в разделе [Microsoft Azure Storage SDK for Android][Azure Storage SDK for Android] (Пакет SDK хранилища Azure для Android).
>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-java-application"></a>Создание приложения Java
В этом руководстве будут использоваться компоненты хранилища, которые могут быть вызваны локально в приложении Java или в коде, работающем в веб-роли или рабочей роли в Azure.

Для этого необходимо установить пакет SDK для Java (JDK) и создать учетную запись хранения Azure в подписке Azure. После того, как это будет сделано, необходимо убедиться, что ваша система разработки отвечает минимальным требованиям и зависимостям, указанным в репозитории [пакета SDK службы хранилища Azure для Java][Azure Storage SDK for Java] на сайте GitHub. Если ваша система отвечает указанным требованиям можно приступить к выполнению инструкций по загрузке библиотек хранилища Azure для Java из репозитория и их установке на своей системе. После завершение этих задач вы сможете приступить к созданию приложения Java с использованием примеров из данной статьи.

## <a name="configure-your-application-to-access-table-storage"></a>Настройка приложения для доступа к хранилищу таблиц
Если нужно использовать API-интерфейсы хранилища Microsoft Azure для доступа к таблицам, добавьте следующие инструкции импорта в верхнюю часть файла Java.

```java
// Include the following imports to use table APIs
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.table.*;
import com.microsoft.azure.storage.table.TableQuery.*;
```

## <a name="set-up-an-azure-storage-connection-string"></a>Настройка строки подключения к хранилищу Azure
Клиент хранилища Azure использует строку подключения с целью хранения конечных точек и учетных данных для доступа к службам управления данными. При работе в клиентском приложении необходимо указать для хранилища строку подключения в следующем формате, используя имя своей учетной записи хранения и первичный ключ доступа для учетной записи хранения, указанные на [портале Azure](https://portal.azure.com) значениями *AccountName* и *AccountKey*. В этом примере показано, как объявить статическое поле для размещения строки подключения:

```java
// Define the connection-string with your values.
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key";
```

Если приложение выполняется в роли на платформе Microsoft Azure, эта строка может храниться в файле конфигурации службы *ServiceConfiguration.cscfg*, для доступа к которой можно использовать вызов метода **RoleEnvironment.getConfigurationSettings** . Ниже приведен пример получения строки подключения из элемента **Setting** с именем *StorageConnectionString* в файле конфигурации службы:

```java
// Retrieve storage account from connection-string.
String storageConnectionString =
    RoleEnvironment.getConfigurationSettings().get("StorageConnectionString");
```

В приведенных ниже примерах предполагается, что вы использовали одно из этих двух определений для получения строки подключения к хранилищу.

## <a name="how-to-create-a-table"></a>Практическое руководство. Создание таблицы
Объект **CloudTableClient** позволяет ссылаться на объекты таблиц и сущностей. Следующий код создает объект **CloudTableClient** и использует его для создания нового объекта **CloudTable**, который представляет таблицу people. 

> [!NOTE]
> Существуют также другие способы создания объектов **CloudStorageAccount**. Дополнительные сведения см. в разделе **CloudStorageAccount** [справочника по пакету SDK для клиента службы хранилища Azure].
>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create the table if it doesn't exist.
    String tableName = "people";
    CloudTable cloudTable = tableClient.getTableReference(tableName);
    cloudTable.createIfNotExists();
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-list-the-tables"></a>Как перечислять таблицы
Чтобы получить список таблиц, вызовите метод **CloudTableClient.listTables()** для извлечения пригодного к итерации списка имен таблиц.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Loop through the collection of table names.
    for (String table : tableClient.listTables())
    {
        // Output each table name.
        System.out.println(table);
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-add-an-entity-to-a-table"></a>Практическое руководство. Добавление сущности в таблицу
Сущности сопоставляются с объектами Java с помощью настраиваемого класса, реализующего **TableEntity**. Для удобства класс **TableServiceEntity** реализует **TableEntity** и использует отражение для сопоставления свойств с указанными для свойств методами получения и задания. Чтобы добавить сущность в таблицу, сначала создайте класс, который определяет свойства сущности. Следующий код определяет класс сущностей, который использует имя клиента как ключ строки, а фамилию клиента — как ключ раздела. Вместе ключ раздела и ключ строки сущности уникальным образом идентифицируют сущность в таблице. Сущности с одним ключом раздела можно запрашивать быстрее, чем сущности с разными ключами раздела.

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

Табличные операций, включающие сущности, требуют объект **TableOperation** . Этот объект определяет выполняемую для сущности операцию, которую можно запустить с помощью объекта **CloudTable** . В следующем коде создается новый экземпляр класса **CustomerEntity** с сохраняемыми данными клиента. Далее код вызывает **TableOperation.insertOrReplace**, чтобы создать объект **TableOperation** для вставки сущности в таблицу, а также связывает с ним новый объект **CustomerEntity**. Наконец код вызывает метод **execute** объекта **CloudTable**, определяя таблицу people и новый объект **TableOperation**, который затем отправляет запрос в службу хранилища для вставки новой сущности клиента в таблицу people или замены сущности, если она уже существует.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for the table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a new customer entity.
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.setEmail("Walter@contoso.com");
    customer1.setPhoneNumber("425-555-0101");

    // Create an operation to add the new customer to the people table.
    TableOperation insertCustomer1 = TableOperation.insertOrReplace(customer1);

    // Submit the operation to the table service.
    cloudTable.execute(insertCustomer1);
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-insert-a-batch-of-entities"></a>Практическое руководство. Вставка пакета сущностей
Вы можете вставить пакет сущностей в таблицу в одной операции записи. Следующий код создает объект **TableBatchOperation** , а затем добавляет в него три операции вставки. Каждая операция вставки добавляется путем создания нового объекта сущности, установки его значений и последующего вызова метода **insert** для объекта **TableBatchOperation**, чтобы связать сущность с новой операцией вставки. Затем код вызывает метод **execute** объекта **CloudTable**, определяя таблицу people и объект **TableBatchOperation**, который отправляет пакет операций таблицы в службу хранилища в одном запросе.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Define a batch operation.
    TableBatchOperation batchOperation = new TableBatchOperation();

    // Create a cloud table object for the table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a customer entity to add to the table.
    CustomerEntity customer = new CustomerEntity("Smith", "Jeff");
    customer.setEmail("Jeff@contoso.com");
    customer.setPhoneNumber("425-555-0104");
    batchOperation.insertOrReplace(customer);

    // Create another customer entity to add to the table.
    CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
    customer2.setEmail("Ben@contoso.com");
    customer2.setPhoneNumber("425-555-0102");
    batchOperation.insertOrReplace(customer2);

    // Create a third customer entity to add to the table.
    CustomerEntity customer3 = new CustomerEntity("Smith", "Denise");
    customer3.setEmail("Denise@contoso.com");
    customer3.setPhoneNumber("425-555-0103");
    batchOperation.insertOrReplace(customer3);

    // Execute the batch of operations on the "people" table.
    cloudTable.execute(batchOperation);
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

Некоторые другие примечания к пакетным операциям:

* В отдельном пакете можно выполнить до 100 операций вставки, удаления, объединения, замены, вставки или замены и вставки или замены операций в любом сочетании.
* Пакетная операция может иметь операцию извлечения, если она является единственной операцией в пакете.
* У всех сущностей в одной пакетной операции должен быть одинаковый ключ раздела.
* Объем полезных данных пакетной операции ограничен размером 4 МБ.

## <a name="how-to-retrieve-all-entities-in-a-partition"></a>Практическое руководство. Получение всех сущностей в разделе
Чтобы запросить из таблицы сущности раздела, можно использовать **TableQuery**. Вызовите **TableQuery.from**, чтобы создать запрос для определенной таблицы, который возвращает результаты заданного типа. Следующий код задает фильтр для сущностей с ключомраздела "Smith". **TableQuery.generateFilterCondition** — это вспомогательный метод для создания фильтров запросов. Вызовите **where** по ссылке, которую вернул метод **TableQuery.from**, чтобы применить фильтр к запросу. При выполнении запроса с помощью вызова **execute** для объекта **CloudTable** он возвращает **Iterator** с указанным типом результата **CustomerEntity**. Затем можно использовать возвращенное значение **Iterator** в каждом цикле для получения результатов. Этот код выводит на консоль поля каждой сущности в результатах запроса.

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

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for the table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a filter condition where the partition key is "Smith".
    String partitionFilter = TableQuery.generateFilterCondition(
        PARTITION_KEY,
        QueryComparisons.EQUAL,
        "Smith");

    // Specify a partition query, using "Smith" as the partition key filter.
    TableQuery<CustomerEntity> partitionQuery =
        TableQuery.from(CustomerEntity.class)
        .where(partitionFilter);

    // Loop through the results, displaying information about the entity.
    for (CustomerEntity entity : cloudTable.execute(partitionQuery)) {
        System.out.println(entity.getPartitionKey() +
            " " + entity.getRowKey() +
            "\t" + entity.getEmail() +
            "\t" + entity.getPhoneNumber());
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-retrieve-a-range-of-entities-in-a-partition"></a>Практическое руководство. Получение диапазона сущностей в разделе
Если вы не хотите запрашивать все сущности в разделе, можно указать диапазон с помощью операторов сравнения в фильтре. В следующем коде совместно используются два фильтра для получения всех сущностей в разделе "Smith", где ключ строки (имя) начинается с буквы до "E" в алфавите. После чего результаты запроса выводятся на консоль. Если вы используете сущности, добавленные в таблицу во время работы с разделом о пакетной вставке, то на этот раз возвращаются только две сущности (Ben Smith и Denise Smith), а Jeff Smith не выводится.

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

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for the table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a filter condition where the partition key is "Smith".
    String partitionFilter = TableQuery.generateFilterCondition(
        PARTITION_KEY,
        QueryComparisons.EQUAL,
        "Smith");

    // Create a filter condition where the row key is less than the letter "E".
    String rowFilter = TableQuery.generateFilterCondition(
        ROW_KEY,
        QueryComparisons.LESS_THAN,
        "E");

    // Combine the two conditions into a filter expression.
    String combinedFilter = TableQuery.combineFilters(partitionFilter,
        Operators.AND, rowFilter);

    // Specify a range query, using "Smith" as the partition key,
    // with the row key being up to the letter "E".
    TableQuery<CustomerEntity> rangeQuery =
        TableQuery.from(CustomerEntity.class)
        .where(combinedFilter);

    // Loop through the results, displaying information about the entity
    for (CustomerEntity entity : cloudTable.execute(rangeQuery)) {
        System.out.println(entity.getPartitionKey() +
            " " + entity.getRowKey() +
            "\t" + entity.getEmail() +
            "\t" + entity.getPhoneNumber());
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-retrieve-a-single-entity"></a>Практическое руководство. Извлечение одной сущности
Можно написать запрос для получения отдельной сущности. В следующем коде выполняется вызов **TableOperation.retrieve** с параметрами ключа раздела и ключа строки для указания клиента Jeff Smith вместо создания **TableQuery** и применения фильтров с таким же результатом. При выполнении операция извлечения возвращает только одну сущность, а не коллекцию. Метод **getResultAsType** приводит результат к типу назначенной цели — объекту **CustomerEntity**. Если этот тип не совместим с типом, указанным в запросе, возникает исключение. Значение NULL возвращается, если ни одна сущность не подходит по ключам раздела и строки. Указание ключа раздела и ключа строки в запросе — самый быстрый способ извлечь одну сущность из службы таблиц.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for the table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Retrieve the entity with partition key of "Smith" and row key of "Jeff"
    TableOperation retrieveSmithJeff =
        TableOperation.retrieve("Smith", "Jeff", CustomerEntity.class);

    // Submit the operation to the table service and get the specific entity.
    CustomerEntity specificEntity =
        cloudTable.execute(retrieveSmithJeff).getResultAsType();

    // Output the entity.
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
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-modify-an-entity"></a>Практическое руководство. Изменение сущности
Чтобы изменить сущность, извлеките ее из службы таблиц, измените объект сущности и сохраните изменения в службе таблиц с помощью операции замены или объединения. Следующий код изменяет существующий номер телефона клиента. Вместо вызова метода **TableOperation.insert**, который мы осуществляли при вставке, этот код вызывает **TableOperation.replace**. Метод **CloudTableClient.execute** вызывает службу таблиц и заменяет сущность, если только другое приложение не изменило ее с момента извлечения данным приложением. Когда это происходит, возникает исключение, и сущность необходимо получить, изменить и сохранить повторно. Этот оптимистичный шаблон повторения в случае конфликтов широко применяется в системе распределенного хранения.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for the table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Retrieve the entity with partition key of "Smith" and row key of "Jeff".
    TableOperation retrieveSmithJeff =
        TableOperation.retrieve("Smith", "Jeff", CustomerEntity.class);

    // Submit the operation to the table service and get the specific entity.
    CustomerEntity specificEntity =
        cloudTable.execute(retrieveSmithJeff).getResultAsType();

    // Specify a new phone number.
    specificEntity.setPhoneNumber("425-555-0105");

    // Create an operation to replace the entity.
    TableOperation replaceEntity = TableOperation.replace(specificEntity);

    // Submit the operation to the table service.
    cloudTable.execute(replaceEntity);
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-query-a-subset-of-entity-properties"></a>Практическое руководство. Запрос подмножества свойств сущности
Запрос к таблице может получить лишь несколько свойств сущности. Этот метод, который называется "проекцией", снижает потребление пропускной способности и может повысить производительность запросов, особенно для крупных сущностей. Запрос в следующем коде использует метод **select**, чтобы возвратить только адреса электронной почты сущностей в таблице. Результаты проецируются в коллекцию **String** с помощью метода **EntityResolver**, который выполняет преобразование типов сущностей, возвращенных с сервера. Дополнительные сведения о проекции см. в записи блога [Azure Tables: Introducing Upsert and Query Projection][Azure Tables: Introducing Upsert and Query Projection] (Таблицы Azure: введение в Upsert и проекции в запросах). Обратите внимание, что проекция не поддерживается в эмуляторе локального хранилища, поэтому этот код выполняется только при использовании учетной записи хранения в службе таблиц.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for the table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Define a projection query that retrieves only the Email property
    TableQuery<CustomerEntity> projectionQuery =
        TableQuery.from(CustomerEntity.class)
        .select(new String[] {"Email"});

    // Define a Entity resolver to project the entity to the Email value.
    EntityResolver<String> emailResolver = new EntityResolver<String>() {
        @Override
        public String resolve(String PartitionKey, String RowKey, Date timeStamp, HashMap<String, EntityProperty> properties, String etag) {
            return properties.get("Email").getValueAsString();
        }
    };

    // Loop through the results, displaying the Email values.
    for (String projectedString :
        cloudTable.execute(projectionQuery, emailResolver)) {
            System.out.println(projectedString);
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-insert-or-replace-an-entity"></a>Как вставлять и заменять сущности
Часто требуется добавить сущность в таблицу, не зная, присутствует ли она там. Операция вставки или замены позволяет сделать один запрос, который вставит сущность, если она не существует, или заменит существующую сущность. В продолжение материала предыдущих примеров следующий код вставляет или заменяет сущность "Walter Harp". После создания новой сущности этот код вызывает метод **TableOperation.insertOrReplace**. Далее код вызывает метод **execute** объекта **CloudTable** с таблицей, а также табличными операциями вставки или замены в качестве параметров. Чтобы обновить только часть сущности, можно вместо этого использовать метод **TableOperation.insertOrMerge**. Обратите внимание, что операция вставить-или-заменить не поддерживается в эмуляторе локального хранилища, поэтому этот код выполняется только при использовании учетной записи хранения в службе таблиц. Дополнительные сведения об операциях "вставка или замена" и "вставка или объединение" см. в записи блога [Azure Tables: Introducing Upsert and Query Projection][Azure Tables: Introducing Upsert and Query Projection] (Таблицы Azure: введение в Upsert и проекции в запросах).

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for the table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a new customer entity.
    CustomerEntity customer5 = new CustomerEntity("Harp", "Walter");
    customer5.setEmail("Walter@contoso.com");
    customer5.setPhoneNumber("425-555-0106");

    // Create an operation to add the new customer to the people table.
    TableOperation insertCustomer5 = TableOperation.insertOrReplace(customer5);

    // Submit the operation to the table service.
    cloudTable.execute(insertCustomer5);
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-delete-an-entity"></a>Практическое руководство. Удаление сущности
Сущность можно легко удалить после ее получения. После получение сущности вызовите **TableOperation.delete** с удаляемой сущностью. Затем вызовите **execute** объекта **CloudTable**. Следующий код извлекает и удаляет сущность клиента.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for the table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create an operation to retrieve the entity with partition key of "Smith" and row key of "Jeff".
    TableOperation retrieveSmithJeff = TableOperation.retrieve("Smith", "Jeff", CustomerEntity.class);

    // Retrieve the entity with partition key of "Smith" and row key of "Jeff".
    CustomerEntity entitySmithJeff =
        cloudTable.execute(retrieveSmithJeff).getResultAsType();

    // Create an operation to delete the entity.
    TableOperation deleteSmithJeff = TableOperation.delete(entitySmithJeff);

    // Submit the delete operation to the table service.
    cloudTable.execute(deleteSmithJeff);
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-delete-a-table"></a>Практическое руководство. Удаление таблицы
Наконец, следующий код удаляет таблицу из учетной записи хранения. Удаленную таблицу нельзя воссоздать в течение определенного времени после удаления. Этот период обычно составляет менее сорока секунд.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Delete the table and all its data if it exists.
    CloudTable cloudTable = tableClient.getTableReference("people");
    cloudTable.deleteIfExists();
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```
[!INCLUDE [storage-check-out-samples-java](../../includes/storage-check-out-samples-java.md)]

## <a name="next-steps"></a>Дополнительная информация

* [Обозреватель хранилищ Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md) — это бесплатное автономное приложение от корпорации Майкрософт, позволяющее визуализировать данные из службы хранилища Azure на платформе Windows, macOS и Linux.
* [Пакет SDK службы хранилища Azure для Java][Azure Storage SDK for Java]
* [справочника по пакету SDK для клиента службы хранилища Azure][справочника по пакету SDK для клиента службы хранилища Azure]
* [REST API службы хранилища Azure][Azure Storage REST API]
* [Блог рабочей группы службы хранилища Azure][Azure Storage Team Blog]

Дополнительные сведения см. в разделе [Azure for Java developers](/java/azure) (Azure для разработчиков Java).

[Azure SDK for Java]: http://go.microsoft.com/fwlink/?LinkID=525671
[Azure Storage SDK for Java]: https://github.com/azure/azure-storage-java
[Azure Storage SDK for Android]: https://github.com/azure/azure-storage-android
[справочника по пакету SDK для клиента службы хранилища Azure]: http://dl.windowsazure.com/storage/javadoc/
[Azure Storage REST API]: https://msdn.microsoft.com/library/azure/dd179355.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
[Azure Tables: Introducing Upsert and Query Projection]: http://blogs.msdn.com/b/windowsazurestorage/archive/2011/09/15/windows-azure-tables-introducing-upsert-and-query-projection.aspx
