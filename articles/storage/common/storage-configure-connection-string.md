---
title: "aaaConfigure строку подключения для хранилища Azure | Документы Microsoft"
description: "Настройка строки подключения для учетной записи хранения Azure. Строка подключения содержит сведения о hello необходимый tooauthenticate доступа учетной записи хранилища tooa из приложения во время выполнения."
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
ms.openlocfilehash: ac1d7d9bf11fa6f44243cda0c40d8faee12e513b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-storage-connection-strings"></a><span data-ttu-id="2b1f8-104">Настройка строк подключения службы хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="2b1f8-104">Configure Azure Storage connection strings</span></span>

<span data-ttu-id="2b1f8-105">Строка подключения содержит hello сведения проверки подлинности, необходимые для tooaccess данных приложения в учетной записи хранилища Azure во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="2b1f8-105">A connection string includes hello authentication information required for your application tooaccess data in an Azure Storage account at runtime.</span></span> <span data-ttu-id="2b1f8-106">Настройка строки подключения позволяет выполнить следующие действия:</span><span class="sxs-lookup"><span data-stu-id="2b1f8-106">You can configure connection strings to:</span></span>

* <span data-ttu-id="2b1f8-107">Подключите toohello эмулятор хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="2b1f8-107">Connect toohello Azure storage emulator.</span></span>
* <span data-ttu-id="2b1f8-108">получить доступ к учетной записи хранения в Azure;</span><span class="sxs-lookup"><span data-stu-id="2b1f8-108">Access a storage account in Azure.</span></span>
* <span data-ttu-id="2b1f8-109">получить доступ к указанным ресурсам Azure через подписанный URL-адрес (SAS).</span><span class="sxs-lookup"><span data-stu-id="2b1f8-109">Access specified resources in Azure via a shared access signature (SAS).</span></span>

[!INCLUDE [storage-account-key-note-include](../../../includes/storage-account-key-note-include.md)]

## <a name="storing-your-connection-string"></a><span data-ttu-id="2b1f8-110">Хранение строки подключения</span><span class="sxs-lookup"><span data-stu-id="2b1f8-110">Storing your connection string</span></span>
<span data-ttu-id="2b1f8-111">Вашему приложению требуется строка подключения tooaccess hello в среды выполнения tooauthenticate запросов, сделанных tooAzure хранилища.</span><span class="sxs-lookup"><span data-stu-id="2b1f8-111">Your application needs tooaccess hello connection string at runtime tooauthenticate requests made tooAzure Storage.</span></span> <span data-ttu-id="2b1f8-112">Есть несколько вариантов для хранения строки подключения.</span><span class="sxs-lookup"><span data-stu-id="2b1f8-112">You have several options for storing your connection string:</span></span>

