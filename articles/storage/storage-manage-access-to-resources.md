---
title: "aaaEnable открытый доступ чтения для контейнеров и больших двоичных объектов в хранилище больших двоичных объектов Azure | Документы Microsoft"
description: "Узнайте, как toomake контейнеры и большие двоичные объекты доступны для анонимного доступа и как tooaccess их программно."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: a2cffee6-3224-4f2a-8183-66ca23b2d2d7
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: marsma
ms.openlocfilehash: 0675b5dc4d32a3a0a34376ae4c049542b07ba03a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-anonymous-read-access-toocontainers-and-blobs"></a><span data-ttu-id="96f1c-103">Управление toocontainers анонимный доступ для чтения и больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="96f1c-103">Manage anonymous read access toocontainers and blobs</span></span>
<span data-ttu-id="96f1c-104">Можно включить анонимные, открытый доступ на чтение tooa контейнера и BLOB-объектов в хранилище больших двоичных объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="96f1c-104">You can enable anonymous, public read access tooa container and its blobs in Azure Blob storage.</span></span> <span data-ttu-id="96f1c-105">Таким образом, вы можете предоставить доступ только для чтения toothese ресурсы без предоставления ключа учетной записи и без необходимости подписанного URL-адреса (SAS).</span><span class="sxs-lookup"><span data-stu-id="96f1c-105">By doing so, you can grant read-only access toothese resources without sharing your account key, and without requiring a shared access signature (SAS).</span></span>

<span data-ttu-id="96f1c-106">Общий доступ на чтение лучше всего подходит для сценариев, место определенных tooalways большие двоичные объекты будут доступны для анонимного доступа на чтение.</span><span class="sxs-lookup"><span data-stu-id="96f1c-106">Public read access is best for scenarios where you want certain blobs tooalways be available for anonymous read access.</span></span> <span data-ttu-id="96f1c-107">Для более точного контроля можно создать подписанный URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="96f1c-107">For more fine-grained control, you can create a shared access signature.</span></span> <span data-ttu-id="96f1c-108">Подписанные URL-адреса позволяют tooprovide ограниченный доступ при помощи различные разрешения для конкретного периода времени.</span><span class="sxs-lookup"><span data-stu-id="96f1c-108">Shared access signatures enable you tooprovide restricted access using different permissions, for a specific time period.</span></span> <span data-ttu-id="96f1c-109">Дополнительные сведения о создании подписанных URL-адресов см. в статье [Использование подписанных URL-адресов (SAS)](storage-dotnet-shared-access-signature-part-1.md).</span><span class="sxs-lookup"><span data-stu-id="96f1c-109">For more information about creating shared access signatures, see [Using shared access signatures (SAS) in Azure Storage](storage-dotnet-shared-access-signature-part-1.md).</span></span>

## <a name="grant-anonymous-users-permissions-toocontainers-and-blobs"></a><span data-ttu-id="96f1c-110">Предоставьте разрешения toocontainers анонимных пользователей и больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="96f1c-110">Grant anonymous users permissions toocontainers and blobs</span></span>
<span data-ttu-id="96f1c-111">По умолчанию контейнер и все большие двоичные объекты в ней может обращаться только владелец учетной записи хранилища hello hello.</span><span class="sxs-lookup"><span data-stu-id="96f1c-111">By default, a container and any blobs within it may be accessed only by hello owner of hello storage account.</span></span> <span data-ttu-id="96f1c-112">toogive анонимным пользователям разрешения на чтение tooa контейнера и BLOB-объектов, можно задать hello контейнера разрешения tooallow общего доступа.</span><span class="sxs-lookup"><span data-stu-id="96f1c-112">toogive anonymous users read permissions tooa container and its blobs, you can set hello container permissions tooallow public access.</span></span> <span data-ttu-id="96f1c-113">Анонимные пользователи могут считывать большие двоичные объекты в контейнере общедоступный без проверки подлинности запроса hello.</span><span class="sxs-lookup"><span data-stu-id="96f1c-113">Anonymous users can read blobs within a publicly accessible container without authenticating hello request.</span></span>

