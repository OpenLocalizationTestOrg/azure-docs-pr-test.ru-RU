---
title: "aaaVisualizing кластер с помощью Service Fabric Explorer | Документы Microsoft"
description: "Обозреватель Service Fabric — это веб-средство для изучения облачных приложений и узлов в кластере Microsoft Azure Service Fabric и управления ими."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: c875b993-b4eb-494b-94b5-e02f5eddbd6a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/12/2017
ms.author: ryanwi
ms.openlocfilehash: 73adc4fc254cf6b949b4419b02a046cee3f6a83d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-your-cluster-with-service-fabric-explorer"></a><span data-ttu-id="31bcc-103">Визуализация кластера с помощью обозревателя Service Fabric</span><span class="sxs-lookup"><span data-stu-id="31bcc-103">Visualize your cluster with Service Fabric Explorer</span></span>
<span data-ttu-id="31bcc-104">Обозреватель Service Fabric — это веб-средство для изучения приложений и узлов в кластере Azure Service Fabric и управления ими.</span><span class="sxs-lookup"><span data-stu-id="31bcc-104">Service Fabric Explorer is a web-based tool for inspecting and managing applications and nodes in an Azure Service Fabric cluster.</span></span> <span data-ttu-id="31bcc-105">Обозреватель Service Fabric размещается непосредственно в кластере hello, поэтому она доступна всегда, независимо от того, где запущен кластера.</span><span class="sxs-lookup"><span data-stu-id="31bcc-105">Service Fabric Explorer is hosted directly within hello cluster, so it is always available, regardless of where your cluster is running.</span></span>

## <a name="video-tutorial"></a><span data-ttu-id="31bcc-106">Видеоруководство</span><span class="sxs-lookup"><span data-stu-id="31bcc-106">Video tutorial</span></span>

<span data-ttu-id="31bcc-107">как просматривать toouse Service Fabric Explorer toolearn hello следующие видео Microsoft Virtual Academy:</span><span class="sxs-lookup"><span data-stu-id="31bcc-107">toolearn how toouse Service Fabric Explorer, watch hello following Microsoft Virtual Academy video:</span></span>

[<center><img src="./media/service-fabric-visualizing-your-cluster/SfxVideo.png" WIDTH="360" HEIGHT="244"></center>](https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=bBTFg46yC_9806218965)

## <a name="connect-tooservice-fabric-explorer"></a><span data-ttu-id="31bcc-108">Подключение tooService Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="31bcc-108">Connect tooService Fabric Explorer</span></span>
<span data-ttu-id="31bcc-109">Если вы следовали инструкциям hello слишком[подготовить среду разработки](service-fabric-get-started.md), Service Fabric Explorer можно запустить на локальном кластере, перейдя по toohttp://localhost:19080 / обозреватель.</span><span class="sxs-lookup"><span data-stu-id="31bcc-109">If you have followed hello instructions too[prepare your development environment](service-fabric-get-started.md), you can launch Service Fabric Explorer on your local cluster by navigating toohttp://localhost:19080/Explorer.</span></span>

## <a name="understand-hello-service-fabric-explorer-layout"></a><span data-ttu-id="31bcc-110">Анализа структуры Service Fabric Explorer hello</span><span class="sxs-lookup"><span data-stu-id="31bcc-110">Understand hello Service Fabric Explorer layout</span></span>
<span data-ttu-id="31bcc-111">Можно перемещаться по Service Fabric Explorer с помощью дерева hello слева hello.</span><span class="sxs-lookup"><span data-stu-id="31bcc-111">You can navigate through Service Fabric Explorer by using hello tree on hello left.</span></span> <span data-ttu-id="31bcc-112">Hello корневого элемента дерева hello панели мониторинга кластера hello Обзор кластера, в том числе сводную приложения и состояние работоспособности узла.</span><span class="sxs-lookup"><span data-stu-id="31bcc-112">At hello root of hello tree, hello cluster dashboard provides an overview of your cluster, including a summary of application and node health.</span></span>

![Панель мониторинга кластера обозревателя Service Fabric][sfx-cluster-dashboard]

