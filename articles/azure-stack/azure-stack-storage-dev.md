---
title: "Начало работы со средствами разработки стек хранилища Azure"
description: "Рекомендации, как приступить к работе со средствами разработки стек хранилища Azure"
services: azure-stack
author: xiaofmao
ms.author: xiaofmao
ms.date: 7/21/2017
ms.topic: get-started-article
ms.service: azure-stack
ms.openlocfilehash: a4c1c316022f992750fe60d28b9be61b17242a64
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-azure-stack-storage-development-tools"></a><span data-ttu-id="eca9e-103">Начало работы со средствами разработки стек хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="eca9e-103">Get started with Azure Stack Storage development tools</span></span> 

<span data-ttu-id="eca9e-104">Стека Microsoft Azure предоставляет набор служб хранилища, включая хранилище больших двоичных объектов Azure, таблиц и очередей.</span><span class="sxs-lookup"><span data-stu-id="eca9e-104">Microsoft Azure Stack provides a set of storage services, including Azure Blob, Table, and Queue storage.</span></span>

<span data-ttu-id="eca9e-105">Краткое руководство о том, как приступить к использованию средств разработки стек хранилища Azure в этой статье.</span><span class="sxs-lookup"><span data-stu-id="eca9e-105">This article provides quick guidance on how to start using Azure Stack Storage development tools.</span></span> <span data-ttu-id="eca9e-106">Более подробные сведения и примеры кода можно найти в хранилище Azure руководства.</span><span class="sxs-lookup"><span data-stu-id="eca9e-106">You can find more detailed information and sample code in the corresponding Azure Storage tutorials.</span></span>

<span data-ttu-id="eca9e-107">Существуют известные различия между хранилища Azure и стек хранилища Azure, включая определенные требования для каждой платформы.</span><span class="sxs-lookup"><span data-stu-id="eca9e-107">There are known differences between Azure Storage and Azure Stack Storage, including some specific requirements for each platform.</span></span> <span data-ttu-id="eca9e-108">Например существуют определенные клиентские библиотеки и требования суффикс конкретной конечной точки для стека Azure.</span><span class="sxs-lookup"><span data-stu-id="eca9e-108">For example, there are specific client libraries and specific endpoint suffix requirements for Azure Stack.</span></span> <span data-ttu-id="eca9e-109">Дополнительные сведения см. в разделе [стек хранилища Azure: различия и рекомендации](azure-stack-acs-differences.md).</span><span class="sxs-lookup"><span data-stu-id="eca9e-109">For more information, see [Azure Stack Storage: Differences and considerations](azure-stack-acs-differences.md).</span></span>

## <a name="azure-client-libraries"></a><span data-ttu-id="eca9e-110">Клиентские библиотеки Azure</span><span class="sxs-lookup"><span data-stu-id="eca9e-110">Azure client libraries</span></span>
<span data-ttu-id="eca9e-111">Поддерживаемая версия интерфейса API REST для стека хранилища Azure — 2015-04-05.</span><span class="sxs-lookup"><span data-stu-id="eca9e-111">The supported REST API version for Azure Stack Storage is 2015-04-05.</span></span> <span data-ttu-id="eca9e-112">Он не имеет полного контроля четности с последней версией API REST хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="eca9e-112">It doesn’t have full parity with the latest version of the Azure Storage REST API.</span></span> <span data-ttu-id="eca9e-113">Поэтому для клиентских библиотек хранилища, необходимо иметь в виду версию, совместимую с REST API 2015-04-05.</span><span class="sxs-lookup"><span data-stu-id="eca9e-113">So for the storage client libraries, you need to be aware of the version that is compatible with REST API 2015-04-05.</span></span>


