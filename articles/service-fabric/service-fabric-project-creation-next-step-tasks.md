---
title: "Дальнейшие действия по созданию проекта Service Fabric | Документация Майкрософт"
description: "Эта статья содержит ссылки на набор основных задач разработки для Service Fabric"
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
ms.openlocfilehash: 74019850c507902d9ef7ec47a364fff234aaf32b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="your-service-fabric-application-and-next-steps"></a><span data-ttu-id="7ba8c-103">Ваше приложение Service Fabric и дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7ba8c-103">Your Service Fabric application and next steps</span></span>
<span data-ttu-id="7ba8c-104">Ваше приложение Azure Service Fabric создано.</span><span class="sxs-lookup"><span data-stu-id="7ba8c-104">Your Azure Service Fabric application has been created.</span></span> <span data-ttu-id="7ba8c-105">В этой статье описываются состав проекта и некоторые возможные дальнейшие действия.</span><span class="sxs-lookup"><span data-stu-id="7ba8c-105">This article describes the makeup of your project and some potential next steps.</span></span>

## <a name="your-application"></a><span data-ttu-id="7ba8c-106">Ваше приложение</span><span class="sxs-lookup"><span data-stu-id="7ba8c-106">Your application</span></span>
<span data-ttu-id="7ba8c-107">Каждое новое приложение включает проект приложения.</span><span class="sxs-lookup"><span data-stu-id="7ba8c-107">Every new application includes an application project.</span></span> <span data-ttu-id="7ba8c-108">В зависимости от типа выбранной службы также могут быть один или два дополнительных проекта.</span><span class="sxs-lookup"><span data-stu-id="7ba8c-108">There may be one or two additional projects, depending on the type of service chosen.</span></span>

### <a name="the-application-project"></a><span data-ttu-id="7ba8c-109">Проект приложения</span><span class="sxs-lookup"><span data-stu-id="7ba8c-109">The application project</span></span>
<span data-ttu-id="7ba8c-110">Проект приложения включает:</span><span class="sxs-lookup"><span data-stu-id="7ba8c-110">The application project consists of:</span></span>

* <span data-ttu-id="7ba8c-111">Набор ссылок на службы, входящие в состав приложения.</span><span class="sxs-lookup"><span data-stu-id="7ba8c-111">A set of references to the services that make up your application.</span></span>
* <span data-ttu-id="7ba8c-112">Три профиля публикации (локальный 1-узловой, локальный 5-узловой и облачный), которые можно использовать для хранения настроек для работы в различных средах, например параметров конечной точки кластера и параметра, определяющего, следует ли разворачивать обновления по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="7ba8c-112">Three publish profiles (1-Node Local, 5-Node Local, and Cloud) that you can use to maintain preferences for working with different environments--such as preferences related to a cluster endpoint and whether to perform upgrade deployments by default.</span></span>
* <span data-ttu-id="7ba8c-113">Три файла с параметрами приложения (те же, что и выше), которые можно использовать для хранения конфигураций приложения для разных сред, включая число разделов, которые создаются для службы.</span><span class="sxs-lookup"><span data-stu-id="7ba8c-113">Three application parameter files (same as above) that you can use to maintain environment-specific application configurations, such as the number of partitions to create for a service.</span></span>
* <span data-ttu-id="7ba8c-114">Сценарий развертывания, который можно использовать для развертывания приложения из командной строки или в составе автоматизированного конвейера непрерывной интеграции и развертывания.</span><span class="sxs-lookup"><span data-stu-id="7ba8c-114">A deployment script that you can use to deploy your application from the command line or as part of an automated continuous integration and deployment pipeline.</span></span>
* <span data-ttu-id="7ba8c-115">Манифест приложения, описывающий приложение.</span><span class="sxs-lookup"><span data-stu-id="7ba8c-115">The application manifest, which describes the application.</span></span> <span data-ttu-id="7ba8c-116">Манифест можно найти в папке ApplicationPackageRoot.</span><span class="sxs-lookup"><span data-stu-id="7ba8c-116">You can find the manifest under the ApplicationPackageRoot folder.</span></span>

### <a name="stateless-service"></a><span data-ttu-id="7ba8c-117">Служба без отслеживания состояния</span><span class="sxs-lookup"><span data-stu-id="7ba8c-117">Stateless service</span></span>
<span data-ttu-id="7ba8c-118">При добавлении новой службы без отслеживания состояния Visual Studio добавляет в решение проект службы, который содержит тип, происходящий из `StatelessService`.</span><span class="sxs-lookup"><span data-stu-id="7ba8c-118">When you add a new stateless service, Visual Studio adds a service project to your solution that includes a type descended from `StatelessService`.</span></span> <span data-ttu-id="7ba8c-119">Служба увеличивает значение локальной переменной в счетчике.</span><span class="sxs-lookup"><span data-stu-id="7ba8c-119">The service increments a local variable in a counter.</span></span>

