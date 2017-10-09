---
title: "aaaCreate первый рабочий процесс между облачных приложений и облачные услуги - приложения логики Azure | Документы Microsoft"
description: "Автоматизируйте бизнес-процессы для сценариев интеграции приложений и системной интеграции путем создания и выполнения рабочих процессов в Azure Logic Apps."
author: jeffhollan
manager: anneta
editor: 
services: logic-apps
keywords: "рабочий процесс, облачные приложения, облачные службы, бизнес-процессы, системная интеграция, интеграция приложений, EAI"
documentationcenter: 
ms.assetid: ce3582b5-9c58-4637-9379-75ff99878dcd
ms.service: logic-apps
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/31/2017
ms.author: LADocs; jehollan; estfan
ms.openlocfilehash: 17ec589b1c8923b5ad3e6479fc856b6ac81754ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-logic-app-workflow-tooautomate-processes-between-cloud-apps-and-cloud-services"></a><span data-ttu-id="5e502-104">Создание первого приложения логики tooautomate бизнес-процессов между облачных приложений и облачные службы</span><span class="sxs-lookup"><span data-stu-id="5e502-104">Create your first logic app workflow tooautomate processes between cloud apps and cloud services</span></span>

<span data-ttu-id="5e502-105">Создавая и выполняя рабочие процессы в [Azure Logic Apps](logic-apps-what-are-logic-apps.md), вы можете ускорить и упростить автоматизацию бизнес-процессов даже без написания кода.</span><span class="sxs-lookup"><span data-stu-id="5e502-105">Without writing any code, you can automate business processes more easily and quickly when you create and run workflows with [Azure Logic Apps](logic-apps-what-are-logic-apps.md).</span></span> <span data-ttu-id="5e502-106">В первом примере показано, как toocreate базовую логику приложения рабочего процесса, который проверяет RSS веб-канала для нового содержимого на веб-сайте.</span><span class="sxs-lookup"><span data-stu-id="5e502-106">This first example shows how toocreate a basic logic app workflow that checks an RSS feed for new content on a website.</span></span> <span data-ttu-id="5e502-107">Когда новые элементы появляются в канале hello веб-сайта, логику приложения hello отправляет электронной почты из Outlook или Gmail учетной записи.</span><span class="sxs-lookup"><span data-stu-id="5e502-107">When new items appear in hello website's feed, hello logic app sends email from an Outlook or Gmail account.</span></span>

<span data-ttu-id="5e502-108">toocreate и выполните приложение логики, потребуется следующее:</span><span class="sxs-lookup"><span data-stu-id="5e502-108">toocreate and run a logic app, you need these items:</span></span>

