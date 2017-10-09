---
title: "aaaUse .NET SDK для Microsoft Azure StorSimple данных диспетчера заданий | Документы Microsoft"
description: "Узнайте, как .NET SDK toouse toolaunch данных StorSimple Manager заданий (личной предварительной версии)"
services: storsimple
documentationcenter: NA
author: vidarmsft
manager: syadav
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 11/22/2016
ms.author: vidarmsft
ms.openlocfilehash: b07fe64369574c994fd28d42786aa02dca435ccc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-net-sdk-tooinitiate-data-transformation-private-preview"></a><span data-ttu-id="2d49f-103">Используйте hello .net SDK tooinitiate преобразования данных (личной предварительной версии)</span><span class="sxs-lookup"><span data-stu-id="2d49f-103">Use hello .Net SDK tooinitiate data transformation (Private Preview)</span></span>

## <a name="overview"></a><span data-ttu-id="2d49f-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="2d49f-104">Overview</span></span>

<span data-ttu-id="2d49f-105">В этой статье объясняется, как можно использовать функцию преобразования данных hello в tootransform службы диспетчера StorSimple данных hello данные на устройстве StorSimple.</span><span class="sxs-lookup"><span data-stu-id="2d49f-105">This article explains how you can use hello data transformation feature within hello StorSimple Data Manager service tootransform StorSimple device data.</span></span> <span data-ttu-id="2d49f-106">Hello преобразованные данные затем используются другими службами Azure в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="2d49f-106">hello transformed data is then consumed by other Azure services in hello cloud.</span></span> <span data-ttu-id="2d49f-107">статья Hello также имеет toohelp Пошаговое руководство создает образец .NET консольного приложения tooinitiate задание преобразования данных и затем отслеживать его завершения.</span><span class="sxs-lookup"><span data-stu-id="2d49f-107">hello article also has a walkthrough toohelp create a sample .NET console application tooinitiate a data transformation job and then track it for completion.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2d49f-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="2d49f-108">Prerequisites</span></span>

