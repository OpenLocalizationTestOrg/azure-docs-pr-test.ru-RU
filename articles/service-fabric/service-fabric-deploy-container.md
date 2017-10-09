---
title: "aaaService структуры и развертывание контейнеры | Документы Microsoft"
description: "Service Fabric и hello использовать контейнеры toodeploy микрослужбу приложений. В этой статье описываются возможности hello, предоставляемых Service Fabric для контейнеров и как toodeploy контейнера Windows изображения в кластер."
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: 799cc9ad-32fd-486e-a6b6-efff6b13622d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 5/16/2017
ms.author: msfussell
ms.openlocfilehash: 8b6540579641474f21b8712b56049c7d177bec26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-windows-container-tooservice-fabric"></a><span data-ttu-id="9f2b1-104">Развертывание tooService контейнера Windows Fabric</span><span class="sxs-lookup"><span data-stu-id="9f2b1-104">Deploy a Windows container tooService Fabric</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9f2b1-105">Развертывание контейнера Windows</span><span class="sxs-lookup"><span data-stu-id="9f2b1-105">Deploy Windows Container</span></span>](service-fabric-deploy-container.md)
> * [<span data-ttu-id="9f2b1-106">Развертывание контейнера Docker</span><span class="sxs-lookup"><span data-stu-id="9f2b1-106">Deploy Docker Container</span></span>](service-fabric-deploy-container-linux.md)
> 
> 

<span data-ttu-id="9f2b1-107">В этой статье описывается процесс построения контейнерного служб в контейнерах Windows hello.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-107">This article walks you through hello process of building containerized services in Windows containers.</span></span>

<span data-ttu-id="9f2b1-108">В Service Fabric реализовано несколько возможностей для создания приложений, состоящих из микрослужб, выполняющихся в контейнерах.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-108">Service Fabric has several capabilities that help you with building applications that are composed of microservices running inside containers.</span></span> 

<span data-ttu-id="9f2b1-109">Hello обладает следующими возможностями:</span><span class="sxs-lookup"><span data-stu-id="9f2b1-109">hello capabilities include:</span></span>

* <span data-ttu-id="9f2b1-110">развертывание и активация образа контейнера;</span><span class="sxs-lookup"><span data-stu-id="9f2b1-110">Container image deployment and activation</span></span>
* <span data-ttu-id="9f2b1-111">управление ресурсами;</span><span class="sxs-lookup"><span data-stu-id="9f2b1-111">Resource governance</span></span>
* <span data-ttu-id="9f2b1-112">проверка подлинности репозитория;</span><span class="sxs-lookup"><span data-stu-id="9f2b1-112">Repository authentication</span></span>
* <span data-ttu-id="9f2b1-113">сопоставление порта контейнера с портом узла;</span><span class="sxs-lookup"><span data-stu-id="9f2b1-113">Container port-to-host port mapping</span></span>
* <span data-ttu-id="9f2b1-114">межконтейнерное обнаружение и взаимодействие;</span><span class="sxs-lookup"><span data-stu-id="9f2b1-114">Container-to-container discovery and communication</span></span>
* <span data-ttu-id="9f2b1-115">Возможность tooconfigure и установка переменных среды</span><span class="sxs-lookup"><span data-stu-id="9f2b1-115">Ability tooconfigure and set environment variables</span></span>

<span data-ttu-id="9f2b1-116">Давайте посмотрим, как каждая из возможностей работает при упаковке toobe контейнерного службы, включенные в приложении.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-116">Let's look at how each of capabilities works when you're packaging a containerized service toobe included in your application.</span></span>

