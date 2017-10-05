---
title: "Обмен данными между ролями в облачных службах | Документация Майкрософт"
description: "Для экземпляров ролей в облачных службах могут быть определены конечные точки (http, https, tcp, udp), взаимодействующие с внешней средой или с другими экземплярами ролей."
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
ms.openlocfilehash: 8e171d56bb67c971337fa383014988074ec828b1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="enable-communication-for-role-instances-in-azure"></a><span data-ttu-id="88bb5-103">Включение обмена данными между экземплярами роли в Azure</span><span class="sxs-lookup"><span data-stu-id="88bb5-103">Enable communication for role instances in azure</span></span>
<span data-ttu-id="88bb5-104">Ролей облачной службы взаимодействуют через внутренние и внешние подключения.</span><span class="sxs-lookup"><span data-stu-id="88bb5-104">Cloud service roles communicate through internal and external connections.</span></span> <span data-ttu-id="88bb5-105">Внешние подключения называются **входными конечными точками**, а внутренние подключения — **внутренними конечными точками**.</span><span class="sxs-lookup"><span data-stu-id="88bb5-105">External connections are called **input endpoints** while internal connections are called **internal endpoints**.</span></span> <span data-ttu-id="88bb5-106">В этом разделе описывается изменение [определения службы](cloud-services-model-and-package.md#csdef) для создания конечных точек.</span><span class="sxs-lookup"><span data-stu-id="88bb5-106">This topic describes how to modify the [service definition](cloud-services-model-and-package.md#csdef) to create endpoints.</span></span>

## <a name="input-endpoint"></a><span data-ttu-id="88bb5-107">Входная конечная точка</span><span class="sxs-lookup"><span data-stu-id="88bb5-107">Input endpoint</span></span>
<span data-ttu-id="88bb5-108">Входная конечная точка используется, когда необходимо предоставить порт вовне.</span><span class="sxs-lookup"><span data-stu-id="88bb5-108">The input endpoint is used when you want to expose a port to the outside.</span></span> <span data-ttu-id="88bb5-109">Необходимо указать тип протокола и порт конечной точки, которые затем применяются для внешнего и внутреннего портов конечной точки.</span><span class="sxs-lookup"><span data-stu-id="88bb5-109">You specify the protocol type and the port of the endpoint which then applies for both the external and internal ports for the endpoint.</span></span> <span data-ttu-id="88bb5-110">Если требуется, для конечной точки можно указать другой внутренний порт с помощью атрибута [localPort](https://msdn.microsoft.com/library/azure/gg557552.aspx#InputEndpoint) .</span><span class="sxs-lookup"><span data-stu-id="88bb5-110">If you want, you can specify a different internal port for the endpoint with the [localPort](https://msdn.microsoft.com/library/azure/gg557552.aspx#InputEndpoint) attribute.</span></span>

<span data-ttu-id="88bb5-111">Входная конечная точка может использовать следующие протоколы: **http, https, tcp, udp**.</span><span class="sxs-lookup"><span data-stu-id="88bb5-111">The input endpoint can use the following protocols: **http, https, tcp, udp**.</span></span>

<span data-ttu-id="88bb5-112">Чтобы создать входную конечную точку, добавьте дочерний элемент **InputEndpoint** в элемент **Endpoints** веб-роли или рабочей роли.</span><span class="sxs-lookup"><span data-stu-id="88bb5-112">To create an input endpoint, add the **InputEndpoint** child element to the **Endpoints** element of either a web or worker role.</span></span>

```xml
<Endpoints>
  <InputEndpoint name="StandardWeb" protocol="http" port="80" localPort="80" />
</Endpoints> 
```

## <a name="instance-input-endpoint"></a><span data-ttu-id="88bb5-113">Входная конечная точка экземпляра</span><span class="sxs-lookup"><span data-stu-id="88bb5-113">Instance input endpoint</span></span>
<span data-ttu-id="88bb5-114">Входные конечные точки экземпляра похожи на входные конечные точки, однако позволяют сопоставить определенные общедоступные порты для каждого отдельного экземпляра роли с помощью перенаправления портов в балансировщик нагрузки.</span><span class="sxs-lookup"><span data-stu-id="88bb5-114">Instance input endpoints are similar to input endpoints but allows you map specific public-facing ports for each individual role instance by using port forwarding on the load balancer.</span></span> <span data-ttu-id="88bb5-115">Можно указать один общедоступный порт или диапазон портов.</span><span class="sxs-lookup"><span data-stu-id="88bb5-115">You can specify a single public-facing port, or a range of ports.</span></span>

<span data-ttu-id="88bb5-116">Входная конечная точка экземпляра может использовать только протокол **TCP** или **UDP**.</span><span class="sxs-lookup"><span data-stu-id="88bb5-116">The instance input endpoint can only use **tcp** or **udp** as the protocol.</span></span>

<span data-ttu-id="88bb5-117">Чтобы создать входную конечную точку экземпляра, добавьте дочерний элемент **InstanceInputEndpoint** в элемент **Endpoints** веб-роли или рабочей роли.</span><span class="sxs-lookup"><span data-stu-id="88bb5-117">To create an instance input endpoint, add the **InstanceInputEndpoint** child element to the **Endpoints** element of either a web or worker role.</span></span>

```xml
<Endpoints>
  <InstanceInputEndpoint name="Endpoint2" protocol="tcp" localPort="10100">
    <AllocatePublicPortFrom>
      <FixedPortRange max="10109" min="10105" />
    </AllocatePublicPortFrom>
  </InstanceInputEndpoint>
</Endpoints>
```

## <a name="internal-endpoint"></a><span data-ttu-id="88bb5-118">Внутренняя конечная точка</span><span class="sxs-lookup"><span data-stu-id="88bb5-118">Internal endpoint</span></span>
<span data-ttu-id="88bb5-119">Внутренние конечные точки доступны для подключения между экземплярами.</span><span class="sxs-lookup"><span data-stu-id="88bb5-119">Internal endpoints are available for instance-to-instance communication.</span></span> <span data-ttu-id="88bb5-120">Порт является необязательным, и если он не указан, конечной точке назначается динамический порт.</span><span class="sxs-lookup"><span data-stu-id="88bb5-120">The port is optional and if omitted, a dynamic port is assigned to the endpoint.</span></span> <span data-ttu-id="88bb5-121">Можно использовать диапазон портов.</span><span class="sxs-lookup"><span data-stu-id="88bb5-121">A port range can be used.</span></span> <span data-ttu-id="88bb5-122">Существует ограничение: до 5 внутренних конечных точек на роль.</span><span class="sxs-lookup"><span data-stu-id="88bb5-122">There is a limit of five internal endpoints per role.</span></span>

<span data-ttu-id="88bb5-123">Внутренняя конечная точка может использовать следующие протоколы: **http, tcp, udp, any**.</span><span class="sxs-lookup"><span data-stu-id="88bb5-123">The internal endpoint can use the following protocols: **http, tcp, udp, any**.</span></span>

<span data-ttu-id="88bb5-124">Чтобы создать внутреннюю входную конечную точку, добавьте дочерний элемент **InternalEndpoint** в элемент **Endpoints** веб-роли или рабочей роли.</span><span class="sxs-lookup"><span data-stu-id="88bb5-124">To create an internal input endpoint, add the **InternalEndpoint** child element to the **Endpoints** element of either a web or worker role.</span></span>

```xml
<Endpoints>
  <InternalEndpoint name="Endpoint3" protocol="any" port="8999" />
</Endpoints> 
```

<span data-ttu-id="88bb5-125">Можно также использовать диапазон портов.</span><span class="sxs-lookup"><span data-stu-id="88bb5-125">You can also use a port range.</span></span>

```xml
<Endpoints>
  <InternalEndpoint name="Endpoint3" protocol="any">
    <FixedPortRange max="8995" min="8999" />
  </InternalEndpoint>
</Endpoints>
```


## <a name="worker-roles-vs-web-roles"></a><span data-ttu-id="88bb5-126">Рабочие роли и Веб-роли</span><span class="sxs-lookup"><span data-stu-id="88bb5-126">Worker roles vs. Web roles</span></span>
<span data-ttu-id="88bb5-127">При работе с веб-ролями и рабочими ролями существует одно незначительное отличие, связанное с конечными точками.</span><span class="sxs-lookup"><span data-stu-id="88bb5-127">There is one minor difference with endpoints when working with both worker and web roles.</span></span> <span data-ttu-id="88bb5-128">У веб-роли должна быть как минимум одна выходная конечная точка, использующая протокол **HTTP** .</span><span class="sxs-lookup"><span data-stu-id="88bb5-128">The web role must have at minimum a single input endpoint using the **HTTP** protocol.</span></span>

```xml
<Endpoints>
  <InputEndpoint name="StandardWeb" protocol="http" port="80" localPort="80" />
  <!-- more endpoints may be declared after the first InputEndPoint -->
</Endpoints>
```

## <a name="using-the-net-sdk-to-access-an-endpoint"></a><span data-ttu-id="88bb5-129">Использование пакета SDK для .NET для доступа к конечной точке</span><span class="sxs-lookup"><span data-stu-id="88bb5-129">Using the .NET SDK to access an endpoint</span></span>
<span data-ttu-id="88bb5-130">Управляемая библиотека Azure предоставляет методы для обмена данными между экземплярами роли во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="88bb5-130">The Azure Managed Library provides methods for role instances to communicate at runtime.</span></span> <span data-ttu-id="88bb5-131">Из кода, выполняемого в экземпляре роли, можно получить информацию о существовании других экземпляров роли и их конечных точек, а также сведения о текущем экземпляре роли.</span><span class="sxs-lookup"><span data-stu-id="88bb5-131">From code running within a role instance, you can retrieve information about the existence of other role instances and their endpoints, as well as information about the current role instance.</span></span>

> [!NOTE]
> <span data-ttu-id="88bb5-132">Можно получать сведения только о тех экземплярах, которые запущены в облачной службе и для которых определена по крайней мере одна внутренняя конечная точка.</span><span class="sxs-lookup"><span data-stu-id="88bb5-132">You can only retrieve information about role instances that are running in your cloud service and that define at least one internal endpoint.</span></span> <span data-ttu-id="88bb5-133">Нельзя получить данные об экземплярах роли, запущенных в другой службе.</span><span class="sxs-lookup"><span data-stu-id="88bb5-133">You cannot obtain data about role instances running in a different service.</span></span>
> 
> 

<span data-ttu-id="88bb5-134">Для получения экземпляров роли можно использовать свойство [Instances](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.role.instances.aspx) .</span><span class="sxs-lookup"><span data-stu-id="88bb5-134">You can use the [Instances](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.role.instances.aspx) property to retrieve instances of a role.</span></span> <span data-ttu-id="88bb5-135">Сначала используйте [CurrentRoleInstance](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.currentroleinstance.aspx), чтобы вернуть ссылку на текущий экземпляр роли, а затем используйте свойство [Role](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.role.aspx), чтобы вернуть ссылку на саму роль.</span><span class="sxs-lookup"><span data-stu-id="88bb5-135">First use the [CurrentRoleInstance](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.currentroleinstance.aspx) to return a reference to the current role instance, and then use the [Role](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.role.aspx) property to return a reference to the role itself.</span></span>

<span data-ttu-id="88bb5-136">При программном подключении к экземпляру роли с помощью пакета SDK для .NET сравнительно легко получить доступ к информации о конечной точке.</span><span class="sxs-lookup"><span data-stu-id="88bb5-136">When you connect to a role instance programmatically through the .NET SDK, it's relatively easy to access the endpoint information.</span></span> <span data-ttu-id="88bb5-137">Например, после подключения к среде определенной роли можно получить порт определенной конечной точки с помощью этого кода:</span><span class="sxs-lookup"><span data-stu-id="88bb5-137">For example, after you've already connected to a specific role environment, you can get the port of a specific endpoint with this code:</span></span>

```csharp
int port = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["StandardWeb"].IPEndpoint.Port;
```

<span data-ttu-id="88bb5-138">Свойство **Instances** возвращает коллекцию объектов **RoleInstance**.</span><span class="sxs-lookup"><span data-stu-id="88bb5-138">The **Instances** property returns a collection of **RoleInstance** objects.</span></span> <span data-ttu-id="88bb5-139">Эта коллекция всегда содержит текущий экземпляр.</span><span class="sxs-lookup"><span data-stu-id="88bb5-139">This collection always contains the current instance.</span></span> <span data-ttu-id="88bb5-140">Если роль не определяет внутреннюю конечную точку, коллекция содержит текущий экземпляр, но не содержит других экземпляров.</span><span class="sxs-lookup"><span data-stu-id="88bb5-140">If the role does not define an internal endpoint, the collection includes the current instance but no other instances.</span></span> <span data-ttu-id="88bb5-141">Число экземпляров роли в коллекции всегда будет равно 1, когда для роли не определена внутренняя конечная точка.</span><span class="sxs-lookup"><span data-stu-id="88bb5-141">The number of role instances in the collection will always be 1 in the case where no internal endpoint is defined for the role.</span></span> <span data-ttu-id="88bb5-142">Если роль определяет внутреннюю конечную точку, ее экземпляры можно обнаружить во время выполнения, и число экземпляров в коллекции будет соответствовать числу экземпляров, указанных для роли в файле конфигурации службы.</span><span class="sxs-lookup"><span data-stu-id="88bb5-142">If the role defines an internal endpoint, its instances are discoverable at runtime, and the number of instances in the collection will correspond to the number of instances specified for the role in the service configuration file.</span></span>

> [!NOTE]
> <span data-ttu-id="88bb5-143">Управляемая библиотека Azure не предоставляет средства определения работоспособности других экземпляров роли, но вы можете реализовать такие оценки работоспособности самостоятельно, если службе нужна подобная функциональность.</span><span class="sxs-lookup"><span data-stu-id="88bb5-143">The Azure Managed Library does not provide a means of determining the health of other role instances, but you can implement such health assessments yourself if your service needs this functionality.</span></span> <span data-ttu-id="88bb5-144">Можно использовать [систему диагностики Azure](cloud-services-dotnet-diagnostics.md) для получения информации о выполняемых экземплярах роли.</span><span class="sxs-lookup"><span data-stu-id="88bb5-144">You can use [Azure Diagnostics](cloud-services-dotnet-diagnostics.md) to obtain information about running role instances.</span></span>
> 
> 

<span data-ttu-id="88bb5-145">Чтобы определить номер порта внутренней конечной точки экземпляра роли, можно использовать свойство [InstanceEndpoints](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.instanceendpoints.aspx) , чтобы вернуть объект Dictionary, содержащий имена конечных точек и их IP-адреса и порты.</span><span class="sxs-lookup"><span data-stu-id="88bb5-145">To determine the port number for an internal endpoint on a role instance, you can use the [InstanceEndpoints](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.instanceendpoints.aspx) property to return a Dictionary object that contains endpoint names and their corresponding IP addresses and ports.</span></span> <span data-ttu-id="88bb5-146">Свойство [IPEndpoint](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstanceendpoint.ipendpoint.aspx) возвращает IP-адрес и порт указанной конечной точкой.</span><span class="sxs-lookup"><span data-stu-id="88bb5-146">The [IPEndpoint](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstanceendpoint.ipendpoint.aspx) property returns the IP address and port for a specified endpoint.</span></span> <span data-ttu-id="88bb5-147">Свойство **PublicIPEndpoint** возвращает порт для конечной точки с балансировкой нагрузки.</span><span class="sxs-lookup"><span data-stu-id="88bb5-147">The **PublicIPEndpoint** property returns the port for a load balanced endpoint.</span></span> <span data-ttu-id="88bb5-148">Часть IP-адреса в свойстве **PublicIPEndpoint** не используется.</span><span class="sxs-lookup"><span data-stu-id="88bb5-148">The IP address portion of the **PublicIPEndpoint** property is not used.</span></span>

<span data-ttu-id="88bb5-149">Вот пример, в котором выполняется итерация экземпляров роли.</span><span class="sxs-lookup"><span data-stu-id="88bb5-149">Here is an example that iterates role instances.</span></span>

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

<span data-ttu-id="88bb5-150">Ниже приведен пример рабочей роли, которая получает конечную точку, предоставляемую через определение службы, и начинает прослушивание подключений.</span><span class="sxs-lookup"><span data-stu-id="88bb5-150">Here is an example of a worker role that gets the endpoint exposed through the service definition and starts listening for connections.</span></span>

> [!WARNING]
> <span data-ttu-id="88bb5-151">Этот код будет работать только для развернутой службы.</span><span class="sxs-lookup"><span data-stu-id="88bb5-151">This code will only work for a deployed service.</span></span> <span data-ttu-id="88bb5-152">При выполнении в эмуляторе вычислений Azure элементы конфигурации службы, создающие конечные точки прямых портов (элементы**InstanceInputEndpoint** ), игнорируются.</span><span class="sxs-lookup"><span data-stu-id="88bb5-152">When running in the Azure Compute Emulator, service configuration elements that create direct port endpoints (**InstanceInputEndpoint** elements) are ignored.</span></span>
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

        // Bind socket listener to internal endpoint and listen
        listener.Bind(myInternalEp);
        listener.Listen(10);
        Trace.TraceInformation("Listening on IP:{0},Port: {1}",
          myInternalEp.Address, myInternalEp.Port);

        while (true)
        {
          // Block the thread and wait for a client request
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
      // Set the maximum number of concurrent connections 
      ServicePointManager.DefaultConnectionLimit = 12;

      // For information on handling configuration changes
      // see the MSDN topic at http://go.microsoft.com/fwlink/?LinkId=166357.
      return base.OnStart();
    }
  }
}
```

## <a name="network-traffic-rules-to-control-role-communication"></a><span data-ttu-id="88bb5-153">Правила сетевого трафика для управления обменом данными между ролями</span><span class="sxs-lookup"><span data-stu-id="88bb5-153">Network traffic rules to control role communication</span></span>
<span data-ttu-id="88bb5-154">После определения внутренних конечных точек можно добавить правила сетевого трафика (на основании созданных конечных точек), чтобы управлять обменом данными между экземплярами роли.</span><span class="sxs-lookup"><span data-stu-id="88bb5-154">After you define internal endpoints, you can add network traffic rules (based on the endpoints that you created) to control how role instances can communicate with each other.</span></span> <span data-ttu-id="88bb5-155">На следующей схеме показаны некоторые общие сценарии управления обменом данными между ролями:</span><span class="sxs-lookup"><span data-stu-id="88bb5-155">The following diagram shows some common scenarios for controlling role communication:</span></span>

<span data-ttu-id="88bb5-156">![Сценарии использования правил сетевого трафика](./media/cloud-services-enable-communication-role-instances/scenarios.png "Сценарии использования правил сетевого трафика")</span><span class="sxs-lookup"><span data-stu-id="88bb5-156">![Network Traffic Rules Scenarios](./media/cloud-services-enable-communication-role-instances/scenarios.png "Network Traffic Rules Scenarios")</span></span>

<span data-ttu-id="88bb5-157">В следующем примере кода показаны определения ролей, показанных на предыдущей схеме.</span><span class="sxs-lookup"><span data-stu-id="88bb5-157">The following code example shows role definitions for the roles shown in the previous diagram.</span></span> <span data-ttu-id="88bb5-158">В каждом определении роли определена по крайней мере одна внутренняя конечная точка:</span><span class="sxs-lookup"><span data-stu-id="88bb5-158">Each role definition includes at least one internal endpoint defined:</span></span>

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
> <span data-ttu-id="88bb5-159">Обмен данными между ролями с внутренним конечными точками с фиксированными и автоматически назначенными портами может быть ограничен.</span><span class="sxs-lookup"><span data-stu-id="88bb5-159">Restriction of communication between roles can occur with internal endpoints of both fixed and automatically assigned ports.</span></span>
> 
> 

<span data-ttu-id="88bb5-160">По умолчанию после определения внутренней конечной точки данные могут передаваться из одной роли во внутреннюю конечную точку другой роли без каких-либо ограничений.</span><span class="sxs-lookup"><span data-stu-id="88bb5-160">By default, after an internal endpoint is defined, communication can flow from any role to the internal endpoint of a role without any restrictions.</span></span> <span data-ttu-id="88bb5-161">Чтобы ограничить обмен данными, необходимо добавить элемент **NetworkTrafficRules** в элемент **ServiceDefinition** в файле определения службы.</span><span class="sxs-lookup"><span data-stu-id="88bb5-161">To restrict communication, you must add a **NetworkTrafficRules** element to the **ServiceDefinition** element in the service definition file.</span></span>

### <a name="scenario-1"></a><span data-ttu-id="88bb5-162">Сценарий 1</span><span class="sxs-lookup"><span data-stu-id="88bb5-162">Scenario 1</span></span>
<span data-ttu-id="88bb5-163">Разрешен только сетевой трафик из **WebRole1** в **WorkerRole1**.</span><span class="sxs-lookup"><span data-stu-id="88bb5-163">Only allow network traffic from **WebRole1** to **WorkerRole1**.</span></span>

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

### <a name="scenario-2"></a><span data-ttu-id="88bb5-164">Сценарий 2</span><span class="sxs-lookup"><span data-stu-id="88bb5-164">Scenario 2</span></span>
<span data-ttu-id="88bb5-165">Разрешен только сетевой трафик из **WebRole1** в **WorkerRole1** и **WorkerRole2**.</span><span class="sxs-lookup"><span data-stu-id="88bb5-165">Only allows network traffic from **WebRole1** to **WorkerRole1** and **WorkerRole2**.</span></span>

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

### <a name="scenario-3"></a><span data-ttu-id="88bb5-166">Сценарий 3</span><span class="sxs-lookup"><span data-stu-id="88bb5-166">Scenario 3</span></span>
<span data-ttu-id="88bb5-167">Разрешен только сетевой трафик из **WebRole1** в **WorkerRole1** и из **WorkerRole1** в **WorkerRole2**.</span><span class="sxs-lookup"><span data-stu-id="88bb5-167">Only allows network traffic from **WebRole1** to **WorkerRole1**, and **WorkerRole1** to **WorkerRole2**.</span></span>

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

### <a name="scenario-4"></a><span data-ttu-id="88bb5-168">Сценарий 4</span><span class="sxs-lookup"><span data-stu-id="88bb5-168">Scenario 4</span></span>
<span data-ttu-id="88bb5-169">Разрешен только сетевой трафик из **WebRole1** в **WorkerRole1**, из **WebRole1** в **WorkerRole2** и из **WorkerRole1** в **WorkerRole2**.</span><span class="sxs-lookup"><span data-stu-id="88bb5-169">Only allows network traffic from **WebRole1** to **WorkerRole1**, **WebRole1** to **WorkerRole2**, and **WorkerRole1** to **WorkerRole2**.</span></span>

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

<span data-ttu-id="88bb5-170">Справочник по схеме XML для элементов, используемых выше, можно найти [здесь](https://msdn.microsoft.com/library/azure/gg557551.aspx).</span><span class="sxs-lookup"><span data-stu-id="88bb5-170">An XML schema reference for the elements used above can be found [here](https://msdn.microsoft.com/library/azure/gg557551.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="88bb5-171">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="88bb5-171">Next steps</span></span>
<span data-ttu-id="88bb5-172">Дополнительная информация о [модели](cloud-services-model-and-package.md)облачной службы</span><span class="sxs-lookup"><span data-stu-id="88bb5-172">Read more about the Cloud Service [model](cloud-services-model-and-package.md).</span></span>

