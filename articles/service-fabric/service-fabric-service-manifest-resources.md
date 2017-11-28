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
# <a name="specify-resources-in-a-service-manifest"></a><span data-ttu-id="bf8cc-103">Указание ресурсов в манифесте службы</span><span class="sxs-lookup"><span data-stu-id="bf8cc-103">Specify resources in a service manifest</span></span>
## <a name="overview"></a><span data-ttu-id="bf8cc-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="bf8cc-104">Overview</span></span>
<span data-ttu-id="bf8cc-105">манифест службы Hello позволяет ресурсы, используемые с toobe службы hello объявлен или изменен без изменения кода hello компиляции.</span><span class="sxs-lookup"><span data-stu-id="bf8cc-105">hello service manifest allows resources that are used by hello service toobe declared/changed without changing hello compiled code.</span></span> <span data-ttu-id="bf8cc-106">Azure Service Fabric поддерживает конфигурацию ресурсов конечной точки для службы hello.</span><span class="sxs-lookup"><span data-stu-id="bf8cc-106">Azure Service Fabric supports configuration of endpoint resources for hello service.</span></span> <span data-ttu-id="bf8cc-107">Hello доступа toohello ресурсы, которые указаны в манифесте hello службы можно управлять через hello SecurityGroup в манифесте приложения hello.</span><span class="sxs-lookup"><span data-stu-id="bf8cc-107">hello access toohello resources that are specified in hello service manifest can be controlled via hello SecurityGroup in hello application manifest.</span></span> <span data-ttu-id="bf8cc-108">объявления Hello ресурсов позволяет toobe эти ресурсы, изменен во время развертывания, это означает, что служба hello не требует toointroduce новый механизм настройки.</span><span class="sxs-lookup"><span data-stu-id="bf8cc-108">hello declaration of resources allows these resources toobe changed at deployment time, meaning hello service doesn't need toointroduce a new configuration mechanism.</span></span> <span data-ttu-id="bf8cc-109">Hello определение схемы для hello файле ServiceManifest.xml устанавливается вместе с hello Service Fabric SDK и средств слишком*C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span><span class="sxs-lookup"><span data-stu-id="bf8cc-109">hello schema definition for hello ServiceManifest.xml file is installed with hello Service Fabric SDK and tools too*C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span></span>

## <a name="endpoints"></a><span data-ttu-id="bf8cc-110">Endpoints</span><span class="sxs-lookup"><span data-stu-id="bf8cc-110">Endpoints</span></span>
<span data-ttu-id="bf8cc-111">Когда ресурс конечной точки задается в манифест службы hello, Service Fabric назначает порты из диапазона портов приложения hello защищены, если порт не указан явно.</span><span class="sxs-lookup"><span data-stu-id="bf8cc-111">When an endpoint resource is defined in hello service manifest, Service Fabric assigns ports from hello reserved application port range when a port isn't specified explicitly.</span></span> <span data-ttu-id="bf8cc-112">Например, рассмотрим hello конечной точки *ServiceEndpoint1* указан в фрагменте hello манифеста, указываемая после абзаца.</span><span class="sxs-lookup"><span data-stu-id="bf8cc-112">For example, look at hello endpoint *ServiceEndpoint1* specified in hello manifest snippet provided after this paragraph.</span></span> <span data-ttu-id="bf8cc-113">Кроме того, службы также могут запрашивать наличие в ресурсе конкретного порта.</span><span class="sxs-lookup"><span data-stu-id="bf8cc-113">Additionally, services can also request a specific port in a resource.</span></span> <span data-ttu-id="bf8cc-114">Реплики службы, которые выполняются на узлах кластера на другой можно назначить разные номера портов, пока реплики службы, запущенной hello тот же порт hello папки узла.</span><span class="sxs-lookup"><span data-stu-id="bf8cc-114">Service replicas running on different cluster nodes can be assigned different port numbers, while replicas of a service running on hello same node share hello port.</span></span> <span data-ttu-id="bf8cc-115">Hello реплик службы можно использовать эти порты при необходимости для репликации и прослушивает клиентские запросы.</span><span class="sxs-lookup"><span data-stu-id="bf8cc-115">hello service replicas can then use these ports as needed for replication and listening for client requests.</span></span>

```xml
<Resources>
  <Endpoints>
    <Endpoint Name="ServiceEndpoint1" Protocol="http"/>
    <Endpoint Name="ServiceEndpoint2" Protocol="http" Port="80"/>
    <Endpoint Name="ServiceEndpoint3" Protocol="https"/>
  </Endpoints>
</Resources>
```

<span data-ttu-id="bf8cc-116">См. слишком[Настройка надежных служб с отслеживанием состояния](service-fabric-reliable-services-configuration.md) tooread Дополнительные сведения о ссылке на конечные точки из файла параметров конфигурации пакета hello (settings.xml).</span><span class="sxs-lookup"><span data-stu-id="bf8cc-116">Refer too[Configuring stateful Reliable Services](service-fabric-reliable-services-configuration.md) tooread more about referencing endpoints from hello config package settings file (settings.xml).</span></span>

