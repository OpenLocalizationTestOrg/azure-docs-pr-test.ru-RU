---
title: "aaaScenario - создать панель мониторинга аналитики клиента без сервера Azure с | Документы Microsoft"
description: "Пример того, как можно построить toomanage клиента панели мониторинга, отзыв, социальных данных и многие другие приложения логики Azure и Azure функции."
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
ms.openlocfilehash: db175e895e37aa795a9c34bf4d65566bf68f8c37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-real-time-customer-insights-dashboard-with-azure-logic-apps-and-azure-functions"></a><span data-ttu-id="8d843-103">Создание панели мониторинга сведений о клиентах в режиме реального времени с помощью Функций Azure и Azure Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="8d843-103">Create a real-time customer insights dashboard with Azure Logic Apps and Azure Functions</span></span>

<span data-ttu-id="8d843-104">Azure без сервера средства предоставляют мощные возможности tooquickly сборки и узлов приложений в облаке hello без необходимости toothink об инфраструктуре.</span><span class="sxs-lookup"><span data-stu-id="8d843-104">Azure Serverless tools provide powerful capabilities tooquickly build and host applications in hello cloud, without having toothink about infrastructure.</span></span>  <span data-ttu-id="8d843-105">В этом случае она будет создана tootrigger мониторинга отзывов пользователей, анализ сопровождение машинного обучения и публикации аналитики источника как Power BI или Озера данных Azure.</span><span class="sxs-lookup"><span data-stu-id="8d843-105">In this scenario, we will create a dashboard tootrigger on customer feedback, analyze feedback with machine learning, and publish insights a source like Power BI or Azure Data Lake.</span></span>

## <a name="overview-of-hello-scenario-and-tools-used"></a><span data-ttu-id="8d843-106">Общие сведения о сценарии hello и средства, используемые</span><span class="sxs-lookup"><span data-stu-id="8d843-106">Overview of hello scenario and tools used</span></span>

