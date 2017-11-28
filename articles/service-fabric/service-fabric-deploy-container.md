---
title: "Service Fabric и развертывание контейнеров | Документация Майкрософт"
description: "Service Fabric и использование контейнеров для развертывания приложений микрослужб. В этой статье рассмотрены возможности, которые платформа Service Fabric предоставляет для контейнеров. Также здесь описано развертывание образа контейнера Windows в кластере."
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
ms.openlocfilehash: 25d6b056421e71fa70ed20a39589f77dbbc25c69
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-a-windows-container-to-service-fabric"></a><span data-ttu-id="b62ab-104">Развертывание контейнера Windows в Service Fabric</span><span class="sxs-lookup"><span data-stu-id="b62ab-104">Deploy a Windows container to Service Fabric</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b62ab-105">Развертывание контейнера Windows</span><span class="sxs-lookup"><span data-stu-id="b62ab-105">Deploy Windows Container</span></span>](service-fabric-deploy-container.md)
> * [<span data-ttu-id="b62ab-106">Развертывание контейнера Docker</span><span class="sxs-lookup"><span data-stu-id="b62ab-106">Deploy Docker Container</span></span>](service-fabric-deploy-container-linux.md)
> 
> 

<span data-ttu-id="b62ab-107">В этой статье подробно рассматривается создание контейнерных служб в контейнерах Windows.</span><span class="sxs-lookup"><span data-stu-id="b62ab-107">This article walks you through the process of building containerized services in Windows containers.</span></span>

<span data-ttu-id="b62ab-108">В Service Fabric реализовано несколько возможностей для создания приложений, состоящих из микрослужб, выполняющихся в контейнерах.</span><span class="sxs-lookup"><span data-stu-id="b62ab-108">Service Fabric has several capabilities that help you with building applications that are composed of microservices running inside containers.</span></span> 

<span data-ttu-id="b62ab-109">и включают следующие возможности:</span><span class="sxs-lookup"><span data-stu-id="b62ab-109">The capabilities include:</span></span>

* <span data-ttu-id="b62ab-110">развертывание и активация образа контейнера;</span><span class="sxs-lookup"><span data-stu-id="b62ab-110">Container image deployment and activation</span></span>
* <span data-ttu-id="b62ab-111">управление ресурсами;</span><span class="sxs-lookup"><span data-stu-id="b62ab-111">Resource governance</span></span>
* <span data-ttu-id="b62ab-112">проверка подлинности репозитория;</span><span class="sxs-lookup"><span data-stu-id="b62ab-112">Repository authentication</span></span>
* <span data-ttu-id="b62ab-113">сопоставление порта контейнера с портом узла;</span><span class="sxs-lookup"><span data-stu-id="b62ab-113">Container port-to-host port mapping</span></span>
* <span data-ttu-id="b62ab-114">межконтейнерное обнаружение и взаимодействие;</span><span class="sxs-lookup"><span data-stu-id="b62ab-114">Container-to-container discovery and communication</span></span>
* <span data-ttu-id="b62ab-115">возможность настройки и установки переменных среды.</span><span class="sxs-lookup"><span data-stu-id="b62ab-115">Ability to configure and set environment variables</span></span>

<span data-ttu-id="b62ab-116">Давайте рассмотрим все эти возможности на примере упаковки контейнерной службы, которая будет включена в приложение.</span><span class="sxs-lookup"><span data-stu-id="b62ab-116">Let's look at how each of capabilities works when you're packaging a containerized service to be included in your application.</span></span>

