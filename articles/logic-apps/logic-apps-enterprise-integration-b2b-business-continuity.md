---
title: "Восстановление aaaDisaster для учетной записи интеграции B2B - приложения логики Azure | Документы Microsoft"
description: "Аварийное восстановление B2B в Logic Apps"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: cf44af18-1fe5-41d5-9e06-cc57a968207c
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/10/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: e86564a3c5a2607d22514936c606e2843cba0416
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="logic-apps-b2b-cross-region-disaster-recovery"></a><span data-ttu-id="844af-103">Межрегиональное аварийное восстановление Logic Apps B2B</span><span class="sxs-lookup"><span data-stu-id="844af-103">Logic Apps B2B cross-region disaster recovery</span></span>

<span data-ttu-id="844af-104">Рабочие нагрузки B2B включают денежные транзакции, например заказы и счета.</span><span class="sxs-lookup"><span data-stu-id="844af-104">B2B workloads involve money transactions like orders and invoices.</span></span> <span data-ttu-id="844af-105">Во время аварии крайне важно для hello toomeet business tooquickly восстановления, согласованные бизнес уровня соглашений об уровне обслуживания с партнерами.</span><span class="sxs-lookup"><span data-stu-id="844af-105">During a disaster event, it's critical for a business tooquickly recover toomeet hello business-level SLAs agreed upon with their partners.</span></span> <span data-ttu-id="844af-106">В этой статье показано, как toobuild непрерывности бизнеса плане для рабочих нагрузок B2B.</span><span class="sxs-lookup"><span data-stu-id="844af-106">This article demonstrates how toobuild a business continuity plan for B2B workloads.</span></span> 

* <span data-ttu-id="844af-107">Готовность к аварийному восстановлению</span><span class="sxs-lookup"><span data-stu-id="844af-107">Disaster Recovery readiness</span></span> 
* <span data-ttu-id="844af-108">При аварии переход toosecondary области</span><span class="sxs-lookup"><span data-stu-id="844af-108">Fail over toosecondary region during a disaster event</span></span> 
* <span data-ttu-id="844af-109">Откат tooprimary области после аварии</span><span class="sxs-lookup"><span data-stu-id="844af-109">Fall back tooprimary region after a disaster event</span></span>

## <a name="disaster-recovery-readiness"></a><span data-ttu-id="844af-110">Готовность к аварийному восстановлению</span><span class="sxs-lookup"><span data-stu-id="844af-110">Disaster Recovery readiness</span></span>  

1. <span data-ttu-id="844af-111">Определите дополнительный регион и создайте [учетной записи интеграции](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) в дополнительный регион hello.</span><span class="sxs-lookup"><span data-stu-id="844af-111">Identify a secondary region and create an [integration account](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) in hello secondary region.</span></span>

2. <span data-ttu-id="844af-112">Добавьте партнеров, схемы и соглашения для потоков сообщений hello необходимые целей учетной записи интеграции toobe репликации toosecondary области hello состояние выполнения.</span><span class="sxs-lookup"><span data-stu-id="844af-112">Add partners, schemas, and agreements for hello required message flows where hello run status needs toobe replicated toosecondary region integration account.</span></span>

   > [!TIP]
   > <span data-ttu-id="844af-113">Убедитесь, что имеется согласованности в соглашение об именовании артефакта для hello интеграции учетной записи по регионам.</span><span class="sxs-lookup"><span data-stu-id="844af-113">Make sure there's consistency in hello integration account artifact's naming convention across regions.</span></span> 

3. <span data-ttu-id="844af-114">hello toopull состояние выполнения из основного региона hello, создайте приложение логики в дополнительный регион hello.</span><span class="sxs-lookup"><span data-stu-id="844af-114">toopull hello run status from hello primary region, create a logic app in hello secondary region.</span></span> 

   <span data-ttu-id="844af-115">Приложение логики должно включать *триггер* и *действие*.</span><span class="sxs-lookup"><span data-stu-id="844af-115">This logic app should have a *trigger* and an *action*.</span></span> 
   <span data-ttu-id="844af-116">Hello триггер должен подключаться учетной записи интеграции tooprimary области, и действие hello должны подключаться к учетной записи интеграции toosecondary области.</span><span class="sxs-lookup"><span data-stu-id="844af-116">hello trigger should connect tooprimary region integration account, and hello action should connect toosecondary region integration account.</span></span> 
   <span data-ttu-id="844af-117">На основании hello интервал времени, триггер hello опрашивает таблицу состояния выполнения основной регион hello и извлекает hello новых записей, если таковые имеются.</span><span class="sxs-lookup"><span data-stu-id="844af-117">Based on hello time interval, hello trigger polls hello primary region run status table and pulls hello new records, if any.</span></span> <span data-ttu-id="844af-118">Действие Hello обновляет их учетной записи интеграции toosecondary области.</span><span class="sxs-lookup"><span data-stu-id="844af-118">hello action updates them toosecondary region integration account.</span></span> 
   <span data-ttu-id="844af-119">Это помогает tooget добавочного состояния из основного региона toosecondary области.</span><span class="sxs-lookup"><span data-stu-id="844af-119">This helps tooget incremental runtime status from primary region toosecondary region.</span></span>