<span data-ttu-id="8d843-107">В заказ tooimplement это решение, мы будет использовать hello два ключевых компонента без сервера приложений в Azure: [функции Azure](https://azure.microsoft.com/services/functions/) и [приложения логики Azure](https://azure.microsoft.com/services/logic-apps/).</span><span class="sxs-lookup"><span data-stu-id="8d843-107">In order tooimplement this solution, we will leverage hello two key components of serverless apps in Azure: [Azure Functions](https://azure.microsoft.com/services/functions/) and [Azure Logic Apps](https://azure.microsoft.com/services/logic-apps/).</span></span>

<span data-ttu-id="8d843-108">Логика приложения — это механизм без сервера рабочих процессов в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="8d843-108">Logic Apps is a serverless workflow engine in hello cloud.</span></span>  <span data-ttu-id="8d843-109">Он обеспечивает согласование по компонентам без сервера, а также подключается к tooover 100 служб и интерфейсов API.</span><span class="sxs-lookup"><span data-stu-id="8d843-109">It provides orchestration across serverless components, and also connects tooover 100 services and APIs.</span></span>  <span data-ttu-id="8d843-110">В этом случае мы создадим tootrigger логики приложения на отзывы от клиентов.</span><span class="sxs-lookup"><span data-stu-id="8d843-110">For this scenario, we will create a logic app tootrigger on feedback from customers.</span></span>  <span data-ttu-id="8d843-111">Ниже перечислены некоторые hello соединителей, которые могут помочь в отклик отзыв toocustomer Outlook.com, Office 365, Monkey опроса, Twitter и HTTP-запроса [из веб-формы](https://blogs.msdn.microsoft.com/logicapps/2017/01/30/calling-a-logic-app-from-an-html-form/).</span><span class="sxs-lookup"><span data-stu-id="8d843-111">Some of hello connectors that can assist in reacting toocustomer feedback include Outlook.com, Office 365, Survey Monkey, Twitter, and an HTTP Request [from a web form](https://blogs.msdn.microsoft.com/logicapps/2017/01/30/calling-a-logic-app-from-an-html-form/).</span></span>  <span data-ttu-id="8d843-112">Для рабочего процесса hello ниже мы отслеживает хэштегом в Twitter.</span><span class="sxs-lookup"><span data-stu-id="8d843-112">For hello workflow below, we will monitor a hashtag on Twitter.</span></span>

<span data-ttu-id="8d843-113">Функции предоставляют без сервера вычислений в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="8d843-113">Functions provide serverless compute in hello cloud.</span></span>  <span data-ttu-id="8d843-114">В этом сценарии мы будем использовать функции Azure tooflag твиты от клиентов на основе ряда предварительно определенных ключевых слов.</span><span class="sxs-lookup"><span data-stu-id="8d843-114">In this scenario, we will use Azure Functions tooflag tweets from customers based on a series of pre-defined key words.</span></span>

<span data-ttu-id="8d843-115">Hello всего решения может быть [сборки в Visual Studio](logic-apps-deploy-from-vs.md) и [развернут как часть шаблона ресурсов](logic-apps-create-deploy-template.md).</span><span class="sxs-lookup"><span data-stu-id="8d843-115">hello entire solution can be [build in Visual Studio](logic-apps-deploy-from-vs.md) and [deployed as part of a resource template](logic-apps-create-deploy-template.md).</span></span>  <span data-ttu-id="8d843-116">Имеется также видеоруководство hello сценария [на канале 9](http://aka.ms/logicappsdemo).</span><span class="sxs-lookup"><span data-stu-id="8d843-116">There is also video walkthrough of hello scenario [on Channel 9](http://aka.ms/logicappsdemo).</span></span>

## <a name="build-hello-logic-app-tootrigger-on-customer-data"></a><span data-ttu-id="8d843-117">Построение tootrigger приложения hello логику на данных о клиентах</span><span class="sxs-lookup"><span data-stu-id="8d843-117">Build hello logic app tootrigger on customer data</span></span>

<span data-ttu-id="8d843-118">После [Создание приложения логики](logic-apps-create-a-logic-app.md) в Visual Studio или hello портала Azure:</span><span class="sxs-lookup"><span data-stu-id="8d843-118">After [creating a logic app](logic-apps-create-a-logic-app.md) in Visual Studio or hello Azure portal:</span></span>

1. <span data-ttu-id="8d843-119">Добавьте триггер, который будет активироваться при размещении **новых твитов** в Twitter.</span><span class="sxs-lookup"><span data-stu-id="8d843-119">Add a trigger for **On New Tweets** from Twitter</span></span>
2. <span data-ttu-id="8d843-120">Настройте tootweets toolisten hello триггер на ключевое слово или хэштегом.</span><span class="sxs-lookup"><span data-stu-id="8d843-120">Configure hello trigger toolisten tootweets on a keyword or hashtag.</span></span>

   > [!NOTE]
   > <span data-ttu-id="8d843-121">Определяет свойство повторения Hello в триггере hello частоты приложения hello логики проверки для новых элементов на основе опроса триггеры</span><span class="sxs-lookup"><span data-stu-id="8d843-121">hello recurrence property on hello trigger will determine how frequently hello logic app checks for new items on polling-based triggers</span></span>

   ![Пример триггера Twitter][1]

<span data-ttu-id="8d843-123">Это приложение будет реагировать на все новые твиты.</span><span class="sxs-lookup"><span data-stu-id="8d843-123">This app will now fire on all new tweets.</span></span>  <span data-ttu-id="8d843-124">Мы может принимать эти данные твит и глубже выраженное мнений hello.</span><span class="sxs-lookup"><span data-stu-id="8d843-124">We can then take that tweet data and understand more of hello sentiment expressed.</span></span>  <span data-ttu-id="8d843-125">Для этого мы используем hello [Когнитивных службы Azure](https://azure.microsoft.com/services/cognitive-services/) мнений toodetect текста.</span><span class="sxs-lookup"><span data-stu-id="8d843-125">For this we use hello [Azure Cognitive Service](https://azure.microsoft.com/services/cognitive-services/) toodetect sentiment of text.</span></span>

1. <span data-ttu-id="8d843-126">Нажмите кнопку **Новый шаг**.</span><span class="sxs-lookup"><span data-stu-id="8d843-126">Click **New Step**</span></span>
1. <span data-ttu-id="8d843-127">Выберите или найдите hello **анализа текста** соединителя</span><span class="sxs-lookup"><span data-stu-id="8d843-127">Select or search for hello **Text Analytics** connector</span></span>
1. <span data-ttu-id="8d843-128">Выберите hello **мнений обнаружить** операции</span><span class="sxs-lookup"><span data-stu-id="8d843-128">Select hello **Detect Sentiment** operation</span></span>
1. <span data-ttu-id="8d843-129">При запросе введите допустимый ключ Когнитивных службы для службы анализа текста hello</span><span class="sxs-lookup"><span data-stu-id="8d843-129">If prompted, provide a valid Cognitive Services key for hello Text Analytics service</span></span>
1. <span data-ttu-id="8d843-130">Добавить hello **твит текст** как hello tooanalyze текста.</span><span class="sxs-lookup"><span data-stu-id="8d843-130">Add hello **Tweet Text** as hello text tooanalyze.</span></span>

<span data-ttu-id="8d843-131">Теперь, когда есть hello твит данные и сведения, полученные на твиты hello ряд других соединители могут относиться:</span><span class="sxs-lookup"><span data-stu-id="8d843-131">Now that we have hello tweet data, and insights on hello tweet, a number of other connectors may be relevant:</span></span>
* <span data-ttu-id="8d843-132">Power BI — добавить tooStreaming строк набора данных: представление твиты режиме реального времени на Информационной панели.</span><span class="sxs-lookup"><span data-stu-id="8d843-132">Power BI - Add Rows tooStreaming Dataset: View tweets real time on a Power BI dashboard.</span></span>
* <span data-ttu-id="8d843-133">Озеро данных Azure — добавить файл: добавить tooinclude tooan Озера данных Azure набора данных для клиента данных в заданиях analytics.</span><span class="sxs-lookup"><span data-stu-id="8d843-133">Azure Data Lake - Append file: Add customer data tooan Azure Data Lake dataset tooinclude in analytics jobs.</span></span>
* <span data-ttu-id="8d843-134">SQL. Добавляются строки. Данные можно сохранить в базе данных для последующего извлечения.</span><span class="sxs-lookup"><span data-stu-id="8d843-134">SQL - Add rows: Store data in a database for later retrieval.</span></span>
* <span data-ttu-id="8d843-135">Slack. Отправляется сообщение. Канал Slack получает оповещение об отрицательном отзыве, для которого нужно предпринять действия.</span><span class="sxs-lookup"><span data-stu-id="8d843-135">Slack - Send message: Alert a slack channel on negative feedback that requires actions.</span></span>

<span data-ttu-id="8d843-136">Это функция Azure также может быть используется toodo несколько пользовательских вычислений на основе данных hello.</span><span class="sxs-lookup"><span data-stu-id="8d843-136">An Azure Function can also be used toodo more custom compute on top of hello data.</span></span>

## <a name="enriching-hello-data-with-an-azure-function"></a><span data-ttu-id="8d843-137">Обогащения данных hello с функцией Azure</span><span class="sxs-lookup"><span data-stu-id="8d843-137">Enriching hello data with an Azure Function</span></span>

<span data-ttu-id="8d843-138">Прежде чем создавать функции, мы должны toohave приложения функции в нашей подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="8d843-138">Before we can create a function, we need toohave a function app in our Azure subscription.</span></span>  <span data-ttu-id="8d843-139">Сведения о создании функцию Azure на портале hello можно [по следующему адресу](../azure-functions/functions-create-first-azure-function-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="8d843-139">Details on creating an Azure Function in hello portal can [be found here](../azure-functions/functions-create-first-azure-function-azure-portal.md)</span></span>

<span data-ttu-id="8d843-140">Для вызова непосредственно из приложения логики toobe функция она должна toohave HTTP активировать привязки.</span><span class="sxs-lookup"><span data-stu-id="8d843-140">For a function toobe called directly from a logic app, it needs toohave an HTTP trigger binding.</span></span>  <span data-ttu-id="8d843-141">Мы рекомендуем использовать hello **HttpTrigger** шаблона.</span><span class="sxs-lookup"><span data-stu-id="8d843-141">We recommend using hello **HttpTrigger** template.</span></span>

<span data-ttu-id="8d843-142">В этом случае тело запроса hello hello Azure функция будет твит текста hello.</span><span class="sxs-lookup"><span data-stu-id="8d843-142">In this scenario, hello request body of hello Azure Function would be hello tweet text.</span></span>  <span data-ttu-id="8d843-143">В коде функции hello просто определите логику на, если текст hello твит содержит ключевое слово или фразу.</span><span class="sxs-lookup"><span data-stu-id="8d843-143">In hello function code, simply define logic on if hello tweet text contains a key word or phrase.</span></span>  <span data-ttu-id="8d843-144">сама функция Hello может храниться как простые или сложные, необходимые для сценария hello.</span><span class="sxs-lookup"><span data-stu-id="8d843-144">hello function itself could be kept as simple or complex as needed for hello scenario.</span></span>

<span data-ttu-id="8d843-145">В конце функции hello hello просто возвращают ответа приложения логики toohello с данными.</span><span class="sxs-lookup"><span data-stu-id="8d843-145">At hello end of hello function, simply return a response toohello logic app with some data.</span></span>  <span data-ttu-id="8d843-146">Это может быть простое логическое значение (например, `containsKeyword`) или сложный объект.</span><span class="sxs-lookup"><span data-stu-id="8d843-146">This could be a simple boolean value (e.g. `containsKeyword`), or a complex object.</span></span>

![Настройка шага Функции Azure][2]

> [!TIP]
> <span data-ttu-id="8d843-148">При доступе к сложным ответа от функции в приложение логики, используйте действие hello синтаксического анализа JSON.</span><span class="sxs-lookup"><span data-stu-id="8d843-148">When accessing a complex response from a function in a logic app, use hello Parse JSON action.</span></span>

<span data-ttu-id="8d843-149">После сохранения функции hello, его можно добавить в приложение логику hello, созданной ранее.</span><span class="sxs-lookup"><span data-stu-id="8d843-149">Once hello function is saved, it can be added into hello logic app created above.</span></span>  <span data-ttu-id="8d843-150">В приложение логику hello:</span><span class="sxs-lookup"><span data-stu-id="8d843-150">In hello logic app:</span></span>

1. <span data-ttu-id="8d843-151">Нажмите кнопку tooadd **новый шаг**</span><span class="sxs-lookup"><span data-stu-id="8d843-151">Click tooadd a **New Step**</span></span>
1. <span data-ttu-id="8d843-152">Выберите hello **функции Azure** соединителя</span><span class="sxs-lookup"><span data-stu-id="8d843-152">Select hello **Azure Functions** connector</span></span>
1. <span data-ttu-id="8d843-153">Выберите существующую функцию toochoose и обзор toohello функция, созданная</span><span class="sxs-lookup"><span data-stu-id="8d843-153">Select toochoose an existing function, and browse toohello function created</span></span>
1. <span data-ttu-id="8d843-154">Отправить в hello **текст твит** для hello **текст запроса**</span><span class="sxs-lookup"><span data-stu-id="8d843-154">Send in hello **Tweet Text** for hello **Request Body**</span></span>

## <a name="running-and-monitoring-hello-solution"></a><span data-ttu-id="8d843-155">Выполнение и отслеживание hello решения</span><span class="sxs-lookup"><span data-stu-id="8d843-155">Running and monitoring hello solution</span></span>

<span data-ttu-id="8d843-156">Одно из преимуществ hello разработки без сервера взаимодействий в приложениях для логики — hello широкие возможности отладки и возможности мониторинга.</span><span class="sxs-lookup"><span data-stu-id="8d843-156">One of hello benefits of authoring serverless orchestrations in Logic Apps is hello rich debug and monitoring capabilities.</span></span>  <span data-ttu-id="8d843-157">Любое выполнение (текущие или исторические) можно просмотреть в среде Visual Studio, hello портал Azure или с помощью API-интерфейса REST hello и пакеты SDK.</span><span class="sxs-lookup"><span data-stu-id="8d843-157">Any run (current or historic) can be viewed from within Visual Studio, hello Azure portal, or via hello REST API and SDKs.</span></span>

<span data-ttu-id="8d843-158">Один из tootest простых способов hello приложения логики использует hello **запуска** кнопку в конструкторе hello.</span><span class="sxs-lookup"><span data-stu-id="8d843-158">One of hello easiest ways tootest a logic app is using hello **Run** button in hello designer.</span></span>  <span data-ttu-id="8d843-159">Щелкнув **запуска** продолжится триггер hello toopoll каждые 5 секунд, пока не будет обнаружено событие и предоставить обеспечивает динамическое представление в процессе запуска hello.</span><span class="sxs-lookup"><span data-stu-id="8d843-159">Clicking **Run** will continue toopoll hello trigger every 5 seconds until an event is detected, and give a live view as hello run progresses.</span></span>

<span data-ttu-id="8d843-160">Можно просмотреть предыдущие журналы выполнения в колонке Обзор hello hello портал Azure, или с помощью Visual Studio Cloud Explorer hello.</span><span class="sxs-lookup"><span data-stu-id="8d843-160">Previous run histories can be viewed on hello Overview blade in hello Azure portal, or using hello Visual Studio Cloud Explorer.</span></span>

## <a name="creating-a-deployment-template-for-automated-deployments"></a><span data-ttu-id="8d843-161">Создание шаблона развертывания для автоматического развертывания</span><span class="sxs-lookup"><span data-stu-id="8d843-161">Creating a deployment template for automated deployments</span></span>

<span data-ttu-id="8d843-162">После разработки решения, его можно записать и развернут с помощью tooany шаблона развертывания Azure регион Azure в Здравствуй, мир!.</span><span class="sxs-lookup"><span data-stu-id="8d843-162">Once a solution has been developed, it can be captured and deployed via an Azure deployment template tooany Azure region in hello world.</span></span>  <span data-ttu-id="8d843-163">Это полезно для изменения параметров разных версий этого рабочего процесса, а также для интеграции этого решения в конвейер сборки и выпуска.</span><span class="sxs-lookup"><span data-stu-id="8d843-163">This is useful for both modifying parameters for different versions of this workflow, but also for integrating this solution in a build and release pipeline.</span></span>  <span data-ttu-id="8d843-164">Дополнительные сведения о создании шаблона развертывания см. [в этой статье](logic-apps-create-deploy-template.md).</span><span class="sxs-lookup"><span data-stu-id="8d843-164">Details on creating a deployment template can be found [in this article](logic-apps-create-deploy-template.md).</span></span>

<span data-ttu-id="8d843-165">Функции Azure также могут быть включены в шаблон развертывания hello - так hello всего решения с все зависимости можно управлять как один шаблон.</span><span class="sxs-lookup"><span data-stu-id="8d843-165">Azure Functions can also be incorporated in hello deployment template - so hello entire solution with all dependencies can be managed as a single template.</span></span>  <span data-ttu-id="8d843-166">Пример развертывания шаблона функции можно найти в hello [быстрый запуск Azure шаблон репозитория](https://github.com/Azure/azure-quickstart-templates/tree/master/101-function-app-create-dynamic).</span><span class="sxs-lookup"><span data-stu-id="8d843-166">An example of a function deployment template can be found in hello [Azure quickstart template repository](https://github.com/Azure/azure-quickstart-templates/tree/master/101-function-app-create-dynamic).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8d843-167">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8d843-167">Next steps</span></span>

* [<span data-ttu-id="8d843-168">Примеры и распространенные сценарии для Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="8d843-168">See other examples and scenarios for Azure Logic Apps</span></span>](logic-apps-examples-and-scenarios.md)
* [<span data-ttu-id="8d843-169">Пошаговое видеоруководство по созданию этого решения</span><span class="sxs-lookup"><span data-stu-id="8d843-169">Watch a video walkthrough on creating this solution end-to-end</span></span>](http://aka.ms/logicappsdemo)
* [<span data-ttu-id="8d843-170">Узнайте, как toohandle и перехвата исключений в пределах приложения логики</span><span class="sxs-lookup"><span data-stu-id="8d843-170">Learn how toohandle and catch exceptions within a logic app</span></span>](logic-apps-exception-handling.md)

<!-- Image References -->
[1]: ./media/logic-apps-scenario-social-serverless/twitter.png
[2]: ./media/logic-apps-scenario-social-serverless/function.png