* <span data-ttu-id="2b1f8-113">Приложения, запущенного на рабочем столе hello, или на устройстве можно хранить строки подключения hello в **app.config** или **web.config** файла.</span><span class="sxs-lookup"><span data-stu-id="2b1f8-113">An application running on hello desktop or on a device can store hello connection string in an **app.config** or **web.config** file.</span></span> <span data-ttu-id="2b1f8-114">Добавить toohello строка подключения hello **AppSettings** раздел в этих файлах.</span><span class="sxs-lookup"><span data-stu-id="2b1f8-114">Add hello connection string toohello **AppSettings** section in these files.</span></span>
* <span data-ttu-id="2b1f8-115">Приложение, работающее в облачную службу Azure можно хранить строки подключения hello в hello [файл схемы (.cscfg) конфигурации службы Azure](https://msdn.microsoft.com/library/ee758710.aspx).</span><span class="sxs-lookup"><span data-stu-id="2b1f8-115">An application running in an Azure cloud service can store hello connection string in hello [Azure service configuration schema (.cscfg) file](https://msdn.microsoft.com/library/ee758710.aspx).</span></span> <span data-ttu-id="2b1f8-116">Добавить toohello строка подключения hello **ConfigurationSettings** раздел файла конфигурации службы hello.</span><span class="sxs-lookup"><span data-stu-id="2b1f8-116">Add hello connection string toohello **ConfigurationSettings** section of hello service configuration file.</span></span>
* <span data-ttu-id="2b1f8-117">Можно использовать строку подключения непосредственно в коде.</span><span class="sxs-lookup"><span data-stu-id="2b1f8-117">You can use your connection string directly in your code.</span></span> <span data-ttu-id="2b1f8-118">Однако в большинстве случаев рекомендуется хранить строку подключения в файле конфигурации.</span><span class="sxs-lookup"><span data-stu-id="2b1f8-118">However, we recommend that you store your connection string in a configuration file in most scenarios.</span></span>

<span data-ttu-id="2b1f8-119">Хранение строки подключения в файле конфигурации упрощает tooswitch строка подключения легко tooupdate hello между эмулятором хранилища hello и учетная запись хранилища Azure в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="2b1f8-119">Storing your connection string in a configuration file makes it easy tooupdate hello connection string tooswitch between hello storage emulator and an Azure storage account in hello cloud.</span></span> <span data-ttu-id="2b1f8-120">Требуется только tooedit hello строка подключения toopoint tooyour целевой среды.</span><span class="sxs-lookup"><span data-stu-id="2b1f8-120">You only need tooedit hello connection string toopoint tooyour target environment.</span></span>

<span data-ttu-id="2b1f8-121">Можно использовать hello [Microsoft Azure Configuration Manager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/) tooaccess в строке подключения во время выполнения независимо от того, где выполняется приложение.</span><span class="sxs-lookup"><span data-stu-id="2b1f8-121">You can use hello [Microsoft Azure Configuration Manager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/) tooaccess your connection string at runtime regardless of where your application is running.</span></span>

## <a name="create-a-connection-string-for-hello-storage-emulator"></a><span data-ttu-id="2b1f8-122">Создать строку подключения для эмулятора хранилища hello</span><span class="sxs-lookup"><span data-stu-id="2b1f8-122">Create a connection string for hello storage emulator</span></span>
[!INCLUDE [storage-emulator-connection-string-include](../../../includes/storage-emulator-connection-string-include.md)]

<span data-ttu-id="2b1f8-123">Дополнительные сведения о эмулятор хранилища hello. в разделе [использовать эмулятор хранилища Azure hello для разработки и тестирования](storage-use-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="2b1f8-123">For more information about hello storage emulator, see [Use hello Azure storage emulator for development and testing](storage-use-emulator.md).</span></span>

## <a name="create-a-connection-string-for-an-azure-storage-account"></a><span data-ttu-id="2b1f8-124">Создание строки подключения для учетной записи хранения Azure</span><span class="sxs-lookup"><span data-stu-id="2b1f8-124">Create a connection string for an Azure storage account</span></span>
<span data-ttu-id="2b1f8-125">toocreate строку подключения для вашей учетной записи хранилища Azure, используйте hello следующий формат.</span><span class="sxs-lookup"><span data-stu-id="2b1f8-125">toocreate a connection string for your Azure storage account, use hello following format.</span></span> <span data-ttu-id="2b1f8-126">Указать, нужно ли учетная запись хранения toohello tooconnect по протоколу HTTPS (рекомендуется) или HTTP, замените `myAccountName` с именем hello своей учетной записи хранилища, а `myAccountKey` с помощью ключа доступа учетной записи:</span><span class="sxs-lookup"><span data-stu-id="2b1f8-126">Indicate whether you want tooconnect toohello storage account through HTTPS (recommended) or HTTP, replace `myAccountName` with hello name of your storage account, and replace `myAccountKey` with your account access key:</span></span>

`DefaultEndpointsProtocol=[http|https];AccountName=myAccountName;AccountKey=myAccountKey`

<span data-ttu-id="2b1f8-127">Например, строка подключения может выглядеть так:</span><span class="sxs-lookup"><span data-stu-id="2b1f8-127">For example, your connection string might look similar to:</span></span>

`DefaultEndpointsProtocol=https;AccountName=storagesample;AccountKey=<account-key>`

<span data-ttu-id="2b1f8-128">Служба хранилища Azure поддерживает в строке подключения как HTTP, так и HTTPS, однако *настоятельно рекомендуется использовать HTTPS*.</span><span class="sxs-lookup"><span data-stu-id="2b1f8-128">Although Azure Storage supports both HTTP and HTTPS in a connection string, *HTTPS is highly recommended*.</span></span>

> [!TIP]
> <span data-ttu-id="2b1f8-129">Строки подключения учетной записи хранилища можно найти в hello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2b1f8-129">You can find your storage account's connection strings in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="2b1f8-130">Перейдите в слишком**параметры** > **ключи доступа** в строках соединения toosee колонке меню вашей учетной записи хранилища для обоих первичный и вторичный ключи доступа.</span><span class="sxs-lookup"><span data-stu-id="2b1f8-130">Navigate too**SETTINGS** > **Access keys** in your storage account's menu blade toosee connection strings for both primary and secondary access keys.</span></span>
>

## <a name="create-a-connection-string-using-a-shared-access-signature"></a><span data-ttu-id="2b1f8-131">Создание строки подключения с помощью подписанного URL-адреса</span><span class="sxs-lookup"><span data-stu-id="2b1f8-131">Create a connection string using a shared access signature</span></span>
[!INCLUDE [storage-use-sas-in-connection-string-include](../../../includes/storage-use-sas-in-connection-string-include.md)]

## <a name="create-a-connection-string-for-an-explicit-storage-endpoint"></a><span data-ttu-id="2b1f8-132">Создание строки подключения для явной конечной точки хранилища</span><span class="sxs-lookup"><span data-stu-id="2b1f8-132">Create a connection string for an explicit storage endpoint</span></span>
<span data-ttu-id="2b1f8-133">Конечные точки службы для явного можно указать в строке подключения вместо использования конечных точек по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="2b1f8-133">You can specify explicit service endpoints in your connection string instead of using hello default endpoints.</span></span> <span data-ttu-id="2b1f8-134">toocreate строка подключения, указывающая явная конечная точка hello полную конечную точку для каждой службы, включая спецификации протокола hello (HTTPS (рекомендуется) или HTTP), укажите в hello следующий формат:</span><span class="sxs-lookup"><span data-stu-id="2b1f8-134">toocreate a connection string that specifies an explicit endpoint, specify hello complete service endpoint for each service, including hello protocol specification (HTTPS (recommended) or HTTP), in hello following format:</span></span>

```
DefaultEndpointsProtocol=[http|https];
BlobEndpoint=myBlobEndpoint;
FileEndpoint=myFileEndpoint;
QueueEndpoint=myQueueEndpoint;
TableEndpoint=myTableEndpoint;
AccountName=myAccountName;
AccountKey=myAccountKey
```

<span data-ttu-id="2b1f8-135">Один сценарий, где вы можете toospecify явная конечная точка — когда сопоставленной вашей tooa конечной точке хранилища больших двоичных объектов [пользовательского домена](../blobs/storage-custom-domain-name.md).</span><span class="sxs-lookup"><span data-stu-id="2b1f8-135">One scenario where you might wish toospecify an explicit endpoint is when you've mapped your Blob storage endpoint tooa [custom domain](../blobs/storage-custom-domain-name.md).</span></span> <span data-ttu-id="2b1f8-136">В этом случае в строке подключения можно указать пользовательскую конечную точку хранилища BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="2b1f8-136">In that case, you can specify your custom endpoint for Blob storage in your connection string.</span></span> <span data-ttu-id="2b1f8-137">При необходимости можно hello конечные точки по умолчанию для hello другие службы, если приложение использует их.</span><span class="sxs-lookup"><span data-stu-id="2b1f8-137">You can optionally specify hello default endpoints for hello other services if your application uses them.</span></span>

<span data-ttu-id="2b1f8-138">Ниже приведен пример строки подключения, указывающее явная конечная точка для hello службы BLOB-объектов:</span><span class="sxs-lookup"><span data-stu-id="2b1f8-138">Here is an example of a connection string that specifies an explicit endpoint for hello Blob service:</span></span>

```
# Blob endpoint only
DefaultEndpointsProtocol=https;
BlobEndpoint=http://www.mydomain.com;
AccountName=storagesample;
AccountKey=<account-key>
```

<span data-ttu-id="2b1f8-139">Этот пример определяет явные конечные точки для всех служб, включая пользовательский домен для hello службы BLOB-объектов:</span><span class="sxs-lookup"><span data-stu-id="2b1f8-139">This example specifies explicit endpoints for all services, including a custom domain for hello Blob service:</span></span>

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

<span data-ttu-id="2b1f8-140">Hello конечной точки значения в строке подключения используется tooconstruct hello запроса служб хранилища toohello идентификаторы URI и определяют форму всех URI-адресов, которые возвращаются tooyour кода hello.</span><span class="sxs-lookup"><span data-stu-id="2b1f8-140">hello endpoint values in a connection string are used tooconstruct hello request URIs toohello storage services, and dictate hello form of any URIs that are returned tooyour code.</span></span>

<span data-ttu-id="2b1f8-141">Если сопоставлена пользовательского домена хранилища tooa конечной точки и опустить этой конечной точки из строки подключения, то нельзя будет toouse соединения строковые данные tooaccess службы из кода.</span><span class="sxs-lookup"><span data-stu-id="2b1f8-141">If you've mapped a storage endpoint tooa custom domain and omit that endpoint from a connection string, then you will not be able toouse that connection string tooaccess data in that service from your code.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2b1f8-142">Значения конечных точек служб в строках подключения должны быть в формате правильно сформированного универсального кода ресурса (URI), включая `https://` (рекомендуется) или `http://`.</span><span class="sxs-lookup"><span data-stu-id="2b1f8-142">Service endpoint values in your connection strings must be well-formed URIs, including `https://` (recommended) or `http://`.</span></span> <span data-ttu-id="2b1f8-143">Так как хранилище Azure еще не поддерживает протокол HTTPS для пользовательских доменов вы *должен* укажите `http://` для любой конечной точки URI, указывающий tooa пользовательского домена.</span><span class="sxs-lookup"><span data-stu-id="2b1f8-143">Because Azure Storage does not yet support HTTPS for custom domains, you *must* specify `http://` for any endpoint URI that points tooa custom domain.</span></span>
>

### <a name="create-a-connection-string-with-an-endpoint-suffix"></a><span data-ttu-id="2b1f8-144">Создание строки подключения с суффиксом конечной точки</span><span class="sxs-lookup"><span data-stu-id="2b1f8-144">Create a connection string with an endpoint suffix</span></span>
<span data-ttu-id="2b1f8-145">toocreate строка соединения для службы хранилища в регионах или экземпляров с другой конечной точке суффиксов, например для Китая Azure или Azure для государственных, hello используйте следующий формат строки соединения.</span><span class="sxs-lookup"><span data-stu-id="2b1f8-145">toocreate a connection string for a storage service in regions or instances with different endpoint suffixes, such as for Azure China or Azure Government, use hello following connection string format.</span></span> <span data-ttu-id="2b1f8-146">Указать, нужно ли учетная запись хранения toohello tooconnect по протоколу HTTPS (рекомендуется) или HTTP, замените `myAccountName` hello имя вашей учетной записи хранилища, замените `myAccountKey` с помощью ключа доступа учетной записи и замените `mySuffix` с hello URI суффикс:</span><span class="sxs-lookup"><span data-stu-id="2b1f8-146">Indicate whether you want tooconnect toohello storage account through HTTPS (recommended) or HTTP, replace `myAccountName` with hello name of your storage account, replace `myAccountKey` with your account access key, and replace `mySuffix` with hello URI suffix:</span></span>

```
DefaultEndpointsProtocol=[http|https];
AccountName=myAccountName;
AccountKey=myAccountKey;
EndpointSuffix=mySuffix;
```

<span data-ttu-id="2b1f8-147">Ниже приведен пример строки подключения для служб хранилища в Azure для Китая.</span><span class="sxs-lookup"><span data-stu-id="2b1f8-147">Here's an example connection string for storage services in Azure China:</span></span>

```
DefaultEndpointsProtocol=https;
AccountName=storagesample;
AccountKey=<account-key>;
EndpointSuffix=core.chinacloudapi.cn;
```

## <a name="parsing-a-connection-string"></a><span data-ttu-id="2b1f8-148">Анализ строки подключения</span><span class="sxs-lookup"><span data-stu-id="2b1f8-148">Parsing a connection string</span></span>
[!INCLUDE [storage-cloud-configuration-manager-include](../../../includes/storage-cloud-configuration-manager-include.md)]

## <a name="next-steps"></a><span data-ttu-id="2b1f8-149">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2b1f8-149">Next steps</span></span>
* [<span data-ttu-id="2b1f8-150">Используйте hello эмулятор хранилища Azure для разработки и тестирования</span><span class="sxs-lookup"><span data-stu-id="2b1f8-150">Use hello Azure storage emulator for development and testing</span></span>](storage-use-emulator.md)
* [<span data-ttu-id="2b1f8-151">Клиентские инструменты службы хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="2b1f8-151">Azure Storage explorers</span></span>](storage-explorers.md)
* [<span data-ttu-id="2b1f8-152">Использование подписанных URL-адресов (SAS)</span><span class="sxs-lookup"><span data-stu-id="2b1f8-152">Using Shared Access Signatures (SAS)</span></span>](storage-dotnet-shared-access-signature-part-1.md)