## <a name="example-specifying-an-http-endpoint-for-your-service"></a><span data-ttu-id="bf8cc-117">Пример. Указание конечной точки HTTP для службы</span><span class="sxs-lookup"><span data-stu-id="bf8cc-117">Example: specifying an HTTP endpoint for your service</span></span>
<span data-ttu-id="bf8cc-118">Hello ниже манифест службы определяет один ресурс конечной точки TCP и два ресурса конечной точки HTTP в hello &lt;ресурсов&gt; элемента.</span><span class="sxs-lookup"><span data-stu-id="bf8cc-118">hello following service manifest defines one TCP endpoint resource and two HTTP endpoint resources in hello &lt;Resources&gt; element.</span></span>

<span data-ttu-id="bf8cc-119">Service Fabric автоматически создает список управления доступом (ACL) для конечных точек HTTP.</span><span class="sxs-lookup"><span data-stu-id="bf8cc-119">HTTP endpoints are automatically ACL'd by Service Fabric.</span></span>

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

## <a name="example-specifying-an-https-endpoint-for-your-service"></a><span data-ttu-id="bf8cc-120">Пример. Указание конечной точки HTTPS для службы</span><span class="sxs-lookup"><span data-stu-id="bf8cc-120">Example: specifying an HTTPS endpoint for your service</span></span>
<span data-ttu-id="bf8cc-121">Hello протокол HTTPS обеспечивает проверку подлинности сервера, а также используется для шифрования передаваемых данных клиент сервер.</span><span class="sxs-lookup"><span data-stu-id="bf8cc-121">hello HTTPS protocol provides server authentication and is also used for encrypting client-server communication.</span></span> <span data-ttu-id="bf8cc-122">tooenable HTTPS в службе Service Fabric, необходимо указать протокол hello в hello *ресурсы "->" конечные точки -> конечная точка* раздел манифеста службы hello, как показано выше, для конечной точки hello *ServiceEndpoint3* .</span><span class="sxs-lookup"><span data-stu-id="bf8cc-122">tooenable HTTPS on your Service Fabric service, specify hello protocol in hello *Resources -> Endpoints -> Endpoint* section of hello service manifest, as shown earlier for hello endpoint *ServiceEndpoint3*.</span></span>

> [!NOTE]
> <span data-ttu-id="bf8cc-123">Протокол службы невозможно изменить при обновлении приложения.</span><span class="sxs-lookup"><span data-stu-id="bf8cc-123">A service’s protocol cannot be changed during application upgrade.</span></span> <span data-ttu-id="bf8cc-124">Если изменить его во время обновления, то это будет считаться критическим изменением.</span><span class="sxs-lookup"><span data-stu-id="bf8cc-124">If it is changed during upgrade, it is a breaking change.</span></span>
> 
> 

<span data-ttu-id="bf8cc-125">Ниже приведен пример ApplicationManifest необходимость tooset для HTTPS.</span><span class="sxs-lookup"><span data-stu-id="bf8cc-125">Here is an example ApplicationManifest that you need tooset for HTTPS.</span></span> <span data-ttu-id="bf8cc-126">необходимо указать Hello отпечаток сертификата.</span><span class="sxs-lookup"><span data-stu-id="bf8cc-126">hello thumbprint for your certificate must be provided.</span></span> <span data-ttu-id="bf8cc-127">Hello EndpointRef является tooEndpointResource ссылку в ServiceManifest, для которых задан протокол HTTPS hello.</span><span class="sxs-lookup"><span data-stu-id="bf8cc-127">hello EndpointRef is a reference tooEndpointResource in ServiceManifest, for which you set hello HTTPS protocol.</span></span> <span data-ttu-id="bf8cc-128">Можно добавить несколько элементов Endpointcertificate.</span><span class="sxs-lookup"><span data-stu-id="bf8cc-128">You can add more than one EndpointCertificate.</span></span>  

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

## <a name="overriding-endpoints-in-servicemanifestxml"></a><span data-ttu-id="bf8cc-129">Переопределение конечных точек в файле ServiceManifest.xml</span><span class="sxs-lookup"><span data-stu-id="bf8cc-129">Overriding Endpoints in ServiceManifest.xml</span></span>

<span data-ttu-id="bf8cc-130">В hello ApplicationManifest добавьте ResourceOverrides раздела, в котором будет раздел tooConfigOverrides того же уровня.</span><span class="sxs-lookup"><span data-stu-id="bf8cc-130">In hello ApplicationManifest add a ResourceOverrides section which will be a sibling tooConfigOverrides section.</span></span> <span data-ttu-id="bf8cc-131">В этом разделе можно указать hello переопределения для раздела hello конечные точки в раздел ресурсов hello, указанного в манифесте службы hello.</span><span class="sxs-lookup"><span data-stu-id="bf8cc-131">In this section you can specify hello override for hello Endpoints section in hello resources section specified in hello Service manifest.</span></span>

