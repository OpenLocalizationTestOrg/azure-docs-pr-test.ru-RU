---
title: "Настройка строки подключения для службы хранилища Azure | Документация Майкрософт"
description: "Настройка строки подключения для учетной записи хранения Azure. Строка подключения содержит сведения, необходимые для аутентификации при доступе к учетной записи хранения из приложения во время выполнения."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: ecb0acb5-90a9-4eb2-93e6-e9860eda5e53
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: marsma
ms.openlocfilehash: 01aa506e2b47fc29a70592e670a206a2b74248a4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="configure-azure-storage-connection-strings"></a><span data-ttu-id="d4723-104">Настройка строк подключения службы хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="d4723-104">Configure Azure Storage connection strings</span></span>

<span data-ttu-id="d4723-105">Строка подключения содержит сведения аутентификации, необходимые приложению для доступа к данным в учетной записи хранения Azure в среде выполнения.</span><span class="sxs-lookup"><span data-stu-id="d4723-105">A connection string includes the authentication information required for your application to access data in an Azure Storage account at runtime.</span></span> <span data-ttu-id="d4723-106">Настройка строки подключения позволяет выполнить следующие действия:</span><span class="sxs-lookup"><span data-stu-id="d4723-106">You can configure connection strings to:</span></span>

* <span data-ttu-id="d4723-107">подключиться к эмулятору хранилища Azure;</span><span class="sxs-lookup"><span data-stu-id="d4723-107">Connect to the Azure storage emulator.</span></span>
* <span data-ttu-id="d4723-108">получить доступ к учетной записи хранения в Azure;</span><span class="sxs-lookup"><span data-stu-id="d4723-108">Access a storage account in Azure.</span></span>
* <span data-ttu-id="d4723-109">получить доступ к указанным ресурсам Azure через подписанный URL-адрес (SAS).</span><span class="sxs-lookup"><span data-stu-id="d4723-109">Access specified resources in Azure via a shared access signature (SAS).</span></span>

[!INCLUDE [storage-account-key-note-include](../../includes/storage-account-key-note-include.md)]

## <a name="storing-your-connection-string"></a><span data-ttu-id="d4723-110">Хранение строки подключения</span><span class="sxs-lookup"><span data-stu-id="d4723-110">Storing your connection string</span></span>
<span data-ttu-id="d4723-111">Приложению требуется доступ к строке подключения в среде выполнения, чтобы выполнять аутентификацию запросов к службе хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="d4723-111">Your application needs to access the connection string at runtime to authenticate requests made to Azure Storage.</span></span> <span data-ttu-id="d4723-112">Есть несколько вариантов для хранения строки подключения.</span><span class="sxs-lookup"><span data-stu-id="d4723-112">You have several options for storing your connection string:</span></span>

