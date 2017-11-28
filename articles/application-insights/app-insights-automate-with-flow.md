---
title: "Автоматизация процессов Azure Application Insights с помощью Microsoft Flow"
description: "Узнайте, как можно использовать Microsoft Flow для быстрой автоматизации повторяющихся процессов с помощью соединителя Application Insights."
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
ms.openlocfilehash: 510f4f284bbd0dbe4171896899f7ade7dee19e39
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="automate-azure-application-insights-processes-with-the-connector-for-microsoft-flow"></a><span data-ttu-id="4fe5c-103">Автоматизация процессов Azure Application Insights с помощью соединителя для Microsoft Flow</span><span class="sxs-lookup"><span data-stu-id="4fe5c-103">Automate Azure Application Insights processes with the connector for Microsoft Flow</span></span>

<span data-ttu-id="4fe5c-104">Постоянно выполняете одинаковые запросы к данным телеметрии, чтобы проверить, что ваша служба работает правильно?</span><span class="sxs-lookup"><span data-stu-id="4fe5c-104">Do you find yourself repeatedly running the same queries on your telemetry data to check that your service is functioning properly?</span></span> <span data-ttu-id="4fe5c-105">Хотите автоматизировать эти запросы для поиска тенденций и аномалий и создавать на их основе собственные рабочие процессы?</span><span class="sxs-lookup"><span data-stu-id="4fe5c-105">Are you looking to automate these queries for finding trends and anomalies and then build your own workflows around them?</span></span> <span data-ttu-id="4fe5c-106">Соединитель Application Insights (предварительная версия) для Microsoft Flow — это то, что вам нужно.</span><span class="sxs-lookup"><span data-stu-id="4fe5c-106">The Azure Application Insights connector (preview) for Microsoft Flow is the right tool for these purposes.</span></span>

<span data-ttu-id="4fe5c-107">Благодаря этой интеграции можно автоматизировать множество процессов, не написав ни строчки кода.</span><span class="sxs-lookup"><span data-stu-id="4fe5c-107">With this integration, you can now automate numerous processes without writing a single line of code.</span></span> <span data-ttu-id="4fe5c-108">После создания последовательности с помощью действия Application Insights будет автоматически запущен запрос Application Insights Analytics.</span><span class="sxs-lookup"><span data-stu-id="4fe5c-108">After you create a flow by using an Application Insights action, the flow automatically runs your Application Insights Analytics query.</span></span> 

