---
title: "Автоматизация процессов Azure Application Insights с помощью Logic Apps."
description: "Узнайте, как можно быстро автоматизировать повторяющиеся процессы, добавив соединитель Application Insights в приложение логики."
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
ms.openlocfilehash: 36df5bc0a019f4197d40fd6fa5a2a9957820c8b4
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="automate-application-insights-processes-by-using-logic-apps"></a><span data-ttu-id="a50bb-103">Автоматизация процессов Application Insights с помощью Logic Apps</span><span class="sxs-lookup"><span data-stu-id="a50bb-103">Automate Application Insights processes by using Logic Apps</span></span>

<span data-ttu-id="a50bb-104">Постоянно выполняете одинаковые запросы к данным телеметрии, чтобы проверить, что ваша служба работает правильно?</span><span class="sxs-lookup"><span data-stu-id="a50bb-104">Do you find yourself repeatedly running the same queries on your telemetry data to check whether your service is functioning properly?</span></span> <span data-ttu-id="a50bb-105">Хотите автоматизировать эти запросы для поиска тенденций и аномалий и создавать на их основе собственные рабочие процессы?</span><span class="sxs-lookup"><span data-stu-id="a50bb-105">Are you looking to automate these queries for finding trends and anomalies and then build your own workflows around them?</span></span> <span data-ttu-id="a50bb-106">Соединитель Application Insights (предварительная версия) для Logic Apps — это то, что вам нужно.</span><span class="sxs-lookup"><span data-stu-id="a50bb-106">The Azure Application Insights connector (preview) for Logic Apps is the right tool for this purpose.</span></span>

<span data-ttu-id="a50bb-107">Благодаря этой интеграции можно автоматизировать множество процессов, не написав ни строчки кода.</span><span class="sxs-lookup"><span data-stu-id="a50bb-107">With this integration, you can automate numerous processes without writing a single line of code.</span></span> <span data-ttu-id="a50bb-108">Можно создать приложение логики с соединителем Application Insights, чтобы быстро автоматизировать любой процесс Application Insights.</span><span class="sxs-lookup"><span data-stu-id="a50bb-108">You can create a logic app with the Application Insights connector to quickly automate any Application Insights process.</span></span> 

