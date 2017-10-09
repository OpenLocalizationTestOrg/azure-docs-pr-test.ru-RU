---
title: "aaaConvert toomicroservices приложений облачных служб Azure | Документы Microsoft"
description: "В этом руководстве сравнивает облачных служб Web и рабочих ролей и toohelp Service Fabric службы без сохранения состояния миграции из облачных служб tooService структуры."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 5880ebb3-8b54-4be8-af4b-95a1bc082603
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: c43b11623b2ba7f6069782a8b7e030c82572a6e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="guide-tooconverting-web-and-worker-roles-tooservice-fabric-stateless-services"></a><span data-ttu-id="9b5f2-103">Руководство по tooconverting Web and Worker Roles tooService структуры службы без сохранения состояния</span><span class="sxs-lookup"><span data-stu-id="9b5f2-103">Guide tooconverting Web and Worker Roles tooService Fabric stateless services</span></span>
<span data-ttu-id="9b5f2-104">В этой статье описывается как toomigrate вашей облачной службы Web and Worker Roles tooService структуры службы без сохранения состояния.</span><span class="sxs-lookup"><span data-stu-id="9b5f2-104">This article describes how toomigrate your Cloud Services Web and Worker Roles tooService Fabric stateless services.</span></span> <span data-ttu-id="9b5f2-105">Это простейший способ переноса hello из облачных служб tooService структуры hello приложений которого общая архитектура будет toostay примерно таким же.</span><span class="sxs-lookup"><span data-stu-id="9b5f2-105">This is hello simplest migration path from Cloud Services tooService Fabric for applications whose overall architecture is going toostay roughly hello same.</span></span>

## <a name="cloud-service-project-tooservice-fabric-application-project"></a><span data-ttu-id="9b5f2-106">Облако проект приложения Fabric tooService проекта служб</span><span class="sxs-lookup"><span data-stu-id="9b5f2-106">Cloud Service project tooService Fabric application project</span></span>
 <span data-ttu-id="9b5f2-107">Проекта облачной службы и проект приложения Fabric Service имеют схожую структуру и оба представляют Привет развертывания модульных для приложения — то есть, каждый из них определяет полный пакет hello, развернутых toorun приложения.</span><span class="sxs-lookup"><span data-stu-id="9b5f2-107">A Cloud Service project and a Service Fabric Application project have a similar structure and both represent hello deployment unit for your application - that is, they each define hello complete package that is deployed toorun your application.</span></span> <span data-ttu-id="9b5f2-108">Проект облачной службы содержит веб-роли или рабочие роли (одну или несколько).</span><span class="sxs-lookup"><span data-stu-id="9b5f2-108">A Cloud Service project contains one or more Web or Worker Roles.</span></span> <span data-ttu-id="9b5f2-109">Подобным образом содержит несколько служб и проект приложения Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="9b5f2-109">Similarly, a Service Fabric Application project contains one or more services.</span></span> 

<span data-ttu-id="9b5f2-110">Hello различие заключается в том couples проекта облачной службы hello hello развертывания приложений с помощью развертывания виртуальной Машины и таким образом, содержит параметры конфигурации виртуальной Машины, в то время как проект приложения Fabric Application hello только определяет приложение, которое будет развертываться набор tooa существующих виртуальных машин в кластере Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="9b5f2-110">hello difference is that hello Cloud Service project couples hello application deployment with a VM deployment and thus contains VM configuration settings in it, whereas hello Service Fabric Application project only defines an application that will be deployed tooa set of existing VMs in a Service Fabric cluster.</span></span> <span data-ttu-id="9b5f2-111">самого кластера Service Fabric Hello развертывается только один раз, либо посредством шаблона диспетчера ресурсов либо через портал Azure hello и несколько Service Fabric, приложения могут быть развернуты tooit.</span><span class="sxs-lookup"><span data-stu-id="9b5f2-111">hello Service Fabric cluster itself is only deployed once, either through an Resource Manager template or through hello Azure portal, and multiple Service Fabric applications can be deployed tooit.</span></span>

![Сравнение проекта облачных служб и проекта Service Fabric][3]

