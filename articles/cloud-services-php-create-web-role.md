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
# <a name="how-toocreate-php-web-and-worker-roles"></a><span data-ttu-id="c45f6-103">Как PHP toocreate рабочих и веб-роли</span><span class="sxs-lookup"><span data-stu-id="c45f6-103">How toocreate PHP web and worker roles</span></span>
## <a name="overview"></a><span data-ttu-id="c45f6-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="c45f6-104">Overview</span></span>
<span data-ttu-id="c45f6-105">В этом руководстве будет показано, как toocreate PHP рабочих и веб-ролей в среде разработки Windows выберите конкретную версию PHP из hello «встроенные» доступных версий, изменение конфигурации PHP hello, включить расширения и наконец, развернуть tooAzure.</span><span class="sxs-lookup"><span data-stu-id="c45f6-105">This guide will show you how toocreate PHP web or worker roles in a Windows development environment, choose a specific version of PHP from hello "built-in" versions available, change hello PHP configuration, enable extensions, and finally, deploy tooAzure.</span></span> <span data-ttu-id="c45f6-106">В нем также рассматриваются как tooconfigure рабочих и веб-роли toouse выполнения PHP (с пользовательской конфигурации и расширения), указываемое.</span><span class="sxs-lookup"><span data-stu-id="c45f6-106">It also describes how tooconfigure a web or worker role toouse a PHP runtime (with custom configuration and extensions) that you provide.</span></span>

## <a name="what-are-php-web-and-worker-roles"></a><span data-ttu-id="c45f6-107">Что такое веб-роли и рабочие роли PHP?</span><span class="sxs-lookup"><span data-stu-id="c45f6-107">What are PHP web and worker roles?</span></span>
<span data-ttu-id="c45f6-108">Azure предоставляет три вычислительные модели для запуска приложений: веб-приложения Azure, виртуальные машины Azure и облачные службы Azure.</span><span class="sxs-lookup"><span data-stu-id="c45f6-108">Azure provides three compute models for running applications: Azure App Service, Azure Virtual Machines, and Azure Cloud Services.</span></span> <span data-ttu-id="c45f6-109">Все три модели поддерживают PHP.</span><span class="sxs-lookup"><span data-stu-id="c45f6-109">All three models support PHP.</span></span> <span data-ttu-id="c45f6-110">Облачные службы — это модель обслуживания типа *платформа как услуга (PaaS)*, в рамках которой используются веб-роли и рабочие роли.</span><span class="sxs-lookup"><span data-stu-id="c45f6-110">Cloud Services, which includes web and worker roles, provides *platform as a service (PaaS)*.</span></span> <span data-ttu-id="c45f6-111">В облачной службе веб-роль предоставляет выделенный Internet Information Services (IIS) веб-сервера toohost интерфейсный веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="c45f6-111">Within a cloud service, a web role provides a dedicated Internet Information Services (IIS) web server toohost front-end web applications.</span></span> <span data-ttu-id="c45f6-112">В рабочей роли могут выполняться асинхронные, долгосрочные или постоянные задачи, для которых не требуется взаимодействие с пользователем.</span><span class="sxs-lookup"><span data-stu-id="c45f6-112">A worker role can run asynchronous, long-running or perpetual tasks independent of user interaction or input.</span></span>

<span data-ttu-id="c45f6-113">Подробнее об этих моделях можно узнать в статье о [вариантах размещения вычислительных сред, предоставляемых Azure](cloud-services/cloud-services-choose-me.md).</span><span class="sxs-lookup"><span data-stu-id="c45f6-113">For more information about these options, see [Compute hosting options provided by Azure](cloud-services/cloud-services-choose-me.md).</span></span>

