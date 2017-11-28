---
title: "Приступая к работе с метаданными OpenAPI в Функциях Azure | Документация Майкрософт"
description: "Приступая к работе со средством поддержки OpenAPI в Функциях Azure"
services: functions
documentationcenter: 
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 03/23/2017
ms.author: alkarche
ms.openlocfilehash: 9b861aacf31e17866293732dc2323f56014c1877
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="creating-openapi-20-swagger-metadata-for-a-function-app-preview"></a><span data-ttu-id="cf8b0-103">Создание метаданных OpenAPI 2.0 (Swagger) для приложения-функции (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="cf8b0-103">Creating OpenAPI 2.0 (Swagger) Metadata for a Function App (Preview)</span></span>

<span data-ttu-id="cf8b0-104">В этом документе описан пошаговый процесс создания определения OpenAPI для простого интерфейса API, размещенного в Функциях Azure.</span><span class="sxs-lookup"><span data-stu-id="cf8b0-104">This document guides you through the step by step process of creating an OpenAPI Definition for a simple API hosted on Azure Functions.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

### <a name="what-is-openapi-swagger"></a><span data-ttu-id="cf8b0-105">Общие сведения об OpenAPI (Swagger)</span><span class="sxs-lookup"><span data-stu-id="cf8b0-105">What is OpenAPI (Swagger)?</span></span>
<span data-ttu-id="cf8b0-106">[Метаданные Swagger](http://swagger.io/) — это файл, который определяет функциональные возможности и режимы работы интерфейса API и позволяет другому программному обеспечению использовать функцию размещения REST API.</span><span class="sxs-lookup"><span data-stu-id="cf8b0-106">[Swagger Metadata](http://swagger.io/) is a file that defines the functionality and operating modes of your API, and allows a function hosting a REST API to be consumed by a wide variety of other software.</span></span> <span data-ttu-id="cf8b0-107">Такие предложения Майкрософт, как PowerApps и [приложения API](https://docs.microsoft.com/azure/app-service-api/app-service-api-dotnet-get-started#a-idcodegena-generate-client-code-for-the-data-tier), а также сторонние инструменты для разработчиков, например [Postman](https://www.getpostman.com/docs/importing_swagger) и [многие другие пакеты](http://swagger.io/tools/), позволяют использовать API с помощью определения Swagger.</span><span class="sxs-lookup"><span data-stu-id="cf8b0-107">Microsoft offerings like PowerApps and [API Apps](https://docs.microsoft.com/azure/app-service-api/app-service-api-dotnet-get-started#a-idcodegena-generate-client-code-for-the-data-tier), as well as 3rd party developer tooling like [Postman](https://www.getpostman.com/docs/importing_swagger) and [many more packages](http://swagger.io/tools/) all allow your API to be consumed with a Swagger definition.</span></span>

## <span data-ttu-id="cf8b0-108"><a name="prepare-function"></a>Создание функции с простым интерфейсом API</span><span class="sxs-lookup"><span data-stu-id="cf8b0-108"><a name="prepare-function"></a>Creating a Function with a simple API</span></span>
  <span data-ttu-id="cf8b0-109">Чтобы создать определение OpenAPI, сначала необходимо создать функцию с простым интерфейсом API.</span><span class="sxs-lookup"><span data-stu-id="cf8b0-109">To create an OpenAPI definition, we first need to create a Function with a simple API.</span></span> <span data-ttu-id="cf8b0-110">Если интерфейс API уже размещен в приложении-функции, можете перейти непосредственно к следующему разделу.</span><span class="sxs-lookup"><span data-stu-id="cf8b0-110">If you already have an API hosted on a Function App, you can skip straight to the next section</span></span>
1. <span data-ttu-id="cf8b0-111">Создайте новое приложение-функцию.</span><span class="sxs-lookup"><span data-stu-id="cf8b0-111">Create a new Function App.</span></span>
    1. <span data-ttu-id="cf8b0-112">Перейдите на [портал Azure](https://portal.azure.com) > `+ New` и найдите "Приложение-функция".</span><span class="sxs-lookup"><span data-stu-id="cf8b0-112">[Azure portal](https://portal.azure.com) > `+ New` > Search for "Function App"</span></span>
1. <span data-ttu-id="cf8b0-113">Создайте новую функцию "Триггер HTTP" в новом приложении-функции.</span><span class="sxs-lookup"><span data-stu-id="cf8b0-113">Create a new HTTP trigger function inside your new Function App</span></span>
    1. <span data-ttu-id="cf8b0-114">Функция заранее заполняется кодом, определяющим очень простой интерфейс REST API.</span><span class="sxs-lookup"><span data-stu-id="cf8b0-114">Your function is pre-populated with code defining a very simple REST API.</span></span>
    1. <span data-ttu-id="cf8b0-115">Любая строка, переданная функции в качестве параметра запроса или в самом запросе, возвращается в виде "Hello {ввод}".</span><span class="sxs-lookup"><span data-stu-id="cf8b0-115">Any string passed to the Function as a query parameter or in the body is returned as "Hello {input}"</span></span>
1. <span data-ttu-id="cf8b0-116">Перейдите на вкладку `Integrate` новой функции "Триггер HTTP".</span><span class="sxs-lookup"><span data-stu-id="cf8b0-116">Go to the `Integrate` tab of your new HTTP Trigger function</span></span>
    1. <span data-ttu-id="cf8b0-117">Переведите переключатель `Allowed HTTP methods` в положение `Selected methods`.</span><span class="sxs-lookup"><span data-stu-id="cf8b0-117">Toggle `Allowed HTTP methods` to `Selected methods`</span></span>
    1. <span data-ttu-id="cf8b0-118">В `Selected HTTP methods` снимите флажки рядом со всеми командами, за исключением POST.</span><span class="sxs-lookup"><span data-stu-id="cf8b0-118">In `Selected HTTP methods` uncheck every verb except POST.</span></span>
    <span data-ttu-id="cf8b0-119">![Выбор методов HTTP](./media/functions-api-definition-getting-started/selectedHTTPmethods.png)</span><span class="sxs-lookup"><span data-stu-id="cf8b0-119">![Selected HTTP Methods](./media/functions-api-definition-getting-started/selectedHTTPmethods.png)</span></span>
    1. <span data-ttu-id="cf8b0-120">Сделав это, вы упростите определение API в дальнейшем.</span><span class="sxs-lookup"><span data-stu-id="cf8b0-120">This step will simplify your API definition later on.</span></span>

## <span data-ttu-id="cf8b0-121"><a name="enable"></a>Включение поддержки определения API</span><span class="sxs-lookup"><span data-stu-id="cf8b0-121"><a name="enable"></a>Enabling API Definition Support</span></span>
1. <span data-ttu-id="cf8b0-122">Перейдите к `your function name`  >  `Platform Features`  >  `API Definition` 
 ![вкладка "Определение"](./media/functions-api-definition-getting-started/definitiontab.png)</span><span class="sxs-lookup"><span data-stu-id="cf8b0-122">Navigate to `your function name` > `Platform Features` > `API Definition`
![Definition Tab](./media/functions-api-definition-getting-started/definitiontab.png)</span></span>
1. <span data-ttu-id="cf8b0-123">Задайте для `API Definition Source` значение `Function (preview)`.</span><span class="sxs-lookup"><span data-stu-id="cf8b0-123">Set `API Definition Source` to `Function (preview)`</span></span>
    1. <span data-ttu-id="cf8b0-124">Выполнив это действие, вы включите набор параметров OpenAPI для приложения-функции, в том числе конечную точку для размещения файла OpenAPI из домена приложения-функции, встроенную копию [редактора OpenAPI](http://editor.swagger.io) и генератор кратких определений.</span><span class="sxs-lookup"><span data-stu-id="cf8b0-124">This step enables a suite of OpenAPI options for your Function App, including an endpoint to host an OpenAPI file from your Function App's domain, an inline copy of the [OpenAPI Editor](http://editor.swagger.io), and a quickstart definition generator.</span></span>
<span data-ttu-id="cf8b0-125">![Включенное определение](./media/functions-api-definition-getting-started/enabledefinition.png)</span><span class="sxs-lookup"><span data-stu-id="cf8b0-125">![Enabled Definition](./media/functions-api-definition-getting-started/enabledefinition.png)</span></span>

## <span data-ttu-id="cf8b0-126"><a name="create-definition"></a>Создание определения API на основе шаблона</span><span class="sxs-lookup"><span data-stu-id="cf8b0-126"><a name="create-definition"></a>Creating your API Definition from a template</span></span>
1. <span data-ttu-id="cf8b0-127">Щелкните `Generate API Definition template`.</span><span class="sxs-lookup"><span data-stu-id="cf8b0-127">Click `Generate API Definition template`</span></span>
    1. <span data-ttu-id="cf8b0-128">На этом этапе выполняется проверка приложения-функции на наличие функций "Триггер HTTP", а данные, полученные в файле functions.json, используются для создания документа OpenAPI.</span><span class="sxs-lookup"><span data-stu-id="cf8b0-128">This step scans your Function App for HTTP Trigger functions and uses the info in functions.json to generate an OpenAPI document.</span></span>
1. <span data-ttu-id="cf8b0-129">Добавьте объект операции в `paths: /api/yourfunctionroute post:`.</span><span class="sxs-lookup"><span data-stu-id="cf8b0-129">Add an operation object to `paths: /api/yourfunctionroute post:`</span></span>
    1. <span data-ttu-id="cf8b0-130">Краткий документ OpenAPI представляет собой структуру полного документа OpenAPI. Чтобы превратить его в полное определение OpenAPI, например в объекты операций и шаблоны ответа, потребуются дополнительные метаданные.</span><span class="sxs-lookup"><span data-stu-id="cf8b0-130">The quickstart OpenAPI document is an outline of a full OpenAPI doc. It requires more metadata to be a full OpenAPI definition, such as operation objects and response templates.</span></span>
    1. <span data-ttu-id="cf8b0-131">В приведенном ниже примере объекта операции заполнен раздел produces/consumes, указан объект parameter и объект response.</span><span class="sxs-lookup"><span data-stu-id="cf8b0-131">The sample operation object below has a filled out produces/consumes section, a parameter object, and a response object.</span></span>
    
    ```yaml
      post:
        operationId: /api/yourfunctionroute/post
        consumes: [application/json]
        produces: [application/json]
        parameters:
          - name: name
            in: body
            description: Your name
            x-ms-summary: Your name
            required: true
            schema:
              type: object
              properties:
                name:
                  type: string
        description: >-
          Replace with Operation Object
          #http://swagger.io/specification/#operationObject
        responses:
          '200':
            description: A Greeting
            x-ms-summary: Your name
            schema:
              type: string
        security:
          - apikeyQuery: []
    ```
    
    > [!NOTE]
    >  <span data-ttu-id="cf8b0-132">x-ms-summary содержит имя, отображаемое в Logic Apps, Flow и PowerApps.</span><span class="sxs-lookup"><span data-stu-id="cf8b0-132">x-ms-summary provides a display name in Logic Apps, Flow, and PowerApps.</span></span>
    >
    > <span data-ttu-id="cf8b0-133">Дополнительные сведения см. в статье [Customize your Swagger definition for PowerApps](https://powerapps.microsoft.com/tutorials/customapi-how-to-swagger/) (Настройка определения Swagger для PowerApps).</span><span class="sxs-lookup"><span data-stu-id="cf8b0-133">Check out [customize your Swagger definition for PowerApps](https://powerapps.microsoft.com/tutorials/customapi-how-to-swagger/) to learn more.</span></span>

1. <span data-ttu-id="cf8b0-134">Щелкните `save` для сохранения изменений. ![Добавление определения шаблона](./media/functions-api-definition-getting-started/addingtemplate.png)</span><span class="sxs-lookup"><span data-stu-id="cf8b0-134">Click `save` to save your changes ![Adding Template Definition](./media/functions-api-definition-getting-started/addingtemplate.png)</span></span>

## <span data-ttu-id="cf8b0-135"><a name="use-definition"></a>Использование определения API</span><span class="sxs-lookup"><span data-stu-id="cf8b0-135"><a name="use-definition"></a>Using Your API Definition</span></span>
1. <span data-ttu-id="cf8b0-136">Скопируйте адрес `API definition URL` и вставьте его в новой вкладке браузера, чтобы просмотреть необработанный документ OpenAPI.</span><span class="sxs-lookup"><span data-stu-id="cf8b0-136">Copy your `API definition URL` and paste it into a new browser tab to view your raw OpenAPI document.</span></span>
1. <span data-ttu-id="cf8b0-137">Документ OpenAPI можно импортировать в различные инструменты для тестирования и интеграции с использованием этого URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="cf8b0-137">You can import your OpenAPI document to any number of tools for testing and integration using that URL.</span></span>
    1. <span data-ttu-id="cf8b0-138">Многие ресурсы Azure могут автоматически импортировать ваш документ OpenAPI, используя URL-адрес определения API, сохраненный в параметрах приложения-функции.</span><span class="sxs-lookup"><span data-stu-id="cf8b0-138">Many Azure resources are able to automatically import your OpenAPI doc using the API Definition URL that is saved in your Function application settings.</span></span> <span data-ttu-id="cf8b0-139">В случае источника определения API `Function` этот URL-адрес обновляется автоматически.</span><span class="sxs-lookup"><span data-stu-id="cf8b0-139">As a part of the `Function` API definition source, we update that url for you.</span></span>


## <span data-ttu-id="cf8b0-140"><a name="test-definition"></a>Использование пользовательского интерфейса Swagger для тестирования определения API</span><span class="sxs-lookup"><span data-stu-id="cf8b0-140"><a name="test-definition"></a>Using the Swagger UI to test your API definition</span></span>
<span data-ttu-id="cf8b0-141">В представление пользовательского интерфейса редактора внедренных определений API встроены инструменты тестирования.</span><span class="sxs-lookup"><span data-stu-id="cf8b0-141">There are testing tools built in to the UI view of the imbedded API definition editor.</span></span> <span data-ttu-id="cf8b0-142">Добавьте ключ API, а затем нажмите кнопку `Try this operation` под каждым методом.</span><span class="sxs-lookup"><span data-stu-id="cf8b0-142">Add your API key, and then use the `Try this operation` button under each method.</span></span> <span data-ttu-id="cf8b0-143">Инструмент будет использовать определение API для форматирования запросов, а успешное получение ответов будет указывать на правильность определения.</span><span class="sxs-lookup"><span data-stu-id="cf8b0-143">The tool will use your API Definition to format the requests and successful responses will indicate that your definition is correct.</span></span>

### <a name="steps"></a><span data-ttu-id="cf8b0-144">Шаги:</span><span class="sxs-lookup"><span data-stu-id="cf8b0-144">Steps:</span></span>

1. <span data-ttu-id="cf8b0-145">Скопируйте ключ API функции.</span><span class="sxs-lookup"><span data-stu-id="cf8b0-145">Copy your function API key</span></span>
    1. <span data-ttu-id="cf8b0-146">Ключ API можно найти в функции триггера HTTP под `function name` > `Keys` > `Function Keys` 
   ![сочетания клавиш](./media/functions-api-definition-getting-started/functionkey.png)</span><span class="sxs-lookup"><span data-stu-id="cf8b0-146">The API key can be found in your HTTP Trigger Function under `function name` > `Keys` > `Function Keys`
![Function key](./media/functions-api-definition-getting-started/functionkey.png)</span></span>
1. <span data-ttu-id="cf8b0-147">Перейдите на страницу `API Definition`.</span><span class="sxs-lookup"><span data-stu-id="cf8b0-147">Navigate to the `API Definition` page.</span></span>
    1. <span data-ttu-id="cf8b0-148">Щелкните `Authenticate` и добавьте ключ API функции в расположенный сверху объект безопасности.</span><span class="sxs-lookup"><span data-stu-id="cf8b0-148">Click `Authenticate` and add your Function API key to the security object at the top.</span></span>
  <span data-ttu-id="cf8b0-149">![Ключ OpenAPI](./media/functions-api-definition-getting-started/definitionTest auth.png)</span><span class="sxs-lookup"><span data-stu-id="cf8b0-149">![OpenAPI key](./media/functions-api-definition-getting-started/definitionTest auth.png)</span></span>
1. <span data-ttu-id="cf8b0-150">Выберите `/api/yourfunctionroute` > `POST`.</span><span class="sxs-lookup"><span data-stu-id="cf8b0-150">select `/api/yourfunctionroute` > `POST`</span></span>
1. <span data-ttu-id="cf8b0-151">Щелкните `Try it out` и введите имя теста.</span><span class="sxs-lookup"><span data-stu-id="cf8b0-151">Click `Try it out` and enter a name to test</span></span>
1. <span data-ttu-id="cf8b0-152">В разделе `Pretty`
![API Definition test](./media/functions-api-definition-getting-started/definitionTest.png) (Тест определения API) должен отобразиться результат "УСПЕШНО".</span><span class="sxs-lookup"><span data-stu-id="cf8b0-152">You should see a SUCCESS result under `Pretty`
![API Definition test](./media/functions-api-definition-getting-started/definitionTest.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="cf8b0-153">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="cf8b0-153">Next steps</span></span>
* [<span data-ttu-id="cf8b0-154">Обзор определения OpenAPI в Функциях</span><span class="sxs-lookup"><span data-stu-id="cf8b0-154">OpenAPI Definition in Functions Overview</span></span>](functions-api-definition.md)
  * <span data-ttu-id="cf8b0-155">Дополнительные сведения о поддержке OpenAPI см. в полной документации.</span><span class="sxs-lookup"><span data-stu-id="cf8b0-155">Read the full documentation for more info on OpenAPI support.</span></span>
* [<span data-ttu-id="cf8b0-156">Справочник разработчика по функциям Azure</span><span class="sxs-lookup"><span data-stu-id="cf8b0-156">Azure Functions developer reference</span></span>](functions-reference.md)  
  * <span data-ttu-id="cf8b0-157">Справочник программиста по созданию функций, а также определению триггеров и привязок.</span><span class="sxs-lookup"><span data-stu-id="cf8b0-157">Programmer reference for coding functions and defining triggers and bindings.</span></span>
* [<span data-ttu-id="cf8b0-158">Репозиторий GitHub для Функций Azure</span><span class="sxs-lookup"><span data-stu-id="cf8b0-158">Azure Functions GitHub repository</span></span>](https://github.com/Azure/Azure-Functions/)
  * <span data-ttu-id="cf8b0-159">Ознакомьтесь со сведениями о Функциях в GitHub и оставьте свои отзывы о предварительной версии средства поддержки определений API.</span><span class="sxs-lookup"><span data-stu-id="cf8b0-159">Check out the Functions GitHub to give us feedback on the API definition support preview!</span></span> <span data-ttu-id="cf8b0-160">Добавьте на GitHub сведения обо всех проблемах, которые необходимо устранить.</span><span class="sxs-lookup"><span data-stu-id="cf8b0-160">Make a GitHub issue for anything you'd like to see updated.</span></span>
