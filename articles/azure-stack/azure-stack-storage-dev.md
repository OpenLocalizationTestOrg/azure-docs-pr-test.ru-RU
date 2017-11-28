---
title: "aaaGet к работе со средствами разработки стек хранилища Azure"
description: "Руководство по tooget работы со средствами разработки стек хранилища Azure"
services: azure-stack
author: xiaofmao
ms.author: xiaofmao
ms.date: 7/21/2017
ms.topic: get-started-article
ms.service: azure-stack
ms.openlocfilehash: 0756ed1b9fad4aed0cca4cfd719ef3334dec6700
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-stack-storage-development-tools"></a><span data-ttu-id="fe0da-103">Начало работы со средствами разработки стек хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="fe0da-103">Get started with Azure Stack Storage development tools</span></span> 

<span data-ttu-id="fe0da-104">Стека Microsoft Azure предоставляет набор служб хранилища, включая хранилище больших двоичных объектов Azure, таблиц и очередей.</span><span class="sxs-lookup"><span data-stu-id="fe0da-104">Microsoft Azure Stack provides a set of storage services, including Azure Blob, Table, and Queue storage.</span></span>

<span data-ttu-id="fe0da-105">В этой статье приведены рекомендации быстрого toostart средствами разработки стек хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="fe0da-105">This article provides quick guidance on how toostart using Azure Stack Storage development tools.</span></span> <span data-ttu-id="fe0da-106">Более подробные сведения и примеры кода можно найти в хранилище Azure руководства hello.</span><span class="sxs-lookup"><span data-stu-id="fe0da-106">You can find more detailed information and sample code in hello corresponding Azure Storage tutorials.</span></span>

<span data-ttu-id="fe0da-107">Существуют известные различия между хранилища Azure и стек хранилища Azure, включая определенные требования для каждой платформы.</span><span class="sxs-lookup"><span data-stu-id="fe0da-107">There are known differences between Azure Storage and Azure Stack Storage, including some specific requirements for each platform.</span></span> <span data-ttu-id="fe0da-108">Например существуют определенные клиентские библиотеки и требования суффикс конкретной конечной точки для стека Azure.</span><span class="sxs-lookup"><span data-stu-id="fe0da-108">For example, there are specific client libraries and specific endpoint suffix requirements for Azure Stack.</span></span> <span data-ttu-id="fe0da-109">Дополнительные сведения см. в разделе [стек хранилища Azure: различия и рекомендации](azure-stack-acs-differences.md).</span><span class="sxs-lookup"><span data-stu-id="fe0da-109">For more information, see [Azure Stack Storage: Differences and considerations](azure-stack-acs-differences.md).</span></span>

## <a name="azure-client-libraries"></a><span data-ttu-id="fe0da-110">Клиентские библиотеки Azure</span><span class="sxs-lookup"><span data-stu-id="fe0da-110">Azure client libraries</span></span>
<span data-ttu-id="fe0da-111">Hello поддерживается API-интерфейса REST для стека хранилища Azure имеет версию 2015-04-05.</span><span class="sxs-lookup"><span data-stu-id="fe0da-111">hello supported REST API version for Azure Stack Storage is 2015-04-05.</span></span> <span data-ttu-id="fe0da-112">Он не имеет полного контроля четности с последней версией hello hello API REST хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="fe0da-112">It doesn’t have full parity with hello latest version of hello Azure Storage REST API.</span></span> <span data-ttu-id="fe0da-113">Так что для клиентских библиотек хранилища hello следует toobe виду hello версии, совместимой с REST API 2015-04-05.</span><span class="sxs-lookup"><span data-stu-id="fe0da-113">So for hello storage client libraries, you need toobe aware of hello version that is compatible with REST API 2015-04-05.</span></span>