4. <span data-ttu-id="844af-120">Непрерывность бизнес-процессов в приложениях для логики интеграции учетная запись является разработана на основе протоколов для B2B - X12, AS2 и EDIFACT toosupport.</span><span class="sxs-lookup"><span data-stu-id="844af-120">Business continuity in Logic Apps integration account is designed toosupport based on B2B protocols - X12, AS2, and EDIFACT.</span></span> <span data-ttu-id="844af-121">toofind подробные инструкции, выберите hello соответствующие ссылки.</span><span class="sxs-lookup"><span data-stu-id="844af-121">toofind detailed steps, select hello respective links.</span></span>

5. <span data-ttu-id="844af-122">Здравствуйте, рекомендация тоже toodeploy все ресурсы основной регион в дополнительном регионе.</span><span class="sxs-lookup"><span data-stu-id="844af-122">hello recommendation is toodeploy all primary region resources in a secondary region too.</span></span> 

   <span data-ttu-id="844af-123">Основной регион ресурсы включают базы данных SQL Azure или Azure Cosmos DB, Azure Service Bus и концентраторы событий Azure, используемый для обмена сообщениями, API управления Azure и компонент приложения логики Azure hello в службе приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="844af-123">Primary region resources include Azure SQL Database or Azure Cosmos DB, Azure Service Bus and Azure Event Hubs used for messaging, Azure API Management, and hello Azure Logic Apps feature in Azure App Service.</span></span>   

6. <span data-ttu-id="844af-124">Установите соединение в основном регионе tooa дополнительный регион.</span><span class="sxs-lookup"><span data-stu-id="844af-124">Establish a connection from a primary region tooa secondary region.</span></span> <span data-ttu-id="844af-125">hello toopull состояние выполнения из основного региона, создайте приложение логики в дополнительном регионе.</span><span class="sxs-lookup"><span data-stu-id="844af-125">toopull hello run status from a primary region, create a logic app in a secondary region.</span></span> 

   <span data-ttu-id="844af-126">приложения логики Hello должна иметь триггер и действие.</span><span class="sxs-lookup"><span data-stu-id="844af-126">hello logic app should have a trigger and an action.</span></span> 
   <span data-ttu-id="844af-127">триггер Hello следует подключить к учетной записи интеграции tooa первичного региона.</span><span class="sxs-lookup"><span data-stu-id="844af-127">hello trigger should connect tooa primary region integration account.</span></span> 
   <span data-ttu-id="844af-128">Действие Hello следует подключить к учетной записи интеграции tooa дополнительный регион.</span><span class="sxs-lookup"><span data-stu-id="844af-128">hello action should connect tooa secondary region integration account.</span></span> 
   <span data-ttu-id="844af-129">На основании hello интервал времени, триггер hello опрашивает таблицу состояния выполнения основной регион hello и извлекает hello новых записей, если таковые имеются.</span><span class="sxs-lookup"><span data-stu-id="844af-129">Based on hello time interval, hello trigger polls hello primary region run status table and pulls hello new records, if any.</span></span> 
   <span data-ttu-id="844af-130">Действие Hello обновляет их учетной записи интеграции tooa дополнительный регион.</span><span class="sxs-lookup"><span data-stu-id="844af-130">hello action updates them tooa secondary region integration account.</span></span> 
   <span data-ttu-id="844af-131">Это позволяет состояние среды выполнения добавочного tooget из hello основной регион toohello дополнительный регион.</span><span class="sxs-lookup"><span data-stu-id="844af-131">This process helps tooget incremental runtime status from hello primary region toohello secondary region.</span></span>