<span data-ttu-id="a50bb-109">Вы также можете добавить дополнительные действия.</span><span class="sxs-lookup"><span data-stu-id="a50bb-109">You can add additional actions as well.</span></span> <span data-ttu-id="a50bb-110">Компонент Logic Apps службы приложений Azure предоставляет сотни действий.</span><span class="sxs-lookup"><span data-stu-id="a50bb-110">The Logic Apps feature of Azure App Service makes hundreds of actions available.</span></span> <span data-ttu-id="a50bb-111">Например, вы можете использовать приложение логики, чтобы автоматически отправить уведомление по электронной почте или создать ошибку в Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="a50bb-111">For example, by using a logic app, you can automatically send an email notification or create a bug in Visual Studio Team Services.</span></span> <span data-ttu-id="a50bb-112">Вы можете также воспользоваться одним из множества доступных [шаблонов](https://docs.microsoft.com/azure/logic-apps/logic-apps-use-logic-app-templates). С их помощью можно ускорить процесс создания приложения логики.</span><span class="sxs-lookup"><span data-stu-id="a50bb-112">You can also use one of the many available [templates](https://docs.microsoft.com/azure/logic-apps/logic-apps-use-logic-app-templates) to help speed up the process of creating your logic app.</span></span> 

## <a name="create-a-logic-app-for-application-insights"></a><span data-ttu-id="a50bb-113">Создание приложения логики для Application Insights</span><span class="sxs-lookup"><span data-stu-id="a50bb-113">Create a logic app for Application Insights</span></span>

<span data-ttu-id="a50bb-114">В этом руководстве вы узнаете, как создать приложение логики, использующее алгоритм автоматической кластеризации Analytics, для группирования атрибутов в данных для веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="a50bb-114">In this tutorial, you learn how to create a logic app that uses the Analytics autocluster algorithm to group attributes in the data for a web application.</span></span> <span data-ttu-id="a50bb-115">Отправка результатов по электронной почте — это лишь один из примеров того, как можно совместно использовать Logic Apps и Application Insights Analytics.</span><span class="sxs-lookup"><span data-stu-id="a50bb-115">The flow automatically sends the results by email, just one example of how you can use Application Insights Analytics and Logic Apps together.</span></span> 

### <a name="step-1-create-a-logic-app"></a><span data-ttu-id="a50bb-116">Шаг 1. Создание приложения логики</span><span class="sxs-lookup"><span data-stu-id="a50bb-116">Step 1: Create a logic app</span></span>
1. <span data-ttu-id="a50bb-117">Войдите на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a50bb-117">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="a50bb-118">На панели **Создать** выберите **Интернет+мобильные устройства**, а затем — **Приложение логики**.</span><span class="sxs-lookup"><span data-stu-id="a50bb-118">In the **New** pane, select **Web + Mobile**, and then select **Logic App**.</span></span>

    ![Окно создания приложения логики](./media/automate-with-logic-apps/logicapp1.png)

### <a name="step-2-create-a-trigger-for-your-logic-app"></a><span data-ttu-id="a50bb-120">Шаг 2. Создание триггера для приложения логики</span><span class="sxs-lookup"><span data-stu-id="a50bb-120">Step 2: Create a trigger for your logic app</span></span>
1. <span data-ttu-id="a50bb-121">В окне **конструктора приложений логики** в разделе **Начинаем с часто используемого триггера** выберите **Повторение**.</span><span class="sxs-lookup"><span data-stu-id="a50bb-121">In the **Logic App Designer** window, under **Start with a common trigger**, select **Recurrence**.</span></span>

    ![Окно конструктора приложений логики](./media/automate-with-logic-apps/logicapp2.png)

2. <span data-ttu-id="a50bb-123">В поле **Частота** выберите **День**, а в поле **Интервал** введите **1**.</span><span class="sxs-lookup"><span data-stu-id="a50bb-123">In the **Frequency** box, select **Day** and then, in the **Interval** box, type **1**.</span></span>

    ![Окно "Повторение" в конструкторе приложений логики](./media/automate-with-logic-apps/step2b.png)

### <a name="step-3-add-an-application-insights-action"></a><span data-ttu-id="a50bb-125">Шаг 3. Добавление действия Application Insights</span><span class="sxs-lookup"><span data-stu-id="a50bb-125">Step 3: Add an Application Insights action</span></span>
1. <span data-ttu-id="a50bb-126">Выберите поле **+Новый шаг**, а затем щелкните **Добавить действие**.</span><span class="sxs-lookup"><span data-stu-id="a50bb-126">Click **New step**, and then click **Add an action**.</span></span>

2. <span data-ttu-id="a50bb-127">В поле поиска **Выберите действие** введите **Azure Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="a50bb-127">In the **Choose an action** search box, type **Azure Application Insights**.</span></span>

3. <span data-ttu-id="a50bb-128">В разделе **Действия** выберите **Azure Application Insights – Visualize Analytics query Preview** (Azure Application Insights — визуализация запроса Analytics [предварительная версия]).</span><span class="sxs-lookup"><span data-stu-id="a50bb-128">Under **Actions**, click **Azure Application Insights – Visualize Analytics query Preview**.</span></span>

    ![Окно "Выберите действие" в конструкторе приложений логики](./media/automate-with-logic-apps/flow2.png)

### <a name="step-4-connect-to-an-application-insights-resource"></a><span data-ttu-id="a50bb-130">Шаг 4. Подключение к ресурсу Application Insights</span><span class="sxs-lookup"><span data-stu-id="a50bb-130">Step 4: Connect to an Application Insights resource</span></span>

<span data-ttu-id="a50bb-131">Чтобы выполнить этот шаг, необходим идентификатор приложения и ключ API для ресурса.</span><span class="sxs-lookup"><span data-stu-id="a50bb-131">To complete this step, you need an application ID and an API key for your resource.</span></span> <span data-ttu-id="a50bb-132">Их можно получить на портале Azure, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="a50bb-132">You can retrieve them from the Azure portal, as shown in the following diagram:</span></span>

![Идентификатор приложения на портале Azure](./media/automate-with-logic-apps/appid.png) 

<span data-ttu-id="a50bb-134">Укажите имя подключения, а также идентификатор приложения и ключ API.</span><span class="sxs-lookup"><span data-stu-id="a50bb-134">Provide a name for your connection, the application ID, and the API key.</span></span>

![Окно подключения последовательности в конструкторе приложений логики](./media/automate-with-logic-apps/flow3.png)

### <a name="step-5-specify-the-analytics-query-and-chart-type"></a><span data-ttu-id="a50bb-136">Шаг 5. Указание запроса Analytics и типа диаграммы</span><span class="sxs-lookup"><span data-stu-id="a50bb-136">Step 5: Specify the Analytics query and chart type</span></span>
<span data-ttu-id="a50bb-137">В следующем примере выбираются невыполненные запросы за последний день. Они сопоставляются с исключениями, которые возникли в рамках операции.</span><span class="sxs-lookup"><span data-stu-id="a50bb-137">In the following example, the query selects the failed requests within the last day and correlates them with exceptions that occurred as part of the operation.</span></span> <span data-ttu-id="a50bb-138">Analytics сопоставляет такие запросы на основе идентификатора operation_Id.</span><span class="sxs-lookup"><span data-stu-id="a50bb-138">Analytics correlates the failed requests, based on the operation_Id identifier.</span></span> <span data-ttu-id="a50bb-139">Затем запрос разделяет результаты с помощью алгоритма автоматической кластеризации.</span><span class="sxs-lookup"><span data-stu-id="a50bb-139">The query then segments the results by using the autocluster algorithm.</span></span> 

<span data-ttu-id="a50bb-140">При создании собственных запросов убедитесь, что они работают должным образом в Analytics, прежде чем добавить их в последовательность.</span><span class="sxs-lookup"><span data-stu-id="a50bb-140">When you create your own queries, verify that they are working properly in Analytics before you add it to your flow.</span></span>

1. <span data-ttu-id="a50bb-141">В поле **Запрос** добавьте следующий запрос Analytics:</span><span class="sxs-lookup"><span data-stu-id="a50bb-141">In the **Query** box, add the following Analytics query:</span></span> 

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

2. <span data-ttu-id="a50bb-142">В поле **Тип диаграммы** выберите **Таблица HTML**.</span><span class="sxs-lookup"><span data-stu-id="a50bb-142">In the **Chart Type** box, select **Html Table**.</span></span>

    ![Окно настройки запроса Analytics](./media/automate-with-logic-apps/flow4.png)

### <a name="step-6-configure-the-logic-app-to-send-email"></a><span data-ttu-id="a50bb-144">Шаг 6. Настройка приложения логики для отправки сообщения электронной почты</span><span class="sxs-lookup"><span data-stu-id="a50bb-144">Step 6: Configure the logic app to send email</span></span>

1. <span data-ttu-id="a50bb-145">Щелкните **Новый шаг**, а затем — **Добавить действие**.</span><span class="sxs-lookup"><span data-stu-id="a50bb-145">Click **New step**, and then select **Add an action**.</span></span>

2. <span data-ttu-id="a50bb-146">В поле поиска введите **Office 365 Outlook**.</span><span class="sxs-lookup"><span data-stu-id="a50bb-146">In the search box, type **Office 365 Outlook**.</span></span>

3. <span data-ttu-id="a50bb-147">Щелкните **Office 365 Outlook – Send an email** (Office 365 Outlook — отправка сообщения электронной почты).</span><span class="sxs-lookup"><span data-stu-id="a50bb-147">Click **Office 365 Outlook – Send an email**.</span></span>

    ![Выбор Office 365 Outlook](./media/automate-with-logic-apps/flow2b.png)

4. <span data-ttu-id="a50bb-149">В окне **Отправка сообщения электронной почты** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="a50bb-149">In the **Send an email** window, do the following:</span></span>

   <span data-ttu-id="a50bb-150">а.</span><span class="sxs-lookup"><span data-stu-id="a50bb-150">a.</span></span> <span data-ttu-id="a50bb-151">Введите адрес электронной почты получателя.</span><span class="sxs-lookup"><span data-stu-id="a50bb-151">Type the email address of the recipient.</span></span>

   <span data-ttu-id="a50bb-152">b.</span><span class="sxs-lookup"><span data-stu-id="a50bb-152">b.</span></span> <span data-ttu-id="a50bb-153">Введите тему сообщения.</span><span class="sxs-lookup"><span data-stu-id="a50bb-153">Type a subject for the email.</span></span>

   <span data-ttu-id="a50bb-154">c.</span><span class="sxs-lookup"><span data-stu-id="a50bb-154">c.</span></span> <span data-ttu-id="a50bb-155">Щелкните в любом месте в поле **Текст**, затем в открывшемся справа меню динамического содержимого выберите **Текст**.</span><span class="sxs-lookup"><span data-stu-id="a50bb-155">Click anywhere in the **Body** box and then, on the dynamic content menu that opens at the right, select **Body**.</span></span>

   <span data-ttu-id="a50bb-156">г)</span><span class="sxs-lookup"><span data-stu-id="a50bb-156">d.</span></span> <span data-ttu-id="a50bb-157">Щелкните **Показать дополнительные параметры**.</span><span class="sxs-lookup"><span data-stu-id="a50bb-157">Click **Show advanced options**.</span></span>

      ![Конфигурация Office 365 Outlook](./media/automate-with-logic-apps/flow5.png)

