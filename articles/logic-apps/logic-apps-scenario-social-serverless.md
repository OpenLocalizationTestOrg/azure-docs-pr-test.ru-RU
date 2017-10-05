---
title: "Сценарий создания панели мониторинга сведений о клиентах с использованием беcсерверных средств в Azure | Документация Майкрософт"
description: "Пример того, как можно создать панель мониторинга для управления отзывами от клиентов, социальными данными и многим другим с помощью Функций Azure и Azure Logic Apps."
keywords: 
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: d565873c-6b1b-4057-9250-cf81a96180ae
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/29/2017
ms.author: jehollan
ms.openlocfilehash: 0b6e118cb13ab8185d8eeb42bec6147155967967
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-real-time-customer-insights-dashboard-with-azure-logic-apps-and-azure-functions"></a><span data-ttu-id="def6e-103">Создание панели мониторинга сведений о клиентах в режиме реального времени с помощью Функций Azure и Azure Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="def6e-103">Create a real-time customer insights dashboard with Azure Logic Apps and Azure Functions</span></span>

<span data-ttu-id="def6e-104">беcсерверные средства Azure предоставляют широкие возможности для быстрого создания и размещения приложений в облаке, не задумываясь об инфраструктуре.</span><span class="sxs-lookup"><span data-stu-id="def6e-104">Azure Serverless tools provide powerful capabilities to quickly build and host applications in the cloud, without having to think about infrastructure.</span></span>  <span data-ttu-id="def6e-105">В рамках этого сценария мы создадим панель мониторинга, которая будет запускаться при получении отзывов от клиентов, анализировать отзывы с помощью машинного обучения и публиковать аналитику в Power BI или Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="def6e-105">In this scenario, we will create a dashboard to trigger on customer feedback, analyze feedback with machine learning, and publish insights a source like Power BI or Azure Data Lake.</span></span>

## <a name="overview-of-the-scenario-and-tools-used"></a><span data-ttu-id="def6e-106">Краткий обзор сценария и используемых инструментов</span><span class="sxs-lookup"><span data-stu-id="def6e-106">Overview of the scenario and tools used</span></span>