## <a name="worker-role-toostateless-service"></a><span data-ttu-id="9b5f2-113">Служба toostateless рабочей роли</span><span class="sxs-lookup"><span data-stu-id="9b5f2-113">Worker Role toostateless service</span></span>
<span data-ttu-id="9b5f2-114">По существу рабочей роли представляет рабочей нагрузки без отслеживания состояния, то есть каждый экземпляр рабочей нагрузки hello идентична и запросы могут быть перенаправленное tooany экземпляра в любое время.</span><span class="sxs-lookup"><span data-stu-id="9b5f2-114">Conceptually, a Worker Role represents a stateless workload, meaning every instance of hello workload is identical and requests can be routed tooany instance at any time.</span></span> <span data-ttu-id="9b5f2-115">Каждый экземпляр не является ожидаемым tooremember hello предыдущего запроса.</span><span class="sxs-lookup"><span data-stu-id="9b5f2-115">Each instance is not expected tooremember hello previous request.</span></span> <span data-ttu-id="9b5f2-116">Состояние данной рабочей нагрузке hello работает с управляемых хранилищем внешнего состояния, например табличного хранилища Azure или Azure DB документа.</span><span class="sxs-lookup"><span data-stu-id="9b5f2-116">State that hello workload operates on is managed by an external state store, such as Azure Table Storage or Azure Document DB.</span></span> <span data-ttu-id="9b5f2-117">В платформе Service Fabric рабочей нагрузке этого типа соответствует служба без отслеживания состояния.</span><span class="sxs-lookup"><span data-stu-id="9b5f2-117">In Service Fabric, this type of workload is represented by a Stateless Service.</span></span> <span data-ttu-id="9b5f2-118">Hello простой подход toomigrating tooService рабочей роли фабрики должен выполнять преобразование tooa кода рабочей роли службы без отслеживания состояния.</span><span class="sxs-lookup"><span data-stu-id="9b5f2-118">hello simplest approach toomigrating a Worker Role tooService Fabric can be done by converting Worker Role code tooa Stateless Service.</span></span>

![TooStateless рабочей роли службы][4]

## <a name="web-role-toostateless-service"></a><span data-ttu-id="9b5f2-120">Веб-службы роли toostateless</span><span class="sxs-lookup"><span data-stu-id="9b5f2-120">Web Role toostateless service</span></span>
<span data-ttu-id="9b5f2-121">Аналогичные tooWorker роли веб-роли также представляет рабочей нагрузки без отслеживания состояния, и поэтому концептуально слишком может быть сопоставленных tooa службы без отслеживания состояния Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="9b5f2-121">Similar tooWorker Role, a Web Role also represents a stateless workload, and so conceptually it too can be mapped tooa Service Fabric stateless service.</span></span> <span data-ttu-id="9b5f2-122">В отличие от веб-ролей, платформа Service Fabric не поддерживает IIS.</span><span class="sxs-lookup"><span data-stu-id="9b5f2-122">However, unlike Web Roles, Service Fabric does not support IIS.</span></span> <span data-ttu-id="9b5f2-123">toomigrate веб-приложения из службы без отслеживания состояния tooa веб-роль требует первый скользящего tooa веб-платформа, может быть резидентным и не зависит от System.Web, например ASP.NET Core 1 или IIS.</span><span class="sxs-lookup"><span data-stu-id="9b5f2-123">toomigrate a web application from a Web Role tooa stateless service requires first moving tooa web framework that can be self-hosted and does not depend on IIS or System.Web, such as ASP.NET Core 1.</span></span>

| <span data-ttu-id="9b5f2-124">**Приложения**</span><span class="sxs-lookup"><span data-stu-id="9b5f2-124">**Application**</span></span> | <span data-ttu-id="9b5f2-125">**Поддерживаются**</span><span class="sxs-lookup"><span data-stu-id="9b5f2-125">**Supported**</span></span> | <span data-ttu-id="9b5f2-126">**Путь перехода**</span><span class="sxs-lookup"><span data-stu-id="9b5f2-126">**Migration path**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9b5f2-127">Веб-формы ASP.NET</span><span class="sxs-lookup"><span data-stu-id="9b5f2-127">ASP.NET Web Forms</span></span> |<span data-ttu-id="9b5f2-128">Нет</span><span class="sxs-lookup"><span data-stu-id="9b5f2-128">No</span></span> |<span data-ttu-id="9b5f2-129">Преобразовать tooASP.NET основы 1 MVC</span><span class="sxs-lookup"><span data-stu-id="9b5f2-129">Convert tooASP.NET Core 1 MVC</span></span> |
| <span data-ttu-id="9b5f2-130">ASP.NET MVC 3</span><span class="sxs-lookup"><span data-stu-id="9b5f2-130">ASP.NET MVC</span></span> |<span data-ttu-id="9b5f2-131">С переносом</span><span class="sxs-lookup"><span data-stu-id="9b5f2-131">With Migration</span></span> |<span data-ttu-id="9b5f2-132">Обновления tooASP.NET основы 1 MVC</span><span class="sxs-lookup"><span data-stu-id="9b5f2-132">Upgrade tooASP.NET Core 1 MVC</span></span> |
| <span data-ttu-id="9b5f2-133">Веб-API ASP.NET</span><span class="sxs-lookup"><span data-stu-id="9b5f2-133">ASP.NET Web API</span></span> |<span data-ttu-id="9b5f2-134">С переносом</span><span class="sxs-lookup"><span data-stu-id="9b5f2-134">With Migration</span></span> |<span data-ttu-id="9b5f2-135">Использование автономно размещаемого сервера или компонента ASP.NET Core 1</span><span class="sxs-lookup"><span data-stu-id="9b5f2-135">Use self-hosted server or ASP.NET Core 1</span></span> |
| <span data-ttu-id="9b5f2-136">ASP.NET Core 1</span><span class="sxs-lookup"><span data-stu-id="9b5f2-136">ASP.NET Core 1</span></span> |<span data-ttu-id="9b5f2-137">Да</span><span class="sxs-lookup"><span data-stu-id="9b5f2-137">Yes</span></span> |<span data-ttu-id="9b5f2-138">Недоступно</span><span class="sxs-lookup"><span data-stu-id="9b5f2-138">N/A</span></span> |

