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
# <a name="configure-php-in-azure-app-service-web-apps"></a>Настройка PHP в веб-приложениях службы приложений Azure
## <a name="introduction"></a>Введение
В этом руководстве будет показано, как tooconfigure hello встроенных среды выполнения PHP для веб-приложений в [службе приложений Azure](http://go.microsoft.com/fwlink/?LinkId=529714)Укажите настраиваемую среду выполнения PHP и включить расширения. Регистрация toouse службы приложений для hello [бесплатной пробной версии]. tooget hello наиболее из этого руководства, необходимо сначала создать веб-приложения PHP в службе приложений.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="how-to-change-hello-built-in-php-version"></a>Как: изменение hello встроенных PHP версии
По умолчанию при создании веб-приложения службы приложений устанавливается среда PHP 5.5, которая будет сразу готова для использования. Здравствуйте, лучшим способом toosee hello доступные версии конфигурации по умолчанию, и hello включенных расширений является скрипт, который вызывает hello toodeploy [phpinfo()] функции.

Версии PHP 5.6 и PHP 7.0 также доступны, но не включены по умолчанию. hello tooupdate версии PHP, выполните один из следующих методов.

### <a name="azure-portal"></a>Портал Azure
1. Обзор tooyour веб-приложения в hello [портала Azure](https://portal.azure.com) и щелкнет hello **параметры** кнопки.
   
    ![Параметры веб-приложения][settings-button]
2. Из hello **параметры** колонке выберите **параметры приложения** и выберите новую версию PHP hello.
   
    ![Параметры приложения][application-settings]
3. Щелкните hello **Сохранить** кнопку вверху hello hello **веб-параметров приложения** колонку.
   
    ![Сохранение параметров конфигурации][save-button]

### <a name="azure-powershell-windows"></a>Azure PowerShell (только для Windows)
1. Откройте Azure PowerShell и учетной записи входа tooyour:
   
        PS C:\> Login-AzureRmAccount
2. Задание версии PHP hello для веб-приложения hello.
   
        PS C:\> Set-AzureWebsite -PhpVersion {5.5 | 5.6 | 7.0} -Name {app-name}
3. Установка версии PHP Hello. Можно подтвердить эти параметры.
   
        PS C:\> Get-AzureWebsite -Name {app-name} | findstr PhpVersion

### <a name="azure-command-line-interface-linux-mac-windows"></a>Интерфейс командной строки Azure для Mac, Linux и Windows
toouse hello Azure интерфейс командной строки, необходимо иметь **Node.js** установлены на компьютере.

1. Откройте терминалов и учетная запись tooyour входа.
   
        azure login
2. Задание версии PHP hello для веб-приложения hello.
   
        azure site set --php-version {5.5 | 5.6 | 7.0} {app-name}

3. Установка версии PHP Hello. Можно подтвердить эти параметры.
   
        azure site show {app-name}

> [!NOTE] 
> Hello [Azure CLI 2.0](https://github.com/Azure/azure-cli) команды, эквивалентные toohello выше:
>
>

    az login
    az appservice web config update --php-version {5.5 | 5.6 | 7.0} -g {resource-group-name} -n {app-name}
    az appservice web config show -g {resource-group-name} -n {app-name}

## <a name="how-to-change-hello-built-in-php-configurations"></a>Как: изменение конфигурации PHP для встроенных hello
Для любой встроенной среде выполнения PHP можно изменить любые параметры конфигурации hello, hello описанных ниже действий. (Дополнительные сведения о директивах php.ini см. в разделе [Список директив php.ini].)

### <a name="changing-phpiniuser-phpiniperdir-phpiniall-configuration-settings"></a>Изменение параметров конфигурации PHP\_INI\_USER, PHP\_INI\_PERDIR, PHP\_INI\_ALL
1. Добавить [. user.ini] корневой каталог файлов tooyour.
2. Добавление конфигурации настроек toohello `.user.ini` текстовый файл с помощью hello того же синтаксиса, вы будете использовать в `php.ini` файла. Например, если требуется, чтобы tooturn hello `display_errors` параметр нужное значение и задайте `upload_max_filesize` параметр too10M, вашей `.user.ini` файл будет содержать следующий текст:
   
        ; Example Settings
        display_errors=On
        upload_max_filesize=10M
   
        ; OPTIONAL: Turn this on toowrite errors tood:\home\LogFiles\php_errors.log
        ; log_errors=On
3. Разверните веб-приложение.
4. Перезапустите веб-приложение hello. (Перезагрузка необходима, так как hello частота, с которой PHP считывает `.user.ini` файлы регулируется hello `user_ini.cache_ttl` параметр, который является параметром уровня системы, составляет 300 секунд (5 минут) по умолчанию. Перезапускать веб-приложения hello принудительно PHP tooread hello новые параметры для hello `.user.ini` файл.)

Как альтернативный toousing `.user.ini` файл, можно использовать hello [ini_set()] функции в параметры конфигурации tooset скрипты, которые не являются директивами системного уровня.

### <a name="changing-phpinisystem-configuration-settings"></a>Изменение параметров конфигурации PHP\_INI\_SYSTEM
1. Добавить параметр приложения tooyour веб-приложения, с ключом hello `PHP_INI_SCAN_DIR` и значение`d:\home\site\ini`
2. Создание `settings.ini` текстовый файл с помощью консоли Kudu (http://&lt;имя сайта&gt;. scm.azurewebsite.net) в hello `d:\home\site\ini` каталога.
3. Добавление конфигурации настроек toohello `settings.ini` текстовый файл с помощью hello того же синтаксиса, используется в файле php.ini. Например, если требуется, чтобы toopoint hello `curl.cainfo` параметр tooa `*.crt` и задайте wincache.maxfilesize параметр too512K, ваш `settings.ini` файл будет содержать этот текст:
   
        ; Example Settings
        curl.cainfo="%ProgramFiles(x86)%\Git\bin\curl-ca-bundle.crt"
        wincache.maxfilesize=512
4. Перезапустите изменения hello tooload веб-приложения.

## <a name="how-to-enable-extensions-in-hello-default-php-runtime"></a>Как: включить расширения в среде выполнения PHP по умолчанию hello
Как отмечалось в hello предыдущего раздела, hello лучшим способом toosee hello версия по умолчанию PHP, его конфигурация по умолчанию и включены hello расширения — toodeploy скрипт, который вызывает [phpinfo()]. tooenable Дополнительные расширения, выполните следующие действия hello.

### <a name="configure-via-ini-settings"></a>Настройка с помощью параметров ini
1. Добавить `ext` toohello каталога `d:\home\site` каталога.
2. Поместите `.dll` расширения файлов в hello `ext` каталога (например, `php_xdebug.dll`). Убедитесь в том, что расширения hello совместимы с версией по умолчанию PHP и являются VC9 и совместимость не потокобезопасный (Обновить).
3. Добавить параметр приложения tooyour веб-приложения, с ключом hello `PHP_INI_SCAN_DIR` и значение`d:\home\site\ini`
4. Создайте файл `ini` в `d:\home\site\ini` с именем `extensions.ini`.
5. Добавление конфигурации настроек toohello `extensions.ini` текстовый файл с помощью hello того же синтаксиса, используется в файле php.ini. Например, если требуется, чтобы расширений MongoDB и XDebug hello tooenable ваш `extensions.ini` файл будет содержать следующий текст:
   
        ; Enable Extensions
        extension=d:\home\site\ext\php_mongo.dll
        zend_extension=d:\home\site\ext\php_xdebug.dll
6. Перезапустите изменения hello tooload веб-приложения.

### <a name="configure-via-app-setting"></a>Настройка с помощью параметров приложения
1. Добавить `bin` каталог toohello корневой каталог.
2. Поместите `.dll` расширения файлов в hello `bin` каталога (например, `php_xdebug.dll`). Убедитесь в том, что расширения hello совместимы с версией по умолчанию PHP и являются VC9 и совместимость не потокобезопасный (Обновить).
3. Разверните веб-приложение.
4. Обзор tooyour веб-приложения в hello портала Azure и щелкнуть hello **параметры** кнопки.
   
    ![Параметры веб-приложения][settings-button]
5. Из hello **параметры** колонке выберите **параметры приложения** и прокрутите toohello **параметры приложения** раздела.
6. В hello **параметры приложения** создайте **PHP_EXTENSIONS** ключа. Hello значение для этого ключа будет иметь корневой путь относительный toowebsite: **файл bin\your-ext**.
   
    ![Включение расширения в параметрах приложения][php-extensions]
7. Щелкните hello **Сохранить** кнопку вверху hello hello **веб-параметров приложения** колонку.
   
    ![Сохранение параметров конфигурации][save-button]

Расширения Zend также поддерживаются с помощью ключа **PHP_ZENDEXTENSIONS**. tooenable несколько расширений включает список разделенных запятыми `.dll` файлы для hello значение параметра приложения.

## <a name="how-to-use-a-custom-php-runtime"></a>Практическое руководство. Настраиваемая среда выполнения PHP
Вместо среды выполнения PHP по умолчанию hello приложения службы веб-приложений можно использовать среду выполнения PHP предоставляют tooexecute скрипты PHP. можно настроить Hello среды выполнения, который предоставляется с `php.ini` файл, который также предоставляют. toouse пользовательской среды выполнения PHP для веб-приложений, выполните шаги hello.

1. Получите версию PHP для Windows, совместимую с VC9 или VC11 и непотокобезопасной технологией (nts). Последние версии PHP для Windows можно найти здесь: [http://windows.php.net/download/]. Более старых версиях можно найти в архиве hello здесь: [http://windows.php.net/downloads/releases/archives/].
2. Изменение hello `php.ini` файл для вашей среды выполнения. Обратите внимание, что все параметры конфигурации, являющиеся директивами system-level-only, не будут учитываться веб-приложениями. (Дополнительные сведения о директивах только системного уровня см. в разделе [Список директив php.ini].)
3. При необходимости добавить расширения среды выполнения PHP tooyour и включить их в hello `php.ini` файла.
4. Добавить `bin` каталог tooyour корневой каталог и put hello каталог, содержащий вашей среды выполнения PHP в нем (например, `bin\php`).
5. Разверните веб-приложение.
6. Обзор tooyour веб-приложения в hello портала Azure и щелкнуть hello **параметры** кнопки.
   
    ![Параметры веб-приложения][settings-button]
7. Из hello **параметры** колонке выберите **параметры приложения** и прокрутите toohello **сопоставления обработчика** раздела. Добавить `*.php` toohello расширения поле и добавьте путь toohello hello `php-cgi.exe` исполняемый файл. При размещении вашей среды выполнения PHP в hello `bin` каталогов в корне приложения hello hello путь будет `D:\home\site\wwwroot\bin\php\php-cgi.exe`.
   
    ![Укажите обработчик в сопоставлении обработчика][handler-mappings]
8. Щелкните hello **Сохранить** кнопку вверху hello hello **веб-параметров приложения** колонку.
   
    ![Сохранение параметров конфигурации][save-button]

<a name="composer" />

## <a name="how-to-enable-composer-automation-in-azure"></a>Практическое руководство. Включение автоматизации Composer в Azure
По умолчанию служба приложений не выполняет никаких действий с файлом composer.json, если он есть в проекте PHP. При использовании [развертывания Git](app-service-deploy-local-git.md), можно включить во время обработки composer.json `git push` путем включения расширения Composer hello.

> [!NOTE]
> [Здесь](https://feedback.azure.com/forums/169385-web-apps-formerly-websites/suggestions/6477437-first-class-support-for-composer-and-pip)вы можете отдать свой голос за первоклассную поддержку Composer в службе приложений!
> 
> 

1. В вашей PHP веб-приложения колонки в hello [портал Azure](https://portal.azure.com), нажмите кнопку **средства** > **расширения**.
   
    ![Azure tooenable колонку параметров портала редактор автоматизации в Azure](./media/web-sites-php-configure/composer-extension-settings.png)
2. Щелкните **Добавить**, а затем — **Composer**.
   
    ![Добавление Composer расширения tooenable редактор автоматизации в Azure](./media/web-sites-php-configure/composer-extension-add.png)
3. Нажмите кнопку **ОК** tooaccept условия. Нажмите кнопку **ОК** снова tooadd hello расширения.
   
    Hello **установленные расширения** колонке теперь будет отображаться расширение Composer hello.  
    ![Примите условия использования tooenable редактор автоматизации в Azure](./media/web-sites-php-configure/composer-extension-view.png)
4. Теперь выполните `git add`, `git commit`, и `git push` как и в предыдущем разделе hello. Вы увидите, что расширение Composer устанавливает зависимости, определенные в файле composer.json.
   
    ![Развертывание Git с помощью автоматизации Composer в Azure](./media/web-sites-php-configure/composer-extension-success.png)

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения см. в разделе hello [Центр разработчика PHP](/develop/php/).

> [!NOTE]
> Tooget работы в службе приложений Azure перед регистрацией учетную запись Azure, перейдите слишком[повторите служб приложений](https://azure.microsoft.com/try/app-service/), в котором можно немедленно создать кратковременных начальный веб-приложения в службе приложений. Никаких кредитных карт и обязательств.
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

