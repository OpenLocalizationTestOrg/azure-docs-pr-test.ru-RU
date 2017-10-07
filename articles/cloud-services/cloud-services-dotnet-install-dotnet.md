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
# <a name="install-net-on-azure-cloud-services-roles"></a>Установка .NET для ролей облачных служб Azure
В этой статье описывается, как tooinstall версии платформы .NET Framework, не входящие в состав hello гостевой ОС Azure. Можно использовать .NET на гостевой ОС tooconfigure hello роли рабочих и веб-облачной службы.

Например можно установить .NET 4.6.1 на hello семейства гостевых ОС 4, который не входят в состав всех выпусков .NET 4.6. (hello семейства гостевой ОС 5 поставляются с .NET 4.6.) Для hello последнюю информацию относительно hello выпусков гостевой ОС Azure см. в разделе hello [новости выпуска гостевой ОС Azure](cloud-services-guestos-update-matrix.md). 

>[!IMPORTANT]
>Hello Azure SDK 2.9 содержит ограничения на развертывание .NET 4.6 в гостевой ОС семейства hello 4 или более ранней версии. Доступно исправление для hello ограничения на hello [документы Microsoft](https://github.com/MicrosoftDocs/azure-cloud-services-files/tree/master/Azure%20Targets%20SDK%202.9) сайта.

tooinstall .NET на веб- и рабочих ролей, включают веб-установщик .NET hello как часть проекта облачной службы. Запустите установщик hello как часть задач запуска роли hello. 

## <a name="add-hello-net-installer-tooyour-project"></a>Добавление проекта tooyour установщика .NET hello
toodownload hello веб-установщик для hello .NET Framework выберите версию hello, что требуется tooinstall:

* [Веб-установщик .NET 4.7](http://go.microsoft.com/fwlink/?LinkId=825298).
* [Веб-установщик .NET 4.6.1](http://go.microsoft.com/fwlink/?LinkId=671729).

Установщик hello tooadd *web* роли:
  1. В **обозревателе решений** в разделе **Роли** проекта облачной службы щелкните правой кнопкой мыши *веб-роль* и выберите **Добавить** > **Новая папка**. Создайте папку с именем **bin**.
  2. Щелкните правой кнопкой мыши папку bin hello и выберите **добавить** > **существующий элемент**. Выберите установщик .NET hello и добавить его папку bin toohello.
  
Установщик hello tooadd *рабочих* роли:
* Щелкните правой кнопкой мыши *рабочую* роль и выберите **Добавить** > **Существующий элемент**. Выберите установщик .NET hello и добавьте его toohello роли. 

При добавлении файлов в папке содержимого роли toohello способом, они автоматически добавляются tooyour пакет облачной службы. Hello файлы, затем последовательно развернутой tooa согласованное на виртуальной машине hello. Повторите эту процедуру для каждой из рабочих и веб-ролей в облачной службе, таким образом, что все роли копию установщика hello.

> [!NOTE]
> Установите .NET 4.6.1 в роль облачной службы, даже если приложению необходим .NET 4.6. Hello гостевой ОС содержит hello базы знаний [обновление 3098779](https://support.microsoft.com/kb/3098779) и [обновление 3097997](https://support.microsoft.com/kb/3097997). Проблемы могут возникнуть при запуске приложений .NET, если .NET 4.6 устанавливается поверх hello базы знаний Майкрософт. Эти проблемы tooavoid установить .NET 4.6.1 вместо версии 4.6. Дополнительные сведения см. в разделе hello [статьи базы знаний 3118750](https://support.microsoft.com/kb/3118750).
> 
> 

![Роль с файлами установщика][1]

## <a name="define-startup-tasks-for-your-roles"></a>Определение начальных задач для ролей
Можно использовать операции tooperform запуска задачи до запуска роли. Установка .NET Framework hello как часть задачи запуска hello гарантирует, что framework hello устанавливается перед выполнением любого кода приложения. Дополнительные сведения о начальных задачах см. в статье [Как настроить и выполнить задачи запуска для облачной службы](cloud-services-startup-tasks.md). 

1. Добавьте следующие файл ServiceDefinition.csdef содержимого toohello под hello hello **WebRole** или **WorkerRole** узел для всех ролей:
   
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
   
    Hello предыдущей конфигурации выполняется команда консоли hello `install.cmd` с tooinstall привилегии администратора hello .NET Framework. Hello конфигурации также создает **LocalStorage** элемента с именем **NETFXInstall**. сценарий запуска Hello задает hello временной папке toouse этого ресурса локального хранилища. 
    
    > [!IMPORTANT]
    > tooensure исправление установки Framework hello, размер набора hello этот ресурс tooat бы 1024 МБ.
    
    Дополнительные сведения о задачах запуска см. в статье [Стандартные задачи запуска в облачной службе](cloud-services-startup-tasks-common.md).

2. Создайте файл с именем **install.cmd** и добавьте следующее hello установить toohello файл сценария.

    Hello скрипт проверяет, hello указанную версию .NET Framework hello уже установлены ли на компьютере hello путем отправки запроса реестр hello. Если не установлена версия hello .NET, веб-установщик .NET hello открывается. toohelp поиска и устранения неполадок, скрипт hello регистрирует все действия toohello файл startuptasklog-(текущую дату и время) .txt, хранящиеся в **InstallLogs** локального хранилища.

    > [!IMPORTANT]
    > Используйте простой текстовый редактор, как файл install.cmd hello toocreate программы Блокнот. При использовании Visual Studio toocreate текстовый файл и измените расширение too.cmd hello, hello файл по-прежнему может содержать метку порядка байтов UTF-8. Марка может вызвать ошибку при выполнении первой строки скрипта hello hello. tooavoid эту ошибку, сделать hello первую строку hello скрипт оператор REM, могут быть пропущены при обработке порядок байтов hello. 
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
   > Этот сценарий показывает, как tooinstall .NET 4.5.2 или версии 4.6 для обеспечения непрерывности, даже если уже находится в .NET 4.5.2 hello гостевой ОС Azure. Необходимо непосредственно установить .NET 4.6.1 вместо версии 4.6, как описано в hello [статьи базы знаний 3118750](https://support.microsoft.com/kb/3118750).
   > 
   > 

3. Добавить роль hello install.cmd файл tooeach с помощью **добавить** > **существующий элемент** в **обозревателе решений** как описано ранее в этом разделе. 

    После завершения этого шага все роли должны иметь файл установщика .NET hello и файл install.cmd hello.

   ![Роль со всеми файлами][2]

## <a name="configure-diagnostics-tootransfer-startup-logs-tooblob-storage"></a>Настройка диагностики tootransfer запуска журналы tooBlob хранилища
Устранение неполадок установки toosimplify, можно настроить tootransfer диагностики Azure все файлы журналов, созданные при запуске hello скрипта или hello хранилища больших двоичных объектов tooAzure установщика .NET. Используя этот подход, можно просмотреть журналы hello загрузка файлов журнала hello из хранилища больших двоичных объектов, а не с рабочего стола tooremote в роль hello.

tooconfigure диагностики, откройте файл diagnostics.wadcfgx hello и добавьте следующие содержимое в hello hello **каталоги** узла: 

```xml 
<DataSources>
 <DirectoryConfiguration containerName="netfx-install">
  <LocalResource name="NETFXInstall" relativePath="log"/>
 </DirectoryConfiguration>
</DataSources>
```

Этот XML-документ настраивает диагностики tootransfer hello файлы в каталог журнала hello в hello **NETFXInstall** toohello ресурсов учетной записи хранения диагностики в hello **netfx install** контейнер больших двоичных объектов.

## <a name="deploy-your-cloud-service"></a>Развертывание облачной службы
При развертывании облачной службы, задачи запуска hello установить hello .NET Framework, если он еще не установлен. Роли облачной службы находятся в hello *занят* состояния при установке hello framework. Если hello framework требуется для установки, службы ролей hello также может перезапуститься. 

## <a name="additional-resources"></a>Дополнительные ресурсы
* [Установка .NET Framework hello][Installing hello .NET Framework]
* [Практическое руководство. Определение установленных версий платформы .NET Framework][How to: Determine Which .NET Framework Versions Are Installed]
* [Устранение неполадок заблокированных установок и удалений .NET Framework][Troubleshooting .NET Framework Installations]

[How to: Determine Which .NET Framework Versions Are Installed]: https://msdn.microsoft.com/library/hh925568.aspx
[Installing hello .NET Framework]: https://msdn.microsoft.com/library/5a4x27ek.aspx
[Troubleshooting .NET Framework Installations]: https://msdn.microsoft.com/library/hh925569.aspx

<!--Image references-->
[1]: ./media/cloud-services-dotnet-install-dotnet/rolecontentwithinstallerfiles.png
[2]: ./media/cloud-services-dotnet-install-dotnet/rolecontentwithallfiles.png
