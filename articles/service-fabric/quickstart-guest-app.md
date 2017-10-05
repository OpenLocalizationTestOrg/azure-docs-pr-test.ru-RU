---
title: "Быстрое развертывание имеющегося приложения в кластере Azure Service Fabric"
description: "Используйте кластер Azure Service Fabric, чтобы разместить имеющееся приложение Node.js с помощью Visual Studio."
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
ms.openlocfilehash: 3601b73872bbea4b4e5324382eb97b7384ca6e13
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/29/2017
---
# <a name="host-a-nodejs-application-on-azure-service-fabric"></a><span data-ttu-id="b5a94-103">Размещение приложения Node.js в Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="b5a94-103">Host a Node.js application on Azure Service Fabric</span></span>

<span data-ttu-id="b5a94-104">Это краткое руководство поможет вам развернуть имеющееся приложение (Node.js в этом примере) в кластере Service Fabric, выполняющемся в Azure.</span><span class="sxs-lookup"><span data-stu-id="b5a94-104">This quickstart helps you deploy an existing application (Node.js in this example) to a Service Fabric cluster running on Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b5a94-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="b5a94-105">Prerequisites</span></span>

<span data-ttu-id="b5a94-106">Перед началом работы [настройте среду разработки](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="b5a94-106">Before you get started, make sure that you have [set up your development environment](service-fabric-get-started.md).</span></span> <span data-ttu-id="b5a94-107">Эта настройка включает установку пакета SDK для Service Fabric и Visual Studio 2017 или 2015.</span><span class="sxs-lookup"><span data-stu-id="b5a94-107">Which includes installing the Service Fabric SDK and Visual Studio 2017 or 2015.</span></span>

<span data-ttu-id="b5a94-108">У вас также должно быть имеющееся приложение Node.js для развертывания.</span><span class="sxs-lookup"><span data-stu-id="b5a94-108">You also need to have an existing Node.js application for deployment.</span></span> <span data-ttu-id="b5a94-109">В этом кратком руководстве используется простой веб-сайт Node.js, который можно загрузить [здесь][download-sample].</span><span class="sxs-lookup"><span data-stu-id="b5a94-109">This quickstart uses a simple Node.js website that can be downloaded [here][download-sample].</span></span> <span data-ttu-id="b5a94-110">Извлеките этот файл в папку `<path-to-project>\ApplicationPackageRoot\<package-name>\Code\` после создания проекта на следующем шаге.</span><span class="sxs-lookup"><span data-stu-id="b5a94-110">Extract this file to your `<path-to-project>\ApplicationPackageRoot\<package-name>\Code\` folder after you create the project in the next step.</span></span>

<span data-ttu-id="b5a94-111">Если у вас еще нет подписки Azure, [создайте бесплатную учетную запись Azure][create-account].</span><span class="sxs-lookup"><span data-stu-id="b5a94-111">If you don't have an Azure subscription, create a [free account][create-account].</span></span>

## <a name="create-the-service"></a><span data-ttu-id="b5a94-112">Создание службы</span><span class="sxs-lookup"><span data-stu-id="b5a94-112">Create the service</span></span>

<span data-ttu-id="b5a94-113">Запустите Visual Studio от имени **администратора**.</span><span class="sxs-lookup"><span data-stu-id="b5a94-113">Launch Visual Studio as an **administrator**.</span></span>

<span data-ttu-id="b5a94-114">Создайте проект, нажав клавиши `CTRL`+`SHIFT`+`N`.</span><span class="sxs-lookup"><span data-stu-id="b5a94-114">Create a project with `CTRL`+`SHIFT`+`N`</span></span>

<span data-ttu-id="b5a94-115">В диалоговом окне **Создать проект** выберите **Облако > Приложение Service Fabric**.</span><span class="sxs-lookup"><span data-stu-id="b5a94-115">In the **New Project** dialog, choose **Cloud > Service Fabric Application**.</span></span>

<span data-ttu-id="b5a94-116">Присвойте приложению имя **MyGuestApp** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="b5a94-116">Name the application **MyGuestApp** and press **OK**.</span></span>

>[!IMPORTANT]
><span data-ttu-id="b5a94-117">Node.js может легко преодолеть лимит в 260 знаков для путей Windows.</span><span class="sxs-lookup"><span data-stu-id="b5a94-117">Node.js can easily break the 260 character limit for paths that windows has.</span></span> <span data-ttu-id="b5a94-118">Используйте короткий путь для самого проекта, например **c:\code\svc1**.</span><span class="sxs-lookup"><span data-stu-id="b5a94-118">Use a short path for the project itself such as **c:\code\svc1**.</span></span>
   
![Диалоговое окно "Новый проект" в Visual Studio][new-project]

<span data-ttu-id="b5a94-120">Вы можете создать любой тип службы Service Fabric из следующего диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="b5a94-120">You can create any type of Service Fabric service from the next dialog.</span></span> <span data-ttu-id="b5a94-121">В рамках этого краткого руководства выберите **Гостевой исполняемый файл**.</span><span class="sxs-lookup"><span data-stu-id="b5a94-121">For this quickstart, choose **Guest Executable**.</span></span>

<span data-ttu-id="b5a94-122">Назовите службу **MyGuestService** и задайте параметрам справа следующие значения:</span><span class="sxs-lookup"><span data-stu-id="b5a94-122">Name the service **MyGuestService** and set the options on the right to the following values:</span></span>

| <span data-ttu-id="b5a94-123">Настройка</span><span class="sxs-lookup"><span data-stu-id="b5a94-123">Setting</span></span>                   | <span data-ttu-id="b5a94-124">Значение</span><span class="sxs-lookup"><span data-stu-id="b5a94-124">Value</span></span> |
| ------------------------- | ------ |
| <span data-ttu-id="b5a94-125">Папка пакета кода</span><span class="sxs-lookup"><span data-stu-id="b5a94-125">Code Package Folder</span></span>       | <span data-ttu-id="b5a94-126">_&lt;папка с вашим приложением Node.js&gt;_</span><span class="sxs-lookup"><span data-stu-id="b5a94-126">_&lt;the folder with your Node.js app&gt;_</span></span> |
| <span data-ttu-id="b5a94-127">Поведение пакета кода</span><span class="sxs-lookup"><span data-stu-id="b5a94-127">Code Package Behavior</span></span>     | <span data-ttu-id="b5a94-128">Скопируйте содержимое папки в проект</span><span class="sxs-lookup"><span data-stu-id="b5a94-128">Copy folder contents to project</span></span> |
| <span data-ttu-id="b5a94-129">Программа</span><span class="sxs-lookup"><span data-stu-id="b5a94-129">Program</span></span>                   | <span data-ttu-id="b5a94-130">node.exe</span><span class="sxs-lookup"><span data-stu-id="b5a94-130">node.exe</span></span> |
| <span data-ttu-id="b5a94-131">Аргументы</span><span class="sxs-lookup"><span data-stu-id="b5a94-131">Arguments</span></span>                 | <span data-ttu-id="b5a94-132">server.js</span><span class="sxs-lookup"><span data-stu-id="b5a94-132">server.js</span></span> |
| <span data-ttu-id="b5a94-133">Рабочая папка</span><span class="sxs-lookup"><span data-stu-id="b5a94-133">Working Folder</span></span>            | <span data-ttu-id="b5a94-134">CodePackage</span><span class="sxs-lookup"><span data-stu-id="b5a94-134">CodePackage</span></span> |

<span data-ttu-id="b5a94-135">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="b5a94-135">Press **OK**.</span></span>

![Диалоговое окно "Новая служба" в Visual Studio][new-service]

<span data-ttu-id="b5a94-137">Visual Studio создаст проект приложения и проект службы субъекта, а затем отобразит их в обозревателе решений.</span><span class="sxs-lookup"><span data-stu-id="b5a94-137">Visual Studio creates the application project and the actor service project and displays them in Solution Explorer.</span></span>

<span data-ttu-id="b5a94-138">Проект приложения (**MyGuestApp**) не содержит никакой код.</span><span class="sxs-lookup"><span data-stu-id="b5a94-138">The application project (**MyGuestApp**) does not contain any code directly.</span></span> <span data-ttu-id="b5a94-139">Он только ссылается на набор проектов служб.</span><span class="sxs-lookup"><span data-stu-id="b5a94-139">Instead, it references a set of service projects.</span></span> <span data-ttu-id="b5a94-140">Также он содержит данные еще трех типов.</span><span class="sxs-lookup"><span data-stu-id="b5a94-140">In addition, it contains three other types of content:</span></span>

* <span data-ttu-id="b5a94-141">**Профили публикации**</span><span class="sxs-lookup"><span data-stu-id="b5a94-141">**Publish profiles**</span></span>  
<span data-ttu-id="b5a94-142">Средства настройки для различных сред.</span><span class="sxs-lookup"><span data-stu-id="b5a94-142">Tooling preferences for different environments.</span></span>

* <span data-ttu-id="b5a94-143">**Сценарии**</span><span class="sxs-lookup"><span data-stu-id="b5a94-143">**Scripts**</span></span>  
<span data-ttu-id="b5a94-144">Сценарий PowerShell для развертывания и обновления приложения.</span><span class="sxs-lookup"><span data-stu-id="b5a94-144">PowerShell script for deploying/upgrading your application.</span></span>

* <span data-ttu-id="b5a94-145">**Определение приложения**</span><span class="sxs-lookup"><span data-stu-id="b5a94-145">**Application definition**</span></span>  
<span data-ttu-id="b5a94-146">Содержит манифест приложения в разделе *ApplicationPackageRoot*.</span><span class="sxs-lookup"><span data-stu-id="b5a94-146">Includes the application manifest under *ApplicationPackageRoot*.</span></span> <span data-ttu-id="b5a94-147">Связанные файлы параметров приложения расположены в разделе *ApplicationParameters*. Они определяют характеристики этого приложения, и с помощью них можно настроить приложение для конкретной среды.</span><span class="sxs-lookup"><span data-stu-id="b5a94-147">Associated application parameter files are under *ApplicationParameters*, which define the application and allow you to configure it specifically for a given environment.</span></span>
    
<span data-ttu-id="b5a94-148">Обзор содержимого проекта службы вы найдете в статье [Начало работы со службами Reliable Services в Service Fabric](service-fabric-reliable-services-quick-start.md).</span><span class="sxs-lookup"><span data-stu-id="b5a94-148">For an overview of the contents of the service project, see [Getting started with Reliable Services](service-fabric-reliable-services-quick-start.md).</span></span>

## <a name="set-up-networking"></a><span data-ttu-id="b5a94-149">Настройка сети</span><span class="sxs-lookup"><span data-stu-id="b5a94-149">Set up networking</span></span>

<span data-ttu-id="b5a94-150">Пример приложения Node.js, которое мы развертываем, использует порт **80**, и нам нужно сообщить Service Fabric о необходимости использования этого порта.</span><span class="sxs-lookup"><span data-stu-id="b5a94-150">The example Node.js app we're deploying uses port **80** and we need to tell Service Fabric that we need that port exposed.</span></span>

<span data-ttu-id="b5a94-151">Откройте файл **ServiceManifest.xml** в проекте.</span><span class="sxs-lookup"><span data-stu-id="b5a94-151">Open the **ServiceManifest.xml** file in the project.</span></span> <span data-ttu-id="b5a94-152">В нижней области манифеста находится `<Resources> \ <Endpoints>` с уже определенной записью.</span><span class="sxs-lookup"><span data-stu-id="b5a94-152">At the bottom of the manifest, there is a `<Resources> \ <Endpoints>` with an entry already defined.</span></span> <span data-ttu-id="b5a94-153">Измените эту запись, чтобы добавить `Port`, `Protocol` и `Type`.</span><span class="sxs-lookup"><span data-stu-id="b5a94-153">Modify that entry to add `Port`, `Protocol`, and `Type`.</span></span> 

```xml
  <Resources>
    <Endpoints>
      <!-- This endpoint is used by the communication listener to obtain the port on which to 
           listen. Please note that if your service is partitioned, this port is shared with 
           replicas of different partitions that are placed in your code. -->
      <Endpoint Name="MyGuestAppServiceTypeEndpoint" Port="80" Protocol="http" Type="Input" />
    </Endpoints>
  </Resources>
```

## <a name="deploy-to-azure"></a><span data-ttu-id="b5a94-154">Развернуть в Azure</span><span class="sxs-lookup"><span data-stu-id="b5a94-154">Deploy to Azure</span></span>

<span data-ttu-id="b5a94-155">Если вы нажмете клавишу **F5** и запустите проект, он будет развернут в локальном кластере.</span><span class="sxs-lookup"><span data-stu-id="b5a94-155">If you press **F5** and run the project, it is deployed to the local cluster.</span></span> <span data-ttu-id="b5a94-156">Тем не менее давайте лучше развернем его в Azure.</span><span class="sxs-lookup"><span data-stu-id="b5a94-156">However, let's deploy to Azure instead.</span></span>

<span data-ttu-id="b5a94-157">Щелкните проект правой кнопкой мыши и выберите **Опубликовать**, чтобы открыть диалоговое окно для публикации в Azure.</span><span class="sxs-lookup"><span data-stu-id="b5a94-157">Right-click on the project and choose **Publish...** which opens a dialog to publish to Azure.</span></span>

![Публикация в диалоговом окне Azure для службы Service Fabric][publish]

<span data-ttu-id="b5a94-159">Выберите целевой профиль **PublishProfiles\Cloud.xml**.</span><span class="sxs-lookup"><span data-stu-id="b5a94-159">Select the **PublishProfiles\Cloud.xml** target profile.</span></span>

<span data-ttu-id="b5a94-160">Выберите учетную запись Azure для развертывания, если вы этого еще не сделали.</span><span class="sxs-lookup"><span data-stu-id="b5a94-160">If you haven't previously, choose an Azure account to deploy to.</span></span> <span data-ttu-id="b5a94-161">Если у вас ее нет, [зарегистрируйте ее][create-account].</span><span class="sxs-lookup"><span data-stu-id="b5a94-161">If you don't have one yet, [sign-up for one][create-account].</span></span>

<span data-ttu-id="b5a94-162">В разделе **Конечная точка подключения:** выберите кластер Service Fabric для развертывания.</span><span class="sxs-lookup"><span data-stu-id="b5a94-162">Under **Connection Endpoint**, select the Service Fabric cluster to deploy to.</span></span> <span data-ttu-id="b5a94-163">Если у вас нет кластера, выберите **&lt;Создать новый кластер&gt;**. Откроется окно веб-браузера на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="b5a94-163">If you do not have one, select **&lt;Create New Cluster...&gt;** which opens up web browser window to the Azure portal.</span></span> <span data-ttu-id="b5a94-164">Дополнительные сведения см. в разделе [Создание кластера на портале Azure](service-fabric-cluster-creation-via-portal.md#create-cluster-in-the-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="b5a94-164">For more information, see [create a cluster in the portal](service-fabric-cluster-creation-via-portal.md#create-cluster-in-the-azure-portal).</span></span> 

<span data-ttu-id="b5a94-165">При создании кластера Service Fabric обязательно установите для параметра **настраиваемых конечных точек** значение **80**.</span><span class="sxs-lookup"><span data-stu-id="b5a94-165">When you create the Service Fabric cluster, make sure to set the **Custom endpoints** setting to **80**.</span></span>

![Конфигурация типа узла Service Fabric с настраиваемой конечной точкой][custom-endpoint]

<span data-ttu-id="b5a94-167">Создание нового кластера Service Fabric займет некоторое время.</span><span class="sxs-lookup"><span data-stu-id="b5a94-167">Creating a new Service Fabric cluster takes some time to complete.</span></span> <span data-ttu-id="b5a94-168">После его создания вернитесь в диалоговое окно публикации и выберите **&lt;Обновить&gt;**.</span><span class="sxs-lookup"><span data-stu-id="b5a94-168">Once it has been created, go back to the publish dialog and select **&lt;Refresh&gt;**.</span></span> <span data-ttu-id="b5a94-169">Новый кластер появится в окне раскрывающегося списка. Выберите его.</span><span class="sxs-lookup"><span data-stu-id="b5a94-169">The new cluster is listed in the drop-down box; select it.</span></span>

<span data-ttu-id="b5a94-170">Щелкните **Опубликовать** и дождитесь завершения развертывания.</span><span class="sxs-lookup"><span data-stu-id="b5a94-170">Press **Publish** and wait for the deployment to finish.</span></span>

<span data-ttu-id="b5a94-171">Это может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="b5a94-171">This may take a few minutes.</span></span> <span data-ttu-id="b5a94-172">После завершения развертывания необходимо подождать некоторое время, чтобы приложение стало полностью доступным.</span><span class="sxs-lookup"><span data-stu-id="b5a94-172">After it completes, it may take a few more minutes for the application to be fully available.</span></span>

## <a name="test-the-website"></a><span data-ttu-id="b5a94-173">Тестирование веб-сайта</span><span class="sxs-lookup"><span data-stu-id="b5a94-173">Test the website</span></span>

<span data-ttu-id="b5a94-174">После публикации службы проверьте ее в веб-браузере.</span><span class="sxs-lookup"><span data-stu-id="b5a94-174">After your service has been published, test it in a web browser.</span></span> 

<span data-ttu-id="b5a94-175">Сначала откройте портал Azure и найдите службу Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b5a94-175">First, open the Azure portal and find your Service Fabric service.</span></span>

<span data-ttu-id="b5a94-176">Просмотрите колонку обзора адреса службы.</span><span class="sxs-lookup"><span data-stu-id="b5a94-176">Check the overview blade of the service address.</span></span> <span data-ttu-id="b5a94-177">Используйте доменное имя из свойства _конечной точки подключения клиента_.</span><span class="sxs-lookup"><span data-stu-id="b5a94-177">Use the domain name from the _Client connection endpoint_ property.</span></span> <span data-ttu-id="b5a94-178">Пример: `http://mysvcfab1.westus2.cloudapp.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="b5a94-178">For example, `http://mysvcfab1.westus2.cloudapp.azure.com`.</span></span>

![Колонка обзора Service Fabric на портале Azure][overview]

<span data-ttu-id="b5a94-180">Перейдите на этот адрес, где вы увидите ответ `HELLO WORLD`.</span><span class="sxs-lookup"><span data-stu-id="b5a94-180">Navigate to this address where you will see the `HELLO WORLD` response.</span></span>

## <a name="delete-the-cluster"></a><span data-ttu-id="b5a94-181">Удаление кластера</span><span class="sxs-lookup"><span data-stu-id="b5a94-181">Delete the cluster</span></span>

<span data-ttu-id="b5a94-182">Не забудьте удалить все ресурсы, которые вы создали в рамках этого краткого руководства, так как за использование этих ресурсов взимается плата.</span><span class="sxs-lookup"><span data-stu-id="b5a94-182">Do not forget to delete all of the resources you've created for this quickstart, as you are charged for those resources.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b5a94-183">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b5a94-183">Next steps</span></span>
<span data-ttu-id="b5a94-184">Ознакомьтесь с дополнительными сведениями о [гостевых исполняемых файлах](service-fabric-deploy-existing-app.md).</span><span class="sxs-lookup"><span data-stu-id="b5a94-184">Read more about [guest executables](service-fabric-deploy-existing-app.md).</span></span>

<!-- Image References -->

[new-project]: ./media/quickstart-guest-app/new-project.png
[new-service]: ./media/quickstart-guest-app/template.png
[solution-exp]: ./media/quickstart-guest-app/solution-explorer.png
[publish]: ./media/quickstart-guest-app/publish.png
[overview]: ./media/quickstart-guest-app/overview.png
[custom-endpoint]: ./media/quickstart-guest-app/custom-endpoint.png

[download-sample]: https://github.com/MicrosoftDocs/azure-cloud-services-files/raw/temp/service-fabric-node-website.zip
[create-account]: https://azure.microsoft.com/free/?WT.mc_id=A261C142F