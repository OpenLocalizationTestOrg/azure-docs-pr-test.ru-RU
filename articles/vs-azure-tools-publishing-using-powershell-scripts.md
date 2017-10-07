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
# <a name="using-windows-powershell-scripts-toopublish-toodev-and-test-environments"></a><span data-ttu-id="23fcd-103">С помощью Windows PowerShell сценарии toopublish toodev и в тестовой среде</span><span class="sxs-lookup"><span data-stu-id="23fcd-103">Using Windows PowerShell scripts toopublish toodev and test environments</span></span>
<span data-ttu-id="23fcd-104">При создании веб-приложения в Visual Studio, можно создать сценарий Windows PowerShell, можно использовать более поздней версии публикации hello tooautomate tooAzure вашего веб-сайта веб-приложения в службе приложений Azure или виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="23fcd-104">When you create a web application in Visual Studio, you can generate a Windows PowerShell script that you can use later tooautomate hello publishing of your website tooAzure as a Web App in Azure App Service or a virtual machine.</span></span> <span data-ttu-id="23fcd-105">Можно изменить и расширить hello сценарий Windows PowerShell в toosuit редактора Visual Studio hello требований или интегрировать hello сценарий с существующей сборки, тестирования и публикации скриптов.</span><span class="sxs-lookup"><span data-stu-id="23fcd-105">You can edit and extend hello Windows PowerShell script in hello Visual Studio editor toosuit your requirements, or integrate hello script with existing build, test, and publishing scripts.</span></span>