<span data-ttu-id="96f1c-114">Можно настроить контейнер hello следующие разрешения:</span><span class="sxs-lookup"><span data-stu-id="96f1c-114">You can configure a container with hello following permissions:</span></span>

* <span data-ttu-id="96f1c-115">**Отсутствует общий доступ на чтение:** hello контейнера и BLOB-объектов может осуществляться только владелец учетной записи хранилища hello.</span><span class="sxs-lookup"><span data-stu-id="96f1c-115">**No public read access:** hello container and its blobs can be accessed only by hello storage account owner.</span></span> <span data-ttu-id="96f1c-116">Это hello по умолчанию для всех новых контейнеров.</span><span class="sxs-lookup"><span data-stu-id="96f1c-116">This is hello default for all new containers.</span></span>
* <span data-ttu-id="96f1c-117">**Открытый доступ для больших двоичных объектов только чтения:** большие двоичные объекты в контейнере hello может считываться анонимный запрос, но данные контейнера недоступны.</span><span class="sxs-lookup"><span data-stu-id="96f1c-117">**Public read access for blobs only:** Blobs within hello container can be read by anonymous request, but container data is not available.</span></span> <span data-ttu-id="96f1c-118">Анонимные клиенты не могут перечислять hello большие двоичные объекты в контейнере hello.</span><span class="sxs-lookup"><span data-stu-id="96f1c-118">Anonymous clients cannot enumerate hello blobs within hello container.</span></span>
* <span data-ttu-id="96f1c-119">**Полный открытый доступ на чтение.** Все данные контейнера и больших двоичных объектов можно считать с помощью анонимного запроса.</span><span class="sxs-lookup"><span data-stu-id="96f1c-119">**Full public read access:** All container and blob data can be read by anonymous request.</span></span> <span data-ttu-id="96f1c-120">Клиенты могут перечислять большие двоичные объекты в контейнере hello с анонимный запрос, но не могут перечислять контейнеры в учетной записи хранилища hello.</span><span class="sxs-lookup"><span data-stu-id="96f1c-120">Clients can enumerate blobs within hello container by anonymous request, but cannot enumerate containers within hello storage account.</span></span>

<span data-ttu-id="96f1c-121">Можно использовать следующие разрешения контейнера tooset hello.</span><span class="sxs-lookup"><span data-stu-id="96f1c-121">You can use hello following tooset container permissions:</span></span>

