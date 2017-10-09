---
title: "Подключаемый модуль для Eclipse Service Fabric aaaAzure | Документы Microsoft"
description: "Начало работы с hello Service Fabric подключаемого модуля для Eclipse."
services: service-fabric
documentationcenter: java
author: sayantancs
manager: timlt
editor: 
ms.assetid: bf84458f-4b87-4de1-9844-19909e368deb
ms.service: service-fabric
ms.devlang: java
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/21/2016
ms.author: saysa
ms.openlocfilehash: 4ba5a28a6282387249a2bd4e62314e891ff04162
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-plug-in-for-eclipse-java-application-development"></a><span data-ttu-id="2b866-103">Подключаемый модуль Service Fabric для разработки приложений Eclipse на Java</span><span class="sxs-lookup"><span data-stu-id="2b866-103">Service Fabric plug-in for Eclipse Java application development</span></span>
<span data-ttu-id="2b866-104">Eclipse является одним из наиболее широко используемых hello интегрированной среды разработки (IDE) для разработчиков Java.</span><span class="sxs-lookup"><span data-stu-id="2b866-104">Eclipse is one of hello most widely used integrated development environments (IDEs) for Java developers.</span></span> <span data-ttu-id="2b866-105">В этой статье описывается как tooset копирование вашей toowork среды Eclipse разработки с Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="2b866-105">In this article, we describe how tooset up your Eclipse development environment toowork with Azure Service Fabric.</span></span> <span data-ttu-id="2b866-106">Узнайте, как создать приложение Service Fabric hello tooinstall Service Fabric подключаемого модуля, и развертывания вашего Service Fabric приложения tooa локальный или удаленный Service Fabric кластера в Eclipse Neon.</span><span class="sxs-lookup"><span data-stu-id="2b866-106">Learn how tooinstall hello Service Fabric plug-in, create a Service Fabric application, and deploy your Service Fabric application tooa local or remote Service Fabric cluster in Eclipse Neon.</span></span>

## <a name="install-or-update-hello-service-fabric-plug-in-in-eclipse-neon"></a><span data-ttu-id="2b866-107">Установите или обновите hello подключаемый модуль в Eclipse Neon Service Fabric</span><span class="sxs-lookup"><span data-stu-id="2b866-107">Install or update hello Service Fabric plug-in in Eclipse Neon</span></span>
<span data-ttu-id="2b866-108">Вы можете установить подключаемый модуль Service Fabric в Eclipse.</span><span class="sxs-lookup"><span data-stu-id="2b866-108">You can install a Service Fabric plug-in in Eclipse.</span></span> <span data-ttu-id="2b866-109">Подключаемый модуль Hello позволяет упростить процесс hello Создание и развертывание служб Java.</span><span class="sxs-lookup"><span data-stu-id="2b866-109">hello plug-in can help simplify hello process of building and deploying Java services.</span></span>

1.  <span data-ttu-id="2b866-110">Убедитесь, что последняя версия Eclipse Neon hello и hello последнюю версию Buildship установлен (1.0.17 или более поздней версии):</span><span class="sxs-lookup"><span data-stu-id="2b866-110">Ensure that you have hello latest version of Eclipse Neon and hello latest version of Buildship (1.0.17 or a later version) installed:</span></span>
    -   <span data-ttu-id="2b866-111">toocheck hello версии установленных компонентов в Eclipse Neon go слишком**справки** > **сведения об установке**.</span><span class="sxs-lookup"><span data-stu-id="2b866-111">toocheck hello versions of installed components, in Eclipse Neon, go too**Help** > **Installation Details**.</span></span>
    -   <span data-ttu-id="2b866-112">в разделе tooupdate Buildship, [Eclipse Buildship: подключаемые модули Eclipse для Gradle][buildship-update].</span><span class="sxs-lookup"><span data-stu-id="2b866-112">tooupdate Buildship, see [Eclipse Buildship: Eclipse Plug-ins for Gradle][buildship-update].</span></span>
    -   <span data-ttu-id="2b866-113">toocheck для и установка обновлений для Eclipse Neon go слишком**справки** > **проверять наличие обновлений**.</span><span class="sxs-lookup"><span data-stu-id="2b866-113">toocheck for and install updates for Eclipse Neon, go too**Help** > **Check for Updates**.</span></span>

