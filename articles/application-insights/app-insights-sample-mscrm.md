---
title: "aaaMicrosoft Dynamics CRM и аналитика приложений Azure | Документы Microsoft"
description: "Получение данных телеметрии из Microsoft Dynamics CRM Online с помощью Application Insights. Пошаговое руководство по настройке, получению данных, визуализации и экспорту."
services: application-insights
documentationcenter: 
author: mazharmicrosoft
manager: carmonm
ms.assetid: 04c66338-687e-49e5-9975-be935f98f156
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 04/16/2017
ms.author: bwren
ms.openlocfilehash: a39398060d6553fb18a26c101f085b7d87443636
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-enabling-telemetry-for-microsoft-dynamics-crm-online-using-application-insights"></a>Пошаговое руководство. Включение телеметрии для Microsoft Dynamics CRM Online с помощью Application Insights
В этой статье показано, как данные телеметрии tooget из [Microsoft Dynamics CRM Online](https://www.dynamics.com/) с помощью [Azure Application Insights](https://azure.microsoft.com/services/application-insights/). Мы рассмотрим hello полный процесс добавления приложения tooyour сценария Application Insights, сбора данных и визуализации данных.

> [!NOTE]
> [Обзор решения образца hello](https://dynamicsandappinsights.codeplex.com/).
> 
> 

## <a name="add-application-insights-toonew-or-existing-crm-online-instance"></a>Добавить Application Insights toonew или существующего экземпляра CRM Online
toomonitor приложения, добавления приложения tooyour пакет SDK Application Insights. Hello SDK отправляет данные телеметрии toohello [портале Application Insights](https://portal.azure.com), где можно использовать наши мощный анализ и средства диагностики, или экспорт данных toostorage hello.

### <a name="create-an-application-insights-resource-in-azure"></a>Создание ресурса Application Insights в Azure
1. Получите [учетную запись Microsoft Azure](http://azure.com/pricing). 
2. Вход в hello [портал Azure](https://portal.azure.com) и добавить новый ресурс Application Insights. Здесь будут обрабатываться и отображаться ваши данные.
   
    ![Щелкните значок «+» и последовательно выберите «Службы для разработчиков», Application Insights.](./media/app-insights-sample-mscrm/01.png)
   
    Выберите в качестве типа приложения hello ASP.NET.
3. Открытие страницы «hello Приступая к работе» и откройте «монитор и диагностики на стороне клиента».
   
    ![Фрагмент кода для вставки на веб-страницу](./media/app-insights-sample-mscrm/03.png)

**Не закрывайте hello кодовая страница** пока hello следующим шагом в другом окне браузера. Вам потребуется скоро кода hello. 

### <a name="create-a-javascript-web-resource-in-microsoft-dynamics-crm"></a>Создание веб-ресурса JavaScript в Microsoft Dynamics CRM
1. Откройте экземпляр CRM Online и войдите с правами администратора.
2. Откройте Microsoft Dynamics CRM параметры настройки, hello Настройка системы
   
    ![Параметры Microsoft Dynamics CRM](./media/app-insights-sample-mscrm/04.png)
   
    ![Параметры > Настройки](./media/app-insights-sample-mscrm/05.png)

    ![Настроить параметр системного hello](./media/app-insights-sample-mscrm/06.png)

1. Создайте ресурс JavaScript.
   
    ![Диалоговое окно создания веб-ресурса](./media/app-insights-sample-mscrm/07.png)
   
    Присвойте ему имя, выберите **сценария (JScript)** и hello откройте текстовый редактор.
   
    ![Привет открыть текстовый редактор](./media/app-insights-sample-mscrm/08.png)
2. Скопируйте код hello из Application Insights. При копировании убедитесь, что tooignore теги сценариев. См. ниже снимок экрана.
   
    ![Задайте ключ инструментирования](./media/app-insights-sample-mscrm/09.png)
   
    Код Hello содержит ключ инструментирования hello, идентифицирующее ваш ресурс Application insights.
3. Щелкните «Сохранить», а затем «Опубликовать».
   
    ![Сохранение и публикация](./media/app-insights-sample-mscrm/10.png)

### <a name="instrument-forms"></a>Формы инструментов
1. В Microsoft CRM Online откройте форму hello учетной записи
   
    ![Форма учетной записи](./media/app-insights-sample-mscrm/11.png)
2. Откройте форму hello свойства
   
    ![Свойства формы](./media/app-insights-sample-mscrm/12.png)
3. Добавить hello JavaScript веб-ресурса, который вы создали
   
    ![Меню "Добавить"](./media/app-insights-sample-mscrm/13.png)
   
    ![Добавить веб-ресурс hello](./media/app-insights-sample-mscrm/14.png)
4. Сохраните и опубликуйте настройки формы.

## <a name="metrics-captured"></a>Собранные показатели телеметрии
Теперь вы настроили сбор данных телеметрии для hello формы. Каждый раз, когда он используется, данные будут отправлены tooyour ресурс Application Insights.

Ниже приведены примеры данных hello, вы увидите.

#### <a name="application-health"></a>Работоспособность приложения
![Время загрузки образца страницы](./media/app-insights-sample-mscrm/15.png)

![Пример диаграммы просмотров страницы](./media/app-insights-sample-mscrm/16.png)

Исключения браузера:

![Диаграмма "Исключения браузера"](./media/app-insights-sample-mscrm/17.png)

Щелкните диаграмму tooget hello более подробно:

![Список исключений](./media/app-insights-sample-mscrm/18.png)

#### <a name="usage"></a>Использование
![Представления числа пользователей, сеансов и просмотров страниц](./media/app-insights-sample-mscrm/19.png)

![Диаграммы сеансов](./media/app-insights-sample-mscrm/20.png)

![Версии браузеров](./media/app-insights-sample-mscrm/21.png)

#### <a name="browsers"></a>Браузеры
![Разбивка времени загрузки страницы](./media/app-insights-sample-mscrm/22.png)

![Количество сеансов по версиям браузера](./media/app-insights-sample-mscrm/23.png)

#### <a name="geolocation"></a>Географическое положение
![Число сеансов по странам](./media/app-insights-sample-mscrm/24.png)

![Число сеансов и пользователей по странам](./media/app-insights-sample-mscrm/25.png)

#### <a name="inside-page-view-request"></a>Запрос на просмотр внутренней страницы
![Сводка по просмотрам страницы](./media/app-insights-sample-mscrm/26.png)

![Поиск событий просмотра страницы](./media/app-insights-sample-mscrm/27.png)

![Похожие просмотры страниц](./media/app-insights-sample-mscrm/28.png)

![Свойства просмотра страниц](./media/app-insights-sample-mscrm/29.png)

![Страницы по сеансам](./media/app-insights-sample-mscrm/30.png)

## <a name="sample-code"></a>Пример кода
[Просмотр образца кода hello](https://dynamicsandappinsights.codeplex.com/).

## <a name="power-bi"></a>Power BI
Это можно сделать еще более глубокого анализа, если вы [Экспорт данных hello tooMicrosoft Power BI](app-insights-export-power-bi.md).

## <a name="sample-microsoft-dynamics-crm-solution"></a>Образец решения Microsoft Dynamics CRM
[Ниже приведен образец решения hello, реализованные в Microsoft Dynamics CRM](https://dynamicsandappinsights.codeplex.com/).

## <a name="learn-more"></a>Подробнее
* [Что такое Azure Application Insights?](app-insights-overview.md)
* [Application Insights для веб-страниц](app-insights-javascript.md)
* [Дополнительные примеры и пошаговые руководства](app-insights-code-samples.md)