* <span data-ttu-id="d4723-113">Приложение, работающее на настольном компьютере или на устройстве, может хранить строку подключения в файле **app.config** или **web.config**.</span><span class="sxs-lookup"><span data-stu-id="d4723-113">An application running on the desktop or on a device can store the connection string in an **app.config** or **web.config** file.</span></span> <span data-ttu-id="d4723-114">Добавьте строку подключения в раздел **AppSettings** в этих файлах.</span><span class="sxs-lookup"><span data-stu-id="d4723-114">Add the connection string to the **AppSettings** section in these files.</span></span>
* <span data-ttu-id="d4723-115">Приложение, работающее в облачной службе Azure, может хранить строку подключения в [файле схемы конфигурации службы Azure (.cscfg)](https://msdn.microsoft.com/library/ee758710.aspx).</span><span class="sxs-lookup"><span data-stu-id="d4723-115">An application running in an Azure cloud service can store the connection string in the [Azure service configuration schema (.cscfg) file](https://msdn.microsoft.com/library/ee758710.aspx).</span></span> <span data-ttu-id="d4723-116">Добавьте строку подключения в раздел **ConfigurationSettings** файла конфигурации службы.</span><span class="sxs-lookup"><span data-stu-id="d4723-116">Add the connection string to the **ConfigurationSettings** section of the service configuration file.</span></span>
* <span data-ttu-id="d4723-117">Можно использовать строку подключения непосредственно в коде.</span><span class="sxs-lookup"><span data-stu-id="d4723-117">You can use your connection string directly in your code.</span></span> <span data-ttu-id="d4723-118">Однако в большинстве случаев рекомендуется хранить строку подключения в файле конфигурации.</span><span class="sxs-lookup"><span data-stu-id="d4723-118">However, we recommend that you store your connection string in a configuration file in most scenarios.</span></span>

<span data-ttu-id="d4723-119">Хранение строки подключения в файле конфигурации упрощает обновление строки подключения для переключения между эмулятором хранения и учетной записью хранения Azure в облаке.</span><span class="sxs-lookup"><span data-stu-id="d4723-119">Storing your connection string in a configuration file makes it easy to update the connection string to switch between the storage emulator and an Azure storage account in the cloud.</span></span> <span data-ttu-id="d4723-120">Вам потребуется только изменить строку подключения, чтобы указать целевую среду.</span><span class="sxs-lookup"><span data-stu-id="d4723-120">You only need to edit the connection string to point to your target environment.</span></span>

<span data-ttu-id="d4723-121">Вы можете использовать [Microsoft Azure Configuration Manager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/) для доступа к строке подключения в среде выполнения независимо от того, где выполняется приложение.</span><span class="sxs-lookup"><span data-stu-id="d4723-121">You can use the [Microsoft Azure Configuration Manager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/) to access your connection string at runtime regardless of where your application is running.</span></span>

## <a name="create-a-connection-string-for-the-storage-emulator"></a><span data-ttu-id="d4723-122">Создание строки подключения для эмулятора хранения</span><span class="sxs-lookup"><span data-stu-id="d4723-122">Create a connection string for the storage emulator</span></span>
[!INCLUDE [storage-emulator-connection-string-include](../../includes/storage-emulator-connection-string-include.md)]

<span data-ttu-id="d4723-123">Дополнительные сведения об эмуляторе хранения см. в статье [Использование эмулятора хранения Azure для разработки и тестирования](storage-use-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="d4723-123">For more information about the storage emulator, see [Use the Azure storage emulator for development and testing](storage-use-emulator.md).</span></span>

## <a name="create-a-connection-string-for-an-azure-storage-account"></a><span data-ttu-id="d4723-124">Создание строки подключения для учетной записи хранения Azure</span><span class="sxs-lookup"><span data-stu-id="d4723-124">Create a connection string for an Azure storage account</span></span>
<span data-ttu-id="d4723-125">Чтобы создать строку подключения для учетной записи хранения Azure, используйте формат, указанный ниже.</span><span class="sxs-lookup"><span data-stu-id="d4723-125">To create a connection string for your Azure storage account, use the following format.</span></span> <span data-ttu-id="d4723-126">Указывает, следует ли подключаться к учетной записи хранения через HTTPS (рекомендуется) или HTTP. Замените `myAccountName` на имя вашей учетной записи хранения и замените `myAccountKey` на ваш ключ доступа учетной записи:</span><span class="sxs-lookup"><span data-stu-id="d4723-126">Indicate whether you want to connect to the storage account through HTTPS (recommended) or HTTP, replace `myAccountName` with the name of your storage account, and replace `myAccountKey` with your account access key:</span></span>

`DefaultEndpointsProtocol=[http|https];AccountName=myAccountName;AccountKey=myAccountKey`

<span data-ttu-id="d4723-127">Например, строка подключения может выглядеть так:</span><span class="sxs-lookup"><span data-stu-id="d4723-127">For example, your connection string might look similar to:</span></span>

`DefaultEndpointsProtocol=https;AccountName=storagesample;AccountKey=<account-key>`

<span data-ttu-id="d4723-128">Служба хранилища Azure поддерживает в строке подключения как HTTP, так и HTTPS, однако *настоятельно рекомендуется использовать HTTPS*.</span><span class="sxs-lookup"><span data-stu-id="d4723-128">Although Azure Storage supports both HTTP and HTTPS in a connection string, *HTTPS is highly recommended*.</span></span>

> [!TIP]
> <span data-ttu-id="d4723-129">Данные о строках подключения учетной записи хранения можно найти на [портале Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d4723-129">You can find your storage account's connection strings in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="d4723-130">В колонке меню учетной записи хранения выберите **ПАРАМЕТРЫ** > **Ключи доступа**, чтобы просмотреть строки подключения для первичных и вторичных ключей доступа.</span><span class="sxs-lookup"><span data-stu-id="d4723-130">Navigate to **SETTINGS** > **Access keys** in your storage account's menu blade to see connection strings for both primary and secondary access keys.</span></span>
>

## <a name="create-a-connection-string-using-a-shared-access-signature"></a><span data-ttu-id="d4723-131">Создание строки подключения с помощью подписанного URL-адреса</span><span class="sxs-lookup"><span data-stu-id="d4723-131">Create a connection string using a shared access signature</span></span>
[!INCLUDE [storage-use-sas-in-connection-string-include](../../includes/storage-use-sas-in-connection-string-include.md)]

## <a name="create-a-connection-string-for-an-explicit-storage-endpoint"></a><span data-ttu-id="d4723-132">Создание строки подключения для явной конечной точки хранилища</span><span class="sxs-lookup"><span data-stu-id="d4723-132">Create a connection string for an explicit storage endpoint</span></span>
<span data-ttu-id="d4723-133">Вы можете указать явные конечные точки службы в строке подключения вместо конечных точек по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="d4723-133">You can specify explicit service endpoints in your connection string instead of using the default endpoints.</span></span> <span data-ttu-id="d4723-134">Чтобы создать строку подключения, определяющую явную конечную точку, укажите полную конечную точку для каждой службы, включая спецификацию протокола (HTTPS (рекомендуется) или HTTP), в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="d4723-134">To create a connection string that specifies an explicit endpoint, specify the complete service endpoint for each service, including the protocol specification (HTTPS (recommended) or HTTP), in the following format:</span></span>

```
DefaultEndpointsProtocol=[http|https];
BlobEndpoint=myBlobEndpoint;
FileEndpoint=myFileEndpoint;
QueueEndpoint=myQueueEndpoint;
TableEndpoint=myTableEndpoint;
AccountName=myAccountName;
AccountKey=myAccountKey
```

<span data-ttu-id="d4723-135">Один из сценариев, когда может потребоваться указать явную конечную точку, — если конечная точка хранилища BLOB-объектов сопоставлена с [личным доменом](storage-custom-domain-name.md).</span><span class="sxs-lookup"><span data-stu-id="d4723-135">One scenario where you might wish to specify an explicit endpoint is when you've mapped your Blob storage endpoint to a [custom domain](storage-custom-domain-name.md).</span></span> <span data-ttu-id="d4723-136">В этом случае в строке подключения можно указать пользовательскую конечную точку хранилища BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="d4723-136">In that case, you can specify your custom endpoint for Blob storage in your connection string.</span></span> <span data-ttu-id="d4723-137">Вы можете дополнительно указать конечные точки по умолчанию для других служб, если приложение их использует.</span><span class="sxs-lookup"><span data-stu-id="d4723-137">You can optionally specify the default endpoints for the other services if your application uses them.</span></span>

<span data-ttu-id="d4723-138">Ниже приведен пример строки подключения, в которой указывается явная конечная точка для службы BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="d4723-138">Here is an example of a connection string that specifies an explicit endpoint for the Blob service:</span></span>

```
# Blob endpoint only
DefaultEndpointsProtocol=https;
BlobEndpoint=http://www.mydomain.com;
AccountName=storagesample;
AccountKey=<account-key>
```

<span data-ttu-id="d4723-139">В следующем примере указываются явные конечные точки для всех служб, включая личный домен для службы BLOB-объектов:</span><span class="sxs-lookup"><span data-stu-id="d4723-139">This example specifies explicit endpoints for all services, including a custom domain for the Blob service:</span></span>

```
# All service endpoints
DefaultEndpointsProtocol=https;
BlobEndpoint=http://www.mydomain.com;
FileEndpoint=https://myaccount.file.core.windows.net;
QueueEndpoint=https://myaccount.queue.core.windows.net;
TableEndpoint=https://myaccount.table.core.windows.net;
AccountName=storagesample;
AccountKey=<account-key>
```

<span data-ttu-id="d4723-140">Значения конечных точек из строки подключения применяются для создания универсальных кодов ресурса (URI) для служб хранилищ, а также определяют форму любых URI, возвращаемых в код.</span><span class="sxs-lookup"><span data-stu-id="d4723-140">The endpoint values in a connection string are used to construct the request URIs to the storage services, and dictate the form of any URIs that are returned to your code.</span></span>

<span data-ttu-id="d4723-141">Если сопоставить конечную точку хранилища с личным доменом и не указывать эту конечную точку в строке подключения, то вы не сможете получить доступ к данным в этой службе из своего кода с помощью данной строки подключения.</span><span class="sxs-lookup"><span data-stu-id="d4723-141">If you've mapped a storage endpoint to a custom domain and omit that endpoint from a connection string, then you will not be able to use that connection string to access data in that service from your code.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d4723-142">Значения конечных точек служб в строках подключения должны быть в формате правильно сформированного универсального кода ресурса (URI), включая `https://` (рекомендуется) или `http://`.</span><span class="sxs-lookup"><span data-stu-id="d4723-142">Service endpoint values in your connection strings must be well-formed URIs, including `https://` (recommended) or `http://`.</span></span> <span data-ttu-id="d4723-143">Так как служба хранилища Azure пока не поддерживает протокол HTTPS для личных доменов, *необходимо* указать `http://` в каждом универсальном коде ресурса (URI) конечной точки, который указывает на личный домен.</span><span class="sxs-lookup"><span data-stu-id="d4723-143">Because Azure Storage does not yet support HTTPS for custom domains, you *must* specify `http://` for any endpoint URI that points to a custom domain.</span></span>
>

### <a name="create-a-connection-string-with-an-endpoint-suffix"></a><span data-ttu-id="d4723-144">Создание строки подключения с суффиксом конечной точки</span><span class="sxs-lookup"><span data-stu-id="d4723-144">Create a connection string with an endpoint suffix</span></span>
<span data-ttu-id="d4723-145">Чтобы создать строку подключения для службы хранилища в регионах или экземплярах с разными суффиксами конечных точек, например Azure China (Azure для Китая) или Azure Government (Azure для государственных организаций), используйте следующий формат строки подключения.</span><span class="sxs-lookup"><span data-stu-id="d4723-145">To create a connection string for a storage service in regions or instances with different endpoint suffixes, such as for Azure China or Azure Government, use the following connection string format.</span></span> <span data-ttu-id="d4723-146">Укажите, следует ли подключаться к учетной записи хранения через HTTPS (рекомендуется) или HTTP. Замените `myAccountName` именем своей учетной записи хранения, замените `myAccountKey` ключом доступа своей учетной записи и замените `mySuffix` суффиксом URI:</span><span class="sxs-lookup"><span data-stu-id="d4723-146">Indicate whether you want to connect to the storage account through HTTPS (recommended) or HTTP, replace `myAccountName` with the name of your storage account, replace `myAccountKey` with your account access key, and replace `mySuffix` with the URI suffix:</span></span>

```
DefaultEndpointsProtocol=[http|https];
AccountName=myAccountName;
AccountKey=myAccountKey;
EndpointSuffix=mySuffix;
```

<span data-ttu-id="d4723-147">Ниже приведен пример строки подключения для служб хранилища в Azure для Китая.</span><span class="sxs-lookup"><span data-stu-id="d4723-147">Here's an example connection string for storage services in Azure China:</span></span>

```
DefaultEndpointsProtocol=https;
AccountName=storagesample;
AccountKey=<account-key>;
EndpointSuffix=core.chinacloudapi.cn;
```

## <a name="parsing-a-connection-string"></a><span data-ttu-id="d4723-148">Анализ строки подключения</span><span class="sxs-lookup"><span data-stu-id="d4723-148">Parsing a connection string</span></span>
[!INCLUDE [storage-cloud-configuration-manager-include](../../includes/storage-cloud-configuration-manager-include.md)]

## <a name="next-steps"></a><span data-ttu-id="d4723-149">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d4723-149">Next steps</span></span>
* [<span data-ttu-id="d4723-150">Использование эмулятора хранения Azure для разработки и тестирования</span><span class="sxs-lookup"><span data-stu-id="d4723-150">Use the Azure storage emulator for development and testing</span></span>](storage-use-emulator.md)
* [<span data-ttu-id="d4723-151">Клиентские инструменты службы хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="d4723-151">Azure Storage explorers</span></span>](storage-explorers.md)
* [<span data-ttu-id="d4723-152">Использование подписанных URL-адресов (SAS)</span><span class="sxs-lookup"><span data-stu-id="d4723-152">Using Shared Access Signatures (SAS)</span></span>](storage-dotnet-shared-access-signature-part-1.md)

