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
# <a name="use-hello-net-sdk-tooinitiate-data-transformation-private-preview"></a>Используйте hello .net SDK tooinitiate преобразования данных (личной предварительной версии)

## <a name="overview"></a>Обзор

В этой статье объясняется, как можно использовать функцию преобразования данных hello в tootransform службы диспетчера StorSimple данных hello данные на устройстве StorSimple. Hello преобразованные данные затем используются другими службами Azure в облаке hello. статья Hello также имеет toohelp Пошаговое руководство создает образец .NET консольного приложения tooinitiate задание преобразования данных и затем отслеживать его завершения.

## <a name="prerequisites"></a>Предварительные требования

Перед началом работы убедитесь, что у вас есть следующие компоненты:
*   Система, в которой установлена среда Visual Studio 2012, 2013, 2015 или 2017.
*   Azure PowerShell установлен. [Скачать Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).
*   Параметры tooinitialize hello преобразования данных задания конфигурации (tooobtain эти параметры включены здесь инструкции).
*   Определение задания, которое правильно настроено в гибридном ресурсе данных в группе ресурсов.
*   Все необходимые hello библиотеки DLL. Загрузить эти библиотеки DLL с hello [репозитории GitHub](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/tree/master/Data_Manager_Job_Run/dlls).
*   `Get-ConfigurationParams.ps1`[сценария](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Data_Manager_Job_Run/Get-ConfigurationParams.ps1) из репозитория github hello.

## <a name="step-by-step"></a>Пошаговое руководство

Выполните следующие шаги toouse .NET toolaunch задание преобразования данных hello.

1. параметры конфигурации tooretrieve hello, hello следующие действия:
    1. Загрузите hello `Get-ConfigurationParams.ps1` из скрипта репозитория github hello в `C:\DataTransformation` расположение.
    1. Запустите hello `Get-ConfigurationParams.ps1` сценарий из репозитория github hello. Введите следующую команду hello:

        ```
        C:\DataTransformation\Get-ConfigurationParams.ps1 -SubscriptionName "AzureSubscriptionName" -ActiveDirectoryKey "AnyRandomPassword" -AppName "ApplicationName"
         ```
        Можно передать в любые значения для hello ActiveDirectoryKey и AppName.


2. Этот скрипт выводит hello следующие значения:
    * Идентификатор клиента
    * Tenant ID
    * Active Directory ключ (аналогично hello один на введенный выше)
    * Идентификатор подписки

3. С помощью Visual Studio 2012, 2013 или 2015 создайте консольное приложение C# .NET.

    1. Запустите **Visual Studio 2012, Visual Studio 2013 или Visual Studio 2015**.
    1. Нажмите кнопку **файл**, слишком точки**New**и нажмите кнопку **проекта**.
    2. Разверните раздел **Шаблоны** и выберите **Visual C#**.
    3. Выберите **консольное приложение** hello списке типов проекта на hello вправо.
    4. Введите **DataTransformationApp** для hello **имя**.
    5. Выберите **C:\DataTransformation** для hello **расположение**.
    6. Нажмите кнопку **ОК** toocreate hello проекта.

4.  Теперь добавьте все библиотеки DLL в hello [библиотеки DLL](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/tree/master/Data_Manager_Job_Run/dlls) папке, что **ссылки** в созданном проекте hello. dll-файлы hello toodownload, hello следующие:

    1. В Visual Studio перейдите слишком**представление > обозреватель решений**.
    1. Щелкните hello стрелка влево toohello проекта приложения преобразования данных. Нажмите кнопку **ссылки** и щелкните правой кнопкой мыши слишком**добавить ссылку**.
    2. Поиск расположения toohello папки hello пакеты, выберите все библиотеки DLL hello и щелкните **добавить**, а затем нажмите кнопку **ОК**.

5. Добавьте следующее hello **с помощью** toohello инструкций исходный файл (Program.cs) в проекте hello.

    ```
    using System;
    using System.Collections.Generic;
    using System.Threading;
    using Microsoft.Azure.Management.HybridData.Models;
    using Microsoft.Internal.Dms.DmsWebJob;
    using Microsoft.Internal.Dms.DmsWebJob.Contracts;
    ```


6. Привет, следующий код инициализирует экземпляр задания преобразования данных hello. Добавьте это в hello **метод Main**. Замените hello значения параметров конфигурации, полученный ранее. Подключите hello значения **имя группы ресурсов** и **имя ресурса данных гибридных**. Hello **имя группы ресурсов** входит hello, на котором размещена hello гибридных данных ресурса, на какие hello определение задания был настроен.

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

7. Укажите hello, с какой hello определение задания должно toobe параметров запуска

    ```
    string jobDefinitionName = "job-definition-name";

    DataTransformationInput dataTransformationInput = dataTransformationJob.GetJobDefinitionParameters(jobDefinitionName);

    ```

    (ИЛИ)

    Параметры определения задания hello toochange во время выполнения, затем добавьте hello, следующий код:

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

8. После инициализации hello добавьте следующий код tootrigger задание преобразования данных для определения задания hello hello. Подключите соответствующий hello **именем определения задания**.

    ```
    // Trigger a job, retrieve hello jobId and hello retry interval for polling.
    int retryAfter;
    string jobId = dataTransformationJob.RunJobAsync(jobDefinitionName, 
    dataTransformationInput, out retryAfter);

    ```

9. Это задание передает hello соответствующих файлах, присутствующих в корневом каталоге hello в указанном контейнере тома StorSimple toohello hello. При загрузке файла удалении сообщения в очереди hello (в hello одной учетной записи хранилища, контейнера hello) с hello одинаковые имена, как определение задания hello. Это сообщение используется как триггер tooinitiate, дальнейшая обработка файла hello.

10. После активации задание hello добавьте hello, после задания hello tootrack код завершения.

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


## <a name="next-steps"></a>Дальнейшие действия

[Использовать пользовательский Интерфейс диспетчера данных StorSimple tootransform данные](storsimple-data-manager-ui.md).
