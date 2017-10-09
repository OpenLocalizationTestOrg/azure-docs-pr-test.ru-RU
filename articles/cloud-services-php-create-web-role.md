---
title: "aaaCreate Azure рабочих и веб-роли для PHP | Документы Microsoft"
description: "Руководство по toocreating PHP рабочих и веб-ролей в облачной службе Azure и настройка среды выполнения PHP hello."
services: 
documentationcenter: php
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 9f7ccda0-bd96-4f7b-a7af-fb279a9e975b
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 04a6e8c9c379cb0f854645941b6bc7d614bb91f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-php-web-and-worker-roles"></a>Как PHP toocreate рабочих и веб-роли
## <a name="overview"></a>Обзор
В этом руководстве будет показано, как toocreate PHP рабочих и веб-ролей в среде разработки Windows выберите конкретную версию PHP из hello «встроенные» доступных версий, изменение конфигурации PHP hello, включить расширения и наконец, развернуть tooAzure. В нем также рассматриваются как tooconfigure рабочих и веб-роли toouse выполнения PHP (с пользовательской конфигурации и расширения), указываемое.

## <a name="what-are-php-web-and-worker-roles"></a>Что такое веб-роли и рабочие роли PHP?
Azure предоставляет три вычислительные модели для запуска приложений: веб-приложения Azure, виртуальные машины Azure и облачные службы Azure. Все три модели поддерживают PHP. Облачные службы — это модель обслуживания типа *платформа как услуга (PaaS)*, в рамках которой используются веб-роли и рабочие роли. В облачной службе веб-роль предоставляет выделенный Internet Information Services (IIS) веб-сервера toohost интерфейсный веб-приложений. В рабочей роли могут выполняться асинхронные, долгосрочные или постоянные задачи, для которых не требуется взаимодействие с пользователем.

Подробнее об этих моделях можно узнать в статье о [вариантах размещения вычислительных сред, предоставляемых Azure](cloud-services/cloud-services-choose-me.md).

## <a name="download-hello-azure-sdk-for-php"></a>Скачать hello Azure SDK для PHP
Hello [пакет Azure SDK для PHP] состоит из нескольких компонентов. Эта статья будет использовать два из них: Azure PowerShell и Привет эмуляторы Azure. Эти два компонента может быть выполнена с помощью Microsoft Web Platform Installer hello. Дополнительные сведения см. в разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview).

## <a name="create-a-cloud-services-project"></a>Создание проекта облачных служб
Hello первым шагом в создании PHP рабочих и веб-роль — toocreate проекта службы Azure. проект службы Azure служит как логический контейнер для рабочих и веб-ролей и на нем hello проекта [службы определения службы(.csdef)] и [конфигурации службы (cscfg)] файлов.

toocreate новый проект служб Azure, запустить Azure PowerShell с правами администратора и выполните следующую команду hello:

    PS C:\>New-AzureServiceProject myProject

Эта команда создает новый каталог (`myProject`) toowhich, можно добавить веб- и рабочих ролей.

## <a name="add-php-web-or-worker-roles"></a>Добавление веб-ролей PHP и ролей работников
tooadd роли tooa PHP веб-проекта, запустите следующую команду из в корневом каталоге проекта hello hello:

    PS C:\myProject> Add-AzurePHPWebRole roleName

Для рабочей роли используйте следующую команду:

    PS C:\myProject> Add-AzurePHPWorkerRole roleName

> [!NOTE]
> Hello `roleName` параметр является необязательным. Если он опущен, имя роли hello будут создаваться автоматически. первый веб-роль Hello создан будет `WebRole1`, hello второй будет `WebRole2`, и т. д. будет Hello первая рабочая роль создана `WorkerRole1`, hello второй будет `WorkerRole2`, и т. д.
>
>

## <a name="specify-hello-built-in-php-version"></a>Укажите встроенные PHP версии hello
При добавлении PHP рабочих и веб-роли tooa проекта, файлы конфигурации hello проекта были изменены, чтобы при его развертывании будет установлен на каждом экземпляре рабочих и веб-приложения PHP. версия hello toosee PHP, который будет установлен по умолчанию, запустите следующую команду hello:

    PS C:\myProject> Get-AzureServiceProjectRoleRuntime