## <a name="entry-point-api-and-lifecycle"></a><span data-ttu-id="9b5f2-139">Жизненный цикл и интерфейс API точки входа</span><span class="sxs-lookup"><span data-stu-id="9b5f2-139">Entry point API and lifecycle</span></span>
<span data-ttu-id="9b5f2-140">Рабочая роль и интерфейсы API службы Service Fabric дают возможность использовать похожие точки входа.</span><span class="sxs-lookup"><span data-stu-id="9b5f2-140">Worker Role and Service Fabric service APIs offer similar entry points:</span></span> 

| <span data-ttu-id="9b5f2-141">**Точка входа**</span><span class="sxs-lookup"><span data-stu-id="9b5f2-141">**Entry Point**</span></span> | <span data-ttu-id="9b5f2-142">**Рабочая роль**</span><span class="sxs-lookup"><span data-stu-id="9b5f2-142">**Worker Role**</span></span> | <span data-ttu-id="9b5f2-143">**Служба Service Fabric**</span><span class="sxs-lookup"><span data-stu-id="9b5f2-143">**Service Fabric service**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9b5f2-144">Обработка</span><span class="sxs-lookup"><span data-stu-id="9b5f2-144">Processing</span></span> |`Run()` |`RunAsync()` |
| <span data-ttu-id="9b5f2-145">Запуск виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="9b5f2-145">VM start</span></span> |`OnStart()` |<span data-ttu-id="9b5f2-146">Недоступно</span><span class="sxs-lookup"><span data-stu-id="9b5f2-146">N/A</span></span> |
| <span data-ttu-id="9b5f2-147">Остановка виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="9b5f2-147">VM stop</span></span> |`OnStop()` |<span data-ttu-id="9b5f2-148">Недоступно</span><span class="sxs-lookup"><span data-stu-id="9b5f2-148">N/A</span></span> |
| <span data-ttu-id="9b5f2-149">Открытие прослушивателя для запросов клиентов</span><span class="sxs-lookup"><span data-stu-id="9b5f2-149">Open listener for client requests</span></span> |<span data-ttu-id="9b5f2-150">Недоступно</span><span class="sxs-lookup"><span data-stu-id="9b5f2-150">N/A</span></span> |<ul><li> <span data-ttu-id="9b5f2-151">`CreateServiceInstanceListener()` для служб без отслеживания состояния</span><span class="sxs-lookup"><span data-stu-id="9b5f2-151">`CreateServiceInstanceListener()` for stateless</span></span></li><li><span data-ttu-id="9b5f2-152">`CreateServiceReplicaListener()` для служб с отслеживанием состояния</span><span class="sxs-lookup"><span data-stu-id="9b5f2-152">`CreateServiceReplicaListener()` for stateful</span></span></li></ul> |

### <a name="worker-role"></a><span data-ttu-id="9b5f2-153">Рабочая роль</span><span class="sxs-lookup"><span data-stu-id="9b5f2-153">Worker Role</span></span>
```C#

using Microsoft.WindowsAzure.ServiceRuntime;

namespace WorkerRole1
{
    public class WorkerRole : RoleEntryPoint
    {
        public override void Run()
        {
        }

        public override bool OnStart()
        {
        }

        public override void OnStop()
        {
        }
    }
}

```

### <a name="service-fabric-stateless-service"></a><span data-ttu-id="9b5f2-154">Служба без отслеживания состояния Service Fabric</span><span class="sxs-lookup"><span data-stu-id="9b5f2-154">Service Fabric Stateless Service</span></span>
```C#

using System.Collections.Generic;
using System.Threading;
using System.Threading.Tasks;
using Microsoft.ServiceFabric.Services.Communication.Runtime;
using Microsoft.ServiceFabric.Services.Runtime;

namespace Stateless1
{
    public class Stateless1 : StatelessService
    {
        protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
        {
        }

        protected override Task RunAsync(CancellationToken cancelServiceInstance)
        {
        }
    }
}

```

<span data-ttu-id="9b5f2-155">Во время обработки которых toobegin имеют Переопределение основной «запуск».</span><span class="sxs-lookup"><span data-stu-id="9b5f2-155">Both have a primary "Run" override in which toobegin processing.</span></span> <span data-ttu-id="9b5f2-156">Службы Service Fabric объединяют `Run`, `Start` и `Stop` в одну точку входа, `RunAsync`.</span><span class="sxs-lookup"><span data-stu-id="9b5f2-156">Service Fabric services  combine `Run`, `Start`, and `Stop` into a single entry point, `RunAsync`.</span></span> <span data-ttu-id="9b5f2-157">Службы должны начать работать после `RunAsync` начинается и прекратить работу при hello `RunAsync` сигнал CancellationToken метода.</span><span class="sxs-lookup"><span data-stu-id="9b5f2-157">Your service should begin working when `RunAsync` starts, and should stop working when hello `RunAsync` method's CancellationToken is signaled.</span></span> 

