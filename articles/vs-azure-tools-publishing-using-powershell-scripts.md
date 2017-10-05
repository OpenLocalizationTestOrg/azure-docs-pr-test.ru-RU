---
title: "Публикация решений в среды разработки и тестирования с помощью сценариев Windows PowerShell | Документация Майкрософт"
description: "Узнайте, как публиковать решения в среды разработки и тестирования с помощью сценариев Windows PowerShell в Visual Studio."
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
ms.openlocfilehash: d4c39eb7a8bc97a980061872ba0f32f375e6976f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="using-windows-powershell-scripts-to-publish-to-dev-and-test-environments"></a><span data-ttu-id="fdde4-103">Использование скриптов Windows PowerShell для публикации в средах разработки и тестирования</span><span class="sxs-lookup"><span data-stu-id="fdde4-103">Using Windows PowerShell scripts to publish to dev and test environments</span></span>
<span data-ttu-id="fdde4-104">При создании веб-приложения в Visual Studio вы можете создать сценарий Windows PowerShell, который позволит автоматизировать публикацию решения на виртуальной машине или веб-сайте (как веб-приложения в службе приложений Azure).</span><span class="sxs-lookup"><span data-stu-id="fdde4-104">When you create a web application in Visual Studio, you can generate a Windows PowerShell script that you can use later to automate the publishing of your website to Azure as a Web App in Azure App Service or a virtual machine.</span></span> <span data-ttu-id="fdde4-105">В редакторе Visual Studio этот сценарий можно изменить и расширить в соответствии со своими потребностями или интегрировать его в существующие сценарии сборки, тестирования и публикации.</span><span class="sxs-lookup"><span data-stu-id="fdde4-105">You can edit and extend the Windows PowerShell script in the Visual Studio editor to suit your requirements, or integrate the script with existing build, test, and publishing scripts.</span></span>

