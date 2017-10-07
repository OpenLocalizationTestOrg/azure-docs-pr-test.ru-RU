---
title: "aaaDeploy tooa приложения Azure Service Fabric стороны кластера | Документы Microsoft"
description: "Узнайте, как кластер стороны toodeploy tooa приложения."
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: msfussell
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/09/2017
ms.author: mikhegn
ms.openlocfilehash: db16b6418fa2533ed915c8b6e612b7a8e7311bed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-application-tooa-party-cluster-in-azure"></a><span data-ttu-id="58364-103">Развертывание приложения tooa стороной кластер в Azure</span><span class="sxs-lookup"><span data-stu-id="58364-103">Deploy an application tooa Party Cluster in Azure</span></span>
<span data-ttu-id="58364-104">Этот учебник входит два ряда и показано, как toodeploy tooa приложения Azure Service Fabric стороны кластер в Azure.</span><span class="sxs-lookup"><span data-stu-id="58364-104">This tutorial is part two of a series and shows you how toodeploy an Azure Service Fabric application tooa Party Cluster in Azure.</span></span>

<span data-ttu-id="58364-105">Во второй части учебника ряда hello, вы узнаете, как:</span><span class="sxs-lookup"><span data-stu-id="58364-105">In part two of hello tutorial series, you learn how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="58364-106">Развертывание приложения tooa удаленного кластера с помощью Visual Studio</span><span class="sxs-lookup"><span data-stu-id="58364-106">Deploy an application tooa remote cluster using Visual Studio</span></span>
> * <span data-ttu-id="58364-107">Удаление приложения из кластера с помощью Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="58364-107">Remove an application from a cluster using Service Fabric Explorer</span></span>

