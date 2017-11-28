---
title: "Подключаемый модуль Azure Service Fabric для Eclipse | Документация Майкрософт"
description: "Начало работы с подключаемым модулем Service Fabric для Eclipse."
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
ms.openlocfilehash: 98c1b99972b9ad7a396d72b98e727286f6822e42
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="service-fabric-plug-in-for-eclipse-java-application-development"></a><span data-ttu-id="dd482-103">Подключаемый модуль Service Fabric для разработки приложений Eclipse на Java</span><span class="sxs-lookup"><span data-stu-id="dd482-103">Service Fabric plug-in for Eclipse Java application development</span></span>
<span data-ttu-id="dd482-104">Eclipse является одной из наиболее часто используемых интегрированных сред разработки (IDE) для разработчиков Java.</span><span class="sxs-lookup"><span data-stu-id="dd482-104">Eclipse is one of the most widely used integrated development environments (IDEs) for Java developers.</span></span> <span data-ttu-id="dd482-105">В этой статье описывается, как настроить среду разработки Eclipse для работы с Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="dd482-105">In this article, we describe how to set up your Eclipse development environment to work with Azure Service Fabric.</span></span> <span data-ttu-id="dd482-106">Вы узнаете, как установить подключаемый модуль Service Fabric, создать приложение Service Fabric и развернуть его в локальный или удаленный кластер Service Fabric в Eclipse Neon.</span><span class="sxs-lookup"><span data-stu-id="dd482-106">Learn how to install the Service Fabric plug-in, create a Service Fabric application, and deploy your Service Fabric application to a local or remote Service Fabric cluster in Eclipse Neon.</span></span>

## <a name="install-or-update-the-service-fabric-plug-in-in-eclipse-neon"></a><span data-ttu-id="dd482-107">Установка и обновление подключаемого модуля Service Fabric в Eclipse Neon</span><span class="sxs-lookup"><span data-stu-id="dd482-107">Install or update the Service Fabric plug-in in Eclipse Neon</span></span>
<span data-ttu-id="dd482-108">Вы можете установить подключаемый модуль Service Fabric в Eclipse.</span><span class="sxs-lookup"><span data-stu-id="dd482-108">You can install a Service Fabric plug-in in Eclipse.</span></span> <span data-ttu-id="dd482-109">Он позволяет упростить процесс создания и развертывания служб Java.</span><span class="sxs-lookup"><span data-stu-id="dd482-109">The plug-in can help simplify the process of building and deploying Java services.</span></span>

1.  <span data-ttu-id="dd482-110">Убедитесь, что установлена последняя версия Eclipse Neon и Buildship (версия 1.0.17 или более поздняя).</span><span class="sxs-lookup"><span data-stu-id="dd482-110">Ensure that you have the latest version of Eclipse Neon and the latest version of Buildship (1.0.17 or a later version) installed:</span></span>
    -   <span data-ttu-id="dd482-111">Чтобы проверить версии установленных компонентов, в Eclipse Neon выберите **Help** > **Installation Details** (Справка > Сведения об установке).</span><span class="sxs-lookup"><span data-stu-id="dd482-111">To check the versions of installed components, in Eclipse Neon, go to **Help** > **Installation Details**.</span></span>
    -   <span data-ttu-id="dd482-112">Сведения об обновлении Buildship см. на странице [Eclipse Buildship: Eclipse Plug-ins for Gradle][buildship-update] (Eclipse Buildship. Подключаемые модули Eclipse для Gradle).</span><span class="sxs-lookup"><span data-stu-id="dd482-112">To update Buildship, see [Eclipse Buildship: Eclipse Plug-ins for Gradle][buildship-update].</span></span>
    -   <span data-ttu-id="dd482-113">Чтобы проверить и установить обновления для Eclipse Neon, выберите **Help** > **Check for Updates** (Справка > Проверить обновления).</span><span class="sxs-lookup"><span data-stu-id="dd482-113">To check for and install updates for Eclipse Neon, go to **Help** > **Check for Updates**.</span></span>

