---
title: "Azure Cosmos DB: Разработку с использованием hello API таблиц в .NET | Документы Microsoft"
description: "Узнайте, как toodevelop с API Azure Cosmos DB таблицы, с помощью .NET"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 4b22cb49-8ea2-483d-bc95-1172cd009498
ms.service: cosmos-db
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/10/2017
ms.author: arramac
ms.custom: mvc
ms.openlocfilehash: 70c6985a1dffdbcdb07e377f8ad10355bb97712a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-develop-with-hello-table-api-in-net"></a>Azure Cosmos DB: Разработку с использованием hello API таблиц в .NET

Azure Cosmos DB — это глобально распределенная многомодельная служба базы данных Майкрософт. Вы можете быстро создать и запрашивать документа, ключ значение и graph баз данных, все из которых преимущества глобального распространения hello и возможности горизонтального масштабирования в основе hello Azure Cosmos БД.

В этом учебнике hello следующие задачи: 

> [!div class="checklist"] 
> * создание учетной записи Azure Cosmos DB; 
> * Включить функции в файле app.config hello 
> * Создание таблицы с помощью hello [API таблиц](table-introduction.md) (Предварительная версия)
> * Добавьте таблицу tooa сущности 
> * Вставка пакета сущностей 
> * Извлечение одной сущности 
> * запрос сущностей с использованием автоматического вторичного индексирования; 
> * Замена сущности 
> * Удаление сущности 
> * Удаление таблицы
 
## <a name="tables-in-azure-cosmos-db"></a>Таблицы в базе данных Azure Cosmos DB 

Azure Cosmos DB предоставляет hello [API таблиц](table-introduction.md) (Предварительный просмотр) для приложений, требующих хранилищу ключей и значений с помощью конструктора без схемы. [Хранилище таблиц Azure](../storage/common/storage-introduction.md) пакеты SDK и API-интерфейс REST может быть используется toowork с Azure Cosmos DB. Можно использовать таблицы Azure Cosmos DB toocreate с высокой пропускной способности. Кроме того, она поддерживает оптимизированные для пропускной способности таблицы, которые неофициально называются таблицами класса "Премиум" и сейчас доступны в общедоступной предварительной версии. 

Вы можете продолжить toouse хранилища Azure Table для таблиц с высокой хранилища и более низкие требования к пропускной способности. Azure Cosmos DB будет внедрить поддержку в будущем обновлении таблицами, оптимизированными для хранения данных и существующих и новых таблиц Azure, учетные записи хранения будут легко обновляется tooAzure Cosmos DB.

При использовании хранилища таблиц Azure в настоящее время можно получить следующие преимущества со Предварительный просмотр «premium таблицы» hello hello.

