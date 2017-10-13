---
title: "Начало работы со средствами разработки стек хранилища Azure"
description: "Рекомендации, как приступить к работе со средствами разработки стек хранилища Azure"
services: azure-stack
author: xiaofmao
ms.author: xiaofmao
ms.date: 9/25/2017
ms.topic: get-started-article
ms.service: azure-stack
ms.openlocfilehash: 5b2898c64c0f1b5d804e63fa4e4e1218fa7a672c
ms.sourcegitcommit: 90e2cced6a773b1b52f999ba73cd8877305d270b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="get-started-with-azure-stack-storage-development-tools"></a><span data-ttu-id="ca3c8-103">Начало работы со средствами разработки стек хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="ca3c8-103">Get started with Azure Stack Storage development tools</span></span>

<span data-ttu-id="ca3c8-104">*Применяется к: стек Azure интегрированных систем и пакет средств разработки стек Azure*</span><span class="sxs-lookup"><span data-stu-id="ca3c8-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>


<span data-ttu-id="ca3c8-105">Стека Microsoft Azure предоставляет набор служб хранилища, включая хранилище больших двоичных объектов Azure, таблиц и очередей.</span><span class="sxs-lookup"><span data-stu-id="ca3c8-105">Microsoft Azure Stack provides a set of storage services, including Azure Blob, Table, and Queue storage.</span></span>

<span data-ttu-id="ca3c8-106">Краткое руководство о том, как приступить к использованию средств разработки стек хранилища Azure в этой статье.</span><span class="sxs-lookup"><span data-stu-id="ca3c8-106">This article provides quick guidance on how to start using Azure Stack Storage development tools.</span></span> <span data-ttu-id="ca3c8-107">Более подробные сведения и примеры кода можно найти в хранилище Azure руководства.</span><span class="sxs-lookup"><span data-stu-id="ca3c8-107">You can find more detailed information and sample code in the corresponding Azure Storage tutorials.</span></span>

<span data-ttu-id="ca3c8-108">Существуют известные различия между хранилища Azure и стек хранилища Azure, включая определенные требования для каждой платформы.</span><span class="sxs-lookup"><span data-stu-id="ca3c8-108">There are known differences between Azure Storage and Azure Stack Storage, including some specific requirements for each platform.</span></span> <span data-ttu-id="ca3c8-109">Например существуют определенные клиентские библиотеки и требования суффикс конкретной конечной точки для стека Azure.</span><span class="sxs-lookup"><span data-stu-id="ca3c8-109">For example, there are specific client libraries and specific endpoint suffix requirements for Azure Stack.</span></span> <span data-ttu-id="ca3c8-110">Дополнительные сведения см. в разделе [стек хранилища Azure: различия и рекомендации](azure-stack-acs-differences.md).</span><span class="sxs-lookup"><span data-stu-id="ca3c8-110">For more information, see [Azure Stack Storage: Differences and considerations](azure-stack-acs-differences.md).</span></span>

## <a name="azure-client-libraries"></a><span data-ttu-id="ca3c8-111">Клиентские библиотеки Azure</span><span class="sxs-lookup"><span data-stu-id="ca3c8-111">Azure client libraries</span></span>
<span data-ttu-id="ca3c8-112">Поддерживаемая версия интерфейса API REST для стека хранилища Azure — 2015-04-05.</span><span class="sxs-lookup"><span data-stu-id="ca3c8-112">The supported REST API version for Azure Stack Storage is 2015-04-05.</span></span> <span data-ttu-id="ca3c8-113">Он не имеет полного контроля четности с последней версией API REST хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="ca3c8-113">It doesn’t have full parity with the latest version of the Azure Storage REST API.</span></span> <span data-ttu-id="ca3c8-114">Поэтому для клиентских библиотек хранилища, необходимо иметь в виду версию, совместимую с REST API 2015-04-05.</span><span class="sxs-lookup"><span data-stu-id="ca3c8-114">So for the storage client libraries, you need to be aware of the version that is compatible with REST API 2015-04-05.</span></span>