Hello выходные данные команды hello выше будет выглядеть toowhat приведен ниже. В этом примере hello `IsDefault` флаг установлен слишком`true` для PHP 5.3.17, что она будет установлена версия PHP по умолчанию hello.

```
Runtime Version     PackageUri                      IsDefault
------- -------     ----------                      ---------
Node 0.6.17         http://nodertncu.blob.core...   False
Node 0.6.20         http://nodertncu.blob.core...   True
Node 0.8.4          http://nodertncu.blob.core...   False
IISNode 0.1.21      http://nodertncu.blob.core...   True
Cache 1.8.0         http://nodertncu.blob.core...   True
PHP 5.3.17          http://nodertncu.blob.core...   True
PHP 5.4.0           http://nodertncu.blob.core...   False
```

Можно задать tooany версии среды выполнения PHP hello hello версий PHP, которые перечислены. Например, версия PHP hello tooset (для роли с именем hello `roleName`) too5.4.0 hello используйте следующую команду:

    PS C:\myProject> Set-AzureServiceProjectRole roleName php 5.4.0

> [!NOTE]
> Доступные версии PHP может измениться в будущих hello.
>
>

## <a name="customize-hello-built-in-php-runtime"></a>Настройка встроенных выполнения PHP hello
У вас есть полный контроль над hello конфигурацию среды выполнения PHP hello, которая устанавливается при выполнении hello описанные выше шаги, включая изменение `php.ini` параметры и Включение расширений.

toocustomize Здравствуйте встроенных среды выполнения PHP, выполните следующие действия:

1. Добавить новую папку с именем `php`, toohello `bin` каталог веб-роли. Для рабочей роли добавьте его корневой каталог toohello роли.
2. В hello `php` папки, создайте другую папку с именем `ext`. Поместите все `.dll` расширения файлов (например, `php_mongo.dll`), которые должны tooenable в этой папке.
3. Добавить `php.ini` файл toohello `php` папки. Включите любые пользовательские расширения и задайте любые директивы PHP в этом файле. Например, если требуется, чтобы tooturn `display_errors` на и включите hello `php_mongo.dll` расширением, содержимое hello вашей `php.ini` файла будет выглядеть следующим:

        display_errors=On
        extension=php_mongo.dll

> [!NOTE]
> Все параметры, которые не заданы явно в hello `php.ini` файл предоставляет будет автоматически устанавливать значения по умолчанию tootheir. Тем не менее, следует помнить, что вы можете добавить полный файл `php.ini` .
>
>

## <a name="use-your-own-php-runtime"></a>Использование собственной среды выполнения PHP
В некоторых случаях вместо выбора встроенных среды выполнения PHP и настроить его так, как описано выше вы можете tooprovide собственные среды выполнения PHP. Например, можно использовать hello одной среды выполнения PHP в веб- или рабочей роли, которая используется в среде разработки. Это позволяет упростить tooensure, что приложения hello не изменяет поведение в рабочей среде.

### <a name="configure-a-web-role-toouse-your-own-php-runtime"></a>Настройка toouse роли web собственные среды выполнения PHP
tooconfigure toouse роли web среды выполнения PHP, который предоставляется, выполните следующие действия.

1. Создайте проект службы Azure и добавьте веб-роль PHP, как описано в этом разделе ранее.
2. Создание `php` папки в hello `bin` папку, которая находится в корневом каталоге веб-роли, а затем добавьте вашей toohello среды выполнения (все двоичные файлы, файлы конфигурации, вложенные папки, т. д.) PHP `php` папки.
3. (НЕОБЯЗАТЕЛЬНО) Если вашей среды выполнения PHP использует hello [драйверы Майкрософт для PHP для SQL Server][sqlsrv drivers], потребуется tooconfigure вашей веб роль tooinstall [собственного клиента SQL Server 2012] [ sql native client] при его инициализации. toodo это, добавьте hello [установщик sqlncli.msi x64] toohello `bin` папки в корневом каталоге веб-роли. сценарий запуска Hello, описанные в следующем шаге hello автоматически будет выполняться hello установщика при подготовке hello роли. Если вашей среды выполнения PHP не использует hello драйверы Майкрософт для PHP для SQL Server, можно удалить следующую строку из hello сценарий, показанный на следующем шаге hello hello:

        msiexec /i sqlncli.msi /qn IACCEPTSQLNCLILICENSETERMS=YES
