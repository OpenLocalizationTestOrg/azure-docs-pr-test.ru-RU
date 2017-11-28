---
title: "aaaConfigure PHP в веб-приложениях службы приложений Azure | Документы Microsoft"
description: "Узнайте, как tooconfigure hello установки PHP по умолчанию или добавить пользовательскую установку PHP для веб-приложений в службе приложений Azure."
services: app-service
documentationcenter: php
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 95c4072b-8570-496b-9c48-ee21a223fb60
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 2e461e4a269a4ce5614f5f05560f38bc53066251
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-php-in-azure-app-service-web-apps"></a><span data-ttu-id="d1110-103">Настройка PHP в веб-приложениях службы приложений Azure</span><span class="sxs-lookup"><span data-stu-id="d1110-103">Configure PHP in Azure App Service Web Apps</span></span>
## <a name="introduction"></a><span data-ttu-id="d1110-104">Введение</span><span class="sxs-lookup"><span data-stu-id="d1110-104">Introduction</span></span>
<span data-ttu-id="d1110-105">В этом руководстве будет показано, как tooconfigure hello встроенных среды выполнения PHP для веб-приложений в [службе приложений Azure](http://go.microsoft.com/fwlink/?LinkId=529714)Укажите настраиваемую среду выполнения PHP и включить расширения.</span><span class="sxs-lookup"><span data-stu-id="d1110-105">This guide will show you how tooconfigure hello built-in PHP runtime for Web Apps in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714), provide a custom PHP runtime, and enable extensions.</span></span> <span data-ttu-id="d1110-106">Регистрация toouse службы приложений для hello [бесплатной пробной версии].</span><span class="sxs-lookup"><span data-stu-id="d1110-106">toouse App Service, sign up for hello [free trial].</span></span> <span data-ttu-id="d1110-107">tooget hello наиболее из этого руководства, необходимо сначала создать веб-приложения PHP в службе приложений.</span><span class="sxs-lookup"><span data-stu-id="d1110-107">tooget hello most from this guide, you should first create a PHP web app in App Service.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="how-to-change-hello-built-in-php-version"></a><span data-ttu-id="d1110-108">Как: изменение hello встроенных PHP версии</span><span class="sxs-lookup"><span data-stu-id="d1110-108">How to: Change hello built-in PHP version</span></span>
<span data-ttu-id="d1110-109">По умолчанию при создании веб-приложения службы приложений устанавливается среда PHP 5.5, которая будет сразу готова для использования.</span><span class="sxs-lookup"><span data-stu-id="d1110-109">By default, PHP 5.5 is installed and immediately available for use when you create an App Service web app.</span></span> <span data-ttu-id="d1110-110">Здравствуйте, лучшим способом toosee hello доступные версии конфигурации по умолчанию, и hello включенных расширений является скрипт, который вызывает hello toodeploy [phpinfo()] функции.</span><span class="sxs-lookup"><span data-stu-id="d1110-110">hello best way toosee hello available release revision, its default configuration, and hello enabled extensions is toodeploy a script that calls hello [phpinfo()] function.</span></span>

<span data-ttu-id="d1110-111">Версии PHP 5.6 и PHP 7.0 также доступны, но не включены по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="d1110-111">PHP 5.6 and PHP 7.0 versions are also available, but not enabled by default.</span></span> <span data-ttu-id="d1110-112">hello tooupdate версии PHP, выполните один из следующих методов.</span><span class="sxs-lookup"><span data-stu-id="d1110-112">tooupdate hello PHP version, follow one of these methods:</span></span>

### <a name="azure-portal"></a><span data-ttu-id="d1110-113">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="d1110-113">Azure Portal</span></span>
1. <span data-ttu-id="d1110-114">Обзор tooyour веб-приложения в hello [портала Azure](https://portal.azure.com) и щелкнет hello **параметры** кнопки.</span><span class="sxs-lookup"><span data-stu-id="d1110-114">Browse tooyour web app in hello [Azure Portal](https://portal.azure.com) and click on hello **Settings** button.</span></span>
   
    ![Параметры веб-приложения][settings-button]
2. <span data-ttu-id="d1110-116">Из hello **параметры** колонке выберите **параметры приложения** и выберите новую версию PHP hello.</span><span class="sxs-lookup"><span data-stu-id="d1110-116">From hello **Settings** blade select **Application Settings** and choose hello new PHP version.</span></span>
   
    ![Параметры приложения][application-settings]
3. <span data-ttu-id="d1110-118">Щелкните hello **Сохранить** кнопку вверху hello hello **веб-параметров приложения** колонку.</span><span class="sxs-lookup"><span data-stu-id="d1110-118">Click hello **Save** button at hello top of hello **Web app settings** blade.</span></span>
   
    ![Сохранение параметров конфигурации][save-button]

### <a name="azure-powershell-windows"></a><span data-ttu-id="d1110-120">Azure PowerShell (только для Windows)</span><span class="sxs-lookup"><span data-stu-id="d1110-120">Azure PowerShell (Windows)</span></span>
1. <span data-ttu-id="d1110-121">Откройте Azure PowerShell и учетной записи входа tooyour:</span><span class="sxs-lookup"><span data-stu-id="d1110-121">Open Azure PowerShell, and login tooyour account:</span></span>
   
        PS C:\> Login-AzureRmAccount
2. <span data-ttu-id="d1110-122">Задание версии PHP hello для веб-приложения hello.</span><span class="sxs-lookup"><span data-stu-id="d1110-122">Set hello PHP version for hello web app.</span></span>
   
        PS C:\> Set-AzureWebsite -PhpVersion {5.5 | 5.6 | 7.0} -Name {app-name}
3. <span data-ttu-id="d1110-123">Установка версии PHP Hello.</span><span class="sxs-lookup"><span data-stu-id="d1110-123">hello PHP version is now set.</span></span> <span data-ttu-id="d1110-124">Можно подтвердить эти параметры.</span><span class="sxs-lookup"><span data-stu-id="d1110-124">You can confirm these settings:</span></span>
   
        PS C:\> Get-AzureWebsite -Name {app-name} | findstr PhpVersion

### <a name="azure-command-line-interface-linux-mac-windows"></a><span data-ttu-id="d1110-125">Интерфейс командной строки Azure для Mac, Linux и Windows</span><span class="sxs-lookup"><span data-stu-id="d1110-125">Azure Command-Line Interface (Linux, Mac, Windows)</span></span>
<span data-ttu-id="d1110-126">toouse hello Azure интерфейс командной строки, необходимо иметь **Node.js** установлены на компьютере.</span><span class="sxs-lookup"><span data-stu-id="d1110-126">toouse hello Azure Command-Line Interface, you must have **Node.js** installed on your computer.</span></span>

1. <span data-ttu-id="d1110-127">Откройте терминалов и учетная запись tooyour входа.</span><span class="sxs-lookup"><span data-stu-id="d1110-127">Open Terminal, and login tooyour account.</span></span>
   
        azure login
2. <span data-ttu-id="d1110-128">Задание версии PHP hello для веб-приложения hello.</span><span class="sxs-lookup"><span data-stu-id="d1110-128">Set hello PHP version for hello web app.</span></span>
   
        azure site set --php-version {5.5 | 5.6 | 7.0} {app-name}

3. <span data-ttu-id="d1110-129">Установка версии PHP Hello.</span><span class="sxs-lookup"><span data-stu-id="d1110-129">hello PHP version is now set.</span></span> <span data-ttu-id="d1110-130">Можно подтвердить эти параметры.</span><span class="sxs-lookup"><span data-stu-id="d1110-130">You can confirm these settings:</span></span>
   
        azure site show {app-name}

> [!NOTE] 
> <span data-ttu-id="d1110-131">Hello [Azure CLI 2.0](https://github.com/Azure/azure-cli) команды, эквивалентные toohello выше:</span><span class="sxs-lookup"><span data-stu-id="d1110-131">hello [Azure CLI 2.0](https://github.com/Azure/azure-cli) commands that are equivalent toohello above are:</span></span>
>
>

    az login
    az appservice web config update --php-version {5.5 | 5.6 | 7.0} -g {resource-group-name} -n {app-name}
    az appservice web config show -g {resource-group-name} -n {app-name}

## <a name="how-to-change-hello-built-in-php-configurations"></a><span data-ttu-id="d1110-132">Как: изменение конфигурации PHP для встроенных hello</span><span class="sxs-lookup"><span data-stu-id="d1110-132">How to: Change hello built-in PHP configurations</span></span>
<span data-ttu-id="d1110-133">Для любой встроенной среде выполнения PHP можно изменить любые параметры конфигурации hello, hello описанных ниже действий.</span><span class="sxs-lookup"><span data-stu-id="d1110-133">For any built-in PHP runtime, you can change any of hello configuration options by following hello steps below.</span></span> <span data-ttu-id="d1110-134">(Дополнительные сведения о директивах php.ini см. в разделе [Список директив php.ini].)</span><span class="sxs-lookup"><span data-stu-id="d1110-134">(For information about php.ini directives, see [List of php.ini directives].)</span></span>

### <a name="changing-phpiniuser-phpiniperdir-phpiniall-configuration-settings"></a><span data-ttu-id="d1110-135">Изменение параметров конфигурации PHP\_INI\_USER, PHP\_INI\_PERDIR, PHP\_INI\_ALL</span><span class="sxs-lookup"><span data-stu-id="d1110-135">Changing PHP\_INI\_USER, PHP\_INI\_PERDIR, PHP\_INI\_ALL configuration settings</span></span>
1. <span data-ttu-id="d1110-136">Добавить [. user.ini] корневой каталог файлов tooyour.</span><span class="sxs-lookup"><span data-stu-id="d1110-136">Add a [.user.ini] file tooyour root directory.</span></span>
2. <span data-ttu-id="d1110-137">Добавление конфигурации настроек toohello `.user.ini` текстовый файл с помощью hello того же синтаксиса, вы будете использовать в `php.ini` файла.</span><span class="sxs-lookup"><span data-stu-id="d1110-137">Add configuration settings toohello `.user.ini` file using hello same syntax you would use in a `php.ini` file.</span></span> <span data-ttu-id="d1110-138">Например, если требуется, чтобы tooturn hello `display_errors` параметр нужное значение и задайте `upload_max_filesize` параметр too10M, вашей `.user.ini` файл будет содержать следующий текст:</span><span class="sxs-lookup"><span data-stu-id="d1110-138">For example, if you wanted tooturn hello `display_errors` setting on and set `upload_max_filesize` setting too10M, your `.user.ini` file would contain this text:</span></span>
   
        ; Example Settings
        display_errors=On
        upload_max_filesize=10M
   
        ; OPTIONAL: Turn this on toowrite errors tood:\home\LogFiles\php_errors.log
        ; log_errors=On
3. <span data-ttu-id="d1110-139">Разверните веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="d1110-139">Deploy your web app.</span></span>
4. <span data-ttu-id="d1110-140">Перезапустите веб-приложение hello.</span><span class="sxs-lookup"><span data-stu-id="d1110-140">Restart hello web app.</span></span> <span data-ttu-id="d1110-141">(Перезагрузка необходима, так как hello частота, с которой PHP считывает `.user.ini` файлы регулируется hello `user_ini.cache_ttl` параметр, который является параметром уровня системы, составляет 300 секунд (5 минут) по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="d1110-141">(Restarting is necessary because hello frequency with which PHP reads `.user.ini` files is governed by hello `user_ini.cache_ttl` setting, which is a system level setting and is 300 seconds (5 minutes) by default.</span></span> <span data-ttu-id="d1110-142">Перезапускать веб-приложения hello принудительно PHP tooread hello новые параметры для hello `.user.ini` файл.)</span><span class="sxs-lookup"><span data-stu-id="d1110-142">Restarting hello web app forces PHP tooread hello new settings in hello `.user.ini` file.)</span></span>

<span data-ttu-id="d1110-143">Как альтернативный toousing `.user.ini` файл, можно использовать hello [ini_set()] функции в параметры конфигурации tooset скрипты, которые не являются директивами системного уровня.</span><span class="sxs-lookup"><span data-stu-id="d1110-143">As an alternative toousing a `.user.ini` file, you can use hello [ini_set()] function in scripts tooset configuration options that are not system-level directives.</span></span>

### <a name="changing-phpinisystem-configuration-settings"></a><span data-ttu-id="d1110-144">Изменение параметров конфигурации PHP\_INI\_SYSTEM</span><span class="sxs-lookup"><span data-stu-id="d1110-144">Changing PHP\_INI\_SYSTEM configuration settings</span></span>
1. <span data-ttu-id="d1110-145">Добавить параметр приложения tooyour веб-приложения, с ключом hello `PHP_INI_SCAN_DIR` и значение`d:\home\site\ini`</span><span class="sxs-lookup"><span data-stu-id="d1110-145">Add an App Setting tooyour Web App with hello key `PHP_INI_SCAN_DIR` and value `d:\home\site\ini`</span></span>
2. <span data-ttu-id="d1110-146">Создание `settings.ini` текстовый файл с помощью консоли Kudu (http://&lt;имя сайта&gt;. scm.azurewebsite.net) в hello `d:\home\site\ini` каталога.</span><span class="sxs-lookup"><span data-stu-id="d1110-146">Create an `settings.ini` file using Kudu Console (http://&lt;site-name&gt;.scm.azurewebsite.net) in hello `d:\home\site\ini` directory.</span></span>
3. <span data-ttu-id="d1110-147">Добавление конфигурации настроек toohello `settings.ini` текстовый файл с помощью hello того же синтаксиса, используется в файле php.ini.</span><span class="sxs-lookup"><span data-stu-id="d1110-147">Add configuration settings toohello `settings.ini` file using hello same syntax you would use in a php.ini file.</span></span> <span data-ttu-id="d1110-148">Например, если требуется, чтобы toopoint hello `curl.cainfo` параметр tooa `*.crt` и задайте wincache.maxfilesize параметр too512K, ваш `settings.ini` файл будет содержать этот текст:</span><span class="sxs-lookup"><span data-stu-id="d1110-148">For example, if you wanted toopoint hello `curl.cainfo` setting tooa `*.crt` file and set 'wincache.maxfilesize' setting too512K, your `settings.ini` file would contain this text:</span></span>
   
        ; Example Settings
        curl.cainfo="%ProgramFiles(x86)%\Git\bin\curl-ca-bundle.crt"
        wincache.maxfilesize=512
4. <span data-ttu-id="d1110-149">Перезапустите изменения hello tooload веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="d1110-149">Restart your Web App tooload hello changes.</span></span>

## <a name="how-to-enable-extensions-in-hello-default-php-runtime"></a><span data-ttu-id="d1110-150">Как: включить расширения в среде выполнения PHP по умолчанию hello</span><span class="sxs-lookup"><span data-stu-id="d1110-150">How to: Enable extensions in hello default PHP runtime</span></span>
<span data-ttu-id="d1110-151">Как отмечалось в hello предыдущего раздела, hello лучшим способом toosee hello версия по умолчанию PHP, его конфигурация по умолчанию и включены hello расширения — toodeploy скрипт, который вызывает [phpinfo()].</span><span class="sxs-lookup"><span data-stu-id="d1110-151">As noted in hello previous section, hello best way toosee hello default PHP version, its default configuration, and hello enabled extensions is toodeploy a script that calls [phpinfo()].</span></span> <span data-ttu-id="d1110-152">tooenable Дополнительные расширения, выполните следующие действия hello.</span><span class="sxs-lookup"><span data-stu-id="d1110-152">tooenable additional extensions, follow hello steps below:</span></span>

### <a name="configure-via-ini-settings"></a><span data-ttu-id="d1110-153">Настройка с помощью параметров ini</span><span class="sxs-lookup"><span data-stu-id="d1110-153">Configure via ini settings</span></span>
1. <span data-ttu-id="d1110-154">Добавить `ext` toohello каталога `d:\home\site` каталога.</span><span class="sxs-lookup"><span data-stu-id="d1110-154">Add a `ext` directory toohello `d:\home\site` directory.</span></span>
2. <span data-ttu-id="d1110-155">Поместите `.dll` расширения файлов в hello `ext` каталога (например, `php_xdebug.dll`).</span><span class="sxs-lookup"><span data-stu-id="d1110-155">Put `.dll` extension files in hello `ext` directory (for example, `php_xdebug.dll`).</span></span> <span data-ttu-id="d1110-156">Убедитесь в том, что расширения hello совместимы с версией по умолчанию PHP и являются VC9 и совместимость не потокобезопасный (Обновить).</span><span class="sxs-lookup"><span data-stu-id="d1110-156">Make sure that hello extensions are compatible with default version of PHP and are VC9 and non-thread-safe (nts) compatible.</span></span>
3. <span data-ttu-id="d1110-157">Добавить параметр приложения tooyour веб-приложения, с ключом hello `PHP_INI_SCAN_DIR` и значение`d:\home\site\ini`</span><span class="sxs-lookup"><span data-stu-id="d1110-157">Add an App Setting tooyour Web App with hello key `PHP_INI_SCAN_DIR` and value `d:\home\site\ini`</span></span>
4. <span data-ttu-id="d1110-158">Создайте файл `ini` в `d:\home\site\ini` с именем `extensions.ini`.</span><span class="sxs-lookup"><span data-stu-id="d1110-158">Create an `ini` file in `d:\home\site\ini` called `extensions.ini`.</span></span>
5. <span data-ttu-id="d1110-159">Добавление конфигурации настроек toohello `extensions.ini` текстовый файл с помощью hello того же синтаксиса, используется в файле php.ini.</span><span class="sxs-lookup"><span data-stu-id="d1110-159">Add configuration settings toohello `extensions.ini` file using hello same syntax you would use in a php.ini file.</span></span> <span data-ttu-id="d1110-160">Например, если требуется, чтобы расширений MongoDB и XDebug hello tooenable ваш `extensions.ini` файл будет содержать следующий текст:</span><span class="sxs-lookup"><span data-stu-id="d1110-160">For example, if you wanted tooenable hello MongoDB and XDebug extensions, your `extensions.ini` file would contain this text:</span></span>
   
        ; Enable Extensions
        extension=d:\home\site\ext\php_mongo.dll
        zend_extension=d:\home\site\ext\php_xdebug.dll
6. <span data-ttu-id="d1110-161">Перезапустите изменения hello tooload веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="d1110-161">Restart your Web App tooload hello changes.</span></span>

### <a name="configure-via-app-setting"></a><span data-ttu-id="d1110-162">Настройка с помощью параметров приложения</span><span class="sxs-lookup"><span data-stu-id="d1110-162">Configure via App Setting</span></span>
1. <span data-ttu-id="d1110-163">Добавить `bin` каталог toohello корневой каталог.</span><span class="sxs-lookup"><span data-stu-id="d1110-163">Add a `bin` directory toohello root directory.</span></span>
2. <span data-ttu-id="d1110-164">Поместите `.dll` расширения файлов в hello `bin` каталога (например, `php_xdebug.dll`).</span><span class="sxs-lookup"><span data-stu-id="d1110-164">Put `.dll` extension files in hello `bin` directory (for example, `php_xdebug.dll`).</span></span> <span data-ttu-id="d1110-165">Убедитесь в том, что расширения hello совместимы с версией по умолчанию PHP и являются VC9 и совместимость не потокобезопасный (Обновить).</span><span class="sxs-lookup"><span data-stu-id="d1110-165">Make sure that hello extensions are compatible with default version of PHP and are VC9 and non-thread-safe (nts) compatible.</span></span>
3. <span data-ttu-id="d1110-166">Разверните веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="d1110-166">Deploy your web app.</span></span>
4. <span data-ttu-id="d1110-167">Обзор tooyour веб-приложения в hello портала Azure и щелкнуть hello **параметры** кнопки.</span><span class="sxs-lookup"><span data-stu-id="d1110-167">Browse tooyour web app in hello Azure Portal and click on hello **Settings** button.</span></span>
   
    ![Параметры веб-приложения][settings-button]
5. <span data-ttu-id="d1110-169">Из hello **параметры** колонке выберите **параметры приложения** и прокрутите toohello **параметры приложения** раздела.</span><span class="sxs-lookup"><span data-stu-id="d1110-169">From hello **Settings** blade select **Application Settings** and scroll toohello **App settings** section.</span></span>
6. <span data-ttu-id="d1110-170">В hello **параметры приложения** создайте **PHP_EXTENSIONS** ключа.</span><span class="sxs-lookup"><span data-stu-id="d1110-170">In hello **App settings** section, create a **PHP_EXTENSIONS** key.</span></span> <span data-ttu-id="d1110-171">Hello значение для этого ключа будет иметь корневой путь относительный toowebsite: **файл bin\your-ext**.</span><span class="sxs-lookup"><span data-stu-id="d1110-171">hello value for this key would be a path relative toowebsite root: **bin\your-ext-file**.</span></span>
   
    ![Включение расширения в параметрах приложения][php-extensions]
7. <span data-ttu-id="d1110-173">Щелкните hello **Сохранить** кнопку вверху hello hello **веб-параметров приложения** колонку.</span><span class="sxs-lookup"><span data-stu-id="d1110-173">Click hello **Save** button at hello top of hello **Web app settings** blade.</span></span>
   
    ![Сохранение параметров конфигурации][save-button]

<span data-ttu-id="d1110-175">Расширения Zend также поддерживаются с помощью ключа **PHP_ZENDEXTENSIONS**.</span><span class="sxs-lookup"><span data-stu-id="d1110-175">Zend extensions are also supported by using a **PHP_ZENDEXTENSIONS** key.</span></span> <span data-ttu-id="d1110-176">tooenable несколько расширений включает список разделенных запятыми `.dll` файлы для hello значение параметра приложения.</span><span class="sxs-lookup"><span data-stu-id="d1110-176">tooenable multiple extensions, include a comma-separated list of `.dll` files for hello app setting value.</span></span>

## <a name="how-to-use-a-custom-php-runtime"></a><span data-ttu-id="d1110-177">Практическое руководство. Настраиваемая среда выполнения PHP</span><span class="sxs-lookup"><span data-stu-id="d1110-177">How to: Use a custom PHP runtime</span></span>
<span data-ttu-id="d1110-178">Вместо среды выполнения PHP по умолчанию hello приложения службы веб-приложений можно использовать среду выполнения PHP предоставляют tooexecute скрипты PHP.</span><span class="sxs-lookup"><span data-stu-id="d1110-178">Instead of hello default PHP runtime, App Service Web Apps can use a PHP runtime that you provide tooexecute PHP scripts.</span></span> <span data-ttu-id="d1110-179">можно настроить Hello среды выполнения, который предоставляется с `php.ini` файл, который также предоставляют.</span><span class="sxs-lookup"><span data-stu-id="d1110-179">hello runtime that you provide can be configured by a `php.ini` file that you also provide.</span></span> <span data-ttu-id="d1110-180">toouse пользовательской среды выполнения PHP для веб-приложений, выполните шаги hello.</span><span class="sxs-lookup"><span data-stu-id="d1110-180">toouse a custom PHP runtime with Web Apps, follow hello steps below.</span></span>

1. <span data-ttu-id="d1110-181">Получите версию PHP для Windows, совместимую с VC9 или VC11 и непотокобезопасной технологией (nts).</span><span class="sxs-lookup"><span data-stu-id="d1110-181">Obtain a non-thread-safe, VC9 or VC11 compatible version of PHP for Windows.</span></span> <span data-ttu-id="d1110-182">Последние версии PHP для Windows можно найти здесь: [http://windows.php.net/download/].</span><span class="sxs-lookup"><span data-stu-id="d1110-182">Recent releases of PHP for Windows can be found here: [http://windows.php.net/download/].</span></span> <span data-ttu-id="d1110-183">Более старых версиях можно найти в архиве hello здесь: [http://windows.php.net/downloads/releases/archives/].</span><span class="sxs-lookup"><span data-stu-id="d1110-183">Older releases can be found in hello archive here: [http://windows.php.net/downloads/releases/archives/].</span></span>
2. <span data-ttu-id="d1110-184">Изменение hello `php.ini` файл для вашей среды выполнения.</span><span class="sxs-lookup"><span data-stu-id="d1110-184">Modify hello `php.ini` file for your runtime.</span></span> <span data-ttu-id="d1110-185">Обратите внимание, что все параметры конфигурации, являющиеся директивами system-level-only, не будут учитываться веб-приложениями.</span><span class="sxs-lookup"><span data-stu-id="d1110-185">Note that any configuration settings that are system-level-only directives will be ignored by Web Apps.</span></span> <span data-ttu-id="d1110-186">(Дополнительные сведения о директивах только системного уровня см. в разделе [Список директив php.ini].)</span><span class="sxs-lookup"><span data-stu-id="d1110-186">(For information about system-level-only directives, see [List of php.ini directives]).</span></span>
3. <span data-ttu-id="d1110-187">При необходимости добавить расширения среды выполнения PHP tooyour и включить их в hello `php.ini` файла.</span><span class="sxs-lookup"><span data-stu-id="d1110-187">Optionally, add extensions tooyour PHP runtime and enable them in hello `php.ini` file.</span></span>
4. <span data-ttu-id="d1110-188">Добавить `bin` каталог tooyour корневой каталог и put hello каталог, содержащий вашей среды выполнения PHP в нем (например, `bin\php`).</span><span class="sxs-lookup"><span data-stu-id="d1110-188">Add a `bin` directory tooyour root directory, and put hello directory that contains your PHP runtime in it (for example, `bin\php`).</span></span>
5. <span data-ttu-id="d1110-189">Разверните веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="d1110-189">Deploy your web app.</span></span>
6. <span data-ttu-id="d1110-190">Обзор tooyour веб-приложения в hello портала Azure и щелкнуть hello **параметры** кнопки.</span><span class="sxs-lookup"><span data-stu-id="d1110-190">Browse tooyour web app in hello Azure Portal and click on hello **Settings** button.</span></span>
   
    ![Параметры веб-приложения][settings-button]
7. <span data-ttu-id="d1110-192">Из hello **параметры** колонке выберите **параметры приложения** и прокрутите toohello **сопоставления обработчика** раздела.</span><span class="sxs-lookup"><span data-stu-id="d1110-192">From hello **Settings** blade select **Application Settings** and scroll toohello **Handler mappings** section.</span></span> <span data-ttu-id="d1110-193">Добавить `*.php` toohello расширения поле и добавьте путь toohello hello `php-cgi.exe` исполняемый файл.</span><span class="sxs-lookup"><span data-stu-id="d1110-193">Add `*.php` toohello Extension field and add hello path toohello `php-cgi.exe` executable.</span></span> <span data-ttu-id="d1110-194">При размещении вашей среды выполнения PHP в hello `bin` каталогов в корне приложения hello hello путь будет `D:\home\site\wwwroot\bin\php\php-cgi.exe`.</span><span class="sxs-lookup"><span data-stu-id="d1110-194">If you put your PHP runtime in hello `bin` directory in hello root of you application, hello path will be `D:\home\site\wwwroot\bin\php\php-cgi.exe`.</span></span>
   
    ![Укажите обработчик в сопоставлении обработчика][handler-mappings]
8. <span data-ttu-id="d1110-196">Щелкните hello **Сохранить** кнопку вверху hello hello **веб-параметров приложения** колонку.</span><span class="sxs-lookup"><span data-stu-id="d1110-196">Click hello **Save** button at hello top of hello **Web app settings** blade.</span></span>
   
    ![Сохранение параметров конфигурации][save-button]

<a name="composer" />

## <a name="how-to-enable-composer-automation-in-azure"></a><span data-ttu-id="d1110-198">Практическое руководство. Включение автоматизации Composer в Azure</span><span class="sxs-lookup"><span data-stu-id="d1110-198">How to: Enable Composer automation in Azure</span></span>
<span data-ttu-id="d1110-199">По умолчанию служба приложений не выполняет никаких действий с файлом composer.json, если он есть в проекте PHP.</span><span class="sxs-lookup"><span data-stu-id="d1110-199">By default, App Service doesn't do anything with composer.json, if you have one in your PHP project.</span></span> <span data-ttu-id="d1110-200">При использовании [развертывания Git](app-service-deploy-local-git.md), можно включить во время обработки composer.json `git push` путем включения расширения Composer hello.</span><span class="sxs-lookup"><span data-stu-id="d1110-200">If you use [Git deployment](app-service-deploy-local-git.md), you can enable composer.json processing during `git push` by enabling hello Composer extension.</span></span>

> [!NOTE]
> <span data-ttu-id="d1110-201">[Здесь](https://feedback.azure.com/forums/169385-web-apps-formerly-websites/suggestions/6477437-first-class-support-for-composer-and-pip)вы можете отдать свой голос за первоклассную поддержку Composer в службе приложений!</span><span class="sxs-lookup"><span data-stu-id="d1110-201">You can [vote for first-class Composer support in App Service here](https://feedback.azure.com/forums/169385-web-apps-formerly-websites/suggestions/6477437-first-class-support-for-composer-and-pip)!</span></span>
> 
> 

1. <span data-ttu-id="d1110-202">В вашей PHP веб-приложения колонки в hello [портал Azure](https://portal.azure.com), нажмите кнопку **средства** > **расширения**.</span><span class="sxs-lookup"><span data-stu-id="d1110-202">In your PHP web app's blade in hello [Azure portal](https://portal.azure.com), click **Tools** > **Extensions**.</span></span>
   
    ![Azure tooenable колонку параметров портала редактор автоматизации в Azure](./media/web-sites-php-configure/composer-extension-settings.png)
2. <span data-ttu-id="d1110-204">Щелкните **Добавить**, а затем — **Composer**.</span><span class="sxs-lookup"><span data-stu-id="d1110-204">Click **Add**, then click **Composer**.</span></span>
   
    ![Добавление Composer расширения tooenable редактор автоматизации в Azure](./media/web-sites-php-configure/composer-extension-add.png)
3. <span data-ttu-id="d1110-206">Нажмите кнопку **ОК** tooaccept условия.</span><span class="sxs-lookup"><span data-stu-id="d1110-206">Click **OK** tooaccept legal terms.</span></span> <span data-ttu-id="d1110-207">Нажмите кнопку **ОК** снова tooadd hello расширения.</span><span class="sxs-lookup"><span data-stu-id="d1110-207">Click **OK** again tooadd hello extension.</span></span>
   
    <span data-ttu-id="d1110-208">Hello **установленные расширения** колонке теперь будет отображаться расширение Composer hello.</span><span class="sxs-lookup"><span data-stu-id="d1110-208">hello **Installed extensions** blade will now show hello Composer extension.</span></span>  
    <span data-ttu-id="d1110-209">![Примите условия использования tooenable редактор автоматизации в Azure](./media/web-sites-php-configure/composer-extension-view.png)</span><span class="sxs-lookup"><span data-stu-id="d1110-209">![Accept legal terms tooenable Composer automation in Azure](./media/web-sites-php-configure/composer-extension-view.png)</span></span>
4. <span data-ttu-id="d1110-210">Теперь выполните `git add`, `git commit`, и `git push` как и в предыдущем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="d1110-210">Now, perform `git add`, `git commit`, and `git push` like in hello previous section.</span></span> <span data-ttu-id="d1110-211">Вы увидите, что расширение Composer устанавливает зависимости, определенные в файле composer.json.</span><span class="sxs-lookup"><span data-stu-id="d1110-211">You'll now see that Composer is installing dependencies defined in composer.json.</span></span>
   
    ![Развертывание Git с помощью автоматизации Composer в Azure](./media/web-sites-php-configure/composer-extension-success.png)

## <a name="next-steps"></a><span data-ttu-id="d1110-213">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d1110-213">Next steps</span></span>
<span data-ttu-id="d1110-214">Дополнительные сведения см. в разделе hello [Центр разработчика PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="d1110-214">For more information, see hello [PHP Developer Center](/develop/php/).</span></span>

> [!NOTE]
> <span data-ttu-id="d1110-215">Tooget работы в службе приложений Azure перед регистрацией учетную запись Azure, перейдите слишком[повторите служб приложений](https://azure.microsoft.com/try/app-service/), в котором можно немедленно создать кратковременных начальный веб-приложения в службе приложений.</span><span class="sxs-lookup"><span data-stu-id="d1110-215">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="d1110-216">Никаких кредитных карт и обязательств.</span><span class="sxs-lookup"><span data-stu-id="d1110-216">No credit cards required; no commitments.</span></span>
> 
> 

[бесплатной пробной версии]: https://www.windowsazure.com/pricing/free-trial/
[phpinfo()]: http://php.net/manual/en/function.phpinfo.php
[select-php-version]: ./media/web-sites-php-configure/select-php-version.png
[Список директив php.ini]: http://www.php.net/manual/en/ini.list.php
[. user.ini]: http://www.php.net/manual/en/configuration.file.per-user.php
[ini_set()]: http://www.php.net/manual/en/function.ini-set.php
[application-settings]: ./media/web-sites-php-configure/application-settings.png
[settings-button]: ./media/web-sites-php-configure/settings-button.png
[save-button]: ./media/web-sites-php-configure/save-button.png
[php-extensions]: ./media/web-sites-php-configure/php-extensions.png
[handler-mappings]: ./media/web-sites-php-configure/handler-mappings.png
[http://windows.php.net/download/]: http://windows.php.net/download/
[http://windows.php.net/downloads/releases/archives/]: http://windows.php.net/downloads/releases/archives/
[SETPHPVERCLI]: ./media/web-sites-php-configure/ChangePHPVersion-XPlatCLI.png
[GETPHPVERCLI]: ./media/web-sites-php-configure/ShowPHPVersion-XplatCLI.png
[SETPHPVERPS]: ./media/web-sites-php-configure/ChangePHPVersion-PS.png
[GETPHPVERPS]: ./media/web-sites-php-configure/ShowPHPVersion-PS.png