5. <span data-ttu-id="a50bb-159">В меню динамического содержимого выполните следующее.</span><span class="sxs-lookup"><span data-stu-id="a50bb-159">On the dynamic content menu, do the following:</span></span>

    <span data-ttu-id="a50bb-160">а.</span><span class="sxs-lookup"><span data-stu-id="a50bb-160">a.</span></span> <span data-ttu-id="a50bb-161">Выберите **Имя вложения**.</span><span class="sxs-lookup"><span data-stu-id="a50bb-161">Select **Attachment Name**.</span></span>

    <span data-ttu-id="a50bb-162">b.</span><span class="sxs-lookup"><span data-stu-id="a50bb-162">b.</span></span> <span data-ttu-id="a50bb-163">Выберите **Содержимое вложения**.</span><span class="sxs-lookup"><span data-stu-id="a50bb-163">Select **Attachment Content**.</span></span>
    
    <span data-ttu-id="a50bb-164">c.</span><span class="sxs-lookup"><span data-stu-id="a50bb-164">c.</span></span> <span data-ttu-id="a50bb-165">В поле **Является HTML** выберите значение **Да**.</span><span class="sxs-lookup"><span data-stu-id="a50bb-165">In the **Is HTML** box, select **Yes**.</span></span>

      ![Экран настройки электронного сообщения Office 365](./media/automate-with-logic-apps/flow7.png)