2.  <span data-ttu-id="2b866-114">hello tooinstall Service Fabric подключаемый модуль в Eclipse Neon go слишком**справки** > **Установка нового программного обеспечения**.</span><span class="sxs-lookup"><span data-stu-id="2b866-114">tooinstall hello Service Fabric plug-in, in Eclipse Neon, go too**Help** > **Install New Software**.</span></span>
  1.    <span data-ttu-id="2b866-115">В hello **работать с** введите **http://dl.microsoft.com/eclipse**.</span><span class="sxs-lookup"><span data-stu-id="2b866-115">In hello **Work with** box, enter **http://dl.microsoft.com/eclipse**.</span></span>
  2.    <span data-ttu-id="2b866-116">Щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="2b866-116">Click **Add**.</span></span>

         ![Подключаемый модуль Service Fabric для Eclipse Neon][sf-eclipse-plugin-install]
  3.    <span data-ttu-id="2b866-118">Выберите hello Service Fabric подключаемого модуля и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="2b866-118">Select hello Service Fabric plug-in, and then click **Next**.</span></span>
  4.    <span data-ttu-id="2b866-119">Выполните шаги установки hello и примите условия лицензии программного обеспечения корпорации Майкрософт hello.</span><span class="sxs-lookup"><span data-stu-id="2b866-119">Complete hello installation steps, and then accept hello Microsoft Software License Terms.</span></span>

<span data-ttu-id="2b866-120">Если уже имеется hello Service Fabric подключаемый модуль установлен, убедитесь, что имеется hello последнюю версию.</span><span class="sxs-lookup"><span data-stu-id="2b866-120">If you already have hello Service Fabric plug-in installed, make sure that you have hello latest version.</span></span> <span data-ttu-id="2b866-121">toocheck наличие доступных обновлений go слишком**справки** > **сведения об установке**.</span><span class="sxs-lookup"><span data-stu-id="2b866-121">toocheck for available updates, go too**Help** > **Installation Details**.</span></span> <span data-ttu-id="2b866-122">В списке установленных подключаемых модулей hello выберите Service Fabric и нажмите кнопку **обновление**.</span><span class="sxs-lookup"><span data-stu-id="2b866-122">In hello list of installed plug-ins, select Service Fabric, and then click **Update**.</span></span> <span data-ttu-id="2b866-123">После этого будут установлены доступные обновления.</span><span class="sxs-lookup"><span data-stu-id="2b866-123">Available updates will be installed.</span></span>