## <a name="download-hello-azure-sdk-for-php"></a><span data-ttu-id="c45f6-114">Скачать hello Azure SDK для PHP</span><span class="sxs-lookup"><span data-stu-id="c45f6-114">Download hello Azure SDK for PHP</span></span>
<span data-ttu-id="c45f6-115">Hello [пакет Azure SDK для PHP] состоит из нескольких компонентов.</span><span class="sxs-lookup"><span data-stu-id="c45f6-115">hello [Azure SDK for PHP] consists of several components.</span></span> <span data-ttu-id="c45f6-116">Эта статья будет использовать два из них: Azure PowerShell и Привет эмуляторы Azure.</span><span class="sxs-lookup"><span data-stu-id="c45f6-116">This article will use two of them: Azure PowerShell and hello Azure emulators.</span></span> <span data-ttu-id="c45f6-117">Эти два компонента может быть выполнена с помощью Microsoft Web Platform Installer hello.</span><span class="sxs-lookup"><span data-stu-id="c45f6-117">These two components can be installed via hello Microsoft Web Platform Installer.</span></span> <span data-ttu-id="c45f6-118">Дополнительные сведения см. в разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c45f6-118">For more information, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="create-a-cloud-services-project"></a><span data-ttu-id="c45f6-119">Создание проекта облачных служб</span><span class="sxs-lookup"><span data-stu-id="c45f6-119">Create a Cloud Services project</span></span>
<span data-ttu-id="c45f6-120">Hello первым шагом в создании PHP рабочих и веб-роль — toocreate проекта службы Azure.</span><span class="sxs-lookup"><span data-stu-id="c45f6-120">hello first step in creating a PHP web or worker role is toocreate an Azure Service project.</span></span> <span data-ttu-id="c45f6-121">проект службы Azure служит как логический контейнер для рабочих и веб-ролей и на нем hello проекта [службы определения службы(.csdef)] и [конфигурации службы (cscfg)] файлов.</span><span class="sxs-lookup"><span data-stu-id="c45f6-121">an Azure Service project serves as a logical container for web and worker roles, and it contains hello project's [service definition (.csdef)] and [service configuration (.cscfg)] files.</span></span>

<span data-ttu-id="c45f6-122">toocreate новый проект служб Azure, запустить Azure PowerShell с правами администратора и выполните следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="c45f6-122">toocreate a new Azure Service project, run Azure PowerShell as an administrator, and execute hello following command:</span></span>

    PS C:\>New-AzureServiceProject myProject

<span data-ttu-id="c45f6-123">Эта команда создает новый каталог (`myProject`) toowhich, можно добавить веб- и рабочих ролей.</span><span class="sxs-lookup"><span data-stu-id="c45f6-123">This command will create a new directory (`myProject`) toowhich you can add web and worker roles.</span></span>

## <a name="add-php-web-or-worker-roles"></a><span data-ttu-id="c45f6-124">Добавление веб-ролей PHP и ролей работников</span><span class="sxs-lookup"><span data-stu-id="c45f6-124">Add PHP web or worker roles</span></span>
<span data-ttu-id="c45f6-125">tooadd роли tooa PHP веб-проекта, запустите следующую команду из в корневом каталоге проекта hello hello:</span><span class="sxs-lookup"><span data-stu-id="c45f6-125">tooadd a PHP web role tooa project, run hello following command from within hello project's root directory:</span></span>

    PS C:\myProject> Add-AzurePHPWebRole roleName

<span data-ttu-id="c45f6-126">Для рабочей роли используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="c45f6-126">For a worker role, use this command:</span></span>

    PS C:\myProject> Add-AzurePHPWorkerRole roleName