<span data-ttu-id="23fcd-106">С помощью этих сценариев вы можете подготавливать временные пользовательские версии сайта. Эти версии также называют средами разработки и тестирования.</span><span class="sxs-lookup"><span data-stu-id="23fcd-106">Using these scripts, you can provision customized versions (also known as dev and test environments) of your site for temporary use.</span></span> <span data-ttu-id="23fcd-107">Например можно настроить определенную версию веб-сайта на виртуальной машине Azure или на hello промежуточных гнезда toorun веб-сайта набор тестов, воспроизведения ошибки, тестирования исправления ошибки, оценки предложенного изменения или настройки нестандартной среды для проведения демонстрации или презентации.</span><span class="sxs-lookup"><span data-stu-id="23fcd-107">For example, you might set up a particular version of your website on an Azure virtual machine or on hello staging slot on a website toorun a test suite, reproduce a bug, test a bug fix, trial a proposed change, or set up a custom environment for a demo or presentation.</span></span> <span data-ttu-id="23fcd-108">После создания скрипта, публикующего ваш проект, можно воссоздать идентичные среды, повторная hello скрипт или скрипт hello со сборкой вашей toocreate приложения web настраиваемой среды для тестирования.</span><span class="sxs-lookup"><span data-stu-id="23fcd-108">After you've created a script that publishes your project, you can recreate identical environments by re-running hello script as needed, or run hello script with your own build of your web application toocreate a custom environment for testing.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="23fcd-109">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="23fcd-109">What you need</span></span>
* <span data-ttu-id="23fcd-110">Пакет Azure SDK, начиная с версии 2.3.</span><span class="sxs-lookup"><span data-stu-id="23fcd-110">Azure SDK 2.3 or later.</span></span> <span data-ttu-id="23fcd-111">Дополнительные сведения см. на странице [скачиваемых файлов для Visual Studio](http://go.microsoft.com/fwlink/?LinkID=624384).</span><span class="sxs-lookup"><span data-stu-id="23fcd-111">See [Visual Studio Downloads](http://go.microsoft.com/fwlink/?LinkID=624384) for more information.</span></span>

<span data-ttu-id="23fcd-112">Не обязательно hello Azure SDK toogenerate hello скрипты для веб-проектов.</span><span class="sxs-lookup"><span data-stu-id="23fcd-112">You do not need hello Azure SDK toogenerate hello scripts for web projects.</span></span> <span data-ttu-id="23fcd-113">Он предназначен для веб-проектов, а не веб-ролей облачных служб.</span><span class="sxs-lookup"><span data-stu-id="23fcd-113">This feature is for web projects, not web roles in cloud services.</span></span>

* <span data-ttu-id="23fcd-114">Azure PowerShell, начиная с версии 0.7.4.</span><span class="sxs-lookup"><span data-stu-id="23fcd-114">Azure PowerShell 0.7.4 or later.</span></span> <span data-ttu-id="23fcd-115">В разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview) для получения дополнительной информации.</span><span class="sxs-lookup"><span data-stu-id="23fcd-115">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for more information.</span></span>
* <span data-ttu-id="23fcd-116">[Windows PowerShell](http://go.microsoft.com/?linkid=9811175) , начиная с версии 3.0.</span><span class="sxs-lookup"><span data-stu-id="23fcd-116">[Windows PowerShell 3.0](http://go.microsoft.com/?linkid=9811175) or later.</span></span>

## <a name="additional-tools"></a><span data-ttu-id="23fcd-117">Дополнительные средства</span><span class="sxs-lookup"><span data-stu-id="23fcd-117">Additional tools</span></span>
<span data-ttu-id="23fcd-118">Если вы занимаетесь разработкой решений для Azure, для работы с PowerShell в Visual Studio доступны дополнительные средства и ресурсы.</span><span class="sxs-lookup"><span data-stu-id="23fcd-118">Additional tools and resources for working with PowerShell in Visual Studio for Azure development are available.</span></span> <span data-ttu-id="23fcd-119">Ознакомьтесь с разделом [Средства PowerShell для Visual Studio](http://go.microsoft.com/fwlink/?LinkId=404012).</span><span class="sxs-lookup"><span data-stu-id="23fcd-119">See [PowerShell Tools for Visual Studio](http://go.microsoft.com/fwlink/?LinkId=404012).</span></span>

## <a name="generating-hello-publish-scripts"></a><span data-ttu-id="23fcd-120">Создание hello скриптов публикации</span><span class="sxs-lookup"><span data-stu-id="23fcd-120">Generating hello publish scripts</span></span>
<span data-ttu-id="23fcd-121">Hello можно создать скрипты публикации для виртуальной машины, на котором размещается веб-сайта при создании нового проекта, следуя [эти инструкции](virtual-machines/windows/classic/web-app-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="23fcd-121">You can generate hello publish scripts for a virtual machine that hosts your website when you create a new project by following [these instructions](virtual-machines/windows/classic/web-app-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span> <span data-ttu-id="23fcd-122">Можно также [создать сценарии публикации для веб-приложений в службе приложений Azure](app-service-web/app-service-web-get-started-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="23fcd-122">You can also [generate publish scripts for web apps in Azure App Service](app-service-web/app-service-web-get-started-dotnet.md).</span></span>

## <a name="scripts-that-visual-studio-generates"></a><span data-ttu-id="23fcd-123">Сценарии, создаваемые в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="23fcd-123">Scripts that Visual Studio generates</span></span>
<span data-ttu-id="23fcd-124">Visual Studio создает папку с именем решения на уровне **PublishScripts** , содержащий два файла Windows PowerShell, скрипт публикации для виртуальной машины или веб-сайт и модуль, который содержит функции, которые можно использовать в hello с помощью скрипта.</span><span class="sxs-lookup"><span data-stu-id="23fcd-124">Visual Studio generates a solution-level folder called **PublishScripts** that contains two Windows PowerShell files, a publish script for your virtual machine or website, and a module that contains functions that you can use in hello scripts.</span></span> <span data-ttu-id="23fcd-125">Visual Studio также создает файл в формате JSON hello, с указанием hello hello проекта, в которой выполняется развертывание.</span><span class="sxs-lookup"><span data-stu-id="23fcd-125">Visual Studio also generates a file in hello JSON format that specifies hello details of hello project you are deploying.</span></span>

### <a name="windows-powershell-publish-script"></a><span data-ttu-id="23fcd-126">Сценарий публикации Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="23fcd-126">Windows PowerShell publish script</span></span>
<span data-ttu-id="23fcd-127">Hello скрипт публикации содержит определенные действия для развертывания виртуальной машины или веб-сайт tooa публикации.</span><span class="sxs-lookup"><span data-stu-id="23fcd-127">hello publish script contains specific publish steps for deploying tooa website or virtual machine.</span></span> <span data-ttu-id="23fcd-128">В Visual Studio работает цветовая подсветка синтаксиса Windows PowerShell и доступна справка по функциям.</span><span class="sxs-lookup"><span data-stu-id="23fcd-128">Visual Studio provides syntax coloring for Windows PowerShell development.</span></span> <span data-ttu-id="23fcd-129">Справка по функции hello доступен, и вы можете свободно изменять функции hello в скрипт toosuit hello собственными потребностями.</span><span class="sxs-lookup"><span data-stu-id="23fcd-129">Help for hello functions is available, and you can freely edit hello functions in hello script toosuit your changing requirements.</span></span>

### <a name="windows-powershell-module"></a><span data-ttu-id="23fcd-130">Модуль Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="23fcd-130">Windows PowerShell module</span></span>
<span data-ttu-id="23fcd-131">Windows PowerShell, модуль, который создается Visual Studio содержит функции, которые hello Hello публикации скрипта используется.</span><span class="sxs-lookup"><span data-stu-id="23fcd-131">hello Windows PowerShell module that Visual Studio generates contains functions that hello publish script uses.</span></span> <span data-ttu-id="23fcd-132">Эти функции Azure PowerShell и не предназначен toobe изменены.</span><span class="sxs-lookup"><span data-stu-id="23fcd-132">These are Azure PowerShell functions and are not intended toobe modified.</span></span> <span data-ttu-id="23fcd-133">В разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview) для получения дополнительной информации.</span><span class="sxs-lookup"><span data-stu-id="23fcd-133">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for more information.</span></span>

### <a name="json-configuration-file"></a><span data-ttu-id="23fcd-134">Файл конфигурации в формате JSON</span><span class="sxs-lookup"><span data-stu-id="23fcd-134">JSON configuration file</span></span>
<span data-ttu-id="23fcd-135">Hello JSON-файл создается в hello **конфигурации** папки и содержит данные конфигурации, указывающие точно tooAzure toodeploy какие ресурсы.</span><span class="sxs-lookup"><span data-stu-id="23fcd-135">hello JSON file is created in hello **Configurations** folder and contains configuration data that specifies exactly which resources toodeploy tooAzure.</span></span> <span data-ttu-id="23fcd-136">Hello имя файла "hello", Visual Studio создает проект имя WAWS-dev.json при создании веб-сайта или имя проекта-VM-dev.json при создании виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="23fcd-136">hello name of hello file that Visual Studio generates is project-name-WAWS-dev.json if you created a website, or project name-VM-dev.json if you created a virtual machine.</span></span> <span data-ttu-id="23fcd-137">Ниже приведен пример файла конфигурации JSON, который создается для веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="23fcd-137">Here's an example of a JSON configuration file that's generated when you create a website.</span></span> <span data-ttu-id="23fcd-138">Большинство значений hello говорят сами за себя.</span><span class="sxs-lookup"><span data-stu-id="23fcd-138">Most of hello values are self-explanatory.</span></span> <span data-ttu-id="23fcd-139">Hello имя веб-сайта формируется Azure, поэтому может не совпадать с именем проекта.</span><span class="sxs-lookup"><span data-stu-id="23fcd-139">hello website name is generated by Azure, so it might not match your project name.</span></span>

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
<span data-ttu-id="23fcd-140">При создании виртуальной машины файл конфигурации JSON hello выглядит примерно следующие toohello.</span><span class="sxs-lookup"><span data-stu-id="23fcd-140">When you create a virtual machine, hello JSON configuration file looks similar toohello following.</span></span> <span data-ttu-id="23fcd-141">Обратите внимание, что облачная служба создается как контейнер для hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="23fcd-141">Note that a cloud service is created as a container for hello virtual machine.</span></span> <span data-ttu-id="23fcd-142">Hello виртуальная машина содержит обычные конечные точки hello для веб-доступа по протоколам HTTP и HTTPS, а также конечные точки для веб-развертывания, что позволяет публиковать веб-сайт toohello с локального компьютера, удаленного рабочего стола и Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="23fcd-142">hello virtual machine contains hello usual endpoints for web access through HTTP and HTTPS, as well as endpoints for Web Deploy, which lets you publish toohello website from your local machine, Remote Desktop, and Windows PowerShell.</span></span>

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

<span data-ttu-id="23fcd-143">Можно изменить toochange конфигурации JSON hello, что происходит при запуске hello скрипты публикации.</span><span class="sxs-lookup"><span data-stu-id="23fcd-143">You can edit hello JSON configuration toochange what happens when you run hello publish scripts.</span></span> <span data-ttu-id="23fcd-144">Hello `cloudService` и `virtualMachine` разделы являются обязательными, но можно удалить hello `databases` статьи, если он не нужен.</span><span class="sxs-lookup"><span data-stu-id="23fcd-144">hello `cloudService` and `virtualMachine` sections are required, but you can delete hello `databases` section if you don't need it.</span></span> <span data-ttu-id="23fcd-145">Hello свойства, которые являются пустыми в файле конфигурации по умолчанию hello, создаваемый Visual Studio являются необязательными; те, которые имеют значения в файле конфигурации по умолчанию hello являются обязательными.</span><span class="sxs-lookup"><span data-stu-id="23fcd-145">hello properties that are empty in hello default configuration file that Visual Studio generates are optional; those that have values in hello default configuration file are required.</span></span>

<span data-ttu-id="23fcd-146">Если у вас есть веб-сайт с несколькими средами развертывания (слотами) вместо одного рабочего сайта в Azure, можно включить имя слота hello в имени hello hello веб-сайта в файл конфигурации JSON hello.</span><span class="sxs-lookup"><span data-stu-id="23fcd-146">If you have a website that has multiple deployment environments (known as slots) instead of a single production site in Azure, you can include hello slot name in hello name of hello website in hello JSON configuration file.</span></span> <span data-ttu-id="23fcd-147">Например, если у вас есть веб-сайта, которая называется **mysite** и слот для него с именем **тестирования** hello URI является mysite test.cloudapp.net, но hello toouse правильное имя в файле конфигурации hello — mysite(test) .</span><span class="sxs-lookup"><span data-stu-id="23fcd-147">For example, if you have a website that's named **mysite** and a slot for it named **test** then hello URI is mysite-test.cloudapp.net, but hello correct name toouse in hello configuration file is mysite(test).</span></span> <span data-ttu-id="23fcd-148">Вы можете только этого hello веб-сайт и слоты уже существуют в вашей подписке.</span><span class="sxs-lookup"><span data-stu-id="23fcd-148">You can only do this if hello website and slots already exist in your subscription.</span></span> <span data-ttu-id="23fcd-149">Если они не существуют, создайте hello веб-сайт, запустив сценарий hello без указания слота hello, а затем создайте слот hello в hello [классический портал Azure](http://go.microsoft.com/fwlink/?LinkID=213885), и после этого запустите сценарий hello с именем hello измененного веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="23fcd-149">If they don't exist, create hello website by running hello script without specifying hello slot, then create hello slot in hello [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), and thereafter run hello script with hello modified website name.</span></span> <span data-ttu-id="23fcd-150">Дополнительные сведения о слотах развертывания для веб-приложений см. в статье [Настройка промежуточных сред для веб-приложений в службе приложений Azure](app-service-web/web-sites-staged-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="23fcd-150">For more information about deployment slots for web apps, see [Set up staging environments for web apps in Azure App Service](app-service-web/web-sites-staged-publishing.md).</span></span>

## <a name="how-toorun-hello-publish-scripts"></a><span data-ttu-id="23fcd-151">Как toorun hello публикации скриптов</span><span class="sxs-lookup"><span data-stu-id="23fcd-151">How toorun hello publish scripts</span></span>
<span data-ttu-id="23fcd-152">Если вы еще не запускали скрипт Windows PowerShell, необходимо сначала установить hello выполнения политики tooenable сценариев toorun.</span><span class="sxs-lookup"><span data-stu-id="23fcd-152">If you have never run a Windows PowerShell script before, you must first set hello execution policy tooenable scripts toorun.</span></span> <span data-ttu-id="23fcd-153">Это значение безопасности функция tooprevent пользователям выполнение сценариев Windows PowerShell, если они уязвимы toomalware или вирусов, связанные с выполнением скриптов.</span><span class="sxs-lookup"><span data-stu-id="23fcd-153">This is a security feature tooprevent users from running Windows PowerShell scripts if they're vulnerable toomalware or viruses that involve executing scripts.</span></span>

### <a name="run-hello-script"></a><span data-ttu-id="23fcd-154">Запустите сценарий hello</span><span class="sxs-lookup"><span data-stu-id="23fcd-154">Run hello script</span></span>
1. <span data-ttu-id="23fcd-155">Создайте пакет hello веб-развертывания для проекта.</span><span class="sxs-lookup"><span data-stu-id="23fcd-155">Create hello Web Deploy package for your project.</span></span> <span data-ttu-id="23fcd-156">Пакет веб-развертывания представляет собой сжатый архив (ZIP-файл) с файлами, требуется toocopy tooyour веб-сайта или виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="23fcd-156">A Web Deploy package is a compressed archive (.zip file) that contain files that you want toocopy tooyour website or virtual machine.</span></span> <span data-ttu-id="23fcd-157">В Visual Studio можно создавать пакеты веб-развертывания для любых веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="23fcd-157">You can create Web Deploy packages in Visual Studio for any web application.</span></span>

![Создание пакета веб-развертывания](./media/vs-azure-tools-publishing-using-powershell-scripts/IC767885.png)

<span data-ttu-id="23fcd-159">Дополнительные сведения см. в статье [Как создать пакет веб-развертывания в Visual Studio](https://msdn.microsoft.com/library/dd465323.aspx).</span><span class="sxs-lookup"><span data-stu-id="23fcd-159">For more information, see [How to: Create a Web Deployment Package in Visual Studio](https://msdn.microsoft.com/library/dd465323.aspx).</span></span> <span data-ttu-id="23fcd-160">Также можно автоматизировать создание hello пакета веб-развертывания, как описано в разделе "hello" **Настройка и расширение hello скрипты публикации** далее в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="23fcd-160">You can also automate hello creation of your Web Deploy package, as described in hello section **Customizing and extending hello publish scripts** later in this topic.</span></span>

1. <span data-ttu-id="23fcd-161">В **обозревателе решений**, откройте контекстное меню hello hello скрипта и нажмите кнопку **открыть с помощью PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="23fcd-161">In **Solution Explorer**, open hello context menu for hello script, and then choose **Open with PowerShell ISE**.</span></span>
2. <span data-ttu-id="23fcd-162">Если это hello при первом запуске после выполнения сценариев Windows PowerShell на этом компьютере, откройте окно командной строки с правами администратора и типа hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="23fcd-162">If this is hello first time you've run Windows PowerShell scripts on this computer, open a command prompt window with Administrator privileges and type hello following command:</span></span>

    ```powershell
    Set-ExecutionPolicy RemoteSigned
    ```

3. <span data-ttu-id="23fcd-163">Войти в tooAzure, используя следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="23fcd-163">Sign in tooAzure by using hello following command.</span></span>

    ```powershell
    Add-AzureAccount
    ```

    <span data-ttu-id="23fcd-164">При появлении запроса введите свои имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="23fcd-164">When prompted, supply your username and password.</span></span>

    <span data-ttu-id="23fcd-165">Обратите внимание, что при автоматизации hello скрипта Данный способ указания учетных данных Azure не будет работать.</span><span class="sxs-lookup"><span data-stu-id="23fcd-165">Note that when you automate hello script, this method of providing Azure credentials won't work.</span></span> <span data-ttu-id="23fcd-166">Вместо этого следует использовать учетные данные tooprovide hello .publishsettings файлов.</span><span class="sxs-lookup"><span data-stu-id="23fcd-166">Instead, you should use hello .publishsettings file tooprovide credentials.</span></span> <span data-ttu-id="23fcd-167">Один раз, можно использовать только команды hello **Get-AzurePublishSettingsFile** toodownload hello файл из Azure, а впоследствии используете **команду Import-AzurePublishSettingsFile** файл tooimport hello.</span><span class="sxs-lookup"><span data-stu-id="23fcd-167">One time only, you use hello command **Get-AzurePublishSettingsFile** toodownload hello file from Azure, and thereafter use **Import-AzurePublishSettingsFile** tooimport hello file.</span></span> <span data-ttu-id="23fcd-168">Подробные инструкции см. в разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="23fcd-168">For detailed instructions, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

4. <span data-ttu-id="23fcd-169">(Необязательно) Если требуется, чтобы toocreate Azure использовать ресурсы, такие как hello виртуальной машины, базы данных и веб-сайт, не публикуя веб-приложения hello **Publish-WebApplication.ps1** с hello **-конфигурации** аргумент значение toohello JSON-файл конфигурации.</span><span class="sxs-lookup"><span data-stu-id="23fcd-169">(Optional) If you want toocreate Azure resources such as hello virtual machine, database, and website without publishing your web application, use hello **Publish-WebApplication.ps1** command with hello **-Configuration** argument set toohello JSON configuration file.</span></span> <span data-ttu-id="23fcd-170">Эта командная строка использует toodetermine файл конфигурации JSON hello toocreate какие ресурсы.</span><span class="sxs-lookup"><span data-stu-id="23fcd-170">This command line uses hello JSON configuration file toodetermine which resources toocreate.</span></span> <span data-ttu-id="23fcd-171">Так как оно использует параметры по умолчанию hello для других аргументов командной строки, он создает ресурсы hello, но не публиковать веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="23fcd-171">Because it uses hello default settings for other command-line arguments, it creates hello resources, but doesn't publish your web application.</span></span> <span data-ttu-id="23fcd-172">Hello — параметр Verbose выводит дополнительную информацию о происходящем.</span><span class="sxs-lookup"><span data-stu-id="23fcd-172">hello –Verbose option gives you more information about what's happening.</span></span>

    ```powershell
    Publish-WebApplication.ps1 -Verbose –Configuration C:\Path\WebProject-WAWS-dev.json
    ```

5. <span data-ttu-id="23fcd-173">Используйте hello **Publish-WebApplication.ps1** команды, как показано в одном hello следующие примеры tooinvoke hello скрипт и опубликовать веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="23fcd-173">Use hello **Publish-WebApplication.ps1** command as shown in one of hello following examples tooinvoke hello script and publish your web application.</span></span> <span data-ttu-id="23fcd-174">При необходимости параметры по умолчанию hello toooverride для любого hello других аргументов, например имя подписки hello, публикации, имя пакета, учетных данных виртуальной машины или учетные данные сервера базы данных, можно указать эти параметры.</span><span class="sxs-lookup"><span data-stu-id="23fcd-174">If you need toooverride hello default settings for any of hello other arguments, such as hello subscription name, publish package name, virtual machine credentials, or database server credentials, you can specify those parameters.</span></span> <span data-ttu-id="23fcd-175">Используйте hello **– Verbose** параметр toosee Дополнительные сведения о ходе выполнения hello hello процесс публикации.</span><span class="sxs-lookup"><span data-stu-id="23fcd-175">Use hello **–Verbose** option toosee more information about hello progress of hello publishing process.</span></span>

    ```powershell
    Publish-WebApplication.ps1 –Configuration C:\Path\WebProject-WAWS-dev-json `
    –SubscriptionName Contoso `
    -WebDeployPackage C:\Documents\Azure\ADWebApp.zip `
    -DatabaseServerPassword @{Name="dbServerName";Password="adminPassword"} `
    -Verbose
    ```

    <span data-ttu-id="23fcd-176">При создании виртуальной машины hello команда выглядит как следующий hello.</span><span class="sxs-lookup"><span data-stu-id="23fcd-176">If you're creating a virtual machine, hello command looks like hello following.</span></span> <span data-ttu-id="23fcd-177">В этом примере также показано, как toospecify hello учетные данные для нескольких баз данных.</span><span class="sxs-lookup"><span data-stu-id="23fcd-177">This example also shows how toospecify hello credentials for multiple databases.</span></span> <span data-ttu-id="23fcd-178">Для hello виртуальных машин, создаваемых этими скриптами SSL-сертификат hello не из доверенного корневого центра.</span><span class="sxs-lookup"><span data-stu-id="23fcd-178">For hello virtual machines that these scripts create, hello SSL certificate is not from a trusted root authority.</span></span> <span data-ttu-id="23fcd-179">Поэтому необходимо toouse hello **– AllowUntrusted** параметр.</span><span class="sxs-lookup"><span data-stu-id="23fcd-179">Therefore, you need toouse hello **–AllowUntrusted** option.</span></span>

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

    <span data-ttu-id="23fcd-180">Hello скрипта можно создавать базы данных, но она не создает серверы баз данных.</span><span class="sxs-lookup"><span data-stu-id="23fcd-180">hello script can create databases, but it doesn't create database servers.</span></span> <span data-ttu-id="23fcd-181">Если вы хотите toocreate сервера базы данных, можно использовать hello **New-AzureSqlDatabaseServer** функции hello модуль Azure.</span><span class="sxs-lookup"><span data-stu-id="23fcd-181">If you want toocreate a database server, you can use hello **New-AzureSqlDatabaseServer** function in hello Azure module.</span></span>

## <a name="customizing-and-extending-hello-publish-scripts"></a><span data-ttu-id="23fcd-182">Настройка и расширение hello скриптов публикации</span><span class="sxs-lookup"><span data-stu-id="23fcd-182">Customizing and extending hello publish scripts</span></span>
<span data-ttu-id="23fcd-183">Вы можете настроить hello публикации скрипта и файл конфигурации JSON.</span><span class="sxs-lookup"><span data-stu-id="23fcd-183">You can customize hello publish script and JSON configuration file.</span></span> <span data-ttu-id="23fcd-184">Здравствуйте, функции в модуле Windows PowerShell hello **AzureWebAppPublishModule.psm1** не предполагаемого toobe изменены.</span><span class="sxs-lookup"><span data-stu-id="23fcd-184">hello functions in hello Windows PowerShell module **AzureWebAppPublishModule.psm1** are not intended toobe modified.</span></span> <span data-ttu-id="23fcd-185">Если просто требуется toospecify другую базу данных или изменить некоторые свойства hello hello виртуальной машины, измените файл конфигурации JSON hello.</span><span class="sxs-lookup"><span data-stu-id="23fcd-185">If you just want toospecify a different database or change some of hello properties of hello virtual machine, edit hello JSON configuration file.</span></span> <span data-ttu-id="23fcd-186">Если функции hello tooextend hello tooautomate скрипт построения и тестирования своего проекта, можно реализовать заглушки функций в **Publish-WebApplication.ps1**.</span><span class="sxs-lookup"><span data-stu-id="23fcd-186">If you want tooextend hello functionality of hello script tooautomate building and testing your project, you can implement function stubs in **Publish-WebApplication.ps1**.</span></span>

<span data-ttu-id="23fcd-187">tooautomate при построении проекта, добавьте код, вызывающий MSBuild слишком`New-WebDeployPackage` , как показано в следующем примере кода.</span><span class="sxs-lookup"><span data-stu-id="23fcd-187">tooautomate building your project, add code that calls MSBuild too`New-WebDeployPackage` as shown in this code example.</span></span> <span data-ttu-id="23fcd-188">путь Hello toohello команды MSBuild отличается в зависимости от версии Visual Studio, вы установили hello.</span><span class="sxs-lookup"><span data-stu-id="23fcd-188">hello path toohello MSBuild command is different depending on hello version of Visual Studio you have installed.</span></span> <span data-ttu-id="23fcd-189">tooget hello правильный путь, можно использовать функции hello **Get-MSBuildCmd**, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="23fcd-189">tooget hello correct path, you can use hello function **Get-MSBuildCmd**, as shown in this example.</span></span>

### <a name="tooautomate-building-your-project"></a><span data-ttu-id="23fcd-190">сборка проекта tooautomate</span><span class="sxs-lookup"><span data-stu-id="23fcd-190">tooautomate building your project</span></span>
1. <span data-ttu-id="23fcd-191">Добавить hello `$ProjectFile` параметр в hello глобальный раздел параметров.</span><span class="sxs-lookup"><span data-stu-id="23fcd-191">Add hello `$ProjectFile` parameter in hello global param section.</span></span>

    ```powershell
    [Parameter(Mandatory = $false)]
    [ValidateScript({Test-Path $_ -PathType Leaf})]
    [String]
    $ProjectFile,
    ```

2. <span data-ttu-id="23fcd-192">Скопируйте функции hello `Get-MSBuildCmd` в файл скрипта.</span><span class="sxs-lookup"><span data-stu-id="23fcd-192">Copy hello function `Get-MSBuildCmd` into your script file.</span></span>

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

3. <span data-ttu-id="23fcd-193">Замените `New-WebDeployPackage` с hello следующим кодом и замените заполнители hello в строке, создающей hello `$msbuildCmd`.</span><span class="sxs-lookup"><span data-stu-id="23fcd-193">Replace `New-WebDeployPackage` with hello following code and replace hello placeholders in hello line constructing `$msbuildCmd`.</span></span> <span data-ttu-id="23fcd-194">Этот код предназначен для Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="23fcd-194">This code is for Visual Studio 2015.</span></span> <span data-ttu-id="23fcd-195">Если вы используете Visual Studio 2013, измените hello **VisualStudioVersion** свойство ниже слишком`12.0`.</span><span class="sxs-lookup"><span data-stu-id="23fcd-195">If you're using Visual Studio 2013, change hello **VisualStudioVersion** property below too`12.0`.</span></span>

    ```powershell
    function New-WebDeployPackage
    {
        #Write a function toobuild and package your web application
    ```

    <span data-ttu-id="23fcd-196">toobuild вашего веб-приложения, используйте MsBuild.exe.</span><span class="sxs-lookup"><span data-stu-id="23fcd-196">toobuild your web application, use MsBuild.exe.</span></span> <span data-ttu-id="23fcd-197">Справочник по командной строке MSBuild доступен по адресу [http://go.microsoft.com/fwlink/?LinkId=391339](http://go.microsoft.com/fwlink/?LinkId=391339).</span><span class="sxs-lookup"><span data-stu-id="23fcd-197">For help, see MSBuild Command-Line Reference at: [http://go.microsoft.com/fwlink/?LinkId=391339](http://go.microsoft.com/fwlink/?LinkId=391339)</span></span>

    ```powershell
    Write-VerboseWithTime 'Build-WebDeployPackage: Start'

    $msbuildCmd = '"{0}" "{1}" /T:Rebuild;Package /P:VisualStudioVersion=14.0 /p:OutputPath="{2}\MSBuildOutputPath" /flp:logfile=msbuild.log,v=d' -f (Get-MSBuildCmd), $ProjectFile, $scriptDirectory

    Write-VerboseWithTime ('Build-WebDeployPackage: ' + $msbuildCmd)
    ```

### <a name="start-execution-of-hello-build-command"></a><span data-ttu-id="23fcd-198">Запуск выполнения команды построения hello</span><span class="sxs-lookup"><span data-stu-id="23fcd-198">Start execution of hello build command</span></span>

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

1. <span data-ttu-id="23fcd-199">Вызовите hello `New-WebDeployPackage` функции перед этой строкой: `$Config = Read-ConfigFile $Configuration` для веб-приложений или `$Config = Read-ConfigFile $Configuration -HasWebDeployPackage:([Bool]$WebDeployPackage)` для виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="23fcd-199">Call hello `New-WebDeployPackage` function before this line: `$Config = Read-ConfigFile $Configuration` for web apps or `$Config = Read-ConfigFile $Configuration -HasWebDeployPackage:([Bool]$WebDeployPackage)` for virtual machines.</span></span>

    ```powershell
    if($ProjectFile)
    {
    $WebDeployPackage = New-WebDeployPackage
    }
    ```

2. <span data-ttu-id="23fcd-200">Вызвать hello настроить сценарий из командной строки с помощью передачи hello `$Project` аргументу, как hello следующий пример командной строки.</span><span class="sxs-lookup"><span data-stu-id="23fcd-200">Invoke hello customized script from command line using passing hello `$Project` argument, as in hello following example command line.</span></span>

    ```powershell
    .\Publish-WebApplicationVM.ps1 -Configuration .\Configurations\WebApplication5-VM-dev.json `
    -ProjectFile ..\WebApplication5\WebApplication5.csproj `
    -VMPassword @{Name="VMUser";Password="Test.123"} `
    -AllowUntrusted `
    -Verbose
    ```

    <span data-ttu-id="23fcd-201">Тестирование tooautomate приложения, добавьте код слишком`Test-WebApplication`.</span><span class="sxs-lookup"><span data-stu-id="23fcd-201">tooautomate testing of your application, add code too`Test-WebApplication`.</span></span> <span data-ttu-id="23fcd-202">Быть toouncomment убедиться, что строки hello в **Publish-WebApplication.ps1** где вызываются эти функции.</span><span class="sxs-lookup"><span data-stu-id="23fcd-202">Be sure toouncomment hello lines in **Publish-WebApplication.ps1** where these functions are called.</span></span> <span data-ttu-id="23fcd-203">Если реализация не предоставлена, можно вручную построить проект с помощью Visual Studio и опубликуйте tooAzure toopublish сценария выполнения hello.</span><span class="sxs-lookup"><span data-stu-id="23fcd-203">If you don't provide an implementation, you can manually build your project with Visual Studio, and then run hello publish script toopublish tooAzure.</span></span>

## <a name="publishing-function-summary"></a><span data-ttu-id="23fcd-204">Обзор функций публикации</span><span class="sxs-lookup"><span data-stu-id="23fcd-204">Publishing function summary</span></span>
<span data-ttu-id="23fcd-205">Команда tooget справки для функций, которые можно использовать в командной строке Windows PowerShell hello hello `Get-Help function-name`.</span><span class="sxs-lookup"><span data-stu-id="23fcd-205">tooget help for functions you can use at hello Windows PowerShell command prompt, use hello command `Get-Help function-name`.</span></span> <span data-ttu-id="23fcd-206">Hello справки включает параметр и примеры их использования.</span><span class="sxs-lookup"><span data-stu-id="23fcd-206">hello help includes parameter help and examples.</span></span> <span data-ttu-id="23fcd-207">Hello же справка включена в исходных файлов скриптов hello **AzureWebAppPublishModule.psm1** и **Publish-WebApplication.ps1**.</span><span class="sxs-lookup"><span data-stu-id="23fcd-207">hello same help text is also in hello script source files, **AzureWebAppPublishModule.psm1** and **Publish-WebApplication.ps1**.</span></span> <span data-ttu-id="23fcd-208">Hello скрипт и Справка переведены на языке Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="23fcd-208">hello script and help are localized in your Visual Studio language.</span></span>

<span data-ttu-id="23fcd-209">**AzureWebAppPublishModule**</span><span class="sxs-lookup"><span data-stu-id="23fcd-209">**AzureWebAppPublishModule**</span></span>

| <span data-ttu-id="23fcd-210">Имя функции</span><span class="sxs-lookup"><span data-stu-id="23fcd-210">Function name</span></span> | <span data-ttu-id="23fcd-211">Описание</span><span class="sxs-lookup"><span data-stu-id="23fcd-211">Description</span></span> |
| --- | --- |
| <span data-ttu-id="23fcd-212">Add-AzureSQLDatabase</span><span class="sxs-lookup"><span data-stu-id="23fcd-212">Add-AzureSQLDatabase</span></span> |<span data-ttu-id="23fcd-213">Создает новую базу данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="23fcd-213">Creates a new Azure SQL database.</span></span> |
| <span data-ttu-id="23fcd-214">Add-AzureSQLDatabases</span><span class="sxs-lookup"><span data-stu-id="23fcd-214">Add-AzureSQLDatabases</span></span> |<span data-ttu-id="23fcd-215">Создает базы данных Azure SQL на основе значений hello в файл конфигурации JSON hello, создаваемый Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="23fcd-215">Creates Azure SQL databases from hello values in hello JSON configuration file that Visual Studio generates.</span></span> |
| <span data-ttu-id="23fcd-216">Add-AzureVM</span><span class="sxs-lookup"><span data-stu-id="23fcd-216">Add-AzureVM</span></span> |<span data-ttu-id="23fcd-217">Создает виртуальную машину Azure и возвращает URL-адрес hello hello развертывания ВМ.</span><span class="sxs-lookup"><span data-stu-id="23fcd-217">Creates a Azure virtual machine and returns hello URL of hello deployed VM.</span></span> <span data-ttu-id="23fcd-218">Hello функция настраивает hello предварительные требования, а затем вызывает hello **New-AzureVM** функции toocreate (модуль Azure) новой виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="23fcd-218">hello function sets up hello prerequisites and then calls hello **New-AzureVM** function (Azure module) toocreate a new virtual machine.</span></span> |
| <span data-ttu-id="23fcd-219">Add-AzureVMEndpoints</span><span class="sxs-lookup"><span data-stu-id="23fcd-219">Add-AzureVMEndpoints</span></span> |<span data-ttu-id="23fcd-220">Добавляет новую виртуальную машину tooa входных конечных точек и возвращает hello виртуальной машины с новой конечной точки hello.</span><span class="sxs-lookup"><span data-stu-id="23fcd-220">Adds new input endpoints tooa virtual machine and returns hello virtual machine with hello new endpoint.</span></span> |
| <span data-ttu-id="23fcd-221">Add-AzureVMStorage</span><span class="sxs-lookup"><span data-stu-id="23fcd-221">Add-AzureVMStorage</span></span> |<span data-ttu-id="23fcd-222">Создает новую учетную запись хранилища Azure в текущей подписке hello.</span><span class="sxs-lookup"><span data-stu-id="23fcd-222">Creates a new Azure storage account in hello current subscription.</span></span> <span data-ttu-id="23fcd-223">Имя учетной записи hello Hello начинается с «devtest», и уникальный буквенно-цифровой строки.</span><span class="sxs-lookup"><span data-stu-id="23fcd-223">hello name of hello account begins with "devtest" followed by a unique alphanumeric string.</span></span> <span data-ttu-id="23fcd-224">функция Hello возвращает имя hello hello новой учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="23fcd-224">hello function returns hello name of hello new storage account.</span></span> <span data-ttu-id="23fcd-225">Необходимо указать расположение или территориальную группу для новой учетной записи хранения hello.</span><span class="sxs-lookup"><span data-stu-id="23fcd-225">You must specify either a location or an affinity group for hello new storage account.</span></span> |
| <span data-ttu-id="23fcd-226">Add-AzureWebsite</span><span class="sxs-lookup"><span data-stu-id="23fcd-226">Add-AzureWebsite</span></span> |<span data-ttu-id="23fcd-227">Создает веб-сайт с указанным именем hello и расположением.</span><span class="sxs-lookup"><span data-stu-id="23fcd-227">Creates a website with hello specified name and location.</span></span> <span data-ttu-id="23fcd-228">Эта функция вызывает hello **New-AzureWebsite** функции hello модуль Azure.</span><span class="sxs-lookup"><span data-stu-id="23fcd-228">This function calls hello **New-AzureWebsite** function in hello Azure module.</span></span> <span data-ttu-id="23fcd-229">Если подписка hello не включает веб-сайт с указанным именем hello, эта функция создает веб-сайт hello и возвращает объект веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="23fcd-229">If hello subscription doesn't already include a website with hello specified name, this function creates hello website and returns a website object.</span></span> <span data-ttu-id="23fcd-230">В противном случае она возвращает `$null`.</span><span class="sxs-lookup"><span data-stu-id="23fcd-230">Otherwise, it returns `$null`.</span></span> |
| <span data-ttu-id="23fcd-231">Backup-Subscription</span><span class="sxs-lookup"><span data-stu-id="23fcd-231">Backup-Subscription</span></span> |<span data-ttu-id="23fcd-232">Здравствуйте, сохраняет текущую подписку Azure в hello `$Script:originalSubscription` переменной в области сценариев. Эта функция сохраняет текущую подписку hello Azure (полученную с помощью `Get-AzureSubscription -Current`) и его учетной записи хранилища и hello подписку, которая изменяется этим скриптом (хранится в переменной hello `$UserSpecifiedSubscription`) и ее учетную запись хранения, в области сценариев.</span><span class="sxs-lookup"><span data-stu-id="23fcd-232">Saves hello current Azure subscription in hello `$Script:originalSubscription` variable in script scope.This function saves hello current Azure subscription (as obtained by `Get-AzureSubscription -Current`) and its storage account, and hello subscription that is changed by this script (stored in hello variable `$UserSpecifiedSubscription`) and its storage account, in script scope.</span></span> <span data-ttu-id="23fcd-233">Сохранение значений hello, можно использовать функции, такие как `Restore-Subscription`, toorestore hello исходной текущей подписки и хранения состояние учетной записи toocurrent при изменении текущего состояния hello.</span><span class="sxs-lookup"><span data-stu-id="23fcd-233">By saving hello values, you can use a function, such as `Restore-Subscription`, toorestore hello original current subscription and storage account toocurrent status if hello current status has changed.</span></span> |
| <span data-ttu-id="23fcd-234">Find-AzureVM</span><span class="sxs-lookup"><span data-stu-id="23fcd-234">Find-AzureVM</span></span> |<span data-ttu-id="23fcd-235">Hello возвращает указана виртуальной машины Azure.</span><span class="sxs-lookup"><span data-stu-id="23fcd-235">Gets hello specified Azure virtual machine.</span></span> |
| <span data-ttu-id="23fcd-236">Format-DevTestMessageWithTime</span><span class="sxs-lookup"><span data-stu-id="23fcd-236">Format-DevTestMessageWithTime</span></span> |<span data-ttu-id="23fcd-237">Добавляет приветственное сообщение tooa даты и времени.</span><span class="sxs-lookup"><span data-stu-id="23fcd-237">Prepends hello date and time tooa message.</span></span> <span data-ttu-id="23fcd-238">Эта функция предназначена для сообщений, записываемых toohello потоки Error и Verbose.</span><span class="sxs-lookup"><span data-stu-id="23fcd-238">This function is designed for messages written toohello Error and Verbose streams.</span></span> |
| <span data-ttu-id="23fcd-239">Get-AzureSQLDatabaseConnectionString</span><span class="sxs-lookup"><span data-stu-id="23fcd-239">Get-AzureSQLDatabaseConnectionString</span></span> |<span data-ttu-id="23fcd-240">Выполняет сборку соединения строки tooconnect tooan базы данных Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="23fcd-240">Assembles a connection string tooconnect tooan Azure SQL database.</span></span> |
| <span data-ttu-id="23fcd-241">Get-AzureVMStorage</span><span class="sxs-lookup"><span data-stu-id="23fcd-241">Get-AzureVMStorage</span></span> |<span data-ttu-id="23fcd-242">Возвращает имя hello первой учетной записи хранения с шаблоном имени hello Здравствуйте, «devtest*"(без учета регистра) в hello указанного расположения или территориальной группе. Если hello «devtest*"не соответствует учетной записи хранилища hello расположение или территориальная группа, hello функция пропускает ее.</span><span class="sxs-lookup"><span data-stu-id="23fcd-242">Returns hello name of hello first storage account with hello name pattern "devtest*" (case insensitive) in hello specified location or affinity group. If hello "devtest*" storage account doesn't match hello location or affinity group, hello function ignores it.</span></span> <span data-ttu-id="23fcd-243">Необходимо указать расположение или территориальную группу.</span><span class="sxs-lookup"><span data-stu-id="23fcd-243">You must specify either a location or an affinity group.</span></span> |
| <span data-ttu-id="23fcd-244">Get-MSDeployCmd</span><span class="sxs-lookup"><span data-stu-id="23fcd-244">Get-MSDeployCmd</span></span> |<span data-ttu-id="23fcd-245">Возвращает средство команда hello toorun MsDeploy.exe.</span><span class="sxs-lookup"><span data-stu-id="23fcd-245">Returns a command toorun hello MsDeploy.exe tool.</span></span> |
| <span data-ttu-id="23fcd-246">New-AzureVMEnvironment</span><span class="sxs-lookup"><span data-stu-id="23fcd-246">New-AzureVMEnvironment</span></span> |<span data-ttu-id="23fcd-247">Находит или создает виртуальную машину в подписке hello, соответствующий значениям hello в файле конфигурации JSON hello.</span><span class="sxs-lookup"><span data-stu-id="23fcd-247">Finds or creates a virtual machine in hello subscription that matches hello values in hello JSON configuration file.</span></span> |
| <span data-ttu-id="23fcd-248">Publish-WebPackage</span><span class="sxs-lookup"><span data-stu-id="23fcd-248">Publish-WebPackage</span></span> |<span data-ttu-id="23fcd-249">Использует MsDeploy.exe и откроется веб-публикации пакета. ZIP-файл toodeploy ресурсов tooa веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="23fcd-249">Uses MsDeploy.exe and a web publish package .Zip file toodeploy resources tooa website.</span></span> <span data-ttu-id="23fcd-250">Эта функция не создает никаких выходных данных.</span><span class="sxs-lookup"><span data-stu-id="23fcd-250">This function doesn't generate any output.</span></span> <span data-ttu-id="23fcd-251">В случае вызова tooMSDeploy.exe hello hello функция создает исключение.</span><span class="sxs-lookup"><span data-stu-id="23fcd-251">If hello call tooMSDeploy.exe fails, hello function throws an exception.</span></span> <span data-ttu-id="23fcd-252">tooget более подробные выходные данные, используйте hello **-Verbose** параметр.</span><span class="sxs-lookup"><span data-stu-id="23fcd-252">tooget more detailed output, use hello **-Verbose** option.</span></span> |
| <span data-ttu-id="23fcd-253">Publish-WebPackageToVM</span><span class="sxs-lookup"><span data-stu-id="23fcd-253">Publish-WebPackageToVM</span></span> |<span data-ttu-id="23fcd-254">Проверяет значения параметров hello, а затем вызывает hello **Publish-WebPackage** функции.</span><span class="sxs-lookup"><span data-stu-id="23fcd-254">Verifies hello parameter values, and then calls hello **Publish-WebPackage** function.</span></span> |
| <span data-ttu-id="23fcd-255">Read-ConfigFile</span><span class="sxs-lookup"><span data-stu-id="23fcd-255">Read-ConfigFile</span></span> |<span data-ttu-id="23fcd-256">Проверяет файл конфигурации JSON hello и возвращает хэш-таблицу выбранных значений.</span><span class="sxs-lookup"><span data-stu-id="23fcd-256">Validates hello JSON configuration file and returns a hash table of selected values.</span></span> |
| <span data-ttu-id="23fcd-257">Restore-Subscription</span><span class="sxs-lookup"><span data-stu-id="23fcd-257">Restore-Subscription</span></span> |<span data-ttu-id="23fcd-258">Сбрасывает hello текущей подписки toohello исходной подписки.</span><span class="sxs-lookup"><span data-stu-id="23fcd-258">Resets hello current subscription toohello original subscription.</span></span> |
| <span data-ttu-id="23fcd-259">Test-AzureModule</span><span class="sxs-lookup"><span data-stu-id="23fcd-259">Test-AzureModule</span></span> |<span data-ttu-id="23fcd-260">Возвращает `$true` Если hello установлен модуль Azure версии 0.7.4 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="23fcd-260">Returns `$true` if hello installed Azure module version is 0.7.4 or later.</span></span> <span data-ttu-id="23fcd-261">Возвращает `$false` Если hello модуль не установлен или имеет более раннюю версию.</span><span class="sxs-lookup"><span data-stu-id="23fcd-261">Returns `$false` if hello module isn't installed or is an earlier version.</span></span> <span data-ttu-id="23fcd-262">У этой функции нет параметров.</span><span class="sxs-lookup"><span data-stu-id="23fcd-262">This function has no parameters.</span></span> |
| <span data-ttu-id="23fcd-263">Test-AzureModuleVersion</span><span class="sxs-lookup"><span data-stu-id="23fcd-263">Test-AzureModuleVersion</span></span> |<span data-ttu-id="23fcd-264">Возвращает `$true` Если hello hello модуль Azure версии 0.7.4 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="23fcd-264">Returns `$true` if hello version of hello Azure module is 0.7.4 or later.</span></span> <span data-ttu-id="23fcd-265">Возвращает `$false` Если hello модуль не установлен или имеет более раннюю версию.</span><span class="sxs-lookup"><span data-stu-id="23fcd-265">Returns `$false` if hello module isn't installed or is an earlier version.</span></span> <span data-ttu-id="23fcd-266">У этой функции нет параметров.</span><span class="sxs-lookup"><span data-stu-id="23fcd-266">This function has no parameters.</span></span> |
| <span data-ttu-id="23fcd-267">Test-HttpsUrl</span><span class="sxs-lookup"><span data-stu-id="23fcd-267">Test-HttpsUrl</span></span> |<span data-ttu-id="23fcd-268">Преобразует входной объект в System.Uri URL-адрес tooa hello.</span><span class="sxs-lookup"><span data-stu-id="23fcd-268">Converts hello input URL tooa System.Uri object.</span></span> <span data-ttu-id="23fcd-269">Возвращает `$True` Если hello URL-адрес является абсолютным и использует схему https.</span><span class="sxs-lookup"><span data-stu-id="23fcd-269">Returns `$True` if hello URL is absolute and its scheme is https.</span></span> <span data-ttu-id="23fcd-270">Возвращает `$false` Если hello URL-адрес является относительным, его схема не является HTTPS или hello входная строка не может быть преобразованный tooa URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="23fcd-270">Returns `$false` if hello URL is relative, its scheme isn't HTTPS, or hello input string can't be converted tooa URL.</span></span> |
| <span data-ttu-id="23fcd-271">Test-Member</span><span class="sxs-lookup"><span data-stu-id="23fcd-271">Test-Member</span></span> |<span data-ttu-id="23fcd-272">Возвращает `$true` Если свойство или метод является членом hello объекта.</span><span class="sxs-lookup"><span data-stu-id="23fcd-272">Returns `$true` if a property or method is a member of hello object.</span></span> <span data-ttu-id="23fcd-273">В противном случае возвращается `$false`.</span><span class="sxs-lookup"><span data-stu-id="23fcd-273">Otherwise, returns `$false`.</span></span> |
| <span data-ttu-id="23fcd-274">Write-ErrorWithTime</span><span class="sxs-lookup"><span data-stu-id="23fcd-274">Write-ErrorWithTime</span></span> |<span data-ttu-id="23fcd-275">Записывает сообщение об ошибке с префиксом hello текущее время.</span><span class="sxs-lookup"><span data-stu-id="23fcd-275">Writes an error message prefixed with hello current time.</span></span> <span data-ttu-id="23fcd-276">Эта функция вызывает hello **Format-DevTestMessageWithTime** функция tooprepend hello время перед записью поток сообщений об ошибках toohello сообщение hello.</span><span class="sxs-lookup"><span data-stu-id="23fcd-276">This function calls hello **Format-DevTestMessageWithTime** function tooprepend hello time before writing hello message toohello Error stream.</span></span> |
| <span data-ttu-id="23fcd-277">Write-HostWithTime</span><span class="sxs-lookup"><span data-stu-id="23fcd-277">Write-HostWithTime</span></span> |<span data-ttu-id="23fcd-278">Записывает сообщение toohello основную программу (**Write-Host**) префикс hello текущее время.</span><span class="sxs-lookup"><span data-stu-id="23fcd-278">Writes a message toohello host program (**Write-Host**) prefixed with hello current time.</span></span> <span data-ttu-id="23fcd-279">результат Hello записи toohello основную программу варьируется.</span><span class="sxs-lookup"><span data-stu-id="23fcd-279">hello effect of writing toohello host program varies.</span></span> <span data-ttu-id="23fcd-280">Большинство программ, на которых размещены Windows PowerShell, записывают эти сообщения toostandard выходных данных.</span><span class="sxs-lookup"><span data-stu-id="23fcd-280">Most programs that host Windows PowerShell write these messages toostandard output.</span></span> |
| <span data-ttu-id="23fcd-281">Write-VerboseWithTime</span><span class="sxs-lookup"><span data-stu-id="23fcd-281">Write-VerboseWithTime</span></span> |<span data-ttu-id="23fcd-282">Записывает подробное сообщение с hello префиксом текущее время.</span><span class="sxs-lookup"><span data-stu-id="23fcd-282">Writes a verbose message prefixed with hello current time.</span></span> <span data-ttu-id="23fcd-283">Так как он вызывает **Write-Verbose**, приветственное сообщение отображается только тогда, когда скрипт hello запуске с hello **Verbose** параметр или если hello **VerbosePreference** приоритет — значение слишком**Продолжить**.</span><span class="sxs-lookup"><span data-stu-id="23fcd-283">Because it calls **Write-Verbose**, hello message displays only when hello script runs with hello **Verbose** parameter or when hello **VerbosePreference** preference is set too**Continue**.</span></span> |

<span data-ttu-id="23fcd-284">**Publish-WebApplication**</span><span class="sxs-lookup"><span data-stu-id="23fcd-284">**Publish-WebApplication**</span></span>

| <span data-ttu-id="23fcd-285">Имя функции</span><span class="sxs-lookup"><span data-stu-id="23fcd-285">Function name</span></span> | <span data-ttu-id="23fcd-286">Описание</span><span class="sxs-lookup"><span data-stu-id="23fcd-286">Description</span></span> |
| --- | --- |
| <span data-ttu-id="23fcd-287">New-AzureWebApplicationEnvironment</span><span class="sxs-lookup"><span data-stu-id="23fcd-287">New-AzureWebApplicationEnvironment</span></span> |<span data-ttu-id="23fcd-288">Создает ресурсы Azure, например веб-сайт или виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="23fcd-288">Creates Azure resources, such as a website or virtual machine.</span></span> |
| <span data-ttu-id="23fcd-289">New-WebDeployPackage</span><span class="sxs-lookup"><span data-stu-id="23fcd-289">New-WebDeployPackage</span></span> |<span data-ttu-id="23fcd-290">Эта функция не реализована.</span><span class="sxs-lookup"><span data-stu-id="23fcd-290">This function isn't implemented.</span></span> <span data-ttu-id="23fcd-291">Можно добавить команды в этой функции toobuild проекта.</span><span class="sxs-lookup"><span data-stu-id="23fcd-291">You can add commands in this function toobuild your project.</span></span> |
| <span data-ttu-id="23fcd-292">Publish-AzureWebApplication</span><span class="sxs-lookup"><span data-stu-id="23fcd-292">Publish-AzureWebApplication</span></span> |<span data-ttu-id="23fcd-293">Публикует tooAzure приложения web.</span><span class="sxs-lookup"><span data-stu-id="23fcd-293">Publishes a web application tooAzure.</span></span> |
| <span data-ttu-id="23fcd-294">Publish-WebApplication</span><span class="sxs-lookup"><span data-stu-id="23fcd-294">Publish-WebApplication</span></span> |<span data-ttu-id="23fcd-295">Создает и развертывает веб-приложения, виртуальные машины, базы данных SQL и учетные записи хранения для веб-проекта Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="23fcd-295">Creates and deploys Web Apps, virtual machines, SQL databases, and storage accounts for a Visual Studio web project.</span></span> |
| <span data-ttu-id="23fcd-296">Test-WebApplication</span><span class="sxs-lookup"><span data-stu-id="23fcd-296">Test-WebApplication</span></span> |<span data-ttu-id="23fcd-297">Эта функция не реализована.</span><span class="sxs-lookup"><span data-stu-id="23fcd-297">This function isn't implemented.</span></span> <span data-ttu-id="23fcd-298">Вы можете добавлять команды в этой функции tootest приложения.</span><span class="sxs-lookup"><span data-stu-id="23fcd-298">You can add commands in this function tootest your application.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="23fcd-299">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="23fcd-299">Next steps</span></span>
<span data-ttu-id="23fcd-300">Дополнительные сведения о возможностях сценариев PowerShell, считывая [использование скриптов Windows PowerShell](https://technet.microsoft.com/library/bb978526.aspx) и увидеть другие скрипты Azure PowerShell hello [центра сценариев](https://azure.microsoft.com/documentation/scripts/).</span><span class="sxs-lookup"><span data-stu-id="23fcd-300">Learn more about PowerShell scripting by reading [Scripting with Windows PowerShell](https://technet.microsoft.com/library/bb978526.aspx) and see other Azure PowerShell scripts at hello [Script Center](https://azure.microsoft.com/documentation/scripts/).</span></span>
