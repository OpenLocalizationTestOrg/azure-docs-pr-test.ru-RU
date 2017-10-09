---
title: "aaaScheduled событий для виртуальных машин Windows в Azure | Документы Microsoft"
description: "Запланированные события использования hello Azure метаданные службы для виртуальных машинах Windows."
services: virtual-machines-windows, virtual-machines-linux, cloud-services
documentationcenter: 
author: zivraf
manager: timlt
editor: 
tags: 
ms.assetid: 28d8e1f2-8e61-4fbe-bfe8-80a68443baba
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/14/2017
ms.author: zivr
ms.openlocfilehash: c9f5f332a5d77e8d54d1ae8bdaadafc1a14f3b77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-metadata-service-scheduled-events-preview-for-windows-vms"></a><span data-ttu-id="bb81f-103">Служба метаданных Azure. Запланированные события (предварительная версия) для виртуальных машин Windows</span><span class="sxs-lookup"><span data-stu-id="bb81f-103">Azure Metadata Service: Scheduled Events (Preview) for Windows VMs</span></span>

> [!NOTE] 
> <span data-ttu-id="bb81f-104">Предварительный просмотр вносятся доступных tooyou, вы принимаете условия использования toohello условие hello.</span><span class="sxs-lookup"><span data-stu-id="bb81f-104">Previews are made available tooyou on hello condition that you agree toohello terms of use.</span></span> <span data-ttu-id="bb81f-105">Дополнительные сведения см. в статье [Дополнительные условия использования предварительных выпусков Microsoft Azure](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).</span><span class="sxs-lookup"><span data-stu-id="bb81f-105">For more information, see [Microsoft Azure Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).</span></span>
>

<span data-ttu-id="bb81f-106">Запланированные события является одним из subservices hello под hello Azure метаданных службы.</span><span class="sxs-lookup"><span data-stu-id="bb81f-106">Scheduled Events is one of hello subservices under hello Azure Metadata Service.</span></span> <span data-ttu-id="bb81f-107">Она предоставляет сведения о предстоящих событиях (например, перезагрузках), что позволяет приложениям подготовиться к ним и уменьшить влияние на работу.</span><span class="sxs-lookup"><span data-stu-id="bb81f-107">It is responsible for surfacing information regarding upcoming events (for example, reboot) so your application can prepare for them and limit disruption.</span></span> <span data-ttu-id="bb81f-108">Эти сведения доступны для всех типов виртуальных машин Azure, включая PaaS и IaaS.</span><span class="sxs-lookup"><span data-stu-id="bb81f-108">It is available for all Azure Virtual Machine types including PaaS and IaaS.</span></span> <span data-ttu-id="bb81f-109">Запланированные события предоставляет виртуальную машину времени задачи профилактического tooperform эффект hello toominimize события.</span><span class="sxs-lookup"><span data-stu-id="bb81f-109">Scheduled Events gives your Virtual Machine time tooperform preventive tasks toominimize hello effect of an event.</span></span> 

<span data-ttu-id="bb81f-110">Запланированные события доступны для виртуальных машин Windows и Linux.</span><span class="sxs-lookup"><span data-stu-id="bb81f-110">Scheduled Events is available for both Linux and Windows VMs.</span></span> <span data-ttu-id="bb81f-111">Сведения о запланированных событиях в Linux см. в статье [Служба метаданных Azure. Запланированные события (предварительная версия) для виртуальных машин Linux](../windows/scheduled-events.md).</span><span class="sxs-lookup"><span data-stu-id="bb81f-111">For information about Scheduled Events on Linux, see [Scheduled Events for Linux VMs](../windows/scheduled-events.md).</span></span>

## <a name="why-scheduled-events"></a><span data-ttu-id="bb81f-112">Зачем нужны запланированные события</span><span class="sxs-lookup"><span data-stu-id="bb81f-112">Why Scheduled Events?</span></span>

<span data-ttu-id="bb81f-113">С запланированные события можно предпринять шаги hello влияние toolimit intiated платформы обслуживания или действия, инициируемые пользователем в службе.</span><span class="sxs-lookup"><span data-stu-id="bb81f-113">With Scheduled Events, you can take steps toolimit hello impact of platform-intiated maintenance or user-initiated actions on your service.</span></span> 

<span data-ttu-id="bb81f-114">Несколькими экземплярами рабочих нагрузок, которые используют состояние toomaintain методы репликации, могут быть уязвимыми toooutages происходит между несколькими экземплярами.</span><span class="sxs-lookup"><span data-stu-id="bb81f-114">Multi-instance workloads, which use replication techniques toomaintain state, may be vulnerable toooutages happening across multiple instances.</span></span> <span data-ttu-id="bb81f-115">Такие простои могут потребовать дорогостоящих действий (например, перестроения индексов) или привести к потере реплики.</span><span class="sxs-lookup"><span data-stu-id="bb81f-115">Such outages may result in expensive tasks (for example, rebuilding indexes) or even a replica loss.</span></span> 

