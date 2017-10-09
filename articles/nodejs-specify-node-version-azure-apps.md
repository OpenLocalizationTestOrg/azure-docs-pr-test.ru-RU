---
title: "aaaSpecifying Node.js версии"
description: "Узнайте, как toospecify hello версию Node.js, используемые веб-сайтов Azure и облачные службы"
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
ms.openlocfilehash: 09c27bfc43c132b6d66f9a2943179e06ee75bedc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="specifying-a-nodejs-version-in-an-azure-application"></a><span data-ttu-id="ddc12-103">Указание версии Node.js в приложении Azure</span><span class="sxs-lookup"><span data-stu-id="ddc12-103">Specifying a Node.js version in an Azure application</span></span>
<span data-ttu-id="ddc12-104">При размещении приложения Node.js, может потребоваться tooensure, что приложение использует конкретную версию Node.js.</span><span class="sxs-lookup"><span data-stu-id="ddc12-104">When hosting a Node.js application, you may want tooensure that your application uses a specific version of Node.js.</span></span> <span data-ttu-id="ddc12-105">Существует несколько способов tooaccomplish это для приложений, размещенных в Azure.</span><span class="sxs-lookup"><span data-stu-id="ddc12-105">There are several ways tooaccomplish this for applications hosted on Azure.</span></span>

## <a name="default-versions"></a><span data-ttu-id="ddc12-106">Версии по умолчанию</span><span class="sxs-lookup"><span data-stu-id="ddc12-106">Default versions</span></span>
<span data-ttu-id="ddc12-107">версии Node.js Hello, предоставляемые Azure постоянно обновляются.</span><span class="sxs-lookup"><span data-stu-id="ddc12-107">hello Node.js versions provided by Azure are constantly updated.</span></span> <span data-ttu-id="ddc12-108">Если не указано иначе, hello версия по умолчанию, которая указана в hello `WEBSITE_NODE_DEFAULT_VERSION` переменная среды будет использоваться.</span><span class="sxs-lookup"><span data-stu-id="ddc12-108">Unless otherwise specified, hello default version that is specified in hello `WEBSITE_NODE_DEFAULT_VERSION` environment variable will be used.</span></span> <span data-ttu-id="ddc12-109">toooverride это значение по умолчанию, повторите шаги hello в следующих разделах этой статьи</span><span class="sxs-lookup"><span data-stu-id="ddc12-109">toooverride this default value, follow hello steps in following sections of this article</span></span>

> [!NOTE]
> <span data-ttu-id="ddc12-110">Если имеются приложения в облачной службе Azure (рабочих и веб-роль) и впервые hello развернуто приложение hello, Azure попытается toouse hello ту же версию Node.js, как вы установили в среде разработки, если он совпадает с одним из версии по умолчанию hello доступный в Azure.</span><span class="sxs-lookup"><span data-stu-id="ddc12-110">If you are hosting your application in an Azure Cloud Service (web or worker role,) and it is hello first time you have deployed hello application, Azure will attempt toouse hello same version of Node.js as you have installed on your development environment if it matches one of hello default versions available on Azure.</span></span>
>
>

## <a name="versioning-with-packagejson"></a><span data-ttu-id="ddc12-111">Управление версиями с использованием package.json</span><span class="sxs-lookup"><span data-stu-id="ddc12-111">Versioning with package.json</span></span>
<span data-ttu-id="ddc12-112">Можно задать версию hello используется, добавив следующие tooyour hello toobe Node.js **package.json** файла:</span><span class="sxs-lookup"><span data-stu-id="ddc12-112">You can specify hello version of Node.js toobe used by adding hello following tooyour **package.json** file:</span></span>

    "engines":{"node":version}

<span data-ttu-id="ddc12-113">Где *версии* — число toouse hello определенной версии.</span><span class="sxs-lookup"><span data-stu-id="ddc12-113">Where *version* is hello specific version number toouse.</span></span> <span data-ttu-id="ddc12-114">Вы можете задать более сложные условия для версии, например:</span><span class="sxs-lookup"><span data-stu-id="ddc12-114">You can specify more complex conditions for version, such as:</span></span>

    "engines":{"node": "0.6.22 || 0.8.x"}

<span data-ttu-id="ddc12-115">Так как 0.6.22 не является одним из доступных в среде размещения hello версий hello, hello самую новую версию hello 0,8 ряда, который доступен используются вместо - 0.8.4.</span><span class="sxs-lookup"><span data-stu-id="ddc12-115">Since 0.6.22 is not one of hello versions available in hello hosting environment, hello highest version of hello 0.8 series that is available will be used instead - 0.8.4.</span></span>

## <a name="versioning-websites-with-app-settings"></a><span data-ttu-id="ddc12-116">Управление версиями веб-сайтов с помощью параметров приложения</span><span class="sxs-lookup"><span data-stu-id="ddc12-116">Versioning Websites with App Settings</span></span>
<span data-ttu-id="ddc12-117">При размещении приложения hello на веб-сайте, можно задать переменную среды hello **WEBSITE_NODE_DEFAULT_VERSION** toohello нужную версию.</span><span class="sxs-lookup"><span data-stu-id="ddc12-117">If you are hosting hello application in a Website, you can set hello environment variable **WEBSITE_NODE_DEFAULT_VERSION** toohello desired version.</span></span>

