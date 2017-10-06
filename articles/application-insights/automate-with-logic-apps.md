---
title: "aaaAutomate аналитики приложения Azure обрабатывает с помощью приложения логики."
description: "Узнайте, как быстро можно автоматизировать повторяющихся процессов, путем добавления hello Application Insights соединитель tooyour логику приложения."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: bwren
ms.openlocfilehash: 8565aadf0644ffb10da8a0964821901907db2e27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="automate-application-insights-processes-by-using-logic-apps"></a><span data-ttu-id="0ee2f-103">Автоматизация процессов Application Insights с помощью Logic Apps</span><span class="sxs-lookup"><span data-stu-id="0ee2f-103">Automate Application Insights processes by using Logic Apps</span></span>

<span data-ttu-id="0ee2f-104">Как найти самостоятельно многократно выполнение hello же запросов в вашей toocheck данные телеметрии ли служба работает правильно?</span><span class="sxs-lookup"><span data-stu-id="0ee2f-104">Do you find yourself repeatedly running hello same queries on your telemetry data toocheck whether your service is functioning properly?</span></span> <span data-ttu-id="0ee2f-105">Вид tooautomate эти запросы используются для поиска тренды и аномалии, а затем построить собственные рабочие процессы вокруг них? Соединитель Hello аналитики приложений Azure (Предварительная версия) для логики приложений — hello правильное средство для этой цели.</span><span class="sxs-lookup"><span data-stu-id="0ee2f-105">Are you looking tooautomate these queries for finding trends and anomalies and then build your own workflows around them? hello Azure Application Insights connector (preview) for Logic Apps is hello right tool for this purpose.</span></span>

<span data-ttu-id="0ee2f-106">Благодаря этой интеграции можно автоматизировать множество процессов, не написав ни строчки кода.</span><span class="sxs-lookup"><span data-stu-id="0ee2f-106">With this integration, you can automate numerous processes without writing a single line of code.</span></span> <span data-ttu-id="0ee2f-107">Приложения логики можно создать соединитель tooquickly hello Application Insights полностью автоматизировать любой процесс Application Insights.</span><span class="sxs-lookup"><span data-stu-id="0ee2f-107">You can create a logic app with hello Application Insights connector tooquickly automate any Application Insights process.</span></span> 

