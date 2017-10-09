---
title: "транзакции aaaMonitor B2B и настройте ведение журнала - приложения логики Azure | Документы Microsoft"
description: "Мониторинг сообщений AS2, X 12 и EDIFACT, запуск ведения журнала диагностики для учетной записи интеграции"
author: padmavc
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: bb7d9432-b697-44db-aa88-bd16ddfad23f
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 07/21/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: a6745ebf41aab331020bfec072f5806711d125bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-set-up-diagnostics-logging-for-b2b-communication-in-integration-accounts"></a>Мониторинг и настройка ведения журнала диагностики для взаимодействия B2B в учетных записях интеграции

После настройки взаимодействия B2B между двумя выполняющимися бизнес-процессами или приложениями с помощью учетной записи интеграции эти сущности могут обмениваться сообщениями друг с другом. tooconfirm это взаимодействие работает надлежащим образом, можно настроить наблюдение за AS2, X12, и сообщения EDIFACT, а также ведение журнала диагностики для вашей учетной записи интеграции через hello [Azure Log Analytics](../log-analytics/log-analytics-overview.md) службы. Эта служба в [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md) отслеживает облачную и локальную среды, помогая обеспечить их доступность и производительность, а также собирает сведения о времени выполнения и событиях для отладки. Также можно [использовать полученные диагностические данные в других службах](#extend-diagnostic-data), таких как служба хранилища Azure и концентраторы событий Azure.

## <a name="requirements"></a>Требования

* Приложение логики, настроенное на ведение журнала диагностики. Дополнительные сведения [как tooset ведение журнала для данного приложения логики](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).

  > [!NOTE]
  > После этого требования соблюдены, должно быть рабочей hello [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md). Следует использовать одну рабочую область OMS hello, при настройке ведения журнала для вашей учетной записи интеграции. Если у вас нет рабочей области OMS, узнайте [как toocreate рабочей области OMS](../log-analytics/log-analytics-get-started.md).

* Учетная запись интеграции со связанными tooyour логику приложения. Дополнительные сведения [учетной записи toocreate интеграцию с приложениями логики tooyour ссылку](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md).

## <a name="turn-on-diagnostics-logging-for-your-integration-account"></a>Включение ведения журнала диагностики для учетной записи интеграции

Вы можете включить ведение журнала, либо непосредственно от учетной записи интеграции или [через hello Azure мониторинг службы](#azure-monitor-service). Служба Azure Monitor предоставляет основные функции мониторинга с помощью данных на уровне инфраструктуры. Узнайте подробнее о службе [Azure Monitor](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md).

### <a name="turn-on-diagnostics-logging-directly-from-your-integration-account"></a>Включение ведения журнала диагностики в учетной записи интеграции

1. В hello [портал Azure](https://portal.azure.com), найдите и выберите свою учетную запись интеграции. В разделе **Мониторинг** выберите **Журналы диагностики**, как показано ниже.

   ![Найдите и выберите учетную запись интеграции, а затем — "Журналы диагностики"](media/logic-apps-monitor-b2b-message/integration-account-diagnostics.png)

2. После выбора учетной записи интеграции hello последующих значений будут выбраны автоматически. Если эти значения верны, выберите **Включить диагностику**. В противном случае выберите необходимые значения hello:

   1. В разделе **подписки**, выберите hello подписки Azure, используемой с вашей учетной записи интеграции.
   2. В разделе **группы ресурсов**выберите hello группы ресурсов, используемой с вашей учетной записи интеграции.
   3. В раскрывающемся списке **Тип ресурса** выберите **Учетные записи интеграции**. 
   4. В раскрывающемся списке **Ресурс** выберите учетную запись интеграции. 
   5. Выберите **Включить диагностику**.

   ![Настройка системы диагностики для учетной записи интеграции](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account.png)

3. В разделе **Параметры диагностики** > **Состояние** выберите **Вкл**.

   ![Включение системы диагностики Microsoft Azure](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account-2.png)

4. Теперь выберите hello OMS рабочей области и данных toouse для ведения журнала, как показано:

   1. Выберите **отправки tooLog Analytics**. 
   2. В разделе **Log Analytics** выберите **Настройка**. 
   3. В разделе **рабочих областей OMS**, выберите toouse рабочей области OMS hello для ведения журнала.
   4. В разделе **журнала**выберите hello **IntegrationAccountTrackingEvents** категории.
   5. Нажмите **Сохранить**.

   ![Настройка аналитики журналов для отправки журналов tooa данных диагностики](media/logic-apps-monitor-b2b-message/send-diagnostics-data-log-analytics-workspace.png)

5. Теперь [настройте отслеживание сообщений B2B в OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).

<a name="azure-monitor-service"></a>

### <a name="turn-on-diagnostics-logging-through-azure-monitor"></a>Включение ведения журнала диагностики в службе Azure Monitor

1. В hello [портал Azure](https://portal.azure.com), на hello главного меню Azure, выберите **монитор**, **журналы диагностики**. Затем выберите учетную запись интеграции, как показано ниже:

   ![Выберите "Мониторинг", "Журналы диагностики", выберите свою учетную запись интеграции](media/logic-apps-monitor-b2b-message/monitor-service-diagnostics-logs.png)

2. После выбора учетной записи интеграции hello последующих значений будут выбраны автоматически. Если эти значения верны, выберите **Включить диагностику**. В противном случае выберите необходимые значения hello:

   1. В разделе **подписки**, выберите hello подписки Azure, используемой с вашей учетной записи интеграции.
   2. В разделе **группы ресурсов**выберите hello группы ресурсов, используемой с вашей учетной записи интеграции.
   3. В раскрывающемся списке **Тип ресурса** выберите **Учетные записи интеграции**.
   4. В раскрывающемся списке **Ресурс** выберите учетную запись интеграции.
   5. Выберите **Включить диагностику**.

   ![Настройка системы диагностики для учетной записи интеграции](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account.png)

3. В разделе **Параметры диагностики** выберите **Вкл**.

   ![Включение системы диагностики Microsoft Azure](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account-2.png)

4. Теперь выберите hello OMS рабочей области и категории событий для ведения журнала, как показано:

   1. Выберите **отправки tooLog Analytics**. 
   2. В разделе **Log Analytics** выберите **Настройка**. 
   3. В разделе **рабочих областей OMS**, выберите toouse рабочей области OMS hello для ведения журнала.
   4. В разделе **журнала**выберите hello **IntegrationAccountTrackingEvents** категории.
   5. Когда все будет готово, нажмите **Сохранить**.

   ![Настройка аналитики журналов для отправки журналов tooa данных диагностики](media/logic-apps-monitor-b2b-message/send-diagnostics-data-log-analytics-workspace.png)

5. Теперь [настройте отслеживание сообщений B2B в OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).

## <a name="extend-how-and-where-you-use-diagnostic-data-with-other-services"></a>Расширение возможностей использования диагностических данных в других службах

Помимо Azure Log Analytics, можно расширить возможности использования диагностических данных приложения логики в других службах Azure, например: 

* [Архивация журналов диагностики Azure в службе хранилища Azure](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md)
* [Журналы диагностики Azure поток tooAzure концентраторов событий](../monitoring-and-diagnostics/monitoring-stream-diagnostic-logs-to-event-hubs.md) 

После этого можно организовать мониторинг в режиме реального времени с помощью данных телеметрии и аналитики из других служб, таких как [Azure Stream Analytics](../stream-analytics/stream-analytics-introduction.md) и [Power BI](../log-analytics/log-analytics-powerbi.md). Например:

* [Поток данных из концентраторов событий tooStream аналитика](../stream-analytics/stream-analytics-define-inputs.md)
* [Анализ потоковой передачи данных с помощью Stream Analytics и создание панели мониторинга в Power BI для анализа данных в режиме реального времени](../stream-analytics/stream-analytics-power-bi-dashboard.md)

На основании hello параметры настройки, убедитесь, что вы первый [создать учетную запись хранилища Azure](../storage/common/storage-create-storage-account.md) или [создать концентратор событий Azure](../event-hubs/event-hubs-create.md). Затем выберите параметры hello место toosend диагностических данных.

![Отправка данных tooAzure хранилища учетной записи или события концентратора](./media/logic-apps-monitor-b2b-message/storage-account-event-hubs.png)

> [!NOTE]
> Сроки хранения применяются только в том случае, при выборе toouse учетной записи хранилища.

## <a name="supported-tracking-schemas"></a>Поддерживаемые схемы отслеживания

Azure поддерживает эти типы схемы, которые имеют фиксированное схемы, за исключением hello пользовательский тип отслеживания.

* [Схема отслеживания AS2](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)
* [Схема отслеживания X12](../logic-apps/logic-apps-track-integration-account-x12-tracking-schema.md)
* [Настраиваемая схема отслеживания](../logic-apps/logic-apps-track-integration-account-custom-tracking-schema.md)

## <a name="next-steps"></a>Дальнейшие действия

* [Отслеживание сообщений B2B в OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md "Отслеживание сообщений B2B в OMS")
* [Дополнительные сведения о hello пакет интеграции Enterprise](../logic-apps/logic-apps-enterprise-integration-overview.md "Дополнительные сведения о пакет интеграции Enterprise")

