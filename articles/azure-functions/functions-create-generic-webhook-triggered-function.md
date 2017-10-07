---
title: "функция в Azure, активируемых универсального веб-перехватчика aaaCreate | Документы Microsoft"
description: "Используйте функции Azure toocreate без сервера функция, вызываемая веб-перехватчик в Azure."
services: functions
documentationcenter: na
author: ggailey777
manager: cfowler
editor: 
tags: 
ms.assetid: fafc10c0-84da-4404-b4fa-eea03c7bf2b1
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 08/12/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 0a4868da91d216c8d20930ce7ec82eaa059c75ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-triggered-by-a-generic-webhook"></a>Создание функции, активируемой универсальным веб-перехватчиком

Функции Azure позволяет выполнять код в среде без сервера без необходимости toofirst создания виртуальной Машины или публикации веб-приложения. Например можно настроить функцию toobe, вызванное предупреждение, подаваемое монитором Azure. В этом разделе показано, как код на C# tooexecute при группа ресурсов находится добавлена tooyour подписки.   

![Универсальный веб-перехватчика активации функции hello портал Azure](./media/functions-create-generic-webhook-triggered-function/function-completed.png)

## <a name="prerequisites"></a>Предварительные требования 

toocomplete этого учебника:

+ Если у вас еще нет подписки Azure, [создайте бесплатную учетную запись Azure](https://azure.microsoft.com/free/?WT.mc_id=A261C142F), прежде чем начинать работу.

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a>Создание приложения-функции Azure

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

Создайте функцию в приложение новые функции hello.

## <a name="create-function"></a>Создание функции, активируемой универсальным веб-перехватчиком

1. Разверните приложения функции и щелкните hello  **+**  рядом слишком**функции**. Если эта функция является hello первый в функции приложения, выберите **пользовательские функции**. Откроется hello полный набор шаблонов функций.

    ![Страница быстрого запуска функции в hello портал Azure](./media/functions-create-generic-webhook-triggered-function/add-first-function.png)

2. Выберите hello **универсального веб-перехватчика - C#** шаблона. Введите имя функции C# и выберите **Создать**.

     ![Создайте функцию универсального веб-перехватчика запускается в hello портал Azure](./media/functions-create-generic-webhook-triggered-function/functions-create-generic-webhook-trigger.png) 

2. В новые функции, щелкните **URL-адрес функции <> / Get**, затем скопируйте и сохраните значение hello. Использовать этот веб-перехватчик значение tooconfigure hello. 

    ![Просмотрите код функции hello](./media/functions-create-generic-webhook-triggered-function/functions-copy-function-url.png)
         
Затем вы создадите конечную точку веб-перехватчика в оповещении журнала действий в Azure Monitor. 

## <a name="create-an-activity-log-alert"></a>Создание оповещения журнала действий

1. В hello портал Azure, перейдите toohello **монитор** службы, выберите **оповещения**и нажмите кнопку **журнала действий добавить оповещение**.   

    ![Монитор](./media/functions-create-generic-webhook-triggered-function/functions-monitor-add-alert.png)

2. Используйте параметры hello, как указано в таблице hello:

    ![Создание оповещения журнала действий](./media/functions-create-generic-webhook-triggered-function/functions-monitor-add-alert-settings.png)

    | Настройка      |  Рекомендуемое значение   | Описание                              |
    | ------------ |  ------- | -------------------------------------------------- |
    | **Имя оповещения журнала действий** | resource-group-create-alert | Имя предупреждения журнала действие hello. |
    | **Подписка** | Ваша подписка | Hello подписку, которую вы используете для этого учебника. | 
    |  **Группа ресурсов** | myResourceGroup | Группа ресурсов Hello, развернутые для hello уведомление ресурсам. С помощью hello одну группу ресурсов, как функция приложения составляющих его проще tooclean после завершения учебника hello. |
    | **Категория событий** | Administrative | В эту категорию входят изменения, внесенные tooAzure ресурсов.  |
    | **Тип ресурса** | Группы ресурсов | Фильтры оповещения tooresource группы действий. |
    | **Группа ресурсов**<br/>и **ресурс** | Все | Отслеживает все ресурсы. |
    | **Имя операции** | Создать группу ресурсов | Фильтры оповещения toocreate операций. |
    | **Level** | Информация | Учитывает оповещения на уровне сведений. | 
    | **Состояние** | Успешно | Фильтрует tooactions предупреждения, завершены успешно. |
    | **Группа действий** | Создать | Создайте новую группу действий, который определяет hello принимает действие при возникновении предупреждения. |
    | **Имя группы действий** | function-webhook | Группа действий для hello tooidentify имя.  | 
    | **Краткое название** | funcwebhook | Короткое имя для группы действий hello. |  

3. В **действия**, добавьте действие, используя параметры hello, как указано в таблице hello: 

    ![Добавление группы действий](./media/functions-create-generic-webhook-triggered-function/functions-monitor-add-alert-settings-2.png)

    | Настройка      |  Рекомендуемое значение   | Описание                              |
    | ------------ |  ------- | -------------------------------------------------- |
    | **Имя** | CallFunctionWebhook | Название действия hello. |
    | **Тип действия** | webhook | Предупреждение toohello Hello ответа —, вызывается URL-адрес веб-перехватчика. |
    | **Дополнительные сведения** | URL-адрес функции | Вставьте URL-адрес веб-перехватчика hello функции hello, скопированное ранее. |v

4. Нажмите кнопку **ОК** toocreate hello появления предупреждения и действия группы.  

веб-перехватчика Hello, теперь называется при создании группы ресурсов в вашей подписке. Затем обновить кода hello в вашей hello toohandle функция журнала данных JSON в тексте hello hello запроса.   

## <a name="update-hello-function-code"></a>Изменения кода hello

1. Перейдите назад tooyour функции приложения hello портала и разверните функции. 

2. Замените код скрипта hello C# в функции hello в портале hello hello, следующий код:

    ```csharp
    #r "Newtonsoft.Json"
    
    using System;
    using System.Net;
    using Newtonsoft.Json;
    using Newtonsoft.Json.Linq;
    
    public static async Task<object> Run(HttpRequestMessage req, TraceWriter log)
    {
        log.Info($"Webhook was triggered!");
    
        // Get hello activityLog object from hello JSON in hello message body.
        string jsonContent = await req.Content.ReadAsStringAsync();
        JToken activityLog = JObject.Parse(jsonContent.ToString())
            .SelectToken("data.context.activityLog");
    
        // Return an error if hello resource in hello activity log isn't a resource group. 
        if (activityLog == null || !string.Equals((string)activityLog["resourceType"], 
            "Microsoft.Resources/subscriptions/resourcegroups"))
        {
            log.Error("An error occured");
            return req.CreateResponse(HttpStatusCode.BadRequest, new
            {
                error = "Unexpected message payload or wrong alert received."
            });
        }
    
        // Write information about hello created resource group toohello streaming log.
        log.Info(string.Format("Resource group '{0}' was {1} on {2}.",
            (string)activityLog["resourceGroupName"],
            ((string)activityLog["subStatus"]).ToLower(), 
            (DateTime)activityLog["submissionTimestamp"]));
    
        return req.CreateResponse(HttpStatusCode.OK);    
    }
    ```

Теперь можно протестировать функции hello, создав новую группу ресурсов в вашей подписке.

## <a name="test-hello-function"></a>Проверка функции hello

1. Щелкните значок группы ресурсов hello в hello левой части hello портал Azure, выберите **+ добавить**, введите команду **имя группы ресурсов**и выберите **создать** toocreate группы ресурсов пустым.
    
    ![Создайте группу ресурсов.](./media/functions-create-generic-webhook-triggered-function/functions-create-resource-group.png)

2. Функция tooyour вернуться назад и разверните hello **журналы** окна. После создания группы ресурсов hello hello триггеры предупреждения журнала действие hello веб-перехватчика и выполняет функции hello. Можно видеть имя hello hello записываются журналы toohello новую группу ресурсов.  

    ![Добавьте тестовый параметр приложения.](./media/functions-create-generic-webhook-triggered-function/function-view-logs.png)

3. (Необязательно) Вернуться назад и удалить созданную группу ресурсов hello. Обратите внимание, что это действие не приводит к возникновению функции hello. Это из-за удаления операций отфильтровываются hello предупреждения. 

## <a name="clean-up-resources"></a>Очистка ресурсов

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a>Дальнейшие действия

Вы создали функцию, которая выполняется при получении запроса от универсального веб-перехватчика. 

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

Дополнительные сведения см. в статье [Привязки HTTP и веб-перехватчика в функциях Azure](functions-bindings-http-webhook.md). toolearn Дополнительные сведения о разработке функции в C# в разделе [Справочник разработчика сценария Azure функции C#](functions-reference-csharp.md).

