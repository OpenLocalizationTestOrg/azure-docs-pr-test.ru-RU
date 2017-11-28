---
title: "Квоты и ограничения служб для пакетной службы Azure | Документация Майкрософт"
description: "Узнайте о квотах по умолчанию, лимитах и ограничениях пакетной службы Azure, а также о том, как запросить увеличение квоты."
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
ms.openlocfilehash: f3f69ed8d3a985afe07e648e7512a88b25278ced
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="batch-service-quotas-and-limits"></a><span data-ttu-id="d0324-103">Квоты и ограничения пакетной службы</span><span class="sxs-lookup"><span data-stu-id="d0324-103">Batch service quotas and limits</span></span>

<span data-ttu-id="d0324-104">Как и в других службах Azure, существуют ограничения на некоторые ресурсы, связанные с пакетной службой.</span><span class="sxs-lookup"><span data-stu-id="d0324-104">As with other Azure services, there are limits on certain resources associated with the Batch service.</span></span> <span data-ttu-id="d0324-105">Многие из этих ограничений являются квотами по умолчанию, которые Azure применяет на уровне подписки или учетной записи.</span><span class="sxs-lookup"><span data-stu-id="d0324-105">Many of these limits are default quotas applied by Azure at the subscription or account level.</span></span> <span data-ttu-id="d0324-106">В данной статье рассматриваются эти значения по умолчанию и то, как запросить увеличение квот.</span><span class="sxs-lookup"><span data-stu-id="d0324-106">This article discusses those defaults, and how you can request quota increases.</span></span>

<span data-ttu-id="d0324-107">Помните об этих квотах при разработке и масштабировании рабочих нагрузок пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="d0324-107">Keep these quotas in mind as you are designing and scaling up your Batch workloads.</span></span> <span data-ttu-id="d0324-108">Например, если в пуле не удается достичь указанного целевого числа вычислительных узлов, возможно, вы достигли основной квоты для учетной записи пакетной службы или региональной квоты на число ядер виртуальной машины для подписки.</span><span class="sxs-lookup"><span data-stu-id="d0324-108">For example, if your pool isn't reaching the target number of compute nodes you've specified, you might have reached the core quota limit for your Batch account, or a regional VM cores quota for your subscription.</span></span>

<span data-ttu-id="d0324-109">Можно запустить несколько рабочих нагрузок пакетной службы в одной учетной записи пакетной службы. Либо распределить рабочие нагрузки между учетными записями пакетной службы в рамках одной подписки, но в разных регионах Azure.</span><span class="sxs-lookup"><span data-stu-id="d0324-109">You can run multiple Batch workloads in a single Batch account, or distribute your workloads among Batch accounts that are in the same subscription, but in different Azure regions.</span></span>