> [!NOTE]
> <span data-ttu-id="c45f6-127">Hello `roleName` параметр является необязательным.</span><span class="sxs-lookup"><span data-stu-id="c45f6-127">hello `roleName` parameter is optional.</span></span> <span data-ttu-id="c45f6-128">Если он опущен, имя роли hello будут создаваться автоматически.</span><span class="sxs-lookup"><span data-stu-id="c45f6-128">If it is omitted, hello role name will be automatically generated.</span></span> <span data-ttu-id="c45f6-129">первый веб-роль Hello создан будет `WebRole1`, hello второй будет `WebRole2`, и т. д.</span><span class="sxs-lookup"><span data-stu-id="c45f6-129">hello first web role created will be `WebRole1`, hello second will be `WebRole2`, and so on.</span></span> <span data-ttu-id="c45f6-130">будет Hello первая рабочая роль создана `WorkerRole1`, hello второй будет `WorkerRole2`, и т. д.</span><span class="sxs-lookup"><span data-stu-id="c45f6-130">hello first worker role created will be `WorkerRole1`, hello second will be `WorkerRole2`, and so on.</span></span>
>
>

## <a name="specify-hello-built-in-php-version"></a><span data-ttu-id="c45f6-131">Укажите встроенные PHP версии hello</span><span class="sxs-lookup"><span data-stu-id="c45f6-131">Specify hello built-in PHP version</span></span>
<span data-ttu-id="c45f6-132">При добавлении PHP рабочих и веб-роли tooa проекта, файлы конфигурации hello проекта были изменены, чтобы при его развертывании будет установлен на каждом экземпляре рабочих и веб-приложения PHP.</span><span class="sxs-lookup"><span data-stu-id="c45f6-132">When you add a PHP web or worker role tooa project, hello project's configuration files are modified so that PHP will be installed on each web or worker instance of your application when it is deployed.</span></span> <span data-ttu-id="c45f6-133">версия hello toosee PHP, который будет установлен по умолчанию, запустите следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="c45f6-133">toosee hello version of PHP that will be installed by default, run hello following command:</span></span>

    PS C:\myProject> Get-AzureServiceProjectRoleRuntime

<span data-ttu-id="c45f6-134">Hello выходные данные команды hello выше будет выглядеть toowhat приведен ниже.</span><span class="sxs-lookup"><span data-stu-id="c45f6-134">hello output from hello command above will look similar toowhat is shown below.</span></span> <span data-ttu-id="c45f6-135">В этом примере hello `IsDefault` флаг установлен слишком`true` для PHP 5.3.17, что она будет установлена версия PHP по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="c45f6-135">In this example, hello `IsDefault` flag is set too`true` for PHP 5.3.17, indicating that it will be hello default PHP version installed.</span></span>

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

<span data-ttu-id="c45f6-136">Можно задать tooany версии среды выполнения PHP hello hello версий PHP, которые перечислены.</span><span class="sxs-lookup"><span data-stu-id="c45f6-136">You can set hello PHP runtime version tooany of hello PHP versions that are listed.</span></span> <span data-ttu-id="c45f6-137">Например, версия PHP hello tooset (для роли с именем hello `roleName`) too5.4.0 hello используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="c45f6-137">For example, tooset hello PHP version (for a role with hello name `roleName`) too5.4.0, use hello following command:</span></span>

    PS C:\myProject> Set-AzureServiceProjectRole roleName php 5.4.0

> [!NOTE]
> <span data-ttu-id="c45f6-138">Доступные версии PHP может измениться в будущих hello.</span><span class="sxs-lookup"><span data-stu-id="c45f6-138">Available PHP versions may change in hello future.</span></span>
>
>

## <a name="customize-hello-built-in-php-runtime"></a><span data-ttu-id="c45f6-139">Настройка встроенных выполнения PHP hello</span><span class="sxs-lookup"><span data-stu-id="c45f6-139">Customize hello built-in PHP runtime</span></span>
<span data-ttu-id="c45f6-140">У вас есть полный контроль над hello конфигурацию среды выполнения PHP hello, которая устанавливается при выполнении hello описанные выше шаги, включая изменение `php.ini` параметры и Включение расширений.</span><span class="sxs-lookup"><span data-stu-id="c45f6-140">You have complete control over hello configuration of hello PHP runtime that is installed when you follow hello steps above, including modification of `php.ini` settings and enabling of extensions.</span></span>