<span data-ttu-id="bb81f-116">Во многих других случаях hello общую доступность службы может быть повышена путем выполнения последовательность отключения, таких как завершение (или отменяемое) транзакции на лету, переназначение задачи tooother виртуальных машин в кластере hello (отработка отказа вручную) или удаление hello Виртуальную машину из пула подсистемы балансировки нагрузки сети.</span><span class="sxs-lookup"><span data-stu-id="bb81f-116">In many other cases, hello overall service availability may be improved by performing a graceful shutdown sequence such as completing (or canceling) in-flight transactions, reassigning tasks tooother VMs in hello cluster (manual failover), or removing hello Virtual Machine from a network load balancer pool.</span></span> 

<span data-ttu-id="bb81f-117">Существуют случаи, где обращения к администратору о предстоящих событий или ведение журнала такого события помочь повышение hello удобство обслуживания приложений, размещенных в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="bb81f-117">There are cases where notifying an administrator about an upcoming event or logging such an event help improving hello serviceability of applications hosted in hello cloud.</span></span>

<span data-ttu-id="bb81f-118">Варианты использования Azure служба метаданных поверхности запланированные события в hello ниже:</span><span class="sxs-lookup"><span data-stu-id="bb81f-118">Azure Metadata Service surfaces Scheduled Events in hello following use cases:</span></span>
-   <span data-ttu-id="bb81f-119">Инициируемое платформой обслуживание (например, развертывание ОС узла).</span><span class="sxs-lookup"><span data-stu-id="bb81f-119">Platform initiated maintenance (for example, Host OS rollout)</span></span>
-   <span data-ttu-id="bb81f-120">Инициируемые пользователем вызовы (например, пользователь перезапускает или повторно развертывает виртуальную машину).</span><span class="sxs-lookup"><span data-stu-id="bb81f-120">User-initiated calls (for example, user restarts or redeploys a VM)</span></span>


## <a name="hello-basics"></a><span data-ttu-id="bb81f-121">Основы Hello</span><span class="sxs-lookup"><span data-stu-id="bb81f-121">hello basics</span></span>  

<span data-ttu-id="bb81f-122">Azure служба метаданных предоставляет сведения о запуске виртуальных машин с помощью конечной точки REST, доступный из hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="bb81f-122">Azure Metadata service exposes information about running Virtual Machines using a REST Endpoint accessible from within hello VM.</span></span> <span data-ttu-id="bb81f-123">сведения о Hello доступна через немаршрутизируемый IP, чтобы она не предоставляется вне hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="bb81f-123">hello information is available via a non-routable IP so that it is not exposed outside hello VM.</span></span>

### <a name="scope"></a><span data-ttu-id="bb81f-124">Область</span><span class="sxs-lookup"><span data-stu-id="bb81f-124">Scope</span></span>
<span data-ttu-id="bb81f-125">Запланированные события, отображается tooall виртуальных машин в облачной службе или tooall виртуальных машин в группе доступности.</span><span class="sxs-lookup"><span data-stu-id="bb81f-125">Scheduled events are surfaced tooall Virtual Machines in a cloud service or tooall Virtual Machines in an Availability Set.</span></span> <span data-ttu-id="bb81f-126">Поэтому следует проверить hello `Resources` в tooidentify событий hello, в которой виртуальные машины будут затронуты toobe.</span><span class="sxs-lookup"><span data-stu-id="bb81f-126">As a result, you should check hello `Resources` field in hello event tooidentify which VMs are going toobe impacted.</span></span> 

