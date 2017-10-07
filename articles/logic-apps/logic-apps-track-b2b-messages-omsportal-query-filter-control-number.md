---
title: "aaaQuery B2B сообщений в Operations Management Suite - приложения логики Azure | Документы Microsoft"
description: "Создание запросов tootrack AS2, X 12 и EDIFACT сообщений в hello Operations Management Suite"
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
ms.date: 07/21/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: aee6644ff19add8f074ed5f1725db87b1d3b74b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="query-for-as2-x12-and-edifact-messages-in-hello-microsoft-operations-management-suite-oms"></a>Запрос для AS2, X 12 и EDIFACT сообщений hello Microsoft Operations Management Suite (OMS)

hello toofind AS2, X 12 и EDIFACT сообщений, которые отслеживаются с [Azure Log Analytics](../log-analytics/log-analytics-overview.md) в hello [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md), можно создавать запросы, которые фильтруют действия в зависимости от конкретных критерии. Например, можно найти сообщения с определенным контрольным номером обмена.

## <a name="requirements"></a>Требования

* Приложение логики, настроенное на ведение журнала диагностики. Дополнительные сведения [как toocreate приложения логики](../logic-apps/logic-apps-create-a-logic-app.md) и [как tooset ведение журнала для данного приложения логики](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).

* Учетная запись интеграции, настроенная для мониторинга и ведения журнала. Дополнительные сведения [как toocreate учетной записи интеграции](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) и [как tooset мониторинга и ведения журнала для этой учетной записи](../logic-apps/logic-apps-monitor-b2b-message.md).

* Если это еще не сделано, [публикации tooLog диагностических данных аналитики](../logic-apps/logic-apps-track-b2b-messages-omsportal.md) и [Настройка отслеживания в OMS сообщений](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).

> [!NOTE]
> После hello предыдущих требования соблюдены, должно быть рабочей hello [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md). Следует использовать одну рабочую область OMS для отслеживания B2B связи в OMS hello. 
>  
> Если у вас нет рабочей области OMS, узнайте [как toocreate рабочей области OMS](../log-analytics/log-analytics-get-started.md).

## <a name="create-message-queries-with-filters-in-hello-operations-management-suite-portal"></a>Создание запросов сообщений с фильтрами в портал Operations Management Suite hello

В этом примере показано, как найти сообщение по контрольному номеру обмена.

> [!TIP] 
> Если известно имя рабочей области OMS, перейдите Домашняя страница рабочей области tooyour (`https://{your-workspace-name}.portal.mms.microsoft.com`) и запустить на шаге 4. В противном случае начните с шага 1.

1. В hello [портал Azure](https://portal.azure.com), выберите **более служб**. Введите в поле поиска "log analytics" и выберите **Log Analytics**, как показано ниже.

   ![Поиск Log Analytics](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/browseloganalytics.png)

2. В разделе **Log Analytics** найдите и выберите рабочую область OMS.

   ![Выбор рабочей области OMS](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/selectla.png)

3. В разделе **Управление** выберите **Портал OMS**.

   ![Выбор портала OMS](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/omsportalpage.png)

4. На домашней странице OMS выберите **Поиск по журналам**.

   ![На домашней странице OMS выберите "Поиск по журналам"](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch.png)

   -или-

   ![Hello OMS выберите пункт меню «Поиск журналов»](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch-2.png)

5. Введите в поле поиска hello, поля, которые должны toofind и нажмите клавишу **ввод**. При вводе OMS предлагает возможные совпадения и операции, которые можно использовать. Дополнительные сведения о [как toofind данных в службе анализа журналов](../log-analytics/log-analytics-log-searches.md).

   В этом примере выполняется поиск событий с параметром **Type=AzureDiagnostics**.

   ![Начните вводить строку запроса](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-start-query.png)

6. В левой панели hello, выберите период hello, которые должны tooview. Выберите tooadd tooyour запрос фильтра **+ добавить**.

   ![Добавить фильтр tooquery](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/query1.png)

7. В разделе **добавить фильтры**, введите имя фильтра hello, чтобы найти нужный фильтр hello. Выберите фильтр hello и выберите **+ добавить**.

   toofind hello контрольного числа, в этом примере ищет слово hello «сообщения» и выбирает **event_record_messageProperties_interchangeControlNumber_s** как фильтр hello.

   ![Выбор фильтра](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-add-filter.png)

9. Hello левой панели выберите значение фильтра hello, toouse и задайте **применить**.

   В этом примере выбирает hello контрольное число сообщения hello нужным нам.

   ![Выбор значения фильтра](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-select-filter-value.png)

10. Теперь возвращают toohello запрос, для которого выполняется сборка. Запрос был обновлен с учетом выбранных фильтра событий и значения. Предыдущие результаты теперь также отфильтрованы.

    ![Возвращает запрос tooyour с отфильтрованные результаты](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-filtered-results.png)

<a name="save-oms-query"></a>

## <a name="save-your-query-for-future-use"></a>Сохранение запроса для использования в будущем

1. Из запроса на hello **поиска журналов** выберите **Сохранить**. Присвойте запросу имя, выберите категорию и нажмите **Сохранить**.

   ![Присвойте запросу имя и категорию](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-save.png)

2. tooview ваш запрос, выберите **Избранное**.

   ![Выберите "Избранное"](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-favorites.png)

3. В разделе **сохраненные поиски**, выберите запрос, можно просмотреть результаты hello. запрос hello редактировать tooupdate hello запрос, чтобы найти другие результаты.

   ![Выбор запроса](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-log-search-find-favorites.png)

## <a name="find-and-run-saved-queries-in-hello-operations-management-suite-portal"></a>Найдите и запустите сохраненные запросы в портал Operations Management Suite hello

1. Откройте домашнюю страницу рабочей области OMS (`https://{your-workspace-name}.portal.mms.microsoft.com`) и выберите **Поиск по журналам**.

   ![На домашней странице OMS выберите "Поиск по журналам"](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch.png)

   -или-

   ![Hello OMS выберите пункт меню «Поиск журналов»](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch-2.png)

2. На hello **поиска журналов** домашнюю страницу, выберите **Избранное**.

   ![Выберите "Избранное"](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-log-search-favorites.png)

3. В разделе **сохраненные поиски**, выберите запрос, можно просмотреть результаты hello. запрос hello редактировать tooupdate hello запрос, чтобы найти другие результаты.

   ![Выбор запроса](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-log-search-find-favorites.png)

## <a name="next-steps"></a>Дальнейшие действия

* [Схемы отслеживания AS2](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)
* [Схемы отслеживания X12](../logic-apps/logic-apps-track-integration-account-x12-tracking-schema.md)
* [Настраиваемые схемы отслеживания](../logic-apps/logic-apps-track-integration-account-custom-tracking-schema.md)