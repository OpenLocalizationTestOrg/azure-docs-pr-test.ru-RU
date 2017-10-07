---
title: "aaaUsing tooDev tooPublish скриптов Windows PowerShell и тестовых средах | Документы Microsoft"
description: "Узнайте, как сценарии Windows PowerShell toouse из Visual Studio toopublish toodevelopment и в тестовой среде."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 5fff1301-5469-4d97-be88-c85c30f837c1
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: 491a058f96255576afa74f6156f20ae9559bb9f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-windows-powershell-scripts-toopublish-toodev-and-test-environments"></a>С помощью Windows PowerShell сценарии toopublish toodev и в тестовой среде
При создании веб-приложения в Visual Studio, можно создать сценарий Windows PowerShell, можно использовать более поздней версии публикации hello tooautomate tooAzure вашего веб-сайта веб-приложения в службе приложений Azure или виртуальной машины. Можно изменить и расширить hello сценарий Windows PowerShell в toosuit редактора Visual Studio hello требований или интегрировать hello сценарий с существующей сборки, тестирования и публикации скриптов.

С помощью этих сценариев вы можете подготавливать временные пользовательские версии сайта. Эти версии также называют средами разработки и тестирования. Например можно настроить определенную версию веб-сайта на виртуальной машине Azure или на hello промежуточных гнезда toorun веб-сайта набор тестов, воспроизведения ошибки, тестирования исправления ошибки, оценки предложенного изменения или настройки нестандартной среды для проведения демонстрации или презентации. После создания скрипта, публикующего ваш проект, можно воссоздать идентичные среды, повторная hello скрипт или скрипт hello со сборкой вашей toocreate приложения web настраиваемой среды для тестирования.

