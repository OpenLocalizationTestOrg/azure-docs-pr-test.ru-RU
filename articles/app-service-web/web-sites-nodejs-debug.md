---
title: "Отладка веб-приложения Node.js в службе приложений Azure"
description: "Подробнее об отладке веб-приложения Node.js в службе приложений Azure."
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
ms.openlocfilehash: 5e302a4c58a171d40e43a22c34c724e868019ec8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-debug-a-nodejs-web-app-in-azure-app-service"></a><span data-ttu-id="ba942-103">Отладка веб-приложения Node.js в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="ba942-103">How to debug a Node.js web app in Azure App Service</span></span>
<span data-ttu-id="ba942-104">Azure предоставляет встроенные средства диагностики, которые помогают отлаживать приложения Node.js, размещенные в веб-приложениях [службы приложений Azure](http://go.microsoft.com/fwlink/?LinkId=529714) .</span><span class="sxs-lookup"><span data-stu-id="ba942-104">Azure provides built-in diagnostics to assist with debugging Node.js applications hosted in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps.</span></span> <span data-ttu-id="ba942-105">В этой статье вы узнаете, как включить ведение журналов stdout и stderr, отображать сведения об ошибке в браузере, а также загружать и просматривать файлы журнала.</span><span class="sxs-lookup"><span data-stu-id="ba942-105">In this article, you will learn how to enable logging of stdout and stderr, display error information in the browser, and how to download and view log files.</span></span>

<span data-ttu-id="ba942-106">Диагностика приложений Node.js, размещенных в Azure, обеспечивается [IISNode].</span><span class="sxs-lookup"><span data-stu-id="ba942-106">Diagnostics for Node.js applications hosted on Azure is provided by [IISNode].</span></span> <span data-ttu-id="ba942-107">Хотя в данной статье рассматриваются наиболее общие параметры для сбора диагностических сведений, она не является полным справочником по работе с IISNode.</span><span class="sxs-lookup"><span data-stu-id="ba942-107">While this article discusses the most common settings for gathering diagnostics information, it does not provide a complete reference for working with IISNode.</span></span> <span data-ttu-id="ba942-108">Дополнительные сведения о работе с IISNode см. в [файле сведений IISNode] на GitHub.</span><span class="sxs-lookup"><span data-stu-id="ba942-108">For more information on working with IISNode, see the [IISNode Readme] on GitHub.</span></span>

<a id="enablelogging"></a>

## <a name="enable-logging"></a><span data-ttu-id="ba942-109">Включение ведения журналов</span><span class="sxs-lookup"><span data-stu-id="ba942-109">Enable logging</span></span>
<span data-ttu-id="ba942-110">По умолчанию веб-приложения службы приложений записывают только диагностические сведения о развертывании, например при развертывании веб-приложения с использованием Git.</span><span class="sxs-lookup"><span data-stu-id="ba942-110">By default, an App Service web app only captures diagnostic information about deployments, such as when you deploy a web app using Git.</span></span> <span data-ttu-id="ba942-111">Эта информация полезна при возникновении проблем во время развертывания, таких как сбой при установке модуля, на который ссылается файл **package.json**, или при использовании пользовательских сценариев развертывания.</span><span class="sxs-lookup"><span data-stu-id="ba942-111">This information is useful if you are having problems during deployment, such as a failure when installing a module referenced in **package.json**, or if you are using a custom deployment script.</span></span>

<span data-ttu-id="ba942-112">Чтобы включить ведение журнала для потоков stdout и stderr, необходимо создать файл **IISNode.yml** в корне приложения Node.js и добавить следующий код:</span><span class="sxs-lookup"><span data-stu-id="ba942-112">To enable the logging of stdout and stderr streams, you must create an **IISNode.yml** file at the root of your Node.js application and add the following:</span></span>

    loggingEnabled: true

<span data-ttu-id="ba942-113">Это обеспечивает ведение журнала для потоков stderr и stdout из приложения Node.js.</span><span class="sxs-lookup"><span data-stu-id="ba942-113">This enables the logging of stderr and stdout from your Node.js application.</span></span>

<span data-ttu-id="ba942-114">Файл **IISNode.yml** может также использоваться для управления возвратом понятных пользователю ошибок или ошибок разработчика в браузер при сбое.</span><span class="sxs-lookup"><span data-stu-id="ba942-114">The **IISNode.yml** file can also be used to control whether friendly errors or developer errors are returned to the browser when a failure occurs.</span></span> <span data-ttu-id="ba942-115">Чтобы включить вывод ошибок разработчика, добавьте в файл **IISNode.yml** следующую строку:</span><span class="sxs-lookup"><span data-stu-id="ba942-115">To enable developer errors, add the following line to the **IISNode.yml** file:</span></span>

    devErrorsEnabled: true

<span data-ttu-id="ba942-116">После включения этого параметра IISNode будет возвращать последние 64 КБ данных, отправленных в stderr, вместо понятного пользователю сообщения об ошибке, такого как "Внутренняя ошибка сервера".</span><span class="sxs-lookup"><span data-stu-id="ba942-116">Once this option is enabled, IISNode will return the last 64K of information sent to stderr instead of a friendly error such as "an internal server error occurred".</span></span>

> [!NOTE]
> <span data-ttu-id="ba942-117">Хотя параметр devErrorsEnabled полезен при диагностике проблем во время разработки, его включение в рабочей среде может привести к тому, что конечному пользователю будут отправляться ошибки разработки.</span><span class="sxs-lookup"><span data-stu-id="ba942-117">While devErrorsEnabled is useful when diagnosing problems during development, enabling it in a production environment may result in development errors being sent to end users.</span></span>
> 
> 

<span data-ttu-id="ba942-118">Если файл **IISNode.yml** еще не существует в приложении, необходимо перезапустить веб-приложение после публикации обновленного приложения.</span><span class="sxs-lookup"><span data-stu-id="ba942-118">If the **IISNode.yml** file did not already exist within your application, you must restart your web app after publishing the updated application.</span></span> <span data-ttu-id="ba942-119">При простом изменении настроек в существующем файле **IISNode.yml** , который ранее был опубликован, перезагрузка не требуется.</span><span class="sxs-lookup"><span data-stu-id="ba942-119">If you are simply changing settings in an existing **IISNode.yml** file that has previously been published, no restart is required.</span></span>

> [!NOTE]
> <span data-ttu-id="ba942-120">Если веб-приложение было создано с помощью средства командной строки Azure или командлетов PowerShell Azure, автоматически создается файл по умолчанию **IISNode.yml** .</span><span class="sxs-lookup"><span data-stu-id="ba942-120">If your web app was created using the Azure Command-Line Tools or Azure PowerShell Cmdlets, a default **IISNode.yml** file is automatically created.</span></span>
> 
> 

<span data-ttu-id="ba942-121">Чтобы перезапустить веб-приложение, выберите его на [портале Azure](https://portal.azure.com)и нажмите кнопку **ПЕРЕЗАПУСТИТЬ** .</span><span class="sxs-lookup"><span data-stu-id="ba942-121">To restart the web app, select the web app in the [Azure Portal](https://portal.azure.com), and then click **RESTART** button:</span></span>

![кнопка перезагрузки][restart-button]

<span data-ttu-id="ba942-123">Если в среде разработки установлены средства командной строки Azure, чтобы перезапустить веб-приложение, можно воспользоваться следующей командой:</span><span class="sxs-lookup"><span data-stu-id="ba942-123">If the Azure Command-Line Tools are installed in your development environment, you can use the following command to restart the web app:</span></span>

    azure site restart [sitename]

> [!NOTE]
> <span data-ttu-id="ba942-124">Параметры конфигурации LoggingEnabled и devErrorsEnabled нужны в IISNode.yml для сбора диагностических сведений, однако IISNode.yml можно использовать для настройки различных параметров среды размещения.</span><span class="sxs-lookup"><span data-stu-id="ba942-124">While loggingEnabled and devErrorsEnabled are the most commonly used IISNode.yml configuration options for capturing diagnostic information, IISNode.yml can be used to configure a variety of options for your hosting environment.</span></span> <span data-ttu-id="ba942-125">Полный список параметров конфигурации доступен в файле [iisnode_schema.xml](https://github.com/tjanczuk/iisnode/blob/master/src/config/iisnode_schema.xml).</span><span class="sxs-lookup"><span data-stu-id="ba942-125">For a full list of the configuration options, see the [iisnode_schema.xml](https://github.com/tjanczuk/iisnode/blob/master/src/config/iisnode_schema.xml) file.</span></span>
> 
> 

<a id="viewlogs"></a>

## <a name="accessing-logs"></a><span data-ttu-id="ba942-126">Доступ к журналам</span><span class="sxs-lookup"><span data-stu-id="ba942-126">Accessing logs</span></span>
<span data-ttu-id="ba942-127">Доступ к журналам диагностики может осуществляться тремя способами; с использованием протокола FTP (File Transfer), путем загрузки ZIP-архива или в режиме потока журнала с обновлением в реальном времени (также известного как заключительный фрагмент).</span><span class="sxs-lookup"><span data-stu-id="ba942-127">Diagnostic logs can be accessed in three ways; Using the File Transfer Protocol (FTP), downloading a Zip archive, or as a live updated stream of the log (also known as a tail).</span></span> <span data-ttu-id="ba942-128">Загрузка ZIP-архива файлов журналов или просмотр потока в режиме реального времени требует наличия средств командной строки Azure.</span><span class="sxs-lookup"><span data-stu-id="ba942-128">Downloading the Zip archive of the log files or viewing the live stream require the Azure Command-Line Tools.</span></span> <span data-ttu-id="ba942-129">Их можно установить с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="ba942-129">These can be installed by using the following command:</span></span>

    npm install azure-cli -g

<span data-ttu-id="ba942-130">После установки доступ к данным средствам осуществляется с помощью команды "azure".</span><span class="sxs-lookup"><span data-stu-id="ba942-130">Once installed, the tools can be accessed using the 'azure' command.</span></span> <span data-ttu-id="ba942-131">Предварительно в средствах командной строки должно быть настроено использование подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="ba942-131">The command-line tools must first be configured to use your Azure subscription.</span></span> <span data-ttu-id="ba942-132">Сведения о том, как это сделать, см. в разделе **Загрузка и импорт настроек публикации** статьи [Использование средств командной строки Azure](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="ba942-132">For information on how to accomplish this task, see the **How to download and import publish settings** section of the [How to Use The Azure Command-Line Tools](../xplat-cli-connect.md) article.</span></span>

### <a name="ftp"></a><span data-ttu-id="ba942-133">FTP</span><span class="sxs-lookup"><span data-stu-id="ba942-133">FTP</span></span>
<span data-ttu-id="ba942-134">Чтобы получить доступ к диагностической информации через FTP, перейдите на [портал Azure](https://portal.azure.com), выберите свое веб-приложение, а затем выберите команду **ПАНЕЛЬ МОНИТОРИНГА**.</span><span class="sxs-lookup"><span data-stu-id="ba942-134">To access the diagnostic information through FTP, visit the [Azure Portal](https://portal.azure.com), select your web app, and then select the **DASHBOARD**.</span></span> <span data-ttu-id="ba942-135">В разделе **быстрых ссылок** ссылки **Журналы диагностики FTP** и **Журналы диагностики FTPS** позволяют перейти к журналам с использованием протокола FTP.</span><span class="sxs-lookup"><span data-stu-id="ba942-135">In the **quick links** section, the **FTP DIAGNOSTIC LOGS** and **FTPS DIAGNOSTIC LOGS** links provide access to the logs using the FTP protocol.</span></span>

> [!NOTE]
> <span data-ttu-id="ba942-136">Если имя пользователя и пароль для FTP или развертывания еще не указаны, это можно сделать на странице управления **Быстрый запуск**, выбрав **Настроить учетные данные развертывания**.</span><span class="sxs-lookup"><span data-stu-id="ba942-136">If you have not previously configured user name and password for FTP or deployment, you can do so from the **Quickstart** management page by selecting **Set up deployment credentials**.</span></span>
> 
> 

<span data-ttu-id="ba942-137">URL-адрес FTP, возвращаемый в панели мониторинга, относится к каталогу **LogFiles** , который будет содержать следующие вложенные папки:</span><span class="sxs-lookup"><span data-stu-id="ba942-137">The FTP URL returned in the dashboard is for the **LogFiles** directory, which will contain the following sub-directories:</span></span>

* <span data-ttu-id="ba942-138">[Метод развертывания](web-sites-deploy.md). При использовании метода развертывания, например Git, будет создан одноименный каталог со сведениями, связанными с развертываниями.</span><span class="sxs-lookup"><span data-stu-id="ba942-138">[Deployment Method](web-sites-deploy.md) - If you use a deployment method such as Git, a directory of the same name will be created and will contain information related to deployments.</span></span>
* <span data-ttu-id="ba942-139">nodejs — данные Stdout и stderr, регистрируемые во всех экземплярах вашего приложения, если параметр loggingEnabled имеет значение true.</span><span class="sxs-lookup"><span data-stu-id="ba942-139">nodejs - Stdout and stderr information captured from all instances of your application (when loggingEnabled is true.)</span></span>

### <a name="zip-archive"></a><span data-ttu-id="ba942-140">ZIP-архив</span><span class="sxs-lookup"><span data-stu-id="ba942-140">Zip archive</span></span>
<span data-ttu-id="ba942-141">Чтобы загрузить ZIP-архив журналов диагностики, выполните следующую команду в средствах командной строки Azure:</span><span class="sxs-lookup"><span data-stu-id="ba942-141">To download a Zip archive of the diagnostic logs, use the following command from the Azure Command-Line Tools:</span></span>

    azure site log download [sitename]

<span data-ttu-id="ba942-142">В результате в текущий каталог будет помещен файл **diagnostics.zip** .</span><span class="sxs-lookup"><span data-stu-id="ba942-142">This will download a **diagnostics.zip** in the current directory.</span></span> <span data-ttu-id="ba942-143">Данный архив содержит следующую структуру каталогов:</span><span class="sxs-lookup"><span data-stu-id="ba942-143">This archive contains the following directory structure:</span></span>

* <span data-ttu-id="ba942-144">deployments — журнал сведений о развертываниях вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="ba942-144">deployments - A log of information about deployments of your application</span></span>
* <span data-ttu-id="ba942-145">LogFiles</span><span class="sxs-lookup"><span data-stu-id="ba942-145">LogFiles</span></span>
  
  * <span data-ttu-id="ba942-146">[Метод развертывания](web-sites-deploy.md). При использовании метода развертывания, например Git, будет создан одноименный каталог со сведениями, связанными с развертываниями.</span><span class="sxs-lookup"><span data-stu-id="ba942-146">[Deployment method](web-sites-deploy.md) - If you use a deployment method such as Git, a directory of the same name will be created and will contain information related to deployments.</span></span>
  * <span data-ttu-id="ba942-147">nodejs — данные Stdout и stderr, регистрируемые во всех экземплярах вашего приложения, если параметр loggingEnabled имеет значение true.</span><span class="sxs-lookup"><span data-stu-id="ba942-147">nodejs - Stdout and stderr information captured from all instances of your application (when loggingEnabled is true.)</span></span>

### <a name="live-stream-tail"></a><span data-ttu-id="ba942-148">Поток в реальном времени (заключительный фрагмент)</span><span class="sxs-lookup"><span data-stu-id="ba942-148">Live stream (tail)</span></span>
<span data-ttu-id="ba942-149">Чтобы просмотреть поток журналов диагностики в реальном времени, выполните следующую команду в средствах командной строки Azure:</span><span class="sxs-lookup"><span data-stu-id="ba942-149">To view a live stream of diagnostic log information, use the following command from the Azure Command-Line Tools:</span></span>

    azure site log tail [sitename]

<span data-ttu-id="ba942-150">В результате будет возвращен поток событий журнала, которые обновляются по мере их возникновения на сервере.</span><span class="sxs-lookup"><span data-stu-id="ba942-150">This will return a stream of log events that are updated as they occur on the server.</span></span> <span data-ttu-id="ba942-151">Этот поток будет возвращать сведения о развертывании, а также сведения stdout и stderr (если параметр loggingEnabled имеет значение true).</span><span class="sxs-lookup"><span data-stu-id="ba942-151">This stream will return deployment information as well as stdout and stderr information (when loggingEnabled is true.)</span></span>

<a id="nextsteps"></a>

## <a name="next-steps"></a><span data-ttu-id="ba942-152">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ba942-152">Next Steps</span></span>
<span data-ttu-id="ba942-153">В этой статье было показано, как включить данные диагностики для Azure и получить к ним доступ.</span><span class="sxs-lookup"><span data-stu-id="ba942-153">In this article you learned how to enable and access diagnostics information for Azure.</span></span> <span data-ttu-id="ba942-154">Хотя эта информация полезна для понимания проблем, возникающих в приложении, она может указывать на проблему с используемым модулем или на то, что версия Node.js, используемая веб-приложениями службы приложений, отличается от версии в среде развертывания.</span><span class="sxs-lookup"><span data-stu-id="ba942-154">While this information is useful in understanding problems that occur with your application, it may point to a problem with a module you are using or that the version of Node.js used by App Service Web Apps is different than the one used in your deployment environment.</span></span>

<span data-ttu-id="ba942-155">Сведения по работе с модулями Azure см. в разделе [Использование модулей Node.js с приложениями Azure](../nodejs-use-node-modules-azure-apps.md).</span><span class="sxs-lookup"><span data-stu-id="ba942-155">For information in working with modules on Azure, see [Using Node.js Modules with Azure Applications](../nodejs-use-node-modules-azure-apps.md).</span></span>

<span data-ttu-id="ba942-156">Сведения об определении версии Node.js для своего приложения см. в разделе [Установка версии Node.js в приложении Azure].</span><span class="sxs-lookup"><span data-stu-id="ba942-156">For information on specifying a Node.js version for your application, see [Specifying a Node.js version in an Azure application].</span></span>

<span data-ttu-id="ba942-157">Дополнительные сведения см. также в [центре по разработке для Node.js](/develop/nodejs/).</span><span class="sxs-lookup"><span data-stu-id="ba942-157">For more information, see also the [Node.js Developer Center](/develop/nodejs/).</span></span>

## <a name="whats-changed"></a><span data-ttu-id="ba942-158">Изменения</span><span class="sxs-lookup"><span data-stu-id="ba942-158">What's changed</span></span>
* <span data-ttu-id="ba942-159">Руководство по переходу от веб-сайтов к службе приложений см. в статье [Служба приложений Azure и существующие службы Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="ba942-159">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

> [!NOTE]
> <span data-ttu-id="ba942-160">Чтобы приступить к работе со службой приложений Azure до создания учетной записи Azure, перейдите к разделу [Пробное использование службы приложений](https://azure.microsoft.com/try/app-service/), где вы можете быстро создать кратковременное веб-приложение начального уровня в службе приложений.</span><span class="sxs-lookup"><span data-stu-id="ba942-160">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="ba942-161">Никаких кредитных карт и обязательств.</span><span class="sxs-lookup"><span data-stu-id="ba942-161">No credit cards required; no commitments.</span></span>
> 
> 

<span data-ttu-id="ba942-162">[IISNode]: https://github.com/tjanczuk/iisnode</span><span class="sxs-lookup"><span data-stu-id="ba942-162">[IISNode]: https://github.com/tjanczuk/iisnode</span></span>
<span data-ttu-id="ba942-163">[файле сведений IISNode]: https://github.com/tjanczuk/iisnode#readme</span><span class="sxs-lookup"><span data-stu-id="ba942-163">[IISNode Readme]: https://github.com/tjanczuk/iisnode#readme</span></span>
[How to Use The Azure Command-Line Interface]:../cli-install-nodejs.md
[Using Node.js Modules with Azure Applications]: ../nodejs-use-node-modules-azure-apps.md
<span data-ttu-id="ba942-164">[Установка версии Node.js в приложении Azure]: ../nodejs-specify-node-version-azure-apps.md</span><span class="sxs-lookup"><span data-stu-id="ba942-164">[Specifying a Node.js version in an Azure application]: ../nodejs-specify-node-version-azure-apps.md</span></span>

[restart-button]: ./media/web-sites-nodejs-debug/restartbutton.png

