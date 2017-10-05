---
title: "Запланированные события для виртуальных машин Linux в Azure | Документация Майкрософт"
description: "Запланированные события, использующие службу метаданных Azure, для виртуальных машин Linux."
services: virtual-machines-windows, virtual-machines-linux, cloud-services
documentationcenter: 
author: zivraf
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/14/2017
ms.author: zivr
ms.openlocfilehash: 75e509a7e39f5b268ce550d0c4dea2261d4fe56f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="azure-metadata-service-scheduled-events-preview-for-linux-vms"></a><span data-ttu-id="2de53-103">Служба метаданных Azure. Запланированные события (предварительная версия) для виртуальных машин Linux</span><span class="sxs-lookup"><span data-stu-id="2de53-103">Azure Metadata Service: Scheduled Events (Preview) for Linux VMs</span></span>

> [!NOTE] 
> <span data-ttu-id="2de53-104">Предварительные версии предоставляются при условии, что вы соглашаетесь с условиями использования.</span><span class="sxs-lookup"><span data-stu-id="2de53-104">Previews are made available to you on the condition that you agree to the terms of use.</span></span> <span data-ttu-id="2de53-105">Дополнительные сведения см. в статье [Дополнительные условия использования предварительных выпусков Microsoft Azure](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).</span><span class="sxs-lookup"><span data-stu-id="2de53-105">For more information, see [Microsoft Azure Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).</span></span>
>

<span data-ttu-id="2de53-106">"Запланированные события" — одна из вспомогательных служб службы метаданных Azure.</span><span class="sxs-lookup"><span data-stu-id="2de53-106">Scheduled Events is one of the subservices under the Azure Metadata Service.</span></span> <span data-ttu-id="2de53-107">Она предоставляет сведения о предстоящих событиях (например, перезагрузках), что позволяет приложениям подготовиться к ним и уменьшить влияние на работу.</span><span class="sxs-lookup"><span data-stu-id="2de53-107">It is responsible for surfacing information regarding upcoming events (for example, reboot) so your application can prepare for them and limit disruption.</span></span> <span data-ttu-id="2de53-108">Эти сведения доступны для всех типов виртуальных машин Azure, включая PaaS и IaaS.</span><span class="sxs-lookup"><span data-stu-id="2de53-108">It is available for all Azure Virtual Machine types including PaaS and IaaS.</span></span> <span data-ttu-id="2de53-109">Благодаря запланированным событиям виртуальная машина получает возможность выполнить упреждающие действия, чтобы свести влияние события к минимуму.</span><span class="sxs-lookup"><span data-stu-id="2de53-109">Scheduled Events gives your Virtual Machine time to perform preventive tasks to minimize the effect of an event.</span></span> 

<span data-ttu-id="2de53-110">Запланированные события доступны для виртуальных машин Windows и Linux.</span><span class="sxs-lookup"><span data-stu-id="2de53-110">Scheduled Events is available for both Windows and Linux VMs.</span></span> <span data-ttu-id="2de53-111">Сведения о запланированных событиях, назначенные в Windows, см. в статье [Служба метаданных Azure. Запланированные события (предварительная версия) для виртуальных машин Windows](../windows/scheduled-events.md).</span><span class="sxs-lookup"><span data-stu-id="2de53-111">For information about Scheduled Events on Windows, see [Scheduled Events for Windows VMs](../windows/scheduled-events.md).</span></span>

## <a name="why-scheduled-events"></a><span data-ttu-id="2de53-112">Зачем нужны запланированные события</span><span class="sxs-lookup"><span data-stu-id="2de53-112">Why Scheduled Events?</span></span>

<span data-ttu-id="2de53-113">Благодаря запланированным событиям вы можете принять меры по ограничению воздействия на службу обслуживания, инициируемого платформой, и действий, инициируемых пользователем.</span><span class="sxs-lookup"><span data-stu-id="2de53-113">With Scheduled Events, you can take steps to limit the impact of platform-intiated maintenance or user-initiated actions on your service.</span></span> 