<span data-ttu-id="def6e-107">Чтобы реализовать это решение, мы будем использовать два ключевых компонента беcсерверных приложений в Azure: [Функции Azure](https://azure.microsoft.com/services/functions/) и [Azure Logic Apps](https://azure.microsoft.com/services/logic-apps/).</span><span class="sxs-lookup"><span data-stu-id="def6e-107">In order to implement this solution, we will leverage the two key components of serverless apps in Azure: [Azure Functions](https://azure.microsoft.com/services/functions/) and [Azure Logic Apps](https://azure.microsoft.com/services/logic-apps/).</span></span>

<span data-ttu-id="def6e-108">Приложения логики — это беcсерверный обработчик рабочего процесса в облаке.</span><span class="sxs-lookup"><span data-stu-id="def6e-108">Logic Apps is a serverless workflow engine in the cloud.</span></span>  <span data-ttu-id="def6e-109">Он обеспечивает оркестрацию беcсерверных компонентов и подключается к более чем 100 службам и интерфейсам API.</span><span class="sxs-lookup"><span data-stu-id="def6e-109">It provides orchestration across serverless components, and also connects to over 100 services and APIs.</span></span>  <span data-ttu-id="def6e-110">В рамках этого сценария мы создадим приложение логики, которое будет запускаться при получении отзывов от клиентов.</span><span class="sxs-lookup"><span data-stu-id="def6e-110">For this scenario, we will create a logic app to trigger on feedback from customers.</span></span>  <span data-ttu-id="def6e-111">Ниже перечислены некоторые соединители, которые могут реагировать на отзывы от клиентов, включая Outlook.com, Office 365, Survey Monkey, Twitter и HTTP-запрос [из веб-формы](https://blogs.msdn.microsoft.com/logicapps/2017/01/30/calling-a-logic-app-from-an-html-form/).</span><span class="sxs-lookup"><span data-stu-id="def6e-111">Some of the connectors that can assist in reacting to customer feedback include Outlook.com, Office 365, Survey Monkey, Twitter, and an HTTP Request [from a web form](https://blogs.msdn.microsoft.com/logicapps/2017/01/30/calling-a-logic-app-from-an-html-form/).</span></span>  <span data-ttu-id="def6e-112">В описанном ниже рабочем процессе мы будем отслеживать хэштег в Twitter.</span><span class="sxs-lookup"><span data-stu-id="def6e-112">For the workflow below, we will monitor a hashtag on Twitter.</span></span>

<span data-ttu-id="def6e-113">Функции предоставляют беcсерверные вычисления в облаке.</span><span class="sxs-lookup"><span data-stu-id="def6e-113">Functions provide serverless compute in the cloud.</span></span>  <span data-ttu-id="def6e-114">В этом случае будут использоваться Функции Azure для пометки твитов от клиентов на основе набора предварительно определенных ключевых слов.</span><span class="sxs-lookup"><span data-stu-id="def6e-114">In this scenario, we will use Azure Functions to flag tweets from customers based on a series of pre-defined key words.</span></span>

<span data-ttu-id="def6e-115">Решение можно целиком [создать в Visual Studio](logic-apps-deploy-from-vs.md) и [развернуть как часть шаблона ресурсов](logic-apps-create-deploy-template.md).</span><span class="sxs-lookup"><span data-stu-id="def6e-115">The entire solution can be [build in Visual Studio](logic-apps-deploy-from-vs.md) and [deployed as part of a resource template](logic-apps-create-deploy-template.md).</span></span>  <span data-ttu-id="def6e-116">Существует также видеоруководство [на Channel 9](http://aka.ms/logicappsdemo).</span><span class="sxs-lookup"><span data-stu-id="def6e-116">There is also video walkthrough of the scenario [on Channel 9](http://aka.ms/logicappsdemo).</span></span>

## <a name="build-the-logic-app-to-trigger-on-customer-data"></a><span data-ttu-id="def6e-117">Создание приложения логики, которое будет запускаться при получении клиентских данных</span><span class="sxs-lookup"><span data-stu-id="def6e-117">Build the logic app to trigger on customer data</span></span>

<span data-ttu-id="def6e-118">После [создания приложения логики](logic-apps-create-a-logic-app.md) в Visual Studio или на портале Azure:</span><span class="sxs-lookup"><span data-stu-id="def6e-118">After [creating a logic app](logic-apps-create-a-logic-app.md) in Visual Studio or the Azure portal:</span></span>

1. <span data-ttu-id="def6e-119">Добавьте триггер, который будет активироваться при размещении **новых твитов** в Twitter.</span><span class="sxs-lookup"><span data-stu-id="def6e-119">Add a trigger for **On New Tweets** from Twitter</span></span>
2. <span data-ttu-id="def6e-120">Настройте триггер для прослушивания твитов по ключевому слову или хэш-тегу.</span><span class="sxs-lookup"><span data-stu-id="def6e-120">Configure the trigger to listen to tweets on a keyword or hashtag.</span></span>

   > [!NOTE]
   > <span data-ttu-id="def6e-121">Свойство повторения триггера определяет, как часто приложение логики будет проверять наличие новых элементов с помощью триггеров на основе опроса.</span><span class="sxs-lookup"><span data-stu-id="def6e-121">The recurrence property on the trigger will determine how frequently the logic app checks for new items on polling-based triggers</span></span>

   ![Пример триггера Twitter][1]

<span data-ttu-id="def6e-123">Это приложение будет реагировать на все новые твиты.</span><span class="sxs-lookup"><span data-stu-id="def6e-123">This app will now fire on all new tweets.</span></span>  <span data-ttu-id="def6e-124">Затем можно подробнее проанализировать тональность выраженного мнения.</span><span class="sxs-lookup"><span data-stu-id="def6e-124">We can then take that tweet data and understand more of the sentiment expressed.</span></span>  <span data-ttu-id="def6e-125">Для этого используется [Azure Cognitive Service](https://azure.microsoft.com/services/cognitive-services/).</span><span class="sxs-lookup"><span data-stu-id="def6e-125">For this we use the [Azure Cognitive Service](https://azure.microsoft.com/services/cognitive-services/) to detect sentiment of text.</span></span>

1. <span data-ttu-id="def6e-126">Нажмите кнопку **Новый шаг**.</span><span class="sxs-lookup"><span data-stu-id="def6e-126">Click **New Step**</span></span>
1. <span data-ttu-id="def6e-127">Выберите или найдите соединитель **Текстовая аналитика**.</span><span class="sxs-lookup"><span data-stu-id="def6e-127">Select or search for the **Text Analytics** connector</span></span>
1. <span data-ttu-id="def6e-128">Выберите операцию **Detect Sentiment** (Определение тональности).</span><span class="sxs-lookup"><span data-stu-id="def6e-128">Select the **Detect Sentiment** operation</span></span>
1. <span data-ttu-id="def6e-129">При запросе введите допустимый ключ Cognitive Services для службы текстовой аналитики.</span><span class="sxs-lookup"><span data-stu-id="def6e-129">If prompted, provide a valid Cognitive Services key for the Text Analytics service</span></span>
1. <span data-ttu-id="def6e-130">Добавьте **текст твита** в качестве текста для анализа.</span><span class="sxs-lookup"><span data-stu-id="def6e-130">Add the **Tweet Text** as the text to analyze.</span></span>

<span data-ttu-id="def6e-131">Теперь, когда получены данные и аналитические сведения о твите, можно использовать ряд других соединителей:</span><span class="sxs-lookup"><span data-stu-id="def6e-131">Now that we have the tweet data, and insights on the tweet, a number of other connectors may be relevant:</span></span>
* <span data-ttu-id="def6e-132">Power BI. Добавляются строки в набор данных потоковой передачи. Твиты можно просматривать в режиме реального времени на панели мониторинга Power BI.</span><span class="sxs-lookup"><span data-stu-id="def6e-132">Power BI - Add Rows to Streaming Dataset: View tweets real time on a Power BI dashboard.</span></span>
* <span data-ttu-id="def6e-133">Azure Data Lake. Добавляется файл. Данные клиента добавляются в набор данных Azure Data Lake для включения в задания аналитики.</span><span class="sxs-lookup"><span data-stu-id="def6e-133">Azure Data Lake - Append file: Add customer data to an Azure Data Lake dataset to include in analytics jobs.</span></span>
* <span data-ttu-id="def6e-134">SQL. Добавляются строки. Данные можно сохранить в базе данных для последующего извлечения.</span><span class="sxs-lookup"><span data-stu-id="def6e-134">SQL - Add rows: Store data in a database for later retrieval.</span></span>
* <span data-ttu-id="def6e-135">Slack. Отправляется сообщение. Канал Slack получает оповещение об отрицательном отзыве, для которого нужно предпринять действия.</span><span class="sxs-lookup"><span data-stu-id="def6e-135">Slack - Send message: Alert a slack channel on negative feedback that requires actions.</span></span>

<span data-ttu-id="def6e-136">Функцию Azure также можно использовать для настраиваемых вычислений на основе данных.</span><span class="sxs-lookup"><span data-stu-id="def6e-136">An Azure Function can also be used to do more custom compute on top of the data.</span></span>

## <a name="enriching-the-data-with-an-azure-function"></a><span data-ttu-id="def6e-137">Обогащение данных с помощью Функции Azure</span><span class="sxs-lookup"><span data-stu-id="def6e-137">Enriching the data with an Azure Function</span></span>

<span data-ttu-id="def6e-138">Чтобы создать функцию, необходимо иметь приложение-функцию в подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="def6e-138">Before we can create a function, we need to have a function app in our Azure subscription.</span></span>  <span data-ttu-id="def6e-139">Сведения о создании Функции Azure на портале можно найти [здесь](../azure-functions/functions-create-first-azure-function-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="def6e-139">Details on creating an Azure Function in the portal can [be found here](../azure-functions/functions-create-first-azure-function-azure-portal.md)</span></span>

<span data-ttu-id="def6e-140">Чтобы функция могла вызываться непосредственно из приложения логики, для нее необходимо настроить привязку триггера HTTP.</span><span class="sxs-lookup"><span data-stu-id="def6e-140">For a function to be called directly from a logic app, it needs to have an HTTP trigger binding.</span></span>  <span data-ttu-id="def6e-141">Мы советуем использовать шаблон **HttpTrigger**.</span><span class="sxs-lookup"><span data-stu-id="def6e-141">We recommend using the **HttpTrigger** template.</span></span>

<span data-ttu-id="def6e-142">В этом случае текстом запроса Функции Azure будет текст твита.</span><span class="sxs-lookup"><span data-stu-id="def6e-142">In this scenario, the request body of the Azure Function would be the tweet text.</span></span>  <span data-ttu-id="def6e-143">В коде функции просто задайте логику для текста твита, содержащего ключевое слово или фразу.</span><span class="sxs-lookup"><span data-stu-id="def6e-143">In the function code, simply define logic on if the tweet text contains a key word or phrase.</span></span>  <span data-ttu-id="def6e-144">Сама функция может быть простой или сложной в зависимости от сценария.</span><span class="sxs-lookup"><span data-stu-id="def6e-144">The function itself could be kept as simple or complex as needed for the scenario.</span></span>

<span data-ttu-id="def6e-145">В конце функции просто верните в приложение логики ответ с данными.</span><span class="sxs-lookup"><span data-stu-id="def6e-145">At the end of the function, simply return a response to the logic app with some data.</span></span>  <span data-ttu-id="def6e-146">Это может быть простое логическое значение (например, `containsKeyword`) или сложный объект.</span><span class="sxs-lookup"><span data-stu-id="def6e-146">This could be a simple boolean value (e.g. `containsKeyword`), or a complex object.</span></span>

![Настройка шага Функции Azure][2]

> [!TIP]
> <span data-ttu-id="def6e-148">При доступе к сложному ответу от функции в приложении логики используйте действие "Анализ JSON".</span><span class="sxs-lookup"><span data-stu-id="def6e-148">When accessing a complex response from a function in a logic app, use the Parse JSON action.</span></span>

<span data-ttu-id="def6e-149">После сохранения функции ее можно добавить в приложение логики, созданное ранее.</span><span class="sxs-lookup"><span data-stu-id="def6e-149">Once the function is saved, it can be added into the logic app created above.</span></span>  <span data-ttu-id="def6e-150">В приложении логики:</span><span class="sxs-lookup"><span data-stu-id="def6e-150">In the logic app:</span></span>

1. <span data-ttu-id="def6e-151">Щелкните **Новый шаг**.</span><span class="sxs-lookup"><span data-stu-id="def6e-151">Click to add a **New Step**</span></span>
1. <span data-ttu-id="def6e-152">Выберите соединитель **Функции Azure**.</span><span class="sxs-lookup"><span data-stu-id="def6e-152">Select the **Azure Functions** connector</span></span>
1. <span data-ttu-id="def6e-153">Щелкните, чтобы выбрать существующую функцию, и перейдите к созданной функции.</span><span class="sxs-lookup"><span data-stu-id="def6e-153">Select to choose an existing function, and browse to the function created</span></span>
1. <span data-ttu-id="def6e-154">Отправьте **текст твита** в качестве **текста запроса**.</span><span class="sxs-lookup"><span data-stu-id="def6e-154">Send in the **Tweet Text** for the **Request Body**</span></span>

## <a name="running-and-monitoring-the-solution"></a><span data-ttu-id="def6e-155">Выполнение и отслеживание решения</span><span class="sxs-lookup"><span data-stu-id="def6e-155">Running and monitoring the solution</span></span>

<span data-ttu-id="def6e-156">Одним из преимуществ создания беcсерверных оркестраций в Logic Apps являются широкие возможности отладки и мониторинга.</span><span class="sxs-lookup"><span data-stu-id="def6e-156">One of the benefits of authoring serverless orchestrations in Logic Apps is the rich debug and monitoring capabilities.</span></span>  <span data-ttu-id="def6e-157">Любое выполнение (текущее или прошлое) можно просмотреть в среде Visual Studio, на портале Azure или с помощью REST API и пакетов SDK.</span><span class="sxs-lookup"><span data-stu-id="def6e-157">Any run (current or historic) can be viewed from within Visual Studio, the Azure portal, or via the REST API and SDKs.</span></span>

<span data-ttu-id="def6e-158">Один из самых простых способов тестирования приложения логики — использовать кнопку **запуска** в конструкторе.</span><span class="sxs-lookup"><span data-stu-id="def6e-158">One of the easiest ways to test a logic app is using the **Run** button in the designer.</span></span>  <span data-ttu-id="def6e-159">После нажатия кнопки **запуска** триггер будет опрашиваться каждые 5 секунд, пока не будет обнаружено событие, после чего появится возможность наблюдать за ходом выполнения в режиме реального времени.</span><span class="sxs-lookup"><span data-stu-id="def6e-159">Clicking **Run** will continue to poll the trigger every 5 seconds until an event is detected, and give a live view as the run progresses.</span></span>

<span data-ttu-id="def6e-160">В колонке обзора на портале Azure или с помощью Visual Studio Cloud Explorer можно просмотреть историю предыдущих выполнений.</span><span class="sxs-lookup"><span data-stu-id="def6e-160">Previous run histories can be viewed on the Overview blade in the Azure portal, or using the Visual Studio Cloud Explorer.</span></span>

## <a name="creating-a-deployment-template-for-automated-deployments"></a><span data-ttu-id="def6e-161">Создание шаблона развертывания для автоматического развертывания</span><span class="sxs-lookup"><span data-stu-id="def6e-161">Creating a deployment template for automated deployments</span></span>

<span data-ttu-id="def6e-162">После разработки решения его можно записать и развернуть с помощью шаблона развертывания Azure в любом регионе Azure в мире.</span><span class="sxs-lookup"><span data-stu-id="def6e-162">Once a solution has been developed, it can be captured and deployed via an Azure deployment template to any Azure region in the world.</span></span>  <span data-ttu-id="def6e-163">Это полезно для изменения параметров разных версий этого рабочего процесса, а также для интеграции этого решения в конвейер сборки и выпуска.</span><span class="sxs-lookup"><span data-stu-id="def6e-163">This is useful for both modifying parameters for different versions of this workflow, but also for integrating this solution in a build and release pipeline.</span></span>  <span data-ttu-id="def6e-164">Дополнительные сведения о создании шаблона развертывания см. [в этой статье](logic-apps-create-deploy-template.md).</span><span class="sxs-lookup"><span data-stu-id="def6e-164">Details on creating a deployment template can be found [in this article](logic-apps-create-deploy-template.md).</span></span>

<span data-ttu-id="def6e-165">Функции Azure также могут быть включены в шаблон развертывания таким образом, чтобы всем решением вместе со всеми зависимостями можно было управлять как одним шаблоном.</span><span class="sxs-lookup"><span data-stu-id="def6e-165">Azure Functions can also be incorporated in the deployment template - so the entire solution with all dependencies can be managed as a single template.</span></span>  <span data-ttu-id="def6e-166">Пример шаблона развертывания функции можно найти в [репозитории шаблонов быстрого запуска Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/101-function-app-create-dynamic).</span><span class="sxs-lookup"><span data-stu-id="def6e-166">An example of a function deployment template can be found in the [Azure quickstart template repository](https://github.com/Azure/azure-quickstart-templates/tree/master/101-function-app-create-dynamic).</span></span>

## <a name="next-steps"></a><span data-ttu-id="def6e-167">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="def6e-167">Next steps</span></span>

* [<span data-ttu-id="def6e-168">Примеры и распространенные сценарии для Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="def6e-168">See other examples and scenarios for Azure Logic Apps</span></span>](logic-apps-examples-and-scenarios.md)
* [<span data-ttu-id="def6e-169">Пошаговое видеоруководство по созданию этого решения</span><span class="sxs-lookup"><span data-stu-id="def6e-169">Watch a video walkthrough on creating this solution end-to-end</span></span>](http://aka.ms/logicappsdemo)
* [<span data-ttu-id="def6e-170">Обработка ошибок и исключений в Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="def6e-170">Learn how to handle and catch exceptions within a logic app</span></span>](logic-apps-exception-handling.md)

<!-- Image References -->
[1]: ./media/logic-apps-scenario-social-serverless/twitter.png
[2]: ./media/logic-apps-scenario-social-serverless/function.png