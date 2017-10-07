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
# <a name="enable-communication-for-role-instances-in-azure"></a>Включение обмена данными между экземплярами роли в Azure
Ролей облачной службы взаимодействуют через внутренние и внешние подключения. Внешние подключения называются **входными конечными точками**, а внутренние подключения — **внутренними конечными точками**. В этом разделе описывается способ toomodify hello [службы определение](cloud-services-model-and-package.md#csdef) toocreate конечных точек.

## <a name="input-endpoint"></a>Входная конечная точка
Конечная точка ввода Hello используется в том случае, если tooexpose toohello порт за пределами. Укажите тип hello протокола и порта hello hello конечной точки, которая применяется для hello внешних и внутренних портов для конечной точки hello. Если требуется, можно указать другой внутренний порт для конечной точки hello с hello [localPort](https://msdn.microsoft.com/library/azure/gg557552.aspx#InputEndpoint) атрибута.

Конечная точка ввода Hello можно использовать следующие протоколы hello: **http, https, tcp, udp**.

добавить конечную точку ввода, toocreate hello **InputEndpoint** toohello дочерний элемент **конечные точки** элемент web и рабочей роли.

```xml
<Endpoints>
  <InputEndpoint name="StandardWeb" protocol="http" port="80" localPort="80" />
</Endpoints> 
```

## <a name="instance-input-endpoint"></a>Входная конечная точка экземпляра
Аналогично конечные точки tooinput входные конечные точки, но позволяет сопоставить определенные порты общедоступным для каждого экземпляра отдельные роли благодаря перенаправлению портов в подсистеме балансировки нагрузки hello. Можно указать один общедоступный порт или диапазон портов.

можно использовать только конечная точка ввода экземпляра Hello **tcp** или **udp** в качестве протокола hello.

добавить конечные точки ввода экземпляра toocreate hello **InstanceInputEndpoint** дочерний элемент toohello **конечные точки** элемент web и рабочей роли.

```xml
<Endpoints>
  <InstanceInputEndpoint name="Endpoint2" protocol="tcp" localPort="10100">
    <AllocatePublicPortFrom>
      <FixedPortRange max="10109" min="10105" />
    </AllocatePublicPortFrom>
  </InstanceInputEndpoint>
</Endpoints>
```

## <a name="internal-endpoint"></a>Внутренняя конечная точка
Внутренние конечные точки доступны для подключения между экземплярами. Hello порт является необязательным, и если не указано, динамический порт назначается toohello конечной точки. Можно использовать диапазон портов. Существует ограничение: до 5 внутренних конечных точек на роль.

Hello внутренней конечной точки можно использовать следующие протоколы hello: **http, tcp, udp, любой**.

toocreate внутренней конечной точки ввода, добавить hello **InternalEndpoint** дочерний элемент toohello **конечные точки** элемент web и рабочей роли.

```xml
<Endpoints>
  <InternalEndpoint name="Endpoint3" protocol="any" port="8999" />
</Endpoints> 
```

Можно также использовать диапазон портов.

```xml
<Endpoints>
  <InternalEndpoint name="Endpoint3" protocol="any">
    <FixedPortRange max="8995" min="8999" />
  </InternalEndpoint>
</Endpoints>
```


## <a name="worker-roles-vs-web-roles"></a>Рабочие роли и Веб-роли
При работе с веб-ролями и рабочими ролями существует одно незначительное отличие, связанное с конечными точками. Hello веб-роль должна иметь как минимум одну конечную точку ввода с помощью hello **HTTP** протокола.

```xml
<Endpoints>
  <InputEndpoint name="StandardWeb" protocol="http" port="80" localPort="80" />
  <!-- more endpoints may be declared after hello first InputEndPoint -->
</Endpoints>
```

## <a name="using-hello-net-sdk-tooaccess-an-endpoint"></a>С помощью tooaccess .NET SDK hello конечной точки
Hello управляемая библиотека Azure предоставляет методы для toocommunicate экземпляров ролей во время выполнения. Из кода, выполняемого в экземпляре роли можно получить сведения о hello наличие других экземпляров ролей и их конечные точки, а также сведения о текущей роли экземпляра hello.

> [!NOTE]
> Можно получать сведения только о тех экземплярах, которые запущены в облачной службе и для которых определена по крайней мере одна внутренняя конечная точка. Нельзя получить данные об экземплярах роли, запущенных в другой службе.
> 
> 

Можно использовать hello [экземпляров](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.role.instances.aspx) свойство tooretrieve экземпляров роли. Сначала с помощью hello [CurrentRoleInstance](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.currentroleinstance.aspx) tooreturn ссылки toohello текущей роли, а затем используйте hello [роли](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.role.aspx) свойство tooreturn самой роли toohello ссылки.

При подключении экземпляра роли tooa программно через hello .NET SDK, это относительно легко tooaccess сведения о конечной точке hello. Например после вы уже подключены среды tooa определенной роли, можно получить порт hello определенной конечной точке с этим кодом:

```csharp
int port = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["StandardWeb"].IPEndpoint.Port;
```

Hello **экземпляров** свойство возвращает коллекцию **RoleInstance** объектов. Эта коллекция всегда содержит текущий экземпляр hello. Если роль hello не определяет внутреннюю конечную точку, коллекция hello включает hello текущего экземпляра, но не другие экземпляры. Hello число экземпляров роли в коллекции hello всегда будет 1 в случае hello, где нет внутренней конечной точки для роли hello. Если роль hello определяет внутреннюю конечную точку, его экземпляры могут быть обнаружены во время выполнения, и hello число экземпляров в коллекции hello будет соответствовать toohello число экземпляров, указанные для роли hello в файл конфигурации службы hello.

> [!NOTE]
> Hello управляемая библиотека Azure не предоставляет средства определения работоспособности hello других экземпляров роли, но вы можно реализовать самостоятельно Если службе нужна подобная функциональность. Можно использовать [диагностики Azure](cloud-services-dotnet-diagnostics.md) tooobtain сведения о выполнении экземпляров роли.
> 
> 

toodetermine hello номер порта для внутренней конечной точки в экземпляре роли, можно использовать hello [InstanceEndpoints](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstance.instanceendpoints.aspx) tooreturn свойство объект словаря, который содержит имена конечных точек и их соответствующие IP-адреса и порты. Hello [IPEndpoint](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleinstanceendpoint.ipendpoint.aspx) свойство возвращает hello IP-адрес и порт для указанной конечной точкой. Hello **PublicIPEndpoint** свойство возвращает hello порт для конечной точки с балансировкой нагрузки. часть Hello IP-адреса hello **PublicIPEndpoint** свойство не используется.

Вот пример, в котором выполняется итерация экземпляров роли.

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

Ниже приведен пример рабочей роли, который получает конечную точку hello, предоставленную до определения службы hello и начинает прослушивание подключений.

> [!WARNING]
> Этот код будет работать только для развернутой службы. При выполнении в эмуляторе вычислений Azure hello службы элементы конфигурации для создания конечных точек прямого порта (**InstanceInputEndpoint** элементов) учитываются.
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

## <a name="network-traffic-rules-toocontrol-role-communication"></a>Роль правил трафика toocontrol сетью
После задания внутренних конечных точек можно добавить сетевого трафика (hello конечных точек, которые были созданы с учетом) правила toocontrol как экземпляры роли могут взаимодействовать друг с другом. Hello следующей диаграмме показаны некоторые общие сценарии по управлению взаимодействием ролей:

![Сценарии использования правил сетевого трафика](./media/cloud-services-enable-communication-role-instances/scenarios.png "Сценарии использования правил сетевого трафика")

Hello примере кода показан определения роли для роли hello hello предыдущей иллюстрации. В каждом определении роли определена по крайней мере одна внутренняя конечная точка:

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
> Обмен данными между ролями с внутренним конечными точками с фиксированными и автоматически назначенными портами может быть ограничен.
> 
> 

По умолчанию определив внутреннюю конечную точку, могут передаваться из любой роли toohello внутренней конечной точке другой роли без каких-либо ограничений. toorestrict связи, необходимо добавить **NetworkTrafficRules** toohello элемент **ServiceDefinition** элемент в файле определения службы hello.

### <a name="scenario-1"></a>Сценарий 1
Разрешить только сетевой трафик от **WebRole1** слишком**WorkerRole1**.

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

### <a name="scenario-2"></a>Сценарий 2
Разрешен только сетевой трафик от **WebRole1** слишком**WorkerRole1** и **WorkerRole2**.

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

### <a name="scenario-3"></a>Сценарий 3
Разрешен только сетевой трафик от **WebRole1** слишком**WorkerRole1**, и **WorkerRole1** слишком**WorkerRole2**.

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

### <a name="scenario-4"></a>Сценарий 4
Разрешен только сетевой трафик от **WebRole1** слишком**WorkerRole1**, **WebRole1** слишком**WorkerRole2**, и  **WorkerRole1** слишком**WorkerRole2**.

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

Справочник по схеме XML для элементов hello выше можно найти [здесь](https://msdn.microsoft.com/library/azure/gg557551.aspx).

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения о hello облачной службы [модели](cloud-services-model-and-package.md).

