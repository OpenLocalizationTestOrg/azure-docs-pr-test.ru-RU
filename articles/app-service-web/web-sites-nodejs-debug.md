---
title: "aaaHow toodebug Node.js веб-приложения в службе приложений Azure"
description: "Узнайте, как toodebug Node.js веб-приложения в службе приложений Azure."
tags: azure-portal
services: app-service\web
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: a48f906c-1a3e-43bc-ae84-7d2dde175b15
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: 888ec5c3f92cfc3aeea4ea86005b9b6a0d1306ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodebug-a-nodejs-web-app-in-azure-app-service"></a><span data-ttu-id="d7e42-103">Как toodebug Node.js веб-приложения в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="d7e42-103">How toodebug a Node.js web app in Azure App Service</span></span>
<span data-ttu-id="d7e42-104">Azure предоставляет tooassist встроенных средств диагностики с отладкой приложений Node.js, размещенных в [службе приложений Azure](http://go.microsoft.com/fwlink/?LinkId=529714) веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="d7e42-104">Azure provides built-in diagnostics tooassist with debugging Node.js applications hosted in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps.</span></span> <span data-ttu-id="d7e42-105">В этой статье вы узнаете, как ведение журнала tooenable stdout и stderr, сведения об ошибках отображения в браузере hello и как toodownload и просмотр файлов журнала.</span><span class="sxs-lookup"><span data-stu-id="d7e42-105">In this article, you will learn how tooenable logging of stdout and stderr, display error information in hello browser, and how toodownload and view log files.</span></span>

<span data-ttu-id="d7e42-106">Диагностика приложений Node.js, размещенных в Azure, обеспечивается [IISNode].</span><span class="sxs-lookup"><span data-stu-id="d7e42-106">Diagnostics for Node.js applications hosted on Azure is provided by [IISNode].</span></span> <span data-ttu-id="d7e42-107">Хотя в этой статье рассматриваются наиболее распространенные параметры hello для сбора данных диагностики, он не предоставляет полный Справочник по работе с IISNode.</span><span class="sxs-lookup"><span data-stu-id="d7e42-107">While this article discusses hello most common settings for gathering diagnostics information, it does not provide a complete reference for working with IISNode.</span></span> <span data-ttu-id="d7e42-108">Дополнительные сведения о работе с IISNode см. в разделе hello [IISNode Readme] на GitHub.</span><span class="sxs-lookup"><span data-stu-id="d7e42-108">For more information on working with IISNode, see hello [IISNode Readme] on GitHub.</span></span>

<a id="enablelogging"></a>

## <a name="enable-logging"></a><span data-ttu-id="d7e42-109">Включение ведения журналов</span><span class="sxs-lookup"><span data-stu-id="d7e42-109">Enable logging</span></span>
<span data-ttu-id="d7e42-110">По умолчанию веб-приложения службы приложений записывают только диагностические сведения о развертывании, например при развертывании веб-приложения с использованием Git.</span><span class="sxs-lookup"><span data-stu-id="d7e42-110">By default, an App Service web app only captures diagnostic information about deployments, such as when you deploy a web app using Git.</span></span> <span data-ttu-id="d7e42-111">Эта информация полезна при возникновении проблем во время развертывания, таких как сбой при установке модуля, на который ссылается файл **package.json**, или при использовании пользовательских сценариев развертывания.</span><span class="sxs-lookup"><span data-stu-id="d7e42-111">This information is useful if you are having problems during deployment, such as a failure when installing a module referenced in **package.json**, or if you are using a custom deployment script.</span></span>

<span data-ttu-id="d7e42-112">tooenable hello при ведении журнала потоки stdout и stderr, необходимо создать **IISNode.yml** hello корневого каталога приложения Node.js и добавьте следующее hello:</span><span class="sxs-lookup"><span data-stu-id="d7e42-112">tooenable hello logging of stdout and stderr streams, you must create an **IISNode.yml** file at hello root of your Node.js application and add hello following:</span></span>

    loggingEnabled: true

<span data-ttu-id="d7e42-113">Это позволяет ведения журнала hello stderr и stdout из приложения Node.js.</span><span class="sxs-lookup"><span data-stu-id="d7e42-113">This enables hello logging of stderr and stdout from your Node.js application.</span></span>

<span data-ttu-id="d7e42-114">Hello **IISNode.yml** файл также можно использовать toocontrol ли понятные ошибки или ошибки разработчика возвращаются toohello браузера при возникновении сбоя.</span><span class="sxs-lookup"><span data-stu-id="d7e42-114">hello **IISNode.yml** file can also be used toocontrol whether friendly errors or developer errors are returned toohello browser when a failure occurs.</span></span> <span data-ttu-id="d7e42-115">ошибки tooenable разработчика, добавьте следующие строки toohello hello **IISNode.yml** файла:</span><span class="sxs-lookup"><span data-stu-id="d7e42-115">tooenable developer errors, add hello following line toohello **IISNode.yml** file:</span></span>

    devErrorsEnabled: true

<span data-ttu-id="d7e42-116">Этот параметр включен, IISNode будет выполнен возврат hello последние 64 КБ данных, отправляемых toostderr вместо сообщением об ошибке, такие как «произошла внутренняя ошибка сервера».</span><span class="sxs-lookup"><span data-stu-id="d7e42-116">Once this option is enabled, IISNode will return hello last 64K of information sent toostderr instead of a friendly error such as "an internal server error occurred".</span></span>

> [!NOTE]
> <span data-ttu-id="d7e42-117">DevErrorsEnabled полезен при диагностике проблем во время разработки, включение его в рабочей среде может привести к ошибкам разработки, отправляемых пользователям tooend.</span><span class="sxs-lookup"><span data-stu-id="d7e42-117">While devErrorsEnabled is useful when diagnosing problems during development, enabling it in a production environment may result in development errors being sent tooend users.</span></span>
> 
> 

<span data-ttu-id="d7e42-118">Если hello **IISNode.yml** файл не существовал в приложении, необходимо перезапустить веб-приложения после публикации приложения hello обновлены.</span><span class="sxs-lookup"><span data-stu-id="d7e42-118">If hello **IISNode.yml** file did not already exist within your application, you must restart your web app after publishing hello updated application.</span></span> <span data-ttu-id="d7e42-119">При простом изменении настроек в существующем файле **IISNode.yml** , который ранее был опубликован, перезагрузка не требуется.</span><span class="sxs-lookup"><span data-stu-id="d7e42-119">If you are simply changing settings in an existing **IISNode.yml** file that has previously been published, no restart is required.</span></span>

> [!NOTE]
> <span data-ttu-id="d7e42-120">Если веб-приложения был создан с помощью средства командной строки hello Azure или командлеты PowerShell для Azure, значение по умолчанию **IISNode.yml** файл создается автоматически.</span><span class="sxs-lookup"><span data-stu-id="d7e42-120">If your web app was created using hello Azure Command-Line Tools or Azure PowerShell Cmdlets, a default **IISNode.yml** file is automatically created.</span></span>
> 
> 

<span data-ttu-id="d7e42-121">toorestart hello веб-приложения, веб-приложения выберите hello в hello [портала Azure](https://portal.azure.com), а затем нажмите кнопку **ПЕРЕЗАПУСТИТЕ** кнопки:</span><span class="sxs-lookup"><span data-stu-id="d7e42-121">toorestart hello web app, select hello web app in hello [Azure Portal](https://portal.azure.com), and then click **RESTART** button:</span></span>

![кнопка перезагрузки][restart-button]

<span data-ttu-id="d7e42-123">Если средства командной строки Azure hello установлены в среде разработки, можно использовать следующие команды toorestart hello веб-приложения hello:</span><span class="sxs-lookup"><span data-stu-id="d7e42-123">If hello Azure Command-Line Tools are installed in your development environment, you can use hello following command toorestart hello web app:</span></span>

    azure site restart [sitename]

> [!NOTE]
> <span data-ttu-id="d7e42-124">Хотя loggingEnabled и devErrorsEnabled, параметры конфигурации IISNode.yml hello чаще всего используется для сбора диагностических сведений, IISNode.yml может быть tooconfigure используется ряд параметров для выбранной среды размещения.</span><span class="sxs-lookup"><span data-stu-id="d7e42-124">While loggingEnabled and devErrorsEnabled are hello most commonly used IISNode.yml configuration options for capturing diagnostic information, IISNode.yml can be used tooconfigure a variety of options for your hosting environment.</span></span> <span data-ttu-id="d7e42-125">Полный список параметров конфигурации hello см. в разделе hello [iisnode_schema.xml](https://github.com/tjanczuk/iisnode/blob/master/src/config/iisnode_schema.xml) файла.</span><span class="sxs-lookup"><span data-stu-id="d7e42-125">For a full list of hello configuration options, see hello [iisnode_schema.xml](https://github.com/tjanczuk/iisnode/blob/master/src/config/iisnode_schema.xml) file.</span></span>
> 
> 

<a id="viewlogs"></a>

## <a name="accessing-logs"></a><span data-ttu-id="d7e42-126">Доступ к журналам</span><span class="sxs-lookup"><span data-stu-id="d7e42-126">Accessing logs</span></span>
<span data-ttu-id="d7e42-127">Журналы диагностики может осуществляться тремя способами; С помощью hello передачи файлов Protocol (FTP), загрузка ZIP-архив, или как активный обновляются потока журнала hello (также известного как заключительный фрагмент).</span><span class="sxs-lookup"><span data-stu-id="d7e42-127">Diagnostic logs can be accessed in three ways; Using hello File Transfer Protocol (FTP), downloading a Zip archive, or as a live updated stream of hello log (also known as a tail).</span></span> <span data-ttu-id="d7e42-128">Загрузка ZIP-архив hello hello файлов журнала или просмотр потоковой трансляции hello требуют hello Azure программы командной строки.</span><span class="sxs-lookup"><span data-stu-id="d7e42-128">Downloading hello Zip archive of hello log files or viewing hello live stream require hello Azure Command-Line Tools.</span></span> <span data-ttu-id="d7e42-129">Их можно устанавливать с помощью hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="d7e42-129">These can be installed by using hello following command:</span></span>

    npm install azure-cli -g

<span data-ttu-id="d7e42-130">После установки средств hello может осуществляться с помощью команды «azure» hello.</span><span class="sxs-lookup"><span data-stu-id="d7e42-130">Once installed, hello tools can be accessed using hello 'azure' command.</span></span> <span data-ttu-id="d7e42-131">Здравствуйте, средства командной строки, сначала должны быть настроенный toouse подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="d7e42-131">hello command-line tools must first be configured toouse your Azure subscription.</span></span> <span data-ttu-id="d7e42-132">Сведения о том, как tooaccomplish это задача см. в разделе hello **как toodownload и импорт параметров публикации** раздел hello [как tooUse hello средства командной строки Azure](../xplat-cli-connect.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="d7e42-132">For information on how tooaccomplish this task, see hello **How toodownload and import publish settings** section of hello [How tooUse hello Azure Command-Line Tools](../xplat-cli-connect.md) article.</span></span>

### <a name="ftp"></a><span data-ttu-id="d7e42-133">FTP</span><span class="sxs-lookup"><span data-stu-id="d7e42-133">FTP</span></span>
<span data-ttu-id="d7e42-134">tooaccess hello диагностических сведений по протоколу FTP, посетите hello [портала Azure](https://portal.azure.com), выберите веб-приложения, а затем выберите hello **МОНИТОРИНГА**.</span><span class="sxs-lookup"><span data-stu-id="d7e42-134">tooaccess hello diagnostic information through FTP, visit hello [Azure Portal](https://portal.azure.com), select your web app, and then select hello **DASHBOARD**.</span></span> <span data-ttu-id="d7e42-135">В hello **быстрые ссылки** статьи, hello **ЖУРНАЛЫ диагностики FTP** и **ЖУРНАЛЫ диагностики FTPS** ссылкам toohello журналы событий с помощью протокола hello FTP.</span><span class="sxs-lookup"><span data-stu-id="d7e42-135">In hello **quick links** section, hello **FTP DIAGNOSTIC LOGS** and **FTPS DIAGNOSTIC LOGS** links provide access toohello logs using hello FTP protocol.</span></span>

> [!NOTE]
> <span data-ttu-id="d7e42-136">Если вы не настроили ранее имя пользователя и пароль для FTP или развертывание, это можно сделать из hello **краткое руководство** управления страницы, выбрав **настроить учетные данные развертывания**.</span><span class="sxs-lookup"><span data-stu-id="d7e42-136">If you have not previously configured user name and password for FTP or deployment, you can do so from hello **Quickstart** management page by selecting **Set up deployment credentials**.</span></span>
> 
> 

<span data-ttu-id="d7e42-137">Hello URL-адрес FTP, возвращаются в панели мониторинга hello предназначен для hello **LogFiles** каталог, который будет содержать следующие вложенные каталоги hello:</span><span class="sxs-lookup"><span data-stu-id="d7e42-137">hello FTP URL returned in hello dashboard is for hello **LogFiles** directory, which will contain hello following sub-directories:</span></span>

* <span data-ttu-id="d7e42-138">[Метод развертывания](web-sites-deploy.md) -при использовании метода развертывания, например Git каталог hello таким же именем будет создана и содержит сведения, связанные с toodeployments.</span><span class="sxs-lookup"><span data-stu-id="d7e42-138">[Deployment Method](web-sites-deploy.md) - If you use a deployment method such as Git, a directory of hello same name will be created and will contain information related toodeployments.</span></span>
* <span data-ttu-id="d7e42-139">nodejs — данные Stdout и stderr, регистрируемые во всех экземплярах вашего приложения, если параметр loggingEnabled имеет значение true.</span><span class="sxs-lookup"><span data-stu-id="d7e42-139">nodejs - Stdout and stderr information captured from all instances of your application (when loggingEnabled is true.)</span></span>

### <a name="zip-archive"></a><span data-ttu-id="d7e42-140">ZIP-архив</span><span class="sxs-lookup"><span data-stu-id="d7e42-140">Zip archive</span></span>
<span data-ttu-id="d7e42-141">toodownload ZIP-архив hello диагностических журналов, hello используйте следующую команду из командной строки средства hello Azure:</span><span class="sxs-lookup"><span data-stu-id="d7e42-141">toodownload a Zip archive of hello diagnostic logs, use hello following command from hello Azure Command-Line Tools:</span></span>

    azure site log download [sitename]

<span data-ttu-id="d7e42-142">Будет загружен **diagnostics.zip** в текущем каталоге hello.</span><span class="sxs-lookup"><span data-stu-id="d7e42-142">This will download a **diagnostics.zip** in hello current directory.</span></span> <span data-ttu-id="d7e42-143">Этот архив содержит hello следующая структура каталогов:</span><span class="sxs-lookup"><span data-stu-id="d7e42-143">This archive contains hello following directory structure:</span></span>

* <span data-ttu-id="d7e42-144">deployments — журнал сведений о развертываниях вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="d7e42-144">deployments - A log of information about deployments of your application</span></span>
* <span data-ttu-id="d7e42-145">LogFiles</span><span class="sxs-lookup"><span data-stu-id="d7e42-145">LogFiles</span></span>
  
  * <span data-ttu-id="d7e42-146">[Метод развертывания](web-sites-deploy.md) -при использовании метода развертывания, например Git каталог hello таким же именем будет создана и содержит сведения, связанные с toodeployments.</span><span class="sxs-lookup"><span data-stu-id="d7e42-146">[Deployment method](web-sites-deploy.md) - If you use a deployment method such as Git, a directory of hello same name will be created and will contain information related toodeployments.</span></span>
  * <span data-ttu-id="d7e42-147">nodejs — данные Stdout и stderr, регистрируемые во всех экземплярах вашего приложения, если параметр loggingEnabled имеет значение true.</span><span class="sxs-lookup"><span data-stu-id="d7e42-147">nodejs - Stdout and stderr information captured from all instances of your application (when loggingEnabled is true.)</span></span>

### <a name="live-stream-tail"></a><span data-ttu-id="d7e42-148">Поток в реальном времени (заключительный фрагмент)</span><span class="sxs-lookup"><span data-stu-id="d7e42-148">Live stream (tail)</span></span>
<span data-ttu-id="d7e42-149">tooview обновляющегося потока данных журнала диагностики, hello используйте следующую команду из командной строки средства hello Azure:</span><span class="sxs-lookup"><span data-stu-id="d7e42-149">tooview a live stream of diagnostic log information, use hello following command from hello Azure Command-Line Tools:</span></span>

    azure site log tail [sitename]

<span data-ttu-id="d7e42-150">Возвращает поток событий журнала, которые обновляются по мере их появления на сервере hello.</span><span class="sxs-lookup"><span data-stu-id="d7e42-150">This will return a stream of log events that are updated as they occur on hello server.</span></span> <span data-ttu-id="d7e42-151">Этот поток будет возвращать сведения о развертывании, а также сведения stdout и stderr (если параметр loggingEnabled имеет значение true).</span><span class="sxs-lookup"><span data-stu-id="d7e42-151">This stream will return deployment information as well as stdout and stderr information (when loggingEnabled is true.)</span></span>

<a id="nextsteps"></a>

## <a name="next-steps"></a><span data-ttu-id="d7e42-152">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d7e42-152">Next Steps</span></span>
<span data-ttu-id="d7e42-153">В этой статье вы узнали, как tooenable и доступа диагностическую информацию по Azure.</span><span class="sxs-lookup"><span data-stu-id="d7e42-153">In this article you learned how tooenable and access diagnostics information for Azure.</span></span> <span data-ttu-id="d7e42-154">Хотя эта информация полезна в основные сведения о возникающих проблем с приложением, он может ссылаться неполадки tooa модуль, который вы используете или этой версии hello Node.js, используемые веб-приложений служб приложений отличается от hello календарем, используемым в развертывании Среда.</span><span class="sxs-lookup"><span data-stu-id="d7e42-154">While this information is useful in understanding problems that occur with your application, it may point tooa problem with a module you are using or that hello version of Node.js used by App Service Web Apps is different than hello one used in your deployment environment.</span></span>

<span data-ttu-id="d7e42-155">Сведения по работе с модулями Azure см. в разделе [Использование модулей Node.js с приложениями Azure](../nodejs-use-node-modules-azure-apps.md).</span><span class="sxs-lookup"><span data-stu-id="d7e42-155">For information in working with modules on Azure, see [Using Node.js Modules with Azure Applications](../nodejs-use-node-modules-azure-apps.md).</span></span>

<span data-ttu-id="d7e42-156">Сведения об определении версии Node.js для своего приложения см. в разделе [Установка версии Node.js в приложении Azure].</span><span class="sxs-lookup"><span data-stu-id="d7e42-156">For information on specifying a Node.js version for your application, see [Specifying a Node.js version in an Azure application].</span></span>

<span data-ttu-id="d7e42-157">Дополнительные сведения см. также: hello [Центр разработчика Node.js](/develop/nodejs/).</span><span class="sxs-lookup"><span data-stu-id="d7e42-157">For more information, see also hello [Node.js Developer Center](/develop/nodejs/).</span></span>

## <a name="whats-changed"></a><span data-ttu-id="d7e42-158">Изменения</span><span class="sxs-lookup"><span data-stu-id="d7e42-158">What's changed</span></span>
* <span data-ttu-id="d7e42-159">Toohello руководство изменений из tooApp веб-сайтов службы. в разделе: [службе приложений Azure и ее влияние на существующие службы Azure](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="d7e42-159">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

> [!NOTE]
> <span data-ttu-id="d7e42-160">Tooget работы в службе приложений Azure перед регистрацией учетную запись Azure, перейдите слишком[повторите служб приложений](https://azure.microsoft.com/try/app-service/), в котором можно немедленно создать кратковременных начальный веб-приложения в службе приложений.</span><span class="sxs-lookup"><span data-stu-id="d7e42-160">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="d7e42-161">Никаких кредитных карт и обязательств.</span><span class="sxs-lookup"><span data-stu-id="d7e42-161">No credit cards required; no commitments.</span></span>
> 
> 

[IISNode]: https://github.com/tjanczuk/iisnode
[IISNode Readme]: https://github.com/tjanczuk/iisnode#readme
[How tooUse hello Azure Command-Line Interface]:../cli-install-nodejs.md
[Using Node.js Modules with Azure Applications]: ../nodejs-use-node-modules-azure-apps.md
[Установка версии Node.js в приложении Azure]: ../nodejs-specify-node-version-azure-apps.md

[restart-button]: ./media/web-sites-nodejs-debug/restartbutton.png