### <a name="discovering-hello-endpoint"></a><span data-ttu-id="bb81f-127">Обнаружение конечной точки hello</span><span class="sxs-lookup"><span data-stu-id="bb81f-127">Discovering hello endpoint</span></span>
<span data-ttu-id="bb81f-128">В случае hello, где создается виртуальной машины в виртуальной сети (VNet), служба метаданных hello доступна из статический немаршрутизируемый IP- `169.254.169.254`.</span><span class="sxs-lookup"><span data-stu-id="bb81f-128">In hello case where a Virtual Machine is created within a Virtual Network (VNet), hello metadata service is available from a static non-routable IP, `169.254.169.254`.</span></span>
<span data-ttu-id="bb81f-129">Если hello виртуальной машины в виртуальной сети вариантов по умолчанию hello для облачных служб и классические ВМ не создается дополнительная логика является toouse конечной точки требуется toodiscover hello.</span><span class="sxs-lookup"><span data-stu-id="bb81f-129">If hello Virtual Machine is not created within a Virtual Network, hello default cases for cloud services and classic VMs, additional logic is required toodiscover hello endpoint toouse.</span></span> <span data-ttu-id="bb81f-130">См. Образец toolearn toothis как слишком[обнаружение конечной точки узлов hello](https://github.com/azure-samples/virtual-machines-python-scheduled-events-discover-endpoint-for-non-vnet-vm).</span><span class="sxs-lookup"><span data-stu-id="bb81f-130">Refer toothis sample toolearn how too[discover hello host endpoint](https://github.com/azure-samples/virtual-machines-python-scheduled-events-discover-endpoint-for-non-vnet-vm).</span></span>

### <a name="versioning"></a><span data-ttu-id="bb81f-131">Управление версиями</span><span class="sxs-lookup"><span data-stu-id="bb81f-131">Versioning</span></span> 
<span data-ttu-id="bb81f-132">Hello метаданных экземпляра службы с версиями.</span><span class="sxs-lookup"><span data-stu-id="bb81f-132">hello Instance Metadata Service is versioned.</span></span> <span data-ttu-id="bb81f-133">Версии являются обязательными, и текущая версия hello `2017-03-01`.</span><span class="sxs-lookup"><span data-stu-id="bb81f-133">Versions are mandatory and hello current version is `2017-03-01`.</span></span>

> [!NOTE] 
> <span data-ttu-id="bb81f-134">Предыдущие выпуски Предварительный просмотр поддерживается {последние} в качестве hello api-version запланированные события.</span><span class="sxs-lookup"><span data-stu-id="bb81f-134">Previous preview releases of scheduled events supported {latest} as hello api-version.</span></span> <span data-ttu-id="bb81f-135">Этот формат не поддерживается и будет считаться устаревшей в будущем hello.</span><span class="sxs-lookup"><span data-stu-id="bb81f-135">This format is no longer supported and will be deprecated in hello future.</span></span>

### <a name="using-headers"></a><span data-ttu-id="bb81f-136">Использование заголовков</span><span class="sxs-lookup"><span data-stu-id="bb81f-136">Using headers</span></span>
<span data-ttu-id="bb81f-137">При запросе hello метаданных службы, необходимо указать заголовок hello `Metadata: true` tooensure hello запрос не был перенаправлен непреднамеренно.</span><span class="sxs-lookup"><span data-stu-id="bb81f-137">When you query hello Metadata Service, you must provide hello header `Metadata: true` tooensure hello request was not unintentionally redirected.</span></span>

### <a name="enabling-scheduled-events"></a><span data-ttu-id="bb81f-138">Включение запланированных событий</span><span class="sxs-lookup"><span data-stu-id="bb81f-138">Enabling Scheduled Events</span></span>
<span data-ttu-id="bb81f-139">Hello при первом запуске запроса для запланированных событий Azure неявно включает hello функцию на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="bb81f-139">hello first time you make a request for scheduled events, Azure implicitly enables hello feature on your Virtual Machine.</span></span> <span data-ttu-id="bb81f-140">Поэтому следует ожидать задержки ответа в первом вызове из копии tootwo минут.</span><span class="sxs-lookup"><span data-stu-id="bb81f-140">As a result, you should expect a delayed response in your first call of up tootwo minutes.</span></span>

### <a name="user-initiated-maintenance"></a><span data-ttu-id="bb81f-141">Обслуживание, инициированное пользователем</span><span class="sxs-lookup"><span data-stu-id="bb81f-141">User initiated maintenance</span></span>
<span data-ttu-id="bb81f-142">Пользователь запустил обслуживание виртуальных машин через hello портал Azure API, CLI, или PowerShell приводит запланированное событие.</span><span class="sxs-lookup"><span data-stu-id="bb81f-142">User initiated virtual machine maintenance via hello Azure portal, API, CLI, or PowerShell results in a scheduled event.</span></span> <span data-ttu-id="bb81f-143">Это позволяет tootest hello обслуживания подготовки логики в приложении а tooprepare вашего приложения для обслуживания инициированной пользователем.</span><span class="sxs-lookup"><span data-stu-id="bb81f-143">This allows you tootest hello maintenance preparation logic in your application and allows your application tooprepare for user initiated maintenance.</span></span>

<span data-ttu-id="bb81f-144">При перезапуске виртуальной машины планируется событие с типом `Reboot`.</span><span class="sxs-lookup"><span data-stu-id="bb81f-144">Restarting a virtual machine schedules an event with type `Reboot`.</span></span> <span data-ttu-id="bb81f-145">При развертывании виртуальной машины планируется событие с типом `Redeploy`.</span><span class="sxs-lookup"><span data-stu-id="bb81f-145">Redeploying a virtual machine schedules an event with type `Redeploy`.</span></span>

> [!NOTE] 
> <span data-ttu-id="bb81f-146">Сейчас можно одновременно запланировать более десяти операций обслуживания, инициированных пользователем.</span><span class="sxs-lookup"><span data-stu-id="bb81f-146">Currently a maximum of 10 user initiated maintenance operations can be simultaneously scheduled.</span></span> <span data-ttu-id="bb81f-147">Это ограничение будет снято еще до выпуска общедоступной версии запланированных событий.</span><span class="sxs-lookup"><span data-stu-id="bb81f-147">This limit will be relaxed before Scheduled Events general availability.</span></span>

> [!NOTE] 
> <span data-ttu-id="bb81f-148">Сейчас обслуживание, инициированное пользователем, которое влияет на запланированные события, не настраивается.</span><span class="sxs-lookup"><span data-stu-id="bb81f-148">Currently user initiated maintenance resulting in Scheduled Events is not configurable.</span></span> <span data-ttu-id="bb81f-149">Возможность настройки запланирована к следующему выпуску.</span><span class="sxs-lookup"><span data-stu-id="bb81f-149">Configurability is planned for a future release.</span></span>

## <a name="using-hello-api"></a><span data-ttu-id="bb81f-150">С помощью hello API</span><span class="sxs-lookup"><span data-stu-id="bb81f-150">Using hello API</span></span>

### <a name="query-for-events"></a><span data-ttu-id="bb81f-151">Запрос сведений о событиях</span><span class="sxs-lookup"><span data-stu-id="bb81f-151">Query for events</span></span>
<span data-ttu-id="bb81f-152">Вы можете запрашивать запланированные события, просто выполнив hello следующий вызов:</span><span class="sxs-lookup"><span data-stu-id="bb81f-152">You can query for Scheduled Events simply by making hello following call:</span></span>

```
curl -H Metadata:true http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01
```

<span data-ttu-id="bb81f-153">Ответ содержит массив запланированных событий.</span><span class="sxs-lookup"><span data-stu-id="bb81f-153">A response contains an array of scheduled events.</span></span> <span data-ttu-id="bb81f-154">Если это будет пустой массив, значит сейчас запланированных событий нет.</span><span class="sxs-lookup"><span data-stu-id="bb81f-154">An empty array means that there are currently no events scheduled.</span></span>
<span data-ttu-id="bb81f-155">В случае hello которых запланированные события, hello ответ содержит массив событий:</span><span class="sxs-lookup"><span data-stu-id="bb81f-155">In hello case where there are scheduled events, hello response contains an array of events:</span></span> 
```
{
    "DocumentIncarnation": {IncarnationID},
    "Events": [
        {
            "EventId": {eventID},
            "EventType": "Reboot" | "Redeploy" | "Freeze",
            "ResourceType": "VirtualMachine",
            "Resources": [{resourceName}],
            "EventStatus": "Scheduled" | "Started",
            "NotBefore": {timeInUTC},              
        }
    ]
}
```

### <a name="event-properties"></a><span data-ttu-id="bb81f-156">Свойства события</span><span class="sxs-lookup"><span data-stu-id="bb81f-156">Event properties</span></span>
|<span data-ttu-id="bb81f-157">Свойство</span><span class="sxs-lookup"><span data-stu-id="bb81f-157">Property</span></span>  |  <span data-ttu-id="bb81f-158">Описание</span><span class="sxs-lookup"><span data-stu-id="bb81f-158">Description</span></span> |
| - | - |
| <span data-ttu-id="bb81f-159">EventId</span><span class="sxs-lookup"><span data-stu-id="bb81f-159">EventId</span></span> | <span data-ttu-id="bb81f-160">Глобальный уникальный идентификатор этого события.</span><span class="sxs-lookup"><span data-stu-id="bb81f-160">Globally unique identifier for this event.</span></span> <br><br> <span data-ttu-id="bb81f-161">Пример:</span><span class="sxs-lookup"><span data-stu-id="bb81f-161">Example:</span></span> <br><ul><li><span data-ttu-id="bb81f-162">602d9444-d2cd-49c7-8624-8643e7171297</span><span class="sxs-lookup"><span data-stu-id="bb81f-162">602d9444-d2cd-49c7-8624-8643e7171297</span></span>  |
| <span data-ttu-id="bb81f-163">EventType</span><span class="sxs-lookup"><span data-stu-id="bb81f-163">EventType</span></span> | <span data-ttu-id="bb81f-164">Влияние, которое оказывает это событие.</span><span class="sxs-lookup"><span data-stu-id="bb81f-164">Impact this event causes.</span></span> <br><br> <span data-ttu-id="bb81f-165">Значения:</span><span class="sxs-lookup"><span data-stu-id="bb81f-165">Values:</span></span> <br><ul><li> <span data-ttu-id="bb81f-166">`Freeze`: hello виртуальной машины — запланированных toopause несколько секунд.</span><span class="sxs-lookup"><span data-stu-id="bb81f-166">`Freeze`: hello Virtual Machine is scheduled toopause for few seconds.</span></span> <span data-ttu-id="bb81f-167">Hello ЦП приостанавливается, но не влияет на открытые файлы, сетевые подключения или оперативной памяти.</span><span class="sxs-lookup"><span data-stu-id="bb81f-167">hello CPU is suspended, but there is no impact on memory, open files, or network connections.</span></span> <li><span data-ttu-id="bb81f-168">`Reboot`: hello запланирована перезагрузка виртуальной машины (непостоянные памяти теряются).</span><span class="sxs-lookup"><span data-stu-id="bb81f-168">`Reboot`: hello Virtual Machine is scheduled for reboot (non-persistent memory is lost).</span></span> <li><span data-ttu-id="bb81f-169">`Redeploy`: hello виртуальной машины является узлом tooanother запланированных toomove (временных дисков теряются).</span><span class="sxs-lookup"><span data-stu-id="bb81f-169">`Redeploy`: hello Virtual Machine is scheduled toomove tooanother node (ephemeral disks are lost).</span></span> |
| <span data-ttu-id="bb81f-170">ResourceType</span><span class="sxs-lookup"><span data-stu-id="bb81f-170">ResourceType</span></span> | <span data-ttu-id="bb81f-171">Тип ресурса, на который влияет это событие.</span><span class="sxs-lookup"><span data-stu-id="bb81f-171">Type of resource this event impacts.</span></span> <br><br> <span data-ttu-id="bb81f-172">Значения:</span><span class="sxs-lookup"><span data-stu-id="bb81f-172">Values:</span></span> <ul><li>`VirtualMachine`|
| <span data-ttu-id="bb81f-173">Ресурсы</span><span class="sxs-lookup"><span data-stu-id="bb81f-173">Resources</span></span>| <span data-ttu-id="bb81f-174">Список ресурсов, на которые влияет это событие.</span><span class="sxs-lookup"><span data-stu-id="bb81f-174">List of resources this event impacts.</span></span> <span data-ttu-id="bb81f-175">Это гарантируется машины toocontain из не более одного [домен обновления](manage-availability.md), но не может содержать все машины в hello UD.</span><span class="sxs-lookup"><span data-stu-id="bb81f-175">This is guaranteed toocontain machines from at most one [Update Domain](manage-availability.md), but may not contain all machines in hello UD.</span></span> <br><br> <span data-ttu-id="bb81f-176">Пример:</span><span class="sxs-lookup"><span data-stu-id="bb81f-176">Example:</span></span> <br><ul><li> <span data-ttu-id="bb81f-177">["FrontEnd_IN_0", "BackEnd_IN_0"]</span><span class="sxs-lookup"><span data-stu-id="bb81f-177">["FrontEnd_IN_0", "BackEnd_IN_0"]</span></span> |
| <span data-ttu-id="bb81f-178">Event Status</span><span class="sxs-lookup"><span data-stu-id="bb81f-178">Event Status</span></span> | <span data-ttu-id="bb81f-179">Состояние этого события.</span><span class="sxs-lookup"><span data-stu-id="bb81f-179">Status of this event.</span></span> <br><br> <span data-ttu-id="bb81f-180">Значения:</span><span class="sxs-lookup"><span data-stu-id="bb81f-180">Values:</span></span> <ul><li><span data-ttu-id="bb81f-181">`Scheduled`: Это событие является запланированных toostart после hello времени, указанного в hello `NotBefore` свойство.</span><span class="sxs-lookup"><span data-stu-id="bb81f-181">`Scheduled`: This event is scheduled toostart after hello time specified in hello `NotBefore` property.</span></span><li><span data-ttu-id="bb81f-182">`Started`. Это событие запущено.</span><span class="sxs-lookup"><span data-stu-id="bb81f-182">`Started`: This event has started.</span></span></ul> <span data-ttu-id="bb81f-183">Не `Completed` или когда-либо предоставляется как состояние; hello событие больше не возвращаются при завершении события hello.</span><span class="sxs-lookup"><span data-stu-id="bb81f-183">No `Completed` or similar status is ever provided; hello event will no longer be returned when hello event is completed.</span></span>
| <span data-ttu-id="bb81f-184">NotBefore</span><span class="sxs-lookup"><span data-stu-id="bb81f-184">NotBefore</span></span>| <span data-ttu-id="bb81f-185">Время, после которого может быть запущено это событие.</span><span class="sxs-lookup"><span data-stu-id="bb81f-185">Time after which this event may start.</span></span> <br><br> <span data-ttu-id="bb81f-186">Пример:</span><span class="sxs-lookup"><span data-stu-id="bb81f-186">Example:</span></span> <br><ul><li> <span data-ttu-id="bb81f-187">2016-09-19T18:29:47Z</span><span class="sxs-lookup"><span data-stu-id="bb81f-187">2016-09-19T18:29:47Z</span></span>  |

### <a name="event-scheduling"></a><span data-ttu-id="bb81f-188">Планирование события</span><span class="sxs-lookup"><span data-stu-id="bb81f-188">Event scheduling</span></span>
<span data-ttu-id="bb81f-189">Каждое событие запланирована минимальное количество времени в будущем hello в зависимости от типа события.</span><span class="sxs-lookup"><span data-stu-id="bb81f-189">Each event is scheduled a minimum amount of time in hello future based on event type.</span></span> <span data-ttu-id="bb81f-190">Это время отражается в свойстве события `NotBefore`.</span><span class="sxs-lookup"><span data-stu-id="bb81f-190">This time is reflected in an event's `NotBefore` property.</span></span> 

|<span data-ttu-id="bb81f-191">EventType</span><span class="sxs-lookup"><span data-stu-id="bb81f-191">EventType</span></span>  | <span data-ttu-id="bb81f-192">Минимальное время уведомления</span><span class="sxs-lookup"><span data-stu-id="bb81f-192">Minimum Notice</span></span> |
| - | - |
| <span data-ttu-id="bb81f-193">Freeze</span><span class="sxs-lookup"><span data-stu-id="bb81f-193">Freeze</span></span>| <span data-ttu-id="bb81f-194">15 минут</span><span class="sxs-lookup"><span data-stu-id="bb81f-194">15 minutes</span></span> |
| <span data-ttu-id="bb81f-195">Reboot</span><span class="sxs-lookup"><span data-stu-id="bb81f-195">Reboot</span></span> | <span data-ttu-id="bb81f-196">15 минут</span><span class="sxs-lookup"><span data-stu-id="bb81f-196">15 minutes</span></span> |
| <span data-ttu-id="bb81f-197">Повторное развертывание</span><span class="sxs-lookup"><span data-stu-id="bb81f-197">Redeploy</span></span> | <span data-ttu-id="bb81f-198">10 минут</span><span class="sxs-lookup"><span data-stu-id="bb81f-198">10 minutes</span></span> |

### <a name="starting-an-event"></a><span data-ttu-id="bb81f-199">Запуск события</span><span class="sxs-lookup"><span data-stu-id="bb81f-199">Starting an event</span></span> 

<span data-ttu-id="bb81f-200">Как только вы узнали о предстоящих событий и завершили свою логику для нормальное завершение работы, вы можете утвердить необработанных событий hello, делая `POST` вызова toohello метаданные службы с hello `EventId`.</span><span class="sxs-lookup"><span data-stu-id="bb81f-200">Once you have learned of an upcoming event and completed your logic for graceful shutdown, you can approve hello outstanding event by making a `POST` call toohello metadata service with hello `EventId`.</span></span> <span data-ttu-id="bb81f-201">Указывает tooAzure, он может сократить минимальное уведомления hello время (если возможно).</span><span class="sxs-lookup"><span data-stu-id="bb81f-201">This indicates tooAzure that it can shorten hello minimum notification time (when possible).</span></span> 

```
curl -H Metadata:true -X POST -d '{"DocumentIncarnation":"5", "StartRequests": [{"EventId": "f020ba2e-3bc0-4c40-a10b-86575a9eabd5"}]}' http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01
```

> [!NOTE] 
> <span data-ttu-id="bb81f-202">Подтверждение события позволяет hello tooproceed событий для всех `Resources` в событии hello не только hello виртуальную машину, которая подтверждает hello событий.</span><span class="sxs-lookup"><span data-stu-id="bb81f-202">Acknowledging an event allows hello event tooproceed for all `Resources` in hello event, not just hello virtual machine that acknowledges hello event.</span></span> <span data-ttu-id="bb81f-203">Таким образом можно tooelect подтверждение hello руководитель toocoordinate, которое может быть простым как первой машине hello в hello `Resources` поля.</span><span class="sxs-lookup"><span data-stu-id="bb81f-203">You may therefore choose tooelect a leader toocoordinate hello acknowledgement, which may be as simple as hello first machine in hello `Resources` field.</span></span>


## <a name="powershell-sample"></a><span data-ttu-id="bb81f-204">Пример для PowerShell</span><span class="sxs-lookup"><span data-stu-id="bb81f-204">PowerShell sample</span></span> 

<span data-ttu-id="bb81f-205">Hello следующие примеры запросов hello метаданные службы для запланированных событий и утверждает каждого необработанные события.</span><span class="sxs-lookup"><span data-stu-id="bb81f-205">hello following sample queries hello metadata service for scheduled events and approves each outstanding event.</span></span>

```PowerShell
# How tooget scheduled events 
function GetScheduledEvents($uri)
{
    $scheduledEvents = Invoke-RestMethod -Headers @{"Metadata"="true"} -URI $uri -Method get
    $json = ConvertTo-Json $scheduledEvents
    Write-Host "Received following events: `n" $json
    return $scheduledEvents
}