## <a name="versioning-cloud-services-with-powershell"></a><span data-ttu-id="ddc12-118">Управление версиями облачных служб с использованием PowerShell</span><span class="sxs-lookup"><span data-stu-id="ddc12-118">Versioning Cloud Services with PowerShell</span></span>
<span data-ttu-id="ddc12-119">При размещении приложения hello в облачной службе и развертывании приложения hello, с помощью Azure PowerShell, версия Node.js hello по умолчанию можно переопределить с помощью hello **AzureServiceProjectRole набор** командлета PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ddc12-119">If you are hosting hello application in a Cloud Service, and are deploying hello application using Azure PowerShell, you can override hello default Node.js version by using hello **Set-AzureServiceProjectRole** PowerShell cmdlet.</span></span> <span data-ttu-id="ddc12-120">Например:</span><span class="sxs-lookup"><span data-stu-id="ddc12-120">For example:</span></span>

    Set-AzureServiceProjectRole WebRole1 Node 0.8.4

<span data-ttu-id="ddc12-121">Параметры hello Примечание в hello выше инструкции, зависят от регистра.</span><span class="sxs-lookup"><span data-stu-id="ddc12-121">Note hello parameters in hello above statement are case-sensitive.</span></span>  <span data-ttu-id="ddc12-122">Можно проверить, проверив hello был выбран hello правильную версию Node.js **ядер** свойство в данной роли **package.json**.</span><span class="sxs-lookup"><span data-stu-id="ddc12-122">You can verify hello correct version of Node.js has been selected by checking hello **engines** property in your role's **package.json**.</span></span>

<span data-ttu-id="ddc12-123">Можно также использовать hello **Get AzureServiceProjectRoleRuntime** tooretrieve список Node.js версии для приложения, размещенные в облачной службе.</span><span class="sxs-lookup"><span data-stu-id="ddc12-123">You can also use hello **Get-AzureServiceProjectRoleRuntime** tooretrieve a list of Node.js versions available for applications hosted as a Cloud Service.</span></span>  <span data-ttu-id="ddc12-124">Всегда убедитесь, что версия hello Node.js зависит от проекта — в этом списке.</span><span class="sxs-lookup"><span data-stu-id="ddc12-124">Always verify hello version of Node.js your project depends on is in this list.</span></span>

## <a name="using-a-custom-version-with-azure-websites"></a><span data-ttu-id="ddc12-125">Использование настраиваемой версии с веб-сайтами Azure</span><span class="sxs-lookup"><span data-stu-id="ddc12-125">Using a custom version with Azure Websites</span></span>
<span data-ttu-id="ddc12-126">Хотя Azure предоставляет несколько версий по умолчанию Node.js, может возникнуть toouse версию, которая по умолчанию не предоставляется.</span><span class="sxs-lookup"><span data-stu-id="ddc12-126">While Azure provides several default versions of Node.js, you may want toouse a version that is not provided by default.</span></span> <span data-ttu-id="ddc12-127">Если приложение размещается в виде веб-сайт Azure, это можно сделать, используя hello **iisnode.yml** файла.</span><span class="sxs-lookup"><span data-stu-id="ddc12-127">If your application is hosted as an Azure Website, you can accomplish this by using hello **iisnode.yml** file.</span></span> <span data-ttu-id="ddc12-128">Hello следующие шаги пошагового hello процесс использования пользовательской версии Node.Js с веб-сайта Azure:</span><span class="sxs-lookup"><span data-stu-id="ddc12-128">hello following steps walk through hello process of using a custom version of Node.Js with an Azure Website:</span></span>

1. <span data-ttu-id="ddc12-129">Создать новый каталог, а затем создайте **server.js** файл в каталоге hello.</span><span class="sxs-lookup"><span data-stu-id="ddc12-129">Create a new directory, and then create a **server.js** file within hello directory.</span></span> <span data-ttu-id="ddc12-130">Hello **server.js** файл должен содержать hello следующее:</span><span class="sxs-lookup"><span data-stu-id="ddc12-130">hello **server.js** file should contain hello following:</span></span>

        var http = require('http');
        http.createServer(function(req,res) {
          res.writeHead(200, {'Content-Type': 'text/html'});
          res.end('Hello from Azure running node version: ' + process.version + '</br>');
        }).listen(process.env.PORT || 3000);

    <span data-ttu-id="ddc12-131">Это позволит отобразить hello Node.js версии используются при просмотре веб-сайта hello.</span><span class="sxs-lookup"><span data-stu-id="ddc12-131">This will display hello Node.js version being used when you browse hello website.</span></span>
2. <span data-ttu-id="ddc12-132">Создание нового веб-сайта и имя hello Примечание hello сайта.</span><span class="sxs-lookup"><span data-stu-id="ddc12-132">Create a new Website and note hello name of hello site.</span></span> <span data-ttu-id="ddc12-133">Например, следующие hello использует hello [средств командной строки Azure] toocreate новый веб-сайт Azure с именем **мой_веб**и затем включите репозитория для веб-сайта hello.</span><span class="sxs-lookup"><span data-stu-id="ddc12-133">For example, hello following uses hello [Azure Command-line tools] toocreate a new Azure Website named **mywebsite**, and then enable a Git repository for hello website.</span></span>

        azure site create mywebsite --git
