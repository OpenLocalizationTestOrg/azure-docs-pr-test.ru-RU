---
title: "aaaAzure службы структуры Docker составления Preview | Документы Microsoft"
description: "Azure Service Fabric принимает Docker Compose toomake формат его проще контейнеры exsiting tooorchestrate, с помощью Service Fabric. Сейчас эта возможность доступна в предварительной версии."
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
ms.openlocfilehash: 824044fd698f0ed94c4212722bc82187905315dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="specifying-volume-plugins-and-logging-drivers-for-your-container"></a><span data-ttu-id="abc3d-104">Указание подключаемых модулей томов и драйверов ведения журналов для контейнера</span><span class="sxs-lookup"><span data-stu-id="abc3d-104">Specifying volume plugins and logging drivers for your container</span></span>

<span data-ttu-id="abc3d-105">Service Fabric поддерживает указание [подключаемых модулей томов Docker](https://docs.docker.com/engine/extend/plugins_volume/) и [драйверов ведения журналов Docker](https://docs.docker.com/engine/admin/logging/overview/) для службы контейнеров.</span><span class="sxs-lookup"><span data-stu-id="abc3d-105">Service Fabric supports specifying [Docker volume plugins](https://docs.docker.com/engine/extend/plugins_volume/) and [Docker logging drivers](https://docs.docker.com/engine/admin/logging/overview/) for your container service.</span></span> <span data-ttu-id="abc3d-106">Hello подключаемые модули указаны в манифесте приложения hello, как показано в следующих манифест hello:</span><span class="sxs-lookup"><span data-stu-id="abc3d-106">hello plugins are specified in hello application manifest as shown in hello following manifest:</span></span>


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

<span data-ttu-id="abc3d-107">В предыдущих пример hello, hello `Source` тег для hello `Volume` ссылается toohello исходной папки.</span><span class="sxs-lookup"><span data-stu-id="abc3d-107">In hello preceding example, hello `Source` tag for hello `Volume` refers toohello source folder.</span></span> <span data-ttu-id="abc3d-108">Исходная папка Hello может быть папка в hello виртуальной Машины, на котором размещена hello контейнеров или постоянного удаленного хранилища.</span><span class="sxs-lookup"><span data-stu-id="abc3d-108">hello source folder could be a folder in hello VM that hosts hello containers or a persistent remote store.</span></span> <span data-ttu-id="abc3d-109">Hello `Destination` тег является расположение hello, hello `Source` hello сопоставленных toowithin выполняется контейнера.</span><span class="sxs-lookup"><span data-stu-id="abc3d-109">hello `Destination` tag is hello location that hello `Source` is mapped toowithin hello running container.</span></span> 

<span data-ttu-id="abc3d-110">При указании тома подключаемого модуля, Service Fabric автоматически создает hello тома, с помощью параметров hello.</span><span class="sxs-lookup"><span data-stu-id="abc3d-110">When specifying a volume plugin, Service Fabric automatically creates hello volume using hello parameters specified.</span></span> <span data-ttu-id="abc3d-111">Hello `Source` тег является именем hello тома hello и hello `Driver` тег указывает подключаемый модуль драйвера тома hello.</span><span class="sxs-lookup"><span data-stu-id="abc3d-111">hello `Source` tag is hello name of hello volume, and hello `Driver` tag specifies hello volume driver plugin.</span></span> <span data-ttu-id="abc3d-112">Параметры можно задать с помощью hello `DriverOption` тег, как показано в hello, следующий фрагмент кода:</span><span class="sxs-lookup"><span data-stu-id="abc3d-112">Options can be specified using hello `DriverOption` tag as shown in hello following snippet:</span></span>

```xml
<Volume Source="myvolume1" Destination="c:\testmountlocation4" Driver="azurefile" IsReadOnly="true">
           <DriverOption Name="share" Value="models"/>
</Volume>
```

<span data-ttu-id="abc3d-113">Если драйвер Docker журнала указан, это необходимые toodeploy журналы hello toohandle агентов (или контейнеры) в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="abc3d-113">If a Docker log driver is specified, it is necessary toodeploy agents (or containers) toohandle hello logs in hello cluster.</span></span>  <span data-ttu-id="abc3d-114">Hello `DriverOption` тега может быть параметры драйвера журнала используется toospecify также.</span><span class="sxs-lookup"><span data-stu-id="abc3d-114">hello `DriverOption` tag can be used toospecify log driver options as well.</span></span>

<span data-ttu-id="abc3d-115">См. следующие кластера Service Fabric tooa контейнеры toodeploy статьи toohello:</span><span class="sxs-lookup"><span data-stu-id="abc3d-115">Refer toohello following articles toodeploy containers tooa Service Fabric cluster:</span></span>


[<span data-ttu-id="abc3d-116">Развертывание контейнера в Service Fabric</span><span class="sxs-lookup"><span data-stu-id="abc3d-116">Deploy a container on Service Fabric</span></span>](service-fabric-deploy-container.md)

