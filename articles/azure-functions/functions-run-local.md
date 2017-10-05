---
title: "Разработка и выполнение Функций Azure локально | Документация Майкрософт"
description: "Узнайте, как программировать и тестировать функции Azure на локальном компьютере перед их запуском в Функциях Azure."
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
ms.openlocfilehash: bbe03973dbd7c70463caa6d1a45efae2ec722c05
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="code-and-test-azure-functions-locally"></a><span data-ttu-id="b5d5f-103">Как программировать и тестировать функции Azure в локальной среде</span><span class="sxs-lookup"><span data-stu-id="b5d5f-103">Code and test Azure functions locally</span></span>

<span data-ttu-id="b5d5f-104">Хотя на [портале Azure] имеется полный набор средств для разработки и тестирования Функций Azure, многие разработчики предпочитают локальную среду разработки.</span><span class="sxs-lookup"><span data-stu-id="b5d5f-104">While the [Azure portal] provides a full set of tools for developing and testing Azure Functions, many developers prefer a local development experience.</span></span> <span data-ttu-id="b5d5f-105">Функции Azure позволяют легко использовать любой редактор кода и локальные средства разработки для разработки и тестирования функций на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="b5d5f-105">Azure Functions makes it easy to use your favorite code editor and local development tools to develop and test your functions on your local computer.</span></span> <span data-ttu-id="b5d5f-106">Функции могут вызывать события в Azure, а вы можете отлаживать функции C# и JavaScript на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="b5d5f-106">Your functions can trigger on events in Azure, and you can debug your C# and JavaScript functions on your local computer.</span></span> 

<span data-ttu-id="b5d5f-107">Если вы используете Visual Studio C# для разработки, Функции Azure также [интегрируются с Visual Studio 2017](functions-develop-vs.md).</span><span class="sxs-lookup"><span data-stu-id="b5d5f-107">If you are a Visual Studio C# developer, Azure Functions also [integrates with Visual Studio 2017](functions-develop-vs.md).</span></span>

## <a name="install-the-azure-functions-core-tools"></a><span data-ttu-id="b5d5f-108">Установка основных инструментов Функций Azure</span><span class="sxs-lookup"><span data-stu-id="b5d5f-108">Install the Azure Functions Core Tools</span></span>

<span data-ttu-id="b5d5f-109">Основные инструменты службы "Функции Azure" являются локальной версией среды выполнения службы "Функции Azure", которые можно запускать на локальном компьютере Windows.</span><span class="sxs-lookup"><span data-stu-id="b5d5f-109">Azure Functions Core Tools is a local version of the Azure Functions runtime that you can run on your local Windows computer.</span></span> <span data-ttu-id="b5d5f-110">Это не эмулятор или симулятор.</span><span class="sxs-lookup"><span data-stu-id="b5d5f-110">It's not an emulator or simulator.</span></span> <span data-ttu-id="b5d5f-111">Это та же среда выполнения, которая используется в Функциях Azure.</span><span class="sxs-lookup"><span data-stu-id="b5d5f-111">It's the same runtime that powers Functions in Azure.</span></span>

