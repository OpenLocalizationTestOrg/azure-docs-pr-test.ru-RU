---
title: "aaaCommunication для ролей в облачных службах | Документы Microsoft"
description: "Экземпляры ролей в облачных служб может иметь конечных точек (http, https, tcp, udp) определенных, взаимодействующих с hello вне или от других экземпляров ролей."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 7008a083-acbe-4fb8-ae60-b837ef971ca1
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/14/2016
ms.author: adegeo
ms.openlocfilehash: 1fb39215ceb8a3f0381ef5e108c1149de115ff8e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="enable-communication-for-role-instances-in-azure"></a><span data-ttu-id="385bc-103">Включение обмена данными между экземплярами роли в Azure</span><span class="sxs-lookup"><span data-stu-id="385bc-103">Enable communication for role instances in azure</span></span>
<span data-ttu-id="385bc-104">Ролей облачной службы взаимодействуют через внутренние и внешние подключения.</span><span class="sxs-lookup"><span data-stu-id="385bc-104">Cloud service roles communicate through internal and external connections.</span></span> <span data-ttu-id="385bc-105">Внешние подключения называются **входными конечными точками**, а внутренние подключения — **внутренними конечными точками**.</span><span class="sxs-lookup"><span data-stu-id="385bc-105">External connections are called **input endpoints** while internal connections are called **internal endpoints**.</span></span> <span data-ttu-id="385bc-106">В этом разделе описывается способ toomodify hello [службы определение](cloud-services-model-and-package.md#csdef) toocreate конечных точек.</span><span class="sxs-lookup"><span data-stu-id="385bc-106">This topic describes how toomodify hello [service definition](cloud-services-model-and-package.md#csdef) toocreate endpoints.</span></span>

## <a name="input-endpoint"></a><span data-ttu-id="385bc-107">Входная конечная точка</span><span class="sxs-lookup"><span data-stu-id="385bc-107">Input endpoint</span></span>
<span data-ttu-id="385bc-108">Конечная точка ввода Hello используется в том случае, если tooexpose toohello порт за пределами.</span><span class="sxs-lookup"><span data-stu-id="385bc-108">hello input endpoint is used when you want tooexpose a port toohello outside.</span></span> <span data-ttu-id="385bc-109">Укажите тип hello протокола и порта hello hello конечной точки, которая применяется для hello внешних и внутренних портов для конечной точки hello.</span><span class="sxs-lookup"><span data-stu-id="385bc-109">You specify hello protocol type and hello port of hello endpoint which then applies for both hello external and internal ports for hello endpoint.</span></span> <span data-ttu-id="385bc-110">Если требуется, можно указать другой внутренний порт для конечной точки hello с hello [localPort](https://msdn.microsoft.com/library/azure/gg557552.aspx#InputEndpoint) атрибута.</span><span class="sxs-lookup"><span data-stu-id="385bc-110">If you want, you can specify a different internal port for hello endpoint with hello [localPort](https://msdn.microsoft.com/library/azure/gg557552.aspx#InputEndpoint) attribute.</span></span>

<span data-ttu-id="385bc-111">Конечная точка ввода Hello можно использовать следующие протоколы hello: **http, https, tcp, udp**.</span><span class="sxs-lookup"><span data-stu-id="385bc-111">hello input endpoint can use hello following protocols: **http, https, tcp, udp**.</span></span>

<span data-ttu-id="385bc-112">добавить конечную точку ввода, toocreate hello **InputEndpoint** toohello дочерний элемент **конечные точки** элемент web и рабочей роли.</span><span class="sxs-lookup"><span data-stu-id="385bc-112">toocreate an input endpoint, add hello **InputEndpoint** child element toohello **Endpoints** element of either a web or worker role.</span></span>

```xml
<Endpoints>
  <InputEndpoint name="StandardWeb" protocol="http" port="80" localPort="80" />
</Endpoints> 
```

## <a name="instance-input-endpoint"></a><span data-ttu-id="385bc-113">Входная конечная точка экземпляра</span><span class="sxs-lookup"><span data-stu-id="385bc-113">Instance input endpoint</span></span>
<span data-ttu-id="385bc-114">Аналогично конечные точки tooinput входные конечные точки, но позволяет сопоставить определенные порты общедоступным для каждого экземпляра отдельные роли благодаря перенаправлению портов в подсистеме балансировки нагрузки hello.</span><span class="sxs-lookup"><span data-stu-id="385bc-114">Instance input endpoints are similar tooinput endpoints but allows you map specific public-facing ports for each individual role instance by using port forwarding on hello load balancer.</span></span> <span data-ttu-id="385bc-115">Можно указать один общедоступный порт или диапазон портов.</span><span class="sxs-lookup"><span data-stu-id="385bc-115">You can specify a single public-facing port, or a range of ports.</span></span>

<span data-ttu-id="385bc-116">можно использовать только конечная точка ввода экземпляра Hello **tcp** или **udp** в качестве протокола hello.</span><span class="sxs-lookup"><span data-stu-id="385bc-116">hello instance input endpoint can only use **tcp** or **udp** as hello protocol.</span></span>

<span data-ttu-id="385bc-117">добавить конечные точки ввода экземпляра toocreate hello **InstanceInputEndpoint** дочерний элемент toohello **конечные точки** элемент web и рабочей роли.</span><span class="sxs-lookup"><span data-stu-id="385bc-117">toocreate an instance input endpoint, add hello **InstanceInputEndpoint** child element toohello **Endpoints** element of either a web or worker role.</span></span>

```xml
<Endpoints>
  <InstanceInputEndpoint name="Endpoint2" protocol="tcp" localPort="10100">
    <AllocatePublicPortFrom>
      <FixedPortRange max="10109" min="10105" />
    </AllocatePublicPortFrom>
  </InstanceInputEndpoint>
</Endpoints>
```

## <a name="internal-endpoint"></a><span data-ttu-id="385bc-118">Внутренняя конечная точка</span><span class="sxs-lookup"><span data-stu-id="385bc-118">Internal endpoint</span></span>
<span data-ttu-id="385bc-119">Внутренние конечные точки доступны для подключения между экземплярами.</span><span class="sxs-lookup"><span data-stu-id="385bc-119">Internal endpoints are available for instance-to-instance communication.</span></span> <span data-ttu-id="385bc-120">Hello порт является необязательным, и если не указано, динамический порт назначается toohello конечной точки.</span><span class="sxs-lookup"><span data-stu-id="385bc-120">hello port is optional and if omitted, a dynamic port is assigned toohello endpoint.</span></span> <span data-ttu-id="385bc-121">Можно использовать диапазон портов.</span><span class="sxs-lookup"><span data-stu-id="385bc-121">A port range can be used.</span></span> <span data-ttu-id="385bc-122">Существует ограничение: до 5 внутренних конечных точек на роль.</span><span class="sxs-lookup"><span data-stu-id="385bc-122">There is a limit of five internal endpoints per role.</span></span>

<span data-ttu-id="385bc-123">Hello внутренней конечной точки можно использовать следующие протоколы hello: **http, tcp, udp, любой**.</span><span class="sxs-lookup"><span data-stu-id="385bc-123">hello internal endpoint can use hello following protocols: **http, tcp, udp, any**.</span></span>

<span data-ttu-id="385bc-124">toocreate внутренней конечной точки ввода, добавить hello **InternalEndpoint** дочерний элемент toohello **конечные точки** элемент web и рабочей роли.</span><span class="sxs-lookup"><span data-stu-id="385bc-124">toocreate an internal input endpoint, add hello **InternalEndpoint** child element toohello **Endpoints** element of either a web or worker role.</span></span>

```xml
<Endpoints>
  <InternalEndpoint name="Endpoint3" protocol="any" port="8999" />
</Endpoints> 
```

<span data-ttu-id="385bc-125">Можно также использовать диапазон портов.</span><span class="sxs-lookup"><span data-stu-id="385bc-125">You can also use a port range.</span></span>

```xml
<Endpoints>
  <InternalEndpoint name="Endpoint3" protocol="any">
    <FixedPortRange max="8995" min="8999" />
  </InternalEndpoint>
</Endpoints>
```


## <a name="worker-roles-vs-web-roles"></a><span data-ttu-id="385bc-126">Рабочие роли и Веб-роли</span><span class="sxs-lookup"><span data-stu-id="385bc-126">Worker roles vs. Web roles</span></span>
<span data-ttu-id="385bc-127">При работе с веб-ролями и рабочими ролями существует одно незначительное отличие, связанное с конечными точками.</span><span class="sxs-lookup"><span data-stu-id="385bc-127">There is one minor difference with endpoints when working with both worker and web roles.</span></span> <span data-ttu-id="385bc-128">Hello веб-роль должна иметь как минимум одну конечную точку ввода с помощью hello **HTTP** протокола.</span><span class="sxs-lookup"><span data-stu-id="385bc-128">hello web role must have at minimum a single input endpoint using hello **HTTP** protocol.</span></span>

```xml
<Endpoints>
  <InputEndpoint name="StandardWeb" protocol="http" port="80" localPort="80" />
  <!-- more endpoints may be declared after hello first InputEndPoint -->
</Endpoints>
```

## <a name="using-hello-net-sdk-tooaccess-an-endpoint"></a><span data-ttu-id="385bc-129">С помощью tooaccess .NET SDK hello конечной точки</span><span class="sxs-lookup"><span data-stu-id="385bc-129">Using hello .NET SDK tooaccess an endpoint</span></span>
<span data-ttu-id="385bc-130">Hello управляемая библиотека Azure предоставляет методы для toocommunicate экземпляров ролей во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="385bc-130">hello Azure Managed Library provides methods for role instances toocommunicate at runtime.</span></span> <span data-ttu-id="385bc-131">Из кода, выполняемого в экземпляре роли можно получить сведения о hello наличие других экземпляров ролей и их конечные точки, а также сведения о текущей роли экземпляра hello.</span><span class="sxs-lookup"><span data-stu-id="385bc-131">From code running within a role instance, you can retrieve information about hello existence of other role instances and their endpoints, as well as information about hello current role instance.</span></span>

> [!NOTE]
> <span data-ttu-id="385bc-132">Можно получать сведения только о тех экземплярах, которые запущены в облачной службе и для которых определена по крайней мере одна внутренняя конечная точка.</span><span class="sxs-lookup"><span data-stu-id="385bc-132">You can only retrieve information about role instances that are running in your cloud service and that define at least one internal endpoint.</span></span> <span data-ttu-id="385bc-133">Нельзя получить данные об экземплярах роли, запущенных в другой службе.</span><span class="sxs-lookup"><span data-stu-id="385bc-133">You cannot obtain data about role instances running in a different service.</span></span>
> 
> 

<span data-ttu-id="385bc-134">Можно использовать hello [экземпляров](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.role.instances.aspx) свойство tooretrieve экземпляров роли.</span><span class="sxs-lookup"><span data-stu-id="385bc-134">You can use hello [Instances](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.role.instances.aspx) property tooretrieve instances of a role.</span></span> <span data-ttu-id="385bc-135">Сначала с помощью hello [CurrentRoleInstance](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.currentroleinstance.aspx) tooreturn ссылки toohello текущей роли, а затем используйте hello [роли](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.role.aspx) свойство tooreturn самой роли toohello ссылки.</span><span class="sxs-lookup"><span data-stu-id="385bc-135">First use hello [CurrentRoleInstance](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.currentroleinstance.aspx) tooreturn a reference toohello current role instance, and then use hello [Role](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.role.aspx) property tooreturn a reference toohello role itself.</span></span>

<span data-ttu-id="385bc-136">При подключении экземпляра роли tooa программно через hello .NET SDK, это относительно легко tooaccess сведения о конечной точке hello.</span><span class="sxs-lookup"><span data-stu-id="385bc-136">When you connect tooa role instance programmatically through hello .NET SDK, it's relatively easy tooaccess hello endpoint information.</span></span> <span data-ttu-id="385bc-137">Например после вы уже подключены среды tooa определенной роли, можно получить порт hello определенной конечной точке с этим кодом:</span><span class="sxs-lookup"><span data-stu-id="385bc-137">For example, after you've already connected tooa specific role environment, you can get hello port of a specific endpoint with this code:</span></span>

```csharp
int port = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["StandardWeb"].IPEndpoint.Port;
```

<span data-ttu-id="385bc-138">Hello **экземпляров** свойство возвращает коллекцию **RoleInstance** объектов.</span><span class="sxs-lookup"><span data-stu-id="385bc-138">hello **Instances** property returns a collection of **RoleInstance** objects.</span></span> <span data-ttu-id="385bc-139">Эта коллекция всегда содержит текущий экземпляр hello.</span><span class="sxs-lookup"><span data-stu-id="385bc-139">This collection always contains hello current instance.</span></span> <span data-ttu-id="385bc-140">Если роль hello не определяет внутреннюю конечную точку, коллекция hello включает hello текущего экземпляра, но не другие экземпляры.</span><span class="sxs-lookup"><span data-stu-id="385bc-140">If hello role does not define an internal endpoint, hello collection includes hello current instance but no other instances.</span></span> <span data-ttu-id="385bc-141">Hello число экземпляров роли в коллекции hello всегда будет 1 в случае hello, где нет внутренней конечной точки для роли hello.</span><span class="sxs-lookup"><span data-stu-id="385bc-141">hello number of role instances in hello collection will always be 1 in hello case where no internal endpoint is defined for hello role.</span></span> <span data-ttu-id="385bc-142">Если роль hello определяет внутреннюю конечную точку, его экземпляры могут быть обнаружены во время выполнения, и hello число экземпляров в коллекции hello будет соответствовать toohello число экземпляров, указанные для роли hello в файл конфигурации службы hello.</span><span class="sxs-lookup"><span data-stu-id="385bc-142">If hello role defines an internal endpoint, its instances are discoverable at runtime, and hello number of instances in hello collection will correspond toohello number of instances specified for hello role in hello service configuration file.</span></span>

> [!NOTE]
> <span data-ttu-id="385bc-143">Hello управляемая библиотека Azure не предоставляет средства определения работоспособности hello других экземпляров роли, но вы можно реализовать самостоятельно Если службе нужна подобная функциональность.</span><span class="sxs-lookup"><span data-stu-id="385bc-143">hello Azure Managed Library does not provide a means of determining hello health of other role instances, but you can implement such health assessments yourself if your service needs this functionality.</span></span> <span data-ttu-id="385bc-144">Можно использовать [диагностики Azure](cloud-services-dotnet-diagnostics.md) tooobtain сведения о выполнении экземпляров роли.</span><span class="sxs-lookup"><span data-stu-id="385bc-144">You can use [Azure Diagnostics](cloud-services-dotnet-diagnostics.md) tooobtain information about running role instances.</span></span>
> 
> 

<span data-ttu-id="385bc-145">toodetermine hello номер порта для внутренней конечной точки в экземпляре роли, можно использовать hello [InstanceEndpoints](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.instanceendpoints.aspx) tooreturn свойство объект словаря, который содержит имена конечных точек и их соответствующие IP-адреса и порты.</span><span class="sxs-lookup"><span data-stu-id="385bc-145">toodetermine hello port number for an internal endpoint on a role instance, you can use hello [InstanceEndpoints](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.instanceendpoints.aspx) property tooreturn a Dictionary object that contains endpoint names and their corresponding IP addresses and ports.</span></span> <span data-ttu-id="385bc-146">Hello [IPEndpoint](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstanceendpoint.ipendpoint.aspx) свойство возвращает hello IP-адрес и порт для указанной конечной точкой.</span><span class="sxs-lookup"><span data-stu-id="385bc-146">hello [IPEndpoint](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstanceendpoint.ipendpoint.aspx) property returns hello IP address and port for a specified endpoint.</span></span> <span data-ttu-id="385bc-147">Hello **PublicIPEndpoint** свойство возвращает hello порт для конечной точки с балансировкой нагрузки.</span><span class="sxs-lookup"><span data-stu-id="385bc-147">hello **PublicIPEndpoint** property returns hello port for a load balanced endpoint.</span></span> <span data-ttu-id="385bc-148">часть Hello IP-адреса hello **PublicIPEndpoint** свойство не используется.</span><span class="sxs-lookup"><span data-stu-id="385bc-148">hello IP address portion of hello **PublicIPEndpoint** property is not used.</span></span>

<span data-ttu-id="385bc-149">Вот пример, в котором выполняется итерация экземпляров роли.</span><span class="sxs-lookup"><span data-stu-id="385bc-149">Here is an example that iterates role instances.</span></span>

```csharp
foreach (RoleInstance roleInst in RoleEnvironment.CurrentRoleInstance.Role.Instances)
{
    Trace.WriteLine("Instance ID: " + roleInst.Id);
    foreach (RoleInstanceEndpoint roleInstEndpoint in roleInst.InstanceEndpoints.Values)
    {
        Trace.WriteLine("Instance endpoint IP address and port: " + roleInstEndpoint.IPEndpoint);
    }
}
```

<span data-ttu-id="385bc-150">Ниже приведен пример рабочей роли, который получает конечную точку hello, предоставленную до определения службы hello и начинает прослушивание подключений.</span><span class="sxs-lookup"><span data-stu-id="385bc-150">Here is an example of a worker role that gets hello endpoint exposed through hello service definition and starts listening for connections.</span></span>

> [!WARNING]
> <span data-ttu-id="385bc-151">Этот код будет работать только для развернутой службы.</span><span class="sxs-lookup"><span data-stu-id="385bc-151">This code will only work for a deployed service.</span></span> <span data-ttu-id="385bc-152">При выполнении в эмуляторе вычислений Azure hello службы элементы конфигурации для создания конечных точек прямого порта (**InstanceInputEndpoint** элементов) учитываются.</span><span class="sxs-lookup"><span data-stu-id="385bc-152">When running in hello Azure Compute Emulator, service configuration elements that create direct port endpoints (**InstanceInputEndpoint** elements) are ignored.</span></span>
> 
> 

```csharp
using System;
using System.Diagnostics;
using System.Linq;
using System.Net;
using System.Net.Sockets;
using System.Threading;
using Microsoft.WindowsAzure;
using Microsoft.WindowsAzure.Diagnostics;
using Microsoft.WindowsAzure.ServiceRuntime;
using Microsoft.WindowsAzure.StorageClient;

namespace WorkerRole1
{
  public class WorkerRole : RoleEntryPoint
  {
    public override void Run()
    {
      try
      {
        // Initialize method-wide variables
        var epName = "Endpoint1";
        var roleInstance = RoleEnvironment.CurrentRoleInstance;

        // Identify direct communication port
        var myPublicEp = roleInstance.InstanceEndpoints[epName].PublicIPEndpoint;
        Trace.TraceInformation("IP:{0}, Port:{1}", myPublicEp.Address, myPublicEp.Port);

        // Identify public endpoint
        var myInternalEp = roleInstance.InstanceEndpoints[epName].IPEndpoint;

        // Create socket listener
        var listener = new Socket(
          myInternalEp.AddressFamily, SocketType.Stream, ProtocolType.Tcp);

        // Bind socket listener toointernal endpoint and listen
        listener.Bind(myInternalEp);
        listener.Listen(10);
        Trace.TraceInformation("Listening on IP:{0},Port: {1}",
          myInternalEp.Address, myInternalEp.Port);

        while (true)
        {
          // Block hello thread and wait for a client request
          Socket handler = listener.Accept();
          Trace.TraceInformation("Client request received.");

          // Define body of socket handler
          var handlerThread = new Thread(
            new ParameterizedThreadStart(h =>
            {
              var socket = h as Socket;
              Trace.TraceInformation("Local:{0} Remote{1}",
                socket.LocalEndPoint, socket.RemoteEndPoint);

              // Shut down and close socket
              socket.Shutdown(SocketShutdown.Both);
              socket.Close();
            }
          ));

          // Start socket handler on new thread
          handlerThread.Start(handler);
        }
      }
      catch (Exception e)
      {
        Trace.TraceError("Caught exception in run. Details: {0}", e);
      }
    }

    public override bool OnStart()
    {
      // Set hello maximum number of concurrent connections 
      ServicePointManager.DefaultConnectionLimit = 12;

      // For information on handling configuration changes
      // see hello MSDN topic at http://go.microsoft.com/fwlink/?LinkId=166357.
      return base.OnStart();
    }
  }
}
```

## <a name="network-traffic-rules-toocontrol-role-communication"></a><span data-ttu-id="385bc-153">Роль правил трафика toocontrol сетью</span><span class="sxs-lookup"><span data-stu-id="385bc-153">Network traffic rules toocontrol role communication</span></span>
<span data-ttu-id="385bc-154">После задания внутренних конечных точек можно добавить сетевого трафика (hello конечных точек, которые были созданы с учетом) правила toocontrol как экземпляры роли могут взаимодействовать друг с другом.</span><span class="sxs-lookup"><span data-stu-id="385bc-154">After you define internal endpoints, you can add network traffic rules (based on hello endpoints that you created) toocontrol how role instances can communicate with each other.</span></span> <span data-ttu-id="385bc-155">Hello следующей диаграмме показаны некоторые общие сценарии по управлению взаимодействием ролей:</span><span class="sxs-lookup"><span data-stu-id="385bc-155">hello following diagram shows some common scenarios for controlling role communication:</span></span>

<span data-ttu-id="385bc-156">![Сценарии использования правил сетевого трафика](./media/cloud-services-enable-communication-role-instances/scenarios.png "Сценарии использования правил сетевого трафика")</span><span class="sxs-lookup"><span data-stu-id="385bc-156">![Network Traffic Rules Scenarios](./media/cloud-services-enable-communication-role-instances/scenarios.png "Network Traffic Rules Scenarios")</span></span>

<span data-ttu-id="385bc-157">Hello примере кода показан определения роли для роли hello hello предыдущей иллюстрации.</span><span class="sxs-lookup"><span data-stu-id="385bc-157">hello following code example shows role definitions for hello roles shown in hello previous diagram.</span></span> <span data-ttu-id="385bc-158">В каждом определении роли определена по крайней мере одна внутренняя конечная точка:</span><span class="sxs-lookup"><span data-stu-id="385bc-158">Each role definition includes at least one internal endpoint defined:</span></span>

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
  <WebRole name="WebRole1" vmsize="Medium">
    <Sites>
      <Site name="Web">
        <Bindings>
          <Binding name="HttpIn" endpointName="HttpIn" />
        </Bindings>
      </Site>
    </Sites>
    <Endpoints>
      <InputEndpoint name="HttpIn" protocol="http" port="80" />
      <InternalEndpoint name="InternalTCP1" protocol="tcp" />
    </Endpoints>
  </WebRole>
  <WorkerRole name="WorkerRole1">
    <Endpoints>
      <InternalEndpoint name="InternalTCP2" protocol="tcp" />
    </Endpoints>
  </WorkerRole>
  <WorkerRole name="WorkerRole2">
    <Endpoints>
      <InternalEndpoint name="InternalTCP3" protocol="tcp" />
      <InternalEndpoint name="InternalTCP4" protocol="tcp" />
    </Endpoints>
  </WorkerRole>
</ServiceDefinition>
```

> [!NOTE]
> <span data-ttu-id="385bc-159">Обмен данными между ролями с внутренним конечными точками с фиксированными и автоматически назначенными портами может быть ограничен.</span><span class="sxs-lookup"><span data-stu-id="385bc-159">Restriction of communication between roles can occur with internal endpoints of both fixed and automatically assigned ports.</span></span>
> 
> 

<span data-ttu-id="385bc-160">По умолчанию определив внутреннюю конечную точку, могут передаваться из любой роли toohello внутренней конечной точке другой роли без каких-либо ограничений.</span><span class="sxs-lookup"><span data-stu-id="385bc-160">By default, after an internal endpoint is defined, communication can flow from any role toohello internal endpoint of a role without any restrictions.</span></span> <span data-ttu-id="385bc-161">toorestrict связи, необходимо добавить **NetworkTrafficRules** toohello элемент **ServiceDefinition** элемент в файле определения службы hello.</span><span class="sxs-lookup"><span data-stu-id="385bc-161">toorestrict communication, you must add a **NetworkTrafficRules** element toohello **ServiceDefinition** element in hello service definition file.</span></span>

### <a name="scenario-1"></a><span data-ttu-id="385bc-162">Сценарий 1</span><span class="sxs-lookup"><span data-stu-id="385bc-162">Scenario 1</span></span>
<span data-ttu-id="385bc-163">Разрешить только сетевой трафик от **WebRole1** слишком**WorkerRole1**.</span><span class="sxs-lookup"><span data-stu-id="385bc-163">Only allow network traffic from **WebRole1** too**WorkerRole1**.</span></span>

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
  <NetworkTrafficRules>
    <OnlyAllowTrafficTo>
      <Destinations>
        <RoleEndpoint endpointName="InternalTCP2" roleName="WorkerRole1"/>
      </Destinations>
      <AllowAllTraffic/>
      <WhenSource matches="AnyRule">
        <FromRole roleName="WebRole1"/>
      </WhenSource>
    </OnlyAllowTrafficTo>
  </NetworkTrafficRules>
</ServiceDefinition>
```

### <a name="scenario-2"></a><span data-ttu-id="385bc-164">Сценарий 2</span><span class="sxs-lookup"><span data-stu-id="385bc-164">Scenario 2</span></span>
<span data-ttu-id="385bc-165">Разрешен только сетевой трафик от **WebRole1** слишком**WorkerRole1** и **WorkerRole2**.</span><span class="sxs-lookup"><span data-stu-id="385bc-165">Only allows network traffic from **WebRole1** too**WorkerRole1** and **WorkerRole2**.</span></span>

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
  <NetworkTrafficRules>
    <OnlyAllowTrafficTo>
      <Destinations>
        <RoleEndpoint endpointName="InternalTCP2" roleName="WorkerRole1"/>
        <RoleEndpoint endpointName="InternalTCP3" roleName="WorkerRole2"/>
      </Destinations>
      <WhenSource matches="AnyRule">
        <FromRole roleName="WebRole1"/>
      </WhenSource>
    </OnlyAllowTrafficTo>
  </NetworkTrafficRules>
</ServiceDefinition>
```

### <a name="scenario-3"></a><span data-ttu-id="385bc-166">Сценарий 3</span><span class="sxs-lookup"><span data-stu-id="385bc-166">Scenario 3</span></span>
<span data-ttu-id="385bc-167">Разрешен только сетевой трафик от **WebRole1** слишком**WorkerRole1**, и **WorkerRole1** слишком**WorkerRole2**.</span><span class="sxs-lookup"><span data-stu-id="385bc-167">Only allows network traffic from **WebRole1** too**WorkerRole1**, and **WorkerRole1** too**WorkerRole2**.</span></span>

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
  <NetworkTrafficRules>
    <OnlyAllowTrafficTo>
      <Destinations>
        <RoleEndpoint endpointName="InternalTCP2" roleName="WorkerRole1"/>
      </Destinations>
      <AllowAllTraffic/>
      <WhenSource matches="AnyRule">
        <FromRole roleName="WebRole1"/>
      </WhenSource>
    </OnlyAllowTrafficTo>
  </NetworkTrafficRules>
  <NetworkTrafficRules>
    <OnlyAllowTrafficTo>
      <Destinations>
        <RoleEndpoint endpointName="InternalTCP3" roleName="WorkerRole2"/>
      </Destinations>
      <WhenSource matches="AnyRule">
        <FromRole roleName="WorkerRole1"/>
      </WhenSource>
    </OnlyAllowTrafficTo>
  </NetworkTrafficRules>
</ServiceDefinition>
```

### <a name="scenario-4"></a><span data-ttu-id="385bc-168">Сценарий 4</span><span class="sxs-lookup"><span data-stu-id="385bc-168">Scenario 4</span></span>
<span data-ttu-id="385bc-169">Разрешен только сетевой трафик от **WebRole1** слишком**WorkerRole1**, **WebRole1** слишком**WorkerRole2**, и  **WorkerRole1** слишком**WorkerRole2**.</span><span class="sxs-lookup"><span data-stu-id="385bc-169">Only allows network traffic from **WebRole1** too**WorkerRole1**, **WebRole1** too**WorkerRole2**, and **WorkerRole1** too**WorkerRole2**.</span></span>

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
  <NetworkTrafficRules>
    <OnlyAllowTrafficTo>
      <Destinations>
        <RoleEndpoint endpointName="InternalTCP2" roleName="WorkerRole1"/>
      </Destinations>
      <AllowAllTraffic/>
      <WhenSource matches="AnyRule">
        <FromRole roleName="WebRole1"/>
      </WhenSource>
    </OnlyAllowTrafficTo>
  </NetworkTrafficRules>
  <NetworkTrafficRules>
    <OnlyAllowTrafficTo >
      <Destinations>
        <RoleEndpoint endpointName="InternalTCP3" roleName="WorkerRole2"/>
      </Destinations>
      <AllowAllTraffic/>
      <WhenSource matches="AnyRule">
        <FromRole roleName="WorkerRole1"/>
      </WhenSource>
    </OnlyAllowTrafficTo>
  </NetworkTrafficRules>
  <NetworkTrafficRules>
    <OnlyAllowTrafficTo >
      <Destinations>
        <RoleEndpoint endpointName="InternalTCP4" roleName="WorkerRole2"/>
      </Destinations>
      <AllowAllTraffic/>
      <WhenSource matches="AnyRule">
        <FromRole roleName="WebRole1"/>
      </WhenSource>
    </OnlyAllowTrafficTo>
  </NetworkTrafficRules>
</ServiceDefinition>
```

<span data-ttu-id="385bc-170">Справочник по схеме XML для элементов hello выше можно найти [здесь](https://msdn.microsoft.com/library/azure/gg557551.aspx).</span><span class="sxs-lookup"><span data-stu-id="385bc-170">An XML schema reference for hello elements used above can be found [here](https://msdn.microsoft.com/library/azure/gg557551.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="385bc-171">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="385bc-171">Next steps</span></span>
<span data-ttu-id="385bc-172">Дополнительные сведения о hello облачной службы [модели](cloud-services-model-and-package.md).</span><span class="sxs-lookup"><span data-stu-id="385bc-172">Read more about hello Cloud Service [model](cloud-services-model-and-package.md).</span></span>

