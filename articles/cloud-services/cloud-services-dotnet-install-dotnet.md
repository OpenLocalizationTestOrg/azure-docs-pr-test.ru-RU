---
title: "Установка .NET для ролей облачных служб Azure | Документация Майкрософт"
description: "В этой статье описывается, как вручную установить платформу .NET Framework для веб-роли и рабочей роли облачной службы."
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
ms.openlocfilehash: a9cffa275ae6b9315b821d3160b17a997a1523f7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="install-net-on-azure-cloud-services-roles"></a><span data-ttu-id="450ca-103">Установка .NET для ролей облачных служб Azure</span><span class="sxs-lookup"><span data-stu-id="450ca-103">Install .NET on Azure Cloud Services roles</span></span>
<span data-ttu-id="450ca-104">В этой статье описывается установка версий платформы .NET Framework, которые не входят в состав гостевой ОС Azure.</span><span class="sxs-lookup"><span data-stu-id="450ca-104">This article describes how to install versions of .NET Framework that don't come with the Azure Guest OS.</span></span> <span data-ttu-id="450ca-105">.NET в гостевой ОС можно использовать для настройки веб-ролей и рабочих ролей облачной службы.</span><span class="sxs-lookup"><span data-stu-id="450ca-105">You can use .NET on the Guest OS to configure your cloud service web and worker roles.</span></span>

<span data-ttu-id="450ca-106">Например, можно установить .NET 4.6.1 в семействе версий 4 гостевых ОС, которые не входят в состав какого-либо из выпусков .NET 4.6.</span><span class="sxs-lookup"><span data-stu-id="450ca-106">For example, you can install .NET 4.6.1 on the Guest OS family 4, which doesn't come with any release of .NET 4.6.</span></span> <span data-ttu-id="450ca-107">(Семейство версий 5 гостевых ОС поставляется с NET 4.6.) Самые актуальные сведения о выпусках гостевой ОС Azure см. в статье [Таблица совместимости выпусков гостевых ОС Azure и пакетов SDK](cloud-services-guestos-update-matrix.md).</span><span class="sxs-lookup"><span data-stu-id="450ca-107">(The Guest OS family 5 does come with .NET 4.6.) For the latest information on the Azure Guest OS releases, see the [Azure Guest OS release news](cloud-services-guestos-update-matrix.md).</span></span> 

