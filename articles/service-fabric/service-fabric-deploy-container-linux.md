---
title: "aaaService структуры и развертывание контейнерами Linux | Документы Microsoft"
description: "Service Fabric и hello используют приложения микрослужбу toodeploy контейнеров Linux. В этой статье описываются возможности hello, предоставляемых Service Fabric для контейнеров и как toodeploy Linux образ контейнера в кластер"
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: 4ba99103-6064-429d-ba17-82861b6ddb11
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 6/29/2017
ms.author: msfussell
ms.openlocfilehash: e28f99a145b0594d871b0ec0566233a7ad235ce8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-linux-container-tooservice-fabric"></a><span data-ttu-id="72064-104">Развертывание tooService контейнера Linux структуры</span><span class="sxs-lookup"><span data-stu-id="72064-104">Deploy a Linux container tooService Fabric</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="72064-105">Развертывание контейнера Windows</span><span class="sxs-lookup"><span data-stu-id="72064-105">Deploy Windows Container</span></span>](service-fabric-deploy-container.md)
> * [<span data-ttu-id="72064-106">Развертывание контейнера Linux</span><span class="sxs-lookup"><span data-stu-id="72064-106">Deploy Linux Container</span></span>](service-fabric-deploy-container-linux.md)
>
>

<span data-ttu-id="72064-107">В этой статье подробно рассматривается создание контейнерных служб в контейнерах Docker в Linux.</span><span class="sxs-lookup"><span data-stu-id="72064-107">This article walks you through building containerized services in Docker containers on Linux.</span></span>

<span data-ttu-id="72064-108">В Service Fabric реализовано несколько способов использования контейнеров для создания приложений, состоящих из контейнерных микрослужб.</span><span class="sxs-lookup"><span data-stu-id="72064-108">Service Fabric has several container capabilities that help you with building applications that are composed of microservices that are containerized.</span></span> <span data-ttu-id="72064-109">Эти службы называются контейнерными.</span><span class="sxs-lookup"><span data-stu-id="72064-109">These services are called containerized services.</span></span>

<span data-ttu-id="72064-110">следующие возможности Hello;</span><span class="sxs-lookup"><span data-stu-id="72064-110">hello capabilities include;</span></span>

* <span data-ttu-id="72064-111">развертывание и активация образа контейнера;</span><span class="sxs-lookup"><span data-stu-id="72064-111">Container image deployment and activation</span></span>
* <span data-ttu-id="72064-112">управление ресурсами;</span><span class="sxs-lookup"><span data-stu-id="72064-112">Resource governance</span></span>
* <span data-ttu-id="72064-113">проверка подлинности репозитория;</span><span class="sxs-lookup"><span data-stu-id="72064-113">Repository authentication</span></span>
* <span data-ttu-id="72064-114">Сопоставление портов toohost порт контейнера</span><span class="sxs-lookup"><span data-stu-id="72064-114">Container port toohost port mapping</span></span>
* <span data-ttu-id="72064-115">межконтейнерное обнаружение и взаимодействие;</span><span class="sxs-lookup"><span data-stu-id="72064-115">Container-to-container discovery and communication</span></span>
* <span data-ttu-id="72064-116">Возможность tooconfigure и установка переменных среды</span><span class="sxs-lookup"><span data-stu-id="72064-116">Ability tooconfigure and set environment variables</span></span>