- поддержка готового к использованию [глобального распределения](distribute-data-globally.md) со множественной адресацией, а также с [ручной и автоматической отработкой отказа](regional-failover.md);
- поддержка автоматического схемонезависимого индексирования данных для всех свойств ("вторичные индексы") и быстрого выполнения запросов; 
- поддержка [независимого масштабирования хранилища и пропускной способности](partition-data.md) в любом количестве регионов;
- Поддержка [выделенной пропускной способности на таблицу](request-units.md) может масштабироваться от сотен toomillions запросов в секунду
- Поддержка [пять уровней пройтись согласованности](consistency-levels.md) tootrade выключения доступность, задержка и согласованности в зависимости от потребностей приложения
- 99,99% доступности в пределах одного региона и возможность tooadd дополнительные области для повышения доступности и [отрасли комплексное соглашений об уровне обслуживания](https://azure.microsoft.com/support/legal/sla/cosmos-db/) на общей доступности
- Работа с hello существующего хранилища Azure .NET SDK и ни одно приложение tooyour изменения кода

Во время предварительного просмотра hello Azure Cosmos DB поддерживает hello таблицы API, с помощью hello .NET SDK. Вы можете загрузить hello [предварительной версии хранилища Azure SDK](https://aka.ms/premiumtablenuget) из NuGet, который имеет hello же классах и подписях методов как hello [пакет SDK хранилища Azure](https://www.nuget.org/packages/WindowsAzure.Storage), но также можно подключить Cosmos DB tooAzure учетные записи, используя hello Таблица API.

toolearn Дополнительные сведения о сложных задач хранилища таблиц Azure, см.:

* [Введение tooAzure Cosmos DB: API таблиц](table-introduction.md)
* Здравствуйте, таблица службы справочной документации для получения подробной информации о доступных API-интерфейсы [клиентская библиотека хранилища для Справочник по .NET](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)

### <a name="about-this-tutorial"></a>О данном учебнике
Этот учебник для разработчиков, знакомых с hello пакета SDK службы хранилища таблиц Azure и хотел toouse hello расширенные функции доступны использует базу данных Azure Cosmos. Он основан на [Приступая к работе с хранилищем таблиц Azure, с помощью .NET](table-storage-how-to-use-dotnet.md) и показано, как tootake преимущества дополнительных возможностей, таких как вторичные индексы, пропускная способность и многоадресными. Мы рассмотрим, как toouse hello Azure toocreate портала учетной записи Azure Cosmos DB и затем постройте и разверните приложение таблицы. В этом руководстве также представлены примеры .NET для создания и удаления таблиц, а также для вставки, обновления, удаления и запроса данных таблицы. 

Если у вас еще нет Visual Studio 2017 г. установлен, можно загрузить и использовать hello **свободного** [2017 г. Visual Studio Community Edition](https://www.visualstudio.com/downloads/). Убедитесь, что включен **разработки Azure** во время установки Visual Studio hello.

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a>Создание учетной записи базы данных

Давайте начнем с создания учетной записи Azure Cosmos DB в hello портал Azure.  

> [!TIP]
> * Уже есть учетная запись Azure Cosmos DB? Если Да, пропустить слишком[Настройка решения Visual Studio](#SetupVS).
> * У вас была учетная запись Azure DocumentDB? Если таким образом, учетной записи теперь учетную запись Azure Cosmos DB и можно сразу перейти слишком[Настройка решения Visual Studio](#SetupVS).  
> * Если вы используете hello Azure Cosmos DB эмулятор, выполните действия hello в [DB эмулятор Azure Cosmos](local-emulator.md) toosetup hello эмулятора и пропускать слишком[настроить решение Visual Studio](#SetupVS).
<!---Loc Comment: Please, check link [Set up your Visual Studio solution] since it's not redirecting tooany location.---> 
>
>

[!INCLUDE [cosmosdb-create-dbaccount-table](../../includes/cosmos-db-create-dbaccount-table.md)] 

## <a name="clone-hello-sample-application"></a>Пример приложения hello клонирования

Теперь давайте клонировать приложении таблицы из github, задайте строку подключения hello и запустите его.

1. Откройте окно терминала git, таких как git bash и `cd` tooa рабочий каталог.  

2. Выполнения hello следующая команда репозитории примеров tooclone hello. 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-table-dotnet-getting-started
    ```

3. Затем откройте файл решения hello в Visual Studio.

## <a name="update-your-connection-string"></a>Обновление строки подключения

Теперь вернитесь toohello Azure портала tooget данные строки подключения и скопируйте его в приложение hello.

1. В hello [портал Azure](http://portal.azure.com/), в вашей Azure Cosmos DB учетной записи, в hello навигации слева щелкните **ключей**и нажмите кнопку **чтения и записи ключей**. Вы используете кнопки копия hello hello правой части экрана toocopy hello hello-строка подключения в файл app.config hello в следующем шаге hello.

2. В Visual Studio откройте файл app.config hello. 

3. Скопируйте значение URI с портала hello (с использованием "Копировать" hello ") и сделать его hello значение hello ключа учетной записи-в файле app.config. Используйте имя учетной записи hello, созданного ранее для имени учетной записи в файл app.config.
  
```
<add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key;TableEndpoint=https://account-name.documents.azure.com" />
```

> [!NOTE]
> toouse приложение, используя стандартные табличного хранилища Azure, требуется строка подключения toochange hello в `app.config file`. Имя учетной записи используйте hello как имя учетной записи таблицы и ключ как хранилище Azure в первичный ключ. <br>
>`<add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key;EndpointSuffix=core.windows.net" />`
> 
>

## <a name="build-and-deploy-hello-app"></a>Построение и развертывание приложения hello
1. В Visual Studio щелкните правой кнопкой мыши проект hello в **обозревателе решений** и нажмите кнопку **управление пакетами NuGet**. 

2. В hello NuGet **Обзор** введите ***WindowsAzure.Storage PremiumTable***. Установите флажок **Включить предварительные выпуски**.

3. На основе результатов hello установить hello **WindowsAzure.Storage PremiumTable** и выберите "сборка" Предварительный просмотр hello `0.0.1-preview`. Это действие устанавливает пакет хранилища таблиц Azure hello и все зависимости.

4. Нажмите сочетание клавиш CTRL + F5 toorun приложения hello. 

Теперь можно вернуться tooData обозревателя и разделе запроса, изменения и работать с данными таблицы. 

> [!NOTE]
> toouse это приложение с эмулятором DB Cosmos Azure, вы просто требуется строка подключения toochange hello в `app.config file`. Используйте hello ниже значения для эмулятора. <br>
>`<add key="StorageConnectionString" value=DefaultEndpointsProtocol=https;AccountName=localhost;AccountKey=<insertkey>==;TableEndpoint=https://localhost -->`
> 
>

## <a name="azure-cosmos-db-capabilities"></a>Возможности базы данных Azure Cosmos DB
Azure Cosmos DB поддерживает ряд возможностей, которые не доступны в API-Интерфейс хранилища Azure Table hello. Hello новые функциональные возможности можно включить, используя следующие hello `appSettings` значения конфигурации. Не удалось ввести любые новые подписи или перегрузки toohello просмотра пакет SDK хранилища Azure. Это позволяет tooconnect tooboth standard и premium таблиц и работа с другими службами хранилища Azure, такими как большие двоичные объекты и очереди. 


| Ключ | Описание |
| --- | --- |
| TableConnectionMode  | База данных Azure Cosmos DB поддерживает два режима подключения. В `Gateway` режиме, запросы всегда осуществляются toohello Azure Cosmos DB шлюз, который перенаправляет его toohello соответствующие секции данных. В `Direct` режим подключения hello клиент выберет hello сопоставление toopartitions таблиц и запросов, выполненных непосредственно для секции данных. Мы рекомендуем `Direct`, по умолчанию hello.  |
| TableConnectionProtocol | База данных Azure Cosmos DB поддерживает два протокола подключения: `Https` и `Tcp`. `Tcp`по умолчанию hello и рекомендуется, так как он является облегченной. |
| TablePreferredLocations | Разделенный запятыми список предпочтительных расположений (множественная адресация) для операций чтения. Каждую учетную запись базы данных Azure Cosmos DB можно связать з разным числом регионов (от одного до более тридцати). Каждый экземпляр клиента можно указать подмножество этих областей в порядке hello предпочтительный для операций чтения с небольшой задержкой. Hello областей должны иметь имена с помощью их [отображаемые имена](https://msdn.microsoft.com/library/azure/gg441293.aspx), например `West US`. Дополнительные сведения см. в статье [How to setup Azure Cosmos DB global distribution using the Table API](tutorial-global-distribution-table.md) (Как настроить глобальное распределение Azure Cosmos DB с помощью API таблицы).
| TableConsistencyLevel | Вы можете изменить показатели доступности, задержки и согласованности, выбрав один из пяти следующих четко определенных уровней согласованности: `Strong`, `Session`, `Bounded-Staleness`, `ConsistentPrefix` и `Eventual`. Значение по умолчанию — `Session`. Выбор уровня согласованности Hello оказывает влияние значительного увеличения производительности в нескольких регионах настроек. Дополнительные сведения см. в статье [Настраиваемые уровни согласованности данных в DocumentDB](consistency-levels.md). |
| TableThroughput | Зарезервированную полосу пропускания для таблицы hello, выраженный в единицах запроса (RU) в секунду. Каждая таблица может поддерживать сотни миллионов единиц запросов в секунду. Дополнительные сведения см. в статье [Единицы запросов в DocumentDB](request-units.md). Значение по умолчанию — `400`. |
| TableIndexingPolicy | Согласованное и автоматическое вторичное индексирование всех столбцов в таблицах. | JSON строки соответствующих toohello спецификация политики индексирования. В разделе [политики индексирования](indexing-policies.md) toosee изменение индексирования политики tooinclude и исключения определенных столбцов. | Автоматическое индексирование всех свойств (хэш-индексация для строк и диапазонная индексация для чисел). |
| TableQueryMaxItemCount | Настройте hello максимальное количество возвращаемых элементов для запроса таблицы в рамках одного цикла обработки. Значение по умолчанию — `-1`, что позволяет динамически определять значение hello во время выполнения DB Cosmos Azure. |
| TableQueryEnableScan | Если запрос hello невозможно использовать индекс hello любой фильтр, запустите его все равно посредством проверки. Значение по умолчанию — `false`.|
| TableQueryMaxDegreeOfParallelism | степень параллелизма для выполнения запроса между разделами Hello. `0`не выполняется параллельно с без предварительной загрузки, `1` последовательный с предварительное и выше значениями hello коэффициент увеличения параллелизма. Значение по умолчанию — `-1`, что позволяет динамически определять значение hello во время выполнения DB Cosmos Azure. |

значение по умолчанию hello toochange, откройте hello `app.config` файл из обозревателя решений в Visual Studio. Добавить содержимое hello hello `<appSettings>` элемент, показанный ниже. Замените `account-name` с именем hello вашей учетной записи хранилища и `account-key` с помощью ключа доступа учетной записи. 

```xml
<configuration>
    <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5.2" />
    </startup>
    <appSettings>
      <!-- Client options -->
      <add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key; TableEndpoint=https://account-name.documents.azure.com" />
      <add key="TableConnectionMode" value="Direct"/>
      <add key="TableConnectionProtocol" value="Tcp"/>
      <add key="TablePreferredLocations" value="East US, West US, North Europe"/>
      <add key="TableConsistencyLevel" value="Eventual"/>

      <!--Table creation options -->
      <add key="TableThroughput" value="700"/>
      <add key="TableIndexingPolicy" value="{""indexingMode"": ""Consistent""}"/>

      <!-- Table query options -->
      <add key="TableQueryMaxItemCount" value="-1"/>
      <add key="TableQueryEnableScan" value="false"/>
      <add key="TableQueryMaxDegreeOfParallelism" value="-1"/>
      <add key="TableQueryContinuationTokenLimitInKb" value="16"/>
            
    </appSettings>
</configuration>
```

Убедитесь, что происходит в приложение hello быстро ознакомиться. Откройте hello `Program.cs` файла и найдите следующие строки кода создать hello ресурсами таблиц. 

## <a name="create-hello-table-client"></a>Создание клиента hello таблиц
Можно инициализировать `CloudTableClient` tooconnect toohello таблицы, учетной записи.

```csharp
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
```
Этот клиент инициализируется с помощью hello `TableConnectionMode`, `TableConnectionProtocol`, `TableConsistencyLevel`, и `TablePreferredLocations` значений конфигурации, если указан в параметрах приложения hello.
    
## <a name="create-a-table"></a>Создание таблицы
Затем создайте таблицу, используя `CloudTable`. Таблицы в базе данных Azure Cosmos можно масштабировать независимо друг от друга с точки зрения хранилища и пропускной способности и секционирование обрабатывается автоматически службой hello. База данных Azure Cosmos DB поддерживает таблицы с фиксированным и неограниченным размером. Дополнительные сведения см. в статье [Секционирование и масштабирование в базе данных Azure Cosmos DB](partition-data.md). 

```csharp
CloudTable table = tableClient.GetTableReference("people");

table.CreateIfNotExists();
```

Создание таблиц существенно отличается. База данных Azure Cosmos DB резервирует пропускную способность, а в службе хранилища Azure к транзакциям применяется модель с оплатой по мере использования. Hello резервирования модель имеет два основных преимущества:

* Пропускная способность выделяется или резервируется, поэтому вам не нужно выполнять регулирование, если частота запросов на уровне или ниже подготовленной пропускной способности.
* Дополнительные модели резервирования Hello [экономически эффективные для нагрузок пропускной способности](key-value-store-cost.md)

Можно настроить пропускную способность по умолчанию hello, настроив параметр hello для `TableThroughput` с точки зрения RU (запроса ед.) в секунду. 

Чтение сущности 1 КБ нормализуется как 1 RU и других операций, нормализованное tooa фиксированное значение единиц Запросов в зависимости от их потребления ЦП, памяти и операций ввода-ВЫВОДА. Дополнительные сведения о [единицах запроса в Azure Cosmos DB](request-units.md).

> [!NOTE]
> Хранилище таблиц SDK в настоящее время не поддерживает изменение пропускной способности, можно изменить пропускной способности hello мгновенно в любой момент, с помощью hello портал Azure или Azure CLI.

Далее мы Пройдите hello простой чтения и записи (CRUD) с помощью пакета SDK службы хранилища Azure Table hello. В этом руководстве показаны такие преимущества базы данных Azure Cosmos DB, как прогнозируемые задержки операций, длительностью менее 10 секунд, и быстрое выполнение запросов.

## <a name="add-an-entity-tooa-table"></a>Добавьте таблицу tooa сущности
Сущности в хранилище таблиц Azure расширять hello `TableEntity` класса и должен иметь `PartitionKey` и `RowKey` свойства. Ниже приведен пример определения сущности клиента.

```csharp
public class CustomerEntity : TableEntity
{
    public CustomerEntity(string lastName, string firstName)
    {
        this.PartitionKey = lastName;
        this.RowKey = firstName;
    }

    public CustomerEntity() { }

    public string Email { get; set; }

    public string PhoneNumber { get; set; }
}
```

Hello, следующий фрагмент кода показывает, как tooinsert сущность с hello хранилища Azure SDK. Azure Cosmos DB предназначен для высокоскоростной любых объемов гарантированный Здравствуй, мир!.

Завершить запись < 15 мс на p99 и ms ~ 6 на p50 для приложений, работающих hello же регионе, что учетная запись Azure Cosmos DB hello. И это время учетные записи для hello фактов, которая записывает подтверждения задней toohello клиента только после их синхронно реплицируются, надежно зафиксированы, и индексируется все содержимое.

Hello API таблиц для Azure Cosmos DB находится в предварительной версии. На этапе общей доступности hello p99 задержки гарантии, поддерживаемых соглашений об уровне обслуживания, как и другие API-интерфейсы DB Cosmos для Azure. 

```csharp
// Create a new customer entity.
CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
customer1.Email = "Walter@contoso.com";
customer1.PhoneNumber = "425-555-0101";

// Create hello TableOperation object that inserts hello customer entity.
TableOperation insertOperation = TableOperation.Insert(customer1);

// Execute hello insert operation.
table.Execute(insertOperation);
```

## <a name="insert-a-batch-of-entities"></a>Вставка пакета сущностей
Azure табличного хранилища поддерживаются пакетной операции API, позволяющий объединить обновления, удаления и вставки в hello одной операции в одном пакете. Azure Cosmos DB имеет некоторые ограничения hello на API пакета hello как хранилище таблиц Azure. Например, можно выполнять несколько операций чтения в пакете, можно выполнять несколько операций записи toohello одной сущности в пакете, и нет ограничений на 100 операций в пакете. 

```csharp
// Create hello batch operation.
TableBatchOperation batchOperation = new TableBatchOperation();

// Create a customer entity and add it toohello table.
CustomerEntity customer1 = new CustomerEntity("Smith", "Jeff");
customer1.Email = "Jeff@contoso.com";
customer1.PhoneNumber = "425-555-0104";

// Create another customer entity and add it toohello table.
CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
customer2.Email = "Ben@contoso.com";
customer2.PhoneNumber = "425-555-0102";

// Add both customer entities toohello batch insert operation.
batchOperation.Insert(customer1);
batchOperation.Insert(customer2);

// Execute hello batch operation.
table.ExecuteBatch(batchOperation);
```
## <a name="retrieve-a-single-entity"></a>Извлечение одной сущности
Извлекает (получает) в Azure Cosmos DB полный < 10 мс на p99 и около 1 мс на p50 в hello же регионе Azure. Можно добавить столько tooyour областей учетной записи для операций чтения с небольшой задержкой, а также развернуть tooread приложений из своей локальной области («многосетевой»), задав `TablePreferredLocations`. 

Можно получить единственную сущность, используя следующий фрагмент кода hello:

```csharp
// Create a retrieve operation that takes a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute hello retrieve operation.
TableResult retrievedResult = table.Execute(retrieveOperation);
```
> [!TIP]
> Дополнительные сведения об API-интерфейсах множественной адресации см. в статье [How to setup Azure Cosmos DB global distribution using the Table API](tutorial-global-distribution-table.md) (Как настроить глобальное распределение Azure Cosmos DB с помощью API таблицы).
>

## <a name="query-entities-using-automatic-secondary-indexes"></a>Запрос сущностей с использованием автоматического вторичного индексирования
Таблицы можно выполнять запросы hello `TableQuery` класса. База данных Azure Cosmos DB содержит ядро СУБД, оптимизированное для операций записи, которое автоматически индексирует все столбцы в таблице. Индексирование в базе данных Azure Cosmos — независимые tooschema. Таким образом даже если схема различны строк или со временем развивается hello схемы, он автоматически индексируется. Поскольку Azure Cosmos DB поддерживает автоматическое вторичные индексы, запросы к любому свойству можно использовать индекс hello и эффективно обслуживать.

```csharp
CloudTable table = tableClient.GetTableReference("people");

// Filter against a property that's not partition key or row key
TableQuery<CustomerEntity> emailQuery = new TableQuery<CustomerEntity>().Where(
    TableQuery.GenerateFilterCondition("Email", QueryComparisons.Equal, "Ben@contoso.com"));

foreach (CustomerEntity entity in table.ExecuteQuery(emailQuery))
{
    Console.WriteLine("{0}, {1}\t{2}\t{3}", entity.PartitionKey, entity.RowKey,
        entity.Email, entity.PhoneNumber);
}
```

Во время предварительного просмотра Azure Cosmos DB поддерживает hello же запрос, функциональные возможности, что хранилище таблиц Azure для hello API таблиц. Кроме того, эта база данных поддерживает сортировку, выполнение статистических вычислений, геопространственные запросы, иерархию и множество встроенных функций. Дополнительные функциональные возможности Hello будет предоставляться в hello таблицы API в будущих версиях. Общие сведения об этих возможностях см. в статье [SQL-запросы и синтаксис SQL в DocumentDB](documentdb-sql-query.md). 

## <a name="replace-an-entity"></a>Замена сущности
tooupdate сущности, получить его из службы таблиц hello, изменить объект сущности hello и сохранять изменения hello обратно toohello службы таблиц. Hello следующий код позволяет изменить номер телефона существующего клиента. 

```csharp
TableOperation updateOperation = TableOperation.Replace(updateEntity);
table.Execute(updateOperation);
```
Аналогичным образом можно выполнить операцию `InsertOrMerge` или `Merge`.  

## <a name="delete-an-entity"></a>Удаление сущности
Можно легко удалить сущность, после его получения с помощью hello же шаблон, показанный для обновления сущности. Привет, следующий код извлекает и удаляет сущность «клиент».

```csharp
TableOperation deleteOperation = TableOperation.Delete(deleteEntity);
table.Execute(deleteOperation);
```

## <a name="delete-a-table"></a>Удаление таблицы
Наконец hello, следующий пример кода удаляет таблицу из учетной записи хранения. Вы можете удалить и воссоздать таблицу с помощью базы данных Azure Cosmos DB.

```csharp
CloudTable table = tableClient.GetTableReference("people");
table.DeleteIfExists();
```

## <a name="clean-up-resources"></a>Очистка ресурсов 

Если вы не будете toocontinue toouse это приложение, используйте следующие шаги toodelete все ресурсы, созданные этого учебника в hello портал Azure hello.   

1. Hello слева в меню портала Azure hello, пункт **групп ресурсов** и щелкните имя hello созданного ресурса hello.  
2. На странице группы ресурсов, нажмите кнопку **удаление**, введите имя hello toodelete ресурсов hello в hello текстовое поле и нажмите кнопку **удалить**. 

## <a name="next-steps"></a>Дальнейшие действия

В этом учебнике мы узнали, как tooget работы с Azure Cosmos DB на hello API таблиц и вы сделали hello следующее: 

> [!div class="checklist"] 
> * создали учетную запись Azure Cosmos DB; 
> * Функциональность включена в файле app.config hello 
> * создали таблицу; 
> * Добавлена таблица tooa сущности 
> * вставили пакет сущностей; 
> * извлекли одну сущность; 
> * запросили сущности в процессе автоматического вторичного индексирования; 
> * заменили сущность; 
> * удалили сущность; 
> * удалили таблицу.  

Теперь можно выполнить следующее руководство toohello и Дополнительные сведения о запросах к таблице данных. 

> [!div class="nextstepaction"]
> [Запрос с hello API таблиц](tutorial-query-table.md)
