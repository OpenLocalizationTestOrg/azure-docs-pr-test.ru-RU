---
title: "Как защитить доступ к данным в Azure Cosmos DB | Документация Майкрософт"
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
ms.openlocfilehash: 383e04f91eec2f465b381ce30f2d6d24c488b731
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="securing-access-to-azure-cosmos-db-data"></a><span data-ttu-id="a5527-103">Защита доступа к данным Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="a5527-103">Securing access to Azure Cosmos DB data</span></span>
<span data-ttu-id="a5527-104">В этой статье приведены общие сведения о защите доступа к данным, хранящимся в [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="a5527-104">This article provides an overview of securing access to data stored in [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span></span>

<span data-ttu-id="a5527-105">Для проверки подлинности пользователей и предоставления доступа к своим данным и ресурсам Azure Cosmos DB использует два типа ключей.</span><span class="sxs-lookup"><span data-stu-id="a5527-105">Azure Cosmos DB uses two types of keys to authenticate users and provide access to its data and resources.</span></span> 

|<span data-ttu-id="a5527-106">Тип ключа</span><span class="sxs-lookup"><span data-stu-id="a5527-106">Key type</span></span>|<span data-ttu-id="a5527-107">Ресурсы</span><span class="sxs-lookup"><span data-stu-id="a5527-107">Resources</span></span>|
|---|---|
|[<span data-ttu-id="a5527-108">Главные ключи</span><span class="sxs-lookup"><span data-stu-id="a5527-108">Master keys</span></span>](#master-keys) |<span data-ttu-id="a5527-109">Используются для административных ресурсов: учетных записей базы данных, баз данных, пользователей и разрешений.</span><span class="sxs-lookup"><span data-stu-id="a5527-109">Used for administrative resources: database accounts, databases, users, and permissions</span></span>|
|[<span data-ttu-id="a5527-110">Маркеры ресурсов</span><span class="sxs-lookup"><span data-stu-id="a5527-110">Resource tokens</span></span>](#resource-tokens)|<span data-ttu-id="a5527-111">Используются для ресурсов приложения: коллекций, документов, вложений, хранимых процедур, триггеров и определяемых пользователем функций (UDF).</span><span class="sxs-lookup"><span data-stu-id="a5527-111">Used for application resources: collections, documents, attachments, stored procedures, triggers, and UDFs</span></span>|

<a id="master-keys"></a>

## <a name="master-keys"></a><span data-ttu-id="a5527-112">Главные ключи</span><span class="sxs-lookup"><span data-stu-id="a5527-112">Master keys</span></span> 

<span data-ttu-id="a5527-113">Главные ключи предоставляют доступ ко всем административным ресурсам для учетной записи базы данных.</span><span class="sxs-lookup"><span data-stu-id="a5527-113">Master keys provide access to the all the administrative resources for the database account.</span></span> <span data-ttu-id="a5527-114">Главные ключи.</span><span class="sxs-lookup"><span data-stu-id="a5527-114">Master keys:</span></span>  
- <span data-ttu-id="a5527-115">предоставляют доступ к учетным записям, базам данных, пользователям и разрешениям;</span><span class="sxs-lookup"><span data-stu-id="a5527-115">Provide access to accounts, databases, users, and permissions.</span></span> 
- <span data-ttu-id="a5527-116">не могут использоваться для предоставления детального доступа к коллекциям и документам;</span><span class="sxs-lookup"><span data-stu-id="a5527-116">Cannot be used to provide granular access to collections and documents.</span></span>
- <span data-ttu-id="a5527-117">создаются в процессе создания учетной записи;</span><span class="sxs-lookup"><span data-stu-id="a5527-117">Are created during the creation of an account.</span></span>
- <span data-ttu-id="a5527-118">можно создать повторно в любое время.</span><span class="sxs-lookup"><span data-stu-id="a5527-118">Can be regenerated at any time.</span></span>

<span data-ttu-id="a5527-119">Каждая учетная запись состоит из двух главных ключей: первичного и вторичного.</span><span class="sxs-lookup"><span data-stu-id="a5527-119">Each account consists of two Master keys: a primary key and secondary key.</span></span> <span data-ttu-id="a5527-120">Двойные ключи позволяют повторно создавать или сменять ключи, обеспечивая постоянный доступ к учетной записи и данным.</span><span class="sxs-lookup"><span data-stu-id="a5527-120">The purpose of dual keys is so that you can regenerate, or roll keys, providing continuous access to your account and data.</span></span> 

<span data-ttu-id="a5527-121">Помимо двух главных ключей в учетной записи Cosmos DB существует еще два ключа только для чтения.</span><span class="sxs-lookup"><span data-stu-id="a5527-121">In addition to the two master keys for the Cosmos DB account, there are two read-only keys.</span></span> <span data-ttu-id="a5527-122">Эти ключи разрешают только операции чтения в учетной записи.</span><span class="sxs-lookup"><span data-stu-id="a5527-122">These read-only keys only allow read operations on the account.</span></span> <span data-ttu-id="a5527-123">Ключи только для чтения не предоставляют доступ к ресурсам разрешений на чтение.</span><span class="sxs-lookup"><span data-stu-id="a5527-123">Read-only keys do not provide access to read permissions resources.</span></span>

<span data-ttu-id="a5527-124">Главные ключи (первичные, вторичные, с доступом только для чтения и с доступом для чтения и записи) можно получить и повторно создать с помощью портала Azure.</span><span class="sxs-lookup"><span data-stu-id="a5527-124">Primary, secondary, read only, and read-write master keys can be retrieved and regenerated using the Azure portal.</span></span> <span data-ttu-id="a5527-125">Дополнительные сведения см. в разделе [Просмотр, копирование и повторное создание ключей доступа](manage-account.md#keys).</span><span class="sxs-lookup"><span data-stu-id="a5527-125">For instructions, see [View, copy, and regenerate access keys](manage-account.md#keys).</span></span>

![Управление доступом (IAM) на портале Azure: демонстрация безопасности базы данных NoSQL](./media/secure-access-to-data/nosql-database-security-master-key-portal.png)

<span data-ttu-id="a5527-127">Процесс ротации главного ключа прост.</span><span class="sxs-lookup"><span data-stu-id="a5527-127">The process of rotating your master key is simple.</span></span> <span data-ttu-id="a5527-128">Перейдите на портал Azure, чтобы получить вторичный ключ, затем замените первичный ключ вторичным ключом в приложении, а затем смените первичный ключ на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="a5527-128">Navigate to the Azure portal to retrieve your secondary key, then replace your primary key with your secondary key in your application, then rotate the primary key in the Azure portal.</span></span>

![Ротация главного ключа на портале Azure: демонстрация безопасности базы данных NoSQL](./media/secure-access-to-data/nosql-database-security-master-key-rotate-workflow.png)

### <a name="code-sample-to-use-a-master-key"></a><span data-ttu-id="a5527-130">Пример кода для использования главного ключа</span><span class="sxs-lookup"><span data-stu-id="a5527-130">Code sample to use a master key</span></span>

<span data-ttu-id="a5527-131">В следующем примере кода показано, как использовать конечную точку учетной записи Cosmos DB и главный ключ для создания экземпляра DocumentClient и построения базы данных.</span><span class="sxs-lookup"><span data-stu-id="a5527-131">The following code sample illustrates how to use a Cosmos DB account endpoint and master key to instantiate a DocumentClient and create a database.</span></span> 

```csharp
//Read the Azure Cosmos DB endpointUrl and authorization keys from config.
//These values are available from the Azure portal on the Azure Cosmos DB account blade under "Keys".
//NB > Keep these values in a safe and secure location. Together they provide Administrative access to your DocDB account.

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

## <a name="resource-tokens"></a><span data-ttu-id="a5527-132">Маркеры ресурсов</span><span class="sxs-lookup"><span data-stu-id="a5527-132">Resource tokens</span></span>

<span data-ttu-id="a5527-133">Маркеры ресурсов предоставляют доступ к ресурсам приложения в базе данных.</span><span class="sxs-lookup"><span data-stu-id="a5527-133">Resource tokens provide access to the application resources within a database.</span></span> <span data-ttu-id="a5527-134">Маркеры ресурсов.</span><span class="sxs-lookup"><span data-stu-id="a5527-134">Resource tokens:</span></span>
- <span data-ttu-id="a5527-135">предоставляют доступ к определенным коллекциям, ключам секции, документам, вложениям, хранимым процедурам, триггерам и определяемым пользователем функциям (UDF);</span><span class="sxs-lookup"><span data-stu-id="a5527-135">Provide access to specific collections, partition keys, documents, attachments, stored procedures, triggers, and UDFs.</span></span>
- <span data-ttu-id="a5527-136">создаются, когда [пользователю](#users) предоставляются [разрешения](#permissions) на доступ к определенному ресурсу;</span><span class="sxs-lookup"><span data-stu-id="a5527-136">Are created when a [user](#users) is granted [permissions](#permissions) to a specific resource.</span></span>
- <span data-ttu-id="a5527-137">создаются повторно, когда в отношении ресурса разрешения выполняется вызов POST, GET или PUT;</span><span class="sxs-lookup"><span data-stu-id="a5527-137">Are recreated when a permission resource is acted upon on by POST, GET, or PUT call.</span></span>
- <span data-ttu-id="a5527-138">используют хэш, который маркер ресурса специально создал для пользователя, ресурса и разрешения;</span><span class="sxs-lookup"><span data-stu-id="a5527-138">Use a hash resource token specifically constructed for the user, resource, and permission.</span></span>
- <span data-ttu-id="a5527-139">имеют ограничение по времени (настраиваемый срок действия).</span><span class="sxs-lookup"><span data-stu-id="a5527-139">Are time bound with a customizable validity period.</span></span> <span data-ttu-id="a5527-140">Допустимый интервал времени по умолчанию составляет один час.</span><span class="sxs-lookup"><span data-stu-id="a5527-140">The default valid timespan is one hour.</span></span> <span data-ttu-id="a5527-141">Однако продолжительность действия маркера можно задать явным образом. Ее значение не должно превышать пять часов;</span><span class="sxs-lookup"><span data-stu-id="a5527-141">Token lifetime, however, may be explicitly specified, up to a maximum of five hours.</span></span>
- <span data-ttu-id="a5527-142">обеспечивают безопасную альтернативу выдаче главного ключа;</span><span class="sxs-lookup"><span data-stu-id="a5527-142">Provide a safe alternative to giving out the master key.</span></span> 
- <span data-ttu-id="a5527-143">позволяют клиентам читать, записывать и удалять ресурсы в учетной записи Cosmos DB в соответствии с предоставленными им разрешениями.</span><span class="sxs-lookup"><span data-stu-id="a5527-143">Enable clients to read, write, and delete resources in the Cosmos DB account according to the permissions they've been granted.</span></span>

<span data-ttu-id="a5527-144">Маркер ресурсов можно использовать (создавая пользователей и разрешения Cosmos DB), если доступ к ресурсам в учетной записи Cosmos DB требуется предоставить клиенту, которому нельзя доверять.</span><span class="sxs-lookup"><span data-stu-id="a5527-144">You can use a resource token (by creating Cosmos DB users and permissions) when you want to provide access to resources in your Cosmos DB account to a client that cannot be trusted with the master key.</span></span>  

<span data-ttu-id="a5527-145">Маркеры ресурсов Cosmos DB — это безопасное альтернативное решение, которое позволяет клиентам читать, записывать и удалять ресурсы в учетной записи Cosmos DB согласно предоставленным разрешениям и без необходимости использовать главный ключ или ключ только для чтения.</span><span class="sxs-lookup"><span data-stu-id="a5527-145">Cosmos DB resource tokens provide a safe alternative that enables clients to read, write, and delete resources in your Cosmos DB account according to the permissions you've granted, and without need for either a master or read only key.</span></span>

<span data-ttu-id="a5527-146">Ниже приведена стандартная схема запроса, создания и отправки маркеров ресурсов клиентам.</span><span class="sxs-lookup"><span data-stu-id="a5527-146">Here is a typical design pattern whereby resource tokens may be requested, generated, and delivered to clients:</span></span>

1. <span data-ttu-id="a5527-147">Служба среднего уровня настроена для обслуживания мобильного приложения по обмену фотографиями.</span><span class="sxs-lookup"><span data-stu-id="a5527-147">A mid-tier service is set up to serve a mobile application to share user photos.</span></span> 
2. <span data-ttu-id="a5527-148">Служба среднего уровня обрабатывает главный ключ учетной записи Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="a5527-148">The mid-tier service possesses the master key of the Cosmos DB account.</span></span>
3. <span data-ttu-id="a5527-149">Приложение по обмену фотографиями устанавливается на мобильных устройствах конечных пользователей.</span><span class="sxs-lookup"><span data-stu-id="a5527-149">The photo app is installed on end-user mobile devices.</span></span> 
4. <span data-ttu-id="a5527-150">При входе в систему приложение для обмена фотографиями идентифицирует пользователя службы.</span><span class="sxs-lookup"><span data-stu-id="a5527-150">On login, the photo app establishes the identity of the user with the mid-tier service.</span></span> <span data-ttu-id="a5527-151">Механизм установления личности пользователя реализуется исключительно в приложении.</span><span class="sxs-lookup"><span data-stu-id="a5527-151">This mechanism of identity establishment is purely up to the application.</span></span>
5. <span data-ttu-id="a5527-152">После установления личности служба среднего уровня запрашивает разрешения на основе удостоверения.</span><span class="sxs-lookup"><span data-stu-id="a5527-152">Once the identity is established, the mid-tier service requests permissions based on the identity.</span></span>
6. <span data-ttu-id="a5527-153">Служба среднего уровня отправляет маркер ресурса обратно в приложение для телефона.</span><span class="sxs-lookup"><span data-stu-id="a5527-153">The mid-tier service sends a resource token back to the phone app.</span></span>
7. <span data-ttu-id="a5527-154">Приложение может по-прежнему использовать маркер ресурса для прямого доступа к ресурсам Cosmos DB с разрешениями, определенными маркером, и в течение интервала времени, разрешенного этим маркером.</span><span class="sxs-lookup"><span data-stu-id="a5527-154">The phone app can continue to use the resource token to directly access Cosmos DB resources with the permissions defined by the resource token and for the interval allowed by the resource token.</span></span> 
8. <span data-ttu-id="a5527-155">По истечении срока действия маркера ресурса последующие запросы получают исключение: 401 — не авторизовано.</span><span class="sxs-lookup"><span data-stu-id="a5527-155">When the resource token expires, subsequent requests receive a 401 unauthorized exception.</span></span>  <span data-ttu-id="a5527-156">На этом этапе приложение для телефона повторно установит личность и запросит новый маркер ресурса.</span><span class="sxs-lookup"><span data-stu-id="a5527-156">At this point, the phone app re-establishes the identity and requests a new resource token.</span></span>

    ![Рабочий процесс маркеров ресурсов Azure Cosmos DB](./media/secure-access-to-data/resourcekeyworkflow.png)

<span data-ttu-id="a5527-158">Создание маркеров ресурсов и управление ими осуществляется собственными клиентскими библиотеками Cosmos DB. Однако если используется REST, то необходимо создать заголовки запросов и проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="a5527-158">Resource token generation and management is handled by the native Cosmos DB client libraries; however, if you use REST you must construct the request/authentication headers.</span></span> <span data-ttu-id="a5527-159">Дополнительные сведения о создании заголовков проверки подлинности для REST см. в статье [Access control in the DocumentDB API](https://docs.microsoft.com/rest/api/documentdb/access-control-on-documentdb-resources) (Управление доступом в API DocumentDB) или в [репозитории исходного кода для наших пакетов SDK](https://github.com/Azure/azure-documentdb-node/blob/master/source/lib/auth.js).</span><span class="sxs-lookup"><span data-stu-id="a5527-159">For more information on creating authentication headers for REST, see [Access Control on Cosmos DB Resources](https://docs.microsoft.com/rest/api/documentdb/access-control-on-documentdb-resources) or the [source code for our SDKs](https://github.com/Azure/azure-documentdb-node/blob/master/source/lib/auth.js).</span></span>

<span data-ttu-id="a5527-160">Пример службы среднего уровня, используемой для создания маркеров ресурсов или в качестве брокера, см. в [репозитории приложения ResourceTokenBroker](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/xamarin/UserItems/ResourceTokenBroker/ResourceTokenBroker/Controllers).</span><span class="sxs-lookup"><span data-stu-id="a5527-160">For an example of a middle tier service used to generate or broker resource tokens, see the [ResourceTokenBroker app](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/xamarin/UserItems/ResourceTokenBroker/ResourceTokenBroker/Controllers).</span></span>

<a id="users"></a>

## <a name="users"></a><span data-ttu-id="a5527-161">Пользователи</span><span class="sxs-lookup"><span data-stu-id="a5527-161">Users</span></span>
<span data-ttu-id="a5527-162">Пользователи Cosmos DB связаны с базой данных Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="a5527-162">Cosmos DB users are associated with a Cosmos DB database.</span></span>  <span data-ttu-id="a5527-163">Каждая база данных может содержать несколько пользователей Cosmos DB или не содержать ни одного.</span><span class="sxs-lookup"><span data-stu-id="a5527-163">Each database can contain zero or more Cosmos DB users.</span></span>  <span data-ttu-id="a5527-164">В следующем примере кода показано, как создать ресурс пользователя Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="a5527-164">The following code sample shows how to create a Cosmos DB user resource.</span></span>

```csharp
//Create a user.
User docUser = new User
{
    Id = "mobileuser"
};

docUser = await client.CreateUserAsync(UriFactory.CreateDatabaseUri("db"), docUser);
```

> [!NOTE]
> <span data-ttu-id="a5527-165">Каждый пользователь Cosmos DB обладает свойством PermissionsLink, которое можно использовать для получения списка [разрешений](#permissions), связанных с этим пользователем.</span><span class="sxs-lookup"><span data-stu-id="a5527-165">Each Cosmos DB user has a PermissionsLink property that can be used to retrieve the list of [permissions](#permissions) associated with the user.</span></span>
> 
> 

<a id="permissions"></a>

## <a name="permissions"></a><span data-ttu-id="a5527-166">Разрешения</span><span class="sxs-lookup"><span data-stu-id="a5527-166">Permissions</span></span>
<span data-ttu-id="a5527-167">Ресурс разрешения Cosmos DB связан с пользователем Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="a5527-167">A Cosmos DB permission resource is associated with a Cosmos DB user.</span></span>  <span data-ttu-id="a5527-168">Каждый пользователь может иметь несколько разрешений Cosmos DB или не иметь ни одного.</span><span class="sxs-lookup"><span data-stu-id="a5527-168">Each user may contain zero or more Cosmos DB permissions.</span></span>  <span data-ttu-id="a5527-169">Ресурс разрешения предоставляет доступ к маркеру безопасности, необходимому пользователю при попытке доступа к конкретному ресурсу приложения.</span><span class="sxs-lookup"><span data-stu-id="a5527-169">A permission resource provides access to a security token that the user needs when trying to access a specific application resource.</span></span>
<span data-ttu-id="a5527-170">Существует два уровня доступа, предоставляемых ресурсом разрешения:</span><span class="sxs-lookup"><span data-stu-id="a5527-170">There are two available access levels that may be provided by a permission resource:</span></span>

* <span data-ttu-id="a5527-171">Все. Пользователь имеет полный набор разрешений для ресурса.</span><span class="sxs-lookup"><span data-stu-id="a5527-171">All: The user has full permission on the resource.</span></span>
* <span data-ttu-id="a5527-172">Чтение. Пользователь может только считывать содержимое ресурса, но не может выполнять на ресурсе операции записи, обновления или удаления.</span><span class="sxs-lookup"><span data-stu-id="a5527-172">Read: The user can only read the contents of the resource but cannot perform write, update, or delete operations on the resource.</span></span>

> [!NOTE]
> <span data-ttu-id="a5527-173">Для выполнения хранимых процедур Cosmos DB пользователь должен иметь полные разрешения на использование коллекции, в которой будут выполняться хранимые процедуры.</span><span class="sxs-lookup"><span data-stu-id="a5527-173">In order to run Cosmos DB stored procedures the user must have the All permission on the collection in which the stored procedure will be run.</span></span>
> 
> 

### <a name="code-sample-to-create-permission"></a><span data-ttu-id="a5527-174">Пример кода для создания разрешения</span><span class="sxs-lookup"><span data-stu-id="a5527-174">Code sample to create permission</span></span>

<span data-ttu-id="a5527-175">В следующем примере кода показано, как создать ресурс разрешения, прочесть его маркер и связать разрешения с созданным выше [пользователем](#users).</span><span class="sxs-lookup"><span data-stu-id="a5527-175">The following code sample shows how to create a permission resource, read the resource token of the permission resource, and associate the permissions with the [user](#users) created above.</span></span>

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

<span data-ttu-id="a5527-176">Если вы указали ключ секции для коллекции, то разрешение для ресурсов коллекции, документа и вложения также должно включать ResourcePartitionKey наряду с ResourceLink.</span><span class="sxs-lookup"><span data-stu-id="a5527-176">If you have specified a partition key for your collection, then the permission for collection, document, and attachment resources must also include the ResourcePartitionKey in addition to the ResourceLink.</span></span>

### <a name="code-sample-to-read-permissions-for-user"></a><span data-ttu-id="a5527-177">Пример кода для чтения разрешений пользователя</span><span class="sxs-lookup"><span data-stu-id="a5527-177">Code sample to read permissions for user</span></span>

<span data-ttu-id="a5527-178">Чтобы получить все ресурсы разрешений, связанные с конкретным пользователем, Cosmos DB предоставляет каждому объекту пользователя доступ к каналу разрешений.</span><span class="sxs-lookup"><span data-stu-id="a5527-178">To easily obtain all permission resources associated with a particular user, Cosmos DB makes available a permission feed for each user object.</span></span>  <span data-ttu-id="a5527-179">В следующем фрагменте кода показано, как получить разрешение, связанное с созданным выше пользователем, сформировать список разрешений и создать новый DocumentClient от имени пользователя.</span><span class="sxs-lookup"><span data-stu-id="a5527-179">The following code snippet shows how to retrieve the permission associated with the user created above, construct a permission list, and instantiate a new DocumentClient on behalf of the user.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="a5527-180">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a5527-180">Next steps</span></span>
* <span data-ttu-id="a5527-181">Дополнительные сведения о безопасности базы данных Cosmos DB см. в статье [Безопасность базы данных в Azure Cosmos DB](database-security.md).</span><span class="sxs-lookup"><span data-stu-id="a5527-181">To learn more about Cosmos DB database security, see [Cosmos DB: Database security](database-security.md).</span></span>
* <span data-ttu-id="a5527-182">Сведения об управлении главными ключами и ключами только для чтения см. в разделе [Просмотр, копирование и повторное создание ключей доступа](manage-account.md#keys).</span><span class="sxs-lookup"><span data-stu-id="a5527-182">To learn about managing master and read-only keys, see [How to manage an Azure Cosmos DB account](manage-account.md#keys).</span></span>
* <span data-ttu-id="a5527-183">Сведения о создании маркеров проверки подлинности Azure Cosmos DB см. в статье [Access control in the DocumentDB API](https://docs.microsoft.com/rest/api/documentdb/access-control-on-documentdb-resources) (Управление доступом в API DocumentDB).</span><span class="sxs-lookup"><span data-stu-id="a5527-183">To learn how to construct Azure Cosmos DB authorization tokens, see [Access Control on Azure Cosmos DB Resources](https://docs.microsoft.com/rest/api/documentdb/access-control-on-documentdb-resources).</span></span>