### <a name="view-hello-clusters-layout"></a><span data-ttu-id="31bcc-114">Просмотр макета hello кластера</span><span class="sxs-lookup"><span data-stu-id="31bcc-114">View hello cluster's layout</span></span>
<span data-ttu-id="31bcc-115">Узлы в кластере Service Fabric размещаются в двухмерной сетке доменов сбоя и обновления,</span><span class="sxs-lookup"><span data-stu-id="31bcc-115">Nodes in a Service Fabric cluster are placed across a two-dimensional grid of fault domains and upgrade domains.</span></span> <span data-ttu-id="31bcc-116">Этой размещение гарантирует, что приложения остаются доступными в hello наличие сбоев оборудования и обновления приложения.</span><span class="sxs-lookup"><span data-stu-id="31bcc-116">This placement ensures that your applications remain available in hello presence of hardware failures and application upgrades.</span></span> <span data-ttu-id="31bcc-117">Можно просмотреть спланированную hello текущего кластера с помощью схемы hello кластера.</span><span class="sxs-lookup"><span data-stu-id="31bcc-117">You can view how hello current cluster is laid out by using hello cluster map.</span></span>

![Схема кластера в обозревателе Service Fabric][sfx-cluster-map]

### <a name="view-applications-and-services"></a><span data-ttu-id="31bcc-119">Просмотр приложений и услуг</span><span class="sxs-lookup"><span data-stu-id="31bcc-119">View applications and services</span></span>
<span data-ttu-id="31bcc-120">кластер Hello содержит две ветви: один для приложений, а другой — для узлов.</span><span class="sxs-lookup"><span data-stu-id="31bcc-120">hello cluster contains two subtrees: one for applications and another for nodes.</span></span>

<span data-ttu-id="31bcc-121">Можно использовать toonavigate представление приложения hello через Service Fabric логической иерархии: приложений, служб, разделов и реплик.</span><span class="sxs-lookup"><span data-stu-id="31bcc-121">You can use hello application view toonavigate through Service Fabric's logical hierarchy: applications, services, partitions, and replicas.</span></span>

<span data-ttu-id="31bcc-122">В следующем примере hello, hello приложения **MyApp** состоит из двух служб, **MyStatefulService** и **WebService**.</span><span class="sxs-lookup"><span data-stu-id="31bcc-122">In hello example below, hello application **MyApp** consists of two services, **MyStatefulService** and **WebService**.</span></span> <span data-ttu-id="31bcc-123">Так как **MyStatefulService** — служба с отслеживанием состояния, она включает раздел с одной основной и двумя вторичными репликами.</span><span class="sxs-lookup"><span data-stu-id="31bcc-123">Since **MyStatefulService** is stateful, it includes a partition with one primary and two secondary replicas.</span></span> <span data-ttu-id="31bcc-124">Напротив, WebSvcService — служба без сохранения состояния и содержит единственный экземпляр.</span><span class="sxs-lookup"><span data-stu-id="31bcc-124">By contrast, WebSvcService is stateless and contains a single instance.</span></span>

![Представление приложений обозревателя Service Fabric][sfx-application-tree]

<span data-ttu-id="31bcc-126">На каждом уровне дерева hello hello основной области отображаются нужные сведения об элементе hello.</span><span class="sxs-lookup"><span data-stu-id="31bcc-126">At each level of hello tree, hello main pane shows pertinent information about hello item.</span></span> <span data-ttu-id="31bcc-127">Например вы увидите состояние работоспособности hello и версия для конкретной службы.</span><span class="sxs-lookup"><span data-stu-id="31bcc-127">For example, you can see hello health status and version for a particular service.</span></span>

![Панель основных сведений обозревателя Service Fabric][sfx-service-essentials]

