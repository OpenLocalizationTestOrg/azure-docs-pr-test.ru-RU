---
title: "Анализ мнений Twitter aaaReal времени с Azure Stream Analytics | Документы Microsoft"
description: "Узнайте, как toouse Stream Analytics в реальном времени анализа мнений Twitter. Пошаговые инструкции из toodata создания события на динамическую панель мониторинга."
keywords: "анализ тенденций twitter в режиме реального времени, анализ тональности, анализ социальных сетей, пример анализа тенденций"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 42068691-074b-4c3b-a527-acafa484fda2
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: jeffstok
ms.openlocfilehash: 157790caa7ea6f5570dd9c9d3bd9694d437eb4c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="real-time-twitter-sentiment-analysis-in-azure-stream-analytics"></a><span data-ttu-id="2728c-105">Анализ тональности в Twitter в режиме реального времени в Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="2728c-105">Real-time Twitter sentiment analysis in Azure Stream Analytics</span></span>

<span data-ttu-id="2728c-106">Узнайте, как toobuild анализ мнений решения для социальных сетей аналитика в реальном времени путем Twitter событий в концентраторы событий Azure.</span><span class="sxs-lookup"><span data-stu-id="2728c-106">Learn how toobuild a sentiment analysis solution for social media analytics by bringing real-time Twitter events into Azure Event Hubs.</span></span> <span data-ttu-id="2728c-107">После этого можно написать tooanalyze hello Azure Stream Analytics запроса данных и либо хранилище hello результаты для дальнейшего использования или использовать панели мониторинга и [Power BI](https://powerbi.com/) tooprovide аналитики в реальном времени.</span><span class="sxs-lookup"><span data-stu-id="2728c-107">You can then write an Azure Stream Analytics query tooanalyze hello data and either store hello results for later use or use a dashboard and [Power BI](https://powerbi.com/) tooprovide insights in real time.</span></span>

<span data-ttu-id="2728c-108">Средства аналитики для социальных сетей помогают организациям определить популярные темы,</span><span class="sxs-lookup"><span data-stu-id="2728c-108">Social media analytics tools help organizations understand trending topics.</span></span> <span data-ttu-id="2728c-109">то есть темы и отношения с большим количеством записей в социальных сетях.</span><span class="sxs-lookup"><span data-stu-id="2728c-109">Trending topics are subjects and attitudes that have a high volume of posts in social media.</span></span> <span data-ttu-id="2728c-110">Анализ мнений, которая также называется *мнение интеллектуального анализа данных*, использует социальные analytics средства toodetermine отношении продуктов, представление и т. д.</span><span class="sxs-lookup"><span data-stu-id="2728c-110">Sentiment analysis, which is also called *opinion mining*, uses social media analytics tools toodetermine attitudes toward a product, idea, and so on.</span></span> 

<span data-ttu-id="2728c-111">Анализ трендов в режиме реального времени Twitter является отличным примером аналитический инструмент, поскольку hello хэштегом подписки модели позволяет ключевые слова toospecific toolisten (хэш) и разрабатывать анализ мнений hello веб-канала.</span><span class="sxs-lookup"><span data-stu-id="2728c-111">Real-time Twitter trend analysis is a great example of an analytics tool, because hello hashtag subscription model enables you toolisten toospecific keywords (hashtags) and develop sentiment analysis of hello feed.</span></span>

## <a name="scenario-social-media-sentiment-analysis-in-real-time"></a><span data-ttu-id="2728c-112">Сценарий: анализ тональности в социальной сети в режиме реального времени</span><span class="sxs-lookup"><span data-stu-id="2728c-112">Scenario: Social media sentiment analysis in real time</span></span>

<span data-ttu-id="2728c-113">Организации, которая содержит веб-сайт новостей носителя заинтересована в получения преимущества по сравнению с его конкурентами с содержимым узел, непосредственно относящиеся tooits читателей.</span><span class="sxs-lookup"><span data-stu-id="2728c-113">A company that has a news media website is interested in gaining an advantage over its competitors by featuring site content that is immediately relevant tooits readers.</span></span> <span data-ttu-id="2728c-114">Hello компания использует анализа социальных сетей на разделы, соответствующие tooreaders, выполнив анализ мнений в реальном времени данных Twitter.</span><span class="sxs-lookup"><span data-stu-id="2728c-114">hello company uses social media analysis on topics that are relevant tooreaders by doing real-time sentiment analysis of Twitter data.</span></span>

<span data-ttu-id="2728c-115">tooidentify тенденций разделы в режиме реального времени в Twitter, hello аналитика в реальном времени потребности компании об объеме твит hello и мнения по ключевые темы.</span><span class="sxs-lookup"><span data-stu-id="2728c-115">tooidentify trending topics in real time on Twitter, hello company needs real-time analytics about hello tweet volume and sentiment for key topics.</span></span> <span data-ttu-id="2728c-116">Другими словами hello связано подсистема аналитики анализ мнений, на основании этого социальные веб-канала.</span><span class="sxs-lookup"><span data-stu-id="2728c-116">In other words, hello need is a sentiment analysis analytics engine that's based on this social media feed.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2728c-117">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="2728c-117">Prerequisites</span></span>
<span data-ttu-id="2728c-118">В этом учебнике используется клиентское приложение, которое подключается tooTwitter и ищет твиты, имеющих определенные хэш (который можно задать).</span><span class="sxs-lookup"><span data-stu-id="2728c-118">In this tutorial, you use a client application that connects tooTwitter and looks for tweets that have certain hashtags (which you can set).</span></span> <span data-ttu-id="2728c-119">В порядке toorun hello приложения и анализ твиты, с помощью потоковой передачи аналитики Azure, необходимо иметь следующие hello hello:</span><span class="sxs-lookup"><span data-stu-id="2728c-119">In order toorun hello application and analyze hello tweets using Azure Streaming Analytics, you must have hello following:</span></span>

* <span data-ttu-id="2728c-120">Подписка Azure</span><span class="sxs-lookup"><span data-stu-id="2728c-120">An Azure subscription</span></span>
* <span data-ttu-id="2728c-121">учетная запись Twitter;</span><span class="sxs-lookup"><span data-stu-id="2728c-121">A Twitter account</span></span> 
* <span data-ttu-id="2728c-122">Приложения Twitter и hello [маркера доступа OAuth](https://dev.twitter.com/oauth/overview/application-owner-access-tokens) для этого приложения.</span><span class="sxs-lookup"><span data-stu-id="2728c-122">A Twitter application, and hello [OAuth access token](https://dev.twitter.com/oauth/overview/application-owner-access-tokens) for that application.</span></span> <span data-ttu-id="2728c-123">Мы предоставляем высокого уровня инструкции toocreate приложения Twitter в более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="2728c-123">We provide high-level instructions for how toocreate a Twitter application later.</span></span>
* <span data-ttu-id="2728c-124">Hello TwitterWPFClient приложение, которое считывает hello Twitter веб-канала.</span><span class="sxs-lookup"><span data-stu-id="2728c-124">hello TwitterWPFClient application, which reads hello Twitter feed.</span></span> <span data-ttu-id="2728c-125">tooget это приложение, hello загрузки [TwitterWPFClient.zip](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TwitterClient/TwitterWPFClient.zip) файла из GitHub и затем распакуйте hello пакета в папку на компьютере.</span><span class="sxs-lookup"><span data-stu-id="2728c-125">tooget this application, download hello [TwitterWPFClient.zip](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TwitterClient/TwitterWPFClient.zip) file from GitHub and then unzip hello package into a folder on your computer.</span></span> <span data-ttu-id="2728c-126">Если вы хотите toosee hello исходного кода и запустить приложение hello в отладчик, можно получить hello исходного кода из [GitHub](https://aka.ms/azure-stream-analytics-telcogenerator).</span><span class="sxs-lookup"><span data-stu-id="2728c-126">If you want toosee hello source code and run hello application in a debugger, you can get hello source code from [GitHub](https://aka.ms/azure-stream-analytics-telcogenerator).</span></span> 

## <a name="create-an-event-hub-for-streaming-analytics-input"></a><span data-ttu-id="2728c-127">Создание концентратора событий для входных данных Streaming Analytics</span><span class="sxs-lookup"><span data-stu-id="2728c-127">Create an event hub for Streaming Analytics input</span></span>

<span data-ttu-id="2728c-128">Пример приложения Hello создает события и помещает их tooan концентратор событий Azure.</span><span class="sxs-lookup"><span data-stu-id="2728c-128">hello sample application generates events and pushes them tooan Azure event hub.</span></span> <span data-ttu-id="2728c-129">Концентраторы событий Azure — hello предпочтительный метод приема событий для Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="2728c-129">Azure event hubs are hello preferred method of event ingestion for Stream Analytics.</span></span> <span data-ttu-id="2728c-130">Дополнительные сведения см. в разделе hello [документации концентраторов событий Azure](../event-hubs/event-hubs-what-is-event-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="2728c-130">For more information, see hello [Azure Event Hubs documentation](../event-hubs/event-hubs-what-is-event-hubs.md).</span></span>


### <a name="create-an-event-hub-namespace-and-event-hub"></a><span data-ttu-id="2728c-131">Создание пространства имен концентраторов событий и концентратора событий</span><span class="sxs-lookup"><span data-stu-id="2728c-131">Create an event hub namespace and event hub</span></span>
<span data-ttu-id="2728c-132">В этой процедуре сначала создать пространство имен концентратора событий и затем добавьте пространство имен toothat концентратора событий.</span><span class="sxs-lookup"><span data-stu-id="2728c-132">In this procedure, you first create an event hub namespace, and then you add an event hub toothat namespace.</span></span> <span data-ttu-id="2728c-133">Пространства имен концентратора событий используются группы toologically связанные экземпляры шины событий.</span><span class="sxs-lookup"><span data-stu-id="2728c-133">Event hub namespaces are used toologically group related event bus instances.</span></span> 

1. <span data-ttu-id="2728c-134">Войдите в портал Azure toohello и нажмите кнопку **New** > **Интернета вещей** > **концентратора событий**.</span><span class="sxs-lookup"><span data-stu-id="2728c-134">Log  in toohello Azure portal and click **New** > **Internet of Things** > **Event Hub**.</span></span> 

2. <span data-ttu-id="2728c-135">В hello **создать пространство имен** колонки, введите имя пространства имен, например `<yourname>-socialtwitter-eh-ns`.</span><span class="sxs-lookup"><span data-stu-id="2728c-135">In hello **Create namespace** blade, enter a namespace name such as `<yourname>-socialtwitter-eh-ns`.</span></span> <span data-ttu-id="2728c-136">Можно использовать любое имя для пространства имен hello, но hello имя должно быть допустимым URL-адреса и должно быть уникальным среди Azure.</span><span class="sxs-lookup"><span data-stu-id="2728c-136">You can use any name for hello namespace, but hello name must be valid for a URL and it must be unique across Azure.</span></span> 
    
3. <span data-ttu-id="2728c-137">Выберите подписку, создайте или выберите группу ресурсов, а затем щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="2728c-137">Select a subscription and create or choose a resource group, then click **Create**.</span></span> 

    ![Создание пространства имен концентратора событий](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-eventhub-namespace.png)
 
4. <span data-ttu-id="2728c-139">После завершения развертывания приветствия имен найти пространство имен концентратора событий hello в списке ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="2728c-139">When hello namespace has finished deploying, find hello event hub namespace in your list of Azure resources.</span></span> 

5. <span data-ttu-id="2728c-140">Нажмите кнопку hello новое пространство имен затем в колонке приветствия имен  **+ &nbsp;концентратора событий**.</span><span class="sxs-lookup"><span data-stu-id="2728c-140">Click hello new namespace, and in hello namespace blade, click **+&nbsp;Event Hub**.</span></span> 

    ![<span data-ttu-id="2728c-141">Кнопка добавления концентратора событий Hello для создания нового концентратора событий</span><span class="sxs-lookup"><span data-stu-id="2728c-141">hello Add Event Hub button for creating a new event hub</span></span> ](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-eventhub-button.png)    
 
6. <span data-ttu-id="2728c-142">Новый концентратор событий имя hello `socialtwitter-eh`.</span><span class="sxs-lookup"><span data-stu-id="2728c-142">Name hello new event hub `socialtwitter-eh`.</span></span> <span data-ttu-id="2728c-143">Вы можете использовать другое имя.</span><span class="sxs-lookup"><span data-stu-id="2728c-143">You can use a different name.</span></span> <span data-ttu-id="2728c-144">В противном случае запишите его, поскольку его нужно имя hello.</span><span class="sxs-lookup"><span data-stu-id="2728c-144">If you do, make a note of it, because you need hello name later.</span></span> <span data-ttu-id="2728c-145">Не нужно tooset другие параметры для концентратора событий hello.</span><span class="sxs-lookup"><span data-stu-id="2728c-145">You don't need tooset any other options for hello event hub.</span></span>

    ![Колонка создания нового концентратора событий](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-eventhub.png)
 
7. <span data-ttu-id="2728c-147">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="2728c-147">Click **Create**.</span></span>


### <a name="grant-access-toohello-event-hub"></a><span data-ttu-id="2728c-148">Концентратор событий toohello предоставление доступа</span><span class="sxs-lookup"><span data-stu-id="2728c-148">Grant access toohello event hub</span></span>

<span data-ttu-id="2728c-149">Процесс для отправки данных концентратора событий tooan, hello концентратора событий должен иметь политику, разрешающую соответствующие права доступа.</span><span class="sxs-lookup"><span data-stu-id="2728c-149">Before a process can send data tooan event hub, hello event hub must have a policy that allows appropriate access.</span></span> <span data-ttu-id="2728c-150">политика доступа Hello создает строку подключения, которая включает сведения об авторизации.</span><span class="sxs-lookup"><span data-stu-id="2728c-150">hello access policy produces a connection string that includes authorization information.</span></span>

1.  <span data-ttu-id="2728c-151">В колонке пространства имен событий hello щелкните **концентраторов событий** и щелкните имя hello нового концентратора событий.</span><span class="sxs-lookup"><span data-stu-id="2728c-151">In hello event namespace blade, click **Event Hubs** and then click hello name of your new event hub.</span></span>

2.  <span data-ttu-id="2728c-152">В колонке концентратора событий hello щелкните **политики общего доступа** и нажмите кнопку  **+ &nbsp;добавить**.</span><span class="sxs-lookup"><span data-stu-id="2728c-152">In hello event hub blade, click **Shared access policies** and then click **+&nbsp;Add**.</span></span>

    >[!NOTE]
    ><span data-ttu-id="2728c-153">Убедитесь, что вы работаете с концентратора событий hello, не hello пространство имен концентратора событий.</span><span class="sxs-lookup"><span data-stu-id="2728c-153">Make sure you're working with hello event hub, not hello event hub namespace.</span></span>

3.  <span data-ttu-id="2728c-154">Добавьте политику с именем `socialtwitter-access`, а для параметра **Утверждение** выберите **Управление**.</span><span class="sxs-lookup"><span data-stu-id="2728c-154">Add a policy named `socialtwitter-access` and for **Claim**, select **Manage**.</span></span>

    ![Колонка создания политики доступа для нового концентратора событий](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-shared-access-policy-manage.png)
 
4.  <span data-ttu-id="2728c-156">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="2728c-156">Click **Create**.</span></span>

5.  <span data-ttu-id="2728c-157">После развертывания политики hello, щелкните его в списке hello политик общего доступа.</span><span class="sxs-lookup"><span data-stu-id="2728c-157">After hello policy has been deployed, click it in hello list of shared access policies.</span></span>

6.  <span data-ttu-id="2728c-158">Поле поиска hello **строки ПЕРВИЧНОГО ключа подключения** и выберите hello копирования кнопку Далее toohello строку подключения.</span><span class="sxs-lookup"><span data-stu-id="2728c-158">Find hello box labeled **CONNECTION STRING-PRIMARY KEY** and click hello copy button next toohello connection string.</span></span> 
    
    ![Копирование hello первичным соединением строковый ключ из политики доступа hello](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-shared-access-policy-copy-connection-string.png)
 
7.  <span data-ttu-id="2728c-160">Вставьте строку подключения hello в текстовый редактор.</span><span class="sxs-lookup"><span data-stu-id="2728c-160">Paste hello connection string into a text editor.</span></span> <span data-ttu-id="2728c-161">Эта строка подключения для hello в следующем разделе, необходимо после внесения tooit некоторые небольшие изменения.</span><span class="sxs-lookup"><span data-stu-id="2728c-161">You need this connection string for hello next section, after you make some small edits tooit.</span></span>

    <span data-ttu-id="2728c-162">Строка подключения Hello выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="2728c-162">hello connection string looks like this:</span></span>

        Endpoint=sb://YOURNAME-socialtwitter-eh-ns.servicebus.windows.net/;SharedAccessKeyName=socialtwitter-access;SharedAccessKey=Gw2NFZw6r...FxKbXaC2op6a0ZsPkI=;EntityPath=socialtwitter-eh

    <span data-ttu-id="2728c-163">Обратите внимание, что строка подключения hello содержит несколько пар ключ значение, разделенных точкой с запятой: `Endpoint`, `SharedAccessKeyName`, `SharedAccessKey`, и `EntityPath`.</span><span class="sxs-lookup"><span data-stu-id="2728c-163">Notice that hello connection string contains multiple key-value pairs, separated with semicolons: `Endpoint`, `SharedAccessKeyName`, `SharedAccessKey`, and `EntityPath`.</span></span>  

    > [!NOTE]
    > <span data-ttu-id="2728c-164">В целях безопасности были удалены части строки соединения hello в примере hello.</span><span class="sxs-lookup"><span data-stu-id="2728c-164">For security, parts of hello connection string in hello example have been removed.</span></span>

8.  <span data-ttu-id="2728c-165">В текстовом редакторе hello, удалите hello `EntityPath` пару из строки подключения hello (не забудьте tooremove hello точкой с запятой, за которым следуют его).</span><span class="sxs-lookup"><span data-stu-id="2728c-165">In hello text editor, remove hello `EntityPath` pair from hello connection string (don't forget tooremove hello semicolon that precedes it).</span></span> <span data-ttu-id="2728c-166">Когда закончите, строка подключения hello выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="2728c-166">When you're done, hello connection string looks like this:</span></span>

        Endpoint=sb://YOURNAME-socialtwitter-eh-ns.servicebus.windows.net/;SharedAccessKeyName=socialtwitter-access;SharedAccessKey=Gw2NFZw6r...FxKbXaC2op6a0ZsPkI=


## <a name="configure-and-start-hello-twitter-client-application"></a><span data-ttu-id="2728c-167">Настройте и запустите клиентское приложение hello Twitter</span><span class="sxs-lookup"><span data-stu-id="2728c-167">Configure and start hello Twitter client application</span></span>
<span data-ttu-id="2728c-168">клиентское приложение Hello получает события твитов непосредственно из Twitter.</span><span class="sxs-lookup"><span data-stu-id="2728c-168">hello client application gets tweet events directly from Twitter.</span></span> <span data-ttu-id="2728c-169">Чтобы toodo так, поэтому он должен hello toocall разрешение API-интерфейсов потоковой передачи Twitter.</span><span class="sxs-lookup"><span data-stu-id="2728c-169">In order toodo so, it needs permission toocall hello Twitter Streaming APIs.</span></span> <span data-ttu-id="2728c-170">tooconfigure разрешение, создать приложение в Twitter, который создает уникальные учетные данные (например токена OAuth).</span><span class="sxs-lookup"><span data-stu-id="2728c-170">tooconfigure that permission, you create an application in Twitter, which generates unique credentials (such as an OAuth token).</span></span> <span data-ttu-id="2728c-171">Затем можно настроить hello клиентского приложения toouse эти учетные данные, когда он выполняет вызовы API.</span><span class="sxs-lookup"><span data-stu-id="2728c-171">You can then configure hello client application toouse these credentials when it makes API calls.</span></span> 

### <a name="create-a-twitter-application"></a><span data-ttu-id="2728c-172">Создание приложения Twitter</span><span class="sxs-lookup"><span data-stu-id="2728c-172">Create a Twitter application</span></span>
<span data-ttu-id="2728c-173">Если вы еще не создали приложение Twitter для этого руководства, сделайте это.</span><span class="sxs-lookup"><span data-stu-id="2728c-173">If you do not already have a Twitter application that you can use for this tutorial, you can create one.</span></span> <span data-ttu-id="2728c-174">У вас уже должна быть учетная запись Twitter.</span><span class="sxs-lookup"><span data-stu-id="2728c-174">You must already have a Twitter account.</span></span>

> [!NOTE]
> <span data-ttu-id="2728c-175">процессы Hello в Twitter для создания приложения и начало hello keys, секреты и токен, может измениться.</span><span class="sxs-lookup"><span data-stu-id="2728c-175">hello exact process in Twitter for creating an application and getting hello keys, secrets, and token might change.</span></span> <span data-ttu-id="2728c-176">Если эти инструкции не совпадают, отображаемые на сайте Twitter hello, см. документацию для разработчиков toohello Twitter.</span><span class="sxs-lookup"><span data-stu-id="2728c-176">If these instructions don't match what you see on hello Twitter site, refer toohello Twitter developer documentation.</span></span>

1. <span data-ttu-id="2728c-177">Go toohello [страницы управления приложения Twitter](https://apps.twitter.com/).</span><span class="sxs-lookup"><span data-stu-id="2728c-177">Go toohello [Twitter application management page](https://apps.twitter.com/).</span></span> 

2. <span data-ttu-id="2728c-178">Создайте новое приложение.</span><span class="sxs-lookup"><span data-stu-id="2728c-178">Create a new application.</span></span> 

    * <span data-ttu-id="2728c-179">URL-адрес веб-сайта hello укажите допустимый URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="2728c-179">For hello website URL, specify a valid URL.</span></span> <span data-ttu-id="2728c-180">Он не имеет toobe действующем сайте.</span><span class="sxs-lookup"><span data-stu-id="2728c-180">It does not have toobe a live site.</span></span> <span data-ttu-id="2728c-181">(Нельзя просто указать `localhost`).</span><span class="sxs-lookup"><span data-stu-id="2728c-181">(You can't specify just `localhost`.)</span></span>
    * <span data-ttu-id="2728c-182">Оставьте пустым поле обратного вызова hello.</span><span class="sxs-lookup"><span data-stu-id="2728c-182">Leave hello callback field blank.</span></span> <span data-ttu-id="2728c-183">клиентское приложение Hello, используемого в этом учебнике не требует обратных вызовов.</span><span class="sxs-lookup"><span data-stu-id="2728c-183">hello client application you use for this tutorial doesn't require callbacks.</span></span>

    ![Создание приложения в Twitter](./media/stream-analytics-twitter-sentiment-analysis-trends/create-twitter-application.png)

3. <span data-ttu-id="2728c-185">При необходимости измените разрешения приложения hello только для tooread.</span><span class="sxs-lookup"><span data-stu-id="2728c-185">Optionally, change hello application's permissions tooread-only.</span></span>

4. <span data-ttu-id="2728c-186">При создании приложения hello go toohello **ключей и маркеры доступа** страницы.</span><span class="sxs-lookup"><span data-stu-id="2728c-186">When hello application is created, go toohello **Keys and Access Tokens** page.</span></span>

5. <span data-ttu-id="2728c-187">Нажмите кнопку hello toogenerate маркер доступа и секрет маркера доступа.</span><span class="sxs-lookup"><span data-stu-id="2728c-187">Click hello button toogenerate an access token and access token secret.</span></span>

<span data-ttu-id="2728c-188">Следует иметь под рукой, так как он понадобится в следующей процедуре hello.</span><span class="sxs-lookup"><span data-stu-id="2728c-188">Keep this information handy, because you will need it in hello next procedure.</span></span>

>[!NOTE]
><span data-ttu-id="2728c-189">Hello ключи и секретные данные для приложения hello Twitter укажите учетную запись Twitter tooyour доступа.</span><span class="sxs-lookup"><span data-stu-id="2728c-189">hello keys and secrets for hello Twitter application provide access tooyour Twitter account.</span></span> <span data-ttu-id="2728c-190">Относить эту информацию как конфиденциальные, hello таким же, как пароль Twitter.</span><span class="sxs-lookup"><span data-stu-id="2728c-190">Treat this information as sensitive, hello same as you do your Twitter password.</span></span> <span data-ttu-id="2728c-191">Например не внедрять эту информацию в приложении, присвоенное tooothers.</span><span class="sxs-lookup"><span data-stu-id="2728c-191">For example, don't embed this information in an application that you give tooothers.</span></span> 


### <a name="configure-hello-client-application"></a><span data-ttu-id="2728c-192">Настройте клиентское приложение hello</span><span class="sxs-lookup"><span data-stu-id="2728c-192">Configure hello client application</span></span>
<span data-ttu-id="2728c-193">Мы создали клиентское приложение, которое соединяется с использованием данных tooTwitter [API-интерфейсов потоковой передачи в Twitter](https://dev.twitter.com/streaming/overview) toocollect события твитов о определенный набор разделов.</span><span class="sxs-lookup"><span data-stu-id="2728c-193">We've created a client application that connects tooTwitter data using [Twitter's Streaming APIs](https://dev.twitter.com/streaming/overview) toocollect tweet events about a specific set of topics.</span></span> <span data-ttu-id="2728c-194">приложение Hello использует hello [Sentiment140](http://help.sentiment140.com/) средства открытым исходным кодом, которое назначает hello следующие твит tooeach мнений значение:</span><span class="sxs-lookup"><span data-stu-id="2728c-194">hello application uses hello [Sentiment140](http://help.sentiment140.com/) open source tool, which assigns hello following sentiment value tooeach tweet:</span></span>

* <span data-ttu-id="2728c-195">0 = негативная тональность</span><span class="sxs-lookup"><span data-stu-id="2728c-195">0 = negative</span></span>
* <span data-ttu-id="2728c-196">2 = нейтральная тональность</span><span class="sxs-lookup"><span data-stu-id="2728c-196">2 = neutral</span></span>
* <span data-ttu-id="2728c-197">4 = позитивная тональность</span><span class="sxs-lookup"><span data-stu-id="2728c-197">4 = positive</span></span>

<span data-ttu-id="2728c-198">После события твитов hello назначения значение мнений, они помещаются в стек toohello концентратора событий, которое было создано ранее.</span><span class="sxs-lookup"><span data-stu-id="2728c-198">After hello tweet events have been assigned a sentiment value, they are pushed toohello event hub that you created earlier.</span></span>

<span data-ttu-id="2728c-199">Перед запуском приложения hello, требуются определенные сведения от вас, таких как ключи Twitter hello и строка подключения концентратора событий hello.</span><span class="sxs-lookup"><span data-stu-id="2728c-199">Before hello application runs, it requires certain information from you, like hello Twitter keys and hello event hub connection string.</span></span> <span data-ttu-id="2728c-200">Можно указать сведения о конфигурации hello следующими способами:</span><span class="sxs-lookup"><span data-stu-id="2728c-200">You can provide hello configuration information in these ways:</span></span>

* <span data-ttu-id="2728c-201">Запустите приложение hello и затем с помощью приложения hello пользовательского интерфейса tooenter hello ключи, секреты и строки подключения.</span><span class="sxs-lookup"><span data-stu-id="2728c-201">Run hello application, and then use hello application's UI tooenter hello keys, secrets, and connection string.</span></span> <span data-ttu-id="2728c-202">После этого данные конфигурации hello используется во время текущего сеанса, но он не сохраняется.</span><span class="sxs-lookup"><span data-stu-id="2728c-202">If you do this, hello configuration information is used for your current session, but it isn't saved.</span></span>
* <span data-ttu-id="2728c-203">Измените файл .config приложения hello и задавать значения hello, существует.</span><span class="sxs-lookup"><span data-stu-id="2728c-203">Edit hello application's .config file and set hello values there.</span></span> <span data-ttu-id="2728c-204">Этот подход сохраняет сведения о конфигурации hello, но это также означает, что это потенциально конфиденциальная информация хранится в виде обычного текста на компьютере.</span><span class="sxs-lookup"><span data-stu-id="2728c-204">This approach persists hello configuration information, but it also means that this potentially sensitive information is stored in plain text on your computer.</span></span>

<span data-ttu-id="2728c-205">Hello следующей процедуре описываются оба подхода.</span><span class="sxs-lookup"><span data-stu-id="2728c-205">hello following procedure documents both approaches.</span></span> 

1. <span data-ttu-id="2728c-206">Убедитесь, что вы загрузили и распаковал hello [TwitterWPFClient.zip](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TwitterClient/TwitterWPFClient.zip) приложения, как указано в предварительных требованиях для hello.</span><span class="sxs-lookup"><span data-stu-id="2728c-206">Make sure you've downloaded and unzipped hello [TwitterWPFClient.zip](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TwitterClient/TwitterWPFClient.zip) application, as listed in hello prerequisites.</span></span>

2. <span data-ttu-id="2728c-207">tooset hello значений во время выполнения (и только для текущего сеанса hello) выполните hello `TwitterWPFClient.exe` приложения.</span><span class="sxs-lookup"><span data-stu-id="2728c-207">tooset hello values at run time (and only for hello current session), run hello `TwitterWPFClient.exe` application.</span></span> <span data-ttu-id="2728c-208">Когда приложение hello будет предложено, введите hello следующие значения:</span><span class="sxs-lookup"><span data-stu-id="2728c-208">When hello application prompts you, enter hello following values:</span></span>

    * <span data-ttu-id="2728c-209">Здравствуйте, ключ пользователя Twitter (ключ API).</span><span class="sxs-lookup"><span data-stu-id="2728c-209">hello Twitter Consumer Key (API Key).</span></span>
    * <span data-ttu-id="2728c-210">Hello секрет пользователя Twitter (секрет API).</span><span class="sxs-lookup"><span data-stu-id="2728c-210">hello Twitter Consumer Secret (API Secret).</span></span>
    * <span data-ttu-id="2728c-211">Здравствуйте, Twitter токена доступа.</span><span class="sxs-lookup"><span data-stu-id="2728c-211">hello Twitter Access Token.</span></span>
    * <span data-ttu-id="2728c-212">Hello Twitter секрет маркера доступа.</span><span class="sxs-lookup"><span data-stu-id="2728c-212">hello Twitter Access Token Secret.</span></span>
    * <span data-ttu-id="2728c-213">Hello строку подключения, сохраненный ранее.</span><span class="sxs-lookup"><span data-stu-id="2728c-213">hello connection string information that you saved earlier.</span></span> <span data-ttu-id="2728c-214">Убедитесь, что используемая строка подключения hello удаленные hello `EntityPath` пару ключ значение из.</span><span class="sxs-lookup"><span data-stu-id="2728c-214">Make sure that you use hello connection string that you removed hello `EntityPath` key-value pair from.</span></span>
    * <span data-ttu-id="2728c-215">Здравствуйте Twitter ключевые слова, которые вы хотите toodetermine мнения по.</span><span class="sxs-lookup"><span data-stu-id="2728c-215">hello Twitter keywords that you want toodetermine sentiment for.</span></span>

   ![Запущенное приложение TwitterWpfClient со скрытыми параметрами](./media/stream-analytics-twitter-sentiment-analysis-trends/wpfclientlines.png)

3. <span data-ttu-id="2728c-217">значения hello tooset постоянно, используйте текстовый редактор tooopen hello TwitterWpfClient.exe.config файл.</span><span class="sxs-lookup"><span data-stu-id="2728c-217">tooset hello values persistently, use a text editor tooopen hello TwitterWpfClient.exe.config file.</span></span> <span data-ttu-id="2728c-218">Затем в hello `<appSettings>` элемент, это сделать:</span><span class="sxs-lookup"><span data-stu-id="2728c-218">Then in hello `<appSettings>` element, do this:</span></span>

    * <span data-ttu-id="2728c-219">Задать `oauth_consumer_key` toohello Twitter потребителя ключом (API).</span><span class="sxs-lookup"><span data-stu-id="2728c-219">Set `oauth_consumer_key` toohello Twitter Consumer Key (API Key).</span></span> 
    * <span data-ttu-id="2728c-220">Задать `oauth_consumer_secret` toohello секрет пользователя Twitter (секрет API).</span><span class="sxs-lookup"><span data-stu-id="2728c-220">Set `oauth_consumer_secret` toohello Twitter Consumer Secret (API Secret).</span></span>
    * <span data-ttu-id="2728c-221">Задать `oauth_token` toohello Twitter токена доступа.</span><span class="sxs-lookup"><span data-stu-id="2728c-221">Set `oauth_token` toohello Twitter Access Token.</span></span>
    * <span data-ttu-id="2728c-222">Задать `oauth_token_secret` toohello Twitter секрет маркера доступа.</span><span class="sxs-lookup"><span data-stu-id="2728c-222">Set `oauth_token_secret` toohello Twitter Access Token Secret.</span></span>

    <span data-ttu-id="2728c-223">Далее в hello `<appSettings>` элемент, внесите следующие изменения:</span><span class="sxs-lookup"><span data-stu-id="2728c-223">Later in hello `<appSettings>` element, make these changes:</span></span>

    * <span data-ttu-id="2728c-224">Задать `EventHubName` имя концентратора событий toohello (то есть toohello значение пути hello сущности).</span><span class="sxs-lookup"><span data-stu-id="2728c-224">Set `EventHubName` toohello event hub name (that is, toohello value of hello entity path).</span></span>
    * <span data-ttu-id="2728c-225">Задать `EventHubNameConnectionString` toohello строку подключения.</span><span class="sxs-lookup"><span data-stu-id="2728c-225">Set `EventHubNameConnectionString` toohello connection string.</span></span> <span data-ttu-id="2728c-226">Убедитесь, что используемая строка подключения hello удаленные hello `EntityPath` пару ключ значение из.</span><span class="sxs-lookup"><span data-stu-id="2728c-226">Make sure that you use hello connection string that you removed hello `EntityPath` key-value pair from.</span></span>

    <span data-ttu-id="2728c-227">Hello `<appSettings>` раздел выглядит как следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="2728c-227">hello `<appSettings>` section looks like hello following example.</span></span> <span data-ttu-id="2728c-228">(Для ясности и безопасности мы перенесли часть строк и удалили некоторые символы.)</span><span class="sxs-lookup"><span data-stu-id="2728c-228">(For clarity and security, we wrapped some lines and removed some characters.)</span></span>

    ![Файл конфигурации приложения TwitterWpfClient в текстовом редакторе, показывающая hello Twitter ключи и секретные данные и данные строки подключения концентратора событий hello](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-tiwtter-app-config.png)
 
4. <span data-ttu-id="2728c-230">Если вы уже не запускали приложение hello, программу TwitterWpfClient.exe.</span><span class="sxs-lookup"><span data-stu-id="2728c-230">If you didn't already start hello application, run TwitterWpfClient.exe now.</span></span> 

5. <span data-ttu-id="2728c-231">Щелкните hello зеленую кнопку toocollect социальных мнений.</span><span class="sxs-lookup"><span data-stu-id="2728c-231">Click hello green start button toocollect social sentiment.</span></span> <span data-ttu-id="2728c-232">Можно увидеть события Твитов с hello **CreatedAt**, **разделе**, и **SentimentScore** значения, отправляемых tooyour концентратора событий.</span><span class="sxs-lookup"><span data-stu-id="2728c-232">You see Tweet events with hello **CreatedAt**, **Topic**, and **SentimentScore** values being sent tooyour event hub.</span></span>

    ![Запущенное приложение TwitterWpfClient со списком твитов](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-twitter-app-listing.png)

    >[!NOTE]
    ><span data-ttu-id="2728c-234">Если возникают ошибки, и вы не видите поток твиты, отображаются в нижней части окна hello hello, повторно проверьте hello ключи и секретные коды.</span><span class="sxs-lookup"><span data-stu-id="2728c-234">If you see errors, and you don't see a stream of tweets displayed in hello lower part of hello window, double-check hello keys and secrets.</span></span> <span data-ttu-id="2728c-235">Также проверьте строку подключения hello (Убедитесь, что он не включает hello `EntityPath` ключей и значений.)</span><span class="sxs-lookup"><span data-stu-id="2728c-235">Also check hello connection string (make sure that it does not include hello `EntityPath` key and value.)</span></span>


## <a name="create-a-stream-analytics-job"></a><span data-ttu-id="2728c-236">Создание задания Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="2728c-236">Create a Stream Analytics job</span></span>

<span data-ttu-id="2728c-237">Теперь, когда события твитов потоковая передача в режиме реального времени из Twitter, настройкой tooanalyze задания Stream Analytics эти события в режиме реального времени.</span><span class="sxs-lookup"><span data-stu-id="2728c-237">Now that tweet events are streaming in real time from Twitter, you can set up a Stream Analytics job tooanalyze these events in real time.</span></span>

1. <span data-ttu-id="2728c-238">В hello портал Azure, щелкните **New** > **Интернета вещей** > **задания Stream Analytics**.</span><span class="sxs-lookup"><span data-stu-id="2728c-238">In hello Azure portal, click **New** > **Internet of Things** > **Stream Analytics job**.</span></span>

2. <span data-ttu-id="2728c-239">Имя задания hello `socialtwitter-sa-job` и укажите подписки, группы ресурсов и расположение.</span><span class="sxs-lookup"><span data-stu-id="2728c-239">Name hello job `socialtwitter-sa-job` and specify a subscription, resource group, and location.</span></span>

    <span data-ttu-id="2728c-240">Это помешает tooplace hello задания и hello концентратора событий в hello же регионе для оптимальной производительности и, что не придется tootransfer данных между регионами.</span><span class="sxs-lookup"><span data-stu-id="2728c-240">It's a good idea tooplace hello job and hello event hub in hello same region for best performance and so that you don't pay tootransfer data between regions.</span></span>

    ![Создание нового задания Stream Analytics](./media/stream-analytics-twitter-sentiment-analysis-trends/newjob.png)

3. <span data-ttu-id="2728c-242">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="2728c-242">Click **Create**.</span></span>

    <span data-ttu-id="2728c-243">создается задание Hello и hello портал отобразит сведения о задании.</span><span class="sxs-lookup"><span data-stu-id="2728c-243">hello job is created and hello portal displays job details.</span></span>


## <a name="specify-hello-job-input"></a><span data-ttu-id="2728c-244">Укажите входной задания hello</span><span class="sxs-lookup"><span data-stu-id="2728c-244">Specify hello job input</span></span>

1. <span data-ttu-id="2728c-245">В задание Stream Analytics в разделе **топологии задания** в середине hello hello задания колонка, щелкните **входов**.</span><span class="sxs-lookup"><span data-stu-id="2728c-245">In your Stream Analytics job, under **Job Topology** in hello middle of hello job blade, click **Inputs**.</span></span> 

2. <span data-ttu-id="2728c-246">В hello **входов** колонка, щелкните  **+ &nbsp;добавить** и затем заполнить hello колонка со следующими значениями:</span><span class="sxs-lookup"><span data-stu-id="2728c-246">In hello **Inputs** blade, click **+&nbsp;Add** and then fill out hello blade with these values:</span></span>

    * <span data-ttu-id="2728c-247">**Входной псевдоним**: hello используйте имя `TwitterStream`.</span><span class="sxs-lookup"><span data-stu-id="2728c-247">**Input alias**: Use hello name `TwitterStream`.</span></span> <span data-ttu-id="2728c-248">Если используется другое имя, запишите его, так как оно понадобится позже.</span><span class="sxs-lookup"><span data-stu-id="2728c-248">If you use a different name, make a note of it because you need it later.</span></span>
    * <span data-ttu-id="2728c-249">**Тип источника**: выберите **Поток данных**.</span><span class="sxs-lookup"><span data-stu-id="2728c-249">**Source type**: Select **Data stream**.</span></span>
    * <span data-ttu-id="2728c-250">**Источник**: выберите **Концентратор событий**.</span><span class="sxs-lookup"><span data-stu-id="2728c-250">**Source**: Select **Event hub**.</span></span>
    * <span data-ttu-id="2728c-251">**Вариант импорта**: выберите **Использовать концентратор событий из текущей подписки**.</span><span class="sxs-lookup"><span data-stu-id="2728c-251">**Import option**: Select **Use event hub from current subscription**.</span></span> 
    * <span data-ttu-id="2728c-252">**Пространство имен служебной шины**: выберите пространство имен концентратора hello событий, созданной ранее (`<yourname>-socialtwitter-eh-ns`).</span><span class="sxs-lookup"><span data-stu-id="2728c-252">**Service bus namespace**: Select hello event hub namespace that you created earlier (`<yourname>-socialtwitter-eh-ns`).</span></span>
    * <span data-ttu-id="2728c-253">**Концентратор событий**: hello выберите концентратор событий, созданной ранее (`socialtwitter-eh`).</span><span class="sxs-lookup"><span data-stu-id="2728c-253">**Event hub**: Select hello event hub that you created earlier (`socialtwitter-eh`).</span></span>
    * <span data-ttu-id="2728c-254">**Имя политики концентратора событий**: выберите политику доступа hello, созданной ранее (`socialtwitter-access`).</span><span class="sxs-lookup"><span data-stu-id="2728c-254">**Event hub policy name**: Select hello access policy that you created earlier (`socialtwitter-access`).</span></span>

    ![Создание новых входных данных для задания Streaming Analytics](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-twitter-new-input.png)

3. <span data-ttu-id="2728c-256">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="2728c-256">Click **Create**.</span></span>


## <a name="specify-hello-job-query"></a><span data-ttu-id="2728c-257">Укажите запрос hello задания</span><span class="sxs-lookup"><span data-stu-id="2728c-257">Specify hello job query</span></span>

<span data-ttu-id="2728c-258">Stream Analytics поддерживает простую декларативную модель запроса для описания преобразований.</span><span class="sxs-lookup"><span data-stu-id="2728c-258">Stream Analytics supports a simple, declarative query model that describes transformations.</span></span> <span data-ttu-id="2728c-259">toolearn Дополнительные сведения о языке hello. в разделе hello [Справка языка запросов Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx).</span><span class="sxs-lookup"><span data-stu-id="2728c-259">toolearn more about hello language, see hello [Azure Stream Analytics Query Language Reference](https://msdn.microsoft.com/library/azure/dn834998.aspx).</span></span>  <span data-ttu-id="2728c-260">Это руководство поможет создать и проверить несколько запросов по данным Twitter.</span><span class="sxs-lookup"><span data-stu-id="2728c-260">This tutorial helps you author and test several queries over Twitter data.</span></span>

<span data-ttu-id="2728c-261">Количество hello toocompare упоминания между разделами, можно использовать [«переворачивающееся» окно](https://msdn.microsoft.com/library/azure/dn835055.aspx) tooget hello число упоминания по разделам каждые пять секунд.</span><span class="sxs-lookup"><span data-stu-id="2728c-261">toocompare hello number of mentions among topics, you can use a [Tumbling window](https://msdn.microsoft.com/library/azure/dn835055.aspx) tooget hello count of mentions by topic every five seconds.</span></span>

1. <span data-ttu-id="2728c-262">Закрыть hello **входов** колонки, если это еще не сделано.</span><span class="sxs-lookup"><span data-stu-id="2728c-262">Close hello **Inputs** blade if you haven't already.</span></span>

2. <span data-ttu-id="2728c-263">В колонке задания hello щелкните hello **запроса** поле.</span><span class="sxs-lookup"><span data-stu-id="2728c-263">In hello job blade, click hello **Query** box.</span></span> <span data-ttu-id="2728c-264">Azure перечислены hello входов и выходов, которые настроены для задания hello и позволяет создать запрос, который позволяет преобразования hello входного потока при передаче toohello выходные данные.</span><span class="sxs-lookup"><span data-stu-id="2728c-264">Azure lists hello inputs and outputs that are configured for hello job, and lets you create a query that lets you transform hello input stream as it is sent toohello output.</span></span>

3. <span data-ttu-id="2728c-265">Убедитесь, что выполнение этого TwitterWpfClient приложения hello.</span><span class="sxs-lookup"><span data-stu-id="2728c-265">Make sure that hello TwitterWpfClient application is running.</span></span> 

3. <span data-ttu-id="2728c-266">В hello **запроса** колонке нажмите кнопку Далее toohello точек hello `TwitterStream` входных данных, а затем выберите **выборку данных из входных данных**.</span><span class="sxs-lookup"><span data-stu-id="2728c-266">In hello **Query** blade, click hello dots next toohello `TwitterStream` input and then select **Sample data from input**.</span></span>

    ![Меню параметров toouse образцы данных для hello запись в задание Streaming Analytics с «Образец данных из входных данных» выбран](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-sample-data-from-input.png)

    <span data-ttu-id="2728c-268">Это открывает колонку, которая позволяет указать, сколько tooget данных образца, определенные в терминах продолжительность tooread hello входного потока.</span><span class="sxs-lookup"><span data-stu-id="2728c-268">This opens a blade that lets you specify how much sample data tooget, defined in terms of how long tooread hello input stream.</span></span>

4. <span data-ttu-id="2728c-269">Задать **минут** too3 и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="2728c-269">Set **Minutes** too3 and then click **OK**.</span></span> 
    
    ![Параметры выборки hello входного потока с выбран «3 минут».](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-input-create-sample-data.png)

    <span data-ttu-id="2728c-271">Azure образцы данные из входного потока hello за 3 минуты и предлагает при готовности данных образец hello.</span><span class="sxs-lookup"><span data-stu-id="2728c-271">Azure samples 3 minutes' worth of data from hello input stream and notifies you when hello sample data is ready.</span></span> <span data-ttu-id="2728c-272">(Это займет некоторое время.)</span><span class="sxs-lookup"><span data-stu-id="2728c-272">(This takes a short while.)</span></span> 

    <span data-ttu-id="2728c-273">данные образца Hello временно хранятся и доступны после открытия окна запроса hello.</span><span class="sxs-lookup"><span data-stu-id="2728c-273">hello sample data is stored temporarily and is available while you have hello query window open.</span></span> <span data-ttu-id="2728c-274">Если закрыть окно запроса hello данные образца hello удаляются и имеют toocreate новый набор образца данных.</span><span class="sxs-lookup"><span data-stu-id="2728c-274">If you close hello query window, hello sample data is discarded, and you have toocreate a new set of sample data.</span></span> 

5. <span data-ttu-id="2728c-275">Изменить запрос hello в редакторе toohello hello кода ниже:</span><span class="sxs-lookup"><span data-stu-id="2728c-275">Change hello query in hello code editor toohello following:</span></span>

    ```
    SELECT System.Timestamp as Time, Topic, COUNT(*)
    FROM TwitterStream TIMESTAMP BY CreatedAt
    GROUP BY TUMBLINGWINDOW(s, 5), Topic
    ```

    <span data-ttu-id="2728c-276">Если не использовать `TwitterStream` как hello псевдоним для ввода hello, замените на псевдоним для `TwitterStream` в запросе hello.</span><span class="sxs-lookup"><span data-stu-id="2728c-276">If didn't use `TwitterStream` as hello alias for hello input, substitute your alias for `TwitterStream` in hello query.</span></span>  

    <span data-ttu-id="2728c-277">Этот запрос использует hello **TIMESTAMP BY** ключевое слово toospecify поле метки времени в toobe hello полезных данных, используемых в hello временных вычислений.</span><span class="sxs-lookup"><span data-stu-id="2728c-277">This query uses hello **TIMESTAMP BY** keyword toospecify a timestamp field in hello payload toobe used in hello temporal computation.</span></span> <span data-ttu-id="2728c-278">Если это поле не указана, операция над окнами hello выполняется с помощью hello времени поступления каждого события в концентратор событий hello.</span><span class="sxs-lookup"><span data-stu-id="2728c-278">If this field isn't specified, hello windowing operation is performed by using hello time that each event arrived at hello event hub.</span></span> <span data-ttu-id="2728c-279">Дополнительные сведения в разделе "hello «время прибытия и время приложения»" [Справка запросов Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx).</span><span class="sxs-lookup"><span data-stu-id="2728c-279">Learn more in hello "Arrival Time vs Application Time" section of [Stream Analytics Query Reference](https://msdn.microsoft.com/library/azure/dn834998.aspx).</span></span>

    <span data-ttu-id="2728c-280">Этот запрос также получают доступ к отметку времени для hello конца каждого окна с помощью hello **System.Timestamp** свойство.</span><span class="sxs-lookup"><span data-stu-id="2728c-280">This query also accesses a timestamp for hello end of each window by using hello **System.Timestamp** property.</span></span>

5. <span data-ttu-id="2728c-281">Нажмите **Проверить**.</span><span class="sxs-lookup"><span data-stu-id="2728c-281">Click **Test**.</span></span> <span data-ttu-id="2728c-282">запрос Hello запускает hello данные, которые вы выборки.</span><span class="sxs-lookup"><span data-stu-id="2728c-282">hello query runs against hello data that you sampled.</span></span>
    
6. <span data-ttu-id="2728c-283">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="2728c-283">Click **Save**.</span></span> <span data-ttu-id="2728c-284">Это экономит hello запроса как часть задание Streaming Analytics hello.</span><span class="sxs-lookup"><span data-stu-id="2728c-284">This saves hello query as part of hello Streaming Analytics job.</span></span> <span data-ttu-id="2728c-285">(Он не сохраняет данные образца hello).</span><span class="sxs-lookup"><span data-stu-id="2728c-285">(It doesn't save hello sample data.)</span></span>


## <a name="experiment-using-different-fields-from-hello-stream"></a><span data-ttu-id="2728c-286">Поэкспериментируйте с помощью разных полей из потока hello</span><span class="sxs-lookup"><span data-stu-id="2728c-286">Experiment using different fields from hello stream</span></span> 

<span data-ttu-id="2728c-287">Hello следующей таблице перечислены поля hello, которые являются частью hello потоковой передачи данных JSON.</span><span class="sxs-lookup"><span data-stu-id="2728c-287">hello following table lists hello fields that are part of hello JSON streaming data.</span></span> <span data-ttu-id="2728c-288">При желании вы свободного tooexperiment в редакторе запросов hello.</span><span class="sxs-lookup"><span data-stu-id="2728c-288">Feel free tooexperiment in hello query editor.</span></span>

|<span data-ttu-id="2728c-289">Свойство JSON</span><span class="sxs-lookup"><span data-stu-id="2728c-289">JSON property</span></span> | <span data-ttu-id="2728c-290">Определение</span><span class="sxs-lookup"><span data-stu-id="2728c-290">Definition</span></span>|
|--- | ---|
|<span data-ttu-id="2728c-291">CreatedAt</span><span class="sxs-lookup"><span data-stu-id="2728c-291">CreatedAt</span></span> | <span data-ttu-id="2728c-292">Hello время была создана, твит hello</span><span class="sxs-lookup"><span data-stu-id="2728c-292">hello time that hello tweet was created</span></span>|
|<span data-ttu-id="2728c-293">Раздел</span><span class="sxs-lookup"><span data-stu-id="2728c-293">Topic</span></span> | <span data-ttu-id="2728c-294">Hello раздел, соответствующий hello указано ключевое слово</span><span class="sxs-lookup"><span data-stu-id="2728c-294">hello topic that matches hello specified keyword</span></span>|
|<span data-ttu-id="2728c-295">SentimentScore</span><span class="sxs-lookup"><span data-stu-id="2728c-295">SentimentScore</span></span> | <span data-ttu-id="2728c-296">показатель мнений Hello из Sentiment140</span><span class="sxs-lookup"><span data-stu-id="2728c-296">hello sentiment score from Sentiment140</span></span>|
|<span data-ttu-id="2728c-297">Автор</span><span class="sxs-lookup"><span data-stu-id="2728c-297">Author</span></span> | <span data-ttu-id="2728c-298">Дескриптор Twitter Hello отправки твитов hello</span><span class="sxs-lookup"><span data-stu-id="2728c-298">hello Twitter handle that sent hello tweet</span></span>|
|<span data-ttu-id="2728c-299">текст</span><span class="sxs-lookup"><span data-stu-id="2728c-299">Text</span></span> | <span data-ttu-id="2728c-300">Полный текст Hello твит hello</span><span class="sxs-lookup"><span data-stu-id="2728c-300">hello full body of hello tweet</span></span>|


## <a name="create-an-output-sink"></a><span data-ttu-id="2728c-301">Создание приемника выходных данных</span><span class="sxs-lookup"><span data-stu-id="2728c-301">Create an output sink</span></span>

<span data-ttu-id="2728c-302">Поток событий, событий ввода tooingest концентратора событий и запроса tooperform преобразования потока hello успешно определена.</span><span class="sxs-lookup"><span data-stu-id="2728c-302">You have now defined an event stream, an event hub input tooingest events, and a query tooperform a transformation over hello stream.</span></span> <span data-ttu-id="2728c-303">Последний шаг Hello — toodefine приемника выходных данных для задания hello.</span><span class="sxs-lookup"><span data-stu-id="2728c-303">hello last step is toodefine an output sink for hello job.</span></span>  

<span data-ttu-id="2728c-304">В этом учебнике записи hello статистическая обработка события твитов из tooAzure запроса задания hello хранилища больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="2728c-304">In this tutorial, you write hello aggregated tweet events from hello job query tooAzure Blob storage.</span></span>  <span data-ttu-id="2728c-305">Также можно отправить на результаты tooAzure базы данных SQL, хранилище таблиц Azure концентраторов событий или для Power BI, в зависимости от приложения.</span><span class="sxs-lookup"><span data-stu-id="2728c-305">You can also push your results tooAzure SQL Database, Azure Table storage, Event Hubs, or Power BI, depending on your application needs.</span></span>

## <a name="specify-hello-job-output"></a><span data-ttu-id="2728c-306">Укажите результат выполнения задания hello</span><span class="sxs-lookup"><span data-stu-id="2728c-306">Specify hello job output</span></span>

1. <span data-ttu-id="2728c-307">В hello **топологии задания** щелкните hello **вывода** поле.</span><span class="sxs-lookup"><span data-stu-id="2728c-307">In hello **Job Topology** section, click hello **Output** box.</span></span> 

2. <span data-ttu-id="2728c-308">В hello **выходов** колонка, щелкните  **+ &nbsp;добавить** и затем заполнить hello колонка со следующими значениями:</span><span class="sxs-lookup"><span data-stu-id="2728c-308">In hello **Outputs** blade, click **+&nbsp;Add** and then fill out hello blade with these values:</span></span>

    * <span data-ttu-id="2728c-309">**Псевдоним вывода**: hello используйте имя `TwitterStream-Output`.</span><span class="sxs-lookup"><span data-stu-id="2728c-309">**Output alias**: Use hello name `TwitterStream-Output`.</span></span> 
    * <span data-ttu-id="2728c-310">**Приемник.** Выберите **хранилище BLOB-объектов**.</span><span class="sxs-lookup"><span data-stu-id="2728c-310">**Sink**: Select **Blob storage**.</span></span>
    * <span data-ttu-id="2728c-311">**Параметры импорта**: выберите **Использовать хранилище BLOB-объектов из текущей подписки**.</span><span class="sxs-lookup"><span data-stu-id="2728c-311">**Import options**: Select **Use blob storage from current subscription**.</span></span>
    * <span data-ttu-id="2728c-312">**Учетная запись хранения**.</span><span class="sxs-lookup"><span data-stu-id="2728c-312">**Storage account**.</span></span> <span data-ttu-id="2728c-313">Выберите **Создать новую учетную запись хранения**.</span><span class="sxs-lookup"><span data-stu-id="2728c-313">Select **Create a new storage account.**</span></span>
    * <span data-ttu-id="2728c-314">**Учетная запись хранения** (второе диалоговое окно).</span><span class="sxs-lookup"><span data-stu-id="2728c-314">**Storage account** (second box).</span></span> <span data-ttu-id="2728c-315">Введите `YOURNAMEsa`, где `YOURNAME` — ваше имя или другая уникальная строка.</span><span class="sxs-lookup"><span data-stu-id="2728c-315">Enter `YOURNAMEsa`, where `YOURNAME` is your name or another unique string.</span></span> <span data-ttu-id="2728c-316">Имя Hello можно использовать только строчные буквы и цифры и должно быть уникальным среди Azure.</span><span class="sxs-lookup"><span data-stu-id="2728c-316">hello name can use only lowercase letters and numbers, and it must be unique across Azure.</span></span> 
    * <span data-ttu-id="2728c-317">**Контейнер**:</span><span class="sxs-lookup"><span data-stu-id="2728c-317">**Container**.</span></span> <span data-ttu-id="2728c-318">Укажите `socialtwitter`.</span><span class="sxs-lookup"><span data-stu-id="2728c-318">Enter `socialtwitter`.</span></span>
    <span data-ttu-id="2728c-319">Имя учетной записи хранения Hello и имя контейнера, используемые вместе tooprovide URI для хранилища больших двоичных объектов hello, следующим образом:</span><span class="sxs-lookup"><span data-stu-id="2728c-319">hello storage account name and container name are used together tooprovide a URI for hello blob storage, like this:</span></span> 

    `http://YOURNAMEsa.blob.core.windows.net/socialtwitter/...`
    
    ![Колонка "Новые выходные данные" для задания Stream Analytics](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-output-blob-storage.png)
    
4. <span data-ttu-id="2728c-321">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="2728c-321">Click **Create**.</span></span> 

    <span data-ttu-id="2728c-322">Azure создает учетную запись хранения hello и автоматически создает ключ.</span><span class="sxs-lookup"><span data-stu-id="2728c-322">Azure creates hello storage account and generates a key automatically.</span></span> 

5. <span data-ttu-id="2728c-323">Закрыть hello **выходов** колонку.</span><span class="sxs-lookup"><span data-stu-id="2728c-323">Close hello **Outputs** blade.</span></span> 


## <a name="start-hello-job"></a><span data-ttu-id="2728c-324">Запустить задание hello</span><span class="sxs-lookup"><span data-stu-id="2728c-324">Start hello job</span></span>

<span data-ttu-id="2728c-325">Входные данные для задания, запрос и выходные данные указаны.</span><span class="sxs-lookup"><span data-stu-id="2728c-325">A job input, query, and output are specified.</span></span> <span data-ttu-id="2728c-326">Все задания Stream Analytics готов toostart hello.</span><span class="sxs-lookup"><span data-stu-id="2728c-326">You are ready toostart hello Stream Analytics job.</span></span>

1. <span data-ttu-id="2728c-327">Убедитесь, что выполнение этого TwitterWpfClient приложения hello.</span><span class="sxs-lookup"><span data-stu-id="2728c-327">Make sure that hello TwitterWpfClient application is running.</span></span> 

2. <span data-ttu-id="2728c-328">В колонке hello задания, нажмите кнопку **запустить**.</span><span class="sxs-lookup"><span data-stu-id="2728c-328">In hello job blade, click **Start**.</span></span>

    ![Запустить задание Stream Analytics hello](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-sa-job-start-output.png)

3. <span data-ttu-id="2728c-330">В hello **запуска задания** колонке для **время начала выходные данные задания**выберите **теперь** и нажмите кнопку **запустить**.</span><span class="sxs-lookup"><span data-stu-id="2728c-330">In hello **Start job** blade, for **Job output start time**, select **Now** and then click **Start**.</span></span> 

    ![Колонка «Запустить задание» для задания Stream Analytics hello](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-sa-job-start-job-blade.png)

    <span data-ttu-id="2728c-332">Azure уведомляет о запуска задания hello и в колонке задания hello hello состояние отображается как **под управлением**.</span><span class="sxs-lookup"><span data-stu-id="2728c-332">Azure notifies you when hello job has started, and in hello job blade, hello status is displayed as **Running**.</span></span>

    ![Выполнение задания](./media/stream-analytics-twitter-sentiment-analysis-trends/jobrunning.png)

## <a name="view-output-for-sentiment-analysis"></a><span data-ttu-id="2728c-334">Просмотр выходных данных для анализа тональности</span><span class="sxs-lookup"><span data-stu-id="2728c-334">View output for sentiment analysis</span></span>

<span data-ttu-id="2728c-335">После задания будет запущен и обрабатывается в режиме реального времени поток Twitter hello, можно просмотреть выходные данные hello для анализа мнений.</span><span class="sxs-lookup"><span data-stu-id="2728c-335">After your job has started running and is processing hello real-time Twitter stream, you can view hello output for sentiment analysis.</span></span>

<span data-ttu-id="2728c-336">Можно использовать средства, подобного [обозреватель хранилищ Azure](https://http://storageexplorer.com/) или [обозреватель Azure](http://www.cerebrata.com/products/azure-explorer/introduction) tooview вывода вашу работу в режиме реального времени.</span><span class="sxs-lookup"><span data-stu-id="2728c-336">You can use a tool like [Azure Storage Explorer](https://http://storageexplorer.com/) or [Azure Explorer](http://www.cerebrata.com/products/azure-explorer/introduction) tooview your job output in real time.</span></span> <span data-ttu-id="2728c-337">Здесь можно использовать [Power BI](https://powerbi.com/) tooextend вашего приложения tooinclude настроенной панели мониторинга, например hello показанной hello следующий снимок экрана:</span><span class="sxs-lookup"><span data-stu-id="2728c-337">From here, you can use [Power BI](https://powerbi.com/) tooextend your application tooinclude a customized dashboard like hello one shown in hello following screenshot:</span></span>

![Power BI](./media/stream-analytics-twitter-sentiment-analysis-trends/power-bi.png)


## <a name="create-another-query-tooidentify-trending-topics"></a><span data-ttu-id="2728c-339">Создать разделы тенденций tooidentify другого запроса</span><span class="sxs-lookup"><span data-stu-id="2728c-339">Create another query tooidentify trending topics</span></span>

<span data-ttu-id="2728c-340">Зависит от другого запроса, можно использовать мнений Twitter toounderstand [скользящее окно](https://msdn.microsoft.com/library/azure/dn835051.aspx).</span><span class="sxs-lookup"><span data-stu-id="2728c-340">Another query you can use toounderstand Twitter sentiment is based on a [Sliding Window](https://msdn.microsoft.com/library/azure/dn835051.aspx).</span></span> <span data-ttu-id="2728c-341">tooidentify тенденций разделов, поиск разделов, которые пересекают пороговое значение для упоминания о в определенное время.</span><span class="sxs-lookup"><span data-stu-id="2728c-341">tooidentify trending topics, you look for topics that cross a threshold value for mentions in a specified amount of time.</span></span>

<span data-ttu-id="2728c-342">Для целей этого учебника hello Проверьте наличие разделы, в которых упоминаются более чем в 20 раз в hello последние 5 секунд.</span><span class="sxs-lookup"><span data-stu-id="2728c-342">For hello purposes of this tutorial, you check for topics that are mentioned more than 20 times in hello last 5 seconds.</span></span>

1. <span data-ttu-id="2728c-343">В колонке hello задания, нажмите кнопку **остановить** toostop hello задания.</span><span class="sxs-lookup"><span data-stu-id="2728c-343">In hello job blade, click **Stop** toostop hello job.</span></span> 

2. <span data-ttu-id="2728c-344">В hello **топологии задания** щелкните hello **запроса** поле.</span><span class="sxs-lookup"><span data-stu-id="2728c-344">In hello **Job Topology** section, click hello **Query** box.</span></span> 

3. <span data-ttu-id="2728c-345">Измените следующие toohello hello запроса:</span><span class="sxs-lookup"><span data-stu-id="2728c-345">Change hello query toohello following:</span></span>

    ```    
    SELECT System.Timestamp as Time, Topic, COUNT(*) as Mentions
    FROM TwitterStream TIMESTAMP BY CreatedAt
    GROUP BY SLIDINGWINDOW(s, 5), topic
    HAVING COUNT(*) > 20
    ```

4. <span data-ttu-id="2728c-346">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="2728c-346">Click **Save**.</span></span>

5. <span data-ttu-id="2728c-347">Убедитесь, что выполнение этого TwitterWpfClient приложения hello.</span><span class="sxs-lookup"><span data-stu-id="2728c-347">Make sure that hello TwitterWpfClient application is running.</span></span> 

6. <span data-ttu-id="2728c-348">Нажмите кнопку **запустить** toorestart hello задания с помощью нового запроса hello.</span><span class="sxs-lookup"><span data-stu-id="2728c-348">Click **Start** toorestart hello job using hello new query.</span></span>


## <a name="get-support"></a><span data-ttu-id="2728c-349">Получение поддержки</span><span class="sxs-lookup"><span data-stu-id="2728c-349">Get support</span></span>
<span data-ttu-id="2728c-350">За дополнительной помощью обращайтесь на наш [форум Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="2728c-350">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2728c-351">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2728c-351">Next steps</span></span>
* [<span data-ttu-id="2728c-352">Введение tooAzure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="2728c-352">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="2728c-353">Приступая к работе с Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="2728c-353">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="2728c-354">Масштабирование заданий в службе Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="2728c-354">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="2728c-355">Справочник по языку запросов Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="2728c-355">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="2728c-356">Справочник по API-интерфейсу REST управления Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="2728c-356">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
