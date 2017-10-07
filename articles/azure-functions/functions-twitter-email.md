---
title: "aaaCreate функцию, которая интегрируется с приложениями логики Azure | Документы Microsoft"
description: "Создайте функцию, которая интегрируется с мнений твит toocategorize приложения логики Azure и Когнитивных служб Azure и отправки уведомлений при низкой мнений."
services: functions, logic-apps, cognitive-services
keywords: "рабочий процесс, облачные приложения, облачные службы, бизнес-процессы, системная интеграция, интеграция приложений, EAI"
documentationcenter: 
author: ggailey777
manager: erikre
editor: 
ms.assetid: 60495cc5-1638-4bf0-8174-52786d227734
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: e176bd946af9a3684b3ad0e4b1bed1c3ee344019
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-that-integrates-with-azure-logic-apps"></a><span data-ttu-id="89176-104">Создание функции, интегрируемой с Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="89176-104">Create a function that integrates with Azure Logic Apps</span></span>

<span data-ttu-id="89176-105">Функции Azure интегрируется с логикой приложения Azure в конструкторе логики приложения hello.</span><span class="sxs-lookup"><span data-stu-id="89176-105">Azure Functions integrates with Azure Logic Apps in hello Logic Apps Designer.</span></span> <span data-ttu-id="89176-106">Эта интеграция позволяет использовать hello вычислительной мощности в взаимодействий с другими Azure и служб сторонних функций.</span><span class="sxs-lookup"><span data-stu-id="89176-106">This integration lets you use hello computing power of Functions in orchestrations with other Azure and third-party services.</span></span> 

<span data-ttu-id="89176-107">В этом учебнике показано функционирование toouse мнений tooanalyze логику приложения и Когнитивных служб Azure из сообщений Twitter.</span><span class="sxs-lookup"><span data-stu-id="89176-107">This tutorial shows you how toouse Functions with Logic Apps and Azure Cognitive Services tooanalyze sentiment from Twitter posts.</span></span> <span data-ttu-id="89176-108">Функция активации HTTP классифицирует твиты как зеленый, желтый или красный, на основе показателя мнений hello.</span><span class="sxs-lookup"><span data-stu-id="89176-108">An HTTP triggered function categorizes tweets as green, yellow, or red based on hello sentiment score.</span></span> <span data-ttu-id="89176-109">При обнаружении недопустимого мнения отправляется электронное сообщение.</span><span class="sxs-lookup"><span data-stu-id="89176-109">An email is sent when poor sentiment is detected.</span></span> 

![Изображение первых двух действий приложения в конструкторе приложений логики](media/functions-twitter-email/designer1.png)

<span data-ttu-id="89176-111">Из этого руководства вы узнаете, как выполнять такие задачи:</span><span class="sxs-lookup"><span data-stu-id="89176-111">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="89176-112">Создайте учетную запись Cognitive Services.</span><span class="sxs-lookup"><span data-stu-id="89176-112">Create a Cognitive Services account.</span></span>
> * <span data-ttu-id="89176-113">Создание функции, классифицирующей мнения, выраженные в твитах.</span><span class="sxs-lookup"><span data-stu-id="89176-113">Create a function that categorizes tweet sentiment.</span></span>
> * <span data-ttu-id="89176-114">Создайте логику приложения, которое подключается tooTwitter.</span><span class="sxs-lookup"><span data-stu-id="89176-114">Create a logic app that connects tooTwitter.</span></span>
> * <span data-ttu-id="89176-115">Добавление мнений обнаружения toohello логику приложения.</span><span class="sxs-lookup"><span data-stu-id="89176-115">Add sentiment detection toohello logic app.</span></span> 
> * <span data-ttu-id="89176-116">Hello логику приложения toohello функции соединения.</span><span class="sxs-lookup"><span data-stu-id="89176-116">Connect hello logic app toohello function.</span></span>
> * <span data-ttu-id="89176-117">Отправьте сообщение электронной почты, на основании hello ответа от функции hello.</span><span class="sxs-lookup"><span data-stu-id="89176-117">Send an email based on hello response from hello function.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="89176-118">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="89176-118">Prerequisites</span></span>

