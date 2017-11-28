---
title: "развертывание приложения Service Fabric aaaAzure | Документы Microsoft"
description: "Используйте API-интерфейсы FabricClient toodeploy hello и удаление приложений в Service Fabric."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: b120ffbf-f1e3-4b26-a492-347c29f8f66b
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/07/2017
ms.author: ryanwi
ms.openlocfilehash: b2986b71c461f3e785ba16ec1b827fe47ad852fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-remove-applications-using-fabricclient"></a><span data-ttu-id="571ec-103">Развертывание и удаление приложений с помощью FabricClient</span><span class="sxs-lookup"><span data-stu-id="571ec-103">Deploy and remove applications using FabricClient</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="571ec-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="571ec-104">PowerShell</span></span>](service-fabric-deploy-remove-applications.md)
> * [<span data-ttu-id="571ec-105">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="571ec-105">Visual Studio</span></span>](service-fabric-publish-app-remote-cluster.md)
> * [<span data-ttu-id="571ec-106">API-интерфейсы FabricClient</span><span class="sxs-lookup"><span data-stu-id="571ec-106">FabricClient APIs</span></span>](service-fabric-deploy-remove-applications-fabricclient.md)
> 
> 

<br/>

<span data-ttu-id="571ec-107">После [создания пакета приложения][10] его можно развернуть в кластере Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="571ec-107">Once an [application type has been packaged][10], it's ready for deployment into an Azure Service Fabric cluster.</span></span> <span data-ttu-id="571ec-108">Развертывание включает hello следующие три шага:</span><span class="sxs-lookup"><span data-stu-id="571ec-108">Deployment involves hello following three steps:</span></span>

1. <span data-ttu-id="571ec-109">Отправка хранилища образов toohello пакета приложения hello</span><span class="sxs-lookup"><span data-stu-id="571ec-109">Upload hello application package toohello image store</span></span>
2. <span data-ttu-id="571ec-110">Регистрация типа приложения hello</span><span class="sxs-lookup"><span data-stu-id="571ec-110">Register hello application type</span></span>
3. <span data-ttu-id="571ec-111">Создание экземпляра приложения hello</span><span class="sxs-lookup"><span data-stu-id="571ec-111">Create hello application instance</span></span>

<span data-ttu-id="571ec-112">После развертывания приложения и экземпляр работает в кластере hello, можно удалить экземпляр приложения hello и его тип приложения.</span><span class="sxs-lookup"><span data-stu-id="571ec-112">After an application is deployed and an instance is running in hello cluster, you can delete hello application instance and its application type.</span></span> <span data-ttu-id="571ec-113">Удаление toocompletely приложение из кластера hello включает в себя hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="571ec-113">toocompletely remove an application from hello cluster involves hello following steps:</span></span>

1. <span data-ttu-id="571ec-114">Удалить (или) запущен экземпляр приложения hello</span><span class="sxs-lookup"><span data-stu-id="571ec-114">Remove (or delete) hello running application instance</span></span>
2. <span data-ttu-id="571ec-115">Отмена регистрации типа приложения hello, если оно больше не требуется</span><span class="sxs-lookup"><span data-stu-id="571ec-115">Unregister hello application type if you no longer need it</span></span>
3. <span data-ttu-id="571ec-116">Удаление пакета приложения hello из хранилища образов hello</span><span class="sxs-lookup"><span data-stu-id="571ec-116">Remove hello application package from hello image store</span></span>

<span data-ttu-id="571ec-117">Если вы используете [Visual Studio для развертывания и отладки приложений](service-fabric-publish-app-remote-cluster.md) в кластере локальной разработки все hello описанные выше шаги автоматически обрабатываются с помощью сценария PowerShell.</span><span class="sxs-lookup"><span data-stu-id="571ec-117">If you use [Visual Studio for deploying and debugging applications](service-fabric-publish-app-remote-cluster.md) on your local development cluster, all hello preceding steps are handled automatically through a PowerShell script.</span></span>  <span data-ttu-id="571ec-118">Этот скрипт находится в hello *сценариев* папку проекта приложения hello.</span><span class="sxs-lookup"><span data-stu-id="571ec-118">This script is found in hello *Scripts* folder of hello application project.</span></span> <span data-ttu-id="571ec-119">В этой статье приведены фона действиями этот скрипт, чтобы можно было выполнять hello и те же операции вне Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="571ec-119">This article provides background on what that script is doing so that you can perform hello same operations outside of Visual Studio.</span></span> 
 