## <a name="what-you-need"></a>Необходимые элементы
* Пакет Azure SDK, начиная с версии 2.3. Дополнительные сведения см. на странице [скачиваемых файлов для Visual Studio](http://go.microsoft.com/fwlink/?LinkID=624384).

Не обязательно hello Azure SDK toogenerate hello скрипты для веб-проектов. Он предназначен для веб-проектов, а не веб-ролей облачных служб.

* Azure PowerShell, начиная с версии 0.7.4. В разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview) для получения дополнительной информации.
* [Windows PowerShell](http://go.microsoft.com/?linkid=9811175) , начиная с версии 3.0.

## <a name="additional-tools"></a>Дополнительные средства
Если вы занимаетесь разработкой решений для Azure, для работы с PowerShell в Visual Studio доступны дополнительные средства и ресурсы. Ознакомьтесь с разделом [Средства PowerShell для Visual Studio](http://go.microsoft.com/fwlink/?LinkId=404012).

## <a name="generating-hello-publish-scripts"></a>Создание hello скриптов публикации
Hello можно создать скрипты публикации для виртуальной машины, на котором размещается веб-сайта при создании нового проекта, следуя [эти инструкции](virtual-machines/windows/classic/web-app-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json). Можно также [создать сценарии публикации для веб-приложений в службе приложений Azure](app-service-web/app-service-web-get-started-dotnet.md).

## <a name="scripts-that-visual-studio-generates"></a>Сценарии, создаваемые в Visual Studio
Visual Studio создает папку с именем решения на уровне **PublishScripts** , содержащий два файла Windows PowerShell, скрипт публикации для виртуальной машины или веб-сайт и модуль, который содержит функции, которые можно использовать в hello с помощью скрипта. Visual Studio также создает файл в формате JSON hello, с указанием hello hello проекта, в которой выполняется развертывание.

### <a name="windows-powershell-publish-script"></a>Сценарий публикации Windows PowerShell
Hello скрипт публикации содержит определенные действия для развертывания виртуальной машины или веб-сайт tooa публикации. В Visual Studio работает цветовая подсветка синтаксиса Windows PowerShell и доступна справка по функциям. Справка по функции hello доступен, и вы можете свободно изменять функции hello в скрипт toosuit hello собственными потребностями.

### <a name="windows-powershell-module"></a>Модуль Windows PowerShell
Windows PowerShell, модуль, который создается Visual Studio содержит функции, которые hello Hello публикации скрипта используется. Эти функции Azure PowerShell и не предназначен toobe изменены. В разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview) для получения дополнительной информации.

### <a name="json-configuration-file"></a>Файл конфигурации в формате JSON
Hello JSON-файл создается в hello **конфигурации** папки и содержит данные конфигурации, указывающие точно tooAzure toodeploy какие ресурсы. Hello имя файла "hello", Visual Studio создает проект имя WAWS-dev.json при создании веб-сайта или имя проекта-VM-dev.json при создании виртуальной машины. Ниже приведен пример файла конфигурации JSON, который создается для веб-сайта. Большинство значений hello говорят сами за себя. Hello имя веб-сайта формируется Azure, поэтому может не совпадать с именем проекта.

```json
{
    "environmentSettings": {
        "webSite": {
            "name": "WebApplication26632",
            "location": "West US"
        },
        "databases": [{
            "connectionStringName": "DefaultConnection",
            "databaseName": "WebApplication26632_db",
            "serverName": "YourDatabaseServerName",
            "user": "sqluser2",
            "password": "",
            "edition": "",
            "size": "",
            "collation": "",
            "location": "West US"
        }]
    }
}
```
При создании виртуальной машины файл конфигурации JSON hello выглядит примерно следующие toohello. Обратите внимание, что облачная служба создается как контейнер для hello виртуальной машины. Hello виртуальная машина содержит обычные конечные точки hello для веб-доступа по протоколам HTTP и HTTPS, а также конечные точки для веб-развертывания, что позволяет публиковать веб-сайт toohello с локального компьютера, удаленного рабочего стола и Windows PowerShell.

```json
{
    "environmentSettings": {
        "cloudService": {
            "name": "myusernamevm1",
            "affinityGroup": "",
            "location": "West US",
            "virtualNetwork": "",
            "subnet": "",
            "availabilitySet": "",
            "virtualMachine": {
                "name": "myusernamevm1",
                "vhdImage": "a699494373c04fc0bc8f2bb1389d6106__Win2K8R2SP1-Datacenter-201403.01-en.us-127GB.vhd",
                "size": "Small",
                "user": "vmuser1",
                "password": "",
                "enableWebDeployExtension": true,
                "endpoints": [{
                        "name": "Http",
                        "protocol": "TCP",
                        "publicPort": "80",
                        "privatePort": "80"
                    },
                    {
                        "name": "Https",
                        "protocol": "TCP",
                        "publicPort": "443",
                        "privatePort": "443"
                    },
                    {
                        "name": "WebDeploy",
                        "protocol": "TCP",
                        "publicPort": "8172",
                        "privatePort": "8172"
                    },
                    {
                        "name": "Remote Desktop",
                        "protocol": "TCP",
                        "publicPort": "3389",
                        "privatePort": "3389"
                    },
                    {
                        "name": "Powershell",
                        "protocol": "TCP",
                        "publicPort": "5986",
                        "privatePort": "5986"
                    }
                ]
            }
        },
        "databases": [{
            "connectionStringName": "",
            "databaseName": "",
            "serverName": "",
            "user": "",
            "password": ""
        }],
        "webDeployParameters": {
            "iisWebApplicationName": "Default Web Site"
        }
    }
}
```

Можно изменить toochange конфигурации JSON hello, что происходит при запуске hello скрипты публикации. Hello `cloudService` и `virtualMachine` разделы являются обязательными, но можно удалить hello `databases` статьи, если он не нужен. Hello свойства, которые являются пустыми в файле конфигурации по умолчанию hello, создаваемый Visual Studio являются необязательными; те, которые имеют значения в файле конфигурации по умолчанию hello являются обязательными.

Если у вас есть веб-сайт с несколькими средами развертывания (слотами) вместо одного рабочего сайта в Azure, можно включить имя слота hello в имени hello hello веб-сайта в файл конфигурации JSON hello. Например, если у вас есть веб-сайта, которая называется **mysite** и слот для него с именем **тестирования** hello URI является mysite test.cloudapp.net, но hello toouse правильное имя в файле конфигурации hello — mysite(test) . Вы можете только этого hello веб-сайт и слоты уже существуют в вашей подписке. Если они не существуют, создайте hello веб-сайт, запустив сценарий hello без указания слота hello, а затем создайте слот hello в hello [классический портал Azure](http://go.microsoft.com/fwlink/?LinkID=213885), и после этого запустите сценарий hello с именем hello измененного веб-сайта. Дополнительные сведения о слотах развертывания для веб-приложений см. в статье [Настройка промежуточных сред для веб-приложений в службе приложений Azure](app-service-web/web-sites-staged-publishing.md).

## <a name="how-toorun-hello-publish-scripts"></a>Как toorun hello публикации скриптов
Если вы еще не запускали скрипт Windows PowerShell, необходимо сначала установить hello выполнения политики tooenable сценариев toorun. Это значение безопасности функция tooprevent пользователям выполнение сценариев Windows PowerShell, если они уязвимы toomalware или вирусов, связанные с выполнением скриптов.

### <a name="run-hello-script"></a>Запустите сценарий hello
1. Создайте пакет hello веб-развертывания для проекта. Пакет веб-развертывания представляет собой сжатый архив (ZIP-файл) с файлами, требуется toocopy tooyour веб-сайта или виртуальной машины. В Visual Studio можно создавать пакеты веб-развертывания для любых веб-приложений.

![Создание пакета веб-развертывания](./media/vs-azure-tools-publishing-using-powershell-scripts/IC767885.png)

Дополнительные сведения см. в статье [Как создать пакет веб-развертывания в Visual Studio](https://msdn.microsoft.com/library/dd465323.aspx). Также можно автоматизировать создание hello пакета веб-развертывания, как описано в разделе "hello" **Настройка и расширение hello скрипты публикации** далее в этом разделе.

1. В **обозревателе решений**, откройте контекстное меню hello hello скрипта и нажмите кнопку **открыть с помощью PowerShell ISE**.
2. Если это hello при первом запуске после выполнения сценариев Windows PowerShell на этом компьютере, откройте окно командной строки с правами администратора и типа hello следующую команду:

    ```powershell
    Set-ExecutionPolicy RemoteSigned
    ```

3. Войти в tooAzure, используя следующую команду hello.

    ```powershell
    Add-AzureAccount
    ```

    При появлении запроса введите свои имя пользователя и пароль.

    Обратите внимание, что при автоматизации hello скрипта Данный способ указания учетных данных Azure не будет работать. Вместо этого следует использовать учетные данные tooprovide hello .publishsettings файлов. Один раз, можно использовать только команды hello **Get-AzurePublishSettingsFile** toodownload hello файл из Azure, а впоследствии используете **команду Import-AzurePublishSettingsFile** файл tooimport hello. Подробные инструкции см. в разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview).

4. (Необязательно) Если требуется, чтобы toocreate Azure использовать ресурсы, такие как hello виртуальной машины, базы данных и веб-сайт, не публикуя веб-приложения hello **Publish-WebApplication.ps1** с hello **-конфигурации** аргумент значение toohello JSON-файл конфигурации. Эта командная строка использует toodetermine файл конфигурации JSON hello toocreate какие ресурсы. Так как оно использует параметры по умолчанию hello для других аргументов командной строки, он создает ресурсы hello, но не публиковать веб-приложения. Hello — параметр Verbose выводит дополнительную информацию о происходящем.

    ```powershell
    Publish-WebApplication.ps1 -Verbose –Configuration C:\Path\WebProject-WAWS-dev.json
    ```

5. Используйте hello **Publish-WebApplication.ps1** команды, как показано в одном hello следующие примеры tooinvoke hello скрипт и опубликовать веб-приложения. При необходимости параметры по умолчанию hello toooverride для любого hello других аргументов, например имя подписки hello, публикации, имя пакета, учетных данных виртуальной машины или учетные данные сервера базы данных, можно указать эти параметры. Используйте hello **– Verbose** параметр toosee Дополнительные сведения о ходе выполнения hello hello процесс публикации.

    ```powershell
    Publish-WebApplication.ps1 –Configuration C:\Path\WebProject-WAWS-dev-json `
    –SubscriptionName Contoso `
    -WebDeployPackage C:\Documents\Azure\ADWebApp.zip `
    -DatabaseServerPassword @{Name="dbServerName";Password="adminPassword"} `
    -Verbose
    ```

    При создании виртуальной машины hello команда выглядит как следующий hello. В этом примере также показано, как toospecify hello учетные данные для нескольких баз данных. Для hello виртуальных машин, создаваемых этими скриптами SSL-сертификат hello не из доверенного корневого центра. Поэтому необходимо toouse hello **– AllowUntrusted** параметр.

    ```powershell
    Publish-WebApplication.ps1 `
    -Configuration C:\Path\ADVM-VM-test.json `
    -SubscriptionName Contoso `
    -WebDeployPackage C:\Path\ADVM.zip `
    -AllowUntrusted `
    -VMPassword @{name = "vmUserName"; password = "YourPasswordHere"} `
    -DatabaseServerPassword @{Name="server1";Password="adminPassword1"}, @{Name="server2";Password="adminPassword2"} `
    -Verbose
    ```

    Hello скрипта можно создавать базы данных, но она не создает серверы баз данных. Если вы хотите toocreate сервера базы данных, можно использовать hello **New-AzureSqlDatabaseServer** функции hello модуль Azure.

## <a name="customizing-and-extending-hello-publish-scripts"></a>Настройка и расширение hello скриптов публикации
Вы можете настроить hello публикации скрипта и файл конфигурации JSON. Здравствуйте, функции в модуле Windows PowerShell hello **AzureWebAppPublishModule.psm1** не предполагаемого toobe изменены. Если просто требуется toospecify другую базу данных или изменить некоторые свойства hello hello виртуальной машины, измените файл конфигурации JSON hello. Если функции hello tooextend hello tooautomate скрипт построения и тестирования своего проекта, можно реализовать заглушки функций в **Publish-WebApplication.ps1**.

tooautomate при построении проекта, добавьте код, вызывающий MSBuild слишком`New-WebDeployPackage` , как показано в следующем примере кода. путь Hello toohello команды MSBuild отличается в зависимости от версии Visual Studio, вы установили hello. tooget hello правильный путь, можно использовать функции hello **Get-MSBuildCmd**, как показано в следующем примере.

### <a name="tooautomate-building-your-project"></a>сборка проекта tooautomate
1. Добавить hello `$ProjectFile` параметр в hello глобальный раздел параметров.

    ```powershell
    [Parameter(Mandatory = $false)]
    [ValidateScript({Test-Path $_ -PathType Leaf})]
    [String]
    $ProjectFile,
    ```

2. Скопируйте функции hello `Get-MSBuildCmd` в файл скрипта.

    ```powershell
    function Get-MSBuildCmd
    {
            process
    {

                $path =  Get-ChildItem "HKLM:\SOFTWARE\Microsoft\MSBuild\ToolsVersions\" |
                                    Sort-Object {[double]$_.PSChildName} -Descending |
                                    Select-Object -First 1 |
                                    Get-ItemProperty -Name MSBuildToolsPath |
                                    Select -ExpandProperty MSBuildToolsPath

                $path = (Join-Path -Path $path -ChildPath 'msbuild.exe')

            return Get-Item $path
        }
    }
    ```

3. Замените `New-WebDeployPackage` с hello следующим кодом и замените заполнители hello в строке, создающей hello `$msbuildCmd`. Этот код предназначен для Visual Studio 2015. Если вы используете Visual Studio 2013, измените hello **VisualStudioVersion** свойство ниже слишком`12.0`.

    ```powershell
    function New-WebDeployPackage
    {
        #Write a function toobuild and package your web application
    ```

    toobuild вашего веб-приложения, используйте MsBuild.exe. Справочник по командной строке MSBuild доступен по адресу [http://go.microsoft.com/fwlink/?LinkId=391339](http://go.microsoft.com/fwlink/?LinkId=391339).

    ```powershell
    Write-VerboseWithTime 'Build-WebDeployPackage: Start'

    $msbuildCmd = '"{0}" "{1}" /T:Rebuild;Package /P:VisualStudioVersion=14.0 /p:OutputPath="{2}\MSBuildOutputPath" /flp:logfile=msbuild.log,v=d' -f (Get-MSBuildCmd), $ProjectFile, $scriptDirectory

    Write-VerboseWithTime ('Build-WebDeployPackage: ' + $msbuildCmd)
    ```

### <a name="start-execution-of-hello-build-command"></a>Запуск выполнения команды построения hello

```powershell
$job = Start-Process cmd.exe -ArgumentList('/C "' + $msbuildCmd + '"') -WindowStyle Normal -Wait -PassThru

if ($job.ExitCode -ne 0) {
    throw('MsBuild exited with an error. ExitCode:' + $job.ExitCode)
}

#Obtain hello project name
$projectName = (Get-Item $ProjectFile).BaseName

#Construct hello path tooweb deploy zip package
$DeployPackageDir =  '.\MSBuildOutputPath\_PublishedWebsites\{0}_Package\{0}.zip' -f $projectName

#Get hello full path for hello web deploy zip package. This is required for MSDeploy toowork
$WebDeployPackage = Resolve-Path –LiteralPath $DeployPackageDir

Write-VerboseWithTime 'Build-WebDeployPackage: End'

return $WebDeployPackage
}
```

1. Вызовите hello `New-WebDeployPackage` функции перед этой строкой: `$Config = Read-ConfigFile $Configuration` для веб-приложений или `$Config = Read-ConfigFile $Configuration -HasWebDeployPackage:([Bool]$WebDeployPackage)` для виртуальных машин.

    ```powershell
    if($ProjectFile)
    {
    $WebDeployPackage = New-WebDeployPackage
    }
    ```

2. Вызвать hello настроить сценарий из командной строки с помощью передачи hello `$Project` аргументу, как hello следующий пример командной строки.

    ```powershell
    .\Publish-WebApplicationVM.ps1 -Configuration .\Configurations\WebApplication5-VM-dev.json `
    -ProjectFile ..\WebApplication5\WebApplication5.csproj `
    -VMPassword @{Name="VMUser";Password="Test.123"} `
    -AllowUntrusted `
    -Verbose
    ```

    Тестирование tooautomate приложения, добавьте код слишком`Test-WebApplication`. Быть toouncomment убедиться, что строки hello в **Publish-WebApplication.ps1** где вызываются эти функции. Если реализация не предоставлена, можно вручную построить проект с помощью Visual Studio и опубликуйте tooAzure toopublish сценария выполнения hello.

## <a name="publishing-function-summary"></a>Обзор функций публикации
Команда tooget справки для функций, которые можно использовать в командной строке Windows PowerShell hello hello `Get-Help function-name`. Hello справки включает параметр и примеры их использования. Hello же справка включена в исходных файлов скриптов hello **AzureWebAppPublishModule.psm1** и **Publish-WebApplication.ps1**. Hello скрипт и Справка переведены на языке Visual Studio.

**AzureWebAppPublishModule**

| Имя функции | Описание |
| --- | --- |
| Add-AzureSQLDatabase |Создает новую базу данных SQL Azure. |
| Add-AzureSQLDatabases |Создает базы данных Azure SQL на основе значений hello в файл конфигурации JSON hello, создаваемый Visual Studio. |
| Add-AzureVM |Создает виртуальную машину Azure и возвращает URL-адрес hello hello развертывания ВМ. Hello функция настраивает hello предварительные требования, а затем вызывает hello **New-AzureVM** функции toocreate (модуль Azure) новой виртуальной машины. |
| Add-AzureVMEndpoints |Добавляет новую виртуальную машину tooa входных конечных точек и возвращает hello виртуальной машины с новой конечной точки hello. |
| Add-AzureVMStorage |Создает новую учетную запись хранилища Azure в текущей подписке hello. Имя учетной записи hello Hello начинается с «devtest», и уникальный буквенно-цифровой строки. функция Hello возвращает имя hello hello новой учетной записи хранения. Необходимо указать расположение или территориальную группу для новой учетной записи хранения hello. |
| Add-AzureWebsite |Создает веб-сайт с указанным именем hello и расположением. Эта функция вызывает hello **New-AzureWebsite** функции hello модуль Azure. Если подписка hello не включает веб-сайт с указанным именем hello, эта функция создает веб-сайт hello и возвращает объект веб-сайта. В противном случае она возвращает `$null`. |
| Backup-Subscription |Здравствуйте, сохраняет текущую подписку Azure в hello `$Script:originalSubscription` переменной в области сценариев. Эта функция сохраняет текущую подписку hello Azure (полученную с помощью `Get-AzureSubscription -Current`) и его учетной записи хранилища и hello подписку, которая изменяется этим скриптом (хранится в переменной hello `$UserSpecifiedSubscription`) и ее учетную запись хранения, в области сценариев. Сохранение значений hello, можно использовать функции, такие как `Restore-Subscription`, toorestore hello исходной текущей подписки и хранения состояние учетной записи toocurrent при изменении текущего состояния hello. |
| Find-AzureVM |Hello возвращает указана виртуальной машины Azure. |
| Format-DevTestMessageWithTime |Добавляет приветственное сообщение tooa даты и времени. Эта функция предназначена для сообщений, записываемых toohello потоки Error и Verbose. |
| Get-AzureSQLDatabaseConnectionString |Выполняет сборку соединения строки tooconnect tooan базы данных Azure SQL. |
| Get-AzureVMStorage |Возвращает имя hello первой учетной записи хранения с шаблоном имени hello Здравствуйте, «devtest*"(без учета регистра) в hello указанного расположения или территориальной группе. Если hello «devtest*"не соответствует учетной записи хранилища hello расположение или территориальная группа, hello функция пропускает ее. Необходимо указать расположение или территориальную группу. |
| Get-MSDeployCmd |Возвращает средство команда hello toorun MsDeploy.exe. |
| New-AzureVMEnvironment |Находит или создает виртуальную машину в подписке hello, соответствующий значениям hello в файле конфигурации JSON hello. |
| Publish-WebPackage |Использует MsDeploy.exe и откроется веб-публикации пакета. ZIP-файл toodeploy ресурсов tooa веб-сайта. Эта функция не создает никаких выходных данных. В случае вызова tooMSDeploy.exe hello hello функция создает исключение. tooget более подробные выходные данные, используйте hello **-Verbose** параметр. |
| Publish-WebPackageToVM |Проверяет значения параметров hello, а затем вызывает hello **Publish-WebPackage** функции. |
| Read-ConfigFile |Проверяет файл конфигурации JSON hello и возвращает хэш-таблицу выбранных значений. |
| Restore-Subscription |Сбрасывает hello текущей подписки toohello исходной подписки. |
| Test-AzureModule |Возвращает `$true` Если hello установлен модуль Azure версии 0.7.4 или более поздней версии. Возвращает `$false` Если hello модуль не установлен или имеет более раннюю версию. У этой функции нет параметров. |
| Test-AzureModuleVersion |Возвращает `$true` Если hello hello модуль Azure версии 0.7.4 или более поздней версии. Возвращает `$false` Если hello модуль не установлен или имеет более раннюю версию. У этой функции нет параметров. |
| Test-HttpsUrl |Преобразует входной объект в System.Uri URL-адрес tooa hello. Возвращает `$True` Если hello URL-адрес является абсолютным и использует схему https. Возвращает `$false` Если hello URL-адрес является относительным, его схема не является HTTPS или hello входная строка не может быть преобразованный tooa URL-адрес. |
| Test-Member |Возвращает `$true` Если свойство или метод является членом hello объекта. В противном случае возвращается `$false`. |
| Write-ErrorWithTime |Записывает сообщение об ошибке с префиксом hello текущее время. Эта функция вызывает hello **Format-DevTestMessageWithTime** функция tooprepend hello время перед записью поток сообщений об ошибках toohello сообщение hello. |
| Write-HostWithTime |Записывает сообщение toohello основную программу (**Write-Host**) префикс hello текущее время. результат Hello записи toohello основную программу варьируется. Большинство программ, на которых размещены Windows PowerShell, записывают эти сообщения toostandard выходных данных. |
| Write-VerboseWithTime |Записывает подробное сообщение с hello префиксом текущее время. Так как он вызывает **Write-Verbose**, приветственное сообщение отображается только тогда, когда скрипт hello запуске с hello **Verbose** параметр или если hello **VerbosePreference** приоритет — значение слишком**Продолжить**. |

**Publish-WebApplication**

| Имя функции | Описание |
| --- | --- |
| New-AzureWebApplicationEnvironment |Создает ресурсы Azure, например веб-сайт или виртуальную машину. |
| New-WebDeployPackage |Эта функция не реализована. Можно добавить команды в этой функции toobuild проекта. |
| Publish-AzureWebApplication |Публикует tooAzure приложения web. |
| Publish-WebApplication |Создает и развертывает веб-приложения, виртуальные машины, базы данных SQL и учетные записи хранения для веб-проекта Visual Studio. |
| Test-WebApplication |Эта функция не реализована. Вы можете добавлять команды в этой функции tootest приложения. |

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения о возможностях сценариев PowerShell, считывая [использование скриптов Windows PowerShell](https://technet.microsoft.com/library/bb978526.aspx) и увидеть другие скрипты Azure PowerShell hello [центра сценариев](https://azure.microsoft.com/documentation/scripts/).