<span data-ttu-id="9b5f2-158">Существует несколько ключевых различий между жизненного цикла hello и временем существования рабочих ролей и Service Fabric служб:</span><span class="sxs-lookup"><span data-stu-id="9b5f2-158">There are several key differences between hello lifecycle and lifetime of Worker Roles and Service Fabric services:</span></span>

* <span data-ttu-id="9b5f2-159">**Жизненный цикл:** hello Главное отличие — что рабочая роль является виртуальной Машины и его жизненного цикла равноценных toohello виртуальную Машину, которая включает в себя события, запускает и останавливает hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="9b5f2-159">**Lifecycle:** hello biggest difference is that a Worker Role is a VM and so its lifecycle is tied toohello VM, which includes events for when hello VM starts and stops.</span></span> <span data-ttu-id="9b5f2-160">Служба Service Fabric имеет жизненного цикла, отдельном от hello жизненный цикл виртуальной Машины, поэтому он не включает события для при hello размещения виртуальной Машины или запуске компьютера или остановка, как они не связаны.</span><span class="sxs-lookup"><span data-stu-id="9b5f2-160">A Service Fabric service has a lifecycle that is separate from hello VM lifecycle, so it does not include events for when hello host VM or machine starts and stop, as they are not related.</span></span>
* <span data-ttu-id="9b5f2-161">**Время существования:** экземпляра рабочей роли будут обновляться при hello `Run` метод завершает работу.</span><span class="sxs-lookup"><span data-stu-id="9b5f2-161">**Lifetime:** A Worker Role instance will recycle if hello `Run` method exits.</span></span> <span data-ttu-id="9b5f2-162">Hello `RunAsync` методы в службе Service Fabric тем не менее можно запустить toocompletion и hello экземпляр службы будет работать.</span><span class="sxs-lookup"><span data-stu-id="9b5f2-162">hello `RunAsync` method in a Service Fabric service however can run toocompletion and hello service instance will stay up.</span></span> 

<span data-ttu-id="9b5f2-163">Службам, которые прослушивают запросы клиента, платформа Service Fabric дает возможность использовать пользовательскую точку входа настройки связи.</span><span class="sxs-lookup"><span data-stu-id="9b5f2-163">Service Fabric provides an optional communication setup entry point for services that listen for client requests.</span></span> <span data-ttu-id="9b5f2-164">Hello RunAsync и точка входа связи переопределяются необязательно в Service Fabric служб - службы может выбрать tooonly прослушивания tooclient запросы или только запустить цикл обработки или оба - которых именно hello RunAsync метод может быть tooexit без перезапуск экземпляра службы hello, так как он может по-прежнему toolisten для клиентских запросов.</span><span class="sxs-lookup"><span data-stu-id="9b5f2-164">Both hello RunAsync and communication entry point are optional overrides in Service Fabric services - your service may choose tooonly listen tooclient requests, or only run a processing loop, or both - which is why hello RunAsync method is allowed tooexit without restarting hello service instance, because it may continue toolisten for client requests.</span></span>

## <a name="application-api-and-environment"></a><span data-ttu-id="9b5f2-165">Интерфейс API и среда приложения</span><span class="sxs-lookup"><span data-stu-id="9b5f2-165">Application API and environment</span></span>
<span data-ttu-id="9b5f2-166">Среда облачные службы Hello API предоставляет сведения и функциональные возможности для hello текущего экземпляра виртуальной Машины, а также сведения о других экземпляров ролей виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="9b5f2-166">hello Cloud Services environment API provides information and functionality for hello current VM instance as well as information about other VM role instances.</span></span> <span data-ttu-id="9b5f2-167">Service Fabric предоставляет сведения, связанные с tooits среды выполнения и некоторые сведения об узле hello службы сейчас выполняется.</span><span class="sxs-lookup"><span data-stu-id="9b5f2-167">Service Fabric provides information related tooits runtime and some information about hello node a service is currently running on.</span></span> 