## <a name="packaging-a-docker-container-with-yeoman"></a><span data-ttu-id="72064-117">Упаковка контейнера Docker с помощью yeoman</span><span class="sxs-lookup"><span data-stu-id="72064-117">Packaging a docker container with yeoman</span></span>
<span data-ttu-id="72064-118">При упаковке контейнер в Linux, вы можете либо toouse yeoman шаблона или [вручную создать пакет приложения hello](#manually).</span><span class="sxs-lookup"><span data-stu-id="72064-118">When packaging a container on Linux, you can choose either toouse a yeoman template or [create hello application package manually](#manually).</span></span>

<span data-ttu-id="72064-119">Приложение службы. Структура может содержать один или несколько контейнеров, каждый с определенной ролью в предоставлении функциональных возможностей приложения hello.</span><span class="sxs-lookup"><span data-stu-id="72064-119">A Service Fabric application can contain one or more containers, each with a specific role in delivering hello application's functionality.</span></span> <span data-ttu-id="72064-120">Hello Service Fabric SDK для Linux включает [Yeoman](http://yeoman.io/) генератор, который позволяет легко toocreate приложения и добавить образ контейнера.</span><span class="sxs-lookup"><span data-stu-id="72064-120">hello Service Fabric SDK for Linux includes a [Yeoman](http://yeoman.io/) generator that makes it easy toocreate your application and add a container image.</span></span> <span data-ttu-id="72064-121">Воспользуемся вызывается приложение с помощью одного контейнера Docker Yeoman toocreate *SimpleContainerApp*.</span><span class="sxs-lookup"><span data-stu-id="72064-121">Let's use Yeoman toocreate an application with a single Docker container called *SimpleContainerApp*.</span></span> <span data-ttu-id="72064-122">Дополнительные службы можно добавить позже, изменив hello созданных файлов манифеста.</span><span class="sxs-lookup"><span data-stu-id="72064-122">You can add more services later by editing hello generated manifest files.</span></span>

## <a name="install-docker-on-your-development-box"></a><span data-ttu-id="72064-123">Установка Docker в среде разработки</span><span class="sxs-lookup"><span data-stu-id="72064-123">Install Docker on your development box</span></span>

<span data-ttu-id="72064-124">Hello для выполнения следующих команд docker tooinstall на компьютере разработки Linux (при использовании образа vagrant hello в OSX docker уже установлена):</span><span class="sxs-lookup"><span data-stu-id="72064-124">Run hello following commands tooinstall docker on your Linux development box (if you are using hello vagrant image on OSX, docker is already installed):</span></span>

```bash
    sudo apt-get install wget
    wget -qO- https://get.docker.io/ | sh
```

## <a name="create-hello-application"></a><span data-ttu-id="72064-125">Создание приложения hello</span><span class="sxs-lookup"><span data-stu-id="72064-125">Create hello application</span></span>
1. <span data-ttu-id="72064-126">В окне терминала введите `yo azuresfcontainer`.</span><span class="sxs-lookup"><span data-stu-id="72064-126">In a terminal, type `yo azuresfcontainer`.</span></span>
2. <span data-ttu-id="72064-127">Укажите имя приложения, например mycontainerap.</span><span class="sxs-lookup"><span data-stu-id="72064-127">Name your application - for example, mycontainerap</span></span>
3. <span data-ttu-id="72064-128">Укажите URL-адрес hello hello образ контейнера из репозитория DockerHub.</span><span class="sxs-lookup"><span data-stu-id="72064-128">Provide hello URL for hello container image from a DockerHub repo.</span></span> <span data-ttu-id="72064-129">Здравствуйте изображения параметр принимает hello формы [репозитория] / [имя изображения]</span><span class="sxs-lookup"><span data-stu-id="72064-129">hello image parameter takes hello form [repo]/[image name]</span></span>
4. <span data-ttu-id="72064-130">Если изображение hello не имеет рабочей нагрузки — точек входа, то вы должны tooexplicitly укажите ввода команды с набором команд toorun внутри контейнера hello, который будет сохранить после запуска контейнера hello с разделителями запятыми.</span><span class="sxs-lookup"><span data-stu-id="72064-130">If hello image does not have a workload entry-point defined, then you need tooexplicitly specify input commands with a comma-delimited set of commands toorun inside hello container, which will keep hello container running after startup.</span></span>

![Генератор Service Fabric Yeoman для контейнеров][sf-yeoman]

## <a name="deploy-hello-application"></a><span data-ttu-id="72064-132">Развертывание приложения hello</span><span class="sxs-lookup"><span data-stu-id="72064-132">Deploy hello application</span></span>

### <a name="using-xplat-cli"></a><span data-ttu-id="72064-133">Использование кроссплатформенного интерфейса командной строки</span><span class="sxs-lookup"><span data-stu-id="72064-133">Using XPlat CLI</span></span>
<span data-ttu-id="72064-134">После построения приложения hello, его можно развернуть toohello локального кластера с помощью hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="72064-134">Once hello application is built, you can deploy it toohello local cluster using hello Azure CLI.</span></span>

1. <span data-ttu-id="72064-135">Подключите toohello локальный кластер Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="72064-135">Connect toohello local Service Fabric cluster.</span></span>

    ```bash
    azure servicefabric cluster connect
    ```

2. <span data-ttu-id="72064-136">Скрипт установки используйте hello, предоставляемых в toocopy hello шаблона приложения hello пакета хранилище образов кластера toohello, регистрация типа приложения hello и создание экземпляра приложения hello.</span><span class="sxs-lookup"><span data-stu-id="72064-136">Use hello install script provided in hello template toocopy hello application package toohello cluster's image store, register hello application type, and create an instance of hello application.</span></span>

    ```bash
    ./install.sh
    ```

3. <span data-ttu-id="72064-137">Откройте браузер и перейдите tooService Fabric Explorer на http://localhost:19080/обозреватель (замените localhost hello частного IP-адреса hello виртуальной Машины при использовании Vagrant в Mac OS X).</span><span class="sxs-lookup"><span data-stu-id="72064-137">Open a browser and navigate tooService Fabric Explorer at http://localhost:19080/Explorer (replace localhost with hello private IP of hello VM if using Vagrant on Mac OS X).</span></span>
4. <span data-ttu-id="72064-138">Разверните узел приложения hello и обратите внимание, что теперь запись для типа приложения, а другая — для первого экземпляра этого типа hello.</span><span class="sxs-lookup"><span data-stu-id="72064-138">Expand hello Applications node and note that there is now an entry for your application type and another for hello first instance of that type.</span></span>
5. <span data-ttu-id="72064-139">Использовать сценарий удаления hello, указанные в экземпляр приложения hello toodelete шаблона hello и отмены регистрации типа приложения hello.</span><span class="sxs-lookup"><span data-stu-id="72064-139">Use hello uninstall script provided in hello template toodelete hello application instance and unregister hello application type.</span></span>

    ```bash
    ./uninstall.sh
    ```

### <a name="using-azure-cli-20"></a><span data-ttu-id="72064-140">Использование Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="72064-140">Using Azure CLI 2.0</span></span>

<span data-ttu-id="72064-141">. В разделе doc hello Справочник по управлению [жизненного цикла приложения с помощью hello Azure CLI 2.0](service-fabric-application-lifecycle-azure-cli-2-0.md).</span><span class="sxs-lookup"><span data-stu-id="72064-141">See hello reference doc on managing an [application life cycle using hello Azure CLI 2.0](service-fabric-application-lifecycle-azure-cli-2-0.md).</span></span>

<span data-ttu-id="72064-142">Пример приложения [извлечение hello код контейнера Service Fabric. Примеры на GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)</span><span class="sxs-lookup"><span data-stu-id="72064-142">For an example application, [checkout hello Service Fabric container code samples on GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)</span></span>

## <a name="adding-more-services-tooan-existing-application"></a><span data-ttu-id="72064-143">Добавление существующего приложения tooan дополнительные службы</span><span class="sxs-lookup"><span data-stu-id="72064-143">Adding more services tooan existing application</span></span>

<span data-ttu-id="72064-144">tooadd tooan приложение, уже созданные с помощью службы в другой контейнер `yo`, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="72064-144">tooadd another container service tooan application already created using `yo`, perform hello following steps:</span></span>

1. <span data-ttu-id="72064-145">Измените корневой каталог toohello существующее приложение hello.</span><span class="sxs-lookup"><span data-stu-id="72064-145">Change directory toohello root of hello existing application.</span></span>  <span data-ttu-id="72064-146">Например `cd ~/YeomanSamples/MyApplication`, если `MyApplication` является приложение hello, созданных Yeoman.</span><span class="sxs-lookup"><span data-stu-id="72064-146">For example, `cd ~/YeomanSamples/MyApplication`, if `MyApplication` is hello application created by Yeoman.</span></span>
2. <span data-ttu-id="72064-147">Запустите `yo azuresfcontainer:AddService`</span><span class="sxs-lookup"><span data-stu-id="72064-147">Run `yo azuresfcontainer:AddService`</span></span>

<a id="manually"></a>

## <a name="manually-package-and-deploy-a-container-image"></a><span data-ttu-id="72064-148">Упаковка и развертывание образа контейнера вручную</span><span class="sxs-lookup"><span data-stu-id="72064-148">Manually package and deploy a container image</span></span>
<span data-ttu-id="72064-149">процесс Hello вручную упаковки контейнерного службы зависит от hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="72064-149">hello process of manually packaging a containerized service is based on hello following steps:</span></span>

1. <span data-ttu-id="72064-150">Опубликуйте репозиторий tooyour контейнеры hello.</span><span class="sxs-lookup"><span data-stu-id="72064-150">Publish hello containers tooyour repository.</span></span>
2. <span data-ttu-id="72064-151">Создайте структуру каталогов пакета hello.</span><span class="sxs-lookup"><span data-stu-id="72064-151">Create hello package directory structure.</span></span>
3. <span data-ttu-id="72064-152">Измените файл манифеста службы hello.</span><span class="sxs-lookup"><span data-stu-id="72064-152">Edit hello service manifest file.</span></span>
4. <span data-ttu-id="72064-153">Измените файл манифеста приложения hello.</span><span class="sxs-lookup"><span data-stu-id="72064-153">Edit hello application manifest file.</span></span>

## <a name="deploy-and-activate-a-container-image"></a><span data-ttu-id="72064-154">Развертывание и активация образа контейнера</span><span class="sxs-lookup"><span data-stu-id="72064-154">Deploy and activate a container image</span></span>
<span data-ttu-id="72064-155">В Service Fabric hello [модель приложения](service-fabric-application-model.md), контейнер представляет узел приложения в службу, которая несколько размещаются реплики.</span><span class="sxs-lookup"><span data-stu-id="72064-155">In hello Service Fabric [application model](service-fabric-application-model.md), a container represents an application host in which multiple service replicas are placed.</span></span> <span data-ttu-id="72064-156">toodeploy и активировать контейнер, put hello имя образа контейнера hello в `ContainerHost` элемент в манифест службы hello.</span><span class="sxs-lookup"><span data-stu-id="72064-156">toodeploy and activate a container, put hello name of hello container image into a `ContainerHost` element in hello service manifest.</span></span>

<span data-ttu-id="72064-157">Добавьте в манифест службы hello, `ContainerHost` для точки входа hello.</span><span class="sxs-lookup"><span data-stu-id="72064-157">In hello service manifest, add a `ContainerHost` for hello entry point.</span></span> <span data-ttu-id="72064-158">Затем набор hello `ImageName` имя hello toobe репозиторий контейнера hello и изображения.</span><span class="sxs-lookup"><span data-stu-id="72064-158">Then set hello `ImageName` toobe hello name of hello container repository and image.</span></span> <span data-ttu-id="72064-159">Hello ниже частичного манифест является примером как вызывать контейнер hello toodeploy `myimage:v1` из репозитория вызывается `myrepo`:</span><span class="sxs-lookup"><span data-stu-id="72064-159">hello following partial manifest shows an example of how toodeploy hello container called `myimage:v1` from a repository called `myrepo`:</span></span>

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

<span data-ttu-id="72064-160">Можно присвоить ввода команды, указав hello необязательно `Commands` элемента с набором команд toorun внутри контейнера hello с разделителями запятыми.</span><span class="sxs-lookup"><span data-stu-id="72064-160">You can provide input commands by specifying hello optional `Commands` element with a comma-delimited set of commands toorun inside hello container.</span></span>

> [!NOTE]
> <span data-ttu-id="72064-161">Если изображение hello не имеет рабочей нагрузки — точек входа, то вы должны tooexplicitly укажите ввода команды внутри `Commands` элемента с набором команд toorun внутри hello контейнер, который будет хранить hello контейнера, запущенного с разделителями запятыми При запуске.</span><span class="sxs-lookup"><span data-stu-id="72064-161">If hello image does not have a workload entry-point defined, then you need tooexplicitly specify input commands inside `Commands` element with a comma-delimited set of commands toorun inside hello container, which will keep hello container running after startup.</span></span>

## <a name="understand-resource-governance"></a><span data-ttu-id="72064-162">Концепция управления ресурсами</span><span class="sxs-lookup"><span data-stu-id="72064-162">Understand resource governance</span></span>
<span data-ttu-id="72064-163">Управление ресурсами — возможность hello контейнера, который ограничивает ресурсы hello, hello контейнера можно использовать на узле hello.</span><span class="sxs-lookup"><span data-stu-id="72064-163">Resource governance is a capability of hello container that restricts hello resources that hello container can use on hello host.</span></span> <span data-ttu-id="72064-164">Hello `ResourceGovernancePolicy`, что указывается в манифесте приложения hello являются ограничения ресурсов используется toodeclare для пакета кода службы.</span><span class="sxs-lookup"><span data-stu-id="72064-164">hello `ResourceGovernancePolicy`, which is specified in hello application manifest is used toodeclare resource limits for a service code package.</span></span> <span data-ttu-id="72064-165">Ограничения ресурсов можно задать для hello следующие ресурсы:</span><span class="sxs-lookup"><span data-stu-id="72064-165">Resource limits can be set for hello following resources:</span></span>

* <span data-ttu-id="72064-166">Память</span><span class="sxs-lookup"><span data-stu-id="72064-166">Memory</span></span>
* <span data-ttu-id="72064-167">MemorySwap;</span><span class="sxs-lookup"><span data-stu-id="72064-167">MemorySwap</span></span>
* <span data-ttu-id="72064-168">CpuShares;</span><span class="sxs-lookup"><span data-stu-id="72064-168">CpuShares (CPU relative weight)</span></span>
* <span data-ttu-id="72064-169">MemoryReservationInMB;</span><span class="sxs-lookup"><span data-stu-id="72064-169">MemoryReservationInMB</span></span>  
* <span data-ttu-id="72064-170">BlkioWeight.</span><span class="sxs-lookup"><span data-stu-id="72064-170">BlkioWeight (BlockIO relative weight).</span></span>

> [!NOTE]
> <span data-ttu-id="72064-171">В будущих выпусках будет добавлена поддержка ограничений на определенные параметры блочного ввода-вывода, включая число операций ввода-вывода, скорость чтения-записи и т. п.</span><span class="sxs-lookup"><span data-stu-id="72064-171">In a future release, support for specifying specific block IO limits such as IOPs, read/write BPS, and others will be included.</span></span>
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

## <a name="authenticate-a-repository"></a><span data-ttu-id="72064-172">Проверка подлинности в репозитории</span><span class="sxs-lookup"><span data-stu-id="72064-172">Authenticate a repository</span></span>
<span data-ttu-id="72064-173">toodownload контейнера, возможно, репозиторий контейнера toohello tooprovide учетных данных для входа.</span><span class="sxs-lookup"><span data-stu-id="72064-173">toodownload a container, you might have tooprovide sign-in credentials toohello container repository.</span></span> <span data-ttu-id="72064-174">Hello учетных данных для входа, указанный в манифесте приложения hello, являются hello используется toospecify входа в систему или ключа SSH, загрузки образа контейнера hello из репозитория образов hello.</span><span class="sxs-lookup"><span data-stu-id="72064-174">hello sign-in credentials, specified in hello application manifest, are used toospecify hello sign-in information, or SSH key, for downloading hello container image from hello image repository.</span></span> <span data-ttu-id="72064-175">Hello пример учетной записи называется *TestUser* вместе с hello пароль в виде открытого текста (*не* рекомендуется):</span><span class="sxs-lookup"><span data-stu-id="72064-175">hello following example shows an account called *TestUser* along with hello password in clear text (*not* recommended):</span></span>

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

<span data-ttu-id="72064-176">Рекомендуется шифровать hello пароль, с помощью сертификата, где развернуты toohello машины.</span><span class="sxs-lookup"><span data-stu-id="72064-176">We recommend that you encrypt hello password by using a certificate that's deployed toohello machine.</span></span>

<span data-ttu-id="72064-177">Hello пример учетной записи называется *TestUser*, где hello пароль был зашифрован с помощью сертификата с именем *MyCert*.</span><span class="sxs-lookup"><span data-stu-id="72064-177">hello following example shows an account called *TestUser*, where hello password was encrypted by using a certificate called *MyCert*.</span></span> <span data-ttu-id="72064-178">Можно использовать hello `Invoke-ServiceFabricEncryptText` PowerShell команды toocreate hello секретный зашифрованного текста hello пароль.</span><span class="sxs-lookup"><span data-stu-id="72064-178">You can use hello `Invoke-ServiceFabricEncryptText` PowerShell command toocreate hello secret cipher text for hello password.</span></span> <span data-ttu-id="72064-179">Дополнительные сведения см. в статье hello [управление секретные данные в приложения Service Fabric](service-fabric-application-secret-management.md).</span><span class="sxs-lookup"><span data-stu-id="72064-179">For more information, see hello article [Managing secrets in Service Fabric applications](service-fabric-application-secret-management.md).</span></span>

<span data-ttu-id="72064-180">закрытый ключ Hello hello сертификата, который использован toodecrypt hello пароль должен быть развернутой toohello локального компьютера в методе по каналу.</span><span class="sxs-lookup"><span data-stu-id="72064-180">hello private key of hello certificate that's used toodecrypt hello password must be deployed toohello local machine in an out-of-band method.</span></span> <span data-ttu-id="72064-181">(В Azure для этого используется Azure Resource Manager.) Затем когда Service Fabric развертывает пакет toohello hello службы компьютера, может расшифровать секретный hello.</span><span class="sxs-lookup"><span data-stu-id="72064-181">(In Azure, this method is Azure Resource Manager.) Then, when Service Fabric deploys hello service package toohello machine, it can decrypt hello secret.</span></span> <span data-ttu-id="72064-182">С помощью секрет hello вместе с именем учетной записи hello, он может затем выполнить проверку подлинности hello репозиторий контейнера.</span><span class="sxs-lookup"><span data-stu-id="72064-182">By using hello secret along with hello account name, it can then authenticate with hello container repository.</span></span>

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

## <a name="configure-container-port-to-host-port-mapping"></a><span data-ttu-id="72064-183">Настройка сопоставления порта контейнера с портом узла</span><span class="sxs-lookup"><span data-stu-id="72064-183">Configure container port-to-host port mapping</span></span>
<span data-ttu-id="72064-184">Можно настроить порт, используемый узла toocommunicate с контейнером hello, указав `PortBinding` в манифесте приложения hello.</span><span class="sxs-lookup"><span data-stu-id="72064-184">You can configure a host port used toocommunicate with hello container by specifying a `PortBinding` in hello application manifest.</span></span> <span data-ttu-id="72064-185">Hello порт maps hello порт toowhich hello службы привязки ожидает передачи данных внутри hello контейнера tooa порту hello узла.</span><span class="sxs-lookup"><span data-stu-id="72064-185">hello port binding maps hello port toowhich hello service is listening inside hello container tooa port on hello host.</span></span>

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

## <a name="configure-container-to-container-discovery-and-communication"></a><span data-ttu-id="72064-186">Настройка межконтейнерного поиска и обмена данными</span><span class="sxs-lookup"><span data-stu-id="72064-186">Configure container-to-container discovery and communication</span></span>
<span data-ttu-id="72064-187">С помощью hello `PortBinding` политики, можно сопоставить tooan порт контейнера `Endpoint` в манифест службы hello.</span><span class="sxs-lookup"><span data-stu-id="72064-187">By using hello `PortBinding` policy, you can map a container port tooan `Endpoint` in hello service manifest.</span></span> <span data-ttu-id="72064-188">Здравствуйте, конечная точка `Endpoint1` можно указать фиксированный порт (например, порт 80).</span><span class="sxs-lookup"><span data-stu-id="72064-188">hello endpoint `Endpoint1` can specify a fixed port (for example, port 80).</span></span> <span data-ttu-id="72064-189">Она также может указывать порт не во всех в этом случае выбирается случайный порт из диапазона портов приложения hello кластера для вас.</span><span class="sxs-lookup"><span data-stu-id="72064-189">It can also specify no port at all, in which case a random port from hello cluster's application port range is chosen for you.</span></span>

<span data-ttu-id="72064-190">При указании конечной точки с помощью hello `Endpoint` тег в манифесте службы hello контейнера гостевой Service Fabric автоматически можно опубликовать toohello этой конечной точки службы именования.</span><span class="sxs-lookup"><span data-stu-id="72064-190">If you specify an endpoint, using hello `Endpoint` tag in hello service manifest of a guest container, Service Fabric can automatically publish this endpoint toohello Naming service.</span></span> <span data-ttu-id="72064-191">Другие службы, работающие в кластере hello таким образом может обнаруживать этого контейнера, с помощью запросов REST hello в разрешении.</span><span class="sxs-lookup"><span data-stu-id="72064-191">Other services that are running in hello cluster can thus discover this container using hello REST queries for resolving.</span></span>

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

<span data-ttu-id="72064-192">С помощью регистрации hello службы именования, можно легко сделать контейнера в связи в коде hello внутри контейнера с помощью hello [обратный прокси-сервер](service-fabric-reverseproxy.md).</span><span class="sxs-lookup"><span data-stu-id="72064-192">By registering with hello Naming service, you can easily do container-to-container communication in hello code within your container by using hello [reverse proxy](service-fabric-reverseproxy.md).</span></span> <span data-ttu-id="72064-193">Обмен данными выполняется путем предоставления hello обратного прокси-сервера HTTP-порт прослушивания и имени hello hello служб, которые требуется toocommunicate с в переменных среды.</span><span class="sxs-lookup"><span data-stu-id="72064-193">Communication is performed by providing hello reverse proxy http listening port and hello name of hello services that you want toocommunicate with as environment variables.</span></span> <span data-ttu-id="72064-194">Дополнительные сведения см. Далее раздел hello.</span><span class="sxs-lookup"><span data-stu-id="72064-194">For more information, see hello next section.</span></span>

## <a name="configure-and-set-environment-variables"></a><span data-ttu-id="72064-195">Настройка и установка переменных среды</span><span class="sxs-lookup"><span data-stu-id="72064-195">Configure and set environment variables</span></span>
<span data-ttu-id="72064-196">Переменные среды можно указать для каждого пакета кода в манифест службы hello, и для служб, развернутых в контейнерах или служб, развернутых как исполняемые файлы, гостевых ОС и процессов.</span><span class="sxs-lookup"><span data-stu-id="72064-196">Environment variables can be specified for each code package in hello service manifest, both for services that are deployed in containers or for services that are deployed as processes/guest executables.</span></span> <span data-ttu-id="72064-197">Эти значения переменных среды может быть переопределено специально в манифесте приложения hello или указано во время развертывания, как параметры приложения.</span><span class="sxs-lookup"><span data-stu-id="72064-197">These environment variable values can be overridden specifically in hello application manifest or specified during deployment as application parameters.</span></span>

<span data-ttu-id="72064-198">Hello следующий фрагмент XML манифеста службы показан пример того, как переменные среды toospecify для пакета кода:</span><span class="sxs-lookup"><span data-stu-id="72064-198">hello following service manifest XML snippet shows an example of how toospecify environment variables for a code package:</span></span>

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

<span data-ttu-id="72064-199">Эти переменные среды может быть переопределено на уровне манифеста приложения hello:</span><span class="sxs-lookup"><span data-stu-id="72064-199">These environment variables can be overridden at hello application manifest level:</span></span>

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <EnvironmentOverrides CodePackageRef="FrontendService.Code">
            <EnvironmentVariable Name="BackendServiceName" Value="[BackendSvc]"/>
            <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
        </EnvironmentOverrides>
    </ServiceManifestImport>
```

<span data-ttu-id="72064-200">В предыдущем примере hello, мы указали явное значение для hello `HttpGateway` переменной среды (19000), пока мы значение hello `BackendServiceName` параметр hello `[BackendSvc]` параметр приложения.</span><span class="sxs-lookup"><span data-stu-id="72064-200">In hello previous example, we specified an explicit value for hello `HttpGateway` environment variable (19000), while we set hello value for `BackendServiceName` parameter via hello `[BackendSvc]` application parameter.</span></span> <span data-ttu-id="72064-201">Эти параметры включают значение hello toospecify `BackendServiceName`значение при развертывании приложения hello и имеет фиксированное значение в манифесте hello.</span><span class="sxs-lookup"><span data-stu-id="72064-201">These settings enable you toospecify hello value for `BackendServiceName`value when you deploy hello application and not have a fixed value in hello manifest.</span></span>

## <a name="complete-examples-for-application-and-service-manifest"></a><span data-ttu-id="72064-202">Полные примеры манифестов для приложения и службы</span><span class="sxs-lookup"><span data-stu-id="72064-202">Complete examples for application and service manifest</span></span>

<span data-ttu-id="72064-203">Ниже приведен пример манифеста приложения.</span><span class="sxs-lookup"><span data-stu-id="72064-203">An example application manifest follows:</span></span>

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

<span data-ttu-id="72064-204">Далее приведен пример службы манифеста (указанных в предшествующих манифест приложения hello):</span><span class="sxs-lookup"><span data-stu-id="72064-204">An example service manifest (specified in hello preceding application manifest) follows:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="72064-205">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="72064-205">Next steps</span></span>
<span data-ttu-id="72064-206">Вы развернули контейнерного службы, узнаете, как toomanage его жизненного цикла, считывая [жизненный цикл приложений фабрики служб](service-fabric-application-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="72064-206">Now that you have deployed a containerized service, learn how toomanage its lifecycle by reading [Service Fabric application lifecycle](service-fabric-application-lifecycle.md).</span></span>

* [<span data-ttu-id="72064-207">Общие сведения о Service Fabric и контейнерах</span><span class="sxs-lookup"><span data-stu-id="72064-207">Overview of Service Fabric and containers</span></span>](service-fabric-containers-overview.md)
* [<span data-ttu-id="72064-208">Взаимодействие с кластерами Service Fabric, с помощью hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="72064-208">Interacting with Service Fabric clusters using hello Azure CLI</span></span>](service-fabric-azure-cli.md)

<!-- Images -->
[sf-yeoman]: ./media/service-fabric-deploy-container-linux/sf-container-yeoman1.png

## <a name="related-articles"></a><span data-ttu-id="72064-209">Связанные статьи</span><span class="sxs-lookup"><span data-stu-id="72064-209">Related articles</span></span>

* [<span data-ttu-id="72064-210">Service Fabric и Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="72064-210">Getting started with Service Fabric and Azure CLI 2.0</span></span>](service-fabric-azure-cli-2-0.md)
* [<span data-ttu-id="72064-211">Использование интерфейса командной строки Azure для взаимодействия с кластером Service Fabric</span><span class="sxs-lookup"><span data-stu-id="72064-211">Getting started with Service Fabric XPlat CLI</span></span>](service-fabric-azure-cli.md)