* [<span data-ttu-id="96f1c-122">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="96f1c-122">Azure portal</span></span>](https://portal.azure.com)
* [<span data-ttu-id="96f1c-123">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="96f1c-123">Azure PowerShell</span></span>](storage-powershell-guide-full.md#how-to-manage-azure-blobs)
* [<span data-ttu-id="96f1c-124">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="96f1c-124">Azure CLI 2.0</span></span>](storage-azure-cli.md#create-and-manage-blobs)
* <span data-ttu-id="96f1c-125">Программно с помощью одного из клиентских библиотек хранилища hello или hello REST API</span><span class="sxs-lookup"><span data-stu-id="96f1c-125">Programmatically, by using one of hello storage client libraries or hello REST API</span></span>

### <a name="set-container-permissions-in-hello-azure-portal"></a><span data-ttu-id="96f1c-126">Задание разрешений для контейнера в hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="96f1c-126">Set container permissions in hello Azure portal</span></span>
<span data-ttu-id="96f1c-127">разрешения контейнера tooset в hello [портал Azure](https://portal.azure.com), выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="96f1c-127">tooset container permissions in hello [Azure portal](https://portal.azure.com), follow these steps:</span></span>

1. <span data-ttu-id="96f1c-128">Откройте ваш **учетной записи хранилища** колонке hello портала.</span><span class="sxs-lookup"><span data-stu-id="96f1c-128">Open your **Storage account** blade in hello portal.</span></span> <span data-ttu-id="96f1c-129">Учетной записи хранилища можно найти, выбрав **учетные записи хранения** в главном меню портала колонке hello.</span><span class="sxs-lookup"><span data-stu-id="96f1c-129">You can find your storage account by selecting **Storage accounts** in hello main portal menu blade.</span></span>
1. <span data-ttu-id="96f1c-130">В разделе **службы BLOB-ОБЪЕКТОВ** колонке hello меню, выберите **контейнеры**.</span><span class="sxs-lookup"><span data-stu-id="96f1c-130">Under **BLOB SERVICE** on hello menu blade, select **Containers**.</span></span>
1. <span data-ttu-id="96f1c-131">Щелкните правой кнопкой мыши строку hello контейнера или tooopen hello hello выберите кнопку с многоточием контейнера **контекстное меню**.</span><span class="sxs-lookup"><span data-stu-id="96f1c-131">Right-click on hello container row or select hello ellipsis tooopen hello container's **Context menu**.</span></span>
1. <span data-ttu-id="96f1c-132">Выберите **доступ к политике** в контекстном меню hello.</span><span class="sxs-lookup"><span data-stu-id="96f1c-132">Select **Access policy** in hello context menu.</span></span>
1. <span data-ttu-id="96f1c-133">Выберите **тип доступа** из hello раскрывающемся меню.</span><span class="sxs-lookup"><span data-stu-id="96f1c-133">Select an **Access type** from hello drop down menu.</span></span>

    ![Диалоговое окно «Изменение метаданных контейнера»](./media/storage-manage-access-to-resources/storage-manage-access-to-resources-0.png)

### <a name="set-container-permissions-with-net"></a><span data-ttu-id="96f1c-135">Назначение разрешений контейнера с помощью .NET</span><span class="sxs-lookup"><span data-stu-id="96f1c-135">Set container permissions with .NET</span></span>
<span data-ttu-id="96f1c-136">tooset разрешения для контейнера с помощью C# и hello клиентской библиотеки хранилища для .NET, сначала получить hello контейнера существующие разрешения с вызывающему Привет **GetPermissions** метод.</span><span class="sxs-lookup"><span data-stu-id="96f1c-136">tooset permissions for a container using C# and hello Storage Client Library for .NET, first retrieve hello container's existing permissions by calling hello **GetPermissions** method.</span></span> <span data-ttu-id="96f1c-137">Затем набор hello **PublicAccess** свойство для hello **BlobContainerPermissions** объект, возвращаемый hello **GetPermissions** метод.</span><span class="sxs-lookup"><span data-stu-id="96f1c-137">Then set hello **PublicAccess** property for hello **BlobContainerPermissions** object that is returned by hello **GetPermissions** method.</span></span> <span data-ttu-id="96f1c-138">Наконец, вызовите hello **SetPermissions** метод с hello обновлены разрешения.</span><span class="sxs-lookup"><span data-stu-id="96f1c-138">Finally, call hello **SetPermissions** method with hello updated permissions.</span></span>

<span data-ttu-id="96f1c-139">Следующий пример Hello задает разрешения контейнера hello toofull общего доступа на чтение.</span><span class="sxs-lookup"><span data-stu-id="96f1c-139">hello following example sets hello container's permissions toofull public read access.</span></span> <span data-ttu-id="96f1c-140">toopublic tooset разрешения чтение для больших двоичных объектов, значение hello **PublicAccess** свойство слишком**BlobContainerPublicAccessType.Blob**.</span><span class="sxs-lookup"><span data-stu-id="96f1c-140">tooset permissions toopublic read access for blobs only, set hello **PublicAccess** property too**BlobContainerPublicAccessType.Blob**.</span></span> <span data-ttu-id="96f1c-141">задать все разрешения для анонимных пользователей tooremove hello свойство слишком**BlobContainerPublicAccessType.Off**.</span><span class="sxs-lookup"><span data-stu-id="96f1c-141">tooremove all permissions for anonymous users, set hello property too**BlobContainerPublicAccessType.Off**.</span></span>

```csharp
public static void SetPublicContainerPermissions(CloudBlobContainer container)
{
    BlobContainerPermissions permissions = container.GetPermissions();
    permissions.PublicAccess = BlobContainerPublicAccessType.Container;
    container.SetPermissions(permissions);
}
```

## <a name="access-containers-and-blobs-anonymously"></a><span data-ttu-id="96f1c-142">Анонимный доступ к контейнерам и большим двоичным объектам</span><span class="sxs-lookup"><span data-stu-id="96f1c-142">Access containers and blobs anonymously</span></span>
<span data-ttu-id="96f1c-143">Клиент, который обращается к контейнерам и большим двоичным объектам анонимно, может использовать конструкторы, не требующие учетных данных.</span><span class="sxs-lookup"><span data-stu-id="96f1c-143">A client that accesses containers and blobs anonymously can use constructors that do not require credentials.</span></span> <span data-ttu-id="96f1c-144">Следующие примеры Hello Показать несколькими разными способами ресурсов службы BLOB-объектов tooreference анонимно.</span><span class="sxs-lookup"><span data-stu-id="96f1c-144">hello following examples show a few different ways tooreference Blob service resources anonymously.</span></span>

### <a name="create-an-anonymous-client-object"></a><span data-ttu-id="96f1c-145">Создание анонимного клиентского объекта</span><span class="sxs-lookup"><span data-stu-id="96f1c-145">Create an anonymous client object</span></span>
<span data-ttu-id="96f1c-146">Можно создать новый объект клиента службы для анонимного доступа, предоставляя hello конечной точки службы BLOB-объекта для учетной записи hello.</span><span class="sxs-lookup"><span data-stu-id="96f1c-146">You can create a new service client object for anonymous access by providing hello Blob service endpoint for hello account.</span></span> <span data-ttu-id="96f1c-147">Тем не менее необходимо также знать имя hello контейнера в этой учетной записи, которая доступна для анонимного доступа.</span><span class="sxs-lookup"><span data-stu-id="96f1c-147">However, you must also know hello name of a container in that account that's available for anonymous access.</span></span>

```csharp
public static void CreateAnonymousBlobClient()
{
    // Create hello client object using hello Blob service endpoint.
    CloudBlobClient blobClient = new CloudBlobClient(new Uri(@"https://storagesample.blob.core.windows.net"));

    // Get a reference tooa container that's available for anonymous access.
    CloudBlobContainer container = blobClient.GetContainerReference("sample-container");

    // Read hello container's properties. Note this is only possible when hello container supports full public read access.
    container.FetchAttributes();
    Console.WriteLine(container.Properties.LastModified);
    Console.WriteLine(container.Properties.ETag);
}
```

### <a name="reference-a-container-anonymously"></a><span data-ttu-id="96f1c-148">Анонимная ссылка на контейнер</span><span class="sxs-lookup"><span data-stu-id="96f1c-148">Reference a container anonymously</span></span>
<span data-ttu-id="96f1c-149">Если у вас есть контейнер tooa hello URL-адрес, который доступна анонимно, можно использовать его tooreference hello контейнера непосредственно.</span><span class="sxs-lookup"><span data-stu-id="96f1c-149">If you have hello URL tooa container that is anonymously available, you can use it tooreference hello container directly.</span></span>

```csharp
public static void ListBlobsAnonymously()
{
    // Get a reference tooa container that's available for anonymous access.
    CloudBlobContainer container = new CloudBlobContainer(new Uri(@"https://storagesample.blob.core.windows.net/sample-container"));

    // List blobs in hello container.
    foreach (IListBlobItem blobItem in container.ListBlobs())
    {
        Console.WriteLine(blobItem.Uri);
    }
}
```

### <a name="reference-a-blob-anonymously"></a><span data-ttu-id="96f1c-150">Анонимная ссылка на большой двоичный объект</span><span class="sxs-lookup"><span data-stu-id="96f1c-150">Reference a blob anonymously</span></span>
<span data-ttu-id="96f1c-151">При наличии hello URL-адрес tooa blob, которая доступна для анонимного доступа, можно создать ссылку hello больших двоичных объектов, непосредственно с помощью URL-адреса:</span><span class="sxs-lookup"><span data-stu-id="96f1c-151">If you have hello URL tooa blob that is available for anonymous access, you can reference hello blob directly using that URL:</span></span>

```csharp
public static void DownloadBlobAnonymously()
{
    CloudBlockBlob blob = new CloudBlockBlob(new Uri(@"https://storagesample.blob.core.windows.net/sample-container/logfile.txt"));
    blob.DownloadToFile(@"C:\Temp\logfile.txt", System.IO.FileMode.Create);
}
```

## <a name="features-available-tooanonymous-users"></a><span data-ttu-id="96f1c-152">Доступные tooanonymous возможности для пользователей</span><span class="sxs-lookup"><span data-stu-id="96f1c-152">Features available tooanonymous users</span></span>
<span data-ttu-id="96f1c-153">Hello в следующей таблице показаны операции, которые могут быть вызваны анонимным пользователям при ACL контейнера имеет значение tooallow общего доступа.</span><span class="sxs-lookup"><span data-stu-id="96f1c-153">hello following table shows which operations may be called by anonymous users when a container's ACL is set tooallow public access.</span></span>

| <span data-ttu-id="96f1c-154">Операция REST</span><span class="sxs-lookup"><span data-stu-id="96f1c-154">REST Operation</span></span> | <span data-ttu-id="96f1c-155">Разрешение на полный общий доступ для чтения</span><span class="sxs-lookup"><span data-stu-id="96f1c-155">Permission with full public read access</span></span> | <span data-ttu-id="96f1c-156">Разрешение на общий доступ для чтения только больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="96f1c-156">Permission with public read access for blobs only</span></span> |
| --- | --- | --- |
| <span data-ttu-id="96f1c-157">Перечисление контейнеров</span><span class="sxs-lookup"><span data-stu-id="96f1c-157">List Containers</span></span> |<span data-ttu-id="96f1c-158">Только владелец</span><span class="sxs-lookup"><span data-stu-id="96f1c-158">Owner only</span></span> |<span data-ttu-id="96f1c-159">Только владелец</span><span class="sxs-lookup"><span data-stu-id="96f1c-159">Owner only</span></span> |
| <span data-ttu-id="96f1c-160">Create Container (Создание контейнера)</span><span class="sxs-lookup"><span data-stu-id="96f1c-160">Create Container</span></span> |<span data-ttu-id="96f1c-161">Только владелец</span><span class="sxs-lookup"><span data-stu-id="96f1c-161">Owner only</span></span> |<span data-ttu-id="96f1c-162">Только владелец</span><span class="sxs-lookup"><span data-stu-id="96f1c-162">Owner only</span></span> |
| <span data-ttu-id="96f1c-163">Get Container Properties (Получение свойств контейнера)</span><span class="sxs-lookup"><span data-stu-id="96f1c-163">Get Container Properties</span></span> |<span data-ttu-id="96f1c-164">Все</span><span class="sxs-lookup"><span data-stu-id="96f1c-164">All</span></span> |<span data-ttu-id="96f1c-165">Только владелец</span><span class="sxs-lookup"><span data-stu-id="96f1c-165">Owner only</span></span> |
| <span data-ttu-id="96f1c-166">Get Container Metadata (Получение метаданных контейнера)</span><span class="sxs-lookup"><span data-stu-id="96f1c-166">Get Container Metadata</span></span> |<span data-ttu-id="96f1c-167">Все</span><span class="sxs-lookup"><span data-stu-id="96f1c-167">All</span></span> |<span data-ttu-id="96f1c-168">Только владелец</span><span class="sxs-lookup"><span data-stu-id="96f1c-168">Owner only</span></span> |
| <span data-ttu-id="96f1c-169">Set Container Metadata (Определение метаданных контейнера)</span><span class="sxs-lookup"><span data-stu-id="96f1c-169">Set Container Metadata</span></span> |<span data-ttu-id="96f1c-170">Только владелец</span><span class="sxs-lookup"><span data-stu-id="96f1c-170">Owner only</span></span> |<span data-ttu-id="96f1c-171">Только владелец</span><span class="sxs-lookup"><span data-stu-id="96f1c-171">Owner only</span></span> |
| <span data-ttu-id="96f1c-172">Get Container ACL (Получение списка управления доступом для контейнера)</span><span class="sxs-lookup"><span data-stu-id="96f1c-172">Get Container ACL</span></span> |<span data-ttu-id="96f1c-173">Только владелец</span><span class="sxs-lookup"><span data-stu-id="96f1c-173">Owner only</span></span> |<span data-ttu-id="96f1c-174">Только владелец</span><span class="sxs-lookup"><span data-stu-id="96f1c-174">Owner only</span></span> |
| <span data-ttu-id="96f1c-175">Set Container ACL (Задание списка управления доступом для контейнера)</span><span class="sxs-lookup"><span data-stu-id="96f1c-175">Set Container ACL</span></span> |<span data-ttu-id="96f1c-176">Только владелец</span><span class="sxs-lookup"><span data-stu-id="96f1c-176">Owner only</span></span> |<span data-ttu-id="96f1c-177">Только владелец</span><span class="sxs-lookup"><span data-stu-id="96f1c-177">Owner only</span></span> |
| <span data-ttu-id="96f1c-178">Delete Container (Удаление контейнера)</span><span class="sxs-lookup"><span data-stu-id="96f1c-178">Delete Container</span></span> |<span data-ttu-id="96f1c-179">Только владелец</span><span class="sxs-lookup"><span data-stu-id="96f1c-179">Owner only</span></span> |<span data-ttu-id="96f1c-180">Только владелец</span><span class="sxs-lookup"><span data-stu-id="96f1c-180">Owner only</span></span> |
| <span data-ttu-id="96f1c-181">List Blobs (Отображение списка BLOB-объектов)</span><span class="sxs-lookup"><span data-stu-id="96f1c-181">List Blobs</span></span> |<span data-ttu-id="96f1c-182">Все</span><span class="sxs-lookup"><span data-stu-id="96f1c-182">All</span></span> |<span data-ttu-id="96f1c-183">Только владелец</span><span class="sxs-lookup"><span data-stu-id="96f1c-183">Owner only</span></span> |
| <span data-ttu-id="96f1c-184">Put BLOB (Вставка BLOB-объекта)</span><span class="sxs-lookup"><span data-stu-id="96f1c-184">Put Blob</span></span> |<span data-ttu-id="96f1c-185">Только владелец</span><span class="sxs-lookup"><span data-stu-id="96f1c-185">Owner only</span></span> |<span data-ttu-id="96f1c-186">Только владелец</span><span class="sxs-lookup"><span data-stu-id="96f1c-186">Owner only</span></span> |
| <span data-ttu-id="96f1c-187">Get BLOB (Получение BLOB-объекта)</span><span class="sxs-lookup"><span data-stu-id="96f1c-187">Get Blob</span></span> |<span data-ttu-id="96f1c-188">Все</span><span class="sxs-lookup"><span data-stu-id="96f1c-188">All</span></span> |<span data-ttu-id="96f1c-189">Все</span><span class="sxs-lookup"><span data-stu-id="96f1c-189">All</span></span> |
| <span data-ttu-id="96f1c-190">Get BLOB Properties (Получение свойств BLOB-объекта)</span><span class="sxs-lookup"><span data-stu-id="96f1c-190">Get Blob Properties</span></span> |<span data-ttu-id="96f1c-191">Все</span><span class="sxs-lookup"><span data-stu-id="96f1c-191">All</span></span> |<span data-ttu-id="96f1c-192">Все</span><span class="sxs-lookup"><span data-stu-id="96f1c-192">All</span></span> |
| <span data-ttu-id="96f1c-193">Set BLOB Properties (Задание свойств службы BLOB-объекта)</span><span class="sxs-lookup"><span data-stu-id="96f1c-193">Set Blob Properties</span></span> |<span data-ttu-id="96f1c-194">Только владелец</span><span class="sxs-lookup"><span data-stu-id="96f1c-194">Owner only</span></span> |<span data-ttu-id="96f1c-195">Только владелец</span><span class="sxs-lookup"><span data-stu-id="96f1c-195">Owner only</span></span> |
| <span data-ttu-id="96f1c-196">Get BLOB Metadata (Получение метаданных BLOB-объекта)</span><span class="sxs-lookup"><span data-stu-id="96f1c-196">Get Blob Metadata</span></span> |<span data-ttu-id="96f1c-197">Все</span><span class="sxs-lookup"><span data-stu-id="96f1c-197">All</span></span> |<span data-ttu-id="96f1c-198">Все</span><span class="sxs-lookup"><span data-stu-id="96f1c-198">All</span></span> |
| <span data-ttu-id="96f1c-199">Set BLOB Metadata (Задание метаданных BLOB-объекта)</span><span class="sxs-lookup"><span data-stu-id="96f1c-199">Set Blob Metadata</span></span> |<span data-ttu-id="96f1c-200">Только владелец</span><span class="sxs-lookup"><span data-stu-id="96f1c-200">Owner only</span></span> |<span data-ttu-id="96f1c-201">Только владелец</span><span class="sxs-lookup"><span data-stu-id="96f1c-201">Owner only</span></span> |
| <span data-ttu-id="96f1c-202">Put Block (Вставка блокировки)</span><span class="sxs-lookup"><span data-stu-id="96f1c-202">Put Block</span></span> |<span data-ttu-id="96f1c-203">Только владелец</span><span class="sxs-lookup"><span data-stu-id="96f1c-203">Owner only</span></span> |<span data-ttu-id="96f1c-204">Только владелец</span><span class="sxs-lookup"><span data-stu-id="96f1c-204">Owner only</span></span> |
| <span data-ttu-id="96f1c-205">Получение списка блоков (только зафиксированные блоки)</span><span class="sxs-lookup"><span data-stu-id="96f1c-205">Get Block List (committed blocks only)</span></span> |<span data-ttu-id="96f1c-206">Все</span><span class="sxs-lookup"><span data-stu-id="96f1c-206">All</span></span> |<span data-ttu-id="96f1c-207">Все</span><span class="sxs-lookup"><span data-stu-id="96f1c-207">All</span></span> |
| <span data-ttu-id="96f1c-208">Получение списка блоков (только незафиксированные блоки или все блоки)</span><span class="sxs-lookup"><span data-stu-id="96f1c-208">Get Block List (uncommitted blocks only or all blocks)</span></span> |<span data-ttu-id="96f1c-209">Только владелец</span><span class="sxs-lookup"><span data-stu-id="96f1c-209">Owner only</span></span> |<span data-ttu-id="96f1c-210">Только владелец</span><span class="sxs-lookup"><span data-stu-id="96f1c-210">Owner only</span></span> |
| <span data-ttu-id="96f1c-211">Put Block List (Вставка списка блокировки)</span><span class="sxs-lookup"><span data-stu-id="96f1c-211">Put Block List</span></span> |<span data-ttu-id="96f1c-212">Только владелец</span><span class="sxs-lookup"><span data-stu-id="96f1c-212">Owner only</span></span> |<span data-ttu-id="96f1c-213">Только владелец</span><span class="sxs-lookup"><span data-stu-id="96f1c-213">Owner only</span></span> |
| <span data-ttu-id="96f1c-214">Delete BLOB (Удаление BLOB-объекта)</span><span class="sxs-lookup"><span data-stu-id="96f1c-214">Delete Blob</span></span> |<span data-ttu-id="96f1c-215">Только владелец</span><span class="sxs-lookup"><span data-stu-id="96f1c-215">Owner only</span></span> |<span data-ttu-id="96f1c-216">Только владелец</span><span class="sxs-lookup"><span data-stu-id="96f1c-216">Owner only</span></span> |
| <span data-ttu-id="96f1c-217">Копирование BLOB-объекта</span><span class="sxs-lookup"><span data-stu-id="96f1c-217">Copy Blob</span></span> |<span data-ttu-id="96f1c-218">Только владелец</span><span class="sxs-lookup"><span data-stu-id="96f1c-218">Owner only</span></span> |<span data-ttu-id="96f1c-219">Только владелец</span><span class="sxs-lookup"><span data-stu-id="96f1c-219">Owner only</span></span> |
| <span data-ttu-id="96f1c-220">Создание моментального снимка большого двоичного объекта</span><span class="sxs-lookup"><span data-stu-id="96f1c-220">Snapshot Blob</span></span> |<span data-ttu-id="96f1c-221">Только владелец</span><span class="sxs-lookup"><span data-stu-id="96f1c-221">Owner only</span></span> |<span data-ttu-id="96f1c-222">Только владелец</span><span class="sxs-lookup"><span data-stu-id="96f1c-222">Owner only</span></span> |
| <span data-ttu-id="96f1c-223">Lease Blob (Аренда BLOB-объекта)</span><span class="sxs-lookup"><span data-stu-id="96f1c-223">Lease Blob</span></span> |<span data-ttu-id="96f1c-224">Только владелец</span><span class="sxs-lookup"><span data-stu-id="96f1c-224">Owner only</span></span> |<span data-ttu-id="96f1c-225">Только владелец</span><span class="sxs-lookup"><span data-stu-id="96f1c-225">Owner only</span></span> |
| <span data-ttu-id="96f1c-226">Put Page (Вставка страницы)</span><span class="sxs-lookup"><span data-stu-id="96f1c-226">Put Page</span></span> |<span data-ttu-id="96f1c-227">Только владелец</span><span class="sxs-lookup"><span data-stu-id="96f1c-227">Owner only</span></span> |<span data-ttu-id="96f1c-228">Только владелец</span><span class="sxs-lookup"><span data-stu-id="96f1c-228">Owner only</span></span> |
| <span data-ttu-id="96f1c-229">Get Page Ranges (Получение диапазона страницы)</span><span class="sxs-lookup"><span data-stu-id="96f1c-229">Get Page Ranges</span></span> |<span data-ttu-id="96f1c-230">Все</span><span class="sxs-lookup"><span data-stu-id="96f1c-230">All</span></span> |<span data-ttu-id="96f1c-231">Все</span><span class="sxs-lookup"><span data-stu-id="96f1c-231">All</span></span> |
| <span data-ttu-id="96f1c-232">Добавление больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="96f1c-232">Append Blob</span></span> |<span data-ttu-id="96f1c-233">Только владелец</span><span class="sxs-lookup"><span data-stu-id="96f1c-233">Owner only</span></span> |<span data-ttu-id="96f1c-234">Только владелец</span><span class="sxs-lookup"><span data-stu-id="96f1c-234">Owner only</span></span> |

## <a name="next-steps"></a><span data-ttu-id="96f1c-235">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="96f1c-235">Next steps</span></span>

* [<span data-ttu-id="96f1c-236">Проверка подлинности для служб хранилища Azure hello</span><span class="sxs-lookup"><span data-stu-id="96f1c-236">Authentication for hello Azure Storage Services</span></span>](https://msdn.microsoft.com/library/azure/dd179428.aspx)
* [<span data-ttu-id="96f1c-237">Использование подписанных URL-адресов (SAS)</span><span class="sxs-lookup"><span data-stu-id="96f1c-237">Using Shared Access Signatures (SAS)</span></span>](storage-dotnet-shared-access-signature-part-1.md)
* [<span data-ttu-id="96f1c-238">Делегирование доступа с помощью подписанного URL-адреса</span><span class="sxs-lookup"><span data-stu-id="96f1c-238">Delegating Access with a Shared Access Signature</span></span>](https://msdn.microsoft.com/library/azure/ee395415.aspx)