<span data-ttu-id="2de53-114">Рабочие нагрузки с несколькими экземплярами, которые используют методы репликации для поддержания состояния, чувствительны к простоям на нескольких экземплярах.</span><span class="sxs-lookup"><span data-stu-id="2de53-114">Multi-instance workloads, which use replication techniques to maintain state, may be vulnerable to outages happening across multiple instances.</span></span> <span data-ttu-id="2de53-115">Такие простои могут потребовать дорогостоящих действий (например, перестроения индексов) или привести к потере реплики.</span><span class="sxs-lookup"><span data-stu-id="2de53-115">Such outages may result in expensive tasks (for example, rebuilding indexes) or even a replica loss.</span></span> 

<span data-ttu-id="2de53-116">Во многих других случаях общая доступность службы может быть повышена, например путем выполнения последовательности нормального завершения работы, такой как завершение (или отмена) незавершенных транзакций, переназначение задач другим виртуальным машинам в кластере (отработка отказа вручную) или удаление виртуальной машины из пула подсистемы балансировки сетевой нагрузки.</span><span class="sxs-lookup"><span data-stu-id="2de53-116">In many other cases, the overall service availability may be improved by performing a graceful shutdown sequence such as completing (or canceling) in-flight transactions, reassigning tasks to other VMs in the cluster (manual failover), or removing the Virtual Machine from a network load balancer pool.</span></span> 

<span data-ttu-id="2de53-117">Иногда простое уведомление администратора о предстоящих событиях или занесение такого события в журнал позволяет повысить удобство обслуживания приложений, размещенных в облаке.</span><span class="sxs-lookup"><span data-stu-id="2de53-117">There are cases where notifying an administrator about an upcoming event or logging such an event help improving the serviceability of applications hosted in the cloud.</span></span>

<span data-ttu-id="2de53-118">Служба метаданных Azure сообщает о запланированных событиях в следующих случаях.</span><span class="sxs-lookup"><span data-stu-id="2de53-118">Azure Metadata Service surfaces Scheduled Events in the following use cases:</span></span>
-   <span data-ttu-id="2de53-119">Инициируемое платформой обслуживание (например, развертывание ОС узла).</span><span class="sxs-lookup"><span data-stu-id="2de53-119">Platform initiated maintenance (for example, Host OS rollout)</span></span>
-   <span data-ttu-id="2de53-120">Инициируемые пользователем вызовы (например, пользователь перезапускает или повторно развертывает виртуальную машину).</span><span class="sxs-lookup"><span data-stu-id="2de53-120">User-initiated calls (for example, user restarts or redeploys a VM)</span></span>


## <a name="the-basics"></a><span data-ttu-id="2de53-121">Основные сведения</span><span class="sxs-lookup"><span data-stu-id="2de53-121">The basics</span></span>  

<span data-ttu-id="2de53-122">Служба метаданных Azure предоставляет сведения о работающих виртуальных машинах через конечную точку REST, доступную из виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="2de53-122">Azure Metadata service exposes information about running Virtual Machines using a REST Endpoint accessible from within the VM.</span></span> <span data-ttu-id="2de53-123">Эта информация предоставляется через немаршрутизируемый IP-адрес, то есть она недоступна вне виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="2de53-123">The information is available via a non-routable IP so that it is not exposed outside the VM.</span></span>

### <a name="scope"></a><span data-ttu-id="2de53-124">Область</span><span class="sxs-lookup"><span data-stu-id="2de53-124">Scope</span></span>
<span data-ttu-id="2de53-125">Запланированные события отображаются на всех виртуальных машинах в облачной службе или на всех виртуальных машинах в группе доступности.</span><span class="sxs-lookup"><span data-stu-id="2de53-125">Scheduled events are surfaced to all Virtual Machines in a cloud service or to all Virtual Machines in an Availability Set.</span></span> <span data-ttu-id="2de53-126">Поэтому важно проверять поле `Resources` в событии, чтобы определить, на какие виртуальные машины повлияет конкретное событие.</span><span class="sxs-lookup"><span data-stu-id="2de53-126">As a result, you should check the `Resources` field in the event to identify which VMs are going to be impacted.</span></span> 