<span data-ttu-id="c45f6-141">toocustomize Здравствуйте встроенных среды выполнения PHP, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="c45f6-141">toocustomize hello built-in PHP runtime, follow these steps:</span></span>

1. <span data-ttu-id="c45f6-142">Добавить новую папку с именем `php`, toohello `bin` каталог веб-роли.</span><span class="sxs-lookup"><span data-stu-id="c45f6-142">Add a new folder, named `php`, toohello `bin` directory of your web role.</span></span> <span data-ttu-id="c45f6-143">Для рабочей роли добавьте его корневой каталог toohello роли.</span><span class="sxs-lookup"><span data-stu-id="c45f6-143">For a worker role, add it toohello role's root directory.</span></span>
2. <span data-ttu-id="c45f6-144">В hello `php` папки, создайте другую папку с именем `ext`.</span><span class="sxs-lookup"><span data-stu-id="c45f6-144">In hello `php` folder, create another folder called `ext`.</span></span> <span data-ttu-id="c45f6-145">Поместите все `.dll` расширения файлов (например, `php_mongo.dll`), которые должны tooenable в этой папке.</span><span class="sxs-lookup"><span data-stu-id="c45f6-145">Put any `.dll` extension files (e.g., `php_mongo.dll`) that you want tooenable in this folder.</span></span>
3. <span data-ttu-id="c45f6-146">Добавить `php.ini` файл toohello `php` папки.</span><span class="sxs-lookup"><span data-stu-id="c45f6-146">Add a `php.ini` file toohello `php` folder.</span></span> <span data-ttu-id="c45f6-147">Включите любые пользовательские расширения и задайте любые директивы PHP в этом файле.</span><span class="sxs-lookup"><span data-stu-id="c45f6-147">Enable any custom extensions and set any PHP directives in this file.</span></span> <span data-ttu-id="c45f6-148">Например, если требуется, чтобы tooturn `display_errors` на и включите hello `php_mongo.dll` расширением, содержимое hello вашей `php.ini` файла будет выглядеть следующим:</span><span class="sxs-lookup"><span data-stu-id="c45f6-148">For example, if you wanted tooturn `display_errors` on and enable hello `php_mongo.dll` extension, hello contents of your `php.ini` file would be as follows:</span></span>

        display_errors=On
        extension=php_mongo.dll

> [!NOTE]
> <span data-ttu-id="c45f6-149">Все параметры, которые не заданы явно в hello `php.ini` файл предоставляет будет автоматически устанавливать значения по умолчанию tootheir.</span><span class="sxs-lookup"><span data-stu-id="c45f6-149">Any settings that you don't explicitly set in hello `php.ini` file that you provide will automatically be set tootheir default values.</span></span> <span data-ttu-id="c45f6-150">Тем не менее, следует помнить, что вы можете добавить полный файл `php.ini` .</span><span class="sxs-lookup"><span data-stu-id="c45f6-150">However, keep in mind that you can add a complete `php.ini` file.</span></span>
>
>

## <a name="use-your-own-php-runtime"></a><span data-ttu-id="c45f6-151">Использование собственной среды выполнения PHP</span><span class="sxs-lookup"><span data-stu-id="c45f6-151">Use your own PHP runtime</span></span>
<span data-ttu-id="c45f6-152">В некоторых случаях вместо выбора встроенных среды выполнения PHP и настроить его так, как описано выше вы можете tooprovide собственные среды выполнения PHP.</span><span class="sxs-lookup"><span data-stu-id="c45f6-152">In some cases, instead of selecting a built-in PHP runtime and configuring it as described above, you may want tooprovide your own PHP runtime.</span></span> <span data-ttu-id="c45f6-153">Например, можно использовать hello одной среды выполнения PHP в веб- или рабочей роли, которая используется в среде разработки.</span><span class="sxs-lookup"><span data-stu-id="c45f6-153">For example, you can use hello same PHP runtime in a web or worker role that you use in your development environment.</span></span> <span data-ttu-id="c45f6-154">Это позволяет упростить tooensure, что приложения hello не изменяет поведение в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="c45f6-154">This makes it easier tooensure that hello application will not change behavior in your production environment.</span></span>

