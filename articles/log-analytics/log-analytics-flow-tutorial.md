---
title: "aaaAutomate анализа журналов Azure обрабатывает с потоком Microsoft"
description: "Дополнительные сведения об использовании Microsoft Flow tooquickly автоматизации повторяющихся процессов с помощью соединителя Azure Log Analytics hello."
services: log-analytics
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: log-analytics
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: bwren
ms.openlocfilehash: 52026df968682842cc9f8d55f6f9875c5f9c10b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="automate-log-analytics-processes-with-hello-connector-for-microsoft-flow"></a><span data-ttu-id="e944a-103">Автоматизировать процессы службы анализа журналов с соединителем hello для Microsoft Flow</span><span class="sxs-lookup"><span data-stu-id="e944a-103">Automate Log Analytics processes with hello connector for Microsoft Flow</span></span>
<span data-ttu-id="e944a-104">[Microsoft Flow](https://ms.flow.microsoft.com) позволяет автоматизировать toocreate рабочих процессов, использующих сотни действия для различных служб.</span><span class="sxs-lookup"><span data-stu-id="e944a-104">[Microsoft Flow](https://ms.flow.microsoft.com) allows you toocreate automated workflows using hundreds of actions for a variety of services.</span></span> <span data-ttu-id="e944a-105">Выходные данные из одного действия может использоваться как входные tooanother, позволяя toocreate интеграции между различными службами.</span><span class="sxs-lookup"><span data-stu-id="e944a-105">Output from one action can be used as input tooanother allowing you toocreate integration between different services.</span></span>  <span data-ttu-id="e944a-106">Соединитель Hello анализа журналов Azure для Microsoft Flow разрешить toobuild рабочих процессов, которые включают данные, полученные путем поиска журналов в службе анализа журналов.</span><span class="sxs-lookup"><span data-stu-id="e944a-106">hello Azure Log Analytics connector for Microsoft Flow allow you toobuild workflows that include data retrieved by log searches in Log Analytics.</span></span>

<span data-ttu-id="e944a-107">Например можно использовать данные анализа журналов Microsoft Flow toouse уведомление по электронной почте из Office 365, создание ошибки в Visual Studio Team Services или резерв сообщение.</span><span class="sxs-lookup"><span data-stu-id="e944a-107">For example, you can use Microsoft Flow toouse Log Analytics data in an email notification from Office 365, create a bug in Visual Studio Team Services, or post a Slack message.</span></span>  <span data-ttu-id="e944a-108">Вы можете запускать рабочие процессы с помощью простого расписания или какого-либо действия в подключенной службе, например при получении почты или твита.</span><span class="sxs-lookup"><span data-stu-id="e944a-108">You can trigger a workflow by a simple schedule or from some action in a connected service such as when a mail or a tweet is received.</span></span>  


> [!NOTE]
> <span data-ttu-id="e944a-109">Hello анализа журналов Azure для Microsoft Flow соединителю вашей рабочей области обновления toobe toohello новый анализа журналов язык запросов.</span><span class="sxs-lookup"><span data-stu-id="e944a-109">hello Azure Log Analytics connector for Microsoft Flow requires your workspace toobe upgraded toohello new Log Analytics query language.</span></span> <span data-ttu-id="e944a-110">Можно узнать больше о новом языке hello и получить tooupgrade процедуры hello в рабочей области [обновление поиск журнала toonew рабочей области Azure Log Analytics](log-analytics-log-search-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="e944a-110">You can learn more about hello new language and get hello procedure tooupgrade your workspace at [Upgrade your Azure Log Analytics workspace toonew log search](log-analytics-log-search-upgrade.md).</span></span>  

<span data-ttu-id="e944a-111">Учебник Hello в этой статье показано, как toocreate поток, который автоматически отправляет hello результатов поиска журналов Служба аналитики журналов по электронной почте, лишь один пример того, как можно использовать в Microsoft Flow анализа журналов.</span><span class="sxs-lookup"><span data-stu-id="e944a-111">hello tutorial in this article shows you how toocreate a flow that automatically sends hello results of a Log Analytics log search by email, just one example of how you can use Log Analytics in Microsoft Flow.</span></span> 


## <a name="step-1-create-a-flow"></a><span data-ttu-id="e944a-112">Шаг 1. Создание последовательности</span><span class="sxs-lookup"><span data-stu-id="e944a-112">Step 1: Create a flow</span></span>
1. <span data-ttu-id="e944a-113">Войдите в слишком[Microsoft Flow](http://flow.microsoft.com)и выберите **Мои потоки**.</span><span class="sxs-lookup"><span data-stu-id="e944a-113">Sign in too[Microsoft Flow](http://flow.microsoft.com), and select **My Flows**.</span></span>
2. <span data-ttu-id="e944a-114">Щелкните **Создать с нуля**.</span><span class="sxs-lookup"><span data-stu-id="e944a-114">Click **+ Create from blank**.</span></span>

## <a name="step-2-create-a-trigger-for-your-flow"></a><span data-ttu-id="e944a-115">Шаг 2. Создание триггера для последовательности</span><span class="sxs-lookup"><span data-stu-id="e944a-115">Step 2: Create a trigger for your flow</span></span>
1. <span data-ttu-id="e944a-116">Щелкните **Search hundreds of connectors and triggers** (Поиск по сотням соединителей и триггеров).</span><span class="sxs-lookup"><span data-stu-id="e944a-116">Click **Search hundreds of connectors and triggers**.</span></span>
2. <span data-ttu-id="e944a-117">Тип **расписание** в поле поиска hello.</span><span class="sxs-lookup"><span data-stu-id="e944a-117">Type **Schedule** in hello search box.</span></span>
3. <span data-ttu-id="e944a-118">Выберите **Расписание**, а затем **Расписание — повторение**.</span><span class="sxs-lookup"><span data-stu-id="e944a-118">Select **Schedule**, and then select **Schedule - Recurrence**.</span></span>
4. <span data-ttu-id="e944a-119">В hello **частоты** выберите **день** и в hello **интервал** введите **1**.</span><span class="sxs-lookup"><span data-stu-id="e944a-119">In hello **Frequency** box select **Day** and in hello **Interval** box, enter **1**.</span></span><br><br><span data-ttu-id="e944a-120">![Диалоговое окно триггера Microsoft Flow](media/log-analytics-flow-tutorial/flow01.png)</span><span class="sxs-lookup"><span data-stu-id="e944a-120">![Microsoft Flow trigger dialog box](media/log-analytics-flow-tutorial/flow01.png)</span></span>


## <a name="step-3-add-a-log-analytics-action"></a><span data-ttu-id="e944a-121">Шаг 3. Добавление действия Log Analytics</span><span class="sxs-lookup"><span data-stu-id="e944a-121">Step 3: Add a Log Analytics action</span></span>
1. <span data-ttu-id="e944a-122">Выберите поле **+ Новый шаг**, а затем щелкните **Добавить действие**.</span><span class="sxs-lookup"><span data-stu-id="e944a-122">Click **+ New step**, and then click **Add an action**.</span></span>
2. <span data-ttu-id="e944a-123">Найдите **Log Analytics**.</span><span class="sxs-lookup"><span data-stu-id="e944a-123">Search for **Log Analytics**.</span></span>
3. <span data-ttu-id="e944a-124">Щелкните **Azure Log Analytics – Run query and visualize results** (Azure Log Analytics – выполнить запрос и отобразить результаты).</span><span class="sxs-lookup"><span data-stu-id="e944a-124">Click **Azure Log Analytics – Run query and visualize results**.</span></span><br><br><span data-ttu-id="e944a-125">![Окно выполнения запроса Log Analytics](media/log-analytics-flow-tutorial/flow02.png)</span><span class="sxs-lookup"><span data-stu-id="e944a-125">![Log Analytics run query window](media/log-analytics-flow-tutorial/flow02.png)</span></span>

## <a name="step-4-configure-hello-log-analytics-action"></a><span data-ttu-id="e944a-126">Шаг 4: Настройка анализа журналов действие hello</span><span class="sxs-lookup"><span data-stu-id="e944a-126">Step 4: Configure hello Log Analytics action</span></span>

1. <span data-ttu-id="e944a-127">Укажите подробности hello для вашей рабочей области, включая hello подписки ID, группа ресурсов и имя рабочей области.</span><span class="sxs-lookup"><span data-stu-id="e944a-127">Specify hello details for your workspace including hello Subscription ID, Resource Group, and Workspace Name.</span></span>
2. <span data-ttu-id="e944a-128">Добавьте следующие toohello запросов анализа журналов hello **запроса** окна.</span><span class="sxs-lookup"><span data-stu-id="e944a-128">Add hello following Log Analytics query toohello **Query** window.</span></span>  <span data-ttu-id="e944a-129">Это лишь пример запроса, поэтому вы можете заменить его любым другим запросом, возвращающим данные.</span><span class="sxs-lookup"><span data-stu-id="e944a-129">This is only a sample query, and you can replace with any other that returns data.</span></span>
```
    Event
    | where EventLevelName == "Error" 
    | where TimeGenerated > ago(1day)
    | summarize count() by Computer
    | sort by Computerindow. 
```

2. <span data-ttu-id="e944a-130">Выберите **HTML-таблицы** для hello **тип диаграммы**.</span><span class="sxs-lookup"><span data-stu-id="e944a-130">Select **HTML Table** for hello **Chart Type**.</span></span><br><br><span data-ttu-id="e944a-131">![Действие Log Analytics](media/log-analytics-flow-tutorial/flow03.png)</span><span class="sxs-lookup"><span data-stu-id="e944a-131">![Log Analytics action](media/log-analytics-flow-tutorial/flow03.png)</span></span>

## <a name="step-5-configure-hello-flow-toosend-email"></a><span data-ttu-id="e944a-132">Шаг 5: Настройка электронной почты toosend потока hello</span><span class="sxs-lookup"><span data-stu-id="e944a-132">Step 5: Configure hello flow toosend email</span></span>

1. <span data-ttu-id="e944a-133">Выберите поле **Новый шаг**, а затем щелкните **Добавить действие**.</span><span class="sxs-lookup"><span data-stu-id="e944a-133">Click **New step**, and then click **+ Add an action**.</span></span>
2. <span data-ttu-id="e944a-134">Выполните поиск по запросу **Office 365 Outlook**.</span><span class="sxs-lookup"><span data-stu-id="e944a-134">Search for **Office 365 Outlook**.</span></span>
3. <span data-ttu-id="e944a-135">Щелкните **Office 365 Outlook – Send an email** (Office 365 Outlook — отправка сообщения электронной почты).</span><span class="sxs-lookup"><span data-stu-id="e944a-135">Click **Office 365 Outlook – Send an email**.</span></span><br><br><span data-ttu-id="e944a-136">![Окно выбора Office 365 Outlook](media/log-analytics-flow-tutorial/flow04.png)</span><span class="sxs-lookup"><span data-stu-id="e944a-136">![Office 365 Outlook selection window](media/log-analytics-flow-tutorial/flow04.png)</span></span>

4. <span data-ttu-id="e944a-137">Укажите адрес электронной почты получателя hello в hello **для** окна и темой сообщения hello в **субъекта**.</span><span class="sxs-lookup"><span data-stu-id="e944a-137">Specify hello email address of a recipient in hello **To** window and a subject for hello email in **Subject**.</span></span>
5. <span data-ttu-id="e944a-138">Щелкните в любом месте hello **текст** поле.</span><span class="sxs-lookup"><span data-stu-id="e944a-138">Click anywhere in hello **Body** box.</span></span>  <span data-ttu-id="e944a-139">В открывшемся окне **Динамическое содержимое** отобразятся значения из предыдущих действий.</span><span class="sxs-lookup"><span data-stu-id="e944a-139">A **Dynamic content** window opens with values from previous actions.</span></span>  
6. <span data-ttu-id="e944a-140">Выберите **Текст**.</span><span class="sxs-lookup"><span data-stu-id="e944a-140">Select **Body**.</span></span>  <span data-ttu-id="e944a-141">Это hello результаты запроса hello hello анализа журналов действий.</span><span class="sxs-lookup"><span data-stu-id="e944a-141">This is hello results of hello query in hello Log Analytics action.</span></span>
6. <span data-ttu-id="e944a-142">Щелкните **Показать дополнительные параметры**.</span><span class="sxs-lookup"><span data-stu-id="e944a-142">Click **Show advanced options**.</span></span>
7. <span data-ttu-id="e944a-143">В hello **HTML-** выберите **Да**.</span><span class="sxs-lookup"><span data-stu-id="e944a-143">In hello **Is HTML** box, select **Yes**.</span></span><br><br><span data-ttu-id="e944a-144">![Окно настройки сообщения электронной почты Office 365](media/log-analytics-flow-tutorial/flow05.png)</span><span class="sxs-lookup"><span data-stu-id="e944a-144">![Office 365 email configuration window](media/log-analytics-flow-tutorial/flow05.png)</span></span>

## <a name="step-6-save-and-test-your-flow"></a><span data-ttu-id="e944a-145">Шаг 6. Сохранение и тестирование последовательности</span><span class="sxs-lookup"><span data-stu-id="e944a-145">Step 6: Save and test your flow</span></span>
1. <span data-ttu-id="e944a-146">В hello **имя потока** , добавьте имя для вашего потока и нажмите кнопку **создания потока**.</span><span class="sxs-lookup"><span data-stu-id="e944a-146">In hello **Flow name** box, add a name for your flow, and then click **Create flow**.</span></span><br><br><span data-ttu-id="e944a-147">![Сохранение последовательности](media/log-analytics-flow-tutorial/flow06.png)</span><span class="sxs-lookup"><span data-stu-id="e944a-147">![Save flow](media/log-analytics-flow-tutorial/flow06.png)</span></span>
2. <span data-ttu-id="e944a-148">поток Hello теперь создается и выполняется следующий день, который является заданному расписанию hello.</span><span class="sxs-lookup"><span data-stu-id="e944a-148">hello flow is now created and will run after a day which is hello schedule you specified.</span></span> 
3. <span data-ttu-id="e944a-149">поток hello tooimmediately тестирования, нажмите кнопку **выполнить** и затем **выполнять поток**.</span><span class="sxs-lookup"><span data-stu-id="e944a-149">tooimmediately test hello flow, click **Run Now** and then **Run flow**.</span></span><br><br><span data-ttu-id="e944a-150">![Запуск последовательности](media/log-analytics-flow-tutorial/flow07.png)</span><span class="sxs-lookup"><span data-stu-id="e944a-150">![Run flow](media/log-analytics-flow-tutorial/flow07.png)</span></span>
3. <span data-ttu-id="e944a-151">По завершении потока hello проверки почты hello hello получателя, указанном вами.</span><span class="sxs-lookup"><span data-stu-id="e944a-151">When hello flow completes, check hello mail of hello recipient that you specified.</span></span>  <span data-ttu-id="e944a-152">Вы должны были получить сообщения, содержащего текст аналогичные toohello следующее:</span><span class="sxs-lookup"><span data-stu-id="e944a-152">You should have received a mail with a body similar toohello following:</span></span><br><br>![Пример электронного сообщения](media/log-analytics-flow-tutorial/flow08.png)


## <a name="next-steps"></a><span data-ttu-id="e944a-154">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e944a-154">Next steps</span></span>

- <span data-ttu-id="e944a-155">Дополнительные сведения о [поиске по журналам Log Analytics](log-analytics-log-search-new.md).</span><span class="sxs-lookup"><span data-stu-id="e944a-155">Learn more about [log searches in Log Analytics](log-analytics-log-search-new.md).</span></span>
- <span data-ttu-id="e944a-156">Дополнительные сведения о [Microsoft Flow](https://ms.flow.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="e944a-156">Learn more about [Microsoft Flow](https://ms.flow.microsoft.com).</span></span>