<span data-ttu-id="844af-132">Непрерывность бизнеса в учетной записи приложения логики интеграции обеспечивает поддержку, на основе протоколов B2B hello X12, AS2 и EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="844af-132">Business continuity in a Logic Apps integration account provides support based on hello B2B protocols X12, AS2, and EDIFACT.</span></span> <span data-ttu-id="844af-133">Подробные инструкции по использованию протоколов X12 и AS2 см. в [этом](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md#x12) и в [этом](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md#as2) разделе данной статьи.</span><span class="sxs-lookup"><span data-stu-id="844af-133">For detailed steps on using X12 and AS2, see [X12](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md#x12) and [AS2](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md#as2) in this article.</span></span>

## <a name="fail-over-tooa-secondary-region-during-a-disaster-event"></a><span data-ttu-id="844af-134">При аварии переход tooa дополнительный регион</span><span class="sxs-lookup"><span data-stu-id="844af-134">Fail over tooa secondary region during a disaster event</span></span>

<span data-ttu-id="844af-135">Во время аварии, когда hello основной регион недоступен для обеспечения непрерывности бизнеса, прямой трафик toohello дополнительный регион.</span><span class="sxs-lookup"><span data-stu-id="844af-135">During a disaster event, when hello primary region is not available for business continuity, direct traffic toohello secondary region.</span></span> <span data-ttu-id="844af-136">Дополнительный регион помогают toorecover бизнеса быстро функции toomeet приветствия согласованных RPO/RTO партнерами.</span><span class="sxs-lookup"><span data-stu-id="844af-136">A secondary region helps a business toorecover functions quickly toomeet hello RPO/RTO agreed upon by their partners.</span></span> <span data-ttu-id="844af-137">Он также сводит к минимуму усилия toofail через из одного региона tooanother области.</span><span class="sxs-lookup"><span data-stu-id="844af-137">It also minimizes efforts toofail over from one region tooanother region.</span></span> 

<span data-ttu-id="844af-138">Нет ожидаемую задержку при копировании контрольных чисел из во вторичный регион tooa первичного региона.</span><span class="sxs-lookup"><span data-stu-id="844af-138">There is an expected latency while copying control numbers from a primary region tooa secondary region.</span></span> <span data-ttu-id="844af-139">tooavoid Отправка повторяющиеся созданный элемент управления цифры toopartners во время аварии, hello рекомендуется tooincrement hello контрольных чисел в соглашениях hello дополнительный регион с помощью [командлеты PowerShell](https://blogs.msdn.microsoft.com/david_burgs_blog/2017/03/09/fresh-of-the-press-new-azure-powershell-cmdlets-for-upcoming-x12-connector-disaster-recovery).</span><span class="sxs-lookup"><span data-stu-id="844af-139">tooavoid sending duplicate generated control numbers toopartners during a disaster event, hello recommendation is tooincrement hello control numbers in hello secondary region agreements by using [PowerShell cmdlets](https://blogs.msdn.microsoft.com/david_burgs_blog/2017/03/09/fresh-of-the-press-new-azure-powershell-cmdlets-for-upcoming-x12-connector-disaster-recovery).</span></span>

## <a name="fall-back-tooa-primary-region-post-disaster-event"></a><span data-ttu-id="844af-140">Откат после аварии событие tooa основной регион</span><span class="sxs-lookup"><span data-stu-id="844af-140">Fall back tooa primary region post-disaster event</span></span>

<span data-ttu-id="844af-141">toofall задней tooa основной регион когда она станет доступна, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="844af-141">toofall back tooa primary region when it is available, follow these steps:</span></span>

1. <span data-ttu-id="844af-142">Остановите прием сообщений от партнеров в дополнительный регион hello.</span><span class="sxs-lookup"><span data-stu-id="844af-142">Stop accepting messages from partners in hello secondary region.</span></span>  

2. <span data-ttu-id="844af-143">Обновлять номера управления hello создается для всех соглашений hello первичного региона с помощью [командлеты PowerShell](https://blogs.msdn.microsoft.com/david_burgs_blog/2017/03/09/fresh-of-the-press-new-azure-powershell-cmdlets-for-upcoming-x12-connector-disaster-recovery).</span><span class="sxs-lookup"><span data-stu-id="844af-143">Increment hello generated control numbers for all hello primary region agreements by using [PowerShell cmdlets](https://blogs.msdn.microsoft.com/david_burgs_blog/2017/03/09/fresh-of-the-press-new-azure-powershell-cmdlets-for-upcoming-x12-connector-disaster-recovery).</span></span>  

3. <span data-ttu-id="844af-144">Прямой трафик из hello дополнительный регион toohello первичного региона.</span><span class="sxs-lookup"><span data-stu-id="844af-144">Direct traffic from hello secondary region toohello primary region.</span></span>

4. <span data-ttu-id="844af-145">Убедитесь, что включен, приложение логики hello, созданные в дополнительный регион hello по запросу, состояние выполнения из основного региона hello.</span><span class="sxs-lookup"><span data-stu-id="844af-145">Check that hello logic app created in hello secondary region for pulling run status from hello primary region is enabled.</span></span>

## <a name="x12"></a><span data-ttu-id="844af-146">X12</span><span class="sxs-lookup"><span data-stu-id="844af-146">X12</span></span> 

<span data-ttu-id="844af-147">Для непрерывности бизнес-процессов для документов EDI X12 используются контрольные номера:</span><span class="sxs-lookup"><span data-stu-id="844af-147">Business continuity for EDI X12 documents is based on control numbers:</span></span>

> [!TIP]
> <span data-ttu-id="844af-148">Можно также использовать hello [X12 быстрого запуска шаблона](https://azure.microsoft.com/documentation/templates/201-logic-app-x12-disaster-recovery-replication/) toocreate логику приложения.</span><span class="sxs-lookup"><span data-stu-id="844af-148">You can also use hello [X12 quick start template](https://azure.microsoft.com/documentation/templates/201-logic-app-x12-disaster-recovery-replication/) toocreate logic apps.</span></span> <span data-ttu-id="844af-149">Создание первичных и вторичных интеграции учетные записи являются шаблона hello toouse необходимые компоненты.</span><span class="sxs-lookup"><span data-stu-id="844af-149">Creating primary and secondary integration accounts are prerequisites toouse hello template.</span></span> <span data-ttu-id="844af-150">Hello шаблон помогает toocreate два логику приложения — один для полученных контрольных чисел и другой для номера созданный элемент управления.</span><span class="sxs-lookup"><span data-stu-id="844af-150">hello template helps toocreate two logic apps, one for received control numbers and another for generated control numbers.</span></span> <span data-ttu-id="844af-151">В логику приложения hello, подключение hello триггер toohello первичного интеграции hello действие toohello получателей интеграции записи и создаются соответствующих триггеров и действий.</span><span class="sxs-lookup"><span data-stu-id="844af-151">Respective triggers and actions are created in hello logic apps, connecting hello trigger toohello primary integration account and hello action toohello secondary integration account.</span></span>

<span data-ttu-id="844af-152">**Предварительные требования**</span><span class="sxs-lookup"><span data-stu-id="844af-152">**Prerequisites**</span></span>

<span data-ttu-id="844af-153">tooenable аварийного восстановления для входящих сообщений, выберите параметры проверки дублирования hello в параметры получения hello X12 соглашения.</span><span class="sxs-lookup"><span data-stu-id="844af-153">tooenable disaster recovery for inbound messages, select hello duplicate check settings in hello X12 agreement's Receive Settings.</span></span>

![Выбор параметров проверки дублирования](./media/logic-apps-enterprise-integration-b2b-business-continuity/dupcheck.png)  

1. <span data-ttu-id="844af-155">Создайте [приложение логики](../logic-apps/logic-apps-create-a-logic-app.md) в дополнительном регионе.</span><span class="sxs-lookup"><span data-stu-id="844af-155">Create a [logic app](../logic-apps/logic-apps-create-a-logic-app.md) in a secondary region.</span></span>    

2. <span data-ttu-id="844af-156">Выполните поиск **X12** и выберите **X12 — при изменении контрольного номера**.</span><span class="sxs-lookup"><span data-stu-id="844af-156">Search on **X12**, and select **X12 - When a control number is modified**.</span></span>   

   ![Поиск по запросу "X12"](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn1.png)

   <span data-ttu-id="844af-158">триггер Hello предлагает tooestablish tooan интеграции учетную запись подключения к.</span><span class="sxs-lookup"><span data-stu-id="844af-158">hello trigger prompts you tooestablish a connection tooan integration account.</span></span> 
   <span data-ttu-id="844af-159">Hello триггер должен быть подключен tooa учетной записи интеграции первичного региона.</span><span class="sxs-lookup"><span data-stu-id="844af-159">hello trigger should be connected tooa primary region integration account.</span></span>

3. <span data-ttu-id="844af-160">Введите имя подключения, выберите ваш *основной регион учетной записи интеграции* из hello, а затем выберите **создать**.</span><span class="sxs-lookup"><span data-stu-id="844af-160">Enter a connection name, select your *primary region integration account* from hello list, and choose **Create**.</span></span>   

   ![Имя учетной записи интеграции для основного региона](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn2.png)

4. <span data-ttu-id="844af-162">Hello **синхронизации номеров управления toostart DateTime** параметр является необязательным.</span><span class="sxs-lookup"><span data-stu-id="844af-162">hello **DateTime toostart control number sync** setting is optional.</span></span> <span data-ttu-id="844af-163">Hello **частоты** можно задать слишком**день**, **час**, **минуту**, или **второй** с интервалом.</span><span class="sxs-lookup"><span data-stu-id="844af-163">hello **Frequency** can be set too**Day**, **Hour**, **Minute**, or **Second** with an interval.</span></span>   

   ![Дата, время и частота](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn3.png)

5. <span data-ttu-id="844af-165">Выберите **New step** (Новый шаг) > **Добавить действие**.</span><span class="sxs-lookup"><span data-stu-id="844af-165">Select **New step** > **Add an action**.</span></span>

   ![Выбор действий "Новый шаг" и "Добавить действие"](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn4.png)

6. <span data-ttu-id="844af-167">Выполните поиск **X12** и выберите **X12 — добавление или изменение контрольных номеров**.</span><span class="sxs-lookup"><span data-stu-id="844af-167">Search on **X12**, and select **X12 - Add or update control numbers**.</span></span>   

   ![Добавление или обновление контрольных номеров](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn5.png)

7. <span data-ttu-id="844af-169">Выберите tooconnect tooa дополнительный регион интеграции учетную запись действия, **изменить подключение** > **добавить новое подключение** список учетных записей доступны интеграции hello.</span><span class="sxs-lookup"><span data-stu-id="844af-169">tooconnect an action tooa secondary region integration account, select **Change connection** > **Add new connection** for a list of hello available integration accounts.</span></span> <span data-ttu-id="844af-170">Введите имя подключения, выберите ваш *дополнительный регион учетной записи интеграции* из hello, а затем выберите **создать**.</span><span class="sxs-lookup"><span data-stu-id="844af-170">Enter a connection name, select your *secondary region integration account* from hello list, and choose **Create**.</span></span> 

   ![Имя учетной записи интеграции для дополнительного региона](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn6.png)

8. <span data-ttu-id="844af-172">Переключение tooraw входных данных, щелкнув значок "hello" в правом верхнем углу.</span><span class="sxs-lookup"><span data-stu-id="844af-172">Switch tooraw inputs by clicking on hello icon in upper right corner.</span></span>

   ![Входные данные tooraw коммутатора](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12rawinputs.png)

9. <span data-ttu-id="844af-174">Выберите текст из динамического содержимого палитры hello и сохранения hello логику приложения.</span><span class="sxs-lookup"><span data-stu-id="844af-174">Select Body from hello dynamic content picker, and save hello logic app.</span></span>

   ![Поля динамического содержимого](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn7.png)

   <span data-ttu-id="844af-176">На основании hello интервал времени, триггер hello опрашивает hello основной регион полученных управления таблица и извлекает hello новых записей.</span><span class="sxs-lookup"><span data-stu-id="844af-176">Based on hello time interval, hello trigger polls hello primary region received control number table and pulls hello new records.</span></span> 
   <span data-ttu-id="844af-177">Действие Hello обновляет записи hello в учетной записи интеграции hello дополнительный регион.</span><span class="sxs-lookup"><span data-stu-id="844af-177">hello action updates hello records in hello secondary region integration account.</span></span> 
   <span data-ttu-id="844af-178">Если нет обновлений, как отображается состояние триггера hello **пропускаются**.</span><span class="sxs-lookup"><span data-stu-id="844af-178">If there are no updates, hello trigger status appears as **Skipped**.</span></span>   

   ![Таблица контрольных номеров](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12recevicedcn8.png)

<span data-ttu-id="844af-180">На основании hello интервал времени, состояние среды выполнения добавочного hello реплицирует во вторичный регион tooa первичного региона.</span><span class="sxs-lookup"><span data-stu-id="844af-180">Based on hello time interval, hello incremental runtime status replicates from a primary region tooa secondary region.</span></span> <span data-ttu-id="844af-181">Во время аварии, когда основной регион hello не является доступным, прямого трафика toohello дополнительный регион для обеспечения непрерывности бизнеса.</span><span class="sxs-lookup"><span data-stu-id="844af-181">During a disaster event, when hello primary region is not available, direct traffic toohello secondary region for business continuity.</span></span> 

## <a name="edifact"></a><span data-ttu-id="844af-182">EDIFACT</span><span class="sxs-lookup"><span data-stu-id="844af-182">EDIFACT</span></span> 

<span data-ttu-id="844af-183">Чтобы обеспечить непрерывность бизнес-процессов для документов EDIFACT EDI, используются контрольные номера.</span><span class="sxs-lookup"><span data-stu-id="844af-183">Business continuity for EDI EDIFACT documents is based on control numbers.</span></span>

<span data-ttu-id="844af-184">**Предварительные требования**</span><span class="sxs-lookup"><span data-stu-id="844af-184">**Prerequisites**</span></span>

<span data-ttu-id="844af-185">tooenable аварийного восстановления для входящих сообщений, выберите параметры проверки дублирования hello в параметров получения соглашения EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="844af-185">tooenable disaster recovery for inbound messages, select hello duplicate check settings in your EDIFACT agreement's Receive Settings.</span></span>

![Выбор параметров проверки дублирования](./media/logic-apps-enterprise-integration-b2b-business-continuity/edifactdupcheck.png)  

1. <span data-ttu-id="844af-187">Создайте [приложение логики](../logic-apps/logic-apps-create-a-logic-app.md) в дополнительном регионе.</span><span class="sxs-lookup"><span data-stu-id="844af-187">Create a [logic app](../logic-apps/logic-apps-create-a-logic-app.md) in a secondary region.</span></span>    

2. <span data-ttu-id="844af-188">Выполните поиск **EDIFACT** и выберите **EDIFACT — при изменении контрольного номера**.</span><span class="sxs-lookup"><span data-stu-id="844af-188">Search on **EDIFACT**, and select **EDIFACT - When a control number is modified**.</span></span>

   ![Поиск по запросу "EDIFACT"](./media/logic-apps-enterprise-integration-b2b-business-continuity/edifactcn1.png)

   <span data-ttu-id="844af-190">триггер Hello предлагает tooestablish tooan интеграции учетную запись подключения к.</span><span class="sxs-lookup"><span data-stu-id="844af-190">hello trigger prompts you tooestablish a connection tooan integration account.</span></span> 
   <span data-ttu-id="844af-191">Hello триггер должен быть подключен tooa учетной записи интеграции первичного региона.</span><span class="sxs-lookup"><span data-stu-id="844af-191">hello trigger should be connected tooa primary region integration account.</span></span> 

3. <span data-ttu-id="844af-192">Введите имя подключения, выберите ваш *основной регион учетной записи интеграции* из hello, а затем выберите **создать**.</span><span class="sxs-lookup"><span data-stu-id="844af-192">Enter a connection name, select your *primary region integration account* from hello list, and choose **Create**.</span></span>    

   ![Имя учетной записи интеграции для основного региона](./media/logic-apps-enterprise-integration-b2b-business-continuity/X12CN2.png)

4. <span data-ttu-id="844af-194">Hello **синхронизации номеров управления toostart DateTime** параметр является необязательным.</span><span class="sxs-lookup"><span data-stu-id="844af-194">hello **DateTime toostart control number sync** setting is optional.</span></span> <span data-ttu-id="844af-195">Hello **частоты** можно задать слишком**день**, **час**, **минуту**, или **второй** с интервалом.</span><span class="sxs-lookup"><span data-stu-id="844af-195">hello **Frequency** can be set too**Day**, **Hour**, **Minute**, or **Second** with an interval.</span></span>    

   ![Дата, время и частота](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn3.png)

6. <span data-ttu-id="844af-197">Выберите **New step** (Новый шаг) > **Добавить действие**.</span><span class="sxs-lookup"><span data-stu-id="844af-197">Select **New step** > **Add an action**.</span></span>    

   ![Выбор действий "Новый шаг" и "Добавить действие"](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn4.png)

7. <span data-ttu-id="844af-199">Выполните поиск **EDIFACT** и выберите **EDIFACT — добавление и изменение контрольных номеров**.</span><span class="sxs-lookup"><span data-stu-id="844af-199">Search on **EDIFACT**, and select **EDIFACT - Add or update control numbers**.</span></span>   

   ![Добавление или обновление контрольных номеров](./media/logic-apps-enterprise-integration-b2b-business-continuity/EdifactChooseAction.png)

8. <span data-ttu-id="844af-201">Выберите tooconnect tooa дополнительный регион интеграции учетную запись действия, **изменить подключение** > **добавить новое подключение** список учетных записей доступны интеграции hello.</span><span class="sxs-lookup"><span data-stu-id="844af-201">tooconnect an action tooa secondary region integration account, select **Change connection** > **Add new connection** for a list of hello available integration accounts.</span></span> <span data-ttu-id="844af-202">Введите имя подключения, выберите ваш *дополнительный регион учетной записи интеграции* из hello, а затем выберите **создать**.</span><span class="sxs-lookup"><span data-stu-id="844af-202">Enter a connection name, select your *secondary region integration account* from hello list, and choose **Create**.</span></span>

   ![Имя учетной записи интеграции для дополнительного региона](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn6.png)

9. <span data-ttu-id="844af-204">Переключение tooraw входных данных, щелкнув значок "hello" в правом верхнем углу.</span><span class="sxs-lookup"><span data-stu-id="844af-204">Switch tooraw inputs by clicking on hello icon in upper right corner.</span></span>

   ![Входные данные tooraw коммутатора](./media/logic-apps-enterprise-integration-b2b-business-continuity/Edifactrawinputs.png)

10. <span data-ttu-id="844af-206">Выберите текст из динамического содержимого палитры hello и сохранения hello логику приложения.</span><span class="sxs-lookup"><span data-stu-id="844af-206">Select Body from hello dynamic content picker, and save hello logic app.</span></span>   

   ![Поля динамического содержимого](./media/logic-apps-enterprise-integration-b2b-business-continuity/X12CN7.png)

   <span data-ttu-id="844af-208">На основании hello интервал времени, триггер hello опрашивает hello основной регион полученных управления таблица и извлекает hello новых записей.</span><span class="sxs-lookup"><span data-stu-id="844af-208">Based on hello time interval, hello trigger polls hello primary region received control number table and pulls hello new records.</span></span>
   <span data-ttu-id="844af-209">Действие Hello обновляет учетной записи интеграции hello записей toohello дополнительный регион.</span><span class="sxs-lookup"><span data-stu-id="844af-209">hello action updates hello records toohello secondary region integration account.</span></span> 
   <span data-ttu-id="844af-210">Если нет обновлений, как отображается состояние триггера hello **пропускаются**.</span><span class="sxs-lookup"><span data-stu-id="844af-210">If there are no updates, hello trigger status appears as **Skipped**.</span></span>

   ![Таблица контрольных номеров](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12recevicedcn8.png)

<span data-ttu-id="844af-212">На основании hello интервал времени, состояние среды выполнения добавочного hello реплицирует во вторичный регион tooa первичного региона.</span><span class="sxs-lookup"><span data-stu-id="844af-212">Based on hello time interval, hello incremental runtime status replicates from a primary region tooa secondary region.</span></span> <span data-ttu-id="844af-213">Во время аварии, когда основной регион hello не является доступным, прямого трафика toohello дополнительный регион для обеспечения непрерывности бизнеса.</span><span class="sxs-lookup"><span data-stu-id="844af-213">During a disaster event, when hello primary region is not available, direct traffic toohello secondary region for business continuity.</span></span> 

## <a name="as2"></a><span data-ttu-id="844af-214">AS2</span><span class="sxs-lookup"><span data-stu-id="844af-214">AS2</span></span> 

<span data-ttu-id="844af-215">Непрерывность бизнес-процессов для документов с помощью протокола AS2 hello основана на идентификатор сообщения hello и значение MIC hello.</span><span class="sxs-lookup"><span data-stu-id="844af-215">Business continuity for documents that use hello AS2 protocol is based on hello message ID and hello MIC value.</span></span>

> [!TIP]
> <span data-ttu-id="844af-216">Можно также использовать hello [шаблоном краткого AS2](https://github.com/Azure/azure-quickstart-templates/pull/3302) toocreate логику приложения.</span><span class="sxs-lookup"><span data-stu-id="844af-216">You can also use hello [AS2 quick start template](https://github.com/Azure/azure-quickstart-templates/pull/3302) toocreate logic apps.</span></span> <span data-ttu-id="844af-217">Создание первичных и вторичных интеграции учетные записи являются шаблона hello toouse необходимые компоненты.</span><span class="sxs-lookup"><span data-stu-id="844af-217">Creating primary and secondary integration accounts are prerequisites toouse hello template.</span></span> <span data-ttu-id="844af-218">Hello шаблон позволяет создать приложение логики, имеющий триггера и действия.</span><span class="sxs-lookup"><span data-stu-id="844af-218">hello template helps create a logic app that has a trigger and an action.</span></span> <span data-ttu-id="844af-219">приложения логики Hello создает подключение из учетной записи основного интеграции tooa триггера и учетной записи действия tooa получателей интеграции.</span><span class="sxs-lookup"><span data-stu-id="844af-219">hello logic app creates a connection from a trigger tooa primary integration account and an action tooa secondary integration account.</span></span>

1. <span data-ttu-id="844af-220">Создание [приложения логики](../logic-apps/logic-apps-create-a-logic-app.md) в дополнительный регион hello.</span><span class="sxs-lookup"><span data-stu-id="844af-220">Create a [logic app](../logic-apps/logic-apps-create-a-logic-app.md) in hello secondary region.</span></span>  

2. <span data-ttu-id="844af-221">Выполните поиск **AS2** и выберите **AS2 — When a MIC value is created** (AS2 — При создании значения MIC).</span><span class="sxs-lookup"><span data-stu-id="844af-221">Search on **AS2**, and select **AS2 - When a MIC value is created**.</span></span>   

   ![Поиск по запросу "AS2"](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid1.png)

   <span data-ttu-id="844af-223">Триггер предлагает tooestablish tooan интеграции учетную запись подключения к.</span><span class="sxs-lookup"><span data-stu-id="844af-223">A trigger prompts you tooestablish a connection tooan integration account.</span></span> 
   <span data-ttu-id="844af-224">Hello триггер должен быть подключен tooa учетной записи интеграции первичного региона.</span><span class="sxs-lookup"><span data-stu-id="844af-224">hello trigger should be connected tooa primary region integration account.</span></span> 
   
3. <span data-ttu-id="844af-225">Введите имя подключения, выберите ваш *основной регион учетной записи интеграции* из hello, а затем выберите **создать**.</span><span class="sxs-lookup"><span data-stu-id="844af-225">Enter a connection name, select your *primary region integration account* from hello list, and choose **Create**.</span></span>

   ![Имя учетной записи интеграции для основного региона](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid2.png)

4. <span data-ttu-id="844af-227">Hello **синхронизации значение DateTime toostart MIC** параметр является необязательным.</span><span class="sxs-lookup"><span data-stu-id="844af-227">hello **DateTime toostart MIC value sync** setting is optional.</span></span> <span data-ttu-id="844af-228">Hello **частоты** можно задать слишком**день**, **час**, **минуту**, или **второй** с интервалом.</span><span class="sxs-lookup"><span data-stu-id="844af-228">hello **Frequency** can be set too**Day**, **Hour**, **Minute**, or **Second** with an interval.</span></span>   

   ![Дата, время и частота](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid3.png)

5. <span data-ttu-id="844af-230">Выберите **New step** (Новый шаг) > **Добавить действие**.</span><span class="sxs-lookup"><span data-stu-id="844af-230">Select **New step** > **Add an action**.</span></span>  

   ![Выбор действий "Новый шаг" и "Добавить действие"](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid4.png)

6. <span data-ttu-id="844af-232">Выполните поиск **AS2** и выберите **AS2 - Add or update MIC contents** (AS2 — Добавление или обновление содержимого MIC).</span><span class="sxs-lookup"><span data-stu-id="844af-232">Search on **AS2**, and select **AS2 - Add or update MIC contents**.</span></span>  

   ![Добавление или обновление MIC](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid5.png)

7. <span data-ttu-id="844af-234">Выберите tooconnect tooa получателей интеграции учетную запись действия, **изменить подключение** > **добавить новое подключение** список учетных записей доступны интеграции hello.</span><span class="sxs-lookup"><span data-stu-id="844af-234">tooconnect an action tooa secondary integration account, select **Change connection** > **Add new connection** for a list of hello available integration accounts.</span></span> <span data-ttu-id="844af-235">Введите имя подключения, выберите ваш *дополнительный регион учетной записи интеграции* из hello, а затем выберите **создать**.</span><span class="sxs-lookup"><span data-stu-id="844af-235">Enter a connection name, select your *secondary region integration account* from hello list, and choose **Create**.</span></span>

   ![Имя учетной записи интеграции для дополнительного региона](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid6.png)

8. <span data-ttu-id="844af-237">Переключение tooraw входных данных, щелкнув значок "hello" в правом верхнем углу.</span><span class="sxs-lookup"><span data-stu-id="844af-237">Switch tooraw inputs by clicking on hello icon in upper right corner.</span></span>

   ![Входные данные tooraw коммутатора](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2rawinputs.png)

9. <span data-ttu-id="844af-239">Выберите текст из динамического содержимого палитры hello и сохранения hello логику приложения.</span><span class="sxs-lookup"><span data-stu-id="844af-239">Select Body from hello dynamic content picker, and save hello logic app.</span></span>   

   ![Динамическое содержимое](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid7.png)

   <span data-ttu-id="844af-241">На основании hello интервал времени, триггер hello опрашивает hello основной регион таблицы и извлекает hello новых записей.</span><span class="sxs-lookup"><span data-stu-id="844af-241">Based on hello time interval, hello trigger polls hello primary region table and pulls hello new records.</span></span> <span data-ttu-id="844af-242">Действие Hello обновляет их учетной записи интеграции toohello дополнительный регион.</span><span class="sxs-lookup"><span data-stu-id="844af-242">hello action updates them toohello secondary region integration account.</span></span> 
   <span data-ttu-id="844af-243">Если нет обновлений, как отображается состояние триггера hello **пропускаются**.</span><span class="sxs-lookup"><span data-stu-id="844af-243">If there are no updates, hello trigger status appears as **Skipped**.</span></span>  

   ![Таблица для основного региона](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid8.png)

<span data-ttu-id="844af-245">На основании hello интервал времени, состояние среды выполнения добавочного hello реплицирует hello основной регион toohello дополнительный регион.</span><span class="sxs-lookup"><span data-stu-id="844af-245">Based on hello time interval, hello incremental runtime status replicates from hello primary region toohello secondary region.</span></span> <span data-ttu-id="844af-246">Во время аварии, когда основной регион hello не является доступным, прямого трафика toohello дополнительный регион для обеспечения непрерывности бизнеса.</span><span class="sxs-lookup"><span data-stu-id="844af-246">During a disaster event, when hello primary region is not available, direct traffic toohello secondary region for business continuity.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="844af-247">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="844af-247">Next steps</span></span>

[<span data-ttu-id="844af-248">Мониторинг сообщений B2B</span><span class="sxs-lookup"><span data-stu-id="844af-248">Monitor B2B messages</span></span>](logic-apps-monitor-b2b-message.md)

