---
title: "Автомасштабирование облачной службы на классическом портале | Документация Майкрософт"
description: "(классический) Узнайте, как с помощью классического портала настроить правила автомасштабирования для веб-роли или рабочей роли облачной службы в Azure."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: eb167d70-4eba-42a4-b157-d8d0688abf4b
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: adegeo
ms.openlocfilehash: 90d55bbac6e113d6add848ace67cf0749e26342b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-configure-auto-scaling-for-a-cloud-service-in-the-classic-portal"></a><span data-ttu-id="8ba78-103">Как настроить автомасштабирование для облачной службы на классическом портале</span><span class="sxs-lookup"><span data-stu-id="8ba78-103">How to configure auto scaling for a Cloud Service in the classic portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8ba78-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="8ba78-104">Azure portal</span></span>](cloud-services-how-to-scale-portal.md)
> * [<span data-ttu-id="8ba78-105">классическом портале Azure</span><span class="sxs-lookup"><span data-stu-id="8ba78-105">Azure classic portal</span></span>](cloud-services-how-to-scale.md)

<span data-ttu-id="8ba78-106">На странице "Масштаб" классического портала Azure можно настроить параметры автомасштабирования для веб-роли или рабочей роли.</span><span class="sxs-lookup"><span data-stu-id="8ba78-106">On the Scale page of the Azure classic portal, you can configure automatic scale settings for your web role or worker role.</span></span> <span data-ttu-id="8ba78-107">Кроме того, можно настроить ручное масштабирование, а не автомасштабирование на основе правил.</span><span class="sxs-lookup"><span data-stu-id="8ba78-107">Alternatively, you can configure manual scaling instead of rules-based automatic scaling.</span></span>

