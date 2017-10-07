---
title: "aaaInstall .NET на ролях в облачных службах Azure | Документы Microsoft"
description: "В этой статье описывается toomanually установки hello .NET Framework на роли рабочих и веб-облачной службы"
services: cloud-services
documentationcenter: .net
author: thraka
manager: timlt
editor: 
ms.assetid: 8d1243dc-879c-4d1f-9ed0-eecd1f6a6653
ms.service: cloud-services
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/24/2017
ms.author: adegeo
ms.openlocfilehash: 45f0f30221292f98c591511b091b02ebe1c1272c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="install-net-on-azure-cloud-services-roles"></a><span data-ttu-id="b988a-103">Установка .NET для ролей облачных служб Azure</span><span class="sxs-lookup"><span data-stu-id="b988a-103">Install .NET on Azure Cloud Services roles</span></span>
<span data-ttu-id="b988a-104">В этой статье описывается, как tooinstall версии платформы .NET Framework, не входящие в состав hello гостевой ОС Azure.</span><span class="sxs-lookup"><span data-stu-id="b988a-104">This article describes how tooinstall versions of .NET Framework that don't come with hello Azure Guest OS.</span></span> <span data-ttu-id="b988a-105">Можно использовать .NET на гостевой ОС tooconfigure hello роли рабочих и веб-облачной службы.</span><span class="sxs-lookup"><span data-stu-id="b988a-105">You can use .NET on hello Guest OS tooconfigure your cloud service web and worker roles.</span></span>

<span data-ttu-id="b988a-106">Например можно установить .NET 4.6.1 на hello семейства гостевых ОС 4, который не входят в состав всех выпусков .NET 4.6.</span><span class="sxs-lookup"><span data-stu-id="b988a-106">For example, you can install .NET 4.6.1 on hello Guest OS family 4, which doesn't come with any release of .NET 4.6.</span></span> <span data-ttu-id="b988a-107">(hello семейства гостевой ОС 5 поставляются с .NET 4.6.) Для hello последнюю информацию относительно hello выпусков гостевой ОС Azure см. в разделе hello [новости выпуска гостевой ОС Azure](cloud-services-guestos-update-matrix.md).</span><span class="sxs-lookup"><span data-stu-id="b988a-107">(hello Guest OS family 5 does come with .NET 4.6.) For hello latest information on hello Azure Guest OS releases, see hello [Azure Guest OS release news](cloud-services-guestos-update-matrix.md).</span></span> 

