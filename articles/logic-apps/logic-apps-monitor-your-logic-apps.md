---
title: "состояние aaaCheck, настройте ведение журнала и получать оповещения - приложения логики Azure | Документы Microsoft"
description: "Мониторинг состояния и производительности приложений логики, запись ведения журнала диагностики и настройка оповещений"
author: jeffhollan
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 5c1b1e15-3b6c-49dc-98a6-bdbe7cb75339
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 07/21/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 81f186e11a669b710f4c06089597eb5a76f7a44e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-status-set-up-diagnostics-logging-and-turn-on-alerts-for-azure-logic-apps"></a>Мониторинг состояния, настройка ведения журнала диагностики и включение предупреждений для Azure Logic Apps

После [создания и запуска приложения логики](../logic-apps/logic-apps-create-a-logic-app.md) можно проверить его журнал запусков, журнал триггеров, состояние и производительность. Для мониторинга событий в режиме реального времени и отладки можно настроить [ведение журнала диагностики](#azure-diagnostics) для приложения логики. Это позволит [выполнять поиск и просматривать события](#find-events), такие как события триггера, события выполнения и события действия. Также можно [использовать полученные диагностические данные в других службах](#extend-diagnostic-data), таких как служба хранилища Azure и концентраторы событий Azure. 

Настройка tooget уведомлений о сбоях или других возможных проблемах [предупреждения](#add-azure-alerts). Например, можно создать оповещение, которое обнаруживает "более пяти запусков в течение часа, которые завершились сбоем". Можно также настроить мониторинг, отслеживание и ведение журнала программными средствами с помощью [параметров и свойств событий системы диагностики Azure](#diagnostic-event-properties).

## <a name="view-runs-and-trigger-history-for-your-logic-app"></a>Просмотр сведений о выполнении и журнале триггеров для приложения логики

1. toofind логику приложения в hello [портал Azure](https://portal.azure.com), на hello главного меню Azure, выберите **дополнительные службы**. В поле поиска hello, найдите «логику приложений» и нажмите кнопку **Logic apps**.

   ![Поиск приложения логики](./media/logic-apps-monitor-your-logic-apps/find-your-logic-app.png)

   Hello портал Azure показывает все приложения hello логики, которые связаны с подпиской Azure. 

2. Выберите приложение логики, а затем нажмите **Обзор**.

   Hello портал Azure показывает hello запусков журнал и журнал триггер для логики приложения. Например:

   ![Журнал запусков и журнал триггеров для приложения логики](media/logic-apps-monitor-your-logic-apps/overview.png)

   * **Запускает журнал** показывает все фрагменты hello логику приложения. 
   * **Активировать журнал** показывает все действия триггера hello логику приложения.

   Описание состояний см. в разделе [Устранение неполадок в работе приложения логики](../logic-apps/logic-apps-diagnosing-failures.md).

   > [!TIP]
   > Если вы не нашли hello появились ожидаемые данные, на панели инструментов hello, выберите **обновление**.

3. tooview hello шаги из конкретного запуска в разделе **журнала выполняется**, выберите запуска. 

   Hello монитора отображается каждый шаг в течение данного запуска. Например:

   ![Действия для определенного запуска](media/logic-apps-monitor-your-logic-apps/monitor-view-updated.png)

4. выберите Дополнительные сведения о запуске hello tooget **сведения о выполнении**. Эти сведения представлены шаги hello, состояния входных данных, и запустите выходные данные для hello. 

   ![Выберите "Подробности о запуске"](media/logic-apps-monitor-your-logic-apps/run-details.png)

   Например, можно получить hello запуска **идентификатор корреляции**, которой может потребоваться при использовании hello [API-интерфейса REST для логики приложений](https://docs.microsoft.com/rest/api/logic).

5. tooget подробности о конкретных шагах, щелкните этот шаг. После этого можно просмотреть такие сведения для данного этапа, как входные данные, выходные данные и все ошибки. Например:

   ![Сведения об этапе](media/logic-apps-monitor-your-logic-apps/monitor-view-details.png)
   
   > [!NOTE]
   > Все сведения о времени выполнения и событиях, шифруются в hello логику приложения службы. Они расшифровываются только в том случае, когда пользователь запрашивает tooview этих данных. Можно также контролировать доступ к событиям toothese с [Azure Role-Based управления доступом (RBAC)](../active-directory/role-based-access-control-what-is.md).

6. tooget сведений о событии триггера, вернитесь к предыдущему окну toohello **Обзор** области. В разделе **активировать журнал**выберите событие триггера hello. Теперь можно просмотреть такие сведения, как входные и выходные данные, например:

   ![Выходные данные события триггера](media/logic-apps-monitor-your-logic-apps/trigger-details.png)

<a name="azure-diagnostics"></a>

## <a name="turn-on-diagnostics-logging-for-your-logic-app"></a>Включение ведения журнала диагностики для приложения логики

Для отладки с использованием сведений о среде выполнения и событиях можно настроить ведение журнала диагностики с помощью [Azure Log Analytics](../log-analytics/log-analytics-overview.md). Аналитика журналов представляет собой службу в [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md) , отслеживает облачных и локальных сред toohelp Ведение их доступности и производительности. 

Прежде чем начать, необходимо toohave рабочей области OMS. Дополнительные сведения [как toocreate рабочей области OMS](../log-analytics/log-analytics-get-started.md).

1. В hello [портал Azure](https://portal.azure.com), найдите и выберите логику приложения. 

2. Меню hello логику приложения колонке под **мониторинг**, выберите **диагностики** > **параметров диагностики**.

   ![Go tooMonitoring диагностики, диагностические параметры](media/logic-apps-monitor-your-logic-apps/logic-app-diagnostics.png)

3. В разделе **Параметры диагностики** выберите **Вкл**.

   ![Включение журналов диагностики](media/logic-apps-monitor-your-logic-apps/turn-on-diagnostics-logic-app.png)

4. Теперь выберите hello OMS рабочей области и категории событий для ведения журнала, как показано:

   1. Выберите **отправки tooLog Analytics**. 
   2. В разделе **Log Analytics** выберите **Настройка**. 
   3. В разделе **рабочих областей OMS**, выберите toouse рабочей области OMS hello для ведения журнала.
   4. В разделе **журнала**выберите hello **WorkflowRuntime** категории.
   5. Выберите метрики интервал приветствия.
   6. Когда все будет готово, нажмите **Сохранить**.

   ![Выберите рабочую область OMS и данные для ведения журнала](media/logic-apps-monitor-your-logic-apps/send-diagnostics-data-log-analytics-workspace.png)

Теперь можно выполнять поиск событий и других данных, таких как события триггера, события выполнения и события действия.

<a name="find-events"></a>

## <a name="find-events-and-data-for-your-logic-app"></a>Поиск событий и данных для приложения логики

toofind и представление события в приложении логику как события триггера, запускать события и действие, выполните следующие действия.

1. В hello [портал Azure](https://portal.azure.com), выберите **более служб**. Введите в поле поиска "log analytics" и выберите **Log Analytics**, как показано ниже.

   ![Выберите "Log Analytics"](media/logic-apps-monitor-your-logic-apps/browseloganalytics.png)

2. В разделе **Log Analytics** найдите и выберите рабочую область OMS. 

   ![Выбор рабочей области OMS](media/logic-apps-monitor-your-logic-apps/selectla.png)

3. В разделе **Управление** выберите **Портал OMS**.

   ![Выберите "Портал OMS"](media/logic-apps-monitor-your-logic-apps/omsportalpage.png)

4. На домашней странице OMS выберите **Поиск по журналам**.

   ![На домашней странице OMS выберите "Поиск по журналам"](media/logic-apps-monitor-your-logic-apps/logsearch.png)

   -или-

   ![Hello OMS выберите пункт меню «Поиск журналов»](media/logic-apps-monitor-your-logic-apps/logsearch-2.png)

5. В поле поиска hello, укажите поля, которые должны toofind и нажмите клавишу **ввод**. При вводе OMS предлагает возможные совпадения и операции, которые можно использовать. 

   Например, toofind hello первые 10 событий, возникших, введите и выберите этот запрос поиска: **категории = WorkflowRuntime | top 10**

   ![Введите строку поиска](media/logic-apps-monitor-your-logic-apps/oms-start-query.png)

   Дополнительные сведения о [как toofind данных в службе анализа журналов](../log-analytics/log-analytics-log-searches.md).

6. На странице результатов hello hello левой панели выберите hello промежуток времени, которые должны tooview.
Выберите запрос, добавив фильтр, toorefine **+ добавить**.

   ![Выберите период времени для результатов запроса](media/logic-apps-monitor-your-logic-apps/query-results.png)

7. В разделе **добавить фильтры**, введите имя фильтра hello, чтобы найти нужный фильтр hello. Выберите фильтр hello и выберите **+ добавить**.

   Этот пример использует hello toofind слово «состояние» сбой события внутри **AzureDiagnostics**.
   Здесь hello фильтр для **status_s** уже выбрана.

   ![Выбор фильтра](media/logic-apps-monitor-your-logic-apps/log-search-add-filter.png)

8. Hello левой панели выберите значение фильтра hello, toouse и задайте **применить**.

   ![Выберите значение фильтра, нажмите кнопку "Применить"](media/logic-apps-monitor-your-logic-apps/log-search-apply-filter.png)

9. Теперь возвращают toohello запрос, для которого выполняется сборка. Запрос был обновлен с учетом выбранных фильтра и значения. Предыдущие результаты теперь также отфильтрованы.

   ![Возвращает запрос tooyour с отфильтрованные результаты](media/logic-apps-monitor-your-logic-apps/log-search-query-filtered-results.png)

10. Выберите запрос для использования в будущем toosave **Сохранить**. Дополнительные сведения [как toosave запроса](../logic-apps/logic-apps-track-b2b-messages-omsportal-query-filter-control-number.md#save-oms-query).

<a name="extend-diagnostic-data"></a>

## <a name="extend-how-and-where-you-use-diagnostic-data-with-other-services"></a>Расширение возможностей использования диагностических данных в других службах

Помимо Azure Log Analytics, можно расширить возможности использования диагностических данных приложения логики в других службах Azure, например: 

* [Архивация журналов диагностики Azure в службе хранилища Azure](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md)
* [Журналы диагностики Azure поток tooAzure концентраторов событий](../monitoring-and-diagnostics/monitoring-stream-diagnostic-logs-to-event-hubs.md) 

После этого можно организовать мониторинг в режиме реального времени с помощью данных телеметрии и аналитики из других служб, таких как [Azure Stream Analytics](../stream-analytics/stream-analytics-introduction.md) и [Power BI](../log-analytics/log-analytics-powerbi.md). Например:

* [Поток данных из концентраторов событий tooStream аналитика](../stream-analytics/stream-analytics-define-inputs.md)
* [Анализ потоковой передачи данных с помощью Stream Analytics и создание панели мониторинга в Power BI для анализа данных в режиме реального времени](../stream-analytics/stream-analytics-power-bi-dashboard.md)

На основании hello параметры настройки, убедитесь, что вы первый [создать учетную запись хранилища Azure](../storage/common/storage-create-storage-account.md) или [создать концентратор событий Azure](../event-hubs/event-hubs-create.md). Затем выберите параметры hello место toosend диагностических данных.

![Отправка данных tooAzure хранилища учетной записи или события концентратора](./media/logic-apps-monitor-your-logic-apps/storage-account-event-hubs.png)

> [!NOTE]
> Сроки хранения применяются только в том случае, при выборе toouse учетной записи хранилища.

<a name="add-azure-alerts"></a>

## <a name="set-up-alerts-for-your-logic-app"></a>Настройка оповещений для приложения логики

Настройка определенных показателей toomonitor или превышены пороговые значения для логики приложения, [оповещения в Azure](../monitoring-and-diagnostics/monitoring-overview-alerts.md). Узнайте подробнее о [метриках в Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md). 

tooset предупреждений без [Azure Log Analytics](../log-analytics/log-analytics-overview.md), выполните следующие действия. Для расширенных критериев оповещений и действий необходимо также [настроить Log Analytics](#azure-diagnostics).

1. Меню hello логику приложения колонке под **мониторинг**, выберите **диагностики** > **предупреждения правила** > **добавить оповещение**как показано ниже:

   ![Добавление оповещения для приложения логики](media/logic-apps-monitor-your-logic-apps/set-up-alerts.png)

2. На hello **Добавление правила оповещения** колонки, создать предупреждение, как показано:

   1. В разделе **Ресурс** выберите приложение логики, если оно еще выбрано. 
   2. Укажите имя и описание для оповещения.
   3. Выберите **метрика** или события, которые должны tootrack.
   4. Выберите **условие**, укажите **пороговое значение** метрика hello и выберите hello **период** для мониторинга эта метрика.
   5. Укажите, требуется ли toosend почты для hello предупреждения. 
   6. Укажите адреса электронной почты для отправки предупреждения hello. 
   Можно также указать URL-адрес веб-перехватчика место toosend hello предупреждение.

   Например, это правило отправляет оповещение после пяти или более сбоев выполнения в течение часа:

   ![Создание правила оповещения для метрики](media/logic-apps-monitor-your-logic-apps/create-alert-rule.png)

> [!TIP]
> приложения логики toorun из оповещения, можно включить hello [триггер запроса](../connectors/connectors-native-reqres.md) в рабочем процессе, которая позволяет выполнять такие задачи, как эти примеры:
> 
> * [POST tooSlack](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app)
> * [Отправка текста](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app)
> * [Добавить tooa очереди сообщений](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app)

<a name="diagnostic-event-properties"></a>

## <a name="azure-diagnostics-event-settings-and-details"></a>Параметры события диагностики Azure и подробные сведения о нем

Каждое событие диагностики содержит подробные сведения о приложении логики и данного события, например, состояние hello, время начала, время окончания и т. д. tooprogrammatically настроить мониторинг, отслеживания и ведения журнала, подразделение можно использовать эти сведения с hello [REST API для приложения логики Azure](https://docs.microsoft.com/rest/api/logic) и hello [REST API для диагностики Azure](../monitoring-and-diagnostics/monitoring-supported-metrics.md#microsoftlogicworkflows).

Здравствуйте, например, `ActionCompleted` событие имеет hello `clientTrackingId` и `trackedProperties` свойства, которые можно использовать для отслеживания и наблюдения:

``` json
{
    "time": "2016-07-09T17:09:54.4773148Z",
    "workflowId": "/SUBSCRIPTIONS/<subscription-ID>/RESOURCEGROUPS/MYRESOURCEGROUP/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/MYLOGICAPP",
    "resourceId": "/SUBSCRIPTIONS/<subscription-ID>/RESOURCEGROUPS/MYRESOURCEGROUP/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/MYLOGICAPP/RUNS/08587361146922712057/ACTIONS/HTTP",
    "category": "WorkflowRuntime",
    "level": "Information",
    "operationName": "Microsoft.Logic/workflows/workflowActionCompleted",
    "properties": {
        "$schema": "2016-06-01",
        "startTime": "2016-07-09T17:09:53.4336305Z",
        "endTime": "2016-07-09T17:09:53.5430281Z",
        "status": "Succeeded",
        "code": "OK",
        "resource": {
            "subscriptionId": "<subscription-ID>",
            "resourceGroupName": "MyResourceGroup",
            "workflowId": "cff00d5458f944d5a766f2f9ad142553",
            "workflowName": "MyLogicApp",
            "runId": "08587361146922712057",
            "location": "westus",
            "actionName": "Http"
        },
        "correlation": {
            "actionTrackingId": "e1931543-906d-4d1d-baed-dee72ddf1047",
            "clientTrackingId": "<my-custom-tracking-ID>"
        },
        "trackedProperties": {
            "myTrackedProperty": "<value>"
        }
    }
}
```

* `clientTrackingId`: Если не указан, Azure автоматически создает этот идентификатор и корреляцию событий между логику приложения будут работать, включая все вложенные рабочие процессы, вызываются из приложения hello логики. Можно вручную задать этот код из триггера, передав `x-ms-client-tracking-id` заголовок с пользовательское значение идентификатора в запросе hello триггера. Можно использовать триггер запроса, триггер HTTP или триггер веб-перехватчика.

* `trackedProperties`: tootrack входные и выходные данные в данные диагностики, tooactions отслеживаемых свойств можно добавить в определение приложения логики JSON. Отслеживаемых свойств можно отслеживать только входные и выходные данные одного действия, но можно использовать hello `correlation` свойства toocorrelate события для действий в сеансе.

  tootrack добавить одно или несколько свойств hello `trackedProperties` раздел и hello свойства, которые хотите toohello определение действия. Например предположим, что требуется tootrack данные, такие как «Идентификатор заказа» в телеметрии:

  ``` json
  "myAction": {
    "type": "http",
    "inputs": {
        "uri": "http://uri",
        "headers": {
            "Content-Type": "application/json"
        },
        "body": "@triggerBody()"
    },
    "trackedProperties": {
        "myActionHTTPStatusCode": "@action()['outputs']['statusCode']",
        "myActionHTTPValue": "@action()['outputs']['body']['<content>']",
        "transactionId": "@action()['inputs']['body']['<content>']"
    }
  }
  ```

## <a name="next-steps"></a>Дальнейшие действия

* [Создание шаблонов для развертывания приложений логики и управления выпусками](../logic-apps/logic-apps-create-deploy-template.md)
* [Сценарии B2B с пакетом интеграции Enterprise](../logic-apps/logic-apps-enterprise-integration-overview.md)
* [Мониторинг сообщений B2B](../logic-apps/logic-apps-monitor-b2b-message.md)