### <a name="view-hello-clusters-nodes"></a><span data-ttu-id="31bcc-129">Просмотреть узлы кластера hello</span><span class="sxs-lookup"><span data-stu-id="31bcc-129">View hello cluster's nodes</span></span>
<span data-ttu-id="31bcc-130">представление узла Hello отображает hello физическую структуру hello кластера.</span><span class="sxs-lookup"><span data-stu-id="31bcc-130">hello node view shows hello physical layout of hello cluster.</span></span> <span data-ttu-id="31bcc-131">Для каждого узла можно просмотреть, какие приложения были развернуты на этом узле</span><span class="sxs-lookup"><span data-stu-id="31bcc-131">For a given node, you can inspect which applications have code deployed on that node.</span></span> <span data-ttu-id="31bcc-132">и какие реплики запущены в настоящее время.</span><span class="sxs-lookup"><span data-stu-id="31bcc-132">More specifically, you can see which replicas are currently running there.</span></span>

## <a name="actions"></a><span data-ttu-id="31bcc-133">Действия</span><span class="sxs-lookup"><span data-stu-id="31bcc-133">Actions</span></span>
<span data-ttu-id="31bcc-134">Обозреватель Service Fabric предлагает tooinvoke быстро действий на узлах, приложений и служб в кластере.</span><span class="sxs-lookup"><span data-stu-id="31bcc-134">Service Fabric Explorer offers a quick way tooinvoke actions on nodes, applications, and services within your cluster.</span></span>

<span data-ttu-id="31bcc-135">Например, toodelete экземпляр приложения выберите приложение hello из дерева hello hello левой части экрана и выберите **действия** > **удалить приложение**.</span><span class="sxs-lookup"><span data-stu-id="31bcc-135">For example, toodelete an application instance, choose hello application from hello tree on hello left, and then choose **Actions** > **Delete Application**.</span></span>

![Удаление приложения в обозревателе Service Fabric][sfx-delete-application]

> [!TIP]
> <span data-ttu-id="31bcc-137">Можно выполнять hello же действия, щелкнув следующий элемент tooeach hello кнопку с многоточием.</span><span class="sxs-lookup"><span data-stu-id="31bcc-137">You can perform hello same actions by clicking hello ellipsis next tooeach element.</span></span>
>
>

<span data-ttu-id="31bcc-138">Hello следующей таблице перечислены действия hello, доступные для каждой сущности:</span><span class="sxs-lookup"><span data-stu-id="31bcc-138">hello following table lists hello actions available for each entity:</span></span>

