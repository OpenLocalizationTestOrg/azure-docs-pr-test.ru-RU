---
title: "Аварийное восстановление учетной записи интеграции B2B в Azure Logic Apps | Документация Майкрософт"
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
ms.openlocfilehash: 4896d9da456bcc17b1a4d92259ef3d57f8575d8b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="logic-apps-b2b-cross-region-disaster-recovery"></a><span data-ttu-id="9cb61-103">Межрегиональное аварийное восстановление Logic Apps B2B</span><span class="sxs-lookup"><span data-stu-id="9cb61-103">Logic Apps B2B cross-region disaster recovery</span></span>

<span data-ttu-id="9cb61-104">Рабочие нагрузки B2B включают денежные транзакции, например заказы и счета.</span><span class="sxs-lookup"><span data-stu-id="9cb61-104">B2B workloads involve money transactions like orders and invoices.</span></span> <span data-ttu-id="9cb61-105">Для компаний в случае аварии чрезвычайно важно быстро восстановить систему для соответствия Соглашениям об уровне обслуживания корпоративного уровня по договоренности с партнерами.</span><span class="sxs-lookup"><span data-stu-id="9cb61-105">During a disaster event, it's critical for a business to quickly recover to meet the business-level SLAs agreed upon with their partners.</span></span> <span data-ttu-id="9cb61-106">В этой статье описывается создание плана обеспечения непрерывности бизнес-процессов для рабочих нагрузок B2B.</span><span class="sxs-lookup"><span data-stu-id="9cb61-106">This article demonstrates how to build a business continuity plan for B2B workloads.</span></span> 

* <span data-ttu-id="9cb61-107">Готовность к аварийному восстановлению</span><span class="sxs-lookup"><span data-stu-id="9cb61-107">Disaster Recovery readiness</span></span> 
* <span data-ttu-id="9cb61-108">Отработка отказа в дополнительный регион во время аварии</span><span class="sxs-lookup"><span data-stu-id="9cb61-108">Fail over to secondary region during a disaster event</span></span> 
* <span data-ttu-id="9cb61-109">Восстановление размещения в основной регион после аварийного восстановления</span><span class="sxs-lookup"><span data-stu-id="9cb61-109">Fall back to primary region after a disaster event</span></span>

## <a name="disaster-recovery-readiness"></a><span data-ttu-id="9cb61-110">Готовность к аварийному восстановлению</span><span class="sxs-lookup"><span data-stu-id="9cb61-110">Disaster Recovery readiness</span></span>  

1. <span data-ttu-id="9cb61-111">Выберите дополнительный регион и создайте в нем [учетную запись интеграции](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md).</span><span class="sxs-lookup"><span data-stu-id="9cb61-111">Identify a secondary region and create an [integration account](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) in the secondary region.</span></span>

2. <span data-ttu-id="9cb61-112">Добавьте партнеров, схемы и соглашения для необходимых потоков сообщений, в которых состояние выполнения нужно реплицировать в учетную запись интеграции дополнительного региона.</span><span class="sxs-lookup"><span data-stu-id="9cb61-112">Add partners, schemas, and agreements for the required message flows where the run status needs to be replicated to secondary region integration account.</span></span>

   > [!TIP]
   > <span data-ttu-id="9cb61-113">Соглашения об именовании артефактов учетной записи интеграции в регионах должны быть согласованы.</span><span class="sxs-lookup"><span data-stu-id="9cb61-113">Make sure there's consistency in the integration account artifact's naming convention across regions.</span></span> 

3. <span data-ttu-id="9cb61-114">Чтобы получить состояние выполнения из основного региона, создайте приложение логики в дополнительном регионе.</span><span class="sxs-lookup"><span data-stu-id="9cb61-114">To pull the run status from the primary region, create a logic app in the secondary region.</span></span> 

   <span data-ttu-id="9cb61-115">Приложение логики должно включать *триггер* и *действие*.</span><span class="sxs-lookup"><span data-stu-id="9cb61-115">This logic app should have a *trigger* and an *action*.</span></span> 
   <span data-ttu-id="9cb61-116">Триггер необходимо подключить к учетной записи интеграции основного региона, а действие — к учетной записи интеграции дополнительного региона.</span><span class="sxs-lookup"><span data-stu-id="9cb61-116">The trigger should connect to primary region integration account, and the action should connect to secondary region integration account.</span></span> 
   <span data-ttu-id="9cb61-117">В зависимости от интервала времени триггер выполняет опрос таблицы состояния выполнения для основного региона и извлекает новые записи при их наличии,</span><span class="sxs-lookup"><span data-stu-id="9cb61-117">Based on the time interval, the trigger polls the primary region run status table and pulls the new records, if any.</span></span> <span data-ttu-id="9cb61-118">а действие обновляет сведения о записях в учетной записи интеграции дополнительного региона.</span><span class="sxs-lookup"><span data-stu-id="9cb61-118">The action updates them to secondary region integration account.</span></span> 
   <span data-ttu-id="9cb61-119">Это позволяет передать добавочное состояние среды выполнения из основного региона в дополнительный.</span><span class="sxs-lookup"><span data-stu-id="9cb61-119">This helps to get incremental runtime status from primary region to secondary region.</span></span>