3. <span data-ttu-id="ddc12-134">Создайте новый каталог с именем **bin** как дочерний hello каталог, содержащий hello **server.js** файла.</span><span class="sxs-lookup"><span data-stu-id="ddc12-134">Create a new directory named **bin** as a child of hello directory containing hello **server.js** file.</span></span>
4. <span data-ttu-id="ddc12-135">Загрузите hello конкретной версии **node.exe** (версия Windows hello) нужно toouse вместе с приложением.</span><span class="sxs-lookup"><span data-stu-id="ddc12-135">Download hello specific version of **node.exe** (hello Windows version) that you wish toouse with your application.</span></span> <span data-ttu-id="ddc12-136">Здравствуйте, например, следующие использует **curl** toodownload версии 0.8.1:</span><span class="sxs-lookup"><span data-stu-id="ddc12-136">For example, hello following uses **curl** toodownload version 0.8.1:</span></span>

        curl -O http://nodejs.org/dist/v0.8.1/node.exe

    <span data-ttu-id="ddc12-137">Сохранить hello **node.exe** файла в hello **bin** папки, созданной ранее.</span><span class="sxs-lookup"><span data-stu-id="ddc12-137">Save hello **node.exe** file into hello **bin** folder created previously.</span></span>
5. <span data-ttu-id="ddc12-138">Создание **iisnode.yml** файл hello же каталоге, что hello **server.js** файла, а затем добавьте следующие содержимого toohello hello **iisnode.yml** файла:</span><span class="sxs-lookup"><span data-stu-id="ddc12-138">Create an **iisnode.yml** file in hello same directory as hello **server.js** file, and then add hello following content toohello **iisnode.yml** file:</span></span>

        nodeProcessCommandLine: "D:\home\site\wwwroot\bin\node.exe"

    <span data-ttu-id="ddc12-139">Этот путь является там, где hello **node.exe** файла в проект будет располагаться после публикации toohello вашего приложения веб-сайта Azure.</span><span class="sxs-lookup"><span data-stu-id="ddc12-139">This path is where hello **node.exe** file within your project will be located once you have published your application toohello Azure Website.</span></span>
6. <span data-ttu-id="ddc12-140">Опубликуйте приложение.</span><span class="sxs-lookup"><span data-stu-id="ddc12-140">Publish your application.</span></span> <span data-ttu-id="ddc12-141">Например так как ранее созданного нового веб-сайта с параметром--git hello, hello следующие команды Добавление hello приложения файлы toomy локального репозитория Git и отправить их toohello репозитория веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="ddc12-141">For example, since I created a new website with hello --git parameter earlier, hello following commands will add hello application files toomy local Git repository, and then push them toohello website repository:</span></span>

        git add .
        git commit -m "testing node v0.8.1"
        git push azure master

    <span data-ttu-id="ddc12-142">После публикации приложения hello откройте веб-сайт hello в браузере.</span><span class="sxs-lookup"><span data-stu-id="ddc12-142">After hello application has published, open hello website in a browser.</span></span> <span data-ttu-id="ddc12-143">Должно появиться сообщение "Hello from Azure running node version: v0.8.1".</span><span class="sxs-lookup"><span data-stu-id="ddc12-143">You should see a message stating "Hello from Azure running node version: v0.8.1".</span></span>

## <a name="next-steps"></a><span data-ttu-id="ddc12-144">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ddc12-144">Next Steps</span></span>
<span data-ttu-id="ddc12-145">Теперь, когда вы знаете, как версия hello toospecify Node.js, используемого приложением, узнайте, каким образом слишком[работают с модулями], [построение и развертывание веб-сайта Node.js](app-service-web/app-service-web-get-started-nodejs.md), и [как toouse hello Azure Средства командной строки для Mac и Linux].</span><span class="sxs-lookup"><span data-stu-id="ddc12-145">Now that you understand how toospecify hello version of Node.js used by your application, learn how too[work with modules], [build and deploy a Node.js Web Site](app-service-web/app-service-web-get-started-nodejs.md), and [How toouse hello Azure Command-Line Tools for Mac and Linux].</span></span>

<span data-ttu-id="ddc12-146">Дополнительные сведения см. в разделе hello [Центр разработчика Node.js](https://azure.microsoft.com/develop/nodejs/).</span><span class="sxs-lookup"><span data-stu-id="ddc12-146">For more information, see hello [Node.js Developer Center](https://azure.microsoft.com/develop/nodejs/).</span></span>

[как toouse hello Azure Средства командной строки для Mac и Linux]:cli-install-nodejs.md
[средств командной строки Azure]:cli-install-nodejs.md
[работают с модулями]: nodejs-use-node-modules-azure-apps.md
[build and deploy a Node.js Web Site]: app-service-web/app-service-web-get-started-nodejs.md
