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
# <a name="walkthrough-enabling-telemetry-for-microsoft-dynamics-crm-online-using-application-insights"></a><span data-ttu-id="71f5c-104">Пошаговое руководство. Включение телеметрии для Microsoft Dynamics CRM Online с помощью Application Insights</span><span class="sxs-lookup"><span data-stu-id="71f5c-104">Walkthrough: Enabling Telemetry for Microsoft Dynamics CRM Online using Application Insights</span></span>
<span data-ttu-id="71f5c-105">В этой статье показано, как данные телеметрии tooget из [Microsoft Dynamics CRM Online](https://www.dynamics.com/) с помощью [Azure Application Insights](https://azure.microsoft.com/services/application-insights/).</span><span class="sxs-lookup"><span data-stu-id="71f5c-105">This article shows you how tooget telemetry data from [Microsoft Dynamics CRM Online](https://www.dynamics.com/) using [Azure Application Insights](https://azure.microsoft.com/services/application-insights/).</span></span> <span data-ttu-id="71f5c-106">Мы рассмотрим hello полный процесс добавления приложения tooyour сценария Application Insights, сбора данных и визуализации данных.</span><span class="sxs-lookup"><span data-stu-id="71f5c-106">We’ll walk through hello complete process of adding Application Insights script tooyour application, capturing data, and data visualization.</span></span>

> [!NOTE]
> <span data-ttu-id="71f5c-107">[Обзор решения образца hello](https://dynamicsandappinsights.codeplex.com/).</span><span class="sxs-lookup"><span data-stu-id="71f5c-107">[Browse hello sample solution](https://dynamicsandappinsights.codeplex.com/).</span></span>
> 
> 

## <a name="add-application-insights-toonew-or-existing-crm-online-instance"></a><span data-ttu-id="71f5c-108">Добавить Application Insights toonew или существующего экземпляра CRM Online</span><span class="sxs-lookup"><span data-stu-id="71f5c-108">Add Application Insights toonew or existing CRM Online instance</span></span>
<span data-ttu-id="71f5c-109">toomonitor приложения, добавления приложения tooyour пакет SDK Application Insights.</span><span class="sxs-lookup"><span data-stu-id="71f5c-109">toomonitor your application, you add an Application Insights SDK tooyour application.</span></span> <span data-ttu-id="71f5c-110">Hello SDK отправляет данные телеметрии toohello [портале Application Insights](https://portal.azure.com), где можно использовать наши мощный анализ и средства диагностики, или экспорт данных toostorage hello.</span><span class="sxs-lookup"><span data-stu-id="71f5c-110">hello SDK sends telemetry toohello [Application Insights portal](https://portal.azure.com), where you can use our powerful analysis and diagnostic tools, or export hello data toostorage.</span></span>

### <a name="create-an-application-insights-resource-in-azure"></a><span data-ttu-id="71f5c-111">Создание ресурса Application Insights в Azure</span><span class="sxs-lookup"><span data-stu-id="71f5c-111">Create an Application Insights resource in Azure</span></span>
1. <span data-ttu-id="71f5c-112">Получите [учетную запись Microsoft Azure](http://azure.com/pricing).</span><span class="sxs-lookup"><span data-stu-id="71f5c-112">Get [an account in Microsoft Azure](http://azure.com/pricing).</span></span> 
2. <span data-ttu-id="71f5c-113">Вход в hello [портал Azure](https://portal.azure.com) и добавить новый ресурс Application Insights.</span><span class="sxs-lookup"><span data-stu-id="71f5c-113">Sign into hello [Azure portal](https://portal.azure.com) and add a new Application Insights resource.</span></span> <span data-ttu-id="71f5c-114">Здесь будут обрабатываться и отображаться ваши данные.</span><span class="sxs-lookup"><span data-stu-id="71f5c-114">This is where your data will be processed and displayed.</span></span>
   
    ![Щелкните значок «+» и последовательно выберите «Службы для разработчиков», Application Insights.](./media/app-insights-sample-mscrm/01.png)
   
    <span data-ttu-id="71f5c-116">Выберите в качестве типа приложения hello ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="71f5c-116">Choose ASP.NET as hello application type.</span></span>
3. <span data-ttu-id="71f5c-117">Открытие страницы «hello Приступая к работе» и откройте «монитор и диагностики на стороне клиента».</span><span class="sxs-lookup"><span data-stu-id="71f5c-117">Open hello Getting Started page and open "Monitor and diagnose client side".</span></span>
   
    ![Фрагмент кода для вставки на веб-страницу](./media/app-insights-sample-mscrm/03.png)

<span data-ttu-id="71f5c-119">**Не закрывайте hello кодовая страница** пока hello следующим шагом в другом окне браузера.</span><span class="sxs-lookup"><span data-stu-id="71f5c-119">**Keep hello code page open** while you do hello next step in another browser window.</span></span> <span data-ttu-id="71f5c-120">Вам потребуется скоро кода hello.</span><span class="sxs-lookup"><span data-stu-id="71f5c-120">You'll need hello code soon.</span></span> 

### <a name="create-a-javascript-web-resource-in-microsoft-dynamics-crm"></a><span data-ttu-id="71f5c-121">Создание веб-ресурса JavaScript в Microsoft Dynamics CRM</span><span class="sxs-lookup"><span data-stu-id="71f5c-121">Create a JavaScript web resource in Microsoft Dynamics CRM</span></span>
1. <span data-ttu-id="71f5c-122">Откройте экземпляр CRM Online и войдите с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="71f5c-122">Open your CRM Online instance and login with administrator privileges.</span></span>
2. <span data-ttu-id="71f5c-123">Откройте Microsoft Dynamics CRM параметры настройки, hello Настройка системы</span><span class="sxs-lookup"><span data-stu-id="71f5c-123">Open Microsoft Dynamics CRM Settings, Customizations, Customize hello System</span></span>
   
    ![Параметры Microsoft Dynamics CRM](./media/app-insights-sample-mscrm/04.png)
   
    ![Параметры > Настройки](./media/app-insights-sample-mscrm/05.png)

    ![Настроить параметр системного hello](./media/app-insights-sample-mscrm/06.png)

1. <span data-ttu-id="71f5c-127">Создайте ресурс JavaScript.</span><span class="sxs-lookup"><span data-stu-id="71f5c-127">Create a JavaScript resource.</span></span>
   
    ![Диалоговое окно создания веб-ресурса](./media/app-insights-sample-mscrm/07.png)
   
    <span data-ttu-id="71f5c-129">Присвойте ему имя, выберите **сценария (JScript)** и hello откройте текстовый редактор.</span><span class="sxs-lookup"><span data-stu-id="71f5c-129">Give it a name, select **Script (JScript)** and open hello text editor.</span></span>
   
    ![Привет открыть текстовый редактор](./media/app-insights-sample-mscrm/08.png)
2. <span data-ttu-id="71f5c-131">Скопируйте код hello из Application Insights.</span><span class="sxs-lookup"><span data-stu-id="71f5c-131">Copy hello code from Application Insights.</span></span> <span data-ttu-id="71f5c-132">При копировании убедитесь, что tooignore теги сценариев.</span><span class="sxs-lookup"><span data-stu-id="71f5c-132">While copying make sure tooignore script tags.</span></span> <span data-ttu-id="71f5c-133">См. ниже снимок экрана.</span><span class="sxs-lookup"><span data-stu-id="71f5c-133">Refer below screenshot:</span></span>
   
    ![Задайте ключ инструментирования](./media/app-insights-sample-mscrm/09.png)
   
    <span data-ttu-id="71f5c-135">Код Hello содержит ключ инструментирования hello, идентифицирующее ваш ресурс Application insights.</span><span class="sxs-lookup"><span data-stu-id="71f5c-135">hello code includes hello instrumentation key that identifies your Application insights resource.</span></span>
3. <span data-ttu-id="71f5c-136">Щелкните «Сохранить», а затем «Опубликовать».</span><span class="sxs-lookup"><span data-stu-id="71f5c-136">Save and publish.</span></span>
   
    ![Сохранение и публикация](./media/app-insights-sample-mscrm/10.png)

### <a name="instrument-forms"></a><span data-ttu-id="71f5c-138">Формы инструментов</span><span class="sxs-lookup"><span data-stu-id="71f5c-138">Instrument Forms</span></span>
1. <span data-ttu-id="71f5c-139">В Microsoft CRM Online откройте форму hello учетной записи</span><span class="sxs-lookup"><span data-stu-id="71f5c-139">In Microsoft CRM Online, open hello Account form</span></span>
   
    ![Форма учетной записи](./media/app-insights-sample-mscrm/11.png)
2. <span data-ttu-id="71f5c-141">Откройте форму hello свойства</span><span class="sxs-lookup"><span data-stu-id="71f5c-141">Open hello form Properties</span></span>
   
    ![Свойства формы](./media/app-insights-sample-mscrm/12.png)
3. <span data-ttu-id="71f5c-143">Добавить hello JavaScript веб-ресурса, который вы создали</span><span class="sxs-lookup"><span data-stu-id="71f5c-143">Add hello JavaScript web resource that you created</span></span>
   
    ![Меню "Добавить"](./media/app-insights-sample-mscrm/13.png)
   
    ![Добавить веб-ресурс hello](./media/app-insights-sample-mscrm/14.png)
4. <span data-ttu-id="71f5c-146">Сохраните и опубликуйте настройки формы.</span><span class="sxs-lookup"><span data-stu-id="71f5c-146">Save and publish your form customizations.</span></span>

## <a name="metrics-captured"></a><span data-ttu-id="71f5c-147">Собранные показатели телеметрии</span><span class="sxs-lookup"><span data-stu-id="71f5c-147">Metrics captured</span></span>
<span data-ttu-id="71f5c-148">Теперь вы настроили сбор данных телеметрии для hello формы.</span><span class="sxs-lookup"><span data-stu-id="71f5c-148">You have now set up telemetry capture for hello form.</span></span> <span data-ttu-id="71f5c-149">Каждый раз, когда он используется, данные будут отправлены tooyour ресурс Application Insights.</span><span class="sxs-lookup"><span data-stu-id="71f5c-149">Whenever it is used, data will be sent tooyour Application Insights resource.</span></span>

<span data-ttu-id="71f5c-150">Ниже приведены примеры данных hello, вы увидите.</span><span class="sxs-lookup"><span data-stu-id="71f5c-150">Here are samples of hello data that you'll see.</span></span>

#### <a name="application-health"></a><span data-ttu-id="71f5c-151">Работоспособность приложения</span><span class="sxs-lookup"><span data-stu-id="71f5c-151">Application health</span></span>
![Время загрузки образца страницы](./media/app-insights-sample-mscrm/15.png)

![Пример диаграммы просмотров страницы](./media/app-insights-sample-mscrm/16.png)

<span data-ttu-id="71f5c-154">Исключения браузера:</span><span class="sxs-lookup"><span data-stu-id="71f5c-154">Browser exceptions:</span></span>

![Диаграмма "Исключения браузера"](./media/app-insights-sample-mscrm/17.png)

<span data-ttu-id="71f5c-156">Щелкните диаграмму tooget hello более подробно:</span><span class="sxs-lookup"><span data-stu-id="71f5c-156">Click hello chart tooget more detail:</span></span>

![Список исключений](./media/app-insights-sample-mscrm/18.png)

#### <a name="usage"></a><span data-ttu-id="71f5c-158">Использование</span><span class="sxs-lookup"><span data-stu-id="71f5c-158">Usage</span></span>
![Представления числа пользователей, сеансов и просмотров страниц](./media/app-insights-sample-mscrm/19.png)

![Диаграммы сеансов](./media/app-insights-sample-mscrm/20.png)

![Версии браузеров](./media/app-insights-sample-mscrm/21.png)

#### <a name="browsers"></a><span data-ttu-id="71f5c-162">Браузеры</span><span class="sxs-lookup"><span data-stu-id="71f5c-162">Browsers</span></span>
![Разбивка времени загрузки страницы](./media/app-insights-sample-mscrm/22.png)

![Количество сеансов по версиям браузера](./media/app-insights-sample-mscrm/23.png)

#### <a name="geolocation"></a><span data-ttu-id="71f5c-165">Географическое положение</span><span class="sxs-lookup"><span data-stu-id="71f5c-165">Geolocation</span></span>
![Число сеансов по странам](./media/app-insights-sample-mscrm/24.png)

![Число сеансов и пользователей по странам](./media/app-insights-sample-mscrm/25.png)

#### <a name="inside-page-view-request"></a><span data-ttu-id="71f5c-168">Запрос на просмотр внутренней страницы</span><span class="sxs-lookup"><span data-stu-id="71f5c-168">Inside page view request</span></span>
![Сводка по просмотрам страницы](./media/app-insights-sample-mscrm/26.png)

![Поиск событий просмотра страницы](./media/app-insights-sample-mscrm/27.png)

![Похожие просмотры страниц](./media/app-insights-sample-mscrm/28.png)

![Свойства просмотра страниц](./media/app-insights-sample-mscrm/29.png)

![Страницы по сеансам](./media/app-insights-sample-mscrm/30.png)

## <a name="sample-code"></a><span data-ttu-id="71f5c-174">Пример кода</span><span class="sxs-lookup"><span data-stu-id="71f5c-174">Sample code</span></span>
<span data-ttu-id="71f5c-175">[Просмотр образца кода hello](https://dynamicsandappinsights.codeplex.com/).</span><span class="sxs-lookup"><span data-stu-id="71f5c-175">[Browse hello sample code](https://dynamicsandappinsights.codeplex.com/).</span></span>

## <a name="power-bi"></a><span data-ttu-id="71f5c-176">Power BI</span><span class="sxs-lookup"><span data-stu-id="71f5c-176">Power BI</span></span>
<span data-ttu-id="71f5c-177">Это можно сделать еще более глубокого анализа, если вы [Экспорт данных hello tooMicrosoft Power BI](app-insights-export-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="71f5c-177">You can do even deeper analysis if you [export hello data tooMicrosoft Power BI](app-insights-export-power-bi.md).</span></span>

## <a name="sample-microsoft-dynamics-crm-solution"></a><span data-ttu-id="71f5c-178">Образец решения Microsoft Dynamics CRM</span><span class="sxs-lookup"><span data-stu-id="71f5c-178">Sample Microsoft Dynamics CRM Solution</span></span>
<span data-ttu-id="71f5c-179">[Ниже приведен образец решения hello, реализованные в Microsoft Dynamics CRM](https://dynamicsandappinsights.codeplex.com/).</span><span class="sxs-lookup"><span data-stu-id="71f5c-179">[Here is hello sample solution implemented in Microsoft Dynamics CRM](https://dynamicsandappinsights.codeplex.com/).</span></span>

## <a name="learn-more"></a><span data-ttu-id="71f5c-180">Подробнее</span><span class="sxs-lookup"><span data-stu-id="71f5c-180">Learn more</span></span>
* [<span data-ttu-id="71f5c-181">Что такое Azure Application Insights?</span><span class="sxs-lookup"><span data-stu-id="71f5c-181">What is Application Insights?</span></span>](app-insights-overview.md)
* [<span data-ttu-id="71f5c-182">Application Insights для веб-страниц</span><span class="sxs-lookup"><span data-stu-id="71f5c-182">Application Insights for web pages</span></span>](app-insights-javascript.md)
* [<span data-ttu-id="71f5c-183">Дополнительные примеры и пошаговые руководства</span><span class="sxs-lookup"><span data-stu-id="71f5c-183">More samples and walkthroughs</span></span>](app-insights-code-samples.md)
