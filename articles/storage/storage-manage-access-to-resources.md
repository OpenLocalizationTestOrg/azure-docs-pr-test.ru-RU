---
title: "Включение открытого доступа на чтение к контейнерам и большим двоичным объектам в хранилище BLOB-объектов Azure | Документация Майкрософт"
description: "Узнайте, как сделать контейнеры и большие двоичные объекты доступными для анонимного доступа и как осуществлять к ним программный доступ."
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
ms.openlocfilehash: c7b83667b58649c156a62fa68cebd854c13e2cba
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="manage-anonymous-read-access-to-containers-and-blobs"></a><span data-ttu-id="cebbb-103">Управление анонимным доступом на чтение к контейнерам и большим двоичным объектам</span><span class="sxs-lookup"><span data-stu-id="cebbb-103">Manage anonymous read access to containers and blobs</span></span>
<span data-ttu-id="cebbb-104">Можно включить анонимный открытый доступ на чтение к контейнеру и его большим двоичным объектам в хранилище BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="cebbb-104">You can enable anonymous, public read access to a container and its blobs in Azure Blob storage.</span></span> <span data-ttu-id="cebbb-105">Таким образом можно предоставить доступ только для чтения к этим ресурсам, не передавая ключ учетной записи и не требуя подписанного URL-адреса (SAS).</span><span class="sxs-lookup"><span data-stu-id="cebbb-105">By doing so, you can grant read-only access to these resources without sharing your account key, and without requiring a shared access signature (SAS).</span></span>

<span data-ttu-id="cebbb-106">Открытый доступ на чтение лучше всего подходит для сценариев, когда определенные большие двоичные объекты нужно сделать всегда доступными для анонимного доступа на чтение.</span><span class="sxs-lookup"><span data-stu-id="cebbb-106">Public read access is best for scenarios where you want certain blobs to always be available for anonymous read access.</span></span> <span data-ttu-id="cebbb-107">Для более точного контроля можно создать подписанный URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="cebbb-107">For more fine-grained control, you can create a shared access signature.</span></span> <span data-ttu-id="cebbb-108">Подписанные URL-адреса позволяют предоставить ограниченный доступ с различными разрешениями на определенный период времени.</span><span class="sxs-lookup"><span data-stu-id="cebbb-108">Shared access signatures enable you to provide restricted access using different permissions, for a specific time period.</span></span> <span data-ttu-id="cebbb-109">Дополнительные сведения о создании подписанных URL-адресов см. в статье [Использование подписанных URL-адресов (SAS)](storage-dotnet-shared-access-signature-part-1.md).</span><span class="sxs-lookup"><span data-stu-id="cebbb-109">For more information about creating shared access signatures, see [Using shared access signatures (SAS) in Azure Storage](storage-dotnet-shared-access-signature-part-1.md).</span></span>

## <a name="grant-anonymous-users-permissions-to-containers-and-blobs"></a><span data-ttu-id="cebbb-110">Предоставление анонимным пользователям разрешений для контейнеров и больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="cebbb-110">Grant anonymous users permissions to containers and blobs</span></span>
<span data-ttu-id="cebbb-111">По умолчанию контейнер и все большие двоичные объекты внутри него доступны только владельцу учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="cebbb-111">By default, a container and any blobs within it may be accessed only by the owner of the storage account.</span></span> <span data-ttu-id="cebbb-112">Чтобы предоставить анонимным пользователями доступ на их чтение, следует разрешить общий доступ к контейнеру.</span><span class="sxs-lookup"><span data-stu-id="cebbb-112">To give anonymous users read permissions to a container and its blobs, you can set the container permissions to allow public access.</span></span> <span data-ttu-id="cebbb-113">Анонимные пользователи могут считывать данные большого двоичного объекта из общедоступного контейнера, при этом их запросы не будут проходить аутентификацию.</span><span class="sxs-lookup"><span data-stu-id="cebbb-113">Anonymous users can read blobs within a publicly accessible container without authenticating the request.</span></span>

