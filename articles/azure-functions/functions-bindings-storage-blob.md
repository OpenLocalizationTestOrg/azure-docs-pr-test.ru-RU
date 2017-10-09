---
title: "aaaAzure хранилища больших двоичных объектов функций привязки | Документы Microsoft"
description: "Понять, как триггеры toouse хранилища Azure и привязки в функциях Azure."
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: "функции azure, функции, обработка событий, динамические вычисления, независимая архитектура"
ms.assetid: aba8976c-6568-4ec7-86f5-410efd6b0fb9
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/25/2017
ms.author: glenga
ms.openlocfilehash: cef44bd2154d0b97cca9220b6c5024a5b620c80d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-blob-storage-bindings"></a><span data-ttu-id="ff5c7-104">Привязки хранилища BLOB-объектов для Функций Azure</span><span class="sxs-lookup"><span data-stu-id="ff5c7-104">Azure Functions Blob storage bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="ff5c7-105">В этой статье объясняется, как tooconfigure и работать с привязками хранилища больших двоичных объектов Azure в функции Azure.</span><span class="sxs-lookup"><span data-stu-id="ff5c7-105">This article explains how tooconfigure and work with Azure Blob storage bindings in Azure Functions.</span></span> <span data-ttu-id="ff5c7-106">Функции Azure поддерживают привязки триггера, а также входные и выходные привязки для хранилища BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="ff5c7-106">Azure Functions supports trigger, input, and output bindings for Azure Blob storage.</span></span> <span data-ttu-id="ff5c7-107">Описание возможностей, доступных во всех привязках, см. в статье [Основные понятия триггеров и привязок в Функциях Azure](functions-triggers-bindings.md).</span><span class="sxs-lookup"><span data-stu-id="ff5c7-107">For features that are available in all bindings, see [Azure Functions triggers and bindings concepts](functions-triggers-bindings.md).</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

