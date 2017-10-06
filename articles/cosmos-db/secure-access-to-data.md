---
title: "aaaLearn как toosecure доступ к toodata в базе данных Azure Cosmos | Документы Microsoft"
description: "Основные понятия управления доступом в Azure Cosmos DB, включая главные ключи, ключи только для чтения, пользователей и разрешения."
services: cosmos-db
author: mimig1
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: 8641225d-e839-4ba6-a6fd-d6314ae3a51c
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/24/2017
ms.author: mimig
ms.openlocfilehash: fef7f8e14b488f6ceab0f2aa279a1e99d4416f08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="securing-access-tooazure-cosmos-db-data"></a>Защита доступа к данным Cosmos DB tooAzure
Это статье представлен обзор защиты доступа toodata, хранящихся в [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).

Azure Cosmos DB использует два типа ключей tooauthenticate пользователей и обеспечивает tooits доступа к данным и ресурсам. 

|Тип ключа|Ресурсы|
|---|---|
|[Главные ключи](#master-keys) |Используются для административных ресурсов: учетных записей базы данных, баз данных, пользователей и разрешений.|
|[Маркеры ресурсов](#resource-tokens)|Используются для ресурсов приложения: коллекций, документов, вложений, хранимых процедур, триггеров и определяемых пользователем функций (UDF).|

<a id="master-keys"></a>

## <a name="master-keys"></a>Главные ключи 

Главные ключи указать все административные ресурсы hello toohello доступа для учетной записи базы данных hello. Главные ключи.  
- Предоставьте доступ tooaccounts, баз данных, пользователей и разрешения. 
- Не может быть toocollections детального доступа используется tooprovide и документы.
- Создаются во время создания hello учетной записи.
- можно создать повторно в любое время.

Каждая учетная запись состоит из двух главных ключей: первичного и вторичного. Hello двух ключей предназначен, чтобы повторно создать или развертывания ключей, содержащий учетную запись tooyour непрерывного доступа и данные. 

В дополнение toohello два главных ключей для учетной записи Cosmos DB hello есть два ключевых только для чтения. Эти разделы доступны только для чтения разрешается только операции чтения hello учетной записи. Ключи только для чтения не предоставляют доступа tooread разрешения ресурсов.

Только для чтения получателя, и главные ключи для чтения и записи могут быть получены и созданы повторно с использованием портала Azure hello. Дополнительные сведения см. в разделе [Просмотр, копирование и повторное создание ключей доступа](manage-account.md#keys).

![Управление доступом (IAM) в hello портал Azure — демонстрации NoSQL безопасности базы данных](./media/secure-access-to-data/nosql-database-security-master-key-portal.png)

Hello процесс смены главного ключа является простым. Перейдите toohello Azure портала tooretrieve вторичного ключа, а затем заменить первичный ключ с помощью вторичного ключа в приложении, а затем повернуть hello первичный ключ в hello портал Azure.

![Смена главного ключа в hello портал Azure — демонстрации NoSQL безопасности базы данных](./media/secure-access-to-data/nosql-database-security-master-key-rotate-workflow.png)

### <a name="code-sample-toouse-a-master-key"></a>Код образца toouse главного ключа

Hello следующем образце кода демонстрируется toouse Cosmos DB DocumentClient учетной записи tooinstantiate конечной точки и главный ключ и создать базу данных. 

```csharp
//Read hello Azure Cosmos DB endpointUrl and authorization keys from config.
//These values are available from hello Azure portal on hello Azure Cosmos DB account blade under "Keys".
//NB > Keep these values in a safe and secure location. Together they provide Administrative access tooyour DocDB account.

private static readonly string endpointUrl = ConfigurationManager.AppSettings["EndPointUrl"];
private static readonly SecureString authorizationKey = ToSecureString(ConfigurationManager.AppSettings["AuthorizationKey"]);

client = new DocumentClient(new Uri(endpointUrl), authorizationKey);

// Create Database
Database database = await client.CreateDatabaseAsync(
    new Database
    {
        Id = databaseName
    });
```

<a id="resource-tokens"></a>

## <a name="resource-tokens"></a>Маркеры ресурсов

Маркеры ресурсов предоставляют доступ toohello ресурсы приложения в базе данных. Маркеры ресурсов.
- Предоставить доступ toospecific коллекции, ключи разделов, документы, вложения, хранимые процедуры, триггеры и определяемые пользователем функции.
- Создаются при [пользователя](#users) предоставляется [разрешений](#permissions) tooa конкретный ресурс.
- создаются повторно, когда в отношении ресурса разрешения выполняется вызов POST, GET или PUT;
- Используйте маркер хэш-ресурса, специально созданный для пользователя hello, ресурсов и разрешений.
- имеют ограничение по времени (настраиваемый срок действия). допустимый интервал времени по умолчанию Hello составляет один час. Время существования маркера, тем не менее, может быть явно указано, копирование tooa не более 5 часов.
- Предоставляют безопасные альтернативные toogiving out hello главного ключа. 
- Включите tooread клиентов, запись и удаление ресурсов в hello учетной записи Cosmos DB toohello разрешения, которые они были предоставлены в соответствии с.

Можно использовать токен ресурсов (создавая Cosmos DB пользователей и разрешения) при необходимости tooprovide tooresources access в DB вашей Cosmos учетной записи клиента tooa, не может быть доверенным главным ключом hello.  

Маркеры ресурсов Cosmos DB являются безопасным вариантом, позволяющий tooread клиентов, запись и удаление ресурсов в вашей учетной записи Cosmos DB toohello разрешения, которые вы предоставили права в соответствии с и без необходимости либо главного или прочитать только ключ.

Ниже приведен шаблон обычно проектирования, при котором маркеры ресурсов может быть запрошенных, созданный и доставляется tooclients:

1. Служба среднего уровня настраивается tooserve фотографий пользователя tooshare мобильного приложения. 
2. Служба среднего уровня Hello обладает hello главный ключ hello Cosmos DB учетной записи.
3. приложение Hello фото устанавливается на мобильных устройствах для конечных пользователей. 
4. При входе в систему приложение hello фото устанавливает hello удостоверение пользователя hello hello промежуточного уровня службы. Этот механизм идентификации проверочной работает исключительно toohello приложения.
5. После установления удостоверение hello hello служба среднего уровня запрашивает разрешения на базе удостоверения hello.
6. Служба среднего уровня Hello отправляет приложение Windows phone маркера задней toohello ресурсов.
7. приложение Hello phone можно будет продолжить toouse hello ресурсов toodirectly токена доступа Cosmos DB ресурсы hello разрешения, определенные маркер ресурса hello и интервала времени hello hello маркером ресурса. 
8. После истечения срока действия маркера ресурсов hello, последующие запросы получают 401 создается исключение.  На этом этапе приложение hello phone повторно устанавливает идентификацию hello и запрашивает новый маркер ресурса.

    ![Рабочий процесс маркеров ресурсов Azure Cosmos DB](./media/secure-access-to-data/resourcekeyworkflow.png)

Создание маркера ресурсов и управления обрабатывается hello Cosmos DB библиотеками native client; Однако при использовании REST должен создать hello заголовки проверки подлинности запроса. Дополнительные сведения о создании заголовки проверки подлинности для REST см. в разделе [управление доступом к ресурсам DB Cosmos](https://docs.microsoft.com/rest/api/documentdb/access-control-on-documentdb-resources) или hello [исходный код для наших SDK](https://github.com/Azure/azure-documentdb-node/blob/master/source/lib/auth.js).

Примером службы среднего уровня toogenerate или посредника маркеры ресурсов см. hello [ResourceTokenBroker приложения](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/xamarin/UserItems/ResourceTokenBroker/ResourceTokenBroker/Controllers).

<a id="users"></a>

## <a name="users"></a>Пользователи
Пользователи Cosmos DB связаны с базой данных Cosmos DB.  Каждая база данных может содержать несколько пользователей Cosmos DB или не содержать ни одного.  Здравствуйте, следующие образце кода показано, как toocreate Cosmos DB пользовательский ресурс.

```csharp
//Create a user.
User docUser = new User
{
    Id = "mobileuser"
};

docUser = await client.CreateUserAsync(UriFactory.CreateDatabaseUri("db"), docUser);
```

> [!NOTE]
> Каждый пользователь Cosmos DB имеет свойство PermissionsLink, которое может быть hello список используемых tooretrieve [разрешений](#permissions) связанное с пользователем hello.
> 
> 

<a id="permissions"></a>

## <a name="permissions"></a>Разрешения
Ресурс разрешения Cosmos DB связан с пользователем Cosmos DB.  Каждый пользователь может иметь несколько разрешений Cosmos DB или не иметь ни одного.  Ресурс разрешение предоставляет доступ tooa маркер безопасности hello потребностей пользователя при попытке tooaccess ресурсов определенного приложения.
Существует два уровня доступа, предоставляемых ресурсом разрешения:

* Все: hello пользователь имеет разрешение на полный доступ на hello ресурсов.
* Ознакомьтесь с разделом hello пользователь может только читать содержимое hello hello ресурса, но не удается выполнить запись, update или delete операции с ресурсом hello.

> [!NOTE]
> В порядке toorun Cosmos DB хранимых процедур hello пользователь должен иметь hello все разрешения на коллекции hello, в какие hello хранимую процедуру будут выполнять.
> 
> 

### <a name="code-sample-toocreate-permission"></a>Разрешение toocreate образец кода

Hello следующем образце кода показано, как toocreate ресурс разрешения чтения hello маркер ресурса для ресурса разрешения hello и связать с hello hello разрешения [пользователя](#users) созданной выше.

```csharp
// Create a permission.
Permission docPermission = new Permission
{
    PermissionMode = PermissionMode.Read,
    ResourceLink = documentCollection.SelfLink,
    Id = "readperm"
};
  
docPermission = await client.CreatePermissionAsync(UriFactory.CreateUserUri("db", "user"), docPermission);
Console.WriteLine(docPermission.Id + " has token of: " + docPermission.Token);
```

При указании ключа секции для коллекции, затем hello разрешения для коллекции, документов и вложения ресурсов также должен включать hello ResourcePartitionKey в дополнение toohello ResourceLink.

### <a name="code-sample-tooread-permissions-for-user"></a>Разрешения для пользователя tooread образец кода

tooeasily получить все разрешения ресурсы, связанные с конкретного пользователя, Cosmos DB делает доступными разрешение перевода для каждого объекта-пользователя.  Hello следующий фрагмент кода показывает способ создания tooretrieve hello разрешение, связанное с пользователем hello выше, составьте список разрешений и создать новый DocumentClient от имени пользователя hello.

```csharp
//Read a permission feed.
FeedResponse<Permission> permFeed = await client.ReadPermissionFeedAsync(
  UriFactory.CreateUserUri("db", "myUser"));
 List<Permission> permList = new List<Permission>();

foreach (Permission perm in permFeed)
{
    permList.Add(perm);
}

DocumentClient userClient = new DocumentClient(new Uri(endpointUrl), permList);
```

## <a name="next-steps"></a>Дальнейшие действия
* toolearn Дополнительные сведения о безопасности Cosmos DB базы данных, в разделе [Cosmos DB: безопасность баз данных](database-security.md).
* в разделе toolearn об управлении ключами master и только для чтения, [как toomanage учетную запись Azure Cosmos DB](manage-account.md#keys).
* tooconstruct Azure Cosmos DB авторизации маркеры, в статье toolearn [управление доступом к ресурсам базы данных Azure Cosmos](https://docs.microsoft.com/rest/api/documentdb/access-control-on-documentdb-resources).