<span data-ttu-id="58364-108">Из этого цикла руководств вы узнаете, как выполнять такие задачи:</span><span class="sxs-lookup"><span data-stu-id="58364-108">In this tutorial series you learn how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="58364-109">[Создание приложения .NET Service Fabric](service-fabric-tutorial-create-dotnet-app.md).</span><span class="sxs-lookup"><span data-stu-id="58364-109">[Build a .NET Service Fabric application](service-fabric-tutorial-create-dotnet-app.md)</span></span>
> * <span data-ttu-id="58364-110">Развертывание кластера удаленного tooa приложения hello</span><span class="sxs-lookup"><span data-stu-id="58364-110">Deploy hello application tooa remote cluster</span></span>
> * <span data-ttu-id="58364-111">[Настройка непрерывной интеграции и непрерывного развертывания с помощью Visual Studio Team Services](service-fabric-tutorial-deploy-app-with-cicd-vsts.md).</span><span class="sxs-lookup"><span data-stu-id="58364-111">[Configure CI/CD using Visual Studio Team Services](service-fabric-tutorial-deploy-app-with-cicd-vsts.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="58364-112">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="58364-112">Prerequisites</span></span>
<span data-ttu-id="58364-113">Перед началом работы с этим руководством выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="58364-113">Before you begin this tutorial:</span></span>
- <span data-ttu-id="58364-114">Если у вас еще нет подписки Azure, создайте [бесплатную учетную запись](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="58364-114">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)</span></span>
- <span data-ttu-id="58364-115">[Установка Visual Studio 2017 г](https://www.visualstudio.com/) и установить hello **разработки Azure** и **ASP.NET и веб-разработки** рабочих нагрузок.</span><span class="sxs-lookup"><span data-stu-id="58364-115">[Install Visual Studio 2017](https://www.visualstudio.com/) and install hello **Azure development** and **ASP.NET and web development** workloads.</span></span>
- [<span data-ttu-id="58364-116">Установите пакет Service Fabric SDK hello</span><span class="sxs-lookup"><span data-stu-id="58364-116">Install hello Service Fabric SDK</span></span>](service-fabric-get-started.md)

## <a name="download-hello-voting-sample-application"></a><span data-ttu-id="58364-117">Загрузите пример приложения hello голосование</span><span class="sxs-lookup"><span data-stu-id="58364-117">Download hello Voting sample application</span></span>
<span data-ttu-id="58364-118">Если вы не сборку пример приложения hello голосование в [часть одного из этого учебника ряда](service-fabric-tutorial-create-dotnet-app.md), вы можете загрузить ее.</span><span class="sxs-lookup"><span data-stu-id="58364-118">If you did not build hello Voting sample application in [part one of this tutorial series](service-fabric-tutorial-create-dotnet-app.md), you can download it.</span></span> <span data-ttu-id="58364-119">В окне командной строки запустите hello, следующая команда tooclone hello образец приложения репозитория tooyour локального компьютера.</span><span class="sxs-lookup"><span data-stu-id="58364-119">In a command window, run hello following command tooclone hello sample app repository tooyour local machine.</span></span>

```
git clone https://github.com/Azure-Samples/service-fabric-dotnet-quickstart
```

## <a name="set-up-a-party-cluster"></a><span data-ttu-id="58364-120">Настройка кластера сообщества</span><span class="sxs-lookup"><span data-stu-id="58364-120">Set up a Party Cluster</span></span>
<span data-ttu-id="58364-121">Кластеры, стороннего производителя, бесплатные, ограничено по времени кластеров Service Fabric размещаются в Azure и выполняются командой Service Fabric hello, где любой пользователь может развертывать приложения и Дополнительные сведения о платформе hello.</span><span class="sxs-lookup"><span data-stu-id="58364-121">Party clusters are free, limited-time Service Fabric clusters hosted on Azure and run by hello Service Fabric team where anyone can deploy applications and learn about hello platform.</span></span> <span data-ttu-id="58364-122">Бесплатно!</span><span class="sxs-lookup"><span data-stu-id="58364-122">For free!</span></span>

<span data-ttu-id="58364-123">tooa доступа tooget кластера стороны Обзор узла toothis: http://aka.ms/tryservicefabric и следовать hello инструкции tooget tooa кластера доступа.</span><span class="sxs-lookup"><span data-stu-id="58364-123">tooget access tooa Party Cluster, browse toothis site: http://aka.ms/tryservicefabric and follow hello instructions tooget access tooa cluster.</span></span> <span data-ttu-id="58364-124">Вы должны Facebook или GitHub учетной записи tooget доступа tooa стороной кластера.</span><span class="sxs-lookup"><span data-stu-id="58364-124">You need a Facebook or GitHub account tooget access tooa Party Cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="58364-125">Кластеры стороннего производителя не защищены, поэтому ваши приложения и все данные, помещенные в них может быть видимым tooothers.</span><span class="sxs-lookup"><span data-stu-id="58364-125">Party clusters are not secured, so your applications and any data you put in them may be visible tooothers.</span></span> <span data-ttu-id="58364-126">Не используется развертывание никаких действий не требуется предоставить другим пользователям toosee.</span><span class="sxs-lookup"><span data-stu-id="58364-126">Don't deploy anything you don't want others toosee.</span></span> <span data-ttu-id="58364-127">Убедиться, что tooread быть через условия использования подробности hello.</span><span class="sxs-lookup"><span data-stu-id="58364-127">Be sure tooread over our Terms of Use for all hello details.</span></span>

## <a name="configure-hello-listening-port"></a><span data-ttu-id="58364-128">Настройка hello прослушивающий порт</span><span class="sxs-lookup"><span data-stu-id="58364-128">Configure hello listening port</span></span>
<span data-ttu-id="58364-129">При создании hello VotingWeb клиентской службы Visual Studio случайным образом выбирает на порт для службы toolisten hello.</span><span class="sxs-lookup"><span data-stu-id="58364-129">When hello VotingWeb front-end service is created, Visual Studio randomly selects a port for hello service toolisten on.</span></span>  <span data-ttu-id="58364-130">Hello службы VotingWeb выступает в качестве интерфейса для этого приложения hello и принимает внешнего трафика, так что давайте привязать, tooa службы фиксированной и хорошо знать порт.</span><span class="sxs-lookup"><span data-stu-id="58364-130">hello VotingWeb service acts as hello front-end for this application and accepts external traffic, so let's bind that service tooa fixed and well-know port.</span></span> <span data-ttu-id="58364-131">В обозревателе решений откройте файл *VotingWeb/PackageRoot/ServiceManifest.xml*.</span><span class="sxs-lookup"><span data-stu-id="58364-131">In Solution Explorer, open  *VotingWeb/PackageRoot/ServiceManifest.xml*.</span></span>  <span data-ttu-id="58364-132">Найти hello **конечной точки** ресурса в hello **ресурсов** и измените hello **порт** too80 значение.</span><span class="sxs-lookup"><span data-stu-id="58364-132">Find hello **Endpoint** resource in hello **Resources** section and change hello **Port** value too80.</span></span>

```xml
<Resources>
    <Endpoints>
      <!-- This endpoint is used by hello communication listener tooobtain hello port on which too
           listen. Please note that if your service is partitioned, this port is shared with 
           replicas of different partitions that are placed in your code. -->
      <Endpoint Protocol="http" Name="ServiceEndpoint" Type="Input" Port="80" />
    </Endpoints>
  </Resources>
```

<span data-ttu-id="58364-133">Также можно обновите значение свойства URL-адрес приложения hello в проекте голосование hello, веб-браузере откроется правильный порт toohello при отладке с помощью «F5».</span><span class="sxs-lookup"><span data-stu-id="58364-133">Also update hello Application URL property value in hello Voting project so a web browser opens toohello correct port when you debug using 'F5'.</span></span>  <span data-ttu-id="58364-134">В обозревателе решений выберите hello **Голосование** проекте и обновите hello **URL-адрес приложения** свойство.</span><span class="sxs-lookup"><span data-stu-id="58364-134">In Solution Explorer, select hello **Voting** project and update hello **Application URL** property.</span></span>

![URL-адрес приложения](./media/service-fabric-tutorial-deploy-app-to-party-cluster/application-url.png)

## <a name="deploy-hello-app-toohello-azure"></a><span data-ttu-id="58364-136">Развертывание приложения hello toohello Azure</span><span class="sxs-lookup"><span data-stu-id="58364-136">Deploy hello app toohello Azure</span></span>
<span data-ttu-id="58364-137">Теперь, когда приложение hello готов, его можно развернуть toohello стороной кластера прямой из Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="58364-137">Now that hello application is ready, you can deploy it toohello Party Cluster direct from Visual Studio.</span></span>

1. <span data-ttu-id="58364-138">Щелкните правой кнопкой мыши **Голосование** в hello в обозревателе решений и выберите **публикации**.</span><span class="sxs-lookup"><span data-stu-id="58364-138">Right-click **Voting** in hello Solution Explorer and choose **Publish**.</span></span>

    ![Диалоговое окно "Опубликовать"](./media/service-fabric-tutorial-deploy-app-to-party-cluster/publish-app.png)

2. <span data-ttu-id="58364-140">Тип в hello конечной точки подключения hello стороны кластера в hello **конечной точки подключения** поле и нажмите кнопку **публикации**.</span><span class="sxs-lookup"><span data-stu-id="58364-140">Type in hello Connection Endpoint of hello Party Cluster in hello **Connection Endpoint** field and click **Publish**.</span></span>

    <span data-ttu-id="58364-141">После публикации hello есть закончилась, должен быть доступ toosend приложении toohello запрос через браузер.</span><span class="sxs-lookup"><span data-stu-id="58364-141">Once hello publish has finished, you should be able toosend a request toohello application via a browser.</span></span>

3. <span data-ttu-id="58364-142">Откройте предпочтительный браузера и введите адрес кластера hello (hello конечной точкой соединения без сведения о порте hello - например, win1kw5649s.westus.cloudapp.azure.com).</span><span class="sxs-lookup"><span data-stu-id="58364-142">Open you preferred browser and type in hello cluster address (hello connection endpoint without hello port information - for example, win1kw5649s.westus.cloudapp.azure.com).</span></span>

    <span data-ttu-id="58364-143">Теперь вы увидите hello же результат, как вы видели, когда запущено приложение hello локально.</span><span class="sxs-lookup"><span data-stu-id="58364-143">You should now see hello same result as you saw when running hello application locally.</span></span>

    ![Ответ API из кластера](./media/service-fabric-tutorial-deploy-app-to-party-cluster/response-from-cluster.png)

## <a name="remove-hello-application-from-a-cluster-using-service-fabric-explorer"></a><span data-ttu-id="58364-145">Удаление приложения hello из кластера с помощью Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="58364-145">Remove hello application from a cluster using Service Fabric Explorer</span></span>
<span data-ttu-id="58364-146">Обозреватель Service Fabric является tooexplore графического пользовательского интерфейса приложений и управление ими в кластере Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="58364-146">Service Fabric Explorer is a graphical user interface tooexplore and manage applications in a Service Fabric cluster.</span></span>

<span data-ttu-id="58364-147">приложение hello tooremove из hello стороны кластера:</span><span class="sxs-lookup"><span data-stu-id="58364-147">tooremove hello application from hello Party Cluster:</span></span>

1. <span data-ttu-id="58364-148">Обзор toohello Service Fabric Explorer с помощью ссылки hello, предоставляемые hello стороны кластера "Регистрация".</span><span class="sxs-lookup"><span data-stu-id="58364-148">Browse toohello Service Fabric Explorer, using hello link provided by hello Party Cluster sign-up page.</span></span> <span data-ttu-id="58364-149">Например, http://win1kw5649s.westus.cloudapp.azure.com:19080/Explorer/index.html.</span><span class="sxs-lookup"><span data-stu-id="58364-149">For example, http://win1kw5649s.westus.cloudapp.azure.com:19080/Explorer/index.html.</span></span>

2. <span data-ttu-id="58364-150">В Service Fabric Explorer перейдите toohello **fabric://Voting** узел в treeview hello hello левой стороны.</span><span class="sxs-lookup"><span data-stu-id="58364-150">In Service Fabric Explorer, navigate toohello **fabric://Voting** node in hello treeview on hello left-hand side.</span></span>

3. <span data-ttu-id="58364-151">Нажмите кнопку hello **действия** кнопку в правом hello **Essentials** области и выберите **удалить приложение**.</span><span class="sxs-lookup"><span data-stu-id="58364-151">Click hello **Action** button in hello right-hand **Essentials** pane, and choose **Delete Application**.</span></span> <span data-ttu-id="58364-152">Подтвердите удаление экземпляра приложения hello, которая удаляет экземпляр hello нашей приложение, работающее в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="58364-152">Confirm deleting hello application instance, which removes hello instance of our application running in hello cluster.</span></span>

![Удаление приложения в Service Fabric Explorer](./media/service-fabric-tutorial-deploy-app-to-party-cluster/delete-application.png)

## <a name="remove-hello-application-type-from-a-cluster-using-service-fabric-explorer"></a><span data-ttu-id="58364-154">Удаление типа приложения hello из кластера с помощью Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="58364-154">Remove hello application type from a cluster using Service Fabric Explorer</span></span>
<span data-ttu-id="58364-155">Приложения развертываются как типы приложений в кластере Service Fabric, который позволяет вам toohave нескольких экземпляров и версий приложения hello, запущенного в рамках кластера hello.</span><span class="sxs-lookup"><span data-stu-id="58364-155">Applications are deployed as application types in a Service Fabric cluster, which enables you toohave multiple instances and versions of hello application running within hello cluster.</span></span> <span data-ttu-id="58364-156">После удаления запущен экземпляр приложения hello, мы можем удалить тип hello, очистка hello toocomplete hello развертывания.</span><span class="sxs-lookup"><span data-stu-id="58364-156">After having removed hello running instance of our application, we can also remove hello type, toocomplete hello cleanup of hello deployment.</span></span>

<span data-ttu-id="58364-157">Дополнительные сведения о модели приложения hello в Service Fabric см. в разделе [модели приложения в Service Fabric](service-fabric-application-model.md).</span><span class="sxs-lookup"><span data-stu-id="58364-157">For more information about hello application model in Service Fabric, see [Model an application in Service Fabric](service-fabric-application-model.md).</span></span>

1. <span data-ttu-id="58364-158">Перейдите toohello **VotingType** узел в hello treeview.</span><span class="sxs-lookup"><span data-stu-id="58364-158">Navigate toohello **VotingType** node in hello treeview.</span></span>

2. <span data-ttu-id="58364-159">Щелкните hello **действия** кнопку в правом hello **Essentials** области и выберите **наполнение типа**.</span><span class="sxs-lookup"><span data-stu-id="58364-159">Click hello **Action** button in hello right-hand **Essentials** pane, and choose **Unprovision Type**.</span></span> <span data-ttu-id="58364-160">Подтвердите Отмена подготовки типа приложения hello.</span><span class="sxs-lookup"><span data-stu-id="58364-160">Confirm unprovisioning hello application type.</span></span>

![Отмена подготовки типа приложения в Service Fabric Explorer](./media/service-fabric-tutorial-deploy-app-to-party-cluster/unprovision-type.png)

<span data-ttu-id="58364-162">Это заключительный шаг учебника hello.</span><span class="sxs-lookup"><span data-stu-id="58364-162">This concludes hello tutorial.</span></span>

## <a name="next-steps"></a><span data-ttu-id="58364-163">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="58364-163">Next steps</span></span>
<span data-ttu-id="58364-164">Из этого руководства вы узнали, как выполнять такие задачи:</span><span class="sxs-lookup"><span data-stu-id="58364-164">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="58364-165">Развертывание приложения tooa удаленного кластера с помощью Visual Studio</span><span class="sxs-lookup"><span data-stu-id="58364-165">Deploy an application tooa remote cluster using Visual Studio</span></span>
> * <span data-ttu-id="58364-166">Удаление приложения из кластера с помощью Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="58364-166">Remove an application from a cluster using Service Fabric Explorer</span></span>

<span data-ttu-id="58364-167">Предварительное toohello Далее учебник.</span><span class="sxs-lookup"><span data-stu-id="58364-167">Advance toohello next tutorial:</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="58364-168">Настройка непрерывной интеграции с Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="58364-168">Set up continuous integration using Visual Studio Team Services</span></span>](service-fabric-tutorial-deploy-app-with-cicd-vsts.md)