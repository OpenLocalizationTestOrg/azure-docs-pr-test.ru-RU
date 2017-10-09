---
title: "aaaMonitor и получения ценной информации о приложении логики выполняется с помощью OMS - приложения логики Azure | Документы Microsoft"
description: "Мониторинг работы логики приложения с мнениями tooget анализа журналов и Operations Management Suite (OMS) и более полных сведений отладки для диагностики и устранения неполадок"
author: divyaswarnkar
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/9/2017
ms.author: LADocs; divswa
ms.openlocfilehash: a76fd6d1ff5c0010550be0f991514ce95f659fd6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-get-insights-about-logic-app-runs-with-operations-management-suite-oms-and-log-analytics"></a>Мониторинг выполнения приложений логики и получение аналитических сведений о них с помощью Operations Management Suite (OMS) и Log Analytics

Для мониторинга и расширенные сведения по отладке, можно включить аналитики журналов в hello одновременно при создании приложения логики. Предоставляет службы анализа журналов диагностики, ведение журнала и мониторинг для логики приложения выполняется через портал Operations Management Suite (OMS) hello. При добавлении tooOMS решение управления логику приложения hello, вы получаете обобщенное состояние для вашей запусков логику приложения и конкретные сведения, как состояние, время выполнения, состояние повторной передачи и идентификаторы корреляции.

В этом разделе показано, как tooturn для анализа журналов или установите hello решения по управлению приложениями логики в OMS можно просматривать события среды выполнения и запуска данных логики приложения.

 > [!TIP]
 > toomonitor существующие логики приложения, выполните следующие действия слишком [включить ведение журнала диагностики и отправка логики приложения среды выполнения данных tooOMS](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).

## <a name="requirements"></a>Требования

Прежде чем начать, необходимо toohave рабочей области OMS. Дополнительные сведения [как toocreate рабочей области OMS](../log-analytics/log-analytics-get-started.md). 

## <a name="turn-on-diagnostics-logging-when-creating-logic-apps"></a>Включение ведения журнала диагностики при создании приложений логики