## <a name="connect-toohello-cluster"></a><span data-ttu-id="571ec-120">Подключите кластер toohello</span><span class="sxs-lookup"><span data-stu-id="571ec-120">Connect toohello cluster</span></span>
<span data-ttu-id="571ec-121">Подключите кластер toohello путем создания [FabricClient](/dotnet/api/system.fabric.fabricclient) экземпляра перед запуском любых hello примеры кода в этой статье.</span><span class="sxs-lookup"><span data-stu-id="571ec-121">Connect toohello cluster by creating a [FabricClient](/dotnet/api/system.fabric.fabricclient) instance before you run any of hello code examples in this article.</span></span> <span data-ttu-id="571ec-122">Примеры соединения tooa локальному кластеру разработки удаленного кластера или кластера, защищенные с помощью Azure Active Directory, X509 сертификаты или Windows Active Directory см. в разделе [кластера безопасное подключение tooa](service-fabric-connect-to-secure-cluster.md#connect-to-a-cluster-using-the-fabricclient-apis).</span><span class="sxs-lookup"><span data-stu-id="571ec-122">For examples of connecting tooa local development cluster or a remote cluster or cluster secured using Azure Active Directory, X509 certificates, or Windows Active Directory see [Connect tooa secure cluster](service-fabric-connect-to-secure-cluster.md#connect-to-a-cluster-using-the-fabricclient-apis).</span></span> <span data-ttu-id="571ec-123">tooconnect toohello локальному кластеру разработки, выполните hello ниже:</span><span class="sxs-lookup"><span data-stu-id="571ec-123">tooconnect toohello local development cluster, run hello following:</span></span>

```csharp
// Connect toohello local cluster.
FabricClient fabricClient = new FabricClient();
```

## <a name="upload-hello-application-package"></a><span data-ttu-id="571ec-124">Отправить пакет приложения hello</span><span class="sxs-lookup"><span data-stu-id="571ec-124">Upload hello application package</span></span>
<span data-ttu-id="571ec-125">Предположим, вы собрали и упаковали в Visual Studio приложение с именем *MyApplication*.</span><span class="sxs-lookup"><span data-stu-id="571ec-125">Suppose you build and package an application named *MyApplication* in Visual Studio.</span></span> <span data-ttu-id="571ec-126">По умолчанию имя типа приложения hello, перечисленные в hello ApplicationManifest.xml является «MyApplicationType».</span><span class="sxs-lookup"><span data-stu-id="571ec-126">By default, hello application type name listed in hello ApplicationManifest.xml is "MyApplicationType".</span></span>  <span data-ttu-id="571ec-127">Hello пакет приложения, который содержит манифест необходимые приложения hello, манифесты и пакеты кода/config/данные, находится в *C:\Users\&lt; имя_пользователя&gt;\Documents\Visual Studio 2017\Projects\ MyApplication\MyApplication\pkg\Debug*.</span><span class="sxs-lookup"><span data-stu-id="571ec-127">hello application package, which contains hello necessary application manifest, service manifests, and code/config/data packages, is located in *C:\Users\&lt;username&gt;\Documents\Visual Studio 2017\Projects\MyApplication\MyApplication\pkg\Debug*.</span></span>

<span data-ttu-id="571ec-128">Отправка пакета приложения hello помещает его в расположении, доступном из внутренних компонентов Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="571ec-128">Uploading hello application package puts it in a location that's accessible by hello internal Service Fabric components.</span></span> <span data-ttu-id="571ec-129">Service Fabric проверка пакета приложения hello во время регистрации hello пакета приложения hello.</span><span class="sxs-lookup"><span data-stu-id="571ec-129">Service Fabric verifies hello application package during hello registration of hello application package.</span></span> <span data-ttu-id="571ec-130">Тем не менее, пакет приложения hello tooverify локально (т. е. перед отправкой), используйте hello [ServiceFabricApplicationPackage тест](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) командлета.</span><span class="sxs-lookup"><span data-stu-id="571ec-130">However, if you want tooverify hello application package locally (i.e., before uploading), use hello [Test-ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="571ec-131">Hello [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) API передает хранилище образов кластера toohello пакета hello приложения.</span><span class="sxs-lookup"><span data-stu-id="571ec-131">hello [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) API uploads hello application package toohello cluster image store.</span></span> 

<span data-ttu-id="571ec-132">Если пакет приложения hello большой или имеет большое количество файлов, вы можете [Сжать](service-fabric-package-apps.md#compress-a-package) и скопируйте его в хранилище образов toohello с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="571ec-132">If hello application package is large and/or has many files, you can [compress it](service-fabric-package-apps.md#compress-a-package) and copy it toohello image store using PowerShell.</span></span> <span data-ttu-id="571ec-133">Hello сжатие приводит к уменьшению размера hello и hello количеством файлов.</span><span class="sxs-lookup"><span data-stu-id="571ec-133">hello compression reduces hello size and hello number of files.</span></span>

<span data-ttu-id="571ec-134">В разделе [понять строка подключения хранилища изображения hello](service-fabric-image-store-connection-string.md) Дополнительные сведения о хранилище образов hello и image хранение строки подключения.</span><span class="sxs-lookup"><span data-stu-id="571ec-134">See [Understand hello image store connection string](service-fabric-image-store-connection-string.md) for supplementary information about hello image store and image store connection string.</span></span>

## <a name="register-hello-application-package"></a><span data-ttu-id="571ec-135">Регистрация пакета приложения hello</span><span class="sxs-lookup"><span data-stu-id="571ec-135">Register hello application package</span></span>
<span data-ttu-id="571ec-136">Тип приложения Hello и версии, объявленные в манифесте приложения hello, становятся доступны для использования при регистрации пакета приложения hello.</span><span class="sxs-lookup"><span data-stu-id="571ec-136">hello application type and version declared in hello application manifest become available for use when hello application package is registered.</span></span> <span data-ttu-id="571ec-137">Hello система считывает переданный на предыдущем шаге hello пакет hello, проверяет пакет hello, обрабатывает содержимое пакета hello и копирует расположение внутреннего системного tooan hello обработки пакета.</span><span class="sxs-lookup"><span data-stu-id="571ec-137">hello system reads hello package uploaded in hello previous step, verifies hello package, processes hello package contents, and copies hello processed package tooan internal system location.</span></span>  

<span data-ttu-id="571ec-138">Hello [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) регистры API hello типа приложения в кластере hello и сделать его доступным для развертывания.</span><span class="sxs-lookup"><span data-stu-id="571ec-138">hello [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) API registers hello application type in hello cluster and make it available for deployment.</span></span>

<span data-ttu-id="571ec-139">Hello [GetApplicationTypeListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationtypelistasync) API предоставляет сведения обо всех типах успешно зарегистрированного приложения.</span><span class="sxs-lookup"><span data-stu-id="571ec-139">hello [GetApplicationTypeListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationtypelistasync) API provides information about all successfully registered application types.</span></span> <span data-ttu-id="571ec-140">Можно использовать этот API toodetermine после завершения регистрации hello.</span><span class="sxs-lookup"><span data-stu-id="571ec-140">You can use this API toodetermine when hello registration is done.</span></span>

## <a name="create-an-application-instance"></a><span data-ttu-id="571ec-141">Создание экземпляра приложения</span><span class="sxs-lookup"><span data-stu-id="571ec-141">Create an application instance</span></span>
<span data-ttu-id="571ec-142">Можно создать приложение на основе любого типа приложения успешно зарегистрирован с помощью hello [CreateApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.createapplicationasync) API.</span><span class="sxs-lookup"><span data-stu-id="571ec-142">You can instantiate an application from any application type that has been registered successfully by using hello [CreateApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.createapplicationasync) API.</span></span> <span data-ttu-id="571ec-143">Имя каждого приложения Hello должно начинаться с hello *«fabric:»* схему и должны быть уникальными для каждого экземпляра приложения (в пределах кластера).</span><span class="sxs-lookup"><span data-stu-id="571ec-143">hello name of each application must start with hello *"fabric:"* scheme and must be unique for each application instance (within a cluster).</span></span> <span data-ttu-id="571ec-144">Также создаются все службы по умолчанию, определенных в манифесте приложения hello объекта тип целевого приложения hello.</span><span class="sxs-lookup"><span data-stu-id="571ec-144">Any default services defined in hello application manifest of hello target application type are also created.</span></span>

<span data-ttu-id="571ec-145">Для каждой версии зарегистрированного типа приложения можно создать несколько экземпляров приложения.</span><span class="sxs-lookup"><span data-stu-id="571ec-145">Multiple application instances can be created for any given version of a registered application type.</span></span> <span data-ttu-id="571ec-146">Каждый экземпляр выполняется изолированно, используя собственный рабочий каталог и набор процессов.</span><span class="sxs-lookup"><span data-stu-id="571ec-146">Each application instance runs in isolation, with its own working directory and set of processes.</span></span>

<span data-ttu-id="571ec-147">toosee имени приложения и службы работают в кластере hello, запустите hello [GetApplicationListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationlistasync) и [GetServiceListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getservicelistasync) API-интерфейсы.</span><span class="sxs-lookup"><span data-stu-id="571ec-147">toosee which named applications and services are running in hello cluster, run hello [GetApplicationListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationlistasync) and [GetServiceListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getservicelistasync) APIs.</span></span>

## <a name="create-a-service-instance"></a><span data-ttu-id="571ec-148">Создание экземпляра службы</span><span class="sxs-lookup"><span data-stu-id="571ec-148">Create a service instance</span></span>
<span data-ttu-id="571ec-149">Можно создать экземпляр службы из типа службы с помощью hello [CreateServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) API.</span><span class="sxs-lookup"><span data-stu-id="571ec-149">You can instantiate a service from a service type using hello [CreateServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) API.</span></span>  <span data-ttu-id="571ec-150">Если служба hello объявляется как служба по умолчанию в манифесте приложения hello, hello службы создается при создании экземпляра приложения hello.</span><span class="sxs-lookup"><span data-stu-id="571ec-150">If hello service is declared as a default service in hello application manifest, hello service is instantiated when hello application is instantiated.</span></span>  <span data-ttu-id="571ec-151">Вызов hello [CreateServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) API для службы, экземпляр которого создается уже вернет исключение типа FabricException, содержащий код ошибки со значением FabricErrorCode.ServiceAlreadyExists.</span><span class="sxs-lookup"><span data-stu-id="571ec-151">Calling hello [CreateServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) API for a service that is already instantiated will return an exception of type FabricException containing an error code with a value of FabricErrorCode.ServiceAlreadyExists.</span></span>

## <a name="remove-a-service-instance"></a><span data-ttu-id="571ec-152">Удаление экземпляра службы</span><span class="sxs-lookup"><span data-stu-id="571ec-152">Remove a service instance</span></span>
<span data-ttu-id="571ec-153">Когда экземпляр службы больше не нужен, его можно удалить из hello запущен экземпляр приложения, вызывающего hello [DeleteServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.deleteserviceasync) API.</span><span class="sxs-lookup"><span data-stu-id="571ec-153">When a service instance is no longer needed, you can remove it from hello running application instance by calling hello [DeleteServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.deleteserviceasync) API.</span></span>  

> [!WARNING]
> <span data-ttu-id="571ec-154">Эта операция необратима, и вы не сможете восстановить состояние службы.</span><span class="sxs-lookup"><span data-stu-id="571ec-154">This operation cannot be reversed, and service state cannot be recovered.</span></span>

## <a name="remove-an-application-instance"></a><span data-ttu-id="571ec-155">Удаление экземпляра приложения</span><span class="sxs-lookup"><span data-stu-id="571ec-155">Remove an application instance</span></span>
<span data-ttu-id="571ec-156">При экземпляр приложения больше не нужен, можно окончательно удалить его по имени, используя hello [DeleteApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.deleteapplicationasync) API.</span><span class="sxs-lookup"><span data-stu-id="571ec-156">When an application instance is no longer needed, you can permanently remove it by name using hello [DeleteApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.deleteapplicationasync) API.</span></span> <span data-ttu-id="571ec-157">[DeleteApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.deleteapplicationasync) автоматически удаляет все службы, которые принадлежат toohello приложения также, без возможности восстановления, удаляя все состояния службы.</span><span class="sxs-lookup"><span data-stu-id="571ec-157">[DeleteApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.deleteapplicationasync) automatically removes all services that belong toohello application as well, permanently removing all service state.</span></span>

> [!WARNING]
> <span data-ttu-id="571ec-158">Эта операция необратима, и вы не сможете восстановить состояние приложения.</span><span class="sxs-lookup"><span data-stu-id="571ec-158">This operation cannot be reversed, and application state cannot be recovered.</span></span>

## <a name="unregister-an-application-type"></a><span data-ttu-id="571ec-159">Отмена регистрации типа приложения</span><span class="sxs-lookup"><span data-stu-id="571ec-159">Unregister an application type</span></span>
<span data-ttu-id="571ec-160">Когда определенной версии типа приложения не нужны, необходимо отменить регистрацию конкретную версию типа приложения hello, используя hello [Unregister ServiceFabricApplicationType](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.unprovisionapplicationasync) API.</span><span class="sxs-lookup"><span data-stu-id="571ec-160">When a particular version of an application type is no longer needed, you should unregister that particular version of hello application type using hello [Unregister-ServiceFabricApplicationType](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.unprovisionapplicationasync) API.</span></span> <span data-ttu-id="571ec-161">Отмена регистрации неиспользуемых версий приложения типы выпуски пространства, используемого хранилища образов hello.</span><span class="sxs-lookup"><span data-stu-id="571ec-161">Unregistering unused versions of application types releases storage space used by hello image store.</span></span> <span data-ttu-id="571ec-162">Версия типа приложения может быть отменена, при условии, что приложения не создаются для этой версии типа приложения hello и обновления нет ожидающих приложения ссылающиеся на этой версии типа приложения hello.</span><span class="sxs-lookup"><span data-stu-id="571ec-162">A version of an application type can be unregistered as long as no applications are instantiated against that version of hello application type and no pending application upgrades are referencing that version of hello application type.</span></span>

## <a name="remove-an-application-package-from-hello-image-store"></a><span data-ttu-id="571ec-163">Удаление пакета приложения из хранилища образов hello</span><span class="sxs-lookup"><span data-stu-id="571ec-163">Remove an application package from hello image store</span></span>
<span data-ttu-id="571ec-164">Если пакет приложения больше не нужен, его можно удалить из hello образа хранилища toofree системные ресурсы, с помощью hello [RemoveApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.removeapplicationpackage) API.</span><span class="sxs-lookup"><span data-stu-id="571ec-164">When an application package is no longer needed, you can delete it from hello image store toofree up system resources using hello [RemoveApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.removeapplicationpackage) API.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="571ec-165">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="571ec-165">Troubleshooting</span></span>
### <a name="copy-servicefabricapplicationpackage-asks-for-an-imagestoreconnectionstring"></a><span data-ttu-id="571ec-166">Команда Copy-ServiceFabricApplicationPackage запрашивает строку ImageStoreConnectionString</span><span class="sxs-lookup"><span data-stu-id="571ec-166">Copy-ServiceFabricApplicationPackage asks for an ImageStoreConnectionString</span></span>
<span data-ttu-id="571ec-167">пакет Service Fabric SDK среды Hello должна уже иметь hello правильно настроить значения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="571ec-167">hello Service Fabric SDK environment should already have hello correct defaults set up.</span></span> <span data-ttu-id="571ec-168">Но при необходимости hello строка ImageStoreConnectionString для всех команд должны соответствует значению hello, hello кластер Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="571ec-168">But if needed, hello ImageStoreConnectionString for all commands should match hello value that hello Service Fabric cluster is using.</span></span> <span data-ttu-id="571ec-169">Hello строка ImageStoreConnectionString можно найти в манифесте кластера hello, полученные при помощи hello [Get ServiceFabricClusterManifest](/powershell/module/servicefabric/get-servicefabricclustermanifest?view=azureservicefabricps) и Get-ImageStoreConnectionStringFromClusterManifest команды:</span><span class="sxs-lookup"><span data-stu-id="571ec-169">You can find hello ImageStoreConnectionString in hello cluster manifest, retrieved using hello [Get-ServiceFabricClusterManifest](/powershell/module/servicefabric/get-servicefabricclustermanifest?view=azureservicefabricps) and Get-ImageStoreConnectionStringFromClusterManifest commands:</span></span>

```powershell
PS C:\> Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest)
```

<span data-ttu-id="571ec-170">Hello **Get ImageStoreConnectionStringFromClusterManifest** , который является частью модуля Service Fabric SDK PowerShell hello, — используется tooget hello изображение хранение строки подключения.</span><span class="sxs-lookup"><span data-stu-id="571ec-170">hello **Get-ImageStoreConnectionStringFromClusterManifest** cmdlet, which is part of hello Service Fabric SDK PowerShell module, is used tooget hello image store connection string.</span></span>  <span data-ttu-id="571ec-171">hello SDK tooimport модуль, запустите:</span><span class="sxs-lookup"><span data-stu-id="571ec-171">tooimport hello SDK module, run:</span></span>

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```


<span data-ttu-id="571ec-172">Строка ImageStoreConnectionString Hello можно найти в манифесте кластера hello:</span><span class="sxs-lookup"><span data-stu-id="571ec-172">hello ImageStoreConnectionString is found in hello cluster manifest:</span></span>

```xml
<ClusterManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Name="Server-Default-SingleNode" Version="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">

    [...]

    <Section Name="Management">
      <Parameter Name="ImageStoreConnectionString" Value="file:D:\ServiceFabric\Data\ImageStore" />
    </Section>

    [...]
```

<span data-ttu-id="571ec-173">В разделе [понять строка подключения хранилища изображения hello](service-fabric-image-store-connection-string.md) Дополнительные сведения о хранилище образов hello и image хранение строки подключения.</span><span class="sxs-lookup"><span data-stu-id="571ec-173">See [Understand hello image store connection string](service-fabric-image-store-connection-string.md) for supplementary information about hello image store and image store connection string.</span></span>

### <a name="deploy-large-application-package"></a><span data-ttu-id="571ec-174">Развертывание пакета приложения большего размера</span><span class="sxs-lookup"><span data-stu-id="571ec-174">Deploy large application package</span></span>
<span data-ttu-id="571ec-175">Проблема. Время ожидания API [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) истекает для пакета большого приложения (несколько ГБ).</span><span class="sxs-lookup"><span data-stu-id="571ec-175">Issue: [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) API times out for a large application package (order of GB).</span></span>
<span data-ttu-id="571ec-176">Попробуйте выполнить следующее.</span><span class="sxs-lookup"><span data-stu-id="571ec-176">Try:</span></span>
- <span data-ttu-id="571ec-177">Задайте больше времени ожидания для метода [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) с помощью параметра `timeout`.</span><span class="sxs-lookup"><span data-stu-id="571ec-177">Specify a larger timeout for [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) method, with `timeout` parameter.</span></span> <span data-ttu-id="571ec-178">По умолчанию hello время ожидания составляет 30 минут.</span><span class="sxs-lookup"><span data-stu-id="571ec-178">By default, hello timeout is 30 minutes.</span></span>
- <span data-ttu-id="571ec-179">Проверьте hello сетевого подключения между исходным компьютером и кластера.</span><span class="sxs-lookup"><span data-stu-id="571ec-179">Check hello network connection between your source machine and cluster.</span></span> <span data-ttu-id="571ec-180">Если используется медленное подключение hello, рассмотрите возможность использования на машине для улучшения подключения к сети.</span><span class="sxs-lookup"><span data-stu-id="571ec-180">If hello connection is slow, consider using a machine with a better network connection.</span></span>
<span data-ttu-id="571ec-181">Если hello клиентский компьютер находится в другом регионе hello кластера, рекомендуется использовать клиентский компьютер в регионе, подробный или же hello кластера.</span><span class="sxs-lookup"><span data-stu-id="571ec-181">If hello client machine is in another region than hello cluster, consider using a client machine in a closer or same region as hello cluster.</span></span>
- <span data-ttu-id="571ec-182">Проверьте, достигнуто ли внешнее регулирование.</span><span class="sxs-lookup"><span data-stu-id="571ec-182">Check if you are hitting external throttling.</span></span> <span data-ttu-id="571ec-183">Например при хранилища azure настроенных toouse hello хранилища образов может регулирование передачи.</span><span class="sxs-lookup"><span data-stu-id="571ec-183">For example, when hello image store is configured toouse azure storage, upload may be throttled.</span></span>

<span data-ttu-id="571ec-184">Проблема. Отправка пакета завершена успешно, но время ожидания API [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) истекло. Попробуйте выполнить следующее.</span><span class="sxs-lookup"><span data-stu-id="571ec-184">Issue: Upload package completed successfully, but [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) API times out. Try:</span></span>
- <span data-ttu-id="571ec-185">[Сжатие пакета hello](service-fabric-package-apps.md#compress-a-package) перед копированием toohello хранилища образов.</span><span class="sxs-lookup"><span data-stu-id="571ec-185">[Compress hello package](service-fabric-package-apps.md#compress-a-package) before copying toohello image store.</span></span>
<span data-ttu-id="571ec-186">Hello Сжатие уменьшает размер hello и запускать hello число файлов, который в свою очередь, снижает объем трафика в hello и работать, Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="571ec-186">hello compression reduces hello size and hello number of files, which in turn reduces hello amount of traffic and work that Service Fabric must perform.</span></span> <span data-ttu-id="571ec-187">операции выгрузки Hello может требоваться (особенно при включении hello сжатия времени), однако скорости регистрации и отмены регистрации типа приложения hello.</span><span class="sxs-lookup"><span data-stu-id="571ec-187">hello upload operation may be slower (especially if you include hello compression time), but register and un-register hello application type are faster.</span></span>
- <span data-ttu-id="571ec-188">Задайте больше времени ожидания для API [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) с помощью параметра `timeout`.</span><span class="sxs-lookup"><span data-stu-id="571ec-188">Specify a larger timeout for [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) API with `timeout` parameter.</span></span>

### <a name="deploy-application-package-with-many-files"></a><span data-ttu-id="571ec-189">Развертывание пакета приложения с несколькими файлами</span><span class="sxs-lookup"><span data-stu-id="571ec-189">Deploy application package with many files</span></span>
<span data-ttu-id="571ec-190">Проблема. Время ожидания метода [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) для пакета приложения со множеством (несколько тысяч) файлов истекло.</span><span class="sxs-lookup"><span data-stu-id="571ec-190">Issue: [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) times out for an application package with many files (order of thousands).</span></span>
<span data-ttu-id="571ec-191">Попробуйте выполнить следующее.</span><span class="sxs-lookup"><span data-stu-id="571ec-191">Try:</span></span>
- <span data-ttu-id="571ec-192">[Сжатие пакета hello](service-fabric-package-apps.md#compress-a-package) перед копированием toohello хранилища образов.</span><span class="sxs-lookup"><span data-stu-id="571ec-192">[Compress hello package](service-fabric-package-apps.md#compress-a-package) before copying toohello image store.</span></span> <span data-ttu-id="571ec-193">Hello Сжатие уменьшает число hello файлов.</span><span class="sxs-lookup"><span data-stu-id="571ec-193">hello compression reduces hello number of files.</span></span>
- <span data-ttu-id="571ec-194">Задайте больше времени ожидания для метода [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) с помощью параметра `timeout`.</span><span class="sxs-lookup"><span data-stu-id="571ec-194">Specify a larger timeout for [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) with `timeout` parameter.</span></span>

## <a name="code-example"></a><span data-ttu-id="571ec-195">Примеры кода</span><span class="sxs-lookup"><span data-stu-id="571ec-195">Code example</span></span>
<span data-ttu-id="571ec-196">Hello следующий пример копирует образ хранилища toohello пакет приложений, подготавливает тип приложения hello, создает экземпляр приложения, создает экземпляр службы, удаляет hello экземпляр приложения, который подготавливает un тип приложения hello и Удаляет пакет приложения hello из хранилища образов hello.</span><span class="sxs-lookup"><span data-stu-id="571ec-196">hello following example copies an application package toohello image store, provisions hello application type, creates an application instance, creates a service instance, removes hello application instance, un-provisions hello application type, and deletes hello application package from hello image store.</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Reflection;
using System.Threading.Tasks;

using System.Fabric;
using System.Fabric.Description;
using System.Threading;

namespace ServiceFabricAppLifecycle
{
class Program
{
static void Main(string[] args)
{

    string clusterConnection = "localhost:19000";
    string appName = "fabric:/MyApplication";
    string appType = "MyApplicationType";
    string appVersion = "1.0.0";
    string serviceName = "fabric:/MyApplication/Stateless1";
    string imageStoreConnectionString = "file:C:\\SfDevCluster\\Data\\ImageStoreShare";
    string packagePathInImageStore = "MyApplication";
    string packagePath = "C:\\Users\\username\\Documents\\Visual Studio 2017\\Projects\\MyApplication\\MyApplication\\pkg\\Debug";
    string serviceType = "Stateless1Type";

    // Connect toohello cluster.
    FabricClient fabricClient = new FabricClient(clusterConnection);

    // Copy hello application package tooa location in hello image store
    try
    {
        fabricClient.ApplicationManager.CopyApplicationPackage(imageStoreConnectionString, packagePath, packagePathInImageStore);
        Console.WriteLine("Application package copied too{0}", packagePathInImageStore);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("Application package copy tooImage Store failed: ");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Provision hello application.  "MyApplicationV1" is hello folder in hello image store where hello application package is located. 
    // hello application type with name "MyApplicationType" and version "1.0.0" (both are found in hello application manifest) 
    // is now registered in hello cluster.            
    try
    {
        fabricClient.ApplicationManager.ProvisionApplicationAsync(packagePathInImageStore).Wait();

        Console.WriteLine("Provisioned application type {0}", packagePathInImageStore);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("Provision Application Type failed:");

        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    //  Create hello application instance.
    try
    {
        ApplicationDescription appDesc = new ApplicationDescription(new Uri(appName), appType, appVersion);
        fabricClient.ApplicationManager.CreateApplicationAsync(appDesc).Wait();
        Console.WriteLine("Created application instance of type {0}, version {1}", appType, appVersion);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("CreateApplication failed.");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Create hello stateless service description.  For stateful services, use a StatefulServiceDescription object.
    StatelessServiceDescription serviceDescription = new StatelessServiceDescription();
    serviceDescription.ApplicationName = new Uri(appName);
    serviceDescription.InstanceCount = 1;
    serviceDescription.PartitionSchemeDescription = new SingletonPartitionSchemeDescription();
    serviceDescription.ServiceName = new Uri(serviceName);
    serviceDescription.ServiceTypeName = serviceType;

    // Create hello service instance.  If hello service is declared as a default service in hello ApplicationManifest.xml,
    // hello service instance is already running and this call will fail.
    try
    {
        fabricClient.ServiceManager.CreateServiceAsync(serviceDescription).Wait();
        Console.WriteLine("Created service instance {0}", serviceName);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("CreateService failed.");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Delete a service instance.
    try
    {
        DeleteServiceDescription deleteServiceDescription = new DeleteServiceDescription(new Uri(serviceName));

        fabricClient.ServiceManager.DeleteServiceAsync(deleteServiceDescription);
        Console.WriteLine("Deleted service instance {0}", serviceName);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("DeleteService failed.");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Delete an application instance from hello application type.
    try
    {
        DeleteApplicationDescription deleteApplicationDescription = new DeleteApplicationDescription(new Uri(appName));

        fabricClient.ApplicationManager.DeleteApplicationAsync(deleteApplicationDescription).Wait();
        Console.WriteLine("Deleted application instance {0}", appName);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("DeleteApplication failed.");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Un-provision hello application type.
    try
    {
        fabricClient.ApplicationManager.UnprovisionApplicationAsync(appType, appVersion).Wait();
        Console.WriteLine("Un-provisioned application type {0}, version {1}", appType, appVersion);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("Un-provision application type failed: ");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Delete hello application package from a location in hello image store.
    try
    {
        fabricClient.ApplicationManager.RemoveApplicationPackage(imageStoreConnectionString, packagePathInImageStore);
        Console.WriteLine("Application package removed from {0}", packagePathInImageStore);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("Application package removal from Image Store failed: ");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    Console.WriteLine("Hit enter...");
    Console.Read();
}        
}
}

```

## <a name="next-steps"></a><span data-ttu-id="571ec-197">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="571ec-197">Next steps</span></span>
[<span data-ttu-id="571ec-198">Обновление приложения Service Fabric</span><span class="sxs-lookup"><span data-stu-id="571ec-198">Service Fabric application upgrade</span></span>](service-fabric-application-upgrade.md)

[<span data-ttu-id="571ec-199">Общие сведения о работоспособности Service Fabric</span><span class="sxs-lookup"><span data-stu-id="571ec-199">Service Fabric health introduction</span></span>](service-fabric-health-introduction.md)

[<span data-ttu-id="571ec-200">Диагностика и устранение неполадок службы Service Fabric</span><span class="sxs-lookup"><span data-stu-id="571ec-200">Diagnose and troubleshoot a Service Fabric service</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[<span data-ttu-id="571ec-201">Моделирование приложения в Service Fabric</span><span class="sxs-lookup"><span data-stu-id="571ec-201">Model an application in Service Fabric</span></span>](service-fabric-application-model.md)

<!--Link references--In actual articles, you only need a single period before hello slash-->
[10]: service-fabric-application-model.md
[11]: service-fabric-application-upgrade.md
