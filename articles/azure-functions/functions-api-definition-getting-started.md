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
# <a name="creating-openapi-20-swagger-metadata-for-a-function-app-preview"></a>Создание метаданных OpenAPI 2.0 (Swagger) для приложения-функции (предварительная версия)

Этот документ поможет выполнить шаг за шагом hello создания определение OpenAPI для простой API, размещенных в Azure функции.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

### <a name="what-is-openapi-swagger"></a>Общие сведения об OpenAPI (Swagger)
[Метаданные swagger](http://swagger.io/) — это файл, который определяет функциональность hello и режимы API позволяет функцию размещение toobe REST API, используемые широкий спектр другого программного обеспечения. Предложения корпорации Майкрософт, например PowerApps и [приложения API](https://docs.microsoft.com/azure/app-service-api/app-service-api-dotnet-get-started#a-idcodegena-generate-client-code-for-the-data-tier), а также средства, такие как сторонние разработчики [почтальон](https://www.getpostman.com/docs/importing_swagger) и [многие дополнительные пакеты](http://swagger.io/tools/) все позволяют вашей toobe API, затраченное с Определение swagger.

## <a name="prepare-function"></a>Создание функции с простым интерфейсом API
  toocreate определение OpenAPI, необходимо сначала toocreate функцию с простой API. При наличии API, размещенным в приложении функции прямой toohello Далее раздел можно пропустить
1. Создайте новое приложение-функцию.
    1. Перейдите на [портал Azure](https://portal.azure.com) > `+ New` и найдите "Приложение-функция".
1. Создайте новую функцию "Триггер HTTP" в новом приложении-функции.
    1. Функция заранее заполняется кодом, определяющим очень простой интерфейс REST API.
    1. Все строки, переданной toohello функции, как параметр запроса или в тексте hello возвращается как «Hello {ввода}»
1. Go toohello `Integrate` вкладка этой новой функции триггера HTTP
    1. Переключить `Allowed HTTP methods` слишком`Selected methods`
    1. В `Selected HTTP methods` снимите флажки рядом со всеми командами, за исключением POST.
    ![Выбор методов HTTP](./media/functions-api-definition-getting-started/selectedHTTPmethods.png)
    1. Сделав это, вы упростите определение API в дальнейшем.

## <a name="enable"></a>Включение поддержки определения API
1. Перейдите в слишком`your function name` > `Platform Features` > `API Definition`
![вкладка "Определение"](./media/functions-api-definition-getting-started/definitiontab.png)
1. Задать `API Definition Source` слишком`Function (preview)`
    1. Этот шаг включает набор параметров OpenAPI функции приложения, включая toohost конечной точки в файл OpenAPI из домена функции приложения, создается копия встроенного hello [OpenAPI редактор](http://editor.swagger.io)и генератор определение краткого руководства.
![Включенное определение](./media/functions-api-definition-getting-started/enabledefinition.png)

## <a name="create-definition"></a>Создание определения API на основе шаблона
1. Щелкните `Generate API Definition template`.
    1. Этот шаг просматривает приложения функции для функций триггер HTTP и использует сведения hello в functions.json toogenerate документ OpenAPI.
1. Добавить объект операции слишком`paths: /api/yourfunctionroute post:`
    1. Hello краткое руководство OpenAPI документ является контуром полный документ OpenAPI. Требуются дополнительные метаданные toobe полное определение OpenAPI, такие как объекты операций и шаблонов ответа.
    1. Создает и использует раздел, объект параметра и объект ответа ниже объекта операции Образец Hello имеет заливкой.
    
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
    >  x-ms-summary содержит имя, отображаемое в Logic Apps, Flow и PowerApps.
    >
    > Извлечение [настроить определение Swagger для PowerApps](https://powerapps.microsoft.com/tutorials/customapi-how-to-swagger/) toolearn дополнительные.

1. Нажмите кнопку `save` toosave изменения ![Добавление определения шаблона](./media/functions-api-definition-getting-started/addingtemplate.png)

## <a name="use-definition"></a>Использование определения API
1. Копия вашего `API definition URL` и вставьте его в новый tooview вкладку браузера необработанные OpenAPI документа.
1. Вы можете импортировать ваш номер tooany OpenAPI документа средств для тестирования и интеграция с использованием этого URL-адреса.
    1. Многие ресурсы Azure являются импорта может tooautomatically OpenAPI документа с помощью hello API определения URL-адрес, сохраненный в параметрах функции приложения. В составе приветствия `Function` API определения источника, корпорация Майкрософт автоматически обновлять этот URL-адрес.


## <a name="test-definition"></a>С помощью пользовательского интерфейса Swagger tootest hello определение API
Средства построения в представлении toohello пользовательского интерфейса редактора определения API hello внедренным тестируете. Добавьте ключ API, а затем использовать hello `Try this operation` кнопку под каждого метода. Hello средство будет использовать определение API tooformat hello запросов и ответов успешно указывает правильность вашего определения.

### <a name="steps"></a>Шаги:

1. Скопируйте ключ API функции.
    1. ключ Hello API можно найти в функции триггера HTTP в `function name` > `Keys` > `Function Keys` 
   ![сочетания клавиш](./media/functions-api-definition-getting-started/functionkey.png)
1. Перейдите toohello `API Definition` страницы.
    1. Нажмите кнопку `Authenticate` и добавьте объект безопасности ключа toohello функции API вверху hello.
  ![Ключ OpenAPI](./media/functions-api-definition-getting-started/definitionTest auth.png)
1. Выберите `/api/yourfunctionroute` > `POST`.
1. Нажмите кнопку `Try it out` и введите имя tootest
1. В разделе `Pretty`
![API Definition test](./media/functions-api-definition-getting-started/definitionTest.png) (Тест определения API) должен отобразиться результат "УСПЕШНО".

## <a name="next-steps"></a>Дальнейшие действия
* [Обзор определения OpenAPI в Функциях](functions-api-definition.md)
  * Ознакомиться с полной документацией hello Дополнительные сведения о поддержке OpenAPI.
* [Справочник разработчика по функциям Azure](functions-reference.md)  
  * Справочник программиста по созданию функций, а также определению триггеров и привязок.
* [Репозиторий GitHub для Функций Azure](https://github.com/Azure/Azure-Functions/)
  * Посетите toogive GitHub функции hello нам отзывы о обзор поддержки определения hello API. Сделайте вопрос GitHub для любого элемента хотелось бы toosee обновлены.
