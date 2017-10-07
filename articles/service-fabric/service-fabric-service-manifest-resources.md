---
title: "конечные точки службы Service Fabric aaaSpecifying | Документы Microsoft"
description: "Как манифеста toodescribe ресурсы конечной точки в службе, включая то, как tooset настройке конечных точек HTTPS"
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: da36cbdb-6531-4dae-88e8-a311ab71520d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: subramar
ms.openlocfilehash: a4ebee353ce5cf86583673674246094f03f368be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="specify-resources-in-a-service-manifest"></a>Указание ресурсов в манифесте службы
## <a name="overview"></a>Обзор
манифест службы Hello позволяет ресурсы, используемые с toobe службы hello объявлен или изменен без изменения кода hello компиляции. Azure Service Fabric поддерживает конфигурацию ресурсов конечной точки для службы hello. Hello доступа toohello ресурсы, которые указаны в манифесте hello службы можно управлять через hello SecurityGroup в манифесте приложения hello. объявления Hello ресурсов позволяет toobe эти ресурсы, изменен во время развертывания, это означает, что служба hello не требует toointroduce новый механизм настройки. Hello определение схемы для hello файле ServiceManifest.xml устанавливается вместе с hello Service Fabric SDK и средств слишком*C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.

## <a name="endpoints"></a>Endpoints
Когда ресурс конечной точки задается в манифест службы hello, Service Fabric назначает порты из диапазона портов приложения hello защищены, если порт не указан явно. Например, рассмотрим hello конечной точки *ServiceEndpoint1* указан в фрагменте hello манифеста, указываемая после абзаца. Кроме того, службы также могут запрашивать наличие в ресурсе конкретного порта. Реплики службы, которые выполняются на узлах кластера на другой можно назначить разные номера портов, пока реплики службы, запущенной hello тот же порт hello папки узла. Hello реплик службы можно использовать эти порты при необходимости для репликации и прослушивает клиентские запросы.

```xml
<Resources>
  <Endpoints>
    <Endpoint Name="ServiceEndpoint1" Protocol="http"/>
    <Endpoint Name="ServiceEndpoint2" Protocol="http" Port="80"/>
    <Endpoint Name="ServiceEndpoint3" Protocol="https"/>
  </Endpoints>
</Resources>
```

См. слишком[Настройка надежных служб с отслеживанием состояния](service-fabric-reliable-services-configuration.md) tooread Дополнительные сведения о ссылке на конечные точки из файла параметров конфигурации пакета hello (settings.xml).

## <a name="example-specifying-an-http-endpoint-for-your-service"></a>Пример. Указание конечной точки HTTP для службы
Hello ниже манифест службы определяет один ресурс конечной точки TCP и два ресурса конечной точки HTTP в hello &lt;ресурсов&gt; элемента.

Service Fabric автоматически создает список управления доступом (ACL) для конечных точек HTTP.

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceManifest Name="Stateful1Pkg"
                 Version="1.0.0"
                 xmlns="http://schemas.microsoft.com/2011/01/fabric"
                 xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <ServiceTypes>
    <!-- This is hello name of your ServiceType.
         This name must match hello string used in hello RegisterServiceType call in Program.cs. -->
    <StatefulServiceType ServiceTypeName="Stateful1Type" HasPersistedState="true" />
  </ServiceTypes>

  <!-- Code package is your service executable. -->
  <CodePackage Name="Code" Version="1.0.0">
    <EntryPoint>
      <ExeHost>
        <Program>Stateful1.exe</Program>
      </ExeHost>
    </EntryPoint>
  </CodePackage>

  <!-- Config package is hello contents of hello Config directoy under PackageRoot that contains an
       independently updateable and versioned set of custom configuration settings for your service. -->
  <ConfigPackage Name="Config" Version="1.0.0" />

  <Resources>
    <Endpoints>
      <!-- This endpoint is used by hello communication listener tooobtain hello port number on which to
           listen. Note that if your service is partitioned, this port is shared with
           replicas of different partitions that are placed in your code. -->
      <Endpoint Name="ServiceEndpoint1" Protocol="http"/>
      <Endpoint Name="ServiceEndpoint2" Protocol="http" Port="80"/>
      <Endpoint Name="ServiceEndpoint3" Protocol="https"/>

      <!-- This endpoint is used by hello replicator for replicating hello state of your service.
           This endpoint is configured through hello ReplicatorSettings config section in hello Settings.xml
           file under hello ConfigPackage. -->
      <Endpoint Name="ReplicatorEndpoint" />
    </Endpoints>
  </Resources>
