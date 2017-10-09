---
title: "aaaAutomate аналитики приложения Azure обрабатывает с потоком Microsoft"
description: "Дополнительные сведения об использовании Microsoft Flow tooquickly автоматизации повторяющихся процессов с помощью соединителя hello Application Insights."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 06/25/2017
ms.author: bwren
ms.openlocfilehash: b34488a6b8b8b0a6add960a67f1426cbbbc13552
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="automate-azure-application-insights-processes-with-hello-connector-for-microsoft-flow"></a><span data-ttu-id="7a84a-103">Автоматизации процессов Azure Application Insights с соединителем hello для Microsoft Flow</span><span class="sxs-lookup"><span data-stu-id="7a84a-103">Automate Azure Application Insights processes with hello connector for Microsoft Flow</span></span>

<span data-ttu-id="7a84a-104">Как найти самостоятельно повторяющемся выполнении hello же запросы на вашей toocheck данные телеметрии, что служба работает правильно?</span><span class="sxs-lookup"><span data-stu-id="7a84a-104">Do you find yourself repeatedly running hello same queries on your telemetry data toocheck that your service is functioning properly?</span></span> <span data-ttu-id="7a84a-105">Вид tooautomate эти запросы используются для поиска тренды и аномалии, а затем построить собственные рабочие процессы вокруг них? Соединитель Hello аналитики приложений Azure (Предварительная версия) для Microsoft Flow — hello правильное средство для следующих целей.</span><span class="sxs-lookup"><span data-stu-id="7a84a-105">Are you looking tooautomate these queries for finding trends and anomalies and then build your own workflows around them? hello Azure Application Insights connector (preview) for Microsoft Flow is hello right tool for these purposes.</span></span>

<span data-ttu-id="7a84a-106">Благодаря этой интеграции можно автоматизировать множество процессов, не написав ни строчки кода.</span><span class="sxs-lookup"><span data-stu-id="7a84a-106">With this integration, you can now automate numerous processes without writing a single line of code.</span></span> <span data-ttu-id="7a84a-107">После создания потока с помощью Application Insights действие, hello потока автоматически запускает запрос аналитики аналитики приложений.</span><span class="sxs-lookup"><span data-stu-id="7a84a-107">After you create a flow by using an Application Insights action, hello flow automatically runs your Application Insights Analytics query.</span></span> 

