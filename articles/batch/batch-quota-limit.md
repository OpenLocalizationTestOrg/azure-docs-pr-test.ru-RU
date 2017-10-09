---
title: "aaaService квоты и лимиты для пакетной службы Azure | Документы Microsoft"
description: "Дополнительные сведения о квотах пакетной службы Azure по умолчанию, ограничения и ограничения и как квота toorequest повышает уровень"
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: 28998df4-8693-431d-b6ad-974c2f8db5fb
ms.service: batch
ms.workload: big-compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 6035d1c7618cfe97ebca3780e02a4ee34f54e534
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="batch-service-quotas-and-limits"></a><span data-ttu-id="21277-103">Квоты и ограничения пакетной службы</span><span class="sxs-lookup"><span data-stu-id="21277-103">Batch service quotas and limits</span></span>

<span data-ttu-id="21277-104">Как с другими службами Azure, существуют ограничения на некоторые ресурсы, связанные с hello пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="21277-104">As with other Azure services, there are limits on certain resources associated with hello Batch service.</span></span> <span data-ttu-id="21277-105">Многие из этих ограничений, по умолчанию квоты, применимые в Azure, на уровне учетной записи или hello подписки.</span><span class="sxs-lookup"><span data-stu-id="21277-105">Many of these limits are default quotas applied by Azure at hello subscription or account level.</span></span> <span data-ttu-id="21277-106">В данной статье рассматриваются эти значения по умолчанию и то, как запросить увеличение квот.</span><span class="sxs-lookup"><span data-stu-id="21277-106">This article discusses those defaults, and how you can request quota increases.</span></span>

<span data-ttu-id="21277-107">Помните об этих квотах при разработке и масштабировании рабочих нагрузок пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="21277-107">Keep these quotas in mind as you are designing and scaling up your Batch workloads.</span></span> <span data-ttu-id="21277-108">Например если пул не достигло hello целевое количество вычислительных узлов, которое вы указали, вы могли попасть hello core квоту для вашей учетной записи пакетной или региональной виртуальной Машины квота для вашей подписки.</span><span class="sxs-lookup"><span data-stu-id="21277-108">For example, if your pool isn't reaching hello target number of compute nodes you've specified, you might have reached hello core quota limit for your Batch account, or a regional VM cores quota for your subscription.</span></span>

<span data-ttu-id="21277-109">Запустите несколько рабочих нагрузок пакета в одной учетной записи пакетной или распределения рабочей нагрузки между пакета учетные записи, которые hello одной подписке, но в разных регионах Azure.</span><span class="sxs-lookup"><span data-stu-id="21277-109">You can run multiple Batch workloads in a single Batch account, or distribute your workloads among Batch accounts that are in hello same subscription, but in different Azure regions.</span></span>

