---
title: "Указание версии Node.js"
description: "Узнайте, как указать версию Node.js, используемую веб-сайтами и облачными службами Azure."
services: 
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: d0e15278-2ab4-4ec8-8256-913839c6d5ef
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: 89627e6a877c9f65a5216c55f58f1c707ea25d44
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="specifying-a-nodejs-version-in-an-azure-application"></a><span data-ttu-id="75c8b-103">Указание версии Node.js в приложении Azure</span><span class="sxs-lookup"><span data-stu-id="75c8b-103">Specifying a Node.js version in an Azure application</span></span>
<span data-ttu-id="75c8b-104">При размещении приложения Node.js может потребоваться, чтобы приложение использовало конкретную версию Node.js.</span><span class="sxs-lookup"><span data-stu-id="75c8b-104">When hosting a Node.js application, you may want to ensure that your application uses a specific version of Node.js.</span></span> <span data-ttu-id="75c8b-105">Существует несколько способов это сделать для приложений, размещенных в Azure.</span><span class="sxs-lookup"><span data-stu-id="75c8b-105">There are several ways to accomplish this for applications hosted on Azure.</span></span>

## <a name="default-versions"></a><span data-ttu-id="75c8b-106">Версии по умолчанию</span><span class="sxs-lookup"><span data-stu-id="75c8b-106">Default versions</span></span>
<span data-ttu-id="75c8b-107">Версии Node.js, предоставляемые Azure, постоянно обновляются.</span><span class="sxs-lookup"><span data-stu-id="75c8b-107">The Node.js versions provided by Azure are constantly updated.</span></span> <span data-ttu-id="75c8b-108">Если не указано иное, будет использоваться версия по умолчанию, которая указана в переменной среды `WEBSITE_NODE_DEFAULT_VERSION` .</span><span class="sxs-lookup"><span data-stu-id="75c8b-108">Unless otherwise specified, the default version that is specified in the `WEBSITE_NODE_DEFAULT_VERSION` environment variable will be used.</span></span> <span data-ttu-id="75c8b-109">Чтобы переопределить это значение по умолчанию, выполните действия, описанные в следующих разделах этой статьи.</span><span class="sxs-lookup"><span data-stu-id="75c8b-109">To override this default value, follow the steps in following sections of this article</span></span>

> [!NOTE]
> <span data-ttu-id="75c8b-110">При первом размещении приложения в облачной службе Azure (веб-роль или рабочая роль), Azure будет пытаться использовать ту же версию Node.js, что установлена в вашей среде разработки, если она совпадает с одной из версий по умолчанию, доступных в Azure.</span><span class="sxs-lookup"><span data-stu-id="75c8b-110">If you are hosting your application in an Azure Cloud Service (web or worker role,) and it is the first time you have deployed the application, Azure will attempt to use the same version of Node.js as you have installed on your development environment if it matches one of the default versions available on Azure.</span></span>
>
>

## <a name="versioning-with-packagejson"></a><span data-ttu-id="75c8b-111">Управление версиями с использованием package.json</span><span class="sxs-lookup"><span data-stu-id="75c8b-111">Versioning with package.json</span></span>
<span data-ttu-id="75c8b-112">Можно указать требуемую версию Node.js, добавив в файл **package.json** следующий текст:</span><span class="sxs-lookup"><span data-stu-id="75c8b-112">You can specify the version of Node.js to be used by adding the following to your **package.json** file:</span></span>

    "engines":{"node":version}

<span data-ttu-id="75c8b-113">Где *версия* указывает на номер конкретной версии, которую нужно использовать.</span><span class="sxs-lookup"><span data-stu-id="75c8b-113">Where *version* is the specific version number to use.</span></span> <span data-ttu-id="75c8b-114">Вы можете задать более сложные условия для версии, например:</span><span class="sxs-lookup"><span data-stu-id="75c8b-114">You can specify more complex conditions for version, such as:</span></span>

    "engines":{"node": "0.6.22 || 0.8.x"}

<span data-ttu-id="75c8b-115">Поскольку 0.6.22 не является одной из версий, доступных в среде размещения, будет использоваться самая новая из доступных версий серии 0.8, то есть 0.8.4.</span><span class="sxs-lookup"><span data-stu-id="75c8b-115">Since 0.6.22 is not one of the versions available in the hosting environment, the highest version of the 0.8 series that is available will be used instead - 0.8.4.</span></span>

## <a name="versioning-websites-with-app-settings"></a><span data-ttu-id="75c8b-116">Управление версиями веб-сайтов с помощью параметров приложения</span><span class="sxs-lookup"><span data-stu-id="75c8b-116">Versioning Websites with App Settings</span></span>
<span data-ttu-id="75c8b-117">При размещении приложения на веб-сайте можно задать переменную среды **WEBSITE_NODE_DEFAULT_VERSION** с нужной версией.</span><span class="sxs-lookup"><span data-stu-id="75c8b-117">If you are hosting the application in a Website, you can set the environment variable **WEBSITE_NODE_DEFAULT_VERSION** to the desired version.</span></span>