<span data-ttu-id="b5d5f-112">[Основные инструменты Функций Azure] предоставляются в виде пакета npm.</span><span class="sxs-lookup"><span data-stu-id="b5d5f-112">The [Azure Functions Core Tools] is provided as an npm package.</span></span> <span data-ttu-id="b5d5f-113">Сначала необходимо [установить NodeJS](https://docs.npmjs.com/getting-started/installing-node), в состав которого входит npm.</span><span class="sxs-lookup"><span data-stu-id="b5d5f-113">You must first [install NodeJS](https://docs.npmjs.com/getting-started/installing-node), which includes npm.</span></span>  

>[!NOTE]
><span data-ttu-id="b5d5f-114">В настоящее время пакет основных инструментов Функций Azure можно установить только на компьютерах Windows.</span><span class="sxs-lookup"><span data-stu-id="b5d5f-114">At this time, the Azure Functions Core Tools package can only be installed on Windows computers.</span></span> <span data-ttu-id="b5d5f-115">Это связано с временным ограничением в узле Функций.</span><span class="sxs-lookup"><span data-stu-id="b5d5f-115">This restriction is due to a temporary limitation in the Functions host.</span></span>

<span data-ttu-id="b5d5f-116">[Основные инструменты Функций Azure] добавляют следующие псевдонимы команд:</span><span class="sxs-lookup"><span data-stu-id="b5d5f-116">[Azure Functions Core Tools] adds the following command aliases:</span></span>
* <span data-ttu-id="b5d5f-117">**func**</span><span class="sxs-lookup"><span data-stu-id="b5d5f-117">**func**</span></span>
* <span data-ttu-id="b5d5f-118">**azfun**</span><span class="sxs-lookup"><span data-stu-id="b5d5f-118">**azfun**</span></span>
* <span data-ttu-id="b5d5f-119">**azurefunctions**</span><span class="sxs-lookup"><span data-stu-id="b5d5f-119">**azurefunctions**</span></span>

<span data-ttu-id="b5d5f-120">Все эти псевдонимы можно использовать вместо команд `func`, показанных в примерах в этой статье.</span><span class="sxs-lookup"><span data-stu-id="b5d5f-120">All of these alias can be used instead of `func` shown in the examples in this topic.</span></span>

## <a name="create-a-local-functions-project"></a><span data-ttu-id="b5d5f-121">Создание локального проекта службы "Функции"</span><span class="sxs-lookup"><span data-stu-id="b5d5f-121">Create a local Functions project</span></span>

<span data-ttu-id="b5d5f-122">В локальном режиме работы проект службы "Функции" является каталогом, в котором находятся файлы host.json и local.settings.json.</span><span class="sxs-lookup"><span data-stu-id="b5d5f-122">When running locally, a Functions project is a directory that has the files host.json and local.settings.json.</span></span> <span data-ttu-id="b5d5f-123">Этот каталог является эквивалентом приложения-функции в Azure.</span><span class="sxs-lookup"><span data-stu-id="b5d5f-123">This directory is the equivalent of a function app in Azure.</span></span> <span data-ttu-id="b5d5f-124">Дополнительные сведения о структуре папок службы "Функции Azure" см. в [этом разделе](functions-reference.md#folder-structure).</span><span class="sxs-lookup"><span data-stu-id="b5d5f-124">To learn more about the Azure Functions folder structure, see the [Azure Functions developers guide](functions-reference.md#folder-structure).</span></span>

<span data-ttu-id="b5d5f-125">В командной строке выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="b5d5f-125">At a command prompt, run the following command:</span></span>

```
func init MyFunctionProj
```

<span data-ttu-id="b5d5f-126">Выходные данные выглядят так:</span><span class="sxs-lookup"><span data-stu-id="b5d5f-126">The output looks like the following example:</span></span>

```
Writing .gitignore
Writing host.json
Writing local.settings.json
Created launch.json
Initialized empty Git repository in D:/Code/Playground/MyFunctionProj/.git/
```

<span data-ttu-id="b5d5f-127">Чтобы отказаться от создания репозитория, используйте параметр `--no-source-control [-n]`.</span><span class="sxs-lookup"><span data-stu-id="b5d5f-127">To opt out of creating a Git repository, use the option `--no-source-control [-n]`.</span></span>

<a name="local-settings"></a>

## <a name="local-settings-file"></a><span data-ttu-id="b5d5f-128">Файл с локальными параметрами</span><span class="sxs-lookup"><span data-stu-id="b5d5f-128">Local settings file</span></span>

<span data-ttu-id="b5d5f-129">Файл local.settings.json хранит параметры приложения, строки подключения и параметры основных инструментов службы "Функции Azure".</span><span class="sxs-lookup"><span data-stu-id="b5d5f-129">The file local.settings.json stores app settings, connection strings, and settings for Azure Functions Core Tools.</span></span> <span data-ttu-id="b5d5f-130">Он имеет следующую структуру:</span><span class="sxs-lookup"><span data-stu-id="b5d5f-130">It has the following structure:</span></span>

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
| <span data-ttu-id="b5d5f-131">Настройка</span><span class="sxs-lookup"><span data-stu-id="b5d5f-131">Setting</span></span>      | <span data-ttu-id="b5d5f-132">Описание</span><span class="sxs-lookup"><span data-stu-id="b5d5f-132">Description</span></span>                            |
| ------------ | -------------------------------------- |
| <span data-ttu-id="b5d5f-133">**IsEncrypted**</span><span class="sxs-lookup"><span data-stu-id="b5d5f-133">**IsEncrypted**</span></span> | <span data-ttu-id="b5d5f-134">Если задано значение **true**, все значения шифруются с помощью ключа локального компьютера.</span><span class="sxs-lookup"><span data-stu-id="b5d5f-134">When set to **true**, all values are encrypted using a local machine key.</span></span> <span data-ttu-id="b5d5f-135">Используется с командами `func settings`.</span><span class="sxs-lookup"><span data-stu-id="b5d5f-135">Used with `func settings` commands.</span></span> <span data-ttu-id="b5d5f-136">Значение по умолчанию — **false**.</span><span class="sxs-lookup"><span data-stu-id="b5d5f-136">Default value is **false**.</span></span> |
| <span data-ttu-id="b5d5f-137">**Значения**</span><span class="sxs-lookup"><span data-stu-id="b5d5f-137">**Values**</span></span> | <span data-ttu-id="b5d5f-138">Коллекция параметров приложения, используемых при локальном выполнении.</span><span class="sxs-lookup"><span data-stu-id="b5d5f-138">Collection of application settings used when running locally.</span></span> <span data-ttu-id="b5d5f-139">Добавьте параметры приложения в этот объект.</span><span class="sxs-lookup"><span data-stu-id="b5d5f-139">Add your application settings to this object.</span></span>  |
| <span data-ttu-id="b5d5f-140">**AzureWebJobsStorage**</span><span class="sxs-lookup"><span data-stu-id="b5d5f-140">**AzureWebJobsStorage**</span></span> | <span data-ttu-id="b5d5f-141">Задает строку подключения к учетной записи хранения Azure, которая используется в среде выполнения Функций Azure.</span><span class="sxs-lookup"><span data-stu-id="b5d5f-141">Sets the connection string to the Azure Storage account that is used internally by the Azure Functions runtime.</span></span> <span data-ttu-id="b5d5f-142">Эта учетная запись хранения поддерживает триггеры функций.</span><span class="sxs-lookup"><span data-stu-id="b5d5f-142">The storage account supports your function's triggers.</span></span> <span data-ttu-id="b5d5f-143">Параметр подключения к учетной записи хранения необходим для всех функций, кроме функций, активируемых протоколом HTTP.</span><span class="sxs-lookup"><span data-stu-id="b5d5f-143">This storage account connection setting is required for all functions except for HTTP triggered functions.</span></span>  |
| <span data-ttu-id="b5d5f-144">**AzureWebJobsDashboard**</span><span class="sxs-lookup"><span data-stu-id="b5d5f-144">**AzureWebJobsDashboard**</span></span> | <span data-ttu-id="b5d5f-145">Задает строку подключения к учетной записи хранения Azure, которая используется для хранения журналов функций.</span><span class="sxs-lookup"><span data-stu-id="b5d5f-145">Sets the connection string to the Azure Storage account that is used to store the function logs.</span></span> <span data-ttu-id="b5d5f-146">Это необязательное значение обеспечивает доступ к журналам на портале.</span><span class="sxs-lookup"><span data-stu-id="b5d5f-146">This optional value makes the logs accessible in the portal.</span></span>|
| <span data-ttu-id="b5d5f-147">**Host**</span><span class="sxs-lookup"><span data-stu-id="b5d5f-147">**Host**</span></span> | <span data-ttu-id="b5d5f-148">Параметры в этом разделе служат для настройки хост-процесса Функций при выполнении в локальной среде.</span><span class="sxs-lookup"><span data-stu-id="b5d5f-148">Settings in this section customize the Functions host process when running locally.</span></span> | 
| <span data-ttu-id="b5d5f-149">**LocalHttpPort**</span><span class="sxs-lookup"><span data-stu-id="b5d5f-149">**LocalHttpPort**</span></span> | <span data-ttu-id="b5d5f-150">Задает порт по умолчанию, используемый при выполнении локального узла Функций (`func host start` и `func run`).</span><span class="sxs-lookup"><span data-stu-id="b5d5f-150">Sets the default port used when running the local Functions host (`func host start` and `func run`).</span></span> <span data-ttu-id="b5d5f-151">Параметр командной строки `--port` имеет приоритет над этим значением.</span><span class="sxs-lookup"><span data-stu-id="b5d5f-151">The `--port` command-line option takes precedence over this value.</span></span> |
| <span data-ttu-id="b5d5f-152">**CORS**</span><span class="sxs-lookup"><span data-stu-id="b5d5f-152">**CORS**</span></span> | <span data-ttu-id="b5d5f-153">Определяет источники, для которых разрешен [общий доступ к ресурсам независимо от источника (CORS)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing).</span><span class="sxs-lookup"><span data-stu-id="b5d5f-153">Defines the origins allowed for [cross-origin resource sharing (CORS)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing).</span></span> <span data-ttu-id="b5d5f-154">Источники указываются в виде разделенного запятыми списка без пробелов.</span><span class="sxs-lookup"><span data-stu-id="b5d5f-154">Origins are supplied as a comma-separated list with no spaces.</span></span> <span data-ttu-id="b5d5f-155">Допускается подстановочное значение (**\***), разрешающее запросы из любого источника.</span><span class="sxs-lookup"><span data-stu-id="b5d5f-155">The wildcard value (**\***) is supported, which allows requests from any origin.</span></span> |
| <span data-ttu-id="b5d5f-156">**ConnectionStrings**</span><span class="sxs-lookup"><span data-stu-id="b5d5f-156">**ConnectionStrings**</span></span> | <span data-ttu-id="b5d5f-157">Содержит строки подключения к базе данных для функций.</span><span class="sxs-lookup"><span data-stu-id="b5d5f-157">Contains the database connection strings for your functions.</span></span> <span data-ttu-id="b5d5f-158">Строки подключения, содержащиеся в этом объекте, добавляются в среду с типом поставщика **System.Data.SqlClient**.</span><span class="sxs-lookup"><span data-stu-id="b5d5f-158">Connection strings in this object are added to the environment with the provider type of **System.Data.SqlClient**.</span></span>  | 

<span data-ttu-id="b5d5f-159">Большинство триггеров и привязок имеют свойство **Connection**, которое сопоставляется с именем переменной среды или параметра приложения.</span><span class="sxs-lookup"><span data-stu-id="b5d5f-159">Most triggers and bindings have a **Connection** property that maps to the name of an environment variable or app setting.</span></span> <span data-ttu-id="b5d5f-160">Для каждого свойства подключения должен быть определен параметр в файле local.settings.json.</span><span class="sxs-lookup"><span data-stu-id="b5d5f-160">For each connection property, there must be app setting defined in local.settings.json file.</span></span> 

<span data-ttu-id="b5d5f-161">Эти параметры также могут считываться в коде как переменные среды.</span><span class="sxs-lookup"><span data-stu-id="b5d5f-161">These settings can also be read in your code as environment variables.</span></span> <span data-ttu-id="b5d5f-162">В C# используйте [System.Environment.GetEnvironmentVariable](https://msdn.microsoft.com/library/system.environment.getenvironmentvariable(v=vs.110).aspx) или [ConfigurationManager.AppSettings](https://msdn.microsoft.com/library/system.configuration.configurationmanager.appsettings%28v=vs.110%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="b5d5f-162">In C#, use [System.Environment.GetEnvironmentVariable](https://msdn.microsoft.com/library/system.environment.getenvironmentvariable(v=vs.110).aspx) or [ConfigurationManager.AppSettings](https://msdn.microsoft.com/library/system.configuration.configurationmanager.appsettings%28v=vs.110%29.aspx).</span></span> <span data-ttu-id="b5d5f-163">Для JavaScript используйте `process.env`.</span><span class="sxs-lookup"><span data-stu-id="b5d5f-163">In JavaScript, use `process.env`.</span></span> <span data-ttu-id="b5d5f-164">Параметры, указанные как системные переменные среды, имеют приоритет над значениями в файле local.settings.json.</span><span class="sxs-lookup"><span data-stu-id="b5d5f-164">Settings specified as a system environment variable take precedence over values in the local.settings.json file.</span></span> 

<span data-ttu-id="b5d5f-165">Параметры в файле local.settings.json используются инструментами Функций только при выполнении в локальной среде.</span><span class="sxs-lookup"><span data-stu-id="b5d5f-165">Settings in the local.settings.json file are only used by Functions tools when running locally.</span></span> <span data-ttu-id="b5d5f-166">По умолчанию эти параметры не переносятся автоматически при публикации проекта в Azure.</span><span class="sxs-lookup"><span data-stu-id="b5d5f-166">By default, these settings are not migrated automatically when the project is published to Azure.</span></span> <span data-ttu-id="b5d5f-167">[При публикации](#publish) используйте параметр `--publish-local-settings`, чтобы добавить эти параметры в приложение-функцию в Azure.</span><span class="sxs-lookup"><span data-stu-id="b5d5f-167">Use the `--publish-local-settings` switch [when you publish](#publish) to make sure these settings are added to the function app in Azure.</span></span>

<span data-ttu-id="b5d5f-168">Если для **AzureWebJobsStorage** не задана допустимая строка подключения к хранилищу, выводится следующее сообщение об ошибке:</span><span class="sxs-lookup"><span data-stu-id="b5d5f-168">When no valid storage connection string is set for **AzureWebJobsStorage**, the following error message is shown:</span></span>  

><span data-ttu-id="b5d5f-169">Отсутствует значение AzureWebJobsStorage в local.settings.json.</span><span class="sxs-lookup"><span data-stu-id="b5d5f-169">Missing value for AzureWebJobsStorage in local.settings.json.</span></span> <span data-ttu-id="b5d5f-170">This is required for all triggers other than HTTP.</span><span class="sxs-lookup"><span data-stu-id="b5d5f-170">This is required for all triggers other than HTTP.</span></span> <span data-ttu-id="b5d5f-171">Выполните команду "func azure functionary fetch-app-settings <functionAppName>" или укажите строку подключения в файле local.settings.json.</span><span class="sxs-lookup"><span data-stu-id="b5d5f-171">You can run 'func azure functionary fetch-app-settings <functionAppName>' or specify a connection string in local.settings.json.</span></span>
  
[!INCLUDE [Note to not use local storage](../../includes/functions-local-settings-note.md)]

### <a name="configure-app-settings"></a><span data-ttu-id="b5d5f-172">Настройка параметров приложения</span><span class="sxs-lookup"><span data-stu-id="b5d5f-172">Configure app settings</span></span>

<span data-ttu-id="b5d5f-173">Чтобы задать значение для строки подключения, выполните одно из следующих действий.</span><span class="sxs-lookup"><span data-stu-id="b5d5f-173">To set a value for connection strings, you can do one of the following:</span></span>
* <span data-ttu-id="b5d5f-174">Введите строку подключения из [обозревателя хранилищ Azure](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="b5d5f-174">Enter the connection string from [Azure Storage Explorer](http://storageexplorer.com/).</span></span>
* <span data-ttu-id="b5d5f-175">Используйте одну из следующих команд:</span><span class="sxs-lookup"><span data-stu-id="b5d5f-175">Use one of the following commands:</span></span>

    ```
    func azure functionapp fetch-app-settings <FunctionAppName>
    ```
    ```
    func azure functionapp storage fetch-connection-string <StorageAccountName>
    ```
    <span data-ttu-id="b5d5f-176">Обе команды требуют сначала выполнить вход в Azure.</span><span class="sxs-lookup"><span data-stu-id="b5d5f-176">Both commands require you to first sign-in to Azure.</span></span>

## <a name="create-a-function"></a><span data-ttu-id="b5d5f-177">Создание функции</span><span class="sxs-lookup"><span data-stu-id="b5d5f-177">Create a function</span></span>

<span data-ttu-id="b5d5f-178">Чтобы создать функцию, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="b5d5f-178">To create a function, run the following command:</span></span>

```
func new
``` 
<span data-ttu-id="b5d5f-179">`func new` имеет указанные ниже необязательные аргументы.</span><span class="sxs-lookup"><span data-stu-id="b5d5f-179">`func new` supports the following optional arguments:</span></span>

| <span data-ttu-id="b5d5f-180">Аргумент</span><span class="sxs-lookup"><span data-stu-id="b5d5f-180">Argument</span></span>     | <span data-ttu-id="b5d5f-181">Описание</span><span class="sxs-lookup"><span data-stu-id="b5d5f-181">Description</span></span>                            |
| ------------ | -------------------------------------- |
| **`--language -l`** | <span data-ttu-id="b5d5f-182">Язык программирования шаблона, например C#, F# или JavaScript.</span><span class="sxs-lookup"><span data-stu-id="b5d5f-182">The template programming language, such as C#, F#, or JavaScript.</span></span> |
| **`--template -t`** | <span data-ttu-id="b5d5f-183">Имя шаблона.</span><span class="sxs-lookup"><span data-stu-id="b5d5f-183">The template name.</span></span> |
| **`--name -n`** | <span data-ttu-id="b5d5f-184">Имя функции.</span><span class="sxs-lookup"><span data-stu-id="b5d5f-184">The function name.</span></span> |

<span data-ttu-id="b5d5f-185">Например, чтобы создать триггер HTTP на JavaScript, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="b5d5f-185">For example, to create a JavaScript HTTP trigger, run:</span></span>

```
func new --language JavaScript --template HttpTrigger --name MyHttpTrigger
```

<span data-ttu-id="b5d5f-186">Чтобы создать функцию, активируемую с помощью очереди, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="b5d5f-186">To create a queue-triggered function, run:</span></span>

```
func new --language JavaScript --template QueueTrigger --name QueueTriggerJS
```

## <a name="run-functions-locally"></a><span data-ttu-id="b5d5f-187">Запуск функций в локальной среде</span><span class="sxs-lookup"><span data-stu-id="b5d5f-187">Run functions locally</span></span>

<span data-ttu-id="b5d5f-188">Чтобы запустить проект службы "Функции", запустите узел этой службы.</span><span class="sxs-lookup"><span data-stu-id="b5d5f-188">To run a Functions project, run the Functions host.</span></span> <span data-ttu-id="b5d5f-189">Узел включает триггеры для всех функций в проекте.</span><span class="sxs-lookup"><span data-stu-id="b5d5f-189">The host enables triggers for all functions in the project:</span></span>

```
func host start
```

<span data-ttu-id="b5d5f-190">`func host start` имеет указанные ниже параметры.</span><span class="sxs-lookup"><span data-stu-id="b5d5f-190">`func host start` supports the following options:</span></span>

| <span data-ttu-id="b5d5f-191">Параметр</span><span class="sxs-lookup"><span data-stu-id="b5d5f-191">Option</span></span>     | <span data-ttu-id="b5d5f-192">Описание</span><span class="sxs-lookup"><span data-stu-id="b5d5f-192">Description</span></span>                            |
| ------------ | -------------------------------------- |
|**`--port -p`** | <span data-ttu-id="b5d5f-193">Локальный порт для прослушивания.</span><span class="sxs-lookup"><span data-stu-id="b5d5f-193">The local port to listen on.</span></span> <span data-ttu-id="b5d5f-194">Значение по умолчанию: 7071.</span><span class="sxs-lookup"><span data-stu-id="b5d5f-194">Default value: 7071.</span></span> |
| **`--debug <type>`** | <span data-ttu-id="b5d5f-195">Возможные значения: `VSCode` и `VS`.</span><span class="sxs-lookup"><span data-stu-id="b5d5f-195">The options are `VSCode` and `VS`.</span></span> |
| **`--cors`** | <span data-ttu-id="b5d5f-196">Список разрешенных источников CORS, разделенный запятыми без пробелов.</span><span class="sxs-lookup"><span data-stu-id="b5d5f-196">A comma-separated list of CORS origins, with no spaces.</span></span> |
| **`--nodeDebugPort -n`** | <span data-ttu-id="b5d5f-197">Порт отладчика узла.</span><span class="sxs-lookup"><span data-stu-id="b5d5f-197">The port for the node debugger to use.</span></span> <span data-ttu-id="b5d5f-198">Значение по умолчанию — значение из launch.json или 5858.</span><span class="sxs-lookup"><span data-stu-id="b5d5f-198">Default: A value from launch.json or 5858.</span></span> |
| **`--debugLevel -d`** | <span data-ttu-id="b5d5f-199">Уровень трассировки консоли (off, verbose, info, warning или error).</span><span class="sxs-lookup"><span data-stu-id="b5d5f-199">The console trace level (off, verbose, info, warning, or error).</span></span> <span data-ttu-id="b5d5f-200">Значение по умолчанию — info.</span><span class="sxs-lookup"><span data-stu-id="b5d5f-200">Default: Info.</span></span>|
| **`--timeout -t`** | <span data-ttu-id="b5d5f-201">Время ожидания для запуска узла Функций в секундах.</span><span class="sxs-lookup"><span data-stu-id="b5d5f-201">The time out for the Functions host t     o start, in seconds.</span></span> <span data-ttu-id="b5d5f-202">Значение по умолчанию — 20 секунд.</span><span class="sxs-lookup"><span data-stu-id="b5d5f-202">Default: 20 seconds.</span></span>|
| **`--useHttps`** | <span data-ttu-id="b5d5f-203">Привязка к https://localhost:{port}, а не к http://localhost:{port}.</span><span class="sxs-lookup"><span data-stu-id="b5d5f-203">Bind to https://localhost:{port} rather than to http://localhost:{port}.</span></span> <span data-ttu-id="b5d5f-204">По умолчанию этот параметр создает доверенный сертификат на компьютере.</span><span class="sxs-lookup"><span data-stu-id="b5d5f-204">By default, this option creates a trusted certificate on your computer.</span></span>|
| **`--pause-on-error`** | <span data-ttu-id="b5d5f-205">Приостановка для получения дополнительных входных данных перед выходом из процесса.</span><span class="sxs-lookup"><span data-stu-id="b5d5f-205">Pause for additional input before exiting the process.</span></span> <span data-ttu-id="b5d5f-206">Это удобно при запуске основных инструментов службы "Функции Azure" из интегрированной среды разработки (IDE).</span><span class="sxs-lookup"><span data-stu-id="b5d5f-206">Useful when launching Azure Functions Core Tools from an integrated development environment (IDE).</span></span>|

<span data-ttu-id="b5d5f-207">При запуске узла службы "Функции" выводится URL-адрес функций, активируемых по HTTP:</span><span class="sxs-lookup"><span data-stu-id="b5d5f-207">When the Functions host starts, it outputs the URL of HTTP-triggered functions:</span></span>

```
Found the following functions:
Host.Functions.MyHttpTrigger

ob host started
Http Function MyHttpTrigger: http://localhost:7071/api/MyHttpTrigger
```

### <a name="debug-in-vs-code-or-visual-studio"></a><span data-ttu-id="b5d5f-208">Отладка в VS Code или Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b5d5f-208">Debug in VS Code or Visual Studio</span></span>

<span data-ttu-id="b5d5f-209">Чтобы подключить отладчик, передайте аргумент `--debug`.</span><span class="sxs-lookup"><span data-stu-id="b5d5f-209">To attach a debugger, pass the `--debug` argument.</span></span> <span data-ttu-id="b5d5f-210">Для отладки функций на JavaScript используйте код Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b5d5f-210">To debug JavaScript functions, use Visual Studio Code.</span></span> <span data-ttu-id="b5d5f-211">Для функций на C# используйте Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b5d5f-211">For C# functions, use Visual Studio.</span></span>

<span data-ttu-id="b5d5f-212">Для отладки функции на C# используйте `--debug vs`.</span><span class="sxs-lookup"><span data-stu-id="b5d5f-212">To debug C# functions, use `--debug vs`.</span></span> <span data-ttu-id="b5d5f-213">Кроме того, можно использовать [инструменты Visual Studio 2017 для Функций Azure](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/).</span><span class="sxs-lookup"><span data-stu-id="b5d5f-213">You can also use [Azure Functions Visual Studio 2017 Tools](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/).</span></span> 

<span data-ttu-id="b5d5f-214">Для запуска узла и настройки отладки JavaScript выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="b5d5f-214">To launch the host and set up JavaScript debugging, run:</span></span>

```
func host start --debug vscode
```

<span data-ttu-id="b5d5f-215">Затем в коде Visual Studio в представлении **Отладка** выберите **Attach to Azure Functions** (Присоединение к службе "Функции Azure").</span><span class="sxs-lookup"><span data-stu-id="b5d5f-215">Then, in Visual Studio Code, in the **Debug** view, select **Attach to Azure Functions**.</span></span> <span data-ttu-id="b5d5f-216">Вы можете присоединить точки останова, просмотреть значения переменных и осуществить пошаговое выполнение кода.</span><span class="sxs-lookup"><span data-stu-id="b5d5f-216">You can attach breakpoints, inspect variables, and step through code.</span></span>

![Отладка с помощью Visual Studio 2015](./media/functions-run-local/vscode-javascript-debugging.png)

### <a name="passing-test-data-to-a-function"></a><span data-ttu-id="b5d5f-218">Передача тестовых данных в функцию</span><span class="sxs-lookup"><span data-stu-id="b5d5f-218">Passing test data to a function</span></span>

<span data-ttu-id="b5d5f-219">Вы также можете вызвать функцию напрямую с помощью `func run <FunctionName>` и предоставить входные данные для нее.</span><span class="sxs-lookup"><span data-stu-id="b5d5f-219">You can also invoke a function directly by using `func run <FunctionName>` and provide input data for the function.</span></span> <span data-ttu-id="b5d5f-220">Эта команда аналогична выполнению функции с помощью вкладки **Тест** на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="b5d5f-220">This command is similar to running a function using the **Test** tab in the Azure portal.</span></span> <span data-ttu-id="b5d5f-221">Эта команда запускает весь узел службы "Функции".</span><span class="sxs-lookup"><span data-stu-id="b5d5f-221">This command launches the entire Functions host.</span></span>

<span data-ttu-id="b5d5f-222">`func run` имеет указанные ниже параметры.</span><span class="sxs-lookup"><span data-stu-id="b5d5f-222">`func run` supports the following options:</span></span>

| <span data-ttu-id="b5d5f-223">Параметр</span><span class="sxs-lookup"><span data-stu-id="b5d5f-223">Option</span></span>     | <span data-ttu-id="b5d5f-224">Описание</span><span class="sxs-lookup"><span data-stu-id="b5d5f-224">Description</span></span>                            |
| ------------ | -------------------------------------- |
| **`--content -c`** | <span data-ttu-id="b5d5f-225">Встроенное содержимое.</span><span class="sxs-lookup"><span data-stu-id="b5d5f-225">Inline content.</span></span> |
| **`--debug -d`** | <span data-ttu-id="b5d5f-226">Подключение отладчика к хост-процессу перед выполнением функции.</span><span class="sxs-lookup"><span data-stu-id="b5d5f-226">Attach a debugger to the host process before running the function.</span></span>|
| **`--timeout -t`** | <span data-ttu-id="b5d5f-227">Время ожидания (в секундах), пока не будет готов локальный узел службы "Функции".</span><span class="sxs-lookup"><span data-stu-id="b5d5f-227">Time to wait (in seconds) until the local Functions host is ready.</span></span>|
| **`--file -f`** | <span data-ttu-id="b5d5f-228">Имя файла для использования в качестве содержимого.</span><span class="sxs-lookup"><span data-stu-id="b5d5f-228">The file name to use as content.</span></span>|
| **`--no-interactive`** | <span data-ttu-id="b5d5f-229">Не запрашивает тип входных данных.</span><span class="sxs-lookup"><span data-stu-id="b5d5f-229">Does not prompt for input.</span></span> <span data-ttu-id="b5d5f-230">Полезно для сценариев автоматизации.</span><span class="sxs-lookup"><span data-stu-id="b5d5f-230">Useful for automation scenarios.</span></span>|

<span data-ttu-id="b5d5f-231">Например, для вызова функции, активируемой по HTTP, и передачи основного содержимого выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="b5d5f-231">For example, to call an HTTP-triggered function and pass content body, run the following command:</span></span>

```
func run MyHttpTrigger -c '{\"name\": \"Azure\"}'
```

## <span data-ttu-id="b5d5f-232"><a name="publish"></a>Публикация в Azure</span><span class="sxs-lookup"><span data-stu-id="b5d5f-232"><a name="publish"></a>Publish to Azure</span></span>

<span data-ttu-id="b5d5f-233">Чтобы опубликовать проект функций для приложения-функции в Azure, используйте команду `publish`:</span><span class="sxs-lookup"><span data-stu-id="b5d5f-233">To publish a Functions project to a function app in Azure, use the `publish` command:</span></span>

```
func azure functionapp publish <FunctionAppName>
```

<span data-ttu-id="b5d5f-234">Можно использовать приведенные ниже параметры.</span><span class="sxs-lookup"><span data-stu-id="b5d5f-234">You can use the following options:</span></span>

| <span data-ttu-id="b5d5f-235">Параметр</span><span class="sxs-lookup"><span data-stu-id="b5d5f-235">Option</span></span>     | <span data-ttu-id="b5d5f-236">Описание</span><span class="sxs-lookup"><span data-stu-id="b5d5f-236">Description</span></span>                            |
| ------------ | -------------------------------------- |
| **`--publish-local-settings -i`** |  <span data-ttu-id="b5d5f-237">Публикация параметров из файла local.settings.json в Azure с запросом на перезапись, если параметр уже существует.</span><span class="sxs-lookup"><span data-stu-id="b5d5f-237">Publish settings in local.settings.json to Azure, prompting to overwrite if the setting already exists.</span></span>|
| **`--overwrite-settings -y`** | <span data-ttu-id="b5d5f-238">Должен использоваться с `-i`.</span><span class="sxs-lookup"><span data-stu-id="b5d5f-238">Must be used with `-i`.</span></span> <span data-ttu-id="b5d5f-239">При другом значении перезаписывает локальное значение AppSettings в Azure.</span><span class="sxs-lookup"><span data-stu-id="b5d5f-239">Overwrites AppSettings in Azure with local value if different.</span></span> <span data-ttu-id="b5d5f-240">Значение по умолчанию — запрос.</span><span class="sxs-lookup"><span data-stu-id="b5d5f-240">Default is prompt.</span></span>|

<span data-ttu-id="b5d5f-241">Команда `publish` отправляет содержимое в каталог проекта функций.</span><span class="sxs-lookup"><span data-stu-id="b5d5f-241">The `publish` command uploads the contents of the Functions project directory.</span></span> <span data-ttu-id="b5d5f-242">При удалении файлов в локальной среде команда `publish` не удаляет их из Azure.</span><span class="sxs-lookup"><span data-stu-id="b5d5f-242">If you delete files locally, the `publish` command does not delete them from Azure.</span></span> <span data-ttu-id="b5d5f-243">Удалить файлы в Azure можно с помощью [средства Kudu](functions-how-to-use-azure-function-app-settings.md#kudu) на [портале Azure].</span><span class="sxs-lookup"><span data-stu-id="b5d5f-243">You can delete files in Azure by using the [Kudu tool](functions-how-to-use-azure-function-app-settings.md#kudu) in the [Azure portal].</span></span>

## <a name="next-steps"></a><span data-ttu-id="b5d5f-244">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b5d5f-244">Next steps</span></span>

<span data-ttu-id="b5d5f-245">Основные инструменты службы "Функции Azure" [имеют открытый код и размещаются на GitHub](https://github.com/azure/azure-functions-cli).</span><span class="sxs-lookup"><span data-stu-id="b5d5f-245">Azure Functions Core Tools is [open source and hosted on GitHub](https://github.com/azure/azure-functions-cli).</span></span>  
<span data-ttu-id="b5d5f-246">Чтобы зарегистрировать ошибку или отправить запрос на функцию, [откройте вопрос на GitHub](https://github.com/azure/azure-functions-cli/issues).</span><span class="sxs-lookup"><span data-stu-id="b5d5f-246">To file a bug or feature request, [open a GitHub issue](https://github.com/azure/azure-functions-cli/issues).</span></span> 

<!-- LINKS -->

[Основные инструменты Функций Azure]: https://www.npmjs.com/package/azure-functions-core-tools
[портале Azure]: https://portal.azure.com 