1. На [портале Azure](https://portal.azure.com) создайте приложение логики. Выберите **Создать** > **Интеграция Enterprise** > **Приложение логики** > **Создать**.

   ![Создайте приложение логики](media/logic-apps-monitor-your-logic-apps-oms/find-logic-apps-azure.png)

2. В hello **создать логику приложение** выполните следующие задачи, как показано:

   1. Введите имя приложения логики и выберите подписку Azure. 
   2. Создайте или выберите существующую группу ресурсов Azure.
   3. Задать **анализа журналов** слишком**на**. 
   Рабочая область OMS выберите hello место слишком отправки данных для логики приложения выполняется. 
   4. Когда вы будете готовы, нажмите кнопку **toodashboard ПИН-код** > **создать**.

      ![Создание приложения логики](./media/logic-apps-monitor-your-logic-apps-oms/create-logic-app.png)

      По завершении этого шага Azure создает приложение логики, которое теперь связано с рабочей областью OMS. 
      Кроме того этот шаг также автоматически устанавливает решение по управлению приложениями логики hello в рабочей области OMS.

3. логика приложения выполняется в OMS, tooview [выполните следующие действия](#view-logic-app-runs-oms).

## <a name="install-hello-logic-apps-management-solution-in-oms"></a>Установка решения управления логику приложения hello в OMS

Если вы уже включили Log Analytics при создании приложения логики, то пропустите этот шаг. Уже имеется решение управления логику приложения hello в OMS.

1. В hello [портал Azure](https://portal.azure.com), выберите **более служб**. В поле поиска введите словосочетание "log analytics" в качестве фильтра и выберите **Log Analytics**, как показано ниже.

   ![Выберите "Log Analytics"](media/logic-apps-monitor-your-logic-apps-oms/find-log-analytics.png)

2. В разделе **Log Analytics** найдите и выберите рабочую область OMS. 

   ![Выбор рабочей области OMS](media/logic-apps-monitor-your-logic-apps-oms/select-logic-app.png)

3. В разделе **Управление** выберите **Портал OMS**.

   ![Выберите "Портал OMS"](media/logic-apps-monitor-your-logic-apps-oms/oms-portal-page.png)

4. На главной странице OMS Если отображается баннер обновления hello, нажмите баннер hello, чтобы сначала обновить рабочую область OMS. Затем выберите **Коллекция решений**.

   ![Выбор "Коллекции решений"](media/logic-apps-monitor-your-logic-apps-oms/solutions-gallery.png)

5. В разделе **все решения**, найдите и выберите плитку hello для hello **управления приложениями логики** решения.

   ![Выбор Logic Apps Management](media/logic-apps-monitor-your-logic-apps-oms/logic-apps-management-tile2.png)

6. Выберите решение tooinstall hello в рабочую область OMS **добавить**.

   ![Кнопка "Добавить" для Logic Apps Management](media/logic-apps-monitor-your-logic-apps-oms/add-logic-apps-management-solution.png)

<a name="view-logic-app-runs-oms"></a>

## <a name="view-your-logic-app-runs-in-your-oms-workspace"></a>Просмотр сведений о выполнении приложений логики в рабочей области OMS

1. число tooview hello и состояние для логики приложения выполняется, последовательно выберите toohello страница обзора для рабочей области OMS. Просмотрите сведения об hello на hello **управления приложениями логики** плитки.

   ![Элемент обзора, показывающий количество и состояние выполнений приложений логики](media/logic-apps-monitor-your-logic-apps-oms/overview.png)

   > [!Note]
   > Если это обновление баннера отображается вместо плитки управления логику приложения hello, выберите баннер hello, чтобы сначала обновить рабочую область OMS.
  
   > ![Обновление рабочей области OMS](media/logic-apps-monitor-your-logic-apps-oms/oms-upgrade-banner.png)

2. tooview Сводка более подробные данные о работы логики приложения выберите hello **управления приложениями логики** плитки.

   Здесь сведения о выполнении приложений логики группируются по имени или по состоянию выполнения.

   ![Сводные данные о состоянии выполнения приложений логики](media/logic-apps-monitor-your-logic-apps-oms/logic-apps-runs-summary.png)
   
3. tooview, все hello выполняется для логики, специфичной для приложения или состояние, выберите hello строку приложения логики или состояние.

   Ниже приведен пример, в котором показаны все фрагменты hello для логики, специфичной для приложения:

   ![Просмотр сведений о выполнении по приложению логики или по состоянию](media/logic-apps-monitor-your-logic-apps-oms/logic-app-run-details.png)

   > [!NOTE]
   > Hello **повторной передачи** столбце отображается «Да» для выполнения, возникающие в результате повторно отправлено выполнения.

4. toofilter эти результаты, можно выполнить фильтрацию клиентские и серверные.

   * Клиентский фильтр: для каждого столбца выберите hello фильтры, которые нужно. 
   Ниже приведены некоторые примеры:

     ![Пример фильтров столбцов](media/logic-apps-monitor-your-logic-apps-oms/filters.png)

   * Серверный фильтр: toochoose число запусков, которые отображаются, используйте элемент управления области hello вверху hello страницы приветствия определенное время окна или toolimit hello. 
   По умолчанию за раз отображается только 1000 записей. 
   
     ![Период времени изменения hello](media/logic-apps-monitor-your-logic-apps-oms/change-interval.png)
 
5. все tooview hello действия и сведения о них конкретного выполнения, выберите строку, откроется страница поиска журналов hello. 

   * tooview эти сведения в таблице, выберите **таблицы**.
   * запрос toochange hello, можно изменить строку запроса hello в строке поиска hello. 
   Для доступа к дополнительным функциональным возможностям выберите **Расширенная аналитика**.

     ![Просмотр действий и сведений о них для выполнения приложения логики](media/logic-apps-monitor-your-logic-apps-oms/log-search-page.png)

     Здесь на странице приветствия анализа журналов Azure, можно обновить запросы и представления hello результаты из таблицы hello. 
     В этом запросе используется [язык запросов Kusto](https://docs.loganalytics.io/learn/tutorials/getting_started_with_queries.html), его можно изменить, если требуется tooview различные результаты. 

     ![Представление запросов в Azure Log Analytics](media/logic-apps-monitor-your-logic-apps-oms/query.png)

## <a name="next-steps"></a>Дальнейшие действия

* [Мониторинг сообщений B2B](../logic-apps/logic-apps-monitor-b2b-message.md)