# How tooapprove a scheduled event
function ApproveScheduledEvent($eventId, $docIncarnation, $uri)
{    
    # Create hello Scheduled Events Approval Document
    $startRequests = [array]@{"EventId" = $eventId}
    $scheduledEventsApproval = @{"StartRequests" = $startRequests; "DocumentIncarnation" = $docIncarnation} 
    
    # Convert tooJSON string
    $approvalString = ConvertTo-Json $scheduledEventsApproval

    Write-Host "Approving with hello following: `n" $approvalString

    # Post approval string tooscheduled events endpoint
    Invoke-RestMethod -Uri $uri -Headers @{"Metadata"="true"} -Method POST -Body $approvalString
}

function HandleScheduledEvents($scheduledEvents)
{
    # Add logic for handling events here
}

######### Sample Scheduled Events Interaction #########

# Set up hello scheduled events URI for a VNET-enabled VM
$localHostIP = "169.254.169.254"
$scheduledEventURI = 'http://{0}/metadata/scheduledevents?api-version=2017-03-01' -f $localHostIP 

# Get events
$scheduledEvents = GetScheduledEvents $scheduledEventURI

# Handle events however is best for your service
HandleScheduledEvents $scheduledEvents

# Approve events when ready (optional)
foreach($event in $scheduledEvents.Events)
{
    Write-Host "Current Event: `n" $event
    $entry = Read-Host "`nApprove event? Y/N"
    if($entry -eq "Y" -or $entry -eq "y")
    {
        ApproveScheduledEvent $event.EventId $scheduledEvents.DocumentIncarnation $scheduledEventURI 
    }
}
``` 


## <a name="c-sample"></a><span data-ttu-id="bb81f-206">Пример на языке C\#</span><span class="sxs-lookup"><span data-stu-id="bb81f-206">C\# sample</span></span> 

<span data-ttu-id="bb81f-207">Hello следующий пример является простой клиента, которая взаимодействует со службой метаданных hello.</span><span class="sxs-lookup"><span data-stu-id="bb81f-207">hello following sample is of a simple client that communicates with hello metadata service.</span></span>

```csharp
public class ScheduledEventsClient
{
    private readonly string scheduledEventsEndpoint;
    private readonly string defaultIpAddress = "169.254.169.254"; 

