---
title: "Настройка конечных точек службы Service Fabric | Документация Майкрософт"
description: "В этой статье поясняется, как описать ресурсы конечной точки в манифесте служб, включая настройку конечных точек HTTPS."
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
ms.openlocfilehash: 08141edfbc8be9bf7bf303419e1e482d5f884860
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="specify-resources-in-a-service-manifest"></a><span data-ttu-id="624a1-103">Указание ресурсов в манифесте службы</span><span class="sxs-lookup"><span data-stu-id="624a1-103">Specify resources in a service manifest</span></span>
## <a name="overview"></a><span data-ttu-id="624a1-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="624a1-104">Overview</span></span>
<span data-ttu-id="624a1-105">Манифест служб позволяет объявлять и изменять ресурсы, используемые в службе, не меняя скомпилированный код.</span><span class="sxs-lookup"><span data-stu-id="624a1-105">The service manifest allows resources that are used by the service to be declared/changed without changing the compiled code.</span></span> <span data-ttu-id="624a1-106">Azure Service Fabric поддерживает настройку ресурсов конечных точек для службы.</span><span class="sxs-lookup"><span data-stu-id="624a1-106">Azure Service Fabric supports configuration of endpoint resources for the service.</span></span> <span data-ttu-id="624a1-107">Доступ к ресурсам, указанным в манифесте служб, можно контролировать в манифесте приложения с помощью элемента SecurityGroup.</span><span class="sxs-lookup"><span data-stu-id="624a1-107">The access to the resources that are specified in the service manifest can be controlled via the SecurityGroup in the application manifest.</span></span> <span data-ttu-id="624a1-108">Объявление ресурсов позволяет изменять их при развертывании, т. е. службе не нужно внедрять новый механизм настройки.</span><span class="sxs-lookup"><span data-stu-id="624a1-108">The declaration of resources allows these resources to be changed at deployment time, meaning the service doesn't need to introduce a new configuration mechanism.</span></span> <span data-ttu-id="624a1-109">Определение схемы для файла ServiceManifest.xml устанавливается с пакетом SDK и средствами для Service Fabric в расположении *C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span><span class="sxs-lookup"><span data-stu-id="624a1-109">The schema definition for the ServiceManifest.xml file is installed with the Service Fabric SDK and tools to *C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span></span>

## <a name="endpoints"></a><span data-ttu-id="624a1-110">Endpoints</span><span class="sxs-lookup"><span data-stu-id="624a1-110">Endpoints</span></span>
<span data-ttu-id="624a1-111">Если ресурс конечной точки определен в манифесте службы, Service Fabric назначает порты из диапазона зарезервированных портов приложений, если порт не указан явным образом.</span><span class="sxs-lookup"><span data-stu-id="624a1-111">When an endpoint resource is defined in the service manifest, Service Fabric assigns ports from the reserved application port range when a port isn't specified explicitly.</span></span> <span data-ttu-id="624a1-112">Например, рассмотрим конечную точку *ServiceEndpoint1* , которая указана во фрагменте кода манифеста, приведенном после абзаца.</span><span class="sxs-lookup"><span data-stu-id="624a1-112">For example, look at the endpoint *ServiceEndpoint1* specified in the manifest snippet provided after this paragraph.</span></span> <span data-ttu-id="624a1-113">Кроме того, службы также могут запрашивать наличие в ресурсе конкретного порта.</span><span class="sxs-lookup"><span data-stu-id="624a1-113">Additionally, services can also request a specific port in a resource.</span></span> <span data-ttu-id="624a1-114">Репликам службы, которые выполняются на различных узлах кластера, можно назначить разные номера портов, а реплики службы, выполняющиеся на одном и том же узле, будут совместно используют один порт.</span><span class="sxs-lookup"><span data-stu-id="624a1-114">Service replicas running on different cluster nodes can be assigned different port numbers, while replicas of a service running on the same node share the port.</span></span> <span data-ttu-id="624a1-115">Реплики службы при необходимости могут использовать эти порты для репликации и прослушивания клиентских запросов.</span><span class="sxs-lookup"><span data-stu-id="624a1-115">The service replicas can then use these ports as needed for replication and listening for client requests.</span></span>