<span data-ttu-id="bf8cc-132">В порядке toooverride конечной точки в ServiceManifest ApplicationParameters изменений с помощью hello ApplicationManifest следующим образом:</span><span class="sxs-lookup"><span data-stu-id="bf8cc-132">In order toooverride EndPoint in ServiceManifest using ApplicationParameters change hello ApplicationManifest as following:</span></span>

<span data-ttu-id="bf8cc-133">В разделе ServiceManifestImport hello добавьте новый раздел «ResourceOverrides»</span><span class="sxs-lookup"><span data-stu-id="bf8cc-133">In hello ServiceManifestImport section add a new section "ResourceOverrides"</span></span>

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

<span data-ttu-id="bf8cc-134">В окне приветствия добавления параметров ниже:</span><span class="sxs-lookup"><span data-stu-id="bf8cc-134">In hello Parameters add below:</span></span>

```xml
  <Parameters>
    <Parameter Name="Port" DefaultValue="" />
    <Parameter Name="Protocol" DefaultValue="" />
    <Parameter Name="Type" DefaultValue="" />
    <Parameter Name="Port1" DefaultValue="" />
    <Parameter Name="Protocol1" DefaultValue="" />
  </Parameters>
```

<span data-ttu-id="bf8cc-135">При развертывании приложения hello теперь можно передать в эти значения как ApplicationParameters например:</span><span class="sxs-lookup"><span data-stu-id="bf8cc-135">While deploying hello application now you can pass in these values as ApplicationParameters for example:</span></span>

```powershell
PS C:\> New-ServiceFabricApplication -ApplicationName fabric:/myapp -ApplicationTypeName "AppType" -ApplicationTypeVersion "1.0.0" -ApplicationParameter @{Port='1001'; Protocol='https'; Type='Input'; Port1='2001'; Protocol='http'}
```

<span data-ttu-id="bf8cc-136">Примечание: Если значения hello предоставляют для hello ApplicationParameters пуст вернемся toohello по умолчанию значение, указанное в hello ServiceManifest для соответствующего EndPointName hello.</span><span class="sxs-lookup"><span data-stu-id="bf8cc-136">Note: If hello values provide for hello ApplicationParameters is empty we go back toohello default value provided in hello ServiceManifest for hello corresponding EndPointName.</span></span>

<span data-ttu-id="bf8cc-137">Например:</span><span class="sxs-lookup"><span data-stu-id="bf8cc-137">For example:</span></span>

<span data-ttu-id="bf8cc-138">Если в hello указанной ServiceManifest</span><span class="sxs-lookup"><span data-stu-id="bf8cc-138">If in hello ServiceManifest you specified</span></span>

```xml
  <Resources>
    <Endpoints>
      <Endpoint Name="ServiceEndpoint1" Protocol="tcp"/>
    </Endpoints>
  </Resources>
```

<span data-ttu-id="bf8cc-139">Здравствуйте порта 1 и Protocol1 значения параметров приложения имеет значение null или пустым.</span><span class="sxs-lookup"><span data-stu-id="bf8cc-139">And hello Port1 and Protocol1 value for Application parameters is null or empty.</span></span> <span data-ttu-id="bf8cc-140">порт Hello по-прежнему определяется по ServiceFabric.</span><span class="sxs-lookup"><span data-stu-id="bf8cc-140">hello port is still decided by ServiceFabric.</span></span> <span data-ttu-id="bf8cc-141">И hello протокола tcp.</span><span class="sxs-lookup"><span data-stu-id="bf8cc-141">And hello Protocol will tcp.</span></span>

<span data-ttu-id="bf8cc-142">Предположим, что вы задали неверное значение.</span><span class="sxs-lookup"><span data-stu-id="bf8cc-142">Suppose you specify a wrong value.</span></span> <span data-ttu-id="bf8cc-143">Например, для порта задано строковое значение Foo вместо целого числа.  Новый ServiceFabricApplication команда завершится с ошибкой: недопустимый параметр переопределения hello с атрибутом «ServiceEndpoint1» имя порта «1» в разделе «ResourceOverrides».</span><span class="sxs-lookup"><span data-stu-id="bf8cc-143">Like for Port you specified a string value "Foo" instead of an int.  New-ServiceFabricApplication command will fail with an error : hello override parameter with name 'ServiceEndpoint1' attribute 'Port1' in section 'ResourceOverrides' is invalid.</span></span> <span data-ttu-id="bf8cc-144">Указанное значение Hello «Foo» и требуется «int».</span><span class="sxs-lookup"><span data-stu-id="bf8cc-144">hello value specified is 'Foo' and required is 'int'.</span></span>
