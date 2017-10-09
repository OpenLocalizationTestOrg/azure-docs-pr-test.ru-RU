---
title: "рабочие нагрузки пакетной службы Azure aaaRun на виртуальных машинах экономичное низким приоритетом (Предварительная версия) | Документы Microsoft"
description: "Узнайте, как виртуальные машины tooreduce tooprovision низкоприоритетных hello стоимости рабочих нагрузок пакетной службы Azure."
services: batch
author: mscurrell
manager: timlt
ms.assetid: dc6ba151-1718-468a-b455-2da549225ab2
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.workload: na
ms.date: 07/21/2017
ms.author: markscu
ms.openlocfilehash: 91a5e89a819d05583e6b146932d925e217b4be4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-low-priority-vms-with-batch-preview"></a><span data-ttu-id="d0ac7-103">Использование низкоприоритетных виртуальных машин в пакетной службе (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="d0ac7-103">Use low-priority VMs with Batch (Preview)</span></span>

<span data-ttu-id="d0ac7-104">Пакетная служба Azure предлагает стоимость hello tooreduce low приоритету виртуальных машин (ВМ) пакета рабочих нагрузок.</span><span class="sxs-lookup"><span data-stu-id="d0ac7-104">Azure Batch offers low-priorty virtual machines (VMs) tooreduce hello cost of Batch workloads.</span></span> <span data-ttu-id="d0ac7-105">Виртуальные машины с низким приоритетом позволяют использовать новые типы рабочих нагрузок пакетной службы, предоставляя большой объем вычислительных ресурсов по доступной цене.</span><span class="sxs-lookup"><span data-stu-id="d0ac7-105">Low-priority VMs make new types of Batch workloads possible by providing a large amount of compute power that is also economical.</span></span>

<span data-ttu-id="d0ac7-106">Низкоприоритетные виртуальные машины используют избыточные ресурсы в Azure.</span><span class="sxs-lookup"><span data-stu-id="d0ac7-106">Low-priority VMs take advantage of surplus capacity in Azure.</span></span> <span data-ttu-id="d0ac7-107">При указании низкоприоритетных виртуальных машин в пулах пакетная служба Azure может автоматически использовать этот избыток при его наличии.</span><span class="sxs-lookup"><span data-stu-id="d0ac7-107">When you specify low-priority VMs in your pools, Azure Batch can automatically use this surplus when available.</span></span>

<span data-ttu-id="d0ac7-108">Hello платой за использование виртуальных машин с низким приоритетом —, когда нет излишком доступен в Azure может возможность прерывания этих виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="d0ac7-108">hello tradeoff for using low-priority VMs is that those VMs may be preempted when no surplus capacity is available in Azure.</span></span> <span data-ttu-id="d0ac7-109">Именно поэтому низкоприоритетные виртуальные машины лучше всего подходят для определенных типов рабочих нагрузок.</span><span class="sxs-lookup"><span data-stu-id="d0ac7-109">For this reason, low-priority VMs are most suitable for certain types of workloads.</span></span> <span data-ttu-id="d0ac7-110">Используйте виртуальные машины с низким приоритетом для пакета и асинхронной обработки рабочих нагрузок, где время выполнения задания hello гибок и hello работа распределяется между много виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="d0ac7-110">Use low-priority VMs for batch and asynchronous processing workloads where hello job completion time is flexible and hello work is distributed across many VMs.</span></span>