|<span data-ttu-id="ca3c8-115">Клиентская библиотека</span><span class="sxs-lookup"><span data-stu-id="ca3c8-115">Client library</span></span>|<span data-ttu-id="ca3c8-116">Стек Azure поддерживаемая версия</span><span class="sxs-lookup"><span data-stu-id="ca3c8-116">Azure Stack supported version</span></span>|<span data-ttu-id="ca3c8-117">Ссылка</span><span class="sxs-lookup"><span data-stu-id="ca3c8-117">Link</span></span>|<span data-ttu-id="ca3c8-118">Спецификация конечной точки</span><span class="sxs-lookup"><span data-stu-id="ca3c8-118">Endpoint specification</span></span>|
|---------|---------|---------|---------|
|<span data-ttu-id="ca3c8-119">.NET</span><span class="sxs-lookup"><span data-stu-id="ca3c8-119">.NET</span></span>     |<span data-ttu-id="ca3c8-120">6.2.0</span><span class="sxs-lookup"><span data-stu-id="ca3c8-120">6.2.0</span></span>|<span data-ttu-id="ca3c8-121">Пакет NuGet:</span><span class="sxs-lookup"><span data-stu-id="ca3c8-121">Nuget package:</span></span><br>[<span data-ttu-id="ca3c8-122">https://www.NuGet.org/Packages/WindowsAzure.Storage/6.2.0</span><span class="sxs-lookup"><span data-stu-id="ca3c8-122">https://www.nuget.org/packages/WindowsAzure.Storage/6.2.0</span></span>](https://www.nuget.org/packages/WindowsAzure.Storage/6.2.0)<br><br><span data-ttu-id="ca3c8-123">Выпуск GitHub:</span><span class="sxs-lookup"><span data-stu-id="ca3c8-123">GitHub release:</span></span><br>[<span data-ttu-id="ca3c8-124">https://github.com/Azure/Azure-Storage-NET/releases/Tag/v6.2.1</span><span class="sxs-lookup"><span data-stu-id="ca3c8-124">https://github.com/Azure/azure-storage-net/releases/tag/v6.2.1</span></span>](https://github.com/Azure/azure-storage-net/releases/tag/v6.2.1)|<span data-ttu-id="ca3c8-125">файл app.config</span><span class="sxs-lookup"><span data-stu-id="ca3c8-125">app.config file</span></span>|
|<span data-ttu-id="ca3c8-126">Java</span><span class="sxs-lookup"><span data-stu-id="ca3c8-126">Java</span></span>|<span data-ttu-id="ca3c8-127">4.1.0</span><span class="sxs-lookup"><span data-stu-id="ca3c8-127">4.1.0</span></span>|<span data-ttu-id="ca3c8-128">Пакет maven:</span><span class="sxs-lookup"><span data-stu-id="ca3c8-128">Maven package:</span></span><br>[<span data-ttu-id="ca3c8-129">http://mvnrepository.com/Artifact/COM.Microsoft.Azure/Azure-Storage/4.1.0</span><span class="sxs-lookup"><span data-stu-id="ca3c8-129">http://mvnrepository.com/artifact/com.microsoft.azure/azure-storage/4.1.0</span></span>](http://mvnrepository.com/artifact/com.microsoft.azure/azure-storage/4.1.0)<br><br><span data-ttu-id="ca3c8-130">Выпуск GitHub:</span><span class="sxs-lookup"><span data-stu-id="ca3c8-130">GitHub release:</span></span><br> [<span data-ttu-id="ca3c8-131">https://github.com/Azure/Azure-Storage-Java/releases/Tag/v4.1.0</span><span class="sxs-lookup"><span data-stu-id="ca3c8-131">https://github.com/Azure/azure-storage-java/releases/tag/v4.1.0</span></span>](https://github.com/Azure/azure-storage-java/releases/tag/v4.1.0)|<span data-ttu-id="ca3c8-132">Настройка строки подключения</span><span class="sxs-lookup"><span data-stu-id="ca3c8-132">Connection string setup</span></span>|
|<span data-ttu-id="ca3c8-133">Node.js</span><span class="sxs-lookup"><span data-stu-id="ca3c8-133">Node.js</span></span>     |<span data-ttu-id="ca3c8-134">1.1.0</span><span class="sxs-lookup"><span data-stu-id="ca3c8-134">1.1.0</span></span>|<span data-ttu-id="ca3c8-135">Ссылка на NPM:</span><span class="sxs-lookup"><span data-stu-id="ca3c8-135">NPM link:</span></span><br>[<span data-ttu-id="ca3c8-136">https://www.npmjs.com/Package/Azure-Storage</span><span class="sxs-lookup"><span data-stu-id="ca3c8-136">https://www.npmjs.com/package/azure-storage</span></span>](https://www.npmjs.com/package/azure-storage)<br><span data-ttu-id="ca3c8-137">(запуска:`npm install azure-storage@1.1.0)`</span><span class="sxs-lookup"><span data-stu-id="ca3c8-137">(run: `npm install azure-storage@1.1.0)`</span></span><br><br><span data-ttu-id="ca3c8-138">Выпуск Github:</span><span class="sxs-lookup"><span data-stu-id="ca3c8-138">Github release:</span></span><br>[<span data-ttu-id="ca3c8-139">https://github.com/Azure/Azure-Storage-node/releases/Tag/1.1.0</span><span class="sxs-lookup"><span data-stu-id="ca3c8-139">https://github.com/Azure/azure-storage-node/releases/tag/1.1.0</span></span>](https://github.com/Azure/azure-storage-node/releases/tag/1.1.0)|<span data-ttu-id="ca3c8-140">Объявление экземпляра службы</span><span class="sxs-lookup"><span data-stu-id="ca3c8-140">Service instance declaration</span></span>||<span data-ttu-id="ca3c8-141">C++</span><span class="sxs-lookup"><span data-stu-id="ca3c8-141">C++</span></span>|<span data-ttu-id="ca3c8-142">2.4.0</span><span class="sxs-lookup"><span data-stu-id="ca3c8-142">2.4.0</span></span>|<span data-ttu-id="ca3c8-143">Пакет NuGet:</span><span class="sxs-lookup"><span data-stu-id="ca3c8-143">Nuget package:</span></span><br>[<span data-ttu-id="ca3c8-144">https://www.NuGet.org/Packages/wastorage.v140/2.4.0</span><span class="sxs-lookup"><span data-stu-id="ca3c8-144">https://www.nuget.org/packages/wastorage.v140/2.4.0</span></span>](https://www.nuget.org/packages/wastorage.v140/2.4.0)<br><br><span data-ttu-id="ca3c8-145">Выпуск GitHub:</span><span class="sxs-lookup"><span data-stu-id="ca3c8-145">GitHub release:</span></span><br>[<span data-ttu-id="ca3c8-146">https://github.com/Azure/Azure-Storage-cpp/releases/Tag/v2.4.0</span><span class="sxs-lookup"><span data-stu-id="ca3c8-146">https://github.com/Azure/azure-storage-cpp/releases/tag/v2.4.0</span></span>](https://github.com/Azure/azure-storage-cpp/releases/tag/v2.4.0)|<span data-ttu-id="ca3c8-147">Настройка строки подключения</span><span class="sxs-lookup"><span data-stu-id="ca3c8-147">Connection string setup</span></span>|
|<span data-ttu-id="ca3c8-148">C++</span><span class="sxs-lookup"><span data-stu-id="ca3c8-148">C++</span></span>|<span data-ttu-id="ca3c8-149">2.4.0</span><span class="sxs-lookup"><span data-stu-id="ca3c8-149">2.4.0</span></span>|<span data-ttu-id="ca3c8-150">Пакет NuGet:</span><span class="sxs-lookup"><span data-stu-id="ca3c8-150">Nuget package:</span></span><br>[<span data-ttu-id="ca3c8-151">https://www.NuGet.org/Packages/wastorage.v140/2.4.0</span><span class="sxs-lookup"><span data-stu-id="ca3c8-151">https://www.nuget.org/packages/wastorage.v140/2.4.0</span></span>](https://www.nuget.org/packages/wastorage.v140/2.4.0)<br><br><span data-ttu-id="ca3c8-152">Выпуск GitHub:</span><span class="sxs-lookup"><span data-stu-id="ca3c8-152">GitHub release:</span></span><br>[<span data-ttu-id="ca3c8-153">https://github.com/Azure/Azure-Storage-cpp/releases/Tag/v2.4.0</span><span class="sxs-lookup"><span data-stu-id="ca3c8-153">https://github.com/Azure/azure-storage-cpp/releases/tag/v2.4.0</span></span>](https://github.com/Azure/azure-storage-cpp/releases/tag/v2.4.0)|<span data-ttu-id="ca3c8-154">Настройка строки подключения</span><span class="sxs-lookup"><span data-stu-id="ca3c8-154">Connection string setup</span></span>|
|<span data-ttu-id="ca3c8-155">PHP</span><span class="sxs-lookup"><span data-stu-id="ca3c8-155">PHP</span></span>|<span data-ttu-id="ca3c8-156">0.15.0</span><span class="sxs-lookup"><span data-stu-id="ca3c8-156">0.15.0</span></span>|<span data-ttu-id="ca3c8-157">Выпуск GitHub:</span><span class="sxs-lookup"><span data-stu-id="ca3c8-157">GitHub release:</span></span><br>[<span data-ttu-id="ca3c8-158">https://github.com/Azure/Azure-Storage-PHP/releases/Tag/V0.15.0</span><span class="sxs-lookup"><span data-stu-id="ca3c8-158">https://github.com/Azure/azure-storage-php/releases/tag/v0.15.0</span></span>](https://github.com/Azure/azure-storage-php/releases/tag/v0.15.0)<br><br><span data-ttu-id="ca3c8-159">Установка через редактор (Подробности см. ниже)</span><span class="sxs-lookup"><span data-stu-id="ca3c8-159">Install via Composer (see details below)</span></span>|<span data-ttu-id="ca3c8-160">Настройка строки подключения</span><span class="sxs-lookup"><span data-stu-id="ca3c8-160">Connection string setup</span></span>|
|<span data-ttu-id="ca3c8-161">Python</span><span class="sxs-lookup"><span data-stu-id="ca3c8-161">Python</span></span>     |<span data-ttu-id="ca3c8-162">0.30.0</span><span class="sxs-lookup"><span data-stu-id="ca3c8-162">0.30.0</span></span>|<span data-ttu-id="ca3c8-163">Пакет PIP-адрес:</span><span class="sxs-lookup"><span data-stu-id="ca3c8-163">PIP package:</span></span><br> [<span data-ttu-id="ca3c8-164">https://pypi.Python.org/pypi/Azure-Storage/0.30.0</span><span class="sxs-lookup"><span data-stu-id="ca3c8-164">https://pypi.python.org/pypi/azure-storage/0.30.0</span></span>](https://pypi.python.org/pypi/azure-storage/0.30.0)<br><span data-ttu-id="ca3c8-165">(Запуска:`pip install -v azure-storage==0.30.0)`</span><span class="sxs-lookup"><span data-stu-id="ca3c8-165">(Run: `pip install -v azure-storage==0.30.0)`</span></span><br><br><span data-ttu-id="ca3c8-166">Выпуск GitHub:</span><span class="sxs-lookup"><span data-stu-id="ca3c8-166">GitHub release:</span></span><br> [<span data-ttu-id="ca3c8-167">https://github.com/Azure/Azure-Storage-Python/releases/Tag/V0.30.0</span><span class="sxs-lookup"><span data-stu-id="ca3c8-167">https://github.com/Azure/azure-storage-python/releases/tag/v0.30.0</span></span>](https://github.com/Azure/azure-storage-python/releases/tag/v0.30.0)|<span data-ttu-id="ca3c8-168">Объявление экземпляра службы</span><span class="sxs-lookup"><span data-stu-id="ca3c8-168">Service instance declaration</span></span>|
|<span data-ttu-id="ca3c8-169">Ruby</span><span class="sxs-lookup"><span data-stu-id="ca3c8-169">Ruby</span></span>|<span data-ttu-id="ca3c8-170">0.12.1</span><span class="sxs-lookup"><span data-stu-id="ca3c8-170">0.12.1</span></span><br><span data-ttu-id="ca3c8-171">Предварительный просмотр</span><span class="sxs-lookup"><span data-stu-id="ca3c8-171">Preview</span></span>|<span data-ttu-id="ca3c8-172">Пакет RubyGems:</span><span class="sxs-lookup"><span data-stu-id="ca3c8-172">RubyGems package:</span></span><br> [<span data-ttu-id="ca3c8-173">https://rubygems.org/gems/Azure-Storage/Versions/0.12.1.Preview</span><span class="sxs-lookup"><span data-stu-id="ca3c8-173">https://rubygems.org/gems/azure-storage/versions/0.12.1.preview</span></span>](https://rubygems.org/gems/azure-storage/versions/0.12.1.preview)<br><br><span data-ttu-id="ca3c8-174">Выпуск GitHub:</span><span class="sxs-lookup"><span data-stu-id="ca3c8-174">GitHub release:</span></span><br> [<span data-ttu-id="ca3c8-175">https://github.com/Azure/Azure-Storage-Ruby/releases/Tag/V0.12.1</span><span class="sxs-lookup"><span data-stu-id="ca3c8-175">https://github.com/Azure/azure-storage-ruby/releases/tag/v0.12.1</span></span>](https://github.com/Azure/azure-storage-ruby/releases/tag/v0.12.1)|<span data-ttu-id="ca3c8-176">Настройка строки подключения</span><span class="sxs-lookup"><span data-stu-id="ca3c8-176">Connection string setup</span></span>|

> [!NOTE]
> <span data-ttu-id="ca3c8-177">Сведения о PHP</span><span class="sxs-lookup"><span data-stu-id="ca3c8-177">PHP details</span></span><br><br>
><span data-ttu-id="ca3c8-178">Установка через редактор:</span><span class="sxs-lookup"><span data-stu-id="ca3c8-178">To install via Composer:</span></span>
>1. <span data-ttu-id="ca3c8-179">Создайте файл с именем `composer.json` в корне проекта со следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="ca3c8-179">Create a file named `composer.json` in the root of the project with following code:</span></span><br>
>
>   ```
>   {
>       "require":{
>           "Microsoft/azure-storage":"0.15.0"
>        }
>    }
>   ```
>
>2. <span data-ttu-id="ca3c8-180">Загрузить [composer.phar](http://getcomposer.org/composer.phar) в корневой папке проекта.</span><span class="sxs-lookup"><span data-stu-id="ca3c8-180">Download [composer.phar](http://getcomposer.org/composer.phar) into the project root.</span></span>
>3. <span data-ttu-id="ca3c8-181">Выполните команду `php composer.phar install`.</span><span class="sxs-lookup"><span data-stu-id="ca3c8-181">Run: `php composer.phar install`.</span></span>
>


## <a name="endpoint-declaration"></a><span data-ttu-id="ca3c8-182">Конечная точка объявления</span><span class="sxs-lookup"><span data-stu-id="ca3c8-182">Endpoint declaration</span></span>
<span data-ttu-id="ca3c8-183">Конечную точку Azure стек состоит из двух частей: имя области и домена Azure стека.</span><span class="sxs-lookup"><span data-stu-id="ca3c8-183">An Azure Stack endpoint includes two parts: the name of a region and the Azure Stack domain.</span></span>
<span data-ttu-id="ca3c8-184">В комплекте разработки Azure стека, конечная точка по умолчанию — **local.azurestack.external**.</span><span class="sxs-lookup"><span data-stu-id="ca3c8-184">In the Azure Stack Development Kit, the default endpoint is **local.azurestack.external**.</span></span>
<span data-ttu-id="ca3c8-185">Если вы не знаете о конечной точке, обратитесь к администратору облака.</span><span class="sxs-lookup"><span data-stu-id="ca3c8-185">Contact your cloud administrator if you’re not sure about your endpoint.</span></span>

## <a name="examples"></a><span data-ttu-id="ca3c8-186">Примеры</span><span class="sxs-lookup"><span data-stu-id="ca3c8-186">Examples</span></span>


### <a name="net"></a><span data-ttu-id="ca3c8-187">.NET</span><span class="sxs-lookup"><span data-stu-id="ca3c8-187">.NET</span></span>

<span data-ttu-id="ca3c8-188">Стек Azure суффикс конечной точки необходимо указать в файле app.config:</span><span class="sxs-lookup"><span data-stu-id="ca3c8-188">For Azure Stack, the endpoint suffix is specified in the app.config file:</span></span>

```
<add key="StorageConnectionString" 
value="DefaultEndpointsProtocol=https;AccountName=myaccount;AccountKey=mykey;
EndpointSuffix=local.azurestack.external;" />
```
### <a name="java"></a><span data-ttu-id="ca3c8-189">Java</span><span class="sxs-lookup"><span data-stu-id="ca3c8-189">Java</span></span>

<span data-ttu-id="ca3c8-190">Стек Azure необходимо указать суффикс конечной точки в настройки строки подключения:</span><span class="sxs-lookup"><span data-stu-id="ca3c8-190">For Azure Stack, the endpoint suffix is specified in the setup of connection string:</span></span>

```
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key;" +
    "EndpointSuffix=local.azurestack.external";
```

### <a name="nodejs"></a><span data-ttu-id="ca3c8-191">Node.js</span><span class="sxs-lookup"><span data-stu-id="ca3c8-191">Node.js</span></span>

<span data-ttu-id="ca3c8-192">Стек Azure суффикс конечной точки необходимо указать в объявлении экземпляра:</span><span class="sxs-lookup"><span data-stu-id="ca3c8-192">For Azure Stack, the endpoint suffix is specified in the declaration instance:</span></span>

```
var blobSvc = azure.createBlobService('myaccount', 'mykey',
'myaccount.blob.local.azurestack.external');
```
### <a name="c"></a><span data-ttu-id="ca3c8-193">C++</span><span class="sxs-lookup"><span data-stu-id="ca3c8-193">C++</span></span>

<span data-ttu-id="ca3c8-194">Стек Azure необходимо указать суффикс конечной точки в настройки строки подключения:</span><span class="sxs-lookup"><span data-stu-id="ca3c8-194">For Azure Stack, the endpoint suffix is specified in the setup of connection string:</span></span>

```
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;
AccountName=your_storage_account;
AccountKey=your_storage_account_key;
EndpointSuffix=local.azurestack.external"));
```

### <a name="php"></a><span data-ttu-id="ca3c8-195">PHP</span><span class="sxs-lookup"><span data-stu-id="ca3c8-195">PHP</span></span>

<span data-ttu-id="ca3c8-196">Стек Azure необходимо указать суффикс конечной точки в настройки строки подключения:</span><span class="sxs-lookup"><span data-stu-id="ca3c8-196">For Azure Stack, the endpoint suffix is specified in the setup of connection string:</span></span>

```
$connectionString = 'BlobEndpoint=http://<storage account name>.blob.local.azurestack.external/;
QueueEndpoint=http:// <storage account name>.queue.local.azurestack.external/;
TableEndpoint=http:// <storage account name>.table.local.azurestack.external/;
AccountName=<storage account name>;AccountKey=<storage account key>'
```

### <a name="python"></a><span data-ttu-id="ca3c8-197">Python</span><span class="sxs-lookup"><span data-stu-id="ca3c8-197">Python</span></span>

<span data-ttu-id="ca3c8-198">Стек Azure суффикс конечной точки необходимо указать в объявлении экземпляра:</span><span class="sxs-lookup"><span data-stu-id="ca3c8-198">For Azure Stack, the endpoint suffix is specified in the declaration instance:</span></span>

```
block_blob_service = BlockBlobService(account_name='myaccount',
account_key='mykey',
endpoint_suffix='local.azurestack.external')
```
### <a name="ruby"></a><span data-ttu-id="ca3c8-199">Ruby</span><span class="sxs-lookup"><span data-stu-id="ca3c8-199">Ruby</span></span>

<span data-ttu-id="ca3c8-200">Стек Azure необходимо указать суффикс конечной точки в настройки строки подключения:</span><span class="sxs-lookup"><span data-stu-id="ca3c8-200">For Azure Stack, the endpoint suffix is specified in the setup of connection string:</span></span>

```
set
AZURE_STORAGE_CONNECTION_STRING=DefaultEndpointsProtocol=https;
AccountName=myaccount;
AccountKey=mykey;
EndpointSuffix=local.azurestack.external
```

## <a name="blob-storage"></a><span data-ttu-id="ca3c8-201">Хранилище BLOB-объектов</span><span class="sxs-lookup"><span data-stu-id="ca3c8-201">Blob storage</span></span>

<span data-ttu-id="ca3c8-202">Стек Azure применяются следующие учебники хранилища больших двоичных объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="ca3c8-202">The following Azure Blob storage tutorials are applicable to Azure Stack.</span></span> <span data-ttu-id="ca3c8-203">Определите требования суффикс конкретной конечной точки для Azure стека, описанный в предыдущем [примеры](#examples) раздела.</span><span class="sxs-lookup"><span data-stu-id="ca3c8-203">Note the specific endpoint suffix requirement for Azure Stack described in the previous [Examples](#examples) section.</span></span>

* [<span data-ttu-id="ca3c8-204">Приступая к работе с хранилищем BLOB-объектов Azure с помощью .NET</span><span class="sxs-lookup"><span data-stu-id="ca3c8-204">Get started with Azure Blob storage using .NET</span></span>](../../storage/blobs/storage-dotnet-how-to-use-blobs.md)
* [<span data-ttu-id="ca3c8-205">Использование хранилища BLOB-объектов из Java</span><span class="sxs-lookup"><span data-stu-id="ca3c8-205">How to use Blob storage from Java</span></span>](../../storage/blobs/storage-java-how-to-use-blob-storage.md)
* <span data-ttu-id="ca3c8-206">[Способы использования хранилища больших двоичных объектов из Node.js]... /.. / storage/blobs/storage-nodejs-how-to-use-blob-storage.md)</span><span class="sxs-lookup"><span data-stu-id="ca3c8-206">[How to use Blob storage from Node.js]../../storage/blobs/storage-nodejs-how-to-use-blob-storage.md)</span></span>
* [<span data-ttu-id="ca3c8-207">Использование хранилища BLOB-объектов из C++</span><span class="sxs-lookup"><span data-stu-id="ca3c8-207">How to use Blob storage from C++</span></span>](../../storage/blobs/storage-c-plus-plus-how-to-use-blobs.md)
* [<span data-ttu-id="ca3c8-208">Использование хранилища BLOB-объектов из PHP</span><span class="sxs-lookup"><span data-stu-id="ca3c8-208">How to use Blob storage from PHP</span></span>](../../storage/blobs/storage-php-how-to-use-blobs.md)
* [<span data-ttu-id="ca3c8-209">Использование хранилища больших двоичных объектов Azure с Python</span><span class="sxs-lookup"><span data-stu-id="ca3c8-209">How to use Azure Blob storage from Python</span></span>](../../storage/blobs/storage-python-how-to-use-blob-storage.md)
* [<span data-ttu-id="ca3c8-210">Использование хранилища BLOB-объектов из Ruby</span><span class="sxs-lookup"><span data-stu-id="ca3c8-210">How to use Blob storage from Ruby</span></span>](../../storage/blobs/storage-ruby-how-to-use-blob-storage.md)

## <a name="queue-storage"></a><span data-ttu-id="ca3c8-211">Хранилище очередей</span><span class="sxs-lookup"><span data-stu-id="ca3c8-211">Queue storage</span></span>

<span data-ttu-id="ca3c8-212">В следующих учебниках хранилища очередей Azure относятся к Azure стека.</span><span class="sxs-lookup"><span data-stu-id="ca3c8-212">The following Azure Queue storage tutorials are applicable to Azure Stack.</span></span> <span data-ttu-id="ca3c8-213">Определите требования суффикс конкретной конечной точки для Azure стека, описанный в предыдущем [примеры](#examples) раздела.</span><span class="sxs-lookup"><span data-stu-id="ca3c8-213">Note the specific endpoint suffix requirement for Azure Stack described in the previous [Examples](#examples) section.</span></span>

* [<span data-ttu-id="ca3c8-214">Приступая к работе с хранилищем очередей Azure с помощью .NET</span><span class="sxs-lookup"><span data-stu-id="ca3c8-214">Get started with Azure Queue storage using .NET</span></span>](../../storage/queues/storage-dotnet-how-to-use-queues.md)
* [<span data-ttu-id="ca3c8-215">Использование хранилища очередей из Java</span><span class="sxs-lookup"><span data-stu-id="ca3c8-215">How to use Queue storage from Java</span></span>](../../storage/queues/storage-java-how-to-use-queue-storage.md)
* [<span data-ttu-id="ca3c8-216">Использование хранилища очередей из Node.js</span><span class="sxs-lookup"><span data-stu-id="ca3c8-216">How to use Queue storage from Node.js</span></span>](../../storage/queues/storage-nodejs-how-to-use-queues.md)
* [<span data-ttu-id="ca3c8-217">Использование хранилища очередей из C++</span><span class="sxs-lookup"><span data-stu-id="ca3c8-217">How to use Queue storage from C++</span></span>](../../storage/queues/storage-c-plus-plus-how-to-use-queues.md)
* [<span data-ttu-id="ca3c8-218">Использование хранилища очередей из PHP</span><span class="sxs-lookup"><span data-stu-id="ca3c8-218">How to use Queue storage from PHP</span></span>](../../storage/queues/storage-php-how-to-use-queues.md)
* [<span data-ttu-id="ca3c8-219">Использование хранилища очередей из Python</span><span class="sxs-lookup"><span data-stu-id="ca3c8-219">How to use Queue storage from Python</span></span>](../../storage/queues/storage-python-how-to-use-queue-storage.md)
* [<span data-ttu-id="ca3c8-220">Использование хранилища очередей из Ruby</span><span class="sxs-lookup"><span data-stu-id="ca3c8-220">How to use Queue storage from Ruby</span></span>](../../storage/queues/storage-ruby-how-to-use-queue-storage.md)


## <a name="table-storage"></a><span data-ttu-id="ca3c8-221">Хранилище таблиц</span><span class="sxs-lookup"><span data-stu-id="ca3c8-221">Table storage</span></span>

<span data-ttu-id="ca3c8-222">В следующих учебниках хранилища таблиц Azure относятся к Azure стека.</span><span class="sxs-lookup"><span data-stu-id="ca3c8-222">The following Azure Table storage tutorials are applicable to Azure Stack.</span></span> <span data-ttu-id="ca3c8-223">Определите требования суффикс конкретной конечной точки для Azure стека, описанный в предыдущем [примеры](#examples) раздела.</span><span class="sxs-lookup"><span data-stu-id="ca3c8-223">Note the specific endpoint suffix requirement for Azure Stack described in the previous [Examples](#examples) section.</span></span>

* [<span data-ttu-id="ca3c8-224">Приступая к работе с хранилищем таблиц Azure с помощью .NET</span><span class="sxs-lookup"><span data-stu-id="ca3c8-224">Get started with Azure Table storage using .NET</span></span>](../../cosmos-db/table-storage-how-to-use-dotnet.md)
* [<span data-ttu-id="ca3c8-225">Использование табличного хранилища из Java</span><span class="sxs-lookup"><span data-stu-id="ca3c8-225">How to use Table storage from Java</span></span>](../../cosmos-db/table-storage-how-to-use-java.md)
* [<span data-ttu-id="ca3c8-226">Использование хранилища Azure таблицы из Node.js</span><span class="sxs-lookup"><span data-stu-id="ca3c8-226">How to use Azure Table storage from Node.js</span></span>](../../cosmos-db/table-storage-how-to-use-nodejs.md)
* [<span data-ttu-id="ca3c8-227">Как использовать хранилище таблиц из C++</span><span class="sxs-lookup"><span data-stu-id="ca3c8-227">How to use Table storage from C++</span></span>](../../cosmos-db/table-storage-how-to-use-c-plus.md)
* [<span data-ttu-id="ca3c8-228">Использование табличного хранилища из PHP</span><span class="sxs-lookup"><span data-stu-id="ca3c8-228">How to use Table storage from PHP</span></span>](../../cosmos-db/table-storage-how-to-use-php.md)
* [<span data-ttu-id="ca3c8-229">Как использовать хранилище таблиц в Python</span><span class="sxs-lookup"><span data-stu-id="ca3c8-229">How to use Table storage in Python</span></span>](../../cosmos-db/table-storage-how-to-use-python.md)
* [<span data-ttu-id="ca3c8-230">Использование табличного хранилища из Ruby</span><span class="sxs-lookup"><span data-stu-id="ca3c8-230">How to use Table storage from Ruby</span></span>](../../cosmos-db/table-storage-how-to-use-ruby.md)

## <a name="next-steps"></a><span data-ttu-id="ca3c8-231">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ca3c8-231">Next steps</span></span>

* [<span data-ttu-id="ca3c8-232">Введение в службу хранилища Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="ca3c8-232">Introduction to Microsoft Azure Storage</span></span>](../../storage/common/storage-introduction.md)