    // Set up hello scheduled events URI for a VNET-enabled VM
    public ScheduledEventsClient()
    {
        scheduledEventsEndpoint = string.Format("http://{0}/metadata/scheduledevents?api-version=2017-03-01", defaultIpAddress);
    }

    // Get events
    public string GetScheduledEvents()
    {
        Uri cloudControlUri = new Uri(scheduledEventsEndpoint);
        using (var webClient = new WebClient())
        {
            webClient.Headers.Add("Metadata", "true");
            return webClient.DownloadString(cloudControlUri);
        }   
    }

    // Approve events
    public void ApproveScheduledEvents(string jsonPost)
    {
        using (var webClient = new WebClient())
        {
            webClient.Headers.Add("Content-Type", "application/json");
            webClient.UploadString(scheduledEventsEndpoint, jsonPost);
        }
    }
}
```

<span data-ttu-id="bb81f-208">Запланированные события может быть представлен с помощью hello следующие структуры данных.</span><span class="sxs-lookup"><span data-stu-id="bb81f-208">Scheduled Events can be represented using hello following data structures:</span></span>

```csharp
public class ScheduledEventsDocument
{
    public string DocumentIncarnation;
    public List<CloudControlEvent> Events { get; set; }
}

public class CloudControlEvent
{
    public string EventId { get; set; }
    public string EventStatus { get; set; }
    public string EventType { get; set; }
    public string ResourceType { get; set; }
    public List<string> Resources { get; set; }
    public DateTime? NotBefore { get; set; }
}