| <span data-ttu-id="9b5f2-168">**Задача среды**</span><span class="sxs-lookup"><span data-stu-id="9b5f2-168">**Environment Task**</span></span> | <span data-ttu-id="9b5f2-169">**Облачные службы**</span><span class="sxs-lookup"><span data-stu-id="9b5f2-169">**Cloud Services**</span></span> | <span data-ttu-id="9b5f2-170">**Service Fabric**</span><span class="sxs-lookup"><span data-stu-id="9b5f2-170">**Service Fabric**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9b5f2-171">Параметры конфигурации и изменение уведомления</span><span class="sxs-lookup"><span data-stu-id="9b5f2-171">Configuration Settings and change notification</span></span> |`RoleEnvironment` |`CodePackageActivationContext` |
| <span data-ttu-id="9b5f2-172">Локальное хранилище</span><span class="sxs-lookup"><span data-stu-id="9b5f2-172">Local Storage</span></span> |`RoleEnvironment` |`CodePackageActivationContext` |
| <span data-ttu-id="9b5f2-173">Сведения о конечной точке</span><span class="sxs-lookup"><span data-stu-id="9b5f2-173">Endpoint Information</span></span> |`RoleInstance` <ul><li><span data-ttu-id="9b5f2-174">Текущий экземпляр: `RoleEnvironment.CurrentRoleInstance`</span><span class="sxs-lookup"><span data-stu-id="9b5f2-174">Current instance: `RoleEnvironment.CurrentRoleInstance`</span></span></li><li><span data-ttu-id="9b5f2-175">Другие роли и экземпляр: `RoleEnvironment.Roles`</span><span class="sxs-lookup"><span data-stu-id="9b5f2-175">Other roles and instance: `RoleEnvironment.Roles`</span></span></li> |<ul><li><span data-ttu-id="9b5f2-176">`NodeContext` для адреса текущего узла</span><span class="sxs-lookup"><span data-stu-id="9b5f2-176">`NodeContext` for current Node address</span></span></li><li><span data-ttu-id="9b5f2-177">`FabricClient` и `ServicePartitionResolver` для обнаружения конечной точки службы</span><span class="sxs-lookup"><span data-stu-id="9b5f2-177">`FabricClient` and `ServicePartitionResolver` for service endpoint discovery</span></span></li> |
| <span data-ttu-id="9b5f2-178">Эмуляция среды</span><span class="sxs-lookup"><span data-stu-id="9b5f2-178">Environment Emulation</span></span> |`RoleEnvironment.IsEmulated` |<span data-ttu-id="9b5f2-179">Недоступно</span><span class="sxs-lookup"><span data-stu-id="9b5f2-179">N/A</span></span> |
| <span data-ttu-id="9b5f2-180">Событие одновременного изменения</span><span class="sxs-lookup"><span data-stu-id="9b5f2-180">Simultaneous change event</span></span> |`RoleEnvironment` |<span data-ttu-id="9b5f2-181">Недоступно</span><span class="sxs-lookup"><span data-stu-id="9b5f2-181">N/A</span></span> |

## <a name="configuration-settings"></a><span data-ttu-id="9b5f2-182">Параметры конфигурации</span><span class="sxs-lookup"><span data-stu-id="9b5f2-182">Configuration settings</span></span>
<span data-ttu-id="9b5f2-183">Параметры конфигурации в облачных службах задаются для роли ВМ и применяются tooall экземпляры этой роли виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="9b5f2-183">Configuration settings in Cloud Services are set for a VM role and apply tooall instances of that VM role.</span></span> <span data-ttu-id="9b5f2-184">Эти параметры представляют собой пары "ключ — значение", заданные в файлах ServiceConfiguration.*.cscfg. Получить к ним прямой доступ можно через RoleEnvironment.</span><span class="sxs-lookup"><span data-stu-id="9b5f2-184">These settings are key-value pairs set in ServiceConfiguration.*.cscfg files and can be accessed directly through RoleEnvironment.</span></span> <span data-ttu-id="9b5f2-185">В Service Fabric параметры применяются по отдельности tooeach службы и приложения tooeach вместо tooa виртуальной Машины, так как виртуальная машина может размещаться несколько служб и приложений.</span><span class="sxs-lookup"><span data-stu-id="9b5f2-185">In Service Fabric, settings apply individually tooeach service and tooeach application, rather than tooa VM, because a VM can host multiple services and applications.</span></span> <span data-ttu-id="9b5f2-186">Служба состоит из трех пакетов:</span><span class="sxs-lookup"><span data-stu-id="9b5f2-186">A service is composed of three packages:</span></span>

* <span data-ttu-id="9b5f2-187">**Код:** содержит hello исполняемых файлов службы, двоичные файлы, библиотеки DLL и другие файлы toorun необходимых для работы служб.</span><span class="sxs-lookup"><span data-stu-id="9b5f2-187">**Code:** contains hello service executables, binaries, DLLs, and any other files a service needs toorun.</span></span>
* <span data-ttu-id="9b5f2-188">**Конфигурация:** все файлы конфигурации и параметры для службы.</span><span class="sxs-lookup"><span data-stu-id="9b5f2-188">**Config:** all configuration files and settings for a service.</span></span>
* <span data-ttu-id="9b5f2-189">**Данные:** статические данные файлы, связанные со службой hello.</span><span class="sxs-lookup"><span data-stu-id="9b5f2-189">**Data:** static data files associated with hello service.</span></span>