4. <span data-ttu-id="9cb61-120">Непрерывность бизнес-процессов в учетной записи интеграции Logic Apps поддерживает протоколы на базе B2B — X12, AS2 и EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="9cb61-120">Business continuity in Logic Apps integration account is designed to support based on B2B protocols - X12, AS2, and EDIFACT.</span></span> <span data-ttu-id="9cb61-121">Чтобы получить дополнительные сведения, используйте соответствующие ссылки.</span><span class="sxs-lookup"><span data-stu-id="9cb61-121">To find detailed steps, select the respective links.</span></span>

5. <span data-ttu-id="9cb61-122">Мы рекомендуем также развернуть все ресурсы основного региона</span><span class="sxs-lookup"><span data-stu-id="9cb61-122">The recommendation is to deploy all primary region resources in a secondary region too.</span></span> 

   <span data-ttu-id="9cb61-123">(например, базы данных SQL Azure и Azure Cosmos DB, служебную шину и концентраторы уведомлений Azure, используемые для обмена сообщениями, управление API Azure и компонент Azure Logic Apps в службе приложений Azure) в дополнительном регионе.</span><span class="sxs-lookup"><span data-stu-id="9cb61-123">Primary region resources include Azure SQL Database or Azure Cosmos DB, Azure Service Bus and Azure Event Hubs used for messaging, Azure API Management, and the Azure Logic Apps feature in Azure App Service.</span></span>   

6. <span data-ttu-id="9cb61-124">Установите подключение между основным и дополнительным регионом.</span><span class="sxs-lookup"><span data-stu-id="9cb61-124">Establish a connection from a primary region to a secondary region.</span></span> <span data-ttu-id="9cb61-125">Чтобы получить состояние выполнения из основного региона, создайте приложение логики в дополнительном регионе.</span><span class="sxs-lookup"><span data-stu-id="9cb61-125">To pull the run status from a primary region, create a logic app in a secondary region.</span></span> 

   <span data-ttu-id="9cb61-126">Приложение логики должно включать триггер и действие.</span><span class="sxs-lookup"><span data-stu-id="9cb61-126">The logic app should have a trigger and an action.</span></span> 
   <span data-ttu-id="9cb61-127">Триггер необходимо подключить к учетной записи интеграции для основного региона,</span><span class="sxs-lookup"><span data-stu-id="9cb61-127">The trigger should connect to a primary region integration account.</span></span> 
   <span data-ttu-id="9cb61-128">а действие — к учетной записи интеграции для дополнительного региона.</span><span class="sxs-lookup"><span data-stu-id="9cb61-128">The action should connect to a secondary region integration account.</span></span> 
   <span data-ttu-id="9cb61-129">В зависимости от интервала времени триггер выполняет опрос таблицы состояния выполнения для основного региона и извлекает новые записи при их наличии,</span><span class="sxs-lookup"><span data-stu-id="9cb61-129">Based on the time interval, the trigger polls the primary region run status table and pulls the new records, if any.</span></span> 
   <span data-ttu-id="9cb61-130">а действие обновляет сведения о записях в учетной записи интеграции дополнительного региона.</span><span class="sxs-lookup"><span data-stu-id="9cb61-130">The action updates them to a secondary region integration account.</span></span> 
   <span data-ttu-id="9cb61-131">Этот процесс позволяет передать добавочное состояние среды выполнения из основного региона в дополнительный.</span><span class="sxs-lookup"><span data-stu-id="9cb61-131">This process helps to get incremental runtime status from the primary region to the secondary region.</span></span>