## <a name="versioning-cloud-services-with-powershell"></a><span data-ttu-id="75c8b-118">Управление версиями облачных служб с использованием PowerShell</span><span class="sxs-lookup"><span data-stu-id="75c8b-118">Versioning Cloud Services with PowerShell</span></span>
<span data-ttu-id="75c8b-119">В случае размещения приложения в облачной службе и при использовании для развертывания Azure PowerShell, версию Node.js по умолчанию можно переопределить с помощью командлета **Set-AzureServiceProjectRole** .</span><span class="sxs-lookup"><span data-stu-id="75c8b-119">If you are hosting the application in a Cloud Service, and are deploying the application using Azure PowerShell, you can override the default Node.js version by using the **Set-AzureServiceProjectRole** PowerShell cmdlet.</span></span> <span data-ttu-id="75c8b-120">Например:</span><span class="sxs-lookup"><span data-stu-id="75c8b-120">For example:</span></span>

    Set-AzureServiceProjectRole WebRole1 Node 0.8.4

<span data-ttu-id="75c8b-121">Обратите внимание, что в параметрах в инструкции выше учитывается регистр.</span><span class="sxs-lookup"><span data-stu-id="75c8b-121">Note the parameters in the above statement are case-sensitive.</span></span>  <span data-ttu-id="75c8b-122">Можно проверить, выбрана ли правильная версия Node.js, выбрав свойство **engines** в **package.json** вашей роли.</span><span class="sxs-lookup"><span data-stu-id="75c8b-122">You can verify the correct version of Node.js has been selected by checking the **engines** property in your role's **package.json**.</span></span>

<span data-ttu-id="75c8b-123">Можно также использовать **Get-AzureServiceProjectRoleRuntime** для получения списка версий Node.js, доступных для приложений, размещенных в виде облачной службы.</span><span class="sxs-lookup"><span data-stu-id="75c8b-123">You can also use the **Get-AzureServiceProjectRoleRuntime** to retrieve a list of Node.js versions available for applications hosted as a Cloud Service.</span></span>  <span data-ttu-id="75c8b-124">Всегда проверяйте, есть ли версия Node.js, от которой зависит ваш проект, в этом списке.</span><span class="sxs-lookup"><span data-stu-id="75c8b-124">Always verify the version of Node.js your project depends on is in this list.</span></span>

## <a name="using-a-custom-version-with-azure-websites"></a><span data-ttu-id="75c8b-125">Использование настраиваемой версии с веб-сайтами Azure</span><span class="sxs-lookup"><span data-stu-id="75c8b-125">Using a custom version with Azure Websites</span></span>
<span data-ttu-id="75c8b-126">Хотя Azure предоставляет несколько версий Node.js по умолчанию, может потребоваться версия, не доступная по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="75c8b-126">While Azure provides several default versions of Node.js, you may want to use a version that is not provided by default.</span></span> <span data-ttu-id="75c8b-127">Если приложение размещено как веб-сайт Azure, это можно сделать с помощью файла **iisnode.yml** .</span><span class="sxs-lookup"><span data-stu-id="75c8b-127">If your application is hosted as an Azure Website, you can accomplish this by using the **iisnode.yml** file.</span></span> <span data-ttu-id="75c8b-128">Ниже рассмотрен процесс использования настраиваемой версии Node.Js на веб-сайте Azure.</span><span class="sxs-lookup"><span data-stu-id="75c8b-128">The following steps walk through the process of using a custom version of Node.Js with an Azure Website:</span></span>

1. <span data-ttu-id="75c8b-129">Создайте новый каталог, а затем создайте в каталоге файл **server.js** .</span><span class="sxs-lookup"><span data-stu-id="75c8b-129">Create a new directory, and then create a **server.js** file within the directory.</span></span> <span data-ttu-id="75c8b-130">Файл **server.js** должен содержать следующее:</span><span class="sxs-lookup"><span data-stu-id="75c8b-130">The **server.js** file should contain the following:</span></span>

        var http = require('http');
        http.createServer(function(req,res) {
          res.writeHead(200, {'Content-Type': 'text/html'});
          res.end('Hello from Azure running node version: ' + process.version + '</br>');
        }).listen(process.env.PORT || 3000);

    <span data-ttu-id="75c8b-131">Будет показана версия Node.js, используемая на момент просмотра веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="75c8b-131">This will display the Node.js version being used when you browse the website.</span></span>
2. <span data-ttu-id="75c8b-132">Создайте новый веб-сайт и запишите его имя.</span><span class="sxs-lookup"><span data-stu-id="75c8b-132">Create a new Website and note the name of the site.</span></span> <span data-ttu-id="75c8b-133">Например, ниже представлен пример использования [средств командной строки Azure] для создания нового веб-сайта Azure с именем **mywebsite**и последующего включения репозитория Git для веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="75c8b-133">For example, the following uses the [Azure Command-line tools] to create a new Azure Website named **mywebsite**, and then enable a Git repository for the website.</span></span>

        azure site create mywebsite --git
