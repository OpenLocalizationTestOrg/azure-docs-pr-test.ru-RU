---
title: "aaaHow toocontainerize микрослужбами вашей Azure Service Fabric (Предварительная версия)"
description: "Azure Service Fabric были добавлены новые функциональные возможности toocontainerize вашей микрослужбами Service Fabric. Эта функция в настоящее время находится на стадии предварительной версии."
services: service-fabric
documentationcenter: .net
author: anmolah
manager: anmolah
editor: anmolah
ms.assetid: 0b41efb3-4063-4600-89f5-b077ea81fa3a
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/04/2017
ms.author: anmola
ms.openlocfilehash: 6edaff73c0828707c7fa736669ba8084663d31ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocontainerize-your-service-fabric-reliable-services-and-reliable-actors-preview"></a><span data-ttu-id="b6911-104">Как toocontainerize структуры вашей службы надежность службы и службы Reliable Actor (Предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="b6911-104">How toocontainerize your Service Fabric Reliable Services and Reliable Actors (Preview)</span></span>

<span data-ttu-id="b6911-105">Service Fabric поддерживает контейнеризацию микрослужб Service Fabric (службы на основе Reliable Services и Reliable Actors).</span><span class="sxs-lookup"><span data-stu-id="b6911-105">Service Fabric supports containerizing Service Fabric microservices (Reliable Services, and Reliable Actor based services).</span></span> <span data-ttu-id="b6911-106">Дополнительные сведения см. в статье [Service Fabric и контейнеры](service-fabric-containers-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b6911-106">For more information, see [service fabric containers](service-fabric-containers-overview.md).</span></span>


 <span data-ttu-id="b6911-107">Эта функция представляет собой предварительную версию и в этой статье приведены различные действия tooget Здравствуйте, работающей в контейнере службы.</span><span class="sxs-lookup"><span data-stu-id="b6911-107">This feature is in preview and this article provides hello various steps tooget your service running inside a container.</span></span>  

> [!NOTE]
> <span data-ttu-id="b6911-108">Эта функция доступна в режиме предварительной версии и не поддерживается в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="b6911-108">This feature is in preview and is not supported in production.</span></span> <span data-ttu-id="b6911-109">Сейчас эта функция работает только в Windows.</span><span class="sxs-lookup"><span data-stu-id="b6911-109">Currently this feature only works for Windows.</span></span>

## <a name="steps-toocontainerize-your-service-fabric-application"></a><span data-ttu-id="b6911-110">Шаги toocontainerize структуры приложения службы</span><span class="sxs-lookup"><span data-stu-id="b6911-110">Steps toocontainerize your Service Fabric Application</span></span>

1. <span data-ttu-id="b6911-111">Откройте приложение Service Fabric в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b6911-111">Open your Service Fabric application in Visual Studio.</span></span>

2. <span data-ttu-id="b6911-112">Добавьте класс [SFBinaryLoader.cs](https://github.com/Azure/service-fabric-scripts-and-templates/blob/master/code/SFBinaryLoaderForContainers/SFBinaryLoader.cs) tooyour проекта.</span><span class="sxs-lookup"><span data-stu-id="b6911-112">Add class [SFBinaryLoader.cs](https://github.com/Azure/service-fabric-scripts-and-templates/blob/master/code/SFBinaryLoaderForContainers/SFBinaryLoader.cs) tooyour project.</span></span> <span data-ttu-id="b6911-113">Код Hello в этом классе является вспомогательный toocorrectly нагрузки hello Service Fabric двоичных файлов среды выполнения в приложении при выполнении внутри контейнера.</span><span class="sxs-lookup"><span data-stu-id="b6911-113">hello code in this class is a helper toocorrectly load hello Service Fabric runtime binaries inside your application when running inside a container.</span></span>

3. <span data-ttu-id="b6911-114">Для каждого пакета кода хотелось бы toocontainerize инициализировать загрузчик hello в точке входа программы hello.</span><span class="sxs-lookup"><span data-stu-id="b6911-114">For each code package you would like toocontainerize, initialize hello loader at hello program entry point.</span></span> <span data-ttu-id="b6911-115">Добавьте статический конструктор hello показано в следующих файла точки входа программы tooyour фрагмента кода hello.</span><span class="sxs-lookup"><span data-stu-id="b6911-115">Add hello static constructor shown in hello following code snippet tooyour program entry point file.</span></span>

  ```csharp
  namespace MyApplication
  {
      internal static class Program
      {
          static Program()
          {
              SFBinaryLoader.Initialize();
          }

          /// <summary>
          /// This is hello entry point of hello service host process.
          /// </summary>
          private static void Main()
          {
  ```

4. <span data-ttu-id="b6911-116">Выполните сборку проекта и [упакуйте](service-fabric-package-apps.md#Package-App) его.</span><span class="sxs-lookup"><span data-stu-id="b6911-116">Build and [package](service-fabric-package-apps.md#Package-App) your project.</span></span> <span data-ttu-id="b6911-117">toobuild и создания пакета, щелкните правой кнопкой мыши проект приложения hello в обозревателе решений и выберите hello **пакета** команды.</span><span class="sxs-lookup"><span data-stu-id="b6911-117">toobuild and create a package, right-click hello application project in Solution Explorer and choose hello **Package** command.</span></span>

5. <span data-ttu-id="b6911-118">Для каждого пакета кода необходимо toocontainerize hello выполнения сценария PowerShell [CreateDockerPackage.ps1](https://github.com/Azure/service-fabric-scripts-and-templates/blob/master/scripts/CodePackageToDockerPackage/CreateDockerPackage.ps1).</span><span class="sxs-lookup"><span data-stu-id="b6911-118">For every code package you need toocontainerize, run hello PowerShell script [CreateDockerPackage.ps1](https://github.com/Azure/service-fabric-scripts-and-templates/blob/master/scripts/CodePackageToDockerPackage/CreateDockerPackage.ps1).</span></span> <span data-ttu-id="b6911-119">Использование Hello выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="b6911-119">hello usage is as follows:</span></span>
  ```powershell
    $codePackagePath = 'Path toohello code package toocontainerize.'
    $dockerPackageOutputDirectoryPath = 'Output path for hello generated docker folder.'
    $applicationExeName = 'Name of hello ode package executable.'
    CreateDockerPackage.ps1 -CodePackageDirectoryPath $codePackagePath -DockerPackageOutputDirectoryPath $dockerPackageOutputDirectoryPath -ApplicationExeName $applicationExeName
 ```
  <span data-ttu-id="b6911-120">Hello скрипт создает папку с артефактами Docker на $dockerPackageOutputDirectoryPath.</span><span class="sxs-lookup"><span data-stu-id="b6911-120">hello script creates a folder with Docker artifacts at $dockerPackageOutputDirectoryPath.</span></span> <span data-ttu-id="b6911-121">Измените hello создан Dockerfile tooexpose все порты, запускать сценарии установки и т.д., в зависимости от потребностей.</span><span class="sxs-lookup"><span data-stu-id="b6911-121">Modify hello generated Dockerfile tooexpose any ports, run setup scripts etc. based on your needs.</span></span>

6. <span data-ttu-id="b6911-122">Затем следует записать слишком[построения](service-fabric-get-started-containers.md#Build-Containers) и [принудительной](service-fabric-get-started-containers.md#Push-Containers) репозиторий tooyour пакета контейнер Docker.</span><span class="sxs-lookup"><span data-stu-id="b6911-122">Next you need too[build](service-fabric-get-started-containers.md#Build-Containers) and [push](service-fabric-get-started-containers.md#Push-Containers) your Docker container package tooyour repository.</span></span>

7. <span data-ttu-id="b6911-123">Измените hello ApplicationManifest.xml и ServiceManifest.xml tooadd образ контейнера, сведения о репозитории, проверка подлинности реестра и сопоставление портов для узла.</span><span class="sxs-lookup"><span data-stu-id="b6911-123">Modify hello ApplicationManifest.xml and ServiceManifest.xml tooadd your container image, repository information, registry authentication, and port-to-host mapping.</span></span> <span data-ttu-id="b6911-124">Изменение манифестов hello, в разделе [создать приложение контейнера Azure Service Fabric](service-fabric-get-started-containers.md).</span><span class="sxs-lookup"><span data-stu-id="b6911-124">For modifying hello manifests, see [Create an Azure Service Fabric container application](service-fabric-get-started-containers.md).</span></span> <span data-ttu-id="b6911-125">Определение пакета кода Hello в toobe манифеста потребностей службы hello, заменены соответствующий образ контейнера.</span><span class="sxs-lookup"><span data-stu-id="b6911-125">hello code package definition in hello service manifest needs toobe replaced with corresponding container image.</span></span> <span data-ttu-id="b6911-126">Убедитесь, что toochange hello EntryPoint tooa ContainerHost типа.</span><span class="sxs-lookup"><span data-stu-id="b6911-126">Make sure toochange hello EntryPoint tooa ContainerHost type.</span></span>

  ```xml
<!-- Code package is your service executable. -->
<CodePackage Name="Code" Version="1.0.0">
  <EntryPoint>
    <!-- Follow this link for more information about deploying Windows containers tooService Fabric: https://aka.ms/sfguestcontainers -->
    <ContainerHost>
      <ImageName>myregistry.azurecr.io/samples/helloworldapp</ImageName>
    </ContainerHost>
  </EntryPoint>
  <!-- Pass environment variables tooyour container: -->    
</CodePackage>
  ```

8. <span data-ttu-id="b6911-127">Добавление сопоставления порта для размещения hello для репликации и конечной точки службы.</span><span class="sxs-lookup"><span data-stu-id="b6911-127">Add hello port-to-host mapping for your replicator and service endpoint.</span></span> <span data-ttu-id="b6911-128">Поскольку оба этих порта, назначаемые во время выполнения Service Fabric, hello ContainerPort устанавливается toozero toouse hello, назначенный порт для сопоставления.</span><span class="sxs-lookup"><span data-stu-id="b6911-128">Since both these ports are assigned at runtime by Service Fabric, hello ContainerPort is set toozero toouse hello assigned port for mapping.</span></span>

 ```xml
<Policies>
  <ContainerHostPolicies CodePackageRef="Code">
    <PortBinding ContainerPort="0" EndpointRef="ServiceEndpoint"/>
    <PortBinding ContainerPort="0" EndpointRef="ReplicatorEndpoint"/>
  </ContainerHostPolicies>
</Policies>
 ```

9. <span data-ttu-id="b6911-129">tootest этого приложения требуется toodeploy его tooa кластера под управлением версии 5.7 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="b6911-129">tootest this application, you need toodeploy it tooa cluster that is running version 5.7 or higher.</span></span> <span data-ttu-id="b6911-130">Кроме того требуется tooedit и обновить tooenable параметры кластера hello предварительную версию этого компонента.</span><span class="sxs-lookup"><span data-stu-id="b6911-130">In addition, you need tooedit and update hello cluster settings tooenable this preview feature.</span></span> <span data-ttu-id="b6911-131">Выполните действия hello в этом [статьи](service-fabric-cluster-fabric-settings.md) tooadd приветствия показано далее.</span><span class="sxs-lookup"><span data-stu-id="b6911-131">Follow hello steps in this [article](service-fabric-cluster-fabric-settings.md) tooadd hello setting shown next.</span></span>
```
      {
        "name": "Hosting",
        "parameters": [
          {
            "name": "FabricContainerAppsEnabled",
            "value": "true"
          }
        ]
      }
```
10. <span data-ttu-id="b6911-132">Далее [развертывание](service-fabric-deploy-remove-applications.md) hello редактировать кластера toothis пакета приложения.</span><span class="sxs-lookup"><span data-stu-id="b6911-132">Next [deploy](service-fabric-deploy-remove-applications.md) hello edited application package toothis cluster.</span></span>

<span data-ttu-id="b6911-133">Теперь в вашем кластере работает контейнерное приложение Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b6911-133">You should now have a containerized Service Fabric application running your cluster.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b6911-134">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b6911-134">Next steps</span></span>
* <span data-ttu-id="b6911-135">Дополнительные сведения о запуске [контейнеров в Service Fabric](service-fabric-get-started-containers.md).</span><span class="sxs-lookup"><span data-stu-id="b6911-135">Learn more about running [containers on Service Fabric](service-fabric-get-started-containers.md).</span></span>
* <span data-ttu-id="b6911-136">Дополнительные сведения о Service Fabric hello [жизненного цикла приложения](service-fabric-application-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="b6911-136">Learn about hello Service Fabric [application life-cycle](service-fabric-application-lifecycle.md).</span></span>
