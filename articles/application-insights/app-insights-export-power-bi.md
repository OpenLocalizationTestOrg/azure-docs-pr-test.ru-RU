---
title: "tooPower aaaExport бизнес-Аналитики из Application Insights | Документы Microsoft"
description: "Аналитические запросы можно просматривать в Power BI."
services: application-insights
documentationcenter: 
author: noamben
manager: carmonm
ms.assetid: 7f13ea66-09dc-450f-b8f9-f40fdad239f2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/18/2016
ms.author: bwren
ms.openlocfilehash: 6668cd7f4e0fbf41695972617f5f8ec207356659
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="feed-power-bi-from-application-insights"></a>Использование данных Application Insights в Power BI
[Power BI](http://www.powerbi.com/) — это набор средств бизнес-аналитики для анализа данных и обмена сведениями. На каждом устройстве доступны панели мониторинга с широкими возможностями. Вы можете объединять данные из различных источников, в том числе аналитические запросы из [ Application Insights](app-insights-overview.md).

Существуют три способа рекомендуемые экспорта tooPower Application Insights данных бизнес-Аналитики. Их можно использовать отдельно или совместно.

* [**Использование адаптера Power BI** ](#power-pi-adapter). С его помощью можно настроить панель мониторинга телеметрии из своего приложения. предопределенные Hello набора диаграмм, но можно добавить собственные запросы с другими источниками.
* [**Экспорт аналитические запросы** ](#export-analytics-queries) -записи любого запроса с помощью аналитика и экспортировать его tooPower бизнес-Аналитики. Его можно разместить на панели мониторинга вместе с другими данными.
* [**Непрерывный Экспорт и Stream Analytics** ](app-insights-export-stream-analytics.md) -это включает в себя дополнительные рабочие tooset вверх. Оно полезно в том случае, если требуется tookeep данных для длительных периодов времени. В противном случае hello других методов, рекомендуется использовать.

## <a name="power-bi-adapter"></a>Использование адаптера Power BI
Этот метод предполагает создание панели мониторинга телеметрии. предопределенные Hello первоначального набора данных, но можно добавить дополнительные tooit данных.

### <a name="get-hello-adapter"></a>Получает адаптер hello
1. Войдите в слишком[Power BI](https://app.powerbi.com/).
2. Выберите **Получение данных**, **Службы**, **Application Insights**.
   
    ![Получение из источника данных Application Insights](./media/app-insights-export-power-bi/power-bi-adapter.png)
3. Подробно hello ресурса Application Insights.
   
    ![Получение из источника данных Application Insights](./media/app-insights-export-power-bi/azure-subscription-resource-group-name.png)
4. Подождите одну или две для импорта toobe данных hello минуты.
   
    ![Использование адаптера Power BI](./media/app-insights-export-power-bi/010.png)

Можно изменить панель мониторинга hello, объединение диаграмм hello Application Insights с их из других источников и аналитические запросы. В коллекции визуализации доступны дополнительные диаграммы, и у каждой диаграммы есть параметры, которые можно задать.

После первоначального импорта hello, hello панели мониторинга и отчеты hello продолжить tooupdate ежедневно. Можно управлять hello расписание обновления для набора данных hello.

## <a name="export-analytics-queries"></a>Экспорт запросов аналитики
Данный маршрут позволяет toowrite любой Analytics вы хотите запросить, а затем экспортируйте этой панели мониторинга Power BI tooa. (Можно добавить toohello панель мониторинга, созданную адаптером hello.)

### <a name="one-time-install-power-bi-desktop"></a>Короткий путь: установка Power BI Desktop
tooimport запроса Application Insights, используйте Power BI версии hello настольного компьютера. Но затем его можно опубликовать веб-toohello или tooyour рабочей области Power BI облака. 

Установите [Power BI Desktop](https://powerbi.microsoft.com/en-us/desktop/).

### <a name="export-an-analytics-query"></a>Экспорт запроса аналитики
1. [Откройте средство аналитики и напишите запрос](app-insights-analytics-tour.md).
2. Тестирование и доработку hello запроса, пока вы довольны hello результаты.

   **Убедитесь, что hello запросов выполняется правильно в аналитике, прежде чем экспортировать его.**
3. На hello **Экспорт** меню, выберите **Power BI (M)**. Сохраните текстовый файл hello.
   
    ![Экспорт запроса Power BI](./media/app-insights-export-power-bi/analytics-export-power-bi.png)
4. В Power BI Desktop выберите **получить данные, пустой запрос** и затем в hello редактор запросов, в разделе **представление** выберите **расширенного редактора запросов**.

    Вставить скрипт язык M hello экспортированы в hello расширенного редактора запросов.

    ![Расширенный редактор запросов](./media/app-insights-export-power-bi/power-bi-import-analytics-query.png)

1. Может потребоваться Power BI-tooaccess tooallow tooprovide учетные данные Azure. Используйте «учетная запись организации» toosign учетной записью Майкрософт.
   
    ![Укажите учетные данные Azure tooenable Power BI toorun запроса Application Insights](./media/app-insights-export-power-bi/power-bi-import-sign-in.png)

    (Если необходимы учетные данные tooverify hello, используйте команду меню hello параметры источника данных в hello редактора запросов. Быть меры предосторожности hello toospecify учетные данные, которые для Azure, который может отличаться от учетных данных для Power BI.)
2. Выбрать визуализацию для запроса и выбирать поля hello для оси x, y и сегментирования измерения.
   
    ![Выбор визуализации](./media/app-insights-export-power-bi/power-bi-analytics-visualize.png)
3. Публикация отчетов Power BI tooyour облака рабочей области. Из нее можно внедрять синхронизированную версию на другие веб-страницы.
   
    ![Выбор визуализации](./media/app-insights-export-power-bi/publish-power-bi.png)
4. Вручную обновить отчет hello интервалы или настроить запланированное обновление на странице параметров hello.

## <a name="troubleshooting"></a>Устранение неполадок

### <a name="401-or-403-unauthorized"></a>401 или 403 — недостаточно прав 
Это может произойти, если токен обновления не обновлен. Повторите эти шаги tooensure, по-прежнему имеется доступ. Если у вас есть доступ, и учетные данные обновлении hello не работает, обратитесь в службу поддержки.

1. Войдите в портал Azure hello и убедитесь, что вам разрешен доступ к ресурсу hello
2. Попробуйте вводить учетные данные hello toorefresh для hello панели мониторинга

### <a name="502-bad-gateway"></a>502 — Недопустимый шлюз
Обычно это вызвано запросом аналитики, который возвращает слишком много данных. Вначале следует проверить с помощью меньший диапазон времени или с помощью hello [Назад](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#ago) или [startofweek/startofmonth](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#startofweek) только для функций [проекта](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#project-operator) hello необходимые поля.

Если уменьшить hello набора данных, поступающих от hello аналитический запрос не соответствует вашим требованиям можно использовать hello [API](https://dev.applicationinsights.io/documentation/overview) toopull набора данных большего размера. Ниже приведены инструкции по инструкции tooconvert hello запросов M Экспорт toouse hello API.

1. Создайте [ключ API](https://dev.applicationinsights.io/documentation/Authorization/API-key-and-App-ID).
2. Обновление hello Power BI M скрипт, который был экспортирован из Analytics, заменив hello ARM URL-адрес с AI API (см. пример ниже)
   * Замените **https://management.azure.com/subscriptions/...**
   * на **https://api.applicationinsights.io/beta/apps/...**
3. Наконец обновления toobasic учетные данные и использовать ваш ключ API
  

**Существующий скрипт**
 ```
 Source = Json.Document(Web.Contents("https://management.azure.com/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups//providers/microsoft.insights/components//api/query?api-version=2014-12-01-preview",[Query=[#"csl"="requests",#"x-ms-app"="AAPBI"],Timeout=#duration(0,0,4,0)]))
 ```
**Обновленный скрипт**
 ```
 Source = Json.Document(Web.Contents("https://api.applicationinsights.io/beta/apps/<APPLICATION_ID>/query?api-version=2014-12-01-preview",[Query=[#"csl"="requests",#"x-ms-app"="AAPBI"],Timeout=#duration(0,0,4,0)]))
 ```

## <a name="about-sampling"></a>Дополнительная информация о выборке
Если приложение отправляет большой объем данных, функция адаптивной выборки hello может работать и отправьте доля телеметрии. то же верно, если вручную выборки в hello SDK или на приема приветствия. [Дополнительная информация о выборке.](app-insights-sampling.md)


## <a name="next-steps"></a>Дальнейшие действия
* [Дополнительные сведения о Power BI](http://www.powerbi.com/learning/)
* [Руководство по аналитике](app-insights-analytics-tour.md)