<span data-ttu-id="9b5f2-190">Каждый из этих пакетов можно отдельно обновить, в том числе до определенной версии.</span><span class="sxs-lookup"><span data-stu-id="9b5f2-190">Each of these packages can be independently versioned and upgraded.</span></span> <span data-ttu-id="9b5f2-191">Службы, аналогичные tooCloud, пакет конфигурации может осуществляться программно через API и события, доступные toonotify службы hello изменения конфигурации пакета.</span><span class="sxs-lookup"><span data-stu-id="9b5f2-191">Similar tooCloud Services, a config package can be accessed programmatically through an API and events are available toonotify hello service of a config package change.</span></span> <span data-ttu-id="9b5f2-192">Файл Settings.xml может использоваться для ключа и значения конфигурации и программный доступ аналогичные toohello разделе параметров приложения из файла App.config.</span><span class="sxs-lookup"><span data-stu-id="9b5f2-192">A Settings.xml file can be used for key-value configuration and programmatic access similar toohello app settings section of an App.config file.</span></span> <span data-ttu-id="9b5f2-193">Однако, в отличие от облачных служб, пакет конфигурации Service Fabric может содержать любые файлы конфигурации в любом формате, будь то XML, JSON, YAML или пользовательский двоичный формат.</span><span class="sxs-lookup"><span data-stu-id="9b5f2-193">However, unlike Cloud Services, a Service Fabric config package can contain any configuration files in any format, whether it's XML, JSON, YAML, or a custom binary format.</span></span> 

### <a name="accessing-configuration"></a><span data-ttu-id="9b5f2-194">Получение доступа к конфигурации</span><span class="sxs-lookup"><span data-stu-id="9b5f2-194">Accessing configuration</span></span>
#### <a name="cloud-services"></a><span data-ttu-id="9b5f2-195">Облачные службы</span><span class="sxs-lookup"><span data-stu-id="9b5f2-195">Cloud Services</span></span>
<span data-ttu-id="9b5f2-196">Доступ к параметрам конфигурации из файла ServiceConfiguration.*.cscfg можно получить с помощью атрибута `RoleEnvironment`.</span><span class="sxs-lookup"><span data-stu-id="9b5f2-196">Configuration settings from ServiceConfiguration.*.cscfg can be accessed through `RoleEnvironment`.</span></span> <span data-ttu-id="9b5f2-197">Эти параметры являются глобально доступной tooall экземпляры роли в hello же развертывании облачной службы.</span><span class="sxs-lookup"><span data-stu-id="9b5f2-197">These settings are globally available tooall role instances in hello same Cloud Service deployment.</span></span>

```C#

string value = RoleEnvironment.GetConfigurationSettingValue("Key");

```

#### <a name="service-fabric"></a><span data-ttu-id="9b5f2-198">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="9b5f2-198">Service Fabric</span></span>
<span data-ttu-id="9b5f2-199">Каждая служба имеет отдельный пакет конфигурации.</span><span class="sxs-lookup"><span data-stu-id="9b5f2-199">Each service has its own individual configuration package.</span></span> <span data-ttu-id="9b5f2-200">Не существует встроенного механизма, который предназначен для глобальных параметров конфигурации, доступных всем приложениям кластера.</span><span class="sxs-lookup"><span data-stu-id="9b5f2-200">There is no built-in mechanism for global configuration settings accessible by all applications in a cluster.</span></span> <span data-ttu-id="9b5f2-201">При использовании Service Fabric специальные Settings.xml конфигурации файл конфигурации пакета, значения в Settings.xml могут быть перезаписаны на уровне приложения hello, внося изменения в параметры уровня приложения невозможно.</span><span class="sxs-lookup"><span data-stu-id="9b5f2-201">When using Service Fabric's special Settings.xml configuration file within a configuration package, values in Settings.xml can be overwritten at hello application level, making application-level configuration settings possible.</span></span>

<span data-ttu-id="9b5f2-202">Параметры конфигурации являются обращений для каждого экземпляра службы через службу hello `CodePackageActivationContext`.</span><span class="sxs-lookup"><span data-stu-id="9b5f2-202">Configuration settings are accesses within each service instance through hello service's `CodePackageActivationContext`.</span></span>

```C#

ConfigurationPackage configPackage = this.Context.CodePackageActivationContext.GetConfigurationPackageObject("Config");

// Access Settings.xml
KeyedCollection<string, ConfigurationProperty> parameters = configPackage.Settings.Sections["MyConfigSection"].Parameters;

string value = parameters["Key"]?.Value;

// Access custom configuration file:
using (StreamReader reader = new StreamReader(Path.Combine(configPackage.Path, "CustomConfig.json")))
{
    MySettings settings = JsonConvert.DeserializeObject<MySettings>(reader.ReadToEnd());
}

```

### <a name="configuration-update-events"></a><span data-ttu-id="9b5f2-203">События обновления конфигурации</span><span class="sxs-lookup"><span data-stu-id="9b5f2-203">Configuration update events</span></span>
#### <a name="cloud-services"></a><span data-ttu-id="9b5f2-204">Облачные службы</span><span class="sxs-lookup"><span data-stu-id="9b5f2-204">Cloud Services</span></span>
<span data-ttu-id="9b5f2-205">Hello `RoleEnvironment.Changed` событие является используется toonotify все экземпляры роли, когда изменение происходит в среде hello, например изменение конфигурации.</span><span class="sxs-lookup"><span data-stu-id="9b5f2-205">hello `RoleEnvironment.Changed` event is used toonotify all role instances when a change occurs in hello environment, such as a configuration change.</span></span> <span data-ttu-id="9b5f2-206">Это используется tooconsume обновлений конфигурации без перезапуска экземпляров роли или перезапуска рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="9b5f2-206">This is used tooconsume configuration updates without recycling role instances or restarting a worker process.</span></span>

