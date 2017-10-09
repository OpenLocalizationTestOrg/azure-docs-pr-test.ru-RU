---
title: "aaaDevelop и выполнения Azure работает локально | Документы Microsoft"
description: "Узнайте, как toocode и тестирования Azure функционирует на локальном компьютере до их выполнения в функции Azure."
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
ms.assetid: 242736be-ec66-4114-924b-31795fd18884
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: multiple
ms.topic: article
ms.date: 07/12/2017
ms.author: glenga
ms.openlocfilehash: 342ed4d6df41a2d2df9067948e19e347bb52c844
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="code-and-test-azure-functions-locally"></a><span data-ttu-id="57c99-103">Как программировать и тестировать функции Azure в локальной среде</span><span class="sxs-lookup"><span data-stu-id="57c99-103">Code and test Azure functions locally</span></span>

<span data-ttu-id="57c99-104">При hello [портал Azure] предоставляет полный набор средств для разработки и тестирования функции Azure, многие разработчики предпочитают процесс локальной разработки.</span><span class="sxs-lookup"><span data-stu-id="57c99-104">While hello [Azure portal] provides a full set of tools for developing and testing Azure Functions, many developers prefer a local development experience.</span></span> <span data-ttu-id="57c99-105">Функции Azure позволяет легко toouse избранные кода редактора и toodevelop средства локальной разработки и тестирования функций на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="57c99-105">Azure Functions makes it easy toouse your favorite code editor and local development tools toodevelop and test your functions on your local computer.</span></span> <span data-ttu-id="57c99-106">Функции могут вызывать события в Azure, а вы можете отлаживать функции C# и JavaScript на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="57c99-106">Your functions can trigger on events in Azure, and you can debug your C# and JavaScript functions on your local computer.</span></span> 

<span data-ttu-id="57c99-107">Если вы используете Visual Studio C# для разработки, Функции Azure также [интегрируются с Visual Studio 2017](functions-develop-vs.md).</span><span class="sxs-lookup"><span data-stu-id="57c99-107">If you are a Visual Studio C# developer, Azure Functions also [integrates with Visual Studio 2017](functions-develop-vs.md).</span></span>

## <a name="install-hello-azure-functions-core-tools"></a><span data-ttu-id="57c99-108">Установка инструментов основные функции hello Azure</span><span class="sxs-lookup"><span data-stu-id="57c99-108">Install hello Azure Functions Core Tools</span></span>

<span data-ttu-id="57c99-109">Основные инструменты Azure функции является локальной версии функции Azure hello среды выполнения, который можно запустить на локальном компьютере Windows.</span><span class="sxs-lookup"><span data-stu-id="57c99-109">Azure Functions Core Tools is a local version of hello Azure Functions runtime that you can run on your local Windows computer.</span></span> <span data-ttu-id="57c99-110">Это не эмулятор или симулятор.</span><span class="sxs-lookup"><span data-stu-id="57c99-110">It's not an emulator or simulator.</span></span> <span data-ttu-id="57c99-111">Он имеет hello одной среды выполнения, лежит в основе функций в Azure.</span><span class="sxs-lookup"><span data-stu-id="57c99-111">It's hello same runtime that powers Functions in Azure.</span></span>

