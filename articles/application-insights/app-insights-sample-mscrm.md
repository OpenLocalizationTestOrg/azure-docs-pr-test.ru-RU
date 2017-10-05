---
title: "Microsoft Dynamics CRM и Azure Application Insights | Документация Майкрософт"
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
ms.openlocfilehash: a9593d5f198e05db80451a599428a296ed02e781
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="walkthrough-enabling-telemetry-for-microsoft-dynamics-crm-online-using-application-insights"></a><span data-ttu-id="255e0-104">Пошаговое руководство. Включение телеметрии для Microsoft Dynamics CRM Online с помощью Application Insights</span><span class="sxs-lookup"><span data-stu-id="255e0-104">Walkthrough: Enabling Telemetry for Microsoft Dynamics CRM Online using Application Insights</span></span>
<span data-ttu-id="255e0-105">В этой статье показано, как получить данные телеметрии из службы [Microsoft Dynamics CRM Online](https://www.dynamics.com/) с помощью [Azure Application Insights](https://azure.microsoft.com/services/application-insights/).</span><span class="sxs-lookup"><span data-stu-id="255e0-105">This article shows you how to get telemetry data from [Microsoft Dynamics CRM Online](https://www.dynamics.com/) using [Azure Application Insights](https://azure.microsoft.com/services/application-insights/).</span></span> <span data-ttu-id="255e0-106">Мы рассмотрим весь процесс добавления сценария Application Insights в приложение, сбор данных и их визуализацию.</span><span class="sxs-lookup"><span data-stu-id="255e0-106">We’ll walk through the complete process of adding Application Insights script to your application, capturing data, and data visualization.</span></span>

> [!NOTE]
> <span data-ttu-id="255e0-107">[Получите пример решения.](https://dynamicsandappinsights.codeplex.com/)</span><span class="sxs-lookup"><span data-stu-id="255e0-107">[Browse the sample solution](https://dynamicsandappinsights.codeplex.com/).</span></span>
> 
> 

## <a name="add-application-insights-to-new-or-existing-crm-online-instance"></a><span data-ttu-id="255e0-108">Добавление Application Insights в новый или существующий экземпляр CRM Online</span><span class="sxs-lookup"><span data-stu-id="255e0-108">Add Application Insights to new or existing CRM Online instance</span></span>
<span data-ttu-id="255e0-109">Чтобы отслеживать работу приложения, добавьте в него пакет SDK для Application Insights.</span><span class="sxs-lookup"><span data-stu-id="255e0-109">To monitor your application, you add an Application Insights SDK to your application.</span></span> <span data-ttu-id="255e0-110">Пакет SDK отправляет данные телеметрии на [портал Application Insights](https://portal.azure.com), где вы можете использовать наши эффективные инструменты анализа и диагностики, а также экспортировать данные в хранилище.</span><span class="sxs-lookup"><span data-stu-id="255e0-110">The SDK sends telemetry to the [Application Insights portal](https://portal.azure.com), where you can use our powerful analysis and diagnostic tools, or export the data to storage.</span></span>

### <a name="create-an-application-insights-resource-in-azure"></a><span data-ttu-id="255e0-111">Создание ресурса Application Insights в Azure</span><span class="sxs-lookup"><span data-stu-id="255e0-111">Create an Application Insights resource in Azure</span></span>
1. <span data-ttu-id="255e0-112">Получите [учетную запись Microsoft Azure](http://azure.com/pricing).</span><span class="sxs-lookup"><span data-stu-id="255e0-112">Get [an account in Microsoft Azure](http://azure.com/pricing).</span></span> 
2. <span data-ttu-id="255e0-113">Войдите на [портал Azure](https://portal.azure.com) и добавьте новый ресурс Application Insights.</span><span class="sxs-lookup"><span data-stu-id="255e0-113">Sign into the [Azure portal](https://portal.azure.com) and add a new Application Insights resource.</span></span> <span data-ttu-id="255e0-114">Здесь будут обрабатываться и отображаться ваши данные.</span><span class="sxs-lookup"><span data-stu-id="255e0-114">This is where your data will be processed and displayed.</span></span>
   
    ![Щелкните значок «+» и последовательно выберите «Службы для разработчиков», Application Insights.](./media/app-insights-sample-mscrm/01.png)
   
    <span data-ttu-id="255e0-116">Выберите приложение ASP.NET в качестве типа приложения.</span><span class="sxs-lookup"><span data-stu-id="255e0-116">Choose ASP.NET as the application type.</span></span>
3. <span data-ttu-id="255e0-117">Откройте страницу "Начало работы", а затем откройте "Мониторинг и диагностика приложения на стороне клиента".</span><span class="sxs-lookup"><span data-stu-id="255e0-117">Open the Getting Started page and open "Monitor and diagnose client side".</span></span>
   
    ![Фрагмент кода для вставки на веб-страницу](./media/app-insights-sample-mscrm/03.png)

<span data-ttu-id="255e0-119">**Не закрывайте страницу с кодом** , выполняя следующий шаг в другом окне браузера.</span><span class="sxs-lookup"><span data-stu-id="255e0-119">**Keep the code page open** while you do the next step in another browser window.</span></span> <span data-ttu-id="255e0-120">Код вскоре вам понадобится.</span><span class="sxs-lookup"><span data-stu-id="255e0-120">You'll need the code soon.</span></span> 

### <a name="create-a-javascript-web-resource-in-microsoft-dynamics-crm"></a><span data-ttu-id="255e0-121">Создание веб-ресурса JavaScript в Microsoft Dynamics CRM</span><span class="sxs-lookup"><span data-stu-id="255e0-121">Create a JavaScript web resource in Microsoft Dynamics CRM</span></span>
1. <span data-ttu-id="255e0-122">Откройте экземпляр CRM Online и войдите с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="255e0-122">Open your CRM Online instance and login with administrator privileges.</span></span>
2. <span data-ttu-id="255e0-123">Последовательно откройте элементы "Параметры Microsoft Dynamics CRM", "Настройка", "Настройка системы".</span><span class="sxs-lookup"><span data-stu-id="255e0-123">Open Microsoft Dynamics CRM Settings, Customizations, Customize the System</span></span>
   
    ![Параметры Microsoft Dynamics CRM](./media/app-insights-sample-mscrm/04.png)
   
    ![Параметры > Настройки](./media/app-insights-sample-mscrm/05.png)

    ![Настройка параметра системы](./media/app-insights-sample-mscrm/06.png)

1. <span data-ttu-id="255e0-127">Создайте ресурс JavaScript.</span><span class="sxs-lookup"><span data-stu-id="255e0-127">Create a JavaScript resource.</span></span>
   
    ![Диалоговое окно создания веб-ресурса](./media/app-insights-sample-mscrm/07.png)
   
    <span data-ttu-id="255e0-129">Присвойте ему имя, выберите тип **Script (JScript)** и откройте текстовый редактор.</span><span class="sxs-lookup"><span data-stu-id="255e0-129">Give it a name, select **Script (JScript)** and open the text editor.</span></span>
   
    ![Откройте текстовый редактор](./media/app-insights-sample-mscrm/08.png)
2. <span data-ttu-id="255e0-131">Скопируйте код из Application Insights.</span><span class="sxs-lookup"><span data-stu-id="255e0-131">Copy the code from Application Insights.</span></span> <span data-ttu-id="255e0-132">При копировании необходимо пропускать теги скриптов.</span><span class="sxs-lookup"><span data-stu-id="255e0-132">While copying make sure to ignore script tags.</span></span> <span data-ttu-id="255e0-133">См. ниже снимок экрана.</span><span class="sxs-lookup"><span data-stu-id="255e0-133">Refer below screenshot:</span></span>
   
    ![Задайте ключ инструментирования](./media/app-insights-sample-mscrm/09.png)
   
    <span data-ttu-id="255e0-135">Код содержит ключ инструментирования, который идентифицирует ресурс Application Insights.</span><span class="sxs-lookup"><span data-stu-id="255e0-135">The code includes the instrumentation key that identifies your Application insights resource.</span></span>
3. <span data-ttu-id="255e0-136">Щелкните «Сохранить», а затем «Опубликовать».</span><span class="sxs-lookup"><span data-stu-id="255e0-136">Save and publish.</span></span>
   
    ![Сохранение и публикация](./media/app-insights-sample-mscrm/10.png)

### <a name="instrument-forms"></a><span data-ttu-id="255e0-138">Формы инструментов</span><span class="sxs-lookup"><span data-stu-id="255e0-138">Instrument Forms</span></span>
1. <span data-ttu-id="255e0-139">В Microsoft CRM Online откройте форму «Учетная запись».</span><span class="sxs-lookup"><span data-stu-id="255e0-139">In Microsoft CRM Online, open the Account form</span></span>
   
    ![Форма учетной записи](./media/app-insights-sample-mscrm/11.png)
2. <span data-ttu-id="255e0-141">Откройте свойства формы.</span><span class="sxs-lookup"><span data-stu-id="255e0-141">Open the form Properties</span></span>
   
    ![Свойства формы](./media/app-insights-sample-mscrm/12.png)
3. <span data-ttu-id="255e0-143">Добавьте созданный веб-ресурс JavaScript.</span><span class="sxs-lookup"><span data-stu-id="255e0-143">Add the JavaScript web resource that you created</span></span>
   
    ![Меню "Добавить"](./media/app-insights-sample-mscrm/13.png)
   
    ![Добавление веб-ресурса](./media/app-insights-sample-mscrm/14.png)
4. <span data-ttu-id="255e0-146">Сохраните и опубликуйте настройки формы.</span><span class="sxs-lookup"><span data-stu-id="255e0-146">Save and publish your form customizations.</span></span>

## <a name="metrics-captured"></a><span data-ttu-id="255e0-147">Собранные показатели телеметрии</span><span class="sxs-lookup"><span data-stu-id="255e0-147">Metrics captured</span></span>
<span data-ttu-id="255e0-148">Теперь сбор данных телеметрии для формы настроен.</span><span class="sxs-lookup"><span data-stu-id="255e0-148">You have now set up telemetry capture for the form.</span></span> <span data-ttu-id="255e0-149">При каждом использовании данные будут отправляться в ресурс Application Insights.</span><span class="sxs-lookup"><span data-stu-id="255e0-149">Whenever it is used, data will be sent to your Application Insights resource.</span></span>

<span data-ttu-id="255e0-150">Ниже приведены примеры отображаемых данных.</span><span class="sxs-lookup"><span data-stu-id="255e0-150">Here are samples of the data that you'll see.</span></span>

#### <a name="application-health"></a><span data-ttu-id="255e0-151">Работоспособность приложения</span><span class="sxs-lookup"><span data-stu-id="255e0-151">Application health</span></span>
![Время загрузки образца страницы](./media/app-insights-sample-mscrm/15.png)

![Пример диаграммы просмотров страницы](./media/app-insights-sample-mscrm/16.png)

<span data-ttu-id="255e0-154">Исключения браузера:</span><span class="sxs-lookup"><span data-stu-id="255e0-154">Browser exceptions:</span></span>

![Диаграмма "Исключения браузера"](./media/app-insights-sample-mscrm/17.png)

<span data-ttu-id="255e0-156">Щелкните диаграмму, чтобы получить более подробную информацию.</span><span class="sxs-lookup"><span data-stu-id="255e0-156">Click the chart to get more detail:</span></span>

![Список исключений](./media/app-insights-sample-mscrm/18.png)

#### <a name="usage"></a><span data-ttu-id="255e0-158">Использование</span><span class="sxs-lookup"><span data-stu-id="255e0-158">Usage</span></span>
![Представления числа пользователей, сеансов и просмотров страниц](./media/app-insights-sample-mscrm/19.png)

![Диаграммы сеансов](./media/app-insights-sample-mscrm/20.png)

![Версии браузеров](./media/app-insights-sample-mscrm/21.png)

#### <a name="browsers"></a><span data-ttu-id="255e0-162">Браузеры</span><span class="sxs-lookup"><span data-stu-id="255e0-162">Browsers</span></span>
![Разбивка времени загрузки страницы](./media/app-insights-sample-mscrm/22.png)

![Количество сеансов по версиям браузера](./media/app-insights-sample-mscrm/23.png)

#### <a name="geolocation"></a><span data-ttu-id="255e0-165">Географическое положение</span><span class="sxs-lookup"><span data-stu-id="255e0-165">Geolocation</span></span>
![Число сеансов по странам](./media/app-insights-sample-mscrm/24.png)

![Число сеансов и пользователей по странам](./media/app-insights-sample-mscrm/25.png)

#### <a name="inside-page-view-request"></a><span data-ttu-id="255e0-168">Запрос на просмотр внутренней страницы</span><span class="sxs-lookup"><span data-stu-id="255e0-168">Inside page view request</span></span>
![Сводка по просмотрам страницы](./media/app-insights-sample-mscrm/26.png)

![Поиск событий просмотра страницы](./media/app-insights-sample-mscrm/27.png)

![Похожие просмотры страниц](./media/app-insights-sample-mscrm/28.png)

![Свойства просмотра страниц](./media/app-insights-sample-mscrm/29.png)

![Страницы по сеансам](./media/app-insights-sample-mscrm/30.png)

## <a name="sample-code"></a><span data-ttu-id="255e0-174">Пример кода</span><span class="sxs-lookup"><span data-stu-id="255e0-174">Sample code</span></span>
<span data-ttu-id="255e0-175">[Получите пример кода](https://dynamicsandappinsights.codeplex.com/).</span><span class="sxs-lookup"><span data-stu-id="255e0-175">[Browse the sample code](https://dynamicsandappinsights.codeplex.com/).</span></span>

## <a name="power-bi"></a><span data-ttu-id="255e0-176">Power BI</span><span class="sxs-lookup"><span data-stu-id="255e0-176">Power BI</span></span>
<span data-ttu-id="255e0-177">Если [экспортировать данные в Microsoft Power BI](app-insights-export-power-bi.md), то можно выполнить еще более подробный анализ данных.</span><span class="sxs-lookup"><span data-stu-id="255e0-177">You can do even deeper analysis if you [export the data to Microsoft Power BI](app-insights-export-power-bi.md).</span></span>

## <a name="sample-microsoft-dynamics-crm-solution"></a><span data-ttu-id="255e0-178">Образец решения Microsoft Dynamics CRM</span><span class="sxs-lookup"><span data-stu-id="255e0-178">Sample Microsoft Dynamics CRM Solution</span></span>
<span data-ttu-id="255e0-179">[Ниже приведен простой пример решения, реализованного в Microsoft Dynamics CRM](https://dynamicsandappinsights.codeplex.com/).</span><span class="sxs-lookup"><span data-stu-id="255e0-179">[Here is the sample solution implemented in Microsoft Dynamics CRM](https://dynamicsandappinsights.codeplex.com/).</span></span>

## <a name="learn-more"></a><span data-ttu-id="255e0-180">Подробнее</span><span class="sxs-lookup"><span data-stu-id="255e0-180">Learn more</span></span>
* [<span data-ttu-id="255e0-181">Что такое Azure Application Insights?</span><span class="sxs-lookup"><span data-stu-id="255e0-181">What is Application Insights?</span></span>](app-insights-overview.md)
* [<span data-ttu-id="255e0-182">Application Insights для веб-страниц</span><span class="sxs-lookup"><span data-stu-id="255e0-182">Application Insights for web pages</span></span>](app-insights-javascript.md)
* [<span data-ttu-id="255e0-183">Дополнительные примеры и пошаговые руководства</span><span class="sxs-lookup"><span data-stu-id="255e0-183">More samples and walkthroughs</span></span>](app-insights-code-samples.md)