3. <span data-ttu-id="75c8b-134">Создайте каталог под именем **bin**, дочерний по отношению к каталогу, содержащему файл **server.js**.</span><span class="sxs-lookup"><span data-stu-id="75c8b-134">Create a new directory named **bin** as a child of the directory containing the **server.js** file.</span></span>
4. <span data-ttu-id="75c8b-135">Загрузите конкретную версию **node.exe** (версию для Windows), которую нужно использовать с вашим приложением.</span><span class="sxs-lookup"><span data-stu-id="75c8b-135">Download the specific version of **node.exe** (the Windows version) that you wish to use with your application.</span></span> <span data-ttu-id="75c8b-136">Например, в следующем примере используется **curl** для загрузки версии 0.8.1:</span><span class="sxs-lookup"><span data-stu-id="75c8b-136">For example, the following uses **curl** to download version 0.8.1:</span></span>

        curl -O http://nodejs.org/dist/v0.8.1/node.exe

    <span data-ttu-id="75c8b-137">Сохраните файл **node.exe** в ранее созданный каталог **bin**.</span><span class="sxs-lookup"><span data-stu-id="75c8b-137">Save the **node.exe** file into the **bin** folder created previously.</span></span>
5. <span data-ttu-id="75c8b-138">Создайте файл **iisnode.yml** в том же каталоге, что и файл **server.js**, а затем добавьте в файл **iisnode.yml** следующее содержимое:</span><span class="sxs-lookup"><span data-stu-id="75c8b-138">Create an **iisnode.yml** file in the same directory as the **server.js** file, and then add the following content to the **iisnode.yml** file:</span></span>

        nodeProcessCommandLine: "D:\home\site\wwwroot\bin\node.exe"

    <span data-ttu-id="75c8b-139">Этот путь указывает расположение файла **node.exe** в проекте после публикации приложения на веб-сайте Azure.</span><span class="sxs-lookup"><span data-stu-id="75c8b-139">This path is where the **node.exe** file within your project will be located once you have published your application to the Azure Website.</span></span>
6. <span data-ttu-id="75c8b-140">Опубликуйте приложение.</span><span class="sxs-lookup"><span data-stu-id="75c8b-140">Publish your application.</span></span> <span data-ttu-id="75c8b-141">Например, поскольку ранее был создан веб-сайт с помощью параметра --git, следующие команды добавят файлы приложения в локальный репозиторий Git и передадут их в репозиторий веб-сайта:</span><span class="sxs-lookup"><span data-stu-id="75c8b-141">For example, since I created a new website with the --git parameter earlier, the following commands will add the application files to my local Git repository, and then push them to the website repository:</span></span>

        git add .
        git commit -m "testing node v0.8.1"
        git push azure master

    <span data-ttu-id="75c8b-142">После публикации приложения откройте веб-сайт в браузере.</span><span class="sxs-lookup"><span data-stu-id="75c8b-142">After the application has published, open the website in a browser.</span></span> <span data-ttu-id="75c8b-143">Должно появиться сообщение "Hello from Azure running node version: v0.8.1".</span><span class="sxs-lookup"><span data-stu-id="75c8b-143">You should see a message stating "Hello from Azure running node version: v0.8.1".</span></span>

## <a name="next-steps"></a><span data-ttu-id="75c8b-144">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="75c8b-144">Next Steps</span></span>
<span data-ttu-id="75c8b-145">Теперь, когда вы научились устанавливать версии Node.js, используемые приложением, узнайте, как [работать с модулями], [создавать и развертывать веб-сайт Node.js](app-service-web/app-service-web-get-started-nodejs.md) и [использовать средства командной строки Azure для Mac и Linux].</span><span class="sxs-lookup"><span data-stu-id="75c8b-145">Now that you understand how to specify the version of Node.js used by your application, learn how to [work with modules], [build and deploy a Node.js Web Site](app-service-web/app-service-web-get-started-nodejs.md), and [How to use the Azure Command-Line Tools for Mac and Linux].</span></span>

<span data-ttu-id="75c8b-146">Дополнительную информацию см. в [центре разработчиков Node.js](https://azure.microsoft.com/develop/nodejs/).</span><span class="sxs-lookup"><span data-stu-id="75c8b-146">For more information, see the [Node.js Developer Center](https://azure.microsoft.com/develop/nodejs/).</span></span>

<span data-ttu-id="75c8b-147">[использовать средства командной строки Azure для Mac и Linux]:cli-install-nodejs.md</span><span class="sxs-lookup"><span data-stu-id="75c8b-147">[How to use the Azure Command-Line Tools for Mac and Linux]:cli-install-nodejs.md</span></span>
<span data-ttu-id="75c8b-148">[средств командной строки Azure]:cli-install-nodejs.md</span><span class="sxs-lookup"><span data-stu-id="75c8b-148">[Azure Command-line tools]:cli-install-nodejs.md</span></span>
<span data-ttu-id="75c8b-149">[работать с модулями]: nodejs-use-node-modules-azure-apps.md</span><span class="sxs-lookup"><span data-stu-id="75c8b-149">[work with modules]: nodejs-use-node-modules-azure-apps.md</span></span>
[build and deploy a Node.js Web Site]: app-service-web/app-service-web-get-started-nodejs.md