> [!NOTE]
> <span data-ttu-id="8ba78-108">Эта статья посвящена веб-ролям и рабочим ролям облачной службы.</span><span class="sxs-lookup"><span data-stu-id="8ba78-108">This article focuses on Cloud Service web and worker roles.</span></span> <span data-ttu-id="8ba78-109">Виртуальные машины (классические), создаваемые напрямую, размещаются в облачной службе.</span><span class="sxs-lookup"><span data-stu-id="8ba78-109">When you create a virtual machine (classic) directly, it is hosted in a cloud service.</span></span> <span data-ttu-id="8ba78-110">Некоторые из представленных здесь сведений относятся к таким типам виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="8ba78-110">Some of this information applies to these types of virtual machines.</span></span> <span data-ttu-id="8ba78-111">Масштабирование группы доступности виртуальных машин представляет собой включение и отключение этих машин в соответствии с заданными правилами масштабирования.</span><span class="sxs-lookup"><span data-stu-id="8ba78-111">Scaling an availability set of virtual machines is just shutting them on and off based on the scale rules you configure.</span></span> <span data-ttu-id="8ba78-112">Дополнительные сведения о виртуальных машинах и группах доступности см. в статье [Как настроить группу доступности для виртуальных машин Windows в классической модели развертывания](../virtual-machines/windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8ba78-112">For more information about Virtual Machines and availability sets, see [Manage the Availability of Virtual Machines](../virtual-machines/windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span></span>

<span data-ttu-id="8ba78-113">При настройке масштабирования приложения следует учитывать следующие сведения.</span><span class="sxs-lookup"><span data-stu-id="8ba78-113">You should consider the following information before you configure scaling for your application:</span></span>

* <span data-ttu-id="8ba78-114">Масштабирование зависит от использования ядер.</span><span class="sxs-lookup"><span data-stu-id="8ba78-114">Scaling is affected by core usage.</span></span>

    <span data-ttu-id="8ba78-115">Более крупные экземпляры ролей задействуют больше ядер.</span><span class="sxs-lookup"><span data-stu-id="8ba78-115">Larger role instances use more cores.</span></span> <span data-ttu-id="8ba78-116">Масштабировать приложение можно только в пределах количества ядер для используемой подписки.</span><span class="sxs-lookup"><span data-stu-id="8ba78-116">You can scale an application only within the limit of cores for your subscription.</span></span> <span data-ttu-id="8ba78-117">Предположим, что ваша подписка имеет ограничение в 20 ядер.</span><span class="sxs-lookup"><span data-stu-id="8ba78-117">For example, say your subscription has a limit of 20 cores.</span></span> <span data-ttu-id="8ba78-118">Если выполняется приложение с двумя средними по размерам облачными службами (всего четыре ядра), то можно увеличить масштаб других развернутых в подписке облачных служб, охватив оставшиеся 16 ядер.</span><span class="sxs-lookup"><span data-stu-id="8ba78-118">If you run an application with two medium-sized cloud services (a total of 4 cores), you can only scale up other cloud service deployments in your subscription by the remaining 16 cores.</span></span> <span data-ttu-id="8ba78-119">Дополнительные сведения о размерах см. в статье [Размеры для облачных служб](cloud-services-sizes-specs.md).</span><span class="sxs-lookup"><span data-stu-id="8ba78-119">For more information about sizes, see [Cloud Service Sizes](cloud-services-sizes-specs.md).</span></span>

* <span data-ttu-id="8ba78-120">Прежде чем приступить к масштабированию приложения на основе порогового значения сообщений, необходимо создать очередь и связать ее с ролью.</span><span class="sxs-lookup"><span data-stu-id="8ba78-120">You must create a queue and associate it with a role before you can scale an application based on a message threshold.</span></span> <span data-ttu-id="8ba78-121">Дополнительные сведения см. в статье [Приступая к работе с хранилищем очередей Azure с помощью .NET](../storage/queues/storage-dotnet-how-to-use-queues.md).</span><span class="sxs-lookup"><span data-stu-id="8ba78-121">For more information, see [How to use the Queue Storage Service](../storage/queues/storage-dotnet-how-to-use-queues.md).</span></span>

* <span data-ttu-id="8ba78-122">Можно масштабировать ресурсы, привязанные к используемой облачной службе.</span><span class="sxs-lookup"><span data-stu-id="8ba78-122">You can scale resources that are linked to your cloud service.</span></span> <span data-ttu-id="8ba78-123">Дополнительные сведения о связанных ресурсах см. в разделе [Практическое руководство. Привязка ресурсов к облачной службе](cloud-services-how-to-manage.md#how-to-link-a-resource-to-a-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="8ba78-123">For more information about linking resources, see [How to: Link a resource to a cloud service](cloud-services-how-to-manage.md#how-to-link-a-resource-to-a-cloud-service).</span></span>

* <span data-ttu-id="8ba78-124">В целях обеспечения высокой доступности приложения необходимо убедиться, что приложение развернуто с двумя и более экземплярами ролей.</span><span class="sxs-lookup"><span data-stu-id="8ba78-124">To enable high availability of your application, you should ensure that it is deployed with two or more role instances.</span></span> <span data-ttu-id="8ba78-125">Дополнительные сведения см. в разделе [Соглашения об уровне обслуживания](https://azure.microsoft.com/support/legal/sla/).</span><span class="sxs-lookup"><span data-stu-id="8ba78-125">For more information, see [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).</span></span>

## <a name="schedule-scaling"></a><span data-ttu-id="8ba78-126">Планирование масштабирования</span><span class="sxs-lookup"><span data-stu-id="8ba78-126">Schedule scaling</span></span>
<span data-ttu-id="8ba78-127">По умолчанию все роли следуют установленному расписанию.</span><span class="sxs-lookup"><span data-stu-id="8ba78-127">By default, all roles do not follow a specific schedule.</span></span> <span data-ttu-id="8ba78-128">Это значит, что изменения в параметрах действуют все время в течение года.</span><span class="sxs-lookup"><span data-stu-id="8ba78-128">Therefore, any settings changed apply to all times and all days throughout the year.</span></span> <span data-ttu-id="8ba78-129">При желании вы можете настроить ручное или автоматическое масштабирование для одного из следующих режимов:</span><span class="sxs-lookup"><span data-stu-id="8ba78-129">If you want, you can setup manual or automatic scaling for one of the following modes:</span></span>

* <span data-ttu-id="8ba78-130">дни недели;</span><span class="sxs-lookup"><span data-stu-id="8ba78-130">Weekdays</span></span>
* <span data-ttu-id="8ba78-131">выходные дни;</span><span class="sxs-lookup"><span data-stu-id="8ba78-131">Weekends</span></span>
* <span data-ttu-id="8ba78-132">ночное время будних дней;</span><span class="sxs-lookup"><span data-stu-id="8ba78-132">Week nights</span></span>
* <span data-ttu-id="8ba78-133">утреннее время будних дней;</span><span class="sxs-lookup"><span data-stu-id="8ba78-133">Week mornings</span></span>
* <span data-ttu-id="8ba78-134">определенные даты;</span><span class="sxs-lookup"><span data-stu-id="8ba78-134">Specific dates</span></span>
* <span data-ttu-id="8ba78-135">определенные диапазоны дат.</span><span class="sxs-lookup"><span data-stu-id="8ba78-135">Specific date ranges</span></span>

<span data-ttu-id="8ba78-136">Параметр расписания настраивается на [классическом портале Azure](https://manage.windowsazure.com/), на странице</span><span class="sxs-lookup"><span data-stu-id="8ba78-136">The schedule setting is configured in the [Azure classic portal](https://manage.windowsazure.com/) on the</span></span>  
<span data-ttu-id="8ba78-137">**Облачные службы** > **\[Ваша облачная служба\]** > **Масштабирование** > **\[Рабочая или промежуточная среда\]**.</span><span class="sxs-lookup"><span data-stu-id="8ba78-137">**Cloud Services** > **\[Your cloud service\]** > **Scale** > **\[Production or Staging\]** page.</span></span>

<span data-ttu-id="8ba78-138">Нажмите кнопку **Настройка параметров расписания** для каждой роли, которую необходимо изменить.</span><span class="sxs-lookup"><span data-stu-id="8ba78-138">Click the **set up schedule times** button for each role you want to change.</span></span>

![Автомасштабирование облачной службы по расписанию][scale_schedules]

## <a name="manual-scale"></a><span data-ttu-id="8ba78-140">Ручное масштабирование</span><span class="sxs-lookup"><span data-stu-id="8ba78-140">Manual scale</span></span>
<span data-ttu-id="8ba78-141">На странице **Масштабирование** можно вручную увеличить или уменьшить количество работающих в облачной службе экземпляров.</span><span class="sxs-lookup"><span data-stu-id="8ba78-141">On the **Scale** page, you can manually increase or decrease the number of running instances in a cloud service.</span></span> <span data-ttu-id="8ba78-142">Этот параметр настраивается для каждого создаваемого расписания, а если расписания нет, то он действует постоянно.</span><span class="sxs-lookup"><span data-stu-id="8ba78-142">This setting is configured for each schedule you've created or to all time if you have not created a schedule.</span></span>

1. <span data-ttu-id="8ba78-143">На [классическом портале Azure](https://manage.windowsazure.com/)щелкните **Облачные службы**, затем щелкните имя облачной службы, чтобы открыть панель мониторинга.</span><span class="sxs-lookup"><span data-stu-id="8ba78-143">In the [Azure classic portal](https://manage.windowsazure.com/), click **Cloud Services**, and then click the name of the cloud service to open the dashboard.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="8ba78-144">Если вы не видите облачную службу, измените **рабочую среду** на **промежуточную** или наоборот.</span><span class="sxs-lookup"><span data-stu-id="8ba78-144">If you don't see your cloud service, you may need to change from **Production** to **Staging** or vice versa.</span></span>

2. <span data-ttu-id="8ba78-145">Щелкните пункт **Масштаб**.</span><span class="sxs-lookup"><span data-stu-id="8ba78-145">Click **Scale**.</span></span>
3. <span data-ttu-id="8ba78-146">Выберите расписание, для которого нужно изменить параметры масштабирования.</span><span class="sxs-lookup"><span data-stu-id="8ba78-146">Select the schedule you want to change scaling options for.</span></span> <span data-ttu-id="8ba78-147">Если расписание не определено, используется значение по умолчанию — *Не настроено*.</span><span class="sxs-lookup"><span data-stu-id="8ba78-147">*No scheduled times* is the default if you have no schedules defined.</span></span>
4. <span data-ttu-id="8ba78-148">Найдите раздел **Масштабирование по метрике** и выберите параметр **Нет**.</span><span class="sxs-lookup"><span data-stu-id="8ba78-148">Find the **Scale by metric** section and select **NONE**.</span></span> <span data-ttu-id="8ba78-149">Это параметр по умолчанию для всех ролей.</span><span class="sxs-lookup"><span data-stu-id="8ba78-149">This setting is the default for all roles.</span></span>
5. <span data-ttu-id="8ba78-150">Каждая роль в облачной службе имеет ползунок для изменения количества используемых экземпляров.</span><span class="sxs-lookup"><span data-stu-id="8ba78-150">Each role in the cloud service has a slider for changing the number of instances to use.</span></span>
   
    ![Ручное масштабирование роли облачной службы][manual_scale]
   
    <span data-ttu-id="8ba78-152">Если вам нужно несколько экземпляров, измените [размер виртуальной машины облачной службы](cloud-services-sizes-specs.md).</span><span class="sxs-lookup"><span data-stu-id="8ba78-152">If you need more instances, you may need to change the [cloud service virtual machine size](cloud-services-sizes-specs.md).</span></span>
6. <span data-ttu-id="8ba78-153">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="8ba78-153">Click **Save**.</span></span>  
   <span data-ttu-id="8ba78-154">Экземпляры роли добавляются и удаляются в зависимости от вашего выбора.</span><span class="sxs-lookup"><span data-stu-id="8ba78-154">Role instances are added or removed based on your selections.</span></span>

> [!TIP]
> <span data-ttu-id="8ba78-155">Увидев значок ![][tip_icon], наведите на него указатель мыши, и вы получите справку о том, что именно делает соответствующий параметр.</span><span class="sxs-lookup"><span data-stu-id="8ba78-155">Whenever you see ![][tip_icon] move your mouse to it and you can get help about what a specific setting does.</span></span>

## <a name="automatic-scale---cpu"></a><span data-ttu-id="8ba78-156">Автоматическое масштабирование: ЦП</span><span class="sxs-lookup"><span data-stu-id="8ba78-156">Automatic scale - CPU</span></span>
<span data-ttu-id="8ba78-157">Масштаб в этом режиме изменяется, если средний процент использования ЦП выходит за пределы определенных пороговых значений.</span><span class="sxs-lookup"><span data-stu-id="8ba78-157">This mode scales if the average percentage of CPU usage goes above or below specified thresholds.</span></span> <span data-ttu-id="8ba78-158">Когда это происходит, создаются или удаляются экземпляры роли.</span><span class="sxs-lookup"><span data-stu-id="8ba78-158">Role instances are created or deleted when this happens.</span></span>

1. <span data-ttu-id="8ba78-159">На [классическом портале Azure](https://manage.windowsazure.com/)щелкните **Облачные службы**, затем щелкните имя облачной службы, чтобы открыть панель мониторинга.</span><span class="sxs-lookup"><span data-stu-id="8ba78-159">In the [Azure classic portal](https://manage.windowsazure.com/), click **Cloud Services**, and then click the name of the cloud service to open the dashboard.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="8ba78-160">Если вы не видите облачную службу, измените **рабочую среду** на **промежуточную** или наоборот.</span><span class="sxs-lookup"><span data-stu-id="8ba78-160">If you don't see your cloud service, you may need to change from **Production** to **Staging** or vice versa.</span></span>

2. <span data-ttu-id="8ba78-161">Щелкните пункт **Масштаб**.</span><span class="sxs-lookup"><span data-stu-id="8ba78-161">Click **Scale**.</span></span>
3. <span data-ttu-id="8ba78-162">Выберите расписание, для которого нужно изменить параметры масштабирования.</span><span class="sxs-lookup"><span data-stu-id="8ba78-162">Select the schedule you want to change scaling options for.</span></span> <span data-ttu-id="8ba78-163">Если расписание не определено, используется значение по умолчанию — *Не настроено*.</span><span class="sxs-lookup"><span data-stu-id="8ba78-163">*No scheduled times* is the default if you have no schedules defined.</span></span>
4. <span data-ttu-id="8ba78-164">Найдите раздел **Масштабирование по метрике** и выберите параметр **ЦП**.</span><span class="sxs-lookup"><span data-stu-id="8ba78-164">Find the **Scale by metric** section and select **CPU**.</span></span>
5. <span data-ttu-id="8ba78-165">Теперь можно настраивать минимальный и максимальный диапазон экземпляров ролей, целевой процент использования ЦП (для увеличения масштаба в случае необходимости) и число экземпляров, на которое следует увеличивать или уменьшать масштаб.</span><span class="sxs-lookup"><span data-stu-id="8ba78-165">Now you can configure a minimum and maximum range of roles instances, the target CPU usage (to trigger a scale up), and how many instances to scale up and down by.</span></span>

![Масштабирование роли облачной службы в зависимости от нагрузки на ЦП][cpu_scale]

> [!TIP]
> <span data-ttu-id="8ba78-167">Увидев значок ![][tip_icon], наведите на него указатель мыши, и вы получите справку о том, что именно делает соответствующий параметр.</span><span class="sxs-lookup"><span data-stu-id="8ba78-167">Whenever you see ![][tip_icon] move your mouse to it and you can get help about what a specific setting does.</span></span>

## <a name="automatic-scale---queue"></a><span data-ttu-id="8ba78-168">Автоматическое масштабирование: очередь</span><span class="sxs-lookup"><span data-stu-id="8ba78-168">Automatic scale - Queue</span></span>
<span data-ttu-id="8ba78-169">В этом режиме автомасштабирование выполняется, если число сообщений в очереди поднимается выше или опускается ниже указанного порогового значения.</span><span class="sxs-lookup"><span data-stu-id="8ba78-169">This mode automatically scales if the number of messages in a queue goes above or below a specified threshold.</span></span> <span data-ttu-id="8ba78-170">Когда это происходит, создаются или удаляются экземпляры роли.</span><span class="sxs-lookup"><span data-stu-id="8ba78-170">Role instances are created or deleted when this happens.</span></span>

1. <span data-ttu-id="8ba78-171">На [классическом портале Azure](https://manage.windowsazure.com/)щелкните **Облачные службы**, затем щелкните имя облачной службы, чтобы открыть панель мониторинга.</span><span class="sxs-lookup"><span data-stu-id="8ba78-171">In the [Azure classic portal](https://manage.windowsazure.com/), click **Cloud Services**, and then click the name of the cloud service to open the dashboard.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="8ba78-172">Если вы не видите облачную службу, измените **рабочую среду** на **промежуточную** или наоборот.</span><span class="sxs-lookup"><span data-stu-id="8ba78-172">If you don't see your cloud service, you may need to change from **Production** to **Staging** or vice versa.</span></span>

2. <span data-ttu-id="8ba78-173">Щелкните пункт **Масштаб**.</span><span class="sxs-lookup"><span data-stu-id="8ba78-173">Click **Scale**.</span></span>
3. <span data-ttu-id="8ba78-174">Найдите раздел **Масштабирование по метрике** и выберите параметр **Очередь**.</span><span class="sxs-lookup"><span data-stu-id="8ba78-174">Find the **Scale by metric** section and select **QUEUE**.</span></span>
4. <span data-ttu-id="8ba78-175">Теперь можно настроить минимальный и максимальный диапазоны экземпляров ролей, очередь и число сообщений в очереди на обработку для каждого экземпляра, а также число экземпляров, на которое следует увеличивать или уменьшать масштаб.</span><span class="sxs-lookup"><span data-stu-id="8ba78-175">Now you can configure a minimum and maximum range of roles instances, the queue and number of queue messages to process for each instance, and how many instances to scale up and down by.</span></span>

![Масштабирование роли облачной службы в зависимости от очереди сообщений][queue_scale]

> [!TIP]
> <span data-ttu-id="8ba78-177">Увидев значок ![][tip_icon], наведите на него указатель мыши, и вы получите справку о том, что именно делает соответствующий параметр.</span><span class="sxs-lookup"><span data-stu-id="8ba78-177">Whenever you see ![][tip_icon] move your mouse to it and you can get help about what a specific setting does.</span></span>

## <a name="scale-linked-resources"></a><span data-ttu-id="8ba78-178">Масштабирование связанных ресурсов</span><span class="sxs-lookup"><span data-stu-id="8ba78-178">Scale linked resources</span></span>
<span data-ttu-id="8ba78-179">Часто при масштабировании роли выгодно масштабировать также и базу данных, используемую приложением.</span><span class="sxs-lookup"><span data-stu-id="8ba78-179">Often when you scale a role, it's beneficial to scale the database that the application is using also.</span></span> <span data-ttu-id="8ba78-180">Связав базу данных с облачной службой, вы сможете получить доступ к параметрам масштабирования для соответствующего ресурса, щелкнув соответствующую ссылку.</span><span class="sxs-lookup"><span data-stu-id="8ba78-180">If you link the database to the cloud service, you can access the scaling settings for that resource by clicking the appropriate link.</span></span>

1. <span data-ttu-id="8ba78-181">На [классическом портале Azure](https://manage.windowsazure.com/)щелкните **Облачные службы**, затем щелкните имя облачной службы, чтобы открыть панель мониторинга.</span><span class="sxs-lookup"><span data-stu-id="8ba78-181">In the [Azure classic portal](https://manage.windowsazure.com/), click **Cloud Services**, and then click the name of the cloud service to open the dashboard.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="8ba78-182">Если вы не видите облачную службу, измените **рабочую среду** на **промежуточную** или наоборот.</span><span class="sxs-lookup"><span data-stu-id="8ba78-182">If you don't see your cloud service, you may need to change from **Production** to **Staging** or vice versa.</span></span>

2. <span data-ttu-id="8ba78-183">Щелкните пункт **Масштаб**.</span><span class="sxs-lookup"><span data-stu-id="8ba78-183">Click **Scale**.</span></span>
3. <span data-ttu-id="8ba78-184">Найдите раздел **Связанные ресурсы** и щелкните **Управление масштабированием для этой базы данных**.</span><span class="sxs-lookup"><span data-stu-id="8ba78-184">Find the **linked resources** section and click **Manage scale for this database**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="8ba78-185">Если вы не видите раздел **Связанные ресурсы** , возможно, что таких ресурсов у вас нет.</span><span class="sxs-lookup"><span data-stu-id="8ba78-185">If you don't see a **linked resources** section, you probably do not have any linked resources.</span></span>

![][linked_resource]

[manual_scale]: ./media/cloud-services-how-to-scale/manual-scale.png
[queue_scale]: ./media/cloud-services-how-to-scale/queue-scale.png
[cpu_scale]: ./media/cloud-services-how-to-scale/cpu-scale.png
[tip_icon]: ./media/cloud-services-how-to-scale/tip.png
[scale_schedules]: ./media/cloud-services-how-to-scale/schedules.png
[scale_popup]: ./media/cloud-services-how-to-scale/schedules-dialog.png
[linked_resource]: ./media/cloud-services-how-to-scale/linked-resources.png
