---
title: "aaaManage приложений в Visual Studio | Документы Microsoft"
description: "Используйте Visual Studio toocreate, разработать пакет, развертывания и отладки Service Fabric приложений и служб."
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: timlt
editor: 
ms.assetid: c317cb7e-7eae-466e-ba41-6aa2518be5cf
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/07/2017
ms.author: mikkelhegn
ms.openlocfilehash: b2d5803d85e4f9645dcbece33a2208bc0955498d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-visual-studio-toosimplify-writing-and-managing-your-service-fabric-applications"></a><span data-ttu-id="6bb51-103">Используйте Visual Studio toosimplify записи и управления приложениями Service Fabric</span><span class="sxs-lookup"><span data-stu-id="6bb51-103">Use Visual Studio toosimplify writing and managing your Service Fabric applications</span></span>
<span data-ttu-id="6bb51-104">Вы можете управлять приложениями и службами Azure Service Fabric с помощью Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6bb51-104">You can manage your Azure Service Fabric applications and services through Visual Studio.</span></span> <span data-ttu-id="6bb51-105">После [Настройка среды разработки](service-fabric-get-started.md), использовать приложения Service Fabric toocreate Visual Studio, добавить службы или пакета, регистр и развертывания приложений в к локальному кластеру разработки.</span><span class="sxs-lookup"><span data-stu-id="6bb51-105">Once you've [set up your development environment](service-fabric-get-started.md), you can use Visual Studio toocreate Service Fabric applications, add services, or package, register, and deploy applications in your local development cluster.</span></span>

## <a name="deploy-your-service-fabric-application"></a><span data-ttu-id="6bb51-106">Развертывание приложения Service Fabric</span><span class="sxs-lookup"><span data-stu-id="6bb51-106">Deploy your Service Fabric application</span></span>
<span data-ttu-id="6bb51-107">По умолчанию развертывание приложения объединяет hello, выполните действия в одной простой операции:</span><span class="sxs-lookup"><span data-stu-id="6bb51-107">By default, deploying an application combines hello following steps into one simple operation:</span></span>

1. <span data-ttu-id="6bb51-108">Создание пакета приложения hello</span><span class="sxs-lookup"><span data-stu-id="6bb51-108">Creating hello application package</span></span>
2. <span data-ttu-id="6bb51-109">Отправка хранилища образов toohello пакета приложения hello</span><span class="sxs-lookup"><span data-stu-id="6bb51-109">Uploading hello application package toohello image store</span></span>
3. <span data-ttu-id="6bb51-110">Регистрация типа приложения hello</span><span class="sxs-lookup"><span data-stu-id="6bb51-110">Registering hello application type</span></span>
4. <span data-ttu-id="6bb51-111">Удаление любых запущенных экземпляров приложения.</span><span class="sxs-lookup"><span data-stu-id="6bb51-111">Removing any running application instances</span></span>
5. <span data-ttu-id="6bb51-112">Создание экземпляра приложения</span><span class="sxs-lookup"><span data-stu-id="6bb51-112">Creating an application instance</span></span>