| <span data-ttu-id="31bcc-139">**Сущность**</span><span class="sxs-lookup"><span data-stu-id="31bcc-139">**Entity**</span></span> | <span data-ttu-id="31bcc-140">**Действие**</span><span class="sxs-lookup"><span data-stu-id="31bcc-140">**Action**</span></span> | <span data-ttu-id="31bcc-141">**Описание**</span><span class="sxs-lookup"><span data-stu-id="31bcc-141">**Description**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="31bcc-142">Тип приложения</span><span class="sxs-lookup"><span data-stu-id="31bcc-142">Application type</span></span> |<span data-ttu-id="31bcc-143">Отмена подготовки типа</span><span class="sxs-lookup"><span data-stu-id="31bcc-143">Unprovision type</span></span> |<span data-ttu-id="31bcc-144">Удаляет пакет приложения hello из хранилища образов hello кластера.</span><span class="sxs-lookup"><span data-stu-id="31bcc-144">Removes hello application package from hello cluster's image store.</span></span> <span data-ttu-id="31bcc-145">Требуется все приложения, тип toobe, сначала удалить.</span><span class="sxs-lookup"><span data-stu-id="31bcc-145">Requires all applications of that type toobe removed first.</span></span> |
| <span data-ttu-id="31bcc-146">Приложение</span><span class="sxs-lookup"><span data-stu-id="31bcc-146">Application</span></span> |<span data-ttu-id="31bcc-147">Удалить приложение</span><span class="sxs-lookup"><span data-stu-id="31bcc-147">Delete Application</span></span> |<span data-ttu-id="31bcc-148">Удаление приложения hello, включая все его службы и их состояния (если таковые имеются).</span><span class="sxs-lookup"><span data-stu-id="31bcc-148">Delete hello application, including all its services and their state (if any).</span></span> |
| <span data-ttu-id="31bcc-149">служба</span><span class="sxs-lookup"><span data-stu-id="31bcc-149">Service</span></span> |<span data-ttu-id="31bcc-150">Удаление службы</span><span class="sxs-lookup"><span data-stu-id="31bcc-150">Delete Service</span></span> |<span data-ttu-id="31bcc-151">Удаление службы hello и его состояние (если таковые имеются).</span><span class="sxs-lookup"><span data-stu-id="31bcc-151">Delete hello service and its state (if any).</span></span> |
| <span data-ttu-id="31bcc-152">Узел</span><span class="sxs-lookup"><span data-stu-id="31bcc-152">Node</span></span> |<span data-ttu-id="31bcc-153">Активировать</span><span class="sxs-lookup"><span data-stu-id="31bcc-153">Activate</span></span> |<span data-ttu-id="31bcc-154">Активация узла hello.</span><span class="sxs-lookup"><span data-stu-id="31bcc-154">Activate hello node.</span></span> |
| <span data-ttu-id="31bcc-155">Узел</span><span class="sxs-lookup"><span data-stu-id="31bcc-155">Node</span></span> | <span data-ttu-id="31bcc-156">Деактивация (пауза)</span><span class="sxs-lookup"><span data-stu-id="31bcc-156">Deactivate (pause)</span></span> | <span data-ttu-id="31bcc-157">Приостановить работу узла hello в ее текущем состоянии.</span><span class="sxs-lookup"><span data-stu-id="31bcc-157">Pause hello node in its current state.</span></span> <span data-ttu-id="31bcc-158">Служб продолжается toorun, но Service Fabric не перемещает заранее ничего на или отключить его если он не требуется tooprevent сбоя или несогласованности данных.</span><span class="sxs-lookup"><span data-stu-id="31bcc-158">Services continue toorun but Service Fabric does not proactively move anything onto or off it unless it is required tooprevent an outage or data inconsistency.</span></span> <span data-ttu-id="31bcc-159">Это действие не типовыми tooenable отладка служб на tooensure конкретный узел, что они не перемещаются во время проверки.</span><span class="sxs-lookup"><span data-stu-id="31bcc-159">This action is typically used tooenable debugging services on a specific node tooensure that they do not move during inspection.</span></span> | |
| <span data-ttu-id="31bcc-160">Узел</span><span class="sxs-lookup"><span data-stu-id="31bcc-160">Node</span></span> | <span data-ttu-id="31bcc-161">Деактивация (перезапуск)</span><span class="sxs-lookup"><span data-stu-id="31bcc-161">Deactivate (restart)</span></span> | <span data-ttu-id="31bcc-162">Безопасное перемещение всех служб в памяти за пределы узла и закрытие постоянных служб.</span><span class="sxs-lookup"><span data-stu-id="31bcc-162">Safely move all in-memory services off a node and close persistent services.</span></span> <span data-ttu-id="31bcc-163">Обычно используется при перезапуске хост-процессах hello или toobe необходимость машины.</span><span class="sxs-lookup"><span data-stu-id="31bcc-163">Typically used when hello host processes or machine need toobe restarted.</span></span> | |
| <span data-ttu-id="31bcc-164">Узел</span><span class="sxs-lookup"><span data-stu-id="31bcc-164">Node</span></span> | <span data-ttu-id="31bcc-165">Деактивация (удаление данных)</span><span class="sxs-lookup"><span data-stu-id="31bcc-165">Deactivate (remove data)</span></span> | <span data-ttu-id="31bcc-166">Закройте все службы, запущенные на узле hello после построения недостаточно свободных реплик.</span><span class="sxs-lookup"><span data-stu-id="31bcc-166">Safely close all services running on hello node after building sufficient spare replicas.</span></span> <span data-ttu-id="31bcc-167">Обычно используется, когда узел (или хотя бы его хранилище) окончательно выводится из эксплуатации.</span><span class="sxs-lookup"><span data-stu-id="31bcc-167">Typically used when a node (or at least its storage) is being permanently taken out of commission.</span></span> | |
| <span data-ttu-id="31bcc-168">Узел</span><span class="sxs-lookup"><span data-stu-id="31bcc-168">Node</span></span> | <span data-ttu-id="31bcc-169">Удаление состояния узла</span><span class="sxs-lookup"><span data-stu-id="31bcc-169">Remove node state</span></span> | <span data-ttu-id="31bcc-170">Удалите знаний реплики узла из кластера hello.</span><span class="sxs-lookup"><span data-stu-id="31bcc-170">Remove knowledge of a node's replicas from hello cluster.</span></span> <span data-ttu-id="31bcc-171">Обычно используется, когда узел, вышедший из строя, уже нельзя восстановить.</span><span class="sxs-lookup"><span data-stu-id="31bcc-171">Typically used when an already failed node is deemed unrecoverable.</span></span> | |
| <span data-ttu-id="31bcc-172">Узел</span><span class="sxs-lookup"><span data-stu-id="31bcc-172">Node</span></span> | <span data-ttu-id="31bcc-173">Перезагрузить</span><span class="sxs-lookup"><span data-stu-id="31bcc-173">Restart</span></span> | <span data-ttu-id="31bcc-174">Моделирование сбоя узла, перезапустив hello узла.</span><span class="sxs-lookup"><span data-stu-id="31bcc-174">Simulate a node failure by restarting hello node.</span></span> <span data-ttu-id="31bcc-175">Дополнительные сведения см. [здесь](/powershell/module/servicefabric/restart-servicefabricnode?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="31bcc-175">More information [here](/powershell/module/servicefabric/restart-servicefabricnode?view=azureservicefabricps)</span></span> | |

<span data-ttu-id="31bcc-176">Поскольку многие действия разрушительных, могут быть ответы tooconfirm намерениям до завершения действия hello.</span><span class="sxs-lookup"><span data-stu-id="31bcc-176">Since many actions are destructive, you may be asked tooconfirm your intent before hello action is completed.</span></span>

> [!TIP]
> <span data-ttu-id="31bcc-177">Каждого действия, которое может быть выполнено с помощью Service Fabric Explorer также может выполняться с помощью PowerShell или API REST, tooenable автоматизации.</span><span class="sxs-lookup"><span data-stu-id="31bcc-177">Every action that can be performed through Service Fabric Explorer can also be performed through PowerShell or a REST API, tooenable automation.</span></span>
>
>

<span data-ttu-id="31bcc-178">Также можно использовать экземпляры приложения Service Fabric Explorer toocreate для данного приложения типа и версии.</span><span class="sxs-lookup"><span data-stu-id="31bcc-178">You can also use Service Fabric Explorer toocreate application instances for a given application type and version.</span></span> <span data-ttu-id="31bcc-179">Выберите тип приложения hello в представлении дерева hello, а затем щелкните hello **создать экземпляр приложения** Далее toohello версии связи хотелось бы hello правой панели.</span><span class="sxs-lookup"><span data-stu-id="31bcc-179">Choose hello application type in hello tree view, then click hello **Create app instance** link next toohello version you'd like in hello right pane.</span></span>

![Создание экземпляра приложения в Service Fabric Explorer][sfx-create-app-instance]

> [!NOTE]
> <span data-ttu-id="31bcc-181">В настоящее время экземпляры приложения, созданные с помощью Service Fabric Explorer, не могут быть параметризованы.</span><span class="sxs-lookup"><span data-stu-id="31bcc-181">Application instances created through Service Fabric Explorer cannot currently be parameterized.</span></span> <span data-ttu-id="31bcc-182">При их создании используются значения параметров по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="31bcc-182">They are created using default parameter values.</span></span>
>
>

## <a name="connect-tooa-remote-service-fabric-cluster"></a><span data-ttu-id="31bcc-183">Подключение tooa удаленного кластера Service Fabric</span><span class="sxs-lookup"><span data-stu-id="31bcc-183">Connect tooa remote Service Fabric cluster</span></span>
<span data-ttu-id="31bcc-184">Если вы знаете hello кластерную конечную точку и иметь достаточные разрешения Service Fabric Explorer доступен из любого браузера.</span><span class="sxs-lookup"><span data-stu-id="31bcc-184">If you know hello cluster's endpoint and have sufficient permissions you can access Service Fabric Explorer from any browser.</span></span> <span data-ttu-id="31bcc-185">Это так, как обозреватель Service Fabric — еще одно служба, которая работает в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="31bcc-185">This is because Service Fabric Explorer is just another service that runs in hello cluster.</span></span>

### <a name="discover-hello-service-fabric-explorer-endpoint-for-a-remote-cluster"></a><span data-ttu-id="31bcc-186">Обнаружить конечную точку Service Fabric Explorer hello для удаленного кластера</span><span class="sxs-lookup"><span data-stu-id="31bcc-186">Discover hello Service Fabric Explorer endpoint for a remote cluster</span></span>
<span data-ttu-id="31bcc-187">tooreach обозреватель Service Fabric для данного кластера, точка веб-браузера:</span><span class="sxs-lookup"><span data-stu-id="31bcc-187">tooreach Service Fabric Explorer for a given cluster, point your browser to:</span></span>

<span data-ttu-id="31bcc-188">http://&lt;конечная_точка_кластера&gt;:19080/Explorer.</span><span class="sxs-lookup"><span data-stu-id="31bcc-188">http://&lt;your-cluster-endpoint&gt;:19080/Explorer</span></span>

<span data-ttu-id="31bcc-189">Для Azure кластеров hello полный URL-адрес доступен также в панели essentials кластера hello hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="31bcc-189">For Azure clusters, hello full URL is also available in hello cluster essentials pane of hello Azure portal.</span></span>

### <a name="connect-tooa-secure-cluster"></a><span data-ttu-id="31bcc-190">Подключите кластер безопасного tooa</span><span class="sxs-lookup"><span data-stu-id="31bcc-190">Connect tooa secure cluster</span></span>
<span data-ttu-id="31bcc-191">Можно управлять кластера Service Fabric доступа tooyour клиента с помощью сертификатов или с помощью Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="31bcc-191">You can control client access tooyour Service Fabric cluster either with certificates or using Azure Active Directory (AAD).</span></span>

<span data-ttu-id="31bcc-192">При попытке tooService tooconnect Fabric Explorer в кластере безопасный, затем в зависимости от конфигурации кластера hello последующего быть toopresent требуется сертификат клиента либо выполнить вход с помощью AAD.</span><span class="sxs-lookup"><span data-stu-id="31bcc-192">If you attempt tooconnect tooService Fabric Explorer on a secure cluster, then depending on hello cluster's configuration you'll be required toopresent a client certificate or log in using AAD.</span></span>

## <a name="next-steps"></a><span data-ttu-id="31bcc-193">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="31bcc-193">Next steps</span></span>
* [<span data-ttu-id="31bcc-194">Обзор Testability</span><span class="sxs-lookup"><span data-stu-id="31bcc-194">Testability overview</span></span>](service-fabric-testability-overview.md)
* [<span data-ttu-id="31bcc-195">Управление приложениями Service Fabric в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="31bcc-195">Managing your Service Fabric applications in Visual Studio</span></span>](service-fabric-manage-application-in-visual-studio.md)
* [<span data-ttu-id="31bcc-196">Развертывание приложений Service Fabric с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="31bcc-196">Service Fabric application deployment using PowerShell</span></span>](service-fabric-deploy-remove-applications.md)

<!--Image references-->
[sfx-cluster-dashboard]: ./media/service-fabric-visualizing-your-cluster/SfxClusterDashboard.png
[sfx-cluster-map]: ./media/service-fabric-visualizing-your-cluster/SfxClusterMap.png
[sfx-application-tree]: ./media/service-fabric-visualizing-your-cluster/SfxApplicationTree.png
[sfx-service-essentials]: ./media/service-fabric-visualizing-your-cluster/SfxServiceEssentials.png
[sfx-delete-application]: ./media/service-fabric-visualizing-your-cluster/SfxDeleteApplication.png
[sfx-create-app-instance]: ./media/service-fabric-visualizing-your-cluster/SfxCreateAppInstance.png
