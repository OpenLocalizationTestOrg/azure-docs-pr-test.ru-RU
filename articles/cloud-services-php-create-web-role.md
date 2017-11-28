---
title: "Создание веб-ролей и рабочих ролей Azure для PHP | Документация Майкрософт"
description: "Руководство по настройке среды выполнения PHP и созданию веб-ролей и рабочих ролей PHP в облачной службе Azure."
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
ms.openlocfilehash: 214fdcfe20f3fa4ebcbe41308404f8b7e7d15310
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-create-php-web-and-worker-roles"></a><span data-ttu-id="21c0a-103">Как создать веб-роли и рабочие роли PHP</span><span class="sxs-lookup"><span data-stu-id="21c0a-103">How to create PHP web and worker roles</span></span>
## <a name="overview"></a><span data-ttu-id="21c0a-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="21c0a-104">Overview</span></span>
<span data-ttu-id="21c0a-105">В этом руководстве мы расскажем, как создать веб-роль и рабочую роль PHP в среде разработки Windows, выбрать определенную версию PHP из доступных «встроенных» версий, изменить конфигурацию PHP, включить расширения и развернуть решение в Azure.</span><span class="sxs-lookup"><span data-stu-id="21c0a-105">This guide will show you how to create PHP web or worker roles in a Windows development environment, choose a specific version of PHP from the "built-in" versions available, change the PHP configuration, enable extensions, and finally, deploy to Azure.</span></span> <span data-ttu-id="21c0a-106">Здесь также описывается, как создать веб-роль или рабочую роль для использования среды выполнения PHP (с настраиваемой конфигурацией и расширениями), которая предоставляется пользователем.</span><span class="sxs-lookup"><span data-stu-id="21c0a-106">It also describes how to configure a web or worker role to use a PHP runtime (with custom configuration and extensions) that you provide.</span></span>

## <a name="what-are-php-web-and-worker-roles"></a><span data-ttu-id="21c0a-107">Что такое веб-роли и рабочие роли PHP?</span><span class="sxs-lookup"><span data-stu-id="21c0a-107">What are PHP web and worker roles?</span></span>
<span data-ttu-id="21c0a-108">Azure предоставляет три вычислительные модели для запуска приложений: веб-приложения Azure, виртуальные машины Azure и облачные службы Azure.</span><span class="sxs-lookup"><span data-stu-id="21c0a-108">Azure provides three compute models for running applications: Azure App Service, Azure Virtual Machines, and Azure Cloud Services.</span></span> <span data-ttu-id="21c0a-109">Все три модели поддерживают PHP.</span><span class="sxs-lookup"><span data-stu-id="21c0a-109">All three models support PHP.</span></span> <span data-ttu-id="21c0a-110">Облачные службы — это модель обслуживания типа *платформа как услуга (PaaS)*, в рамках которой используются веб-роли и рабочие роли.</span><span class="sxs-lookup"><span data-stu-id="21c0a-110">Cloud Services, which includes web and worker roles, provides *platform as a service (PaaS)*.</span></span> <span data-ttu-id="21c0a-111">Веб-роль облачной службы предоставляет выделенный веб-сервер служб IIS, на котором размещаются интерфейсные веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="21c0a-111">Within a cloud service, a web role provides a dedicated Internet Information Services (IIS) web server to host front-end web applications.</span></span> <span data-ttu-id="21c0a-112">В рабочей роли могут выполняться асинхронные, долгосрочные или постоянные задачи, для которых не требуется взаимодействие с пользователем.</span><span class="sxs-lookup"><span data-stu-id="21c0a-112">A worker role can run asynchronous, long-running or perpetual tasks independent of user interaction or input.</span></span>