4. Определить задачи запуска, которая настраивает [Internet Information Services (IIS)] [ iis.net] toouse вашей toohandle среды выполнения PHP запросы для `.php` страницы. toodo это, откройте hello `setup_web.cmd` файла (в hello `bin` файла корневого каталога веб-роли) в текстовом редакторе и заменить его содержимое hello следующий скрипт:

    ```cmd
    @ECHO ON
    cd "%~dp0"

    if "%EMULATED%"=="true" exit /b 0

    msiexec /i sqlncli.msi /qn IACCEPTSQLNCLILICENSETERMS=YES

    SET PHP_FULL_PATH=%~dp0php\php-cgi.exe
    SET NEW_PATH=%PATH%;%RoleRoot%\base\x86

    %WINDIR%\system32\inetsrv\appcmd.exe set config -section:system.webServer/fastCgi /+"[fullPath='%PHP_FULL_PATH%',maxInstances='12',idleTimeout='60000',activityTimeout='3600',requestTimeout='60000',instanceMaxRequests='10000',protocol='NamedPipe',flushNamedPipe='False']" /commit:apphost
    %WINDIR%\system32\inetsrv\appcmd.exe set config -section:system.webServer/fastCgi /+"[fullPath='%PHP_FULL_PATH%'].environmentVariables.[name='PATH',value='%NEW_PATH%']" /commit:apphost
    %WINDIR%\system32\inetsrv\appcmd.exe set config -section:system.webServer/fastCgi /+"[fullPath='%PHP_FULL_PATH%'].environmentVariables.[name='PHP_FCGI_MAX_REQUESTS',value='10000']" /commit:apphost
    %WINDIR%\system32\inetsrv\appcmd.exe set config -section:system.webServer/handlers /+"[name='PHP',path='*.php',verb='GET,HEAD,POST',modules='FastCgiModule',scriptProcessor='%PHP_FULL_PATH%',resourceType='Either',requireAccess='Script']" /commit:apphost
    %WINDIR%\system32\inetsrv\appcmd.exe set config -section:system.webServer/fastCgi /"[fullPath='%PHP_FULL_PATH%'].queueLength:50000"
    ```
