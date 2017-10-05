---
title: "Создание функции, интегрируемой с Azure Logic Apps | Документация Майкрософт"
description: "Создайте функцию, которая интегрируется с Azure Logic Apps и Azure Cognitive Services для классификации мнений в твитах и отправки уведомлений, если мнение недопустимо."
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
ms.openlocfilehash: 4a5dc668e21c5328b308c8f5852aaa922232374d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-function-that-integrates-with-azure-logic-apps"></a><span data-ttu-id="74eb6-104">Создание функции, интегрируемой с Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="74eb6-104">Create a function that integrates with Azure Logic Apps</span></span>

<span data-ttu-id="74eb6-105">Функции Azure интегрируются с Azure Logic Apps в конструкторе Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="74eb6-105">Azure Functions integrates with Azure Logic Apps in the Logic Apps Designer.</span></span> <span data-ttu-id="74eb6-106">Такая интеграция позволяет использовать вычислительную мощность Функций при оркестрации с другими службами Azure и сторонними службами.</span><span class="sxs-lookup"><span data-stu-id="74eb6-106">This integration lets you use the computing power of Functions in orchestrations with other Azure and third-party services.</span></span> 

<span data-ttu-id="74eb6-107">В этом руководстве показано, как анализировать мнения, выраженные в записях в Twitter, с помощью Функций, Logic Apps и Azure Cognitive Services.</span><span class="sxs-lookup"><span data-stu-id="74eb6-107">This tutorial shows you how to use Functions with Logic Apps and Azure Cognitive Services to analyze sentiment from Twitter posts.</span></span> <span data-ttu-id="74eb6-108">Функция, активируемая HTTP, классифицирует твиты на категории green, yellow или red на основе оценки мнения.</span><span class="sxs-lookup"><span data-stu-id="74eb6-108">An HTTP triggered function categorizes tweets as green, yellow, or red based on the sentiment score.</span></span> <span data-ttu-id="74eb6-109">При обнаружении недопустимого мнения отправляется электронное сообщение.</span><span class="sxs-lookup"><span data-stu-id="74eb6-109">An email is sent when poor sentiment is detected.</span></span> 

![Изображение первых двух действий приложения в конструкторе приложений логики](media/functions-twitter-email/designer1.png)

<span data-ttu-id="74eb6-111">Из этого руководства вы узнаете, как выполнять такие задачи:</span><span class="sxs-lookup"><span data-stu-id="74eb6-111">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="74eb6-112">Создайте учетную запись Cognitive Services.</span><span class="sxs-lookup"><span data-stu-id="74eb6-112">Create a Cognitive Services account.</span></span>
> * <span data-ttu-id="74eb6-113">Создание функции, классифицирующей мнения, выраженные в твитах.</span><span class="sxs-lookup"><span data-stu-id="74eb6-113">Create a function that categorizes tweet sentiment.</span></span>
> * <span data-ttu-id="74eb6-114">Создание приложения логики, подключающегося к Twitter.</span><span class="sxs-lookup"><span data-stu-id="74eb6-114">Create a logic app that connects to Twitter.</span></span>
> * <span data-ttu-id="74eb6-115">Добавление обнаружения мнений в приложение логики.</span><span class="sxs-lookup"><span data-stu-id="74eb6-115">Add sentiment detection to the logic app.</span></span> 
> * <span data-ttu-id="74eb6-116">Подключение приложения логики к функции.</span><span class="sxs-lookup"><span data-stu-id="74eb6-116">Connect the logic app to the function.</span></span>
> * <span data-ttu-id="74eb6-117">Отправка электронного сообщения в зависимости от ответа из функции.</span><span class="sxs-lookup"><span data-stu-id="74eb6-117">Send an email based on the response from the function.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="74eb6-118">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="74eb6-118">Prerequisites</span></span>

