---
title: "aaaGetting работы с метаданными OpenAPI в функциях Azure | Документы Microsoft"
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
ms.openlocfilehash: fee3464c9a0a11b6d3891ccd0e9c5343d6bedcad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="creating-openapi-20-swagger-metadata-for-a-function-app-preview"></a><span data-ttu-id="34a4f-103">Создание метаданных OpenAPI 2.0 (Swagger) для приложения-функции (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="34a4f-103">Creating OpenAPI 2.0 (Swagger) Metadata for a Function App (Preview)</span></span>

<span data-ttu-id="34a4f-104">Этот документ поможет выполнить шаг за шагом hello создания определение OpenAPI для простой API, размещенных в Azure функции.</span><span class="sxs-lookup"><span data-stu-id="34a4f-104">This document guides you through hello step by step process of creating an OpenAPI Definition for a simple API hosted on Azure Functions.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

### <a name="what-is-openapi-swagger"></a><span data-ttu-id="34a4f-105">Общие сведения об OpenAPI (Swagger)</span><span class="sxs-lookup"><span data-stu-id="34a4f-105">What is OpenAPI (Swagger)?</span></span>
<span data-ttu-id="34a4f-106">[Метаданные swagger](http://swagger.io/) — это файл, который определяет функциональность hello и режимы API позволяет функцию размещение toobe REST API, используемые широкий спектр другого программного обеспечения.</span><span class="sxs-lookup"><span data-stu-id="34a4f-106">[Swagger Metadata](http://swagger.io/) is a file that defines hello functionality and operating modes of your API, and allows a function hosting a REST API toobe consumed by a wide variety of other software.</span></span> <span data-ttu-id="34a4f-107">Предложения корпорации Майкрософт, например PowerApps и [приложения API](https://docs.microsoft.com/azure/app-service-api/app-service-api-dotnet-get-started#a-idcodegena-generate-client-code-for-the-data-tier), а также средства, такие как сторонние разработчики [почтальон](https://www.getpostman.com/docs/importing_swagger) и [многие дополнительные пакеты](http://swagger.io/tools/) все позволяют вашей toobe API, затраченное с Определение swagger.</span><span class="sxs-lookup"><span data-stu-id="34a4f-107">Microsoft offerings like PowerApps and [API Apps](https://docs.microsoft.com/azure/app-service-api/app-service-api-dotnet-get-started#a-idcodegena-generate-client-code-for-the-data-tier), as well as 3rd party developer tooling like [Postman](https://www.getpostman.com/docs/importing_swagger) and [many more packages](http://swagger.io/tools/) all allow your API toobe consumed with a Swagger definition.</span></span>

## <span data-ttu-id="34a4f-108"><a name="prepare-function"></a>Создание функции с простым интерфейсом API</span><span class="sxs-lookup"><span data-stu-id="34a4f-108"><a name="prepare-function"></a>Creating a Function with a simple API</span></span>
  <span data-ttu-id="34a4f-109">toocreate определение OpenAPI, необходимо сначала toocreate функцию с простой API.</span><span class="sxs-lookup"><span data-stu-id="34a4f-109">toocreate an OpenAPI definition, we first need toocreate a Function with a simple API.</span></span> <span data-ttu-id="34a4f-110">При наличии API, размещенным в приложении функции прямой toohello Далее раздел можно пропустить</span><span class="sxs-lookup"><span data-stu-id="34a4f-110">If you already have an API hosted on a Function App, you can skip straight toohello next section</span></span>
1. <span data-ttu-id="34a4f-111">Создайте новое приложение-функцию.</span><span class="sxs-lookup"><span data-stu-id="34a4f-111">Create a new Function App.</span></span>
    1. <span data-ttu-id="34a4f-112">Перейдите на [портал Azure](https://portal.azure.com) > `+ New` и найдите "Приложение-функция".</span><span class="sxs-lookup"><span data-stu-id="34a4f-112">[Azure portal](https://portal.azure.com) > `+ New` > Search for "Function App"</span></span>
1. <span data-ttu-id="34a4f-113">Создайте новую функцию "Триггер HTTP" в новом приложении-функции.</span><span class="sxs-lookup"><span data-stu-id="34a4f-113">Create a new HTTP trigger function inside your new Function App</span></span>
    1. <span data-ttu-id="34a4f-114">Функция заранее заполняется кодом, определяющим очень простой интерфейс REST API.</span><span class="sxs-lookup"><span data-stu-id="34a4f-114">Your function is pre-populated with code defining a very simple REST API.</span></span>
    1. <span data-ttu-id="34a4f-115">Все строки, переданной toohello функции, как параметр запроса или в тексте hello возвращается как «Hello {ввода}»</span><span class="sxs-lookup"><span data-stu-id="34a4f-115">Any string passed toohello Function as a query parameter or in hello body is returned as "Hello {input}"</span></span>
1. <span data-ttu-id="34a4f-116">Go toohello `Integrate` вкладка этой новой функции триггера HTTP</span><span class="sxs-lookup"><span data-stu-id="34a4f-116">Go toohello `Integrate` tab of your new HTTP Trigger function</span></span>
    1. <span data-ttu-id="34a4f-117">Переключить `Allowed HTTP methods` слишком`Selected methods`</span><span class="sxs-lookup"><span data-stu-id="34a4f-117">Toggle `Allowed HTTP methods` too`Selected methods`</span></span>
    1. <span data-ttu-id="34a4f-118">В `Selected HTTP methods` снимите флажки рядом со всеми командами, за исключением POST.</span><span class="sxs-lookup"><span data-stu-id="34a4f-118">In `Selected HTTP methods` uncheck every verb except POST.</span></span>
    <span data-ttu-id="34a4f-119">![Выбор методов HTTP](./media/functions-api-definition-getting-started/selectedHTTPmethods.png)</span><span class="sxs-lookup"><span data-stu-id="34a4f-119">![Selected HTTP Methods](./media/functions-api-definition-getting-started/selectedHTTPmethods.png)</span></span>
    1. <span data-ttu-id="34a4f-120">Сделав это, вы упростите определение API в дальнейшем.</span><span class="sxs-lookup"><span data-stu-id="34a4f-120">This step will simplify your API definition later on.</span></span>

## <span data-ttu-id="34a4f-121"><a name="enable"></a>Включение поддержки определения API</span><span class="sxs-lookup"><span data-stu-id="34a4f-121"><a name="enable"></a>Enabling API Definition Support</span></span>
1. <span data-ttu-id="34a4f-122">Перейдите в слишком`your function name` > `Platform Features` > `API Definition`
![вкладка "Определение"](./media/functions-api-definition-getting-started/definitiontab.png)</span><span class="sxs-lookup"><span data-stu-id="34a4f-122">Navigate too`your function name` > `Platform Features` > `API Definition`
![Definition Tab](./media/functions-api-definition-getting-started/definitiontab.png)</span></span>
1. <span data-ttu-id="34a4f-123">Задать `API Definition Source` слишком`Function (preview)`</span><span class="sxs-lookup"><span data-stu-id="34a4f-123">Set `API Definition Source` too`Function (preview)`</span></span>
    1. <span data-ttu-id="34a4f-124">Этот шаг включает набор параметров OpenAPI функции приложения, включая toohost конечной точки в файл OpenAPI из домена функции приложения, создается копия встроенного hello [OpenAPI редактор](http://editor.swagger.io)и генератор определение краткого руководства.</span><span class="sxs-lookup"><span data-stu-id="34a4f-124">This step enables a suite of OpenAPI options for your Function App, including an endpoint toohost an OpenAPI file from your Function App's domain, an inline copy of hello [OpenAPI Editor](http://editor.swagger.io), and a quickstart definition generator.</span></span>
<span data-ttu-id="34a4f-125">![Включенное определение](./media/functions-api-definition-getting-started/enabledefinition.png)</span><span class="sxs-lookup"><span data-stu-id="34a4f-125">![Enabled Definition](./media/functions-api-definition-getting-started/enabledefinition.png)</span></span>

## <span data-ttu-id="34a4f-126"><a name="create-definition"></a>Создание определения API на основе шаблона</span><span class="sxs-lookup"><span data-stu-id="34a4f-126"><a name="create-definition"></a>Creating your API Definition from a template</span></span>
1. <span data-ttu-id="34a4f-127">Щелкните `Generate API Definition template`.</span><span class="sxs-lookup"><span data-stu-id="34a4f-127">Click `Generate API Definition template`</span></span>
    1. <span data-ttu-id="34a4f-128">Этот шаг просматривает приложения функции для функций триггер HTTP и использует сведения hello в functions.json toogenerate документ OpenAPI.</span><span class="sxs-lookup"><span data-stu-id="34a4f-128">This step scans your Function App for HTTP Trigger functions and uses hello info in functions.json toogenerate an OpenAPI document.</span></span>
1. <span data-ttu-id="34a4f-129">Добавить объект операции слишком`paths: /api/yourfunctionroute post:`</span><span class="sxs-lookup"><span data-stu-id="34a4f-129">Add an operation object too`paths: /api/yourfunctionroute post:`</span></span>
    1. <span data-ttu-id="34a4f-130">Hello краткое руководство OpenAPI документ является контуром полный документ OpenAPI. Требуются дополнительные метаданные toobe полное определение OpenAPI, такие как объекты операций и шаблонов ответа.</span><span class="sxs-lookup"><span data-stu-id="34a4f-130">hello quickstart OpenAPI document is an outline of a full OpenAPI doc. It requires more metadata toobe a full OpenAPI definition, such as operation objects and response templates.</span></span>
    1. <span data-ttu-id="34a4f-131">Создает и использует раздел, объект параметра и объект ответа ниже объекта операции Образец Hello имеет заливкой.</span><span class="sxs-lookup"><span data-stu-id="34a4f-131">hello sample operation object below has a filled out produces/consumes section, a parameter object, and a response object.</span></span>
    
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
    >  <span data-ttu-id="34a4f-132">x-ms-summary содержит имя, отображаемое в Logic Apps, Flow и PowerApps.</span><span class="sxs-lookup"><span data-stu-id="34a4f-132">x-ms-summary provides a display name in Logic Apps, Flow, and PowerApps.</span></span>
    >
    > <span data-ttu-id="34a4f-133">Извлечение [настроить определение Swagger для PowerApps](https://powerapps.microsoft.com/tutorials/customapi-how-to-swagger/) toolearn дополнительные.</span><span class="sxs-lookup"><span data-stu-id="34a4f-133">Check out [customize your Swagger definition for PowerApps](https://powerapps.microsoft.com/tutorials/customapi-how-to-swagger/) toolearn more.</span></span>

1. <span data-ttu-id="34a4f-134">Нажмите кнопку `save` toosave изменения ![Добавление определения шаблона](./media/functions-api-definition-getting-started/addingtemplate.png)</span><span class="sxs-lookup"><span data-stu-id="34a4f-134">Click `save` toosave your changes ![Adding Template Definition](./media/functions-api-definition-getting-started/addingtemplate.png)</span></span>

## <span data-ttu-id="34a4f-135"><a name="use-definition"></a>Использование определения API</span><span class="sxs-lookup"><span data-stu-id="34a4f-135"><a name="use-definition"></a>Using Your API Definition</span></span>
1. <span data-ttu-id="34a4f-136">Копия вашего `API definition URL` и вставьте его в новый tooview вкладку браузера необработанные OpenAPI документа.</span><span class="sxs-lookup"><span data-stu-id="34a4f-136">Copy your `API definition URL` and paste it into a new browser tab tooview your raw OpenAPI document.</span></span>
1. <span data-ttu-id="34a4f-137">Вы можете импортировать ваш номер tooany OpenAPI документа средств для тестирования и интеграция с использованием этого URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="34a4f-137">You can import your OpenAPI document tooany number of tools for testing and integration using that URL.</span></span>
    1. <span data-ttu-id="34a4f-138">Многие ресурсы Azure являются импорта может tooautomatically OpenAPI документа с помощью hello API определения URL-адрес, сохраненный в параметрах функции приложения.</span><span class="sxs-lookup"><span data-stu-id="34a4f-138">Many Azure resources are able tooautomatically import your OpenAPI doc using hello API Definition URL that is saved in your Function application settings.</span></span> <span data-ttu-id="34a4f-139">В составе приветствия `Function` API определения источника, корпорация Майкрософт автоматически обновлять этот URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="34a4f-139">As a part of hello `Function` API definition source, we update that url for you.</span></span>


## <span data-ttu-id="34a4f-140"><a name="test-definition"></a>С помощью пользовательского интерфейса Swagger tootest hello определение API</span><span class="sxs-lookup"><span data-stu-id="34a4f-140"><a name="test-definition"></a>Using hello Swagger UI tootest your API definition</span></span>
<span data-ttu-id="34a4f-141">Средства построения в представлении toohello пользовательского интерфейса редактора определения API hello внедренным тестируете.</span><span class="sxs-lookup"><span data-stu-id="34a4f-141">There are testing tools built in toohello UI view of hello imbedded API definition editor.</span></span> <span data-ttu-id="34a4f-142">Добавьте ключ API, а затем использовать hello `Try this operation` кнопку под каждого метода.</span><span class="sxs-lookup"><span data-stu-id="34a4f-142">Add your API key, and then use hello `Try this operation` button under each method.</span></span> <span data-ttu-id="34a4f-143">Hello средство будет использовать определение API tooformat hello запросов и ответов успешно указывает правильность вашего определения.</span><span class="sxs-lookup"><span data-stu-id="34a4f-143">hello tool will use your API Definition tooformat hello requests and successful responses will indicate that your definition is correct.</span></span>

### <a name="steps"></a><span data-ttu-id="34a4f-144">Шаги:</span><span class="sxs-lookup"><span data-stu-id="34a4f-144">Steps:</span></span>

1. <span data-ttu-id="34a4f-145">Скопируйте ключ API функции.</span><span class="sxs-lookup"><span data-stu-id="34a4f-145">Copy your function API key</span></span>
    1. <span data-ttu-id="34a4f-146">ключ Hello API можно найти в функции триггера HTTP в `function name` > `Keys` > `Function Keys` 
   ![сочетания клавиш](./media/functions-api-definition-getting-started/functionkey.png)</span><span class="sxs-lookup"><span data-stu-id="34a4f-146">hello API key can be found in your HTTP Trigger Function under `function name` > `Keys` > `Function Keys`
![Function key](./media/functions-api-definition-getting-started/functionkey.png)</span></span>
1. <span data-ttu-id="34a4f-147">Перейдите toohello `API Definition` страницы.</span><span class="sxs-lookup"><span data-stu-id="34a4f-147">Navigate toohello `API Definition` page.</span></span>
    1. <span data-ttu-id="34a4f-148">Нажмите кнопку `Authenticate` и добавьте объект безопасности ключа toohello функции API вверху hello.</span><span class="sxs-lookup"><span data-stu-id="34a4f-148">Click `Authenticate` and add your Function API key toohello security object at hello top.</span></span>
  <span data-ttu-id="34a4f-149">![Ключ OpenAPI](./media/functions-api-definition-getting-started/definitionTest auth.png)</span><span class="sxs-lookup"><span data-stu-id="34a4f-149">![OpenAPI key](./media/functions-api-definition-getting-started/definitionTest auth.png)</span></span>
1. <span data-ttu-id="34a4f-150">Выберите `/api/yourfunctionroute` > `POST`.</span><span class="sxs-lookup"><span data-stu-id="34a4f-150">select `/api/yourfunctionroute` > `POST`</span></span>
1. <span data-ttu-id="34a4f-151">Нажмите кнопку `Try it out` и введите имя tootest</span><span class="sxs-lookup"><span data-stu-id="34a4f-151">Click `Try it out` and enter a name tootest</span></span>
1. <span data-ttu-id="34a4f-152">В разделе `Pretty`
![API Definition test](./media/functions-api-definition-getting-started/definitionTest.png) (Тест определения API) должен отобразиться результат "УСПЕШНО".</span><span class="sxs-lookup"><span data-stu-id="34a4f-152">You should see a SUCCESS result under `Pretty`
![API Definition test](./media/functions-api-definition-getting-started/definitionTest.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="34a4f-153">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="34a4f-153">Next steps</span></span>
* [<span data-ttu-id="34a4f-154">Обзор определения OpenAPI в Функциях</span><span class="sxs-lookup"><span data-stu-id="34a4f-154">OpenAPI Definition in Functions Overview</span></span>](functions-api-definition.md)
  * <span data-ttu-id="34a4f-155">Ознакомиться с полной документацией hello Дополнительные сведения о поддержке OpenAPI.</span><span class="sxs-lookup"><span data-stu-id="34a4f-155">Read hello full documentation for more info on OpenAPI support.</span></span>
* [<span data-ttu-id="34a4f-156">Справочник разработчика по функциям Azure</span><span class="sxs-lookup"><span data-stu-id="34a4f-156">Azure Functions developer reference</span></span>](functions-reference.md)  
  * <span data-ttu-id="34a4f-157">Справочник программиста по созданию функций, а также определению триггеров и привязок.</span><span class="sxs-lookup"><span data-stu-id="34a4f-157">Programmer reference for coding functions and defining triggers and bindings.</span></span>
* [<span data-ttu-id="34a4f-158">Репозиторий GitHub для Функций Azure</span><span class="sxs-lookup"><span data-stu-id="34a4f-158">Azure Functions GitHub repository</span></span>](https://github.com/Azure/Azure-Functions/)
  * <span data-ttu-id="34a4f-159">Посетите toogive GitHub функции hello нам отзывы о обзор поддержки определения hello API.</span><span class="sxs-lookup"><span data-stu-id="34a4f-159">Check out hello Functions GitHub toogive us feedback on hello API definition support preview!</span></span> <span data-ttu-id="34a4f-160">Сделайте вопрос GitHub для любого элемента хотелось бы toosee обновлены.</span><span class="sxs-lookup"><span data-stu-id="34a4f-160">Make a GitHub issue for anything you'd like toosee updated.</span></span>