## <a name="package-a-windows-container"></a><span data-ttu-id="9f2b1-117">Упаковка контейнера Windows</span><span class="sxs-lookup"><span data-stu-id="9f2b1-117">Package a Windows container</span></span>
<span data-ttu-id="9f2b1-118">При создании пакета, контейнера, вы можете toouse либо шаблон проекта Visual Studio или [вручную создать пакет приложения hello](#manually).</span><span class="sxs-lookup"><span data-stu-id="9f2b1-118">When you package a container, you can choose toouse either a Visual Studio project template or [create hello application package manually](#manually).</span></span>  <span data-ttu-id="9f2b1-119">При использовании Visual Studio, структура пакета приложения hello, и файлы манифеста создаются шаблоном hello новый проект.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-119">When you use Visual Studio, hello application package structure and manifest files are created by hello New Project template for you.</span></span>

> [!TIP]
> <span data-ttu-id="9f2b1-120">Hello простым способом toopackage образ контейнера в службу — toouse Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-120">hello easiest way toopackage an existing container image into a service is toouse Visual Studio.</span></span>

## <a name="use-visual-studio-toopackage-an-existing-container-image"></a><span data-ttu-id="9f2b1-121">Используйте Visual Studio toopackage существующего образа контейнера</span><span class="sxs-lookup"><span data-stu-id="9f2b1-121">Use Visual Studio toopackage an existing container image</span></span>
<span data-ttu-id="9f2b1-122">Visual Studio предоставляет Service Fabric toohelp шаблона службы, развертывание кластера Service Fabric tooa контейнера.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-122">Visual Studio provides a Service Fabric service template toohelp you deploy a container tooa Service Fabric cluster.</span></span>

1. <span data-ttu-id="9f2b1-123">Чтобы создать приложение Service Fabric, выберите **Файл** > **Создать проект**.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-123">Choose **File** > **New Project**, and create a Service Fabric application.</span></span>
2. <span data-ttu-id="9f2b1-124">Выберите **контейнера гостевой** как hello шаблона службы.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-124">Choose **Guest Container** as hello service template.</span></span>
3. <span data-ttu-id="9f2b1-125">Выберите **имя образа** и предоставить hello путь toohello образ в репозитории контейнера.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-125">Choose **Image Name** and provide hello path toohello image in your container repository.</span></span> <span data-ttu-id="9f2b1-126">например `myrepo/myimage:v1` в https://hub.docker.com.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-126">For example, `myrepo/myimage:v1` in https://hub.docker.com</span></span>
4. <span data-ttu-id="9f2b1-127">Присвойте службе имя и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-127">Give your service a name, and click **OK**.</span></span>
5. <span data-ttu-id="9f2b1-128">Если контейнерного службе нужна конечную точку для взаимодействия, теперь можно добавить hello протокол, порт и файле ServiceManifest.xml toohello типа.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-128">If your containerized service needs an endpoint for communication, you can now add hello protocol, port, and type toohello ServiceManifest.xml file.</span></span> <span data-ttu-id="9f2b1-129">Например:</span><span class="sxs-lookup"><span data-stu-id="9f2b1-129">For example:</span></span> 
     
    `<Endpoint Name="MyContainerServiceEndpoint" Protocol="http" Port="80" UriScheme="http" PathSuffix="myapp/" Type="Input" />`
    
    <span data-ttu-id="9f2b1-130">Предоставляя hello `UriScheme`, Service Fabric автоматически регистрирует конечную точку контейнера hello hello службы именования для возможности обнаружения.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-130">By providing hello `UriScheme`, Service Fabric automatically registers hello container endpoint with hello Naming service for discoverability.</span></span> <span data-ttu-id="9f2b1-131">порт Hello можно фиксированной (как показано в предшествующих пример hello) или динамическое выделение памяти.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-131">hello port can either be fixed (as shown in hello preceding example) or dynamically allocated.</span></span> <span data-ttu-id="9f2b1-132">Если не указать порт, динамически выделяется из диапазона портов приложения hello (что произойдет с любой службой).</span><span class="sxs-lookup"><span data-stu-id="9f2b1-132">If you don't specify a port, it is dynamically allocated from hello application port range (as would happen with any service).</span></span>
    <span data-ttu-id="9f2b1-133">Требуется сопоставление tooconfigure hello контейнера toohost портов, указав `PortBinding` политики в манифесте приложения hello.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-133">You also need tooconfigure hello container toohost port mapping by specifying a `PortBinding` policy in hello application manifest.</span></span> <span data-ttu-id="9f2b1-134">Дополнительные сведения см. в разделе [настроить сопоставления портов контейнера toohost](#Portsection).</span><span class="sxs-lookup"><span data-stu-id="9f2b1-134">For more information, see [Configure container toohost port mapping](#Portsection).</span></span>
6. <span data-ttu-id="9f2b1-135">Если для контейнера требуется управление ресурсами, добавьте `ResourceGovernancePolicy`.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-135">If your container needs resource governance then add a `ResourceGovernancePolicy`.</span></span>
8. <span data-ttu-id="9f2b1-136">Если контейнер должен tooauthenticate с частном репозитории, затем добавьте `RepositoryCredentials`.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-136">If your container needs tooauthenticate with a private repository, then add `RepositoryCredentials`.</span></span>
7. <span data-ttu-id="9f2b1-137">При запуске на компьютере Windows Server 2016 с включенной поддержкой контейнера, можно использовать пакет hello и опубликовать действия toodeploy tooyour локального кластера.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-137">If you are running on a Windows Server 2016 machine with container support enabled, you can use hello package and publish action toodeploy tooyour local cluster.</span></span> 
8. <span data-ttu-id="9f2b1-138">Когда все будет готово, можно опубликовать hello приложения tooa удаленного кластера или установить в элемент управления toosource решения hello.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-138">When ready, you can publish hello application tooa remote cluster or check in hello solution toosource control.</span></span> 

<span data-ttu-id="9f2b1-139">Пример извлечения hello [образцы кода контейнера Service Fabric на GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)</span><span class="sxs-lookup"><span data-stu-id="9f2b1-139">For an example, checkout hello [Service Fabric container code samples on GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)</span></span>

## <a name="creating-a-windows-server-2016-cluster"></a><span data-ttu-id="9f2b1-140">Создание кластера Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="9f2b1-140">Creating a Windows Server 2016 cluster</span></span>
<span data-ttu-id="9f2b1-141">toodeploy контейнерного приложения, необходимо включить в кластер под управлением Windows Server 2016 с поддержкой контейнера toocreate.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-141">toodeploy your containerized application, you need toocreate a cluster running Windows Server 2016 with container support enabled.</span></span> <span data-ttu-id="9f2b1-142">Кластер может выполняться локально или быть развернут с использованием Azure Resource Manager в Azure.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-142">Your cluster may be running locally, or deployed via Azure Resource Manager in Azure.</span></span> 

<span data-ttu-id="9f2b1-143">toodeploy имени кластера с помощью диспетчера ресурсов Azure, выберите hello **Windows Server 2016 с контейнерами** изображения параметр в Azure.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-143">toodeploy a cluster using Azure Resource Manager, choose hello **Windows Server 2016 with Containers** image option in Azure.</span></span> <span data-ttu-id="9f2b1-144">См. в статье hello [создание кластера Service Fabric с помощью диспетчера ресурсов Azure](service-fabric-cluster-creation-via-arm.md).</span><span class="sxs-lookup"><span data-stu-id="9f2b1-144">See hello article [Create a Service Fabric cluster by using Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span></span> <span data-ttu-id="9f2b1-145">Убедитесь, что при использовании hello следующие параметры диспетчера ресурсов Azure:</span><span class="sxs-lookup"><span data-stu-id="9f2b1-145">Ensure that you use hello following Azure Resource Manager settings:</span></span>

```xml
"vmImageOffer": { "type": "string","defaultValue": "WindowsServer"     },
"vmImageSku": { "defaultValue": "2016-Datacenter-with-Containers","type": "string"     },
"vmImageVersion": { "defaultValue": "latest","type": "string"     },  
```
<span data-ttu-id="9f2b1-146">Можно также использовать hello [шаблона узла Azure Resource Manager пять](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype) toocreate кластера.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-146">You can also use hello [Five Node Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype) toocreate a cluster.</span></span> <span data-ttu-id="9f2b1-147">Кроме того, можно прочитать [записи блога сообщества](https://loekd.blogspot.com/2017/01/running-windows-containers-on-azure.html) об использовании Service Fabric и контейнеров Windows.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-147">Alternatively read a community [blog post](https://loekd.blogspot.com/2017/01/running-windows-containers-on-azure.html) on using Service Fabric and Windows containers.</span></span>

<a id="manually"></a>

## <a name="manually-package-and-deploy-a-container-image"></a><span data-ttu-id="9f2b1-148">Упаковка и развертывание образа контейнера вручную</span><span class="sxs-lookup"><span data-stu-id="9f2b1-148">Manually package and deploy a container image</span></span>
<span data-ttu-id="9f2b1-149">процесс Hello вручную упаковки контейнерного службы зависит от hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="9f2b1-149">hello process of manually packaging a containerized service is based on hello following steps:</span></span>

1. <span data-ttu-id="9f2b1-150">Опубликуйте репозиторий tooyour контейнеры hello.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-150">Publish hello containers tooyour repository.</span></span>
2. <span data-ttu-id="9f2b1-151">Создайте структуру каталогов пакета hello.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-151">Create hello package directory structure.</span></span>
3. <span data-ttu-id="9f2b1-152">Измените файл манифеста службы hello.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-152">Edit hello service manifest file.</span></span>
4. <span data-ttu-id="9f2b1-153">Измените файл манифеста приложения hello.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-153">Edit hello application manifest file.</span></span>

## <a name="deploy-and-activate-a-container-image"></a><span data-ttu-id="9f2b1-154">Развертывание и активация образа контейнера</span><span class="sxs-lookup"><span data-stu-id="9f2b1-154">Deploy and activate a container image</span></span>
<span data-ttu-id="9f2b1-155">В Service Fabric hello [модель приложения](service-fabric-application-model.md), контейнер представляет узел приложения в службу, которая несколько размещаются реплики.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-155">In hello Service Fabric [application model](service-fabric-application-model.md), a container represents an application host in which multiple service replicas are placed.</span></span> <span data-ttu-id="9f2b1-156">toodeploy и активировать контейнер, put hello имя образа контейнера hello в `ContainerHost` элемент в манифест службы hello.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-156">toodeploy and activate a container, put hello name of hello container image into a `ContainerHost` element in hello service manifest.</span></span>

<span data-ttu-id="9f2b1-157">Добавьте в манифест службы hello, `ContainerHost` для точки входа hello.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-157">In hello service manifest, add a `ContainerHost` for hello entry point.</span></span> <span data-ttu-id="9f2b1-158">Затем набор hello `ImageName` имя hello toobe репозиторий контейнера hello и изображения.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-158">Then set hello `ImageName` toobe hello name of hello container repository and image.</span></span> <span data-ttu-id="9f2b1-159">Hello ниже частичного манифест является примером как вызывать контейнер hello toodeploy `myimage:v1` из репозитория вызывается `myrepo`:</span><span class="sxs-lookup"><span data-stu-id="9f2b1-159">hello following partial manifest shows an example of how toodeploy hello container called `myimage:v1` from a repository called `myrepo`:</span></span>

```xml
    <CodePackage Name="Code" Version="1.0">
        <EntryPoint>
          <ContainerHost>
            <ImageName>myrepo/myimage:v1</ImageName>
            <Commands></Commands>
          </ContainerHost>
        </EntryPoint>
    </CodePackage>
```

<span data-ttu-id="9f2b1-160">Можно указать toorun дополнительные команды при запуске hello контейнере hello `Commands` элемента.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-160">You can specify optional commands toorun upon starting hello container under hello `Commands` element.</span></span> <span data-ttu-id="9f2b1-161">Команды нужно разделить запятыми.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-161">For multiple commands, comma-delimit them.</span></span> 

## <a name="understand-resource-governance"></a><span data-ttu-id="9f2b1-162">Концепция управления ресурсами</span><span class="sxs-lookup"><span data-stu-id="9f2b1-162">Understand resource governance</span></span>
<span data-ttu-id="9f2b1-163">Управление ресурсами — возможность hello контейнера, который ограничивает ресурсы hello, hello контейнера можно использовать на узле hello.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-163">Resource governance is a capability of hello container that restricts hello resources that hello container can use on hello host.</span></span> <span data-ttu-id="9f2b1-164">Hello `ResourceGovernancePolicy`, что указывается в манифесте приложения hello являются ограничения ресурсов используется toodeclare для пакета кода службы.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-164">hello `ResourceGovernancePolicy`, which is specified in hello application manifest is used toodeclare resource limits for a service code package.</span></span> <span data-ttu-id="9f2b1-165">Ограничения ресурсов можно задать для hello следующие ресурсы:</span><span class="sxs-lookup"><span data-stu-id="9f2b1-165">Resource limits can be set for hello following resources:</span></span>

* <span data-ttu-id="9f2b1-166">Память</span><span class="sxs-lookup"><span data-stu-id="9f2b1-166">Memory</span></span>
* <span data-ttu-id="9f2b1-167">MemorySwap;</span><span class="sxs-lookup"><span data-stu-id="9f2b1-167">MemorySwap</span></span>
* <span data-ttu-id="9f2b1-168">CpuShares;</span><span class="sxs-lookup"><span data-stu-id="9f2b1-168">CpuShares (CPU relative weight)</span></span>
* <span data-ttu-id="9f2b1-169">MemoryReservationInMB;</span><span class="sxs-lookup"><span data-stu-id="9f2b1-169">MemoryReservationInMB</span></span>  
* <span data-ttu-id="9f2b1-170">BlkioWeight.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-170">BlkioWeight (BlockIO relative weight).</span></span>

> [!NOTE]
> <span data-ttu-id="9f2b1-171">Поддержка ограничений на определенные параметры блочного ввода-вывода, включая число операций ввода-вывода, скорость чтения-записи и т. п., планируется в будущих выпусках.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-171">Support for specifying specific block IO limits such as IOPs, read/write BPS, and others are planned for a future release.</span></span>
> 
> 

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ResourceGovernancePolicy CodePackageRef="FrontendService.Code" CpuShares="500"
            MemoryInMB="1024" MemorySwapInMB="4084" MemoryReservationInMB="1024" />
        </Policies>
    </ServiceManifestImport>
```

## <a name="authenticate-a-repository"></a><span data-ttu-id="9f2b1-172">Проверка подлинности в репозитории</span><span class="sxs-lookup"><span data-stu-id="9f2b1-172">Authenticate a repository</span></span>
<span data-ttu-id="9f2b1-173">toodownload контейнера, возможно, репозиторий контейнера toohello tooprovide учетных данных для входа.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-173">toodownload a container, you might have tooprovide sign-in credentials toohello container repository.</span></span> <span data-ttu-id="9f2b1-174">Hello учетных данных для входа, указанный в манифесте приложения hello, являются hello используется toospecify входа в систему или ключа SSH, загрузки образа контейнера hello из репозитория образов hello.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-174">hello sign-in credentials, specified in hello application manifest, are used toospecify hello sign-in information, or SSH key, for downloading hello container image from hello image repository.</span></span> <span data-ttu-id="9f2b1-175">Hello пример учетной записи называется *TestUser* вместе с hello пароль в виде открытого текста (*не* рекомендуется):</span><span class="sxs-lookup"><span data-stu-id="9f2b1-175">hello following example shows an account called *TestUser* along with hello password in clear text (*not* recommended):</span></span>

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                <RepositoryCredentials AccountName="TestUser" Password="12345" PasswordEncrypted="false"/>
            </ContainerHostPolicies>
        </Policies>
    </ServiceManifestImport>
```

<span data-ttu-id="9f2b1-176">Рекомендуется шифровать hello пароль, с помощью сертификата, где развернуты toohello машины.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-176">We recommend that you encrypt hello password by using a certificate that's deployed toohello machine.</span></span>

<span data-ttu-id="9f2b1-177">Hello пример учетной записи называется *TestUser*, где hello пароль был зашифрован с помощью сертификата с именем *MyCert*.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-177">hello following example shows an account called *TestUser*, where hello password was encrypted by using a certificate called *MyCert*.</span></span> <span data-ttu-id="9f2b1-178">Можно использовать hello `Invoke-ServiceFabricEncryptText` PowerShell команды toocreate hello секретный зашифрованного текста hello пароль.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-178">You can use hello `Invoke-ServiceFabricEncryptText` PowerShell command toocreate hello secret cipher text for hello password.</span></span> <span data-ttu-id="9f2b1-179">Дополнительные сведения см. в статье hello [управление секретные данные в приложения Service Fabric](service-fabric-application-secret-management.md).</span><span class="sxs-lookup"><span data-stu-id="9f2b1-179">For more information, see hello article [Managing secrets in Service Fabric applications](service-fabric-application-secret-management.md).</span></span>

<span data-ttu-id="9f2b1-180">закрытый ключ Hello hello сертификата, который использован toodecrypt hello пароль должен быть развернутой toohello локального компьютера в методе по каналу.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-180">hello private key of hello certificate that's used toodecrypt hello password must be deployed toohello local machine in an out-of-band method.</span></span> <span data-ttu-id="9f2b1-181">(В Azure для этого используется Azure Resource Manager.) Затем когда Service Fabric развертывает пакет toohello hello службы компьютера, может расшифровать секретный hello.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-181">(In Azure, this method is Azure Resource Manager.) Then, when Service Fabric deploys hello service package toohello machine, it can decrypt hello secret.</span></span> <span data-ttu-id="9f2b1-182">С помощью секрет hello вместе с именем учетной записи hello, он может затем выполнить проверку подлинности hello репозиторий контейнера.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-182">By using hello secret along with hello account name, it can then authenticate with hello container repository.</span></span>

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                <RepositoryCredentials AccountName="TestUser" Password="[Put encrypted password here using MyCert certificate ]" PasswordEncrypted="true"/>
            </ContainerHostPolicies>
        </Policies>
    </ServiceManifestImport>
```

## <span data-ttu-id="9f2b1-183"><a name ="Portsection"></a>Настройка сопоставления портов toohost контейнера</span><span class="sxs-lookup"><span data-stu-id="9f2b1-183"><a name ="Portsection"></a> Configure container toohost port mapping</span></span>
<span data-ttu-id="9f2b1-184">Можно настроить порт, используемый узла toocommunicate с контейнером hello, указав `PortBinding` в манифесте приложения hello.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-184">You can configure a host port used toocommunicate with hello container by specifying a `PortBinding` in hello application manifest.</span></span> <span data-ttu-id="9f2b1-185">Hello порт maps hello порт toowhich hello службы привязки ожидает передачи данных внутри hello контейнера tooa порту hello узла.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-185">hello port binding maps hello port toowhich hello service is listening inside hello container tooa port on hello host.</span></span>

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                <PortBinding ContainerPort="8905"/>
            </ContainerHostPolicies>
        </Policies>
    </ServiceManifestImport>
```

## <a name="configure-container-to-container-discovery-and-communication"></a><span data-ttu-id="9f2b1-186">Настройка межконтейнерного поиска и обмена данными</span><span class="sxs-lookup"><span data-stu-id="9f2b1-186">Configure container-to-container discovery and communication</span></span>
<span data-ttu-id="9f2b1-187">Можно использовать hello `PortBinding` элемент toomap tooan конечную точку порт контейнера в манифест службы hello.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-187">You can use hello `PortBinding` element toomap a container port tooan endpoint in hello service manifest.</span></span> <span data-ttu-id="9f2b1-188">В следующем примере hello, hello конечной точки `Endpoint1` указывает 8905 фиксированный порт.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-188">In hello following example, hello endpoint `Endpoint1` specifies a fixed port, 8905.</span></span> <span data-ttu-id="9f2b1-189">Она также может указывать порт не во всех в этом случае выбирается случайный порт из диапазона портов приложения hello кластера для вас.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-189">It can also specify no port at all, in which case a random port from hello cluster's application port range is chosen for you.</span></span>


```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                <PortBinding ContainerPort="8905" EndpointRef="Endpoint1"/>
            </ContainerHostPolicies>
        </Policies>
    </ServiceManifestImport>
```
<span data-ttu-id="9f2b1-190">При указании конечной точки с помощью hello `Endpoint` тег в манифесте службы hello контейнера гостевой Service Fabric автоматически можно опубликовать toohello этой конечной точки службы именования.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-190">If you specify an endpoint, using hello `Endpoint` tag in hello service manifest of a guest container, Service Fabric can automatically publish this endpoint toohello Naming service.</span></span> <span data-ttu-id="9f2b1-191">Другие службы, работающие в кластере hello таким образом может обнаруживать этого контейнера, с помощью запросов REST hello в разрешении.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-191">Other services that are running in hello cluster can thus discover this container using hello REST queries for resolving.</span></span>

<span data-ttu-id="9f2b1-192">С помощью регистрации hello службы именования, можно выполнять контейнера в связи внутри контейнера с помощью hello [обратный прокси-сервер](service-fabric-reverseproxy.md).</span><span class="sxs-lookup"><span data-stu-id="9f2b1-192">By registering with hello Naming service, you can perform container-to-container communication within your container by using hello [reverse proxy](service-fabric-reverseproxy.md).</span></span> <span data-ttu-id="9f2b1-193">Обмен данными выполняется путем предоставления hello обратного прокси-сервера HTTP-порт прослушивания и имени hello hello служб, которые требуется toocommunicate с в переменных среды.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-193">Communication is performed by providing hello reverse proxy http listening port and hello name of hello services that you want toocommunicate with as environment variables.</span></span> <span data-ttu-id="9f2b1-194">Дополнительные сведения см. Далее раздел hello.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-194">For more information, see hello next section.</span></span> 

## <a name="configure-and-set-environment-variables"></a><span data-ttu-id="9f2b1-195">Настройка и установка переменных среды</span><span class="sxs-lookup"><span data-stu-id="9f2b1-195">Configure and set environment variables</span></span>
<span data-ttu-id="9f2b1-196">Переменные среды можно указать для каждого пакета кода hello манифеста службы.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-196">Environment variables can be specified for each code package in hello service manifest.</span></span> <span data-ttu-id="9f2b1-197">Эта функция доступна для всех служб, вне зависимости от того, как они развернуты: в качестве контейнеров, процессов или гостевых исполняемых файлов.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-197">This feature is available for all services irrespective of whether they are deployed as containers or processes or guest executables.</span></span> <span data-ttu-id="9f2b1-198">Можно переопределить переменную среды, значения в приложение hello манифеста или указать их во время развертывания, как параметры приложения.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-198">You can override environment variable values in hello application manifest or specify them during deployment as application parameters.</span></span>

<span data-ttu-id="9f2b1-199">Hello следующий фрагмент XML манифеста службы показан пример того, как переменные среды toospecify для пакета кода:</span><span class="sxs-lookup"><span data-stu-id="9f2b1-199">hello following service manifest XML snippet shows an example of how toospecify environment variables for a code package:</span></span>

```xml
    <ServiceManifest Name="FrontendServicePackage" Version="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <Description>a guest executable service in a container</Description>
        <ServiceTypes>
            <StatelessServiceType ServiceTypeName="StatelessFrontendService"  UseImplicitHost="true"/>
        </ServiceTypes>
        <CodePackage Name="FrontendService.Code" Version="1.0">
            <EntryPoint>
            <ContainerHost>
                <ImageName>myrepo/myimage:v1</ImageName>
                <Commands></Commands>
            </ContainerHost>
            </EntryPoint>
            <EnvironmentVariables>
                <EnvironmentVariable Name="HttpGatewayPort" Value=""/>
                <EnvironmentVariable Name="BackendServiceName" Value=""/>
            </EnvironmentVariables>
        </CodePackage>
    </ServiceManifest>
```

<span data-ttu-id="9f2b1-200">Эти переменные среды может быть переопределено на уровне манифеста приложения hello:</span><span class="sxs-lookup"><span data-stu-id="9f2b1-200">These environment variables can be overridden at hello application manifest level:</span></span>

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <EnvironmentOverrides CodePackageRef="FrontendService.Code">
            <EnvironmentVariable Name="BackendServiceName" Value="[BackendSvc]"/>
            <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
        </EnvironmentOverrides>
    </ServiceManifestImport>
```

<span data-ttu-id="9f2b1-201">В предыдущем примере hello, мы указали явное значение для hello `HttpGateway` переменной среды (19000), пока мы значение hello `BackendServiceName` параметр hello `[BackendSvc]` параметр приложения.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-201">In hello previous example, we specified an explicit value for hello `HttpGateway` environment variable (19000), while we set hello value for `BackendServiceName` parameter via hello `[BackendSvc]` application parameter.</span></span> <span data-ttu-id="9f2b1-202">Эти параметры включают значение hello toospecify `BackendServiceName`значение при развертывании приложения hello и имеет фиксированное значение в манифесте hello.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-202">These settings enable you toospecify hello value for `BackendServiceName`value when you deploy hello application and not have a fixed value in hello manifest.</span></span>

## <a name="configure-isolation-mode"></a><span data-ttu-id="9f2b1-203">Настройка режима изоляции</span><span class="sxs-lookup"><span data-stu-id="9f2b1-203">Configure isolation mode</span></span>

<span data-ttu-id="9f2b1-204">Windows поддерживает два режима изоляции для контейнеров: режим изоляции процессов и Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-204">Windows supports two isolation modes for containers - process and Hyper-V.</span></span>  <span data-ttu-id="9f2b1-205">С режимом изоляции процессов hello запущенных на всех контейнеров hello hello же hello ядро общей папки узла машины с узла hello.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-205">With hello process isolation mode, all hello containers running on hello same host machine share hello kernel with hello host.</span></span> <span data-ttu-id="9f2b1-206">С режимом изоляции hello Hyper-V изолированы hello ядра между каждым контейнером Hyper-V и узлом контейнера hello.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-206">With hello Hyper-V isolation mode, hello kernels are isolated between each Hyper-V container and hello container host.</span></span> <span data-ttu-id="9f2b1-207">Указанный режим изоляции Hello в hello `ContainerHostPolicies` тег в файле манифеста приложения hello.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-207">hello isolation mode is specified in hello `ContainerHostPolicies` tag in hello application manifest file.</span></span>  <span data-ttu-id="9f2b1-208">Режимы изоляции Hello, которые могут быть указаны `process`, `hyperv`, и `default`.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-208">hello isolation modes that can be specified are `process`, `hyperv`, and `default`.</span></span> <span data-ttu-id="9f2b1-209">Hello `default` режим изоляции по умолчанию слишком`process` на сервере Windows размещает и по умолчанию слишком`hyperv` на узлах Windows 10.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-209">hello `default` isolation mode defaults too`process` on Windows Server hosts, and defaults too`hyperv` on Windows 10 hosts.</span></span>  <span data-ttu-id="9f2b1-210">Hello следующий фрагмент кода показывает, как режим изоляции hello задается в файле манифеста приложения hello.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-210">hello following snippet shows how hello isolation mode is specified in hello application manifest file.</span></span>

```xml
   <ContainerHostPolicies CodePackageRef="NodeService.Code" Isolation="hyperv">
```


## <a name="complete-examples-for-application-and-service-manifest"></a><span data-ttu-id="9f2b1-211">Полные примеры манифестов для приложения и службы</span><span class="sxs-lookup"><span data-stu-id="9f2b1-211">Complete examples for application and service manifest</span></span>

<span data-ttu-id="9f2b1-212">Ниже приведен пример манифеста приложения.</span><span class="sxs-lookup"><span data-stu-id="9f2b1-212">An example application manifest follows:</span></span>

```xml
    <ApplicationManifest ApplicationTypeName="SimpleContainerApp" ApplicationTypeVersion="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <Description>A simple service container application</Description>
        <Parameters>
            <Parameter Name="ServiceInstanceCount" DefaultValue="3"></Parameter>
            <Parameter Name="BackEndSvcName" DefaultValue="bkend"></Parameter>
        </Parameters>
        <ServiceManifestImport>
            <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
            <EnvironmentOverrides CodePackageRef="FrontendService.Code">
                <EnvironmentVariable Name="BackendServiceName" Value="[BackendSvcName]"/>
                <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
            </EnvironmentOverrides>
            <Policies>
                <ResourceGovernancePolicy CodePackageRef="Code" CpuShares="500" MemoryInMB="1024" MemorySwapInMB="4084" MemoryReservationInMB="1024" />
                <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                    <RepositoryCredentials AccountName="username" Password="****" PasswordEncrypted="true"/>
                    <PortBinding ContainerPort="8905" EndpointRef="Endpoint1"/>
                </ContainerHostPolicies>
            </Policies>
        </ServiceManifestImport>
    </ApplicationManifest>
```

<span data-ttu-id="9f2b1-213">Далее приведен пример службы манифеста (указанных в предшествующих манифест приложения hello):</span><span class="sxs-lookup"><span data-stu-id="9f2b1-213">An example service manifest (specified in hello preceding application manifest) follows:</span></span>

```xml
    <ServiceManifest Name="FrontendServicePackage" Version="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <Description> A service that implements a stateless front end in a container</Description>
        <ServiceTypes>
            <StatelessServiceType ServiceTypeName="StatelessFrontendService"  UseImplicitHost="true"/>
        </ServiceTypes>
        <CodePackage Name="FrontendService.Code" Version="1.0">
            <EntryPoint>
            <ContainerHost>
                <ImageName>myrepo/myimage:v1</ImageName>
                <Commands></Commands>
            </ContainerHost>
            </EntryPoint>
            <EnvironmentVariables>
                <EnvironmentVariable Name="HttpGatewayPort" Value=""/>
                <EnvironmentVariable Name="BackendServiceName" Value=""/>
            </EnvironmentVariables>
        </CodePackage>
        <ConfigPackage Name="FrontendService.Config" Version="1.0" />
        <DataPackage Name="FrontendService.Data" Version="1.0" />
        <Resources>
            <Endpoints>
                <Endpoint Name="Endpoint1" UriScheme="http" Port="80" Protocol="http"/>
            </Endpoints>
        </Resources>
    </ServiceManifest>
```

## <a name="next-steps"></a><span data-ttu-id="9f2b1-214">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9f2b1-214">Next steps</span></span>
<span data-ttu-id="9f2b1-215">Вы развернули контейнерного службы, узнаете, как toomanage его жизненного цикла, считывая [жизненный цикл приложений фабрики служб](service-fabric-application-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="9f2b1-215">Now that you have deployed a containerized service, learn how toomanage its lifecycle by reading [Service Fabric application lifecycle](service-fabric-application-lifecycle.md).</span></span>

* [<span data-ttu-id="9f2b1-216">Общие сведения о Service Fabric и контейнерах</span><span class="sxs-lookup"><span data-stu-id="9f2b1-216">Overview of Service Fabric and containers</span></span>](service-fabric-containers-overview.md)
* <span data-ttu-id="9f2b1-217">В качестве примера можно ознакомиться с [примерами кода контейнера Service Fabric на сайте GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers).</span><span class="sxs-lookup"><span data-stu-id="9f2b1-217">For an example, checkout [Service Fabric container code samples on GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)</span></span>