> [!NOTE]
> <span data-ttu-id="ff5c7-108">[Учетная запись хранения только для больших двоичных объектов](../storage/common/storage-create-storage-account.md#blob-storage-accounts) не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="ff5c7-108">A [blob only storage account](../storage/common/storage-create-storage-account.md#blob-storage-accounts) is not supported.</span></span> <span data-ttu-id="ff5c7-109">Триггерам и привязкам хранилища BLOB-объектов требуется учетная запись хранения общего назначения.</span><span class="sxs-lookup"><span data-stu-id="ff5c7-109">Blob storage triggers and bindings require a general-purpose storage account.</span></span> 
> 

<a name="trigger"></a>
<a name="storage-blob-trigger"></a>
## <a name="blob-storage-triggers-and-bindings"></a><span data-ttu-id="ff5c7-110">Триггеры и привязки хранилища BLOB-объектов</span><span class="sxs-lookup"><span data-stu-id="ff5c7-110">Blob storage triggers and bindings</span></span>

<span data-ttu-id="ff5c7-111">Использование триггера хранилища больших двоичных объектов Azure hello, коде функция вызывается при обнаружении нового или обновленного большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="ff5c7-111">Using hello Azure Blob storage trigger, your function code is called when a new or updated blob is detected.</span></span> <span data-ttu-id="ff5c7-112">содержимое большого двоичного объекта Hello предоставляются как функции ввода toohello.</span><span class="sxs-lookup"><span data-stu-id="ff5c7-112">hello blob contents are provided as input toohello function.</span></span>

<span data-ttu-id="ff5c7-113">Определение триггера хранилища больших двоичных объектов, с помощью hello **Интеграция** вкладка на портале функции hello.</span><span class="sxs-lookup"><span data-stu-id="ff5c7-113">Define a blob storage trigger using hello **Integrate** tab in hello Functions portal.</span></span> <span data-ttu-id="ff5c7-114">Hello портал создает следующие определения в hello hello **привязки** раздел *function.json*:</span><span class="sxs-lookup"><span data-stu-id="ff5c7-114">hello portal creates hello following definition in hello  **bindings** section of *function.json*:</span></span>

```json
{
    "name": "<hello name used tooidentify hello trigger data in your code>",
    "type": "blobTrigger",
    "direction": "in",
    "path": "<container toomonitor, and optionally a blob name pattern - see below>",
    "connection": "<Name of app setting - see below>"
}
```

<span data-ttu-id="ff5c7-115">Входные данные большого двоичного объекта и привязок выходного определяются с помощью `blob` hello тип привязки:</span><span class="sxs-lookup"><span data-stu-id="ff5c7-115">Blob input and output bindings are defined using `blob` as hello binding type:</span></span>

```json
{
  "name": "<hello name used tooidentify hello blob input in your code>",
  "type": "blob",
  "direction": "in", // other supported directions are "inout" and "out"
  "path": "<Path of input blob - see below>",
  "connection":"<Name of app setting - see below>"
},
```

* <span data-ttu-id="ff5c7-116">Hello `path` поддерживает свойство привязки выражений и параметров фильтра.</span><span class="sxs-lookup"><span data-stu-id="ff5c7-116">hello `path` property supports binding expressions and filter parameters.</span></span> <span data-ttu-id="ff5c7-117">См. раздел [Шаблоны имен](#pattern).</span><span class="sxs-lookup"><span data-stu-id="ff5c7-117">See [Name patterns](#pattern).</span></span>
* <span data-ttu-id="ff5c7-118">Hello `connection` свойство должно содержать имя hello Настройка приложения, содержащий строки подключения хранилища.</span><span class="sxs-lookup"><span data-stu-id="ff5c7-118">hello `connection` property must contain hello name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="ff5c7-119">В hello портал Azure, hello стандартного редактора в hello **Интеграция** настраивает этот параметр приложения автоматически при выборе учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="ff5c7-119">In hello Azure portal, hello standard editor in hello **Integrate** tab configures this app setting for you when you select a storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="ff5c7-120">При использовании большого двоичного объекта триггера в плане использования, может быть вверх tooa 10 минут задержки в обработке новых больших двоичных объектов после приложения функции неактивными.</span><span class="sxs-lookup"><span data-stu-id="ff5c7-120">When you're using a blob trigger on a Consumption plan, there can be up tooa 10-minute delay in processing new blobs after a function app has gone idle.</span></span> <span data-ttu-id="ff5c7-121">После запуска приложение функции hello, большие двоичные объекты обрабатываются немедленно.</span><span class="sxs-lookup"><span data-stu-id="ff5c7-121">After hello function app is running, blobs are processed immediately.</span></span> <span data-ttu-id="ff5c7-122">tooavoid этом начальной задержки, рассмотрите одну из следующих вариантов hello:</span><span class="sxs-lookup"><span data-stu-id="ff5c7-122">tooavoid this initial delay, consider one of hello following options:</span></span>
> - <span data-ttu-id="ff5c7-123">Используйте план службы приложений с включенной функцией AlwaysOn.</span><span class="sxs-lookup"><span data-stu-id="ff5c7-123">Use an App Service plan with Always On enabled.</span></span>
> - <span data-ttu-id="ff5c7-124">Используйте другой механизм tootrigger hello большой двоичный объект обработка, например очереди сообщение, содержащее имя большого двоичного объекта hello.</span><span class="sxs-lookup"><span data-stu-id="ff5c7-124">Use another mechanism tootrigger hello blob processing, such as a queue message that contains hello blob name.</span></span> <span data-ttu-id="ff5c7-125">Пример см. в разделе [Пример входной привязки](#input-sample).</span><span class="sxs-lookup"><span data-stu-id="ff5c7-125">For an example, see [Queue trigger with blob input binding](#input-sample).</span></span>

<a name="pattern"></a>

### <a name="name-patterns"></a><span data-ttu-id="ff5c7-126">Шаблоны имен</span><span class="sxs-lookup"><span data-stu-id="ff5c7-126">Name patterns</span></span>
<span data-ttu-id="ff5c7-127">Можно указать шаблон имени большого двоичного объекта в hello `path` свойство, которое может быть выражением фильтра или привязки.</span><span class="sxs-lookup"><span data-stu-id="ff5c7-127">You can specify a blob name pattern in hello `path` property, which can be a filter or binding expression.</span></span> <span data-ttu-id="ff5c7-128">См. раздел [Выражения привязки и шаблоны](functions-triggers-bindings.md#binding-expressions-and-patterns).</span><span class="sxs-lookup"><span data-stu-id="ff5c7-128">See [Binding expressions and patterns](functions-triggers-bindings.md#binding-expressions-and-patterns).</span></span>

<span data-ttu-id="ff5c7-129">Например tooblobs toofilter, начинающиеся с «исходный», строка hello использовать следующие определения hello.</span><span class="sxs-lookup"><span data-stu-id="ff5c7-129">For example, toofilter tooblobs that start with hello string "original," use hello following definition.</span></span> <span data-ttu-id="ff5c7-130">Этот путь находит большой двоичный объект с именем *исходный Blob1.txt* в hello *ввода* контейнера, а значение hello hello `name` является переменной в коде функция `Blob1`.</span><span class="sxs-lookup"><span data-stu-id="ff5c7-130">This path finds a blob named *original-Blob1.txt* in hello *input* container, and hello value of hello `name` variable in function code is `Blob1`.</span></span>

```json
"path": "input/original-{name}",
```

<span data-ttu-id="ff5c7-131">toobind toohello большого двоичного объекта имя и расширение файла отдельно, использовать два шаблона.</span><span class="sxs-lookup"><span data-stu-id="ff5c7-131">toobind toohello blob file name and extension separately, use two patterns.</span></span> <span data-ttu-id="ff5c7-132">Этот путь также находит большой двоичный объект с именем *исходный Blob1.txt*и значение hello hello `blobname` и `blobextension` переменные в код функции *Blob1 исходный* и *txt*.</span><span class="sxs-lookup"><span data-stu-id="ff5c7-132">This path also finds a blob named *original-Blob1.txt*, and hello value of hello `blobname` and `blobextension` variables in function code are *original-Blob1* and *txt*.</span></span>

```json
"path": "input/{blobname}.{blobextension}",
```

<span data-ttu-id="ff5c7-133">Тип файла hello больших двоичных объектов можно ограничить с помощью фиксированное значение для расширения файла hello.</span><span class="sxs-lookup"><span data-stu-id="ff5c7-133">You can restrict hello file type of blobs by using a fixed value for hello file extension.</span></span> <span data-ttu-id="ff5c7-134">Например tootrigger только на файлы с расширением PNG hello используйте следующий шаблон:</span><span class="sxs-lookup"><span data-stu-id="ff5c7-134">For instance, tootrigger only on .png files, use hello following pattern:</span></span>

```json
"path": "samples/{name}.png",
```

<span data-ttu-id="ff5c7-135">Фигурные скобки используются в качестве специальных символов в шаблонах имен.</span><span class="sxs-lookup"><span data-stu-id="ff5c7-135">Curly braces are special characters in name patterns.</span></span> <span data-ttu-id="ff5c7-136">toospecify имена больших двоичных объектов, имеющих фигурные скобки в имени hello, escape hello фигурные скобки, с помощью двух фигурные скобки.</span><span class="sxs-lookup"><span data-stu-id="ff5c7-136">toospecify blob names that have curly braces in hello name, you can escape hello braces using two braces.</span></span> <span data-ttu-id="ff5c7-137">Hello следующий пример находит большой двоичный объект с именем *{20140101}-soundfile.mp3* в hello *изображения* контейнера и hello `name` значение переменной в коде функции hello  *soundfile.mp3*.</span><span class="sxs-lookup"><span data-stu-id="ff5c7-137">hello following example finds a blob named *{20140101}-soundfile.mp3* in hello *images* container, and hello `name` variable value in hello function code is *soundfile.mp3*.</span></span> 

```json
"path": "images/{{20140101}}-{name}",
```

### <a name="trigger-metadata"></a><span data-ttu-id="ff5c7-138">Метаданные триггера</span><span class="sxs-lookup"><span data-stu-id="ff5c7-138">Trigger metadata</span></span>

<span data-ttu-id="ff5c7-139">триггер Hello больших двоичных объектов предоставляет несколько свойств метаданных.</span><span class="sxs-lookup"><span data-stu-id="ff5c7-139">hello blob trigger provides several metadata properties.</span></span> <span data-ttu-id="ff5c7-140">Эти свойства можно использовать как часть выражений привязки в других привязках или как параметры в коде.</span><span class="sxs-lookup"><span data-stu-id="ff5c7-140">These properties can be used as part of bindings expressions in other bindings or as parameters in your code.</span></span> <span data-ttu-id="ff5c7-141">Эти значения имеют hello совпадает с семантикой [CloudBlob](https://docs.microsoft.com/en-us/dotnet/api/microsoft.windowsazure.storage.blob.cloudblob?view=azure-dotnet).</span><span class="sxs-lookup"><span data-stu-id="ff5c7-141">These values have hello same semantics as [CloudBlob](https://docs.microsoft.com/en-us/dotnet/api/microsoft.windowsazure.storage.blob.cloudblob?view=azure-dotnet).</span></span>

- <span data-ttu-id="ff5c7-142">**BlobTrigger**.</span><span class="sxs-lookup"><span data-stu-id="ff5c7-142">**BlobTrigger**.</span></span> <span data-ttu-id="ff5c7-143">Введите `string`.</span><span class="sxs-lookup"><span data-stu-id="ff5c7-143">Type `string`.</span></span> <span data-ttu-id="ff5c7-144">Hello активации пути больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="ff5c7-144">hello triggering blob path</span></span>
- <span data-ttu-id="ff5c7-145">**Uri**</span><span class="sxs-lookup"><span data-stu-id="ff5c7-145">**Uri**.</span></span> <span data-ttu-id="ff5c7-146">Введите `System.Uri`.</span><span class="sxs-lookup"><span data-stu-id="ff5c7-146">Type `System.Uri`.</span></span> <span data-ttu-id="ff5c7-147">URI Hello большого двоичного объекта для основного расположения hello.</span><span class="sxs-lookup"><span data-stu-id="ff5c7-147">hello blob's URI for hello primary location.</span></span>
- <span data-ttu-id="ff5c7-148">**Properties**</span><span class="sxs-lookup"><span data-stu-id="ff5c7-148">**Properties**.</span></span> <span data-ttu-id="ff5c7-149">Введите `Microsoft.WindowsAzure.Storage.Blob.BlobProperties`.</span><span class="sxs-lookup"><span data-stu-id="ff5c7-149">Type `Microsoft.WindowsAzure.Storage.Blob.BlobProperties`.</span></span> <span data-ttu-id="ff5c7-150">Здравствуйте, системные свойства большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="ff5c7-150">hello blob's system properties.</span></span>
- <span data-ttu-id="ff5c7-151">**Metadata**</span><span class="sxs-lookup"><span data-stu-id="ff5c7-151">**Metadata**.</span></span> <span data-ttu-id="ff5c7-152">Введите `IDictionary<string,string>`.</span><span class="sxs-lookup"><span data-stu-id="ff5c7-152">Type `IDictionary<string,string>`.</span></span> <span data-ttu-id="ff5c7-153">Здравствуйте, определяемые пользователем метаданные для большого двоичного объекта hello.</span><span class="sxs-lookup"><span data-stu-id="ff5c7-153">hello user-defined metadata for hello blob.</span></span>

<a name="receipts"></a>

### <a name="blob-receipts"></a><span data-ttu-id="ff5c7-154">Уведомления о получении большого двоичного объекта</span><span class="sxs-lookup"><span data-stu-id="ff5c7-154">Blob receipts</span></span>
<span data-ttu-id="ff5c7-155">Hello Azure функции среды выполнения гарантирует, что функция триггера не большого двоичного объекта вызывается более одного раза для hello же нового или обновленного большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="ff5c7-155">hello Azure Functions runtime ensures that no blob trigger function gets called more than once for hello same new or updated blob.</span></span> <span data-ttu-id="ff5c7-156">toodetermine, если версия данного большого двоичного объекта был обработан, это обеспечивает *большого двоичного объекта уведомления*.</span><span class="sxs-lookup"><span data-stu-id="ff5c7-156">toodetermine if a given blob version has been processed, it maintains *blob receipts*.</span></span>

<span data-ttu-id="ff5c7-157">Хранилища Azure функции уведомления в контейнер больших двоичных объектов *размещаемые на веб-заданий для azure* в учетной записи хранилища Azure для приложения функции hello (, заданному параметром приложения hello `AzureWebJobsStorage`).</span><span class="sxs-lookup"><span data-stu-id="ff5c7-157">Azure Functions stores blob receipts in a container named *azure-webjobs-hosts* in hello Azure storage account for your function app (defined by hello app setting `AzureWebJobsStorage`).</span></span> <span data-ttu-id="ff5c7-158">Получение большого двоичного объекта имеет hello следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="ff5c7-158">A blob receipt has hello following information:</span></span>

* <span data-ttu-id="ff5c7-159">Hello запуска функции («*&lt;функция имя приложения >*. Функции.  *&lt;имя функции >*», например: «MyFunctionApp.Functions.CopyBlob»)</span><span class="sxs-lookup"><span data-stu-id="ff5c7-159">hello triggered function ("*&lt;function app name>*.Functions.*&lt;function name>*", for example: "MyFunctionApp.Functions.CopyBlob")</span></span>
* <span data-ttu-id="ff5c7-160">Имя контейнера Hello</span><span class="sxs-lookup"><span data-stu-id="ff5c7-160">hello container name</span></span>
* <span data-ttu-id="ff5c7-161">Тип большого двоичного объекта Hello («BlockBlob» или «PageBlob»)</span><span class="sxs-lookup"><span data-stu-id="ff5c7-161">hello blob type ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="ff5c7-162">Имя BLOB-объекта Hello</span><span class="sxs-lookup"><span data-stu-id="ff5c7-162">hello blob name</span></span>
* <span data-ttu-id="ff5c7-163">Hello ETag (идентификатор версии большого двоичного объекта, например: «0x8D1DC6E70A277EF»)</span><span class="sxs-lookup"><span data-stu-id="ff5c7-163">hello ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

<span data-ttu-id="ff5c7-164">Повторная обработка tooforce большого двоичного объекта, удалить уведомление о больших двоичных объектов hello для этого большого двоичного объекта из hello *размещаемые на веб-заданий для azure* контейнера вручную.</span><span class="sxs-lookup"><span data-stu-id="ff5c7-164">tooforce reprocessing of a blob, delete hello blob receipt for that blob from hello *azure-webjobs-hosts* container manually.</span></span>

<a name="poison"></a>

### <a name="handling-poison-blobs"></a><span data-ttu-id="ff5c7-165">Обработка подозрительных больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="ff5c7-165">Handling poison blobs</span></span>
<span data-ttu-id="ff5c7-166">При сбое функции триггера BLOB-объекта Функции Azure по умолчанию выполняют ее для этого BLOB-объекта еще 5 раз.</span><span class="sxs-lookup"><span data-stu-id="ff5c7-166">When a blob trigger function fails for a given blob, Azure Functions retries that function a total of 5 times by default.</span></span> 

<span data-ttu-id="ff5c7-167">При сбое на все 5 попыток функции Azure добавляет с именем хранилища очереди сообщений tooa *веб-заданий blobtrigger обработки подозрительных сообщений*.</span><span class="sxs-lookup"><span data-stu-id="ff5c7-167">If all 5 tries fail, Azure Functions adds a message tooa Storage queue named *webjobs-blobtrigger-poison*.</span></span> <span data-ttu-id="ff5c7-168">приветственное сообщение очереди подозрительных больших двоичных объектов является объект JSON, содержащий hello следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="ff5c7-168">hello queue message for poison blobs is a JSON object that contains hello following properties:</span></span>

* <span data-ttu-id="ff5c7-169">Идентификатор FunctionId (в формате hello  *&lt;функция имя приложения >*. Функции.  *&lt;имя функции >*)</span><span class="sxs-lookup"><span data-stu-id="ff5c7-169">FunctionId (in hello format *&lt;function app name>*.Functions.*&lt;function name>*)</span></span>
* <span data-ttu-id="ff5c7-170">BlobType (BlockBlob или PageBlob);</span><span class="sxs-lookup"><span data-stu-id="ff5c7-170">BlobType ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="ff5c7-171">ContainerName;</span><span class="sxs-lookup"><span data-stu-id="ff5c7-171">ContainerName</span></span>
* <span data-ttu-id="ff5c7-172">BlobName</span><span class="sxs-lookup"><span data-stu-id="ff5c7-172">BlobName</span></span>
* <span data-ttu-id="ff5c7-173">ETag (идентификатор версии BLOB-объектов, например 0x8D1DC6E70A277EF)</span><span class="sxs-lookup"><span data-stu-id="ff5c7-173">ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

### <a name="blob-polling-for-large-containers"></a><span data-ttu-id="ff5c7-174">Опрос больших двоичных объектов для больших контейнеров</span><span class="sxs-lookup"><span data-stu-id="ff5c7-174">Blob polling for large containers</span></span>
<span data-ttu-id="ff5c7-175">Если контейнер больших двоичных объектов hello отслеживается содержит более 10 000 больших двоичных объектов, функции hello, среда выполнения просматривает журнала toowatch файлов для новых или измененных больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="ff5c7-175">If hello blob container being monitored contains more than 10,000 blobs, hello Functions runtime scans log files toowatch for new or changed blobs.</span></span> <span data-ttu-id="ff5c7-176">Это не происходит в режиме реального времени.</span><span class="sxs-lookup"><span data-stu-id="ff5c7-176">This process is not real time.</span></span> <span data-ttu-id="ff5c7-177">Функция может не происходит до нескольких минут или больше после создания большого двоичного объекта hello.</span><span class="sxs-lookup"><span data-stu-id="ff5c7-177">A function might not get triggered until several minutes or longer after hello blob is created.</span></span> <span data-ttu-id="ff5c7-178">Кроме того, [журналы службы хранилища создаются по принципу лучшего из возможного](/rest/api/storageservices/About-Storage-Analytics-Logging),</span><span class="sxs-lookup"><span data-stu-id="ff5c7-178">In addition, [storage logs are created on a "best effort"](/rest/api/storageservices/About-Storage-Analytics-Logging) basis.</span></span> <span data-ttu-id="ff5c7-179">то есть не гарантируется регистрация всех событий.</span><span class="sxs-lookup"><span data-stu-id="ff5c7-179">There is no guarantee that all events are captured.</span></span> <span data-ttu-id="ff5c7-180">В некоторых случаях журналы могут пропускаться.</span><span class="sxs-lookup"><span data-stu-id="ff5c7-180">Under some conditions, logs may be missed.</span></span> <span data-ttu-id="ff5c7-181">Если требуется обработка большого двоичного объекта быстрее и надежнее, рассмотрите возможность создания [сообщения в очереди](../storage/queues/storage-dotnet-how-to-use-queues.md) при создании hello большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="ff5c7-181">If you require faster or more reliable blob processing, consider creating a [queue message](../storage/queues/storage-dotnet-how-to-use-queues.md) when you create hello blob.</span></span> <span data-ttu-id="ff5c7-182">Затем с помощью [очереди триггера](functions-bindings-storage-queue.md) вместо триггер tooprocess hello больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="ff5c7-182">Then, use a [queue trigger](functions-bindings-storage-queue.md) instead of a blob trigger tooprocess hello blob.</span></span>

<a name="triggerusage"></a>

## <a name="using-a-blob-trigger-and-input-binding"></a><span data-ttu-id="ff5c7-183">Использование триггера BLOB-объекта и привязки для ввода</span><span class="sxs-lookup"><span data-stu-id="ff5c7-183">Using a blob trigger and input binding</span></span>
<span data-ttu-id="ff5c7-184">В функциях .NET доступ к данным blob hello, с помощью параметра метода, например `Stream paramName`.</span><span class="sxs-lookup"><span data-stu-id="ff5c7-184">In .NET functions, access hello blob data using a method parameter such as `Stream paramName`.</span></span> <span data-ttu-id="ff5c7-185">Здесь `paramName` hello значение, указанное в hello [конфигурация триггеров](#trigger).</span><span class="sxs-lookup"><span data-stu-id="ff5c7-185">Here, `paramName` is hello value you specified in hello [trigger configuration](#trigger).</span></span> <span data-ttu-id="ff5c7-186">В функциях Node.js доступа hello входных данных больших двоичных объектов с помощью `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="ff5c7-186">In Node.js functions, access hello input blob data using `context.bindings.<name>`.</span></span>

<span data-ttu-id="ff5c7-187">В .NET можно привязать tooany типов hello в расположенном ниже списке hello.</span><span class="sxs-lookup"><span data-stu-id="ff5c7-187">In .NET, you can bind tooany of hello types in hello list below.</span></span> <span data-ttu-id="ff5c7-188">При использовании в привязке для ввода некоторые из этих типов требуют направления привязки `inout` в файле *function.json*.</span><span class="sxs-lookup"><span data-stu-id="ff5c7-188">If used as an input binding, some of these types require an `inout` binding direction in *function.json*.</span></span> <span data-ttu-id="ff5c7-189">Это направление не поддерживается стандартном редакторе hello, поэтому необходимо использовать расширенный редактор hello.</span><span class="sxs-lookup"><span data-stu-id="ff5c7-189">This direction is not supported by hello standard editor, so you must use hello advanced editor.</span></span>

* `TextReader`
* `Stream`
* <span data-ttu-id="ff5c7-190">`ICloudBlob` (требует направления привязки inout)</span><span class="sxs-lookup"><span data-stu-id="ff5c7-190">`ICloudBlob` (requires "inout" binding direction)</span></span>
* <span data-ttu-id="ff5c7-191">`CloudBlockBlob` (требует направления привязки inout)</span><span class="sxs-lookup"><span data-stu-id="ff5c7-191">`CloudBlockBlob` (requires "inout" binding direction)</span></span>
* <span data-ttu-id="ff5c7-192">`CloudPageBlob` (требует направления привязки inout)</span><span class="sxs-lookup"><span data-stu-id="ff5c7-192">`CloudPageBlob` (requires "inout" binding direction)</span></span>
* <span data-ttu-id="ff5c7-193">`CloudAppendBlob` (требует направления привязки inout)</span><span class="sxs-lookup"><span data-stu-id="ff5c7-193">`CloudAppendBlob` (requires "inout" binding direction)</span></span>

<span data-ttu-id="ff5c7-194">Если ожидаются текст больших двоичных объектов, можно также привязать tooa .NET `string` типа.</span><span class="sxs-lookup"><span data-stu-id="ff5c7-194">If text blobs are expected, you can also bind tooa .NET `string` type.</span></span> <span data-ttu-id="ff5c7-195">Рекомендуется, только если размер большого двоичного объекта hello мал, как содержимое hello весь большой двоичный объект загружается в память.</span><span class="sxs-lookup"><span data-stu-id="ff5c7-195">This is only recommended if hello blob size is small, as hello entire blob contents are loaded into memory.</span></span> <span data-ttu-id="ff5c7-196">Как правило, он является более предпочтительным, чем toouse `Stream` или `CloudBlockBlob` типа.</span><span class="sxs-lookup"><span data-stu-id="ff5c7-196">Generally, it is preferable toouse a `Stream` or `CloudBlockBlob` type.</span></span>

## <a name="trigger-sample"></a><span data-ttu-id="ff5c7-197">Пример триггера</span><span class="sxs-lookup"><span data-stu-id="ff5c7-197">Trigger sample</span></span>
<span data-ttu-id="ff5c7-198">Предположим, что имеется следующая function.json hello, определяющий триггер хранилища больших двоичных объектов:</span><span class="sxs-lookup"><span data-stu-id="ff5c7-198">Suppose you have hello following function.json that defines a blob storage trigger:</span></span>

```json
{
    "disabled": false,
    "bindings": [
        {
            "name": "myBlob",
            "type": "blobTrigger",
            "direction": "in",
            "path": "samples-workitems",
            "connection":"MyStorageAccount"
        }
    ]
}
```

<span data-ttu-id="ff5c7-199">См. Образец hello конкретного языка, зарегистрировавший hello содержимое каждого добавленного toohello отслеживаемых контейнера BLOB-объекта.</span><span class="sxs-lookup"><span data-stu-id="ff5c7-199">See hello language-specific sample that logs hello contents of each blob that is added toohello monitored container.</span></span>

* [<span data-ttu-id="ff5c7-200">C#</span><span class="sxs-lookup"><span data-stu-id="ff5c7-200">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="ff5c7-201">Node.js</span><span class="sxs-lookup"><span data-stu-id="ff5c7-201">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="blob-trigger-examples-in-c"></a><span data-ttu-id="ff5c7-202">Примеры триггеров BLOB-объектов на C#</span><span class="sxs-lookup"><span data-stu-id="ff5c7-202">Blob trigger examples in C#</span></span> #

```cs
// Blob trigger sample using a Stream binding
public static void Run(Stream myBlob, TraceWriter log)
{
   log.Info($"C# Blob trigger function Processed blob\n Name:{name} \n Size: {myBlob.Length} Bytes");
}
```

```cs
// Blob trigger binding tooa CloudBlockBlob
#r "Microsoft.WindowsAzure.Storage"

using Microsoft.WindowsAzure.Storage.Blob;

public static void Run(CloudBlockBlob myBlob, string name, TraceWriter log)
{
    log.Info($"C# Blob trigger function Processed blob\n Name:{name}\nURI:{myBlob.StorageUri}");
}
```

<a name="triggernodejs"></a>

### <a name="trigger-example-in-nodejs"></a><span data-ttu-id="ff5c7-203">Пример триггера в Node.js</span><span class="sxs-lookup"><span data-stu-id="ff5c7-203">Trigger example in Node.js</span></span>

```javascript
module.exports = function(context) {
    context.log('Node.js Blob trigger function processed', context.bindings.myBlob);
    context.done();
};
```
<a name="outputusage"></a>
<a name="storage-blob-output-binding"></a>

## <a name="using-a-blob-output-binding"></a><span data-ttu-id="ff5c7-204">Использование привязки BLOB-объекта для вывода</span><span class="sxs-lookup"><span data-stu-id="ff5c7-204">Using a blob output binding</span></span>

<span data-ttu-id="ff5c7-205">В функциях .NET, следует использовать либо `out string` параметров в сигнатуры функции или использовать один из типов hello в hello после списка.</span><span class="sxs-lookup"><span data-stu-id="ff5c7-205">In .NET functions, you should either use a `out string` parameter in your function signature or use one of hello types in hello following list.</span></span> <span data-ttu-id="ff5c7-206">В функции Node.js, доступ к hello вывода больших двоичных объектов с помощью `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="ff5c7-206">In Node.js functions, you access hello output blob using `context.bindings.<name>`.</span></span>

<span data-ttu-id="ff5c7-207">В функциях .NET могут выводиться tooany из hello следующие типы:</span><span class="sxs-lookup"><span data-stu-id="ff5c7-207">In .NET functions you can output tooany of hello following types:</span></span>

* `out string`
* `TextWriter`
* `Stream`
* `CloudBlobStream`
* `ICloudBlob`
* `CloudBlockBlob` 
* `CloudPageBlob` 

<a name="input-sample"></a>

## <a name="queue-trigger-with-blob-input-and-output-sample"></a><span data-ttu-id="ff5c7-208">Пример триггера очереди с вводом и выводом BLOB-объекта</span><span class="sxs-lookup"><span data-stu-id="ff5c7-208">Queue trigger with blob input and output sample</span></span>
<span data-ttu-id="ff5c7-209">Предположим, что имеется следующая function.json hello, определяющий [хранилища очередей триггер](functions-bindings-storage-queue.md)входных данных в хранилище больших двоичных объектов и выходные данные в хранилище больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="ff5c7-209">Suppose you have hello following function.json, that defines a [Queue Storage trigger](functions-bindings-storage-queue.md), a blob storage input, and a blob storage output.</span></span> <span data-ttu-id="ff5c7-210">Использование уведомления hello hello `queueTrigger` свойства метаданных.</span><span class="sxs-lookup"><span data-stu-id="ff5c7-210">Notice hello use of hello `queueTrigger` metadata property.</span></span> <span data-ttu-id="ff5c7-211">в большом двоичном объекте hello входной и выходной `path` свойства:</span><span class="sxs-lookup"><span data-stu-id="ff5c7-211">in hello blob input and output `path` properties:</span></span>

```json
{
  "bindings": [
    {
      "queueName": "myqueue-items",
      "connection": "MyStorageConnection",
      "name": "myQueueItem",
      "type": "queueTrigger",
      "direction": "in"
    },
    {
      "name": "myInputBlob",
      "type": "blob",
      "path": "samples-workitems/{queueTrigger}",
      "connection": "MyStorageConnection",
      "direction": "in"
    },
    {
      "name": "myOutputBlob",
      "type": "blob",
      "path": "samples-workitems/{queueTrigger}-Copy",
      "connection": "MyStorageConnection",
      "direction": "out"
    }
  ],
  "disabled": false
}
``` 

<span data-ttu-id="ff5c7-212">См. пример hello зависящие от языка, который копирует hello ввода toohello выходные данные больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="ff5c7-212">See hello language-specific sample that copies hello input blob toohello output blob.</span></span>

* [<span data-ttu-id="ff5c7-213">C#</span><span class="sxs-lookup"><span data-stu-id="ff5c7-213">C#</span></span>](#incsharp)
* [<span data-ttu-id="ff5c7-214">Node.js</span><span class="sxs-lookup"><span data-stu-id="ff5c7-214">Node.js</span></span>](#innodejs)

<a name="incsharp"></a>

### <a name="blob-binding-example-in-c"></a><span data-ttu-id="ff5c7-215">Пример привязки BLOB-объекта на C#</span><span class="sxs-lookup"><span data-stu-id="ff5c7-215">Blob binding example in C#</span></span> #

```cs
// Copy blob from input toooutput, based on a queue trigger
public static void Run(string myQueueItem, Stream myInputBlob, out string myOutputBlob, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    myOutputBlob = myInputBlob;
}
```

<a name="innodejs"></a>

### <a name="blob-binding-example-in-nodejs"></a><span data-ttu-id="ff5c7-216">Пример привязки BLOB-объекта в Node.js</span><span class="sxs-lookup"><span data-stu-id="ff5c7-216">Blob binding example in Node.js</span></span>

```javascript
// Copy blob from input toooutput, based on a queue trigger
module.exports = function(context) {
    context.log('Node.js Queue trigger function processed', context.bindings.myQueueItem);
    context.bindings.myOutputBlob = context.bindings.myInputBlob;
    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="ff5c7-217">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ff5c7-217">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