<span data-ttu-id="6bb51-113">В Visual Studio нажав клавишу **F5** развертывает приложения и присоединения экземпляров приложения tooall hello отладчика.</span><span class="sxs-lookup"><span data-stu-id="6bb51-113">In Visual Studio, pressing **F5** deploys your application and attach hello debugger tooall application instances.</span></span> <span data-ttu-id="6bb51-114">Можно использовать **Ctrl + F5** toodeploy приложение без отладки, или вы можете опубликовать tooa локального или удаленного кластера с помощью hello профиль публикации.</span><span class="sxs-lookup"><span data-stu-id="6bb51-114">You can use **Ctrl+F5** toodeploy an application without debugging, or you can publish tooa local or remote cluster by using hello publish profile.</span></span> <span data-ttu-id="6bb51-115">Дополнительные сведения см. в разделе [публикации удаленного кластера tooa приложений с помощью Visual Studio](service-fabric-publish-app-remote-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="6bb51-115">For more information, see [Publish an application tooa remote cluster by using Visual Studio](service-fabric-publish-app-remote-cluster.md).</span></span>

### <a name="application-debug-mode"></a><span data-ttu-id="6bb51-116">Режим отладки приложения</span><span class="sxs-lookup"><span data-stu-id="6bb51-116">Application Debug Mode</span></span>
<span data-ttu-id="6bb51-117">Visual Studio предоставляет свойство с именем **режим отладки приложения**, который управляет способ развертывания приложения toohandle Visual входящим в процессе отладки.</span><span class="sxs-lookup"><span data-stu-id="6bb51-117">Visual Studio provide a property called **Application Debug Mode**, which controls how you want Visual Studios toohandle Application deployment as part of debugging.</span></span>

#### <a name="tooset-hello-application-debug-mode-property"></a><span data-ttu-id="6bb51-118">hello tooset свойство режима отладки приложения</span><span class="sxs-lookup"><span data-stu-id="6bb51-118">tooset hello Application Debug Mode property</span></span>
1. <span data-ttu-id="6bb51-119">На hello Service Fabric проекта приложения (*.sfproj) контекстное меню, выберите **свойства** (или нажмите клавишу hello **F4** ключа).</span><span class="sxs-lookup"><span data-stu-id="6bb51-119">On hello Service Fabric application project's (*.sfproj) shortcut menu, choose **Properties** (or press hello **F4** key).</span></span>
2. <span data-ttu-id="6bb51-120">В hello **свойства** окна, набор hello **режим отладки приложения** свойство.</span><span class="sxs-lookup"><span data-stu-id="6bb51-120">In hello **Properties** window, set hello **Application Debug Mode** property.</span></span>

![Настройка свойства "Режим отладки приложения"][debugmodeproperty]

#### <a name="application-debug-modes"></a><span data-ttu-id="6bb51-122">Режимы отладки приложения</span><span class="sxs-lookup"><span data-stu-id="6bb51-122">Application Debug Modes</span></span>

1. <span data-ttu-id="6bb51-123">**Обновление приложения** этот режим позволяет изменить tooquickly и отладка кода и поддерживает редактирование статического веб-файлов во время отладки.</span><span class="sxs-lookup"><span data-stu-id="6bb51-123">**Refresh Application** This mode enables you tooquickly change and debug your code and supports editing static web files while debugging.</span></span> <span data-ttu-id="6bb51-124">Этот режим работает, только если локальный кластер разработки находится в [режиме с 1 узлом](/service-fabric-get-started-with-a-local-cluster.md#one-node-and-five-node-cluster-mode).</span><span class="sxs-lookup"><span data-stu-id="6bb51-124">This mode only works if your local development cluster is in [1-Node mode](/service-fabric-get-started-with-a-local-cluster.md#one-node-and-five-node-cluster-mode).</span></span>
2. <span data-ttu-id="6bb51-125">**Удалить приложение** причины hello toobe приложения удаляются при завершении сеанса отладки hello.</span><span class="sxs-lookup"><span data-stu-id="6bb51-125">**Remove Application** causes hello application toobe removed when hello debug session ends.</span></span>
3. <span data-ttu-id="6bb51-126">**Автоматическое обновление** hello приложения по-прежнему toorun при завершении сеанса отладки hello.</span><span class="sxs-lookup"><span data-stu-id="6bb51-126">**Auto Upgrade** hello application continues toorun when hello debug session ends.</span></span> <span data-ttu-id="6bb51-127">Hello следующего сеанса отладки будет считать hello развертывания обновления.</span><span class="sxs-lookup"><span data-stu-id="6bb51-127">hello next debug session will treat hello deployment as an upgrade.</span></span> <span data-ttu-id="6bb51-128">Hello процесс обновления сохраняет все данные, введенные в предыдущем сеансе отладки.</span><span class="sxs-lookup"><span data-stu-id="6bb51-128">hello upgrade process preserves any data that you entered in a previous debug session.</span></span>
4. <span data-ttu-id="6bb51-129">**Оставьте приложение** сохраняет приложения hello, работающих в кластере hello, когда hello отладки окончания сеанса.</span><span class="sxs-lookup"><span data-stu-id="6bb51-129">**Keep Application** hello application keeps running in hello cluster when hello debug session ends.</span></span> <span data-ttu-id="6bb51-130">Hello начала hello следующего сеанса отладки, приложение hello будет удалено.</span><span class="sxs-lookup"><span data-stu-id="6bb51-130">At hello beginning of hello next debug session, hello application will be removed.</span></span>

<span data-ttu-id="6bb51-131">Для **автоматическое обновление** данные сохраняются, применяя возможности обновления приложения hello структуры службы.</span><span class="sxs-lookup"><span data-stu-id="6bb51-131">For **Auto Upgrade** data is preserved by applying hello application upgrade capabilities of Service Fabric.</span></span> <span data-ttu-id="6bb51-132">Дополнительные сведения об обновлении приложений и выполнении обновления в реальной среде см. в статье [Обновление приложения Service Fabric](service-fabric-application-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="6bb51-132">For more information about upgrading applications and how you might perform an upgrade in a real environment, see [Service Fabric application upgrade](service-fabric-application-upgrade.md).</span></span>

## <a name="add-a-service-tooyour-service-fabric-application"></a><span data-ttu-id="6bb51-133">Добавление службы tooyour приложения Service Fabric</span><span class="sxs-lookup"><span data-stu-id="6bb51-133">Add a service tooyour Service Fabric application</span></span>
<span data-ttu-id="6bb51-134">Его функциональность можно добавить новый tooextend приложения tooyour служб.</span><span class="sxs-lookup"><span data-stu-id="6bb51-134">You can add new services tooyour application tooextend its functionality.</span></span>  <span data-ttu-id="6bb51-135">tooensure, что служба hello включена в пакет приложения, добавить службу hello через hello **новый Service Fabric...**  элемента меню.</span><span class="sxs-lookup"><span data-stu-id="6bb51-135">tooensure that hello service is included in your application package, add hello service through hello **New Fabric Service...** menu item.</span></span>

![Добавление новой службы Service Fabric][newservice]

<span data-ttu-id="6bb51-137">Выберите приложение Service Fabric проекта типа tooadd tooyour и укажите имя для службы hello.</span><span class="sxs-lookup"><span data-stu-id="6bb51-137">Select a Service Fabric project type tooadd tooyour application, and specify a name for hello service.</span></span>  <span data-ttu-id="6bb51-138">В разделе [выборе платформы для службы](service-fabric-choose-framework.md) toohelp, решите, какие службы введите toouse.</span><span class="sxs-lookup"><span data-stu-id="6bb51-138">See [Choosing a framework for your service](service-fabric-choose-framework.md) toohelp you decide which service type toouse.</span></span>

![Выберите приложение Service Fabric тип проекта службы tooadd tooyour][addserviceproject]

<span data-ttu-id="6bb51-140">Новая служба Hello добавляется решение tooyour и существующий пакет приложения.</span><span class="sxs-lookup"><span data-stu-id="6bb51-140">hello new service is added tooyour solution and existing application package.</span></span> <span data-ttu-id="6bb51-141">ссылки на службу Hello и экземпляра службы по умолчанию будут добавлены toohello манифест приложения, вызывающие toobe hello службы создается и запускается hello в следующий раз при развертывании приложения hello.</span><span class="sxs-lookup"><span data-stu-id="6bb51-141">hello service references and a default service instance will be added toohello application manifest, causing hello service toobe created and started hello next time you deploy hello application.</span></span>

![Новая служба Hello добавляется tooyour манифест приложения][newserviceapplicationmanifest]

## <a name="package-your-service-fabric-application"></a><span data-ttu-id="6bb51-143">Создание пакета приложения Service Fabric</span><span class="sxs-lookup"><span data-stu-id="6bb51-143">Package your Service Fabric application</span></span>
<span data-ttu-id="6bb51-144">toodeploy приложения hello и ее служб tooa кластер, необходимо toocreate пакета приложения.</span><span class="sxs-lookup"><span data-stu-id="6bb51-144">toodeploy hello application and its services tooa cluster, you need toocreate an application package.</span></span>  <span data-ttu-id="6bb51-145">пакет Hello организует манифест приложения hello, манифесты службы и другие необходимые файлы в определенном формате.</span><span class="sxs-lookup"><span data-stu-id="6bb51-145">hello package organizes hello application manifest, service manifests, and other necessary files in a specific layout.</span></span>  <span data-ttu-id="6bb51-146">Visual Studio настраивает и управляет hello пакета в папку проекта приложения hello, в каталоге «pkg» hello.</span><span class="sxs-lookup"><span data-stu-id="6bb51-146">Visual Studio sets up and manages hello package in hello application project's folder, in hello 'pkg' directory.</span></span>  <span data-ttu-id="6bb51-147">Щелкнув **пакета** из hello **приложения** создает контекстного меню или обновления hello пакета приложения.</span><span class="sxs-lookup"><span data-stu-id="6bb51-147">Clicking **Package** from hello **Application** context menu creates or updates hello application package.</span></span>

## <a name="remove-applications-and-application-types-using-cloud-explorer"></a><span data-ttu-id="6bb51-148">Удаление приложений и типов приложений с использованием Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="6bb51-148">Remove applications and application types using Cloud Explorer</span></span>
<span data-ttu-id="6bb51-149">Можно выполнять операции управления базовый кластер из среды Visual Studio с помощью Cloud Explorer, который можно открыть из hello **представление** меню.</span><span class="sxs-lookup"><span data-stu-id="6bb51-149">You can perform basic cluster management operations from within Visual Studio using Cloud Explorer, which you can launch from hello **View** menu.</span></span> <span data-ttu-id="6bb51-150">Например, вы можете удалить приложения и отменить подготовку типов приложений на локальном или удаленном кластерах.</span><span class="sxs-lookup"><span data-stu-id="6bb51-150">For instance, you can delete applications and unprovision application types on local or remote clusters.</span></span>

![Удаление приложения][removeapplication]

> [!TIP]
> <span data-ttu-id="6bb51-152">Сведения о расширенных функциях управления кластером см. в статье [Визуализация кластера с помощью Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="6bb51-152">For richer cluster management functionality, see [Visualizing your cluster with Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>
>
>

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="6bb51-153">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6bb51-153">Next steps</span></span>
* [<span data-ttu-id="6bb51-154">Модель приложений Service Fabric</span><span class="sxs-lookup"><span data-stu-id="6bb51-154">Service Fabric application model</span></span>](service-fabric-application-model.md)
* [<span data-ttu-id="6bb51-155">Развертывание приложений Service Fabric</span><span class="sxs-lookup"><span data-stu-id="6bb51-155">Service Fabric application deployment</span></span>](service-fabric-deploy-remove-applications.md)
* [<span data-ttu-id="6bb51-156">Управление параметрами приложения для нескольких сред</span><span class="sxs-lookup"><span data-stu-id="6bb51-156">Managing application parameters for multiple environments</span></span>](service-fabric-manage-multiple-environment-app-configuration.md)
* [<span data-ttu-id="6bb51-157">Отладка приложений Service Fabric</span><span class="sxs-lookup"><span data-stu-id="6bb51-157">Debugging your Service Fabric application</span></span>](service-fabric-debugging-your-application.md)
* [<span data-ttu-id="6bb51-158">Визуализация кластера с помощью обозревателя Service Fabric</span><span class="sxs-lookup"><span data-stu-id="6bb51-158">Visualizing your cluster by using Service Fabric Explorer</span></span>](service-fabric-visualizing-your-cluster.md)

<!--Image references-->
[addserviceproject]:./media/service-fabric-manage-application-in-visual-studio/addserviceproject.png
[manageservicefabric]: ./media/service-fabric-manage-application-in-visual-studio/manageservicefabric.png
[newservice]:./media/service-fabric-manage-application-in-visual-studio/newservice.png
[newserviceapplicationmanifest]:./media/service-fabric-manage-application-in-visual-studio/newserviceapplicationmanifest.png
[debugmodeproperty]:./media/service-fabric-manage-application-in-visual-studio/debugmodeproperty.png
[removeapplication]:./media/service-fabric-manage-application-in-visual-studio/removeapplication.png