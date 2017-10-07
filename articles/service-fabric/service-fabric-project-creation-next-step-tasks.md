---
title: "следующие шаги создания проекта aaaService структуры | Документы Microsoft"
description: "В этой статье содержатся ссылки набор основных задач разработки tooa для Service Fabric"
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 299d1f97-1ca9-440d-9f81-d1d0dd2bf4df
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: rwike77
ms.openlocfilehash: 45598bfabedf280fba8af449ef920f40b409a609
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="your-service-fabric-application-and-next-steps"></a><span data-ttu-id="2c46a-103">Ваше приложение Service Fabric и дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2c46a-103">Your Service Fabric application and next steps</span></span>
<span data-ttu-id="2c46a-104">Ваше приложение Azure Service Fabric создано.</span><span class="sxs-lookup"><span data-stu-id="2c46a-104">Your Azure Service Fabric application has been created.</span></span> <span data-ttu-id="2c46a-105">В этой статье описывающего hello план проекта и некоторые возможные дальнейшие действия.</span><span class="sxs-lookup"><span data-stu-id="2c46a-105">This article describes hello makeup of your project and some potential next steps.</span></span>

## <a name="your-application"></a><span data-ttu-id="2c46a-106">Ваше приложение</span><span class="sxs-lookup"><span data-stu-id="2c46a-106">Your application</span></span>
<span data-ttu-id="2c46a-107">Каждое новое приложение включает проект приложения.</span><span class="sxs-lookup"><span data-stu-id="2c46a-107">Every new application includes an application project.</span></span> <span data-ttu-id="2c46a-108">Возможно, один или два дополнительных проекта, в зависимости от типа hello выбранной службы.</span><span class="sxs-lookup"><span data-stu-id="2c46a-108">There may be one or two additional projects, depending on hello type of service chosen.</span></span>

### <a name="hello-application-project"></a><span data-ttu-id="2c46a-109">проект приложения Hello</span><span class="sxs-lookup"><span data-stu-id="2c46a-109">hello application project</span></span>
<span data-ttu-id="2c46a-110">проект приложения Hello состоит из:</span><span class="sxs-lookup"><span data-stu-id="2c46a-110">hello application project consists of:</span></span>

* <span data-ttu-id="2c46a-111">Набор служб toohello ссылки, входящих в состав приложения.</span><span class="sxs-lookup"><span data-stu-id="2c46a-111">A set of references toohello services that make up your application.</span></span>
* <span data-ttu-id="2c46a-112">Три публикация профилей (узел 1 локальной, 5-узловая локальной и облачной), которые можно использовать toomaintain настройках для работы с различных сред — как конечную точку кластера tooa связанные настройки и ли tooperform обновить развертывания по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="2c46a-112">Three publish profiles (1-Node Local, 5-Node Local, and Cloud) that you can use toomaintain preferences for working with different environments--such as preferences related tooa cluster endpoint and whether tooperform upgrade deployments by default.</span></span>
* <span data-ttu-id="2c46a-113">Три параметра файлов приложения (то же, как описано выше), которые можно использовать конфигурации приложения для конкретной среды toomaintain, например количество hello toocreate секций для службы.</span><span class="sxs-lookup"><span data-stu-id="2c46a-113">Three application parameter files (same as above) that you can use toomaintain environment-specific application configurations, such as hello number of partitions toocreate for a service.</span></span>
* <span data-ttu-id="2c46a-114">Скрипт развертывания, можно использовать toodeploy приложения из командной строки hello, или как часть автоматических непрерывной интеграции и развертывания конвейера.</span><span class="sxs-lookup"><span data-stu-id="2c46a-114">A deployment script that you can use toodeploy your application from hello command line or as part of an automated continuous integration and deployment pipeline.</span></span>
* <span data-ttu-id="2c46a-115">манифест приложения Hello, описывающий приложения hello.</span><span class="sxs-lookup"><span data-stu-id="2c46a-115">hello application manifest, which describes hello application.</span></span> <span data-ttu-id="2c46a-116">Hello манифеста можно найти в папке ApplicationPackageRoot hello.</span><span class="sxs-lookup"><span data-stu-id="2c46a-116">You can find hello manifest under hello ApplicationPackageRoot folder.</span></span>