>[!IMPORTANT]
><span data-ttu-id="b988a-108">Hello Azure SDK 2.9 содержит ограничения на развертывание .NET 4.6 в гостевой ОС семейства hello 4 или более ранней версии.</span><span class="sxs-lookup"><span data-stu-id="b988a-108">hello Azure SDK 2.9 contains a restriction on deploying .NET 4.6 on hello Guest OS family 4 or earlier.</span></span> <span data-ttu-id="b988a-109">Доступно исправление для hello ограничения на hello [документы Microsoft](https://github.com/MicrosoftDocs/azure-cloud-services-files/tree/master/Azure%20Targets%20SDK%202.9) сайта.</span><span class="sxs-lookup"><span data-stu-id="b988a-109">A fix for hello restriction is available on hello [Microsoft Docs](https://github.com/MicrosoftDocs/azure-cloud-services-files/tree/master/Azure%20Targets%20SDK%202.9) site.</span></span>

<span data-ttu-id="b988a-110">tooinstall .NET на веб- и рабочих ролей, включают веб-установщик .NET hello как часть проекта облачной службы.</span><span class="sxs-lookup"><span data-stu-id="b988a-110">tooinstall .NET on your web and worker roles, include hello .NET web installer as part of your cloud service project.</span></span> <span data-ttu-id="b988a-111">Запустите установщик hello как часть задач запуска роли hello.</span><span class="sxs-lookup"><span data-stu-id="b988a-111">Start hello installer as part of hello role's startup tasks.</span></span> 

## <a name="add-hello-net-installer-tooyour-project"></a><span data-ttu-id="b988a-112">Добавление проекта tooyour установщика .NET hello</span><span class="sxs-lookup"><span data-stu-id="b988a-112">Add hello .NET installer tooyour project</span></span>
<span data-ttu-id="b988a-113">toodownload hello веб-установщик для hello .NET Framework выберите версию hello, что требуется tooinstall:</span><span class="sxs-lookup"><span data-stu-id="b988a-113">toodownload hello web installer for hello .NET Framework, choose hello version that you want tooinstall:</span></span>

* <span data-ttu-id="b988a-114">[Веб-установщик .NET 4.7](http://go.microsoft.com/fwlink/?LinkId=825298).</span><span class="sxs-lookup"><span data-stu-id="b988a-114">[.NET 4.7 web installer](http://go.microsoft.com/fwlink/?LinkId=825298)</span></span>
* <span data-ttu-id="b988a-115">[Веб-установщик .NET 4.6.1](http://go.microsoft.com/fwlink/?LinkId=671729).</span><span class="sxs-lookup"><span data-stu-id="b988a-115">[.NET 4.6.1 web installer](http://go.microsoft.com/fwlink/?LinkId=671729)</span></span>

<span data-ttu-id="b988a-116">Установщик hello tooadd *web* роли:</span><span class="sxs-lookup"><span data-stu-id="b988a-116">tooadd hello installer for a *web* role:</span></span>
  1. <span data-ttu-id="b988a-117">В **обозревателе решений** в разделе **Роли** проекта облачной службы щелкните правой кнопкой мыши *веб-роль* и выберите **Добавить** > **Новая папка**.</span><span class="sxs-lookup"><span data-stu-id="b988a-117">In **Solution Explorer**, under **Roles** in your cloud service project, right-click your *web* role and select **Add** > **New Folder**.</span></span> <span data-ttu-id="b988a-118">Создайте папку с именем **bin**.</span><span class="sxs-lookup"><span data-stu-id="b988a-118">Create a folder named **bin**.</span></span>
  2. <span data-ttu-id="b988a-119">Щелкните правой кнопкой мыши папку bin hello и выберите **добавить** > **существующий элемент**.</span><span class="sxs-lookup"><span data-stu-id="b988a-119">Right-click hello bin folder and select **Add** > **Existing Item**.</span></span> <span data-ttu-id="b988a-120">Выберите установщик .NET hello и добавить его папку bin toohello.</span><span class="sxs-lookup"><span data-stu-id="b988a-120">Select hello .NET installer and add it toohello bin folder.</span></span>
  
<span data-ttu-id="b988a-121">Установщик hello tooadd *рабочих* роли:</span><span class="sxs-lookup"><span data-stu-id="b988a-121">tooadd hello installer for a *worker* role:</span></span>
* <span data-ttu-id="b988a-122">Щелкните правой кнопкой мыши *рабочую* роль и выберите **Добавить** > **Существующий элемент**.</span><span class="sxs-lookup"><span data-stu-id="b988a-122">Right-click your *worker* role and select **Add** > **Existing Item**.</span></span> <span data-ttu-id="b988a-123">Выберите установщик .NET hello и добавьте его toohello роли.</span><span class="sxs-lookup"><span data-stu-id="b988a-123">Select hello .NET installer and add it toohello role.</span></span> 

<span data-ttu-id="b988a-124">При добавлении файлов в папке содержимого роли toohello способом, они автоматически добавляются tooyour пакет облачной службы.</span><span class="sxs-lookup"><span data-stu-id="b988a-124">When files are added in this way toohello role content folder, they're automatically added tooyour cloud service package.</span></span> <span data-ttu-id="b988a-125">Hello файлы, затем последовательно развернутой tooa согласованное на виртуальной машине hello.</span><span class="sxs-lookup"><span data-stu-id="b988a-125">hello files are then deployed tooa consistent location on hello virtual machine.</span></span> <span data-ttu-id="b988a-126">Повторите эту процедуру для каждой из рабочих и веб-ролей в облачной службе, таким образом, что все роли копию установщика hello.</span><span class="sxs-lookup"><span data-stu-id="b988a-126">Repeat this process for each web and worker role in your cloud service so that all roles have a copy of hello installer.</span></span>

> [!NOTE]
> <span data-ttu-id="b988a-127">Установите .NET 4.6.1 в роль облачной службы, даже если приложению необходим .NET 4.6.</span><span class="sxs-lookup"><span data-stu-id="b988a-127">You should install .NET 4.6.1 on your cloud service role even if your application targets .NET 4.6.</span></span> <span data-ttu-id="b988a-128">Hello гостевой ОС содержит hello базы знаний [обновление 3098779](https://support.microsoft.com/kb/3098779) и [обновление 3097997](https://support.microsoft.com/kb/3097997).</span><span class="sxs-lookup"><span data-stu-id="b988a-128">hello Guest OS includes hello Knowledge Base [update 3098779](https://support.microsoft.com/kb/3098779) and [update 3097997](https://support.microsoft.com/kb/3097997).</span></span> <span data-ttu-id="b988a-129">Проблемы могут возникнуть при запуске приложений .NET, если .NET 4.6 устанавливается поверх hello базы знаний Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="b988a-129">Issues can occur when you run your .NET applications if .NET 4.6 is installed on top of hello Knowledge Base updates.</span></span> <span data-ttu-id="b988a-130">Эти проблемы tooavoid установить .NET 4.6.1 вместо версии 4.6.</span><span class="sxs-lookup"><span data-stu-id="b988a-130">tooavoid these issues, install .NET 4.6.1 rather than version 4.6.</span></span> <span data-ttu-id="b988a-131">Дополнительные сведения см. в разделе hello [статьи базы знаний 3118750](https://support.microsoft.com/kb/3118750).</span><span class="sxs-lookup"><span data-stu-id="b988a-131">For more information, see hello [Knowledge Base article 3118750](https://support.microsoft.com/kb/3118750).</span></span>
> 
> 

![Роль с файлами установщика][1]

## <a name="define-startup-tasks-for-your-roles"></a><span data-ttu-id="b988a-133">Определение начальных задач для ролей</span><span class="sxs-lookup"><span data-stu-id="b988a-133">Define startup tasks for your roles</span></span>
<span data-ttu-id="b988a-134">Можно использовать операции tooperform запуска задачи до запуска роли.</span><span class="sxs-lookup"><span data-stu-id="b988a-134">You can use startup tasks tooperform operations before a role starts.</span></span> <span data-ttu-id="b988a-135">Установка .NET Framework hello как часть задачи запуска hello гарантирует, что framework hello устанавливается перед выполнением любого кода приложения.</span><span class="sxs-lookup"><span data-stu-id="b988a-135">Installing hello .NET Framework as part of hello startup task ensures that hello framework is installed before any application code is run.</span></span> <span data-ttu-id="b988a-136">Дополнительные сведения о начальных задачах см. в статье [Как настроить и выполнить задачи запуска для облачной службы](cloud-services-startup-tasks.md).</span><span class="sxs-lookup"><span data-stu-id="b988a-136">For more information on startup tasks, see [Run startup tasks in Azure](cloud-services-startup-tasks.md).</span></span> 

1. <span data-ttu-id="b988a-137">Добавьте следующие файл ServiceDefinition.csdef содержимого toohello под hello hello **WebRole** или **WorkerRole** узел для всех ролей:</span><span class="sxs-lookup"><span data-stu-id="b988a-137">Add hello following content toohello ServiceDefinition.csdef file under hello **WebRole** or **WorkerRole** node for all roles:</span></span>
   
    ```xml
    <LocalResources>
      <LocalStorage name="NETFXInstall" sizeInMB="1024" cleanOnRoleRecycle="false" />
    </LocalResources>    
    <Startup>
      <Task commandLine="install.cmd" executionContext="elevated" taskType="simple">
        <Environment>
          <Variable name="PathToNETFXInstall">
            <RoleInstanceValue xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='NETFXInstall']/@path" />
          </Variable>
          <Variable name="ComputeEmulatorRunning">
            <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
          </Variable>
        </Environment>
      </Task>
    </Startup>
    ```
   
    <span data-ttu-id="b988a-138">Hello предыдущей конфигурации выполняется команда консоли hello `install.cmd` с tooinstall привилегии администратора hello .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="b988a-138">hello preceding configuration runs hello console command `install.cmd` with administrator privileges tooinstall hello .NET Framework.</span></span> <span data-ttu-id="b988a-139">Hello конфигурации также создает **LocalStorage** элемента с именем **NETFXInstall**.</span><span class="sxs-lookup"><span data-stu-id="b988a-139">hello configuration also creates a **LocalStorage** element named **NETFXInstall**.</span></span> <span data-ttu-id="b988a-140">сценарий запуска Hello задает hello временной папке toouse этого ресурса локального хранилища.</span><span class="sxs-lookup"><span data-stu-id="b988a-140">hello startup script sets hello temp folder toouse this local storage resource.</span></span> 
    
    > [!IMPORTANT]
    > <span data-ttu-id="b988a-141">tooensure исправление установки Framework hello, размер набора hello этот ресурс tooat бы 1024 МБ.</span><span class="sxs-lookup"><span data-stu-id="b988a-141">tooensure correct installation of hello framework, set hello size of this resource tooat least 1,024 MB.</span></span>
    
    <span data-ttu-id="b988a-142">Дополнительные сведения о задачах запуска см. в статье [Стандартные задачи запуска в облачной службе](cloud-services-startup-tasks-common.md).</span><span class="sxs-lookup"><span data-stu-id="b988a-142">For more information about startup tasks, see [Common Azure Cloud Services startup tasks](cloud-services-startup-tasks-common.md).</span></span>

2. <span data-ttu-id="b988a-143">Создайте файл с именем **install.cmd** и добавьте следующее hello установить toohello файл сценария.</span><span class="sxs-lookup"><span data-stu-id="b988a-143">Create a file named **install.cmd** and add hello following install script toohello file.</span></span>

    <span data-ttu-id="b988a-144">Hello скрипт проверяет, hello указанную версию .NET Framework hello уже установлены ли на компьютере hello путем отправки запроса реестр hello.</span><span class="sxs-lookup"><span data-stu-id="b988a-144">hello script checks whether hello specified version of hello .NET Framework is already installed on hello machine by querying hello registry.</span></span> <span data-ttu-id="b988a-145">Если не установлена версия hello .NET, веб-установщик .NET hello открывается.</span><span class="sxs-lookup"><span data-stu-id="b988a-145">If hello .NET version is not installed, then hello .NET web installer is opened.</span></span> <span data-ttu-id="b988a-146">toohelp поиска и устранения неполадок, скрипт hello регистрирует все действия toohello файл startuptasklog-(текущую дату и время) .txt, хранящиеся в **InstallLogs** локального хранилища.</span><span class="sxs-lookup"><span data-stu-id="b988a-146">toohelp troubleshoot any issues, hello script logs all activity toohello file startuptasklog-(current date and time).txt that is stored in **InstallLogs** local storage.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="b988a-147">Используйте простой текстовый редактор, как файл install.cmd hello toocreate программы Блокнот.</span><span class="sxs-lookup"><span data-stu-id="b988a-147">Use a basic text editor like Windows Notepad toocreate hello install.cmd file.</span></span> <span data-ttu-id="b988a-148">При использовании Visual Studio toocreate текстовый файл и измените расширение too.cmd hello, hello файл по-прежнему может содержать метку порядка байтов UTF-8.</span><span class="sxs-lookup"><span data-stu-id="b988a-148">If you use Visual Studio toocreate a text file and change hello extension too.cmd, hello file might still contain a UTF-8 byte order mark.</span></span> <span data-ttu-id="b988a-149">Марка может вызвать ошибку при выполнении первой строки скрипта hello hello.</span><span class="sxs-lookup"><span data-stu-id="b988a-149">This mark can cause an error when hello first line of hello script is run.</span></span> <span data-ttu-id="b988a-150">tooavoid эту ошибку, сделать hello первую строку hello скрипт оператор REM, могут быть пропущены при обработке порядок байтов hello.</span><span class="sxs-lookup"><span data-stu-id="b988a-150">tooavoid this error, make hello first line of hello script a REM statement that can be skipped by hello byte order processing.</span></span> 
    > 
    >
   
    ```cmd
    REM Set hello value of netfx tooinstall appropriate .NET Framework. 
    REM ***** tooinstall .NET 4.5.2 set hello variable netfx too"NDP452" *****
    REM ***** tooinstall .NET 4.6 set hello variable netfx too"NDP46" *****
    REM ***** tooinstall .NET 4.6.1 set hello variable netfx too"NDP461" *****
    REM ***** tooinstall .NET 4.6.2 set hello variable netfx too"NDP462" *****
    REM ***** tooinstall .NET 4.7 set hello variable netfx too"NDP47" *****
    set netfx="NDP47"

    REM ***** Set script start timestamp *****
    set timehour=%time:~0,2%
    set timestamp=%date:~-4,4%%date:~-10,2%%date:~-7,2%-%timehour: =0%%time:~3,2%
    set "log=install.cmd started %timestamp%."

    REM ***** Exit script if running in Emulator *****
    if %ComputeEmulatorRunning%=="true" goto exit

    REM ***** Needed toocorrectly install .NET 4.6.1, otherwise you may see an out of disk space error *****
    set TMP=%PathToNETFXInstall%
    set TEMP=%PathToNETFXInstall%

    REM ***** Setup .NET filenames and registry keys *****
    if %netfx%=="NDP47" goto NDP47
    if %netfx%=="NDP462" goto NDP462
    if %netfx%=="NDP461" goto NDP461
    if %netfx%=="NDP46" goto NDP46
        set "netfxinstallfile=NDP452-KB2901954-Web.exe"
        set netfxregkey="0x5cbf5"
        goto logtimestamp

    :NDP46
    set "netfxinstallfile=NDP46-KB3045560-Web.exe"
    set netfxregkey="0x6004f"
    goto logtimestamp

    :NDP461
    set "netfxinstallfile=NDP461-KB3102438-Web.exe"
    set netfxregkey="0x6040e"
    goto logtimestamp

    :NDP462
    set "netfxinstallfile=NDP462-KB3151802-Web.exe"
    set netfxregkey="0x60632"

    :NDP47
    set "netfxinstallfile=NDP47-KB3186500-Web.exe"
    set netfxregkey="0x707FE"

    :logtimestamp
    REM ***** Setup LogFile with timestamp *****
    md "%PathToNETFXInstall%\log"
    set startuptasklog="%PathToNETFXInstall%log\startuptasklog-%timestamp%.txt"
    set netfxinstallerlog="%PathToNETFXInstall%log\NetFXInstallerLog-%timestamp%"
    echo %log% >> %startuptasklog%
    echo Logfile generated at: %startuptasklog% >> %startuptasklog%
    echo TMP set to: %TMP% >> %startuptasklog%
    echo TEMP set to: %TEMP% >> %startuptasklog%

    REM ***** Check if .NET is installed *****
    echo Checking if .NET (%netfx%) is installed >> %startuptasklog%
    set /A netfxregkeydecimal=%netfxregkey%
    set foundkey=0
    FOR /F "usebackq skip=2 tokens=1,2*" %%A in (`reg query "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\NET Framework Setup\NDP\v4\Full" /v Release 2^>nul`) do @set /A foundkey=%%C
    echo Minimum required key: %netfxregkeydecimal% -- found key: %foundkey% >> %startuptasklog%
    if %foundkey% GEQ %netfxregkeydecimal% goto installed

    REM ***** Installing .NET *****
    echo Installing .NET with commandline: start /wait %~dp0%netfxinstallfile% /q /serialdownload /log %netfxinstallerlog%  /chainingpackage "CloudService Startup Task" >> %startuptasklog%
    start /wait %~dp0%netfxinstallfile% /q /serialdownload /log %netfxinstallerlog% /chainingpackage "CloudService Startup Task" >> %startuptasklog% 2>>&1
    if %ERRORLEVEL%== 0 goto installed
        echo .NET installer exited with code %ERRORLEVEL% >> %startuptasklog%    
        if %ERRORLEVEL%== 3010 goto restart
        if %ERRORLEVEL%== 1641 goto restart
        echo .NET (%netfx%) install failed with Error Code %ERRORLEVEL%. Further logs can be found in %netfxinstallerlog% >> %startuptasklog%

    :restart
    echo Restarting toocomplete .NET (%netfx%) installation >> %startuptasklog%
    EXIT /B %ERRORLEVEL%

    :installed
    echo .NET (%netfx%) is installed >> %startuptasklog%

    :end
    echo install.cmd completed: %date:~-4,4%%date:~-10,2%%date:~-7,2%-%timehour: =0%%time:~3,2% >> %startuptasklog%

    :exit
    EXIT /B 0
    ```
   
   > [!NOTE]
   > <span data-ttu-id="b988a-151">Этот сценарий показывает, как tooinstall .NET 4.5.2 или версии 4.6 для обеспечения непрерывности, даже если уже находится в .NET 4.5.2 hello гостевой ОС Azure.</span><span class="sxs-lookup"><span data-stu-id="b988a-151">This script shows how tooinstall .NET 4.5.2 or version 4.6 for continuity, even though .NET 4.5.2 is already available on hello Azure Guest OS.</span></span> <span data-ttu-id="b988a-152">Необходимо непосредственно установить .NET 4.6.1 вместо версии 4.6, как описано в hello [статьи базы знаний 3118750](https://support.microsoft.com/kb/3118750).</span><span class="sxs-lookup"><span data-stu-id="b988a-152">You should directly install .NET 4.6.1 rather than version 4.6, as described in hello [Knowledge Base article 3118750](https://support.microsoft.com/kb/3118750).</span></span>
   > 
   > 

3. <span data-ttu-id="b988a-153">Добавить роль hello install.cmd файл tooeach с помощью **добавить** > **существующий элемент** в **обозревателе решений** как описано ранее в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="b988a-153">Add hello install.cmd file tooeach role by using **Add** > **Existing Item** in **Solution Explorer** as described earlier in this topic.</span></span> 

    <span data-ttu-id="b988a-154">После завершения этого шага все роли должны иметь файл установщика .NET hello и файл install.cmd hello.</span><span class="sxs-lookup"><span data-stu-id="b988a-154">After this step is complete, all roles should have hello .NET installer file and hello install.cmd file.</span></span>

   ![Роль со всеми файлами][2]

## <a name="configure-diagnostics-tootransfer-startup-logs-tooblob-storage"></a><span data-ttu-id="b988a-156">Настройка диагностики tootransfer запуска журналы tooBlob хранилища</span><span class="sxs-lookup"><span data-stu-id="b988a-156">Configure Diagnostics tootransfer startup logs tooBlob storage</span></span>
<span data-ttu-id="b988a-157">Устранение неполадок установки toosimplify, можно настроить tootransfer диагностики Azure все файлы журналов, созданные при запуске hello скрипта или hello хранилища больших двоичных объектов tooAzure установщика .NET.</span><span class="sxs-lookup"><span data-stu-id="b988a-157">toosimplify troubleshooting installation issues, you can configure Azure Diagnostics tootransfer any log files generated by hello startup script or hello .NET installer tooAzure Blob storage.</span></span> <span data-ttu-id="b988a-158">Используя этот подход, можно просмотреть журналы hello загрузка файлов журнала hello из хранилища больших двоичных объектов, а не с рабочего стола tooremote в роль hello.</span><span class="sxs-lookup"><span data-stu-id="b988a-158">By using this approach, you can view hello logs by downloading hello log files from Blob storage rather than having tooremote desktop into hello role.</span></span>

<span data-ttu-id="b988a-159">tooconfigure диагностики, откройте файл diagnostics.wadcfgx hello и добавьте следующие содержимое в hello hello **каталоги** узла:</span><span class="sxs-lookup"><span data-stu-id="b988a-159">tooconfigure Diagnostics, open hello diagnostics.wadcfgx file and add hello following content under hello **Directories** node:</span></span> 

```xml 
<DataSources>
 <DirectoryConfiguration containerName="netfx-install">
  <LocalResource name="NETFXInstall" relativePath="log"/>
 </DirectoryConfiguration>
</DataSources>
```

<span data-ttu-id="b988a-160">Этот XML-документ настраивает диагностики tootransfer hello файлы в каталог журнала hello в hello **NETFXInstall** toohello ресурсов учетной записи хранения диагностики в hello **netfx install** контейнер больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="b988a-160">This XML configures Diagnostics tootransfer hello files in hello log directory in hello **NETFXInstall** resource toohello Diagnostics storage account in hello **netfx-install** blob container.</span></span>

## <a name="deploy-your-cloud-service"></a><span data-ttu-id="b988a-161">Развертывание облачной службы</span><span class="sxs-lookup"><span data-stu-id="b988a-161">Deploy your cloud service</span></span>
<span data-ttu-id="b988a-162">При развертывании облачной службы, задачи запуска hello установить hello .NET Framework, если он еще не установлен.</span><span class="sxs-lookup"><span data-stu-id="b988a-162">When you deploy your cloud service, hello startup tasks install hello .NET Framework if it's not already installed.</span></span> <span data-ttu-id="b988a-163">Роли облачной службы находятся в hello *занят* состояния при установке hello framework.</span><span class="sxs-lookup"><span data-stu-id="b988a-163">Your cloud service roles are in hello *busy* state while hello framework is being installed.</span></span> <span data-ttu-id="b988a-164">Если hello framework требуется для установки, службы ролей hello также может перезапуститься.</span><span class="sxs-lookup"><span data-stu-id="b988a-164">If hello framework installation requires a restart, hello service roles might also restart.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="b988a-165">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="b988a-165">Additional resources</span></span>
* <span data-ttu-id="b988a-166">[Установка .NET Framework hello][Installing hello .NET Framework]</span><span class="sxs-lookup"><span data-stu-id="b988a-166">[Installing hello .NET Framework][Installing hello .NET Framework]</span></span>
* <span data-ttu-id="b988a-167">[Практическое руководство. Определение установленных версий платформы .NET Framework][How to: Determine Which .NET Framework Versions Are Installed]</span><span class="sxs-lookup"><span data-stu-id="b988a-167">[Determine which .NET Framework versions are installed][How to: Determine Which .NET Framework Versions Are Installed]</span></span>
* <span data-ttu-id="b988a-168">[Устранение неполадок заблокированных установок и удалений .NET Framework][Troubleshooting .NET Framework Installations]</span><span class="sxs-lookup"><span data-stu-id="b988a-168">[Troubleshooting .NET Framework installations][Troubleshooting .NET Framework Installations]</span></span>

[How to: Determine Which .NET Framework Versions Are Installed]: https://msdn.microsoft.com/library/hh925568.aspx
[Installing hello .NET Framework]: https://msdn.microsoft.com/library/5a4x27ek.aspx
[Troubleshooting .NET Framework Installations]: https://msdn.microsoft.com/library/hh925569.aspx

<!--Image references-->
[1]: ./media/cloud-services-dotnet-install-dotnet/rolecontentwithinstallerfiles.png
[2]: ./media/cloud-services-dotnet-install-dotnet/rolecontentwithallfiles.png
