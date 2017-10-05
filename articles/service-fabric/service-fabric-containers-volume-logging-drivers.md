---
title: "Средство Docker Compose для Azure Service Fabric (предварительная версия) | Документация Майкрософт"
description: "Платформа Azure Service Fabric принимает формат Docker Compose для упрощения управления существующими контейнерами с помощью Service Fabric. Сейчас эта возможность доступна в предварительной версии."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: ab49c4b9-74a8-4907-b75b-8d2ee84c6d90
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: b12ef95add6347621f7d4865fac46568f91a1e12
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="specifying-volume-plugins-and-logging-drivers-for-your-container"></a><span data-ttu-id="909f4-104">Указание подключаемых модулей томов и драйверов ведения журналов для контейнера</span><span class="sxs-lookup"><span data-stu-id="909f4-104">Specifying volume plugins and logging drivers for your container</span></span>

<span data-ttu-id="909f4-105">Service Fabric поддерживает указание [подключаемых модулей томов Docker](https://docs.docker.com/engine/extend/plugins_volume/) и [драйверов ведения журналов Docker](https://docs.docker.com/engine/admin/logging/overview/) для службы контейнеров.</span><span class="sxs-lookup"><span data-stu-id="909f4-105">Service Fabric supports specifying [Docker volume plugins](https://docs.docker.com/engine/extend/plugins_volume/) and [Docker logging drivers](https://docs.docker.com/engine/admin/logging/overview/) for your container service.</span></span> <span data-ttu-id="909f4-106">Подключаемые модули указываются в манифесте приложения, как показано в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="909f4-106">The plugins are specified in the application manifest as shown in the following manifest:</span></span>


```xml
?xml version="1.0" encoding="UTF-8"?>
<ApplicationManifest ApplicationTypeName="WinNodeJsApp" ApplicationTypeVersion="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
    <Description>Calculator Application</Description>
    <Parameters>
        <Parameter Name="ServiceInstanceCount" DefaultValue="3"></Parameter>
      <Parameter Name="MyCpuShares" DefaultValue="3"></Parameter>
    </Parameters>
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="NodeServicePackage" ServiceManifestVersion="1.0"/>
     <Policies>
       <ContainerHostPolicies CodePackageRef="NodeService.Code" Isolation="hyperv"> 
        <PortBinding ContainerPort="8905" EndpointRef="Endpoint1"/>
        <RepositoryCredentials PasswordEncrypted="false" Password="****" AccountName="test"/>
        <LogConfig Driver="etwlogs" >
          <DriverOption Name="test" Value="vale"/>
        </LogConfig>
        <Volume Source="c:\workspace" Destination="c:\testmountlocation1" IsReadOnly="false"></Volume>
        <Volume Source="d:\myfolder" Destination="c:\testmountlocation2" IsReadOnly="true"> </Volume>
        <Volume Source="myexternalvolume" Destination="c:\testmountlocation3" Driver="sf" IsReadOnly="true"></Volume>
       </ContainerHostPolicies>
   </Policies>
    </ServiceManifestImport>
    <ServiceTemplates>
        <StatelessService ServiceTypeName="StatelessNodeService" InstanceCount="5">
            <SingletonPartition></SingletonPartition>
        </StatelessService>
    </ServiceTemplates>
</ApplicationManifest>
```

<span data-ttu-id="909f4-107">В приведенном выше примере тег `Source` для `Volume` указывает на исходную папку.</span><span class="sxs-lookup"><span data-stu-id="909f4-107">In the preceding example, the `Source` tag for the `Volume` refers to the source folder.</span></span> <span data-ttu-id="909f4-108">Исходной папкой может быть папка в виртуальной машине, в которой размещаются контейнеры, или постоянное удаленное хранилище.</span><span class="sxs-lookup"><span data-stu-id="909f4-108">The source folder could be a folder in the VM that hosts the containers or a persistent remote store.</span></span> <span data-ttu-id="909f4-109">Тег `Destination` — это расположение, с которым сопоставляется `Source` в работающем контейнере.</span><span class="sxs-lookup"><span data-stu-id="909f4-109">The `Destination` tag is the location that the `Source` is mapped to within the running container.</span></span> 

<span data-ttu-id="909f4-110">При указании подключаемого модуля тома Service Fabric автоматически создает том, используя заданные параметры.</span><span class="sxs-lookup"><span data-stu-id="909f4-110">When specifying a volume plugin, Service Fabric automatically creates the volume using the parameters specified.</span></span> <span data-ttu-id="909f4-111">Тег `Source` — это имя тома, а тег `Driver` указывает подключаемый модуль драйвера тома.</span><span class="sxs-lookup"><span data-stu-id="909f4-111">The `Source` tag is the name of the volume, and the `Driver` tag specifies the volume driver plugin.</span></span> <span data-ttu-id="909f4-112">Параметры можно указать с помощью тега `DriverOption`, как показано в следующем фрагменте:</span><span class="sxs-lookup"><span data-stu-id="909f4-112">Options can be specified using the `DriverOption` tag as shown in the following snippet:</span></span>

```xml
<Volume Source="myvolume1" Destination="c:\testmountlocation4" Driver="azurefile" IsReadOnly="true">
           <DriverOption Name="share" Value="models"/>
</Volume>
```

<span data-ttu-id="909f4-113">Если задан драйвер ведения журналов Docker, необходимо развернуть агенты (или контейнеры) для обработки журналов в кластере.</span><span class="sxs-lookup"><span data-stu-id="909f4-113">If a Docker log driver is specified, it is necessary to deploy agents (or containers) to handle the logs in the cluster.</span></span>  <span data-ttu-id="909f4-114">Тег `DriverOption` также может использоваться для указания параметров драйвера ведения журналов.</span><span class="sxs-lookup"><span data-stu-id="909f4-114">The `DriverOption` tag can be used to specify log driver options as well.</span></span>

<span data-ttu-id="909f4-115">Сведения о развертывании контейнеров в кластере Service Fabric см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="909f4-115">Refer to the following articles to deploy containers to a Service Fabric cluster:</span></span>


[<span data-ttu-id="909f4-116">Развертывание контейнера в Service Fabric</span><span class="sxs-lookup"><span data-stu-id="909f4-116">Deploy a container on Service Fabric</span></span>](service-fabric-deploy-container.md)