<span data-ttu-id="9cb61-132">Непрерывность бизнес-процессов в учетной записи интеграции Logic Apps поддерживает протоколы на базе B2B — X12, AS2 и EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="9cb61-132">Business continuity in a Logic Apps integration account provides support based on the B2B protocols X12, AS2, and EDIFACT.</span></span> <span data-ttu-id="9cb61-133">Подробные инструкции по использованию протоколов X12 и AS2 см. в [этом](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md#x12) и в [этом](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md#as2) разделе данной статьи.</span><span class="sxs-lookup"><span data-stu-id="9cb61-133">For detailed steps on using X12 and AS2, see [X12](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md#x12) and [AS2](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md#as2) in this article.</span></span>

## <a name="fail-over-to-a-secondary-region-during-a-disaster-event"></a><span data-ttu-id="9cb61-134">Отработка отказа в дополнительный регион во время аварии</span><span class="sxs-lookup"><span data-stu-id="9cb61-134">Fail over to a secondary region during a disaster event</span></span>

<span data-ttu-id="9cb61-135">Во время аварийного события, когда основной регион является недоступным для обеспечения непрерывности бизнес-процессов, перенаправьте трафик к дополнительному региону.</span><span class="sxs-lookup"><span data-stu-id="9cb61-135">During a disaster event, when the primary region is not available for business continuity, direct traffic to the secondary region.</span></span> <span data-ttu-id="9cb61-136">Дополнительный регион помогает компании быстро восстановить работу в соответствии с показателями RPO и RTO, согласованными с партнерами.</span><span class="sxs-lookup"><span data-stu-id="9cb61-136">A secondary region helps a business to recover functions quickly to meet the RPO/RTO agreed upon by their partners.</span></span> <span data-ttu-id="9cb61-137">При использовании этого региона очень просто выполнить отработку отказа из одного региона в другой.</span><span class="sxs-lookup"><span data-stu-id="9cb61-137">It also minimizes efforts to fail over from one region to another region.</span></span> 

<span data-ttu-id="9cb61-138">При копировании контрольных номеров из основного региона в дополнительный вы столкнетесь с ожидаемой задержкой.</span><span class="sxs-lookup"><span data-stu-id="9cb61-138">There is an expected latency while copying control numbers from a primary region to a secondary region.</span></span> <span data-ttu-id="9cb61-139">Чтобы избежать отправки повторно созданных контрольных номеров партнерам во время аварийного события, мы рекомендуем увеличивать эти номера в соглашениях для дополнительного региона с помощью [командлетов PowerShell](https://blogs.msdn.microsoft.com/david_burgs_blog/2017/03/09/fresh-of-the-press-new-azure-powershell-cmdlets-for-upcoming-x12-connector-disaster-recovery).</span><span class="sxs-lookup"><span data-stu-id="9cb61-139">To avoid sending duplicate generated control numbers to partners during a disaster event, the recommendation is to increment the control numbers in the secondary region agreements by using [PowerShell cmdlets](https://blogs.msdn.microsoft.com/david_burgs_blog/2017/03/09/fresh-of-the-press-new-azure-powershell-cmdlets-for-upcoming-x12-connector-disaster-recovery).</span></span>

## <a name="fall-back-to-a-primary-region-post-disaster-event"></a><span data-ttu-id="9cb61-140">Восстановление размещения в основной регион после аварийного восстановления</span><span class="sxs-lookup"><span data-stu-id="9cb61-140">Fall back to a primary region post-disaster event</span></span>

<span data-ttu-id="9cb61-141">Чтобы восстановить размещение в основной регион (если он доступен), сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="9cb61-141">To fall back to a primary region when it is available, follow these steps:</span></span>

1. <span data-ttu-id="9cb61-142">Не принимайте сообщения от партнеров в дополнительном регионе.</span><span class="sxs-lookup"><span data-stu-id="9cb61-142">Stop accepting messages from partners in the secondary region.</span></span>  

2. <span data-ttu-id="9cb61-143">Увеличьте создаваемые контрольные номера для всех соглашений основного региона с помощью [командлетов PowerShell](https://blogs.msdn.microsoft.com/david_burgs_blog/2017/03/09/fresh-of-the-press-new-azure-powershell-cmdlets-for-upcoming-x12-connector-disaster-recovery).</span><span class="sxs-lookup"><span data-stu-id="9cb61-143">Increment the generated control numbers for all the primary region agreements by using [PowerShell cmdlets](https://blogs.msdn.microsoft.com/david_burgs_blog/2017/03/09/fresh-of-the-press-new-azure-powershell-cmdlets-for-upcoming-x12-connector-disaster-recovery).</span></span>  

3. <span data-ttu-id="9cb61-144">Перенаправьте трафик из дополнительного региона в основной.</span><span class="sxs-lookup"><span data-stu-id="9cb61-144">Direct traffic from the secondary region to the primary region.</span></span>

4. <span data-ttu-id="9cb61-145">Проверьте, включено ли приложение логики, созданное в дополнительном регионе, чтобы передать состояние выполнения из основного региона.</span><span class="sxs-lookup"><span data-stu-id="9cb61-145">Check that the logic app created in the secondary region for pulling run status from the primary region is enabled.</span></span>

## <a name="x12"></a><span data-ttu-id="9cb61-146">X12</span><span class="sxs-lookup"><span data-stu-id="9cb61-146">X12</span></span> 

<span data-ttu-id="9cb61-147">Для непрерывности бизнес-процессов для документов EDI X12 используются контрольные номера:</span><span class="sxs-lookup"><span data-stu-id="9cb61-147">Business continuity for EDI X12 documents is based on control numbers:</span></span>

> [!TIP]
> <span data-ttu-id="9cb61-148">Чтобы создать приложения логики, вы также можете использовать [шаблон быстрого запуска X12](https://azure.microsoft.com/documentation/templates/201-logic-app-x12-disaster-recovery-replication/).</span><span class="sxs-lookup"><span data-stu-id="9cb61-148">You can also use the [X12 quick start template](https://azure.microsoft.com/documentation/templates/201-logic-app-x12-disaster-recovery-replication/) to create logic apps.</span></span> <span data-ttu-id="9cb61-149">Для использования этого шаблона необходимо создать учетные записи интеграции для основного и дополнительного регионов.</span><span class="sxs-lookup"><span data-stu-id="9cb61-149">Creating primary and secondary integration accounts are prerequisites to use the template.</span></span> <span data-ttu-id="9cb61-150">С помощью шаблона вы создадите два приложения логики: одно для полученного контрольного номера, а второе — для созданного.</span><span class="sxs-lookup"><span data-stu-id="9cb61-150">The template helps to create two logic apps, one for received control numbers and another for generated control numbers.</span></span> <span data-ttu-id="9cb61-151">Соответствующие триггеры и действия создаются в Logic Apps. Триггер подключается к учетной записи интеграции для основного региона, а действие — к учетной записи интеграции для дополнительного региона.</span><span class="sxs-lookup"><span data-stu-id="9cb61-151">Respective triggers and actions are created in the logic apps, connecting the trigger to the primary integration account and the action to the secondary integration account.</span></span>

<span data-ttu-id="9cb61-152">**Предварительные требования**</span><span class="sxs-lookup"><span data-stu-id="9cb61-152">**Prerequisites**</span></span>

<span data-ttu-id="9cb61-153">Чтобы включить аварийное восстановление для входящих сообщений, выберите параметры проверки дублирования в разделе с настройками получения соглашения X12.</span><span class="sxs-lookup"><span data-stu-id="9cb61-153">To enable disaster recovery for inbound messages, select the duplicate check settings in the X12 agreement's Receive Settings.</span></span>

![Выбор параметров проверки дублирования](./media/logic-apps-enterprise-integration-b2b-business-continuity/dupcheck.png)  

1. <span data-ttu-id="9cb61-155">Создайте [приложение логики](../logic-apps/logic-apps-create-a-logic-app.md) в дополнительном регионе.</span><span class="sxs-lookup"><span data-stu-id="9cb61-155">Create a [logic app](../logic-apps/logic-apps-create-a-logic-app.md) in a secondary region.</span></span>    

2. <span data-ttu-id="9cb61-156">Выполните поиск **X12** и выберите **X12 — при изменении контрольного номера**.</span><span class="sxs-lookup"><span data-stu-id="9cb61-156">Search on **X12**, and select **X12 - When a control number is modified**.</span></span>   

   ![Поиск по запросу "X12"](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn1.png)

   <span data-ttu-id="9cb61-158">При выборе триггера вам будет предложено установить соединение с учетной записью интеграции.</span><span class="sxs-lookup"><span data-stu-id="9cb61-158">The trigger prompts you to establish a connection to an integration account.</span></span> 
   <span data-ttu-id="9cb61-159">Триггер необходимо подключить к учетной записи интеграции для основного региона.</span><span class="sxs-lookup"><span data-stu-id="9cb61-159">The trigger should be connected to a primary region integration account.</span></span>

3. <span data-ttu-id="9cb61-160">Присвойте имя для подключения, выберите из списка свою *учетную запись интеграции для основного региона*, а затем выберите **Создать**.</span><span class="sxs-lookup"><span data-stu-id="9cb61-160">Enter a connection name, select your *primary region integration account* from the list, and choose **Create**.</span></span>   

   ![Имя учетной записи интеграции для основного региона](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn2.png)

4. <span data-ttu-id="9cb61-162">Параметр **Дата и время начала синхронизации контрольного номера** является необязательным.</span><span class="sxs-lookup"><span data-stu-id="9cb61-162">The **DateTime to start control number sync** setting is optional.</span></span> <span data-ttu-id="9cb61-163">Вы можете задать **частоту** с интервалом в **днях**, **часах**, **минутах** или **секундах**.</span><span class="sxs-lookup"><span data-stu-id="9cb61-163">The **Frequency** can be set to **Day**, **Hour**, **Minute**, or **Second** with an interval.</span></span>   

   ![Дата, время и частота](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn3.png)

5. <span data-ttu-id="9cb61-165">Выберите **New step** (Новый шаг) > **Добавить действие**.</span><span class="sxs-lookup"><span data-stu-id="9cb61-165">Select **New step** > **Add an action**.</span></span>

   ![Выбор действий "Новый шаг" и "Добавить действие"](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn4.png)

6. <span data-ttu-id="9cb61-167">Выполните поиск **X12** и выберите **X12 — добавление или изменение контрольных номеров**.</span><span class="sxs-lookup"><span data-stu-id="9cb61-167">Search on **X12**, and select **X12 - Add or update control numbers**.</span></span>   

   ![Добавление или обновление контрольных номеров](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn5.png)

7. <span data-ttu-id="9cb61-169">Для подключения действия к учетной записи интеграции для дополнительного региона выберите **Change connection** (Изменить подключение) > **Добавить новое подключение**, чтобы получить список доступных учетных записей интеграции.</span><span class="sxs-lookup"><span data-stu-id="9cb61-169">To connect an action to a secondary region integration account, select **Change connection** > **Add new connection** for a list of the available integration accounts.</span></span> <span data-ttu-id="9cb61-170">Введите имя для подключения, выберите из списка свою *учетную запись интеграции для дополнительного региона*, а затем выберите **Создать**.</span><span class="sxs-lookup"><span data-stu-id="9cb61-170">Enter a connection name, select your *secondary region integration account* from the list, and choose **Create**.</span></span> 

   ![Имя учетной записи интеграции для дополнительного региона](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn6.png)

8. <span data-ttu-id="9cb61-172">Переключитесь на необработанные входные данные, щелкнув значок в правом верхнем углу.</span><span class="sxs-lookup"><span data-stu-id="9cb61-172">Switch to raw inputs by clicking on the icon in upper right corner.</span></span>

   ![Переключение на необработанные входные данные](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12rawinputs.png)

9. <span data-ttu-id="9cb61-174">Выберите "Текст" с помощью средства выбора динамического содержимого и сохраните приложение логики.</span><span class="sxs-lookup"><span data-stu-id="9cb61-174">Select Body from the dynamic content picker, and save the logic app.</span></span>

   ![Поля динамического содержимого](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn7.png)

   <span data-ttu-id="9cb61-176">В зависимости от интервала времени триггер выполняет опрос таблицы полученных контрольных номеров для основного региона и извлекает новые записи при их наличии,</span><span class="sxs-lookup"><span data-stu-id="9cb61-176">Based on the time interval, the trigger polls the primary region received control number table and pulls the new records.</span></span> 
   <span data-ttu-id="9cb61-177">а действие обновляет сведения о записях в учетной записи интеграции дополнительного региона.</span><span class="sxs-lookup"><span data-stu-id="9cb61-177">The action updates the records in the secondary region integration account.</span></span> 
   <span data-ttu-id="9cb61-178">Если эти сведения не обновляются, состояние триггера отображается как **Пропущено**.</span><span class="sxs-lookup"><span data-stu-id="9cb61-178">If there are no updates, the trigger status appears as **Skipped**.</span></span>   

   ![Таблица контрольных номеров](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12recevicedcn8.png)

<span data-ttu-id="9cb61-180">В зависимости от интервала времени дополнительное состояние о среде выполнения реплицируется из основного региона в дополнительный.</span><span class="sxs-lookup"><span data-stu-id="9cb61-180">Based on the time interval, the incremental runtime status replicates from a primary region to a secondary region.</span></span> <span data-ttu-id="9cb61-181">Во время аварийного события, когда основной регион является недоступным, перенаправьте трафик к дополнительному региону для обеспечения непрерывности бизнес-процессов.</span><span class="sxs-lookup"><span data-stu-id="9cb61-181">During a disaster event, when the primary region is not available, direct traffic to the secondary region for business continuity.</span></span> 

## <a name="edifact"></a><span data-ttu-id="9cb61-182">EDIFACT</span><span class="sxs-lookup"><span data-stu-id="9cb61-182">EDIFACT</span></span> 

<span data-ttu-id="9cb61-183">Чтобы обеспечить непрерывность бизнес-процессов для документов EDIFACT EDI, используются контрольные номера.</span><span class="sxs-lookup"><span data-stu-id="9cb61-183">Business continuity for EDI EDIFACT documents is based on control numbers.</span></span>

<span data-ttu-id="9cb61-184">**Предварительные требования**</span><span class="sxs-lookup"><span data-stu-id="9cb61-184">**Prerequisites**</span></span>

<span data-ttu-id="9cb61-185">Чтобы включить аварийное восстановление для входящих сообщений, выберите параметры проверки дублирования в разделе с настройками получения соглашения EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="9cb61-185">To enable disaster recovery for inbound messages, select the duplicate check settings in your EDIFACT agreement's Receive Settings.</span></span>

![Выбор параметров проверки дублирования](./media/logic-apps-enterprise-integration-b2b-business-continuity/edifactdupcheck.png)  

1. <span data-ttu-id="9cb61-187">Создайте [приложение логики](../logic-apps/logic-apps-create-a-logic-app.md) в дополнительном регионе.</span><span class="sxs-lookup"><span data-stu-id="9cb61-187">Create a [logic app](../logic-apps/logic-apps-create-a-logic-app.md) in a secondary region.</span></span>    

2. <span data-ttu-id="9cb61-188">Выполните поиск **EDIFACT** и выберите **EDIFACT — при изменении контрольного номера**.</span><span class="sxs-lookup"><span data-stu-id="9cb61-188">Search on **EDIFACT**, and select **EDIFACT - When a control number is modified**.</span></span>

   ![Поиск по запросу "EDIFACT"](./media/logic-apps-enterprise-integration-b2b-business-continuity/edifactcn1.png)

   <span data-ttu-id="9cb61-190">При выборе триггера вам будет предложено установить соединение с учетной записью интеграции.</span><span class="sxs-lookup"><span data-stu-id="9cb61-190">The trigger prompts you to establish a connection to an integration account.</span></span> 
   <span data-ttu-id="9cb61-191">Триггер необходимо подключить к учетной записи интеграции для основного региона.</span><span class="sxs-lookup"><span data-stu-id="9cb61-191">The trigger should be connected to a primary region integration account.</span></span> 

3. <span data-ttu-id="9cb61-192">Присвойте имя для подключения, выберите из списка свою *учетную запись интеграции для основного региона*, а затем выберите **Создать**.</span><span class="sxs-lookup"><span data-stu-id="9cb61-192">Enter a connection name, select your *primary region integration account* from the list, and choose **Create**.</span></span>    

   ![Имя учетной записи интеграции для основного региона](./media/logic-apps-enterprise-integration-b2b-business-continuity/X12CN2.png)

4. <span data-ttu-id="9cb61-194">Параметр **Дата и время начала синхронизации контрольного номера** является необязательным.</span><span class="sxs-lookup"><span data-stu-id="9cb61-194">The **DateTime to start control number sync** setting is optional.</span></span> <span data-ttu-id="9cb61-195">Вы можете задать **частоту** с интервалом в **днях**, **часах**, **минутах** или **секундах**.</span><span class="sxs-lookup"><span data-stu-id="9cb61-195">The **Frequency** can be set to **Day**, **Hour**, **Minute**, or **Second** with an interval.</span></span>    

   ![Дата, время и частота](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn3.png)

6. <span data-ttu-id="9cb61-197">Выберите **New step** (Новый шаг) > **Добавить действие**.</span><span class="sxs-lookup"><span data-stu-id="9cb61-197">Select **New step** > **Add an action**.</span></span>    

   ![Выбор действий "Новый шаг" и "Добавить действие"](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn4.png)

7. <span data-ttu-id="9cb61-199">Выполните поиск **EDIFACT** и выберите **EDIFACT — добавление и изменение контрольных номеров**.</span><span class="sxs-lookup"><span data-stu-id="9cb61-199">Search on **EDIFACT**, and select **EDIFACT - Add or update control numbers**.</span></span>   

   ![Добавление или обновление контрольных номеров](./media/logic-apps-enterprise-integration-b2b-business-continuity/EdifactChooseAction.png)

8. <span data-ttu-id="9cb61-201">Для подключения действия к учетной записи интеграции для дополнительного региона выберите **Change connection** (Изменить подключение) > **Добавить новое подключение**, чтобы получить список доступных учетных записей интеграции.</span><span class="sxs-lookup"><span data-stu-id="9cb61-201">To connect an action to a secondary region integration account, select **Change connection** > **Add new connection** for a list of the available integration accounts.</span></span> <span data-ttu-id="9cb61-202">Введите имя для подключения, выберите из списка свою *учетную запись интеграции для дополнительного региона*, а затем выберите **Создать**.</span><span class="sxs-lookup"><span data-stu-id="9cb61-202">Enter a connection name, select your *secondary region integration account* from the list, and choose **Create**.</span></span>

   ![Имя учетной записи интеграции для дополнительного региона](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn6.png)

9. <span data-ttu-id="9cb61-204">Переключитесь на необработанные входные данные, щелкнув значок в правом верхнем углу.</span><span class="sxs-lookup"><span data-stu-id="9cb61-204">Switch to raw inputs by clicking on the icon in upper right corner.</span></span>

   ![Переключение на необработанные входные данные](./media/logic-apps-enterprise-integration-b2b-business-continuity/Edifactrawinputs.png)

10. <span data-ttu-id="9cb61-206">Выберите "Текст" с помощью средства выбора динамического содержимого и сохраните приложение логики.</span><span class="sxs-lookup"><span data-stu-id="9cb61-206">Select Body from the dynamic content picker, and save the logic app.</span></span>   

   ![Поля динамического содержимого](./media/logic-apps-enterprise-integration-b2b-business-continuity/X12CN7.png)

   <span data-ttu-id="9cb61-208">В зависимости от интервала времени триггер выполняет опрос таблицы полученных контрольных номеров для основного региона и извлекает новые записи при их наличии,</span><span class="sxs-lookup"><span data-stu-id="9cb61-208">Based on the time interval, the trigger polls the primary region received control number table and pulls the new records.</span></span>
   <span data-ttu-id="9cb61-209">а действие обновляет сведения о записях в учетной записи интеграции дополнительного региона.</span><span class="sxs-lookup"><span data-stu-id="9cb61-209">The action updates the records to the secondary region integration account.</span></span> 
   <span data-ttu-id="9cb61-210">Если эти сведения не обновляются, состояние триггера отображается как **Пропущено**.</span><span class="sxs-lookup"><span data-stu-id="9cb61-210">If there are no updates, the trigger status appears as **Skipped**.</span></span>

   ![Таблица контрольных номеров](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12recevicedcn8.png)

<span data-ttu-id="9cb61-212">В зависимости от интервала времени дополнительное состояние о среде выполнения реплицируется из основного региона в дополнительный.</span><span class="sxs-lookup"><span data-stu-id="9cb61-212">Based on the time interval, the incremental runtime status replicates from a primary region to a secondary region.</span></span> <span data-ttu-id="9cb61-213">Во время аварийного события, когда основной регион является недоступным, перенаправьте трафик к дополнительному региону для обеспечения непрерывности бизнес-процессов.</span><span class="sxs-lookup"><span data-stu-id="9cb61-213">During a disaster event, when the primary region is not available, direct traffic to the secondary region for business continuity.</span></span> 

## <a name="as2"></a><span data-ttu-id="9cb61-214">AS2</span><span class="sxs-lookup"><span data-stu-id="9cb61-214">AS2</span></span> 

<span data-ttu-id="9cb61-215">Для непрерывности бизнес-процессов для документов, использующих протокол AS2, используется идентификатор сообщения и значение MIC.</span><span class="sxs-lookup"><span data-stu-id="9cb61-215">Business continuity for documents that use the AS2 protocol is based on the message ID and the MIC value.</span></span>

> [!TIP]
> <span data-ttu-id="9cb61-216">Чтобы создать приложения логики, вы также можете использовать [шаблон быстрого запуска AS2](https://github.com/Azure/azure-quickstart-templates/pull/3302).</span><span class="sxs-lookup"><span data-stu-id="9cb61-216">You can also use the [AS2 quick start template](https://github.com/Azure/azure-quickstart-templates/pull/3302) to create logic apps.</span></span> <span data-ttu-id="9cb61-217">Для использования этого шаблона необходимо создать учетные записи интеграции для основного и дополнительного регионов.</span><span class="sxs-lookup"><span data-stu-id="9cb61-217">Creating primary and secondary integration accounts are prerequisites to use the template.</span></span> <span data-ttu-id="9cb61-218">Шаблон позволяет создать приложение логики с триггером и действием.</span><span class="sxs-lookup"><span data-stu-id="9cb61-218">The template helps create a logic app that has a trigger and an action.</span></span> <span data-ttu-id="9cb61-219">Приложение логики создает подключение от триггера к учетной записи интеграции для основного региона и подключение от действия к учетной записи интеграции для дополнительного региона.</span><span class="sxs-lookup"><span data-stu-id="9cb61-219">The logic app creates a connection from a trigger to a primary integration account and an action to a secondary integration account.</span></span>

1. <span data-ttu-id="9cb61-220">Создайте [приложение логики](../logic-apps/logic-apps-create-a-logic-app.md) в дополнительном регионе.</span><span class="sxs-lookup"><span data-stu-id="9cb61-220">Create a [logic app](../logic-apps/logic-apps-create-a-logic-app.md) in the secondary region.</span></span>  

2. <span data-ttu-id="9cb61-221">Выполните поиск **AS2** и выберите **AS2 — When a MIC value is created** (AS2 — При создании значения MIC).</span><span class="sxs-lookup"><span data-stu-id="9cb61-221">Search on **AS2**, and select **AS2 - When a MIC value is created**.</span></span>   

   ![Поиск по запросу "AS2"](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid1.png)

   <span data-ttu-id="9cb61-223">При выборе триггера вам будет предложено установить соединение с учетной записью интеграции.</span><span class="sxs-lookup"><span data-stu-id="9cb61-223">A trigger prompts you to establish a connection to an integration account.</span></span> 
   <span data-ttu-id="9cb61-224">Триггер необходимо подключить к учетной записи интеграции для основного региона.</span><span class="sxs-lookup"><span data-stu-id="9cb61-224">The trigger should be connected to a primary region integration account.</span></span> 
   
3. <span data-ttu-id="9cb61-225">Присвойте имя для подключения, выберите из списка свою *учетную запись интеграции для основного региона*, а затем выберите **Создать**.</span><span class="sxs-lookup"><span data-stu-id="9cb61-225">Enter a connection name, select your *primary region integration account* from the list, and choose **Create**.</span></span>

   ![Имя учетной записи интеграции для основного региона](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid2.png)

4. <span data-ttu-id="9cb61-227">Параметр **DateTime to start MIC value sync** (Дата и время для запуска синхронизации значения MIC) является необязательным.</span><span class="sxs-lookup"><span data-stu-id="9cb61-227">The **DateTime to start MIC value sync** setting is optional.</span></span> <span data-ttu-id="9cb61-228">Вы можете задать **частоту** с интервалом в **днях**, **часах**, **минутах** или **секундах**.</span><span class="sxs-lookup"><span data-stu-id="9cb61-228">The **Frequency** can be set to **Day**, **Hour**, **Minute**, or **Second** with an interval.</span></span>   

   ![Дата, время и частота](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid3.png)

5. <span data-ttu-id="9cb61-230">Выберите **New step** (Новый шаг) > **Добавить действие**.</span><span class="sxs-lookup"><span data-stu-id="9cb61-230">Select **New step** > **Add an action**.</span></span>  

   ![Выбор действий "Новый шаг" и "Добавить действие"](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid4.png)

6. <span data-ttu-id="9cb61-232">Выполните поиск **AS2** и выберите **AS2 - Add or update MIC contents** (AS2 — Добавление или обновление содержимого MIC).</span><span class="sxs-lookup"><span data-stu-id="9cb61-232">Search on **AS2**, and select **AS2 - Add or update MIC contents**.</span></span>  

   ![Добавление или обновление MIC](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid5.png)

7. <span data-ttu-id="9cb61-234">Для подключения действия к учетной записи интеграции для дополнительного региона выберите **Change connection** (Изменить подключение) > **Добавить новое подключение**, чтобы получить список доступных учетных записей интеграции.</span><span class="sxs-lookup"><span data-stu-id="9cb61-234">To connect an action to a secondary integration account, select **Change connection** > **Add new connection** for a list of the available integration accounts.</span></span> <span data-ttu-id="9cb61-235">Введите имя для подключения, выберите из списка свою *учетную запись интеграции для дополнительного региона*, а затем выберите **Создать**.</span><span class="sxs-lookup"><span data-stu-id="9cb61-235">Enter a connection name, select your *secondary region integration account* from the list, and choose **Create**.</span></span>

   ![Имя учетной записи интеграции для дополнительного региона](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid6.png)

8. <span data-ttu-id="9cb61-237">Переключитесь на необработанные входные данные, щелкнув значок в правом верхнем углу.</span><span class="sxs-lookup"><span data-stu-id="9cb61-237">Switch to raw inputs by clicking on the icon in upper right corner.</span></span>

   ![Переключение на необработанные входные данные](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2rawinputs.png)

9. <span data-ttu-id="9cb61-239">Выберите "Текст" с помощью средства выбора динамического содержимого и сохраните приложение логики.</span><span class="sxs-lookup"><span data-stu-id="9cb61-239">Select Body from the dynamic content picker, and save the logic app.</span></span>   

   ![Динамическое содержимое](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid7.png)

   <span data-ttu-id="9cb61-241">В зависимости от интервала времени триггер выполняет опрос таблицы для основного региона и извлекает новые записи,</span><span class="sxs-lookup"><span data-stu-id="9cb61-241">Based on the time interval, the trigger polls the primary region table and pulls the new records.</span></span> <span data-ttu-id="9cb61-242">а действие обновляет сведения о записях в учетной записи интеграции дополнительного региона.</span><span class="sxs-lookup"><span data-stu-id="9cb61-242">The action updates them to the secondary region integration account.</span></span> 
   <span data-ttu-id="9cb61-243">Если эти сведения не обновляются, состояние триггера отображается как **Пропущено**.</span><span class="sxs-lookup"><span data-stu-id="9cb61-243">If there are no updates, the trigger status appears as **Skipped**.</span></span>  

   ![Таблица для основного региона](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid8.png)

<span data-ttu-id="9cb61-245">В зависимости от интервала времени дополнительное состояние о среде выполнения реплицируется из основного региона в дополнительный.</span><span class="sxs-lookup"><span data-stu-id="9cb61-245">Based on the time interval, the incremental runtime status replicates from the primary region to the secondary region.</span></span> <span data-ttu-id="9cb61-246">Во время аварийного события, когда основной регион является недоступным, перенаправьте трафик к дополнительному региону для обеспечения непрерывности бизнес-процессов.</span><span class="sxs-lookup"><span data-stu-id="9cb61-246">During a disaster event, when the primary region is not available, direct traffic to the secondary region for business continuity.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="9cb61-247">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9cb61-247">Next steps</span></span>

[<span data-ttu-id="9cb61-248">Мониторинг сообщений B2B</span><span class="sxs-lookup"><span data-stu-id="9cb61-248">Monitor B2B messages</span></span>](logic-apps-monitor-b2b-message.md)

