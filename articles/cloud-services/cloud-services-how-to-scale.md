---
title: "aaaAuto масштабирования облачной службы в классическом портале hello | Документы Microsoft"
description: "(классические) Узнайте, как toouse hello классического портала tooconfigure автоматического масштабирования правила для облака службы веб-роли или рабочей роли в Azure."
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
ms.openlocfilehash: ddb5816d4d22192c6d2f51d7508e390779742078
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-auto-scaling-for-a-cloud-service-in-hello-classic-portal"></a><span data-ttu-id="39d2e-103">Как tooconfigure автоматическое масштабирование для облачной службы в классическом портале hello</span><span class="sxs-lookup"><span data-stu-id="39d2e-103">How tooconfigure auto scaling for a Cloud Service in hello classic portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="39d2e-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="39d2e-104">Azure portal</span></span>](cloud-services-how-to-scale-portal.md)
> * [<span data-ttu-id="39d2e-105">классическом портале Azure</span><span class="sxs-lookup"><span data-stu-id="39d2e-105">Azure classic portal</span></span>](cloud-services-how-to-scale.md)

<span data-ttu-id="39d2e-106">На странице приветствия шкалы hello классический портал Azure можно настроить параметры автоматического масштабирования для веб-роли или рабочей роли.</span><span class="sxs-lookup"><span data-stu-id="39d2e-106">On hello Scale page of hello Azure classic portal, you can configure automatic scale settings for your web role or worker role.</span></span> <span data-ttu-id="39d2e-107">Кроме того, можно настроить ручное масштабирование, а не автомасштабирование на основе правил.</span><span class="sxs-lookup"><span data-stu-id="39d2e-107">Alternatively, you can configure manual scaling instead of rules-based automatic scaling.</span></span>