<span data-ttu-id="cebbb-114">Можно настроить контейнер со следующими разрешениями:</span><span class="sxs-lookup"><span data-stu-id="cebbb-114">You can configure a container with the following permissions:</span></span>

* <span data-ttu-id="cebbb-115">**Без открытого доступа на чтение.** К контейнеру и его большим двоичным объектам может обращаться только владелец учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="cebbb-115">**No public read access:** The container and its blobs can be accessed only by the storage account owner.</span></span> <span data-ttu-id="cebbb-116">Это способ доступа по умолчанию для всех новых контейнеров.</span><span class="sxs-lookup"><span data-stu-id="cebbb-116">This is the default for all new containers.</span></span>
* <span data-ttu-id="cebbb-117">**Общий доступ на чтение только для больших двоичных объектов.** Большие двоичные объекты в контейнере можно считать с помощью анонимного запроса, но данные контейнера недоступны.</span><span class="sxs-lookup"><span data-stu-id="cebbb-117">**Public read access for blobs only:** Blobs within the container can be read by anonymous request, but container data is not available.</span></span> <span data-ttu-id="cebbb-118">Анонимные клиенты не могут перечислять большие двоичные объекты внутри контейнера.</span><span class="sxs-lookup"><span data-stu-id="cebbb-118">Anonymous clients cannot enumerate the blobs within the container.</span></span>
* <span data-ttu-id="cebbb-119">**Полный открытый доступ на чтение.** Все данные контейнера и больших двоичных объектов можно считать с помощью анонимного запроса.</span><span class="sxs-lookup"><span data-stu-id="cebbb-119">**Full public read access:** All container and blob data can be read by anonymous request.</span></span> <span data-ttu-id="cebbb-120">Клиенты могут перечислять большие двоичные объекты внутри контейнера с помощью анонимного запроса, но не могут перечислять контейнеры в учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="cebbb-120">Clients can enumerate blobs within the container by anonymous request, but cannot enumerate containers within the storage account.</span></span>

<span data-ttu-id="cebbb-121">Чтобы установить разрешения для контейнера, можно использовать:</span><span class="sxs-lookup"><span data-stu-id="cebbb-121">You can use the following to set container permissions:</span></span>