### <a name="stateless-service"></a><span data-ttu-id="2c46a-117">Служба без отслеживания состояния</span><span class="sxs-lookup"><span data-stu-id="2c46a-117">Stateless service</span></span>
<span data-ttu-id="2c46a-118">При добавлении новой службы без сохранения состояния, Visual Studio добавляет проект решении tooyour службы, включающее тип потомками `StatelessService`.</span><span class="sxs-lookup"><span data-stu-id="2c46a-118">When you add a new stateless service, Visual Studio adds a service project tooyour solution that includes a type descended from `StatelessService`.</span></span> <span data-ttu-id="2c46a-119">Служба Hello увеличивает значение локальной переменной в счетчике.</span><span class="sxs-lookup"><span data-stu-id="2c46a-119">hello service increments a local variable in a counter.</span></span>

### <a name="stateful-service"></a><span data-ttu-id="2c46a-120">Служба с отслеживанием состояния</span><span class="sxs-lookup"><span data-stu-id="2c46a-120">Stateful service</span></span>
<span data-ttu-id="2c46a-121">При добавлении новой службы с отслеживанием состояния, Visual Studio добавляет проект решении tooyour службы, включающее тип потомками `StatefulService`.</span><span class="sxs-lookup"><span data-stu-id="2c46a-121">When you add a new stateful service, Visual Studio adds a service project tooyour solution that includes a type descended from `StatefulService`.</span></span> <span data-ttu-id="2c46a-122">Hello службы увеличивает значение счетчика в его `RunAsync` метод и сохраняет результат hello в `ReliableDictionary`.</span><span class="sxs-lookup"><span data-stu-id="2c46a-122">hello service increments a counter in its `RunAsync` method and stores hello result in a `ReliableDictionary`.</span></span>

### <a name="actor-service"></a><span data-ttu-id="2c46a-123">Служба субъекта</span><span class="sxs-lookup"><span data-stu-id="2c46a-123">Actor service</span></span>
<span data-ttu-id="2c46a-124">При добавлении нового надежного субъекта, Visual Studio добавляет два решения проектов tooyour: проект субъекта и проекте интерфейса.</span><span class="sxs-lookup"><span data-stu-id="2c46a-124">When you add a new reliable actor, Visual Studio adds two projects tooyour solution: an actor project and an interface project.</span></span>

<span data-ttu-id="2c46a-125">проект субъекта Hello предоставляет методы задания и начало hello значение счетчика, надежно сохраняются в пределах состояния субъекта hello.</span><span class="sxs-lookup"><span data-stu-id="2c46a-125">hello actor project provides methods for setting and getting hello value of a counter that is reliably persisted within hello actor's state.</span></span> <span data-ttu-id="2c46a-126">Hello проекта интерфейса предоставляет интерфейс других служб можно использовать tooinvoke hello субъекта.</span><span class="sxs-lookup"><span data-stu-id="2c46a-126">hello interface project provides an interface that other services can use tooinvoke hello actor.</span></span>

### <a name="stateless-web-api"></a><span data-ttu-id="2c46a-127">Веб-API без отслеживания состояния</span><span class="sxs-lookup"><span data-stu-id="2c46a-127">Stateless Web API</span></span>
<span data-ttu-id="2c46a-128">проект без сохранения состояния веб-API Hello предоставляет простую веб-службы, которые можно использовать tooopen приложений tooexternal-клиентов.</span><span class="sxs-lookup"><span data-stu-id="2c46a-128">hello stateless Web API project provides a basic web service that you can use tooopen your application tooexternal clients.</span></span> <span data-ttu-id="2c46a-129">Дополнительные сведения о структуру проекта hello. в разделе [веб-API службы фабрики служб с резидентным OWIN](service-fabric-reliable-services-communication-webapi.md).</span><span class="sxs-lookup"><span data-stu-id="2c46a-129">For more information about how hello project structured, see [Service Fabric Web API services with OWIN self-hosting](service-fabric-reliable-services-communication-webapi.md).</span></span>