* <span data-ttu-id="5e502-109">Подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="5e502-109">An Azure subscription.</span></span> <span data-ttu-id="5e502-110">Если у вас нет подписки, вы можете [создать бесплатную пробную версию учетной записи Azure](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="5e502-110">If you don't have a subscription, you can [start with a free Azure account](https://azure.microsoft.com/free/).</span></span> <span data-ttu-id="5e502-111">В противном случае вы можете [зарегистрироваться на получение подписки с оплатой по мере использования](https://azure.microsoft.com/pricing/purchase-options/).</span><span class="sxs-lookup"><span data-stu-id="5e502-111">Otherwise, you can [sign up for a Pay-As-You-Go subscription](https://azure.microsoft.com/pricing/purchase-options/).</span></span>

  <span data-ttu-id="5e502-112">Подписка Azure используется для выставления счетов за использование приложения логики.</span><span class="sxs-lookup"><span data-stu-id="5e502-112">Your Azure subscription is used for billing logic app usage.</span></span> <span data-ttu-id="5e502-113">Узнайте об [измерении использования](../logic-apps/logic-apps-pricing.md) и [модели ценообразования](https://azure.microsoft.com/pricing/details/logic-apps) Azure Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="5e502-113">Learn how [usage metering](../logic-apps/logic-apps-pricing.md) and [pricing](https://azure.microsoft.com/pricing/details/logic-apps) work for Azure Logic Apps.</span></span>

<span data-ttu-id="5e502-114">Кроме того, в этом примере вам потребуются следующие элементы:</span><span class="sxs-lookup"><span data-stu-id="5e502-114">Also, this example requires these items:</span></span>

* <span data-ttu-id="5e502-115">Учетная запись Outlook.com, Office 365 Outlook или Gmail.</span><span class="sxs-lookup"><span data-stu-id="5e502-115">An Outlook.com, Office 365 Outlook, or Gmail account</span></span>

    > [!TIP]
    > <span data-ttu-id="5e502-116">Если у вас есть личная [учетная запись Майкрософт](https://account.microsoft.com/account), у вас также есть и учетная запись Outlook.com,</span><span class="sxs-lookup"><span data-stu-id="5e502-116">If you have a personal [Microsoft account](https://account.microsoft.com/account), you have an Outlook.com account.</span></span> <span data-ttu-id="5e502-117">а если рабочая или учебная учетная запись Azure — то учетная запись **Office 365 Outlook**.</span><span class="sxs-lookup"><span data-stu-id="5e502-117">Otherwise, if you have an Azure work or school account, you have an **Office 365 Outlook** account.</span></span>

* <span data-ttu-id="5e502-118">Tooa связь веб-сайта RSS-канал.</span><span class="sxs-lookup"><span data-stu-id="5e502-118">A link tooa website's RSS feed.</span></span> <span data-ttu-id="5e502-119">В этом примере используется hello [RSS-канала верхнего истории с веб-сайта hello CNN.com](http://rss.cnn.com/rss/cnn_topstories.rss):`http://rss.cnn.com/rss/cnn_topstories.rss`</span><span class="sxs-lookup"><span data-stu-id="5e502-119">This example uses hello [RSS feed for top stories from hello CNN.com website](http://rss.cnn.com/rss/cnn_topstories.rss): `http://rss.cnn.com/rss/cnn_topstories.rss`</span></span>

## <a name="add-a-trigger-that-starts-your-workflow"></a><span data-ttu-id="5e502-120">Добавление триггера запуска рабочего процесса</span><span class="sxs-lookup"><span data-stu-id="5e502-120">Add a trigger that starts your workflow</span></span>

<span data-ttu-id="5e502-121">Объект [ *триггер* ](./logic-apps-what-are-logic-apps.md#logic-app-concepts) является событие, которое запускает рабочий процесс логику приложения и является первым элементом hello, необходимый вашему приложению логику.</span><span class="sxs-lookup"><span data-stu-id="5e502-121">A [*trigger*](./logic-apps-what-are-logic-apps.md#logic-app-concepts) is an event that starts your logic app workflow and is hello first item that your logic app needs.</span></span>

1. <span data-ttu-id="5e502-122">Войдите в toohello [портал Azure](https://portal.azure.com "портал Azure").</span><span class="sxs-lookup"><span data-stu-id="5e502-122">Sign in toohello [Azure portal](https://portal.azure.com "Azure portal").</span></span>

2. <span data-ttu-id="5e502-123">Hello в левом меню, выберите **New** > **интеграцию** > **приложения логики** как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="5e502-123">From hello left menu, choose **New** > **Enterprise Integration** > **Logic App** as shown here:</span></span>

     ![Портал Azure, "Создать", "Интеграция с предприятием", "Приложение логики"](media/logic-apps-create-a-logic-app/azure-portal-create-logic-app.png)

   > [!TIP]
   > <span data-ttu-id="5e502-125">Вы также можете **New**, введите в поле поиска hello, `logic app`, и нажмите клавишу ВВОД.</span><span class="sxs-lookup"><span data-stu-id="5e502-125">You can also choose **New**, then in hello search box, type `logic app`, and press Enter.</span></span> <span data-ttu-id="5e502-126">Затем выберите **Приложение логики** > **Создать**.</span><span class="sxs-lookup"><span data-stu-id="5e502-126">Then choose **Logic App** > **Create**.</span></span>

3. <span data-ttu-id="5e502-127">Введите имя приложения логики и выберите подписку Azure.</span><span class="sxs-lookup"><span data-stu-id="5e502-127">Name your logic app and select your Azure subscription.</span></span> <span data-ttu-id="5e502-128">Теперь создайте или выберите группу ресурсов Azure, что поможет вам упорядочить связанные ресурсы Azure и управлять ими.</span><span class="sxs-lookup"><span data-stu-id="5e502-128">Now create or select an Azure resource group, which helps you organize and manage related Azure resources.</span></span> <span data-ttu-id="5e502-129">Наконец выберите расположение hello центра обработки данных для размещения логики приложения.</span><span class="sxs-lookup"><span data-stu-id="5e502-129">Finally, select hello datacenter location for hosting your logic app.</span></span> <span data-ttu-id="5e502-130">Когда вы будете готовы, нажмите кнопку **toodashboard ПИН-код** и затем **создать**.</span><span class="sxs-lookup"><span data-stu-id="5e502-130">When you're ready, choose **Pin toodashboard** and then **Create**.</span></span>

     ![Сведения о приложении логики](media/logic-apps-create-a-logic-app/logic-app-settings.png)

   > [!NOTE]
   > <span data-ttu-id="5e502-132">При выборе **toodashboard ПИН-код**, логику приложения отображается на панели мониторинга Azure hello после развертывания и откроется автоматически.</span><span class="sxs-lookup"><span data-stu-id="5e502-132">When you select **Pin toodashboard**, your logic app appears on hello Azure dashboard after deployment, and opens automatically.</span></span> <span data-ttu-id="5e502-133">Если логика приложения не отображается в мониторинга hello hello **все ресурсы** плитки, выберите **см более**и выберите приложение логики.</span><span class="sxs-lookup"><span data-stu-id="5e502-133">If your logic app doesn't appear on hello dashboard, on hello **All resources** tile, choose **See More**, and select your logic app.</span></span> <span data-ttu-id="5e502-134">Или в левом меню hello, выберите **дополнительные службы**.</span><span class="sxs-lookup"><span data-stu-id="5e502-134">Or on hello left menu, choose **More services**.</span></span> <span data-ttu-id="5e502-135">В разделе **Интеграция с предприятием** выберите **Logic Apps**, а затем — свое приложение логики.</span><span class="sxs-lookup"><span data-stu-id="5e502-135">Under **Enterprise Integration**, choose **Logic Apps**, and select your logic app.</span></span>

4. <span data-ttu-id="5e502-136">При открытии логику приложения hello первый раз hello конструктор логику приложения показано шаблоны, которые можно использовать tooget работы.</span><span class="sxs-lookup"><span data-stu-id="5e502-136">When you open your logic app for hello first time, hello Logic App Designer shows templates that you can use tooget started.</span></span> <span data-ttu-id="5e502-137">Сейчас выберите **Пустое приложение логики**. Это позволит создать приложение логики с нуля.</span><span class="sxs-lookup"><span data-stu-id="5e502-137">For now, choose **Blank Logic App** so you can build your logic app from scratch.</span></span>

    <span data-ttu-id="5e502-138">Hello логику конструктора приложения открывается и показывает доступные службы и *триггеры* , можно использовать в логике приложения.</span><span class="sxs-lookup"><span data-stu-id="5e502-138">hello Logic App Designer opens and shows  available services and *triggers* that  you can use in your logic app.</span></span>

5. <span data-ttu-id="5e502-139">Введите в поле поиска hello `RSS`и выбрать этот триггер: **RSS - при публикации элементов потока данных**</span><span class="sxs-lookup"><span data-stu-id="5e502-139">In hello search box, type `RSS`, and select this trigger: **RSS - When a feed item is published**</span></span> 

    ![Триггер RSS](media/logic-apps-create-a-logic-app/rss-trigger.png)

6. <span data-ttu-id="5e502-141">Введите hello ссылку для нужных tootrack RSS-канал hello веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="5e502-141">Enter hello link for hello website's RSS feed that you want tootrack.</span></span> 

     <span data-ttu-id="5e502-142">Вы также можете изменить **частоту** и **интервал**.</span><span class="sxs-lookup"><span data-stu-id="5e502-142">You can also change **Frequency** and **Interval**.</span></span> 
     <span data-ttu-id="5e502-143">Эти параметры определяют частоту, с которой приложение логики будет проверять новые элементы и возвращать найденные в рамках определенного интервала.</span><span class="sxs-lookup"><span data-stu-id="5e502-143">These settings determine how often your logic app checks for new items and returns all items found during that time span.</span></span>

     <span data-ttu-id="5e502-144">В этом примере проверим каждый день в течение главные темы учтена toohello CNN веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="5e502-144">For this example, let's check every day for   top stories posted toohello CNN website.</span></span>

     ![Укажите RSS-канал, частоту и интервал триггера.](media/logic-apps-create-a-logic-app/rss-trigger-setup.png)

7. <span data-ttu-id="5e502-146">Сохраните результаты.</span><span class="sxs-lookup"><span data-stu-id="5e502-146">Save your work for now.</span></span> <span data-ttu-id="5e502-147">(В панели команд конструктора hello, выберите **Сохранить**.)</span><span class="sxs-lookup"><span data-stu-id="5e502-147">(On hello designer command bar, choose **Save**.)</span></span>

   ![Сохранение приложения логики](media/logic-apps-create-a-logic-app/save-logic-app.png)

   <span data-ttu-id="5e502-149">При сохранении, логику приложения в эксплуатацию, но в настоящее время приложение логики проверяет только новые элементы в hello указан RSS-канал.</span><span class="sxs-lookup"><span data-stu-id="5e502-149">When you save, your logic app goes live, but currently, your logic app only checks for new items in hello specified RSS feed.</span></span> 
   <span data-ttu-id="5e502-150">toomake в этом примере более полезной, мы добавьте действие, которое выполняет логику приложения после триггер срабатывает.</span><span class="sxs-lookup"><span data-stu-id="5e502-150">toomake this example more useful, we add an action that your logic app performs after your trigger fires.</span></span>

## <a name="add-an-action-that-responds-tooyour-trigger"></a><span data-ttu-id="5e502-151">Добавьте действие, которое отвечает tooyour триггера</span><span class="sxs-lookup"><span data-stu-id="5e502-151">Add an action that responds tooyour trigger</span></span>

<span data-ttu-id="5e502-152">[*Действие*](./logic-apps-what-are-logic-apps.md#logic-app-concepts) — это задание, выполняемое рабочим процессом приложения логики.</span><span class="sxs-lookup"><span data-stu-id="5e502-152">An [*action*](./logic-apps-what-are-logic-apps.md#logic-app-concepts) is a task performed by your logic app workflow.</span></span> <span data-ttu-id="5e502-153">После добавления в приложение логику tooyour триггера, можно добавить действие tooperform операций с данными, созданный с помощью этого триггера.</span><span class="sxs-lookup"><span data-stu-id="5e502-153">After you add a trigger tooyour logic app, you can add an action tooperform operations with data generated by that trigger.</span></span> <span data-ttu-id="5e502-154">В нашем примере мы теперь добавьте действие, которое отправляет по электронной почте, когда новые элементы появляются в веб-канал RSS hello веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="5e502-154">For our example, we now add an action that sends email when new items appear in hello website's RSS feed.</span></span>

1. <span data-ttu-id="5e502-155">В конструкторе hello в триггер, выберите **новый шаг** > **добавить действие** как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="5e502-155">In hello designer, under your trigger, choose **New step** > **Add an action** as shown here:</span></span>

   ![Добавление действия](media/logic-apps-create-a-logic-app/add-new-action.png)

   <span data-ttu-id="5e502-157">Здравствуйте, конструкторе показан [Доступные соединители](../connectors/apis-list.md) , можно выбрать действие tooperform, когда срабатывает триггер.</span><span class="sxs-lookup"><span data-stu-id="5e502-157">hello designer shows [available connectors](../connectors/apis-list.md) so that you can select an action tooperform when your trigger fires.</span></span>

2. <span data-ttu-id="5e502-158">На основании учетной записи электронной почты, выполните шаги hello для Outlook или Gmail.</span><span class="sxs-lookup"><span data-stu-id="5e502-158">Based on your email account, follow hello steps for Outlook or Gmail.</span></span>

   * <span data-ttu-id="5e502-159">Введите toosend электронной почты из вашей учетной записи Outlook, в поле поиска hello, `outlook`.</span><span class="sxs-lookup"><span data-stu-id="5e502-159">toosend email from your Outlook account, in hello search box, enter `outlook`.</span></span> <span data-ttu-id="5e502-160">В разделе **Службы** выберите **Outlook.com** для личной учетной записи Майкрософт или **Office 365 Outlook** для рабочей или учебной учетной записи Azure.</span><span class="sxs-lookup"><span data-stu-id="5e502-160">Under **Services**, choose **Outlook.com** for personal Microsoft accounts, or choose **Office 365 Outlook** for Azure work or school accounts.</span></span> 
   <span data-ttu-id="5e502-161">В разделе **Действия** выберите **Отправить электронное письмо**.</span><span class="sxs-lookup"><span data-stu-id="5e502-161">Under **Actions**, select **Send an email**.</span></span>

       ![Выбор действия Outlook "Отправить электронное письмо"](media/logic-apps-create-a-logic-app/actions.png)

   * <span data-ttu-id="5e502-163">Введите toosend электронную почту, используя свою учетную запись Gmail, в поле поиска hello, `gmail`.</span><span class="sxs-lookup"><span data-stu-id="5e502-163">toosend email from your Gmail account, in hello search box, enter `gmail`.</span></span> 
   <span data-ttu-id="5e502-164">В разделе **Действия** выберите **Отправить электронное письмо**.</span><span class="sxs-lookup"><span data-stu-id="5e502-164">Under **Actions**, select **Send email**.</span></span>

       ![Выбор действия Gmail "Отправить электронное письмо"](media/logic-apps-create-a-logic-app/actions-gmail.png)

3. <span data-ttu-id="5e502-166">При появлении запроса учетных данных войдите с использованием hello имя пользователя и пароль для учетной записи электронной почты.</span><span class="sxs-lookup"><span data-stu-id="5e502-166">When you're prompted for credentials, sign in with hello username and password for your email account.</span></span> 

4. <span data-ttu-id="5e502-167">Укажите hello сведения для этого действия, как адрес электронной почты hello назначения и выберите параметры hello tooinclude данных hello в сообщении электронной почты hello, например:</span><span class="sxs-lookup"><span data-stu-id="5e502-167">Provide hello details for this action, like hello destination email address, and choose hello parameters for hello data tooinclude in hello email, for example:</span></span>

   ![Выберите данные tooinclude в сообщении электронной почты](media/logic-apps-create-a-logic-app/rss-action-setup.png)

    <span data-ttu-id="5e502-169">Если вы выбрали Outlook, приложение логики может выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="5e502-169">So if you chose Outlook,  your logic app might look like this example:</span></span>

    ![Готовое приложение логики](media/logic-apps-create-a-logic-app/save-run-complete-logic-app.png)

5.  <span data-ttu-id="5e502-171">Сохраните изменения.</span><span class="sxs-lookup"><span data-stu-id="5e502-171">Save your changes.</span></span> <span data-ttu-id="5e502-172">(В панели команд конструктора hello, выберите **Сохранить**.)</span><span class="sxs-lookup"><span data-stu-id="5e502-172">(On hello designer command bar, choose **Save**.)</span></span>

6. <span data-ttu-id="5e502-173">Теперь приложение логики можно вручную запустить, чтобы протестировать.</span><span class="sxs-lookup"><span data-stu-id="5e502-173">You can now manually run your logic app for testing.</span></span> <span data-ttu-id="5e502-174">На панели команд конструктора hello, выберите **запуска**.</span><span class="sxs-lookup"><span data-stu-id="5e502-174">On hello designer command bar, choose **Run**.</span></span> <span data-ttu-id="5e502-175">В противном случае можно позволить проверьте ли hello RSS-канал на основе расписания hello, которую вы настроили логику приложения.</span><span class="sxs-lookup"><span data-stu-id="5e502-175">Otherwise, you can let your logic app check hello specified RSS feed based on hello schedule that you set up.</span></span>

   <span data-ttu-id="5e502-176">Если логика приложения обнаруживает новые элементы, приложение hello логику отправляет электронной почты, содержащее выбранных данных.</span><span class="sxs-lookup"><span data-stu-id="5e502-176">If your logic app finds new items, hello logic app sends email that includes your selected data.</span></span> 
   <span data-ttu-id="5e502-177">Если новые элементы не найдены, логика приложения пропускает hello действие, которое отправляет по электронной почте.</span><span class="sxs-lookup"><span data-stu-id="5e502-177">If no new items are found, your logic app skips hello action that sends email.</span></span>

7. <span data-ttu-id="5e502-178">toomonitor и проверка запуска логику приложения, а также активировать журнал, в меню приложения логики, выберите **Обзор**.</span><span class="sxs-lookup"><span data-stu-id="5e502-178">toomonitor and check your logic app's run and trigger history, on your logic app menu, choose **Overview**.</span></span>

   ![Мониторинг и просмотр журнала триггера и выполнения приложения логики](media/logic-apps-create-a-logic-app/logic-app-run-trigger-history.png)

   > [!TIP]
   > <span data-ttu-id="5e502-180">Если вы не нашли hello появились ожидаемые данные, на панели команд hello, попробуйте выбрать **обновление**.</span><span class="sxs-lookup"><span data-stu-id="5e502-180">If you don't find hello data that you expect, on hello command bar, try choosing **Refresh**.</span></span>

   <span data-ttu-id="5e502-181">Дополнительные сведения о состоянии приложения логики toolearn или запуска и активировать журнал или toodiagnose логику приложения см. в разделе [Устранение логику приложения](logic-apps-diagnosing-failures.md).</span><span class="sxs-lookup"><span data-stu-id="5e502-181">toolearn more about your logic app's status or run and trigger history, or toodiagnose your logic app, see [Troubleshoot your logic app](logic-apps-diagnosing-failures.md).</span></span>

      > [!NOTE]
      > <span data-ttu-id="5e502-182">Приложение логики продолжает работать до отключения приложения.</span><span class="sxs-lookup"><span data-stu-id="5e502-182">Your logic app continues running until you turn off your app.</span></span> <span data-ttu-id="5e502-183">Выберите tooturn отключение приложения сейчас, в меню приложения логики, **Обзор**.</span><span class="sxs-lookup"><span data-stu-id="5e502-183">tooturn off your app for now, on your logic app menu, choose **Overview**.</span></span> <span data-ttu-id="5e502-184">На панели команд hello, выберите **отключить**.</span><span class="sxs-lookup"><span data-stu-id="5e502-184">On hello command bar, choose **Disable**.</span></span>

<span data-ttu-id="5e502-185">Поздравляем, вы только что настроили и запустили свое первое базовое приложение логики.</span><span class="sxs-lookup"><span data-stu-id="5e502-185">Congratulations, you just set up and run your first basic logic app.</span></span> <span data-ttu-id="5e502-186">Вы также узнали, как можно легко создать рабочие процессы автоматизации и как интегрировать облачные приложения и облачные службы без написания кода.</span><span class="sxs-lookup"><span data-stu-id="5e502-186">You also learned how easily you can create workflows that automate processes, and integrate cloud apps and cloud services - all without code.</span></span>

## <a name="manage-your-logic-app"></a><span data-ttu-id="5e502-187">Управление приложением логики</span><span class="sxs-lookup"><span data-stu-id="5e502-187">Manage your logic app</span></span>

<span data-ttu-id="5e502-188">toomanage приложения, можно выполнять задачи, такие как проверка состояния hello, изменить, просмотра журнала, отключить или удалить логику приложения.</span><span class="sxs-lookup"><span data-stu-id="5e502-188">toomanage your app, you can perform tasks like check hello status, edit, view history, turn off, or delete your logic app.</span></span>

1. <span data-ttu-id="5e502-189">Войдите в toohello [портал Azure](https://portal.azure.com "портал Azure").</span><span class="sxs-lookup"><span data-stu-id="5e502-189">Sign in toohello [Azure portal](https://portal.azure.com "Azure portal").</span></span>

2. <span data-ttu-id="5e502-190">В левом меню hello, выберите **дополнительные службы**.</span><span class="sxs-lookup"><span data-stu-id="5e502-190">On hello left menu, choose **More services**.</span></span> <span data-ttu-id="5e502-191">В разделе **Интеграция Enterprise** выберите **Приложения логики**.</span><span class="sxs-lookup"><span data-stu-id="5e502-191">Under **Enterprise Integration**, choose **Logic Apps**.</span></span> <span data-ttu-id="5e502-192">Выберите приложение логики.</span><span class="sxs-lookup"><span data-stu-id="5e502-192">Select your logic app.</span></span> 

   <span data-ttu-id="5e502-193">В меню приложения hello логики можно найти эти задачи управления логики приложения:</span><span class="sxs-lookup"><span data-stu-id="5e502-193">In hello logic app menu, you can find these logic app management tasks:</span></span>

   |<span data-ttu-id="5e502-194">Задача</span><span class="sxs-lookup"><span data-stu-id="5e502-194">Task</span></span>|<span data-ttu-id="5e502-195">Действия</span><span class="sxs-lookup"><span data-stu-id="5e502-195">Steps</span></span>| 
   |:---|:---| 
   | <span data-ttu-id="5e502-196">Просмотр состояния, журнала выполнения приложения, а также общих сведений о нем.</span><span class="sxs-lookup"><span data-stu-id="5e502-196">View your app's status, execution history, and general information</span></span>| <span data-ttu-id="5e502-197">Выберите **Обзор**.</span><span class="sxs-lookup"><span data-stu-id="5e502-197">Choose **Overview**.</span></span>| 
   | <span data-ttu-id="5e502-198">Изменение приложения</span><span class="sxs-lookup"><span data-stu-id="5e502-198">Edit your app</span></span> | <span data-ttu-id="5e502-199">Выберите **Конструктор приложений логики**.</span><span class="sxs-lookup"><span data-stu-id="5e502-199">Choose **Logic App Designer**.</span></span> | 
   | <span data-ttu-id="5e502-200">Просмотр определения JSON рабочего процесса приложения</span><span class="sxs-lookup"><span data-stu-id="5e502-200">View your app's workflow JSON definition</span></span> | <span data-ttu-id="5e502-201">Выберите **Представление кода приложения логики**.</span><span class="sxs-lookup"><span data-stu-id="5e502-201">Choose **Logic App Code View**.</span></span> | 
   | <span data-ttu-id="5e502-202">Просмотр выполненных в приложении логики операций</span><span class="sxs-lookup"><span data-stu-id="5e502-202">View operations performed on your logic app</span></span> | <span data-ttu-id="5e502-203">Выберите **Журнал действий**.</span><span class="sxs-lookup"><span data-stu-id="5e502-203">Choose **Activity log**.</span></span> | 
   | <span data-ttu-id="5e502-204">Просмотр предыдущих версий приложения логики</span><span class="sxs-lookup"><span data-stu-id="5e502-204">View past versions for your logic app</span></span> | <span data-ttu-id="5e502-205">Выберите **Версии**.</span><span class="sxs-lookup"><span data-stu-id="5e502-205">Choose **Versions**.</span></span> | 
   | <span data-ttu-id="5e502-206">Временное отключение приложения</span><span class="sxs-lookup"><span data-stu-id="5e502-206">Turn off your app temporarily</span></span> | <span data-ttu-id="5e502-207">Выберите **Обзор**, затем на панели команд hello, выберите **отключить**.</span><span class="sxs-lookup"><span data-stu-id="5e502-207">Choose **Overview**, then on hello command bar, choose **Disable**.</span></span> | 
   | <span data-ttu-id="5e502-208">Удаление приложения</span><span class="sxs-lookup"><span data-stu-id="5e502-208">Delete your app</span></span> | <span data-ttu-id="5e502-209">Выберите **Обзор**, затем на панели команд hello, выберите **удалить**.</span><span class="sxs-lookup"><span data-stu-id="5e502-209">Choose **Overview**, then on hello command bar, choose **Delete**.</span></span> <span data-ttu-id="5e502-210">Введите имя приложения логики и выберите **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="5e502-210">Enter your logic app's name, and choose **Delete**.</span></span> | 

## <a name="get-help"></a><span data-ttu-id="5e502-211">Получение справки</span><span class="sxs-lookup"><span data-stu-id="5e502-211">Get help</span></span>

<span data-ttu-id="5e502-212">вопросы tooask ответить на вопросы и узнайте, какие другие логику приложения Azure пользователи делают, посетите hello [форуме по Azure логику приложений](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="5e502-212">tooask questions, answer questions, and learn what other Azure Logic Apps users are doing, visit hello [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="5e502-213">toohelp улучшить логику приложения Azure и соединителей, проголосовать или отправить идеями hello [веб-сайт отзывов пользователей приложения логики Azure](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="5e502-213">toohelp improve Azure Logic Apps and connectors, vote on or submit ideas at hello [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5e502-214">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5e502-214">Next steps</span></span>

*  [<span data-ttu-id="5e502-215">Добавление условий и запуск рабочих процессов</span><span class="sxs-lookup"><span data-stu-id="5e502-215">Add conditions and run workflows</span></span>](../logic-apps/logic-apps-use-logic-app-features.md)
*    [<span data-ttu-id="5e502-216">Настройка рабочего процесса с помощью встроенного шаблона или схемы для быстрого начала работы</span><span class="sxs-lookup"><span data-stu-id="5e502-216">Logic app templates</span></span>](../logic-apps/logic-apps-use-logic-app-templates.md)
*  [<span data-ttu-id="5e502-217">Создание приложения логики с помощью шаблона</span><span class="sxs-lookup"><span data-stu-id="5e502-217">Create logic apps from Azure Resource Manager templates</span></span>](../logic-apps/logic-apps-arm-provision.md)