+ <span data-ttu-id="74eb6-119">Активная учетная запись [Twitter](https://twitter.com/).</span><span class="sxs-lookup"><span data-stu-id="74eb6-119">An active [Twitter](https://twitter.com/) account.</span></span> 
+ <span data-ttu-id="74eb6-120">Учетная запись [Outlook.com](https://outlook.com/) (для отправки уведомлений).</span><span class="sxs-lookup"><span data-stu-id="74eb6-120">An [Outlook.com](https://outlook.com/) account (for sending notifications).</span></span>
+ <span data-ttu-id="74eb6-121">В этой статье в качестве отправной точки используются ресурсы, созданные при работе со статьей [Создание первой функции на портале Azure](functions-create-first-azure-function.md).</span><span class="sxs-lookup"><span data-stu-id="74eb6-121">This topic uses as its starting point the resources created in [Create your first function from the Azure portal](functions-create-first-azure-function.md).</span></span>  
<span data-ttu-id="74eb6-122">Выполните шаги в этой статье для создания приложения-функции, если вы еще не сделали этого.</span><span class="sxs-lookup"><span data-stu-id="74eb6-122">If you haven't already done so, complete these steps now to create your function app.</span></span>

## <a name="create-a-cognitive-services-account"></a><span data-ttu-id="74eb6-123">Создание учетной записи Cognitive Services</span><span class="sxs-lookup"><span data-stu-id="74eb6-123">Create a Cognitive Services account</span></span>

<span data-ttu-id="74eb6-124">Учетная запись Cognitive Services необходима, чтобы определить мнения, выраженные в твитах, которые мы отслеживаем.</span><span class="sxs-lookup"><span data-stu-id="74eb6-124">A Cognitive Services account is required to detect the sentiment of tweets being monitored.</span></span>

1. <span data-ttu-id="74eb6-125">Выполните вход на [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="74eb6-125">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>

2. <span data-ttu-id="74eb6-126">Щелкните **Создать** в верхнем левом углу портала Azure.</span><span class="sxs-lookup"><span data-stu-id="74eb6-126">Click the **New** button found on the upper left-hand corner of the Azure portal.</span></span>

3. <span data-ttu-id="74eb6-127">Щелкните **Данные+аналитика** > **Cognitive Services**.</span><span class="sxs-lookup"><span data-stu-id="74eb6-127">Click **Data + Analytics** > **Cognitive  Services**.</span></span> <span data-ttu-id="74eb6-128">Затем используйте параметры, указанные в таблице, примите условия и установите флажок **Закрепить на панели мониторинга**.</span><span class="sxs-lookup"><span data-stu-id="74eb6-128">Then, use the settings as specified in the table, accept the terms, and check **Pin to dashboard**.</span></span>

    ![Колонка создания учетной записи Cognitive Services](media/functions-twitter-email/cog_svcs_account.png)

    | <span data-ttu-id="74eb6-130">Настройка</span><span class="sxs-lookup"><span data-stu-id="74eb6-130">Setting</span></span>      |  <span data-ttu-id="74eb6-131">Рекомендуемое значение</span><span class="sxs-lookup"><span data-stu-id="74eb6-131">Suggested value</span></span>   | <span data-ttu-id="74eb6-132">Описание</span><span class="sxs-lookup"><span data-stu-id="74eb6-132">Description</span></span>                                        |
    | --- | --- | --- |
    | <span data-ttu-id="74eb6-133">**Имя**</span><span class="sxs-lookup"><span data-stu-id="74eb6-133">**Name**</span></span> | <span data-ttu-id="74eb6-134">MyCognitiveServicesAccnt</span><span class="sxs-lookup"><span data-stu-id="74eb6-134">MyCognitiveServicesAccnt</span></span> | <span data-ttu-id="74eb6-135">Выберите уникальное имя учетной записи.</span><span class="sxs-lookup"><span data-stu-id="74eb6-135">Choose a unique account name.</span></span> |
    | <span data-ttu-id="74eb6-136">**Тип API.**</span><span class="sxs-lookup"><span data-stu-id="74eb6-136">**API type**</span></span> | <span data-ttu-id="74eb6-137">API анализа текста</span><span class="sxs-lookup"><span data-stu-id="74eb6-137">Text Analytics API</span></span> | <span data-ttu-id="74eb6-138">API, используемый для анализа текста.</span><span class="sxs-lookup"><span data-stu-id="74eb6-138">API used to analyze text.</span></span>  |
    | <span data-ttu-id="74eb6-139">**Расположение**</span><span class="sxs-lookup"><span data-stu-id="74eb6-139">**Location**</span></span> | <span data-ttu-id="74eb6-140">Запад США</span><span class="sxs-lookup"><span data-stu-id="74eb6-140">West US</span></span> | <span data-ttu-id="74eb6-141">Сейчас для анализа текста доступен только регион **западная часть США**.</span><span class="sxs-lookup"><span data-stu-id="74eb6-141">Currently, only **West US** is available for text analytics.</span></span> |
    | <span data-ttu-id="74eb6-142">**Ценовая категория**</span><span class="sxs-lookup"><span data-stu-id="74eb6-142">**Pricing tier**</span></span> | <span data-ttu-id="74eb6-143">F0</span><span class="sxs-lookup"><span data-stu-id="74eb6-143">F0</span></span> | <span data-ttu-id="74eb6-144">Всегда начинайте с самого нижнего уровня.</span><span class="sxs-lookup"><span data-stu-id="74eb6-144">Start with the lowest tier.</span></span> <span data-ttu-id="74eb6-145">Если вы превысили количество вызовов, перейдите на более высокий уровень.</span><span class="sxs-lookup"><span data-stu-id="74eb6-145">If you run out of calls, scale to a higher tier.</span></span>|
    | <span data-ttu-id="74eb6-146">**Группа ресурсов**</span><span class="sxs-lookup"><span data-stu-id="74eb6-146">**Resource group**</span></span> | <span data-ttu-id="74eb6-147">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="74eb6-147">myResourceGroup</span></span> | <span data-ttu-id="74eb6-148">Используйте одну группу ресурсов для всех служб в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="74eb6-148">Use the same resource group for all services in this tutorial.</span></span>|

4. <span data-ttu-id="74eb6-149">Нажмите кнопку **Создать**, чтобы создать учетную запись.</span><span class="sxs-lookup"><span data-stu-id="74eb6-149">Click **Create** to create your account.</span></span> <span data-ttu-id="74eb6-150">После создания учетной записи щелкните новую учетную запись Cognitive Services, прикрепленную к панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="74eb6-150">After the account is created, click your new Cognitive Services account pinned to the dashboard.</span></span> 

5. <span data-ttu-id="74eb6-151">В учетной записи щелкните **Ключи**, скопируйте значение **ключа 1** и сохраните его.</span><span class="sxs-lookup"><span data-stu-id="74eb6-151">In the account, click **Keys**, and then copy the value of **Key 1** and save it.</span></span> <span data-ttu-id="74eb6-152">Этот ключ используется для подключения приложения логики к учетной записи Cognitive Services.</span><span class="sxs-lookup"><span data-stu-id="74eb6-152">You use this key to connect the logic app to your Cognitive Services account.</span></span> 
 
    ![ключей](media/functions-twitter-email/keys.png)

## <a name="create-the-function"></a><span data-ttu-id="74eb6-154">Создание функции</span><span class="sxs-lookup"><span data-stu-id="74eb6-154">Create the function</span></span>

<span data-ttu-id="74eb6-155">Функции предоставляют отличный способ разгрузки задач обработки в рабочем процессе приложений логики.</span><span class="sxs-lookup"><span data-stu-id="74eb6-155">Functions provides a great way to offload processing tasks in a logic apps workflow.</span></span> <span data-ttu-id="74eb6-156">В этом руководстве для обработки оценок мнений, выраженных в твитах, из Cognitive Services и возвращения значения категории используется функция, активируемая HTTP.</span><span class="sxs-lookup"><span data-stu-id="74eb6-156">This tutorial uses an HTTP triggered function to process tweet sentiment scores from Cognitive Services and return a category value.</span></span>  

1. <span data-ttu-id="74eb6-157">Разверните свое приложение-функцию, нажмите кнопку **+** рядом с пунктом **Функции**, а затем щелкните шаблон **HTTPTrigger**.</span><span class="sxs-lookup"><span data-stu-id="74eb6-157">Expand your function app, click the **+** button next to **Functions**, click the **HTTPTrigger** template.</span></span> <span data-ttu-id="74eb6-158">Введите `CategorizeSentiment` в качестве **имени** функции и нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="74eb6-158">Type `CategorizeSentiment` for the function **Name** and click **Create**.</span></span>

    ![Колонка приложения-функции, добавление функции](media/functions-twitter-email/add_fun.png)

2. <span data-ttu-id="74eb6-160">Замените содержимое файла run.csx следующим кодом и нажмите кнопку **Сохранить**:</span><span class="sxs-lookup"><span data-stu-id="74eb6-160">Replace the contents of the run.csx file with the following code, then click **Save**:</span></span>

    ```c#
    using System.Net;
    
    public static async Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
    {
        // The sentiment category defaults to 'GREEN'. 
        string category = "GREEN";
    
        // Get the sentiment score from the request body.
        double score = await req.Content.ReadAsAsync<double>();
        log.Info(string.Format("The sentiment score received is '{0}'.",
                    score.ToString()));
    
        // Set the category based on the sentiment score.
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
    <span data-ttu-id="74eb6-161">Этот код функции возвращает цветовую категорию на основе оценки мнений, полученной в запросе.</span><span class="sxs-lookup"><span data-stu-id="74eb6-161">This function code returns a color category based on the sentiment score received in the request.</span></span> 

3. <span data-ttu-id="74eb6-162">Чтобы проверить функцию, щелкните **Тест** в правой области сверху. После этого откроется вкладка "Тест". В разделе **Текст запроса** введите значение `0.2`, а затем нажмите кнопку **Запуск**.</span><span class="sxs-lookup"><span data-stu-id="74eb6-162">To test the function, click **Test** at the far right to expand the Test tab. Type a value of `0.2` for the **Request body**, and then click **Run**.</span></span> <span data-ttu-id="74eb6-163">В тексте ответа возвратится значение **RED**.</span><span class="sxs-lookup"><span data-stu-id="74eb6-163">A value of **RED** is returned in the body of the response.</span></span> 

    ![Проверка функции на портале Azure](./media/functions-twitter-email/test.png)

<span data-ttu-id="74eb6-165">Теперь у вас есть функция, классифицирующая оценку мнений.</span><span class="sxs-lookup"><span data-stu-id="74eb6-165">Now you have a function that categorizes sentiment scores.</span></span> <span data-ttu-id="74eb6-166">Создайте приложение логики, интегрирующее функцию с учетными записями Twitter и Cognitive Services.</span><span class="sxs-lookup"><span data-stu-id="74eb6-166">Next, you create a logic app that integrates your function with your Twitter and Cognitive Services accounts.</span></span> 

## <a name="create-a-logic-app"></a><span data-ttu-id="74eb6-167">Создайте приложение логики</span><span class="sxs-lookup"><span data-stu-id="74eb6-167">Create a logic app</span></span>   

1. <span data-ttu-id="74eb6-168">На портале Azure щелкните **Создать** в верхнем левом углу.</span><span class="sxs-lookup"><span data-stu-id="74eb6-168">In the Azure portal, click the **New** button found on the upper left-hand corner of the Azure portal.</span></span>

2. <span data-ttu-id="74eb6-169">Щелкните **Интеграция Enterprise** > **Приложение логики**.</span><span class="sxs-lookup"><span data-stu-id="74eb6-169">Click **Enterprise Integration** > **Logic App**.</span></span> <span data-ttu-id="74eb6-170">Затем используйте параметры, указанные в таблице, установите флажок **Закрепить на панели мониторинга** и нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="74eb6-170">Then, use the settings as specified in the table, check **Pin to dashboard**, and click **Create**.</span></span>
 
4. <span data-ttu-id="74eb6-171">Затем введите **имя**, например `TweetSentiment`, используйте параметры, указанные в таблице, примите условия и установите флажок **Закрепить на панели мониторинга**.</span><span class="sxs-lookup"><span data-stu-id="74eb6-171">Then, type a **Name** like `TweetSentiment`,  use the settings as specified in the table, accept the terms, and check **Pin to dashboard**.</span></span>

    ![Создание приложения логики на портале Azure](./media/functions-twitter-email/new_logicApp.png)

    | <span data-ttu-id="74eb6-173">Настройка</span><span class="sxs-lookup"><span data-stu-id="74eb6-173">Setting</span></span>      |  <span data-ttu-id="74eb6-174">Рекомендуемое значение</span><span class="sxs-lookup"><span data-stu-id="74eb6-174">Suggested value</span></span>   | <span data-ttu-id="74eb6-175">Описание</span><span class="sxs-lookup"><span data-stu-id="74eb6-175">Description</span></span>                                        |
    | ----------------- | ------------ | ------------- |
    | <span data-ttu-id="74eb6-176">**Имя**</span><span class="sxs-lookup"><span data-stu-id="74eb6-176">**Name**</span></span> | <span data-ttu-id="74eb6-177">TweetSentiment</span><span class="sxs-lookup"><span data-stu-id="74eb6-177">TweetSentiment</span></span> | <span data-ttu-id="74eb6-178">Выберите соответствующее имя для своего приложения.</span><span class="sxs-lookup"><span data-stu-id="74eb6-178">Choose an appropriate name for your app.</span></span> |
    | <span data-ttu-id="74eb6-179">**Группа ресурсов**</span><span class="sxs-lookup"><span data-stu-id="74eb6-179">**Resource group**</span></span> | <span data-ttu-id="74eb6-180">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="74eb6-180">myResourceGroup</span></span> | <span data-ttu-id="74eb6-181">API, используемый для анализа текста.</span><span class="sxs-lookup"><span data-stu-id="74eb6-181">API used to analyze text.</span></span>  |
    | <span data-ttu-id="74eb6-182">**Расположение**</span><span class="sxs-lookup"><span data-stu-id="74eb6-182">**Location**</span></span> | <span data-ttu-id="74eb6-183">Восток США</span><span class="sxs-lookup"><span data-stu-id="74eb6-183">East US</span></span> | <span data-ttu-id="74eb6-184">Выберите расположение рядом с вами.</span><span class="sxs-lookup"><span data-stu-id="74eb6-184">Choose a location close to you.</span></span> |
    | <span data-ttu-id="74eb6-185">**Группа ресурсов**</span><span class="sxs-lookup"><span data-stu-id="74eb6-185">**Resource group**</span></span> | <span data-ttu-id="74eb6-186">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="74eb6-186">myResourceGroup</span></span> | <span data-ttu-id="74eb6-187">Выберите ту же имеющуюся группу ресурсов, что и раньше.</span><span class="sxs-lookup"><span data-stu-id="74eb6-187">Choose the same existing resource group as before.</span></span>|

4. <span data-ttu-id="74eb6-188">Щелкните **Создать**, чтобы создать приложение логики.</span><span class="sxs-lookup"><span data-stu-id="74eb6-188">Click **Create** to create your logic app.</span></span> <span data-ttu-id="74eb6-189">После создания приложения щелкните новое приложение логики, прикрепленное к панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="74eb6-189">After the app is created, click your new logic app pinned to the dashboard.</span></span> <span data-ttu-id="74eb6-190">Затем в конструкторе Logic Apps прокрутите вниз и выберите шаблон **Пустое приложение логики**.</span><span class="sxs-lookup"><span data-stu-id="74eb6-190">Then in the Logic Apps Designer, scroll down and click the **Blank Logic App** template.</span></span> 

    ![Шаблон "Пустое приложение логики" Logic Apps](media/functions-twitter-email/blank.png)

<span data-ttu-id="74eb6-192">Теперь вы можете добавлять в приложение службы и триггеры с помощью конструктора Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="74eb6-192">You can now use the Logic Apps Designer to add services and triggers to your app.</span></span>

## <a name="connect-to-twitter"></a><span data-ttu-id="74eb6-193">Подключение к Twitter</span><span class="sxs-lookup"><span data-stu-id="74eb6-193">Connect to Twitter</span></span>

<span data-ttu-id="74eb6-194">Сначала подключитесь к своей учетной записи Twitter.</span><span class="sxs-lookup"><span data-stu-id="74eb6-194">First, create a connection to your Twitter account.</span></span> <span data-ttu-id="74eb6-195">Приложение логики выполняет опрос твитов, которые активируют запуск приложения.</span><span class="sxs-lookup"><span data-stu-id="74eb6-195">The logic app polls for tweets, which trigger the app to run.</span></span>

1. <span data-ttu-id="74eb6-196">В конструкторе щелкните службу **Twitter** и щелкните триггер **Время публикации нового твита**.</span><span class="sxs-lookup"><span data-stu-id="74eb6-196">In the designer, click the **Twitter** service, and click the **When a new tweet is posted** trigger.</span></span> <span data-ttu-id="74eb6-197">Войдите в свою учетную запись Twitter и авторизуйте Logic Apps для ее использования.</span><span class="sxs-lookup"><span data-stu-id="74eb6-197">Sign in to your Twitter account and authorize Logic Apps to use your account.</span></span>

2. <span data-ttu-id="74eb6-198">Используйте параметры триггера Twitter, указанные в таблице.</span><span class="sxs-lookup"><span data-stu-id="74eb6-198">Use the Twitter trigger settings as specified in the table.</span></span> 

    ![Параметры соединителя Twitter](media/functions-twitter-email/azure_tweet.png)

    | <span data-ttu-id="74eb6-200">Настройка</span><span class="sxs-lookup"><span data-stu-id="74eb6-200">Setting</span></span>      |  <span data-ttu-id="74eb6-201">Рекомендуемое значение</span><span class="sxs-lookup"><span data-stu-id="74eb6-201">Suggested value</span></span>   | <span data-ttu-id="74eb6-202">Описание</span><span class="sxs-lookup"><span data-stu-id="74eb6-202">Description</span></span>                                        |
    | ----------------- | ------------ | ------------- |
    | <span data-ttu-id="74eb6-203">**Текст поискового запроса**</span><span class="sxs-lookup"><span data-stu-id="74eb6-203">**Search text**</span></span> | <span data-ttu-id="74eb6-204">#Azure</span><span class="sxs-lookup"><span data-stu-id="74eb6-204">#Azure</span></span> | <span data-ttu-id="74eb6-205">Используйте популярный хэш-тег, который приведет к созданию новых твитов за выбранный интервал.</span><span class="sxs-lookup"><span data-stu-id="74eb6-205">Use a hashtag that is popular enough for to generate new tweets in the chosen interval.</span></span> <span data-ttu-id="74eb6-206">Если при использовании уровня "Бесплатный" и выбранного хэш-тега создается слишком много твитов, вы можете быстро использовать все транзакции в учетной записи Cognitive Services.</span><span class="sxs-lookup"><span data-stu-id="74eb6-206">When using the Free tier and your hashtag is too popular, you can quickly use up the transactions in your Cognitive Services account.</span></span> |
    | <span data-ttu-id="74eb6-207">**Frequency**</span><span class="sxs-lookup"><span data-stu-id="74eb6-207">**Frequency**</span></span> | <span data-ttu-id="74eb6-208">Минута</span><span class="sxs-lookup"><span data-stu-id="74eb6-208">Minute</span></span> | <span data-ttu-id="74eb6-209">Единица, используемая для определения частоты опроса Twitter.</span><span class="sxs-lookup"><span data-stu-id="74eb6-209">The frequency unit used for polling Twitter.</span></span>  |
    | <span data-ttu-id="74eb6-210">**Интервал**</span><span class="sxs-lookup"><span data-stu-id="74eb6-210">**Interval**</span></span> | <span data-ttu-id="74eb6-211">15</span><span class="sxs-lookup"><span data-stu-id="74eb6-211">15</span></span> | <span data-ttu-id="74eb6-212">Время между запросами Twitter в единицах, определяющих частоту.</span><span class="sxs-lookup"><span data-stu-id="74eb6-212">The time elapsed between Twitter requests, in frequency units.</span></span> |

3.  <span data-ttu-id="74eb6-213">Щелкните **Сохранить**, чтобы подключиться к своей учетной записи Twitter.</span><span class="sxs-lookup"><span data-stu-id="74eb6-213">Click **Save** to connect to your Twitter account.</span></span> 

<span data-ttu-id="74eb6-214">Теперь приложение подключено к Twitter.</span><span class="sxs-lookup"><span data-stu-id="74eb6-214">Now your app is connected to Twitter.</span></span> <span data-ttu-id="74eb6-215">Далее вы подключитесь к анализу текста для обнаружения мнений в собранных твитах.</span><span class="sxs-lookup"><span data-stu-id="74eb6-215">Next, you connect to text analytics to detect the sentiment of collected tweets.</span></span>

## <a name="add-sentiment-detection"></a><span data-ttu-id="74eb6-216">Добавление определения мнений</span><span class="sxs-lookup"><span data-stu-id="74eb6-216">Add sentiment detection</span></span>

1. <span data-ttu-id="74eb6-217">Щелкните **New Step** (Создать шаг), а затем — **Добавить действие**.</span><span class="sxs-lookup"><span data-stu-id="74eb6-217">Click **New Step**, and then **Add an action**.</span></span>

    ![Выбор действий "Новый шаг" и "Добавить действие"](media/functions-twitter-email/new_step.png)

2. <span data-ttu-id="74eb6-219">На странице **выбора действия** щелкните **Текстовая аналитика** и выберите действие **Detect sentiment** (Обнаружить мнение).</span><span class="sxs-lookup"><span data-stu-id="74eb6-219">In **Choose an action**, click **Text Analytics**, and then click the **Detect sentiment** action.</span></span>

    ![Определение мнений](media/functions-twitter-email/detect_sent.png)

3. <span data-ttu-id="74eb6-221">Введите имя подключения, например `MyCognitiveServicesConnection`, вставьте ключ для сохраненной учетной записи Cognitive Services и нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="74eb6-221">Type a connection name such as `MyCognitiveServicesConnection`, paste the key for your Cognitive Services account that you saved, and click **Create**.</span></span>  

4. <span data-ttu-id="74eb6-222">Щелкните **Text to analyze** (Текст для анализа) > **Текст твита**, а затем нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="74eb6-222">Click **Text to analyze** > **Tweet text**, and then click **Save**.</span></span>  

    ![Определение мнений](media/functions-twitter-email/ds_tta.png)

<span data-ttu-id="74eb6-224">Теперь, когда настроено выявление мнений, можно добавить подключение к функции, которая использует результат оценки мнений.</span><span class="sxs-lookup"><span data-stu-id="74eb6-224">Now that sentiment detection is configured, you can add a connection to your function that consumes the sentiment score output.</span></span>

## <a name="connect-sentiment-output-to-your-function"></a><span data-ttu-id="74eb6-225">Подключение выходных данных мнений к функции</span><span class="sxs-lookup"><span data-stu-id="74eb6-225">Connect sentiment output to your function</span></span>

1. <span data-ttu-id="74eb6-226">В конструкторе Logic Apps щелкните **New step** (Создать шаг) > **Добавить действие**, а затем выберите **Функции Azure**.</span><span class="sxs-lookup"><span data-stu-id="74eb6-226">In the Logic Apps Designer, click **New step** > **Add an action**, and then click **Azure Functions**.</span></span> 

2. <span data-ttu-id="74eb6-227">Щелкните **Выберите функцию Azure** и выберите функцию **CategorizeSentiment**, созданную ранее.</span><span class="sxs-lookup"><span data-stu-id="74eb6-227">Click **Choose an Azure function**, select the **CategorizeSentiment** function you created earlier.</span></span>  

    ![Окно с функцией Azure и параметром "Выберите функцию Azure"](media/functions-twitter-email/choose_fun.png)

3. <span data-ttu-id="74eb6-229">В разделе **Текст запроса** щелкните кнопку **Score** (Оценка) и **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="74eb6-229">In **Request Body**, click **Score** and then **Save**.</span></span>

    ![Оценка](media/functions-twitter-email/trigger_score.png)

<span data-ttu-id="74eb6-231">Теперь функция активируется при отправке оценки мнений из приложения логики.</span><span class="sxs-lookup"><span data-stu-id="74eb6-231">Now, your function is triggered when a sentiment score is sent from the logic app.</span></span> <span data-ttu-id="74eb6-232">Функция возвращает категорию с цветовой кодировкой в приложение логики.</span><span class="sxs-lookup"><span data-stu-id="74eb6-232">A color-coded category is returned to the logic app by the function.</span></span> <span data-ttu-id="74eb6-233">Далее следует добавить уведомление по электронной почте, отправляемое при возвращении мнения со значением **RED** из функции.</span><span class="sxs-lookup"><span data-stu-id="74eb6-233">Next, you add an email notification that is sent when a sentiment value of **RED** is returned from the function.</span></span> 

## <a name="add-email-notifications"></a><span data-ttu-id="74eb6-234">Добавление уведомлений по почте</span><span class="sxs-lookup"><span data-stu-id="74eb6-234">Add email notifications</span></span>

<span data-ttu-id="74eb6-235">Последняя часть рабочего процесса заключается в активации электронного сообщения, если мнению присвоена оценка _RED_.</span><span class="sxs-lookup"><span data-stu-id="74eb6-235">The last part of the workflow is to trigger an email when the sentiment is scored as _RED_.</span></span> <span data-ttu-id="74eb6-236">В этом разделе использует соединитель Outlook.com.</span><span class="sxs-lookup"><span data-stu-id="74eb6-236">This topic uses an Outlook.com connector.</span></span> <span data-ttu-id="74eb6-237">Вы можете выполнить аналогичные шаги для использования соединителя Gmail или Office 365 Outlook.</span><span class="sxs-lookup"><span data-stu-id="74eb6-237">You can perform similar steps to use a Gmail or Office 365 Outlook connector.</span></span>   

1. <span data-ttu-id="74eb6-238">В конструкторе Logic Apps щелкните **New step** (Создать шаг) > **Добавить условие**.</span><span class="sxs-lookup"><span data-stu-id="74eb6-238">In the Logic Apps Designer, click **New step** > **Add a condition**.</span></span> 

2. <span data-ttu-id="74eb6-239">Щелкните **Выберите значение**, а затем — **Текст**.</span><span class="sxs-lookup"><span data-stu-id="74eb6-239">Click **Choose a value**, then click **Body**.</span></span> <span data-ttu-id="74eb6-240">Выберите **равняется**, щелкните **Выберите значение**, введите `RED` и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="74eb6-240">Select **is equal to**, click **Choose a value** and type `RED`, and click **Save**.</span></span> 

    ![Добавьте условие к приложению логики.](media/functions-twitter-email/condition.png)

3. <span data-ttu-id="74eb6-242">В разделе **If Yes, Do Nothing** (Если да, ничего не предпринимать) нажмите кнопку **Добавить действие**, найдите `outlook.com`, щелкните **Отправить электронное письмо** и выполните вход в учетную запись Outlook.com.</span><span class="sxs-lookup"><span data-stu-id="74eb6-242">In **IF YES, DO NOTHING**, click **Add an action**, search for `outlook.com`, click **Send an email**, and sign in to your Outlook.com account.</span></span>
    
    ![Выбор действия для условия.](media/functions-twitter-email/outlook.png)

    > [!NOTE]
    > <span data-ttu-id="74eb6-244">Если у вас нет учетной записи Outlook.com, можно выбрать другой соединитель, например Gmail или Office 365 Outlook</span><span class="sxs-lookup"><span data-stu-id="74eb6-244">If you don't have an Outlook.com account, you can choose another connector, such as Gmail or Office 365 Outlook</span></span>

4. <span data-ttu-id="74eb6-245">В разделе с действием **Отправить электронное письмо** используйте параметры электронной почты, указанные в таблице.</span><span class="sxs-lookup"><span data-stu-id="74eb6-245">In the **Send an email** action, use the email settings as specified in the table.</span></span> 

    ![Настройка электронной почты для действия "Отправить электронное письмо".](media/functions-twitter-email/sendemail.png)

    | <span data-ttu-id="74eb6-247">Настройка</span><span class="sxs-lookup"><span data-stu-id="74eb6-247">Setting</span></span>      |  <span data-ttu-id="74eb6-248">Рекомендуемое значение</span><span class="sxs-lookup"><span data-stu-id="74eb6-248">Suggested value</span></span>   | <span data-ttu-id="74eb6-249">Описание</span><span class="sxs-lookup"><span data-stu-id="74eb6-249">Description</span></span>  |
    | ----------------- | ------------ | ------------- |
    | <span data-ttu-id="74eb6-250">**To**</span><span class="sxs-lookup"><span data-stu-id="74eb6-250">**To**</span></span> | <span data-ttu-id="74eb6-251">Введите адрес электронной почты</span><span class="sxs-lookup"><span data-stu-id="74eb6-251">Type your email address</span></span> | <span data-ttu-id="74eb6-252">Адрес электронной почты, на который приходит уведомление.</span><span class="sxs-lookup"><span data-stu-id="74eb6-252">The email address that receives the notification.</span></span> |
    | <span data-ttu-id="74eb6-253">**Тема**</span><span class="sxs-lookup"><span data-stu-id="74eb6-253">**Subject**</span></span> | <span data-ttu-id="74eb6-254">Negative tweet sentiment detected (Обнаружено отрицательное мнение, выраженное в твите)</span><span class="sxs-lookup"><span data-stu-id="74eb6-254">Negative tweet sentiment detected</span></span>  | <span data-ttu-id="74eb6-255">Строка темы уведомления по почте.</span><span class="sxs-lookup"><span data-stu-id="74eb6-255">The subject line of the email notification.</span></span>  |
    | <span data-ttu-id="74eb6-256">**Текст**</span><span class="sxs-lookup"><span data-stu-id="74eb6-256">**Body**</span></span> | <span data-ttu-id="74eb6-257">"Текст твита", "Расположение"</span><span class="sxs-lookup"><span data-stu-id="74eb6-257">Tweet text, Location</span></span> | <span data-ttu-id="74eb6-258">Щелкните параметры **Текст твита** и **Расположение**.</span><span class="sxs-lookup"><span data-stu-id="74eb6-258">Click the **Tweet text** and **Location** parameters.</span></span> |

5.  <span data-ttu-id="74eb6-259">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="74eb6-259">Click **Save**.</span></span>

<span data-ttu-id="74eb6-260">Теперь, когда рабочий процесс завершен, вы можете включить приложение логики и увидеть функцию в действии.</span><span class="sxs-lookup"><span data-stu-id="74eb6-260">Now that the workflow is complete, you can enable the logic app and see the function at work.</span></span>

## <a name="test-the-workflow"></a><span data-ttu-id="74eb6-261">Проверка рабочего процесса</span><span class="sxs-lookup"><span data-stu-id="74eb6-261">Test the workflow</span></span>

1. <span data-ttu-id="74eb6-262">В конструкторе Logic Apps щелкните **Запуск**, чтобы запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="74eb6-262">In the Logic App Designer, click **Run** to start the app.</span></span>

2. <span data-ttu-id="74eb6-263">В левом столбце щелкните **Обзор**, чтобы просмотреть сведения о состоянии приложения логики.</span><span class="sxs-lookup"><span data-stu-id="74eb6-263">In the left column, click **Overview** to see the status of the logic app.</span></span> 
 
    ![Состояние выполнения приложения логики](media/functions-twitter-email/over1.png)

3. <span data-ttu-id="74eb6-265">(Необязательно.) Щелкните одну из запущенных функций, чтобы просмотреть сведения о выполнении.</span><span class="sxs-lookup"><span data-stu-id="74eb6-265">(Optional) Click one of the runs to see details of the execution.</span></span>

4. <span data-ttu-id="74eb6-266">Перейдите к функции, просмотрите журналы и убедитесь, что значения мнений получены и обработаны.</span><span class="sxs-lookup"><span data-stu-id="74eb6-266">Go to your function, view the logs, and verify that sentiment values were received and processed.</span></span>
 
    ![Просмотр журналов функции](media/functions-twitter-email/sent.png)

5. <span data-ttu-id="74eb6-268">При обнаружении потенциально негативного мнения вы получите электронное сообщение.</span><span class="sxs-lookup"><span data-stu-id="74eb6-268">When a potentially negative sentiment is detected, you receive an email.</span></span> <span data-ttu-id="74eb6-269">Если вы еще не получили его, вы можете изменить код функции таким образом, чтобы каждый раз возвращалась категория RED:</span><span class="sxs-lookup"><span data-stu-id="74eb6-269">If you haven't received an email, you can change the function code to return RED every time:</span></span>

        return req.CreateResponse(HttpStatusCode.OK, "RED");

    <span data-ttu-id="74eb6-270">Проверив уведомления по почте, вернитесь к исходному коду:</span><span class="sxs-lookup"><span data-stu-id="74eb6-270">After you have verified email notifications, change back to the original code:</span></span>

        return req.CreateResponse(HttpStatusCode.OK, category);

    > [!IMPORTANT]
    > <span data-ttu-id="74eb6-271">Завершив работу с этим руководством, вам следует отключить приложение логики.</span><span class="sxs-lookup"><span data-stu-id="74eb6-271">After you have completed this tutorial, you should disable the logic app.</span></span> <span data-ttu-id="74eb6-272">Так вы не будете платить за выполнение и не используете все транзакции в учетной записи Cognitive Services.</span><span class="sxs-lookup"><span data-stu-id="74eb6-272">By disabling the app, you avoid being charged for executions and using up the transactions in your Cognitive Services account.</span></span>

<span data-ttu-id="74eb6-273">Вы узнали, насколько легко можно интегрировать Функции в рабочий процесс Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="74eb6-273">Now you have seen how easy it is to integrate Functions into a Logic Apps workflow.</span></span>

## <a name="disable-the-logic-app"></a><span data-ttu-id="74eb6-274">Отключение приложения логики</span><span class="sxs-lookup"><span data-stu-id="74eb6-274">Disable the logic app</span></span>

<span data-ttu-id="74eb6-275">Чтобы отключить приложение логики, щелкните **Обзор** и **Отключить** в верхней части экрана.</span><span class="sxs-lookup"><span data-stu-id="74eb6-275">To disable the logic app, click **Overview** and then click **Disable** at the top of the screen.</span></span> <span data-ttu-id="74eb6-276">Приложение логики будет отключено, а вы не будете платить за его использование. При этом вам не нужно удалять приложение.</span><span class="sxs-lookup"><span data-stu-id="74eb6-276">This stops the logic app from running and incurring charges without deleting the app.</span></span> 

![Журналы функций](media/functions-twitter-email/disable-logic-app.png)

## <a name="next-steps"></a><span data-ttu-id="74eb6-278">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="74eb6-278">Next steps</span></span>

<span data-ttu-id="74eb6-279">Из этого руководства вы узнали, как выполнять такие задачи:</span><span class="sxs-lookup"><span data-stu-id="74eb6-279">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="74eb6-280">Создайте учетную запись Cognitive Services.</span><span class="sxs-lookup"><span data-stu-id="74eb6-280">Create a Cognitive Services account.</span></span>
> * <span data-ttu-id="74eb6-281">Создание функции, классифицирующей мнения, выраженные в твитах.</span><span class="sxs-lookup"><span data-stu-id="74eb6-281">Create a function that categorizes tweet sentiment.</span></span>
> * <span data-ttu-id="74eb6-282">Создание приложения логики, подключающегося к Twitter.</span><span class="sxs-lookup"><span data-stu-id="74eb6-282">Create a logic app that connects to Twitter.</span></span>
> * <span data-ttu-id="74eb6-283">Добавление обнаружения мнений в приложение логики.</span><span class="sxs-lookup"><span data-stu-id="74eb6-283">Add sentiment detection to the logic app.</span></span> 
> * <span data-ttu-id="74eb6-284">Подключение приложения логики к функции.</span><span class="sxs-lookup"><span data-stu-id="74eb6-284">Connect the logic app to the function.</span></span>
> * <span data-ttu-id="74eb6-285">Отправка электронного сообщения в зависимости от ответа из функции.</span><span class="sxs-lookup"><span data-stu-id="74eb6-285">Send an email based on the response from the function.</span></span>

<span data-ttu-id="74eb6-286">Перейдите к следующему руководству, чтобы научиться создавать бессерверные API для функций.</span><span class="sxs-lookup"><span data-stu-id="74eb6-286">Advance to the next tutorial to learn how to create a serverless API for your function.</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="74eb6-287">Создание бессерверного API с помощью Функций Azure</span><span class="sxs-lookup"><span data-stu-id="74eb6-287">Create a serverless API using Azure Functions</span></span>](functions-create-serverless-api.md)

<span data-ttu-id="74eb6-288">Дополнительные сведения об Azure Logic Apps см. в [этой статье](../logic-apps/logic-apps-what-are-logic-apps.md).</span><span class="sxs-lookup"><span data-stu-id="74eb6-288">To learn more about Logic Apps, see [Azure Logic Apps](../logic-apps/logic-apps-what-are-logic-apps.md).</span></span>