> [!NOTE]
> <span data-ttu-id="39d2e-108">Эта статья посвящена веб-ролям и рабочим ролям облачной службы.</span><span class="sxs-lookup"><span data-stu-id="39d2e-108">This article focuses on Cloud Service web and worker roles.</span></span> <span data-ttu-id="39d2e-109">Виртуальные машины (классические), создаваемые напрямую, размещаются в облачной службе.</span><span class="sxs-lookup"><span data-stu-id="39d2e-109">When you create a virtual machine (classic) directly, it is hosted in a cloud service.</span></span> <span data-ttu-id="39d2e-110">Некоторые из этих сведений применяет toothese типов виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="39d2e-110">Some of this information applies toothese types of virtual machines.</span></span> <span data-ttu-id="39d2e-111">Масштабирование наборе доступности виртуальных машин, просто завершает их включение и отключение на основе правил масштабирования hello, настроенные.</span><span class="sxs-lookup"><span data-stu-id="39d2e-111">Scaling an availability set of virtual machines is just shutting them on and off based on hello scale rules you configure.</span></span> <span data-ttu-id="39d2e-112">Дополнительные сведения о виртуальных машинах и группах доступности см. в разделе [hello Управление доступностью виртуальных машин](../virtual-machines/windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="39d2e-112">For more information about Virtual Machines and availability sets, see [Manage hello Availability of Virtual Machines](../virtual-machines/windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span></span>

<span data-ttu-id="39d2e-113">Рекомендуется использовать следующую информацию, прежде чем настраивать масштабирование приложения hello.</span><span class="sxs-lookup"><span data-stu-id="39d2e-113">You should consider hello following information before you configure scaling for your application:</span></span>

* <span data-ttu-id="39d2e-114">Масштабирование зависит от использования ядер.</span><span class="sxs-lookup"><span data-stu-id="39d2e-114">Scaling is affected by core usage.</span></span>

    <span data-ttu-id="39d2e-115">Более крупные экземпляры ролей задействуют больше ядер.</span><span class="sxs-lookup"><span data-stu-id="39d2e-115">Larger role instances use more cores.</span></span> <span data-ttu-id="39d2e-116">Можно масштабировать приложения только в течение ограниченного hello ядер для подписки.</span><span class="sxs-lookup"><span data-stu-id="39d2e-116">You can scale an application only within hello limit of cores for your subscription.</span></span> <span data-ttu-id="39d2e-117">Предположим, что ваша подписка имеет ограничение в 20 ядер.</span><span class="sxs-lookup"><span data-stu-id="39d2e-117">For example, say your subscription has a limit of 20 cores.</span></span> <span data-ttu-id="39d2e-118">При запуске приложения с двух средних облачные службы (всего 4 ядра) можно только увеличивать масштаб другие развертывания облачной службы в подписке, hello оставшиеся 16 ядер.</span><span class="sxs-lookup"><span data-stu-id="39d2e-118">If you run an application with two medium-sized cloud services (a total of 4 cores), you can only scale up other cloud service deployments in your subscription by hello remaining 16 cores.</span></span> <span data-ttu-id="39d2e-119">Дополнительные сведения о размерах см. в статье [Размеры для облачных служб](cloud-services-sizes-specs.md).</span><span class="sxs-lookup"><span data-stu-id="39d2e-119">For more information about sizes, see [Cloud Service Sizes](cloud-services-sizes-specs.md).</span></span>

* <span data-ttu-id="39d2e-120">Прежде чем приступить к масштабированию приложения на основе порогового значения сообщений, необходимо создать очередь и связать ее с ролью.</span><span class="sxs-lookup"><span data-stu-id="39d2e-120">You must create a queue and associate it with a role before you can scale an application based on a message threshold.</span></span> <span data-ttu-id="39d2e-121">Дополнительные сведения см. в разделе [как toouse hello службы хранилища очередей](../storage/queues/storage-dotnet-how-to-use-queues.md).</span><span class="sxs-lookup"><span data-stu-id="39d2e-121">For more information, see [How toouse hello Queue Storage Service](../storage/queues/storage-dotnet-how-to-use-queues.md).</span></span>

* <span data-ttu-id="39d2e-122">Можно масштабировать ресурсы, связанные tooyour облачной службы.</span><span class="sxs-lookup"><span data-stu-id="39d2e-122">You can scale resources that are linked tooyour cloud service.</span></span> <span data-ttu-id="39d2e-123">Дополнительные сведения о связывании ресурсов см. в разделе [как: связать облачной службы tooa ресурсов](cloud-services-how-to-manage.md#how-to-link-a-resource-to-a-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="39d2e-123">For more information about linking resources, see [How to: Link a resource tooa cloud service](cloud-services-how-to-manage.md#how-to-link-a-resource-to-a-cloud-service).</span></span>

* <span data-ttu-id="39d2e-124">tooenable высокий уровень доступности приложения, следует убедиться, развертывается с двумя или более экземпляров роли.</span><span class="sxs-lookup"><span data-stu-id="39d2e-124">tooenable high availability of your application, you should ensure that it is deployed with two or more role instances.</span></span> <span data-ttu-id="39d2e-125">Дополнительные сведения см. в разделе [Соглашения об уровне обслуживания](https://azure.microsoft.com/support/legal/sla/).</span><span class="sxs-lookup"><span data-stu-id="39d2e-125">For more information, see [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).</span></span>

## <a name="schedule-scaling"></a><span data-ttu-id="39d2e-126">Планирование масштабирования</span><span class="sxs-lookup"><span data-stu-id="39d2e-126">Schedule scaling</span></span>
<span data-ttu-id="39d2e-127">По умолчанию все роли следуют установленному расписанию.</span><span class="sxs-lookup"><span data-stu-id="39d2e-127">By default, all roles do not follow a specific schedule.</span></span> <span data-ttu-id="39d2e-128">Таким образом любые изменения параметров, применяются tooall время и все дни в течение года hello.</span><span class="sxs-lookup"><span data-stu-id="39d2e-128">Therefore, any settings changed apply tooall times and all days throughout hello year.</span></span> <span data-ttu-id="39d2e-129">Если вы хотите, вы можете настроить ручного или автоматического масштабирования для одного из следующих режимов hello:</span><span class="sxs-lookup"><span data-stu-id="39d2e-129">If you want, you can setup manual or automatic scaling for one of hello following modes:</span></span>

* <span data-ttu-id="39d2e-130">дни недели;</span><span class="sxs-lookup"><span data-stu-id="39d2e-130">Weekdays</span></span>
* <span data-ttu-id="39d2e-131">выходные дни;</span><span class="sxs-lookup"><span data-stu-id="39d2e-131">Weekends</span></span>
* <span data-ttu-id="39d2e-132">ночное время будних дней;</span><span class="sxs-lookup"><span data-stu-id="39d2e-132">Week nights</span></span>
* <span data-ttu-id="39d2e-133">утреннее время будних дней;</span><span class="sxs-lookup"><span data-stu-id="39d2e-133">Week mornings</span></span>
* <span data-ttu-id="39d2e-134">определенные даты;</span><span class="sxs-lookup"><span data-stu-id="39d2e-134">Specific dates</span></span>
* <span data-ttu-id="39d2e-135">определенные диапазоны дат.</span><span class="sxs-lookup"><span data-stu-id="39d2e-135">Specific date ranges</span></span>

<span data-ttu-id="39d2e-136">Hello расписание настраивается в hello [классический портал Azure](https://manage.windowsazure.com/) на hello</span><span class="sxs-lookup"><span data-stu-id="39d2e-136">hello schedule setting is configured in hello [Azure classic portal](https://manage.windowsazure.com/) on hello</span></span>  
<span data-ttu-id="39d2e-137">**Облачные службы** > **\[Ваша облачная служба\]** > **Масштабирование** > **\[Рабочая или промежуточная среда\]**.</span><span class="sxs-lookup"><span data-stu-id="39d2e-137">**Cloud Services** > **\[Your cloud service\]** > **Scale** > **\[Production or Staging\]** page.</span></span>

<span data-ttu-id="39d2e-138">Нажмите кнопку hello **Настройка планируемого времени** кнопки для каждой роли необходимо toochange.</span><span class="sxs-lookup"><span data-stu-id="39d2e-138">Click hello **set up schedule times** button for each role you want toochange.</span></span>

![Автомасштабирование облачной службы по расписанию][scale_schedules]

## <a name="manual-scale"></a><span data-ttu-id="39d2e-140">Ручное масштабирование</span><span class="sxs-lookup"><span data-stu-id="39d2e-140">Manual scale</span></span>
<span data-ttu-id="39d2e-141">На hello **шкалы** страницы, можно вручную увеличить или уменьшить hello число выполняющихся экземпляров в облачной службе.</span><span class="sxs-lookup"><span data-stu-id="39d2e-141">On hello **Scale** page, you can manually increase or decrease hello number of running instances in a cloud service.</span></span> <span data-ttu-id="39d2e-142">Этот параметр настраивается для каждого расписания, созданные или tooall время, если вы не создали расписание.</span><span class="sxs-lookup"><span data-stu-id="39d2e-142">This setting is configured for each schedule you've created or tooall time if you have not created a schedule.</span></span>

1. <span data-ttu-id="39d2e-143">В hello [классический портал Azure](https://manage.windowsazure.com/), нажмите кнопку **облачные службы**и щелкните имя hello панель мониторинга hello tooopen hello облачной службы.</span><span class="sxs-lookup"><span data-stu-id="39d2e-143">In hello [Azure classic portal](https://manage.windowsazure.com/), click **Cloud Services**, and then click hello name of hello cloud service tooopen hello dashboard.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="39d2e-144">Если вы не видите облачной службы, может потребоваться toochange из **рабочей** слишком**промежуточной** или наоборот.</span><span class="sxs-lookup"><span data-stu-id="39d2e-144">If you don't see your cloud service, you may need toochange from **Production** too**Staging** or vice versa.</span></span>

2. <span data-ttu-id="39d2e-145">Щелкните пункт **Масштаб**.</span><span class="sxs-lookup"><span data-stu-id="39d2e-145">Click **Scale**.</span></span>
3. <span data-ttu-id="39d2e-146">Выберите расписание hello требуется toochange параметры для масштабирования.</span><span class="sxs-lookup"><span data-stu-id="39d2e-146">Select hello schedule you want toochange scaling options for.</span></span> <span data-ttu-id="39d2e-147">*Не запланированное время* — по умолчанию hello в том случае, если расписания не определены.</span><span class="sxs-lookup"><span data-stu-id="39d2e-147">*No scheduled times* is hello default if you have no schedules defined.</span></span>
4. <span data-ttu-id="39d2e-148">Найти hello **масштабирование по метрике** , выберите **NONE**.</span><span class="sxs-lookup"><span data-stu-id="39d2e-148">Find hello **Scale by metric** section and select **NONE**.</span></span> <span data-ttu-id="39d2e-149">Этот параметр является hello по умолчанию для всех ролей.</span><span class="sxs-lookup"><span data-stu-id="39d2e-149">This setting is hello default for all roles.</span></span>
5. <span data-ttu-id="39d2e-150">Каждая роль в облачной службе hello имеет ползунок для изменения номера hello объекта toouse экземпляров.</span><span class="sxs-lookup"><span data-stu-id="39d2e-150">Each role in hello cloud service has a slider for changing hello number of instances toouse.</span></span>
   
    ![Ручное масштабирование роли облачной службы][manual_scale]
   
    <span data-ttu-id="39d2e-152">Если требуется несколько экземпляров, может потребоваться toochange hello [облачные службы размер виртуальной машины](cloud-services-sizes-specs.md).</span><span class="sxs-lookup"><span data-stu-id="39d2e-152">If you need more instances, you may need toochange hello [cloud service virtual machine size](cloud-services-sizes-specs.md).</span></span>
6. <span data-ttu-id="39d2e-153">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="39d2e-153">Click **Save**.</span></span>  
   <span data-ttu-id="39d2e-154">Экземпляры роли добавляются и удаляются в зависимости от вашего выбора.</span><span class="sxs-lookup"><span data-stu-id="39d2e-154">Role instances are added or removed based on your selections.</span></span>

> [!TIP]
> <span data-ttu-id="39d2e-155">Каждый раз, когда вы видите ![][tip_icon] перемещение вашей мыши tooit и получить справку о какой определенный параметр.</span><span class="sxs-lookup"><span data-stu-id="39d2e-155">Whenever you see ![][tip_icon] move your mouse tooit and you can get help about what a specific setting does.</span></span>

## <a name="automatic-scale---cpu"></a><span data-ttu-id="39d2e-156">Автоматическое масштабирование: ЦП</span><span class="sxs-lookup"><span data-stu-id="39d2e-156">Automatic scale - CPU</span></span>
<span data-ttu-id="39d2e-157">В этом режиме масштабируется, если hello средний процент использования ЦП выходит за пределы выше или заданные пороговые значения.</span><span class="sxs-lookup"><span data-stu-id="39d2e-157">This mode scales if hello average percentage of CPU usage goes above or below specified thresholds.</span></span> <span data-ttu-id="39d2e-158">Когда это происходит, создаются или удаляются экземпляры роли.</span><span class="sxs-lookup"><span data-stu-id="39d2e-158">Role instances are created or deleted when this happens.</span></span>

1. <span data-ttu-id="39d2e-159">В hello [классический портал Azure](https://manage.windowsazure.com/), нажмите кнопку **облачные службы**и щелкните имя hello панель мониторинга hello tooopen hello облачной службы.</span><span class="sxs-lookup"><span data-stu-id="39d2e-159">In hello [Azure classic portal](https://manage.windowsazure.com/), click **Cloud Services**, and then click hello name of hello cloud service tooopen hello dashboard.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="39d2e-160">Если вы не видите облачной службы, может потребоваться toochange из **рабочей** слишком**промежуточной** или наоборот.</span><span class="sxs-lookup"><span data-stu-id="39d2e-160">If you don't see your cloud service, you may need toochange from **Production** too**Staging** or vice versa.</span></span>

2. <span data-ttu-id="39d2e-161">Щелкните пункт **Масштаб**.</span><span class="sxs-lookup"><span data-stu-id="39d2e-161">Click **Scale**.</span></span>
3. <span data-ttu-id="39d2e-162">Выберите расписание hello требуется toochange параметры для масштабирования.</span><span class="sxs-lookup"><span data-stu-id="39d2e-162">Select hello schedule you want toochange scaling options for.</span></span> <span data-ttu-id="39d2e-163">*Не запланированное время* — по умолчанию hello в том случае, если расписания не определены.</span><span class="sxs-lookup"><span data-stu-id="39d2e-163">*No scheduled times* is hello default if you have no schedules defined.</span></span>
4. <span data-ttu-id="39d2e-164">Найти hello **масштабирование по метрике** , выберите **ЦП**.</span><span class="sxs-lookup"><span data-stu-id="39d2e-164">Find hello **Scale by metric** section and select **CPU**.</span></span>
5. <span data-ttu-id="39d2e-165">Теперь можно настроить минимального и максимального диапазона экземпляры ролей, использование ЦП hello (tootrigger a масштабирования вверх) и число экземпляров tooscale вверх и вниз по.</span><span class="sxs-lookup"><span data-stu-id="39d2e-165">Now you can configure a minimum and maximum range of roles instances, hello target CPU usage (tootrigger a scale up), and how many instances tooscale up and down by.</span></span>

![Масштабирование роли облачной службы в зависимости от нагрузки на ЦП][cpu_scale]

> [!TIP]
> <span data-ttu-id="39d2e-167">Каждый раз, когда вы видите ![][tip_icon] перемещение вашей мыши tooit и получить справку о какой определенный параметр.</span><span class="sxs-lookup"><span data-stu-id="39d2e-167">Whenever you see ![][tip_icon] move your mouse tooit and you can get help about what a specific setting does.</span></span>

## <a name="automatic-scale---queue"></a><span data-ttu-id="39d2e-168">Автоматическое масштабирование: очередь</span><span class="sxs-lookup"><span data-stu-id="39d2e-168">Automatic scale - Queue</span></span>
<span data-ttu-id="39d2e-169">Этот режим автоматически масштабируется, если hello количество сообщений в очереди становится выше или ниже указанного порогового значения.</span><span class="sxs-lookup"><span data-stu-id="39d2e-169">This mode automatically scales if hello number of messages in a queue goes above or below a specified threshold.</span></span> <span data-ttu-id="39d2e-170">Когда это происходит, создаются или удаляются экземпляры роли.</span><span class="sxs-lookup"><span data-stu-id="39d2e-170">Role instances are created or deleted when this happens.</span></span>

1. <span data-ttu-id="39d2e-171">В hello [классический портал Azure](https://manage.windowsazure.com/), нажмите кнопку **облачные службы**и щелкните имя hello панель мониторинга hello tooopen hello облачной службы.</span><span class="sxs-lookup"><span data-stu-id="39d2e-171">In hello [Azure classic portal](https://manage.windowsazure.com/), click **Cloud Services**, and then click hello name of hello cloud service tooopen hello dashboard.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="39d2e-172">Если вы не видите облачной службы, может потребоваться toochange из **рабочей** слишком**промежуточной** или наоборот.</span><span class="sxs-lookup"><span data-stu-id="39d2e-172">If you don't see your cloud service, you may need toochange from **Production** too**Staging** or vice versa.</span></span>

2. <span data-ttu-id="39d2e-173">Щелкните пункт **Масштаб**.</span><span class="sxs-lookup"><span data-stu-id="39d2e-173">Click **Scale**.</span></span>
3. <span data-ttu-id="39d2e-174">Найти hello **масштабирование по метрике** , выберите **ОЧЕРЕДИ**.</span><span class="sxs-lookup"><span data-stu-id="39d2e-174">Find hello **Scale by metric** section and select **QUEUE**.</span></span>
4. <span data-ttu-id="39d2e-175">Теперь можно настроить минимального и максимального диапазона экземпляров ролей, очереди hello и количество tooprocess очереди сообщений для каждого экземпляра и сколько экземпляров tooscale вверх и вниз по.</span><span class="sxs-lookup"><span data-stu-id="39d2e-175">Now you can configure a minimum and maximum range of roles instances, hello queue and number of queue messages tooprocess for each instance, and how many instances tooscale up and down by.</span></span>

![Масштабирование роли облачной службы в зависимости от очереди сообщений][queue_scale]

> [!TIP]
> <span data-ttu-id="39d2e-177">Каждый раз, когда вы видите ![][tip_icon] перемещение вашей мыши tooit и получить справку о какой определенный параметр.</span><span class="sxs-lookup"><span data-stu-id="39d2e-177">Whenever you see ![][tip_icon] move your mouse tooit and you can get help about what a specific setting does.</span></span>

## <a name="scale-linked-resources"></a><span data-ttu-id="39d2e-178">Масштабирование связанных ресурсов</span><span class="sxs-lookup"><span data-stu-id="39d2e-178">Scale linked resources</span></span>
<span data-ttu-id="39d2e-179">Часто при масштабировании роль это hello полезным tooscale базы данных, которая также использует приложение hello.</span><span class="sxs-lookup"><span data-stu-id="39d2e-179">Often when you scale a role, it's beneficial tooscale hello database that hello application is using also.</span></span> <span data-ttu-id="39d2e-180">При компоновке hello базы данных toohello облачной службы, можно получить доступ к hello масштабирование параметры для этого ресурса, щелкнув соответствующую ссылку hello.</span><span class="sxs-lookup"><span data-stu-id="39d2e-180">If you link hello database toohello cloud service, you can access hello scaling settings for that resource by clicking hello appropriate link.</span></span>

1. <span data-ttu-id="39d2e-181">В hello [классический портал Azure](https://manage.windowsazure.com/), нажмите кнопку **облачные службы**и щелкните имя hello панель мониторинга hello tooopen hello облачной службы.</span><span class="sxs-lookup"><span data-stu-id="39d2e-181">In hello [Azure classic portal](https://manage.windowsazure.com/), click **Cloud Services**, and then click hello name of hello cloud service tooopen hello dashboard.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="39d2e-182">Если вы не видите облачной службы, может потребоваться toochange из **рабочей** слишком**промежуточной** или наоборот.</span><span class="sxs-lookup"><span data-stu-id="39d2e-182">If you don't see your cloud service, you may need toochange from **Production** too**Staging** or vice versa.</span></span>

2. <span data-ttu-id="39d2e-183">Щелкните пункт **Масштаб**.</span><span class="sxs-lookup"><span data-stu-id="39d2e-183">Click **Scale**.</span></span>
3. <span data-ttu-id="39d2e-184">Найти hello **связанные ресурсы** и нажмите кнопку **управление масштабированием для этой базы данных**.</span><span class="sxs-lookup"><span data-stu-id="39d2e-184">Find hello **linked resources** section and click **Manage scale for this database**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="39d2e-185">Если вы не видите раздел **Связанные ресурсы** , возможно, что таких ресурсов у вас нет.</span><span class="sxs-lookup"><span data-stu-id="39d2e-185">If you don't see a **linked resources** section, you probably do not have any linked resources.</span></span>

![][linked_resource]

[manual_scale]: ./media/cloud-services-how-to-scale/manual-scale.png
[queue_scale]: ./media/cloud-services-how-to-scale/queue-scale.png
[cpu_scale]: ./media/cloud-services-how-to-scale/cpu-scale.png
[tip_icon]: ./media/cloud-services-how-to-scale/tip.png
[scale_schedules]: ./media/cloud-services-how-to-scale/schedules.png
[scale_popup]: ./media/cloud-services-how-to-scale/schedules-dialog.png
[linked_resource]: ./media/cloud-services-how-to-scale/linked-resources.png