public class ScheduledEventsApproval
{
    public string DocumentIncarnation;
    public List<StartRequest> StartRequests = new List<StartRequest>();
}

public class StartRequest
{
    [JsonProperty("EventId")]
    private string eventId;

    public StartRequest(string eventId)
    {
        this.eventId = eventId;
    }
}
```

<span data-ttu-id="bb81f-209">Hello следующие примеры запросов hello метаданные службы для запланированных событий и утверждает каждого необработанные события.</span><span class="sxs-lookup"><span data-stu-id="bb81f-209">hello following sample queries hello metadata service for scheduled events and approves each outstanding event.</span></span>

```csharp
public class Program
{
    static ScheduledEventsClient client;

    static void Main(string[] args)
    {
        client = new ScheduledEventsClient();

        while (true)
        {
            string json = client.GetDocument();
            ScheduledEventsDocument scheduledEventsDocument = JsonConvert.DeserializeObject<ScheduledEventsDocument>(json);

            HandleEvents(scheduledEventsDocument.Events);

            // Wait for user response
            Console.WriteLine("Press Enter tooapprove executing events\n");
            Console.ReadLine();

            // Approve events
            ScheduledEventsApproval scheduledEventsApprovalDocument = new ScheduledEventsApproval()
            {
                DocumentIncarnation = scheduledEventsDocument.DocumentIncarnation
            };
        
            foreach (CloudControlEvent event in scheduledEventsDocument.Events)
            {
                scheduledEventsApprovalDocument.StartRequests.Add(new StartRequest(event.EventId));
            }

            if (scheduledEventsApprovalDocument.StartRequests.Count > 0)
            {
                // Serialize using Newtonsoft.Json
                string approveEventsJsonDocument =
                    JsonConvert.SerializeObject(scheduledEventsApprovalDocument);

                Console.WriteLine($"Approving events with json: {approveEventsJsonDocument}\n");
                client.ApproveScheduledEvents(approveEventsJsonDocument);
            }

            Console.WriteLine("Complete. Press enter toorepeat\n\n");
            Console.ReadLine();
            Console.Clear();
        }
    }

