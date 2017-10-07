---
title: "aaaQuickly развернуть существующий кластер Azure Service Fabric tooan приложения"
description: "Использование Azure Service Fabric кластера toohost существующего приложения Node.js в Visual Studio."
services: service-fabric
documentationcenter: nodejs
author: thraka
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/13/2017
ms.author: adegeo
ms.openlocfilehash: 20a3eb4a9206ba465acf96d0976ba241b07158bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="host-a-nodejs-application-on-azure-service-fabric"></a><span data-ttu-id="6d67b-103">Размещение приложения Node.js в Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="6d67b-103">Host a Node.js application on Azure Service Fabric</span></span>

<span data-ttu-id="6d67b-104">Это краткое руководство поможет вам развернуть кластер Service Fabric существующего приложения (Node.js в этом примере) tooa работает в Azure.</span><span class="sxs-lookup"><span data-stu-id="6d67b-104">This quickstart helps you deploy an existing application (Node.js in this example) tooa Service Fabric cluster running on Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6d67b-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="6d67b-105">Prerequisites</span></span>

<span data-ttu-id="6d67b-106">Перед началом работы [настройте среду разработки](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="6d67b-106">Before you get started, make sure that you have [set up your development environment](service-fabric-get-started.md).</span></span> <span data-ttu-id="6d67b-107">В том числе установка hello Service Fabric SDK и Visual Studio 2017 г. или 2015 г.</span><span class="sxs-lookup"><span data-stu-id="6d67b-107">Which includes installing hello Service Fabric SDK and Visual Studio 2017 or 2015.</span></span>

<span data-ttu-id="6d67b-108">Необходимо также toohave существующее приложение Node.js для развертывания.</span><span class="sxs-lookup"><span data-stu-id="6d67b-108">You also need toohave an existing Node.js application for deployment.</span></span> <span data-ttu-id="6d67b-109">В этом кратком руководстве используется простой веб-сайт Node.js, который можно загрузить [здесь][download-sample].</span><span class="sxs-lookup"><span data-stu-id="6d67b-109">This quickstart uses a simple Node.js website that can be downloaded [here][download-sample].</span></span> <span data-ttu-id="6d67b-110">Извлечь этот файл tooyour `<path-to-project>\ApplicationPackageRoot\<package-name>\Code\` папку после создания проекта hello в следующем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="6d67b-110">Extract this file tooyour `<path-to-project>\ApplicationPackageRoot\<package-name>\Code\` folder after you create hello project in hello next step.</span></span>

<span data-ttu-id="6d67b-111">Если у вас еще нет подписки Azure, [создайте бесплатную учетную запись Azure][create-account].</span><span class="sxs-lookup"><span data-stu-id="6d67b-111">If you don't have an Azure subscription, create a [free account][create-account].</span></span>

## <a name="create-hello-service"></a><span data-ttu-id="6d67b-112">Создать службу hello</span><span class="sxs-lookup"><span data-stu-id="6d67b-112">Create hello service</span></span>

<span data-ttu-id="6d67b-113">Запустите Visual Studio от имени **администратора**.</span><span class="sxs-lookup"><span data-stu-id="6d67b-113">Launch Visual Studio as an **administrator**.</span></span>

<span data-ttu-id="6d67b-114">Создайте проект, нажав клавиши `CTRL`+`SHIFT`+`N`.</span><span class="sxs-lookup"><span data-stu-id="6d67b-114">Create a project with `CTRL`+`SHIFT`+`N`</span></span>

<span data-ttu-id="6d67b-115">В hello **новый проект** диалоговое окно, выберите **облака > приложение Service Fabric**.</span><span class="sxs-lookup"><span data-stu-id="6d67b-115">In hello **New Project** dialog, choose **Cloud > Service Fabric Application**.</span></span>

<span data-ttu-id="6d67b-116">Имя приложения hello **MyGuestApp** и нажмите клавишу **ОК**.</span><span class="sxs-lookup"><span data-stu-id="6d67b-116">Name hello application **MyGuestApp** and press **OK**.</span></span>

>[!IMPORTANT]
><span data-ttu-id="6d67b-117">Node.js легко может нарушить работу 260 знаков hello для путей, которые имеет windows.</span><span class="sxs-lookup"><span data-stu-id="6d67b-117">Node.js can easily break hello 260 character limit for paths that windows has.</span></span> <span data-ttu-id="6d67b-118">Использовать короткий путь для самого hello проекта, такие как **c:\code\svc1**.</span><span class="sxs-lookup"><span data-stu-id="6d67b-118">Use a short path for hello project itself such as **c:\code\svc1**.</span></span>
   
![Диалоговое окно "Новый проект" в Visual Studio][new-project]

<span data-ttu-id="6d67b-120">В следующем диалоговом окне приветствия, можно создать любой тип службы Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="6d67b-120">You can create any type of Service Fabric service from hello next dialog.</span></span> <span data-ttu-id="6d67b-121">В рамках этого краткого руководства выберите **Гостевой исполняемый файл**.</span><span class="sxs-lookup"><span data-stu-id="6d67b-121">For this quickstart, choose **Guest Executable**.</span></span>

<span data-ttu-id="6d67b-122">Имя службы hello **MyGuestService** и задание параметров hello на правом toohello hello следующие значения:</span><span class="sxs-lookup"><span data-stu-id="6d67b-122">Name hello service **MyGuestService** and set hello options on hello right toohello following values:</span></span>

| <span data-ttu-id="6d67b-123">Настройка</span><span class="sxs-lookup"><span data-stu-id="6d67b-123">Setting</span></span>                   | <span data-ttu-id="6d67b-124">Значение</span><span class="sxs-lookup"><span data-stu-id="6d67b-124">Value</span></span> |
| ------------------------- | ------ |
| <span data-ttu-id="6d67b-125">Папка пакета кода</span><span class="sxs-lookup"><span data-stu-id="6d67b-125">Code Package Folder</span></span>       | <span data-ttu-id="6d67b-126">_&lt;Папка Hello приложение Node.js&gt;_</span><span class="sxs-lookup"><span data-stu-id="6d67b-126">_&lt;hello folder with your Node.js app&gt;_</span></span> |
| <span data-ttu-id="6d67b-127">Поведение пакета кода</span><span class="sxs-lookup"><span data-stu-id="6d67b-127">Code Package Behavior</span></span>     | <span data-ttu-id="6d67b-128">Скопируйте папку tooproject содержимое</span><span class="sxs-lookup"><span data-stu-id="6d67b-128">Copy folder contents tooproject</span></span> |
| <span data-ttu-id="6d67b-129">Программа</span><span class="sxs-lookup"><span data-stu-id="6d67b-129">Program</span></span>                   | <span data-ttu-id="6d67b-130">node.exe</span><span class="sxs-lookup"><span data-stu-id="6d67b-130">node.exe</span></span> |
| <span data-ttu-id="6d67b-131">Аргументы</span><span class="sxs-lookup"><span data-stu-id="6d67b-131">Arguments</span></span>                 | <span data-ttu-id="6d67b-132">server.js</span><span class="sxs-lookup"><span data-stu-id="6d67b-132">server.js</span></span> |
| <span data-ttu-id="6d67b-133">Рабочая папка</span><span class="sxs-lookup"><span data-stu-id="6d67b-133">Working Folder</span></span>            | <span data-ttu-id="6d67b-134">CodePackage</span><span class="sxs-lookup"><span data-stu-id="6d67b-134">CodePackage</span></span> |

<span data-ttu-id="6d67b-135">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="6d67b-135">Press **OK**.</span></span>

![Диалоговое окно "Новая служба" в Visual Studio][new-service]

<span data-ttu-id="6d67b-137">Visual Studio создает проект приложения hello и проект службы субъекта hello и отображает их в обозревателе решений.</span><span class="sxs-lookup"><span data-stu-id="6d67b-137">Visual Studio creates hello application project and hello actor service project and displays them in Solution Explorer.</span></span>

<span data-ttu-id="6d67b-138">проект приложения Hello (**MyGuestApp**) содержит код напрямую.</span><span class="sxs-lookup"><span data-stu-id="6d67b-138">hello application project (**MyGuestApp**) does not contain any code directly.</span></span> <span data-ttu-id="6d67b-139">Он только ссылается на набор проектов служб.</span><span class="sxs-lookup"><span data-stu-id="6d67b-139">Instead, it references a set of service projects.</span></span> <span data-ttu-id="6d67b-140">Также он содержит данные еще трех типов.</span><span class="sxs-lookup"><span data-stu-id="6d67b-140">In addition, it contains three other types of content:</span></span>

* <span data-ttu-id="6d67b-141">**Профили публикации**</span><span class="sxs-lookup"><span data-stu-id="6d67b-141">**Publish profiles**</span></span>  
<span data-ttu-id="6d67b-142">Средства настройки для различных сред.</span><span class="sxs-lookup"><span data-stu-id="6d67b-142">Tooling preferences for different environments.</span></span>

* <span data-ttu-id="6d67b-143">**Сценарии**</span><span class="sxs-lookup"><span data-stu-id="6d67b-143">**Scripts**</span></span>  
<span data-ttu-id="6d67b-144">Сценарий PowerShell для развертывания и обновления приложения.</span><span class="sxs-lookup"><span data-stu-id="6d67b-144">PowerShell script for deploying/upgrading your application.</span></span>

* <span data-ttu-id="6d67b-145">**Определение приложения**</span><span class="sxs-lookup"><span data-stu-id="6d67b-145">**Application definition**</span></span>  
<span data-ttu-id="6d67b-146">Включает в себя манифест приложения hello под *ApplicationPackageRoot*.</span><span class="sxs-lookup"><span data-stu-id="6d67b-146">Includes hello application manifest under *ApplicationPackageRoot*.</span></span> <span data-ttu-id="6d67b-147">Файлы параметров связанного приложения находятся в *ApplicationParameters*, который определении приложения hello и позволяют tooconfigure он специально для данной среды.</span><span class="sxs-lookup"><span data-stu-id="6d67b-147">Associated application parameter files are under *ApplicationParameters*, which define hello application and allow you tooconfigure it specifically for a given environment.</span></span>
    
<span data-ttu-id="6d67b-148">Общие сведения о hello содержимое проекта службы hello. в разделе [Приступая к работе с надежного обмена](service-fabric-reliable-services-quick-start.md).</span><span class="sxs-lookup"><span data-stu-id="6d67b-148">For an overview of hello contents of hello service project, see [Getting started with Reliable Services](service-fabric-reliable-services-quick-start.md).</span></span>

## <a name="set-up-networking"></a><span data-ttu-id="6d67b-149">Настройка сети</span><span class="sxs-lookup"><span data-stu-id="6d67b-149">Set up networking</span></span>

<span data-ttu-id="6d67b-150">пример Hello, мы развертываете приложение Node.js использует порт **80** нам нужны tootell Service Fabric, нам нужно, что порт доступ.</span><span class="sxs-lookup"><span data-stu-id="6d67b-150">hello example Node.js app we're deploying uses port **80** and we need tootell Service Fabric that we need that port exposed.</span></span>

<span data-ttu-id="6d67b-151">Откройте hello **ServiceManifest.xml** файл в проекте hello.</span><span class="sxs-lookup"><span data-stu-id="6d67b-151">Open hello **ServiceManifest.xml** file in hello project.</span></span> <span data-ttu-id="6d67b-152">Внизу hello hello манифеста — `<Resources> \ <Endpoints>` с записью уже определен.</span><span class="sxs-lookup"><span data-stu-id="6d67b-152">At hello bottom of hello manifest, there is a `<Resources> \ <Endpoints>` with an entry already defined.</span></span> <span data-ttu-id="6d67b-153">Изменение этой записи tooadd `Port`, `Protocol`, и `Type`.</span><span class="sxs-lookup"><span data-stu-id="6d67b-153">Modify that entry tooadd `Port`, `Protocol`, and `Type`.</span></span> 

```xml
  <Resources>
    <Endpoints>
      <!-- This endpoint is used by hello communication listener tooobtain hello port on which too
           listen. Please note that if your service is partitioned, this port is shared with 
           replicas of different partitions that are placed in your code. -->
      <Endpoint Name="MyGuestAppServiceTypeEndpoint" Port="80" Protocol="http" Type="Input" />
    </Endpoints>
  </Resources>
```

## <a name="deploy-tooazure"></a><span data-ttu-id="6d67b-154">Развертывание tooAzure</span><span class="sxs-lookup"><span data-stu-id="6d67b-154">Deploy tooAzure</span></span>

<span data-ttu-id="6d67b-155">Если нажать клавишу **F5** и запустите проект hello, развернутых toohello локального кластера.</span><span class="sxs-lookup"><span data-stu-id="6d67b-155">If you press **F5** and run hello project, it is deployed toohello local cluster.</span></span> <span data-ttu-id="6d67b-156">Тем не менее давайте развернуть tooAzure вместо него.</span><span class="sxs-lookup"><span data-stu-id="6d67b-156">However, let's deploy tooAzure instead.</span></span>

<span data-ttu-id="6d67b-157">Правой кнопкой мыши проект hello и выберите **публикации...**  . Откроется диалоговое окно toopublish tooAzure.</span><span class="sxs-lookup"><span data-stu-id="6d67b-157">Right-click on hello project and choose **Publish...** which opens a dialog toopublish tooAzure.</span></span>

![Диалоговое окно tooazure для служба service fabric публикации][publish]

<span data-ttu-id="6d67b-159">Выберите hello **PublishProfiles\Cloud.xml** целевой профиль.</span><span class="sxs-lookup"><span data-stu-id="6d67b-159">Select hello **PublishProfiles\Cloud.xml** target profile.</span></span>

<span data-ttu-id="6d67b-160">Если вы еще не ранее, выберите toodeploy учетная запись Azure для.</span><span class="sxs-lookup"><span data-stu-id="6d67b-160">If you haven't previously, choose an Azure account toodeploy to.</span></span> <span data-ttu-id="6d67b-161">Если у вас ее нет, [зарегистрируйте ее][create-account].</span><span class="sxs-lookup"><span data-stu-id="6d67b-161">If you don't have one yet, [sign-up for one][create-account].</span></span>

<span data-ttu-id="6d67b-162">В разделе **конечной точки подключения**, выберите hello toodeploy кластера Service Fabric для.</span><span class="sxs-lookup"><span data-stu-id="6d67b-162">Under **Connection Endpoint**, select hello Service Fabric cluster toodeploy to.</span></span> <span data-ttu-id="6d67b-163">Если нет, выберите  **&lt;создать новый кластер... &gt;**  которого открывается toohello окна браузера web портал Azure.</span><span class="sxs-lookup"><span data-stu-id="6d67b-163">If you do not have one, select **&lt;Create New Cluster...&gt;** which opens up web browser window toohello Azure portal.</span></span> <span data-ttu-id="6d67b-164">Дополнительные сведения см. в разделе [создания кластера в портале hello](service-fabric-cluster-creation-via-portal.md#create-cluster-in-the-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="6d67b-164">For more information, see [create a cluster in hello portal](service-fabric-cluster-creation-via-portal.md#create-cluster-in-the-azure-portal).</span></span> 

<span data-ttu-id="6d67b-165">При создании кластера Service Fabric hello, убедитесь, что hello tooset **пользовательские конечные точки** задание слишком**80**.</span><span class="sxs-lookup"><span data-stu-id="6d67b-165">When you create hello Service Fabric cluster, make sure tooset hello **Custom endpoints** setting too**80**.</span></span>

![Конфигурация типа узла Service Fabric с настраиваемой конечной точкой][custom-endpoint]

<span data-ttu-id="6d67b-167">Создание нового кластера Service Fabric занимает некоторое время toocomplete.</span><span class="sxs-lookup"><span data-stu-id="6d67b-167">Creating a new Service Fabric cluster takes some time toocomplete.</span></span> <span data-ttu-id="6d67b-168">Если он был создан, перейдите назад toohello диалоговое окно публикации и выберите  **&lt;обновление&gt;**.</span><span class="sxs-lookup"><span data-stu-id="6d67b-168">Once it has been created, go back toohello publish dialog and select **&lt;Refresh&gt;**.</span></span> <span data-ttu-id="6d67b-169">Hello нового кластера, перечисленные в поле со списком hello; выберите его.</span><span class="sxs-lookup"><span data-stu-id="6d67b-169">hello new cluster is listed in hello drop-down box; select it.</span></span>

<span data-ttu-id="6d67b-170">Нажмите клавишу **публикации** и дождитесь toofinish развертывания hello.</span><span class="sxs-lookup"><span data-stu-id="6d67b-170">Press **Publish** and wait for hello deployment toofinish.</span></span>

<span data-ttu-id="6d67b-171">Это может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="6d67b-171">This may take a few minutes.</span></span> <span data-ttu-id="6d67b-172">После его завершения может потребоваться несколько минут для toobe приложения hello полностью доступны.</span><span class="sxs-lookup"><span data-stu-id="6d67b-172">After it completes, it may take a few more minutes for hello application toobe fully available.</span></span>

## <a name="test-hello-website"></a><span data-ttu-id="6d67b-173">Веб-сайт для тестирования hello</span><span class="sxs-lookup"><span data-stu-id="6d67b-173">Test hello website</span></span>

<span data-ttu-id="6d67b-174">После публикации службы проверьте ее в веб-браузере.</span><span class="sxs-lookup"><span data-stu-id="6d67b-174">After your service has been published, test it in a web browser.</span></span> 

<span data-ttu-id="6d67b-175">Во-первых откройте hello портал Azure и найти службу Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="6d67b-175">First, open hello Azure portal and find your Service Fabric service.</span></span>

<span data-ttu-id="6d67b-176">Проверьте колонке Обзор hello hello адреса службы.</span><span class="sxs-lookup"><span data-stu-id="6d67b-176">Check hello overview blade of hello service address.</span></span> <span data-ttu-id="6d67b-177">Используйте hello доменное имя от hello _конечной точки подключения клиента_ свойство.</span><span class="sxs-lookup"><span data-stu-id="6d67b-177">Use hello domain name from hello _Client connection endpoint_ property.</span></span> <span data-ttu-id="6d67b-178">Например, `http://mysvcfab1.westus2.cloudapp.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="6d67b-178">For example, `http://mysvcfab1.westus2.cloudapp.azure.com`.</span></span>

![Колонка Общие сведения о Service fabric на hello портал Azure][overview]

<span data-ttu-id="6d67b-180">Перейдите toothis адрес, где можно будет увидеть hello `HELLO WORLD` ответа.</span><span class="sxs-lookup"><span data-stu-id="6d67b-180">Navigate toothis address where you will see hello `HELLO WORLD` response.</span></span>

## <a name="delete-hello-cluster"></a><span data-ttu-id="6d67b-181">Удалить кластер hello</span><span class="sxs-lookup"><span data-stu-id="6d67b-181">Delete hello cluster</span></span>

<span data-ttu-id="6d67b-182">Не забудьте toodelete все ресурсы hello, созданный для краткого руководства, что и у вас взимается для этих ресурсов.</span><span class="sxs-lookup"><span data-stu-id="6d67b-182">Do not forget toodelete all of hello resources you've created for this quickstart, as you are charged for those resources.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6d67b-183">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6d67b-183">Next steps</span></span>
<span data-ttu-id="6d67b-184">Ознакомьтесь с дополнительными сведениями о [гостевых исполняемых файлах](service-fabric-deploy-existing-app.md).</span><span class="sxs-lookup"><span data-stu-id="6d67b-184">Read more about [guest executables](service-fabric-deploy-existing-app.md).</span></span>

<!-- Image References -->

[new-project]: ./media/quickstart-guest-app/new-project.png
[new-service]: ./media/quickstart-guest-app/template.png
[solution-exp]: ./media/quickstart-guest-app/solution-explorer.png
[publish]: ./media/quickstart-guest-app/publish.png
[overview]: ./media/quickstart-guest-app/overview.png
[custom-endpoint]: ./media/quickstart-guest-app/custom-endpoint.png

[download-sample]: https://github.com/MicrosoftDocs/azure-cloud-services-files/raw/temp/service-fabric-node-website.zip
[create-account]: https://azure.microsoft.com/free/?WT.mc_id=A261C142F