### <a name="discovering-the-endpoint"></a><span data-ttu-id="2de53-127">Обнаружение конечной точки</span><span class="sxs-lookup"><span data-stu-id="2de53-127">Discovering the endpoint</span></span>
<span data-ttu-id="2de53-128">Если виртуальная машина создана в виртуальной сети, служба метаданных доступна по статическому немаршрутизируемому IP-адресу `169.254.169.254`.</span><span class="sxs-lookup"><span data-stu-id="2de53-128">In the case where a Virtual Machine is created within a Virtual Network (VNet), the metadata service is available from a static non-routable IP, `169.254.169.254`.</span></span>
<span data-ttu-id="2de53-129">Если виртуальная машина не создается в виртуальной сети, что является стандартным сценарием для облачных служб и классических виртуальных машин, для обнаружения используемой конечной точки требуется дополнительная логика.</span><span class="sxs-lookup"><span data-stu-id="2de53-129">If the Virtual Machine is not created within a Virtual Network, the default cases for cloud services and classic VMs, additional logic is required to discover the endpoint to use.</span></span> <span data-ttu-id="2de53-130">Просмотрите этот пример, чтобы узнать как выполнить [обнаружение конечной точки узла](https://github.com/azure-samples/virtual-machines-python-scheduled-events-discover-endpoint-for-non-vnet-vm).</span><span class="sxs-lookup"><span data-stu-id="2de53-130">Refer to this sample to learn how to [discover the host endpoint](https://github.com/azure-samples/virtual-machines-python-scheduled-events-discover-endpoint-for-non-vnet-vm).</span></span>

### <a name="versioning"></a><span data-ttu-id="2de53-131">Управление версиями</span><span class="sxs-lookup"><span data-stu-id="2de53-131">Versioning</span></span> 
<span data-ttu-id="2de53-132">Для службы метаданных экземпляров включено управление версиями.</span><span class="sxs-lookup"><span data-stu-id="2de53-132">The Instance Metadata Service is versioned.</span></span> <span data-ttu-id="2de53-133">Версии являются обязательными. На данный момент используется версия от `2017-03-01`.</span><span class="sxs-lookup"><span data-stu-id="2de53-133">Versions are mandatory and the current version is `2017-03-01`.</span></span>

> [!NOTE] 
> <span data-ttu-id="2de53-134">В предыдущих выпусках предварительной версии в качестве api-version поддерживалось значение {latest}.</span><span class="sxs-lookup"><span data-stu-id="2de53-134">Previous preview releases of scheduled events supported {latest} as the api-version.</span></span> <span data-ttu-id="2de53-135">Этот формат больше не поддерживается и в дальнейшем будет считаться устаревшим.</span><span class="sxs-lookup"><span data-stu-id="2de53-135">This format is no longer supported and will be deprecated in the future.</span></span>

### <a name="using-headers"></a><span data-ttu-id="2de53-136">Использование заголовков</span><span class="sxs-lookup"><span data-stu-id="2de53-136">Using headers</span></span>
<span data-ttu-id="2de53-137">При запросе службы метаданных необходимо указать заголовок `Metadata: true`, чтобы избежать случайного перенаправления запроса.</span><span class="sxs-lookup"><span data-stu-id="2de53-137">When you query the Metadata Service, you must provide the header `Metadata: true` to ensure the request was not unintentionally redirected.</span></span>

### <a name="enabling-scheduled-events"></a><span data-ttu-id="2de53-138">Включение запланированных событий</span><span class="sxs-lookup"><span data-stu-id="2de53-138">Enabling Scheduled Events</span></span>
<span data-ttu-id="2de53-139">При первом создании запроса запланированных событий Azure неявно включает эту функцию на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="2de53-139">The first time you make a request for scheduled events, Azure implicitly enables the feature on your Virtual Machine.</span></span> <span data-ttu-id="2de53-140">Это означает, что при первом вызове возможна задержка с ответом длительностью до двух минут.</span><span class="sxs-lookup"><span data-stu-id="2de53-140">As a result, you should expect a delayed response in your first call of up to two minutes.</span></span>

### <a name="user-initiated-maintenance"></a><span data-ttu-id="2de53-141">Обслуживание, инициированное пользователем</span><span class="sxs-lookup"><span data-stu-id="2de53-141">User initiated maintenance</span></span>
<span data-ttu-id="2de53-142">Обслуживание виртуальных машин, инициированное пользователем на портале Azure, в API, Azure CLI или PowerShell, приведет к созданию запланированных событий.</span><span class="sxs-lookup"><span data-stu-id="2de53-142">User initiated virtual machine maintenance via the Azure portal, API, CLI, or PowerShell results in a scheduled event.</span></span> <span data-ttu-id="2de53-143">Это позволяет протестировать логику подготовки обслуживания в вашем приложении, а также позволит ему подготовиться к обслуживанию, инициированном пользователем.</span><span class="sxs-lookup"><span data-stu-id="2de53-143">This allows you to test the maintenance preparation logic in your application and allows your application to prepare for user initiated maintenance.</span></span>

<span data-ttu-id="2de53-144">При перезапуске виртуальной машины планируется событие с типом `Reboot`.</span><span class="sxs-lookup"><span data-stu-id="2de53-144">Restarting a virtual machine schedules an event with type `Reboot`.</span></span> <span data-ttu-id="2de53-145">При развертывании виртуальной машины планируется событие с типом `Redeploy`.</span><span class="sxs-lookup"><span data-stu-id="2de53-145">Redeploying a virtual machine schedules an event with type `Redeploy`.</span></span>

> [!NOTE] 
> <span data-ttu-id="2de53-146">Сейчас можно одновременно запланировать более десяти операций обслуживания, инициированных пользователем.</span><span class="sxs-lookup"><span data-stu-id="2de53-146">Currently a maximum of 10 user initiated maintenance operations can be simultaneously scheduled.</span></span> <span data-ttu-id="2de53-147">Это ограничение будет снято еще до выпуска общедоступной версии запланированных событий.</span><span class="sxs-lookup"><span data-stu-id="2de53-147">This limit will be relaxed before Scheduled Events general availability.</span></span>

> [!NOTE] 
> <span data-ttu-id="2de53-148">Сейчас обслуживание, инициированное пользователем, которое влияет на запланированные события, не настраивается.</span><span class="sxs-lookup"><span data-stu-id="2de53-148">Currently user initiated maintenance resulting in Scheduled Events is not configurable.</span></span> <span data-ttu-id="2de53-149">Возможность настройки запланирована к следующему выпуску.</span><span class="sxs-lookup"><span data-stu-id="2de53-149">Configurability is planned for a future release.</span></span>

## <a name="using-the-api"></a><span data-ttu-id="2de53-150">Использование API</span><span class="sxs-lookup"><span data-stu-id="2de53-150">Using the API</span></span>

### <a name="query-for-events"></a><span data-ttu-id="2de53-151">Запрос сведений о событиях</span><span class="sxs-lookup"><span data-stu-id="2de53-151">Query for events</span></span>
<span data-ttu-id="2de53-152">Чтобы получить сведения о запланированных событиях, достаточно отправить следующий запрос:</span><span class="sxs-lookup"><span data-stu-id="2de53-152">You can query for Scheduled Events simply by making the following call:</span></span>

```
curl -H Metadata:true http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01
```

<span data-ttu-id="2de53-153">Ответ содержит массив запланированных событий.</span><span class="sxs-lookup"><span data-stu-id="2de53-153">A response contains an array of scheduled events.</span></span> <span data-ttu-id="2de53-154">Если это будет пустой массив, значит сейчас запланированных событий нет.</span><span class="sxs-lookup"><span data-stu-id="2de53-154">An empty array means that there are currently no events scheduled.</span></span>
<span data-ttu-id="2de53-155">Если передаются запланированные события, массив событий в ответе выглядит так:</span><span class="sxs-lookup"><span data-stu-id="2de53-155">In the case where there are scheduled events, the response contains an array of events:</span></span> 
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

### <a name="event-properties"></a><span data-ttu-id="2de53-156">Свойства события</span><span class="sxs-lookup"><span data-stu-id="2de53-156">Event properties</span></span>
|<span data-ttu-id="2de53-157">Свойство</span><span class="sxs-lookup"><span data-stu-id="2de53-157">Property</span></span>  |  <span data-ttu-id="2de53-158">Описание</span><span class="sxs-lookup"><span data-stu-id="2de53-158">Description</span></span> |
| - | - |
| <span data-ttu-id="2de53-159">EventId</span><span class="sxs-lookup"><span data-stu-id="2de53-159">EventId</span></span> | <span data-ttu-id="2de53-160">Глобальный уникальный идентификатор этого события.</span><span class="sxs-lookup"><span data-stu-id="2de53-160">Globally unique identifier for this event.</span></span> <br><br> <span data-ttu-id="2de53-161">Пример:</span><span class="sxs-lookup"><span data-stu-id="2de53-161">Example:</span></span> <br><ul><li><span data-ttu-id="2de53-162">602d9444-d2cd-49c7-8624-8643e7171297</span><span class="sxs-lookup"><span data-stu-id="2de53-162">602d9444-d2cd-49c7-8624-8643e7171297</span></span>  |
| <span data-ttu-id="2de53-163">EventType</span><span class="sxs-lookup"><span data-stu-id="2de53-163">EventType</span></span> | <span data-ttu-id="2de53-164">Влияние, которое оказывает это событие.</span><span class="sxs-lookup"><span data-stu-id="2de53-164">Impact this event causes.</span></span> <br><br> <span data-ttu-id="2de53-165">Значения:</span><span class="sxs-lookup"><span data-stu-id="2de53-165">Values:</span></span> <br><ul><li> <span data-ttu-id="2de53-166">`Freeze`. Виртуальная машина будет приостановлена на несколько секунд.</span><span class="sxs-lookup"><span data-stu-id="2de53-166">`Freeze`: The Virtual Machine is scheduled to pause for few seconds.</span></span> <span data-ttu-id="2de53-167">Работа ЦП приостанавливается, но это действие не повлияет на память, открытые файлы и сетевые подключения.</span><span class="sxs-lookup"><span data-stu-id="2de53-167">The CPU is suspended, but there is no impact on memory, open files, or network connections.</span></span> <li><span data-ttu-id="2de53-168">`Reboot`. Планирование перезагрузки виртуальной машины (временная память будет потеряна).</span><span class="sxs-lookup"><span data-stu-id="2de53-168">`Reboot`: The Virtual Machine is scheduled for reboot (non-persistent memory is lost).</span></span> <li><span data-ttu-id="2de53-169">`Redeploy`. Виртуальная машина будет перемещена на другой узел с потерей данных на временных дисках.</span><span class="sxs-lookup"><span data-stu-id="2de53-169">`Redeploy`: The Virtual Machine is scheduled to move to another node (ephemeral disks are lost).</span></span> |
| <span data-ttu-id="2de53-170">ResourceType</span><span class="sxs-lookup"><span data-stu-id="2de53-170">ResourceType</span></span> | <span data-ttu-id="2de53-171">Тип ресурса, на который влияет это событие.</span><span class="sxs-lookup"><span data-stu-id="2de53-171">Type of resource this event impacts.</span></span> <br><br> <span data-ttu-id="2de53-172">Значения:</span><span class="sxs-lookup"><span data-stu-id="2de53-172">Values:</span></span> <ul><li>`VirtualMachine`|
| <span data-ttu-id="2de53-173">Ресурсы</span><span class="sxs-lookup"><span data-stu-id="2de53-173">Resources</span></span>| <span data-ttu-id="2de53-174">Список ресурсов, на которые влияет это событие.</span><span class="sxs-lookup"><span data-stu-id="2de53-174">List of resources this event impacts.</span></span> <span data-ttu-id="2de53-175">Обязательно будет содержать виртуальные машины максимум из одного [домена обновления](manage-availability.md), но не может содержать все машины в таком домене.</span><span class="sxs-lookup"><span data-stu-id="2de53-175">This is guaranteed to contain machines from at most one [Update Domain](manage-availability.md), but may not contain all machines in the UD.</span></span> <br><br> <span data-ttu-id="2de53-176">Пример:</span><span class="sxs-lookup"><span data-stu-id="2de53-176">Example:</span></span> <br><ul><li> <span data-ttu-id="2de53-177">["FrontEnd_IN_0", "BackEnd_IN_0"]</span><span class="sxs-lookup"><span data-stu-id="2de53-177">["FrontEnd_IN_0", "BackEnd_IN_0"]</span></span> |
| <span data-ttu-id="2de53-178">Event Status</span><span class="sxs-lookup"><span data-stu-id="2de53-178">Event Status</span></span> | <span data-ttu-id="2de53-179">Состояние этого события.</span><span class="sxs-lookup"><span data-stu-id="2de53-179">Status of this event.</span></span> <br><br> <span data-ttu-id="2de53-180">Значения:</span><span class="sxs-lookup"><span data-stu-id="2de53-180">Values:</span></span> <ul><li><span data-ttu-id="2de53-181">`Scheduled`. Это запланированное событие состоится по истечении времени, указанного в свойстве `NotBefore`.</span><span class="sxs-lookup"><span data-stu-id="2de53-181">`Scheduled`: This event is scheduled to start after the time specified in the `NotBefore` property.</span></span><li><span data-ttu-id="2de53-182">`Started`. Это событие запущено.</span><span class="sxs-lookup"><span data-stu-id="2de53-182">`Started`: This event has started.</span></span></ul> <span data-ttu-id="2de53-183">Состояние `Completed` (или аналогичное) никогда не предоставляется; событие не возвращается после завершения события.</span><span class="sxs-lookup"><span data-stu-id="2de53-183">No `Completed` or similar status is ever provided; the event will no longer be returned when the event is completed.</span></span>
| <span data-ttu-id="2de53-184">NotBefore</span><span class="sxs-lookup"><span data-stu-id="2de53-184">NotBefore</span></span>| <span data-ttu-id="2de53-185">Время, после которого может быть запущено это событие.</span><span class="sxs-lookup"><span data-stu-id="2de53-185">Time after which this event may start.</span></span> <br><br> <span data-ttu-id="2de53-186">Пример:</span><span class="sxs-lookup"><span data-stu-id="2de53-186">Example:</span></span> <br><ul><li> <span data-ttu-id="2de53-187">2016-09-19T18:29:47Z</span><span class="sxs-lookup"><span data-stu-id="2de53-187">2016-09-19T18:29:47Z</span></span>  |

### <a name="event-scheduling"></a><span data-ttu-id="2de53-188">Планирование события</span><span class="sxs-lookup"><span data-stu-id="2de53-188">Event scheduling</span></span>
<span data-ttu-id="2de53-189">В зависимости от типа каждое будущее событие будет выполняться минимальное количество времени.</span><span class="sxs-lookup"><span data-stu-id="2de53-189">Each event is scheduled a minimum amount of time in the future based on event type.</span></span> <span data-ttu-id="2de53-190">Это время отражается в свойстве события `NotBefore`.</span><span class="sxs-lookup"><span data-stu-id="2de53-190">This time is reflected in an event's `NotBefore` property.</span></span> 

|<span data-ttu-id="2de53-191">EventType</span><span class="sxs-lookup"><span data-stu-id="2de53-191">EventType</span></span>  | <span data-ttu-id="2de53-192">Минимальное время уведомления</span><span class="sxs-lookup"><span data-stu-id="2de53-192">Minimum Notice</span></span> |
| - | - |
| <span data-ttu-id="2de53-193">Freeze</span><span class="sxs-lookup"><span data-stu-id="2de53-193">Freeze</span></span>| <span data-ttu-id="2de53-194">15 минут</span><span class="sxs-lookup"><span data-stu-id="2de53-194">15 minutes</span></span> |
| <span data-ttu-id="2de53-195">Reboot</span><span class="sxs-lookup"><span data-stu-id="2de53-195">Reboot</span></span> | <span data-ttu-id="2de53-196">15 минут</span><span class="sxs-lookup"><span data-stu-id="2de53-196">15 minutes</span></span> |
| <span data-ttu-id="2de53-197">Повторное развертывание</span><span class="sxs-lookup"><span data-stu-id="2de53-197">Redeploy</span></span> | <span data-ttu-id="2de53-198">10 минут</span><span class="sxs-lookup"><span data-stu-id="2de53-198">10 minutes</span></span> |

### <a name="starting-an-event"></a><span data-ttu-id="2de53-199">Запуск события</span><span class="sxs-lookup"><span data-stu-id="2de53-199">Starting an event</span></span> 

<span data-ttu-id="2de53-200">Когда вы узнаете о предстоящем событии и выполняете все действия для корректного завершения работы, вы можете утвердить ожидающее событие, выполнив вызов `POST` к службе метаданных Azure с помощью `EventId`.</span><span class="sxs-lookup"><span data-stu-id="2de53-200">Once you have learned of an upcoming event and completed your logic for graceful shutdown, you can approve the outstanding event by making a `POST` call to the metadata service with the `EventId`.</span></span> <span data-ttu-id="2de53-201">Это указывает службе Azure, что она может сократить минимальное время уведомления (если возможно).</span><span class="sxs-lookup"><span data-stu-id="2de53-201">This indicates to Azure that it can shorten the minimum notification time (when possible).</span></span> 

```
curl -H Metadata:true -X POST -d '{"DocumentIncarnation":"5", "StartRequests": [{"EventId": "f020ba2e-3bc0-4c40-a10b-86575a9eabd5"}]}' http://169.254.169.254/metadata/scheduledevents?api-version=2017-03-01
```

> [!NOTE] 
> <span data-ttu-id="2de53-202">Подтверждение событий позволяет выполнить событие для всех ресурсов `Resources` в событии, а не только для виртуальной машины, которая подтверждает событие.</span><span class="sxs-lookup"><span data-stu-id="2de53-202">Acknowledging an event allows the event to proceed for all `Resources` in the event, not just the virtual machine that acknowledges the event.</span></span> <span data-ttu-id="2de53-203">Таким образом, можно выбрать "лидера" для координации подтверждения, например первую виртуальную машину в поле `Resources`.</span><span class="sxs-lookup"><span data-stu-id="2de53-203">You may therefore choose to elect a leader to coordinate the acknowledgement, which may be as simple as the first machine in the `Resources` field.</span></span>




## <a name="python-sample"></a><span data-ttu-id="2de53-204">Пример на языке Python</span><span class="sxs-lookup"><span data-stu-id="2de53-204">Python sample</span></span> 

<span data-ttu-id="2de53-205">В следующем примере выполняется запрос запланированных событий в службе метаданных, а затем утверждение каждого ожидающего события.</span><span class="sxs-lookup"><span data-stu-id="2de53-205">The following sample queries the metadata service for scheduled events and approves each outstanding event.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="2de53-206">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2de53-206">Next steps</span></span> 

- <span data-ttu-id="2de53-207">Дополнительные сведения об API, доступных в [службе метаданных экземпляра](instance-metadata-service.md).</span><span class="sxs-lookup"><span data-stu-id="2de53-207">Read more about the APIs available in the [Instance Metadata service](instance-metadata-service.md).</span></span>
- <span data-ttu-id="2de53-208">Подробнее о [плановом обслуживании виртуальных машин Linux в Azure](planned-maintenance.md).</span><span class="sxs-lookup"><span data-stu-id="2de53-208">Learn about [planned maintenance for Linux virtual machines in Azure](planned-maintenance.md).</span></span>