```C#

RoleEnvironment.Changed += RoleEnvironmentChanged;

private void RoleEnvironmentChanged(object sender, RoleEnvironmentChangedEventArgs e)
{
   // Get hello list of configuration changes
   var settingChanges = e.Changes.OfType<RoleEnvironmentConfigurationSettingChange>();
foreach (var settingChange in settingChanges) 
   {
      Trace.WriteLine("Setting: " + settingChange.ConfigurationSettingName, "Information");
   }
}

```

#### <a name="service-fabric"></a><span data-ttu-id="9b5f2-207">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="9b5f2-207">Service Fabric</span></span>
<span data-ttu-id="9b5f2-208">Каждый из трех типов пакета hello в службе - кода, конфигурации и данных - имеют события, уведомляющие экземпляр службы обновлена, добавлении или удалении пакета.</span><span class="sxs-lookup"><span data-stu-id="9b5f2-208">Each of hello three package types in a service - Code, Config, and Data - have events that notify a service instance when a package is updated, added, or removed.</span></span> <span data-ttu-id="9b5f2-209">Служба может содержать несколько пакетов каждого типа.</span><span class="sxs-lookup"><span data-stu-id="9b5f2-209">A service can contain multiple packages of each type.</span></span> <span data-ttu-id="9b5f2-210">Например, служба может иметь несколько пакетов конфигурации, для каждого из которых можно задать версию и каждый из которых можно обновлять.</span><span class="sxs-lookup"><span data-stu-id="9b5f2-210">For example, a service may have multiple config packages, each individually versioned and upgradeable.</span></span> 

<span data-ttu-id="9b5f2-211">Эти события являются доступными tooconsume изменения в пакеты служб без перезапуска экземпляра службы hello.</span><span class="sxs-lookup"><span data-stu-id="9b5f2-211">These events are available tooconsume changes in service packages without restarting hello service instance.</span></span>

```C#

this.Context.CodePackageActivationContext.ConfigurationPackageModifiedEvent +=
                    this.CodePackageActivationContext_ConfigurationPackageModifiedEvent;

private void CodePackageActivationContext_ConfigurationPackageModifiedEvent(object sender, PackageModifiedEventArgs<ConfigurationPackage> e)
{
    this.UpdateCustomConfig(e.NewPackage.Path);
    this.UpdateSettings(e.NewPackage.Settings);
}

```

## <a name="startup-tasks"></a><span data-ttu-id="9b5f2-212">Задачи при запуске</span><span class="sxs-lookup"><span data-stu-id="9b5f2-212">Startup tasks</span></span>
<span data-ttu-id="9b5f2-213">Задачи при запуске — это действия, выполняемые перед запуском приложения.</span><span class="sxs-lookup"><span data-stu-id="9b5f2-213">Startup tasks are actions that are taken before an application starts.</span></span> <span data-ttu-id="9b5f2-214">Задачи запуска — типовыми toorun сценариев установки, с использованием повышенных привилегий.</span><span class="sxs-lookup"><span data-stu-id="9b5f2-214">A startup task is typically used toorun setup scripts using elevated privileges.</span></span> <span data-ttu-id="9b5f2-215">Эти задачи поддерживаются и облачными службами, и платформой Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="9b5f2-215">Both Cloud Services and Service Fabric support start-up tasks.</span></span> <span data-ttu-id="9b5f2-216">Hello основное отличие заключается в, в облачных службах, задачи запуска — равноценных tooa виртуальной Машины, так как он является частью экземпляра роли, а в Service Fabric задачи запуска — tooa связанные службы, которая не является равноценных tooany конкретной виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="9b5f2-216">hello main difference is that in Cloud Services, a startup task is tied tooa VM because it is part of a role instance, whereas in Service Fabric a startup task is tied tooa service, which is not tied tooany particular VM.</span></span>

| <span data-ttu-id="9b5f2-217">Облачные службы</span><span class="sxs-lookup"><span data-stu-id="9b5f2-217">Cloud Services</span></span> | <span data-ttu-id="9b5f2-218">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="9b5f2-218">Service Fabric</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9b5f2-219">Расположение конфигурации</span><span class="sxs-lookup"><span data-stu-id="9b5f2-219">Configuration location</span></span> |<span data-ttu-id="9b5f2-220">ServiceDefinition.csdef</span><span class="sxs-lookup"><span data-stu-id="9b5f2-220">ServiceDefinition.csdef</span></span> |
| <span data-ttu-id="9b5f2-221">Привилегии</span><span class="sxs-lookup"><span data-stu-id="9b5f2-221">Privileges</span></span> |<span data-ttu-id="9b5f2-222">Ограниченные или повышенные</span><span class="sxs-lookup"><span data-stu-id="9b5f2-222">"limited" or "elevated"</span></span> |
| <span data-ttu-id="9b5f2-223">Виртуализация</span><span class="sxs-lookup"><span data-stu-id="9b5f2-223">Sequencing</span></span> |<span data-ttu-id="9b5f2-224">Простая, фоновая, на переднем плане</span><span class="sxs-lookup"><span data-stu-id="9b5f2-224">"simple", "background", "foreground"</span></span> |