### <a name="step-7-save-and-test-your-logic-app"></a><span data-ttu-id="a50bb-167">Шаг 7. Сохранение и тестирование приложения логики</span><span class="sxs-lookup"><span data-stu-id="a50bb-167">Step 7: Save and test your logic app</span></span>
* <span data-ttu-id="a50bb-168">Нажмите кнопку **Сохранить**, чтобы сохранить изменения.</span><span class="sxs-lookup"><span data-stu-id="a50bb-168">Click **Save** to save your changes.</span></span>

<span data-ttu-id="a50bb-169">Можно либо подождать, пока триггер не запустит приложение логики, либо запустить его немедленно, щелкнув **Запуск**.</span><span class="sxs-lookup"><span data-stu-id="a50bb-169">You can wait for the trigger to run the logic app, or you can run the logic app immediately by selecting **Run**.</span></span>

![Экран создания приложения логики](./media/automate-with-logic-apps/step7.png)

<span data-ttu-id="a50bb-171">При выполнении приложения логики получатели, указанные в списке рассылки, получат сообщение электронной почты, которое выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="a50bb-171">When your logic app runs, the recipients you specified in the email list will receive an email that looks like the following:</span></span>

![Сообщение электронной почты приложения логики](./media/automate-with-logic-apps/flow9.png)

## <a name="next-steps"></a><span data-ttu-id="a50bb-173">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a50bb-173">Next steps</span></span>

- <span data-ttu-id="a50bb-174">Узнайте больше о создании [запросов Analytics](app-insights-analytics-using.md).</span><span class="sxs-lookup"><span data-stu-id="a50bb-174">Learn more about creating [Analytics queries](app-insights-analytics-using.md).</span></span>
- <span data-ttu-id="a50bb-175">Дополнительные сведения о [Logic Apps](https://docs.microsoft.com/azure/logic-apps/logic-apps-what-are-logic-apps).</span><span class="sxs-lookup"><span data-stu-id="a50bb-175">Learn more about [Logic Apps](https://docs.microsoft.com/azure/logic-apps/logic-apps-what-are-logic-apps).</span></span>



<!--Link references-->