### <a name="stateful-service"></a><span data-ttu-id="7ba8c-120">Служба с отслеживанием состояния</span><span class="sxs-lookup"><span data-stu-id="7ba8c-120">Stateful service</span></span>
<span data-ttu-id="7ba8c-121">При добавлении новой службы с отслеживанием состояния Visual Studio добавляет в решение проект службы, который содержит тип, происходящий из `StatefulService`.</span><span class="sxs-lookup"><span data-stu-id="7ba8c-121">When you add a new stateful service, Visual Studio adds a service project to your solution that includes a type descended from `StatefulService`.</span></span> <span data-ttu-id="7ba8c-122">Служба увеличивает значение счетчика в своем методе `RunAsync` и сохраняет результат в `ReliableDictionary`.</span><span class="sxs-lookup"><span data-stu-id="7ba8c-122">The service increments a counter in its `RunAsync` method and stores the result in a `ReliableDictionary`.</span></span>

### <a name="actor-service"></a><span data-ttu-id="7ba8c-123">Служба субъекта</span><span class="sxs-lookup"><span data-stu-id="7ba8c-123">Actor service</span></span>
<span data-ttu-id="7ba8c-124">При добавлении нового надежного субъекта Visual Studio добавляет в решение два проекта: проект субъекта и проект интерфейса.</span><span class="sxs-lookup"><span data-stu-id="7ba8c-124">When you add a new reliable actor, Visual Studio adds two projects to your solution: an actor project and an interface project.</span></span>

<span data-ttu-id="7ba8c-125">Проект субъекта предоставляет методы для настройки и получения значения счетчика, надежно сохраняемого в состоянии субъекта.</span><span class="sxs-lookup"><span data-stu-id="7ba8c-125">The actor project provides methods for setting and getting the value of a counter that is reliably persisted within the actor's state.</span></span> <span data-ttu-id="7ba8c-126">Проект интерфейса предоставляет интерфейс, который используется другими службами для вызова субъекта.</span><span class="sxs-lookup"><span data-stu-id="7ba8c-126">The interface project provides an interface that other services can use to invoke the actor.</span></span>

### <a name="stateless-web-api"></a><span data-ttu-id="7ba8c-127">Веб-API без отслеживания состояния</span><span class="sxs-lookup"><span data-stu-id="7ba8c-127">Stateless Web API</span></span>
<span data-ttu-id="7ba8c-128">Проект веб-API без отслеживания состояния предоставляет простую веб-службу, которую можно использовать для открытия приложения во внешних клиентах.</span><span class="sxs-lookup"><span data-stu-id="7ba8c-128">The stateless Web API project provides a basic web service that you can use to open your application to external clients.</span></span> <span data-ttu-id="7ba8c-129">Дополнительные сведения о структуре проекта см. в разделе [Приступая к работе со службами веб-API Service Fabric с саморазмещением OWIN](service-fabric-reliable-services-communication-webapi.md).</span><span class="sxs-lookup"><span data-stu-id="7ba8c-129">For more information about how the project structured, see [Service Fabric Web API services with OWIN self-hosting](service-fabric-reliable-services-communication-webapi.md).</span></span>


### <a name="aspnet-core"></a><span data-ttu-id="7ba8c-130">ASP.NET core</span><span class="sxs-lookup"><span data-stu-id="7ba8c-130">ASP.NET core</span></span>
<span data-ttu-id="7ba8c-131">Пакет SDK для Service Fabric предоставляет набор тех же шаблонов ASP.NET Core, которые доступны для автономных проектов ASP.NET Core. Набор включает пустой шаблон, а также шаблоны [веб-API][aspnet-webapi] и [веб-приложения][aspnet-webapp].</span><span class="sxs-lookup"><span data-stu-id="7ba8c-131">The Service Fabric SDK provides the same set of ASP.NET Core templates that are available for standalone ASP.NET Core projects: empty, [Web API][aspnet-webapi], and [Web Application][aspnet-webapp].</span></span>

### <a name="guest-executables-and-guest-containers"></a><span data-ttu-id="7ba8c-132">Гостевые исполняемые файлы и контейнеры</span><span class="sxs-lookup"><span data-stu-id="7ba8c-132">Guest executables and guest containers</span></span>