<span data-ttu-id="57c99-112">Hello [основные инструменты Azure функции] предоставляется в виде пакета npm.</span><span class="sxs-lookup"><span data-stu-id="57c99-112">hello [Azure Functions Core Tools] is provided as an npm package.</span></span> <span data-ttu-id="57c99-113">Сначала необходимо [установить NodeJS](https://docs.npmjs.com/getting-started/installing-node), в состав которого входит npm.</span><span class="sxs-lookup"><span data-stu-id="57c99-113">You must first [install NodeJS](https://docs.npmjs.com/getting-started/installing-node), which includes npm.</span></span>  

>[!NOTE]
><span data-ttu-id="57c99-114">В настоящее время пакет основные инструменты Azure функции hello можно установить только на компьютерах Windows.</span><span class="sxs-lookup"><span data-stu-id="57c99-114">At this time, hello Azure Functions Core Tools package can only be installed on Windows computers.</span></span> <span data-ttu-id="57c99-115">Это ограничение действует из-за tooa временное ограничение в узле функции hello.</span><span class="sxs-lookup"><span data-stu-id="57c99-115">This restriction is due tooa temporary limitation in hello Functions host.</span></span>

<span data-ttu-id="57c99-116">[основные инструменты Azure функции] добавляет hello следующие псевдонимы команд:</span><span class="sxs-lookup"><span data-stu-id="57c99-116">[Azure Functions Core Tools] adds hello following command aliases:</span></span>
* <span data-ttu-id="57c99-117">**func**</span><span class="sxs-lookup"><span data-stu-id="57c99-117">**func**</span></span>
* <span data-ttu-id="57c99-118">**azfun**</span><span class="sxs-lookup"><span data-stu-id="57c99-118">**azfun**</span></span>
* <span data-ttu-id="57c99-119">**azurefunctions**</span><span class="sxs-lookup"><span data-stu-id="57c99-119">**azurefunctions**</span></span>

<span data-ttu-id="57c99-120">Все эти псевдоним может использоваться вместо `func` показано в примерах hello в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="57c99-120">All of these alias can be used instead of `func` shown in hello examples in this topic.</span></span>

## <a name="create-a-local-functions-project"></a><span data-ttu-id="57c99-121">Создание локального проекта службы "Функции"</span><span class="sxs-lookup"><span data-stu-id="57c99-121">Create a local Functions project</span></span>

<span data-ttu-id="57c99-122">При выполнении локально, проект функции — каталог, имеющий hello файлы host.json и local.settings.json.</span><span class="sxs-lookup"><span data-stu-id="57c99-122">When running locally, a Functions project is a directory that has hello files host.json and local.settings.json.</span></span> <span data-ttu-id="57c99-123">Этот каталог является hello эквивалентные функции приложения в Azure.</span><span class="sxs-lookup"><span data-stu-id="57c99-123">This directory is hello equivalent of a function app in Azure.</span></span> <span data-ttu-id="57c99-124">toolearn Дополнительные сведения о hello Azure функции структуру папок, в разделе hello [руководство для разработчиков Azure функции](functions-reference.md#folder-structure).</span><span class="sxs-lookup"><span data-stu-id="57c99-124">toolearn more about hello Azure Functions folder structure, see hello [Azure Functions developers guide](functions-reference.md#folder-structure).</span></span>

<span data-ttu-id="57c99-125">В командной строке выполните следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="57c99-125">At a command prompt, run hello following command:</span></span>

```
func init MyFunctionProj
```

<span data-ttu-id="57c99-126">Hello вывода выглядит как следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="57c99-126">hello output looks like hello following example:</span></span>

```
Writing .gitignore
Writing host.json
Writing local.settings.json
Created launch.json
Initialized empty Git repository in D:/Code/Playground/MyFunctionProj/.git/
```

<span data-ttu-id="57c99-127">tooopt за пределы Создание репозитория Git, используйте параметр hello `--no-source-control [-n]`.</span><span class="sxs-lookup"><span data-stu-id="57c99-127">tooopt out of creating a Git repository, use hello option `--no-source-control [-n]`.</span></span>

<a name="local-settings"></a>

## <a name="local-settings-file"></a><span data-ttu-id="57c99-128">Файл с локальными параметрами</span><span class="sxs-lookup"><span data-stu-id="57c99-128">Local settings file</span></span>

<span data-ttu-id="57c99-129">файл local.settings.json Hello хранит параметры приложения, строки подключения и параметры для средства основных функций Azure.</span><span class="sxs-lookup"><span data-stu-id="57c99-129">hello file local.settings.json stores app settings, connection strings, and settings for Azure Functions Core Tools.</span></span> <span data-ttu-id="57c99-130">Он имеет hello следующие структуры:</span><span class="sxs-lookup"><span data-stu-id="57c99-130">It has hello following structure:</span></span>

```json
{
  "IsEncrypted": false,   
  "Values": {
    "AzureWebJobsStorage": "<connection string>", 
    "AzureWebJobsDashboard": "<connection string>", 
  },
  "Host": {
    "LocalHttpPort": 7071, 
    "CORS": "*" 
  },
  "ConnectionStrings": {
    "SQLConnectionString": "Value"
  }
}
```
| <span data-ttu-id="57c99-131">Настройка</span><span class="sxs-lookup"><span data-stu-id="57c99-131">Setting</span></span>      | <span data-ttu-id="57c99-132">Описание</span><span class="sxs-lookup"><span data-stu-id="57c99-132">Description</span></span>                            |
| ------------ | -------------------------------------- |
| <span data-ttu-id="57c99-133">**IsEncrypted**</span><span class="sxs-lookup"><span data-stu-id="57c99-133">**IsEncrypted**</span></span> | <span data-ttu-id="57c99-134">Если задано слишком**true**, все значения шифруются с помощью ключа локального компьютера.</span><span class="sxs-lookup"><span data-stu-id="57c99-134">When set too**true**, all values are encrypted using a local machine key.</span></span> <span data-ttu-id="57c99-135">Используется с командами `func settings`.</span><span class="sxs-lookup"><span data-stu-id="57c99-135">Used with `func settings` commands.</span></span> <span data-ttu-id="57c99-136">Значение по умолчанию — **false**.</span><span class="sxs-lookup"><span data-stu-id="57c99-136">Default value is **false**.</span></span> |
| <span data-ttu-id="57c99-137">**Значения**</span><span class="sxs-lookup"><span data-stu-id="57c99-137">**Values**</span></span> | <span data-ttu-id="57c99-138">Коллекция параметров приложения, используемых при локальном выполнении.</span><span class="sxs-lookup"><span data-stu-id="57c99-138">Collection of application settings used when running locally.</span></span> <span data-ttu-id="57c99-139">Добавьте объект toothis параметров приложения.</span><span class="sxs-lookup"><span data-stu-id="57c99-139">Add your application settings toothis object.</span></span>  |
| <span data-ttu-id="57c99-140">**AzureWebJobsStorage**</span><span class="sxs-lookup"><span data-stu-id="57c99-140">**AzureWebJobsStorage**</span></span> | <span data-ttu-id="57c99-141">Задает hello toohello строка подключения учетной записи хранения Azure, который используется средой выполнения Azure функции hello.</span><span class="sxs-lookup"><span data-stu-id="57c99-141">Sets hello connection string toohello Azure Storage account that is used internally by hello Azure Functions runtime.</span></span> <span data-ttu-id="57c99-142">Учетная запись хранения Hello поддерживает ваша функция триггеры.</span><span class="sxs-lookup"><span data-stu-id="57c99-142">hello storage account supports your function's triggers.</span></span> <span data-ttu-id="57c99-143">Параметр подключения к учетной записи хранения необходим для всех функций, кроме функций, активируемых протоколом HTTP.</span><span class="sxs-lookup"><span data-stu-id="57c99-143">This storage account connection setting is required for all functions except for HTTP triggered functions.</span></span>  |
| <span data-ttu-id="57c99-144">**AzureWebJobsDashboard**</span><span class="sxs-lookup"><span data-stu-id="57c99-144">**AzureWebJobsDashboard**</span></span> | <span data-ttu-id="57c99-145">Задает hello соединения строки toohello учетную запись хранилища Azure, используемых toostore журналов функций hello.</span><span class="sxs-lookup"><span data-stu-id="57c99-145">Sets hello connection string toohello Azure Storage account that is used toostore hello function logs.</span></span> <span data-ttu-id="57c99-146">Это необязательное значение становится журналы hello, доступным в портал hello.</span><span class="sxs-lookup"><span data-stu-id="57c99-146">This optional value makes hello logs accessible in hello portal.</span></span>|
| <span data-ttu-id="57c99-147">**Host**</span><span class="sxs-lookup"><span data-stu-id="57c99-147">**Host**</span></span> | <span data-ttu-id="57c99-148">Параметры в этом разделе настраивать функции hello хост-процесса, когда выполняется локально.</span><span class="sxs-lookup"><span data-stu-id="57c99-148">Settings in this section customize hello Functions host process when running locally.</span></span> | 
| <span data-ttu-id="57c99-149">**LocalHttpPort**</span><span class="sxs-lookup"><span data-stu-id="57c99-149">**LocalHttpPort**</span></span> | <span data-ttu-id="57c99-150">Порт по умолчанию, используемые при запуске hello локальный узел функции hello наборы (`func host start` и `func run`).</span><span class="sxs-lookup"><span data-stu-id="57c99-150">Sets hello default port used when running hello local Functions host (`func host start` and `func run`).</span></span> <span data-ttu-id="57c99-151">Hello `--port` параметр командной строки имеют приоритет над это значение.</span><span class="sxs-lookup"><span data-stu-id="57c99-151">hello `--port` command-line option takes precedence over this value.</span></span> |
| <span data-ttu-id="57c99-152">**CORS**</span><span class="sxs-lookup"><span data-stu-id="57c99-152">**CORS**</span></span> | <span data-ttu-id="57c99-153">Определяет источники hello, разрешенное для [ресурсов независимо от источника (CORS) для управления доступом](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing).</span><span class="sxs-lookup"><span data-stu-id="57c99-153">Defines hello origins allowed for [cross-origin resource sharing (CORS)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing).</span></span> <span data-ttu-id="57c99-154">Источники указываются в виде разделенного запятыми списка без пробелов.</span><span class="sxs-lookup"><span data-stu-id="57c99-154">Origins are supplied as a comma-separated list with no spaces.</span></span> <span data-ttu-id="57c99-155">Здравствуйте, использование подстановочного знака (**\***) поддерживается, который разрешает запросы из любого источника.</span><span class="sxs-lookup"><span data-stu-id="57c99-155">hello wildcard value (**\***) is supported, which allows requests from any origin.</span></span> |
| <span data-ttu-id="57c99-156">**ConnectionStrings**</span><span class="sxs-lookup"><span data-stu-id="57c99-156">**ConnectionStrings**</span></span> | <span data-ttu-id="57c99-157">Содержит hello строки подключения базы данных для функций.</span><span class="sxs-lookup"><span data-stu-id="57c99-157">Contains hello database connection strings for your functions.</span></span> <span data-ttu-id="57c99-158">Строки подключения в этом объекте добавляются toohello среды с типом поставщика hello **System.Data.SqlClient**.</span><span class="sxs-lookup"><span data-stu-id="57c99-158">Connection strings in this object are added toohello environment with hello provider type of **System.Data.SqlClient**.</span></span>  | 

<span data-ttu-id="57c99-159">Большинство триггеры и привязки **подключения** свойство, которое сопоставляет toohello имя параметра приложения или переменной среды.</span><span class="sxs-lookup"><span data-stu-id="57c99-159">Most triggers and bindings have a **Connection** property that maps toohello name of an environment variable or app setting.</span></span> <span data-ttu-id="57c99-160">Для каждого свойства подключения должен быть определен параметр в файле local.settings.json.</span><span class="sxs-lookup"><span data-stu-id="57c99-160">For each connection property, there must be app setting defined in local.settings.json file.</span></span> 

<span data-ttu-id="57c99-161">Эти параметры также могут считываться в коде как переменные среды.</span><span class="sxs-lookup"><span data-stu-id="57c99-161">These settings can also be read in your code as environment variables.</span></span> <span data-ttu-id="57c99-162">В C# используйте [System.Environment.GetEnvironmentVariable](https://msdn.microsoft.com/library/system.environment.getenvironmentvariable(v=vs.110).aspx) или [ConfigurationManager.AppSettings](https://msdn.microsoft.com/library/system.configuration.configurationmanager.appsettings%28v=vs.110%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="57c99-162">In C#, use [System.Environment.GetEnvironmentVariable](https://msdn.microsoft.com/library/system.environment.getenvironmentvariable(v=vs.110).aspx) or [ConfigurationManager.AppSettings](https://msdn.microsoft.com/library/system.configuration.configurationmanager.appsettings%28v=vs.110%29.aspx).</span></span> <span data-ttu-id="57c99-163">Для JavaScript используйте `process.env`.</span><span class="sxs-lookup"><span data-stu-id="57c99-163">In JavaScript, use `process.env`.</span></span> <span data-ttu-id="57c99-164">Параметры, указанные как переменную среды имеют приоритет над значениями в файле local.settings.json hello.</span><span class="sxs-lookup"><span data-stu-id="57c99-164">Settings specified as a system environment variable take precedence over values in hello local.settings.json file.</span></span> 

<span data-ttu-id="57c99-165">Параметры в файле local.settings.json hello используются только средствами функции при выполнении локально.</span><span class="sxs-lookup"><span data-stu-id="57c99-165">Settings in hello local.settings.json file are only used by Functions tools when running locally.</span></span> <span data-ttu-id="57c99-166">По умолчанию эти параметры не переносятся автоматически при опубликованных tooAzure hello проекта.</span><span class="sxs-lookup"><span data-stu-id="57c99-166">By default, these settings are not migrated automatically when hello project is published tooAzure.</span></span> <span data-ttu-id="57c99-167">Используйте hello `--publish-local-settings` переключения [при публикации](#publish) toomake убедиться, что эти параметры будут добавлены toohello функции приложения в Azure.</span><span class="sxs-lookup"><span data-stu-id="57c99-167">Use hello `--publish-local-settings` switch [when you publish](#publish) toomake sure these settings are added toohello function app in Azure.</span></span>

<span data-ttu-id="57c99-168">Если задано не допустимую строку соединения хранения для **AzureWebJobsStorage**, отображается сообщение об ошибке после hello:</span><span class="sxs-lookup"><span data-stu-id="57c99-168">When no valid storage connection string is set for **AzureWebJobsStorage**, hello following error message is shown:</span></span>  

><span data-ttu-id="57c99-169">Отсутствует значение AzureWebJobsStorage в local.settings.json.</span><span class="sxs-lookup"><span data-stu-id="57c99-169">Missing value for AzureWebJobsStorage in local.settings.json.</span></span> <span data-ttu-id="57c99-170">This is required for all triggers other than HTTP.</span><span class="sxs-lookup"><span data-stu-id="57c99-170">This is required for all triggers other than HTTP.</span></span> <span data-ttu-id="57c99-171">Выполните команду "func azure functionary fetch-app-settings <functionAppName>" или укажите строку подключения в файле local.settings.json.</span><span class="sxs-lookup"><span data-stu-id="57c99-171">You can run 'func azure functionary fetch-app-settings <functionAppName>' or specify a connection string in local.settings.json.</span></span>
  
[!INCLUDE [Note toonot use local storage](../../includes/functions-local-settings-note.md)]

### <a name="configure-app-settings"></a><span data-ttu-id="57c99-172">Настройка параметров приложения</span><span class="sxs-lookup"><span data-stu-id="57c99-172">Configure app settings</span></span>

<span data-ttu-id="57c99-173">tooset значение для строки подключения, необходимо выполнить одно из следующих hello:</span><span class="sxs-lookup"><span data-stu-id="57c99-173">tooset a value for connection strings, you can do one of hello following:</span></span>
* <span data-ttu-id="57c99-174">Введите строку подключения hello из [обозреватель хранилищ Azure](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="57c99-174">Enter hello connection string from [Azure Storage Explorer](http://storageexplorer.com/).</span></span>
* <span data-ttu-id="57c99-175">Используйте один из следующих команд hello.</span><span class="sxs-lookup"><span data-stu-id="57c99-175">Use one of hello following commands:</span></span>

    ```
    func azure functionapp fetch-app-settings <FunctionAppName>
    ```
    ```
    func azure functionapp storage fetch-connection-string <StorageAccountName>
    ```
    <span data-ttu-id="57c99-176">Обе команды требуется вы toofirst входа tooAzure.</span><span class="sxs-lookup"><span data-stu-id="57c99-176">Both commands require you toofirst sign-in tooAzure.</span></span>

## <a name="create-a-function"></a><span data-ttu-id="57c99-177">Создание функции</span><span class="sxs-lookup"><span data-stu-id="57c99-177">Create a function</span></span>

<span data-ttu-id="57c99-178">toocreate функции запуска hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="57c99-178">toocreate a function, run hello following command:</span></span>

```
func new
``` 
<span data-ttu-id="57c99-179">`func new`поддерживает следующие необязательные аргументы hello:</span><span class="sxs-lookup"><span data-stu-id="57c99-179">`func new` supports hello following optional arguments:</span></span>

| <span data-ttu-id="57c99-180">Аргумент</span><span class="sxs-lookup"><span data-stu-id="57c99-180">Argument</span></span>     | <span data-ttu-id="57c99-181">Описание</span><span class="sxs-lookup"><span data-stu-id="57c99-181">Description</span></span>                            |
| ------------ | -------------------------------------- |
| **`--language -l`** | <span data-ttu-id="57c99-182">Hello шаблон программирования на языке, например C#, F # или JavaScript.</span><span class="sxs-lookup"><span data-stu-id="57c99-182">hello template programming language, such as C#, F#, or JavaScript.</span></span> |
| **`--template -t`** | <span data-ttu-id="57c99-183">Имя шаблона Hello.</span><span class="sxs-lookup"><span data-stu-id="57c99-183">hello template name.</span></span> |
| **`--name -n`** | <span data-ttu-id="57c99-184">имя функции Hello.</span><span class="sxs-lookup"><span data-stu-id="57c99-184">hello function name.</span></span> |

<span data-ttu-id="57c99-185">Например toocreate триггер JavaScript HTTP запуска:</span><span class="sxs-lookup"><span data-stu-id="57c99-185">For example, toocreate a JavaScript HTTP trigger, run:</span></span>

```
func new --language JavaScript --template HttpTrigger --name MyHttpTrigger
```

<span data-ttu-id="57c99-186">toocreate функции активации очереди, выполните:</span><span class="sxs-lookup"><span data-stu-id="57c99-186">toocreate a queue-triggered function, run:</span></span>

```
func new --language JavaScript --template QueueTrigger --name QueueTriggerJS
```

## <a name="run-functions-locally"></a><span data-ttu-id="57c99-187">Запуск функций в локальной среде</span><span class="sxs-lookup"><span data-stu-id="57c99-187">Run functions locally</span></span>

<span data-ttu-id="57c99-188">toorun проект функции выполнять функции сервера hello.</span><span class="sxs-lookup"><span data-stu-id="57c99-188">toorun a Functions project, run hello Functions host.</span></span> <span data-ttu-id="57c99-189">Hello узла включает триггеры для всех функций в проекте hello:</span><span class="sxs-lookup"><span data-stu-id="57c99-189">hello host enables triggers for all functions in hello project:</span></span>

```
func host start
```

<span data-ttu-id="57c99-190">`func host start`hello поддерживает следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="57c99-190">`func host start` supports hello following options:</span></span>

| <span data-ttu-id="57c99-191">Параметр</span><span class="sxs-lookup"><span data-stu-id="57c99-191">Option</span></span>     | <span data-ttu-id="57c99-192">Описание</span><span class="sxs-lookup"><span data-stu-id="57c99-192">Description</span></span>                            |
| ------------ | -------------------------------------- |
|**`--port -p`** | <span data-ttu-id="57c99-193">Hello toolisten локальных портов на.</span><span class="sxs-lookup"><span data-stu-id="57c99-193">hello local port toolisten on.</span></span> <span data-ttu-id="57c99-194">Значение по умолчанию: 7071.</span><span class="sxs-lookup"><span data-stu-id="57c99-194">Default value: 7071.</span></span> |
| **`--debug <type>`** | <span data-ttu-id="57c99-195">Параметры Hello `VSCode` и `VS`.</span><span class="sxs-lookup"><span data-stu-id="57c99-195">hello options are `VSCode` and `VS`.</span></span> |
| **`--cors`** | <span data-ttu-id="57c99-196">Список разрешенных источников CORS, разделенный запятыми без пробелов.</span><span class="sxs-lookup"><span data-stu-id="57c99-196">A comma-separated list of CORS origins, with no spaces.</span></span> |
| **`--nodeDebugPort -n`** | <span data-ttu-id="57c99-197">порт Hello для отладчика toouse hello узла.</span><span class="sxs-lookup"><span data-stu-id="57c99-197">hello port for hello node debugger toouse.</span></span> <span data-ttu-id="57c99-198">Значение по умолчанию — значение из launch.json или 5858.</span><span class="sxs-lookup"><span data-stu-id="57c99-198">Default: A value from launch.json or 5858.</span></span> |
| **`--debugLevel -d`** | <span data-ttu-id="57c99-199">уровень трассировки Hello консоли (Выкл., verbose, информация, предупреждение или ошибка).</span><span class="sxs-lookup"><span data-stu-id="57c99-199">hello console trace level (off, verbose, info, warning, or error).</span></span> <span data-ttu-id="57c99-200">Значение по умолчанию — info.</span><span class="sxs-lookup"><span data-stu-id="57c99-200">Default: Info.</span></span>|
| **`--timeout -t`** | <span data-ttu-id="57c99-201">Hello hello функции узла запуск, истечение времени ожидания в секундах.</span><span class="sxs-lookup"><span data-stu-id="57c99-201">hello time out for hello Functions host t     o start, in seconds.</span></span> <span data-ttu-id="57c99-202">Значение по умолчанию — 20 секунд.</span><span class="sxs-lookup"><span data-stu-id="57c99-202">Default: 20 seconds.</span></span>|
| **`--useHttps`** | <span data-ttu-id="57c99-203">Привязать toohttps://localhost: {port} вместо toohttp://localhost: {port}.</span><span class="sxs-lookup"><span data-stu-id="57c99-203">Bind toohttps://localhost:{port} rather than toohttp://localhost:{port}.</span></span> <span data-ttu-id="57c99-204">По умолчанию этот параметр создает доверенный сертификат на компьютере.</span><span class="sxs-lookup"><span data-stu-id="57c99-204">By default, this option creates a trusted certificate on your computer.</span></span>|
| **`--pause-on-error`** | <span data-ttu-id="57c99-205">Приостановка для дополнительных входных данных перед выходом из процесса hello.</span><span class="sxs-lookup"><span data-stu-id="57c99-205">Pause for additional input before exiting hello process.</span></span> <span data-ttu-id="57c99-206">Это удобно при запуске основных инструментов службы "Функции Azure" из интегрированной среды разработки (IDE).</span><span class="sxs-lookup"><span data-stu-id="57c99-206">Useful when launching Azure Functions Core Tools from an integrated development environment (IDE).</span></span>|

<span data-ttu-id="57c99-207">При запуске узла функции hello, он выводит hello функции активации HTTP URL-адрес:</span><span class="sxs-lookup"><span data-stu-id="57c99-207">When hello Functions host starts, it outputs hello URL of HTTP-triggered functions:</span></span>

```
Found hello following functions:
Host.Functions.MyHttpTrigger

ob host started
Http Function MyHttpTrigger: http://localhost:7071/api/MyHttpTrigger
```

### <a name="debug-in-vs-code-or-visual-studio"></a><span data-ttu-id="57c99-208">Отладка в VS Code или Visual Studio</span><span class="sxs-lookup"><span data-stu-id="57c99-208">Debug in VS Code or Visual Studio</span></span>

<span data-ttu-id="57c99-209">tooattach отладчик, передайте hello `--debug` аргумент.</span><span class="sxs-lookup"><span data-stu-id="57c99-209">tooattach a debugger, pass hello `--debug` argument.</span></span> <span data-ttu-id="57c99-210">toodebug функции JavaScript, используют кода Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="57c99-210">toodebug JavaScript functions, use Visual Studio Code.</span></span> <span data-ttu-id="57c99-211">Для функций на C# используйте Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="57c99-211">For C# functions, use Visual Studio.</span></span>

<span data-ttu-id="57c99-212">функции toodebug C# используют `--debug vs`.</span><span class="sxs-lookup"><span data-stu-id="57c99-212">toodebug C# functions, use `--debug vs`.</span></span> <span data-ttu-id="57c99-213">Кроме того, можно использовать [инструменты Visual Studio 2017 для Функций Azure](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/).</span><span class="sxs-lookup"><span data-stu-id="57c99-213">You can also use [Azure Functions Visual Studio 2017 Tools](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/).</span></span> 

<span data-ttu-id="57c99-214">toolaunch hello узла и Настройка отладки JavaScript, выполните:</span><span class="sxs-lookup"><span data-stu-id="57c99-214">toolaunch hello host and set up JavaScript debugging, run:</span></span>

```
func host start --debug vscode
```

<span data-ttu-id="57c99-215">Затем в коде Visual Studio в hello **отладки** представление, выберите **прикрепляются функции tooAzure**.</span><span class="sxs-lookup"><span data-stu-id="57c99-215">Then, in Visual Studio Code, in hello **Debug** view, select **Attach tooAzure Functions**.</span></span> <span data-ttu-id="57c99-216">Вы можете присоединить точки останова, просмотреть значения переменных и осуществить пошаговое выполнение кода.</span><span class="sxs-lookup"><span data-stu-id="57c99-216">You can attach breakpoints, inspect variables, and step through code.</span></span>

![Отладка с помощью Visual Studio 2015](./media/functions-run-local/vscode-javascript-debugging.png)

### <a name="passing-test-data-tooa-function"></a><span data-ttu-id="57c99-218">Функции tooa передача проверки данных</span><span class="sxs-lookup"><span data-stu-id="57c99-218">Passing test data tooa function</span></span>

<span data-ttu-id="57c99-219">Можно также вызвать функцию напрямую с помощью `func run <FunctionName>` и предоставить входные данные для функции hello.</span><span class="sxs-lookup"><span data-stu-id="57c99-219">You can also invoke a function directly by using `func run <FunctionName>` and provide input data for hello function.</span></span> <span data-ttu-id="57c99-220">Эта команда является toorunning аналогичные функции с помощью hello **тест** hello портал Azure на вкладке.</span><span class="sxs-lookup"><span data-stu-id="57c99-220">This command is similar toorunning a function using hello **Test** tab in hello Azure portal.</span></span> <span data-ttu-id="57c99-221">Эта команда запускает hello всей функции узла.</span><span class="sxs-lookup"><span data-stu-id="57c99-221">This command launches hello entire Functions host.</span></span>

<span data-ttu-id="57c99-222">`func run`hello поддерживает следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="57c99-222">`func run` supports hello following options:</span></span>

| <span data-ttu-id="57c99-223">Параметр</span><span class="sxs-lookup"><span data-stu-id="57c99-223">Option</span></span>     | <span data-ttu-id="57c99-224">Описание</span><span class="sxs-lookup"><span data-stu-id="57c99-224">Description</span></span>                            |
| ------------ | -------------------------------------- |
| **`--content -c`** | <span data-ttu-id="57c99-225">Встроенное содержимое.</span><span class="sxs-lookup"><span data-stu-id="57c99-225">Inline content.</span></span> |
| **`--debug -d`** | <span data-ttu-id="57c99-226">Присоедините отладчик toohello хост-процесса перед выполнением функции hello.</span><span class="sxs-lookup"><span data-stu-id="57c99-226">Attach a debugger toohello host process before running hello function.</span></span>|
| **`--timeout -t`** | <span data-ttu-id="57c99-227">Toowait время (в секундах) до локальный узел функции hello готов.</span><span class="sxs-lookup"><span data-stu-id="57c99-227">Time toowait (in seconds) until hello local Functions host is ready.</span></span>|
| **`--file -f`** | <span data-ttu-id="57c99-228">Здравствуйте toouse имя файла, как содержимое.</span><span class="sxs-lookup"><span data-stu-id="57c99-228">hello file name toouse as content.</span></span>|
| **`--no-interactive`** | <span data-ttu-id="57c99-229">Не запрашивает тип входных данных.</span><span class="sxs-lookup"><span data-stu-id="57c99-229">Does not prompt for input.</span></span> <span data-ttu-id="57c99-230">Полезно для сценариев автоматизации.</span><span class="sxs-lookup"><span data-stu-id="57c99-230">Useful for automation scenarios.</span></span>|

<span data-ttu-id="57c99-231">Например toocall функции активации HTTP и основной текст прохода, запустите следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="57c99-231">For example, toocall an HTTP-triggered function and pass content body, run hello following command:</span></span>

```
func run MyHttpTrigger -c '{\"name\": \"Azure\"}'
```

## <span data-ttu-id="57c99-232"><a name="publish"></a>Публикация tooAzure</span><span class="sxs-lookup"><span data-stu-id="57c99-232"><a name="publish"></a>Publish tooAzure</span></span>

<span data-ttu-id="57c99-233">toopublish приложении функция tooa функции проекта в Azure, используйте hello `publish` команды:</span><span class="sxs-lookup"><span data-stu-id="57c99-233">toopublish a Functions project tooa function app in Azure, use hello `publish` command:</span></span>

```
func azure functionapp publish <FunctionAppName>
```

<span data-ttu-id="57c99-234">Можно использовать следующие варианты hello.</span><span class="sxs-lookup"><span data-stu-id="57c99-234">You can use hello following options:</span></span>

| <span data-ttu-id="57c99-235">Параметр</span><span class="sxs-lookup"><span data-stu-id="57c99-235">Option</span></span>     | <span data-ttu-id="57c99-236">Описание</span><span class="sxs-lookup"><span data-stu-id="57c99-236">Description</span></span>                            |
| ------------ | -------------------------------------- |
| **`--publish-local-settings -i`** |  <span data-ttu-id="57c99-237">Параметры публикации в tooAzure local.settings.json, вывод запроса toooverwrite hello задание уже существует.</span><span class="sxs-lookup"><span data-stu-id="57c99-237">Publish settings in local.settings.json tooAzure, prompting toooverwrite if hello setting already exists.</span></span>|
| **`--overwrite-settings -y`** | <span data-ttu-id="57c99-238">Должен использоваться с `-i`.</span><span class="sxs-lookup"><span data-stu-id="57c99-238">Must be used with `-i`.</span></span> <span data-ttu-id="57c99-239">При другом значении перезаписывает локальное значение AppSettings в Azure.</span><span class="sxs-lookup"><span data-stu-id="57c99-239">Overwrites AppSettings in Azure with local value if different.</span></span> <span data-ttu-id="57c99-240">Значение по умолчанию — запрос.</span><span class="sxs-lookup"><span data-stu-id="57c99-240">Default is prompt.</span></span>|

<span data-ttu-id="57c99-241">Hello `publish` команда отправляет содержимое hello каталог проекта функции hello.</span><span class="sxs-lookup"><span data-stu-id="57c99-241">hello `publish` command uploads hello contents of hello Functions project directory.</span></span> <span data-ttu-id="57c99-242">При удалении файлов в локальной системе hello `publish` команда не удаляет их из Azure.</span><span class="sxs-lookup"><span data-stu-id="57c99-242">If you delete files locally, hello `publish` command does not delete them from Azure.</span></span> <span data-ttu-id="57c99-243">Можно удалить файлы в Azure с помощью hello [средство Kudu](functions-how-to-use-azure-function-app-settings.md#kudu) в hello [портал Azure].</span><span class="sxs-lookup"><span data-stu-id="57c99-243">You can delete files in Azure by using hello [Kudu tool](functions-how-to-use-azure-function-app-settings.md#kudu) in hello [Azure portal].</span></span>

## <a name="next-steps"></a><span data-ttu-id="57c99-244">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="57c99-244">Next steps</span></span>

<span data-ttu-id="57c99-245">Основные инструменты службы "Функции Azure" [имеют открытый код и размещаются на GitHub](https://github.com/azure/azure-functions-cli).</span><span class="sxs-lookup"><span data-stu-id="57c99-245">Azure Functions Core Tools is [open source and hosted on GitHub](https://github.com/azure/azure-functions-cli).</span></span>  
<span data-ttu-id="57c99-246">запрос ошибку или компонент toofile [откройте вопрос GitHub](https://github.com/azure/azure-functions-cli/issues).</span><span class="sxs-lookup"><span data-stu-id="57c99-246">toofile a bug or feature request, [open a GitHub issue](https://github.com/azure/azure-functions-cli/issues).</span></span> 

<!-- LINKS -->

[основные инструменты Azure функции]: https://www.npmjs.com/package/azure-functions-core-tools
[портал Azure]: https://portal.azure.com 