### <a name="configure-a-web-role-toouse-your-own-php-runtime"></a><span data-ttu-id="c45f6-155">Настройка toouse роли web собственные среды выполнения PHP</span><span class="sxs-lookup"><span data-stu-id="c45f6-155">Configure a web role toouse your own PHP runtime</span></span>
<span data-ttu-id="c45f6-156">tooconfigure toouse роли web среды выполнения PHP, который предоставляется, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="c45f6-156">tooconfigure a web role toouse a PHP runtime that you provide, follow these steps:</span></span>

1. <span data-ttu-id="c45f6-157">Создайте проект службы Azure и добавьте веб-роль PHP, как описано в этом разделе ранее.</span><span class="sxs-lookup"><span data-stu-id="c45f6-157">Create an Azure Service project and add a PHP web role as described previously in this topic.</span></span>
2. <span data-ttu-id="c45f6-158">Создание `php` папки в hello `bin` папку, которая находится в корневом каталоге веб-роли, а затем добавьте вашей toohello среды выполнения (все двоичные файлы, файлы конфигурации, вложенные папки, т. д.) PHP `php` папки.</span><span class="sxs-lookup"><span data-stu-id="c45f6-158">Create a `php` folder in hello `bin` folder that is in your web role's root directory, and then add your PHP runtime (all binaries, configuration files, subfolders, etc.) toohello `php` folder.</span></span>
3. <span data-ttu-id="c45f6-159">(НЕОБЯЗАТЕЛЬНО) Если вашей среды выполнения PHP использует hello [драйверы Майкрософт для PHP для SQL Server][sqlsrv drivers], потребуется tooconfigure вашей веб роль tooinstall [собственного клиента SQL Server 2012] [ sql native client] при его инициализации.</span><span class="sxs-lookup"><span data-stu-id="c45f6-159">(OPTIONAL) If your PHP runtime uses hello [Microsoft Drivers for PHP for SQL Server][sqlsrv drivers], you will need tooconfigure your web role tooinstall [SQL Server Native Client 2012][sql native client] when it is provisioned.</span></span> <span data-ttu-id="c45f6-160">toodo это, добавьте hello [установщик sqlncli.msi x64] toohello `bin` папки в корневом каталоге веб-роли.</span><span class="sxs-lookup"><span data-stu-id="c45f6-160">toodo this, add hello [sqlncli.msi x64 installer] toohello `bin` folder in your web role's root directory.</span></span> <span data-ttu-id="c45f6-161">сценарий запуска Hello, описанные в следующем шаге hello автоматически будет выполняться hello установщика при подготовке hello роли.</span><span class="sxs-lookup"><span data-stu-id="c45f6-161">hello startup script described in hello next step will silently run hello installer when hello role is provisioned.</span></span> <span data-ttu-id="c45f6-162">Если вашей среды выполнения PHP не использует hello драйверы Майкрософт для PHP для SQL Server, можно удалить следующую строку из hello сценарий, показанный на следующем шаге hello hello:</span><span class="sxs-lookup"><span data-stu-id="c45f6-162">If your PHP runtime does not use hello Microsoft Drivers for PHP for SQL Server, you can remove hello following line from hello script shown in hello next step:</span></span>

        msiexec /i sqlncli.msi /qn IACCEPTSQLNCLILICENSETERMS=YES