</ServiceManifest>
```

## <a name="example-specifying-an-https-endpoint-for-your-service"></a>Пример. Указание конечной точки HTTPS для службы
Hello протокол HTTPS обеспечивает проверку подлинности сервера, а также используется для шифрования передаваемых данных клиент сервер. tooenable HTTPS в службе Service Fabric, необходимо указать протокол hello в hello *ресурсы "->" конечные точки -> конечная точка* раздел манифеста службы hello, как показано выше, для конечной точки hello *ServiceEndpoint3* .

> [!NOTE]
> Протокол службы невозможно изменить при обновлении приложения. Если изменить его во время обновления, то это будет считаться критическим изменением.
> 
> 

Ниже приведен пример ApplicationManifest необходимость tooset для HTTPS. необходимо указать Hello отпечаток сертификата. Hello EndpointRef является tooEndpointResource ссылку в ServiceManifest, для которых задан протокол HTTPS hello. Можно добавить несколько элементов Endpointcertificate.  

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest ApplicationTypeName="Application1Type"
                     ApplicationTypeVersion="1.0.0"
                     xmlns="http://schemas.microsoft.com/2011/01/fabric"
                     xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                     xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <Parameters>
    <Parameter Name="Stateful1_MinReplicaSetSize" DefaultValue="3" />
    <Parameter Name="Stateful1_PartitionCount" DefaultValue="1" />
    <Parameter Name="Stateful1_TargetReplicaSetSize" DefaultValue="3" />
  </Parameters>
  <!-- Import hello ServiceManifest from hello ServicePackage. hello ServiceManifestName and ServiceManifestVersion
       should match hello Name and Version attributes of hello ServiceManifest element defined in the
       ServiceManifest.xml file. -->
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="Stateful1Pkg" ServiceManifestVersion="1.0.0" />
    <ConfigOverrides />
    <Policies>
      <EndpointBindingPolicy CertificateRef="TestCert1" EndpointRef="ServiceEndpoint3"/>
    </Policies>
  </ServiceManifestImport>
  <DefaultServices>
    <!-- hello section below creates instances of service types when an instance of this
         application type is created. You can also create one or more instances of service type by using the
         Service Fabric PowerShell module.

         hello attribute ServiceTypeName below must match hello name defined in hello imported ServiceManifest.xml file. -->
    <Service Name="Stateful1">
      <StatefulService ServiceTypeName="Stateful1Type" TargetReplicaSetSize="[Stateful1_TargetReplicaSetSize]" MinReplicaSetSize="[Stateful1_ ]">
        <UniformInt64Partition PartitionCount="[Stateful1_PartitionCount]" LowKey="-9223372036854775808" HighKey="9223372036854775807" />
      </StatefulService>
    </Service>
  </DefaultServices>
  <Certificates>
    <EndpointCertificate Name="TestCert1" X509FindValue="FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF F0" X509StoreName="MY" />  
  </Certificates>
</ApplicationManifest>
```

## <a name="overriding-endpoints-in-servicemanifestxml"></a>Переопределение конечных точек в файле ServiceManifest.xml

В hello ApplicationManifest добавьте ResourceOverrides раздела, в котором будет раздел tooConfigOverrides того же уровня. В этом разделе можно указать hello переопределения для раздела hello конечные точки в раздел ресурсов hello, указанного в манифесте службы hello.

В порядке toooverride конечной точки в ServiceManifest ApplicationParameters изменений с помощью hello ApplicationManifest следующим образом:

В разделе ServiceManifestImport hello добавьте новый раздел «ResourceOverrides»

```xml
<ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="Stateless1Pkg" ServiceManifestVersion="1.0.0" />
    <ConfigOverrides />
    <ResourceOverrides>
      <Endpoints>
        <Endpoint Name="ServiceEndpoint" Port="[Port]" Protocol="[Protocol]" Type="[Type]" />
        <Endpoint Name="ServiceEndpoint1" Port="[Port1]" Protocol="[Protocol1] "/>
      </Endpoints>
    </ResourceOverrides>
        <Policies>
           <EndpointBindingPolicy CertificateRef="TestCert1" EndpointRef="ServiceEndpoint"/>
        </Policies>
  </ServiceManifestImport>
```

В окне приветствия добавления параметров ниже:

```xml
  <Parameters>
    <Parameter Name="Port" DefaultValue="" />
    <Parameter Name="Protocol" DefaultValue="" />
    <Parameter Name="Type" DefaultValue="" />
    <Parameter Name="Port1" DefaultValue="" />
    <Parameter Name="Protocol1" DefaultValue="" />
  </Parameters>
```

При развертывании приложения hello теперь можно передать в эти значения как ApplicationParameters например:

```powershell
PS C:\> New-ServiceFabricApplication -ApplicationName fabric:/myapp -ApplicationTypeName "AppType" -ApplicationTypeVersion "1.0.0" -ApplicationParameter @{Port='1001'; Protocol='https'; Type='Input'; Port1='2001'; Protocol='http'}
```

Примечание: Если значения hello предоставляют для hello ApplicationParameters пуст вернемся toohello по умолчанию значение, указанное в hello ServiceManifest для соответствующего EndPointName hello.

Например:

Если в hello указанной ServiceManifest

```xml
  <Resources>
    <Endpoints>
      <Endpoint Name="ServiceEndpoint1" Protocol="tcp"/>
    </Endpoints>
  </Resources>
```

Здравствуйте порта 1 и Protocol1 значения параметров приложения имеет значение null или пустым. порт Hello по-прежнему определяется по ServiceFabric. И hello протокола tcp.

Предположим, что вы задали неверное значение. Например, для порта задано строковое значение Foo вместо целого числа.  Новый ServiceFabricApplication команда завершится с ошибкой: недопустимый параметр переопределения hello с атрибутом «ServiceEndpoint1» имя порта «1» в разделе «ResourceOverrides». Указанное значение Hello «Foo» и требуется «int».