|<span data-ttu-id="eca9e-114">Клиентская библиотека</span><span class="sxs-lookup"><span data-stu-id="eca9e-114">Client library</span></span>|<span data-ttu-id="eca9e-115">Стек Azure поддерживаемая версия</span><span class="sxs-lookup"><span data-stu-id="eca9e-115">Azure Stack supported version</span></span>|<span data-ttu-id="eca9e-116">Ссылка</span><span class="sxs-lookup"><span data-stu-id="eca9e-116">Link</span></span>|<span data-ttu-id="eca9e-117">Спецификация конечной точки</span><span class="sxs-lookup"><span data-stu-id="eca9e-117">Endpoint specification</span></span>|
|---------|---------|---------|---------|
|<span data-ttu-id="eca9e-118">.NET</span><span class="sxs-lookup"><span data-stu-id="eca9e-118">.NET</span></span>     |<span data-ttu-id="eca9e-119">6.2.0</span><span class="sxs-lookup"><span data-stu-id="eca9e-119">6.2.0</span></span>|<span data-ttu-id="eca9e-120">Пакет NuGet:</span><span class="sxs-lookup"><span data-stu-id="eca9e-120">Nuget package:</span></span><br>[<span data-ttu-id="eca9e-121">https://www.NuGet.org/Packages/WindowsAzure.Storage/6.2.0</span><span class="sxs-lookup"><span data-stu-id="eca9e-121">https://www.nuget.org/packages/WindowsAzure.Storage/6.2.0</span></span>](https://www.nuget.org/packages/WindowsAzure.Storage/6.2.0)<br><br><span data-ttu-id="eca9e-122">Выпуск GitHub:</span><span class="sxs-lookup"><span data-stu-id="eca9e-122">GitHub release:</span></span><br>[<span data-ttu-id="eca9e-123">https://github.com/Azure/Azure-Storage-NET/releases/Tag/v6.2.1</span><span class="sxs-lookup"><span data-stu-id="eca9e-123">https://github.com/Azure/azure-storage-net/releases/tag/v6.2.1</span></span>](https://github.com/Azure/azure-storage-net/releases/tag/v6.2.1)|<span data-ttu-id="eca9e-124">файл app.config</span><span class="sxs-lookup"><span data-stu-id="eca9e-124">app.config file</span></span>|
|<span data-ttu-id="eca9e-125">Java</span><span class="sxs-lookup"><span data-stu-id="eca9e-125">Java</span></span>|<span data-ttu-id="eca9e-126">4.1.0</span><span class="sxs-lookup"><span data-stu-id="eca9e-126">4.1.0</span></span>|<span data-ttu-id="eca9e-127">Пакет maven:</span><span class="sxs-lookup"><span data-stu-id="eca9e-127">Maven package:</span></span><br>[<span data-ttu-id="eca9e-128">http://mvnrepository.com/Artifact/COM.Microsoft.Azure/Azure-Storage/4.1.0</span><span class="sxs-lookup"><span data-stu-id="eca9e-128">http://mvnrepository.com/artifact/com.microsoft.azure/azure-storage/4.1.0</span></span>](http://mvnrepository.com/artifact/com.microsoft.azure/azure-storage/4.1.0)<br><br><span data-ttu-id="eca9e-129">Выпуск GitHub:</span><span class="sxs-lookup"><span data-stu-id="eca9e-129">GitHub release:</span></span><br> [<span data-ttu-id="eca9e-130">https://github.com/Azure/Azure-Storage-Java/releases/Tag/v4.1.0</span><span class="sxs-lookup"><span data-stu-id="eca9e-130">https://github.com/Azure/azure-storage-java/releases/tag/v4.1.0</span></span>](https://github.com/Azure/azure-storage-java/releases/tag/v4.1.0)|<span data-ttu-id="eca9e-131">Настройка строки подключения</span><span class="sxs-lookup"><span data-stu-id="eca9e-131">Connection string setup</span></span>|
|<span data-ttu-id="eca9e-132">Node.js</span><span class="sxs-lookup"><span data-stu-id="eca9e-132">Node.js</span></span>     |<span data-ttu-id="eca9e-133">1.1.0</span><span class="sxs-lookup"><span data-stu-id="eca9e-133">1.1.0</span></span>|<span data-ttu-id="eca9e-134">Ссылка на NPM:</span><span class="sxs-lookup"><span data-stu-id="eca9e-134">NPM link:</span></span><br>[<span data-ttu-id="eca9e-135">https://www.npmjs.com/Package/Azure-Storage</span><span class="sxs-lookup"><span data-stu-id="eca9e-135">https://www.npmjs.com/package/azure-storage</span></span>](https://www.npmjs.com/package/azure-storage)<br><span data-ttu-id="eca9e-136">(запуска:`npm install azure-storage@1.1.0)`</span><span class="sxs-lookup"><span data-stu-id="eca9e-136">(run: `npm install azure-storage@1.1.0)`</span></span><br><br><span data-ttu-id="eca9e-137">Выпуск Github:</span><span class="sxs-lookup"><span data-stu-id="eca9e-137">Github release:</span></span><br>[<span data-ttu-id="eca9e-138">https://github.com/Azure/Azure-Storage-node/releases/Tag/1.1.0</span><span class="sxs-lookup"><span data-stu-id="eca9e-138">https://github.com/Azure/azure-storage-node/releases/tag/1.1.0</span></span>](https://github.com/Azure/azure-storage-node/releases/tag/1.1.0)|<span data-ttu-id="eca9e-139">Объявление экземпляра службы</span><span class="sxs-lookup"><span data-stu-id="eca9e-139">Service instance declaration</span></span>||<span data-ttu-id="eca9e-140">C++</span><span class="sxs-lookup"><span data-stu-id="eca9e-140">C++</span></span>|<span data-ttu-id="eca9e-141">2.4.0</span><span class="sxs-lookup"><span data-stu-id="eca9e-141">2.4.0</span></span>|<span data-ttu-id="eca9e-142">Пакет NuGet:</span><span class="sxs-lookup"><span data-stu-id="eca9e-142">Nuget package:</span></span><br>[<span data-ttu-id="eca9e-143">https://www.NuGet.org/Packages/wastorage.v140/2.4.0</span><span class="sxs-lookup"><span data-stu-id="eca9e-143">https://www.nuget.org/packages/wastorage.v140/2.4.0</span></span>](https://www.nuget.org/packages/wastorage.v140/2.4.0)<br><br><span data-ttu-id="eca9e-144">Выпуск GitHub:</span><span class="sxs-lookup"><span data-stu-id="eca9e-144">GitHub release:</span></span><br>[<span data-ttu-id="eca9e-145">https://github.com/Azure/Azure-Storage-cpp/releases/Tag/v2.4.0</span><span class="sxs-lookup"><span data-stu-id="eca9e-145">https://github.com/Azure/azure-storage-cpp/releases/tag/v2.4.0</span></span>](https://github.com/Azure/azure-storage-cpp/releases/tag/v2.4.0)|<span data-ttu-id="eca9e-146">Настройка строки подключения</span><span class="sxs-lookup"><span data-stu-id="eca9e-146">Connection string setup</span></span>|
|<span data-ttu-id="eca9e-147">C++</span><span class="sxs-lookup"><span data-stu-id="eca9e-147">C++</span></span>|<span data-ttu-id="eca9e-148">2.4.0</span><span class="sxs-lookup"><span data-stu-id="eca9e-148">2.4.0</span></span>|<span data-ttu-id="eca9e-149">Пакет NuGet:</span><span class="sxs-lookup"><span data-stu-id="eca9e-149">Nuget package:</span></span><br>[<span data-ttu-id="eca9e-150">https://www.NuGet.org/Packages/wastorage.v140/2.4.0</span><span class="sxs-lookup"><span data-stu-id="eca9e-150">https://www.nuget.org/packages/wastorage.v140/2.4.0</span></span>](https://www.nuget.org/packages/wastorage.v140/2.4.0)<br><br><span data-ttu-id="eca9e-151">Выпуск GitHub:</span><span class="sxs-lookup"><span data-stu-id="eca9e-151">GitHub release:</span></span><br>[<span data-ttu-id="eca9e-152">https://github.com/Azure/Azure-Storage-cpp/releases/Tag/v2.4.0</span><span class="sxs-lookup"><span data-stu-id="eca9e-152">https://github.com/Azure/azure-storage-cpp/releases/tag/v2.4.0</span></span>](https://github.com/Azure/azure-storage-cpp/releases/tag/v2.4.0)|<span data-ttu-id="eca9e-153">Настройка строки подключения</span><span class="sxs-lookup"><span data-stu-id="eca9e-153">Connection string setup</span></span>|
|<span data-ttu-id="eca9e-154">PHP</span><span class="sxs-lookup"><span data-stu-id="eca9e-154">PHP</span></span>|<span data-ttu-id="eca9e-155">0.15.0</span><span class="sxs-lookup"><span data-stu-id="eca9e-155">0.15.0</span></span>|<span data-ttu-id="eca9e-156">Выпуск GitHub:</span><span class="sxs-lookup"><span data-stu-id="eca9e-156">GitHub release:</span></span><br>[<span data-ttu-id="eca9e-157">https://github.com/Azure/Azure-Storage-PHP/releases/Tag/V0.15.0</span><span class="sxs-lookup"><span data-stu-id="eca9e-157">https://github.com/Azure/azure-storage-php/releases/tag/v0.15.0</span></span>](https://github.com/Azure/azure-storage-php/releases/tag/v0.15.0)<br><br><span data-ttu-id="eca9e-158">Установка через редактор (Подробности см. ниже)</span><span class="sxs-lookup"><span data-stu-id="eca9e-158">Install via Composer (see details below)</span></span>|<span data-ttu-id="eca9e-159">Настройка строки подключения</span><span class="sxs-lookup"><span data-stu-id="eca9e-159">Connection string setup</span></span>|
|<span data-ttu-id="eca9e-160">Python</span><span class="sxs-lookup"><span data-stu-id="eca9e-160">Python</span></span>     |<span data-ttu-id="eca9e-161">0.30.0</span><span class="sxs-lookup"><span data-stu-id="eca9e-161">0.30.0</span></span>|<span data-ttu-id="eca9e-162">Пакет PIP-адрес:</span><span class="sxs-lookup"><span data-stu-id="eca9e-162">PIP package:</span></span><br> [<span data-ttu-id="eca9e-163">https://pypi.Python.org/pypi/Azure-Storage/0.30.0</span><span class="sxs-lookup"><span data-stu-id="eca9e-163">https://pypi.python.org/pypi/azure-storage/0.30.0</span></span>](https://pypi.python.org/pypi/azure-storage/0.30.0)<br><span data-ttu-id="eca9e-164">(Запуска:`pip install -v azure-storage==0.30.0)`</span><span class="sxs-lookup"><span data-stu-id="eca9e-164">(Run: `pip install -v azure-storage==0.30.0)`</span></span><br><br><span data-ttu-id="eca9e-165">Выпуск GitHub:</span><span class="sxs-lookup"><span data-stu-id="eca9e-165">GitHub release:</span></span><br> [<span data-ttu-id="eca9e-166">https://github.com/Azure/Azure-Storage-Python/releases/Tag/V0.30.0</span><span class="sxs-lookup"><span data-stu-id="eca9e-166">https://github.com/Azure/azure-storage-python/releases/tag/v0.30.0</span></span>](https://github.com/Azure/azure-storage-python/releases/tag/v0.30.0)|<span data-ttu-id="eca9e-167">Объявление экземпляра службы</span><span class="sxs-lookup"><span data-stu-id="eca9e-167">Service instance declaration</span></span>|
|<span data-ttu-id="eca9e-168">Ruby</span><span class="sxs-lookup"><span data-stu-id="eca9e-168">Ruby</span></span>|<span data-ttu-id="eca9e-169">0.12.1</span><span class="sxs-lookup"><span data-stu-id="eca9e-169">0.12.1</span></span><br><span data-ttu-id="eca9e-170">Предварительный просмотр</span><span class="sxs-lookup"><span data-stu-id="eca9e-170">Preview</span></span>|<span data-ttu-id="eca9e-171">Пакет RubyGems:</span><span class="sxs-lookup"><span data-stu-id="eca9e-171">RubyGems package:</span></span><br> [<span data-ttu-id="eca9e-172">https://rubygems.org/gems/Azure-Storage/Versions/0.12.1.Preview</span><span class="sxs-lookup"><span data-stu-id="eca9e-172">https://rubygems.org/gems/azure-storage/versions/0.12.1.preview</span></span>](https://rubygems.org/gems/azure-storage/versions/0.12.1.preview)<br><br><span data-ttu-id="eca9e-173">Выпуск GitHub:</span><span class="sxs-lookup"><span data-stu-id="eca9e-173">GitHub release:</span></span><br> [<span data-ttu-id="eca9e-174">https://github.com/Azure/Azure-Storage-Ruby/releases/Tag/V0.12.1</span><span class="sxs-lookup"><span data-stu-id="eca9e-174">https://github.com/Azure/azure-storage-ruby/releases/tag/v0.12.1</span></span>](https://github.com/Azure/azure-storage-ruby/releases/tag/v0.12.1)|<span data-ttu-id="eca9e-175">Настройка строки подключения</span><span class="sxs-lookup"><span data-stu-id="eca9e-175">Connection string setup</span></span>|

> [!NOTE]
> <span data-ttu-id="eca9e-176">Сведения о PHP</span><span class="sxs-lookup"><span data-stu-id="eca9e-176">PHP details</span></span><br><br>
><span data-ttu-id="eca9e-177">Установка через редактор:</span><span class="sxs-lookup"><span data-stu-id="eca9e-177">To install via Composer:</span></span>
>1. <span data-ttu-id="eca9e-178">Создайте файл с именем `composer.json` в корне проекта со следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="eca9e-178">Create a file named `composer.json` in the root of the project with following code:</span></span><br>
>
>   ```
>   {
>       "require":{
>           "Microsoft/azure-storage":"0.15.0"
>        }
>    }
>   ```
>
>2. <span data-ttu-id="eca9e-179">Загрузить [composer.phar](http://getcomposer.org/composer.phar) в корневой папке проекта.</span><span class="sxs-lookup"><span data-stu-id="eca9e-179">Download [composer.phar](http://getcomposer.org/composer.phar) into the project root.</span></span>
>3. <span data-ttu-id="eca9e-180">Выполните команду `php composer.phar install`.</span><span class="sxs-lookup"><span data-stu-id="eca9e-180">Run: `php composer.phar install`.</span></span>
>


## <a name="endpoint-declaration"></a><span data-ttu-id="eca9e-181">Конечная точка объявления</span><span class="sxs-lookup"><span data-stu-id="eca9e-181">Endpoint declaration</span></span>
<span data-ttu-id="eca9e-182">Конечную точку Azure стек состоит из двух частей: имя области и домена Azure стека.</span><span class="sxs-lookup"><span data-stu-id="eca9e-182">An Azure Stack endpoint includes two parts: the name of a region and the Azure Stack domain.</span></span>
<span data-ttu-id="eca9e-183">В комплекте разработки Azure стека, конечная точка по умолчанию — **local.azurestack.external**.</span><span class="sxs-lookup"><span data-stu-id="eca9e-183">In the Azure Stack Development Kit, the default endpoint is **local.azurestack.external**.</span></span>
<span data-ttu-id="eca9e-184">Если вы не знаете о конечной точке, обратитесь к администратору облака.</span><span class="sxs-lookup"><span data-stu-id="eca9e-184">Contact your cloud administrator if you’re not sure about your endpoint.</span></span>

## <a name="examples"></a><span data-ttu-id="eca9e-185">Примеры</span><span class="sxs-lookup"><span data-stu-id="eca9e-185">Examples</span></span>


### <a name="net"></a><span data-ttu-id="eca9e-186">.NET</span><span class="sxs-lookup"><span data-stu-id="eca9e-186">.NET</span></span>

<span data-ttu-id="eca9e-187">Стек Azure суффикс конечной точки необходимо указать в файле app.config:</span><span class="sxs-lookup"><span data-stu-id="eca9e-187">For Azure Stack, the endpoint suffix is specified in the app.config file:</span></span>

```
<add key="StorageConnectionString" 
value="DefaultEndpointsProtocol=https;AccountName=myaccount;AccountKey=mykey;
EndpointSuffix=local.azurestack.external;" />
```
### <a name="java"></a><span data-ttu-id="eca9e-188">Java</span><span class="sxs-lookup"><span data-stu-id="eca9e-188">Java</span></span>

<span data-ttu-id="eca9e-189">Стек Azure необходимо указать суффикс конечной точки в настройки строки подключения:</span><span class="sxs-lookup"><span data-stu-id="eca9e-189">For Azure Stack, the endpoint suffix is specified in the setup of connection string:</span></span>

```
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key;" +
    "EndpointSuffix=local.azurestack.external";
```

### <a name="nodejs"></a><span data-ttu-id="eca9e-190">Node.js</span><span class="sxs-lookup"><span data-stu-id="eca9e-190">Node.js</span></span>

<span data-ttu-id="eca9e-191">Стек Azure суффикс конечной точки необходимо указать в объявлении экземпляра:</span><span class="sxs-lookup"><span data-stu-id="eca9e-191">For Azure Stack, the endpoint suffix is specified in the declaration instance:</span></span>

```
var blobSvc = azure.createBlobService('myaccount', 'mykey',
'myaccount.blob.local.azurestack.external');
```
### <a name="c"></a><span data-ttu-id="eca9e-192">C++</span><span class="sxs-lookup"><span data-stu-id="eca9e-192">C++</span></span>

<span data-ttu-id="eca9e-193">Стек Azure необходимо указать суффикс конечной точки в настройки строки подключения:</span><span class="sxs-lookup"><span data-stu-id="eca9e-193">For Azure Stack, the endpoint suffix is specified in the setup of connection string:</span></span>

```
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;
AccountName=your_storage_account;
AccountKey=your_storage_account_key;
EndpointSuffix=local.azurestack.external"));
```

### <a name="php"></a><span data-ttu-id="eca9e-194">PHP</span><span class="sxs-lookup"><span data-stu-id="eca9e-194">PHP</span></span>

<span data-ttu-id="eca9e-195">Стек Azure необходимо указать суффикс конечной точки в настройки строки подключения:</span><span class="sxs-lookup"><span data-stu-id="eca9e-195">For Azure Stack, the endpoint suffix is specified in the setup of connection string:</span></span>

```
$connectionString = 'BlobEndpoint=http://<storage account name>.blob.local.azurestack.external/;
QueueEndpoint=http:// <storage account name>.queue.local.azurestack.external/;
TableEndpoint=http:// <storage account name>.table.local.azurestack.external/;
AccountName=<storage account name>;AccountKey=<storage account key>'
```

### <a name="python"></a><span data-ttu-id="eca9e-196">Python</span><span class="sxs-lookup"><span data-stu-id="eca9e-196">Python</span></span>

<span data-ttu-id="eca9e-197">Стек Azure суффикс конечной точки необходимо указать в объявлении экземпляра:</span><span class="sxs-lookup"><span data-stu-id="eca9e-197">For Azure Stack, the endpoint suffix is specified in the declaration instance:</span></span>

```
block_blob_service = BlockBlobService(account_name='myaccount',
account_key='mykey',
endpoint_suffix='local.azurestack.external')
```
### <a name="ruby"></a><span data-ttu-id="eca9e-198">Ruby</span><span class="sxs-lookup"><span data-stu-id="eca9e-198">Ruby</span></span>

<span data-ttu-id="eca9e-199">Стек Azure необходимо указать суффикс конечной точки в настройки строки подключения:</span><span class="sxs-lookup"><span data-stu-id="eca9e-199">For Azure Stack, the endpoint suffix is specified in the setup of connection string:</span></span>

```
set
AZURE_STORAGE_CONNECTION_STRING=DefaultEndpointsProtocol=https;
AccountName=myaccount;
AccountKey=mykey;
EndpointSuffix=local.azurestack.external
```

## <a name="blob-storage"></a><span data-ttu-id="eca9e-200">Хранилище BLOB-объектов</span><span class="sxs-lookup"><span data-stu-id="eca9e-200">Blob storage</span></span>

<span data-ttu-id="eca9e-201">Стек Azure применяются следующие учебники хранилища больших двоичных объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="eca9e-201">The following Azure Blob storage tutorials are applicable to Azure Stack.</span></span> <span data-ttu-id="eca9e-202">Определите требования суффикс конкретной конечной точки для Azure стека, описанный в предыдущем [примеры](#examples) раздела.</span><span class="sxs-lookup"><span data-stu-id="eca9e-202">Note the specific endpoint suffix requirement for Azure Stack described in the previous [Examples](#examples) section.</span></span>

* [<span data-ttu-id="eca9e-203">Приступая к работе с хранилищем BLOB-объектов Azure с помощью .NET</span><span class="sxs-lookup"><span data-stu-id="eca9e-203">Get started with Azure Blob storage using .NET</span></span>](../storage/blobs/storage-dotnet-how-to-use-blobs.md)
* [<span data-ttu-id="eca9e-204">Использование хранилища BLOB-объектов из Java</span><span class="sxs-lookup"><span data-stu-id="eca9e-204">How to use Blob storage from Java</span></span>](../storage/blobs/storage-java-how-to-use-blob-storage.md)
* [<span data-ttu-id="eca9e-205">Использование хранилища больших двоичных объектов из Node.js</span><span class="sxs-lookup"><span data-stu-id="eca9e-205">How to use Blob storage from Node.js</span></span>](../storage/blobs/storage-nodejs-how-to-use-blob-storage.md)
* [<span data-ttu-id="eca9e-206">Использование хранилища BLOB-объектов из C++</span><span class="sxs-lookup"><span data-stu-id="eca9e-206">How to use Blob storage from C++</span></span>](../storage/blobs/storage-c-plus-plus-how-to-use-blobs.md)
* [<span data-ttu-id="eca9e-207">Использование хранилища BLOB-объектов из PHP</span><span class="sxs-lookup"><span data-stu-id="eca9e-207">How to use Blob storage from PHP</span></span>](../storage/blobs/storage-php-how-to-use-blobs.md)
* [<span data-ttu-id="eca9e-208">Использование хранилища больших двоичных объектов Azure с Python</span><span class="sxs-lookup"><span data-stu-id="eca9e-208">How to use Azure Blob storage from Python</span></span>](../storage/blobs/storage-python-how-to-use-blob-storage.md)
* [<span data-ttu-id="eca9e-209">Использование хранилища BLOB-объектов из Ruby</span><span class="sxs-lookup"><span data-stu-id="eca9e-209">How to use Blob storage from Ruby</span></span>](../storage/blobs/storage-ruby-how-to-use-blob-storage.md)

## <a name="queue-storage"></a><span data-ttu-id="eca9e-210">Хранилище очередей</span><span class="sxs-lookup"><span data-stu-id="eca9e-210">Queue storage</span></span>

<span data-ttu-id="eca9e-211">В следующих учебниках хранилища очередей Azure относятся к Azure стека.</span><span class="sxs-lookup"><span data-stu-id="eca9e-211">The following Azure Queue storage tutorials are applicable to Azure Stack.</span></span> <span data-ttu-id="eca9e-212">Определите требования суффикс конкретной конечной точки для Azure стека, описанный в предыдущем [примеры](#examples) раздела.</span><span class="sxs-lookup"><span data-stu-id="eca9e-212">Note the specific endpoint suffix requirement for Azure Stack described in the previous [Examples](#examples) section.</span></span>

* [<span data-ttu-id="eca9e-213">Приступая к работе с хранилищем очередей Azure с помощью .NET</span><span class="sxs-lookup"><span data-stu-id="eca9e-213">Get started with Azure Queue storage using .NET</span></span>](../storage/queues/storage-dotnet-how-to-use-queues.md)
* [<span data-ttu-id="eca9e-214">Использование хранилища очередей из Java</span><span class="sxs-lookup"><span data-stu-id="eca9e-214">How to use Queue storage from Java</span></span>](../storage/queues/storage-java-how-to-use-queue-storage.md)
* [<span data-ttu-id="eca9e-215">Использование хранилища очередей из Node.js</span><span class="sxs-lookup"><span data-stu-id="eca9e-215">How to use Queue storage from Node.js</span></span>](../storage/queues/storage-nodejs-how-to-use-queues.md)
* [<span data-ttu-id="eca9e-216">Использование хранилища очередей из C++</span><span class="sxs-lookup"><span data-stu-id="eca9e-216">How to use Queue storage from C++</span></span>](../storage/queues/storage-c-plus-plus-how-to-use-queues.md)
* [<span data-ttu-id="eca9e-217">Использование хранилища очередей из PHP</span><span class="sxs-lookup"><span data-stu-id="eca9e-217">How to use Queue storage from PHP</span></span>](../storage/queues/storage-php-how-to-use-queues.md)
* [<span data-ttu-id="eca9e-218">Использование хранилища очередей из Python</span><span class="sxs-lookup"><span data-stu-id="eca9e-218">How to use Queue storage from Python</span></span>](../storage/queues/storage-python-how-to-use-queue-storage.md)
* [<span data-ttu-id="eca9e-219">Использование хранилища очередей из Ruby</span><span class="sxs-lookup"><span data-stu-id="eca9e-219">How to use Queue storage from Ruby</span></span>](../storage/queues/storage-ruby-how-to-use-queue-storage.md)


## <a name="table-storage"></a><span data-ttu-id="eca9e-220">Хранилище таблиц</span><span class="sxs-lookup"><span data-stu-id="eca9e-220">Table storage</span></span>

<span data-ttu-id="eca9e-221">В следующих учебниках хранилища таблиц Azure относятся к Azure стека.</span><span class="sxs-lookup"><span data-stu-id="eca9e-221">The following Azure Table storage tutorials are applicable to Azure Stack.</span></span> <span data-ttu-id="eca9e-222">Определите требования суффикс конкретной конечной точки для Azure стека, описанный в предыдущем [примеры](#examples) раздела.</span><span class="sxs-lookup"><span data-stu-id="eca9e-222">Note the specific endpoint suffix requirement for Azure Stack described in the previous [Examples](#examples) section.</span></span>

* [<span data-ttu-id="eca9e-223">Приступая к работе с хранилищем таблиц Azure с помощью .NET</span><span class="sxs-lookup"><span data-stu-id="eca9e-223">Get started with Azure Table storage using .NET</span></span>](../cosmos-db/table-storage-how-to-use-dotnet.md)
* [<span data-ttu-id="eca9e-224">Использование табличного хранилища из Java</span><span class="sxs-lookup"><span data-stu-id="eca9e-224">How to use Table storage from Java</span></span>](../cosmos-db/table-storage-how-to-use-java.md)
* [<span data-ttu-id="eca9e-225">Использование хранилища Azure таблицы из Node.js</span><span class="sxs-lookup"><span data-stu-id="eca9e-225">How to use Azure Table storage from Node.js</span></span>](../cosmos-db/table-storage-how-to-use-nodejs.md)
* [<span data-ttu-id="eca9e-226">Как использовать хранилище таблиц из C++</span><span class="sxs-lookup"><span data-stu-id="eca9e-226">How to use Table storage from C++</span></span>](../cosmos-db/table-storage-how-to-use-c-plus.md)
* [<span data-ttu-id="eca9e-227">Использование табличного хранилища из PHP</span><span class="sxs-lookup"><span data-stu-id="eca9e-227">How to use Table storage from PHP</span></span>](../cosmos-db/table-storage-how-to-use-php.md)
* [<span data-ttu-id="eca9e-228">Как использовать хранилище таблиц в Python</span><span class="sxs-lookup"><span data-stu-id="eca9e-228">How to use Table storage in Python</span></span>](../cosmos-db/table-storage-how-to-use-python.md)
* [<span data-ttu-id="eca9e-229">Использование табличного хранилища из Ruby</span><span class="sxs-lookup"><span data-stu-id="eca9e-229">How to use Table storage from Ruby</span></span>](../cosmos-db/table-storage-how-to-use-ruby.md)

## <a name="next-steps"></a><span data-ttu-id="eca9e-230">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="eca9e-230">Next steps</span></span>

* [<span data-ttu-id="eca9e-231">Введение в службу хранилища Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="eca9e-231">Introduction to Microsoft Azure Storage</span></span>](../storage/common/storage-introduction.md)