<span data-ttu-id="0ee2f-108">Вы также можете добавить дополнительные действия.</span><span class="sxs-lookup"><span data-stu-id="0ee2f-108">You can add additional actions as well.</span></span> <span data-ttu-id="0ee2f-109">Hello Logic Apps службы приложения Azure позволяют сотни действия доступны.</span><span class="sxs-lookup"><span data-stu-id="0ee2f-109">hello Logic Apps feature of Azure App Service makes hundreds of actions available.</span></span> <span data-ttu-id="0ee2f-110">Например, вы можете использовать приложение логики, чтобы автоматически отправить уведомление по электронной почте или создать ошибку в Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="0ee2f-110">For example, by using a logic app, you can automatically send an email notification or create a bug in Visual Studio Team Services.</span></span> <span data-ttu-id="0ee2f-111">Можно также использовать один hello многие доступные [шаблоны](https://docs.microsoft.com/azure/logic-apps/logic-apps-use-logic-app-templates) toohelp ускорить процесс создания логики приложения hello.</span><span class="sxs-lookup"><span data-stu-id="0ee2f-111">You can also use one of hello many available [templates](https://docs.microsoft.com/azure/logic-apps/logic-apps-use-logic-app-templates) toohelp speed up hello process of creating your logic app.</span></span> 

## <a name="create-a-logic-app-for-application-insights"></a><span data-ttu-id="0ee2f-112">Создание приложения логики для Application Insights</span><span class="sxs-lookup"><span data-stu-id="0ee2f-112">Create a logic app for Application Insights</span></span>

<span data-ttu-id="0ee2f-113">В этом учебнике вы узнаете, как toocreate логику приложения, в котором используется hello Analytics autocluster алгоритм toogroup атрибуты в hello данных для веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="0ee2f-113">In this tutorial, you learn how toocreate a logic app that uses hello Analytics autocluster algorithm toogroup attributes in hello data for a web application.</span></span> <span data-ttu-id="0ee2f-114">Hello потока автоматически отправляет результаты hello по электронной почте, лишь один пример того, как можно использовать приложения аналитика Analytics и Logic Apps друг с другом.</span><span class="sxs-lookup"><span data-stu-id="0ee2f-114">hello flow automatically sends hello results by email, just one example of how you can use Application Insights Analytics and Logic Apps together.</span></span> 

### <a name="step-1-create-a-logic-app"></a><span data-ttu-id="0ee2f-115">Шаг 1. Создание приложения логики</span><span class="sxs-lookup"><span data-stu-id="0ee2f-115">Step 1: Create a logic app</span></span>
1. <span data-ttu-id="0ee2f-116">Войдите в toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0ee2f-116">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="0ee2f-117">В hello **New** выберите **Интернет + мобильные устройства**, а затем выберите **приложения логики**.</span><span class="sxs-lookup"><span data-stu-id="0ee2f-117">In hello **New** pane, select **Web + Mobile**, and then select **Logic App**.</span></span>

    ![Окно создания приложения логики](./media/automate-with-logic-apps/logicapp1.png)

### <a name="step-2-create-a-trigger-for-your-logic-app"></a><span data-ttu-id="0ee2f-119">Шаг 2. Создание триггера для приложения логики</span><span class="sxs-lookup"><span data-stu-id="0ee2f-119">Step 2: Create a trigger for your logic app</span></span>
1. <span data-ttu-id="0ee2f-120">В hello **конструктор логику приложения** окна в разделе **начинаться с общий триггер**выберите **повторения**.</span><span class="sxs-lookup"><span data-stu-id="0ee2f-120">In hello **Logic App Designer** window, under **Start with a common trigger**, select **Recurrence**.</span></span>

    ![Окно конструктора приложений логики](./media/automate-with-logic-apps/logicapp2.png)

2. <span data-ttu-id="0ee2f-122">В hello **частоты** выберите **день** и затем в hello **интервал** введите **1**.</span><span class="sxs-lookup"><span data-stu-id="0ee2f-122">In hello **Frequency** box, select **Day** and then, in hello **Interval** box, type **1**.</span></span>

    ![Окно "Повторение" в конструкторе приложений логики](./media/automate-with-logic-apps/step2b.png)

### <a name="step-3-add-an-application-insights-action"></a><span data-ttu-id="0ee2f-124">Шаг 3. Добавление действия Application Insights</span><span class="sxs-lookup"><span data-stu-id="0ee2f-124">Step 3: Add an Application Insights action</span></span>
1. <span data-ttu-id="0ee2f-125">Выберите поле **+Новый шаг**, а затем щелкните **Добавить действие**.</span><span class="sxs-lookup"><span data-stu-id="0ee2f-125">Click **New step**, and then click **Add an action**.</span></span>

2. <span data-ttu-id="0ee2f-126">В hello **выбрать действия** поле поиска, введите **Azure Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="0ee2f-126">In hello **Choose an action** search box, type **Azure Application Insights**.</span></span>

3. <span data-ttu-id="0ee2f-127">В разделе **Действия** выберите **Azure Application Insights – Visualize Analytics query Preview** (Azure Application Insights — визуализация запроса Analytics [предварительная версия]).</span><span class="sxs-lookup"><span data-stu-id="0ee2f-127">Under **Actions**, click **Azure Application Insights – Visualize Analytics query Preview**.</span></span>

    ![Окно "Выберите действие" в конструкторе приложений логики](./media/automate-with-logic-apps/flow2.png)

### <a name="step-4-connect-tooan-application-insights-resource"></a><span data-ttu-id="0ee2f-129">Шаг 4: Подключение tooan ресурс Application Insights</span><span class="sxs-lookup"><span data-stu-id="0ee2f-129">Step 4: Connect tooan Application Insights resource</span></span>

<span data-ttu-id="0ee2f-130">toocomplete этот шаг требуется для вашего ресурса идентификатора приложения и ключ API.</span><span class="sxs-lookup"><span data-stu-id="0ee2f-130">toocomplete this step, you need an application ID and an API key for your resource.</span></span> <span data-ttu-id="0ee2f-131">Их можно восстановить из hello портал Azure, как показано в hello, следующая схема:</span><span class="sxs-lookup"><span data-stu-id="0ee2f-131">You can retrieve them from hello Azure portal, as shown in hello following diagram:</span></span>

![Идентификатор приложения в hello портал Azure](./media/automate-with-logic-apps/appid.png) 

<span data-ttu-id="0ee2f-133">Введите имя для соединения, идентификатор приложения hello и ключ API hello.</span><span class="sxs-lookup"><span data-stu-id="0ee2f-133">Provide a name for your connection, hello application ID, and hello API key.</span></span>

![Окно подключения последовательности в конструкторе приложений логики](./media/automate-with-logic-apps/flow3.png)

### <a name="step-5-specify-hello-analytics-query-and-chart-type"></a><span data-ttu-id="0ee2f-135">Шаг 5: Укажите hello аналитический запрос и тип диаграммы</span><span class="sxs-lookup"><span data-stu-id="0ee2f-135">Step 5: Specify hello Analytics query and chart type</span></span>
<span data-ttu-id="0ee2f-136">В следующем примере hello hello запрос выбирает hello сбой запросов в последний день hello и сопоставляет их с исключения, которые возникают в ходе операции hello.</span><span class="sxs-lookup"><span data-stu-id="0ee2f-136">In hello following example, hello query selects hello failed requests within hello last day and correlates them with exceptions that occurred as part of hello operation.</span></span> <span data-ttu-id="0ee2f-137">Аналитика сопоставляет hello не удалось выполнить запросы, исходя из идентификатора operation_Id hello.</span><span class="sxs-lookup"><span data-stu-id="0ee2f-137">Analytics correlates hello failed requests, based on hello operation_Id identifier.</span></span> <span data-ttu-id="0ee2f-138">Затем запрос Hello сегменты hello результаты с помощью алгоритма autocluster hello.</span><span class="sxs-lookup"><span data-stu-id="0ee2f-138">hello query then segments hello results by using hello autocluster algorithm.</span></span> 

<span data-ttu-id="0ee2f-139">При создании собственных запросов, убедитесь, что они работают надлежащим образом в Analytics перед его добавлением tooyour потока.</span><span class="sxs-lookup"><span data-stu-id="0ee2f-139">When you create your own queries, verify that they are working properly in Analytics before you add it tooyour flow.</span></span>

1. <span data-ttu-id="0ee2f-140">В hello **запроса** добавьте hello в следующем запросе аналитика:</span><span class="sxs-lookup"><span data-stu-id="0ee2f-140">In hello **Query** box, add hello following Analytics query:</span></span> 

    ```
    requests
    | where timestamp > ago(1d)
    | where success == "False"
    | project name, operation_Id
    | join ( exceptions
        | project problemId, outerMessage, operation_Id
    ) on operation_Id
    | evaluate autocluster()
    ```

2. <span data-ttu-id="0ee2f-141">В hello **тип диаграммы** выберите **HTML-таблицы**.</span><span class="sxs-lookup"><span data-stu-id="0ee2f-141">In hello **Chart Type** box, select **Html Table**.</span></span>

    ![Окно настройки запроса Analytics](./media/automate-with-logic-apps/flow4.png)

### <a name="step-6-configure-hello-logic-app-toosend-email"></a><span data-ttu-id="0ee2f-143">Шаг 6: Настройка hello логику приложения toosend по электронной почте</span><span class="sxs-lookup"><span data-stu-id="0ee2f-143">Step 6: Configure hello logic app toosend email</span></span>

1. <span data-ttu-id="0ee2f-144">Щелкните **Новый шаг**, а затем — **Добавить действие**.</span><span class="sxs-lookup"><span data-stu-id="0ee2f-144">Click **New step**, and then select **Add an action**.</span></span>

2. <span data-ttu-id="0ee2f-145">Введите в поле поиска hello **Office 365 Outlook**.</span><span class="sxs-lookup"><span data-stu-id="0ee2f-145">In hello search box, type **Office 365 Outlook**.</span></span>

3. <span data-ttu-id="0ee2f-146">Щелкните **Office 365 Outlook – Send an email** (Office 365 Outlook — отправка сообщения электронной почты).</span><span class="sxs-lookup"><span data-stu-id="0ee2f-146">Click **Office 365 Outlook – Send an email**.</span></span>

    ![Выбор Office 365 Outlook](./media/automate-with-logic-apps/flow2b.png)

4. <span data-ttu-id="0ee2f-148">В hello **отправить сообщение электронной почты** окне hello следующие:</span><span class="sxs-lookup"><span data-stu-id="0ee2f-148">In hello **Send an email** window, do hello following:</span></span>

   <span data-ttu-id="0ee2f-149">а.</span><span class="sxs-lookup"><span data-stu-id="0ee2f-149">a.</span></span> <span data-ttu-id="0ee2f-150">Введите адрес электронной почты получателя hello hello.</span><span class="sxs-lookup"><span data-stu-id="0ee2f-150">Type hello email address of hello recipient.</span></span>

   <span data-ttu-id="0ee2f-151">b.</span><span class="sxs-lookup"><span data-stu-id="0ee2f-151">b.</span></span> <span data-ttu-id="0ee2f-152">Введите тему сообщения hello.</span><span class="sxs-lookup"><span data-stu-id="0ee2f-152">Type a subject for hello email.</span></span>

   <span data-ttu-id="0ee2f-153">c.</span><span class="sxs-lookup"><span data-stu-id="0ee2f-153">c.</span></span> <span data-ttu-id="0ee2f-154">Щелкните в любом месте hello **текст** и меню hello динамического содержимого, открывающееся hello справа выберите **текст**.</span><span class="sxs-lookup"><span data-stu-id="0ee2f-154">Click anywhere in hello **Body** box and then, on hello dynamic content menu that opens at hello right, select **Body**.</span></span>

   <span data-ttu-id="0ee2f-155">d.</span><span class="sxs-lookup"><span data-stu-id="0ee2f-155">d.</span></span> <span data-ttu-id="0ee2f-156">Щелкните **Показать дополнительные параметры**.</span><span class="sxs-lookup"><span data-stu-id="0ee2f-156">Click **Show advanced options**.</span></span>

      ![Конфигурация Office 365 Outlook](./media/automate-with-logic-apps/flow5.png)

5. <span data-ttu-id="0ee2f-158">В меню hello динамического содержимого hello следующие:</span><span class="sxs-lookup"><span data-stu-id="0ee2f-158">On hello dynamic content menu, do hello following:</span></span>

    <span data-ttu-id="0ee2f-159">а.</span><span class="sxs-lookup"><span data-stu-id="0ee2f-159">a.</span></span> <span data-ttu-id="0ee2f-160">Выберите **Имя вложения**.</span><span class="sxs-lookup"><span data-stu-id="0ee2f-160">Select **Attachment Name**.</span></span>

    <span data-ttu-id="0ee2f-161">b.</span><span class="sxs-lookup"><span data-stu-id="0ee2f-161">b.</span></span> <span data-ttu-id="0ee2f-162">Выберите **Содержимое вложения**.</span><span class="sxs-lookup"><span data-stu-id="0ee2f-162">Select **Attachment Content**.</span></span>
    
    <span data-ttu-id="0ee2f-163">c.</span><span class="sxs-lookup"><span data-stu-id="0ee2f-163">c.</span></span> <span data-ttu-id="0ee2f-164">В hello **HTML-** выберите **Да**.</span><span class="sxs-lookup"><span data-stu-id="0ee2f-164">In hello **Is HTML** box, select **Yes**.</span></span>

      ![Экран настройки электронного сообщения Office 365](./media/automate-with-logic-apps/flow7.png)

### <a name="step-7-save-and-test-your-logic-app"></a><span data-ttu-id="0ee2f-166">Шаг 7. Сохранение и тестирование приложения логики</span><span class="sxs-lookup"><span data-stu-id="0ee2f-166">Step 7: Save and test your logic app</span></span>
* <span data-ttu-id="0ee2f-167">Нажмите кнопку **Сохранить** toosave изменения.</span><span class="sxs-lookup"><span data-stu-id="0ee2f-167">Click **Save** toosave your changes.</span></span>

<span data-ttu-id="0ee2f-168">Вы можете ожидать hello триггер toorun hello логику приложения или немедленно запустить приложение hello логику, выбрав **запуска**.</span><span class="sxs-lookup"><span data-stu-id="0ee2f-168">You can wait for hello trigger toorun hello logic app, or you can run hello logic app immediately by selecting **Run**.</span></span>

![Экран создания приложения логики](./media/automate-with-logic-apps/step7.png)

<span data-ttu-id="0ee2f-170">При запуске приложения логики hello получателей, указанных в список сообщений электронной почты hello получит сообщение электронной почты, который выглядит как следующий hello:</span><span class="sxs-lookup"><span data-stu-id="0ee2f-170">When your logic app runs, hello recipients you specified in hello email list will receive an email that looks like hello following:</span></span>

![Сообщение электронной почты приложения логики](./media/automate-with-logic-apps/flow9.png)

## <a name="next-steps"></a><span data-ttu-id="0ee2f-172">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0ee2f-172">Next steps</span></span>

- <span data-ttu-id="0ee2f-173">Узнайте больше о создании [запросов Analytics](app-insights-analytics-using.md).</span><span class="sxs-lookup"><span data-stu-id="0ee2f-173">Learn more about creating [Analytics queries](app-insights-analytics-using.md).</span></span>
- <span data-ttu-id="0ee2f-174">Дополнительные сведения о [Logic Apps](https://docs.microsoft.com/azure/logic-apps/logic-apps-what-are-logic-apps).</span><span class="sxs-lookup"><span data-stu-id="0ee2f-174">Learn more about [Logic Apps](https://docs.microsoft.com/azure/logic-apps/logic-apps-what-are-logic-apps).</span></span>



<!--Link references-->





