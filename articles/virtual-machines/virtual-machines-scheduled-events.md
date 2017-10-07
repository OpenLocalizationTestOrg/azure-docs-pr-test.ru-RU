---
title: "aaaScheduled события с помощью метаданных службы Azure | Документы Microsoft"
description: "Ответ tooImpactful события на виртуальной машине до их возникновения."
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
ms.date: 12/10/2016
ms.author: zivr
ms.openlocfilehash: b5c0849958c3ab48fa9c2cbff7db62f2e9d7daf1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-metadata-service---scheduled-events-preview"></a><span data-ttu-id="8ef66-103">Служба метаданных Azure. Запланированные события (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="8ef66-103">Azure Metadata Service - Scheduled Events (Preview)</span></span>

> [!NOTE] 
> <span data-ttu-id="8ef66-104">Предварительный просмотр вносятся доступных tooyou, вы принимаете условия использования toohello условие hello.</span><span class="sxs-lookup"><span data-stu-id="8ef66-104">Previews are made available tooyou on hello condition that you agree toohello terms of use.</span></span> <span data-ttu-id="8ef66-105">Дополнительные сведения см. в статье [Дополнительные условия использования предварительных выпусков Microsoft Azure](https://azure.microsoft.com/en-us/support/legal/preview-supplemental-terms/).</span><span class="sxs-lookup"><span data-stu-id="8ef66-105">For more information, see [Microsoft Azure Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/en-us/support/legal/preview-supplemental-terms/).</span></span>
>

<span data-ttu-id="8ef66-106">Запланированные события является одним из subservices hello под hello Azure метаданных службы.</span><span class="sxs-lookup"><span data-stu-id="8ef66-106">Scheduled Events is one of hello subservices under hello Azure Metadata Service.</span></span> <span data-ttu-id="8ef66-107">Она предоставляет сведения о предстоящих событиях (например, перезагрузках), что позволяет приложениям подготовиться к ним и уменьшить влияние на работу.</span><span class="sxs-lookup"><span data-stu-id="8ef66-107">It is responsible for surfacing information regarding upcoming events (for example, reboot) so your application can prepare for them and limit disruption.</span></span> <span data-ttu-id="8ef66-108">Эти сведения доступны для всех типов виртуальных машин Azure, включая PaaS и IaaS.</span><span class="sxs-lookup"><span data-stu-id="8ef66-108">It is available for all Azure Virtual Machine types including PaaS and IaaS.</span></span> <span data-ttu-id="8ef66-109">Запланированные события предоставляет виртуальную машину времени задачи профилактического tooperform эффект hello toominimize события.</span><span class="sxs-lookup"><span data-stu-id="8ef66-109">Scheduled Events gives your Virtual Machine time tooperform preventive tasks toominimize hello effect of an event.</span></span> 

## <a name="introduction---why-scheduled-events"></a><span data-ttu-id="8ef66-110">Введение. Зачем использовать запланированные события?</span><span class="sxs-lookup"><span data-stu-id="8ef66-110">Introduction - Why Scheduled Events?</span></span>

<span data-ttu-id="8ef66-111">С запланированные события можно предпринять шаги hello влияние toolimit intiated платформы обслуживания или действия, инициируемые пользователем в службе.</span><span class="sxs-lookup"><span data-stu-id="8ef66-111">With Scheduled Events, you can take steps toolimit hello impact of platform-intiated maintenance or user-initiated actions on your service.</span></span> 

<span data-ttu-id="8ef66-112">Несколькими экземплярами рабочих нагрузок, которые используют состояние toomaintain методы репликации, могут быть уязвимыми toooutages происходит между несколькими экземплярами.</span><span class="sxs-lookup"><span data-stu-id="8ef66-112">Multi-instance workloads, which use replication techniques toomaintain state, may be vulnerable toooutages happening across multiple instances.</span></span> <span data-ttu-id="8ef66-113">Такие простои могут потребовать дорогостоящих действий (например, перестроения индексов) или привести к потере реплики.</span><span class="sxs-lookup"><span data-stu-id="8ef66-113">Such outages may result in expensive tasks (for example, rebuilding indexes) or even a replica loss.</span></span> 

<span data-ttu-id="8ef66-114">Во многих других случаях hello общую доступность службы может быть повышена путем выполнения последовательность отключения, таких как завершение (или отменяемое) транзакции на лету, переназначение задачи tooother виртуальных машин в кластере hello (отработка отказа вручную) или удаление hello Виртуальную машину из пула подсистемы балансировки нагрузки сети.</span><span class="sxs-lookup"><span data-stu-id="8ef66-114">In many other cases, hello overall service availability may be improved by performing a graceful shutdown sequence such as completing (or canceling) in-flight transactions, reassigning tasks tooother VMs in hello cluster (manual failover), or removing hello Virtual Machine from a network load balancer pool.</span></span> 

<span data-ttu-id="8ef66-115">Существуют случаи, где обращения к администратору о предстоящих событий или ведение журнала такого события помочь повышение hello удобство обслуживания приложений, размещенных в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="8ef66-115">There are cases where notifying an administrator about an upcoming event or logging such an event help improving hello serviceability of applications hosted in hello cloud.</span></span>

<span data-ttu-id="8ef66-116">Варианты использования Azure служба метаданных поверхности запланированные события в hello ниже:</span><span class="sxs-lookup"><span data-stu-id="8ef66-116">Azure Metadata Service surfaces Scheduled Events in hello following use cases:</span></span>
-   <span data-ttu-id="8ef66-117">Инициируемое платформой обслуживание (например, развертывание ОС узла).</span><span class="sxs-lookup"><span data-stu-id="8ef66-117">Platform initiated maintenance (for example, Host OS rollout)</span></span>
-   <span data-ttu-id="8ef66-118">Инициируемые пользователем вызовы (например, пользователь перезапускает или повторно развертывает виртуальную машину).</span><span class="sxs-lookup"><span data-stu-id="8ef66-118">User-initiated calls (for example, user restarts or redeploys a VM)</span></span>


## <a name="scheduled-events---hello-basics"></a><span data-ttu-id="8ef66-119">Запланированные события - hello основы</span><span class="sxs-lookup"><span data-stu-id="8ef66-119">Scheduled Events - hello Basics</span></span>  

<span data-ttu-id="8ef66-120">Azure служба метаданных предоставляет сведения о запуске виртуальных машин с помощью конечной точки REST, доступный из hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="8ef66-120">Azure Metadata service exposes information about running Virtual Machines using a REST Endpoint accessible from within hello VM.</span></span> <span data-ttu-id="8ef66-121">сведения о Hello доступна через немаршрутизируемый IP, чтобы она не предоставляется вне hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="8ef66-121">hello information is available via a non-routable IP so that it is not exposed outside hello VM.</span></span>

### <a name="scope"></a><span data-ttu-id="8ef66-122">Область</span><span class="sxs-lookup"><span data-stu-id="8ef66-122">Scope</span></span>
<span data-ttu-id="8ef66-123">Запланированные события, отображается tooall виртуальных машин в облачной службе или tooall виртуальных машин в группе доступности.</span><span class="sxs-lookup"><span data-stu-id="8ef66-123">Scheduled events are surfaced tooall Virtual Machines in a cloud service or tooall Virtual Machines in an Availability Set.</span></span> <span data-ttu-id="8ef66-124">Поэтому следует проверить hello `Resources` в tooidentify событий hello, в которой виртуальные машины будут затронуты toobe.</span><span class="sxs-lookup"><span data-stu-id="8ef66-124">As a result, you should check hello `Resources` field in hello event tooidentify which VMs are going toobe impacted.</span></span> 

### <a name="discovering-hello-endpoint"></a><span data-ttu-id="8ef66-125">Обнаружение hello конечной точки</span><span class="sxs-lookup"><span data-stu-id="8ef66-125">Discovering hello Endpoint</span></span>
<span data-ttu-id="8ef66-126">В случае hello, где создается виртуальной машины в виртуальной сети (VNet), служба метаданных hello доступна из статический немаршрутизируемый IP- `169.254.169.254`.</span><span class="sxs-lookup"><span data-stu-id="8ef66-126">In hello case where a Virtual Machine is created within a Virtual Network (VNet), hello metadata service is available from a static non-routable IP, `169.254.169.254`.</span></span>
<span data-ttu-id="8ef66-127">Если hello виртуальной машины в виртуальной сети вариантов по умолчанию hello для облачных служб и классические ВМ не создается дополнительная логика является toouse конечной точки требуется toodiscover hello.</span><span class="sxs-lookup"><span data-stu-id="8ef66-127">If hello Virtual Machine is not created within a Virtual Network, hello default cases for cloud services and classic VMs, additional logic is required toodiscover hello endpoint toouse.</span></span> <span data-ttu-id="8ef66-128">См. Образец toolearn toothis как слишком[обнаружение конечной точки узлов hello](https://github.com/azure-samples/virtual-machines-python-scheduled-events-discover-endpoint-for-non-vnet-vm).</span><span class="sxs-lookup"><span data-stu-id="8ef66-128">Refer toothis sample toolearn how too[discover hello host endpoint](https://github.com/azure-samples/virtual-machines-python-scheduled-events-discover-endpoint-for-non-vnet-vm).</span></span>

### <a name="versioning"></a><span data-ttu-id="8ef66-129">Управление версиями</span><span class="sxs-lookup"><span data-stu-id="8ef66-129">Versioning</span></span> 
<span data-ttu-id="8ef66-130">Hello метаданных экземпляра службы с версиями.</span><span class="sxs-lookup"><span data-stu-id="8ef66-130">hello Instance Metadata Service is versioned.</span></span> <span data-ttu-id="8ef66-131">Версии являются обязательными, и текущая версия hello `2017-03-01`.</span><span class="sxs-lookup"><span data-stu-id="8ef66-131">Versions are mandatory and hello current version is `2017-03-01`.</span></span>

> [!NOTE] 
> <span data-ttu-id="8ef66-132">Предыдущие выпуски Предварительный просмотр поддерживается {последние} в качестве hello api-version запланированные события.</span><span class="sxs-lookup"><span data-stu-id="8ef66-132">Previous preview releases of scheduled events supported {latest} as hello api-version.</span></span> <span data-ttu-id="8ef66-133">Этот формат не поддерживается и будет считаться устаревшей в будущем hello.</span><span class="sxs-lookup"><span data-stu-id="8ef66-133">This format is no longer supported and will be deprecated in hello future.</span></span>

### <a name="using-headers"></a><span data-ttu-id="8ef66-134">Использование заголовков</span><span class="sxs-lookup"><span data-stu-id="8ef66-134">Using Headers</span></span>
<span data-ttu-id="8ef66-135">При запросе hello метаданных службы, необходимо указать заголовок hello `Metadata: true` tooensure hello запрос не был перенаправлен непреднамеренно.</span><span class="sxs-lookup"><span data-stu-id="8ef66-135">When you query hello Metadata Service, you must provide hello header `Metadata: true` tooensure hello request was not unintentionally redirected.</span></span>

### <a name="enabling-scheduled-events"></a><span data-ttu-id="8ef66-136">Включение запланированных событий</span><span class="sxs-lookup"><span data-stu-id="8ef66-136">Enabling Scheduled Events</span></span>
<span data-ttu-id="8ef66-137">Hello при первом запуске запроса для запланированных событий Azure неявно включает hello функцию на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="8ef66-137">hello first time you make a request for scheduled events, Azure implicitly enables hello feature on your Virtual Machine.</span></span> <span data-ttu-id="8ef66-138">Поэтому следует ожидать задержки ответа в первом вызове из копии tootwo минут.</span><span class="sxs-lookup"><span data-stu-id="8ef66-138">As a result, you should expect a delayed response in your first call of up tootwo minutes.</span></span>

### <a name="user-initiated-maintenance"></a><span data-ttu-id="8ef66-139">Обслуживание, инициированное пользователем</span><span class="sxs-lookup"><span data-stu-id="8ef66-139">User Initiated Maintenance</span></span>
<span data-ttu-id="8ef66-140">Пользователь запустил обслуживание виртуальных машин через hello портал Azure API, CLI, или PowerShell приведет к запланированные события.</span><span class="sxs-lookup"><span data-stu-id="8ef66-140">User initiated virtual machine maintenance via hello Azure portal, API, CLI, or PowerShell will result in Scheduled Events.</span></span> <span data-ttu-id="8ef66-141">Это позволяет tootest hello обслуживания подготовки логики в приложении а tooprepare вашего приложения для обслуживания инициированной пользователем.</span><span class="sxs-lookup"><span data-stu-id="8ef66-141">This allows you tootest hello maintenance preparation logic in your application and allows your application tooprepare for user initiated maintenance.</span></span>

<span data-ttu-id="8ef66-142">При перезапуске виртуальной машины планируется событие с типом `Reboot`.</span><span class="sxs-lookup"><span data-stu-id="8ef66-142">Restarting a virtual machine will schedule an event with type `Reboot`.</span></span> <span data-ttu-id="8ef66-143">При повторном развертыванию виртуальной машины планируется событие с типом `Redeploy`.</span><span class="sxs-lookup"><span data-stu-id="8ef66-143">Redeploying a virtual machine will schedule an event with type `Redeploy`.</span></span>

> [!NOTE] 
> <span data-ttu-id="8ef66-144">Сейчас можно одновременно запланировать более десяти операций обслуживания, инициированных пользователем.</span><span class="sxs-lookup"><span data-stu-id="8ef66-144">Currently a maximum of 10 user initiated maintenance operations can be simultaneously scheduled.</span></span> <span data-ttu-id="8ef66-145">Это ограничение будет снято еще до выпуска общедоступной версии запланированных событий.</span><span class="sxs-lookup"><span data-stu-id="8ef66-145">This limit will be relaxed before Scheduled Events General Availability.</span></span>

> [!NOTE] 
> <span data-ttu-id="8ef66-146">Сейчас обслуживание, инициированное пользователем, которое влияет на запланированные события, не настраивается.</span><span class="sxs-lookup"><span data-stu-id="8ef66-146">Currently user initiated maintenance resulting in Scheduled Events is not configurable.</span></span> <span data-ttu-id="8ef66-147">Возможность настройки запланирована к следующему выпуску.</span><span class="sxs-lookup"><span data-stu-id="8ef66-147">Configurability is planned for a future release.</span></span>

## <a name="using-hello-api"></a><span data-ttu-id="8ef66-148">С помощью hello API</span><span class="sxs-lookup"><span data-stu-id="8ef66-148">Using hello API</span></span>

### <a name="query-for-events"></a><span data-ttu-id="8ef66-149">Запрос сведений о событиях</span><span class="sxs-lookup"><span data-stu-id="8ef66-149">Query for events</span></span>
<span data-ttu-id="8ef66-150">Вы можете запрашивать запланированные события, просто выполнив hello следующий вызов:</span><span class="sxs-lookup"><span data-stu-id="8ef66-150">You can query for Scheduled Events simply by making hello following call:</span></span>

```
curl -H Metadata:true http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01
```

<span data-ttu-id="8ef66-151">Ответ содержит массив запланированных событий.</span><span class="sxs-lookup"><span data-stu-id="8ef66-151">A response contains an array of scheduled events.</span></span> <span data-ttu-id="8ef66-152">Если это будет пустой массив, значит сейчас запланированных событий нет.</span><span class="sxs-lookup"><span data-stu-id="8ef66-152">An empty array means that there are currently no events scheduled.</span></span>
<span data-ttu-id="8ef66-153">В случае hello которых запланированные события, hello ответ содержит массив событий:</span><span class="sxs-lookup"><span data-stu-id="8ef66-153">In hello case where there are scheduled events, hello response contains an array of events:</span></span> 
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

### <a name="event-properties"></a><span data-ttu-id="8ef66-154">Свойства события</span><span class="sxs-lookup"><span data-stu-id="8ef66-154">Event Properties</span></span>
|<span data-ttu-id="8ef66-155">Свойство</span><span class="sxs-lookup"><span data-stu-id="8ef66-155">Property</span></span>  |  <span data-ttu-id="8ef66-156">Описание</span><span class="sxs-lookup"><span data-stu-id="8ef66-156">Description</span></span> |
| - | - |
| <span data-ttu-id="8ef66-157">EventId</span><span class="sxs-lookup"><span data-stu-id="8ef66-157">EventId</span></span> | <span data-ttu-id="8ef66-158">Глобальный уникальный идентификатор этого события.</span><span class="sxs-lookup"><span data-stu-id="8ef66-158">Globally unique identifier for this event.</span></span> <br><br> <span data-ttu-id="8ef66-159">Пример:</span><span class="sxs-lookup"><span data-stu-id="8ef66-159">Example:</span></span> <br><ul><li><span data-ttu-id="8ef66-160">602d9444-d2cd-49c7-8624-8643e7171297</span><span class="sxs-lookup"><span data-stu-id="8ef66-160">602d9444-d2cd-49c7-8624-8643e7171297</span></span>  |
| <span data-ttu-id="8ef66-161">EventType</span><span class="sxs-lookup"><span data-stu-id="8ef66-161">EventType</span></span> | <span data-ttu-id="8ef66-162">Влияние, которое оказывает это событие.</span><span class="sxs-lookup"><span data-stu-id="8ef66-162">Impact this event causes.</span></span> <br><br> <span data-ttu-id="8ef66-163">Значения:</span><span class="sxs-lookup"><span data-stu-id="8ef66-163">Values:</span></span> <br><ul><li> <span data-ttu-id="8ef66-164">`Freeze`: hello виртуальной машины — запланированных toopause несколько секунд.</span><span class="sxs-lookup"><span data-stu-id="8ef66-164">`Freeze`: hello Virtual Machine is scheduled toopause for few seconds.</span></span> <span data-ttu-id="8ef66-165">Hello ЦП будет приостановлена, но не влияет на открытые файлы, сетевые подключения или оперативной памяти.</span><span class="sxs-lookup"><span data-stu-id="8ef66-165">hello CPU will be suspended, but there is no impact on memory, open files, or network connections.</span></span> <li><span data-ttu-id="8ef66-166">`Reboot`: hello запланирована перезагрузка виртуальной машины (непостоянные памяти теряются).</span><span class="sxs-lookup"><span data-stu-id="8ef66-166">`Reboot`: hello Virtual Machine is scheduled for reboot (non-persistent memory is lost).</span></span> <li><span data-ttu-id="8ef66-167">`Redeploy`: hello виртуальной машины является узлом tooanother запланированных toomove (временных дисков теряются).</span><span class="sxs-lookup"><span data-stu-id="8ef66-167">`Redeploy`: hello Virtual Machine is scheduled toomove tooanother node (ephemeral disks are lost).</span></span> |
| <span data-ttu-id="8ef66-168">ResourceType</span><span class="sxs-lookup"><span data-stu-id="8ef66-168">ResourceType</span></span> | <span data-ttu-id="8ef66-169">Тип ресурса, на который влияет это событие.</span><span class="sxs-lookup"><span data-stu-id="8ef66-169">Type of resource this event impacts.</span></span> <br><br> <span data-ttu-id="8ef66-170">Значения:</span><span class="sxs-lookup"><span data-stu-id="8ef66-170">Values:</span></span> <ul><li>`VirtualMachine`|
| <span data-ttu-id="8ef66-171">Ресурсы</span><span class="sxs-lookup"><span data-stu-id="8ef66-171">Resources</span></span>| <span data-ttu-id="8ef66-172">Список ресурсов, на которые влияет это событие.</span><span class="sxs-lookup"><span data-stu-id="8ef66-172">List of resources this event impacts.</span></span> <span data-ttu-id="8ef66-173">Это гарантируется машины toocontain из не более одного [домен обновления](windows/manage-availability.md), но не может содержать все машины в hello UD.</span><span class="sxs-lookup"><span data-stu-id="8ef66-173">This is guaranteed toocontain machines from at most one [Update Domain](windows/manage-availability.md), but may not contain all machines in hello UD.</span></span> <br><br> <span data-ttu-id="8ef66-174">Пример:</span><span class="sxs-lookup"><span data-stu-id="8ef66-174">Example:</span></span> <br><ul><li> <span data-ttu-id="8ef66-175">["FrontEnd_IN_0", "BackEnd_IN_0"]</span><span class="sxs-lookup"><span data-stu-id="8ef66-175">["FrontEnd_IN_0", "BackEnd_IN_0"]</span></span> |
| <span data-ttu-id="8ef66-176">Event Status</span><span class="sxs-lookup"><span data-stu-id="8ef66-176">Event Status</span></span> | <span data-ttu-id="8ef66-177">Состояние этого события.</span><span class="sxs-lookup"><span data-stu-id="8ef66-177">Status of this event.</span></span> <br><br> <span data-ttu-id="8ef66-178">Значения:</span><span class="sxs-lookup"><span data-stu-id="8ef66-178">Values:</span></span> <ul><li><span data-ttu-id="8ef66-179">`Scheduled`: Это событие является запланированных toostart после hello времени, указанного в hello `NotBefore` свойство.</span><span class="sxs-lookup"><span data-stu-id="8ef66-179">`Scheduled`: This event is scheduled toostart after hello time specified in hello `NotBefore` property.</span></span><li><span data-ttu-id="8ef66-180">`Started`. Это событие запущено.</span><span class="sxs-lookup"><span data-stu-id="8ef66-180">`Started`: This event has started.</span></span></ul> <span data-ttu-id="8ef66-181">Не `Completed` или когда-либо предоставляется как состояние; hello событие больше не возвращаются при завершении события hello.</span><span class="sxs-lookup"><span data-stu-id="8ef66-181">No `Completed` or similar status is ever provided; hello event will no longer be returned when hello event is completed.</span></span>
| <span data-ttu-id="8ef66-182">NotBefore</span><span class="sxs-lookup"><span data-stu-id="8ef66-182">NotBefore</span></span>| <span data-ttu-id="8ef66-183">Время, после которого может быть запущено это событие.</span><span class="sxs-lookup"><span data-stu-id="8ef66-183">Time after which this event may start.</span></span> <br><br> <span data-ttu-id="8ef66-184">Пример:</span><span class="sxs-lookup"><span data-stu-id="8ef66-184">Example:</span></span> <br><ul><li> <span data-ttu-id="8ef66-185">2016-09-19T18:29:47Z</span><span class="sxs-lookup"><span data-stu-id="8ef66-185">2016-09-19T18:29:47Z</span></span>  |

### <a name="event-scheduling"></a><span data-ttu-id="8ef66-186">Планирование события</span><span class="sxs-lookup"><span data-stu-id="8ef66-186">Event Scheduling</span></span>
<span data-ttu-id="8ef66-187">Каждое событие запланирована минимальное количество времени в будущем hello в зависимости от типа события.</span><span class="sxs-lookup"><span data-stu-id="8ef66-187">Each event is scheduled a minimum amount of time in hello future based on event type.</span></span> <span data-ttu-id="8ef66-188">Это время отражается в свойстве события `NotBefore`.</span><span class="sxs-lookup"><span data-stu-id="8ef66-188">This time is reflected in an event's `NotBefore` property.</span></span> 

|<span data-ttu-id="8ef66-189">EventType</span><span class="sxs-lookup"><span data-stu-id="8ef66-189">EventType</span></span>  | <span data-ttu-id="8ef66-190">Минимальное время уведомления</span><span class="sxs-lookup"><span data-stu-id="8ef66-190">Minimum Notice</span></span> |
| - | - |
| <span data-ttu-id="8ef66-191">Freeze</span><span class="sxs-lookup"><span data-stu-id="8ef66-191">Freeze</span></span>| <span data-ttu-id="8ef66-192">15 минут</span><span class="sxs-lookup"><span data-stu-id="8ef66-192">15 minutes</span></span> |
| <span data-ttu-id="8ef66-193">Reboot</span><span class="sxs-lookup"><span data-stu-id="8ef66-193">Reboot</span></span> | <span data-ttu-id="8ef66-194">15 минут</span><span class="sxs-lookup"><span data-stu-id="8ef66-194">15 minutes</span></span> |
| <span data-ttu-id="8ef66-195">Повторное развертывание</span><span class="sxs-lookup"><span data-stu-id="8ef66-195">Redeploy</span></span> | <span data-ttu-id="8ef66-196">10 минут</span><span class="sxs-lookup"><span data-stu-id="8ef66-196">10 minutes</span></span> |

### <a name="starting-an-event-expedite"></a><span data-ttu-id="8ef66-197">Запуск (ускорение) события</span><span class="sxs-lookup"><span data-stu-id="8ef66-197">Starting an event (expedite)</span></span>

<span data-ttu-id="8ef66-198">Как только вы узнали о предстоящих событий и завершили свою логику для нормальное завершение работы, вы можете утвердить необработанных событий hello, делая `POST` вызова toohello метаданные службы с hello `EventId`.</span><span class="sxs-lookup"><span data-stu-id="8ef66-198">Once you have learned of an upcoming event and completed your logic for graceful shutdown, you can approve hello outstanding event by making a `POST` call toohello metadata service with hello `EventId`.</span></span> <span data-ttu-id="8ef66-199">Указывает tooAzure, он может сократить минимальное уведомления hello время (если возможно).</span><span class="sxs-lookup"><span data-stu-id="8ef66-199">This indicates tooAzure that it can shorten hello minimum notification time (when possible).</span></span> 

```
curl -H Metadata:true -X POST -d '{"DocumentIncarnation":"5", "StartRequests": [{"EventId": "f020ba2e-3bc0-4c40-a10b-86575a9eabd5"}]}' http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01
```

> [!NOTE] 
> <span data-ttu-id="8ef66-200">Подтверждение событий позволит hello tooproceed событий для всех `Resources` в событии hello не только hello виртуальную машину, которая подтверждает hello событий.</span><span class="sxs-lookup"><span data-stu-id="8ef66-200">Acknowledging a event will allow hello event tooproceed for all `Resources` in hello event, not just hello virtual machine that acknowledges hello event.</span></span> <span data-ttu-id="8ef66-201">Таким образом можно tooelect подтверждение hello руководитель toocoordinate, которое может быть простым как первой машине hello в hello `Resources` поля.</span><span class="sxs-lookup"><span data-stu-id="8ef66-201">You may therefore choose tooelect a leader toocoordinate hello acknowledgement, which may be as simple as hello first machine in hello `Resources` field.</span></span>

## <a name="samples"></a><span data-ttu-id="8ef66-202">Примеры</span><span class="sxs-lookup"><span data-stu-id="8ef66-202">Samples</span></span>

### <a name="powershell-sample"></a><span data-ttu-id="8ef66-203">Пример для PowerShell</span><span class="sxs-lookup"><span data-stu-id="8ef66-203">PowerShell Sample</span></span> 

<span data-ttu-id="8ef66-204">Hello следующие примеры запросов hello метаданные службы для запланированных событий и утверждает каждого необработанные события.</span><span class="sxs-lookup"><span data-stu-id="8ef66-204">hello following sample queries hello metadata service for scheduled events and approves each outstanding event.</span></span>

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


### <a name="c-sample"></a><span data-ttu-id="8ef66-205">Пример на языке C\#</span><span class="sxs-lookup"><span data-stu-id="8ef66-205">C\# Sample</span></span> 

<span data-ttu-id="8ef66-206">Hello следующий пример является простой клиента, которая взаимодействует со службой метаданных hello.</span><span class="sxs-lookup"><span data-stu-id="8ef66-206">hello following sample is of a simple client that communicates with hello metadata service.</span></span>

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

<span data-ttu-id="8ef66-207">Запланированные события может быть представлен с помощью hello следующие структуры данных.</span><span class="sxs-lookup"><span data-stu-id="8ef66-207">Scheduled Events can be represented using hello following data structures:</span></span>

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

<span data-ttu-id="8ef66-208">Hello следующие примеры запросов hello метаданные службы для запланированных событий и утверждает каждого необработанные события.</span><span class="sxs-lookup"><span data-stu-id="8ef66-208">hello following sample queries hello metadata service for scheduled events and approves each outstanding event.</span></span>

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

### <a name="python-sample"></a><span data-ttu-id="8ef66-209">Пример на Python</span><span class="sxs-lookup"><span data-stu-id="8ef66-209">Python Sample</span></span> 

<span data-ttu-id="8ef66-210">Hello следующие примеры запросов hello метаданные службы для запланированных событий и утверждает каждого необработанные события.</span><span class="sxs-lookup"><span data-stu-id="8ef66-210">hello following sample queries hello metadata service for scheduled events and approves each outstanding event.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="8ef66-211">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8ef66-211">Next Steps</span></span> 

- <span data-ttu-id="8ef66-212">Дополнительные сведения о hello API-интерфейса в hello [экземпляр метаданных службы](virtual-machines-instancemetadataservice-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8ef66-212">Read more about hello APIs available in hello [instance metadata service](virtual-machines-instancemetadataservice-overview.md).</span></span>
- <span data-ttu-id="8ef66-213">Подробнее о [плановом обслуживании виртуальных машин Windows в Azure](windows/planned-maintenance.md).</span><span class="sxs-lookup"><span data-stu-id="8ef66-213">Learn about [planned maintenance for Windows virtual machines in Azure](windows/planned-maintenance.md).</span></span>
- <span data-ttu-id="8ef66-214">Подробнее о [плановом обслуживании виртуальных машин Linux в Azure](linux/planned-maintenance.md).</span><span class="sxs-lookup"><span data-stu-id="8ef66-214">Learn about [planned maintenance for Linux virtual machines in Azure](linux/planned-maintenance.md).</span></span>