<span data-ttu-id="4fe5c-109">Вы также можете добавить дополнительные действия.</span><span class="sxs-lookup"><span data-stu-id="4fe5c-109">You can add additional actions as well.</span></span> <span data-ttu-id="4fe5c-110">Служба Flow предоставляет сотни действий.</span><span class="sxs-lookup"><span data-stu-id="4fe5c-110">Microsoft Flow makes hundreds of actions available.</span></span> <span data-ttu-id="4fe5c-111">Например, вы можете использовать Microsoft Flow, чтобы автоматически отправить уведомление по электронной почте или создать ошибку в Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="4fe5c-111">For example, you can use Microsoft Flow to automatically send an email notification or create a bug in Visual Studio Team Services.</span></span> <span data-ttu-id="4fe5c-112">Вы также можете воспользоваться одним из нескольких [шаблонов](https://ms.flow.microsoft.com/en-us/connectors/shared_applicationinsights/?slug=azure-application-insights), доступных для соединителя для Microsoft Flow.</span><span class="sxs-lookup"><span data-stu-id="4fe5c-112">You can also use one of the many [templates](https://ms.flow.microsoft.com/en-us/connectors/shared_applicationinsights/?slug=azure-application-insights) that are available for the connector for Microsoft Flow.</span></span> <span data-ttu-id="4fe5c-113">С помощью этих шаблонов можно ускорить процесс создания последовательности.</span><span class="sxs-lookup"><span data-stu-id="4fe5c-113">These templates speed up the process of creating a flow.</span></span> 

<!--The Application Insights connector also works with [Azure Power Apps](https://powerapps.microsoft.com/en-us/) and [Azure Logic Apps](https://azure.microsoft.com/services/logic-apps/?v=17.23h). --> 

## <a name="create-a-flow-for-application-insights"></a><span data-ttu-id="4fe5c-114">Создание последовательности для Application Insights</span><span class="sxs-lookup"><span data-stu-id="4fe5c-114">Create a flow for Application Insights</span></span>

<span data-ttu-id="4fe5c-115">В этом руководстве вы узнаете, как создать последовательность, использующую алгоритм автоматической кластеризации Analytics, для группирования атрибутов данных для веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="4fe5c-115">In this tutorial, you will learn how to create a flow that uses the Analytics auto-cluster algorithm to group attributes in the data for a web application.</span></span> <span data-ttu-id="4fe5c-116">Отправка результатов по электронной почте — это лишь один из примеров того, как можно совместно использовать Microsoft Flow и Application Insights Analytics.</span><span class="sxs-lookup"><span data-stu-id="4fe5c-116">The flow automatically sends the results by email, just one example of how you can use Microsoft Flow and Application Insights Analytics together.</span></span> 

### <a name="step-1-create-a-flow"></a><span data-ttu-id="4fe5c-117">Шаг 1. Создание последовательности</span><span class="sxs-lookup"><span data-stu-id="4fe5c-117">Step 1: Create a flow</span></span>
1. <span data-ttu-id="4fe5c-118">Войдите в службу [Microsoft Flow](http://flow.microsoft.com) и выберите **Мои последовательности**.</span><span class="sxs-lookup"><span data-stu-id="4fe5c-118">Sign in to [Microsoft Flow](http://flow.microsoft.com), and then select **My Flows**.</span></span>
2. <span data-ttu-id="4fe5c-119">Щелкните **Create a flow from blank** (Создать последовательность с нуля).</span><span class="sxs-lookup"><span data-stu-id="4fe5c-119">Click **Create a flow from blank**.</span></span>

### <a name="step-2-create-a-trigger-for-your-flow"></a><span data-ttu-id="4fe5c-120">Шаг 2. Создание триггера для последовательности</span><span class="sxs-lookup"><span data-stu-id="4fe5c-120">Step 2: Create a trigger for your flow</span></span>
1. <span data-ttu-id="4fe5c-121">Выберите **Расписание**, а затем **Расписание — повторение**.</span><span class="sxs-lookup"><span data-stu-id="4fe5c-121">Select **Schedule**, and then select **Schedule - Recurrence**.</span></span>
2. <span data-ttu-id="4fe5c-122">В поле **Частота** выберите **День**, а в поле **Интервал** введите **1**.</span><span class="sxs-lookup"><span data-stu-id="4fe5c-122">In the **Frequency** box, select **Day**, and in the **Interval** box, enter **1**.</span></span>

    ![Диалоговое окно триггера Microsoft Flow](./media/app-insights-automate-with-flow/flow1.png)


### <a name="step-3-add-an-application-insights-action"></a><span data-ttu-id="4fe5c-124">Шаг 3. Добавление действия Application Insights</span><span class="sxs-lookup"><span data-stu-id="4fe5c-124">Step 3: Add an Application Insights action</span></span>
1. <span data-ttu-id="4fe5c-125">Выберите поле **+Новый шаг**, а затем щелкните **Добавить действие**.</span><span class="sxs-lookup"><span data-stu-id="4fe5c-125">Click **New step**, and then click **Add an action**.</span></span>
2. <span data-ttu-id="4fe5c-126">Выполните поиск по запросу **Azure Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="4fe5c-126">Search for **Azure Application Insights**.</span></span>
3. <span data-ttu-id="4fe5c-127">Выберите **Azure Application Insights – Visualize Analytics query Preview** (Azure Application Insights — визуализация запроса Analytics [предварительная версия]).</span><span class="sxs-lookup"><span data-stu-id="4fe5c-127">Click **Azure Application Insights – Visualize Analytics query Preview**.</span></span>

    ![Окно запуска запроса Analytics](./media/app-insights-automate-with-flow/flow2.png)

### <a name="step-4-connect-to-an-application-insights-resource"></a><span data-ttu-id="4fe5c-129">Шаг 4. Подключение к ресурсу Application Insights</span><span class="sxs-lookup"><span data-stu-id="4fe5c-129">Step 4: Connect to an Application Insights resource</span></span>

<span data-ttu-id="4fe5c-130">Чтобы выполнить этот шаг, необходим идентификатор приложения и ключ API для ресурса.</span><span class="sxs-lookup"><span data-stu-id="4fe5c-130">To complete this step, you need an application ID and an API key for your resource.</span></span> <span data-ttu-id="4fe5c-131">Их можно получить на портале Azure, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="4fe5c-131">You can retrieve them from the Azure portal, as shown in the following diagram:</span></span>

![Идентификатор приложения на портале Azure](./media/app-insights-automate-with-flow/appid.png) 

- <span data-ttu-id="4fe5c-133">Укажите имя подключения, а также идентификатор приложения и ключ API.</span><span class="sxs-lookup"><span data-stu-id="4fe5c-133">Provide a name for your connection, along with the application ID and API key.</span></span>

    ![Окно подключения Microsoft Flow](./media/app-insights-automate-with-flow/flow3.png)

### <a name="step-5-specify-the-analytics-query-and-chart-type"></a><span data-ttu-id="4fe5c-135">Шаг 5. Указание запроса Analytics и типа диаграммы</span><span class="sxs-lookup"><span data-stu-id="4fe5c-135">Step 5: Specify the Analytics query and chart type</span></span>
<span data-ttu-id="4fe5c-136">В этом примере выбираются невыполненные запросы за последний день. Они сопоставляются с исключениями, которые возникли в рамках операции.</span><span class="sxs-lookup"><span data-stu-id="4fe5c-136">This example query selects the failed requests within the last day and correlates them with exceptions that occurred as part of the operation.</span></span> <span data-ttu-id="4fe5c-137">Analytics сопоставляет их на основе идентификатора operation_Id.</span><span class="sxs-lookup"><span data-stu-id="4fe5c-137">Analytics correlates them based on the operation_Id identifier.</span></span> <span data-ttu-id="4fe5c-138">Затем запрос разделяет результаты с помощью алгоритма автоматической кластеризации.</span><span class="sxs-lookup"><span data-stu-id="4fe5c-138">The query then segments the results by using the autocluster algorithm.</span></span> 

<span data-ttu-id="4fe5c-139">При создании собственных запросов убедитесь, что они работают должным образом в Analytics, прежде чем добавить их в последовательность.</span><span class="sxs-lookup"><span data-stu-id="4fe5c-139">When you create your own queries, verify that they are working properly in Analytics before you add it to your flow.</span></span>

- <span data-ttu-id="4fe5c-140">Добавьте следующий запрос Analytics и выберите тип диаграммы "Таблица HTML".</span><span class="sxs-lookup"><span data-stu-id="4fe5c-140">Add the following Analytics query, and then select the HTML table chart type.</span></span> 

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

### <a name="step-6-configure-the-flow-to-send-email"></a><span data-ttu-id="4fe5c-142">Шаг 6. Настройка последовательности для отправки электронной почты</span><span class="sxs-lookup"><span data-stu-id="4fe5c-142">Step 6: Configure the flow to send email</span></span>

1. <span data-ttu-id="4fe5c-143">Выберите поле **+Новый шаг**, а затем щелкните **Добавить действие**.</span><span class="sxs-lookup"><span data-stu-id="4fe5c-143">Click **New step**, and then click **Add an action**.</span></span>
2. <span data-ttu-id="4fe5c-144">Выполните поиск по запросу **Office 365 Outlook**.</span><span class="sxs-lookup"><span data-stu-id="4fe5c-144">Search for **Office 365 Outlook**.</span></span>
3. <span data-ttu-id="4fe5c-145">Щелкните **Office 365 Outlook – Send an email** (Office 365 Outlook — отправка сообщения электронной почты).</span><span class="sxs-lookup"><span data-stu-id="4fe5c-145">Click **Office 365 Outlook – Send an email**.</span></span>

    ![Окно выбора Office 365 Outlook](./media/app-insights-automate-with-flow/flow2b.png)

4. <span data-ttu-id="4fe5c-147">В окне **Отправка сообщения электронной почты** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="4fe5c-147">In the **Send an email** window, do the following:</span></span>

   <span data-ttu-id="4fe5c-148">а.</span><span class="sxs-lookup"><span data-stu-id="4fe5c-148">a.</span></span> <span data-ttu-id="4fe5c-149">Введите адрес электронной почты получателя.</span><span class="sxs-lookup"><span data-stu-id="4fe5c-149">Type the email address of the recipient.</span></span>

   <span data-ttu-id="4fe5c-150">b.</span><span class="sxs-lookup"><span data-stu-id="4fe5c-150">b.</span></span> <span data-ttu-id="4fe5c-151">Введите тему сообщения.</span><span class="sxs-lookup"><span data-stu-id="4fe5c-151">Type a subject for the email.</span></span>

   <span data-ttu-id="4fe5c-152">c.</span><span class="sxs-lookup"><span data-stu-id="4fe5c-152">c.</span></span> <span data-ttu-id="4fe5c-153">Щелкните в любом месте в поле **Текст**, затем в открывшемся справа меню динамического содержимого выберите **Текст**.</span><span class="sxs-lookup"><span data-stu-id="4fe5c-153">Click anywhere in the **Body** box and then, on the dynamic content menu that opens at the right, select **Body**.</span></span>

   <span data-ttu-id="4fe5c-154">г)</span><span class="sxs-lookup"><span data-stu-id="4fe5c-154">d.</span></span> <span data-ttu-id="4fe5c-155">Щелкните **Показать дополнительные параметры**.</span><span class="sxs-lookup"><span data-stu-id="4fe5c-155">Click **Show advanced options**.</span></span>

    ![Конфигурация Office 365 Outlook](./media/app-insights-automate-with-flow/flow5.png)

5. <span data-ttu-id="4fe5c-157">В меню динамического содержимого выполните следующее.</span><span class="sxs-lookup"><span data-stu-id="4fe5c-157">On the dynamic content menu, do the following:</span></span>

    <span data-ttu-id="4fe5c-158">а.</span><span class="sxs-lookup"><span data-stu-id="4fe5c-158">a.</span></span> <span data-ttu-id="4fe5c-159">Выберите **Имя вложения**.</span><span class="sxs-lookup"><span data-stu-id="4fe5c-159">Select **Attachment Name**.</span></span>

    <span data-ttu-id="4fe5c-160">b.</span><span class="sxs-lookup"><span data-stu-id="4fe5c-160">b.</span></span> <span data-ttu-id="4fe5c-161">Выберите **Содержимое вложения**.</span><span class="sxs-lookup"><span data-stu-id="4fe5c-161">Select **Attachment Content**.</span></span>
    
    <span data-ttu-id="4fe5c-162">c.</span><span class="sxs-lookup"><span data-stu-id="4fe5c-162">c.</span></span> <span data-ttu-id="4fe5c-163">В поле **Является HTML** выберите значение **Да**.</span><span class="sxs-lookup"><span data-stu-id="4fe5c-163">In the **Is HTML** box, select **Yes**.</span></span>

    ![Экран настройки сообщения электронной почты Office 365](./media/app-insights-automate-with-flow/flow7.png)

### <a name="step-7-save-and-test-your-flow"></a><span data-ttu-id="4fe5c-165">Шаг 7. Сохранение и тестирование последовательности</span><span class="sxs-lookup"><span data-stu-id="4fe5c-165">Step 7: Save and test your flow</span></span>
- <span data-ttu-id="4fe5c-166">В поле **Имя последовательности** добавьте имя последовательности и нажмите кнопку **Создать последовательность**.</span><span class="sxs-lookup"><span data-stu-id="4fe5c-166">In the **Flow name** box, add a name for your flow, and then click **Create flow**.</span></span>

    ![Окно создания последовательности](./media/app-insights-automate-with-flow/flow8.png)

<span data-ttu-id="4fe5c-168">Вы можете подождать, пока триггер запустит действие, или немедленно запустить последовательность, [запустив триггер по запросу](https://flow.microsoft.com/blog/run-now-and-six-more-services/).</span><span class="sxs-lookup"><span data-stu-id="4fe5c-168">You can wait for the trigger to run this action, or you can run the flow immediately by [running the trigger on demand](https://flow.microsoft.com/blog/run-now-and-six-more-services/).</span></span>

<span data-ttu-id="4fe5c-169">При выполнении последовательности получатели, указанные в списке рассылки, получат сообщение электронной почты, которое выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="4fe5c-169">When the flow runs, the recipients you have specified in the email list receive an email message that looks like the following:</span></span>

![Пример электронного сообщения](./media/app-insights-automate-with-flow/flow9.png)


## <a name="next-steps"></a><span data-ttu-id="4fe5c-171">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4fe5c-171">Next steps</span></span>

- <span data-ttu-id="4fe5c-172">Узнайте больше о создании [запросов Analytics](app-insights-analytics-using.md).</span><span class="sxs-lookup"><span data-stu-id="4fe5c-172">Learn more about creating [Analytics queries](app-insights-analytics-using.md).</span></span>
- <span data-ttu-id="4fe5c-173">Дополнительные сведения о [Microsoft Flow](https://ms.flow.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="4fe5c-173">Learn more about [Microsoft Flow](https://ms.flow.microsoft.com).</span></span>



<!--Link references-->