<span data-ttu-id="21c0a-113">Подробнее об этих моделях можно узнать в статье о [вариантах размещения вычислительных сред, предоставляемых Azure](cloud-services/cloud-services-choose-me.md).</span><span class="sxs-lookup"><span data-stu-id="21c0a-113">For more information about these options, see [Compute hosting options provided by Azure](cloud-services/cloud-services-choose-me.md).</span></span>

## <a name="download-the-azure-sdk-for-php"></a><span data-ttu-id="21c0a-114">Загрузка пакета Azure SDK для PHP</span><span class="sxs-lookup"><span data-stu-id="21c0a-114">Download the Azure SDK for PHP</span></span>
<span data-ttu-id="21c0a-115">[Пакет Azure SDK для PHP] состоит из нескольких компонентов.</span><span class="sxs-lookup"><span data-stu-id="21c0a-115">The [Azure SDK for PHP] consists of several components.</span></span> <span data-ttu-id="21c0a-116">В данной статье будут использоваться два из них: Azure PowerShell и эмуляторы Azure.</span><span class="sxs-lookup"><span data-stu-id="21c0a-116">This article will use two of them: Azure PowerShell and the Azure emulators.</span></span> <span data-ttu-id="21c0a-117">Эти два компонента можно установить при помощи установщика веб-платформы Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="21c0a-117">These two components can be installed via the Microsoft Web Platform Installer.</span></span> <span data-ttu-id="21c0a-118">Подробнее: [Установка и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="21c0a-118">For more information, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="create-a-cloud-services-project"></a><span data-ttu-id="21c0a-119">Создание проекта облачных служб</span><span class="sxs-lookup"><span data-stu-id="21c0a-119">Create a Cloud Services project</span></span>
<span data-ttu-id="21c0a-120">Первым шагом в создании веб-роли или рабочей роли PHP является создание проекта службы Azure.</span><span class="sxs-lookup"><span data-stu-id="21c0a-120">The first step in creating a PHP web or worker role is to create an Azure Service project.</span></span> <span data-ttu-id="21c0a-121">Он служит логическим контейнером для обеих ролей и содержит файлы [определения службы (CSDEF)] и [конфигурации службы (CSCFG)].</span><span class="sxs-lookup"><span data-stu-id="21c0a-121">an Azure Service project serves as a logical container for web and worker roles, and it contains the project's [service definition (.csdef)] and [service configuration (.cscfg)] files.</span></span>

<span data-ttu-id="21c0a-122">Чтобы создать новый проект службы Azure, запустите Azure PowerShell от имени администратора и выполните следующую команду.</span><span class="sxs-lookup"><span data-stu-id="21c0a-122">To create a new Azure Service project, run Azure PowerShell as an administrator, and execute the following command:</span></span>

    PS C:\>New-AzureServiceProject myProject

<span data-ttu-id="21c0a-123">Эта команда создаст новый каталог (`myProject`), в который можно добавить веб-роли и рабочие роли.</span><span class="sxs-lookup"><span data-stu-id="21c0a-123">This command will create a new directory (`myProject`) to which you can add web and worker roles.</span></span>

## <a name="add-php-web-or-worker-roles"></a><span data-ttu-id="21c0a-124">Добавление веб-ролей PHP и ролей работников</span><span class="sxs-lookup"><span data-stu-id="21c0a-124">Add PHP web or worker roles</span></span>
<span data-ttu-id="21c0a-125">Чтобы добавить в проект веб-роль PHP, выполните следующую команду из корневого каталога проекта.</span><span class="sxs-lookup"><span data-stu-id="21c0a-125">To add a PHP web role to a project, run the following command from within the project's root directory:</span></span>

    PS C:\myProject> Add-AzurePHPWebRole roleName

<span data-ttu-id="21c0a-126">Для рабочей роли используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="21c0a-126">For a worker role, use this command:</span></span>

    PS C:\myProject> Add-AzurePHPWorkerRole roleName

> [!NOTE]
> <span data-ttu-id="21c0a-127">Параметр `roleName` не обязателен.</span><span class="sxs-lookup"><span data-stu-id="21c0a-127">The `roleName` parameter is optional.</span></span> <span data-ttu-id="21c0a-128">Если он опущен, имя роли будет создано автоматически.</span><span class="sxs-lookup"><span data-stu-id="21c0a-128">If it is omitted, the role name will be automatically generated.</span></span> <span data-ttu-id="21c0a-129">Первая веб-роль создается с именем `WebRole1`, вторая — `WebRole2` и т. д.</span><span class="sxs-lookup"><span data-stu-id="21c0a-129">The first web role created will be `WebRole1`, the second will be `WebRole2`, and so on.</span></span> <span data-ttu-id="21c0a-130">Первая рабочая роль создается с именем `WorkerRole1`, вторая — `WorkerRole2` и т. д.</span><span class="sxs-lookup"><span data-stu-id="21c0a-130">The first worker role created will be `WorkerRole1`, the second will be `WorkerRole2`, and so on.</span></span>
>
>

## <a name="specify-the-built-in-php-version"></a><span data-ttu-id="21c0a-131">Указание встроенной версии PHP</span><span class="sxs-lookup"><span data-stu-id="21c0a-131">Specify the built-in PHP version</span></span>
<span data-ttu-id="21c0a-132">При добавлении в проект PHP веб-роли или рабочей роли, файлы конфигурации проекта изменяются таким образом, чтобы можно было установить PHP в каждом экземпляре веб-роли или рабочей роли вашего приложения при его развертывании.</span><span class="sxs-lookup"><span data-stu-id="21c0a-132">When you add a PHP web or worker role to a project, the project's configuration files are modified so that PHP will be installed on each web or worker instance of your application when it is deployed.</span></span> <span data-ttu-id="21c0a-133">Чтобы посмотреть версию PHP, которая будет установлена по умолчанию, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="21c0a-133">To see the version of PHP that will be installed by default, run the following command:</span></span>

    PS C:\myProject> Get-AzureServiceProjectRoleRuntime

<span data-ttu-id="21c0a-134">Выход приведенной выше команды будут выглядеть аналогично, приведенным ниже данным.</span><span class="sxs-lookup"><span data-stu-id="21c0a-134">The output from the command above will look similar to what is shown below.</span></span> <span data-ttu-id="21c0a-135">В этом примере флаг `IsDefault` установлен в значение `true` для PHP 5.3.17, что указывает, что это будет версия PHP, установленная по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="21c0a-135">In this example, the `IsDefault` flag is set to `true` for PHP 5.3.17, indicating that it will be the default PHP version installed.</span></span>

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

<span data-ttu-id="21c0a-136">Можно установить версию среды выполнения PHP в любой из указанных версий PHP.</span><span class="sxs-lookup"><span data-stu-id="21c0a-136">You can set the PHP runtime version to any of the PHP versions that are listed.</span></span> <span data-ttu-id="21c0a-137">Например, чтобы задать версию PHP 5.4.0 для роли с именем `roleName`, используйте следующую команду.</span><span class="sxs-lookup"><span data-stu-id="21c0a-137">For example, to set the PHP version (for a role with the name `roleName`) to 5.4.0, use the following command:</span></span>

    PS C:\myProject> Set-AzureServiceProjectRole roleName php 5.4.0

> [!NOTE]
> <span data-ttu-id="21c0a-138">Доступные версии PHP могут изменяться со временем.</span><span class="sxs-lookup"><span data-stu-id="21c0a-138">Available PHP versions may change in the future.</span></span>
>
>

## <a name="customize-the-built-in-php-runtime"></a><span data-ttu-id="21c0a-139">Настройка встроенной среды выполнения PHP</span><span class="sxs-lookup"><span data-stu-id="21c0a-139">Customize the built-in PHP runtime</span></span>
<span data-ttu-id="21c0a-140">У вас есть полный контроль над конфигурацией среды выполнения PHP, которая устанавливается при выполнении описанных выше действий, включая изменение параметров `php.ini` и включение расширений.</span><span class="sxs-lookup"><span data-stu-id="21c0a-140">You have complete control over the configuration of the PHP runtime that is installed when you follow the steps above, including modification of `php.ini` settings and enabling of extensions.</span></span>

<span data-ttu-id="21c0a-141">Чтобы настроить встроенную среду выполнения PHP, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="21c0a-141">To customize the built-in PHP runtime, follow these steps:</span></span>

1. <span data-ttu-id="21c0a-142">Добавьте новую папку с именем `php` в каталог `bin` вашей веб-роли.</span><span class="sxs-lookup"><span data-stu-id="21c0a-142">Add a new folder, named `php`, to the `bin` directory of your web role.</span></span> <span data-ttu-id="21c0a-143">Что касается рабочей роли, добавьте ее в корневой каталог роли.</span><span class="sxs-lookup"><span data-stu-id="21c0a-143">For a worker role, add it to the role's root directory.</span></span>
2. <span data-ttu-id="21c0a-144">В папке `php` создайте другую папку с именем `ext`.</span><span class="sxs-lookup"><span data-stu-id="21c0a-144">In the `php` folder, create another folder called `ext`.</span></span> <span data-ttu-id="21c0a-145">Поместите в эту папку все файлы с расширением `.dll` (например, `php_mongo.dll`), которые хотите подключить.</span><span class="sxs-lookup"><span data-stu-id="21c0a-145">Put any `.dll` extension files (e.g., `php_mongo.dll`) that you want to enable in this folder.</span></span>
3. <span data-ttu-id="21c0a-146">Добавьте файл `php.ini` в папку `php`.</span><span class="sxs-lookup"><span data-stu-id="21c0a-146">Add a `php.ini` file to the `php` folder.</span></span> <span data-ttu-id="21c0a-147">Включите любые пользовательские расширения и задайте любые директивы PHP в этом файле.</span><span class="sxs-lookup"><span data-stu-id="21c0a-147">Enable any custom extensions and set any PHP directives in this file.</span></span> <span data-ttu-id="21c0a-148">Например, если вы хотите включить `display_errors` и включить расширение `php_mongo.dll`, содержимое вашего файла `php.ini` будет такое:</span><span class="sxs-lookup"><span data-stu-id="21c0a-148">For example, if you wanted to turn `display_errors` on and enable the `php_mongo.dll` extension, the contents of your `php.ini` file would be as follows:</span></span>

        display_errors=On
        extension=php_mongo.dll

> [!NOTE]
> <span data-ttu-id="21c0a-149">Для тех параметров, которые вы не задали явным образом в предоставленном вами файле `php.ini`, будут автоматически использоваться значения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="21c0a-149">Any settings that you don't explicitly set in the `php.ini` file that you provide will automatically be set to their default values.</span></span> <span data-ttu-id="21c0a-150">Тем не менее, следует помнить, что вы можете добавить полный файл `php.ini` .</span><span class="sxs-lookup"><span data-stu-id="21c0a-150">However, keep in mind that you can add a complete `php.ini` file.</span></span>
>
>

## <a name="use-your-own-php-runtime"></a><span data-ttu-id="21c0a-151">Использование собственной среды выполнения PHP</span><span class="sxs-lookup"><span data-stu-id="21c0a-151">Use your own PHP runtime</span></span>
<span data-ttu-id="21c0a-152">В некоторых случаях вместо выбора встроенной среды выполнения PHP и настройки в соответствии с указанными выше инструкциями вам может понадобиться предоставить собственную среду выполнения PHP.</span><span class="sxs-lookup"><span data-stu-id="21c0a-152">In some cases, instead of selecting a built-in PHP runtime and configuring it as described above, you may want to provide your own PHP runtime.</span></span> <span data-ttu-id="21c0a-153">Например, вы можете использовать в рабочей роли или веб-роли ту же среду выполнения PHP, что и в среде разработки.</span><span class="sxs-lookup"><span data-stu-id="21c0a-153">For example, you can use the same PHP runtime in a web or worker role that you use in your development environment.</span></span> <span data-ttu-id="21c0a-154">Это поможет гарантировать, что приложение не изменит свое поведение в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="21c0a-154">This makes it easier to ensure that the application will not change behavior in your production environment.</span></span>

### <a name="configure-a-web-role-to-use-your-own-php-runtime"></a><span data-ttu-id="21c0a-155">Настройка собственной среды выполнения PHP для веб-роли</span><span class="sxs-lookup"><span data-stu-id="21c0a-155">Configure a web role to use your own PHP runtime</span></span>
<span data-ttu-id="21c0a-156">Чтобы использовать в веб-роли собственную среду выполнения PHP, выполните приведенные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="21c0a-156">To configure a web role to use a PHP runtime that you provide, follow these steps:</span></span>

1. <span data-ttu-id="21c0a-157">Создайте проект службы Azure и добавьте веб-роль PHP, как описано в этом разделе ранее.</span><span class="sxs-lookup"><span data-stu-id="21c0a-157">Create an Azure Service project and add a PHP web role as described previously in this topic.</span></span>
2. <span data-ttu-id="21c0a-158">Создайте папку `php` в папке `bin`, которая находится в корневом каталоге веб-роли, затем добавьте в папку `php` среду выполнения PHP (все двоичные файлы, файлы конфигурации, вложенные папки и т. д.).</span><span class="sxs-lookup"><span data-stu-id="21c0a-158">Create a `php` folder in the `bin` folder that is in your web role's root directory, and then add your PHP runtime (all binaries, configuration files, subfolders, etc.) to the `php` folder.</span></span>
3. <span data-ttu-id="21c0a-159">(Дополнительно.) Если среда выполнения PHP использует [драйверы Microsoft для PHP для SQL Server][sqlsrv drivers], то необходимо настроить веб-роль для установки [SQL Server Native Client 2012][sql native client] после ее подготовки.</span><span class="sxs-lookup"><span data-stu-id="21c0a-159">(OPTIONAL) If your PHP runtime uses the [Microsoft Drivers for PHP for SQL Server][sqlsrv drivers], you will need to configure your web role to install [SQL Server Native Client 2012][sql native client] when it is provisioned.</span></span> <span data-ttu-id="21c0a-160">Для этого добавьте установщик [sqlncli.msi x64] в папку `bin` в корневом каталоге веб-роли.</span><span class="sxs-lookup"><span data-stu-id="21c0a-160">To do this, add the [sqlncli.msi x64 installer] to the `bin` folder in your web role's root directory.</span></span> <span data-ttu-id="21c0a-161">Скрипт запуска, описанный на следующем шаге, запустит установщик без вмешательства пользователя при подготовке роли.</span><span class="sxs-lookup"><span data-stu-id="21c0a-161">The startup script described in the next step will silently run the installer when the role is provisioned.</span></span> <span data-ttu-id="21c0a-162">Если среда выполнения PHP не использует драйверы Microsoft для PHP для SQL Server, можно удалить следующую строку из скрипта, показанного на следующем шаге.</span><span class="sxs-lookup"><span data-stu-id="21c0a-162">If your PHP runtime does not use the Microsoft Drivers for PHP for SQL Server, you can remove the following line from the script shown in the next step:</span></span>

        msiexec /i sqlncli.msi /qn IACCEPTSQLNCLILICENSETERMS=YES
4. <span data-ttu-id="21c0a-163">Чтобы [службы IIS][iis.net] использовали вашу среду PHP для обработки запросов для страниц `.php`, определите задачу запуска, изменяющую настройки IIS.</span><span class="sxs-lookup"><span data-stu-id="21c0a-163">Define a startup task that configures [Internet Information Services (IIS)][iis.net] to use your PHP runtime to handle requests for `.php` pages.</span></span> <span data-ttu-id="21c0a-164">Для этого откройте файл`setup_web.cmd` (в файле `bin` корневого каталога веб-роли) в текстовом редакторе и замените его содержимое на следующий скрипт:</span><span class="sxs-lookup"><span data-stu-id="21c0a-164">To do this, open the `setup_web.cmd` file (in the `bin` file of your web role's root directory) in a text editor and replace its contents with the following script:</span></span>

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
5. <span data-ttu-id="21c0a-165">Добавьте файлы вашего приложения в корневой каталог веб-роли.</span><span class="sxs-lookup"><span data-stu-id="21c0a-165">Add your application files to your web role's root directory.</span></span> <span data-ttu-id="21c0a-166">Это будет корневой каталог веб-сервера.</span><span class="sxs-lookup"><span data-stu-id="21c0a-166">This will be the web server's root directory.</span></span>
6. <span data-ttu-id="21c0a-167">Опубликуйте приложение, как описано ниже в разделе [Публикация приложения](#publish-your-application).</span><span class="sxs-lookup"><span data-stu-id="21c0a-167">Publish your application as described in the [Publish your application](#publish-your-application) section below.</span></span>

> [!NOTE]
> <span data-ttu-id="21c0a-168">Сценарий `download.ps1` (в папке `bin` корневого каталога веб-роли) можно удалить после выполнения описанной выше настройки собственной среды выполнения PHP.</span><span class="sxs-lookup"><span data-stu-id="21c0a-168">The `download.ps1` script (in the `bin` folder of the web role's root directory) can be deleted after you follow the steps described above for using your own PHP runtime.</span></span>
>
>

### <a name="configure-a-worker-role-to-use-your-own-php-runtime"></a><span data-ttu-id="21c0a-169">Настройка собственной среды выполнения PHP для рабочей роли</span><span class="sxs-lookup"><span data-stu-id="21c0a-169">Configure a worker role to use your own PHP runtime</span></span>
<span data-ttu-id="21c0a-170">Чтобы использовать в рабочей роли собственную среду выполнения PHP, выполните приведенные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="21c0a-170">To configure a worker role to use a PHP runtime that you provide, follow these steps:</span></span>

1. <span data-ttu-id="21c0a-171">Создайте проект службы Azure и добавьте рабочую роль PHP, как описано в этом разделе ранее.</span><span class="sxs-lookup"><span data-stu-id="21c0a-171">Create an Azure Service project and add a PHP worker role as described previously in this topic.</span></span>
2. <span data-ttu-id="21c0a-172">Создайте папку `php` в корневом каталоге рабочей роли, а затем добавьте в папку `php` среду выполнения PHP (все двоичные файлы, файлы конфигурации, вложенные папки и т. д.).</span><span class="sxs-lookup"><span data-stu-id="21c0a-172">Create a `php` folder in the worker role's root directory, and then add your PHP runtime (all binaries, configuration files, subfolders, etc.) to the `php` folder.</span></span>
3. <span data-ttu-id="21c0a-173">(Дополнительно.) Если среда выполнения PHP использует [драйверы Microsoft для PHP для SQL Server][sqlsrv drivers], то необходимо настроить рабочую роль для установки [SQL Server Native Client 2012][sql native client] после ее подготовки.</span><span class="sxs-lookup"><span data-stu-id="21c0a-173">(OPTIONAL) If your PHP runtime uses [Microsoft Drivers for PHP for SQL Server][sqlsrv drivers], you will need to configure your worker role to install [SQL Server Native Client 2012][sql native client] when it is provisioned.</span></span> <span data-ttu-id="21c0a-174">Для этого добавьте установщик [sqlncli.msi x64] в корневой каталог рабочей роли.</span><span class="sxs-lookup"><span data-stu-id="21c0a-174">To do this, add the [sqlncli.msi x64 installer] to the worker role's root directory.</span></span> <span data-ttu-id="21c0a-175">Скрипт запуска, описанный на следующем шаге, запустит установщик без вмешательства пользователя при подготовке роли.</span><span class="sxs-lookup"><span data-stu-id="21c0a-175">The startup script described in the next step will silently run the installer when the role is provisioned.</span></span> <span data-ttu-id="21c0a-176">Если среда выполнения PHP не использует драйверы Microsoft для PHP для SQL Server, можно удалить следующую строку из скрипта, показанного на следующем шаге.</span><span class="sxs-lookup"><span data-stu-id="21c0a-176">If your PHP runtime does not use the Microsoft Drivers for PHP for SQL Server, you can remove the following line from the script shown in the next step:</span></span>

        msiexec /i sqlncli.msi /qn IACCEPTSQLNCLILICENSETERMS=YES
4. <span data-ttu-id="21c0a-177">Определите задачу запуска, которая при подготовке роли добавляет исполняемый файл `php.exe` в переменную среды PATH рабочей роли.</span><span class="sxs-lookup"><span data-stu-id="21c0a-177">Define a startup task that adds your `php.exe` executable to the worker role's PATH environment variable when the role is provisioned.</span></span> <span data-ttu-id="21c0a-178">Для этого откройте файл `setup_worker.cmd` (в корневом каталоге рабочей роли) в текстовом редакторе и замените его содержимое на следующий скрипт:</span><span class="sxs-lookup"><span data-stu-id="21c0a-178">To do this, open the `setup_worker.cmd` file (in the worker role's root directory) in a text editor and replace its contents with the following script:</span></span>

    ```cmd
    @echo on

    cd "%~dp0"

    echo Granting permissions for Network Service to the web root directory...
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
5. <span data-ttu-id="21c0a-179">Добавьте файлы вашего приложения в корневой каталог рабочей роли.</span><span class="sxs-lookup"><span data-stu-id="21c0a-179">Add your application files to your worker role's root directory.</span></span>
6. <span data-ttu-id="21c0a-180">Опубликуйте приложение, как описано ниже в разделе [Публикация приложения](#publish-your-application).</span><span class="sxs-lookup"><span data-stu-id="21c0a-180">Publish your application as described in the [Publish your application](#publish-your-application) section below.</span></span>

## <a name="run-your-application-in-the-compute-and-storage-emulators"></a><span data-ttu-id="21c0a-181">Запуск приложения в эмуляторах вычисления и хранения</span><span class="sxs-lookup"><span data-stu-id="21c0a-181">Run your application in the compute and storage emulators</span></span>
<span data-ttu-id="21c0a-182">Эмуляторы Azure представляют собой локальную среду, в которой можно тестировать приложения Azure перед их развертыванием в облаке.</span><span class="sxs-lookup"><span data-stu-id="21c0a-182">The Azure emulators provide a local environment in which you can test your Azure application before you deploy it to the cloud.</span></span> <span data-ttu-id="21c0a-183">Существует несколько различий между эмуляторами и средой Azure.</span><span class="sxs-lookup"><span data-stu-id="21c0a-183">There are some differences between the emulators and the Azure environment.</span></span> <span data-ttu-id="21c0a-184">Чтобы разобраться в них, ознакомьтесь со статьей [Использование эмулятора хранения Azure для разработки и тестирования](storage/common/storage-use-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="21c0a-184">To understand this better, see [Use the Azure storage emulator for development and testing](storage/common/storage-use-emulator.md).</span></span>

<span data-ttu-id="21c0a-185">Обратите внимание, что для использования эмулятора вычислений следует установить PHP локально.</span><span class="sxs-lookup"><span data-stu-id="21c0a-185">Note that you must have PHP installed locally to use the compute emulator.</span></span> <span data-ttu-id="21c0a-186">Эмулятор вычислений будет использовать локальную установку PHP для запуска приложения.</span><span class="sxs-lookup"><span data-stu-id="21c0a-186">The compute emulator will use your local PHP installation to run your application.</span></span>

<span data-ttu-id="21c0a-187">Чтобы выполнить свой проект в эмуляторах, выполните следующую команду из корневого каталога своего проекта.</span><span class="sxs-lookup"><span data-stu-id="21c0a-187">To run your project in the emulators, execute the following command from your project's root directory:</span></span>

    PS C:\MyProject> Start-AzureEmulator

<span data-ttu-id="21c0a-188">Вы увидите примерно такие выходные данные:</span><span class="sxs-lookup"><span data-stu-id="21c0a-188">You will see output similar to this:</span></span>

    Creating local package...
    Starting Emulator...
    Role is running at http://127.0.0.1:81
    Started

<span data-ttu-id="21c0a-189">Запущенное в эмуляторе приложение можно просмотреть в браузере, перейдя по адресу, который указан в выходных данных (в приведенном выше примере это`http://127.0.0.1:81` ).</span><span class="sxs-lookup"><span data-stu-id="21c0a-189">You can see your application running in the emulator by opening a web browser and browsing to the local address shown in the output (`http://127.0.0.1:81` in the example output above).</span></span>

<span data-ttu-id="21c0a-190">Чтобы остановить эмуляторы, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="21c0a-190">To stop the emulators, execute this command:</span></span>

    PS C:\MyProject> Stop-AzureEmulator

## <a name="publish-your-application"></a><span data-ttu-id="21c0a-191">Публикация приложения</span><span class="sxs-lookup"><span data-stu-id="21c0a-191">Publish your application</span></span>
<span data-ttu-id="21c0a-192">Чтобы опубликовать приложение, сначала импортируйте параметры публикации с помощью командлета [Import-AzurePublishSettingsFile](https://msdn.microsoft.com/library/azure/dn790370.aspx) .</span><span class="sxs-lookup"><span data-stu-id="21c0a-192">To publish your application, you need to first import your publish settings by using the [Import-AzurePublishSettingsFile](https://msdn.microsoft.com/library/azure/dn790370.aspx) cmdlet.</span></span> <span data-ttu-id="21c0a-193">После этого опубликуйте приложение, используя командлет [Publish-AzureServiceProject](https://msdn.microsoft.com/library/azure/dn495166.aspx) .</span><span class="sxs-lookup"><span data-stu-id="21c0a-193">Then you can publish your application by using the [Publish-AzureServiceProject](https://msdn.microsoft.com/library/azure/dn495166.aspx) cmdlet.</span></span> <span data-ttu-id="21c0a-194">Подробнее о входе: [Установка и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="21c0a-194">For information about signing in, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="next-steps"></a><span data-ttu-id="21c0a-195">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="21c0a-195">Next steps</span></span>
<span data-ttu-id="21c0a-196">Дополнительную информацию можно найти в [Центре разработчика PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="21c0a-196">For more information, see the [PHP Developer Center](/develop/php/).</span></span>

[Пакет Azure SDK для PHP]: /develop/php/common-tasks/download-php-sdk/
[install ps and emulators]: http://go.microsoft.com/fwlink/p/?linkid=320376&clcid=0x409
[определения службы (CSDEF)]: http://msdn.microsoft.com/library/windowsazure/ee758711.aspx
[конфигурации службы (CSCFG)]: http://msdn.microsoft.com/library/windowsazure/ee758710.aspx
[iis.net]: http://www.iis.net/
[sql native client]: http://msdn.microsoft.com/sqlserver/aa937733.aspx
[sqlsrv drivers]: http://php.net/sqlsrv
[sqlncli.msi x64]: http://go.microsoft.com/fwlink/?LinkID=239648