> [!NOTE]
> <span data-ttu-id="2b866-124">При установке или обновлении hello Service Fabric подключаемый модуль выполняется медленно, возможно из-за параметра tooan Eclipse.</span><span class="sxs-lookup"><span data-stu-id="2b866-124">If installing or updating hello Service Fabric plug-in is slow, it might be due tooan Eclipse setting.</span></span> <span data-ttu-id="2b866-125">Eclipse собирает метаданных на все сайты tooupdate изменения, зарегистрированные в вашем экземпляре Eclipse.</span><span class="sxs-lookup"><span data-stu-id="2b866-125">Eclipse collects metadata on all changes tooupdate sites that are registered with your Eclipse instance.</span></span> <span data-ttu-id="2b866-126">toospeed hello процесс проверки и установки обновления Service Fabric подключаемого модуля, go слишком**доступных сайтов программного обеспечения**.</span><span class="sxs-lookup"><span data-stu-id="2b866-126">toospeed up hello process of checking for and installing a Service Fabric plug-in update, go too**Available Software Sites**.</span></span> <span data-ttu-id="2b866-127">Снимите флажки hello для всех сайтов, за исключением hello тот, который указывает расположение подключаемого модуля Service Fabric toohello (http://dl.microsoft.com/eclipse/azure/servicefabric).</span><span class="sxs-lookup"><span data-stu-id="2b866-127">Clear hello check boxes for all sites except for hello one that points toohello Service Fabric plug-in location (http://dl.microsoft.com/eclipse/azure/servicefabric).</span></span>

## <a name="create-a-service-fabric-application-in-eclipse"></a><span data-ttu-id="2b866-128">Создание приложения Service Fabric в Eclipse</span><span class="sxs-lookup"><span data-stu-id="2b866-128">Create a Service Fabric application in Eclipse</span></span>

1.  <span data-ttu-id="2b866-129">В Eclipse Neon перейдите слишком**файл** > **New** > **других**.</span><span class="sxs-lookup"><span data-stu-id="2b866-129">In Eclipse Neon, go too**File** > **New** > **Other**.</span></span> <span data-ttu-id="2b866-130">Выберите **Service Fabric Project** (Проект Service Fabric) и нажмите кнопку **Next** (Далее).</span><span class="sxs-lookup"><span data-stu-id="2b866-130">Select  **Service Fabric Project**, and then click **Next**.</span></span>

    ![Создание проекта Service Fabric, страница 1][create-application/p1]

2.  <span data-ttu-id="2b866-132">Введите имя проекта и нажмите кнопку **Next** (Далее).</span><span class="sxs-lookup"><span data-stu-id="2b866-132">Enter a name for your project, and then click **Next**.</span></span>

    ![Создание проекта Service Fabric, страница 2][create-application/p2]

3.  <span data-ttu-id="2b866-134">В списке шаблонов hello выберите **шаблона службы**.</span><span class="sxs-lookup"><span data-stu-id="2b866-134">In hello list of templates, select **Service Template**.</span></span> <span data-ttu-id="2b866-135">Выберите тип шаблона службы (субъект, без отслеживания состояния, контейнер или гостевой двоичный файл) и нажмите кнопку **Next** (Далее).</span><span class="sxs-lookup"><span data-stu-id="2b866-135">Select your service template type (Actor, Stateless, Container, or Guest Binary), and then click **Next**.</span></span>

    ![Создание проекта Service Fabric, страница 3][create-application/p3]

4.  <span data-ttu-id="2b866-137">Введите имя службы hello и службы сведения и нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="2b866-137">Enter hello service name and service details, and then click **Finish**.</span></span>

    ![Создание проекта Service Fabric, страница 4][create-application/p4]

5. <span data-ttu-id="2b866-139">При создании первого проекта Service Fabric в hello **открыть связанный перспективу** диалоговое окно, нажмите кнопку **Да**.</span><span class="sxs-lookup"><span data-stu-id="2b866-139">When you create your first Service Fabric project, in hello **Open Associated Perspective** dialog box, click **Yes**.</span></span>

    ![Создание проекта Service Fabric, страница 5][create-application/p5]

6.  <span data-ttu-id="2b866-141">Новый проект выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="2b866-141">Your new project looks like this:</span></span>

    ![Создание проекта Service Fabric, страница 6][create-application/p6]

## <a name="build-and-deploy-a-service-fabric-application-in-eclipse"></a><span data-ttu-id="2b866-143">Создание и развертывание приложения Service Fabric в Eclipse</span><span class="sxs-lookup"><span data-stu-id="2b866-143">Build and deploy a Service Fabric application in Eclipse</span></span>

1.  <span data-ttu-id="2b866-144">Щелкните правой кнопкой мыши новое приложение Service Fabric, а затем выберите **Service Fabric**.</span><span class="sxs-lookup"><span data-stu-id="2b866-144">Right-click your new Service Fabric application, and then select **Service Fabric**.</span></span>

    ![Контекстное меню Service Fabric][publish/RightClick]

2. <span data-ttu-id="2b866-146">В подменю «hello» выберите нужный параметр hello:</span><span class="sxs-lookup"><span data-stu-id="2b866-146">In hello submenu, select hello option you want:</span></span>
    -   <span data-ttu-id="2b866-147">Щелкните приложение hello toobuild без очистки, **сборки приложения**.</span><span class="sxs-lookup"><span data-stu-id="2b866-147">toobuild hello application without cleaning, click **Build Application**.</span></span>
    -   <span data-ttu-id="2b866-148">Нажмите кнопку toodo чистую сборку приложения hello **перестроить приложения**.</span><span class="sxs-lookup"><span data-stu-id="2b866-148">toodo a clean build of hello application, click **Rebuild Application**.</span></span>
    -   <span data-ttu-id="2b866-149">приложение hello tooclean артефактов сборки, откройте **чистой приложения**.</span><span class="sxs-lookup"><span data-stu-id="2b866-149">tooclean hello application of built artifacts, click **Clean Application**.</span></span>

3.  <span data-ttu-id="2b866-150">В этом меню также есть параметры, позволяющие развернуть, отменить развертывание и опубликовать приложение.</span><span class="sxs-lookup"><span data-stu-id="2b866-150">From this menu, you also can deploy, undeploy, and publish your application:</span></span>
    -   <span data-ttu-id="2b866-151">toodeploy tooyour локального кластера, нажмите кнопку **развертывание приложения**.</span><span class="sxs-lookup"><span data-stu-id="2b866-151">toodeploy tooyour local cluster, click **Deploy Application**.</span></span>
    -   <span data-ttu-id="2b866-152">В hello **публикация приложения** диалогового окна выберите профиль публикации:</span><span class="sxs-lookup"><span data-stu-id="2b866-152">In hello **Publish Application** dialog box, select a publish profile:</span></span>
        -  <span data-ttu-id="2b866-153">**Local.json**;</span><span class="sxs-lookup"><span data-stu-id="2b866-153">**Local.json**</span></span>
        -  <span data-ttu-id="2b866-154">**Cloud.json**.</span><span class="sxs-lookup"><span data-stu-id="2b866-154">**Cloud.json**</span></span>

     <span data-ttu-id="2b866-155">Эти файлы JavaScript Object Notation (JSON) хранения сведений (например, конечные точки подключения и сведения о безопасности), которые требуется tooconnect tooyour локальной или кластера с облаком (Azure).</span><span class="sxs-lookup"><span data-stu-id="2b866-155">These JavaScript Object Notation (JSON) files store information (such as connection endpoints and security information) that is required tooconnect tooyour local or cloud (Azure) cluster.</span></span>

  ![Меню публикации Service Fabric][publish/Publish]

<span data-ttu-id="2b866-157">Альтернативный способ toodeploy приложения Service Fabric с помощью Eclipse выполняется конфигураций.</span><span class="sxs-lookup"><span data-stu-id="2b866-157">An alternate way toodeploy your Service Fabric application is by using Eclipse run configurations.</span></span>

  1.    <span data-ttu-id="2b866-158">Go слишком**запуска** > **конфигурации запусков**.</span><span class="sxs-lookup"><span data-stu-id="2b866-158">Go too**Run** > **Run Configurations**.</span></span>
  2.    <span data-ttu-id="2b866-159">В разделе **проекта Gradle**выберите hello **ServiceFabricDeployer** конфигурации запуска.</span><span class="sxs-lookup"><span data-stu-id="2b866-159">Under **Gradle Project**, select hello **ServiceFabricDeployer** run configuration.</span></span>
  3.    <span data-ttu-id="2b866-160">В правой панели hello в hello **аргументы** вкладке для **publishProfile**выберите **локального** или **облака**.</span><span class="sxs-lookup"><span data-stu-id="2b866-160">In hello right pane, on hello **Arguments** tab, for **publishProfile**, select **local** or **cloud**.</span></span>  <span data-ttu-id="2b866-161">по умолчанию Hello — **локальной**.</span><span class="sxs-lookup"><span data-stu-id="2b866-161">hello default is **local**.</span></span> <span data-ttu-id="2b866-162">toodeploy tooa удаленного или облака кластера, выберите **облака**.</span><span class="sxs-lookup"><span data-stu-id="2b866-162">toodeploy tooa remote or cloud cluster, select **cloud**.</span></span>
  4.    <span data-ttu-id="2b866-163">tooensure, что соответствующие сведения hello заполняется hello профилей публикации, изменить **Local.json** или **Cloud.json** при необходимости.</span><span class="sxs-lookup"><span data-stu-id="2b866-163">tooensure that hello proper information is populated in hello publish profiles, edit **Local.json** or **Cloud.json** as needed.</span></span> <span data-ttu-id="2b866-164">Вы можете добавить или обновить сведения о конечной точке и учетные данные безопасности.</span><span class="sxs-lookup"><span data-stu-id="2b866-164">You can add or update endpoint details and security credentials.</span></span>
  5.    <span data-ttu-id="2b866-165">Убедитесь, что **рабочий каталог** указывает toohello приложение, toodeploy.</span><span class="sxs-lookup"><span data-stu-id="2b866-165">Ensure that **Working Directory** points toohello application you want toodeploy.</span></span> <span data-ttu-id="2b866-166">toochange Здравствуйте, приложения, нажмите кнопку hello **рабочей** кнопку, а затем выберите приложение hello.</span><span class="sxs-lookup"><span data-stu-id="2b866-166">toochange hello application, click hello **Workspace** button, and then select hello application you want.</span></span>
  6.    <span data-ttu-id="2b866-167">Щелкните **Apply** (Применить), а затем — **Run** (Запуск).</span><span class="sxs-lookup"><span data-stu-id="2b866-167">Click **Apply**, and then click **Run**.</span></span>

<span data-ttu-id="2b866-168">Приложение будет собрано и развернуто через несколько секунд.</span><span class="sxs-lookup"><span data-stu-id="2b866-168">Your application builds and deploys within a few moments.</span></span> <span data-ttu-id="2b866-169">Можно отслеживать состояние развертывания hello в обозреватель Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="2b866-169">You can monitor hello deployment status in Service Fabric Explorer.</span></span>  

## <a name="add-a-service-fabric-service-tooyour-service-fabric-application"></a><span data-ttu-id="2b866-170">Добавить tooyour служба Service Fabric приложения Service Fabric</span><span class="sxs-lookup"><span data-stu-id="2b866-170">Add a Service Fabric service tooyour Service Fabric application</span></span>

<span data-ttu-id="2b866-171">tooadd Service Fabric service tooan существующие приложения Service Fabric, hello следующие действия:</span><span class="sxs-lookup"><span data-stu-id="2b866-171">tooadd a Service Fabric service tooan existing Service Fabric application, do hello following steps:</span></span>

1.  <span data-ttu-id="2b866-172">Щелкните правой кнопкой мыши проект hello вы tooadd службе и нажмите кнопку **Service Fabric**.</span><span class="sxs-lookup"><span data-stu-id="2b866-172">Right-click hello project you want tooadd a service to, and then click **Service Fabric**.</span></span>

    ![Добавление службы Service Fabric, страница 1][add-service/p1]

2.  <span data-ttu-id="2b866-174">Нажмите кнопку **добавьте служба Service Fabric**, а hello полный набор tooadd действия проект toohello службы.</span><span class="sxs-lookup"><span data-stu-id="2b866-174">Click **Add Service Fabric Service**, and complete hello set of steps tooadd a service toohello project.</span></span>
3.  <span data-ttu-id="2b866-175">Шаблон службы выберите hello tooadd tooyour проекта и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="2b866-175">Select hello service template you want tooadd tooyour project, and then click **Next**.</span></span>

    ![Добавление службы Service Fabric, страница 2][add-service/p2]

4.  <span data-ttu-id="2b866-177">Введите имя службы hello (и другие сведения, при необходимости) и нажмите кнопку hello **добавить службу** кнопки.</span><span class="sxs-lookup"><span data-stu-id="2b866-177">Enter hello service name (and other details, as needed), and then click hello **Add Service** button.</span></span>  

    ![Добавление службы Service Fabric, страница 3][add-service/p3]

5.  <span data-ttu-id="2b866-179">После добавления службы hello общей структуры проекта выглядит примерно toohello следующих проектов:</span><span class="sxs-lookup"><span data-stu-id="2b866-179">After hello service is added, your overall project structure looks similar toohello following project:</span></span>

    ![Добавление службы Service Fabric, страница 4][add-service/p4]

## <a name="edit-manifest-versions-of-your-service-fabric-java-application"></a><span data-ttu-id="2b866-181">Изменение версий манифеста приложения Service Fabric на Java</span><span class="sxs-lookup"><span data-stu-id="2b866-181">Edit Manifest versions of your Service Fabric Java application</span></span>

<span data-ttu-id="2b866-182">tooedit версии манифеста, щелкните правой кнопкой мыши проект hello, go слишком**Service Fabric** и выберите **изменение версии манифеста...**  из раскрывающегося меню hello.</span><span class="sxs-lookup"><span data-stu-id="2b866-182">tooedit manifest versions, right click on hello project, go too**Service Fabric** and select **Edit Manifest Versions...** from hello menu dropdown.</span></span> <span data-ttu-id="2b866-183">В мастере приветствия, можно обновить hello манифеста для манифеста, манифест службы приложения и hello версии для **кода**, **Config** и **данные** пакетов.</span><span class="sxs-lookup"><span data-stu-id="2b866-183">In hello wizard, you can update hello manifest versions for application manifest, service manifest and hello versions for **Code**, **Config** and **Data** packages.</span></span>

<span data-ttu-id="2b866-184">Если выбран параметр hello **автоматическое обновление версий приложения и службы** и затем обновить версию, затем hello манифеста версии будут обновляться автоматически.</span><span class="sxs-lookup"><span data-stu-id="2b866-184">If you check hello option **Automatically update application and service versions** and then update a version, then hello manifest versions will be automatically updated.</span></span> <span data-ttu-id="2b866-185">toogive пример сначала выбрать флажок hello, а затем обновленную версию hello **кода** версии из 0.0.0 too0.0.1 и нажмите кнопку **Готово**, затем службы версии манифеста и манифест приложения версия будет автоматически обновляются too0.0.1.</span><span class="sxs-lookup"><span data-stu-id="2b866-185">toogive an example, you first select hello check-box, then update hello version of **Code** version from 0.0.0 too0.0.1 and click on **Finish**, then service manifest version and application manifest version will be automatically updated too0.0.1.</span></span>

## <a name="upgrade-your-service-fabric-java-application"></a><span data-ttu-id="2b866-186">Обновление приложения Service Fabric на Java</span><span class="sxs-lookup"><span data-stu-id="2b866-186">Upgrade your Service Fabric Java application</span></span>

<span data-ttu-id="2b866-187">Для сценария обновления, предположим, вы создали hello **App1** проекта с помощью подключаемого модуля в Eclipse Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="2b866-187">For an upgrade scenario, say you created hello **App1** project by using hello Service Fabric plug-in in Eclipse.</span></span> <span data-ttu-id="2b866-188">Он был развернут с помощью подключаемого модуля toocreate hello приложения с именем **fabric: / App1Application**.</span><span class="sxs-lookup"><span data-stu-id="2b866-188">You deployed it by using hello plug-in toocreate an application named **fabric:/App1Application**.</span></span> <span data-ttu-id="2b866-189">Тип приложения Hello **App1AppicationType**, и версия приложения hello-1.0.</span><span class="sxs-lookup"><span data-stu-id="2b866-189">hello application type is **App1AppicationType**, and hello application version is 1.0.</span></span> <span data-ttu-id="2b866-190">Теперь требуется tooupgrade приложения без прерывания доступа.</span><span class="sxs-lookup"><span data-stu-id="2b866-190">Now, you want tooupgrade your application without interrupting availability.</span></span>

<span data-ttu-id="2b866-191">Во-первых, внесите изменения tooyour приложения, а затем перестроить hello изменения службы.</span><span class="sxs-lookup"><span data-stu-id="2b866-191">First, make any changes tooyour application, and then rebuild hello modified service.</span></span> <span data-ttu-id="2b866-192">Обновление hello изменить файл манифеста службы (ServiceManifest.xml) с версиями hello обновления для службы hello (и кода, конфигурации и данных, таких как соответствующие).</span><span class="sxs-lookup"><span data-stu-id="2b866-192">Update hello modified service’s manifest file (ServiceManifest.xml) with hello updated versions for hello service (and Code, Config, or Data, as relevant).</span></span> <span data-ttu-id="2b866-193">Кроме того изменить манифест приложения hello (ApplicationManifest.xml) с hello обновить номер версии для приложения hello и hello измененные службы.</span><span class="sxs-lookup"><span data-stu-id="2b866-193">Also, modify hello application’s manifest (ApplicationManifest.xml) with hello updated version number for hello application and hello modified service.</span></span>  

<span data-ttu-id="2b866-194">tooupgrade приложения с помощью Eclipse Neon, можно создать профиль повторяющиеся конфигурации запуска.</span><span class="sxs-lookup"><span data-stu-id="2b866-194">tooupgrade your application by using Eclipse Neon, you can create a duplicate run configuration profile.</span></span> <span data-ttu-id="2b866-195">Затем используйте tooupgrade приложения при необходимости.</span><span class="sxs-lookup"><span data-stu-id="2b866-195">Then, use it tooupgrade your application as needed.</span></span>

1.  <span data-ttu-id="2b866-196">Go слишком**запуска** > **конфигурации запусков**.</span><span class="sxs-lookup"><span data-stu-id="2b866-196">Go too**Run** > **Run Configurations**.</span></span> <span data-ttu-id="2b866-197">Hello левой панели щелкните hello маленькую стрелку toohello слева от **Gradle проекта**.</span><span class="sxs-lookup"><span data-stu-id="2b866-197">In hello left pane, click hello small arrow toohello left of **Gradle Project**.</span></span>
2.  <span data-ttu-id="2b866-198">Щелкните правой кнопкой мыши **ServiceFabricDeployer** и выберите **Duplicate** (Дублировать).</span><span class="sxs-lookup"><span data-stu-id="2b866-198">Right-click **ServiceFabricDeployer**, and then select **Duplicate**.</span></span> <span data-ttu-id="2b866-199">Введите новое имя для этой конфигурации, например **ServiceFabricUpgrader**.</span><span class="sxs-lookup"><span data-stu-id="2b866-199">Enter a new name for this configuration, for example, **ServiceFabricUpgrader**.</span></span>
3.  <span data-ttu-id="2b866-200">На правой панели hello и на hello **аргументы** измените **- Pconfig = «развертывание»** слишком**- Pconfig = «обновить»**и нажмите кнопку **применить**.</span><span class="sxs-lookup"><span data-stu-id="2b866-200">In hello right panel, on hello **Arguments** tab, change **-Pconfig='deploy'** too**-Pconfig='upgrade'**, and then click **Apply**.</span></span>

<span data-ttu-id="2b866-201">Этот процесс создает и сохраняет профиль конфигурации запуска можно использовать в любое время tooupgrade приложения.</span><span class="sxs-lookup"><span data-stu-id="2b866-201">This process creates and saves a run configuration profile you can use at any time tooupgrade your application.</span></span> <span data-ttu-id="2b866-202">Он также возвращает hello последнюю версию типа обновленное приложение из файла манифеста приложения hello.</span><span class="sxs-lookup"><span data-stu-id="2b866-202">It also gets hello latest updated application type version from hello application manifest file.</span></span>

<span data-ttu-id="2b866-203">обновление приложения Hello занимает несколько минут.</span><span class="sxs-lookup"><span data-stu-id="2b866-203">hello application upgrade takes a few minutes.</span></span> <span data-ttu-id="2b866-204">Вы можете отслеживать обновления приложения hello в обозреватель Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="2b866-204">You can monitor hello application upgrade in Service Fabric Explorer.</span></span>

## <a name="migrating-old-service-fabric-java-applications-toobe-used-with-maven"></a><span data-ttu-id="2b866-205">Миграция старый toobe приложений Java структуры службы, используемые с Maven</span><span class="sxs-lookup"><span data-stu-id="2b866-205">Migrating old Service Fabric Java applications toobe used with Maven</span></span>
<span data-ttu-id="2b866-206">Служба Fabric Java библиотеки недавно были удалены из репозитория tooMaven Service Fabric Java SDK.</span><span class="sxs-lookup"><span data-stu-id="2b866-206">We have recently moved Service Fabric Java libraries from Service Fabric Java SDK tooMaven repository.</span></span> <span data-ttu-id="2b866-207">Хотя hello новые приложения, созданные с помощью Eclipse, создаст последних измененных проектов (которые будут может toowork с Maven), необходимо обновить существующие структуры службы без сохранения состояния и приложения Java субъектов, которые использовали hello Service Fabric Java SDK более ранние версии, toouse hello Java структуры службы зависимостей из Maven.</span><span class="sxs-lookup"><span data-stu-id="2b866-207">While hello new applications you generate using Eclipse, will generate latest updated projects (which will be able toowork with Maven), you can update your existing Service Fabric stateless or actor Java applications, which were using hello Service Fabric Java SDK earlier, toouse hello Service Fabric Java dependencies from Maven.</span></span> <span data-ttu-id="2b866-208">Выполните шаги hello упомянутые [здесь](service-fabric-migrate-old-javaapp-to-use-maven.md) tooensure старые приложения работает с Maven.</span><span class="sxs-lookup"><span data-stu-id="2b866-208">Please follow hello steps mentioned [here](service-fabric-migrate-old-javaapp-to-use-maven.md) tooensure your older application works with Maven.</span></span>

<!-- Images -->

[sf-eclipse-plugin-install]: ./media/service-fabric-get-started-eclipse/service-fabric-eclipse-plugin.png

[create-application/p1]:./media/service-fabric-get-started-eclipse/create-application/p1.png
[create-application/p2]:./media/service-fabric-get-started-eclipse/create-application/p2.png
[create-application/p3]:./media/service-fabric-get-started-eclipse/create-application/p3.png
[create-application/p4]:./media/service-fabric-get-started-eclipse/create-application/p4.png
[create-application/p5]:./media/service-fabric-get-started-eclipse/create-application/p5.png
[create-application/p6]:./media/service-fabric-get-started-eclipse/create-application/p6.png

[publish/Publish]: ./media/service-fabric-get-started-eclipse/publish/Publish.png
[publish/RightClick]: ./media/service-fabric-get-started-eclipse/publish/RightClick.png

[add-service/p1]: ./media/service-fabric-get-started-eclipse/add-service/p1.png
[add-service/p2]: ./media/service-fabric-get-started-eclipse/add-service/p2.png
[add-service/p3]: ./media/service-fabric-get-started-eclipse/add-service/p3.png
[add-service/p4]: ./media/service-fabric-get-started-eclipse/add-service/p4.png

<!-- Links -->
[buildship-update]: https://projects.eclipse.org/projects/tools.buildship