<span data-ttu-id="21277-110">Если планируется toorun рабочих нагрузок в пакете, может потребоваться tooincrease один или несколько квот hello выше по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="21277-110">If you plan toorun production workloads in Batch, you may need tooincrease one or more of hello quotas above hello default.</span></span> <span data-ttu-id="21277-111">Если вы хотите tooraise квоту, можно открыть оперативного [запроса поддержки клиентов](#increase-a-quota) бесплатно.</span><span class="sxs-lookup"><span data-stu-id="21277-111">If you want tooraise a quota, you can open an online [customer support request](#increase-a-quota) at no charge.</span></span>

> [!NOTE]
> <span data-ttu-id="21277-112">Квота — это кредитный лимит, а не гарантия наличия ресурсов.</span><span class="sxs-lookup"><span data-stu-id="21277-112">A quota is a credit limit, not a capacity guarantee.</span></span> <span data-ttu-id="21277-113">Если вам нужны ресурсы в очень большом объеме, обратитесь в службу поддержки Azure.</span><span class="sxs-lookup"><span data-stu-id="21277-113">If you have large-scale capacity needs, please contact Azure support.</span></span>
> 
> 

## <a name="resource-quotas"></a><span data-ttu-id="21277-114">Квоты ресурсов</span><span class="sxs-lookup"><span data-stu-id="21277-114">Resource quotas</span></span>
[!INCLUDE [azure-batch-limits](../../includes/azure-batch-limits.md)]

## <a name="quotas-in-user-subscription-mode"></a><span data-ttu-id="21277-115">Квоты в режиме пользовательской подписки</span><span class="sxs-lookup"><span data-stu-id="21277-115">Quotas in user subscription mode</span></span>

<span data-ttu-id="21277-116">На учетную запись пакетного режима выделения пула задать слишком**подписки пользователя**, пакетной обработки виртуальные машины и другие ресурсы, такие как учетные записи хранения, созданные непосредственно в подписке при создании пула создается.</span><span class="sxs-lookup"><span data-stu-id="21277-116">For a Batch account with pool allocation mode set too**user subscription**, Batch VMs and other resources, such as storage accounts, are created directly in your subscription when a pool is created.</span></span> <span data-ttu-id="21277-117">Квота ядер Hello пакетной службы Azure не применяется tooan учетную запись, созданную в этом режиме.</span><span class="sxs-lookup"><span data-stu-id="21277-117">hello Azure Batch cores quota does not apply tooan account created in this mode.</span></span> <span data-ttu-id="21277-118">Вместо этого применяются квоты hello в вашей подписке для региональных вычислительных ядер и другие ресурсы.</span><span class="sxs-lookup"><span data-stu-id="21277-118">Instead, hello quotas in your subscription for regional compute cores and other resources are applied.</span></span> <span data-ttu-id="21277-119">Вы можете подробнее узнать об этих квотах в статье [Лимиты, квоты и ограничения подписки и обслуживания Azure](../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="21277-119">Learn more about these quotas in [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md).</span></span>

<span data-ttu-id="21277-120">При планировании потребление ресурсов при создании учетной записи в пользовательском режиме подписки, Примечание hello следующие ресурсы пакета (в дополнение toocompute ядра) являются обязательными для каждые 40 виртуальных машин Linux или 20 виртуальных машин Windows:</span><span class="sxs-lookup"><span data-stu-id="21277-120">When planning resource usage for an account created in user subscription mode, note hello following Batch resources (in addition toocompute cores) are required for every 40 Linux VMs, or 20 Windows VMs:</span></span>

| <span data-ttu-id="21277-121">Ресурс</span><span class="sxs-lookup"><span data-stu-id="21277-121">Resource</span></span> | <span data-ttu-id="21277-122">Квота</span><span class="sxs-lookup"><span data-stu-id="21277-122">Quota</span></span> | <span data-ttu-id="21277-123">Поставщик</span><span class="sxs-lookup"><span data-stu-id="21277-123">Provider</span></span> |
| --- | ---| --- |
| <span data-ttu-id="21277-124">одна учетная запись хранения;</span><span class="sxs-lookup"><span data-stu-id="21277-124">One storage account</span></span> | <span data-ttu-id="21277-125">Учетные записи хранения</span><span class="sxs-lookup"><span data-stu-id="21277-125">Storage Accounts</span></span> | <span data-ttu-id="21277-126">Microsoft.Storage;</span><span class="sxs-lookup"><span data-stu-id="21277-126">Microsoft.Storage</span></span> |
| <span data-ttu-id="21277-127">Один общедоступный IP-адрес</span><span class="sxs-lookup"><span data-stu-id="21277-127">One public IP address</span></span> | <span data-ttu-id="21277-128">Общедоступные IP-адреса</span><span class="sxs-lookup"><span data-stu-id="21277-128">Public IP Addresses</span></span> | <span data-ttu-id="21277-129">Microsoft.Network.</span><span class="sxs-lookup"><span data-stu-id="21277-129">Microsoft.Network</span></span> | 
| <span data-ttu-id="21277-130">Одна виртуальную сеть</span><span class="sxs-lookup"><span data-stu-id="21277-130">One virtual network</span></span> | <span data-ttu-id="21277-131">Виртуальные сети</span><span class="sxs-lookup"><span data-stu-id="21277-131">Virtual Networks</span></span> | <span data-ttu-id="21277-132">Microsoft.Network.</span><span class="sxs-lookup"><span data-stu-id="21277-132">Microsoft.Network</span></span> | 
| <span data-ttu-id="21277-133">Одна группа безопасности сети</span><span class="sxs-lookup"><span data-stu-id="21277-133">One network security group</span></span> | <span data-ttu-id="21277-134">группы сетевой безопасности;</span><span class="sxs-lookup"><span data-stu-id="21277-134">Network Security Groups</span></span> | <span data-ttu-id="21277-135">Microsoft.Network.</span><span class="sxs-lookup"><span data-stu-id="21277-135">Microsoft.Network</span></span> | 
| <span data-ttu-id="21277-136">Один масштабируемый набор виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="21277-136">One virtual machine scale set</span></span> | <span data-ttu-id="21277-137">Наборы для масштабирования виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="21277-137">Virtual Machine Scale Sets</span></span> | <span data-ttu-id="21277-138">Microsoft.Compute;</span><span class="sxs-lookup"><span data-stu-id="21277-138">Microsoft.Compute</span></span> | 
| <span data-ttu-id="21277-139">Один балансировщик нагрузки</span><span class="sxs-lookup"><span data-stu-id="21277-139">One load balancer</span></span> | <span data-ttu-id="21277-140">Балансировщики нагрузки</span><span class="sxs-lookup"><span data-stu-id="21277-140">Load Balancers</span></span> | <span data-ttu-id="21277-141">Microsoft.Network.</span><span class="sxs-lookup"><span data-stu-id="21277-141">Microsoft.Network</span></span> | 

<span data-ttu-id="21277-142">Квота ядер Hello на региональном уровне или на семейство виртуальная машина должна быть набор соответствующим toohello ВМ размера для пула или пулов:</span><span class="sxs-lookup"><span data-stu-id="21277-142">hello cores quota at a regional level or per VM family should be set according toohello VM size required for your Batch pool or pools:</span></span>

| <span data-ttu-id="21277-143">Quota</span><span class="sxs-lookup"><span data-stu-id="21277-143">Quota</span></span> | <span data-ttu-id="21277-144">Поставщик</span><span class="sxs-lookup"><span data-stu-id="21277-144">Provider</span></span> |
| --- | ---- |
| <span data-ttu-id="21277-145">Общее региональное количество ядер</span><span class="sxs-lookup"><span data-stu-id="21277-145">Total Regional Cores</span></span> | <span data-ttu-id="21277-146">Microsoft.Compute;</span><span class="sxs-lookup"><span data-stu-id="21277-146">Microsoft.Compute</span></span> |
| <span data-ttu-id="21277-147">…</span><span class="sxs-lookup"><span data-stu-id="21277-147">…</span></span> <span data-ttu-id="21277-148">Семейство ядер</span><span class="sxs-lookup"><span data-stu-id="21277-148">Family Cores</span></span> | <span data-ttu-id="21277-149">Microsoft.Compute;</span><span class="sxs-lookup"><span data-stu-id="21277-149">Microsoft.Compute</span></span> |



## <a name="other-limits"></a><span data-ttu-id="21277-150">Другие ограничения</span><span class="sxs-lookup"><span data-stu-id="21277-150">Other limits</span></span>
| <span data-ttu-id="21277-151">**Ресурс**</span><span class="sxs-lookup"><span data-stu-id="21277-151">**Resource**</span></span> | <span data-ttu-id="21277-152">**Максимальное ограничение**</span><span class="sxs-lookup"><span data-stu-id="21277-152">**Maximum Limit**</span></span> |
| --- | --- |
| <span data-ttu-id="21277-153">[Количество параллельных задач](batch-parallel-node-tasks.md) на один вычислительный узел</span><span class="sxs-lookup"><span data-stu-id="21277-153">[Concurrent tasks](batch-parallel-node-tasks.md) per compute node</span></span> |<span data-ttu-id="21277-154">В 4 раза больше, чем количество ядер в узле</span><span class="sxs-lookup"><span data-stu-id="21277-154">4 x number of node cores</span></span> |
| <span data-ttu-id="21277-155">[Количество приложений](batch-application-packages.md) на одну учетную запись пакетной службы</span><span class="sxs-lookup"><span data-stu-id="21277-155">[Applications](batch-application-packages.md) per Batch account</span></span> |<span data-ttu-id="21277-156">20</span><span class="sxs-lookup"><span data-stu-id="21277-156">20</span></span> |
| <span data-ttu-id="21277-157">Пакеты приложения на приложение</span><span class="sxs-lookup"><span data-stu-id="21277-157">Application packages per application</span></span> |<span data-ttu-id="21277-158">40</span><span class="sxs-lookup"><span data-stu-id="21277-158">40</span></span> |
| <span data-ttu-id="21277-159">Размер пакета приложения (каждый)</span><span class="sxs-lookup"><span data-stu-id="21277-159">Application package size (each)</span></span> |<span data-ttu-id="21277-160">Примерно 195 ГБ<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="21277-160">Approx. 195GB<sup>1</sup></span></span> |
| <span data-ttu-id="21277-161">Максимальный размер задачи запуска</span><span class="sxs-lookup"><span data-stu-id="21277-161">Maximum start task size</span></span> | <span data-ttu-id="21277-162">32 768 символов<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="21277-162">32768 characters<sup>2</sup></span></span> |

<span data-ttu-id="21277-163"><sup>1</sup> Ограничение службы хранилища Azure для максимального размера блочного BLOB-объекта.</span><span class="sxs-lookup"><span data-stu-id="21277-163"><sup>1</sup> Azure Storage limit for maximum block blob size</span></span><br /><span data-ttu-id="21277-164">
<sup>2</sup> Включая файлы ресурсов и переменные среды</span><span class="sxs-lookup"><span data-stu-id="21277-164">
<sup>2</sup> Includes resource files and environment variables</span></span>

## <a name="view-batch-quotas"></a><span data-ttu-id="21277-165">Просмотр квот пакетной службы</span><span class="sxs-lookup"><span data-stu-id="21277-165">View Batch quotas</span></span>
<span data-ttu-id="21277-166">Просмотр квотами пакетной учетной записи в hello [портал Azure][portal].</span><span class="sxs-lookup"><span data-stu-id="21277-166">View your Batch account quotas in hello [Azure portal][portal].</span></span>

1. <span data-ttu-id="21277-167">Выберите **учетные записи пакета** hello портала, выберите учетную запись пакета hello, вас интересует.</span><span class="sxs-lookup"><span data-stu-id="21277-167">Select **Batch accounts** in hello portal, then select hello Batch account you're interested in.</span></span>
2. <span data-ttu-id="21277-168">Выберите **свойства** колонке меню учетной записи пакетной hello.</span><span class="sxs-lookup"><span data-stu-id="21277-168">Select **Properties** on hello Batch account's menu blade.</span></span>
3. <span data-ttu-id="21277-169">Свойства колонке Hello отображает hello **квоты** примененные toohello пакетной учетной записи</span><span class="sxs-lookup"><span data-stu-id="21277-169">hello Properties blade displays hello **quotas** currently applied toohello Batch account</span></span>
   
    ![Квоты для учетной записи пакетной службы][account_quotas]

<span data-ttu-id="21277-171">Для пакетной учетной записи, созданные в пользовательском режиме подписки hello представления, связанные с квотами подписки в hello портала Azure.</span><span class="sxs-lookup"><span data-stu-id="21277-171">For a Batch account created in user subscription mode, view hello related subscription quotas in hello Azure Portal.</span></span>

1. <span data-ttu-id="21277-172">Выберите **подписки**и выберите hello подписку, которую вы используете для hello пакетной учетной записи.</span><span class="sxs-lookup"><span data-stu-id="21277-172">Select **Subscriptions**, and select hello subscription you are using for hello Batch account.</span></span>

2. <span data-ttu-id="21277-173">На hello **подписки** колонке выберите **использование + квоты**.</span><span class="sxs-lookup"><span data-stu-id="21277-173">On hello **Subscription** blade, select **Usage + quotas**.</span></span>



## <a name="increase-a-quota"></a><span data-ttu-id="21277-174">Увеличение квоты</span><span class="sxs-lookup"><span data-stu-id="21277-174">Increase a quota</span></span>
<span data-ttu-id="21277-175">Выполните эти шаги toorequest, увеличьте квоту для учетной записи пакета или подписки с помощью hello [портал Azure][portal].</span><span class="sxs-lookup"><span data-stu-id="21277-175">Follow these steps toorequest a quota increase for your Batch account or your subscription using hello [Azure portal][portal].</span></span> <span data-ttu-id="21277-176">Тип Hello увеличение квоты, зависит от режима выделения пула hello учетная запись пакетной.</span><span class="sxs-lookup"><span data-stu-id="21277-176">hello type of quota increase depends on hello pool allocation mode of your Batch account.</span></span>

### <a name="increase-a-batch-cores-quota"></a><span data-ttu-id="21277-177">Увеличение квоты на ядра в пакетной службе</span><span class="sxs-lookup"><span data-stu-id="21277-177">Increase a Batch cores quota</span></span> 

<span data-ttu-id="21277-178">Если учетная запись пакетной был создан в **пакетной службы** режим, выполните эти действия toorequest на увеличение квоты ядер пакета:</span><span class="sxs-lookup"><span data-stu-id="21277-178">If your Batch account was created in **Batch service** mode, follow these steps toorequest a Batch cores quota increase:</span></span>

1. <span data-ttu-id="21277-179">Выберите hello **Справка и поддержка** плитки на панели мониторинга портала или hello вопросительный знак (**?**) в правом верхнем углу hello hello портала.</span><span class="sxs-lookup"><span data-stu-id="21277-179">Select hello **Help + support** tile on your portal dashboard, or hello question mark (**?**) in hello upper-right corner of hello portal.</span></span>
2. <span data-ttu-id="21277-180">Выберите **Новый запрос в службу поддержки** > **Основные**.</span><span class="sxs-lookup"><span data-stu-id="21277-180">Select **New support request** > **Basics**.</span></span>
3. <span data-ttu-id="21277-181">На hello **основы** колонки:</span><span class="sxs-lookup"><span data-stu-id="21277-181">On hello **Basics** blade:</span></span>
   
    <span data-ttu-id="21277-182">а.</span><span class="sxs-lookup"><span data-stu-id="21277-182">a.</span></span> <span data-ttu-id="21277-183">**Тип проблемы** > **Квота**.</span><span class="sxs-lookup"><span data-stu-id="21277-183">**Issue Type** > **Quota**</span></span>
   
    <span data-ttu-id="21277-184">b.</span><span class="sxs-lookup"><span data-stu-id="21277-184">b.</span></span> <span data-ttu-id="21277-185">Выберите свою подписку.</span><span class="sxs-lookup"><span data-stu-id="21277-185">Select your subscription.</span></span>
   
    <span data-ttu-id="21277-186">В.</span><span class="sxs-lookup"><span data-stu-id="21277-186">c.</span></span> <span data-ttu-id="21277-187">**Тип квоты** > **Пакетная служба**.</span><span class="sxs-lookup"><span data-stu-id="21277-187">**Quota type** > **Batch**</span></span>
   
    <span data-ttu-id="21277-188">d.</span><span class="sxs-lookup"><span data-stu-id="21277-188">d.</span></span> <span data-ttu-id="21277-189">**План поддержки** > **Quota support - Included** (Поддержка квоты включена).</span><span class="sxs-lookup"><span data-stu-id="21277-189">**Support plan** > **Quota support - Included**</span></span>
   
    <span data-ttu-id="21277-190">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="21277-190">Click **Next**.</span></span>
4. <span data-ttu-id="21277-191">На hello **проблема** колонки:</span><span class="sxs-lookup"><span data-stu-id="21277-191">On hello **Problem** blade:</span></span>
   
    <span data-ttu-id="21277-192">а.</span><span class="sxs-lookup"><span data-stu-id="21277-192">a.</span></span> <span data-ttu-id="21277-193">Выберите **серьезность** tooyour в соответствии с [влияние на бизнес][support_sev].</span><span class="sxs-lookup"><span data-stu-id="21277-193">Select a **Severity** according tooyour [business impact][support_sev].</span></span>
   
    <span data-ttu-id="21277-194">b.</span><span class="sxs-lookup"><span data-stu-id="21277-194">b.</span></span> <span data-ttu-id="21277-195">В **сведения**, укажите каждой из квот toochange, имя учетной записи пакетной hello и hello новое ограничение.</span><span class="sxs-lookup"><span data-stu-id="21277-195">In **Details**, specify each quota you want toochange, hello Batch account name, and hello new limit.</span></span>
   
    <span data-ttu-id="21277-196">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="21277-196">Click **Next**.</span></span>
5. <span data-ttu-id="21277-197">На hello **контактные данные** колонки:</span><span class="sxs-lookup"><span data-stu-id="21277-197">On hello **Contact information** blade:</span></span>
   
    <span data-ttu-id="21277-198">а.</span><span class="sxs-lookup"><span data-stu-id="21277-198">a.</span></span> <span data-ttu-id="21277-199">Выберите **Preferred contact method**(Предпочтительный способ связи).</span><span class="sxs-lookup"><span data-stu-id="21277-199">Select a **Preferred contact method**.</span></span>
   
    <span data-ttu-id="21277-200">b.</span><span class="sxs-lookup"><span data-stu-id="21277-200">b.</span></span> <span data-ttu-id="21277-201">Проверьте и введите необходимые hello контактные сведения.</span><span class="sxs-lookup"><span data-stu-id="21277-201">Verify and enter hello required contact details.</span></span>
   
    <span data-ttu-id="21277-202">Нажмите кнопку **создать** запроса на поддержку toosubmit hello.</span><span class="sxs-lookup"><span data-stu-id="21277-202">Click **Create** toosubmit hello support request.</span></span>

<span data-ttu-id="21277-203">После отправки запроса служба поддержки Azure свяжется с вами.</span><span class="sxs-lookup"><span data-stu-id="21277-203">Once you've submitted your support request, Azure support will contact you.</span></span> <span data-ttu-id="21277-204">Обратите внимание, что завершения hello запроса может занять too2 рабочих дней.</span><span class="sxs-lookup"><span data-stu-id="21277-204">Note that completing hello request can take up too2 business days.</span></span>

### <a name="increase-a-subscription-cores-quota"></a><span data-ttu-id="21277-205">Увеличение квот на ядра для подписки</span><span class="sxs-lookup"><span data-stu-id="21277-205">Increase a subscription cores quota</span></span>

<span data-ttu-id="21277-206">Если учетная запись пакетной службы была создана в режиме **пользовательской подписки** и вам нужны дополнительные региональные ядра или ядра семейства виртуальных машин, запросите увеличение квоты в подписке.</span><span class="sxs-lookup"><span data-stu-id="21277-206">If your Batch account was created in **user subscription** mode and you need additional regional or VM family cores, request a quota increase in your subscription.</span></span> <span data-ttu-id="21277-207">Описание шагов см. в статье [Запросы на увеличение квоты ядер Resource Manager](../azure-supportability/resource-manager-core-quotas-request.md).</span><span class="sxs-lookup"><span data-stu-id="21277-207">For steps, see [Resource Manager core quota increase requests](../azure-supportability/resource-manager-core-quotas-request.md).</span></span>



## <a name="related-topics"></a><span data-ttu-id="21277-208">Связанные разделы</span><span class="sxs-lookup"><span data-stu-id="21277-208">Related topics</span></span>
* [<span data-ttu-id="21277-209">Создать учетную запись пакетной службы Azure с помощью портала Azure hello</span><span class="sxs-lookup"><span data-stu-id="21277-209">Create an Azure Batch account using hello Azure portal</span></span>](batch-account-create-portal.md)
* [<span data-ttu-id="21277-210">Обзор функций пакетной службы Azure</span><span class="sxs-lookup"><span data-stu-id="21277-210">Azure Batch feature overview</span></span>](batch-api-basics.md)
* [<span data-ttu-id="21277-211">Подписка Azure, границы, квоты и ограничения службы</span><span class="sxs-lookup"><span data-stu-id="21277-211">Azure subscription and service limits, quotas, and constraints</span></span>](../azure-subscription-service-limits.md)

[portal]: https://portal.azure.com
[portal_classic_increase]: https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/
[support_sev]: http://aka.ms/supportseverity

[account_quotas]: ./media/batch-quota-limit/accountquota_portal.PNG