2.  <span data-ttu-id="dd482-114">Для установки подключаемого модуля Service Fabric в Eclipse Neon щелкните **Help** > **Install New Software** (Справка > Установка нового программного обеспечения).</span><span class="sxs-lookup"><span data-stu-id="dd482-114">To install the Service Fabric plug-in, in Eclipse Neon, go to **Help** > **Install New Software**.</span></span>
  1.    <span data-ttu-id="dd482-115">В поле **Work with** (Работать с) введите **http://dl.microsoft.com/eclipse**.</span><span class="sxs-lookup"><span data-stu-id="dd482-115">In the **Work with** box, enter **http://dl.microsoft.com/eclipse**.</span></span>
  2.    <span data-ttu-id="dd482-116">Щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="dd482-116">Click **Add**.</span></span>

         ![Подключаемый модуль Service Fabric для Eclipse Neon][sf-eclipse-plugin-install]
  3.    <span data-ttu-id="dd482-118">Выберите подключаемый модуль Service Fabric и нажмите кнопку **Next** (Далее).</span><span class="sxs-lookup"><span data-stu-id="dd482-118">Select the Service Fabric plug-in, and then click **Next**.</span></span>
  4.    <span data-ttu-id="dd482-119">Выполните установку и примите условия лицензионного соглашения на использование программного обеспечения корпорации Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="dd482-119">Complete the installation steps, and then accept the Microsoft Software License Terms.</span></span>

<span data-ttu-id="dd482-120">Если подключаемый модуль Service Fabric уже установлен, убедитесь, что вы используете последнюю версию.</span><span class="sxs-lookup"><span data-stu-id="dd482-120">If you already have the Service Fabric plug-in installed, make sure that you have the latest version.</span></span> <span data-ttu-id="dd482-121">Чтобы проверить наличие доступных обновлений, выберите **Help** > **Installation Details** (Справка > Сведения об установке).</span><span class="sxs-lookup"><span data-stu-id="dd482-121">To check for available updates, go to **Help** > **Installation Details**.</span></span> <span data-ttu-id="dd482-122">В списке установленных подключаемых модулей выберите Service Fabric и щелкните **Update** (Обновить).</span><span class="sxs-lookup"><span data-stu-id="dd482-122">In the list of installed plug-ins, select Service Fabric, and then click **Update**.</span></span> <span data-ttu-id="dd482-123">После этого будут установлены доступные обновления.</span><span class="sxs-lookup"><span data-stu-id="dd482-123">Available updates will be installed.</span></span>