>[!IMPORTANT]
><span data-ttu-id="450ca-108">Пакет SDK 2.9 для Azure содержит ограничение на развертывание .NET 4.6 в семействе версий 4 гостевых ОС.</span><span class="sxs-lookup"><span data-stu-id="450ca-108">The Azure SDK 2.9 contains a restriction on deploying .NET 4.6 on the Guest OS family 4 or earlier.</span></span> <span data-ttu-id="450ca-109">Исправление ограничения доступно на сайте [документации Майкрософт](https://github.com/MicrosoftDocs/azure-cloud-services-files/tree/master/Azure%20Targets%20SDK%202.9).</span><span class="sxs-lookup"><span data-stu-id="450ca-109">A fix for the restriction is available on the [Microsoft Docs](https://github.com/MicrosoftDocs/azure-cloud-services-files/tree/master/Azure%20Targets%20SDK%202.9) site.</span></span>

<span data-ttu-id="450ca-110">Чтобы установить .NET для веб-ролей и рабочих ролей, включите веб-установщик .NET в качестве части проекта облачной службы.</span><span class="sxs-lookup"><span data-stu-id="450ca-110">To install .NET on your web and worker roles, include the .NET web installer as part of your cloud service project.</span></span> <span data-ttu-id="450ca-111">Запустите установщик в рамках задач запуска роли.</span><span class="sxs-lookup"><span data-stu-id="450ca-111">Start the installer as part of the role's startup tasks.</span></span> 

## <a name="add-the-net-installer-to-your-project"></a><span data-ttu-id="450ca-112">Добавление установщика .NET в проект</span><span class="sxs-lookup"><span data-stu-id="450ca-112">Add the .NET installer to your project</span></span>
<span data-ttu-id="450ca-113">Чтобы скачать веб-установщик для платформы .NET Framework, выберите версию, которую требуется установить:</span><span class="sxs-lookup"><span data-stu-id="450ca-113">To download the web installer for the .NET Framework, choose the version that you want to install:</span></span>

* <span data-ttu-id="450ca-114">[Веб-установщик .NET 4.7](http://go.microsoft.com/fwlink/?LinkId=825298).</span><span class="sxs-lookup"><span data-stu-id="450ca-114">[.NET 4.7 web installer](http://go.microsoft.com/fwlink/?LinkId=825298)</span></span>
* <span data-ttu-id="450ca-115">[Веб-установщик .NET 4.6.1](http://go.microsoft.com/fwlink/?LinkId=671729).</span><span class="sxs-lookup"><span data-stu-id="450ca-115">[.NET 4.6.1 web installer](http://go.microsoft.com/fwlink/?LinkId=671729)</span></span>

<span data-ttu-id="450ca-116">Чтобы добавить установщик для *веб*-роли:</span><span class="sxs-lookup"><span data-stu-id="450ca-116">To add the installer for a *web* role:</span></span>
  1. <span data-ttu-id="450ca-117">В **обозревателе решений** в разделе **Роли** проекта облачной службы щелкните правой кнопкой мыши *веб-роль* и выберите **Добавить** > **Новая папка**.</span><span class="sxs-lookup"><span data-stu-id="450ca-117">In **Solution Explorer**, under **Roles** in your cloud service project, right-click your *web* role and select **Add** > **New Folder**.</span></span> <span data-ttu-id="450ca-118">Создайте папку с именем **bin**.</span><span class="sxs-lookup"><span data-stu-id="450ca-118">Create a folder named **bin**.</span></span>
  2. <span data-ttu-id="450ca-119">Щелкните правой кнопкой мыши папку bin и выберите **Добавить** > **Существующий элемент**.</span><span class="sxs-lookup"><span data-stu-id="450ca-119">Right-click the bin folder and select **Add** > **Existing Item**.</span></span> <span data-ttu-id="450ca-120">Выберите установщик .NET и добавьте его в папку bin.</span><span class="sxs-lookup"><span data-stu-id="450ca-120">Select the .NET installer and add it to the bin folder.</span></span>
  
<span data-ttu-id="450ca-121">Чтобы добавить установщик для *рабочей* роли:</span><span class="sxs-lookup"><span data-stu-id="450ca-121">To add the installer for a *worker* role:</span></span>
* <span data-ttu-id="450ca-122">Щелкните правой кнопкой мыши *рабочую* роль и выберите **Добавить** > **Существующий элемент**.</span><span class="sxs-lookup"><span data-stu-id="450ca-122">Right-click your *worker* role and select **Add** > **Existing Item**.</span></span> <span data-ttu-id="450ca-123">Выберите установщик .NET и добавьте его в роль.</span><span class="sxs-lookup"><span data-stu-id="450ca-123">Select the .NET installer and add it to the role.</span></span> 

<span data-ttu-id="450ca-124">При добавлении файлов таким образом в папку содержимого роли они автоматически добавляются в пакет облачной службы.</span><span class="sxs-lookup"><span data-stu-id="450ca-124">When files are added in this way to the role content folder, they're automatically added to your cloud service package.</span></span> <span data-ttu-id="450ca-125">Файлы затем развертываются в согласованное расположение на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="450ca-125">The files are then deployed to a consistent location on the virtual machine.</span></span> <span data-ttu-id="450ca-126">Повторите эту процедуру для каждой веб-роли и рабочей роли в облачной службе, чтобы у всех ролей была копия установщика.</span><span class="sxs-lookup"><span data-stu-id="450ca-126">Repeat this process for each web and worker role in your cloud service so that all roles have a copy of the installer.</span></span>

> [!NOTE]
> <span data-ttu-id="450ca-127">Установите .NET 4.6.1 в роль облачной службы, даже если приложению необходим .NET 4.6.</span><span class="sxs-lookup"><span data-stu-id="450ca-127">You should install .NET 4.6.1 on your cloud service role even if your application targets .NET 4.6.</span></span> <span data-ttu-id="450ca-128">Гостевая ОС включает [обновление 3098779](https://support.microsoft.com/kb/3098779) и [обновление 3097997](https://support.microsoft.com/kb/3097997) базы знаний.</span><span class="sxs-lookup"><span data-stu-id="450ca-128">The Guest OS includes the Knowledge Base [update 3098779](https://support.microsoft.com/kb/3098779) and [update 3097997](https://support.microsoft.com/kb/3097997).</span></span> <span data-ttu-id="450ca-129">Проблемы могут возникнуть при запуске приложений .NET, если .NET 4.6 установлена поверх обновлений базы знаний Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="450ca-129">Issues can occur when you run your .NET applications if .NET 4.6 is installed on top of the Knowledge Base updates.</span></span> <span data-ttu-id="450ca-130">Чтобы избежать этих проблем, установите .NET 4.6.1 вместо версии 4.6.</span><span class="sxs-lookup"><span data-stu-id="450ca-130">To avoid these issues, install .NET 4.6.1 rather than version 4.6.</span></span> <span data-ttu-id="450ca-131">Дополнительные сведения см. в [статье базы знаний 3118750](https://support.microsoft.com/kb/3118750).</span><span class="sxs-lookup"><span data-stu-id="450ca-131">For more information, see the [Knowledge Base article 3118750](https://support.microsoft.com/kb/3118750).</span></span>
> 
> 

![Роль с файлами установщика][1]

## <a name="define-startup-tasks-for-your-roles"></a><span data-ttu-id="450ca-133">Определение начальных задач для ролей</span><span class="sxs-lookup"><span data-stu-id="450ca-133">Define startup tasks for your roles</span></span>
<span data-ttu-id="450ca-134">С помощью задач запуска вы можете выполнять различные операции перед запуском роли.</span><span class="sxs-lookup"><span data-stu-id="450ca-134">You can use startup tasks to perform operations before a role starts.</span></span> <span data-ttu-id="450ca-135">Установка платформы .NET Framework как части начальной задачи позволяет установить платформу до того, как будет запущено выполнение программного кода.</span><span class="sxs-lookup"><span data-stu-id="450ca-135">Installing the .NET Framework as part of the startup task ensures that the framework is installed before any application code is run.</span></span> <span data-ttu-id="450ca-136">Дополнительные сведения о начальных задачах см. в статье [Как настроить и выполнить задачи запуска для облачной службы](cloud-services-startup-tasks.md).</span><span class="sxs-lookup"><span data-stu-id="450ca-136">For more information on startup tasks, see [Run startup tasks in Azure](cloud-services-startup-tasks.md).</span></span> 

1. <span data-ttu-id="450ca-137">В файл ServiceDefinition.csdef в узле **WebRole** или **WorkerRole** добавьте для всех ролей следующее содержимое:</span><span class="sxs-lookup"><span data-stu-id="450ca-137">Add the following content to the ServiceDefinition.csdef file under the **WebRole** or **WorkerRole** node for all roles:</span></span>
   
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
   
    <span data-ttu-id="450ca-138">Предыдущая конфигурация выполняет консольную команду `install.cmd` с правами администратора и устанавливает платформу .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="450ca-138">The preceding configuration runs the console command `install.cmd` with administrator privileges to install the .NET Framework.</span></span> <span data-ttu-id="450ca-139">Конфигурация также создает элемент **LocalStorage** с именем **NETFXInstall**.</span><span class="sxs-lookup"><span data-stu-id="450ca-139">The configuration also creates a **LocalStorage** element named **NETFXInstall**.</span></span> <span data-ttu-id="450ca-140">Сценарий запуска задает временную папку для использования этого локального ресурса хранилища.</span><span class="sxs-lookup"><span data-stu-id="450ca-140">The startup script sets the temp folder to use this local storage resource.</span></span> 
    
    > [!IMPORTANT]
    > <span data-ttu-id="450ca-141">Для обеспечения правильной установки платформы размер этого ресурса должен быть не менее 1024 МБ.</span><span class="sxs-lookup"><span data-stu-id="450ca-141">To ensure correct installation of the framework, set the size of this resource to at least 1,024 MB.</span></span>
    
    <span data-ttu-id="450ca-142">Дополнительные сведения о задачах запуска см. в статье [Стандартные задачи запуска в облачной службе](cloud-services-startup-tasks-common.md).</span><span class="sxs-lookup"><span data-stu-id="450ca-142">For more information about startup tasks, see [Common Azure Cloud Services startup tasks](cloud-services-startup-tasks-common.md).</span></span>

2. <span data-ttu-id="450ca-143">Создайте файл с именем **install.cmd** и добавьте в него следующий скрипт установки.</span><span class="sxs-lookup"><span data-stu-id="450ca-143">Create a file named **install.cmd** and add the following install script to the file.</span></span>

    <span data-ttu-id="450ca-144">Скрипт путем поиска по реестру проверяет, установлена ли на компьютере выбранная версия .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="450ca-144">The script checks whether the specified version of the .NET Framework is already installed on the machine by querying the registry.</span></span> <span data-ttu-id="450ca-145">Если требуемая версия .NET не установлена, открывается веб-установщик .NET.</span><span class="sxs-lookup"><span data-stu-id="450ca-145">If the .NET version is not installed, then the .NET web installer is opened.</span></span> <span data-ttu-id="450ca-146">Для помощи в устранении возникших проблем скрипт регистрирует все действия в файл startuptasklog-(текущая дата и время).txt, который хранится в локальном хранилище **InstallLogs**.</span><span class="sxs-lookup"><span data-stu-id="450ca-146">To help troubleshoot any issues, the script logs all activity to the file startuptasklog-(current date and time).txt that is stored in **InstallLogs** local storage.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="450ca-147">Для создания файла install.cmd используйте простой текстовый редактор, например Блокнот.</span><span class="sxs-lookup"><span data-stu-id="450ca-147">Use a basic text editor like Windows Notepad to create the install.cmd file.</span></span> <span data-ttu-id="450ca-148">Если для создания текстового файла и изменения расширения на .cmd используется Visual Studio, файл по-прежнему может содержать метку порядка байтов UTF-8.</span><span class="sxs-lookup"><span data-stu-id="450ca-148">If you use Visual Studio to create a text file and change the extension to .cmd, the file might still contain a UTF-8 byte order mark.</span></span> <span data-ttu-id="450ca-149">Эта метка может вызвать ошибку при выполнении первой строки скрипта.</span><span class="sxs-lookup"><span data-stu-id="450ca-149">This mark can cause an error when the first line of the script is run.</span></span> <span data-ttu-id="450ca-150">Чтобы избежать этой ошибки, сделайте первую строку скрипта оператором REM, который может быть пропущен при обработке порядка байтов.</span><span class="sxs-lookup"><span data-stu-id="450ca-150">To avoid this error, make the first line of the script a REM statement that can be skipped by the byte order processing.</span></span> 
    > 
    >
   
    ```cmd
    REM Set the value of netfx to install appropriate .NET Framework. 
    REM ***** To install .NET 4.5.2 set the variable netfx to "NDP452" *****
    REM ***** To install .NET 4.6 set the variable netfx to "NDP46" *****
    REM ***** To install .NET 4.6.1 set the variable netfx to "NDP461" *****
    REM ***** To install .NET 4.6.2 set the variable netfx to "NDP462" *****
    REM ***** To install .NET 4.7 set the variable netfx to "NDP47" *****
    set netfx="NDP47"

    REM ***** Set script start timestamp *****
    set timehour=%time:~0,2%
    set timestamp=%date:~-4,4%%date:~-10,2%%date:~-7,2%-%timehour: =0%%time:~3,2%
    set "log=install.cmd started %timestamp%."

    REM ***** Exit script if running in Emulator *****
    if %ComputeEmulatorRunning%=="true" goto exit

    REM ***** Needed to correctly install .NET 4.6.1, otherwise you may see an out of disk space error *****
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
    echo Restarting to complete .NET (%netfx%) installation >> %startuptasklog%
    EXIT /B %ERRORLEVEL%

    :installed
    echo .NET (%netfx%) is installed >> %startuptasklog%

    :end
    echo install.cmd completed: %date:~-4,4%%date:~-10,2%%date:~-7,2%-%timehour: =0%%time:~3,2% >> %startuptasklog%

    :exit
    EXIT /B 0
    ```
   
   > [!NOTE]
   > <span data-ttu-id="450ca-151">Этот скрипт показывает, как установить .NET 4.5.2 или 4.6 для обеспечения непрерывности работы, несмотря на то что версия .NET 4.5.2 уже доступна в гостевой ОС Azure.</span><span class="sxs-lookup"><span data-stu-id="450ca-151">This script shows how to install .NET 4.5.2 or version 4.6 for continuity, even though .NET 4.5.2 is already available on the Azure Guest OS.</span></span> <span data-ttu-id="450ca-152">Необходимо сразу же установить .NET 4.6.1 вместо версии 4.6, как описано в [статье базы знаний 3118750](https://support.microsoft.com/kb/3118750).</span><span class="sxs-lookup"><span data-stu-id="450ca-152">You should directly install .NET 4.6.1 rather than version 4.6, as described in the [Knowledge Base article 3118750](https://support.microsoft.com/kb/3118750).</span></span>
   > 
   > 

3. <span data-ttu-id="450ca-153">Добавьте файл install.cmd для каждой роли, используя команды **Добавить** > **Существующий элемент** в **обозревателе решений**, как описано ранее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="450ca-153">Add the install.cmd file to each role by using **Add** > **Existing Item** in **Solution Explorer** as described earlier in this topic.</span></span> 

    <span data-ttu-id="450ca-154">После завершения этого шага все роли должны иметь файл установщика .NET и файл install.cmd.</span><span class="sxs-lookup"><span data-stu-id="450ca-154">After this step is complete, all roles should have the .NET installer file and the install.cmd file.</span></span>

   ![Роль со всеми файлами][2]

## <a name="configure-diagnostics-to-transfer-startup-logs-to-blob-storage"></a><span data-ttu-id="450ca-156">Настройка диагностики для передачи журналов задач запуска в хранилище BLOB-объектов</span><span class="sxs-lookup"><span data-stu-id="450ca-156">Configure Diagnostics to transfer startup logs to Blob storage</span></span>
<span data-ttu-id="450ca-157">Чтобы упростить устранение неполадок при установке, можно настроить в системе диагностики Microsoft Azure передачу всех файлов журналов, созданных скриптом запуска или установщиком .NET, в хранилище BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="450ca-157">To simplify troubleshooting installation issues, you can configure Azure Diagnostics to transfer any log files generated by the startup script or the .NET installer to Azure Blob storage.</span></span> <span data-ttu-id="450ca-158">Это позволит просматривать журналы, скачивая их из хранилища BLOB-объектов, а не на удаленном рабочем столе, где хранится роль.</span><span class="sxs-lookup"><span data-stu-id="450ca-158">By using this approach, you can view the logs by downloading the log files from Blob storage rather than having to remote desktop into the role.</span></span>

<span data-ttu-id="450ca-159">Чтобы настроить систему диагностики, откройте файл diagnostics.wadcfgx и добавьте в узел **Directories** следующее содержимое:</span><span class="sxs-lookup"><span data-stu-id="450ca-159">To configure Diagnostics, open the diagnostics.wadcfgx file and add the following content under the **Directories** node:</span></span> 

```xml 
<DataSources>
 <DirectoryConfiguration containerName="netfx-install">
  <LocalResource name="NETFXInstall" relativePath="log"/>
 </DirectoryConfiguration>
</DataSources>
```

<span data-ttu-id="450ca-160">Этот XML-код позволяет системе диагностики передавать файлы из каталога log в ресурсе **NETFXInstall** в учетную запись хранения диагностических данных в контейнере больших двоичных объектов **netfx-install**.</span><span class="sxs-lookup"><span data-stu-id="450ca-160">This XML configures Diagnostics to transfer the files in the log directory in the **NETFXInstall** resource to the Diagnostics storage account in the **netfx-install** blob container.</span></span>

## <a name="deploy-your-cloud-service"></a><span data-ttu-id="450ca-161">Развертывание облачной службы</span><span class="sxs-lookup"><span data-stu-id="450ca-161">Deploy your cloud service</span></span>
<span data-ttu-id="450ca-162">При развертывании облачной службы задачи запуска устанавливают платформу .NET Framework, если она еще не установлена.</span><span class="sxs-lookup"><span data-stu-id="450ca-162">When you deploy your cloud service, the startup tasks install the .NET Framework if it's not already installed.</span></span> <span data-ttu-id="450ca-163">Роли облачной службы находятся в состоянии *занятости* при установке платформы.</span><span class="sxs-lookup"><span data-stu-id="450ca-163">Your cloud service roles are in the *busy* state while the framework is being installed.</span></span> <span data-ttu-id="450ca-164">Если при установке платформы необходима перезагрузка, роли службы также могут перезапуститься.</span><span class="sxs-lookup"><span data-stu-id="450ca-164">If the framework installation requires a restart, the service roles might also restart.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="450ca-165">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="450ca-165">Additional resources</span></span>
* <span data-ttu-id="450ca-166">[Установка платформы .NET Framework][Installing the .NET Framework]</span><span class="sxs-lookup"><span data-stu-id="450ca-166">[Installing the .NET Framework][Installing the .NET Framework]</span></span>
* <span data-ttu-id="450ca-167">[Практическое руководство. Определение установленных версий платформы .NET Framework][How to: Determine Which .NET Framework Versions Are Installed]</span><span class="sxs-lookup"><span data-stu-id="450ca-167">[Determine which .NET Framework versions are installed][How to: Determine Which .NET Framework Versions Are Installed]</span></span>
* <span data-ttu-id="450ca-168">[Устранение неполадок заблокированных установок и удалений .NET Framework][Troubleshooting .NET Framework Installations]</span><span class="sxs-lookup"><span data-stu-id="450ca-168">[Troubleshooting .NET Framework installations][Troubleshooting .NET Framework Installations]</span></span>

[How to: Determine Which .NET Framework Versions Are Installed]: https://msdn.microsoft.com/library/hh925568.aspx
[Installing the .NET Framework]: https://msdn.microsoft.com/library/5a4x27ek.aspx
[Troubleshooting .NET Framework Installations]: https://msdn.microsoft.com/library/hh925569.aspx

<!--Image references-->
[1]: ./media/cloud-services-dotnet-install-dotnet/rolecontentwithinstallerfiles.png
[2]: ./media/cloud-services-dotnet-install-dotnet/rolecontentwithallfiles.png