4. <span data-ttu-id="c45f6-163">Определить задачи запуска, которая настраивает [Internet Information Services (IIS)] [ iis.net] toouse вашей toohandle среды выполнения PHP запросы для `.php` страницы.</span><span class="sxs-lookup"><span data-stu-id="c45f6-163">Define a startup task that configures [Internet Information Services (IIS)][iis.net] toouse your PHP runtime toohandle requests for `.php` pages.</span></span> <span data-ttu-id="c45f6-164">toodo это, откройте hello `setup_web.cmd` файла (в hello `bin` файла корневого каталога веб-роли) в текстовом редакторе и заменить его содержимое hello следующий скрипт:</span><span class="sxs-lookup"><span data-stu-id="c45f6-164">toodo this, open hello `setup_web.cmd` file (in hello `bin` file of your web role's root directory) in a text editor and replace its contents with hello following script:</span></span>

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
5. <span data-ttu-id="c45f6-165">Добавление приложения файлы tooyour веб-роли в корневой каталог.</span><span class="sxs-lookup"><span data-stu-id="c45f6-165">Add your application files tooyour web role's root directory.</span></span> <span data-ttu-id="c45f6-166">Это будет hello веб-сервера в корневом каталоге.</span><span class="sxs-lookup"><span data-stu-id="c45f6-166">This will be hello web server's root directory.</span></span>
6. <span data-ttu-id="c45f6-167">Опубликовать приложение, как описано в hello [опубликовать приложение](#publish-your-application) разделе ниже.</span><span class="sxs-lookup"><span data-stu-id="c45f6-167">Publish your application as described in hello [Publish your application](#publish-your-application) section below.</span></span>

> [!NOTE]
> <span data-ttu-id="c45f6-168">Hello `download.ps1` сценария (в hello `bin` папки корневого каталога веб-роли hello) могут быть удалены после выполнения действий hello, описанные выше, с помощью собственного среды выполнения PHP.</span><span class="sxs-lookup"><span data-stu-id="c45f6-168">hello `download.ps1` script (in hello `bin` folder of hello web role's root directory) can be deleted after you follow hello steps described above for using your own PHP runtime.</span></span>
>
>

### <a name="configure-a-worker-role-toouse-your-own-php-runtime"></a><span data-ttu-id="c45f6-169">Настройка рабочей роли toouse собственные среды выполнения PHP</span><span class="sxs-lookup"><span data-stu-id="c45f6-169">Configure a worker role toouse your own PHP runtime</span></span>
<span data-ttu-id="c45f6-170">tooconfigure toouse роли рабочей среды выполнения PHP, который предоставляется, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="c45f6-170">tooconfigure a worker role toouse a PHP runtime that you provide, follow these steps:</span></span>

1. <span data-ttu-id="c45f6-171">Создайте проект службы Azure и добавьте рабочую роль PHP, как описано в этом разделе ранее.</span><span class="sxs-lookup"><span data-stu-id="c45f6-171">Create an Azure Service project and add a PHP worker role as described previously in this topic.</span></span>
2. <span data-ttu-id="c45f6-172">Создать `php` папки в корневом каталоге hello рабочей роли и добавьте ваш toohello среды выполнения (все двоичные файлы, файлы конфигурации, вложенные папки, т. д.) PHP `php` папки.</span><span class="sxs-lookup"><span data-stu-id="c45f6-172">Create a `php` folder in hello worker role's root directory, and then add your PHP runtime (all binaries, configuration files, subfolders, etc.) toohello `php` folder.</span></span>
3. <span data-ttu-id="c45f6-173">(НЕОБЯЗАТЕЛЬНО) Если вашей среды выполнения PHP использует [драйверы Майкрософт для PHP для SQL Server][sqlsrv drivers], вам потребуется tooconfigure вашей рабочей роли tooinstall [собственного клиента SQL Server 2012] [ sql native client] при его инициализации.</span><span class="sxs-lookup"><span data-stu-id="c45f6-173">(OPTIONAL) If your PHP runtime uses [Microsoft Drivers for PHP for SQL Server][sqlsrv drivers], you will need tooconfigure your worker role tooinstall [SQL Server Native Client 2012][sql native client] when it is provisioned.</span></span> <span data-ttu-id="c45f6-174">toodo это, добавьте hello [установщик sqlncli.msi x64] toohello рабочей роли корневого каталога.</span><span class="sxs-lookup"><span data-stu-id="c45f6-174">toodo this, add hello [sqlncli.msi x64 installer] toohello worker role's root directory.</span></span> <span data-ttu-id="c45f6-175">сценарий запуска Hello, описанные в следующем шаге hello автоматически будет выполняться hello установщика при подготовке hello роли.</span><span class="sxs-lookup"><span data-stu-id="c45f6-175">hello startup script described in hello next step will silently run hello installer when hello role is provisioned.</span></span> <span data-ttu-id="c45f6-176">Если вашей среды выполнения PHP не использует hello драйверы Майкрософт для PHP для SQL Server, можно удалить следующую строку из hello сценарий, показанный на следующем шаге hello hello:</span><span class="sxs-lookup"><span data-stu-id="c45f6-176">If your PHP runtime does not use hello Microsoft Drivers for PHP for SQL Server, you can remove hello following line from hello script shown in hello next step:</span></span>

        msiexec /i sqlncli.msi /qn IACCEPTSQLNCLILICENSETERMS=YES
4. <span data-ttu-id="c45f6-177">Определить задачи запуска, которая добавляет к `php.exe` переменной среды PATH исполняемый toohello рабочей роли при подготовке hello роли.</span><span class="sxs-lookup"><span data-stu-id="c45f6-177">Define a startup task that adds your `php.exe` executable toohello worker role's PATH environment variable when hello role is provisioned.</span></span> <span data-ttu-id="c45f6-178">toodo это, откройте hello `setup_worker.cmd` (в корневом каталоге hello рабочей роли) в текстовом редакторе и замените его содержимое hello следующий скрипт:</span><span class="sxs-lookup"><span data-stu-id="c45f6-178">toodo this, open hello `setup_worker.cmd` file (in hello worker role's root directory) in a text editor and replace its contents with hello following script:</span></span>

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
5. <span data-ttu-id="c45f6-179">Добавление приложения файлы tooyour рабочей роли в корневой каталог.</span><span class="sxs-lookup"><span data-stu-id="c45f6-179">Add your application files tooyour worker role's root directory.</span></span>
6. <span data-ttu-id="c45f6-180">Опубликовать приложение, как описано в hello [опубликовать приложение](#publish-your-application) разделе ниже.</span><span class="sxs-lookup"><span data-stu-id="c45f6-180">Publish your application as described in hello [Publish your application](#publish-your-application) section below.</span></span>

## <a name="run-your-application-in-hello-compute-and-storage-emulators"></a><span data-ttu-id="c45f6-181">Запустите приложение hello эмуляторов вычислений и хранилища</span><span class="sxs-lookup"><span data-stu-id="c45f6-181">Run your application in hello compute and storage emulators</span></span>
<span data-ttu-id="c45f6-182">Привет эмуляторы Azure предоставляют локальной среде, в котором можно протестировать приложение Azure перед его развертыванием в облаке toohello.</span><span class="sxs-lookup"><span data-stu-id="c45f6-182">hello Azure emulators provide a local environment in which you can test your Azure application before you deploy it toohello cloud.</span></span> <span data-ttu-id="c45f6-183">Существуют некоторые различия между Привет эмуляторы и hello среды Azure.</span><span class="sxs-lookup"><span data-stu-id="c45f6-183">There are some differences between hello emulators and hello Azure environment.</span></span> <span data-ttu-id="c45f6-184">toounderstand это предпочтительнее. в разделе [использовать эмулятор хранилища Azure hello для разработки и тестирования](storage/common/storage-use-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="c45f6-184">toounderstand this better, see [Use hello Azure storage emulator for development and testing](storage/common/storage-use-emulator.md).</span></span>

<span data-ttu-id="c45f6-185">Обратите внимание, что необходимо PHP локально установлен эмулятор вычислений toouse hello.</span><span class="sxs-lookup"><span data-stu-id="c45f6-185">Note that you must have PHP installed locally toouse hello compute emulator.</span></span> <span data-ttu-id="c45f6-186">Эмулятор вычислений Hello использовать ваш локальный toorun установки PHP ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="c45f6-186">hello compute emulator will use your local PHP installation toorun your application.</span></span>

<span data-ttu-id="c45f6-187">toorun проект в Привет эмуляторы, выполните следующую команду из корневого каталога проекта hello:</span><span class="sxs-lookup"><span data-stu-id="c45f6-187">toorun your project in hello emulators, execute hello following command from your project's root directory:</span></span>

    PS C:\MyProject> Start-AzureEmulator

<span data-ttu-id="c45f6-188">Вы увидите примерно toothis выходные данные:</span><span class="sxs-lookup"><span data-stu-id="c45f6-188">You will see output similar toothis:</span></span>

    Creating local package...
    Starting Emulator...
    Role is running at http://127.0.0.1:81
    Started

<span data-ttu-id="c45f6-189">Вы увидите приложение, работающее в эмуляторе hello, открыв браузер и перейдя локальный адрес toohello показано в выходных данных hello (`http://127.0.0.1:81` в выходных данных примера hello выше).</span><span class="sxs-lookup"><span data-stu-id="c45f6-189">You can see your application running in hello emulator by opening a web browser and browsing toohello local address shown in hello output (`http://127.0.0.1:81` in hello example output above).</span></span>

<span data-ttu-id="c45f6-190">toostop Привет эмуляторы, выполнить следующую команду:</span><span class="sxs-lookup"><span data-stu-id="c45f6-190">toostop hello emulators, execute this command:</span></span>

    PS C:\MyProject> Stop-AzureEmulator

## <a name="publish-your-application"></a><span data-ttu-id="c45f6-191">Публикация приложения</span><span class="sxs-lookup"><span data-stu-id="c45f6-191">Publish your application</span></span>
<span data-ttu-id="c45f6-192">toopublish приложение, необходимо импортировать toofirst вашей параметры публикации с помощью hello [команду Import-AzurePublishSettingsFile](https://msdn.microsoft.com/library/azure/dn790370.aspx) командлета.</span><span class="sxs-lookup"><span data-stu-id="c45f6-192">toopublish your application, you need toofirst import your publish settings by using hello [Import-AzurePublishSettingsFile](https://msdn.microsoft.com/library/azure/dn790370.aspx) cmdlet.</span></span> <span data-ttu-id="c45f6-193">Затем приложение можно опубликовать с помощью hello [AzureServiceProject публикации](https://msdn.microsoft.com/library/azure/dn495166.aspx) командлета.</span><span class="sxs-lookup"><span data-stu-id="c45f6-193">Then you can publish your application by using hello [Publish-AzureServiceProject](https://msdn.microsoft.com/library/azure/dn495166.aspx) cmdlet.</span></span> <span data-ttu-id="c45f6-194">Сведения о входе в разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c45f6-194">For information about signing in, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c45f6-195">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c45f6-195">Next steps</span></span>
<span data-ttu-id="c45f6-196">Дополнительные сведения см. в разделе hello [Центр разработчика PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="c45f6-196">For more information, see hello [PHP Developer Center](/develop/php/).</span></span>

[пакет Azure SDK для PHP]: /develop/php/common-tasks/download-php-sdk/
[install ps and emulators]: http://go.microsoft.com/fwlink/p/?linkid=320376&clcid=0x409
[службы определения службы(.csdef)]: http://msdn.microsoft.com/library/windowsazure/ee758711.aspx
[конфигурации службы (cscfg)]: http://msdn.microsoft.com/library/windowsazure/ee758710.aspx
[iis.net]: http://www.iis.net/
[sql native client]: http://msdn.microsoft.com/sqlserver/aa937733.aspx
[sqlsrv drivers]: http://php.net/sqlsrv
[установщик sqlncli.msi x64]: http://go.microsoft.com/fwlink/?LinkID=239648