## <a name="package-a-windows-container"></a><span data-ttu-id="b62ab-117">Упаковка контейнера Windows</span><span class="sxs-lookup"><span data-stu-id="b62ab-117">Package a Windows container</span></span>
<span data-ttu-id="b62ab-118">При упаковке контейнера вы можете использовать шаблон проекта Visual Studio или [создать пакет приложения вручную](#manually).</span><span class="sxs-lookup"><span data-stu-id="b62ab-118">When you package a container, you can choose to use either a Visual Studio project template or [create the application package manually](#manually).</span></span>  <span data-ttu-id="b62ab-119">Если вы используете Visual Studio, шаблон проекта создаст для вас структуру пакета приложения и файлы манифеста.</span><span class="sxs-lookup"><span data-stu-id="b62ab-119">When you use Visual Studio, the application package structure and manifest files are created by the New Project template for you.</span></span>

> [!TIP]
> <span data-ttu-id="b62ab-120">Упаковать имеющийся образ контейнера в службу проще всего с помощью Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b62ab-120">The easiest way to package an existing container image into a service is to use Visual Studio.</span></span>

## <a name="use-visual-studio-to-package-an-existing-container-image"></a><span data-ttu-id="b62ab-121">Упаковка существующего образа контейнера с помощью Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b62ab-121">Use Visual Studio to package an existing container image</span></span>
<span data-ttu-id="b62ab-122">Visual Studio предоставляет шаблон службы Service Fabric для развертывания контейнера файла в кластере Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b62ab-122">Visual Studio provides a Service Fabric service template to help you deploy a container to a Service Fabric cluster.</span></span>

1. <span data-ttu-id="b62ab-123">Чтобы создать приложение Service Fabric, выберите **Файл** > **Создать проект**.</span><span class="sxs-lookup"><span data-stu-id="b62ab-123">Choose **File** > **New Project**, and create a Service Fabric application.</span></span>
2. <span data-ttu-id="b62ab-124">Выберите **гостевой контейнер** в качестве шаблона службы.</span><span class="sxs-lookup"><span data-stu-id="b62ab-124">Choose **Guest Container** as the service template.</span></span>
3. <span data-ttu-id="b62ab-125">Выберите **имя образа** и укажите путь к образу в репозитории контейнера,</span><span class="sxs-lookup"><span data-stu-id="b62ab-125">Choose **Image Name** and provide the path to the image in your container repository.</span></span> <span data-ttu-id="b62ab-126">например `myrepo/myimage:v1` в https://hub.docker.com.</span><span class="sxs-lookup"><span data-stu-id="b62ab-126">For example, `myrepo/myimage:v1` in https://hub.docker.com</span></span>
4. <span data-ttu-id="b62ab-127">Присвойте службе имя и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="b62ab-127">Give your service a name, and click **OK**.</span></span>
5. <span data-ttu-id="b62ab-128">Если контейнерной службе нужна конечная точка для обмена данными, можно добавить значения протокола, порта и типа в файл ServiceManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="b62ab-128">If your containerized service needs an endpoint for communication, you can now add the protocol, port, and type to the ServiceManifest.xml file.</span></span> <span data-ttu-id="b62ab-129">Например:</span><span class="sxs-lookup"><span data-stu-id="b62ab-129">For example:</span></span> 
     
    `<Endpoint Name="MyContainerServiceEndpoint" Protocol="http" Port="80" UriScheme="http" PathSuffix="myapp/" Type="Input" />`
    
    <span data-ttu-id="b62ab-130">Если указать `UriScheme`, конечная точка контейнера будет автоматически зарегистрирована в службе именования Service Fabric, что улучшит ее поиск.</span><span class="sxs-lookup"><span data-stu-id="b62ab-130">By providing the `UriScheme`, Service Fabric automatically registers the container endpoint with the Naming service for discoverability.</span></span> <span data-ttu-id="b62ab-131">Порт может быть фиксированным (как показано в приведенном выше примере) или выделяться динамически.</span><span class="sxs-lookup"><span data-stu-id="b62ab-131">The port can either be fixed (as shown in the preceding example) or dynamically allocated.</span></span> <span data-ttu-id="b62ab-132">Если не указать порт, он динамически выделяется из диапазона портов приложения (как и в случае с любой службой).</span><span class="sxs-lookup"><span data-stu-id="b62ab-132">If you don't specify a port, it is dynamically allocated from the application port range (as would happen with any service).</span></span>
    <span data-ttu-id="b62ab-133">Кроме того, необходимо настроить сопоставление порта контейнера с портом узла, указав политику `PortBinding` в манифесте приложения.</span><span class="sxs-lookup"><span data-stu-id="b62ab-133">You also need to configure the container to host port mapping by specifying a `PortBinding` policy in the application manifest.</span></span> <span data-ttu-id="b62ab-134">Дополнительные сведения см. в разделе [Настройка сопоставления порта контейнера с портом узла](#Portsection).</span><span class="sxs-lookup"><span data-stu-id="b62ab-134">For more information, see [Configure container to host port mapping](#Portsection).</span></span>
6. <span data-ttu-id="b62ab-135">Если для контейнера требуется управление ресурсами, добавьте `ResourceGovernancePolicy`.</span><span class="sxs-lookup"><span data-stu-id="b62ab-135">If your container needs resource governance then add a `ResourceGovernancePolicy`.</span></span>
8. <span data-ttu-id="b62ab-136">Если для контейнера требуется проверка подлинности в частном репозитории, добавьте `RepositoryCredentials`.</span><span class="sxs-lookup"><span data-stu-id="b62ab-136">If your container needs to authenticate with a private repository, then add `RepositoryCredentials`.</span></span>
7. <span data-ttu-id="b62ab-137">Если используется компьютер Windows Server 2016 с активированной поддержкой контейнеров, вы можете использовать пакет и опубликовать действие, чтобы выполнить развертывание в локальном кластере.</span><span class="sxs-lookup"><span data-stu-id="b62ab-137">If you are running on a Windows Server 2016 machine with container support enabled, you can use the package and publish action to deploy to your local cluster.</span></span> 
8. <span data-ttu-id="b62ab-138">Когда все будет готово, можно опубликовать приложение на удаленном кластере или вернуть решение в систему управления версиями.</span><span class="sxs-lookup"><span data-stu-id="b62ab-138">When ready, you can publish the application to a remote cluster or check in the solution to source control.</span></span> 

<span data-ttu-id="b62ab-139">В качестве примера можно ознакомиться с [примерами кода контейнера Service Fabric на сайте GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers).</span><span class="sxs-lookup"><span data-stu-id="b62ab-139">For an example, checkout the [Service Fabric container code samples on GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)</span></span>

## <a name="creating-a-windows-server-2016-cluster"></a><span data-ttu-id="b62ab-140">Создание кластера Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="b62ab-140">Creating a Windows Server 2016 cluster</span></span>
<span data-ttu-id="b62ab-141">Чтобы развернуть контейнерное приложение, необходимо создать кластер под управлением Windows Server 2016 с поддержкой контейнеров.</span><span class="sxs-lookup"><span data-stu-id="b62ab-141">To deploy your containerized application, you need to create a cluster running Windows Server 2016 with container support enabled.</span></span> <span data-ttu-id="b62ab-142">Кластер может выполняться локально или быть развернут с использованием Azure Resource Manager в Azure.</span><span class="sxs-lookup"><span data-stu-id="b62ab-142">Your cluster may be running locally, or deployed via Azure Resource Manager in Azure.</span></span> 

<span data-ttu-id="b62ab-143">Чтобы развернуть кластер с помощью Azure Resource Manager, выберите вариант образа **Windows Server 2016 with Containers** (Windows Server 2016 с контейнерами) в Azure.</span><span class="sxs-lookup"><span data-stu-id="b62ab-143">To deploy a cluster using Azure Resource Manager, choose the **Windows Server 2016 with Containers** image option in Azure.</span></span> <span data-ttu-id="b62ab-144">Ознакомьтесь со статьей [Создание кластера Service Fabric в Azure с помощью Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span><span class="sxs-lookup"><span data-stu-id="b62ab-144">See the article [Create a Service Fabric cluster by using Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span></span> <span data-ttu-id="b62ab-145">Используйте приведенные ниже параметры Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b62ab-145">Ensure that you use the following Azure Resource Manager settings:</span></span>

```xml
"vmImageOffer": { "type": "string","defaultValue": "WindowsServer"     },
"vmImageSku": { "defaultValue": "2016-Datacenter-with-Containers","type": "string"     },
"vmImageVersion": { "defaultValue": "latest","type": "string"     },  
```
<span data-ttu-id="b62ab-146">Для создания кластера можно также использовать [шаблон Azure Resource Manager кластера с 5 узлами](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype).</span><span class="sxs-lookup"><span data-stu-id="b62ab-146">You can also use the [Five Node Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype) to create a cluster.</span></span> <span data-ttu-id="b62ab-147">Кроме того, можно прочитать [записи блога сообщества](https://loekd.blogspot.com/2017/01/running-windows-containers-on-azure.html) об использовании Service Fabric и контейнеров Windows.</span><span class="sxs-lookup"><span data-stu-id="b62ab-147">Alternatively read a community [blog post](https://loekd.blogspot.com/2017/01/running-windows-containers-on-azure.html) on using Service Fabric and Windows containers.</span></span>

<a id="manually"></a>

## <a name="manually-package-and-deploy-a-container-image"></a><span data-ttu-id="b62ab-148">Упаковка и развертывание образа контейнера вручную</span><span class="sxs-lookup"><span data-stu-id="b62ab-148">Manually package and deploy a container image</span></span>
<span data-ttu-id="b62ab-149">Упаковка контейнерной службы вручную включает следующие этапы.</span><span class="sxs-lookup"><span data-stu-id="b62ab-149">The process of manually packaging a containerized service is based on the following steps:</span></span>

1. <span data-ttu-id="b62ab-150">Публикация контейнеров в репозиторий.</span><span class="sxs-lookup"><span data-stu-id="b62ab-150">Publish the containers to your repository.</span></span>
2. <span data-ttu-id="b62ab-151">Создание структуры каталогов пакета.</span><span class="sxs-lookup"><span data-stu-id="b62ab-151">Create the package directory structure.</span></span>
3. <span data-ttu-id="b62ab-152">Редактирование файла манифеста службы.</span><span class="sxs-lookup"><span data-stu-id="b62ab-152">Edit the service manifest file.</span></span>
4. <span data-ttu-id="b62ab-153">Редактирование файла манифеста приложения.</span><span class="sxs-lookup"><span data-stu-id="b62ab-153">Edit the application manifest file.</span></span>

## <a name="deploy-and-activate-a-container-image"></a><span data-ttu-id="b62ab-154">Развертывание и активация образа контейнера</span><span class="sxs-lookup"><span data-stu-id="b62ab-154">Deploy and activate a container image</span></span>
<span data-ttu-id="b62ab-155">В [модели приложения](service-fabric-application-model.md)Service Fabric контейнер представляет собой узел приложения, в котором размещается несколько реплик службы.</span><span class="sxs-lookup"><span data-stu-id="b62ab-155">In the Service Fabric [application model](service-fabric-application-model.md), a container represents an application host in which multiple service replicas are placed.</span></span> <span data-ttu-id="b62ab-156">Чтобы развернуть и активировать контейнер, вставьте имя образа контейнера в элемент `ContainerHost` в манифесте служб.</span><span class="sxs-lookup"><span data-stu-id="b62ab-156">To deploy and activate a container, put the name of the container image into a `ContainerHost` element in the service manifest.</span></span>

<span data-ttu-id="b62ab-157">Добавьте в манифест службы элемент `ContainerHost` для точки входа.</span><span class="sxs-lookup"><span data-stu-id="b62ab-157">In the service manifest, add a `ContainerHost` for the entry point.</span></span> <span data-ttu-id="b62ab-158">Затем установите `ImageName` в качестве имени репозитория и образа контейнера.</span><span class="sxs-lookup"><span data-stu-id="b62ab-158">Then set the `ImageName` to be the name of the container repository and image.</span></span> <span data-ttu-id="b62ab-159">Следующий фрагмент манифеста содержит пример развертывания контейнера с именем `myimage:v1` из репозитория с именем `myrepo`.</span><span class="sxs-lookup"><span data-stu-id="b62ab-159">The following partial manifest shows an example of how to deploy the container called `myimage:v1` from a repository called `myrepo`:</span></span>

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

<span data-ttu-id="b62ab-160">Вы можете указать в элементе `Commands` необязательные команды, которые будут выполняться при запуске контейнера.</span><span class="sxs-lookup"><span data-stu-id="b62ab-160">You can specify optional commands to run upon starting the container under the `Commands` element.</span></span> <span data-ttu-id="b62ab-161">Команды нужно разделить запятыми.</span><span class="sxs-lookup"><span data-stu-id="b62ab-161">For multiple commands, comma-delimit them.</span></span> 

## <a name="understand-resource-governance"></a><span data-ttu-id="b62ab-162">Концепция управления ресурсами</span><span class="sxs-lookup"><span data-stu-id="b62ab-162">Understand resource governance</span></span>
<span data-ttu-id="b62ab-163">Управление ресурсами подразумевает, что вы можете определять ресурсы, которые контейнер может использовать на узле.</span><span class="sxs-lookup"><span data-stu-id="b62ab-163">Resource governance is a capability of the container that restricts the resources that the container can use on the host.</span></span> <span data-ttu-id="b62ab-164">Параметр `ResourceGovernancePolicy`, определяемый в манифесте приложения, позволяет объявить ограничения для ресурсов, доступных из пакета кода службы.</span><span class="sxs-lookup"><span data-stu-id="b62ab-164">The `ResourceGovernancePolicy`, which is specified in the application manifest is used to declare resource limits for a service code package.</span></span> <span data-ttu-id="b62ab-165">Ограничения ресурсов можно задать для следующих ресурсов:</span><span class="sxs-lookup"><span data-stu-id="b62ab-165">Resource limits can be set for the following resources:</span></span>

* <span data-ttu-id="b62ab-166">Память</span><span class="sxs-lookup"><span data-stu-id="b62ab-166">Memory</span></span>
* <span data-ttu-id="b62ab-167">MemorySwap;</span><span class="sxs-lookup"><span data-stu-id="b62ab-167">MemorySwap</span></span>
* <span data-ttu-id="b62ab-168">CpuShares;</span><span class="sxs-lookup"><span data-stu-id="b62ab-168">CpuShares (CPU relative weight)</span></span>
* <span data-ttu-id="b62ab-169">MemoryReservationInMB;</span><span class="sxs-lookup"><span data-stu-id="b62ab-169">MemoryReservationInMB</span></span>  
* <span data-ttu-id="b62ab-170">BlkioWeight.</span><span class="sxs-lookup"><span data-stu-id="b62ab-170">BlkioWeight (BlockIO relative weight).</span></span>

> [!NOTE]
> <span data-ttu-id="b62ab-171">Поддержка ограничений на определенные параметры блочного ввода-вывода, включая число операций ввода-вывода, скорость чтения-записи и т. п., планируется в будущих выпусках.</span><span class="sxs-lookup"><span data-stu-id="b62ab-171">Support for specifying specific block IO limits such as IOPs, read/write BPS, and others are planned for a future release.</span></span>
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

## <a name="authenticate-a-repository"></a><span data-ttu-id="b62ab-172">Проверка подлинности в репозитории</span><span class="sxs-lookup"><span data-stu-id="b62ab-172">Authenticate a repository</span></span>
<span data-ttu-id="b62ab-173">Для скачивания контейнера вам могут понадобится учетные данные для входа в репозиторий контейнера.</span><span class="sxs-lookup"><span data-stu-id="b62ab-173">To download a container, you might have to provide sign-in credentials to the container repository.</span></span> <span data-ttu-id="b62ab-174">Учетные данные для входа, указанные в манифесте приложения, определяют имя и пароль для входа (или ключ SSH). Они нужны для скачивания образа контейнера из репозитория образов.</span><span class="sxs-lookup"><span data-stu-id="b62ab-174">The sign-in credentials, specified in the application manifest, are used to specify the sign-in information, or SSH key, for downloading the container image from the image repository.</span></span> <span data-ttu-id="b62ab-175">В следующем примере представлена учетная запись с именем *TestUser* и паролем в виде открытого текста (такая практика *не рекомендуется*).</span><span class="sxs-lookup"><span data-stu-id="b62ab-175">The following example shows an account called *TestUser* along with the password in clear text (*not* recommended):</span></span>

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

<span data-ttu-id="b62ab-176">Мы советуем шифровать пароль с использованием сертификата, развернутого на компьютере.</span><span class="sxs-lookup"><span data-stu-id="b62ab-176">We recommend that you encrypt the password by using a certificate that's deployed to the machine.</span></span>

<span data-ttu-id="b62ab-177">В следующем примере представлена учетная запись с именем *TestUser* и паролем, зашифрованным с помощью сертификата с именем *MyCert*.</span><span class="sxs-lookup"><span data-stu-id="b62ab-177">The following example shows an account called *TestUser*, where the password was encrypted by using a certificate called *MyCert*.</span></span> <span data-ttu-id="b62ab-178">Можно использовать команду PowerShell `Invoke-ServiceFabricEncryptText` для создания секретного текста зашифрованного пароля.</span><span class="sxs-lookup"><span data-stu-id="b62ab-178">You can use the `Invoke-ServiceFabricEncryptText` PowerShell command to create the secret cipher text for the password.</span></span> <span data-ttu-id="b62ab-179">Этот процесс описан в статье [Управление секретами в приложениях Service Fabric](service-fabric-application-secret-management.md).</span><span class="sxs-lookup"><span data-stu-id="b62ab-179">For more information, see the article [Managing secrets in Service Fabric applications](service-fabric-application-secret-management.md).</span></span>

<span data-ttu-id="b62ab-180">На локальном компьютере следует развернуть закрытый ключ сертификата, который позволит расшифровывать на нем пароль, с использованием внешних средств.</span><span class="sxs-lookup"><span data-stu-id="b62ab-180">The private key of the certificate that's used to decrypt the password must be deployed to the local machine in an out-of-band method.</span></span> <span data-ttu-id="b62ab-181">(В Azure для этого используется Azure Resource Manager.) Когда Service Fabric развернет на компьютере пакет службы, секретный код можно будет расшифровать,</span><span class="sxs-lookup"><span data-stu-id="b62ab-181">(In Azure, this method is Azure Resource Manager.) Then, when Service Fabric deploys the service package to the machine, it can decrypt the secret.</span></span> <span data-ttu-id="b62ab-182">а затем выполнить проверку подлинности в репозитории контейнера, используя этот секрет и имя учетной записи.</span><span class="sxs-lookup"><span data-stu-id="b62ab-182">By using the secret along with the account name, it can then authenticate with the container repository.</span></span>

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

## <span data-ttu-id="b62ab-183"><a name ="Portsection"></a> Настройка сопоставления порта контейнера с портом узла</span><span class="sxs-lookup"><span data-stu-id="b62ab-183"><a name ="Portsection"></a> Configure container to host port mapping</span></span>
<span data-ttu-id="b62ab-184">С помощью политики `PortBinding` в манифесте приложения можно указать порт узла, который будет использоваться для обмена данными с контейнером.</span><span class="sxs-lookup"><span data-stu-id="b62ab-184">You can configure a host port used to communicate with the container by specifying a `PortBinding` in the application manifest.</span></span> <span data-ttu-id="b62ab-185">Это сопоставление связывает порт, который прослушивает служба в контейнере, с портом на узле.</span><span class="sxs-lookup"><span data-stu-id="b62ab-185">The port binding maps the port to which the service is listening inside the container to a port on the host.</span></span>

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

## <a name="configure-container-to-container-discovery-and-communication"></a><span data-ttu-id="b62ab-186">Настройка межконтейнерного поиска и обмена данными</span><span class="sxs-lookup"><span data-stu-id="b62ab-186">Configure container-to-container discovery and communication</span></span>
<span data-ttu-id="b62ab-187">Используйте элемент `PortBinding` для сопоставления порта контейнера с конечной точкой в манифесте службы.</span><span class="sxs-lookup"><span data-stu-id="b62ab-187">You can use the `PortBinding` element to map a container port to an endpoint in the service manifest.</span></span> <span data-ttu-id="b62ab-188">В указанном ниже примере конечная точка `Endpoint1` указывает фиксированный порт 8905.</span><span class="sxs-lookup"><span data-stu-id="b62ab-188">In the following example, the endpoint `Endpoint1` specifies a fixed port, 8905.</span></span> <span data-ttu-id="b62ab-189">Если не указать здесь номер порта, будет автоматически выбран случайный порт из диапазона портов для приложений кластера.</span><span class="sxs-lookup"><span data-stu-id="b62ab-189">It can also specify no port at all, in which case a random port from the cluster's application port range is chosen for you.</span></span>


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
<span data-ttu-id="b62ab-190">Если указать конечную точку с помощью тега `Endpoint` в манифесте службы для гостевого контейнера, Service Fabric может автоматически опубликовать эту конечную точку в службе именования.</span><span class="sxs-lookup"><span data-stu-id="b62ab-190">If you specify an endpoint, using the `Endpoint` tag in the service manifest of a guest container, Service Fabric can automatically publish this endpoint to the Naming service.</span></span> <span data-ttu-id="b62ab-191">Это позволит другим службам, которые выполняются в кластере, находить этот контейнер с помощью запросов REST.</span><span class="sxs-lookup"><span data-stu-id="b62ab-191">Other services that are running in the cluster can thus discover this container using the REST queries for resolving.</span></span>

<span data-ttu-id="b62ab-192">Зарегистрировав контейнер в службе именования, вы выполните обмен данными между контейнерами в своем контейнере, используя [обратный прокси-сервер](service-fabric-reverseproxy.md).</span><span class="sxs-lookup"><span data-stu-id="b62ab-192">By registering with the Naming service, you can perform container-to-container communication within your container by using the [reverse proxy](service-fabric-reverseproxy.md).</span></span> <span data-ttu-id="b62ab-193">Для этого достаточно указать в переменных среды http-порт прослушивания обратного прокси-сервера и имена служб, с которыми будет выполняться обмен данными.</span><span class="sxs-lookup"><span data-stu-id="b62ab-193">Communication is performed by providing the reverse proxy http listening port and the name of the services that you want to communicate with as environment variables.</span></span> <span data-ttu-id="b62ab-194">Этот процесс описан в следующем разделе.</span><span class="sxs-lookup"><span data-stu-id="b62ab-194">For more information, see the next section.</span></span> 

## <a name="configure-and-set-environment-variables"></a><span data-ttu-id="b62ab-195">Настройка и установка переменных среды</span><span class="sxs-lookup"><span data-stu-id="b62ab-195">Configure and set environment variables</span></span>
<span data-ttu-id="b62ab-196">Переменные среды можно указать для каждого пакета кода в манифесте служб.</span><span class="sxs-lookup"><span data-stu-id="b62ab-196">Environment variables can be specified for each code package in the service manifest.</span></span> <span data-ttu-id="b62ab-197">Эта функция доступна для всех служб, вне зависимости от того, как они развернуты: в качестве контейнеров, процессов или гостевых исполняемых файлов.</span><span class="sxs-lookup"><span data-stu-id="b62ab-197">This feature is available for all services irrespective of whether they are deployed as containers or processes or guest executables.</span></span> <span data-ttu-id="b62ab-198">Вы можете переопределить значения переменных среды в манифесте приложения или указать их в качестве параметров приложения во время развертывания.</span><span class="sxs-lookup"><span data-stu-id="b62ab-198">You can override environment variable values in the application manifest or specify them during deployment as application parameters.</span></span>

<span data-ttu-id="b62ab-199">Следующий фрагмент XML-кода из манифеста службы демонстрирует, как определить переменные среды для пакета кода.</span><span class="sxs-lookup"><span data-stu-id="b62ab-199">The following service manifest XML snippet shows an example of how to specify environment variables for a code package:</span></span>

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

<span data-ttu-id="b62ab-200">Эти переменные среды можно переопределить на уровне манифеста приложения:</span><span class="sxs-lookup"><span data-stu-id="b62ab-200">These environment variables can be overridden at the application manifest level:</span></span>

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <EnvironmentOverrides CodePackageRef="FrontendService.Code">
            <EnvironmentVariable Name="BackendServiceName" Value="[BackendSvc]"/>
            <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
        </EnvironmentOverrides>
    </ServiceManifestImport>
```

<span data-ttu-id="b62ab-201">В приведенном выше примере мы указали явное значение (19000) для переменной среды `HttpGateway`. Значение для параметра `BackendServiceName` мы указали с помощью параметра приложения `[BackendSvc]`.</span><span class="sxs-lookup"><span data-stu-id="b62ab-201">In the previous example, we specified an explicit value for the `HttpGateway` environment variable (19000), while we set the value for `BackendServiceName` parameter via the `[BackendSvc]` application parameter.</span></span> <span data-ttu-id="b62ab-202">Так мы можем указать значение для `BackendServiceName` при развертывании приложения, а не использовать фиксированное значение в манифесте.</span><span class="sxs-lookup"><span data-stu-id="b62ab-202">These settings enable you to specify the value for `BackendServiceName`value when you deploy the application and not have a fixed value in the manifest.</span></span>

## <a name="configure-isolation-mode"></a><span data-ttu-id="b62ab-203">Настройка режима изоляции</span><span class="sxs-lookup"><span data-stu-id="b62ab-203">Configure isolation mode</span></span>

<span data-ttu-id="b62ab-204">Windows поддерживает два режима изоляции для контейнеров: режим изоляции процессов и Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="b62ab-204">Windows supports two isolation modes for containers - process and Hyper-V.</span></span>  <span data-ttu-id="b62ab-205">В режиме изоляции процесса все контейнеры, запущенные на одном хост-компьютере, совместно используют ядро и узел.</span><span class="sxs-lookup"><span data-stu-id="b62ab-205">With the process isolation mode, all the containers running on the same host machine share the kernel with the host.</span></span> <span data-ttu-id="b62ab-206">В режиме изоляции Hyper-V все контейнеры Hyper-V и узлы контейнера используют отдельные ядра.</span><span class="sxs-lookup"><span data-stu-id="b62ab-206">With the Hyper-V isolation mode, the kernels are isolated between each Hyper-V container and the container host.</span></span> <span data-ttu-id="b62ab-207">Режим изоляции указывается в теге `ContainerHostPolicies` в файле манифеста приложения.</span><span class="sxs-lookup"><span data-stu-id="b62ab-207">The isolation mode is specified in the `ContainerHostPolicies` tag in the application manifest file.</span></span>  <span data-ttu-id="b62ab-208">Вы можете указать следующие режимы изоляции: `process`, `hyperv` и `default`.</span><span class="sxs-lookup"><span data-stu-id="b62ab-208">The isolation modes that can be specified are `process`, `hyperv`, and `default`.</span></span> <span data-ttu-id="b62ab-209">Режим изоляции `default` на узлах Windows Server по умолчанию имеет значение `process`, а на узлах Windows 10 значение `hyperv`.</span><span class="sxs-lookup"><span data-stu-id="b62ab-209">The `default` isolation mode defaults to `process` on Windows Server hosts, and defaults to `hyperv` on Windows 10 hosts.</span></span>  <span data-ttu-id="b62ab-210">В указанном ниже фрагменте кода показано, как режим изоляции указывается в файле манифеста приложения.</span><span class="sxs-lookup"><span data-stu-id="b62ab-210">The following snippet shows how the isolation mode is specified in the application manifest file.</span></span>

```xml
   <ContainerHostPolicies CodePackageRef="NodeService.Code" Isolation="hyperv">
```


## <a name="complete-examples-for-application-and-service-manifest"></a><span data-ttu-id="b62ab-211">Полные примеры манифестов для приложения и службы</span><span class="sxs-lookup"><span data-stu-id="b62ab-211">Complete examples for application and service manifest</span></span>

<span data-ttu-id="b62ab-212">Ниже приведен пример манифеста приложения.</span><span class="sxs-lookup"><span data-stu-id="b62ab-212">An example application manifest follows:</span></span>

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

<span data-ttu-id="b62ab-213">А вот пример манифеста службы (указывается в предложенном выше манифесте приложения).</span><span class="sxs-lookup"><span data-stu-id="b62ab-213">An example service manifest (specified in the preceding application manifest) follows:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="b62ab-214">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b62ab-214">Next steps</span></span>
<span data-ttu-id="b62ab-215">Теперь, когда вы успешно развернули контейнерную службу, изучите рекомендации по управлению ее жизненным циклом в статье [Жизненный цикл приложения Service Fabric](service-fabric-application-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="b62ab-215">Now that you have deployed a containerized service, learn how to manage its lifecycle by reading [Service Fabric application lifecycle](service-fabric-application-lifecycle.md).</span></span>

* [<span data-ttu-id="b62ab-216">Общие сведения о Service Fabric и контейнерах</span><span class="sxs-lookup"><span data-stu-id="b62ab-216">Overview of Service Fabric and containers</span></span>](service-fabric-containers-overview.md)
* <span data-ttu-id="b62ab-217">В качестве примера можно ознакомиться с [примерами кода контейнера Service Fabric на сайте GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers).</span><span class="sxs-lookup"><span data-stu-id="b62ab-217">For an example, checkout [Service Fabric container code samples on GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)</span></span>
