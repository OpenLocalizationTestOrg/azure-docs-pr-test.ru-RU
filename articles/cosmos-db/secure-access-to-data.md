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
# <a name="securing-access-tooazure-cosmos-db-data"></a><span data-ttu-id="b243f-103">Защита доступа к данным Cosmos DB tooAzure</span><span class="sxs-lookup"><span data-stu-id="b243f-103">Securing access tooAzure Cosmos DB data</span></span>
<span data-ttu-id="b243f-104">Это статье представлен обзор защиты доступа toodata, хранящихся в [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="b243f-104">This article provides an overview of securing access toodata stored in [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span></span>

<span data-ttu-id="b243f-105">Azure Cosmos DB использует два типа ключей tooauthenticate пользователей и обеспечивает tooits доступа к данным и ресурсам.</span><span class="sxs-lookup"><span data-stu-id="b243f-105">Azure Cosmos DB uses two types of keys tooauthenticate users and provide access tooits data and resources.</span></span> 

|<span data-ttu-id="b243f-106">Тип ключа</span><span class="sxs-lookup"><span data-stu-id="b243f-106">Key type</span></span>|<span data-ttu-id="b243f-107">Ресурсы</span><span class="sxs-lookup"><span data-stu-id="b243f-107">Resources</span></span>|
|---|---|
|[<span data-ttu-id="b243f-108">Главные ключи</span><span class="sxs-lookup"><span data-stu-id="b243f-108">Master keys</span></span>](#master-keys) |<span data-ttu-id="b243f-109">Используются для административных ресурсов: учетных записей базы данных, баз данных, пользователей и разрешений.</span><span class="sxs-lookup"><span data-stu-id="b243f-109">Used for administrative resources: database accounts, databases, users, and permissions</span></span>|
|[<span data-ttu-id="b243f-110">Маркеры ресурсов</span><span class="sxs-lookup"><span data-stu-id="b243f-110">Resource tokens</span></span>](#resource-tokens)|<span data-ttu-id="b243f-111">Используются для ресурсов приложения: коллекций, документов, вложений, хранимых процедур, триггеров и определяемых пользователем функций (UDF).</span><span class="sxs-lookup"><span data-stu-id="b243f-111">Used for application resources: collections, documents, attachments, stored procedures, triggers, and UDFs</span></span>|

<a id="master-keys"></a>

## <a name="master-keys"></a><span data-ttu-id="b243f-112">Главные ключи</span><span class="sxs-lookup"><span data-stu-id="b243f-112">Master keys</span></span> 

<span data-ttu-id="b243f-113">Главные ключи указать все административные ресурсы hello toohello доступа для учетной записи базы данных hello.</span><span class="sxs-lookup"><span data-stu-id="b243f-113">Master keys provide access toohello all hello administrative resources for hello database account.</span></span> <span data-ttu-id="b243f-114">Главные ключи.</span><span class="sxs-lookup"><span data-stu-id="b243f-114">Master keys:</span></span>  
- <span data-ttu-id="b243f-115">Предоставьте доступ tooaccounts, баз данных, пользователей и разрешения.</span><span class="sxs-lookup"><span data-stu-id="b243f-115">Provide access tooaccounts, databases, users, and permissions.</span></span> 
- <span data-ttu-id="b243f-116">Не может быть toocollections детального доступа используется tooprovide и документы.</span><span class="sxs-lookup"><span data-stu-id="b243f-116">Cannot be used tooprovide granular access toocollections and documents.</span></span>
- <span data-ttu-id="b243f-117">Создаются во время создания hello учетной записи.</span><span class="sxs-lookup"><span data-stu-id="b243f-117">Are created during hello creation of an account.</span></span>
- <span data-ttu-id="b243f-118">можно создать повторно в любое время.</span><span class="sxs-lookup"><span data-stu-id="b243f-118">Can be regenerated at any time.</span></span>

<span data-ttu-id="b243f-119">Каждая учетная запись состоит из двух главных ключей: первичного и вторичного.</span><span class="sxs-lookup"><span data-stu-id="b243f-119">Each account consists of two Master keys: a primary key and secondary key.</span></span> <span data-ttu-id="b243f-120">Hello двух ключей предназначен, чтобы повторно создать или развертывания ключей, содержащий учетную запись tooyour непрерывного доступа и данные.</span><span class="sxs-lookup"><span data-stu-id="b243f-120">hello purpose of dual keys is so that you can regenerate, or roll keys, providing continuous access tooyour account and data.</span></span> 

<span data-ttu-id="b243f-121">В дополнение toohello два главных ключей для учетной записи Cosmos DB hello есть два ключевых только для чтения.</span><span class="sxs-lookup"><span data-stu-id="b243f-121">In addition toohello two master keys for hello Cosmos DB account, there are two read-only keys.</span></span> <span data-ttu-id="b243f-122">Эти разделы доступны только для чтения разрешается только операции чтения hello учетной записи.</span><span class="sxs-lookup"><span data-stu-id="b243f-122">These read-only keys only allow read operations on hello account.</span></span> <span data-ttu-id="b243f-123">Ключи только для чтения не предоставляют доступа tooread разрешения ресурсов.</span><span class="sxs-lookup"><span data-stu-id="b243f-123">Read-only keys do not provide access tooread permissions resources.</span></span>

<span data-ttu-id="b243f-124">Только для чтения получателя, и главные ключи для чтения и записи могут быть получены и созданы повторно с использованием портала Azure hello.</span><span class="sxs-lookup"><span data-stu-id="b243f-124">Primary, secondary, read only, and read-write master keys can be retrieved and regenerated using hello Azure portal.</span></span> <span data-ttu-id="b243f-125">Дополнительные сведения см. в разделе [Просмотр, копирование и повторное создание ключей доступа](manage-account.md#keys).</span><span class="sxs-lookup"><span data-stu-id="b243f-125">For instructions, see [View, copy, and regenerate access keys](manage-account.md#keys).</span></span>

![Управление доступом (IAM) в hello портал Azure — демонстрации NoSQL безопасности базы данных](./media/secure-access-to-data/nosql-database-security-master-key-portal.png)

<span data-ttu-id="b243f-127">Hello процесс смены главного ключа является простым.</span><span class="sxs-lookup"><span data-stu-id="b243f-127">hello process of rotating your master key is simple.</span></span> <span data-ttu-id="b243f-128">Перейдите toohello Azure портала tooretrieve вторичного ключа, а затем заменить первичный ключ с помощью вторичного ключа в приложении, а затем повернуть hello первичный ключ в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="b243f-128">Navigate toohello Azure portal tooretrieve your secondary key, then replace your primary key with your secondary key in your application, then rotate hello primary key in hello Azure portal.</span></span>

![Смена главного ключа в hello портал Azure — демонстрации NoSQL безопасности базы данных](./media/secure-access-to-data/nosql-database-security-master-key-rotate-workflow.png)

### <a name="code-sample-toouse-a-master-key"></a><span data-ttu-id="b243f-130">Код образца toouse главного ключа</span><span class="sxs-lookup"><span data-stu-id="b243f-130">Code sample toouse a master key</span></span>

<span data-ttu-id="b243f-131">Hello следующем образце кода демонстрируется toouse Cosmos DB DocumentClient учетной записи tooinstantiate конечной точки и главный ключ и создать базу данных.</span><span class="sxs-lookup"><span data-stu-id="b243f-131">hello following code sample illustrates how toouse a Cosmos DB account endpoint and master key tooinstantiate a DocumentClient and create a database.</span></span> 

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

## <a name="resource-tokens"></a><span data-ttu-id="b243f-132">Маркеры ресурсов</span><span class="sxs-lookup"><span data-stu-id="b243f-132">Resource tokens</span></span>

<span data-ttu-id="b243f-133">Маркеры ресурсов предоставляют доступ toohello ресурсы приложения в базе данных.</span><span class="sxs-lookup"><span data-stu-id="b243f-133">Resource tokens provide access toohello application resources within a database.</span></span> <span data-ttu-id="b243f-134">Маркеры ресурсов.</span><span class="sxs-lookup"><span data-stu-id="b243f-134">Resource tokens:</span></span>
- <span data-ttu-id="b243f-135">Предоставить доступ toospecific коллекции, ключи разделов, документы, вложения, хранимые процедуры, триггеры и определяемые пользователем функции.</span><span class="sxs-lookup"><span data-stu-id="b243f-135">Provide access toospecific collections, partition keys, documents, attachments, stored procedures, triggers, and UDFs.</span></span>
- <span data-ttu-id="b243f-136">Создаются при [пользователя](#users) предоставляется [разрешений](#permissions) tooa конкретный ресурс.</span><span class="sxs-lookup"><span data-stu-id="b243f-136">Are created when a [user](#users) is granted [permissions](#permissions) tooa specific resource.</span></span>
- <span data-ttu-id="b243f-137">создаются повторно, когда в отношении ресурса разрешения выполняется вызов POST, GET или PUT;</span><span class="sxs-lookup"><span data-stu-id="b243f-137">Are recreated when a permission resource is acted upon on by POST, GET, or PUT call.</span></span>
- <span data-ttu-id="b243f-138">Используйте маркер хэш-ресурса, специально созданный для пользователя hello, ресурсов и разрешений.</span><span class="sxs-lookup"><span data-stu-id="b243f-138">Use a hash resource token specifically constructed for hello user, resource, and permission.</span></span>
- <span data-ttu-id="b243f-139">имеют ограничение по времени (настраиваемый срок действия).</span><span class="sxs-lookup"><span data-stu-id="b243f-139">Are time bound with a customizable validity period.</span></span> <span data-ttu-id="b243f-140">допустимый интервал времени по умолчанию Hello составляет один час.</span><span class="sxs-lookup"><span data-stu-id="b243f-140">hello default valid timespan is one hour.</span></span> <span data-ttu-id="b243f-141">Время существования маркера, тем не менее, может быть явно указано, копирование tooa не более 5 часов.</span><span class="sxs-lookup"><span data-stu-id="b243f-141">Token lifetime, however, may be explicitly specified, up tooa maximum of five hours.</span></span>
- <span data-ttu-id="b243f-142">Предоставляют безопасные альтернативные toogiving out hello главного ключа.</span><span class="sxs-lookup"><span data-stu-id="b243f-142">Provide a safe alternative toogiving out hello master key.</span></span> 
- <span data-ttu-id="b243f-143">Включите tooread клиентов, запись и удаление ресурсов в hello учетной записи Cosmos DB toohello разрешения, которые они были предоставлены в соответствии с.</span><span class="sxs-lookup"><span data-stu-id="b243f-143">Enable clients tooread, write, and delete resources in hello Cosmos DB account according toohello permissions they've been granted.</span></span>

<span data-ttu-id="b243f-144">Можно использовать токен ресурсов (создавая Cosmos DB пользователей и разрешения) при необходимости tooprovide tooresources access в DB вашей Cosmos учетной записи клиента tooa, не может быть доверенным главным ключом hello.</span><span class="sxs-lookup"><span data-stu-id="b243f-144">You can use a resource token (by creating Cosmos DB users and permissions) when you want tooprovide access tooresources in your Cosmos DB account tooa client that cannot be trusted with hello master key.</span></span>  

<span data-ttu-id="b243f-145">Маркеры ресурсов Cosmos DB являются безопасным вариантом, позволяющий tooread клиентов, запись и удаление ресурсов в вашей учетной записи Cosmos DB toohello разрешения, которые вы предоставили права в соответствии с и без необходимости либо главного или прочитать только ключ.</span><span class="sxs-lookup"><span data-stu-id="b243f-145">Cosmos DB resource tokens provide a safe alternative that enables clients tooread, write, and delete resources in your Cosmos DB account according toohello permissions you've granted, and without need for either a master or read only key.</span></span>

<span data-ttu-id="b243f-146">Ниже приведен шаблон обычно проектирования, при котором маркеры ресурсов может быть запрошенных, созданный и доставляется tooclients:</span><span class="sxs-lookup"><span data-stu-id="b243f-146">Here is a typical design pattern whereby resource tokens may be requested, generated, and delivered tooclients:</span></span>

1. <span data-ttu-id="b243f-147">Служба среднего уровня настраивается tooserve фотографий пользователя tooshare мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="b243f-147">A mid-tier service is set up tooserve a mobile application tooshare user photos.</span></span> 
2. <span data-ttu-id="b243f-148">Служба среднего уровня Hello обладает hello главный ключ hello Cosmos DB учетной записи.</span><span class="sxs-lookup"><span data-stu-id="b243f-148">hello mid-tier service possesses hello master key of hello Cosmos DB account.</span></span>
3. <span data-ttu-id="b243f-149">приложение Hello фото устанавливается на мобильных устройствах для конечных пользователей.</span><span class="sxs-lookup"><span data-stu-id="b243f-149">hello photo app is installed on end-user mobile devices.</span></span> 
4. <span data-ttu-id="b243f-150">При входе в систему приложение hello фото устанавливает hello удостоверение пользователя hello hello промежуточного уровня службы.</span><span class="sxs-lookup"><span data-stu-id="b243f-150">On login, hello photo app establishes hello identity of hello user with hello mid-tier service.</span></span> <span data-ttu-id="b243f-151">Этот механизм идентификации проверочной работает исключительно toohello приложения.</span><span class="sxs-lookup"><span data-stu-id="b243f-151">This mechanism of identity establishment is purely up toohello application.</span></span>
5. <span data-ttu-id="b243f-152">После установления удостоверение hello hello служба среднего уровня запрашивает разрешения на базе удостоверения hello.</span><span class="sxs-lookup"><span data-stu-id="b243f-152">Once hello identity is established, hello mid-tier service requests permissions based on hello identity.</span></span>
6. <span data-ttu-id="b243f-153">Служба среднего уровня Hello отправляет приложение Windows phone маркера задней toohello ресурсов.</span><span class="sxs-lookup"><span data-stu-id="b243f-153">hello mid-tier service sends a resource token back toohello phone app.</span></span>
7. <span data-ttu-id="b243f-154">приложение Hello phone можно будет продолжить toouse hello ресурсов toodirectly токена доступа Cosmos DB ресурсы hello разрешения, определенные маркер ресурса hello и интервала времени hello hello маркером ресурса.</span><span class="sxs-lookup"><span data-stu-id="b243f-154">hello phone app can continue toouse hello resource token toodirectly access Cosmos DB resources with hello permissions defined by hello resource token and for hello interval allowed by hello resource token.</span></span> 
8. <span data-ttu-id="b243f-155">После истечения срока действия маркера ресурсов hello, последующие запросы получают 401 создается исключение.</span><span class="sxs-lookup"><span data-stu-id="b243f-155">When hello resource token expires, subsequent requests receive a 401 unauthorized exception.</span></span>  <span data-ttu-id="b243f-156">На этом этапе приложение hello phone повторно устанавливает идентификацию hello и запрашивает новый маркер ресурса.</span><span class="sxs-lookup"><span data-stu-id="b243f-156">At this point, hello phone app re-establishes hello identity and requests a new resource token.</span></span>

    ![Рабочий процесс маркеров ресурсов Azure Cosmos DB](./media/secure-access-to-data/resourcekeyworkflow.png)

<span data-ttu-id="b243f-158">Создание маркера ресурсов и управления обрабатывается hello Cosmos DB библиотеками native client; Однако при использовании REST должен создать hello заголовки проверки подлинности запроса.</span><span class="sxs-lookup"><span data-stu-id="b243f-158">Resource token generation and management is handled by hello native Cosmos DB client libraries; however, if you use REST you must construct hello request/authentication headers.</span></span> <span data-ttu-id="b243f-159">Дополнительные сведения о создании заголовки проверки подлинности для REST см. в разделе [управление доступом к ресурсам DB Cosmos](https://docs.microsoft.com/rest/api/documentdb/access-control-on-documentdb-resources) или hello [исходный код для наших SDK](https://github.com/Azure/azure-documentdb-node/blob/master/source/lib/auth.js).</span><span class="sxs-lookup"><span data-stu-id="b243f-159">For more information on creating authentication headers for REST, see [Access Control on Cosmos DB Resources](https://docs.microsoft.com/rest/api/documentdb/access-control-on-documentdb-resources) or hello [source code for our SDKs](https://github.com/Azure/azure-documentdb-node/blob/master/source/lib/auth.js).</span></span>

<span data-ttu-id="b243f-160">Примером службы среднего уровня toogenerate или посредника маркеры ресурсов см. hello [ResourceTokenBroker приложения](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/xamarin/UserItems/ResourceTokenBroker/ResourceTokenBroker/Controllers).</span><span class="sxs-lookup"><span data-stu-id="b243f-160">For an example of a middle tier service used toogenerate or broker resource tokens, see hello [ResourceTokenBroker app](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/xamarin/UserItems/ResourceTokenBroker/ResourceTokenBroker/Controllers).</span></span>

<a id="users"></a>

## <a name="users"></a><span data-ttu-id="b243f-161">Пользователи</span><span class="sxs-lookup"><span data-stu-id="b243f-161">Users</span></span>
<span data-ttu-id="b243f-162">Пользователи Cosmos DB связаны с базой данных Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="b243f-162">Cosmos DB users are associated with a Cosmos DB database.</span></span>  <span data-ttu-id="b243f-163">Каждая база данных может содержать несколько пользователей Cosmos DB или не содержать ни одного.</span><span class="sxs-lookup"><span data-stu-id="b243f-163">Each database can contain zero or more Cosmos DB users.</span></span>  <span data-ttu-id="b243f-164">Здравствуйте, следующие образце кода показано, как toocreate Cosmos DB пользовательский ресурс.</span><span class="sxs-lookup"><span data-stu-id="b243f-164">hello following code sample shows how toocreate a Cosmos DB user resource.</span></span>

```csharp
//Create a user.
User docUser = new User
{
    Id = "mobileuser"
};

docUser = await client.CreateUserAsync(UriFactory.CreateDatabaseUri("db"), docUser);
```

> [!NOTE]
> <span data-ttu-id="b243f-165">Каждый пользователь Cosmos DB имеет свойство PermissionsLink, которое может быть hello список используемых tooretrieve [разрешений](#permissions) связанное с пользователем hello.</span><span class="sxs-lookup"><span data-stu-id="b243f-165">Each Cosmos DB user has a PermissionsLink property that can be used tooretrieve hello list of [permissions](#permissions) associated with hello user.</span></span>
> 
> 

<a id="permissions"></a>

## <a name="permissions"></a><span data-ttu-id="b243f-166">Разрешения</span><span class="sxs-lookup"><span data-stu-id="b243f-166">Permissions</span></span>
<span data-ttu-id="b243f-167">Ресурс разрешения Cosmos DB связан с пользователем Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="b243f-167">A Cosmos DB permission resource is associated with a Cosmos DB user.</span></span>  <span data-ttu-id="b243f-168">Каждый пользователь может иметь несколько разрешений Cosmos DB или не иметь ни одного.</span><span class="sxs-lookup"><span data-stu-id="b243f-168">Each user may contain zero or more Cosmos DB permissions.</span></span>  <span data-ttu-id="b243f-169">Ресурс разрешение предоставляет доступ tooa маркер безопасности hello потребностей пользователя при попытке tooaccess ресурсов определенного приложения.</span><span class="sxs-lookup"><span data-stu-id="b243f-169">A permission resource provides access tooa security token that hello user needs when trying tooaccess a specific application resource.</span></span>
<span data-ttu-id="b243f-170">Существует два уровня доступа, предоставляемых ресурсом разрешения:</span><span class="sxs-lookup"><span data-stu-id="b243f-170">There are two available access levels that may be provided by a permission resource:</span></span>

* <span data-ttu-id="b243f-171">Все: hello пользователь имеет разрешение на полный доступ на hello ресурсов.</span><span class="sxs-lookup"><span data-stu-id="b243f-171">All: hello user has full permission on hello resource.</span></span>
* <span data-ttu-id="b243f-172">Ознакомьтесь с разделом hello пользователь может только читать содержимое hello hello ресурса, но не удается выполнить запись, update или delete операции с ресурсом hello.</span><span class="sxs-lookup"><span data-stu-id="b243f-172">Read: hello user can only read hello contents of hello resource but cannot perform write, update, or delete operations on hello resource.</span></span>

> [!NOTE]
> <span data-ttu-id="b243f-173">В порядке toorun Cosmos DB хранимых процедур hello пользователь должен иметь hello все разрешения на коллекции hello, в какие hello хранимую процедуру будут выполнять.</span><span class="sxs-lookup"><span data-stu-id="b243f-173">In order toorun Cosmos DB stored procedures hello user must have hello All permission on hello collection in which hello stored procedure will be run.</span></span>
> 
> 

### <a name="code-sample-toocreate-permission"></a><span data-ttu-id="b243f-174">Разрешение toocreate образец кода</span><span class="sxs-lookup"><span data-stu-id="b243f-174">Code sample toocreate permission</span></span>

<span data-ttu-id="b243f-175">Hello следующем образце кода показано, как toocreate ресурс разрешения чтения hello маркер ресурса для ресурса разрешения hello и связать с hello hello разрешения [пользователя](#users) созданной выше.</span><span class="sxs-lookup"><span data-stu-id="b243f-175">hello following code sample shows how toocreate a permission resource, read hello resource token of hello permission resource, and associate hello permissions with hello [user](#users) created above.</span></span>

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

<span data-ttu-id="b243f-176">При указании ключа секции для коллекции, затем hello разрешения для коллекции, документов и вложения ресурсов также должен включать hello ResourcePartitionKey в дополнение toohello ResourceLink.</span><span class="sxs-lookup"><span data-stu-id="b243f-176">If you have specified a partition key for your collection, then hello permission for collection, document, and attachment resources must also include hello ResourcePartitionKey in addition toohello ResourceLink.</span></span>

### <a name="code-sample-tooread-permissions-for-user"></a><span data-ttu-id="b243f-177">Разрешения для пользователя tooread образец кода</span><span class="sxs-lookup"><span data-stu-id="b243f-177">Code sample tooread permissions for user</span></span>

<span data-ttu-id="b243f-178">tooeasily получить все разрешения ресурсы, связанные с конкретного пользователя, Cosmos DB делает доступными разрешение перевода для каждого объекта-пользователя.</span><span class="sxs-lookup"><span data-stu-id="b243f-178">tooeasily obtain all permission resources associated with a particular user, Cosmos DB makes available a permission feed for each user object.</span></span>  <span data-ttu-id="b243f-179">Hello следующий фрагмент кода показывает способ создания tooretrieve hello разрешение, связанное с пользователем hello выше, составьте список разрешений и создать новый DocumentClient от имени пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="b243f-179">hello following code snippet shows how tooretrieve hello permission associated with hello user created above, construct a permission list, and instantiate a new DocumentClient on behalf of hello user.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="b243f-180">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b243f-180">Next steps</span></span>
* <span data-ttu-id="b243f-181">toolearn Дополнительные сведения о безопасности Cosmos DB базы данных, в разделе [Cosmos DB: безопасность баз данных](database-security.md).</span><span class="sxs-lookup"><span data-stu-id="b243f-181">toolearn more about Cosmos DB database security, see [Cosmos DB: Database security](database-security.md).</span></span>
* <span data-ttu-id="b243f-182">в разделе toolearn об управлении ключами master и только для чтения, [как toomanage учетную запись Azure Cosmos DB](manage-account.md#keys).</span><span class="sxs-lookup"><span data-stu-id="b243f-182">toolearn about managing master and read-only keys, see [How toomanage an Azure Cosmos DB account](manage-account.md#keys).</span></span>
* <span data-ttu-id="b243f-183">tooconstruct Azure Cosmos DB авторизации маркеры, в статье toolearn [управление доступом к ресурсам базы данных Azure Cosmos](https://docs.microsoft.com/rest/api/documentdb/access-control-on-documentdb-resources).</span><span class="sxs-lookup"><span data-stu-id="b243f-183">toolearn how tooconstruct Azure Cosmos DB authorization tokens, see [Access Control on Azure Cosmos DB Resources](https://docs.microsoft.com/rest/api/documentdb/access-control-on-documentdb-resources).</span></span>