* [<span data-ttu-id="cebbb-122">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="cebbb-122">Azure portal</span></span>](https://portal.azure.com)
* [<span data-ttu-id="cebbb-123">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="cebbb-123">Azure PowerShell</span></span>](storage-powershell-guide-full.md#how-to-manage-azure-blobs)
* [<span data-ttu-id="cebbb-124">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="cebbb-124">Azure CLI 2.0</span></span>](storage-azure-cli.md#create-and-manage-blobs)
* <span data-ttu-id="cebbb-125">программный метод с помощью одной из клиентских библиотек службы хранилища или REST API.</span><span class="sxs-lookup"><span data-stu-id="cebbb-125">Programmatically, by using one of the storage client libraries or the REST API</span></span>

### <a name="set-container-permissions-in-the-azure-portal"></a><span data-ttu-id="cebbb-126">Настройка разрешений контейнера на портале Azure</span><span class="sxs-lookup"><span data-stu-id="cebbb-126">Set container permissions in the Azure portal</span></span>
<span data-ttu-id="cebbb-127">Чтобы задать разрешения контейнера на [портале Azure](https://portal.azure.com), выполните следующее.</span><span class="sxs-lookup"><span data-stu-id="cebbb-127">To set container permissions in the [Azure portal](https://portal.azure.com), follow these steps:</span></span>

1. <span data-ttu-id="cebbb-128">Откройте колонку **Учетная запись хранения** на портале.</span><span class="sxs-lookup"><span data-stu-id="cebbb-128">Open your **Storage account** blade in the portal.</span></span> <span data-ttu-id="cebbb-129">Чтобы найти свою учетную запись хранения, выберите **Учетные записи хранения** в основной колонке меню портала.</span><span class="sxs-lookup"><span data-stu-id="cebbb-129">You can find your storage account by selecting **Storage accounts** in the main portal menu blade.</span></span>
1. <span data-ttu-id="cebbb-130">В разделе **Служба BLOB-объектов** колонки меню выберите **Контейнеры**.</span><span class="sxs-lookup"><span data-stu-id="cebbb-130">Under **BLOB SERVICE** on the menu blade, select **Containers**.</span></span>
1. <span data-ttu-id="cebbb-131">Щелкните правой кнопкой мыши строку контейнера или щелкните многоточие, чтобы открыть **контекстное меню** контейнера.</span><span class="sxs-lookup"><span data-stu-id="cebbb-131">Right-click on the container row or select the ellipsis to open the container's **Context menu**.</span></span>
1. <span data-ttu-id="cebbb-132">Выберите **Политика доступа** в контекстном меню.</span><span class="sxs-lookup"><span data-stu-id="cebbb-132">Select **Access policy** in the context menu.</span></span>
1. <span data-ttu-id="cebbb-133">Из раскрывающегося списка выберите **Тип доступа**.</span><span class="sxs-lookup"><span data-stu-id="cebbb-133">Select an **Access type** from the drop down menu.</span></span>

    ![Диалоговое окно «Изменение метаданных контейнера»](./media/storage-manage-access-to-resources/storage-manage-access-to-resources-0.png)

### <a name="set-container-permissions-with-net"></a><span data-ttu-id="cebbb-135">Назначение разрешений контейнера с помощью .NET</span><span class="sxs-lookup"><span data-stu-id="cebbb-135">Set container permissions with .NET</span></span>
<span data-ttu-id="cebbb-136">Чтобы задать разрешения для контейнера с помощью C# и клиентской библиотеки службы хранилища для .NET, сначала нужно получить существующие разрешения контейнера, вызвав метод **GetPermissions**.</span><span class="sxs-lookup"><span data-stu-id="cebbb-136">To set permissions for a container using C# and the Storage Client Library for .NET, first retrieve the container's existing permissions by calling the **GetPermissions** method.</span></span> <span data-ttu-id="cebbb-137">Затем задайте свойство **PublicAccess** для объекта **BlobContainerPermissions**, который возвращается методом **GetPermissions**.</span><span class="sxs-lookup"><span data-stu-id="cebbb-137">Then set the **PublicAccess** property for the **BlobContainerPermissions** object that is returned by the **GetPermissions** method.</span></span> <span data-ttu-id="cebbb-138">Наконец, вызовите метод **SetPermissions** с обновленными разрешениями.</span><span class="sxs-lookup"><span data-stu-id="cebbb-138">Finally, call the **SetPermissions** method with the updated permissions.</span></span>

<span data-ttu-id="cebbb-139">В следующем примере задаются разрешения контейнера на полный общий доступ на чтение.</span><span class="sxs-lookup"><span data-stu-id="cebbb-139">The following example sets the container's permissions to full public read access.</span></span> <span data-ttu-id="cebbb-140">Чтобы задать общий доступ на чтение только для BLOB-объектов, задайте для свойства **PublicAccess** значение **BlobContainerPublicAccessType.Blob**.</span><span class="sxs-lookup"><span data-stu-id="cebbb-140">To set permissions to public read access for blobs only, set the **PublicAccess** property to **BlobContainerPublicAccessType.Blob**.</span></span> <span data-ttu-id="cebbb-141">Чтобы удалить все разрешения для анонимных пользователей, задайте для этого свойства значение **BlobContainerPublicAccessType.Off**.</span><span class="sxs-lookup"><span data-stu-id="cebbb-141">To remove all permissions for anonymous users, set the property to **BlobContainerPublicAccessType.Off**.</span></span>

```csharp
public static void SetPublicContainerPermissions(CloudBlobContainer container)
{
    BlobContainerPermissions permissions = container.GetPermissions();
    permissions.PublicAccess = BlobContainerPublicAccessType.Container;
    container.SetPermissions(permissions);
}
```

## <a name="access-containers-and-blobs-anonymously"></a><span data-ttu-id="cebbb-142">Анонимный доступ к контейнерам и большим двоичным объектам</span><span class="sxs-lookup"><span data-stu-id="cebbb-142">Access containers and blobs anonymously</span></span>
<span data-ttu-id="cebbb-143">Клиент, который обращается к контейнерам и большим двоичным объектам анонимно, может использовать конструкторы, не требующие учетных данных.</span><span class="sxs-lookup"><span data-stu-id="cebbb-143">A client that accesses containers and blobs anonymously can use constructors that do not require credentials.</span></span> <span data-ttu-id="cebbb-144">В следующих примерах показано несколько разных способов анонимной ссылки на ресурсы службы BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="cebbb-144">The following examples show a few different ways to reference Blob service resources anonymously.</span></span>

### <a name="create-an-anonymous-client-object"></a><span data-ttu-id="cebbb-145">Создание анонимного клиентского объекта</span><span class="sxs-lookup"><span data-stu-id="cebbb-145">Create an anonymous client object</span></span>
<span data-ttu-id="cebbb-146">Можно создать новый клиентский объект службы для анонимного доступа, указав конечную точку службы DLOB-объектов для соответствующей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="cebbb-146">You can create a new service client object for anonymous access by providing the Blob service endpoint for the account.</span></span> <span data-ttu-id="cebbb-147">Тем не менее необходимо также знать имя контейнера в этой учетной записи, которая доступна для анонимного доступа.</span><span class="sxs-lookup"><span data-stu-id="cebbb-147">However, you must also know the name of a container in that account that's available for anonymous access.</span></span>

```csharp
public static void CreateAnonymousBlobClient()
{
    // Create the client object using the Blob service endpoint.
    CloudBlobClient blobClient = new CloudBlobClient(new Uri(@"https://storagesample.blob.core.windows.net"));

    // Get a reference to a container that's available for anonymous access.
    CloudBlobContainer container = blobClient.GetContainerReference("sample-container");

    // Read the container's properties. Note this is only possible when the container supports full public read access.
    container.FetchAttributes();
    Console.WriteLine(container.Properties.LastModified);
    Console.WriteLine(container.Properties.ETag);
}
```

### <a name="reference-a-container-anonymously"></a><span data-ttu-id="cebbb-148">Анонимная ссылка на контейнер</span><span class="sxs-lookup"><span data-stu-id="cebbb-148">Reference a container anonymously</span></span>
<span data-ttu-id="cebbb-149">При наличии URL-адреса контейнера, который доступен анонимно, можно воспользоваться им для прямой ссылки на контейнер.</span><span class="sxs-lookup"><span data-stu-id="cebbb-149">If you have the URL to a container that is anonymously available, you can use it to reference the container directly.</span></span>

```csharp
public static void ListBlobsAnonymously()
{
    // Get a reference to a container that's available for anonymous access.
    CloudBlobContainer container = new CloudBlobContainer(new Uri(@"https://storagesample.blob.core.windows.net/sample-container"));

    // List blobs in the container.
    foreach (IListBlobItem blobItem in container.ListBlobs())
    {
        Console.WriteLine(blobItem.Uri);
    }
}
```

### <a name="reference-a-blob-anonymously"></a><span data-ttu-id="cebbb-150">Анонимная ссылка на большой двоичный объект</span><span class="sxs-lookup"><span data-stu-id="cebbb-150">Reference a blob anonymously</span></span>
<span data-ttu-id="cebbb-151">Если имеется URL-адрес большого двоичного объекта, который доступен для анонимного доступа, можно создать прямую ссылку на этот большой двоичный объект, используя URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="cebbb-151">If you have the URL to a blob that is available for anonymous access, you can reference the blob directly using that URL:</span></span>

```csharp
public static void DownloadBlobAnonymously()
{
    CloudBlockBlob blob = new CloudBlockBlob(new Uri(@"https://storagesample.blob.core.windows.net/sample-container/logfile.txt"));
    blob.DownloadToFile(@"C:\Temp\logfile.txt", System.IO.FileMode.Create);
}
```

## <a name="features-available-to-anonymous-users"></a><span data-ttu-id="cebbb-152">Функции, доступные анонимным пользователям</span><span class="sxs-lookup"><span data-stu-id="cebbb-152">Features available to anonymous users</span></span>
<span data-ttu-id="cebbb-153">В следующей таблице приведены операции, которые могут быть вызваны анонимными пользователями, если в списке управления доступом к контейнеру разрешен общий доступ.</span><span class="sxs-lookup"><span data-stu-id="cebbb-153">The following table shows which operations may be called by anonymous users when a container's ACL is set to allow public access.</span></span>

| <span data-ttu-id="cebbb-154">Операция REST</span><span class="sxs-lookup"><span data-stu-id="cebbb-154">REST Operation</span></span> | <span data-ttu-id="cebbb-155">Разрешение на полный общий доступ для чтения</span><span class="sxs-lookup"><span data-stu-id="cebbb-155">Permission with full public read access</span></span> | <span data-ttu-id="cebbb-156">Разрешение на общий доступ для чтения только больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="cebbb-156">Permission with public read access for blobs only</span></span> |
| --- | --- | --- |
| <span data-ttu-id="cebbb-157">Перечисление контейнеров</span><span class="sxs-lookup"><span data-stu-id="cebbb-157">List Containers</span></span> |<span data-ttu-id="cebbb-158">Только владелец</span><span class="sxs-lookup"><span data-stu-id="cebbb-158">Owner only</span></span> |<span data-ttu-id="cebbb-159">Только владелец</span><span class="sxs-lookup"><span data-stu-id="cebbb-159">Owner only</span></span> |
| <span data-ttu-id="cebbb-160">Create Container (Создание контейнера)</span><span class="sxs-lookup"><span data-stu-id="cebbb-160">Create Container</span></span> |<span data-ttu-id="cebbb-161">Только владелец</span><span class="sxs-lookup"><span data-stu-id="cebbb-161">Owner only</span></span> |<span data-ttu-id="cebbb-162">Только владелец</span><span class="sxs-lookup"><span data-stu-id="cebbb-162">Owner only</span></span> |
| <span data-ttu-id="cebbb-163">Get Container Properties (Получение свойств контейнера)</span><span class="sxs-lookup"><span data-stu-id="cebbb-163">Get Container Properties</span></span> |<span data-ttu-id="cebbb-164">Все</span><span class="sxs-lookup"><span data-stu-id="cebbb-164">All</span></span> |<span data-ttu-id="cebbb-165">Только владелец</span><span class="sxs-lookup"><span data-stu-id="cebbb-165">Owner only</span></span> |
| <span data-ttu-id="cebbb-166">Get Container Metadata (Получение метаданных контейнера)</span><span class="sxs-lookup"><span data-stu-id="cebbb-166">Get Container Metadata</span></span> |<span data-ttu-id="cebbb-167">Все</span><span class="sxs-lookup"><span data-stu-id="cebbb-167">All</span></span> |<span data-ttu-id="cebbb-168">Только владелец</span><span class="sxs-lookup"><span data-stu-id="cebbb-168">Owner only</span></span> |
| <span data-ttu-id="cebbb-169">Set Container Metadata (Определение метаданных контейнера)</span><span class="sxs-lookup"><span data-stu-id="cebbb-169">Set Container Metadata</span></span> |<span data-ttu-id="cebbb-170">Только владелец</span><span class="sxs-lookup"><span data-stu-id="cebbb-170">Owner only</span></span> |<span data-ttu-id="cebbb-171">Только владелец</span><span class="sxs-lookup"><span data-stu-id="cebbb-171">Owner only</span></span> |
| <span data-ttu-id="cebbb-172">Get Container ACL (Получение списка управления доступом для контейнера)</span><span class="sxs-lookup"><span data-stu-id="cebbb-172">Get Container ACL</span></span> |<span data-ttu-id="cebbb-173">Только владелец</span><span class="sxs-lookup"><span data-stu-id="cebbb-173">Owner only</span></span> |<span data-ttu-id="cebbb-174">Только владелец</span><span class="sxs-lookup"><span data-stu-id="cebbb-174">Owner only</span></span> |
| <span data-ttu-id="cebbb-175">Set Container ACL (Задание списка управления доступом для контейнера)</span><span class="sxs-lookup"><span data-stu-id="cebbb-175">Set Container ACL</span></span> |<span data-ttu-id="cebbb-176">Только владелец</span><span class="sxs-lookup"><span data-stu-id="cebbb-176">Owner only</span></span> |<span data-ttu-id="cebbb-177">Только владелец</span><span class="sxs-lookup"><span data-stu-id="cebbb-177">Owner only</span></span> |
| <span data-ttu-id="cebbb-178">Delete Container (Удаление контейнера)</span><span class="sxs-lookup"><span data-stu-id="cebbb-178">Delete Container</span></span> |<span data-ttu-id="cebbb-179">Только владелец</span><span class="sxs-lookup"><span data-stu-id="cebbb-179">Owner only</span></span> |<span data-ttu-id="cebbb-180">Только владелец</span><span class="sxs-lookup"><span data-stu-id="cebbb-180">Owner only</span></span> |
| <span data-ttu-id="cebbb-181">List Blobs (Отображение списка BLOB-объектов)</span><span class="sxs-lookup"><span data-stu-id="cebbb-181">List Blobs</span></span> |<span data-ttu-id="cebbb-182">Все</span><span class="sxs-lookup"><span data-stu-id="cebbb-182">All</span></span> |<span data-ttu-id="cebbb-183">Только владелец</span><span class="sxs-lookup"><span data-stu-id="cebbb-183">Owner only</span></span> |
| <span data-ttu-id="cebbb-184">Put BLOB (Вставка BLOB-объекта)</span><span class="sxs-lookup"><span data-stu-id="cebbb-184">Put Blob</span></span> |<span data-ttu-id="cebbb-185">Только владелец</span><span class="sxs-lookup"><span data-stu-id="cebbb-185">Owner only</span></span> |<span data-ttu-id="cebbb-186">Только владелец</span><span class="sxs-lookup"><span data-stu-id="cebbb-186">Owner only</span></span> |
| <span data-ttu-id="cebbb-187">Get BLOB (Получение BLOB-объекта)</span><span class="sxs-lookup"><span data-stu-id="cebbb-187">Get Blob</span></span> |<span data-ttu-id="cebbb-188">Все</span><span class="sxs-lookup"><span data-stu-id="cebbb-188">All</span></span> |<span data-ttu-id="cebbb-189">Все</span><span class="sxs-lookup"><span data-stu-id="cebbb-189">All</span></span> |
| <span data-ttu-id="cebbb-190">Get BLOB Properties (Получение свойств BLOB-объекта)</span><span class="sxs-lookup"><span data-stu-id="cebbb-190">Get Blob Properties</span></span> |<span data-ttu-id="cebbb-191">Все</span><span class="sxs-lookup"><span data-stu-id="cebbb-191">All</span></span> |<span data-ttu-id="cebbb-192">Все</span><span class="sxs-lookup"><span data-stu-id="cebbb-192">All</span></span> |
| <span data-ttu-id="cebbb-193">Set BLOB Properties (Задание свойств службы BLOB-объекта)</span><span class="sxs-lookup"><span data-stu-id="cebbb-193">Set Blob Properties</span></span> |<span data-ttu-id="cebbb-194">Только владелец</span><span class="sxs-lookup"><span data-stu-id="cebbb-194">Owner only</span></span> |<span data-ttu-id="cebbb-195">Только владелец</span><span class="sxs-lookup"><span data-stu-id="cebbb-195">Owner only</span></span> |
| <span data-ttu-id="cebbb-196">Get BLOB Metadata (Получение метаданных BLOB-объекта)</span><span class="sxs-lookup"><span data-stu-id="cebbb-196">Get Blob Metadata</span></span> |<span data-ttu-id="cebbb-197">Все</span><span class="sxs-lookup"><span data-stu-id="cebbb-197">All</span></span> |<span data-ttu-id="cebbb-198">Все</span><span class="sxs-lookup"><span data-stu-id="cebbb-198">All</span></span> |
| <span data-ttu-id="cebbb-199">Set BLOB Metadata (Задание метаданных BLOB-объекта)</span><span class="sxs-lookup"><span data-stu-id="cebbb-199">Set Blob Metadata</span></span> |<span data-ttu-id="cebbb-200">Только владелец</span><span class="sxs-lookup"><span data-stu-id="cebbb-200">Owner only</span></span> |<span data-ttu-id="cebbb-201">Только владелец</span><span class="sxs-lookup"><span data-stu-id="cebbb-201">Owner only</span></span> |
| <span data-ttu-id="cebbb-202">Put Block (Вставка блокировки)</span><span class="sxs-lookup"><span data-stu-id="cebbb-202">Put Block</span></span> |<span data-ttu-id="cebbb-203">Только владелец</span><span class="sxs-lookup"><span data-stu-id="cebbb-203">Owner only</span></span> |<span data-ttu-id="cebbb-204">Только владелец</span><span class="sxs-lookup"><span data-stu-id="cebbb-204">Owner only</span></span> |
| <span data-ttu-id="cebbb-205">Получение списка блоков (только зафиксированные блоки)</span><span class="sxs-lookup"><span data-stu-id="cebbb-205">Get Block List (committed blocks only)</span></span> |<span data-ttu-id="cebbb-206">Все</span><span class="sxs-lookup"><span data-stu-id="cebbb-206">All</span></span> |<span data-ttu-id="cebbb-207">Все</span><span class="sxs-lookup"><span data-stu-id="cebbb-207">All</span></span> |
| <span data-ttu-id="cebbb-208">Получение списка блоков (только незафиксированные блоки или все блоки)</span><span class="sxs-lookup"><span data-stu-id="cebbb-208">Get Block List (uncommitted blocks only or all blocks)</span></span> |<span data-ttu-id="cebbb-209">Только владелец</span><span class="sxs-lookup"><span data-stu-id="cebbb-209">Owner only</span></span> |<span data-ttu-id="cebbb-210">Только владелец</span><span class="sxs-lookup"><span data-stu-id="cebbb-210">Owner only</span></span> |
| <span data-ttu-id="cebbb-211">Put Block List (Вставка списка блокировки)</span><span class="sxs-lookup"><span data-stu-id="cebbb-211">Put Block List</span></span> |<span data-ttu-id="cebbb-212">Только владелец</span><span class="sxs-lookup"><span data-stu-id="cebbb-212">Owner only</span></span> |<span data-ttu-id="cebbb-213">Только владелец</span><span class="sxs-lookup"><span data-stu-id="cebbb-213">Owner only</span></span> |
| <span data-ttu-id="cebbb-214">Delete BLOB (Удаление BLOB-объекта)</span><span class="sxs-lookup"><span data-stu-id="cebbb-214">Delete Blob</span></span> |<span data-ttu-id="cebbb-215">Только владелец</span><span class="sxs-lookup"><span data-stu-id="cebbb-215">Owner only</span></span> |<span data-ttu-id="cebbb-216">Только владелец</span><span class="sxs-lookup"><span data-stu-id="cebbb-216">Owner only</span></span> |
| <span data-ttu-id="cebbb-217">Копирование BLOB-объекта</span><span class="sxs-lookup"><span data-stu-id="cebbb-217">Copy Blob</span></span> |<span data-ttu-id="cebbb-218">Только владелец</span><span class="sxs-lookup"><span data-stu-id="cebbb-218">Owner only</span></span> |<span data-ttu-id="cebbb-219">Только владелец</span><span class="sxs-lookup"><span data-stu-id="cebbb-219">Owner only</span></span> |
| <span data-ttu-id="cebbb-220">Создание моментального снимка большого двоичного объекта</span><span class="sxs-lookup"><span data-stu-id="cebbb-220">Snapshot Blob</span></span> |<span data-ttu-id="cebbb-221">Только владелец</span><span class="sxs-lookup"><span data-stu-id="cebbb-221">Owner only</span></span> |<span data-ttu-id="cebbb-222">Только владелец</span><span class="sxs-lookup"><span data-stu-id="cebbb-222">Owner only</span></span> |
| <span data-ttu-id="cebbb-223">Lease Blob (Аренда BLOB-объекта)</span><span class="sxs-lookup"><span data-stu-id="cebbb-223">Lease Blob</span></span> |<span data-ttu-id="cebbb-224">Только владелец</span><span class="sxs-lookup"><span data-stu-id="cebbb-224">Owner only</span></span> |<span data-ttu-id="cebbb-225">Только владелец</span><span class="sxs-lookup"><span data-stu-id="cebbb-225">Owner only</span></span> |
| <span data-ttu-id="cebbb-226">Put Page (Вставка страницы)</span><span class="sxs-lookup"><span data-stu-id="cebbb-226">Put Page</span></span> |<span data-ttu-id="cebbb-227">Только владелец</span><span class="sxs-lookup"><span data-stu-id="cebbb-227">Owner only</span></span> |<span data-ttu-id="cebbb-228">Только владелец</span><span class="sxs-lookup"><span data-stu-id="cebbb-228">Owner only</span></span> |
| <span data-ttu-id="cebbb-229">Get Page Ranges (Получение диапазона страницы)</span><span class="sxs-lookup"><span data-stu-id="cebbb-229">Get Page Ranges</span></span> |<span data-ttu-id="cebbb-230">Все</span><span class="sxs-lookup"><span data-stu-id="cebbb-230">All</span></span> |<span data-ttu-id="cebbb-231">Все</span><span class="sxs-lookup"><span data-stu-id="cebbb-231">All</span></span> |
| <span data-ttu-id="cebbb-232">Добавление больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="cebbb-232">Append Blob</span></span> |<span data-ttu-id="cebbb-233">Только владелец</span><span class="sxs-lookup"><span data-stu-id="cebbb-233">Owner only</span></span> |<span data-ttu-id="cebbb-234">Только владелец</span><span class="sxs-lookup"><span data-stu-id="cebbb-234">Owner only</span></span> |

## <a name="next-steps"></a><span data-ttu-id="cebbb-235">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="cebbb-235">Next steps</span></span>

* [<span data-ttu-id="cebbb-236">Проверка подлинности для служб хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="cebbb-236">Authentication for the Azure Storage Services</span></span>](https://msdn.microsoft.com/library/azure/dd179428.aspx)
* [<span data-ttu-id="cebbb-237">Использование подписанных URL-адресов (SAS)</span><span class="sxs-lookup"><span data-stu-id="cebbb-237">Using Shared Access Signatures (SAS)</span></span>](storage-dotnet-shared-access-signature-part-1.md)
* [<span data-ttu-id="cebbb-238">Делегирование доступа с помощью подписанного URL-адреса</span><span class="sxs-lookup"><span data-stu-id="cebbb-238">Delegating Access with a Shared Access Signature</span></span>](https://msdn.microsoft.com/library/azure/ee395415.aspx)