|<span data-ttu-id="fe0da-114">Клиентская библиотека</span><span class="sxs-lookup"><span data-stu-id="fe0da-114">Client library</span></span>|<span data-ttu-id="fe0da-115">Стек Azure поддерживаемая версия</span><span class="sxs-lookup"><span data-stu-id="fe0da-115">Azure Stack supported version</span></span>|<span data-ttu-id="fe0da-116">Ссылка</span><span class="sxs-lookup"><span data-stu-id="fe0da-116">Link</span></span>|<span data-ttu-id="fe0da-117">Спецификация конечной точки</span><span class="sxs-lookup"><span data-stu-id="fe0da-117">Endpoint specification</span></span>|
|---------|---------|---------|---------|
|<span data-ttu-id="fe0da-118">.NET</span><span class="sxs-lookup"><span data-stu-id="fe0da-118">.NET</span></span>     |<span data-ttu-id="fe0da-119">6.2.0</span><span class="sxs-lookup"><span data-stu-id="fe0da-119">6.2.0</span></span>|<span data-ttu-id="fe0da-120">Пакет NuGet:</span><span class="sxs-lookup"><span data-stu-id="fe0da-120">Nuget package:</span></span><br>[<span data-ttu-id="fe0da-121">https://www.NuGet.org/Packages/WindowsAzure.Storage/6.2.0</span><span class="sxs-lookup"><span data-stu-id="fe0da-121">https://www.nuget.org/packages/WindowsAzure.Storage/6.2.0</span></span>](https://www.nuget.org/packages/WindowsAzure.Storage/6.2.0)<br><br><span data-ttu-id="fe0da-122">Выпуск GitHub:</span><span class="sxs-lookup"><span data-stu-id="fe0da-122">GitHub release:</span></span><br>[<span data-ttu-id="fe0da-123">https://github.com/Azure/Azure-Storage-NET/releases/Tag/v6.2.1</span><span class="sxs-lookup"><span data-stu-id="fe0da-123">https://github.com/Azure/azure-storage-net/releases/tag/v6.2.1</span></span>](https://github.com/Azure/azure-storage-net/releases/tag/v6.2.1)|<span data-ttu-id="fe0da-124">файл app.config</span><span class="sxs-lookup"><span data-stu-id="fe0da-124">app.config file</span></span>|
|<span data-ttu-id="fe0da-125">Java</span><span class="sxs-lookup"><span data-stu-id="fe0da-125">Java</span></span>|<span data-ttu-id="fe0da-126">4.1.0</span><span class="sxs-lookup"><span data-stu-id="fe0da-126">4.1.0</span></span>|<span data-ttu-id="fe0da-127">Пакет maven:</span><span class="sxs-lookup"><span data-stu-id="fe0da-127">Maven package:</span></span><br>[<span data-ttu-id="fe0da-128">http://mvnrepository.com/Artifact/COM.Microsoft.Azure/Azure-Storage/4.1.0</span><span class="sxs-lookup"><span data-stu-id="fe0da-128">http://mvnrepository.com/artifact/com.microsoft.azure/azure-storage/4.1.0</span></span>](http://mvnrepository.com/artifact/com.microsoft.azure/azure-storage/4.1.0)<br><br><span data-ttu-id="fe0da-129">Выпуск GitHub:</span><span class="sxs-lookup"><span data-stu-id="fe0da-129">GitHub release:</span></span><br> [<span data-ttu-id="fe0da-130">https://github.com/Azure/Azure-Storage-Java/releases/Tag/v4.1.0</span><span class="sxs-lookup"><span data-stu-id="fe0da-130">https://github.com/Azure/azure-storage-java/releases/tag/v4.1.0</span></span>](https://github.com/Azure/azure-storage-java/releases/tag/v4.1.0)|<span data-ttu-id="fe0da-131">Настройка строки подключения</span><span class="sxs-lookup"><span data-stu-id="fe0da-131">Connection string setup</span></span>|
|<span data-ttu-id="fe0da-132">Node.js</span><span class="sxs-lookup"><span data-stu-id="fe0da-132">Node.js</span></span>     |<span data-ttu-id="fe0da-133">1.1.0</span><span class="sxs-lookup"><span data-stu-id="fe0da-133">1.1.0</span></span>|<span data-ttu-id="fe0da-134">Ссылка на NPM:</span><span class="sxs-lookup"><span data-stu-id="fe0da-134">NPM link:</span></span><br>[<span data-ttu-id="fe0da-135">https://www.npmjs.com/Package/Azure-Storage</span><span class="sxs-lookup"><span data-stu-id="fe0da-135">https://www.npmjs.com/package/azure-storage</span></span>](https://www.npmjs.com/package/azure-storage)<br><span data-ttu-id="fe0da-136">(запуска:`npm install azure-storage@1.1.0)`</span><span class="sxs-lookup"><span data-stu-id="fe0da-136">(run: `npm install azure-storage@1.1.0)`</span></span><br><br><span data-ttu-id="fe0da-137">Выпуск Github:</span><span class="sxs-lookup"><span data-stu-id="fe0da-137">Github release:</span></span><br>[<span data-ttu-id="fe0da-138">https://github.com/Azure/Azure-Storage-node/releases/Tag/1.1.0</span><span class="sxs-lookup"><span data-stu-id="fe0da-138">https://github.com/Azure/azure-storage-node/releases/tag/1.1.0</span></span>](https://github.com/Azure/azure-storage-node/releases/tag/1.1.0)|<span data-ttu-id="fe0da-139">Объявление экземпляра службы</span><span class="sxs-lookup"><span data-stu-id="fe0da-139">Service instance declaration</span></span>||<span data-ttu-id="fe0da-140">C++</span><span class="sxs-lookup"><span data-stu-id="fe0da-140">C++</span></span>|<span data-ttu-id="fe0da-141">2.4.0</span><span class="sxs-lookup"><span data-stu-id="fe0da-141">2.4.0</span></span>|<span data-ttu-id="fe0da-142">Пакет NuGet:</span><span class="sxs-lookup"><span data-stu-id="fe0da-142">Nuget package:</span></span><br>[<span data-ttu-id="fe0da-143">https://www.NuGet.org/Packages/wastorage.v140/2.4.0</span><span class="sxs-lookup"><span data-stu-id="fe0da-143">https://www.nuget.org/packages/wastorage.v140/2.4.0</span></span>](https://www.nuget.org/packages/wastorage.v140/2.4.0)<br><br><span data-ttu-id="fe0da-144">Выпуск GitHub:</span><span class="sxs-lookup"><span data-stu-id="fe0da-144">GitHub release:</span></span><br>[<span data-ttu-id="fe0da-145">https://github.com/Azure/Azure-Storage-cpp/releases/Tag/v2.4.0</span><span class="sxs-lookup"><span data-stu-id="fe0da-145">https://github.com/Azure/azure-storage-cpp/releases/tag/v2.4.0</span></span>](https://github.com/Azure/azure-storage-cpp/releases/tag/v2.4.0)|<span data-ttu-id="fe0da-146">Настройка строки подключения</span><span class="sxs-lookup"><span data-stu-id="fe0da-146">Connection string setup</span></span>|
|<span data-ttu-id="fe0da-147">C++</span><span class="sxs-lookup"><span data-stu-id="fe0da-147">C++</span></span>|<span data-ttu-id="fe0da-148">2.4.0</span><span class="sxs-lookup"><span data-stu-id="fe0da-148">2.4.0</span></span>|<span data-ttu-id="fe0da-149">Пакет NuGet:</span><span class="sxs-lookup"><span data-stu-id="fe0da-149">Nuget package:</span></span><br>[<span data-ttu-id="fe0da-150">https://www.NuGet.org/Packages/wastorage.v140/2.4.0</span><span class="sxs-lookup"><span data-stu-id="fe0da-150">https://www.nuget.org/packages/wastorage.v140/2.4.0</span></span>](https://www.nuget.org/packages/wastorage.v140/2.4.0)<br><br><span data-ttu-id="fe0da-151">Выпуск GitHub:</span><span class="sxs-lookup"><span data-stu-id="fe0da-151">GitHub release:</span></span><br>[<span data-ttu-id="fe0da-152">https://github.com/Azure/Azure-Storage-cpp/releases/Tag/v2.4.0</span><span class="sxs-lookup"><span data-stu-id="fe0da-152">https://github.com/Azure/azure-storage-cpp/releases/tag/v2.4.0</span></span>](https://github.com/Azure/azure-storage-cpp/releases/tag/v2.4.0)|<span data-ttu-id="fe0da-153">Настройка строки подключения</span><span class="sxs-lookup"><span data-stu-id="fe0da-153">Connection string setup</span></span>|
|<span data-ttu-id="fe0da-154">PHP</span><span class="sxs-lookup"><span data-stu-id="fe0da-154">PHP</span></span>|<span data-ttu-id="fe0da-155">0.15.0</span><span class="sxs-lookup"><span data-stu-id="fe0da-155">0.15.0</span></span>|<span data-ttu-id="fe0da-156">Выпуск GitHub:</span><span class="sxs-lookup"><span data-stu-id="fe0da-156">GitHub release:</span></span><br>[<span data-ttu-id="fe0da-157">https://github.com/Azure/Azure-Storage-PHP/releases/Tag/V0.15.0</span><span class="sxs-lookup"><span data-stu-id="fe0da-157">https://github.com/Azure/azure-storage-php/releases/tag/v0.15.0</span></span>](https://github.com/Azure/azure-storage-php/releases/tag/v0.15.0)<br><br><span data-ttu-id="fe0da-158">Установка через редактор (Подробности см. ниже)</span><span class="sxs-lookup"><span data-stu-id="fe0da-158">Install via Composer (see details below)</span></span>|<span data-ttu-id="fe0da-159">Настройка строки подключения</span><span class="sxs-lookup"><span data-stu-id="fe0da-159">Connection string setup</span></span>|
|<span data-ttu-id="fe0da-160">Python</span><span class="sxs-lookup"><span data-stu-id="fe0da-160">Python</span></span>     |<span data-ttu-id="fe0da-161">0.30.0</span><span class="sxs-lookup"><span data-stu-id="fe0da-161">0.30.0</span></span>|<span data-ttu-id="fe0da-162">Пакет PIP-адрес:</span><span class="sxs-lookup"><span data-stu-id="fe0da-162">PIP package:</span></span><br> [<span data-ttu-id="fe0da-163">https://pypi.Python.org/pypi/Azure-Storage/0.30.0</span><span class="sxs-lookup"><span data-stu-id="fe0da-163">https://pypi.python.org/pypi/azure-storage/0.30.0</span></span>](https://pypi.python.org/pypi/azure-storage/0.30.0)<br><span data-ttu-id="fe0da-164">(Запуска:`pip install -v azure-storage==0.30.0)`</span><span class="sxs-lookup"><span data-stu-id="fe0da-164">(Run: `pip install -v azure-storage==0.30.0)`</span></span><br><br><span data-ttu-id="fe0da-165">Выпуск GitHub:</span><span class="sxs-lookup"><span data-stu-id="fe0da-165">GitHub release:</span></span><br> [<span data-ttu-id="fe0da-166">https://github.com/Azure/Azure-Storage-Python/releases/Tag/V0.30.0</span><span class="sxs-lookup"><span data-stu-id="fe0da-166">https://github.com/Azure/azure-storage-python/releases/tag/v0.30.0</span></span>](https://github.com/Azure/azure-storage-python/releases/tag/v0.30.0)|<span data-ttu-id="fe0da-167">Объявление экземпляра службы</span><span class="sxs-lookup"><span data-stu-id="fe0da-167">Service instance declaration</span></span>|
|<span data-ttu-id="fe0da-168">Ruby</span><span class="sxs-lookup"><span data-stu-id="fe0da-168">Ruby</span></span>|<span data-ttu-id="fe0da-169">0.12.1</span><span class="sxs-lookup"><span data-stu-id="fe0da-169">0.12.1</span></span><br><span data-ttu-id="fe0da-170">Предварительный просмотр</span><span class="sxs-lookup"><span data-stu-id="fe0da-170">Preview</span></span>|<span data-ttu-id="fe0da-171">Пакет RubyGems:</span><span class="sxs-lookup"><span data-stu-id="fe0da-171">RubyGems package:</span></span><br> [<span data-ttu-id="fe0da-172">https://rubygems.org/gems/Azure-Storage/Versions/0.12.1.Preview</span><span class="sxs-lookup"><span data-stu-id="fe0da-172">https://rubygems.org/gems/azure-storage/versions/0.12.1.preview</span></span>](https://rubygems.org/gems/azure-storage/versions/0.12.1.preview)<br><br><span data-ttu-id="fe0da-173">Выпуск GitHub:</span><span class="sxs-lookup"><span data-stu-id="fe0da-173">GitHub release:</span></span><br> [<span data-ttu-id="fe0da-174">https://github.com/Azure/Azure-Storage-Ruby/releases/Tag/V0.12.1</span><span class="sxs-lookup"><span data-stu-id="fe0da-174">https://github.com/Azure/azure-storage-ruby/releases/tag/v0.12.1</span></span>](https://github.com/Azure/azure-storage-ruby/releases/tag/v0.12.1)|<span data-ttu-id="fe0da-175">Настройка строки подключения</span><span class="sxs-lookup"><span data-stu-id="fe0da-175">Connection string setup</span></span>|

> [!NOTE]
> <span data-ttu-id="fe0da-176">Сведения о PHP</span><span class="sxs-lookup"><span data-stu-id="fe0da-176">PHP details</span></span><br><br>
><span data-ttu-id="fe0da-177">tooinstall через редактор:</span><span class="sxs-lookup"><span data-stu-id="fe0da-177">tooinstall via Composer:</span></span>
>1. <span data-ttu-id="fe0da-178">Создайте файл с именем `composer.json` в корневом каталоге hello hello проекта со следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="fe0da-178">Create a file named `composer.json` in hello root of hello project with following code:</span></span><br>
>
>   ```
>   {
>       "require":{
>           "Microsoft/azure-storage":"0.15.0"
>        }
>    }
>   ```
>
>2. <span data-ttu-id="fe0da-179">Загрузить [composer.phar](http://getcomposer.org/composer.phar) в корневой каталог проекта hello.</span><span class="sxs-lookup"><span data-stu-id="fe0da-179">Download [composer.phar](http://getcomposer.org/composer.phar) into hello project root.</span></span>
>3. <span data-ttu-id="fe0da-180">Выполните команду `php composer.phar install`.</span><span class="sxs-lookup"><span data-stu-id="fe0da-180">Run: `php composer.phar install`.</span></span>
>


## <a name="endpoint-declaration"></a><span data-ttu-id="fe0da-181">Конечная точка объявления</span><span class="sxs-lookup"><span data-stu-id="fe0da-181">Endpoint declaration</span></span>
<span data-ttu-id="fe0da-182">Конечную точку Azure стек состоит из двух частей: hello имя домена, регион и hello Azure стека.</span><span class="sxs-lookup"><span data-stu-id="fe0da-182">An Azure Stack endpoint includes two parts: hello name of a region and hello Azure Stack domain.</span></span>
<span data-ttu-id="fe0da-183">В hello пакет средств разработки Azure стека является конечной точки по умолчанию hello **local.azurestack.external**.</span><span class="sxs-lookup"><span data-stu-id="fe0da-183">In hello Azure Stack Development Kit, hello default endpoint is **local.azurestack.external**.</span></span>
<span data-ttu-id="fe0da-184">Если вы не знаете о конечной точке, обратитесь к администратору облака.</span><span class="sxs-lookup"><span data-stu-id="fe0da-184">Contact your cloud administrator if you’re not sure about your endpoint.</span></span>

## <a name="examples"></a><span data-ttu-id="fe0da-185">Примеры</span><span class="sxs-lookup"><span data-stu-id="fe0da-185">Examples</span></span>


### <a name="net"></a><span data-ttu-id="fe0da-186">.NET</span><span class="sxs-lookup"><span data-stu-id="fe0da-186">.NET</span></span>

<span data-ttu-id="fe0da-187">Для стека Azure hello суффикс конечной точки должно быть указано в файле app.config hello:</span><span class="sxs-lookup"><span data-stu-id="fe0da-187">For Azure Stack, hello endpoint suffix is specified in hello app.config file:</span></span>

```
<add key="StorageConnectionString" 
value="DefaultEndpointsProtocol=https;AccountName=myaccount;AccountKey=mykey;
EndpointSuffix=local.azurestack.external;" />
```
### <a name="java"></a><span data-ttu-id="fe0da-188">Java</span><span class="sxs-lookup"><span data-stu-id="fe0da-188">Java</span></span>

<span data-ttu-id="fe0da-189">Для стека Azure hello суффикс конечной точки указывается в программе установки hello строки соединения:</span><span class="sxs-lookup"><span data-stu-id="fe0da-189">For Azure Stack, hello endpoint suffix is specified in hello setup of connection string:</span></span>

```
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key;" +
    "EndpointSuffix=local.azurestack.external";
```

### <a name="nodejs"></a><span data-ttu-id="fe0da-190">Node.js</span><span class="sxs-lookup"><span data-stu-id="fe0da-190">Node.js</span></span>

<span data-ttu-id="fe0da-191">Для стека Azure hello суффикс конечной точки должно быть указано в экземпляре объявления hello:</span><span class="sxs-lookup"><span data-stu-id="fe0da-191">For Azure Stack, hello endpoint suffix is specified in hello declaration instance:</span></span>

```
var blobSvc = azure.createBlobService('myaccount', 'mykey',
'myaccount.blob.local.azurestack.external');
```
### <a name="c"></a><span data-ttu-id="fe0da-192">C++</span><span class="sxs-lookup"><span data-stu-id="fe0da-192">C++</span></span>

<span data-ttu-id="fe0da-193">Для стека Azure hello суффикс конечной точки указывается в программе установки hello строки соединения:</span><span class="sxs-lookup"><span data-stu-id="fe0da-193">For Azure Stack, hello endpoint suffix is specified in hello setup of connection string:</span></span>

```
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;
AccountName=your_storage_account;
AccountKey=your_storage_account_key;
EndpointSuffix=local.azurestack.external"));
```

### <a name="php"></a><span data-ttu-id="fe0da-194">PHP</span><span class="sxs-lookup"><span data-stu-id="fe0da-194">PHP</span></span>

<span data-ttu-id="fe0da-195">Для стека Azure hello суффикс конечной точки указывается в программе установки hello строки соединения:</span><span class="sxs-lookup"><span data-stu-id="fe0da-195">For Azure Stack, hello endpoint suffix is specified in hello setup of connection string:</span></span>

```
$connectionString = 'BlobEndpoint=http://<storage account name>.blob.local.azurestack.external/;
QueueEndpoint=http:// <storage account name>.queue.local.azurestack.external/;
TableEndpoint=http:// <storage account name>.table.local.azurestack.external/;
AccountName=<storage account name>;AccountKey=<storage account key>'
```

### <a name="python"></a><span data-ttu-id="fe0da-196">Python</span><span class="sxs-lookup"><span data-stu-id="fe0da-196">Python</span></span>

<span data-ttu-id="fe0da-197">Для стека Azure hello суффикс конечной точки должно быть указано в экземпляре объявления hello:</span><span class="sxs-lookup"><span data-stu-id="fe0da-197">For Azure Stack, hello endpoint suffix is specified in hello declaration instance:</span></span>

```
block_blob_service = BlockBlobService(account_name='myaccount',
account_key='mykey',
endpoint_suffix='local.azurestack.external')
```
### <a name="ruby"></a><span data-ttu-id="fe0da-198">Ruby</span><span class="sxs-lookup"><span data-stu-id="fe0da-198">Ruby</span></span>

<span data-ttu-id="fe0da-199">Для стека Azure hello суффикс конечной точки указывается в программе установки hello строки соединения:</span><span class="sxs-lookup"><span data-stu-id="fe0da-199">For Azure Stack, hello endpoint suffix is specified in hello setup of connection string:</span></span>

```
set
AZURE_STORAGE_CONNECTION_STRING=DefaultEndpointsProtocol=https;
AccountName=myaccount;
AccountKey=mykey;
EndpointSuffix=local.azurestack.external
```

## <a name="blob-storage"></a><span data-ttu-id="fe0da-200">Хранилище BLOB-объектов</span><span class="sxs-lookup"><span data-stu-id="fe0da-200">Blob storage</span></span>

<span data-ttu-id="fe0da-201">Hello следующие учебники хранилища больших двоичных объектов Azure, применимые tooAzure стека.</span><span class="sxs-lookup"><span data-stu-id="fe0da-201">hello following Azure Blob storage tutorials are applicable tooAzure Stack.</span></span> <span data-ttu-id="fe0da-202">Примечание hello конкретной конечной точки суффикс требования для Azure стека, описанной в предыдущем hello [примеры](#examples) раздела.</span><span class="sxs-lookup"><span data-stu-id="fe0da-202">Note hello specific endpoint suffix requirement for Azure Stack described in hello previous [Examples](#examples) section.</span></span>

* [<span data-ttu-id="fe0da-203">Приступая к работе с хранилищем BLOB-объектов Azure с помощью .NET</span><span class="sxs-lookup"><span data-stu-id="fe0da-203">Get started with Azure Blob storage using .NET</span></span>](../storage/blobs/storage-dotnet-how-to-use-blobs.md)
* [<span data-ttu-id="fe0da-204">Как toouse хранилища BLOB-объектов из Java</span><span class="sxs-lookup"><span data-stu-id="fe0da-204">How toouse Blob storage from Java</span></span>](../storage/blobs/storage-java-how-to-use-blob-storage.md)
* [<span data-ttu-id="fe0da-205">Как toouse хранилища BLOB-объектов из Node.js</span><span class="sxs-lookup"><span data-stu-id="fe0da-205">How toouse Blob storage from Node.js</span></span>](../storage/blobs/storage-nodejs-how-to-use-blob-storage.md)
* [<span data-ttu-id="fe0da-206">Как toouse хранилища BLOB-объектов из C++</span><span class="sxs-lookup"><span data-stu-id="fe0da-206">How toouse Blob storage from C++</span></span>](../storage/blobs/storage-c-plus-plus-how-to-use-blobs.md)
* [<span data-ttu-id="fe0da-207">Как toouse хранилища BLOB-объектов из PHP</span><span class="sxs-lookup"><span data-stu-id="fe0da-207">How toouse Blob storage from PHP</span></span>](../storage/blobs/storage-php-how-to-use-blobs.md)
* [<span data-ttu-id="fe0da-208">Как toouse хранилища больших двоичных объектов Azure с Python</span><span class="sxs-lookup"><span data-stu-id="fe0da-208">How toouse Azure Blob storage from Python</span></span>](../storage/blobs/storage-python-how-to-use-blob-storage.md)
* [<span data-ttu-id="fe0da-209">Как toouse хранилища BLOB-объектов из Ruby</span><span class="sxs-lookup"><span data-stu-id="fe0da-209">How toouse Blob storage from Ruby</span></span>](../storage/blobs/storage-ruby-how-to-use-blob-storage.md)

## <a name="queue-storage"></a><span data-ttu-id="fe0da-210">Хранилище очередей</span><span class="sxs-lookup"><span data-stu-id="fe0da-210">Queue storage</span></span>

<span data-ttu-id="fe0da-211">Hello следующие учебники хранилища очередей Azure — применимо tooAzure стека.</span><span class="sxs-lookup"><span data-stu-id="fe0da-211">hello following Azure Queue storage tutorials are applicable tooAzure Stack.</span></span> <span data-ttu-id="fe0da-212">Примечание hello конкретной конечной точки суффикс требования для Azure стека, описанной в предыдущем hello [примеры](#examples) раздела.</span><span class="sxs-lookup"><span data-stu-id="fe0da-212">Note hello specific endpoint suffix requirement for Azure Stack described in hello previous [Examples](#examples) section.</span></span>

* [<span data-ttu-id="fe0da-213">Приступая к работе с хранилищем очередей Azure с помощью .NET</span><span class="sxs-lookup"><span data-stu-id="fe0da-213">Get started with Azure Queue storage using .NET</span></span>](../storage/queues/storage-dotnet-how-to-use-queues.md)
* [<span data-ttu-id="fe0da-214">Как toouse хранилища очередей из Java</span><span class="sxs-lookup"><span data-stu-id="fe0da-214">How toouse Queue storage from Java</span></span>](../storage/queues/storage-java-how-to-use-queue-storage.md)
* [<span data-ttu-id="fe0da-215">Как toouse хранилища очередей из Node.js</span><span class="sxs-lookup"><span data-stu-id="fe0da-215">How toouse Queue storage from Node.js</span></span>](../storage/queues/storage-nodejs-how-to-use-queues.md)
* [<span data-ttu-id="fe0da-216">Как toouse хранилища очередей из C++</span><span class="sxs-lookup"><span data-stu-id="fe0da-216">How toouse Queue storage from C++</span></span>](../storage/queues/storage-c-plus-plus-how-to-use-queues.md)
* [<span data-ttu-id="fe0da-217">Как toouse хранилища очередей из PHP</span><span class="sxs-lookup"><span data-stu-id="fe0da-217">How toouse Queue storage from PHP</span></span>](../storage/queues/storage-php-how-to-use-queues.md)
* [<span data-ttu-id="fe0da-218">Как toouse хранилища очередей из Python</span><span class="sxs-lookup"><span data-stu-id="fe0da-218">How toouse Queue storage from Python</span></span>](../storage/queues/storage-python-how-to-use-queue-storage.md)
* [<span data-ttu-id="fe0da-219">Как toouse хранилища очередей из Ruby</span><span class="sxs-lookup"><span data-stu-id="fe0da-219">How toouse Queue storage from Ruby</span></span>](../storage/queues/storage-ruby-how-to-use-queue-storage.md)


## <a name="table-storage"></a><span data-ttu-id="fe0da-220">Хранилище таблиц</span><span class="sxs-lookup"><span data-stu-id="fe0da-220">Table storage</span></span>

<span data-ttu-id="fe0da-221">Hello следующие учебники хранилища таблиц Azure, применимые tooAzure стека.</span><span class="sxs-lookup"><span data-stu-id="fe0da-221">hello following Azure Table storage tutorials are applicable tooAzure Stack.</span></span> <span data-ttu-id="fe0da-222">Примечание hello конкретной конечной точки суффикс требования для Azure стека, описанной в предыдущем hello [примеры](#examples) раздела.</span><span class="sxs-lookup"><span data-stu-id="fe0da-222">Note hello specific endpoint suffix requirement for Azure Stack described in hello previous [Examples](#examples) section.</span></span>

* [<span data-ttu-id="fe0da-223">Приступая к работе с хранилищем таблиц Azure с помощью .NET</span><span class="sxs-lookup"><span data-stu-id="fe0da-223">Get started with Azure Table storage using .NET</span></span>](../cosmos-db/table-storage-how-to-use-dotnet.md)
* [<span data-ttu-id="fe0da-224">Как toouse хранилище таблиц из Java</span><span class="sxs-lookup"><span data-stu-id="fe0da-224">How toouse Table storage from Java</span></span>](../cosmos-db/table-storage-how-to-use-java.md)
* [<span data-ttu-id="fe0da-225">Как toouse хранилище таблиц Azure из Node.js</span><span class="sxs-lookup"><span data-stu-id="fe0da-225">How toouse Azure Table storage from Node.js</span></span>](../cosmos-db/table-storage-how-to-use-nodejs.md)
* [<span data-ttu-id="fe0da-226">Как toouse хранилище таблиц из C++</span><span class="sxs-lookup"><span data-stu-id="fe0da-226">How toouse Table storage from C++</span></span>](../cosmos-db/table-storage-how-to-use-c-plus.md)
* [<span data-ttu-id="fe0da-227">Как toouse хранилище таблиц из PHP</span><span class="sxs-lookup"><span data-stu-id="fe0da-227">How toouse Table storage from PHP</span></span>](../cosmos-db/table-storage-how-to-use-php.md)
* [<span data-ttu-id="fe0da-228">Как toouse хранилища таблиц на Python</span><span class="sxs-lookup"><span data-stu-id="fe0da-228">How toouse Table storage in Python</span></span>](../cosmos-db/table-storage-how-to-use-python.md)
* [<span data-ttu-id="fe0da-229">Как toouse хранилище таблиц из Ruby</span><span class="sxs-lookup"><span data-stu-id="fe0da-229">How toouse Table storage from Ruby</span></span>](../cosmos-db/table-storage-how-to-use-ruby.md)

## <a name="next-steps"></a><span data-ttu-id="fe0da-230">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fe0da-230">Next steps</span></span>

* [<span data-ttu-id="fe0da-231">Введение tooMicrosoft хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="fe0da-231">Introduction tooMicrosoft Azure Storage</span></span>](../storage/common/storage-introduction.md)