<span data-ttu-id="7a84a-108">Вы также можете добавить дополнительные действия.</span><span class="sxs-lookup"><span data-stu-id="7a84a-108">You can add additional actions as well.</span></span> <span data-ttu-id="7a84a-109">Служба Flow предоставляет сотни действий.</span><span class="sxs-lookup"><span data-stu-id="7a84a-109">Microsoft Flow makes hundreds of actions available.</span></span> <span data-ttu-id="7a84a-110">Например можно использовать Microsoft Flow tooautomatically отправки уведомления по электронной почте или создание ошибки в Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="7a84a-110">For example, you can use Microsoft Flow tooautomatically send an email notification or create a bug in Visual Studio Team Services.</span></span> <span data-ttu-id="7a84a-111">Можно также использовать один из hello многие [шаблоны](https://ms.flow.microsoft.com/en-us/connectors/shared_applicationinsights/?slug=azure-application-insights) , доступных для hello соединитель для потока корпорации Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="7a84a-111">You can also use one of hello many [templates](https://ms.flow.microsoft.com/en-us/connectors/shared_applicationinsights/?slug=azure-application-insights) that are available for hello connector for Microsoft Flow.</span></span> <span data-ttu-id="7a84a-112">Эти шаблоны ускорить процесс создания потока hello.</span><span class="sxs-lookup"><span data-stu-id="7a84a-112">These templates speed up hello process of creating a flow.</span></span> 

<!--hello Application Insights connector also works with [Azure Power Apps](https://powerapps.microsoft.com/en-us/) and [Azure Logic Apps](https://azure.microsoft.com/services/logic-apps/?v=17.23h). --> 

## <a name="create-a-flow-for-application-insights"></a><span data-ttu-id="7a84a-113">Создание последовательности для Application Insights</span><span class="sxs-lookup"><span data-stu-id="7a84a-113">Create a flow for Application Insights</span></span>

<span data-ttu-id="7a84a-114">В этом учебнике вы узнаете, как toocreate поток, который использует hello Analytics кластера автоматически алгоритм toogroup атрибуты в hello данных для веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="7a84a-114">In this tutorial, you will learn how toocreate a flow that uses hello Analytics auto-cluster algorithm toogroup attributes in hello data for a web application.</span></span> <span data-ttu-id="7a84a-115">поток Hello автоматически отправляет результаты hello по электронной почте, лишь один пример того, как можно использовать Microsoft Flow и аналитика аналитики приложений друг с другом.</span><span class="sxs-lookup"><span data-stu-id="7a84a-115">hello flow automatically sends hello results by email, just one example of how you can use Microsoft Flow and Application Insights Analytics together.</span></span> 

### <a name="step-1-create-a-flow"></a><span data-ttu-id="7a84a-116">Шаг 1. Создание последовательности</span><span class="sxs-lookup"><span data-stu-id="7a84a-116">Step 1: Create a flow</span></span>
1. <span data-ttu-id="7a84a-117">Вход слишком[Microsoft Flow](http://flow.microsoft.com)и выберите **Мои потоки**.</span><span class="sxs-lookup"><span data-stu-id="7a84a-117">Sign in too[Microsoft Flow](http://flow.microsoft.com), and then select **My Flows**.</span></span>
2. <span data-ttu-id="7a84a-118">Щелкните **Create a flow from blank** (Создать последовательность с нуля).</span><span class="sxs-lookup"><span data-stu-id="7a84a-118">Click **Create a flow from blank**.</span></span>

### <a name="step-2-create-a-trigger-for-your-flow"></a><span data-ttu-id="7a84a-119">Шаг 2. Создание триггера для последовательности</span><span class="sxs-lookup"><span data-stu-id="7a84a-119">Step 2: Create a trigger for your flow</span></span>
1. <span data-ttu-id="7a84a-120">Выберите **Расписание**, а затем **Расписание — повторение**.</span><span class="sxs-lookup"><span data-stu-id="7a84a-120">Select **Schedule**, and then select **Schedule - Recurrence**.</span></span>
2. <span data-ttu-id="7a84a-121">В hello **частоты** выберите **день**и в hello **интервал** введите **1**.</span><span class="sxs-lookup"><span data-stu-id="7a84a-121">In hello **Frequency** box, select **Day**, and in hello **Interval** box, enter **1**.</span></span>

    ![Диалоговое окно триггера Microsoft Flow](./media/app-insights-automate-with-flow/flow1.png)


### <a name="step-3-add-an-application-insights-action"></a><span data-ttu-id="7a84a-123">Шаг 3. Добавление действия Application Insights</span><span class="sxs-lookup"><span data-stu-id="7a84a-123">Step 3: Add an Application Insights action</span></span>
1. <span data-ttu-id="7a84a-124">Выберите поле **+Новый шаг**, а затем щелкните **Добавить действие**.</span><span class="sxs-lookup"><span data-stu-id="7a84a-124">Click **New step**, and then click **Add an action**.</span></span>
2. <span data-ttu-id="7a84a-125">Выполните поиск по запросу **Azure Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="7a84a-125">Search for **Azure Application Insights**.</span></span>
3. <span data-ttu-id="7a84a-126">Выберите **Azure Application Insights – Visualize Analytics query Preview** (Azure Application Insights — визуализация запроса Analytics [предварительная версия]).</span><span class="sxs-lookup"><span data-stu-id="7a84a-126">Click **Azure Application Insights – Visualize Analytics query Preview**.</span></span>

    ![Окно запуска запроса Analytics](./media/app-insights-automate-with-flow/flow2.png)

### <a name="step-4-connect-tooan-application-insights-resource"></a><span data-ttu-id="7a84a-128">Шаг 4: Подключение tooan ресурс Application Insights</span><span class="sxs-lookup"><span data-stu-id="7a84a-128">Step 4: Connect tooan Application Insights resource</span></span>

<span data-ttu-id="7a84a-129">toocomplete этот шаг требуется для вашего ресурса идентификатора приложения и ключ API.</span><span class="sxs-lookup"><span data-stu-id="7a84a-129">toocomplete this step, you need an application ID and an API key for your resource.</span></span> <span data-ttu-id="7a84a-130">Их можно восстановить из hello портал Azure, как показано в hello, следующая схема:</span><span class="sxs-lookup"><span data-stu-id="7a84a-130">You can retrieve them from hello Azure portal, as shown in hello following diagram:</span></span>

![Идентификатор приложения в hello портал Azure](./media/app-insights-automate-with-flow/appid.png) 

- <span data-ttu-id="7a84a-132">Введите имя для соединения, вместе с hello приложения идентификатор и ключ API.</span><span class="sxs-lookup"><span data-stu-id="7a84a-132">Provide a name for your connection, along with hello application ID and API key.</span></span>

    ![Окно подключения Microsoft Flow](./media/app-insights-automate-with-flow/flow3.png)

### <a name="step-5-specify-hello-analytics-query-and-chart-type"></a><span data-ttu-id="7a84a-134">Шаг 5: Укажите hello аналитический запрос и тип диаграммы</span><span class="sxs-lookup"><span data-stu-id="7a84a-134">Step 5: Specify hello Analytics query and chart type</span></span>
<span data-ttu-id="7a84a-135">Следующий пример запроса выбирает hello сбой запросов в последний день hello и сопоставляет их с исключения, которые возникают в ходе операции hello.</span><span class="sxs-lookup"><span data-stu-id="7a84a-135">This example query selects hello failed requests within hello last day and correlates them with exceptions that occurred as part of hello operation.</span></span> <span data-ttu-id="7a84a-136">Аналитика сопоставляет их на основе идентификатора operation_Id hello.</span><span class="sxs-lookup"><span data-stu-id="7a84a-136">Analytics correlates them based on hello operation_Id identifier.</span></span> <span data-ttu-id="7a84a-137">Затем запрос Hello сегменты hello результаты с помощью алгоритма autocluster hello.</span><span class="sxs-lookup"><span data-stu-id="7a84a-137">hello query then segments hello results by using hello autocluster algorithm.</span></span> 

<span data-ttu-id="7a84a-138">При создании собственных запросов, убедитесь, что они работают надлежащим образом в Analytics перед его добавлением tooyour потока.</span><span class="sxs-lookup"><span data-stu-id="7a84a-138">When you create your own queries, verify that they are working properly in Analytics before you add it tooyour flow.</span></span>

- <span data-ttu-id="7a84a-139">Добавьте hello в следующем запросе аналитика и выберите тип диаграммы таблицы HTML hello.</span><span class="sxs-lookup"><span data-stu-id="7a84a-139">Add hello following Analytics query, and then select hello HTML table chart type.</span></span> 

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
    
    ![Окно настройки запроса Analytics](./media/app-insights-automate-with-flow/flow4.png)

### <a name="step-6-configure-hello-flow-toosend-email"></a><span data-ttu-id="7a84a-141">Шаг 6: Настройка электронной почты toosend потока hello</span><span class="sxs-lookup"><span data-stu-id="7a84a-141">Step 6: Configure hello flow toosend email</span></span>

1. <span data-ttu-id="7a84a-142">Выберите поле **+Новый шаг**, а затем щелкните **Добавить действие**.</span><span class="sxs-lookup"><span data-stu-id="7a84a-142">Click **New step**, and then click **Add an action**.</span></span>
2. <span data-ttu-id="7a84a-143">Выполните поиск по запросу **Office 365 Outlook**.</span><span class="sxs-lookup"><span data-stu-id="7a84a-143">Search for **Office 365 Outlook**.</span></span>
3. <span data-ttu-id="7a84a-144">Щелкните **Office 365 Outlook – Send an email** (Office 365 Outlook — отправка сообщения электронной почты).</span><span class="sxs-lookup"><span data-stu-id="7a84a-144">Click **Office 365 Outlook – Send an email**.</span></span>

    ![Окно выбора Office 365 Outlook](./media/app-insights-automate-with-flow/flow2b.png)

4. <span data-ttu-id="7a84a-146">В hello **отправить сообщение электронной почты** окне hello следующие:</span><span class="sxs-lookup"><span data-stu-id="7a84a-146">In hello **Send an email** window, do hello following:</span></span>

   <span data-ttu-id="7a84a-147">а.</span><span class="sxs-lookup"><span data-stu-id="7a84a-147">a.</span></span> <span data-ttu-id="7a84a-148">Введите адрес электронной почты получателя hello hello.</span><span class="sxs-lookup"><span data-stu-id="7a84a-148">Type hello email address of hello recipient.</span></span>

   <span data-ttu-id="7a84a-149">b.</span><span class="sxs-lookup"><span data-stu-id="7a84a-149">b.</span></span> <span data-ttu-id="7a84a-150">Введите тему сообщения hello.</span><span class="sxs-lookup"><span data-stu-id="7a84a-150">Type a subject for hello email.</span></span>

   <span data-ttu-id="7a84a-151">c.</span><span class="sxs-lookup"><span data-stu-id="7a84a-151">c.</span></span> <span data-ttu-id="7a84a-152">Щелкните в любом месте hello **текст** и меню hello динамического содержимого, открывающееся hello справа выберите **текст**.</span><span class="sxs-lookup"><span data-stu-id="7a84a-152">Click anywhere in hello **Body** box and then, on hello dynamic content menu that opens at hello right, select **Body**.</span></span>

   <span data-ttu-id="7a84a-153">d.</span><span class="sxs-lookup"><span data-stu-id="7a84a-153">d.</span></span> <span data-ttu-id="7a84a-154">Щелкните **Показать дополнительные параметры**.</span><span class="sxs-lookup"><span data-stu-id="7a84a-154">Click **Show advanced options**.</span></span>

    ![Конфигурация Office 365 Outlook](./media/app-insights-automate-with-flow/flow5.png)

5. <span data-ttu-id="7a84a-156">В меню hello динамического содержимого hello следующие:</span><span class="sxs-lookup"><span data-stu-id="7a84a-156">On hello dynamic content menu, do hello following:</span></span>

    <span data-ttu-id="7a84a-157">а.</span><span class="sxs-lookup"><span data-stu-id="7a84a-157">a.</span></span> <span data-ttu-id="7a84a-158">Выберите **Имя вложения**.</span><span class="sxs-lookup"><span data-stu-id="7a84a-158">Select **Attachment Name**.</span></span>

    <span data-ttu-id="7a84a-159">b.</span><span class="sxs-lookup"><span data-stu-id="7a84a-159">b.</span></span> <span data-ttu-id="7a84a-160">Выберите **Содержимое вложения**.</span><span class="sxs-lookup"><span data-stu-id="7a84a-160">Select **Attachment Content**.</span></span>
    
    <span data-ttu-id="7a84a-161">c.</span><span class="sxs-lookup"><span data-stu-id="7a84a-161">c.</span></span> <span data-ttu-id="7a84a-162">В hello **HTML-** выберите **Да**.</span><span class="sxs-lookup"><span data-stu-id="7a84a-162">In hello **Is HTML** box, select **Yes**.</span></span>

    ![Экран настройки сообщения электронной почты Office 365](./media/app-insights-automate-with-flow/flow7.png)

### <a name="step-7-save-and-test-your-flow"></a><span data-ttu-id="7a84a-164">Шаг 7. Сохранение и тестирование последовательности</span><span class="sxs-lookup"><span data-stu-id="7a84a-164">Step 7: Save and test your flow</span></span>
- <span data-ttu-id="7a84a-165">В hello **имя потока** , добавьте имя для вашего потока и нажмите кнопку **создания потока**.</span><span class="sxs-lookup"><span data-stu-id="7a84a-165">In hello **Flow name** box, add a name for your flow, and then click **Create flow**.</span></span>

    ![Окно создания последовательности](./media/app-insights-automate-with-flow/flow8.png)

<span data-ttu-id="7a84a-167">Можно подождать hello триггер toorun это действие или hello потока можно запустить немедленно по [выполнения триггера hello по требованию](https://flow.microsoft.com/blog/run-now-and-six-more-services/).</span><span class="sxs-lookup"><span data-stu-id="7a84a-167">You can wait for hello trigger toorun this action, or you can run hello flow immediately by [running hello trigger on demand](https://flow.microsoft.com/blog/run-now-and-six-more-services/).</span></span>

<span data-ttu-id="7a84a-168">При запуске потока hello hello получатели, заданные в списка по электронной почте hello получать сообщения электронной почты, который выглядит как следующий hello:</span><span class="sxs-lookup"><span data-stu-id="7a84a-168">When hello flow runs, hello recipients you have specified in hello email list receive an email message that looks like hello following:</span></span>

![Пример электронного сообщения](./media/app-insights-automate-with-flow/flow9.png)


## <a name="next-steps"></a><span data-ttu-id="7a84a-170">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7a84a-170">Next steps</span></span>

- <span data-ttu-id="7a84a-171">Узнайте больше о создании [запросов Analytics](app-insights-analytics-using.md).</span><span class="sxs-lookup"><span data-stu-id="7a84a-171">Learn more about creating [Analytics queries](app-insights-analytics-using.md).</span></span>
- <span data-ttu-id="7a84a-172">Дополнительные сведения о [Microsoft Flow](https://ms.flow.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="7a84a-172">Learn more about [Microsoft Flow](https://ms.flow.microsoft.com).</span></span>



<!--Link references-->