### <a name="aspnet-core"></a><span data-ttu-id="2c46a-130">ASP.NET core</span><span class="sxs-lookup"><span data-stu-id="2c46a-130">ASP.NET core</span></span>
<span data-ttu-id="2c46a-131">Hello Service Fabric SDK предоставляет hello же установить ASP.NET Core шаблонов, доступных для проектов ASP.NET Core автономного: пустое, [веб-API][aspnet-webapi], и [веб-приложение][aspnet-webapp].</span><span class="sxs-lookup"><span data-stu-id="2c46a-131">hello Service Fabric SDK provides hello same set of ASP.NET Core templates that are available for standalone ASP.NET Core projects: empty, [Web API][aspnet-webapi], and [Web Application][aspnet-webapp].</span></span>

### <a name="guest-executables-and-guest-containers"></a><span data-ttu-id="2c46a-132">Гостевые исполняемые файлы и контейнеры</span><span class="sxs-lookup"><span data-stu-id="2c46a-132">Guest executables and guest containers</span></span>

<span data-ttu-id="2c46a-133">Service Fabric «guest» — это служба, который не встроен в моделях программирования платформы hello.</span><span class="sxs-lookup"><span data-stu-id="2c46a-133">A Service Fabric 'guest' is a service that is not built with hello platform's programming models.</span></span> <span data-ttu-id="2c46a-134">Вы можете упаковать hello двоичные файлы для гостевой либо [непосредственно в пакет приложения hello](service-fabric-deploy-existing-app.md) или [через образ контейнера](service-fabric-deploy-container.md).</span><span class="sxs-lookup"><span data-stu-id="2c46a-134">You can package hello binaries for a guest either [directly in hello application package](service-fabric-deploy-existing-app.md) or [through a container image](service-fabric-deploy-container.md).</span></span> <span data-ttu-id="2c46a-135">В обоих случаях Visual Studio создает hello необходимые артефакты в hello **ApplicationPackageRoot** папку проекта приложения hello.</span><span class="sxs-lookup"><span data-stu-id="2c46a-135">In both cases, Visual Studio creates hello necessary artifacts in hello **ApplicationPackageRoot** folder of hello application project.</span></span> <span data-ttu-id="2c46a-136">Visual Studio не создаст новый проект служб, так как код hello уже существует в другом месте.</span><span class="sxs-lookup"><span data-stu-id="2c46a-136">Visual Studio will not create a new service project because hello code already exists elsewhere.</span></span> <span data-ttu-id="2c46a-137">Если вы хотите toomanage гостевые проекты наряду с проект приложения hello Service Fabric, их можно добавить toohello одного решения Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2c46a-137">If you would like toomanage your guest projects alongside hello Service Fabric application project, you can add them toohello same Visual Studio solution.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2c46a-138">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2c46a-138">Next steps</span></span>
### <a name="create-an-azure-cluster"></a><span data-ttu-id="2c46a-139">Создание кластера Azure</span><span class="sxs-lookup"><span data-stu-id="2c46a-139">Create an Azure cluster</span></span>
<span data-ttu-id="2c46a-140">Hello Service Fabric SDK предоставляет локального кластера для разработки и тестирования.</span><span class="sxs-lookup"><span data-stu-id="2c46a-140">hello Service Fabric SDK provides a local cluster for development and testing.</span></span> <span data-ttu-id="2c46a-141">toocreate кластер в Azure, в разделе [установка кластера Service Fabric с портала Azure hello][create-cluster-in-portal].</span><span class="sxs-lookup"><span data-stu-id="2c46a-141">toocreate a cluster in Azure, see [Setting up a Service Fabric cluster from hello Azure portal][create-cluster-in-portal].</span></span>