> [!NOTE]
> <span data-ttu-id="dd482-124">Если установка или обновление подключаемого модуля Service Fabric выполняется медленно, это может быть связано с настройкой Eclipse.</span><span class="sxs-lookup"><span data-stu-id="dd482-124">If installing or updating the Service Fabric plug-in is slow, it might be due to an Eclipse setting.</span></span> <span data-ttu-id="dd482-125">Eclipse собирает метаданные обо всех изменениях на сайтах обновления, зарегистрированных с помощью экземпляра Eclipse.</span><span class="sxs-lookup"><span data-stu-id="dd482-125">Eclipse collects metadata on all changes to update sites that are registered with your Eclipse instance.</span></span> <span data-ttu-id="dd482-126">Чтобы ускорить процесс проверки и установки обновления подключаемого модуля Service Fabric, щелкните **Available Software Sites** (Доступные сайты программного обеспечения).</span><span class="sxs-lookup"><span data-stu-id="dd482-126">To speed up the process of checking for and installing a Service Fabric plug-in update, go to **Available Software Sites**.</span></span> <span data-ttu-id="dd482-127">Снимите флажки напротив всех сайтов, которые не указывают на расположение подключаемого модуля Service Fabric (http://dl.microsoft.com/eclipse/azure/servicefabric).</span><span class="sxs-lookup"><span data-stu-id="dd482-127">Clear the check boxes for all sites except for the one that points to the Service Fabric plug-in location (http://dl.microsoft.com/eclipse/azure/servicefabric).</span></span>

## <a name="create-a-service-fabric-application-in-eclipse"></a><span data-ttu-id="dd482-128">Создание приложения Service Fabric в Eclipse</span><span class="sxs-lookup"><span data-stu-id="dd482-128">Create a Service Fabric application in Eclipse</span></span>

1.  <span data-ttu-id="dd482-129">В Eclipse Neon выберите **File** > **New** > **Other** (Файл > Создать > Другое).</span><span class="sxs-lookup"><span data-stu-id="dd482-129">In Eclipse Neon, go to **File** > **New** > **Other**.</span></span> <span data-ttu-id="dd482-130">Выберите **Service Fabric Project** (Проект Service Fabric) и нажмите кнопку **Next** (Далее).</span><span class="sxs-lookup"><span data-stu-id="dd482-130">Select  **Service Fabric Project**, and then click **Next**.</span></span>

    ![Создание проекта Service Fabric, страница 1][create-application/p1]

2.  <span data-ttu-id="dd482-132">Введите имя проекта и нажмите кнопку **Next** (Далее).</span><span class="sxs-lookup"><span data-stu-id="dd482-132">Enter a name for your project, and then click **Next**.</span></span>

    ![Создание проекта Service Fabric, страница 2][create-application/p2]

3.  <span data-ttu-id="dd482-134">В списке шаблонов выберите **Service Template** (Шаблон службы).</span><span class="sxs-lookup"><span data-stu-id="dd482-134">In the list of templates, select **Service Template**.</span></span> <span data-ttu-id="dd482-135">Выберите тип шаблона службы (субъект, без отслеживания состояния, контейнер или гостевой двоичный файл) и нажмите кнопку **Next** (Далее).</span><span class="sxs-lookup"><span data-stu-id="dd482-135">Select your service template type (Actor, Stateless, Container, or Guest Binary), and then click **Next**.</span></span>

    ![Создание проекта Service Fabric, страница 3][create-application/p3]

4.  <span data-ttu-id="dd482-137">Введите имя службы и сведения о ней, а затем нажмите кнопку **Finish** (Готово).</span><span class="sxs-lookup"><span data-stu-id="dd482-137">Enter the service name and service details, and then click **Finish**.</span></span>

    ![Создание проекта Service Fabric, страница 4][create-application/p4]

5. <span data-ttu-id="dd482-139">Если вы создаете первый проект Service Fabric, в диалоговом окне **Open Associated Perspective** (Открыть связанную перспективу) нажмите кнопку **Yes** (Да).</span><span class="sxs-lookup"><span data-stu-id="dd482-139">When you create your first Service Fabric project, in the **Open Associated Perspective** dialog box, click **Yes**.</span></span>

    ![Создание проекта Service Fabric, страница 5][create-application/p5]

6.  <span data-ttu-id="dd482-141">Новый проект выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="dd482-141">Your new project looks like this:</span></span>

    ![Создание проекта Service Fabric, страница 6][create-application/p6]

## <a name="build-and-deploy-a-service-fabric-application-in-eclipse"></a><span data-ttu-id="dd482-143">Создание и развертывание приложения Service Fabric в Eclipse</span><span class="sxs-lookup"><span data-stu-id="dd482-143">Build and deploy a Service Fabric application in Eclipse</span></span>

1.  <span data-ttu-id="dd482-144">Щелкните правой кнопкой мыши новое приложение Service Fabric, а затем выберите **Service Fabric**.</span><span class="sxs-lookup"><span data-stu-id="dd482-144">Right-click your new Service Fabric application, and then select **Service Fabric**.</span></span>

    ![Контекстное меню Service Fabric][publish/RightClick]

2. <span data-ttu-id="dd482-146">В подменю выберите нужный параметр:</span><span class="sxs-lookup"><span data-stu-id="dd482-146">In the submenu, select the option you want:</span></span>
    -   <span data-ttu-id="dd482-147">Чтобы выполнить сборку приложения без очистки, щелкните **Build Application** (Создать приложение).</span><span class="sxs-lookup"><span data-stu-id="dd482-147">To build the application without cleaning, click **Build Application**.</span></span>
    -   <span data-ttu-id="dd482-148">Для выполнения чистой сборки приложения щелкните **Rebuild Application** (Повторно создать приложение).</span><span class="sxs-lookup"><span data-stu-id="dd482-148">To do a clean build of the application, click **Rebuild Application**.</span></span>
    -   <span data-ttu-id="dd482-149">Чтобы выполнить очистку приложения от артефактов сборки, щелкните **Clean Application** (Очистить приложение).</span><span class="sxs-lookup"><span data-stu-id="dd482-149">To clean the application of built artifacts, click **Clean Application**.</span></span>

3.  <span data-ttu-id="dd482-150">В этом меню также есть параметры, позволяющие развернуть, отменить развертывание и опубликовать приложение.</span><span class="sxs-lookup"><span data-stu-id="dd482-150">From this menu, you also can deploy, undeploy, and publish your application:</span></span>
    -   <span data-ttu-id="dd482-151">Чтобы выполнить развертывание в локальном кластере, щелкните **Deploy Application** (Развернуть приложение).</span><span class="sxs-lookup"><span data-stu-id="dd482-151">To deploy to your local cluster, click **Deploy Application**.</span></span>
    -   <span data-ttu-id="dd482-152">В диалоговом окне **Publish Application** (Публикация приложения) выберите профиль публикации:</span><span class="sxs-lookup"><span data-stu-id="dd482-152">In the **Publish Application** dialog box, select a publish profile:</span></span>
        -  <span data-ttu-id="dd482-153">**Local.json**;</span><span class="sxs-lookup"><span data-stu-id="dd482-153">**Local.json**</span></span>
        -  <span data-ttu-id="dd482-154">**Cloud.json**.</span><span class="sxs-lookup"><span data-stu-id="dd482-154">**Cloud.json**</span></span>

     <span data-ttu-id="dd482-155">В этих файлах в формате JSON хранится информация (например, о конечных точках подключения и безопасности), необходимая для подключения к локальному или облачному кластеру (Azure).</span><span class="sxs-lookup"><span data-stu-id="dd482-155">These JavaScript Object Notation (JSON) files store information (such as connection endpoints and security information) that is required to connect to your local or cloud (Azure) cluster.</span></span>

  ![Меню публикации Service Fabric][publish/Publish]

<span data-ttu-id="dd482-157">Альтернативным способом развертывания приложения Service Fabric является использование конфигураций запуска Eclipse.</span><span class="sxs-lookup"><span data-stu-id="dd482-157">An alternate way to deploy your Service Fabric application is by using Eclipse run configurations.</span></span>

  1.    <span data-ttu-id="dd482-158">Выберите **Run** > **Run Configurations** (Запуск > Конфигурации запуска).</span><span class="sxs-lookup"><span data-stu-id="dd482-158">Go to **Run** > **Run Configurations**.</span></span>
  2.    <span data-ttu-id="dd482-159">Выберите конфигурацию запуска **ServiceFabricDeployer** в разделе **Grade Project** (Проект Gradle).</span><span class="sxs-lookup"><span data-stu-id="dd482-159">Under **Gradle Project**, select the **ServiceFabricDeployer** run configuration.</span></span>
  3.    <span data-ttu-id="dd482-160">На вкладке **Arguments** (Аргументы) в области справа для параметра **publishProfile** выберите значение **local** (локальная среда) или **cloud** (облако).</span><span class="sxs-lookup"><span data-stu-id="dd482-160">In the right pane, on the **Arguments** tab, for **publishProfile**, select **local** or **cloud**.</span></span>  <span data-ttu-id="dd482-161">По умолчанию используется значение **local**.</span><span class="sxs-lookup"><span data-stu-id="dd482-161">The default is **local**.</span></span> <span data-ttu-id="dd482-162">Для развертывания в удаленном (облачном) кластере выберите **облачную** среду.</span><span class="sxs-lookup"><span data-stu-id="dd482-162">To deploy to a remote or cloud cluster, select **cloud**.</span></span>
  4.    <span data-ttu-id="dd482-163">Чтобы убедиться, что в профилях публикации указаны нужные сведения, измените **Local.json** или **Cloud.json** при необходимости.</span><span class="sxs-lookup"><span data-stu-id="dd482-163">To ensure that the proper information is populated in the publish profiles, edit **Local.json** or **Cloud.json** as needed.</span></span> <span data-ttu-id="dd482-164">Вы можете добавить или обновить сведения о конечной точке и учетные данные безопасности.</span><span class="sxs-lookup"><span data-stu-id="dd482-164">You can add or update endpoint details and security credentials.</span></span>
  5.    <span data-ttu-id="dd482-165">Убедитесь, что **рабочий каталог** указывает на приложение, которое необходимо развернуть.</span><span class="sxs-lookup"><span data-stu-id="dd482-165">Ensure that **Working Directory** points to the application you want to deploy.</span></span> <span data-ttu-id="dd482-166">Чтобы изменить приложение, нажмите кнопку **Workspace** (Рабочая область) и выберите нужное приложение.</span><span class="sxs-lookup"><span data-stu-id="dd482-166">To change the application, click the **Workspace** button, and then select the application you want.</span></span>
  6.    <span data-ttu-id="dd482-167">Щелкните **Apply** (Применить), а затем — **Run** (Запуск).</span><span class="sxs-lookup"><span data-stu-id="dd482-167">Click **Apply**, and then click **Run**.</span></span>

<span data-ttu-id="dd482-168">Приложение будет собрано и развернуто через несколько секунд.</span><span class="sxs-lookup"><span data-stu-id="dd482-168">Your application builds and deploys within a few moments.</span></span> <span data-ttu-id="dd482-169">Состояние развертывания можно отслеживать в Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="dd482-169">You can monitor the deployment status in Service Fabric Explorer.</span></span>  

## <a name="add-a-service-fabric-service-to-your-service-fabric-application"></a><span data-ttu-id="dd482-170">Добавление службы Service Fabric в приложение Service Fabric</span><span class="sxs-lookup"><span data-stu-id="dd482-170">Add a Service Fabric service to your Service Fabric application</span></span>

<span data-ttu-id="dd482-171">Чтобы добавить службу Service Fabric в имеющееся приложение Service Fabric, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="dd482-171">To add a Service Fabric service to an existing Service Fabric application, do the following steps:</span></span>

1.  <span data-ttu-id="dd482-172">Щелкните правой кнопкой мыши проект, в который нужно добавить службу, и выберите **Service Fabric**.</span><span class="sxs-lookup"><span data-stu-id="dd482-172">Right-click the project you want to add a service to, and then click **Service Fabric**.</span></span>

    ![Добавление службы Service Fabric, страница 1][add-service/p1]

2.  <span data-ttu-id="dd482-174">Щелкните **Add Service Fabric Service** (Добавить службу Service Fabric) и выполните действия для добавления службы в проект.</span><span class="sxs-lookup"><span data-stu-id="dd482-174">Click **Add Service Fabric Service**, and complete the set of steps to add a service to the project.</span></span>
3.  <span data-ttu-id="dd482-175">Выберите шаблон службы и нажмите кнопку **Next** (Далее).</span><span class="sxs-lookup"><span data-stu-id="dd482-175">Select the service template you want to add to your project, and then click **Next**.</span></span>

    ![Добавление службы Service Fabric, страница 2][add-service/p2]

4.  <span data-ttu-id="dd482-177">Введите имя службы (и другие сведения при необходимости), а затем нажмите кнопку **Add Service** (Добавить службу).</span><span class="sxs-lookup"><span data-stu-id="dd482-177">Enter the service name (and other details, as needed), and then click the **Add Service** button.</span></span>  

    ![Добавление службы Service Fabric, страница 3][add-service/p3]

5.  <span data-ttu-id="dd482-179">После добавления службы общая структура проекта будет аналогична приведенной ниже.</span><span class="sxs-lookup"><span data-stu-id="dd482-179">After the service is added, your overall project structure looks similar to the following project:</span></span>

    ![Добавление службы Service Fabric, страница 4][add-service/p4]

## <a name="edit-manifest-versions-of-your-service-fabric-java-application"></a><span data-ttu-id="dd482-181">Изменение версий манифеста приложения Service Fabric на Java</span><span class="sxs-lookup"><span data-stu-id="dd482-181">Edit Manifest versions of your Service Fabric Java application</span></span>

<span data-ttu-id="dd482-182">Чтобы изменить версии манифеста, щелкните проект правой кнопкой мыши, щелкните пункт **Service Fabric**, а затем в раскрывающемся меню выберите **Изменить версии манифеста...**</span><span class="sxs-lookup"><span data-stu-id="dd482-182">To edit manifest versions, right click on the project, go to **Service Fabric** and select **Edit Manifest Versions...** from the menu dropdown.</span></span> <span data-ttu-id="dd482-183">В мастере можно обновить версии манифеста приложения, служб и версии пакетов **кода**, **конфигурации** и **данных**.</span><span class="sxs-lookup"><span data-stu-id="dd482-183">In the wizard, you can update the manifest versions for application manifest, service manifest and the versions for **Code**, **Config** and **Data** packages.</span></span>

<span data-ttu-id="dd482-184">Если вы установите флажок **Автоматическое обновление версий приложения и службы**, а затем обновите версию, то версии манифестов обновятся автоматически.</span><span class="sxs-lookup"><span data-stu-id="dd482-184">If you check the option **Automatically update application and service versions** and then update a version, then the manifest versions will be automatically updated.</span></span> <span data-ttu-id="dd482-185">Например, если вы сначала установите флажок, а затем обновите версию **кода** с 0.0.0 до 0.0.1, а затем щелкните **Готово**, то версия манифеста служб и манифеста приложения будет автоматически обновлена до 0.0.1.</span><span class="sxs-lookup"><span data-stu-id="dd482-185">To give an example, you first select the check-box, then update the version of **Code** version from 0.0.0 to 0.0.1 and click on **Finish**, then service manifest version and application manifest version will be automatically updated to 0.0.1.</span></span>

## <a name="upgrade-your-service-fabric-java-application"></a><span data-ttu-id="dd482-186">Обновление приложения Service Fabric на Java</span><span class="sxs-lookup"><span data-stu-id="dd482-186">Upgrade your Service Fabric Java application</span></span>

<span data-ttu-id="dd482-187">Чтобы рассмотреть сценарий обновления, предположим, вы создали проект **App1** с помощью подключаемого модуля Service Fabric в Eclipse.</span><span class="sxs-lookup"><span data-stu-id="dd482-187">For an upgrade scenario, say you created the **App1** project by using the Service Fabric plug-in in Eclipse.</span></span> <span data-ttu-id="dd482-188">Он был развернут с помощью подключаемого модуля для создания приложения с именем **fabric:/App1Application**.</span><span class="sxs-lookup"><span data-stu-id="dd482-188">You deployed it by using the plug-in to create an application named **fabric:/App1Application**.</span></span> <span data-ttu-id="dd482-189">Тип приложения — **App1AppicationType**, а версия приложения — 1.0.</span><span class="sxs-lookup"><span data-stu-id="dd482-189">The application type is **App1AppicationType**, and the application version is 1.0.</span></span> <span data-ttu-id="dd482-190">Теперь необходимо обновить приложение, не прерывая доступ к нему.</span><span class="sxs-lookup"><span data-stu-id="dd482-190">Now, you want to upgrade your application without interrupting availability.</span></span>

<span data-ttu-id="dd482-191">Сначала внесите изменения в приложение, а затем выполните повторную сборку службы в измененном виде.</span><span class="sxs-lookup"><span data-stu-id="dd482-191">First, make any changes to your application, and then rebuild the modified service.</span></span> <span data-ttu-id="dd482-192">Замените файл манифеста измененной службы (ServiceManifest.xml) обновленной версией для этой службы (а также все необходимые файлы из каталогов Code, Config и Data).</span><span class="sxs-lookup"><span data-stu-id="dd482-192">Update the modified service’s manifest file (ServiceManifest.xml) with the updated versions for the service (and Code, Config, or Data, as relevant).</span></span> <span data-ttu-id="dd482-193">Замените также манифест приложения (ApplicationManifest.xml) обновленной версией для приложения и измененной службы.</span><span class="sxs-lookup"><span data-stu-id="dd482-193">Also, modify the application’s manifest (ApplicationManifest.xml) with the updated version number for the application and the modified service.</span></span>  

<span data-ttu-id="dd482-194">Чтобы обновить приложение с помощью Eclipse Neon, можно создать профиль повторяющейся конфигурации запуска.</span><span class="sxs-lookup"><span data-stu-id="dd482-194">To upgrade your application by using Eclipse Neon, you can create a duplicate run configuration profile.</span></span> <span data-ttu-id="dd482-195">Затем вы сможете использовать его для обновления приложения.</span><span class="sxs-lookup"><span data-stu-id="dd482-195">Then, use it to upgrade your application as needed.</span></span>

1.  <span data-ttu-id="dd482-196">Выберите **Run** > **Run Configurations** (Запуск > Конфигурации запуска).</span><span class="sxs-lookup"><span data-stu-id="dd482-196">Go to **Run** > **Run Configurations**.</span></span> <span data-ttu-id="dd482-197">Щелкните небольшую стрелку слева от **Gradle Project** (Проект Gradle) в области слева.</span><span class="sxs-lookup"><span data-stu-id="dd482-197">In the left pane, click the small arrow to the left of **Gradle Project**.</span></span>
2.  <span data-ttu-id="dd482-198">Щелкните правой кнопкой мыши **ServiceFabricDeployer** и выберите **Duplicate** (Дублировать).</span><span class="sxs-lookup"><span data-stu-id="dd482-198">Right-click **ServiceFabricDeployer**, and then select **Duplicate**.</span></span> <span data-ttu-id="dd482-199">Введите новое имя для этой конфигурации, например **ServiceFabricUpgrader**.</span><span class="sxs-lookup"><span data-stu-id="dd482-199">Enter a new name for this configuration, for example, **ServiceFabricUpgrader**.</span></span>
3.  <span data-ttu-id="dd482-200">На панели справа на вкладке **Arguments** (Аргументы) измените **-Pconfig='deploy'** на **-Pconfig='upgrade'**, а затем нажмите кнопку **Apply** (Применить).</span><span class="sxs-lookup"><span data-stu-id="dd482-200">In the right panel, on the **Arguments** tab, change **-Pconfig='deploy'** to **-Pconfig='upgrade'**, and then click **Apply**.</span></span>

<span data-ttu-id="dd482-201">Это действие позволяет создать и сохранить профиль конфигурации запуска, который можно использовать для обновления приложения в любое время.</span><span class="sxs-lookup"><span data-stu-id="dd482-201">This process creates and saves a run configuration profile you can use at any time to upgrade your application.</span></span> <span data-ttu-id="dd482-202">При этом вы также получаете последнюю обновленную версию типа приложения из файла манифеста приложения.</span><span class="sxs-lookup"><span data-stu-id="dd482-202">It also gets the latest updated application type version from the application manifest file.</span></span>

<span data-ttu-id="dd482-203">Обновление приложения занимает несколько минут.</span><span class="sxs-lookup"><span data-stu-id="dd482-203">The application upgrade takes a few minutes.</span></span> <span data-ttu-id="dd482-204">Его можно отслеживать в Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="dd482-204">You can monitor the application upgrade in Service Fabric Explorer.</span></span>

## <a name="migrating-old-service-fabric-java-applications-to-be-used-with-maven"></a><span data-ttu-id="dd482-205">Перенос устаревших приложений Java из Service Fabric для использования с Maven</span><span class="sxs-lookup"><span data-stu-id="dd482-205">Migrating old Service Fabric Java applications to be used with Maven</span></span>
<span data-ttu-id="dd482-206">Мы недавно переместили библиотеки Java для Service Fabric из пакета SDK для Java Service Fabric в репозиторий Maven.</span><span class="sxs-lookup"><span data-stu-id="dd482-206">We have recently moved Service Fabric Java libraries from Service Fabric Java SDK to Maven repository.</span></span> <span data-ttu-id="dd482-207">В новых приложениях, созданных с помощью Eclipse, создаются последние обновленные проекты (что позволяет работать с Maven). Но вы можете обновить существующие приложения Service Fabric без учета состояния или Java Reliable Actor, в которых ранее применялся пакет SDK для Service Fabric Java, чтобы использовать зависимости Java для Service Fabric из Maven.</span><span class="sxs-lookup"><span data-stu-id="dd482-207">While the new applications you generate using Eclipse, will generate latest updated projects (which will be able to work with Maven), you can update your existing Service Fabric stateless or actor Java applications, which were using the Service Fabric Java SDK earlier, to use the Service Fabric Java dependencies from Maven.</span></span> <span data-ttu-id="dd482-208">Выполните [инструкции](service-fabric-migrate-old-javaapp-to-use-maven.md), чтобы устаревшие приложения могли взаимодействовать с Maven.</span><span class="sxs-lookup"><span data-stu-id="dd482-208">Please follow the steps mentioned [here](service-fabric-migrate-old-javaapp-to-use-maven.md) to ensure your older application works with Maven.</span></span>

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