+ <span data-ttu-id="89176-119">Активная учетная запись [Twitter](https://twitter.com/).</span><span class="sxs-lookup"><span data-stu-id="89176-119">An active [Twitter](https://twitter.com/) account.</span></span> 
+ <span data-ttu-id="89176-120">Учетная запись [Outlook.com](https://outlook.com/) (для отправки уведомлений).</span><span class="sxs-lookup"><span data-stu-id="89176-120">An [Outlook.com](https://outlook.com/) account (for sending notifications).</span></span>
+ <span data-ttu-id="89176-121">В этом разделе используется как его начала ресурсы hello точки, созданные в [создания первой функции из портала Azure hello](functions-create-first-azure-function.md).</span><span class="sxs-lookup"><span data-stu-id="89176-121">This topic uses as its starting point hello resources created in [Create your first function from hello Azure portal](functions-create-first-azure-function.md).</span></span>  
<span data-ttu-id="89176-122">Если это еще не сделано, выполните toocreate теперь эти действия функции приложения.</span><span class="sxs-lookup"><span data-stu-id="89176-122">If you haven't already done so, complete these steps now toocreate your function app.</span></span>

## <a name="create-a-cognitive-services-account"></a><span data-ttu-id="89176-123">Создание учетной записи Cognitive Services</span><span class="sxs-lookup"><span data-stu-id="89176-123">Create a Cognitive Services account</span></span>

<span data-ttu-id="89176-124">Учетная запись службы Когнитивных — идея hello необходимые toodetect твиты отслеживается.</span><span class="sxs-lookup"><span data-stu-id="89176-124">A Cognitive Services account is required toodetect hello sentiment of tweets being monitored.</span></span>

1. <span data-ttu-id="89176-125">Войдите в toohello [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="89176-125">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>

2. <span data-ttu-id="89176-126">Нажмите кнопку hello **New** кнопка найдена в верхнем левом углу hello hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="89176-126">Click hello **New** button found on hello upper left-hand corner of hello Azure portal.</span></span>

3. <span data-ttu-id="89176-127">Щелкните **Данные+аналитика** > **Cognitive Services**.</span><span class="sxs-lookup"><span data-stu-id="89176-127">Click **Data + Analytics** > **Cognitive  Services**.</span></span> <span data-ttu-id="89176-128">Затем использовать hello параметры, как указано в таблице hello, примите условия hello и проверьте **toodashboard ПИН-кода**.</span><span class="sxs-lookup"><span data-stu-id="89176-128">Then, use hello settings as specified in hello table, accept hello terms, and check **Pin toodashboard**.</span></span>

    ![Колонка создания учетной записи Cognitive Services](media/functions-twitter-email/cog_svcs_account.png)

    | <span data-ttu-id="89176-130">Настройка</span><span class="sxs-lookup"><span data-stu-id="89176-130">Setting</span></span>      |  <span data-ttu-id="89176-131">Рекомендуемое значение</span><span class="sxs-lookup"><span data-stu-id="89176-131">Suggested value</span></span>   | <span data-ttu-id="89176-132">Описание</span><span class="sxs-lookup"><span data-stu-id="89176-132">Description</span></span>                                        |
    | --- | --- | --- |
    | <span data-ttu-id="89176-133">**Имя**</span><span class="sxs-lookup"><span data-stu-id="89176-133">**Name**</span></span> | <span data-ttu-id="89176-134">MyCognitiveServicesAccnt</span><span class="sxs-lookup"><span data-stu-id="89176-134">MyCognitiveServicesAccnt</span></span> | <span data-ttu-id="89176-135">Выберите уникальное имя учетной записи.</span><span class="sxs-lookup"><span data-stu-id="89176-135">Choose a unique account name.</span></span> |
    | <span data-ttu-id="89176-136">**Тип API.**</span><span class="sxs-lookup"><span data-stu-id="89176-136">**API type**</span></span> | <span data-ttu-id="89176-137">API анализа текста</span><span class="sxs-lookup"><span data-stu-id="89176-137">Text Analytics API</span></span> | <span data-ttu-id="89176-138">API используемого tooanalyze текста.</span><span class="sxs-lookup"><span data-stu-id="89176-138">API used tooanalyze text.</span></span>  |
    | <span data-ttu-id="89176-139">**Расположение**</span><span class="sxs-lookup"><span data-stu-id="89176-139">**Location**</span></span> | <span data-ttu-id="89176-140">Запад США</span><span class="sxs-lookup"><span data-stu-id="89176-140">West US</span></span> | <span data-ttu-id="89176-141">Сейчас для анализа текста доступен только регион **западная часть США**.</span><span class="sxs-lookup"><span data-stu-id="89176-141">Currently, only **West US** is available for text analytics.</span></span> |
    | <span data-ttu-id="89176-142">**Ценовая категория**</span><span class="sxs-lookup"><span data-stu-id="89176-142">**Pricing tier**</span></span> | <span data-ttu-id="89176-143">F0</span><span class="sxs-lookup"><span data-stu-id="89176-143">F0</span></span> | <span data-ttu-id="89176-144">Начните с hello нижнего уровня.</span><span class="sxs-lookup"><span data-stu-id="89176-144">Start with hello lowest tier.</span></span> <span data-ttu-id="89176-145">При запуске из вызовов, масштабируйте tooa высокого уровня.</span><span class="sxs-lookup"><span data-stu-id="89176-145">If you run out of calls, scale tooa higher tier.</span></span>|
    | <span data-ttu-id="89176-146">**Группа ресурсов**</span><span class="sxs-lookup"><span data-stu-id="89176-146">**Resource group**</span></span> | <span data-ttu-id="89176-147">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="89176-147">myResourceGroup</span></span> | <span data-ttu-id="89176-148">Используйте hello же группу ресурсов для всех служб в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="89176-148">Use hello same resource group for all services in this tutorial.</span></span>|

4. <span data-ttu-id="89176-149">Нажмите кнопку **создать** toocreate вашей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="89176-149">Click **Create** toocreate your account.</span></span> <span data-ttu-id="89176-150">После создания учетной записи hello щелкните новой панели мониторинга закрепленных toohello Когнитивных службы учетной записи.</span><span class="sxs-lookup"><span data-stu-id="89176-150">After hello account is created, click your new Cognitive Services account pinned toohello dashboard.</span></span> 

5. <span data-ttu-id="89176-151">Hello учетную запись, нажмите кнопку **ключи**, а затем скопируйте значение hello **раздел 1** и сохраните его.</span><span class="sxs-lookup"><span data-stu-id="89176-151">In hello account, click **Keys**, and then copy hello value of **Key 1** and save it.</span></span> <span data-ttu-id="89176-152">Использовании этого ключа tooconnect hello логику приложения tooyour Когнитивных службы учетной записи.</span><span class="sxs-lookup"><span data-stu-id="89176-152">You use this key tooconnect hello logic app tooyour Cognitive Services account.</span></span> 
 
    ![ключей](media/functions-twitter-email/keys.png)

## <a name="create-hello-function"></a><span data-ttu-id="89176-154">Создание функции hello</span><span class="sxs-lookup"><span data-stu-id="89176-154">Create hello function</span></span>

<span data-ttu-id="89176-155">Функции предоставляет toooffload хорошим способом обработки задач в рабочем процессе логику приложения.</span><span class="sxs-lookup"><span data-stu-id="89176-155">Functions provides a great way toooffload processing tasks in a logic apps workflow.</span></span> <span data-ttu-id="89176-156">В этом учебнике используется HTTP при запуске функции tooprocess твит мнений показатели Когнитивных службы и возвращают значения категории.</span><span class="sxs-lookup"><span data-stu-id="89176-156">This tutorial uses an HTTP triggered function tooprocess tweet sentiment scores from Cognitive Services and return a category value.</span></span>  

1. <span data-ttu-id="89176-157">Функции приложения, щелкните hello  **+**  рядом слишком**функции**, нажмите кнопку hello **HTTPTrigger** шаблона.</span><span class="sxs-lookup"><span data-stu-id="89176-157">Expand your function app, click hello **+** button next too**Functions**, click hello **HTTPTrigger** template.</span></span> <span data-ttu-id="89176-158">Тип `CategorizeSentiment` для функции hello **имя** и нажмите кнопку **создать**.</span><span class="sxs-lookup"><span data-stu-id="89176-158">Type `CategorizeSentiment` for hello function **Name** and click **Create**.</span></span>

    ![Колонка приложения-функции, добавление функции](media/functions-twitter-email/add_fun.png)

2. <span data-ttu-id="89176-160">Замените содержимое файла run.csx hello hello hello после кода, а затем нажмите кнопку **Сохранить**:</span><span class="sxs-lookup"><span data-stu-id="89176-160">Replace hello contents of hello run.csx file with hello following code, then click **Save**:</span></span>

    ```c#
    using System.Net;
    
    public static async Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
    {
        // hello sentiment category defaults too'GREEN'. 
        string category = "GREEN";
    
        // Get hello sentiment score from hello request body.
        double score = await req.Content.ReadAsAsync<double>();
        log.Info(string.Format("hello sentiment score received is '{0}'.",
                    score.ToString()));
    
        // Set hello category based on hello sentiment score.
        if (score < .3)
        {
            category = "RED";
        }
        else if (score < .6)
        {
            category = "YELLOW";
        }
        return req.CreateResponse(HttpStatusCode.OK, category);
    }
    ```
    <span data-ttu-id="89176-161">Этот код функции возвращает цветовую категорию на основе показателя мнений hello, получено в запросе hello.</span><span class="sxs-lookup"><span data-stu-id="89176-161">This function code returns a color category based on hello sentiment score received in hello request.</span></span> 

3. <span data-ttu-id="89176-162">функция tootest hello, нажмите кнопку **тест** hello правого tooexpand hello теста вкладку в. Введите значение `0.2` для hello **текст запроса**, а затем нажмите кнопку **запуска**.</span><span class="sxs-lookup"><span data-stu-id="89176-162">tootest hello function, click **Test** at hello far right tooexpand hello Test tab. Type a value of `0.2` for hello **Request body**, and then click **Run**.</span></span> <span data-ttu-id="89176-163">Значение **RED** возвращается в тексте hello hello ответа.</span><span class="sxs-lookup"><span data-stu-id="89176-163">A value of **RED** is returned in hello body of hello response.</span></span> 

    ![Проверка функции hello в hello портал Azure](./media/functions-twitter-email/test.png)

<span data-ttu-id="89176-165">Теперь у вас есть функция, классифицирующая оценку мнений.</span><span class="sxs-lookup"><span data-stu-id="89176-165">Now you have a function that categorizes sentiment scores.</span></span> <span data-ttu-id="89176-166">Создайте приложение логики, интегрирующее функцию с учетными записями Twitter и Cognitive Services.</span><span class="sxs-lookup"><span data-stu-id="89176-166">Next, you create a logic app that integrates your function with your Twitter and Cognitive Services accounts.</span></span> 

## <a name="create-a-logic-app"></a><span data-ttu-id="89176-167">Создайте приложение логики</span><span class="sxs-lookup"><span data-stu-id="89176-167">Create a logic app</span></span>   

1. <span data-ttu-id="89176-168">В hello портал Azure, щелкнув hello **New** кнопка найдена в верхнем левом углу hello hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="89176-168">In hello Azure portal, click hello **New** button found on hello upper left-hand corner of hello Azure portal.</span></span>

2. <span data-ttu-id="89176-169">Щелкните **Интеграция Enterprise** > **Приложение логики**.</span><span class="sxs-lookup"><span data-stu-id="89176-169">Click **Enterprise Integration** > **Logic App**.</span></span> <span data-ttu-id="89176-170">Затем проверьте параметры использования hello как, указанные в таблице hello **toodashboard ПИН-код**и нажмите кнопку **создать**.</span><span class="sxs-lookup"><span data-stu-id="89176-170">Then, use hello settings as specified in hello table, check **Pin toodashboard**, and click **Create**.</span></span>
 
4. <span data-ttu-id="89176-171">Введите **имя** как `TweetSentiment`, использовать параметры hello, как указано в таблице hello, примите условия hello и проверьте **toodashboard ПИН-кода**.</span><span class="sxs-lookup"><span data-stu-id="89176-171">Then, type a **Name** like `TweetSentiment`,  use hello settings as specified in hello table, accept hello terms, and check **Pin toodashboard**.</span></span>

    ![Создание приложения логики в hello портал Azure](./media/functions-twitter-email/new_logicApp.png)

    | <span data-ttu-id="89176-173">Настройка</span><span class="sxs-lookup"><span data-stu-id="89176-173">Setting</span></span>      |  <span data-ttu-id="89176-174">Рекомендуемое значение</span><span class="sxs-lookup"><span data-stu-id="89176-174">Suggested value</span></span>   | <span data-ttu-id="89176-175">Описание</span><span class="sxs-lookup"><span data-stu-id="89176-175">Description</span></span>                                        |
    | ----------------- | ------------ | ------------- |
    | <span data-ttu-id="89176-176">**Имя**</span><span class="sxs-lookup"><span data-stu-id="89176-176">**Name**</span></span> | <span data-ttu-id="89176-177">TweetSentiment</span><span class="sxs-lookup"><span data-stu-id="89176-177">TweetSentiment</span></span> | <span data-ttu-id="89176-178">Выберите соответствующее имя для своего приложения.</span><span class="sxs-lookup"><span data-stu-id="89176-178">Choose an appropriate name for your app.</span></span> |
    | <span data-ttu-id="89176-179">**Группа ресурсов**</span><span class="sxs-lookup"><span data-stu-id="89176-179">**Resource group**</span></span> | <span data-ttu-id="89176-180">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="89176-180">myResourceGroup</span></span> | <span data-ttu-id="89176-181">API используемого tooanalyze текста.</span><span class="sxs-lookup"><span data-stu-id="89176-181">API used tooanalyze text.</span></span>  |
    | <span data-ttu-id="89176-182">**Расположение**</span><span class="sxs-lookup"><span data-stu-id="89176-182">**Location**</span></span> | <span data-ttu-id="89176-183">Восток США</span><span class="sxs-lookup"><span data-stu-id="89176-183">East US</span></span> | <span data-ttu-id="89176-184">Выберите расположение закрыть tooyou.</span><span class="sxs-lookup"><span data-stu-id="89176-184">Choose a location close tooyou.</span></span> |
    | <span data-ttu-id="89176-185">**Группа ресурсов**</span><span class="sxs-lookup"><span data-stu-id="89176-185">**Resource group**</span></span> | <span data-ttu-id="89176-186">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="89176-186">myResourceGroup</span></span> | <span data-ttu-id="89176-187">Выберите hello же существующую группу ресурсов, как и раньше.</span><span class="sxs-lookup"><span data-stu-id="89176-187">Choose hello same existing resource group as before.</span></span>|

4. <span data-ttu-id="89176-188">Нажмите кнопку **создать** toocreate логику приложения.</span><span class="sxs-lookup"><span data-stu-id="89176-188">Click **Create** toocreate your logic app.</span></span> <span data-ttu-id="89176-189">После создания приложения hello щелкните новой панели мониторинга закрепленных toohello логику приложения.</span><span class="sxs-lookup"><span data-stu-id="89176-189">After hello app is created, click your new logic app pinned toohello dashboard.</span></span> <span data-ttu-id="89176-190">Затем в hello конструктора логики приложения, прокрутите вниз и нажмите кнопку hello **пустое приложение логики** шаблона.</span><span class="sxs-lookup"><span data-stu-id="89176-190">Then in hello Logic Apps Designer, scroll down and click hello **Blank Logic App** template.</span></span> 

    ![Шаблон "Пустое приложение логики" Logic Apps](media/functions-twitter-email/blank.png)

<span data-ttu-id="89176-192">Теперь можно использовать конструктор приложений логики tooadd службы и триггеры tooyour приложение hello.</span><span class="sxs-lookup"><span data-stu-id="89176-192">You can now use hello Logic Apps Designer tooadd services and triggers tooyour app.</span></span>

## <a name="connect-tootwitter"></a><span data-ttu-id="89176-193">Подключение tooTwitter</span><span class="sxs-lookup"><span data-stu-id="89176-193">Connect tooTwitter</span></span>

<span data-ttu-id="89176-194">Сначала необходимо создаете соединение tooyour учетную запись Twitter.</span><span class="sxs-lookup"><span data-stu-id="89176-194">First, create a connection tooyour Twitter account.</span></span> <span data-ttu-id="89176-195">приложения логики Hello запрашивает твиты, которые триггер toorun приложения hello.</span><span class="sxs-lookup"><span data-stu-id="89176-195">hello logic app polls for tweets, which trigger hello app toorun.</span></span>

1. <span data-ttu-id="89176-196">В конструкторе hello щелкните hello **Twitter** службы и нажмите кнопку hello **при учете новый твит** триггера.</span><span class="sxs-lookup"><span data-stu-id="89176-196">In hello designer, click hello **Twitter** service, and click hello **When a new tweet is posted** trigger.</span></span> <span data-ttu-id="89176-197">Войдите в учетную запись Twitter tooyour и авторизуйте toouse Logic Apps вашей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="89176-197">Sign in tooyour Twitter account and authorize Logic Apps toouse your account.</span></span>

2. <span data-ttu-id="89176-198">Используйте параметры триггера hello Twitter, как указано в таблице hello.</span><span class="sxs-lookup"><span data-stu-id="89176-198">Use hello Twitter trigger settings as specified in hello table.</span></span> 

    ![Параметры соединителя Twitter](media/functions-twitter-email/azure_tweet.png)

    | <span data-ttu-id="89176-200">Настройка</span><span class="sxs-lookup"><span data-stu-id="89176-200">Setting</span></span>      |  <span data-ttu-id="89176-201">Рекомендуемое значение</span><span class="sxs-lookup"><span data-stu-id="89176-201">Suggested value</span></span>   | <span data-ttu-id="89176-202">Описание</span><span class="sxs-lookup"><span data-stu-id="89176-202">Description</span></span>                                        |
    | ----------------- | ------------ | ------------- |
    | <span data-ttu-id="89176-203">**Текст поискового запроса**</span><span class="sxs-lookup"><span data-stu-id="89176-203">**Search text**</span></span> | <span data-ttu-id="89176-204">#Azure</span><span class="sxs-lookup"><span data-stu-id="89176-204">#Azure</span></span> | <span data-ttu-id="89176-205">Используйте хэштегом, который популярен достаточно для нового твиты toogenerate hello выбранного интервала.</span><span class="sxs-lookup"><span data-stu-id="89176-205">Use a hashtag that is popular enough for toogenerate new tweets in hello chosen interval.</span></span> <span data-ttu-id="89176-206">При использовании бесплатный уровень hello и вашей хэштегом слишком популярных, можно быстро использовать hello транзакций в вашей учетной записи службы Когнитивных.</span><span class="sxs-lookup"><span data-stu-id="89176-206">When using hello Free tier and your hashtag is too popular, you can quickly use up hello transactions in your Cognitive Services account.</span></span> |
    | <span data-ttu-id="89176-207">**Frequency**</span><span class="sxs-lookup"><span data-stu-id="89176-207">**Frequency**</span></span> | <span data-ttu-id="89176-208">Минута</span><span class="sxs-lookup"><span data-stu-id="89176-208">Minute</span></span> | <span data-ttu-id="89176-209">Hello частоты единица, используемая для опроса Twitter.</span><span class="sxs-lookup"><span data-stu-id="89176-209">hello frequency unit used for polling Twitter.</span></span>  |
    | <span data-ttu-id="89176-210">**Интервал**</span><span class="sxs-lookup"><span data-stu-id="89176-210">**Interval**</span></span> | <span data-ttu-id="89176-211">15</span><span class="sxs-lookup"><span data-stu-id="89176-211">15</span></span> | <span data-ttu-id="89176-212">Hello время, прошедшее между единиц частоты запросов Twitter.</span><span class="sxs-lookup"><span data-stu-id="89176-212">hello time elapsed between Twitter requests, in frequency units.</span></span> |

3.  <span data-ttu-id="89176-213">Нажмите кнопку **Сохранить** tooconnect tooyour учетную запись Twitter.</span><span class="sxs-lookup"><span data-stu-id="89176-213">Click **Save** tooconnect tooyour Twitter account.</span></span> 

<span data-ttu-id="89176-214">Теперь приложение будет подключенных tooTwitter.</span><span class="sxs-lookup"><span data-stu-id="89176-214">Now your app is connected tooTwitter.</span></span> <span data-ttu-id="89176-215">Затем вы подключения tootext toodetect analytics hello идея собранных твиты.</span><span class="sxs-lookup"><span data-stu-id="89176-215">Next, you connect tootext analytics toodetect hello sentiment of collected tweets.</span></span>

## <a name="add-sentiment-detection"></a><span data-ttu-id="89176-216">Добавление определения мнений</span><span class="sxs-lookup"><span data-stu-id="89176-216">Add sentiment detection</span></span>

1. <span data-ttu-id="89176-217">Щелкните **New Step** (Создать шаг), а затем — **Добавить действие**.</span><span class="sxs-lookup"><span data-stu-id="89176-217">Click **New Step**, and then **Add an action**.</span></span>

    ![Выбор действий "Новый шаг" и "Добавить действие"](media/functions-twitter-email/new_step.png)

2. <span data-ttu-id="89176-219">В **выбрать действия**, нажмите кнопку **анализа текста**и нажмите кнопку hello **обнаружить мнений** действие.</span><span class="sxs-lookup"><span data-stu-id="89176-219">In **Choose an action**, click **Text Analytics**, and then click hello **Detect sentiment** action.</span></span>

    ![Определение мнений](media/functions-twitter-email/detect_sent.png)

3. <span data-ttu-id="89176-221">Введите имя подключения, например `MyCognitiveServicesConnection`, вставьте hello ключ для учетной записи Когнитивных служб, которые сохранены и нажмите кнопку **создать**.</span><span class="sxs-lookup"><span data-stu-id="89176-221">Type a connection name such as `MyCognitiveServicesConnection`, paste hello key for your Cognitive Services account that you saved, and click **Create**.</span></span>  

4. <span data-ttu-id="89176-222">Нажмите кнопку **tooanalyze текст** > **твит текст**, а затем нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="89176-222">Click **Text tooanalyze** > **Tweet text**, and then click **Save**.</span></span>  

    ![Определение мнений](media/functions-twitter-email/ds_tta.png)

<span data-ttu-id="89176-224">Теперь, когда настроено выявление мнений, можно добавить функции tooyour соединение, использующее вывода показатель мнений hello.</span><span class="sxs-lookup"><span data-stu-id="89176-224">Now that sentiment detection is configured, you can add a connection tooyour function that consumes hello sentiment score output.</span></span>

## <a name="connect-sentiment-output-tooyour-function"></a><span data-ttu-id="89176-225">Функции tooyour мнений выходные данные соединения</span><span class="sxs-lookup"><span data-stu-id="89176-225">Connect sentiment output tooyour function</span></span>

1. <span data-ttu-id="89176-226">В hello конструктора логики приложения, щелкните **новый шаг** > **добавить действие**и нажмите кнопку **функции Azure**.</span><span class="sxs-lookup"><span data-stu-id="89176-226">In hello Logic Apps Designer, click **New step** > **Add an action**, and then click **Azure Functions**.</span></span> 

2. <span data-ttu-id="89176-227">Нажмите кнопку **выберите Azure функцию**выберите hello **CategorizeSentiment** функция, было создано ранее.</span><span class="sxs-lookup"><span data-stu-id="89176-227">Click **Choose an Azure function**, select hello **CategorizeSentiment** function you created earlier.</span></span>  

    ![Окно с функцией Azure и параметром "Выберите функцию Azure"](media/functions-twitter-email/choose_fun.png)

3. <span data-ttu-id="89176-229">В разделе **Текст запроса** щелкните кнопку **Score** (Оценка) и **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="89176-229">In **Request Body**, click **Score** and then **Save**.</span></span>

    ![Оценка](media/functions-twitter-email/trigger_score.png)

<span data-ttu-id="89176-231">Теперь ваша функция срабатывает, когда показатель мнений отправляется из логики приложения hello.</span><span class="sxs-lookup"><span data-stu-id="89176-231">Now, your function is triggered when a sentiment score is sent from hello logic app.</span></span> <span data-ttu-id="89176-232">Цветное категории возвращается приложения логики toohello функции hello.</span><span class="sxs-lookup"><span data-stu-id="89176-232">A color-coded category is returned toohello logic app by hello function.</span></span> <span data-ttu-id="89176-233">Затем добавьте уведомление по электронной почте, отправляемых, когда значение мнений **RED** возвращается из функции hello.</span><span class="sxs-lookup"><span data-stu-id="89176-233">Next, you add an email notification that is sent when a sentiment value of **RED** is returned from hello function.</span></span> 

## <a name="add-email-notifications"></a><span data-ttu-id="89176-234">Добавление уведомлений по почте</span><span class="sxs-lookup"><span data-stu-id="89176-234">Add email notifications</span></span>

<span data-ttu-id="89176-235">Последняя часть Hello hello рабочего процесса является tootrigger сообщение электронной почты при мнений hello, оценивается как _RED_.</span><span class="sxs-lookup"><span data-stu-id="89176-235">hello last part of hello workflow is tootrigger an email when hello sentiment is scored as _RED_.</span></span> <span data-ttu-id="89176-236">В этом разделе использует соединитель Outlook.com.</span><span class="sxs-lookup"><span data-stu-id="89176-236">This topic uses an Outlook.com connector.</span></span> <span data-ttu-id="89176-237">Можно выполнить аналогичные шаги toouse соединитель Gmail или Office 365 Outlook.</span><span class="sxs-lookup"><span data-stu-id="89176-237">You can perform similar steps toouse a Gmail or Office 365 Outlook connector.</span></span>   

1. <span data-ttu-id="89176-238">В hello конструктора логики приложения, щелкните **новый шаг** > **добавить условие**.</span><span class="sxs-lookup"><span data-stu-id="89176-238">In hello Logic Apps Designer, click **New step** > **Add a condition**.</span></span> 

2. <span data-ttu-id="89176-239">Щелкните **Выберите значение**, а затем — **Текст**.</span><span class="sxs-lookup"><span data-stu-id="89176-239">Click **Choose a value**, then click **Body**.</span></span> <span data-ttu-id="89176-240">Выберите **равняется**, щелкните **Выберите значение**, введите `RED` и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="89176-240">Select **is equal to**, click **Choose a value** and type `RED`, and click **Save**.</span></span> 

    ![Добавьте условие toohello логику приложения.](media/functions-twitter-email/condition.png)

3. <span data-ttu-id="89176-242">В **Если Да, НИЧЕГО не**, нажмите кнопку **добавить действие**, поиск `outlook.com`, нажмите кнопку **отправить сообщение электронной почты**и выполните вход tooyour Outlook.com учетной записи.</span><span class="sxs-lookup"><span data-stu-id="89176-242">In **IF YES, DO NOTHING**, click **Add an action**, search for `outlook.com`, click **Send an email**, and sign in tooyour Outlook.com account.</span></span>
    
    ![Выберите действие для hello условия.](media/functions-twitter-email/outlook.png)

    > [!NOTE]
    > <span data-ttu-id="89176-244">Если у вас нет учетной записи Outlook.com, можно выбрать другой соединитель, например Gmail или Office 365 Outlook</span><span class="sxs-lookup"><span data-stu-id="89176-244">If you don't have an Outlook.com account, you can choose another connector, such as Gmail or Office 365 Outlook</span></span>

4. <span data-ttu-id="89176-245">В hello **отправить сообщение электронной почты** действия, параметры электронной почты используйте hello как, указанные в таблице hello.</span><span class="sxs-lookup"><span data-stu-id="89176-245">In hello **Send an email** action, use hello email settings as specified in hello table.</span></span> 

    ![Настройте hello электронной почты для отправки hello действия электронной почты.](media/functions-twitter-email/sendemail.png)

    | <span data-ttu-id="89176-247">Настройка</span><span class="sxs-lookup"><span data-stu-id="89176-247">Setting</span></span>      |  <span data-ttu-id="89176-248">Рекомендуемое значение</span><span class="sxs-lookup"><span data-stu-id="89176-248">Suggested value</span></span>   | <span data-ttu-id="89176-249">Описание</span><span class="sxs-lookup"><span data-stu-id="89176-249">Description</span></span>  |
    | ----------------- | ------------ | ------------- |
    | <span data-ttu-id="89176-250">**To**</span><span class="sxs-lookup"><span data-stu-id="89176-250">**To**</span></span> | <span data-ttu-id="89176-251">Введите адрес электронной почты</span><span class="sxs-lookup"><span data-stu-id="89176-251">Type your email address</span></span> | <span data-ttu-id="89176-252">Hello адрес электронной почты, который получает уведомление о hello.</span><span class="sxs-lookup"><span data-stu-id="89176-252">hello email address that receives hello notification.</span></span> |
    | <span data-ttu-id="89176-253">**Тема**</span><span class="sxs-lookup"><span data-stu-id="89176-253">**Subject**</span></span> | <span data-ttu-id="89176-254">Negative tweet sentiment detected (Обнаружено отрицательное мнение, выраженное в твите)</span><span class="sxs-lookup"><span data-stu-id="89176-254">Negative tweet sentiment detected</span></span>  | <span data-ttu-id="89176-255">Строка темы Hello hello уведомления по электронной почте.</span><span class="sxs-lookup"><span data-stu-id="89176-255">hello subject line of hello email notification.</span></span>  |
    | <span data-ttu-id="89176-256">**Текст**</span><span class="sxs-lookup"><span data-stu-id="89176-256">**Body**</span></span> | <span data-ttu-id="89176-257">"Текст твита", "Расположение"</span><span class="sxs-lookup"><span data-stu-id="89176-257">Tweet text, Location</span></span> | <span data-ttu-id="89176-258">Нажмите кнопку hello **твит текст** и **расположение** параметров.</span><span class="sxs-lookup"><span data-stu-id="89176-258">Click hello **Tweet text** and **Location** parameters.</span></span> |

5.  <span data-ttu-id="89176-259">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="89176-259">Click **Save**.</span></span>

<span data-ttu-id="89176-260">Теперь, когда hello рабочий процесс будет завершен, можно включить логику приложения hello и в описании функции hello на работе.</span><span class="sxs-lookup"><span data-stu-id="89176-260">Now that hello workflow is complete, you can enable hello logic app and see hello function at work.</span></span>

## <a name="test-hello-workflow"></a><span data-ttu-id="89176-261">Рабочий процесс теста hello</span><span class="sxs-lookup"><span data-stu-id="89176-261">Test hello workflow</span></span>

1. <span data-ttu-id="89176-262">В hello конструктор логики приложения, щелкните **запуска** toostart приложение hello.</span><span class="sxs-lookup"><span data-stu-id="89176-262">In hello Logic App Designer, click **Run** toostart hello app.</span></span>

2. <span data-ttu-id="89176-263">В левом столбце hello, щелкните **Обзор** toosee состояние hello hello логику приложения.</span><span class="sxs-lookup"><span data-stu-id="89176-263">In hello left column, click **Overview** toosee hello status of hello logic app.</span></span> 
 
    ![Состояние выполнения приложения логики](media/functions-twitter-email/over1.png)

3. <span data-ttu-id="89176-265">(Необязательно) Выберите один из hello запусков toosee подробности выполнения hello.</span><span class="sxs-lookup"><span data-stu-id="89176-265">(Optional) Click one of hello runs toosee details of hello execution.</span></span>

4. <span data-ttu-id="89176-266">Go tooyour функции, просмотрите журналы hello и убедитесь, что значения мнений были получены и обработаны.</span><span class="sxs-lookup"><span data-stu-id="89176-266">Go tooyour function, view hello logs, and verify that sentiment values were received and processed.</span></span>
 
    ![Просмотр журналов функции](media/functions-twitter-email/sent.png)

5. <span data-ttu-id="89176-268">При обнаружении потенциально негативного мнения вы получите электронное сообщение.</span><span class="sxs-lookup"><span data-stu-id="89176-268">When a potentially negative sentiment is detected, you receive an email.</span></span> <span data-ttu-id="89176-269">Если вы еще не получили сообщение электронной почты, можно изменить tooreturn кода функции hello красный каждый раз:</span><span class="sxs-lookup"><span data-stu-id="89176-269">If you haven't received an email, you can change hello function code tooreturn RED every time:</span></span>

        return req.CreateResponse(HttpStatusCode.OK, "RED");

    <span data-ttu-id="89176-270">После проверки уведомления по электронной почте, измените задней toohello исходный код:</span><span class="sxs-lookup"><span data-stu-id="89176-270">After you have verified email notifications, change back toohello original code:</span></span>

        return req.CreateResponse(HttpStatusCode.OK, category);

    > [!IMPORTANT]
    > <span data-ttu-id="89176-271">После завершения этого учебника, следует отключить приложение hello логику.</span><span class="sxs-lookup"><span data-stu-id="89176-271">After you have completed this tutorial, you should disable hello logic app.</span></span> <span data-ttu-id="89176-272">Отключение приложение hello, можно избежать, сняты выполнений и по использованию транзакций hello в вашей учетной записи службы Когнитивных.</span><span class="sxs-lookup"><span data-stu-id="89176-272">By disabling hello app, you avoid being charged for executions and using up hello transactions in your Cognitive Services account.</span></span>

<span data-ttu-id="89176-273">Теперь вы уже узнали, как просто можно toointegrate функции в рабочем процессе приложения логики.</span><span class="sxs-lookup"><span data-stu-id="89176-273">Now you have seen how easy it is toointegrate Functions into a Logic Apps workflow.</span></span>

## <a name="disable-hello-logic-app"></a><span data-ttu-id="89176-274">Отключить приложение логики hello</span><span class="sxs-lookup"><span data-stu-id="89176-274">Disable hello logic app</span></span>

<span data-ttu-id="89176-275">приложения логики toodisable hello, нажмите кнопку **Обзор** и нажмите кнопку **отключить** hello верхней части экрана приветствия.</span><span class="sxs-lookup"><span data-stu-id="89176-275">toodisable hello logic app, click **Overview** and then click **Disable** at hello top of hello screen.</span></span> <span data-ttu-id="89176-276">Это предотвратит hello логики приложения, запускать и взимается плата, не удаляя приложение hello.</span><span class="sxs-lookup"><span data-stu-id="89176-276">This stops hello logic app from running and incurring charges without deleting hello app.</span></span> 

![Журналы функций](media/functions-twitter-email/disable-logic-app.png)

## <a name="next-steps"></a><span data-ttu-id="89176-278">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="89176-278">Next steps</span></span>

<span data-ttu-id="89176-279">Из этого руководства вы узнали, как выполнять такие задачи:</span><span class="sxs-lookup"><span data-stu-id="89176-279">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="89176-280">Создайте учетную запись Cognitive Services.</span><span class="sxs-lookup"><span data-stu-id="89176-280">Create a Cognitive Services account.</span></span>
> * <span data-ttu-id="89176-281">Создание функции, классифицирующей мнения, выраженные в твитах.</span><span class="sxs-lookup"><span data-stu-id="89176-281">Create a function that categorizes tweet sentiment.</span></span>
> * <span data-ttu-id="89176-282">Создайте логику приложения, которое подключается tooTwitter.</span><span class="sxs-lookup"><span data-stu-id="89176-282">Create a logic app that connects tooTwitter.</span></span>
> * <span data-ttu-id="89176-283">Добавление мнений обнаружения toohello логику приложения.</span><span class="sxs-lookup"><span data-stu-id="89176-283">Add sentiment detection toohello logic app.</span></span> 
> * <span data-ttu-id="89176-284">Hello логику приложения toohello функции соединения.</span><span class="sxs-lookup"><span data-stu-id="89176-284">Connect hello logic app toohello function.</span></span>
> * <span data-ttu-id="89176-285">Отправьте сообщение электронной почты, на основании hello ответа от функции hello.</span><span class="sxs-lookup"><span data-stu-id="89176-285">Send an email based on hello response from hello function.</span></span>

<span data-ttu-id="89176-286">Как переместить следующий учебник toolearn toohello toocreate без сервера API для функции.</span><span class="sxs-lookup"><span data-stu-id="89176-286">Advance toohello next tutorial toolearn how toocreate a serverless API for your function.</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="89176-287">Создание бессерверного API с помощью Функций Azure</span><span class="sxs-lookup"><span data-stu-id="89176-287">Create a serverless API using Azure Functions</span></span>](functions-create-serverless-api.md)

<span data-ttu-id="89176-288">toolearn Дополнительные сведения о приложении логики в разделе [приложения логики Azure](../logic-apps/logic-apps-what-are-logic-apps.md).</span><span class="sxs-lookup"><span data-stu-id="89176-288">toolearn more about Logic Apps, see [Azure Logic Apps](../logic-apps/logic-apps-what-are-logic-apps.md).</span></span>