### <a name="cloud-services"></a><span data-ttu-id="9b5f2-225">Облачные службы</span><span class="sxs-lookup"><span data-stu-id="9b5f2-225">Cloud Services</span></span>
<span data-ttu-id="9b5f2-226">В облачных службах точка входа для запуска настраивается для каждой роли в файле ServiceDefintion.csdef.</span><span class="sxs-lookup"><span data-stu-id="9b5f2-226">In Cloud Services a startup entry point is configured per role in ServiceDefinition.csdef.</span></span> 

```xml

<ServiceDefinition>
    <Startup>
        <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple" >
            <Environment>
                <Variable name="MyVersionNumber" value="1.0.0.0" />
            </Environment>
        </Task>
    </Startup>
    ...
</ServiceDefinition>

```

### <a name="service-fabric"></a><span data-ttu-id="9b5f2-227">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="9b5f2-227">Service Fabric</span></span>
<span data-ttu-id="9b5f2-228">В Service Fabric точка входа для запуска настраивается для каждой роли в файле ServiceManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="9b5f2-228">In Service Fabric a startup entry point is configured per service in ServiceManifest.xml:</span></span>

```xml

<ServiceManifest>
  <CodePackage Name="Code" Version="1.0.0">
    <SetupEntryPoint>
      <ExeHost>
        <Program>Startup.bat</Program>
      </ExeHost>
    </SetupEntryPoint>
    ...
</ServiceManifest>

``` 

## <a name="a-note-about-development-environment"></a><span data-ttu-id="9b5f2-229">Примечание о среде разработки</span><span class="sxs-lookup"><span data-stu-id="9b5f2-229">A note about development environment</span></span>
<span data-ttu-id="9b5f2-230">Облачные службы и Service Fabric интегрированного в Visual Studio с помощью шаблонов проектов и поддержка для отладки, настройке и развертыванию локально и tooAzure.</span><span class="sxs-lookup"><span data-stu-id="9b5f2-230">Both Cloud Services and Service Fabric are integrated with Visual Studio with project templates and support for debugging, configuring, and deploying both locally and tooAzure.</span></span> <span data-ttu-id="9b5f2-231">Кроме того, облачные службы и платформа Service Fabric дают возможность пользоваться локальной средой выполнения разработки.</span><span class="sxs-lookup"><span data-stu-id="9b5f2-231">Both Cloud Services and Service Fabric also provide a local development runtime environment.</span></span> <span data-ttu-id="9b5f2-232">Hello различие состоит в том, пока hello облачной службы среды выполнения разработки эмулирует hello среды Azure, в котором она выполняется, Service Fabric не использовать симулятор — он использует hello завершения среда выполнения Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="9b5f2-232">hello difference is that while hello Cloud Service development runtime emulates hello Azure environment on which it runs, Service Fabric does not use an emulator - it uses hello complete Service Fabric runtime.</span></span> <span data-ttu-id="9b5f2-233">Hello Service Fabric, среда выполнения на локальном компьютере разработчика hello одной среде, работающей в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="9b5f2-233">hello Service Fabric environment you run on your local development machine is hello same environment that runs in production.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9b5f2-234">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9b5f2-234">Next steps</span></span>
<span data-ttu-id="9b5f2-235">Более подробные сведения о надежных структуры службы и hello фундаментальные различия между облачными службами и toounderstand архитектуры приложения Service Fabric, как tootake преимуществами hello полный набор возможностей Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="9b5f2-235">Read more about Service Fabric Reliable Services and hello fundamental differences between Cloud Services and Service Fabric application architecture toounderstand how tootake advantage of hello full set of Service Fabric features.</span></span>

* [<span data-ttu-id="9b5f2-236">Начало работы со службами Reliable Services в Service Fabric</span><span class="sxs-lookup"><span data-stu-id="9b5f2-236">Getting started with Service Fabric Reliable Services</span></span>](service-fabric-reliable-services-quick-start.md)
* [<span data-ttu-id="9b5f2-237">Руководство по концептуальной toohello различия между облачными службами и Service Fabric</span><span class="sxs-lookup"><span data-stu-id="9b5f2-237">Conceptual guide toohello differences between Cloud Services and Service Fabric</span></span>](service-fabric-cloud-services-migration-differences.md)

<!--Image references-->
[3]: ./media/service-fabric-cloud-services-migration-worker-role-stateless-service/service-fabric-cloud-service-projects.png
[4]: ./media/service-fabric-cloud-services-migration-worker-role-stateless-service/worker-role-to-stateless-service.png