```xml
<Resources>
  <Endpoints>
    <Endpoint Name="ServiceEndpoint1" Protocol="http"/>
    <Endpoint Name="ServiceEndpoint2" Protocol="http" Port="80"/>
    <Endpoint Name="ServiceEndpoint3" Protocol="https"/>
  </Endpoints>
</Resources>
```

<span data-ttu-id="624a1-116">Дополнительные сведения о создании ссылок на конечные точки из файла параметров пакета конфигурации (settings.xml) см. в статье [Настройка надежных служб с отслеживанием состояния](service-fabric-reliable-services-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="624a1-116">Refer to [Configuring stateful Reliable Services](service-fabric-reliable-services-configuration.md) to read more about referencing endpoints from the config package settings file (settings.xml).</span></span>

## <a name="example-specifying-an-http-endpoint-for-your-service"></a><span data-ttu-id="624a1-117">Пример. Указание конечной точки HTTP для службы</span><span class="sxs-lookup"><span data-stu-id="624a1-117">Example: specifying an HTTP endpoint for your service</span></span>
<span data-ttu-id="624a1-118">Следующий манифест служб в элементе &lt;Resources&gt; определяет один ресурс конечной точки TCP и два ресурса конечной точки HTTP.</span><span class="sxs-lookup"><span data-stu-id="624a1-118">The following service manifest defines one TCP endpoint resource and two HTTP endpoint resources in the &lt;Resources&gt; element.</span></span>

<span data-ttu-id="624a1-119">Service Fabric автоматически создает список управления доступом (ACL) для конечных точек HTTP.</span><span class="sxs-lookup"><span data-stu-id="624a1-119">HTTP endpoints are automatically ACL'd by Service Fabric.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceManifest Name="Stateful1Pkg"
                 Version="1.0.0"
                 xmlns="http://schemas.microsoft.com/2011/01/fabric"
                 xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <ServiceTypes>
    <!-- This is the name of your ServiceType.
         This name must match the string used in the RegisterServiceType call in Program.cs. -->
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

  <!-- Config package is the contents of the Config directoy under PackageRoot that contains an
       independently updateable and versioned set of custom configuration settings for your service. -->
  <ConfigPackage Name="Config" Version="1.0.0" />

  <Resources>
    <Endpoints>
      <!-- This endpoint is used by the communication listener to obtain the port number on which to
           listen. Note that if your service is partitioned, this port is shared with
           replicas of different partitions that are placed in your code. -->
      <Endpoint Name="ServiceEndpoint1" Protocol="http"/>
      <Endpoint Name="ServiceEndpoint2" Protocol="http" Port="80"/>
      <Endpoint Name="ServiceEndpoint3" Protocol="https"/>

      <!-- This endpoint is used by the replicator for replicating the state of your service.
           This endpoint is configured through the ReplicatorSettings config section in the Settings.xml
           file under the ConfigPackage. -->
      <Endpoint Name="ReplicatorEndpoint" />
    </Endpoints>
  </Resources>
</ServiceManifest>
```

## <a name="example-specifying-an-https-endpoint-for-your-service"></a><span data-ttu-id="624a1-120">Пример. Указание конечной точки HTTPS для службы</span><span class="sxs-lookup"><span data-stu-id="624a1-120">Example: specifying an HTTPS endpoint for your service</span></span>
<span data-ttu-id="624a1-121">Протокол HTTPS обеспечивает аутентификацию сервера, а также используется для шифрования данных, передаваемых между клиентом сервером.</span><span class="sxs-lookup"><span data-stu-id="624a1-121">The HTTPS protocol provides server authentication and is also used for encrypting client-server communication.</span></span> <span data-ttu-id="624a1-122">Чтобы включить протокол HTTPS в службе Service Fabric, укажите его в разделе *Ресурсы > Конечные точки > Конечная точка* манифеста служб, как показано выше для конечной точки *ServiceEndpoint3*.</span><span class="sxs-lookup"><span data-stu-id="624a1-122">To enable HTTPS on your Service Fabric service, specify the protocol in the *Resources -> Endpoints -> Endpoint* section of the service manifest, as shown earlier for the endpoint *ServiceEndpoint3*.</span></span>

> [!NOTE]
> <span data-ttu-id="624a1-123">Протокол службы невозможно изменить при обновлении приложения.</span><span class="sxs-lookup"><span data-stu-id="624a1-123">A service’s protocol cannot be changed during application upgrade.</span></span> <span data-ttu-id="624a1-124">Если изменить его во время обновления, то это будет считаться критическим изменением.</span><span class="sxs-lookup"><span data-stu-id="624a1-124">If it is changed during upgrade, it is a breaking change.</span></span>
> 
> 

<span data-ttu-id="624a1-125">Ниже приведен пример ApplicationManifest, который необходимо задать для HTTPS.</span><span class="sxs-lookup"><span data-stu-id="624a1-125">Here is an example ApplicationManifest that you need to set for HTTPS.</span></span> <span data-ttu-id="624a1-126">Требуется предоставить отпечаток для сертификата.</span><span class="sxs-lookup"><span data-stu-id="624a1-126">The thumbprint for your certificate must be provided.</span></span> <span data-ttu-id="624a1-127">EndpointRef является ссылкой на EndpointResource в ServiceManifest, для которого задается протокол HTTPS.</span><span class="sxs-lookup"><span data-stu-id="624a1-127">The EndpointRef is a reference to EndpointResource in ServiceManifest, for which you set the HTTPS protocol.</span></span> <span data-ttu-id="624a1-128">Можно добавить несколько элементов Endpointcertificate.</span><span class="sxs-lookup"><span data-stu-id="624a1-128">You can add more than one EndpointCertificate.</span></span>  

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
  <!-- Import the ServiceManifest from the ServicePackage. The ServiceManifestName and ServiceManifestVersion
       should match the Name and Version attributes of the ServiceManifest element defined in the
       ServiceManifest.xml file. -->
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="Stateful1Pkg" ServiceManifestVersion="1.0.0" />
    <ConfigOverrides />
    <Policies>
      <EndpointBindingPolicy CertificateRef="TestCert1" EndpointRef="ServiceEndpoint3"/>
    </Policies>
  </ServiceManifestImport>
  <DefaultServices>
    <!-- The section below creates instances of service types when an instance of this
         application type is created. You can also create one or more instances of service type by using the
         Service Fabric PowerShell module.

         The attribute ServiceTypeName below must match the name defined in the imported ServiceManifest.xml file. -->
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

## <a name="overriding-endpoints-in-servicemanifestxml"></a><span data-ttu-id="624a1-129">Переопределение конечных точек в файле ServiceManifest.xml</span><span class="sxs-lookup"><span data-stu-id="624a1-129">Overriding Endpoints in ServiceManifest.xml</span></span>

<span data-ttu-id="624a1-130">В ApplicationManifest добавьте раздел ResourceOverrides, который будет находиться на одном уровне с разделом ConfigOverrides.</span><span class="sxs-lookup"><span data-stu-id="624a1-130">In the ApplicationManifest add a ResourceOverrides section which will be a sibling to ConfigOverrides section.</span></span> <span data-ttu-id="624a1-131">В этом разделе можно задать параметры переопределения для раздела конечных точек в разделе ресурсов, указанном в манифесте служб.</span><span class="sxs-lookup"><span data-stu-id="624a1-131">In this section you can specify the override for the Endpoints section in the resources section specified in the Service manifest.</span></span>

<span data-ttu-id="624a1-132">Чтобы переопределить EndPoint в ServiceManifest, используя ApplicationParameters, измените ApplicationManifest следующим образом:</span><span class="sxs-lookup"><span data-stu-id="624a1-132">In order to override EndPoint in ServiceManifest using ApplicationParameters change the ApplicationManifest as following:</span></span>

<span data-ttu-id="624a1-133">Добавьте новый подраздел ResourceOverrides в раздел ServiceManifestImport.</span><span class="sxs-lookup"><span data-stu-id="624a1-133">In the ServiceManifestImport section add a new section "ResourceOverrides"</span></span>

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

<span data-ttu-id="624a1-134">В раздел Parameters добавьте следующее:</span><span class="sxs-lookup"><span data-stu-id="624a1-134">In the Parameters add below:</span></span>

```xml
  <Parameters>
    <Parameter Name="Port" DefaultValue="" />
    <Parameter Name="Protocol" DefaultValue="" />
    <Parameter Name="Type" DefaultValue="" />
    <Parameter Name="Port1" DefaultValue="" />
    <Parameter Name="Protocol1" DefaultValue="" />
  </Parameters>
```

<span data-ttu-id="624a1-135">Теперь при развертывании приложения вы можете передать эти значения в качестве объекта ApplicationParameters, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="624a1-135">While deploying the application now you can pass in these values as ApplicationParameters for example:</span></span>

```powershell
PS C:\> New-ServiceFabricApplication -ApplicationName fabric:/myapp -ApplicationTypeName "AppType" -ApplicationTypeVersion "1.0.0" -ApplicationParameter @{Port='1001'; Protocol='https'; Type='Input'; Port1='2001'; Protocol='http'}
```

<span data-ttu-id="624a1-136">Примечание. Если для ApplicationParameters значения не заданы, мы возвращаемся к значению по умолчанию, предоставленному в ServiceManifest для соответствующей конечной точки.</span><span class="sxs-lookup"><span data-stu-id="624a1-136">Note: If the values provide for the ApplicationParameters is empty we go back to the default value provided in the ServiceManifest for the corresponding EndPointName.</span></span>

<span data-ttu-id="624a1-137">Например:</span><span class="sxs-lookup"><span data-stu-id="624a1-137">For example:</span></span>

<span data-ttu-id="624a1-138">Допустим, в ServiceManifest заданы следующие значения:</span><span class="sxs-lookup"><span data-stu-id="624a1-138">If in the ServiceManifest you specified</span></span>

```xml
  <Resources>
    <Endpoints>
      <Endpoint Name="ServiceEndpoint1" Protocol="tcp"/>
    </Endpoints>
  </Resources>
```

<span data-ttu-id="624a1-139">Если в ApplicationParameters параметры Port1 и Protocol1 имеют значение или же оно не задано,</span><span class="sxs-lookup"><span data-stu-id="624a1-139">And the Port1 and Protocol1 value for Application parameters is null or empty.</span></span> <span data-ttu-id="624a1-140">порт по-прежнему определяет платформа Service Fabric,</span><span class="sxs-lookup"><span data-stu-id="624a1-140">The port is still decided by ServiceFabric.</span></span> <span data-ttu-id="624a1-141">а в качестве протокола используется TCP.</span><span class="sxs-lookup"><span data-stu-id="624a1-141">And the Protocol will tcp.</span></span>

<span data-ttu-id="624a1-142">Предположим, что вы задали неверное значение.</span><span class="sxs-lookup"><span data-stu-id="624a1-142">Suppose you specify a wrong value.</span></span> <span data-ttu-id="624a1-143">Например, для порта задано строковое значение Foo вместо целого числа.  При выполнении команды New-ServiceFabricApplication произойдет ошибка: The override parameter with name 'ServiceEndpoint1' attribute 'Port1' in section 'ResourceOverrides' is invalid.</span><span class="sxs-lookup"><span data-stu-id="624a1-143">Like for Port you specified a string value "Foo" instead of an int.  New-ServiceFabricApplication command will fail with an error : The override parameter with name 'ServiceEndpoint1' attribute 'Port1' in section 'ResourceOverrides' is invalid.</span></span> <span data-ttu-id="624a1-144">The value specified is 'Foo' and required is 'int' (Недопустимый параметр переопределения ServiceEndpoint1 атрибута Port1 в разделе ResourceOverrides. Указано значение Foo, а требуется целое число).</span><span class="sxs-lookup"><span data-stu-id="624a1-144">The value specified is 'Foo' and required is 'int'.</span></span>