<span data-ttu-id="2d49f-109">Перед началом работы убедитесь, что у вас есть следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="2d49f-109">Before you begin, ensure that you have:</span></span>
*   <span data-ttu-id="2d49f-110">Система, в которой установлена среда Visual Studio 2012, 2013, 2015 или 2017.</span><span class="sxs-lookup"><span data-stu-id="2d49f-110">A system with Visual Studio 2012, 2013, 2015, or 2017 installed.</span></span>
*   <span data-ttu-id="2d49f-111">Azure PowerShell установлен.</span><span class="sxs-lookup"><span data-stu-id="2d49f-111">Azure Powershell installed.</span></span> <span data-ttu-id="2d49f-112">[Скачать Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span><span class="sxs-lookup"><span data-stu-id="2d49f-112">[Download Azure Powershell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span></span>
*   <span data-ttu-id="2d49f-113">Параметры tooinitialize hello преобразования данных задания конфигурации (tooobtain эти параметры включены здесь инструкции).</span><span class="sxs-lookup"><span data-stu-id="2d49f-113">Configuration settings tooinitialize hello Data Transformation job (instructions tooobtain these settings are included here).</span></span>
*   <span data-ttu-id="2d49f-114">Определение задания, которое правильно настроено в гибридном ресурсе данных в группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="2d49f-114">A job definition that has been correctly configured in a Hybrid Data Resource within a Resource Group.</span></span>
*   <span data-ttu-id="2d49f-115">Все необходимые hello библиотеки DLL.</span><span class="sxs-lookup"><span data-stu-id="2d49f-115">All hello required dlls.</span></span> <span data-ttu-id="2d49f-116">Загрузить эти библиотеки DLL с hello [репозитории GitHub](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/tree/master/Data_Manager_Job_Run/dlls).</span><span class="sxs-lookup"><span data-stu-id="2d49f-116">Download these dlls from hello [GitHub repository](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/tree/master/Data_Manager_Job_Run/dlls).</span></span>
*   <span data-ttu-id="2d49f-117">`Get-ConfigurationParams.ps1`[сценария](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Data_Manager_Job_Run/Get-ConfigurationParams.ps1) из репозитория github hello.</span><span class="sxs-lookup"><span data-stu-id="2d49f-117">`Get-ConfigurationParams.ps1` [script](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Data_Manager_Job_Run/Get-ConfigurationParams.ps1) from hello github repository.</span></span>

## <a name="step-by-step"></a><span data-ttu-id="2d49f-118">Пошаговое руководство</span><span class="sxs-lookup"><span data-stu-id="2d49f-118">Step-by-step</span></span>

<span data-ttu-id="2d49f-119">Выполните следующие шаги toouse .NET toolaunch задание преобразования данных hello.</span><span class="sxs-lookup"><span data-stu-id="2d49f-119">Perform hello following steps toouse .NET toolaunch a data transformation job.</span></span>

1. <span data-ttu-id="2d49f-120">параметры конфигурации tooretrieve hello, hello следующие действия:</span><span class="sxs-lookup"><span data-stu-id="2d49f-120">tooretrieve hello configuration parameters, do hello following steps:</span></span>
    1. <span data-ttu-id="2d49f-121">Загрузите hello `Get-ConfigurationParams.ps1` из скрипта репозитория github hello в `C:\DataTransformation` расположение.</span><span class="sxs-lookup"><span data-stu-id="2d49f-121">Download hello `Get-ConfigurationParams.ps1` from hello github repository script in `C:\DataTransformation` location.</span></span>
    1. <span data-ttu-id="2d49f-122">Запустите hello `Get-ConfigurationParams.ps1` сценарий из репозитория github hello.</span><span class="sxs-lookup"><span data-stu-id="2d49f-122">Run hello `Get-ConfigurationParams.ps1` script from hello github repository.</span></span> <span data-ttu-id="2d49f-123">Введите следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="2d49f-123">Type hello following command:</span></span>

        ```
        C:\DataTransformation\Get-ConfigurationParams.ps1 -SubscriptionName "AzureSubscriptionName" -ActiveDirectoryKey "AnyRandomPassword" -AppName "ApplicationName"
         ```
        <span data-ttu-id="2d49f-124">Можно передать в любые значения для hello ActiveDirectoryKey и AppName.</span><span class="sxs-lookup"><span data-stu-id="2d49f-124">You can pass in any values for hello ActiveDirectoryKey and AppName.</span></span>


2. <span data-ttu-id="2d49f-125">Этот скрипт выводит hello следующие значения:</span><span class="sxs-lookup"><span data-stu-id="2d49f-125">This script outputs hello following values:</span></span>
    * <span data-ttu-id="2d49f-126">Идентификатор клиента</span><span class="sxs-lookup"><span data-stu-id="2d49f-126">Client ID</span></span>
    * <span data-ttu-id="2d49f-127">Tenant ID</span><span class="sxs-lookup"><span data-stu-id="2d49f-127">Tenant ID</span></span>
    * <span data-ttu-id="2d49f-128">Active Directory ключ (аналогично hello один на введенный выше)</span><span class="sxs-lookup"><span data-stu-id="2d49f-128">Active Directory key (same as hello one entered above)</span></span>
    * <span data-ttu-id="2d49f-129">Идентификатор подписки</span><span class="sxs-lookup"><span data-stu-id="2d49f-129">Subscription ID</span></span>

3. <span data-ttu-id="2d49f-130">С помощью Visual Studio 2012, 2013 или 2015 создайте консольное приложение C# .NET.</span><span class="sxs-lookup"><span data-stu-id="2d49f-130">Using Visual Studio 2012, 2013 or 2015, create a C# .NET console application.</span></span>

    1. <span data-ttu-id="2d49f-131">Запустите **Visual Studio 2012, Visual Studio 2013 или Visual Studio 2015**.</span><span class="sxs-lookup"><span data-stu-id="2d49f-131">Launch **Visual Studio 2012/2013/2015**.</span></span>
    1. <span data-ttu-id="2d49f-132">Нажмите кнопку **файл**, слишком точки**New**и нажмите кнопку **проекта**.</span><span class="sxs-lookup"><span data-stu-id="2d49f-132">Click **File**, point too**New**, and click **Project**.</span></span>
    2. <span data-ttu-id="2d49f-133">Разверните раздел **Шаблоны** и выберите **Visual C#**.</span><span class="sxs-lookup"><span data-stu-id="2d49f-133">Expand **Templates**, and select **Visual C#**.</span></span>
    3. <span data-ttu-id="2d49f-134">Выберите **консольное приложение** hello списке типов проекта на hello вправо.</span><span class="sxs-lookup"><span data-stu-id="2d49f-134">Select **Console Application** from hello list of project types on hello right.</span></span>
    4. <span data-ttu-id="2d49f-135">Введите **DataTransformationApp** для hello **имя**.</span><span class="sxs-lookup"><span data-stu-id="2d49f-135">Enter **DataTransformationApp** for hello **Name**.</span></span>
    5. <span data-ttu-id="2d49f-136">Выберите **C:\DataTransformation** для hello **расположение**.</span><span class="sxs-lookup"><span data-stu-id="2d49f-136">Select **C:\DataTransformation** for hello **Location**.</span></span>
    6. <span data-ttu-id="2d49f-137">Нажмите кнопку **ОК** toocreate hello проекта.</span><span class="sxs-lookup"><span data-stu-id="2d49f-137">Click **OK** toocreate hello project.</span></span>

4.  <span data-ttu-id="2d49f-138">Теперь добавьте все библиотеки DLL в hello [библиотеки DLL](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/tree/master/Data_Manager_Job_Run/dlls) папке, что **ссылки** в созданном проекте hello.</span><span class="sxs-lookup"><span data-stu-id="2d49f-138">Now, add all DLLs present in hello [dlls](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/tree/master/Data_Manager_Job_Run/dlls) folder as **References** in hello project that you created.</span></span> <span data-ttu-id="2d49f-139">dll-файлы hello toodownload, hello следующие:</span><span class="sxs-lookup"><span data-stu-id="2d49f-139">toodownload hello dll files, do hello following:</span></span>

    1. <span data-ttu-id="2d49f-140">В Visual Studio перейдите слишком**представление > обозреватель решений**.</span><span class="sxs-lookup"><span data-stu-id="2d49f-140">In Visual Studio, go too**View > Solution Explorer**.</span></span>
    1. <span data-ttu-id="2d49f-141">Щелкните hello стрелка влево toohello проекта приложения преобразования данных.</span><span class="sxs-lookup"><span data-stu-id="2d49f-141">Click hello arrow toohello left of Data Transformation App project.</span></span> <span data-ttu-id="2d49f-142">Нажмите кнопку **ссылки** и щелкните правой кнопкой мыши слишком**добавить ссылку**.</span><span class="sxs-lookup"><span data-stu-id="2d49f-142">Click **References** and then right-click too**Add Reference**.</span></span>
    2. <span data-ttu-id="2d49f-143">Поиск расположения toohello папки hello пакеты, выберите все библиотеки DLL hello и щелкните **добавить**, а затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="2d49f-143">Browse toohello location of hello packages folder, select all hello DLLs and click **Add**, and then click **OK**.</span></span>

5. <span data-ttu-id="2d49f-144">Добавьте следующее hello **с помощью** toohello инструкций исходный файл (Program.cs) в проекте hello.</span><span class="sxs-lookup"><span data-stu-id="2d49f-144">Add hello following **using** statements toohello source file (Program.cs) in hello project.</span></span>

    ```
    using System;
    using System.Collections.Generic;
    using System.Threading;
    using Microsoft.Azure.Management.HybridData.Models;
    using Microsoft.Internal.Dms.DmsWebJob;
    using Microsoft.Internal.Dms.DmsWebJob.Contracts;
    ```


6. <span data-ttu-id="2d49f-145">Привет, следующий код инициализирует экземпляр задания преобразования данных hello.</span><span class="sxs-lookup"><span data-stu-id="2d49f-145">hello following code initializes hello data transformation job instance.</span></span> <span data-ttu-id="2d49f-146">Добавьте это в hello **метод Main**.</span><span class="sxs-lookup"><span data-stu-id="2d49f-146">Add this in hello **Main method**.</span></span> <span data-ttu-id="2d49f-147">Замените hello значения параметров конфигурации, полученный ранее.</span><span class="sxs-lookup"><span data-stu-id="2d49f-147">Replace hello values of configuration parameters as obtained earlier.</span></span> <span data-ttu-id="2d49f-148">Подключите hello значения **имя группы ресурсов** и **имя ресурса данных гибридных**.</span><span class="sxs-lookup"><span data-stu-id="2d49f-148">Plug in hello values of **Resource Group Name** and **Hybrid Data Resource name**.</span></span> <span data-ttu-id="2d49f-149">Hello **имя группы ресурсов** входит hello, на котором размещена hello гибридных данных ресурса, на какие hello определение задания был настроен.</span><span class="sxs-lookup"><span data-stu-id="2d49f-149">hello **Resource Group Name** is hello one that hosts hello Hybrid Data Resource on which hello job definition was configured.</span></span>

    ```
    // Setup hello configuration parameters.
    var configParams = new ConfigurationParams
    {
        ClientId = "client-id",
        TenantId = "tenant-id",
        ActiveDirectoryKey = "active-directory-key",
        SubscriptionId = "subscription-id",
        ResourceGroupName = "resource-group-name",
        ResourceName = "resource-name"
    };

    // Initialize hello Data Transformation Job instance.
    DataTransformationJob dataTransformationJob = new DataTransformationJob(configParams);

    ```

7. <span data-ttu-id="2d49f-150">Укажите hello, с какой hello определение задания должно toobe параметров запуска</span><span class="sxs-lookup"><span data-stu-id="2d49f-150">Specify hello parameters with which hello job definition needs toobe run</span></span>

    ```
    string jobDefinitionName = "job-definition-name";

    DataTransformationInput dataTransformationInput = dataTransformationJob.GetJobDefinitionParameters(jobDefinitionName);

    ```

    <span data-ttu-id="2d49f-151">(ИЛИ)</span><span class="sxs-lookup"><span data-stu-id="2d49f-151">(OR)</span></span>

    <span data-ttu-id="2d49f-152">Параметры определения задания hello toochange во время выполнения, затем добавьте hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="2d49f-152">If you want toochange hello job definition parameters during run time, then add hello following code:</span></span>

    ```
    string jobDefinitionName = "job-definition-name";
    // Must start with a '\'
    var rootDirectories = new List<string> {@"\root"};

    // Name of hello volume on hello StorSimple device.
    var volumeNames = new List<string> {"volume-name"};

    var dataTransformationInput = new DataTransformationInput
    {
        // If you require hello latest existing backup toobe picked else use TakeNow tootrigger a new backup.
        BackupChoice = BackupChoice.UseExistingLatest.ToString(),
        // Name of hello StorSimple device.
        DeviceName = "device-name",
        // Name of hello container in Azure storage where hello files will be placed after execution.
        ContainerName = "container-name",
        // File name filter (search pattern) toobe applied on files under hello root directory. * - Match all files.
        FileNameFilter = "*",
        // List of root directories.
        RootDirectories = rootDirectories,
        // Name of hello volume on StorSimple device on which hello relevant data is present. 
        VolumeNames = volumeNames
    };
    
    ```

8. <span data-ttu-id="2d49f-153">После инициализации hello добавьте следующий код tootrigger задание преобразования данных для определения задания hello hello.</span><span class="sxs-lookup"><span data-stu-id="2d49f-153">After hello initialization, add hello following code tootrigger a data transformation job on hello job definition.</span></span> <span data-ttu-id="2d49f-154">Подключите соответствующий hello **именем определения задания**.</span><span class="sxs-lookup"><span data-stu-id="2d49f-154">Plug in hello appropriate **Job Definition Name**.</span></span>

    ```
    // Trigger a job, retrieve hello jobId and hello retry interval for polling.
    int retryAfter;
    string jobId = dataTransformationJob.RunJobAsync(jobDefinitionName, 
    dataTransformationInput, out retryAfter);

    ```

9. <span data-ttu-id="2d49f-155">Это задание передает hello соответствующих файлах, присутствующих в корневом каталоге hello в указанном контейнере тома StorSimple toohello hello.</span><span class="sxs-lookup"><span data-stu-id="2d49f-155">This job uploads hello matched files present under hello root directory on hello StorSimple volume toohello specified container.</span></span> <span data-ttu-id="2d49f-156">При загрузке файла удалении сообщения в очереди hello (в hello одной учетной записи хранилища, контейнера hello) с hello одинаковые имена, как определение задания hello.</span><span class="sxs-lookup"><span data-stu-id="2d49f-156">When a file is uploaded, a message is dropped in hello queue (in hello same storage account as hello container) with hello same name as hello job definition.</span></span> <span data-ttu-id="2d49f-157">Это сообщение используется как триггер tooinitiate, дальнейшая обработка файла hello.</span><span class="sxs-lookup"><span data-stu-id="2d49f-157">This message can be used as a trigger tooinitiate any further processing of hello file.</span></span>

10. <span data-ttu-id="2d49f-158">После активации задание hello добавьте hello, после задания hello tootrack код завершения.</span><span class="sxs-lookup"><span data-stu-id="2d49f-158">Once hello job has been triggered, add hello following code tootrack hello job for completion.</span></span>

    ```
    Job jobDetails = null;

    // Poll hello job.
    do
    {
        jobDetails = dataTransformationJob.GetJob(jobDefinitionName, jobId);

        // Wait before polling for hello status again.
        Thread.Sleep(TimeSpan.FromSeconds(retryAfter));

    } while (jobDetails.Status == JobStatus.InProgress);

    // Completion status of hello job.
    Console.WriteLine("JobStatus: {0}", jobDetails.Status);
    
    // toohold hello console before exiting.
    Console.Read();

    ```


## <a name="next-steps"></a><span data-ttu-id="2d49f-159">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2d49f-159">Next steps</span></span>

<span data-ttu-id="2d49f-160">[Использовать пользовательский Интерфейс диспетчера данных StorSimple tootransform данные](storsimple-data-manager-ui.md).</span><span class="sxs-lookup"><span data-stu-id="2d49f-160">[Use StorSimple Data Manager UI tootransform your data](storsimple-data-manager-ui.md).</span></span>