<span data-ttu-id="d0324-110">Если планируется выполнять рабочие нагрузки в производственной среде с использованием пакетной службы, имеет смысл увеличить одну или несколько квот по сравнению со значениями по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="d0324-110">If you plan to run production workloads in Batch, you may need to increase one or more of the quotas above the default.</span></span> <span data-ttu-id="d0324-111">Для увеличения квоты отправьте (бесплатно) [запрос в службу поддержки клиентов](#increase-a-quota) .</span><span class="sxs-lookup"><span data-stu-id="d0324-111">If you want to raise a quota, you can open an online [customer support request](#increase-a-quota) at no charge.</span></span>

> [!NOTE]
> <span data-ttu-id="d0324-112">Квота — это кредитный лимит, а не гарантия наличия ресурсов.</span><span class="sxs-lookup"><span data-stu-id="d0324-112">A quota is a credit limit, not a capacity guarantee.</span></span> <span data-ttu-id="d0324-113">Если вам нужны ресурсы в очень большом объеме, обратитесь в службу поддержки Azure.</span><span class="sxs-lookup"><span data-stu-id="d0324-113">If you have large-scale capacity needs, please contact Azure support.</span></span>
> 
> 

## <a name="resource-quotas"></a><span data-ttu-id="d0324-114">Квоты ресурсов</span><span class="sxs-lookup"><span data-stu-id="d0324-114">Resource quotas</span></span>
[!INCLUDE [azure-batch-limits](../../includes/azure-batch-limits.md)]

## <a name="quotas-in-user-subscription-mode"></a><span data-ttu-id="d0324-115">Квоты в режиме пользовательской подписки</span><span class="sxs-lookup"><span data-stu-id="d0324-115">Quotas in user subscription mode</span></span>

<span data-ttu-id="d0324-116">Для учетной записи пакетной службы, для которой задан режим выделения пула **Пользовательская подписка**, виртуальные машины пакетной службы и другие ресурсы, такие как учетные записи хранения, создаются непосредственно в подписке при создании пула.</span><span class="sxs-lookup"><span data-stu-id="d0324-116">For a Batch account with pool allocation mode set to **user subscription**, Batch VMs and other resources, such as storage accounts, are created directly in your subscription when a pool is created.</span></span> <span data-ttu-id="d0324-117">Квота на ядра пакетной службы Azure не применяется к учетной записи, созданной в этом режиме.</span><span class="sxs-lookup"><span data-stu-id="d0324-117">The Azure Batch cores quota does not apply to an account created in this mode.</span></span> <span data-ttu-id="d0324-118">Вместо этого применяются региональные квоты на вычислительные ядра и другие ресурсы в подписке.</span><span class="sxs-lookup"><span data-stu-id="d0324-118">Instead, the quotas in your subscription for regional compute cores and other resources are applied.</span></span> <span data-ttu-id="d0324-119">Вы можете подробнее узнать об этих квотах в статье [Лимиты, квоты и ограничения подписки и обслуживания Azure](../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="d0324-119">Learn more about these quotas in [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md).</span></span>

<span data-ttu-id="d0324-120">При планировании использования ресурсов для учетной записи, созданной в режиме пользовательской подписки, обратите внимание, что для каждых 40 виртуальных машин Linux или 20 виртуальных машин Windows нужны следующие ресурсы пакетной службы (в дополнение к вычислительным ядрам):</span><span class="sxs-lookup"><span data-stu-id="d0324-120">When planning resource usage for an account created in user subscription mode, note the following Batch resources (in addition to compute cores) are required for every 40 Linux VMs, or 20 Windows VMs:</span></span>

| <span data-ttu-id="d0324-121">Ресурс</span><span class="sxs-lookup"><span data-stu-id="d0324-121">Resource</span></span> | <span data-ttu-id="d0324-122">Квота</span><span class="sxs-lookup"><span data-stu-id="d0324-122">Quota</span></span> | <span data-ttu-id="d0324-123">Поставщик</span><span class="sxs-lookup"><span data-stu-id="d0324-123">Provider</span></span> |
| --- | ---| --- |
| <span data-ttu-id="d0324-124">одна учетная запись хранения;</span><span class="sxs-lookup"><span data-stu-id="d0324-124">One storage account</span></span> | <span data-ttu-id="d0324-125">Учетные записи хранения</span><span class="sxs-lookup"><span data-stu-id="d0324-125">Storage Accounts</span></span> | <span data-ttu-id="d0324-126">Microsoft.Storage;</span><span class="sxs-lookup"><span data-stu-id="d0324-126">Microsoft.Storage</span></span> |
| <span data-ttu-id="d0324-127">Один общедоступный IP-адрес</span><span class="sxs-lookup"><span data-stu-id="d0324-127">One public IP address</span></span> | <span data-ttu-id="d0324-128">Общедоступные IP-адреса</span><span class="sxs-lookup"><span data-stu-id="d0324-128">Public IP Addresses</span></span> | <span data-ttu-id="d0324-129">Microsoft.Network.</span><span class="sxs-lookup"><span data-stu-id="d0324-129">Microsoft.Network</span></span> | 
| <span data-ttu-id="d0324-130">Одна виртуальную сеть</span><span class="sxs-lookup"><span data-stu-id="d0324-130">One virtual network</span></span> | <span data-ttu-id="d0324-131">Виртуальные сети</span><span class="sxs-lookup"><span data-stu-id="d0324-131">Virtual Networks</span></span> | <span data-ttu-id="d0324-132">Microsoft.Network.</span><span class="sxs-lookup"><span data-stu-id="d0324-132">Microsoft.Network</span></span> | 
| <span data-ttu-id="d0324-133">Одна группа безопасности сети</span><span class="sxs-lookup"><span data-stu-id="d0324-133">One network security group</span></span> | <span data-ttu-id="d0324-134">группы сетевой безопасности;</span><span class="sxs-lookup"><span data-stu-id="d0324-134">Network Security Groups</span></span> | <span data-ttu-id="d0324-135">Microsoft.Network.</span><span class="sxs-lookup"><span data-stu-id="d0324-135">Microsoft.Network</span></span> | 
| <span data-ttu-id="d0324-136">Один масштабируемый набор виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="d0324-136">One virtual machine scale set</span></span> | <span data-ttu-id="d0324-137">Наборы для масштабирования виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="d0324-137">Virtual Machine Scale Sets</span></span> | <span data-ttu-id="d0324-138">Microsoft.Compute;</span><span class="sxs-lookup"><span data-stu-id="d0324-138">Microsoft.Compute</span></span> | 
| <span data-ttu-id="d0324-139">Один балансировщик нагрузки</span><span class="sxs-lookup"><span data-stu-id="d0324-139">One load balancer</span></span> | <span data-ttu-id="d0324-140">Балансировщики нагрузки</span><span class="sxs-lookup"><span data-stu-id="d0324-140">Load Balancers</span></span> | <span data-ttu-id="d0324-141">Microsoft.Network.</span><span class="sxs-lookup"><span data-stu-id="d0324-141">Microsoft.Network</span></span> | 

<span data-ttu-id="d0324-142">Квота на ядра на региональном уровне или на семейство виртуальных машин должна быть задана в соответствии с размером виртуальной машины, требуемым для пула или пулов пакетной службы:</span><span class="sxs-lookup"><span data-stu-id="d0324-142">The cores quota at a regional level or per VM family should be set according to the VM size required for your Batch pool or pools:</span></span>

| <span data-ttu-id="d0324-143">Квота</span><span class="sxs-lookup"><span data-stu-id="d0324-143">Quota</span></span> | <span data-ttu-id="d0324-144">Поставщик</span><span class="sxs-lookup"><span data-stu-id="d0324-144">Provider</span></span> |
| --- | ---- |
| <span data-ttu-id="d0324-145">Общее региональное количество ядер</span><span class="sxs-lookup"><span data-stu-id="d0324-145">Total Regional Cores</span></span> | <span data-ttu-id="d0324-146">Microsoft.Compute;</span><span class="sxs-lookup"><span data-stu-id="d0324-146">Microsoft.Compute</span></span> |
| <span data-ttu-id="d0324-147">…</span><span class="sxs-lookup"><span data-stu-id="d0324-147">…</span></span> <span data-ttu-id="d0324-148">Семейство ядер</span><span class="sxs-lookup"><span data-stu-id="d0324-148">Family Cores</span></span> | <span data-ttu-id="d0324-149">Microsoft.Compute;</span><span class="sxs-lookup"><span data-stu-id="d0324-149">Microsoft.Compute</span></span> |



## <a name="other-limits"></a><span data-ttu-id="d0324-150">Другие ограничения</span><span class="sxs-lookup"><span data-stu-id="d0324-150">Other limits</span></span>
| <span data-ttu-id="d0324-151">**Ресурс**</span><span class="sxs-lookup"><span data-stu-id="d0324-151">**Resource**</span></span> | <span data-ttu-id="d0324-152">**Максимальное ограничение**</span><span class="sxs-lookup"><span data-stu-id="d0324-152">**Maximum Limit**</span></span> |
| --- | --- |
| <span data-ttu-id="d0324-153">[Количество параллельных задач](batch-parallel-node-tasks.md) на один вычислительный узел</span><span class="sxs-lookup"><span data-stu-id="d0324-153">[Concurrent tasks](batch-parallel-node-tasks.md) per compute node</span></span> |<span data-ttu-id="d0324-154">В 4 раза больше, чем количество ядер в узле</span><span class="sxs-lookup"><span data-stu-id="d0324-154">4 x number of node cores</span></span> |
| <span data-ttu-id="d0324-155">[Количество приложений](batch-application-packages.md) на одну учетную запись пакетной службы</span><span class="sxs-lookup"><span data-stu-id="d0324-155">[Applications](batch-application-packages.md) per Batch account</span></span> |<span data-ttu-id="d0324-156">20</span><span class="sxs-lookup"><span data-stu-id="d0324-156">20</span></span> |
| <span data-ttu-id="d0324-157">Пакеты приложения на приложение</span><span class="sxs-lookup"><span data-stu-id="d0324-157">Application packages per application</span></span> |<span data-ttu-id="d0324-158">40</span><span class="sxs-lookup"><span data-stu-id="d0324-158">40</span></span> |
| <span data-ttu-id="d0324-159">Размер пакета приложения (каждый)</span><span class="sxs-lookup"><span data-stu-id="d0324-159">Application package size (each)</span></span> |<span data-ttu-id="d0324-160">Примерно 195 ГБ<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="d0324-160">Approx. 195GB<sup>1</sup></span></span> |
| <span data-ttu-id="d0324-161">Максимальный размер задачи запуска</span><span class="sxs-lookup"><span data-stu-id="d0324-161">Maximum start task size</span></span> | <span data-ttu-id="d0324-162">32 768 символов<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="d0324-162">32768 characters<sup>2</sup></span></span> |

<span data-ttu-id="d0324-163"><sup>1</sup> Ограничение службы хранилища Azure для максимального размера блочного BLOB-объекта.</span><span class="sxs-lookup"><span data-stu-id="d0324-163"><sup>1</sup> Azure Storage limit for maximum block blob size</span></span><br /><span data-ttu-id="d0324-164">
<sup>2</sup> Включая файлы ресурсов и переменные среды</span><span class="sxs-lookup"><span data-stu-id="d0324-164">
<sup>2</sup> Includes resource files and environment variables</span></span>

## <a name="view-batch-quotas"></a><span data-ttu-id="d0324-165">Просмотр квот пакетной службы</span><span class="sxs-lookup"><span data-stu-id="d0324-165">View Batch quotas</span></span>
<span data-ttu-id="d0324-166">Просмотрите квоты своей учетной записи пакетной службы на [портале Azure][portal].</span><span class="sxs-lookup"><span data-stu-id="d0324-166">View your Batch account quotas in the [Azure portal][portal].</span></span>

1. <span data-ttu-id="d0324-167">Щелкните **Уч. записи пакетной службы** на портале, затем выберите учетную запись пакетной службы, которая вас интересует.</span><span class="sxs-lookup"><span data-stu-id="d0324-167">Select **Batch accounts** in the portal, then select the Batch account you're interested in.</span></span>
2. <span data-ttu-id="d0324-168">Выберите **Свойства** в колонке меню учетной записи пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="d0324-168">Select **Properties** on the Batch account's menu blade.</span></span>
3. <span data-ttu-id="d0324-169">В колонке **Свойства** отображаются квоты, которые в настоящее время действуют в отношении учетной записи пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="d0324-169">The Properties blade displays the **quotas** currently applied to the Batch account</span></span>
   
    ![Квоты для учетной записи пакетной службы][account_quotas]

<span data-ttu-id="d0324-171">Для учетной записи пакетной службы, созданной в режиме пользовательской подписки, просмотрите соответствующие квоты подписки на портале.</span><span class="sxs-lookup"><span data-stu-id="d0324-171">For a Batch account created in user subscription mode, view the related subscription quotas in the Azure Portal.</span></span>

1. <span data-ttu-id="d0324-172">Выберите **Подписки** и укажите подписку, используемую для учетной записи пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="d0324-172">Select **Subscriptions**, and select the subscription you are using for the Batch account.</span></span>

2. <span data-ttu-id="d0324-173">В колонке **Подписки** выберите **Использование и квоты**.</span><span class="sxs-lookup"><span data-stu-id="d0324-173">On the **Subscription** blade, select **Usage + quotas**.</span></span>



## <a name="increase-a-quota"></a><span data-ttu-id="d0324-174">Увеличение квоты</span><span class="sxs-lookup"><span data-stu-id="d0324-174">Increase a quota</span></span>
<span data-ttu-id="d0324-175">Выполните следующие действия, чтобы запросить увеличение квоты для своей учетной записи или подписки на [портале Azure][portal].</span><span class="sxs-lookup"><span data-stu-id="d0324-175">Follow these steps to request a quota increase for your Batch account or your subscription using the [Azure portal][portal].</span></span> <span data-ttu-id="d0324-176">Тип увеличения квоты зависит от режима выделения пула в вашей учетной записи пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="d0324-176">The type of quota increase depends on the pool allocation mode of your Batch account.</span></span>

### <a name="increase-a-batch-cores-quota"></a><span data-ttu-id="d0324-177">Увеличение квоты на ядра в пакетной службе</span><span class="sxs-lookup"><span data-stu-id="d0324-177">Increase a Batch cores quota</span></span> 

<span data-ttu-id="d0324-178">Если учетная запись пакетной службы была создана в режиме **пакетной службы**, выполните следующие действия, чтобы запросить увеличение квоты на ядра для пакетной службы:</span><span class="sxs-lookup"><span data-stu-id="d0324-178">If your Batch account was created in **Batch service** mode, follow these steps to request a Batch cores quota increase:</span></span>

1. <span data-ttu-id="d0324-179">На панели мониторинга портала выберите элемент **Справка и поддержка** или щелкните вопросительный знак (**?**) в правом верхнем углу портала.</span><span class="sxs-lookup"><span data-stu-id="d0324-179">Select the **Help + support** tile on your portal dashboard, or the question mark (**?**) in the upper-right corner of the portal.</span></span>
2. <span data-ttu-id="d0324-180">Выберите **Новый запрос в службу поддержки** > **Основные**.</span><span class="sxs-lookup"><span data-stu-id="d0324-180">Select **New support request** > **Basics**.</span></span>
3. <span data-ttu-id="d0324-181">В колонке **Основы** :</span><span class="sxs-lookup"><span data-stu-id="d0324-181">On the **Basics** blade:</span></span>
   
    <span data-ttu-id="d0324-182">а.</span><span class="sxs-lookup"><span data-stu-id="d0324-182">a.</span></span> <span data-ttu-id="d0324-183">**Тип проблемы** > **Квота**.</span><span class="sxs-lookup"><span data-stu-id="d0324-183">**Issue Type** > **Quota**</span></span>
   
    <span data-ttu-id="d0324-184">b.</span><span class="sxs-lookup"><span data-stu-id="d0324-184">b.</span></span> <span data-ttu-id="d0324-185">Выберите свою подписку.</span><span class="sxs-lookup"><span data-stu-id="d0324-185">Select your subscription.</span></span>
   
    <span data-ttu-id="d0324-186">В.</span><span class="sxs-lookup"><span data-stu-id="d0324-186">c.</span></span> <span data-ttu-id="d0324-187">**Тип квоты** > **Пакетная служба**.</span><span class="sxs-lookup"><span data-stu-id="d0324-187">**Quota type** > **Batch**</span></span>
   
    <span data-ttu-id="d0324-188">d.</span><span class="sxs-lookup"><span data-stu-id="d0324-188">d.</span></span> <span data-ttu-id="d0324-189">**План поддержки** > **Quota support - Included** (Поддержка квоты включена).</span><span class="sxs-lookup"><span data-stu-id="d0324-189">**Support plan** > **Quota support - Included**</span></span>
   
    <span data-ttu-id="d0324-190">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="d0324-190">Click **Next**.</span></span>
4. <span data-ttu-id="d0324-191">В колонке **Проблема** :</span><span class="sxs-lookup"><span data-stu-id="d0324-191">On the **Problem** blade:</span></span>
   
    <span data-ttu-id="d0324-192">а.</span><span class="sxs-lookup"><span data-stu-id="d0324-192">a.</span></span> <span data-ttu-id="d0324-193">Выберите **Серьезность** в соответствии с [последствиями для организации][support_sev].</span><span class="sxs-lookup"><span data-stu-id="d0324-193">Select a **Severity** according to your [business impact][support_sev].</span></span>
   
    <span data-ttu-id="d0324-194">b.</span><span class="sxs-lookup"><span data-stu-id="d0324-194">b.</span></span> <span data-ttu-id="d0324-195">В разделе **Сведения**укажите все квоты,которые хотите изменить, имя учетной записи пакетной службы и новые ограничения.</span><span class="sxs-lookup"><span data-stu-id="d0324-195">In **Details**, specify each quota you want to change, the Batch account name, and the new limit.</span></span>
   
    <span data-ttu-id="d0324-196">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="d0324-196">Click **Next**.</span></span>
5. <span data-ttu-id="d0324-197">В колонке **Контактные данные** :</span><span class="sxs-lookup"><span data-stu-id="d0324-197">On the **Contact information** blade:</span></span>
   
    <span data-ttu-id="d0324-198">а.</span><span class="sxs-lookup"><span data-stu-id="d0324-198">a.</span></span> <span data-ttu-id="d0324-199">Выберите **Preferred contact method**(Предпочтительный способ связи).</span><span class="sxs-lookup"><span data-stu-id="d0324-199">Select a **Preferred contact method**.</span></span>
   
    <span data-ttu-id="d0324-200">b.</span><span class="sxs-lookup"><span data-stu-id="d0324-200">b.</span></span> <span data-ttu-id="d0324-201">Проверьте и введите необходимые контактные данные.</span><span class="sxs-lookup"><span data-stu-id="d0324-201">Verify and enter the required contact details.</span></span>
   
    <span data-ttu-id="d0324-202">Щелкните **Создать** , чтобы отправить запрос в службу поддержки.</span><span class="sxs-lookup"><span data-stu-id="d0324-202">Click **Create** to submit the support request.</span></span>

<span data-ttu-id="d0324-203">После отправки запроса служба поддержки Azure свяжется с вами.</span><span class="sxs-lookup"><span data-stu-id="d0324-203">Once you've submitted your support request, Azure support will contact you.</span></span> <span data-ttu-id="d0324-204">Обратите внимание, что обработка запроса может занять до 2 рабочих дней.</span><span class="sxs-lookup"><span data-stu-id="d0324-204">Note that completing the request can take up to 2 business days.</span></span>

### <a name="increase-a-subscription-cores-quota"></a><span data-ttu-id="d0324-205">Увеличение квот на ядра для подписки</span><span class="sxs-lookup"><span data-stu-id="d0324-205">Increase a subscription cores quota</span></span>

<span data-ttu-id="d0324-206">Если учетная запись пакетной службы была создана в режиме **пользовательской подписки** и вам нужны дополнительные региональные ядра или ядра семейства виртуальных машин, запросите увеличение квоты в подписке.</span><span class="sxs-lookup"><span data-stu-id="d0324-206">If your Batch account was created in **user subscription** mode and you need additional regional or VM family cores, request a quota increase in your subscription.</span></span> <span data-ttu-id="d0324-207">Описание шагов см. в статье [Запросы на увеличение квоты ядер Resource Manager](../azure-supportability/resource-manager-core-quotas-request.md).</span><span class="sxs-lookup"><span data-stu-id="d0324-207">For steps, see [Resource Manager core quota increase requests](../azure-supportability/resource-manager-core-quotas-request.md).</span></span>



## <a name="related-topics"></a><span data-ttu-id="d0324-208">Связанные разделы</span><span class="sxs-lookup"><span data-stu-id="d0324-208">Related topics</span></span>
* [<span data-ttu-id="d0324-209">Создание учетной записи пакетной службы Azure на портале Azure и управление ею</span><span class="sxs-lookup"><span data-stu-id="d0324-209">Create an Azure Batch account using the Azure portal</span></span>](batch-account-create-portal.md)
* [<span data-ttu-id="d0324-210">Обзор функций пакетной службы Azure</span><span class="sxs-lookup"><span data-stu-id="d0324-210">Azure Batch feature overview</span></span>](batch-api-basics.md)
* [<span data-ttu-id="d0324-211">Подписка Azure, границы, квоты и ограничения службы</span><span class="sxs-lookup"><span data-stu-id="d0324-211">Azure subscription and service limits, quotas, and constraints</span></span>](../azure-subscription-service-limits.md)

[portal]: https://portal.azure.com
[portal_classic_increase]: https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/
[support_sev]: http://aka.ms/supportseverity

[account_quotas]: ./media/batch-quota-limit/accountquota_portal.PNG