    private static void HandleEvents(List<CloudControlEvent> events)
    {
        // Add logic for handling events here
    }
}
```

## <a name="python-sample"></a><span data-ttu-id="bb81f-210">Пример на языке Python</span><span class="sxs-lookup"><span data-stu-id="bb81f-210">Python sample</span></span> 

<span data-ttu-id="bb81f-211">Hello следующие примеры запросов hello метаданные службы для запланированных событий и утверждает каждого необработанные события.</span><span class="sxs-lookup"><span data-stu-id="bb81f-211">hello following sample queries hello metadata service for scheduled events and approves each outstanding event.</span></span>

```python
#!/usr/bin/python

import json
import urllib2
import socket
import sys

metadata_url = "http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01"
headers = "{Metadata:true}"
this_host = socket.gethostname()

def get_scheduled_events():
   req = urllib2.Request(metadata_url)
   req.add_header('Metadata', 'true')
   resp = urllib2.urlopen(req)
   data = json.loads(resp.read())
   return data

def handle_scheduled_events(data):
    for evt in data['Events']:
        eventid = evt['EventId']
        status = evt['EventStatus']
        resources = evt['Resources']
        eventtype = evt['EventType']
        resourcetype = evt['ResourceType']
        notbefore = evt['NotBefore'].replace(" ","_")
        if this_host in resources:
            print "+ Scheduled Event. This host is scheduled for " + eventype + " not before " + notbefore
            # Add logic for handling events here

def main():
   data = get_scheduled_events()
   handle_scheduled_events(data)
   
if __name__ == '__main__':
  main()
  sys.exit(0)
```

## <a name="next-steps"></a><span data-ttu-id="bb81f-212">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="bb81f-212">Next steps</span></span> 

- <span data-ttu-id="bb81f-213">Дополнительные сведения о hello API-интерфейса в hello [метаданные экземпляра службы](instance-metadata-service.md).</span><span class="sxs-lookup"><span data-stu-id="bb81f-213">Read more about hello APIs available in hello [Instance Metadata service](instance-metadata-service.md).</span></span>
- <span data-ttu-id="bb81f-214">Подробнее о [плановом обслуживании виртуальных машин Windows в Azure](planned-maintenance.md).</span><span class="sxs-lookup"><span data-stu-id="bb81f-214">Learn about [planned maintenance for Windows virtual machines in Azure](planned-maintenance.md).</span></span>