### <a name="publish-your-application-tooazure"></a><span data-ttu-id="2c46a-142">Публикация вашего приложения tooAzure</span><span class="sxs-lookup"><span data-stu-id="2c46a-142">Publish your application tooAzure</span></span>
<span data-ttu-id="2c46a-143">Можно опубликовать приложение непосредственно из Visual Studio tooan Azure кластера.</span><span class="sxs-lookup"><span data-stu-id="2c46a-143">You can publish your application directly from Visual Studio tooan Azure cluster.</span></span> <span data-ttu-id="2c46a-144">toolearn, изучите раздел [публикация вашего приложения tooAzure][publish-app-to-azure].</span><span class="sxs-lookup"><span data-stu-id="2c46a-144">toolearn how, see [Publishing your application tooAzure][publish-app-to-azure].</span></span>

### <a name="use-service-fabric-explorer-toovisualize-your-cluster"></a><span data-ttu-id="2c46a-145">Использовать обозреватель Service Fabric toovisualize кластера</span><span class="sxs-lookup"><span data-stu-id="2c46a-145">Use Service Fabric Explorer toovisualize your cluster</span></span>
<span data-ttu-id="2c46a-146">Обозреватель Service Fabric предлагает простой способ toovisualize кластера, включая развернутых приложений и физическую структуру.</span><span class="sxs-lookup"><span data-stu-id="2c46a-146">Service Fabric Explorer offers an easy way toovisualize your cluster, including deployed applications and physical layout.</span></span> <span data-ttu-id="2c46a-147">toolearn более, в разделе [визуализация кластера с помощью Service Fabric Explorer][visualize-with-sfx].</span><span class="sxs-lookup"><span data-stu-id="2c46a-147">toolearn more, see [Visualizing your cluster by using Service Fabric Explorer][visualize-with-sfx].</span></span>

### <a name="version-and-upgrade-your-services"></a><span data-ttu-id="2c46a-148">Версии и обновление служб</span><span class="sxs-lookup"><span data-stu-id="2c46a-148">Version and upgrade your services</span></span>
<span data-ttu-id="2c46a-149">Service Fabric обеспечивает независимое управление версиями и обновление независимых служб в приложении.</span><span class="sxs-lookup"><span data-stu-id="2c46a-149">Service Fabric enables independent versioning and upgrading of independent services in an application.</span></span> <span data-ttu-id="2c46a-150">toolearn более, в разделе [управления версиями и обновление служб][app-upgrade-tutorial].</span><span class="sxs-lookup"><span data-stu-id="2c46a-150">toolearn more, see [Versioning and upgrading your services][app-upgrade-tutorial].</span></span>

### <a name="configure-continuous-integration-with-visual-studio-team-services"></a><span data-ttu-id="2c46a-151">Настройка непрерывной интеграции с Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="2c46a-151">Configure continuous integration with Visual Studio Team Services</span></span>
<span data-ttu-id="2c46a-152">toolearn процесс непрерывной интеграции можно настроить для приложения Service Fabric разделе [настроить непрерывную интеграцию с Visual Studio Team Services][ci-with-vso].</span><span class="sxs-lookup"><span data-stu-id="2c46a-152">toolearn how you can set up a continuous integration process for your Service Fabric application, see [Configure continuous integration with Visual Studio Team Services][ci-with-vso].</span></span>

<!-- Links -->
[add-web-frontend]: service-fabric-add-a-web-frontend.md
[create-cluster-in-portal]: service-fabric-cluster-creation-via-portal.md
[publish-app-to-azure]: service-fabric-publish-app-remote-cluster.md
[visualize-with-sfx]: service-fabric-visualizing-your-cluster.md
[ci-with-vso]: service-fabric-set-up-continuous-integration.md
[reliable-services-webapi]: service-fabric-reliable-services-communication-webapi.md
[app-upgrade-tutorial]: service-fabric-application-upgrade-tutorial.md
[aspnet-webapi]: https://docs.asp.net/en/latest/tutorials/first-web-api.html
[aspnet-webapp]: https://docs.asp.net/en/latest/tutorials/first-mvc-app/index.html