<span data-ttu-id="fdde4-106">С помощью этих сценариев вы можете подготавливать временные пользовательские версии сайта. Эти версии также называют средами разработки и тестирования.</span><span class="sxs-lookup"><span data-stu-id="fdde4-106">Using these scripts, you can provision customized versions (also known as dev and test environments) of your site for temporary use.</span></span> <span data-ttu-id="fdde4-107">Например, на виртуальной машине Azure или в промежуточном слоте веб-сайта можно настроить определенную версию веб-сайта и использовать ее для проведения различных тестов, воспроизведения ошибки, проверки исправления ошибки или исследования предлагаемого изменения. Вы также можете создать специальную среду для демонстраций или презентаций.</span><span class="sxs-lookup"><span data-stu-id="fdde4-107">For example, you might set up a particular version of your website on an Azure virtual machine or on the staging slot on a website to run a test suite, reproduce a bug, test a bug fix, trial a proposed change, or set up a custom environment for a demo or presentation.</span></span> <span data-ttu-id="fdde4-108">Создав сценарий публикации проекта, вы можете с его помощью воссоздавать идентичные среды или использовать его в своей сборке веб-приложения для создания отдельной среды тестирования.</span><span class="sxs-lookup"><span data-stu-id="fdde4-108">After you've created a script that publishes your project, you can recreate identical environments by re-running the script as needed, or run the script with your own build of your web application to create a custom environment for testing.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="fdde4-109">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="fdde4-109">What you need</span></span>
* <span data-ttu-id="fdde4-110">Пакет Azure SDK, начиная с версии 2.3.</span><span class="sxs-lookup"><span data-stu-id="fdde4-110">Azure SDK 2.3 or later.</span></span> <span data-ttu-id="fdde4-111">Дополнительные сведения см. на странице [скачиваемых файлов для Visual Studio](http://go.microsoft.com/fwlink/?LinkID=624384).</span><span class="sxs-lookup"><span data-stu-id="fdde4-111">See [Visual Studio Downloads](http://go.microsoft.com/fwlink/?LinkID=624384) for more information.</span></span>

<span data-ttu-id="fdde4-112">Пакет Azure SDK не нужен для создания сценариев для веб-проектов.</span><span class="sxs-lookup"><span data-stu-id="fdde4-112">You do not need the Azure SDK to generate the scripts for web projects.</span></span> <span data-ttu-id="fdde4-113">Он предназначен для веб-проектов, а не веб-ролей облачных служб.</span><span class="sxs-lookup"><span data-stu-id="fdde4-113">This feature is for web projects, not web roles in cloud services.</span></span>

* <span data-ttu-id="fdde4-114">Azure PowerShell, начиная с версии 0.7.4.</span><span class="sxs-lookup"><span data-stu-id="fdde4-114">Azure PowerShell 0.7.4 or later.</span></span> <span data-ttu-id="fdde4-115">Дополнительные сведения см. в статье [Как установить и настроить Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="fdde4-115">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for more information.</span></span>
* <span data-ttu-id="fdde4-116">[Windows PowerShell](http://go.microsoft.com/?linkid=9811175) , начиная с версии 3.0.</span><span class="sxs-lookup"><span data-stu-id="fdde4-116">[Windows PowerShell 3.0](http://go.microsoft.com/?linkid=9811175) or later.</span></span>

## <a name="additional-tools"></a><span data-ttu-id="fdde4-117">Дополнительные средства</span><span class="sxs-lookup"><span data-stu-id="fdde4-117">Additional tools</span></span>
<span data-ttu-id="fdde4-118">Если вы занимаетесь разработкой решений для Azure, для работы с PowerShell в Visual Studio доступны дополнительные средства и ресурсы.</span><span class="sxs-lookup"><span data-stu-id="fdde4-118">Additional tools and resources for working with PowerShell in Visual Studio for Azure development are available.</span></span> <span data-ttu-id="fdde4-119">Ознакомьтесь с разделом [Средства PowerShell для Visual Studio](http://go.microsoft.com/fwlink/?LinkId=404012).</span><span class="sxs-lookup"><span data-stu-id="fdde4-119">See [PowerShell Tools for Visual Studio](http://go.microsoft.com/fwlink/?LinkId=404012).</span></span>

## <a name="generating-the-publish-scripts"></a><span data-ttu-id="fdde4-120">Создание сценариев публикации</span><span class="sxs-lookup"><span data-stu-id="fdde4-120">Generating the publish scripts</span></span>
<span data-ttu-id="fdde4-121">Чтобы создать сценарии публикации для виртуальной машины, на которой будет размещен веб-сайт, при создании проекта воспользуйтесь [этими инструкциями](virtual-machines/windows/classic/web-app-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fdde4-121">You can generate the publish scripts for a virtual machine that hosts your website when you create a new project by following [these instructions](virtual-machines/windows/classic/web-app-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span> <span data-ttu-id="fdde4-122">Можно также [создать сценарии публикации для веб-приложений в службе приложений Azure](app-service-web/app-service-web-get-started-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="fdde4-122">You can also [generate publish scripts for web apps in Azure App Service](app-service-web/app-service-web-get-started-dotnet.md).</span></span>

## <a name="scripts-that-visual-studio-generates"></a><span data-ttu-id="fdde4-123">Сценарии, создаваемые в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="fdde4-123">Scripts that Visual Studio generates</span></span>
<span data-ttu-id="fdde4-124">Visual Studio создает в решении папку **PublishScripts** , в которой хранятся два файла Windows PowerShell: сценарий публикации для виртуальной машины или веб-сайта и модуль с функциями, которые можно использовать в сценариях.</span><span class="sxs-lookup"><span data-stu-id="fdde4-124">Visual Studio generates a solution-level folder called **PublishScripts** that contains two Windows PowerShell files, a publish script for your virtual machine or website, and a module that contains functions that you can use in the scripts.</span></span> <span data-ttu-id="fdde4-125">Visual Studio также создает файл в формате JSON, в котором хранятся сведения о развертываемом проекте.</span><span class="sxs-lookup"><span data-stu-id="fdde4-125">Visual Studio also generates a file in the JSON format that specifies the details of the project you are deploying.</span></span>

### <a name="windows-powershell-publish-script"></a><span data-ttu-id="fdde4-126">Сценарий публикации Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="fdde4-126">Windows PowerShell publish script</span></span>
<span data-ttu-id="fdde4-127">Сценарий публикации содержит действия по развертыванию решения на веб-сайте или виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="fdde4-127">The publish script contains specific publish steps for deploying to a website or virtual machine.</span></span> <span data-ttu-id="fdde4-128">В Visual Studio работает цветовая подсветка синтаксиса Windows PowerShell и доступна справка по функциям.</span><span class="sxs-lookup"><span data-stu-id="fdde4-128">Visual Studio provides syntax coloring for Windows PowerShell development.</span></span> <span data-ttu-id="fdde4-129">Кроме того, вы можете свободно изменять функции сценария в соответствии со своими потребностями.</span><span class="sxs-lookup"><span data-stu-id="fdde4-129">Help for the functions is available, and you can freely edit the functions in the script to suit your changing requirements.</span></span>

### <a name="windows-powershell-module"></a><span data-ttu-id="fdde4-130">Модуль Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="fdde4-130">Windows PowerShell module</span></span>
<span data-ttu-id="fdde4-131">Создаваемый в Visual Studio модуль Windows PowerShell содержит функции, которые используются в сценарии публикации.</span><span class="sxs-lookup"><span data-stu-id="fdde4-131">The Windows PowerShell module that Visual Studio generates contains functions that the publish script uses.</span></span> <span data-ttu-id="fdde4-132">Это функции Azure PowerShell. Их не нужно изменять.</span><span class="sxs-lookup"><span data-stu-id="fdde4-132">These are Azure PowerShell functions and are not intended to be modified.</span></span> <span data-ttu-id="fdde4-133">Дополнительные сведения см. в статье [Как установить и настроить Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="fdde4-133">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for more information.</span></span>

### <a name="json-configuration-file"></a><span data-ttu-id="fdde4-134">Файл конфигурации в формате JSON</span><span class="sxs-lookup"><span data-stu-id="fdde4-134">JSON configuration file</span></span>
<span data-ttu-id="fdde4-135">JSON-файл создается в папке **Конфигурации**. Он содержит данные конфигурации, указывающие, какие именно ресурсы нужно развернуть в Azure.</span><span class="sxs-lookup"><span data-stu-id="fdde4-135">The JSON file is created in the **Configurations** folder and contains configuration data that specifies exactly which resources to deploy to Azure.</span></span> <span data-ttu-id="fdde4-136">Если вы создали веб-сайт, Visual Studio создает этот файл с именем имя_проекта-WAWS-dev.json. Если вы создали виртуальную машину, Visual Studio создает этот файл с именем имя_проекта-VM-dev.json.</span><span class="sxs-lookup"><span data-stu-id="fdde4-136">The name of the file that Visual Studio generates is project-name-WAWS-dev.json if you created a website, or project name-VM-dev.json if you created a virtual machine.</span></span> <span data-ttu-id="fdde4-137">Ниже приведен пример файла конфигурации JSON, который создается для веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="fdde4-137">Here's an example of a JSON configuration file that's generated when you create a website.</span></span> <span data-ttu-id="fdde4-138">Большая часть значений не нуждается в объяснении.</span><span class="sxs-lookup"><span data-stu-id="fdde4-138">Most of the values are self-explanatory.</span></span> <span data-ttu-id="fdde4-139">Имя веб-сайта задает служба Azure, поэтому оно может не совпадать с именем вашего проекта.</span><span class="sxs-lookup"><span data-stu-id="fdde4-139">The website name is generated by Azure, so it might not match your project name.</span></span>

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
<span data-ttu-id="fdde4-140">В случае создания виртуальной машины файл конфигурации JSON выглядит так, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="fdde4-140">When you create a virtual machine, the JSON configuration file looks similar to the following.</span></span> <span data-ttu-id="fdde4-141">Обратите внимание, что для виртуальной машины создается контейнер в виде облачной службы.</span><span class="sxs-lookup"><span data-stu-id="fdde4-141">Note that a cloud service is created as a container for the virtual machine.</span></span> <span data-ttu-id="fdde4-142">Виртуальная машина содержит обычные конечные точки для веб-доступа через HTTP и HTTPS, а также конечные точки для веб-развертывания, что позволяет публиковать решение на веб-сайт с локального компьютера, удаленного рабочего стола или через Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fdde4-142">The virtual machine contains the usual endpoints for web access through HTTP and HTTPS, as well as endpoints for Web Deploy, which lets you publish to the website from your local machine, Remote Desktop, and Windows PowerShell.</span></span>

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

<span data-ttu-id="fdde4-143">Редактируя файл конфигурации JSON, вы можете влиять на результат выполнения сценариев публикации.</span><span class="sxs-lookup"><span data-stu-id="fdde4-143">You can edit the JSON configuration to change what happens when you run the publish scripts.</span></span> <span data-ttu-id="fdde4-144">Разделы `cloudService` и `virtualMachine` обязательны, а вот раздел `databases` можно удалить, если он не нужен.</span><span class="sxs-lookup"><span data-stu-id="fdde4-144">The `cloudService` and `virtualMachine` sections are required, but you can delete the `databases` section if you don't need it.</span></span> <span data-ttu-id="fdde4-145">Пустые свойства в стандартном файле конфигурации, который создается в Visual Studio, можно не использовать. Свойства, которые имеют значения в стандартном файле конфигурации, — обязательные.</span><span class="sxs-lookup"><span data-stu-id="fdde4-145">The properties that are empty in the default configuration file that Visual Studio generates are optional; those that have values in the default configuration file are required.</span></span>

<span data-ttu-id="fdde4-146">Если у вас есть веб-сайт с несколькими средами развертывания (также известны как слоты), вместо рабочего веб-сайта в Azure в файле конфигурации JSON в имени веб-сайта можно указать имя слота.</span><span class="sxs-lookup"><span data-stu-id="fdde4-146">If you have a website that has multiple deployment environments (known as slots) instead of a single production site in Azure, you can include the slot name in the name of the website in the JSON configuration file.</span></span> <span data-ttu-id="fdde4-147">Например, у вас есть веб-сайт с именем **mysite**, а его слот называется **test**. В этом случае универсальный код ресурса (URI) будет mysite-test.cloudapp.net, а в файле конфигурации будет использоваться имя mysite(test).</span><span class="sxs-lookup"><span data-stu-id="fdde4-147">For example, if you have a website that's named **mysite** and a slot for it named **test** then the URI is mysite-test.cloudapp.net, but the correct name to use in the configuration file is mysite(test).</span></span> <span data-ttu-id="fdde4-148">Так можно сделать, только если веб-сайт и слоты уже есть в вашей подписке.</span><span class="sxs-lookup"><span data-stu-id="fdde4-148">You can only do this if the website and slots already exist in your subscription.</span></span> <span data-ttu-id="fdde4-149">Если их еще нет, создайте веб-сайт, запустив сценарий без указания слота, затем создайте слот на [классическом портале Azure](http://go.microsoft.com/fwlink/?LinkID=213885). После этого запустите сценарий с измененным именем веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="fdde4-149">If they don't exist, create the website by running the script without specifying the slot, then create the slot in the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), and thereafter run the script with the modified website name.</span></span> <span data-ttu-id="fdde4-150">Дополнительные сведения о слотах развертывания для веб-приложений см. в статье [Настройка промежуточных сред для веб-приложений в службе приложений Azure](app-service-web/web-sites-staged-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="fdde4-150">For more information about deployment slots for web apps, see [Set up staging environments for web apps in Azure App Service](app-service-web/web-sites-staged-publishing.md).</span></span>

## <a name="how-to-run-the-publish-scripts"></a><span data-ttu-id="fdde4-151">Запуск скриптов публикации</span><span class="sxs-lookup"><span data-stu-id="fdde4-151">How to run the publish scripts</span></span>
<span data-ttu-id="fdde4-152">Если вы раньше не запускали сценарии Windows PowerShell, вам сначала необходимо настроить политику выполнения. Это позволит сценариям выполняться.</span><span class="sxs-lookup"><span data-stu-id="fdde4-152">If you have never run a Windows PowerShell script before, you must first set the execution policy to enable scripts to run.</span></span> <span data-ttu-id="fdde4-153">Такая процедура предусмотрена для того, чтобы защитить пользователей от вредоносных программ и вирусов, которые могут распространяться с помощью выполняемых сценариев, включая сценарии Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fdde4-153">This is a security feature to prevent users from running Windows PowerShell scripts if they're vulnerable to malware or viruses that involve executing scripts.</span></span>

### <a name="run-the-script"></a><span data-ttu-id="fdde4-154">Запуск сценария</span><span class="sxs-lookup"><span data-stu-id="fdde4-154">Run the script</span></span>
1. <span data-ttu-id="fdde4-155">Создайте пакет веб-развертывания для своего проекта.</span><span class="sxs-lookup"><span data-stu-id="fdde4-155">Create the Web Deploy package for your project.</span></span> <span data-ttu-id="fdde4-156">Пакет веб-развертывания — это сжатый файл (ZIP-архив), содержащий файлы, которые нужно скопировать на веб-сайт или виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="fdde4-156">A Web Deploy package is a compressed archive (.zip file) that contain files that you want to copy to your website or virtual machine.</span></span> <span data-ttu-id="fdde4-157">В Visual Studio можно создавать пакеты веб-развертывания для любых веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="fdde4-157">You can create Web Deploy packages in Visual Studio for any web application.</span></span>

![Создание пакета веб-развертывания](./media/vs-azure-tools-publishing-using-powershell-scripts/IC767885.png)

<span data-ttu-id="fdde4-159">Дополнительные сведения см. в статье [Как создать пакет веб-развертывания в Visual Studio](https://msdn.microsoft.com/library/dd465323.aspx).</span><span class="sxs-lookup"><span data-stu-id="fdde4-159">For more information, see [How to: Create a Web Deployment Package in Visual Studio](https://msdn.microsoft.com/library/dd465323.aspx).</span></span> <span data-ttu-id="fdde4-160">Создание пакета веб-развертывания можно автоматизировать. Это описано в разделе **Настройка и расширение сценариев публикации** далее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="fdde4-160">You can also automate the creation of your Web Deploy package, as described in the section **Customizing and extending the publish scripts** later in this topic.</span></span>

1. <span data-ttu-id="fdde4-161">В **обозревателе решений** откройте контекстное меню сценария и выберите **Открыть с помощью PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="fdde4-161">In **Solution Explorer**, open the context menu for the script, and then choose **Open with PowerShell ISE**.</span></span>
2. <span data-ttu-id="fdde4-162">Если вы запускаете сценарии Windows PowerShell на этом компьютере впервые, откройте окно командной строки с правами администратора и введите такую команду:</span><span class="sxs-lookup"><span data-stu-id="fdde4-162">If this is the first time you've run Windows PowerShell scripts on this computer, open a command prompt window with Administrator privileges and type the following command:</span></span>

    ```powershell
    Set-ExecutionPolicy RemoteSigned
    ```

3. <span data-ttu-id="fdde4-163">Войдите в Azure, выполнив такую команду:</span><span class="sxs-lookup"><span data-stu-id="fdde4-163">Sign in to Azure by using the following command.</span></span>

    ```powershell
    Add-AzureAccount
    ```

    <span data-ttu-id="fdde4-164">При появлении запроса введите свои имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="fdde4-164">When prompted, supply your username and password.</span></span>

    <span data-ttu-id="fdde4-165">Обратите внимание, что после автоматизации работы сценария этот способ указания учетных данных Azure не будет работать.</span><span class="sxs-lookup"><span data-stu-id="fdde4-165">Note that when you automate the script, this method of providing Azure credentials won't work.</span></span> <span data-ttu-id="fdde4-166">В таком случае учетные данные нужно указать в файле PUBLISHSETTINGS.</span><span class="sxs-lookup"><span data-stu-id="fdde4-166">Instead, you should use the .publishsettings file to provide credentials.</span></span> <span data-ttu-id="fdde4-167">Один раз скачайте файл из Azure, выполнив команду **Get-AzurePublishSettingsFile**, после чего импортируйте его с помощью команды **Import-AzurePublishSettingsFile**.</span><span class="sxs-lookup"><span data-stu-id="fdde4-167">One time only, you use the command **Get-AzurePublishSettingsFile** to download the file from Azure, and thereafter use **Import-AzurePublishSettingsFile** to import the file.</span></span> <span data-ttu-id="fdde4-168">Подробные инструкции см. в статье [Установка и настройка служб Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="fdde4-168">For detailed instructions, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

4. <span data-ttu-id="fdde4-169">(Этот этап можно пропустить.) Если вы хотите создать ресурсы Azure, такие как виртуальная машина, база данных и веб-сайт, не публикуя свое веб-приложение, выполните команду **Publish-WebApplication.ps1**, указав в качестве значения параметра **-Configuration** ссылку на JSON-файл конфигурации.</span><span class="sxs-lookup"><span data-stu-id="fdde4-169">(Optional) If you want to create Azure resources such as the virtual machine, database, and website without publishing your web application, use the **Publish-WebApplication.ps1** command with the **-Configuration** argument set to the JSON configuration file.</span></span> <span data-ttu-id="fdde4-170">Используя файл конфигурации JSON, эта командная строка определяет, какие именно ресурсы нужно создать.</span><span class="sxs-lookup"><span data-stu-id="fdde4-170">This command line uses the JSON configuration file to determine which resources to create.</span></span> <span data-ttu-id="fdde4-171">Так как для других аргументов командной строки используются параметры по умолчанию, командная строка создает ресурсы, не публикуя веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="fdde4-171">Because it uses the default settings for other command-line arguments, it creates the resources, but doesn't publish your web application.</span></span> <span data-ttu-id="fdde4-172">Параметр -Verbose позволяет получить дополнительные сведения о том, что происходит при выполнении командной строки.</span><span class="sxs-lookup"><span data-stu-id="fdde4-172">The –Verbose option gives you more information about what's happening.</span></span>

    ```powershell
    Publish-WebApplication.ps1 -Verbose –Configuration C:\Path\WebProject-WAWS-dev.json
    ```

5. <span data-ttu-id="fdde4-173">С помощью команды **Publish-WebApplication.ps1** вызовите сценарий и опубликуйте свое веб-приложение (см. пример ниже).</span><span class="sxs-lookup"><span data-stu-id="fdde4-173">Use the **Publish-WebApplication.ps1** command as shown in one of the following examples to invoke the script and publish your web application.</span></span> <span data-ttu-id="fdde4-174">Если вам нужно изменить стандартные параметры других аргументов, например имя подписки, имя публикуемого пакета, учетные данные виртуальной машины или сервера базы данных, укажите эти параметры.</span><span class="sxs-lookup"><span data-stu-id="fdde4-174">If you need to override the default settings for any of the other arguments, such as the subscription name, publish package name, virtual machine credentials, or database server credentials, you can specify those parameters.</span></span> <span data-ttu-id="fdde4-175">Параметр **-Verbose** позволяет получить дополнительные сведения о ходе публикации.</span><span class="sxs-lookup"><span data-stu-id="fdde4-175">Use the **–Verbose** option to see more information about the progress of the publishing process.</span></span>

    ```powershell
    Publish-WebApplication.ps1 –Configuration C:\Path\WebProject-WAWS-dev-json `
    –SubscriptionName Contoso `
    -WebDeployPackage C:\Documents\Azure\ADWebApp.zip `
    -DatabaseServerPassword @{Name="dbServerName";Password="adminPassword"} `
    -Verbose
    ```

    <span data-ttu-id="fdde4-176">Если вы создаете виртуальную машину, команда должна выглядеть так, как показано в примере ниже.</span><span class="sxs-lookup"><span data-stu-id="fdde4-176">If you're creating a virtual machine, the command looks like the following.</span></span> <span data-ttu-id="fdde4-177">В этом примере также показано, как указывать учетные данные для нескольких баз данных.</span><span class="sxs-lookup"><span data-stu-id="fdde4-177">This example also shows how to specify the credentials for multiple databases.</span></span> <span data-ttu-id="fdde4-178">SSL-сертификат виртуальных машин, создаваемых этими сценариями, происходит из ненадежного корневого центра.</span><span class="sxs-lookup"><span data-stu-id="fdde4-178">For the virtual machines that these scripts create, the SSL certificate is not from a trusted root authority.</span></span> <span data-ttu-id="fdde4-179">Поэтому вам нужно использовать параметр **-AllowUntrusted** .</span><span class="sxs-lookup"><span data-stu-id="fdde4-179">Therefore, you need to use the **–AllowUntrusted** option.</span></span>

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

    <span data-ttu-id="fdde4-180">Этот сценарий создает базы данных. Он не может создавать серверы баз данных.</span><span class="sxs-lookup"><span data-stu-id="fdde4-180">The script can create databases, but it doesn't create database servers.</span></span> <span data-ttu-id="fdde4-181">Если вы хотите создать сервер базы данных, используйте функцию **New-AzureSqlDatabaseServer** в модуле Azure.</span><span class="sxs-lookup"><span data-stu-id="fdde4-181">If you want to create a database server, you can use the **New-AzureSqlDatabaseServer** function in the Azure module.</span></span>

## <a name="customizing-and-extending-the-publish-scripts"></a><span data-ttu-id="fdde4-182">Настройка и расширение сценариев публикации</span><span class="sxs-lookup"><span data-stu-id="fdde4-182">Customizing and extending the publish scripts</span></span>
<span data-ttu-id="fdde4-183">Вы можете настраивать сценарии публикации и изменять файл конфигурации JSON.</span><span class="sxs-lookup"><span data-stu-id="fdde4-183">You can customize the publish script and JSON configuration file.</span></span> <span data-ttu-id="fdde4-184">Функции в модуле Windows PowerShell **AzureWebAppPublishModule.psm1** нельзя изменять.</span><span class="sxs-lookup"><span data-stu-id="fdde4-184">The functions in the Windows PowerShell module **AzureWebAppPublishModule.psm1** are not intended to be modified.</span></span> <span data-ttu-id="fdde4-185">Чтобы выбрать другую базу данных или изменить некоторые свойства виртуальной машины, внесите необходимые изменения в файл конфигурации JSON.</span><span class="sxs-lookup"><span data-stu-id="fdde4-185">If you just want to specify a different database or change some of the properties of the virtual machine, edit the JSON configuration file.</span></span> <span data-ttu-id="fdde4-186">Если вы хотите расширить функциональность сценария и автоматизировать сборку и тестирование проекта, добавьте заготовки функций в файл **Publish-WebApplication.ps1**.</span><span class="sxs-lookup"><span data-stu-id="fdde4-186">If you want to extend the functionality of the script to automate building and testing your project, you can implement function stubs in **Publish-WebApplication.ps1**.</span></span>

<span data-ttu-id="fdde4-187">Чтобы автоматизировать сборку проекта, добавьте код, вызывающий функцию MSBuild `New-WebDeployPackage` (см. пример кода ниже).</span><span class="sxs-lookup"><span data-stu-id="fdde4-187">To automate building your project, add code that calls MSBuild to `New-WebDeployPackage` as shown in this code example.</span></span> <span data-ttu-id="fdde4-188">Путь к команде MSBuild зависит от установленной версии Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fdde4-188">The path to the MSBuild command is different depending on the version of Visual Studio you have installed.</span></span> <span data-ttu-id="fdde4-189">Получить правильный путь можно с помощью функции **Get-MSBuildCmd** (см. пример ниже).</span><span class="sxs-lookup"><span data-stu-id="fdde4-189">To get the correct path, you can use the function **Get-MSBuildCmd**, as shown in this example.</span></span>

### <a name="to-automate-building-your-project"></a><span data-ttu-id="fdde4-190">Автоматизация сборки проекта</span><span class="sxs-lookup"><span data-stu-id="fdde4-190">To automate building your project</span></span>
1. <span data-ttu-id="fdde4-191">Добавьте параметр `$ProjectFile` в раздел глобальных параметров.</span><span class="sxs-lookup"><span data-stu-id="fdde4-191">Add the `$ProjectFile` parameter in the global param section.</span></span>

    ```powershell
    [Parameter(Mandatory = $false)]
    [ValidateScript({Test-Path $_ -PathType Leaf})]
    [String]
    $ProjectFile,
    ```

2. <span data-ttu-id="fdde4-192">Скопируйте функцию `Get-MSBuildCmd` в файл сценария.</span><span class="sxs-lookup"><span data-stu-id="fdde4-192">Copy the function `Get-MSBuildCmd` into your script file.</span></span>

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

3. <span data-ttu-id="fdde4-193">Замените `New-WebDeployPackage` следующим кодом и замените заполнители в строке `$msbuildCmd`.</span><span class="sxs-lookup"><span data-stu-id="fdde4-193">Replace `New-WebDeployPackage` with the following code and replace the placeholders in the line constructing `$msbuildCmd`.</span></span> <span data-ttu-id="fdde4-194">Этот код предназначен для Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="fdde4-194">This code is for Visual Studio 2015.</span></span> <span data-ttu-id="fdde4-195">Если вы используете Visual Studio 2013, измените значение свойства **VisualStudioVersion** значением `12.0`.</span><span class="sxs-lookup"><span data-stu-id="fdde4-195">If you're using Visual Studio 2013, change the **VisualStudioVersion** property below to `12.0`.</span></span>

    ```powershell
    function New-WebDeployPackage
    {
        #Write a function to build and package your web application
    ```

    <span data-ttu-id="fdde4-196">Для создания веб-приложения используйте файл MsBuild.exe.</span><span class="sxs-lookup"><span data-stu-id="fdde4-196">To build your web application, use MsBuild.exe.</span></span> <span data-ttu-id="fdde4-197">Справочник по командной строке MSBuild доступен по адресу [http://go.microsoft.com/fwlink/?LinkId=391339](http://go.microsoft.com/fwlink/?LinkId=391339).</span><span class="sxs-lookup"><span data-stu-id="fdde4-197">For help, see MSBuild Command-Line Reference at: [http://go.microsoft.com/fwlink/?LinkId=391339](http://go.microsoft.com/fwlink/?LinkId=391339)</span></span>

    ```powershell
    Write-VerboseWithTime 'Build-WebDeployPackage: Start'

    $msbuildCmd = '"{0}" "{1}" /T:Rebuild;Package /P:VisualStudioVersion=14.0 /p:OutputPath="{2}\MSBuildOutputPath" /flp:logfile=msbuild.log,v=d' -f (Get-MSBuildCmd), $ProjectFile, $scriptDirectory

    Write-VerboseWithTime ('Build-WebDeployPackage: ' + $msbuildCmd)
    ```

### <a name="start-execution-of-the-build-command"></a><span data-ttu-id="fdde4-198">Запуск команды сборки</span><span class="sxs-lookup"><span data-stu-id="fdde4-198">Start execution of the build command</span></span>

```powershell
$job = Start-Process cmd.exe -ArgumentList('/C "' + $msbuildCmd + '"') -WindowStyle Normal -Wait -PassThru

if ($job.ExitCode -ne 0) {
    throw('MsBuild exited with an error. ExitCode:' + $job.ExitCode)
}

#Obtain the project name
$projectName = (Get-Item $ProjectFile).BaseName

#Construct the path to web deploy zip package
$DeployPackageDir =  '.\MSBuildOutputPath\_PublishedWebsites\{0}_Package\{0}.zip' -f $projectName

#Get the full path for the web deploy zip package. This is required for MSDeploy to work
$WebDeployPackage = Resolve-Path –LiteralPath $DeployPackageDir

Write-VerboseWithTime 'Build-WebDeployPackage: End'

return $WebDeployPackage
}
```

1. <span data-ttu-id="fdde4-199">Вызовите функцию `New-WebDeployPackage` перед строкой `$Config = Read-ConfigFile $Configuration` (для веб-приложений) или `$Config = Read-ConfigFile $Configuration -HasWebDeployPackage:([Bool]$WebDeployPackage)` (для виртуальных машин).</span><span class="sxs-lookup"><span data-stu-id="fdde4-199">Call the `New-WebDeployPackage` function before this line: `$Config = Read-ConfigFile $Configuration` for web apps or `$Config = Read-ConfigFile $Configuration -HasWebDeployPackage:([Bool]$WebDeployPackage)` for virtual machines.</span></span>

    ```powershell
    if($ProjectFile)
    {
    $WebDeployPackage = New-WebDeployPackage
    }
    ```

2. <span data-ttu-id="fdde4-200">Вызовите настроенный сценарий из командной строки, передав аргумент `$Project`, как показано в следующем примере ниже.</span><span class="sxs-lookup"><span data-stu-id="fdde4-200">Invoke the customized script from command line using passing the `$Project` argument, as in the following example command line.</span></span>

    ```powershell
    .\Publish-WebApplicationVM.ps1 -Configuration .\Configurations\WebApplication5-VM-dev.json `
    -ProjectFile ..\WebApplication5\WebApplication5.csproj `
    -VMPassword @{Name="VMUser";Password="Test.123"} `
    -AllowUntrusted `
    -Verbose
    ```

    <span data-ttu-id="fdde4-201">Чтобы автоматизировать тестирование приложения, добавьте код в `Test-WebApplication`.</span><span class="sxs-lookup"><span data-stu-id="fdde4-201">To automate testing of your application, add code to `Test-WebApplication`.</span></span> <span data-ttu-id="fdde4-202">Обязательно раскомментируйте строки в файле **Publish-WebApplication.ps1** , в которых вызываются эти функции.</span><span class="sxs-lookup"><span data-stu-id="fdde4-202">Be sure to uncomment the lines in **Publish-WebApplication.ps1** where these functions are called.</span></span> <span data-ttu-id="fdde4-203">Если реализация не указана, проект можно вручную собрать в Visual Studio и опубликовать его в Azure с помощью сценария публикации.</span><span class="sxs-lookup"><span data-stu-id="fdde4-203">If you don't provide an implementation, you can manually build your project with Visual Studio, and then run the publish script to publish to Azure.</span></span>

## <a name="publishing-function-summary"></a><span data-ttu-id="fdde4-204">Обзор функций публикации</span><span class="sxs-lookup"><span data-stu-id="fdde4-204">Publishing function summary</span></span>
<span data-ttu-id="fdde4-205">Чтобы получить справку по функциям, выполните в командной строке Windows PowerShell команду `Get-Help function-name`.</span><span class="sxs-lookup"><span data-stu-id="fdde4-205">To get help for functions you can use at the Windows PowerShell command prompt, use the command `Get-Help function-name`.</span></span> <span data-ttu-id="fdde4-206">Справочная информация содержит описание параметров и примеры их использования.</span><span class="sxs-lookup"><span data-stu-id="fdde4-206">The help includes parameter help and examples.</span></span> <span data-ttu-id="fdde4-207">Та же справочная информация приведена в исходных файлах сценариев: **AzureWebAppPublishModule.psm1** и **Publish-WebApplication.ps1**.</span><span class="sxs-lookup"><span data-stu-id="fdde4-207">The same help text is also in the script source files, **AzureWebAppPublishModule.psm1** and **Publish-WebApplication.ps1**.</span></span> <span data-ttu-id="fdde4-208">Сценарий и справка переведены на язык интерфейса Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fdde4-208">The script and help are localized in your Visual Studio language.</span></span>

<span data-ttu-id="fdde4-209">**AzureWebAppPublishModule**</span><span class="sxs-lookup"><span data-stu-id="fdde4-209">**AzureWebAppPublishModule**</span></span>

| <span data-ttu-id="fdde4-210">Имя функции</span><span class="sxs-lookup"><span data-stu-id="fdde4-210">Function name</span></span> | <span data-ttu-id="fdde4-211">Описание</span><span class="sxs-lookup"><span data-stu-id="fdde4-211">Description</span></span> |
| --- | --- |
| <span data-ttu-id="fdde4-212">Add-AzureSQLDatabase</span><span class="sxs-lookup"><span data-stu-id="fdde4-212">Add-AzureSQLDatabase</span></span> |<span data-ttu-id="fdde4-213">Создает новую базу данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="fdde4-213">Creates a new Azure SQL database.</span></span> |
| <span data-ttu-id="fdde4-214">Add-AzureSQLDatabases</span><span class="sxs-lookup"><span data-stu-id="fdde4-214">Add-AzureSQLDatabases</span></span> |<span data-ttu-id="fdde4-215">Создает базы данных SQL Azure на основе значений в файле конфигурации JSON, который создается в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fdde4-215">Creates Azure SQL databases from the values in the JSON configuration file that Visual Studio generates.</span></span> |
| <span data-ttu-id="fdde4-216">Add-AzureVM</span><span class="sxs-lookup"><span data-stu-id="fdde4-216">Add-AzureVM</span></span> |<span data-ttu-id="fdde4-217">Создает виртуальную машину Azure и возвращает URL-адрес развернутой виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="fdde4-217">Creates a Azure virtual machine and returns the URL of the deployed VM.</span></span> <span data-ttu-id="fdde4-218">Функция настраивает обязательные компоненты и затем вызывает функцию **New-AzureVM** (в модуле Azure), которая создает виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="fdde4-218">The function sets up the prerequisites and then calls the **New-AzureVM** function (Azure module) to create a new virtual machine.</span></span> |
| <span data-ttu-id="fdde4-219">Add-AzureVMEndpoints</span><span class="sxs-lookup"><span data-stu-id="fdde4-219">Add-AzureVMEndpoints</span></span> |<span data-ttu-id="fdde4-220">Добавляет новые входные конечные точки для виртуальной машины и возвращает виртуальную машину с новой конечной точкой.</span><span class="sxs-lookup"><span data-stu-id="fdde4-220">Adds new input endpoints to a virtual machine and returns the virtual machine with the new endpoint.</span></span> |
| <span data-ttu-id="fdde4-221">Add-AzureVMStorage</span><span class="sxs-lookup"><span data-stu-id="fdde4-221">Add-AzureVMStorage</span></span> |<span data-ttu-id="fdde4-222">Создает в текущей подписке новую учетную запись хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="fdde4-222">Creates a new Azure storage account in the current subscription.</span></span> <span data-ttu-id="fdde4-223">Имя учетной записи начинается с devtest, после чего следует уникальная строка из букв и цифр.</span><span class="sxs-lookup"><span data-stu-id="fdde4-223">The name of the account begins with "devtest" followed by a unique alphanumeric string.</span></span> <span data-ttu-id="fdde4-224">Функция возвращает имя новой учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="fdde4-224">The function returns the name of the new storage account.</span></span> <span data-ttu-id="fdde4-225">Для новой учетной записи хранения необходимо указать расположение или территориальную группу.</span><span class="sxs-lookup"><span data-stu-id="fdde4-225">You must specify either a location or an affinity group for the new storage account.</span></span> |
| <span data-ttu-id="fdde4-226">Add-AzureWebsite</span><span class="sxs-lookup"><span data-stu-id="fdde4-226">Add-AzureWebsite</span></span> |<span data-ttu-id="fdde4-227">Создает веб-сайт с указанными именем и расположением.</span><span class="sxs-lookup"><span data-stu-id="fdde4-227">Creates a website with the specified name and location.</span></span> <span data-ttu-id="fdde4-228">Эта функция вызывает функцию **New-AzureWebsite** в модуле Azure.</span><span class="sxs-lookup"><span data-stu-id="fdde4-228">This function calls the **New-AzureWebsite** function in the Azure module.</span></span> <span data-ttu-id="fdde4-229">Если в подписке еще нет веб-сайта с указанным именем, функция создает его и возвращает объект веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="fdde4-229">If the subscription doesn't already include a website with the specified name, this function creates the website and returns a website object.</span></span> <span data-ttu-id="fdde4-230">В противном случае она возвращает `$null`.</span><span class="sxs-lookup"><span data-stu-id="fdde4-230">Otherwise, it returns `$null`.</span></span> |
| <span data-ttu-id="fdde4-231">Backup-Subscription</span><span class="sxs-lookup"><span data-stu-id="fdde4-231">Backup-Subscription</span></span> |<span data-ttu-id="fdde4-232">Сохраняет текущую подписку Azure в переменной `$Script:originalSubscription` в области сценария. Эта функция сохраняет текущую подписку Azure (полученную с помощью команды `Get-AzureSubscription -Current`) и ее учетную запись хранения, а также подписку, которую изменяет этот сценарий (хранится в переменной `$UserSpecifiedSubscription`), и ее учетную запись хранения в области сценария.</span><span class="sxs-lookup"><span data-stu-id="fdde4-232">Saves the current Azure subscription in the `$Script:originalSubscription` variable in script scope.This function saves the current Azure subscription (as obtained by `Get-AzureSubscription -Current`) and its storage account, and the subscription that is changed by this script (stored in the variable `$UserSpecifiedSubscription`) and its storage account, in script scope.</span></span> <span data-ttu-id="fdde4-233">Сохранив эти значения, вы сможете (например, с помощью функции `Restore-Subscription`) восстановить исходное состояние текущей подписки и учетной записи хранения, если оно изменилось.</span><span class="sxs-lookup"><span data-stu-id="fdde4-233">By saving the values, you can use a function, such as `Restore-Subscription`, to restore the original current subscription and storage account to current status if the current status has changed.</span></span> |
| <span data-ttu-id="fdde4-234">Find-AzureVM</span><span class="sxs-lookup"><span data-stu-id="fdde4-234">Find-AzureVM</span></span> |<span data-ttu-id="fdde4-235">Возвращает указанную виртуальную машину Azure.</span><span class="sxs-lookup"><span data-stu-id="fdde4-235">Gets the specified Azure virtual machine.</span></span> |
| <span data-ttu-id="fdde4-236">Format-DevTestMessageWithTime</span><span class="sxs-lookup"><span data-stu-id="fdde4-236">Format-DevTestMessageWithTime</span></span> |<span data-ttu-id="fdde4-237">Добавляет в сообщение дату и время.</span><span class="sxs-lookup"><span data-stu-id="fdde4-237">Prepends the date and time to a message.</span></span> <span data-ttu-id="fdde4-238">Эта функция предназначена для сообщений, которые записываются в потоки Error и Verbose.</span><span class="sxs-lookup"><span data-stu-id="fdde4-238">This function is designed for messages written to the Error and Verbose streams.</span></span> |
| <span data-ttu-id="fdde4-239">Get-AzureSQLDatabaseConnectionString</span><span class="sxs-lookup"><span data-stu-id="fdde4-239">Get-AzureSQLDatabaseConnectionString</span></span> |<span data-ttu-id="fdde4-240">Собирает строку подключения к базе данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="fdde4-240">Assembles a connection string to connect to an Azure SQL database.</span></span> |
| <span data-ttu-id="fdde4-241">Get-AzureVMStorage</span><span class="sxs-lookup"><span data-stu-id="fdde4-241">Get-AzureVMStorage</span></span> |<span data-ttu-id="fdde4-242">Возвращает из указанного расположения или территориальной группы первую учетную запись хранения, в имени которой есть строка devtest *(без учета регистра). Если учетная запись хранения devtest* не соответствует расположению или территориальной группе, функция пропускает ее.</span><span class="sxs-lookup"><span data-stu-id="fdde4-242">Returns the name of the first storage account with the name pattern "devtest*" (case insensitive) in the specified location or affinity group. If the "devtest*" storage account doesn't match the location or affinity group, the function ignores it.</span></span> <span data-ttu-id="fdde4-243">Необходимо указать расположение или территориальную группу.</span><span class="sxs-lookup"><span data-stu-id="fdde4-243">You must specify either a location or an affinity group.</span></span> |
| <span data-ttu-id="fdde4-244">Get-MSDeployCmd</span><span class="sxs-lookup"><span data-stu-id="fdde4-244">Get-MSDeployCmd</span></span> |<span data-ttu-id="fdde4-245">Возвращает команду для запуска средства MsDeploy.exe.</span><span class="sxs-lookup"><span data-stu-id="fdde4-245">Returns a command to run the MsDeploy.exe tool.</span></span> |
| <span data-ttu-id="fdde4-246">New-AzureVMEnvironment</span><span class="sxs-lookup"><span data-stu-id="fdde4-246">New-AzureVMEnvironment</span></span> |<span data-ttu-id="fdde4-247">Находит или создает в подписке виртуальную машину, которая соответствует значениям в файле конфигурации JSON.</span><span class="sxs-lookup"><span data-stu-id="fdde4-247">Finds or creates a virtual machine in the subscription that matches the values in the JSON configuration file.</span></span> |
| <span data-ttu-id="fdde4-248">Publish-WebPackage</span><span class="sxs-lookup"><span data-stu-id="fdde4-248">Publish-WebPackage</span></span> |<span data-ttu-id="fdde4-249">Развертывает ресурсы на веб-сайт с помощью средства MsDeploy.exe и пакета веб-публикации (ZIP-файл).</span><span class="sxs-lookup"><span data-stu-id="fdde4-249">Uses MsDeploy.exe and a web publish package .Zip file to deploy resources to a website.</span></span> <span data-ttu-id="fdde4-250">Эта функция не создает никаких выходных данных.</span><span class="sxs-lookup"><span data-stu-id="fdde4-250">This function doesn't generate any output.</span></span> <span data-ttu-id="fdde4-251">Если вызов MSDeploy.exe завершился ошибкой, функция создает исключение.</span><span class="sxs-lookup"><span data-stu-id="fdde4-251">If the call to MSDeploy.exe fails, the function throws an exception.</span></span> <span data-ttu-id="fdde4-252">Чтобы получить более подробные выходные данные, используйте параметр **-Verbose** .</span><span class="sxs-lookup"><span data-stu-id="fdde4-252">To get more detailed output, use the **-Verbose** option.</span></span> |
| <span data-ttu-id="fdde4-253">Publish-WebPackageToVM</span><span class="sxs-lookup"><span data-stu-id="fdde4-253">Publish-WebPackageToVM</span></span> |<span data-ttu-id="fdde4-254">Проверяет значения параметров, а затем вызывает функцию **Publish-WebPackage** .</span><span class="sxs-lookup"><span data-stu-id="fdde4-254">Verifies the parameter values, and then calls the **Publish-WebPackage** function.</span></span> |
| <span data-ttu-id="fdde4-255">Read-ConfigFile</span><span class="sxs-lookup"><span data-stu-id="fdde4-255">Read-ConfigFile</span></span> |<span data-ttu-id="fdde4-256">Проверяет файл конфигурации JSON и возвращает хэш-таблицу выбранных значений.</span><span class="sxs-lookup"><span data-stu-id="fdde4-256">Validates the JSON configuration file and returns a hash table of selected values.</span></span> |
| <span data-ttu-id="fdde4-257">Restore-Subscription</span><span class="sxs-lookup"><span data-stu-id="fdde4-257">Restore-Subscription</span></span> |<span data-ttu-id="fdde4-258">Восстанавливает исходное состояние подписки.</span><span class="sxs-lookup"><span data-stu-id="fdde4-258">Resets the current subscription to the original subscription.</span></span> |
| <span data-ttu-id="fdde4-259">Test-AzureModule</span><span class="sxs-lookup"><span data-stu-id="fdde4-259">Test-AzureModule</span></span> |<span data-ttu-id="fdde4-260">Возвращает `$true` , если установленный модуль Azure имеет версию 0.7.4 и выше.</span><span class="sxs-lookup"><span data-stu-id="fdde4-260">Returns `$true` if the installed Azure module version is 0.7.4 or later.</span></span> <span data-ttu-id="fdde4-261">Возвращает `$false` , если модуль не установлен или имеет более раннюю версию.</span><span class="sxs-lookup"><span data-stu-id="fdde4-261">Returns `$false` if the module isn't installed or is an earlier version.</span></span> <span data-ttu-id="fdde4-262">У этой функции нет параметров.</span><span class="sxs-lookup"><span data-stu-id="fdde4-262">This function has no parameters.</span></span> |
| <span data-ttu-id="fdde4-263">Test-AzureModuleVersion</span><span class="sxs-lookup"><span data-stu-id="fdde4-263">Test-AzureModuleVersion</span></span> |<span data-ttu-id="fdde4-264">Возвращает `$true` , если модуль Azure имеет версию 0.7.4 и выше.</span><span class="sxs-lookup"><span data-stu-id="fdde4-264">Returns `$true` if the version of the Azure module is 0.7.4 or later.</span></span> <span data-ttu-id="fdde4-265">Возвращает `$false` , если модуль не установлен или имеет более раннюю версию.</span><span class="sxs-lookup"><span data-stu-id="fdde4-265">Returns `$false` if the module isn't installed or is an earlier version.</span></span> <span data-ttu-id="fdde4-266">У этой функции нет параметров.</span><span class="sxs-lookup"><span data-stu-id="fdde4-266">This function has no parameters.</span></span> |
| <span data-ttu-id="fdde4-267">Test-HttpsUrl</span><span class="sxs-lookup"><span data-stu-id="fdde4-267">Test-HttpsUrl</span></span> |<span data-ttu-id="fdde4-268">Преобразует входной URL-адрес в объект System.Uri.</span><span class="sxs-lookup"><span data-stu-id="fdde4-268">Converts the input URL to a System.Uri object.</span></span> <span data-ttu-id="fdde4-269">Возвращает `$True` , если URL-адрес является абсолютным адресом и использует схему HTTPS.</span><span class="sxs-lookup"><span data-stu-id="fdde4-269">Returns `$True` if the URL is absolute and its scheme is https.</span></span> <span data-ttu-id="fdde4-270">Возвращает `$false` , если URL-адрес является относительным, не использует схему HTTPS или входную строку невозможно преобразовать в URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="fdde4-270">Returns `$false` if the URL is relative, its scheme isn't HTTPS, or the input string can't be converted to a URL.</span></span> |
| <span data-ttu-id="fdde4-271">Test-Member</span><span class="sxs-lookup"><span data-stu-id="fdde4-271">Test-Member</span></span> |<span data-ttu-id="fdde4-272">Возвращает `$true` , если свойство или метод является членом объекта.</span><span class="sxs-lookup"><span data-stu-id="fdde4-272">Returns `$true` if a property or method is a member of the object.</span></span> <span data-ttu-id="fdde4-273">В противном случае возвращается `$false`.</span><span class="sxs-lookup"><span data-stu-id="fdde4-273">Otherwise, returns `$false`.</span></span> |
| <span data-ttu-id="fdde4-274">Write-ErrorWithTime</span><span class="sxs-lookup"><span data-stu-id="fdde4-274">Write-ErrorWithTime</span></span> |<span data-ttu-id="fdde4-275">Записывает сообщение об ошибке с текущим временем в префиксе.</span><span class="sxs-lookup"><span data-stu-id="fdde4-275">Writes an error message prefixed with the current time.</span></span> <span data-ttu-id="fdde4-276">Эта функция вызывает функцию **Format-DevTestMessageWithTime** , которая добавляет время перед записью сообщения в поток Error.</span><span class="sxs-lookup"><span data-stu-id="fdde4-276">This function calls the **Format-DevTestMessageWithTime** function to prepend the time before writing the message to the Error stream.</span></span> |
| <span data-ttu-id="fdde4-277">Write-HostWithTime</span><span class="sxs-lookup"><span data-stu-id="fdde4-277">Write-HostWithTime</span></span> |<span data-ttu-id="fdde4-278">Записывает в основную программу (**Write-Host**) сообщение с текущим временем в префиксе.</span><span class="sxs-lookup"><span data-stu-id="fdde4-278">Writes a message to the host program (**Write-Host**) prefixed with the current time.</span></span> <span data-ttu-id="fdde4-279">Результат записи в основную программу варьируется.</span><span class="sxs-lookup"><span data-stu-id="fdde4-279">The effect of writing to the host program varies.</span></span> <span data-ttu-id="fdde4-280">Большинство программ, использующих Windows PowerShell, записывают эти сообщения в стандартный вывод.</span><span class="sxs-lookup"><span data-stu-id="fdde4-280">Most programs that host Windows PowerShell write these messages to standard output.</span></span> |
| <span data-ttu-id="fdde4-281">Write-VerboseWithTime</span><span class="sxs-lookup"><span data-stu-id="fdde4-281">Write-VerboseWithTime</span></span> |<span data-ttu-id="fdde4-282">Записывает подробное сообщение с текущим временем в префиксе.</span><span class="sxs-lookup"><span data-stu-id="fdde4-282">Writes a verbose message prefixed with the current time.</span></span> <span data-ttu-id="fdde4-283">Так как функция вызывает функцию **Write-Verbose**, сообщение появляется, только если сценарий запускается с параметром **-Verbose** или для параметра **VerbosePreference** задано значение **Continue**.</span><span class="sxs-lookup"><span data-stu-id="fdde4-283">Because it calls **Write-Verbose**, the message displays only when the script runs with the **Verbose** parameter or when the **VerbosePreference** preference is set to **Continue**.</span></span> |

<span data-ttu-id="fdde4-284">**Publish-WebApplication**</span><span class="sxs-lookup"><span data-stu-id="fdde4-284">**Publish-WebApplication**</span></span>

| <span data-ttu-id="fdde4-285">Имя функции</span><span class="sxs-lookup"><span data-stu-id="fdde4-285">Function name</span></span> | <span data-ttu-id="fdde4-286">Описание</span><span class="sxs-lookup"><span data-stu-id="fdde4-286">Description</span></span> |
| --- | --- |
| <span data-ttu-id="fdde4-287">New-AzureWebApplicationEnvironment</span><span class="sxs-lookup"><span data-stu-id="fdde4-287">New-AzureWebApplicationEnvironment</span></span> |<span data-ttu-id="fdde4-288">Создает ресурсы Azure, например веб-сайт или виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="fdde4-288">Creates Azure resources, such as a website or virtual machine.</span></span> |
| <span data-ttu-id="fdde4-289">New-WebDeployPackage</span><span class="sxs-lookup"><span data-stu-id="fdde4-289">New-WebDeployPackage</span></span> |<span data-ttu-id="fdde4-290">Эта функция не реализована.</span><span class="sxs-lookup"><span data-stu-id="fdde4-290">This function isn't implemented.</span></span> <span data-ttu-id="fdde4-291">В нее можно добавлять команды для сборки проекта.</span><span class="sxs-lookup"><span data-stu-id="fdde4-291">You can add commands in this function to build your project.</span></span> |
| <span data-ttu-id="fdde4-292">Publish-AzureWebApplication</span><span class="sxs-lookup"><span data-stu-id="fdde4-292">Publish-AzureWebApplication</span></span> |<span data-ttu-id="fdde4-293">Публикует веб-приложение в Azure.</span><span class="sxs-lookup"><span data-stu-id="fdde4-293">Publishes a web application to Azure.</span></span> |
| <span data-ttu-id="fdde4-294">Publish-WebApplication</span><span class="sxs-lookup"><span data-stu-id="fdde4-294">Publish-WebApplication</span></span> |<span data-ttu-id="fdde4-295">Создает и развертывает веб-приложения, виртуальные машины, базы данных SQL и учетные записи хранения для веб-проекта Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fdde4-295">Creates and deploys Web Apps, virtual machines, SQL databases, and storage accounts for a Visual Studio web project.</span></span> |
| <span data-ttu-id="fdde4-296">Test-WebApplication</span><span class="sxs-lookup"><span data-stu-id="fdde4-296">Test-WebApplication</span></span> |<span data-ttu-id="fdde4-297">Эта функция не реализована.</span><span class="sxs-lookup"><span data-stu-id="fdde4-297">This function isn't implemented.</span></span> <span data-ttu-id="fdde4-298">В нее можно добавлять команды для тестирования приложения.</span><span class="sxs-lookup"><span data-stu-id="fdde4-298">You can add commands in this function to test your application.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="fdde4-299">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fdde4-299">Next steps</span></span>
<span data-ttu-id="fdde4-300">Дополнительные сведения о сценариях PowerShell см. в статье [Работа со сценариями в Windows PowerShell](https://technet.microsoft.com/library/bb978526.aspx). Рекомендуем также посетить [центр сценариев](https://azure.microsoft.com/documentation/scripts/) и ознакомиться с другими сценариями Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fdde4-300">Learn more about PowerShell scripting by reading [Scripting with Windows PowerShell](https://technet.microsoft.com/library/bb978526.aspx) and see other Azure PowerShell scripts at the [Script Center](https://azure.microsoft.com/documentation/scripts/).</span></span>