<span data-ttu-id="d0ac7-111">Низкоприоритетные виртуальные машины значительно дешевле выделенных аналогов.</span><span class="sxs-lookup"><span data-stu-id="d0ac7-111">Low-priority VMs are significantly less expensive than dedicated VMs.</span></span> <span data-ttu-id="d0ac7-112">Сведения о ценах на пакетную службу см. [здесь](https://azure.microsoft.com/pricing/details/batch/).</span><span class="sxs-lookup"><span data-stu-id="d0ac7-112">For pricing details, see [Batch Pricing](https://azure.microsoft.com/pricing/details/batch/).</span></span>

<span data-ttu-id="d0ac7-113">Дополнительные сведения по виртуальные машины с низким приоритетом, в разделе hello объявлении в блоге: [пакета вычислений в малую долю цена hello](https://azure.microsoft.com/blog/announcing-public-preview-of-azure-batch-low-priority-vms/).</span><span class="sxs-lookup"><span data-stu-id="d0ac7-113">For an additional discussion of low-priority VMs, see hello blog post announcement: [Batch computing at a fraction of hello price](https://azure.microsoft.com/blog/announcing-public-preview-of-azure-batch-low-priority-vms/).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d0ac7-114">Сейчас низкоприоритетные виртуальные машины доступны в предварительной версии для рабочих нагрузок, выполняющихся в пакетной службе.</span><span class="sxs-lookup"><span data-stu-id="d0ac7-114">Low-priority VMs are currently in preview, and are available only for workloads running in Batch.</span></span> 
>
>

## <a name="use-cases-for-low-priority-vms"></a><span data-ttu-id="d0ac7-115">Варианты использования низкоприоритетных виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="d0ac7-115">Use cases for low-priority VMs</span></span>

<span data-ttu-id="d0ac7-116">Имея hello характеристики виртуальные машины с низким приоритетом, какие рабочие нагрузки можно и их нельзя использовать?</span><span class="sxs-lookup"><span data-stu-id="d0ac7-116">Given hello characteristics of low-priority VMs, what workloads can and cannot use them?</span></span> <span data-ttu-id="d0ac7-117">Как правило, это рабочие нагрузки пакетной обработки, так как задания разбиваются на несколько параллельных задач или развертываются и распределяются по нескольким виртуальным машинам.</span><span class="sxs-lookup"><span data-stu-id="d0ac7-117">In general, batch processing workloads are a good fit, as jobs are broken into many parallel tasks or there are many jobs that are scaled out and distributed across many VMs.</span></span>

-   <span data-ttu-id="d0ac7-118">Использование toomaximize излишком в Azure, подходящий заданий можно масштабировать.</span><span class="sxs-lookup"><span data-stu-id="d0ac7-118">toomaximize use of surplus capacity in Azure, suitable jobs can scale out.</span></span>

-   <span data-ttu-id="d0ac7-119">Иногда виртуальные машины могут быть недоступны или будет невозможно заместить, который приведет к ограниченной емкости для задания и может вызвать прерывание tootask и повторов.</span><span class="sxs-lookup"><span data-stu-id="d0ac7-119">Occasionally VMs may not be available or will be preempted, which will result in reduced capacity for jobs and may lead tootask interruption and reruns.</span></span> <span data-ttu-id="d0ac7-120">Задания, поэтому должно быть гибкие hello времени, которые они могут предпринять toorun.</span><span class="sxs-lookup"><span data-stu-id="d0ac7-120">Jobs must therefore be flexible in hello time they can take toorun.</span></span>

-   <span data-ttu-id="d0ac7-121">Прерывание заданий с более продолжительными задачами может привести к более серьезным последствиям.</span><span class="sxs-lookup"><span data-stu-id="d0ac7-121">Jobs with longer tasks may be impacted more if interrupted.</span></span> <span data-ttu-id="d0ac7-122">Если длительные задачи реализуют выполняется toosave контрольные точки, как они выполняются, то влияние прерывания будет гораздо меньше.</span><span class="sxs-lookup"><span data-stu-id="d0ac7-122">If long-running tasks implement checkpointing toosave progress as they execute, then the impact of interruption would be far less.</span></span> <span data-ttu-id="d0ac7-123">Задачи с более короткий интервал выполнения лучше всего обычно toowork с низким приоритетом виртуальные машины как влияние hello прерывания гораздо меньше.</span><span class="sxs-lookup"><span data-stu-id="d0ac7-123">Tasks with shorter execution times tend toowork best with low-priority VMs as hello impact of interruption is far less.</span></span>

-   <span data-ttu-id="d0ac7-124">Длительные заданий MPI, использующих несколько виртуальных машин не подходит toouse низкоприоритетных виртуальных машинах с одной виртуальной Машины внеочередного выполнения будет все наличие toobe снова запустите задание toohello скорее всего, руководитель.</span><span class="sxs-lookup"><span data-stu-id="d0ac7-124">Long-running MPI jobs that utilize multiple VMs are not well suited toouse low-priority VMs as one preempted VM will likely lead toohello whole job having toobe run again.</span></span>

<span data-ttu-id="d0ac7-125">Некоторые примеры пакетной обработки используйте toouse хорошо подходит случаев являются виртуальные машины с низким приоритетом.</span><span class="sxs-lookup"><span data-stu-id="d0ac7-125">Some examples of batch processing use cases well suited toouse low-priority VMs are:</span></span>

-   <span data-ttu-id="d0ac7-126">**Разработка и тестирование.** При разработке крупномасштабных решений, в частности, можно существенно сэкономить средства.</span><span class="sxs-lookup"><span data-stu-id="d0ac7-126">**Development and testing**: In particular, if large-scale solutions are being developed significant savings can be realized.</span></span> <span data-ttu-id="d0ac7-127">Преимущества доступны для всех видов тестирования, но лучше всего подходит крупномасштабное нагрузочное тестирование и тестирование регрессии.</span><span class="sxs-lookup"><span data-stu-id="d0ac7-127">All types of testing can benefit, but large-scale load testing and regression testing are great uses.</span></span>

-   <span data-ttu-id="d0ac7-128">**Добавление емкости по требованию**: виртуальные машины с низким приоритетом можно использовать в дополнение regular выделенных виртуальных машин — если она доступна, масштабировать и поэтому быстрее выполнить более низкую стоимость заданий; при недоступна, hello базового плана выделенных виртуальных машин доступны.</span><span class="sxs-lookup"><span data-stu-id="d0ac7-128">**Supplementing on-demand capacity**: Low-priority VMs can be used to supplement regular dedicated VMs - when available, jobs can scale and therefore complete quicker for lower cost; when not available, hello baseline of dedicated VMs are available.</span></span>

-   <span data-ttu-id="d0ac7-129">**Время выполнения задания гибкие**: если задания таймера hello гибкость имеют toocomplete, а затем вероятностью падения емкости можно допустимое; тем не менее, с hello добавления задания низкого приоритета виртуальные машины будут часто выполняются быстрее и более низкую стоимость.</span><span class="sxs-lookup"><span data-stu-id="d0ac7-129">**Flexible job execution time**: If there is flexibility in hello time jobs have toocomplete, then potential drops in capacity can be tolerated; however, with hello addition of low-priority VMs jobs will frequently run faster and for a lower cost.</span></span>

<span data-ttu-id="d0ac7-130">Пулы пакета может быть настроенный toouse времени выполнения задания низкого приоритета виртуальных машин несколькими способами в зависимости от hello гибкость в:</span><span class="sxs-lookup"><span data-stu-id="d0ac7-130">Batch pools can be configured toouse low-priority VMs in a few ways, depending on hello flexibility in job execution time:</span></span>

-   <span data-ttu-id="d0ac7-131">Виртуальные машины с низким приоритетом можно использовать только в пуле. При этом пакетная служба будет просто восстанавливать замещенные ресурсы, когда они станут доступными.</span><span class="sxs-lookup"><span data-stu-id="d0ac7-131">Low-priority VMs can solely be used in a pool and Batch will simply recover any preempted capacity when available.</span></span> <span data-ttu-id="d0ac7-132">Это hello дешевые способом tooexecute заданий, которые используются только низкого приоритета виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="d0ac7-132">This is hello cheapest way tooexecute jobs as only low-priority VMs are used.</span></span>

-   <span data-ttu-id="d0ac7-133">Низкоприоритетные виртуальные машины можно использовать в сочетании с фиксированными базовыми выделенными виртуальными машинами.</span><span class="sxs-lookup"><span data-stu-id="d0ac7-133">Low-priority VMs can be used in conjunction with a fixed baseline of dedicated VMs.</span></span> <span data-ttu-id="d0ac7-134">Hello фиксированное число выделенных виртуальных машин гарантирует, что имеется всегда некоторые tookeep емкости хода работ.</span><span class="sxs-lookup"><span data-stu-id="d0ac7-134">hello fixed number of dedicated VMs ensures there is always some capacity tookeep a job progressing.</span></span>

-   <span data-ttu-id="d0ac7-135">Может существовать динамического набора виртуальных машин выделенным и низкого приоритета дешевле ВМ низкого приоритета используются только при наличии, но hello дорогими full выделенных виртуальных машин масштабируются при необходимости tookeep минимальный объем емкости доступных tookeep hello заданий выполняет.</span><span class="sxs-lookup"><span data-stu-id="d0ac7-135">There can be dynamic mix of dedicated and low-priority VMs, so that the cheaper low-priority VMs are solely used when available, but hello full-priced dedicated VMs are scaled up when required, tookeep a minimum amount of capacity available tookeep hello jobs progressing.</span></span>

## <a name="batch-support-for-low-priority-vms"></a><span data-ttu-id="d0ac7-136">Поддержка пакетной службы для виртуальных машин с низким приоритетом</span><span class="sxs-lookup"><span data-stu-id="d0ac7-136">Batch support for low-priority VMs</span></span>

<span data-ttu-id="d0ac7-137">Пакет Azure предоставляет несколько возможностей, сделайте его легко tooconsume и использовать преимущества виртуальных машин с низким приоритетом.</span><span class="sxs-lookup"><span data-stu-id="d0ac7-137">Azure Batch provides several capabilities that make it easy tooconsume and benefit from low-priority VMs:</span></span>

-   <span data-ttu-id="d0ac7-138">Пулы пакетной службы могут содержать выделенные и низкоприоритетные виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="d0ac7-138">Batch pools can contain both dedicated VMs and low-priority VMs.</span></span> <span data-ttu-id="d0ac7-139">Hello количество каждого типа ВМ можно указать при создании пула, или изменить в любое время для существующего пула, с помощью операции hello явного изменения размера или автоматическое масштабирование.</span><span class="sxs-lookup"><span data-stu-id="d0ac7-139">hello number of each type of VM can be specified when a pool is created, or changed at any time for an existing pool, using hello explicit resize operation or using auto-scale.</span></span> <span data-ttu-id="d0ac7-140">Отправка заданий и задач может оставаться без изменений и не нужно беспокоиться hello типов ВМ в пуле hello.</span><span class="sxs-lookup"><span data-stu-id="d0ac7-140">Job and task submission can remain unchanged and do not need to be concerned with hello VM types in hello pool.</span></span> <span data-ttu-id="d0ac7-141">Это также возможно toohave пул полностью используйте низкого приоритета виртуальных машин toorun задания, но не раскрутки выделенных виртуальных машин экономно Если емкость hello падает ниже установленного порога, чтобы сохранить заданий, выполняемых.</span><span class="sxs-lookup"><span data-stu-id="d0ac7-141">It is also possible toohave a pool completely use low-priority VMs toorun jobs as cheaply as possible, but spin up dedicated VMs if hello capacity drops below a minimum threshold, to keep jobs running.</span></span>

-   <span data-ttu-id="d0ac7-142">Пулы пакета поиска автоматически toohello целевое количество виртуальных машин с низким приоритетом.</span><span class="sxs-lookup"><span data-stu-id="d0ac7-142">Batch pools automatically seek toohello target number of low-priority VMs.</span></span> <span data-ttu-id="d0ac7-143">Если прерывания виртуальные машины, пакет попытается hello tooreplace потерянных емкости и возврата toohello целевой.</span><span class="sxs-lookup"><span data-stu-id="d0ac7-143">If VMs are preempted, then Batch will attempt tooreplace hello lost capacity and return toohello target.</span></span>

-   <span data-ttu-id="d0ac7-144">В случае прерывания задач hello пакета обнаружит и автоматически повторной постановки в очередь снова запустите toobe задачи.</span><span class="sxs-lookup"><span data-stu-id="d0ac7-144">In hello case of tasks being interrupted, Batch will detect and automatically requeue tasks toobe run again.</span></span>

-   <span data-ttu-id="d0ac7-145">Низкоприоритетные виртуальные машины имеют квоту ядер, которая отличается от квоты выделенных виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="d0ac7-145">Low-priority VMs have a core quota that differs from that of dedicated VMs.</span></span> 
    <span data-ttu-id="d0ac7-146">Hello квоты для виртуальных машин с низким приоритетом выше, чем выделенных виртуальных машин, так как виртуальные машины с низким приоритетом снижение расходов.</span><span class="sxs-lookup"><span data-stu-id="d0ac7-146">hello quote for low-priority VMs is higher than that of dedicated VMs, because low-priority VMs cost less.</span></span> <span data-ttu-id="d0ac7-147">Дополнительные сведения см. в статье [Квоты и ограничения пакетной службы](batch-quota-limit.md#resource-quotas).</span><span class="sxs-lookup"><span data-stu-id="d0ac7-147">See [Batch service quotas and limits](batch-quota-limit.md#resource-quotas) for more information.</span></span>    

> [!NOTE]
> <span data-ttu-id="d0ac7-148">Виртуальные машины с низким приоритетом не поддерживаются для массовых учетных записей, где режим распределения пула hello установлено слишком[подписки пользователя](batch-account-create-portal.md#user-subscription-mode).</span><span class="sxs-lookup"><span data-stu-id="d0ac7-148">Low-priority VMs are not currently supported for Batch accounts where hello pool allocation mode is set too[User subscription](batch-account-create-portal.md#user-subscription-mode).</span></span>
>
>

## <a name="create-and-update-pools"></a><span data-ttu-id="d0ac7-149">Создание и обновление пулов</span><span class="sxs-lookup"><span data-stu-id="d0ac7-149">Create and update pools</span></span>

<span data-ttu-id="d0ac7-150">Пул пакет может содержать выделенным и низкого приоритета виртуальных машин (также назывались tooas вычислительных узлов).</span><span class="sxs-lookup"><span data-stu-id="d0ac7-150">A Batch pool can contain both dedicated and low-priority VMs (also referred tooas compute nodes).</span></span> <span data-ttu-id="d0ac7-151">Можно задать hello целевое количество вычислительных узлов для виртуальных машин, выделенных и низким приоритетом.</span><span class="sxs-lookup"><span data-stu-id="d0ac7-151">You can set hello target number of compute nodes for both dedicated and low-priority VMs.</span></span> <span data-ttu-id="d0ac7-152">Hello целевое количество узлов номер hello виртуальных машин требуется toohave в пуле hello.</span><span class="sxs-lookup"><span data-stu-id="d0ac7-152">hello target number of nodes specifies hello number of VMs you want toohave in hello pool.</span></span>

<span data-ttu-id="d0ac7-153">Например toocreate пул с помощью облачной службы Azure виртуальные машины с целью 5 выделенных виртуальных машин и 20 виртуальных машин с низким приоритетом:</span><span class="sxs-lookup"><span data-stu-id="d0ac7-153">For example, toocreate a pool using Azure cloud service VMs with a target of 5 dedicated VMs and 20 low-priority VMs:</span></span>

```csharp
CloudPool pool = batchClient.PoolOperations.CreatePool(
    poolId: "cspool",
    targetDedicatedComputeNodes: 5,
    targetLowPriorityComputeNodes: 20,
    virtualMachineSize: "Standard_D2_v2",
    cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4") // WS 2012 R2
);
```

<span data-ttu-id="d0ac7-154">toocreate пул с помощью виртуальных машин Azure (в данном случае виртуальных машин Linux) с целью 5 выделенных виртуальных машин и 20 виртуальных машин с низким приоритетом:</span><span class="sxs-lookup"><span data-stu-id="d0ac7-154">toocreate a pool using Azure virtual machines (in this case Linux VMs) with a target of 5 dedicated VMs and 20 low-priority VMs:</span></span>

```csharp
ImageReference imageRef = new ImageReference(
    publisher: "Canonical",
    offer: "UbuntuServer",
    sku: "16.04.0-LTS",
    version: "latest");

// Create hello pool
VirtualMachineConfiguration virtualMachineConfiguration =
    new VirtualMachineConfiguration("batch.node.ubuntu 16.04", imageRef);

pool = batchClient.PoolOperations.CreatePool(
    poolId: "vmpool",
    targetDedicatedComputeNodes: 5,
    targetLowPriorityComputeNodes: 20,
    virtualMachineSize: "Standard\_D2\_v2",
    virtualMachineConfiguration: virtualMachineConfiguration);
```

<span data-ttu-id="d0ac7-155">Можно получить hello текущее число узлов для виртуальных машин, выделенных и низким приоритетом:</span><span class="sxs-lookup"><span data-stu-id="d0ac7-155">You can get hello current number of nodes for both dedicated and low-priority VMs:</span></span>

```csharp
int? numDedicated = pool1.CurrentDedicatedComputeNodes;
int? numLowPri = pool1.CurrentLowPriorityComputeNodes;
```

<span data-ttu-id="d0ac7-156">Пул узлы имеют tooindicate свойства, если узел hello выделенными и низкого приоритета виртуальной Машины:</span><span class="sxs-lookup"><span data-stu-id="d0ac7-156">Pool nodes have a property tooindicate if hello node is a dedicated or low-priority VM:</span></span>

```csharp
bool? isNodeDedicated = poolNode.IsDedicated;
```

<span data-ttu-id="d0ac7-157">Задать прерывания один или несколько узлов в пуле, операция списка узлов в пуле по-прежнему будет возвращать те узлы, текущее число узлов низкого приоритета для hello не изменится, однако эти узлы будут иметь свое состояние toothe **замещена**состояние.</span><span class="sxs-lookup"><span data-stu-id="d0ac7-157">When one or more nodes in a pool are preempted, a list nodes operation on the pool will still return those nodes, hello current number of low-priority nodes will remain unchanged, but those nodes will have their state set toothe **Preempted** state.</span></span> <span data-ttu-id="d0ac7-158">Пакет попытается замены toofind виртуальные машины, и в случае успешного выполнения hello узлы будут проходить через **создание** и затем **запуск** состояния перед тем как стать доступными для выполнения задач, так же, как новые узлы.</span><span class="sxs-lookup"><span data-stu-id="d0ac7-158">Batch will attempt toofind replacement VMs and, if successful, hello nodes will go through **Creating** and then **Starting** states before becoming available for task execution, just like new nodes.</span></span>

## <a name="scale-a-pool-containing-low-priority-vms"></a><span data-ttu-id="d0ac7-159">Масштабирование пула низкоприоритетных виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="d0ac7-159">Scale a pool containing low-priority VMs</span></span>

<span data-ttu-id="d0ac7-160">С помощью пулы, состоящей исключительно выделенных виртуальных машин, это возможных tooscale пула содержащего низкоприоритетных виртуальных машин путем вызова метода hello изменения размера или с помощью автоматического масштабирования.</span><span class="sxs-lookup"><span data-stu-id="d0ac7-160">As with pools solely consisting of dedicated VMs, it is possible tooscale a pool containing low-priority VMs by calling hello Resize method or by using auto-scale.</span></span>

<span data-ttu-id="d0ac7-161">Hello операция изменения размера пула принимает второй необязательный параметр, который обновляет значение **targetLowPriorityNodes**:</span><span class="sxs-lookup"><span data-stu-id="d0ac7-161">hello pool resize operation takes a second optional parameter that updates the value of **targetLowPriorityNodes**:</span></span>

```csharp
pool.Resize(targetDedicatedComputeNodes: 0, targetLowPriorityComputeNodes: 25);
```

<span data-ttu-id="d0ac7-162">Формула автоматического масштабирования пула Hello поддерживает виртуальные машины с низким приоритетом следующим образом:</span><span class="sxs-lookup"><span data-stu-id="d0ac7-162">hello pool auto-scale formula supports low-priority VMs as follows:</span></span>

-   <span data-ttu-id="d0ac7-163">Можно получить или задать значение hello переменной определяемого пользователем службы hello **$TargetLowPriorityNodes**.</span><span class="sxs-lookup"><span data-stu-id="d0ac7-163">You can get or set hello value of hello service-defined variable **$TargetLowPriorityNodes**.</span></span>

-   <span data-ttu-id="d0ac7-164">Можно получить hello значения переменной определяемого пользователем службы hello **$CurrentLowPriorityNodes**.</span><span class="sxs-lookup"><span data-stu-id="d0ac7-164">You can get hello value of hello service-defined variable **$CurrentLowPriorityNodes**.</span></span>

-   <span data-ttu-id="d0ac7-165">Можно получить hello значения переменной определяемого пользователем службы hello **$PreemptedNodeCount**.</span><span class="sxs-lookup"><span data-stu-id="d0ac7-165">You can get hello value of hello service-defined variable **$PreemptedNodeCount**.</span></span> 
    <span data-ttu-id="d0ac7-166">Эта переменная возвращает hello количество узлов в hello различные состояния и дает возможность масштабирования вверх или вниз hello количество выделенных узлов, в зависимости от числа hello прерванный узлов, которые недоступны.</span><span class="sxs-lookup"><span data-stu-id="d0ac7-166">This variable returns hello number of nodes in hello preempted state and allows you to scale up or down hello number of dedicated nodes, depending on hello number of preempted nodes that are unavailable.</span></span>

## <a name="jobs-and-tasks"></a><span data-ttu-id="d0ac7-167">Задания и задачи</span><span class="sxs-lookup"><span data-stu-id="d0ac7-167">Jobs and tasks</span></span>

<span data-ttu-id="d0ac7-168">Заданий и задач требуется поддержка очень мало низкоприоритетных узлов; поддерживают только Hello выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="d0ac7-168">Jobs and tasks require very little support for low-priority nodes; hello only support is as follows:</span></span>

-   <span data-ttu-id="d0ac7-169">Hello JobManagerTask свойства задания имеет новое свойство, **AllowLowPriorityNode**.</span><span class="sxs-lookup"><span data-stu-id="d0ac7-169">hello JobManagerTask property of a job has a new property, **AllowLowPriorityNode**.</span></span> 
    <span data-ttu-id="d0ac7-170">Если это свойство имеет значение true, задача диспетчера заданий hello могут быть назначены на выделенном или низким приоритетом узла.</span><span class="sxs-lookup"><span data-stu-id="d0ac7-170">When this property is true, hello job manager task can be scheduled on either a dedicated or low-priority node.</span></span> <span data-ttu-id="d0ac7-171">Если это свойство имеет значение false, hello задачи диспетчера заданий будет запланированных tooa только выделенный узел.</span><span class="sxs-lookup"><span data-stu-id="d0ac7-171">If this property is false, hello job manager task will be scheduled tooa dedicated node only.</span></span>

-   <span data-ttu-id="d0ac7-172">[Переменной среды](batch-compute-node-environment-variables.md) является приложение tooa доступных задач, чтобы он мог определить, выполняется ли он на узле с низким приоритетом или выделенный.</span><span class="sxs-lookup"><span data-stu-id="d0ac7-172">An [environment variable](batch-compute-node-environment-variables.md) is available tooa task application so that it can determine whether it is running on a low-priority or dedicated node.</span></span> <span data-ttu-id="d0ac7-173">переменная среды Hello — AZ_BATCH_NODE_IS_DEDICATED.</span><span class="sxs-lookup"><span data-stu-id="d0ac7-173">hello environment variable is AZ_BATCH_NODE_IS_DEDICATED.</span></span>

## <a name="handling-preemption"></a><span data-ttu-id="d0ac7-174">Обработка замещения</span><span class="sxs-lookup"><span data-stu-id="d0ac7-174">Handling preemption</span></span>

<span data-ttu-id="d0ac7-175">Иногда может быть высвобождены виртуальных машин; в этом случае пакет hello следующие:</span><span class="sxs-lookup"><span data-stu-id="d0ac7-175">VMs may occasionally be preempted; when this happens, Batch does hello following:</span></span>

-   <span data-ttu-id="d0ac7-176">Hello прерванный виртуальные машины имели свое состояние, также обновляются**замещена**.</span><span class="sxs-lookup"><span data-stu-id="d0ac7-176">hello preempted VMs have their state updated too**Preempted**.</span></span>
-   <span data-ttu-id="d0ac7-177">Если задачи выполнялись на hello высвобождены ВМ узлов, а затем повторно поставлен в очередь и снова запустите эти задачи.</span><span class="sxs-lookup"><span data-stu-id="d0ac7-177">If tasks were running on hello preempted node VMs, then those tasks are requeued and run again.</span></span>
-   <span data-ttu-id="d0ac7-178">фактически удаляется Hello виртуальной Машины, начальные tooany данные, хранящиеся локально на hello потерю виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="d0ac7-178">hello VM is effectively deleted, leading tooany data stored locally on hello VM being lost.</span></span>
-   <span data-ttu-id="d0ac7-179">пул Hello постоянно предпринимает tooreach hello целевое количество доступных узлов низким приоритетом.</span><span class="sxs-lookup"><span data-stu-id="d0ac7-179">hello pool continually attempts tooreach hello target number of low-priority nodes available.</span></span> <span data-ttu-id="d0ac7-180">При обнаружении замены идентификаторы узлов сохраняются, но узлы повторно инициализируются и их состояние меняется на **Создание** и **Запуск** перед тем, как они станут доступными для планирования задач.</span><span class="sxs-lookup"><span data-stu-id="d0ac7-180">When replacement capacity is found, the nodes keep their ids, but are re-initialized, going through **Creating** and **Starting** states before they are available for task scheduling.</span></span>
-   <span data-ttu-id="d0ac7-181">Замещение счетчики доступны как показатель в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="d0ac7-181">Preemption counts are available as a metric in hello Azure portal.</span></span>

## <a name="metrics"></a><span data-ttu-id="d0ac7-182">Метрики</span><span class="sxs-lookup"><span data-stu-id="d0ac7-182">Metrics</span></span>

<span data-ttu-id="d0ac7-183">Доступны новые метрики в hello [портал Azure](https://portal.azure.com) для узлов с низким приоритетом.</span><span class="sxs-lookup"><span data-stu-id="d0ac7-183">New metrics are available in hello [Azure portal](https://portal.azure.com) for low-priority nodes.</span></span> <span data-ttu-id="d0ac7-184">Это такие метрики:</span><span class="sxs-lookup"><span data-stu-id="d0ac7-184">These metrics are:</span></span>

- <span data-ttu-id="d0ac7-185">Low-Priority Node Count</span><span class="sxs-lookup"><span data-stu-id="d0ac7-185">Low-Priority Node Count</span></span>
- <span data-ttu-id="d0ac7-186">Low-Priority Core Count;</span><span class="sxs-lookup"><span data-stu-id="d0ac7-186">Low-Priority Core Count</span></span> 
- <span data-ttu-id="d0ac7-187">Preempted Node Count</span><span class="sxs-lookup"><span data-stu-id="d0ac7-187">Preempted Node Count</span></span>

<span data-ttu-id="d0ac7-188">метрики tooview в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="d0ac7-188">tooview metrics in hello Azure portal:</span></span>

1. <span data-ttu-id="d0ac7-189">Перейти tooyour пакетной учетной записи на портале hello и открыть параметры hello пакетной учетной записи.</span><span class="sxs-lookup"><span data-stu-id="d0ac7-189">Navigate tooyour Batch account in hello portal, and view hello settings for your Batch account.</span></span>
2. <span data-ttu-id="d0ac7-190">Выберите **метрики** из hello **мониторинг** раздела.</span><span class="sxs-lookup"><span data-stu-id="d0ac7-190">Select **Metrics** from hello **Monitoring** section.</span></span>
3. <span data-ttu-id="d0ac7-191">Выберите метрики hello нужен hello **доступные метрики** списка.</span><span class="sxs-lookup"><span data-stu-id="d0ac7-191">Select hello metrics you desire from hello **Available Metrics** list.</span></span>

![Метрики для узлов с низким приоритетом](media/batch-low-pri-vms/low-pri-metrics.png)

## <a name="next-steps"></a><span data-ttu-id="d0ac7-193">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d0ac7-193">Next steps</span></span>

* <span data-ttu-id="d0ac7-194">Чтение hello [пакета Обзор возможностей для разработчиков](batch-api-basics.md), важные сведения для тех, кто Подготовка toouse пакета.</span><span class="sxs-lookup"><span data-stu-id="d0ac7-194">Read hello [Batch feature overview for developers](batch-api-basics.md), essential information for anyone preparing toouse Batch.</span></span> <span data-ttu-id="d0ac7-195">Hello статья содержит более подробные сведения о пакете службы ресурсы, такие как пулы, узлы, заданий и задач и hello множество функций API, которые можно использовать при создании пакета приложения.</span><span class="sxs-lookup"><span data-stu-id="d0ac7-195">hello article contains more detailed information about Batch service resources like pools, nodes, jobs, and tasks, and hello many API features that you can use while building your Batch application.</span></span>
* <span data-ttu-id="d0ac7-196">Дополнительные сведения о hello [API-интерфейсы пакета и средства](batch-apis-tools.md) для сборки пакета решения.</span><span class="sxs-lookup"><span data-stu-id="d0ac7-196">Learn about hello [Batch APIs and tools](batch-apis-tools.md) available for building Batch solutions.</span></span>