5. Добавление приложения файлы tooyour веб-роли в корневой каталог. Это будет hello веб-сервера в корневом каталоге.
6. Опубликовать приложение, как описано в hello [опубликовать приложение](#publish-your-application) разделе ниже.

> [!NOTE]
> Hello `download.ps1` сценария (в hello `bin` папки корневого каталога веб-роли hello) могут быть удалены после выполнения действий hello, описанные выше, с помощью собственного среды выполнения PHP.
>
>

### <a name="configure-a-worker-role-toouse-your-own-php-runtime"></a>Настройка рабочей роли toouse собственные среды выполнения PHP
tooconfigure toouse роли рабочей среды выполнения PHP, который предоставляется, выполните следующие действия.

1. Создайте проект службы Azure и добавьте рабочую роль PHP, как описано в этом разделе ранее.
2. Создать `php` папки в корневом каталоге hello рабочей роли и добавьте ваш toohello среды выполнения (все двоичные файлы, файлы конфигурации, вложенные папки, т. д.) PHP `php` папки.
3. (НЕОБЯЗАТЕЛЬНО) Если вашей среды выполнения PHP использует [драйверы Майкрософт для PHP для SQL Server][sqlsrv drivers], вам потребуется tooconfigure вашей рабочей роли tooinstall [собственного клиента SQL Server 2012] [ sql native client] при его инициализации. toodo это, добавьте hello [установщик sqlncli.msi x64] toohello рабочей роли корневого каталога. сценарий запуска Hello, описанные в следующем шаге hello автоматически будет выполняться hello установщика при подготовке hello роли. Если вашей среды выполнения PHP не использует hello драйверы Майкрософт для PHP для SQL Server, можно удалить следующую строку из hello сценарий, показанный на следующем шаге hello hello:

        msiexec /i sqlncli.msi /qn IACCEPTSQLNCLILICENSETERMS=YES
4. Определить задачи запуска, которая добавляет к `php.exe` переменной среды PATH исполняемый toohello рабочей роли при подготовке hello роли. toodo это, откройте hello `setup_worker.cmd` (в корневом каталоге hello рабочей роли) в текстовом редакторе и замените его содержимое hello следующий скрипт:

    ```cmd
    @echo on

    cd "%~dp0"

    echo Granting permissions for Network Service toohello web root directory...
    icacls ..\ /grant "Network Service":(OI)(CI)W
    if %ERRORLEVEL% neq 0 goto error
    echo OK

    if "%EMULATED%"=="true" exit /b 0

    msiexec /i sqlncli.msi /qn IACCEPTSQLNCLILICENSETERMS=YES

    setx Path "%PATH%;%~dp0php" /M

    if %ERRORLEVEL% neq 0 goto error

    echo SUCCESS
    exit /b 0

    :error

    echo FAILED
    exit /b -1
    ```
5. Добавление приложения файлы tooyour рабочей роли в корневой каталог.
6. Опубликовать приложение, как описано в hello [опубликовать приложение](#publish-your-application) разделе ниже.

## <a name="run-your-application-in-hello-compute-and-storage-emulators"></a>Запустите приложение hello эмуляторов вычислений и хранилища
Привет эмуляторы Azure предоставляют локальной среде, в котором можно протестировать приложение Azure перед его развертыванием в облаке toohello. Существуют некоторые различия между Привет эмуляторы и hello среды Azure. toounderstand это предпочтительнее. в разделе [использовать эмулятор хранилища Azure hello для разработки и тестирования](storage/common/storage-use-emulator.md).

Обратите внимание, что необходимо PHP локально установлен эмулятор вычислений toouse hello. Эмулятор вычислений Hello использовать ваш локальный toorun установки PHP ваше приложение.

toorun проект в Привет эмуляторы, выполните следующую команду из корневого каталога проекта hello:

    PS C:\MyProject> Start-AzureEmulator

Вы увидите примерно toothis выходные данные:

    Creating local package...
    Starting Emulator...
    Role is running at http://127.0.0.1:81
    Started

Вы увидите приложение, работающее в эмуляторе hello, открыв браузер и перейдя локальный адрес toohello показано в выходных данных hello (`http://127.0.0.1:81` в выходных данных примера hello выше).

toostop Привет эмуляторы, выполнить следующую команду:

    PS C:\MyProject> Stop-AzureEmulator

## <a name="publish-your-application"></a>Публикация приложения
toopublish приложение, необходимо импортировать toofirst вашей параметры публикации с помощью hello [команду Import-AzurePublishSettingsFile](https://msdn.microsoft.com/library/azure/dn790370.aspx) командлета. Затем приложение можно опубликовать с помощью hello [AzureServiceProject публикации](https://msdn.microsoft.com/library/azure/dn495166.aspx) командлета. Сведения о входе в разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview).

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения см. в разделе hello [Центр разработчика PHP](/develop/php/).

[пакет Azure SDK для PHP]: /develop/php/common-tasks/download-php-sdk/
[install ps and emulators]: http://go.microsoft.com/fwlink/p/?linkid=320376&clcid=0x409
[службы определения службы(.csdef)]: http://msdn.microsoft.com/library/windowsazure/ee758711.aspx
[конфигурации службы (cscfg)]: http://msdn.microsoft.com/library/windowsazure/ee758710.aspx
[iis.net]: http://www.iis.net/
[sql native client]: http://msdn.microsoft.com/sqlserver/aa937733.aspx
[sqlsrv drivers]: http://php.net/sqlsrv
[установщик sqlncli.msi x64]: http://go.microsoft.com/fwlink/?LinkID=239648