<span data-ttu-id="7ba8c-133">Гостевая система Service Fabric — это служба, созданная не на основе моделей программирования платформы.</span><span class="sxs-lookup"><span data-stu-id="7ba8c-133">A Service Fabric 'guest' is a service that is not built with the platform's programming models.</span></span> <span data-ttu-id="7ba8c-134">Двоичные файлы гостевой системы можно упаковать [непосредственно в пакете приложения](service-fabric-deploy-existing-app.md) или [через образ контейнера](service-fabric-deploy-container.md).</span><span class="sxs-lookup"><span data-stu-id="7ba8c-134">You can package the binaries for a guest either [directly in the application package](service-fabric-deploy-existing-app.md) or [through a container image](service-fabric-deploy-container.md).</span></span> <span data-ttu-id="7ba8c-135">В обоих случаях Visual Studio создает необходимые артефакты в папке **ApplicationPackageRoot** проекта приложения.</span><span class="sxs-lookup"><span data-stu-id="7ba8c-135">In both cases, Visual Studio creates the necessary artifacts in the **ApplicationPackageRoot** folder of the application project.</span></span> <span data-ttu-id="7ba8c-136">Visual Studio не создаст проект службы, так как код уже находится в другом месте.</span><span class="sxs-lookup"><span data-stu-id="7ba8c-136">Visual Studio will not create a new service project because the code already exists elsewhere.</span></span> <span data-ttu-id="7ba8c-137">Чтобы управлять гостевыми проектами вместе с проектом приложения Service Fabric, их можно добавить в то же решение Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7ba8c-137">If you would like to manage your guest projects alongside the Service Fabric application project, you can add them to the same Visual Studio solution.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7ba8c-138">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7ba8c-138">Next steps</span></span>
### <a name="create-an-azure-cluster"></a><span data-ttu-id="7ba8c-139">Создание кластера Azure</span><span class="sxs-lookup"><span data-stu-id="7ba8c-139">Create an Azure cluster</span></span>
<span data-ttu-id="7ba8c-140">Пакет SDK Service Fabric предоставляет локальный кластер для разработки и тестирования.</span><span class="sxs-lookup"><span data-stu-id="7ba8c-140">The Service Fabric SDK provides a local cluster for development and testing.</span></span> <span data-ttu-id="7ba8c-141">Сведения о создании кластера в Azure см. в статье [Создание кластера Service Fabric в Azure с помощью портала Azure][create-cluster-in-portal].</span><span class="sxs-lookup"><span data-stu-id="7ba8c-141">To create a cluster in Azure, see [Setting up a Service Fabric cluster from the Azure portal][create-cluster-in-portal].</span></span>

### <a name="publish-your-application-to-azure"></a><span data-ttu-id="7ba8c-142">Публикация изменений в Azure</span><span class="sxs-lookup"><span data-stu-id="7ba8c-142">Publish your application to Azure</span></span>
<span data-ttu-id="7ba8c-143">Приложение в кластер Azure можно опубликовать напрямую из Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7ba8c-143">You can publish your application directly from Visual Studio to an Azure cluster.</span></span> <span data-ttu-id="7ba8c-144">Чтобы узнать, как это сделать, см. сведения в статье [Публикация приложения на удаленный кластер с помощью Visual Studio][publish-app-to-azure].</span><span class="sxs-lookup"><span data-stu-id="7ba8c-144">To learn how, see [Publishing your application to Azure][publish-app-to-azure].</span></span>

### <a name="use-service-fabric-explorer-to-visualize-your-cluster"></a><span data-ttu-id="7ba8c-145">Визуализация кластера с помощью обозревателя Service Fabric</span><span class="sxs-lookup"><span data-stu-id="7ba8c-145">Use Service Fabric Explorer to visualize your cluster</span></span>
<span data-ttu-id="7ba8c-146">Обозреватель Service Fabric предоставляет простой способ визуализации кластера, включая развернутые приложения и физическую структуру.</span><span class="sxs-lookup"><span data-stu-id="7ba8c-146">Service Fabric Explorer offers an easy way to visualize your cluster, including deployed applications and physical layout.</span></span> <span data-ttu-id="7ba8c-147">Дополнительные сведения см. в статье [Визуализация кластера с помощью обозревателя Service Fabric][visualize-with-sfx].</span><span class="sxs-lookup"><span data-stu-id="7ba8c-147">To learn more, see [Visualizing your cluster by using Service Fabric Explorer][visualize-with-sfx].</span></span>

### <a name="version-and-upgrade-your-services"></a><span data-ttu-id="7ba8c-148">Версии и обновление служб</span><span class="sxs-lookup"><span data-stu-id="7ba8c-148">Version and upgrade your services</span></span>
<span data-ttu-id="7ba8c-149">Service Fabric обеспечивает независимое управление версиями и обновление независимых служб в приложении.</span><span class="sxs-lookup"><span data-stu-id="7ba8c-149">Service Fabric enables independent versioning and upgrading of independent services in an application.</span></span> <span data-ttu-id="7ba8c-150">Дополнительные сведения см. в [руководстве по обновлению приложений Service Fabric с помощью Visual Studio][app-upgrade-tutorial].</span><span class="sxs-lookup"><span data-stu-id="7ba8c-150">To learn more, see [Versioning and upgrading your services][app-upgrade-tutorial].</span></span>

### <a name="configure-continuous-integration-with-visual-studio-team-services"></a><span data-ttu-id="7ba8c-151">Настройка непрерывной интеграции с Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="7ba8c-151">Configure continuous integration with Visual Studio Team Services</span></span>
<span data-ttu-id="7ba8c-152">Чтобы узнать, как настроить процесс непрерывной интеграции для приложения Service Fabric, см. сведения в статье [Настройка непрерывных интеграций и развертывания с помощью Visual Studio Team Services][ci-with-vso].</span><span class="sxs-lookup"><span data-stu-id="7ba8c-152">To learn how you can set up a continuous integration process for your Service Fabric application, see [Configure continuous integration with Visual Studio Team Services][ci-with-vso].</span></span>

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
