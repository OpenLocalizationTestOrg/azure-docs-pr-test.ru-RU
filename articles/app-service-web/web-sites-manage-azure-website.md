---
title: "aaaManage веб-приложения в службе приложений Azure"
description: "Tooresources ссылки для управления веб-приложения в службе приложений Azure."
services: app-service\web
documentationcenter: 
author: erikre
manager: erikre
editor: 
ms.assetid: d5e2887a-84f9-4747-a573-867635cb8b39
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/24/2016
ms.author: rachelap
ms.openlocfilehash: daf69245e66068b0e97e3ae1c3fb5fce45605b91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-web-app-in-azure-app-service"></a><span data-ttu-id="9fdf9-103">Управление веб-приложением в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="9fdf9-103">Manage a web app in Azure App Service</span></span>
<span data-ttu-id="9fdf9-104">В этом разделе содержатся ссылки tooresources для управления веб-приложения в [службе приложений Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="9fdf9-104">This topic contains links tooresources for managing a web app in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="9fdf9-105">Управление включает в себя все задачи hello, сохранить бесперебойной работы веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="9fdf9-105">Management includes all of hello tasks that keep your web app running smoothly.</span></span> 

<span data-ttu-id="9fdf9-106">За время жизни hello веб-приложения будет выполнять задачи управления при перемещении от операции toonormal первоначального развертывания, обслуживания и обновления.</span><span class="sxs-lookup"><span data-stu-id="9fdf9-106">Over hello lifetime of a web app, you will perform different management tasks, as you move from initial deployment toonormal operation, maintenance, and updates.</span></span>

<span data-ttu-id="9fdf9-107">Многие веб-приложения управления задачи могут выполняться в hello портала Azure.</span><span class="sxs-lookup"><span data-stu-id="9fdf9-107">Many web app management tasks can be performed in hello Azure Portal.</span></span>

## <a name="before-you-deploy-your-web-app-tooproduction"></a><span data-ttu-id="9fdf9-108">Перед развертыванием вашей tooproduction web app</span><span class="sxs-lookup"><span data-stu-id="9fdf9-108">Before you deploy your web app tooproduction</span></span>
### <a name="choose-a-tier"></a><span data-ttu-id="9fdf9-109">Выберите уровень.</span><span class="sxs-lookup"><span data-stu-id="9fdf9-109">Choose a tier</span></span>
<span data-ttu-id="9fdf9-110">Служба приложений Azure доступна для 5 уровней: Free, Shared, Basic, Standard и Premium.</span><span class="sxs-lookup"><span data-stu-id="9fdf9-110">Azure App Service is offered in five tiers: Free, Shared, Basic, Standard, and Premium.</span></span> <span data-ttu-id="9fdf9-111">Сведения о функции hello и цен для каждого уровня см. в разделе [сведения о ценах](https://azure.microsoft.com/pricing/details/app-service/).</span><span class="sxs-lookup"><span data-stu-id="9fdf9-111">For information about hello features and pricing for each tier, see [Pricing details](https://azure.microsoft.com/pricing/details/app-service/).</span></span> 

* <span data-ttu-id="9fdf9-112">[Планы служб приложений](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) позволяют группировать несколько веб-приложений в группе hello того же уровня.</span><span class="sxs-lookup"><span data-stu-id="9fdf9-112">[App Service plans](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) let you group multiple web apps under hello same tier.</span></span>
* <span data-ttu-id="9fdf9-113">Всегда можно [сменить уровень](web-sites-scale.md) после создания веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="9fdf9-113">You can always [switch tiers](web-sites-scale.md) after you create your web app.</span></span>

### <a name="configuration"></a><span data-ttu-id="9fdf9-114">Конфигурация</span><span class="sxs-lookup"><span data-stu-id="9fdf9-114">Configuration</span></span>
<span data-ttu-id="9fdf9-115">Используйте hello [портала Azure](https://portal.azure.com/) tooset различные параметры конфигурации.</span><span class="sxs-lookup"><span data-stu-id="9fdf9-115">Use hello [Azure Portal](https://portal.azure.com/) tooset various configuration options.</span></span> <span data-ttu-id="9fdf9-116">Подробные сведения см. в разделе [Настройка веб-приложений в службе приложений Azure](web-sites-configure.md).</span><span class="sxs-lookup"><span data-stu-id="9fdf9-116">For details, see [Configure web apps in Azure App Service](web-sites-configure.md).</span></span> <span data-ttu-id="9fdf9-117">Вот краткий контрольный список:</span><span class="sxs-lookup"><span data-stu-id="9fdf9-117">Here is a quick checklist:</span></span>

* <span data-ttu-id="9fdf9-118">При необходимости выберите **версии сред выполнения** для .NET, PHP, Java или Python.</span><span class="sxs-lookup"><span data-stu-id="9fdf9-118">Select **runtime versions** for .NET, PHP, Java, or Python, if needed.</span></span>
* <span data-ttu-id="9fdf9-119">Включить **WebSockets** Если веб-приложение использует протокол WebSocket hello.</span><span class="sxs-lookup"><span data-stu-id="9fdf9-119">Enable **WebSockets** if your web app uses hello WebSocket protocol.</span></span> <span data-ttu-id="9fdf9-120">(Это относится к приложениям, которые используют [ASP.NET SignalR](http://www.asp.net/signalr) или [socket.io](web-sites-nodejs-chat-app-socketio.md).)</span><span class="sxs-lookup"><span data-stu-id="9fdf9-120">(This includes apps that use [ASP.NET SignalR](http://www.asp.net/signalr) or [socket.io](web-sites-nodejs-chat-app-socketio.md).)</span></span>
* <span data-ttu-id="9fdf9-121">Вы используете непрерывные веб-задания?</span><span class="sxs-lookup"><span data-stu-id="9fdf9-121">Are you running continuous web jobs?</span></span> <span data-ttu-id="9fdf9-122">Если да, то выберите параметр **Always On**(Всегда включено).</span><span class="sxs-lookup"><span data-stu-id="9fdf9-122">If so, enable **Always On**.</span></span>
* <span data-ttu-id="9fdf9-123">Набор hello **документ по умолчанию**, такие как index.html.</span><span class="sxs-lookup"><span data-stu-id="9fdf9-123">Set hello **default document**, such as index.html.</span></span>

<span data-ttu-id="9fdf9-124">Добавление toothese базовые параметры конфигурации вы можете tooconfigure hello следующее:</span><span class="sxs-lookup"><span data-stu-id="9fdf9-124">In addition toothese basic configuration settings, you may want tooconfigure hello following:</span></span>

* <span data-ttu-id="9fdf9-125">Шифрование **SSL**.</span><span class="sxs-lookup"><span data-stu-id="9fdf9-125">**Secure Socket Layer (SSL)** encryption.</span></span> <span data-ttu-id="9fdf9-126">toouse SSL с именем пользовательского домена, необходимо получить SSL сертификатов и настройка вашей toouse web app его.</span><span class="sxs-lookup"><span data-stu-id="9fdf9-126">toouse SSL with a custom domain name, you must get an SSL certificate and configure your web app toouse it.</span></span> <span data-ttu-id="9fdf9-127">Ознакомьтесь со статьей [Включение протокола HTTPS для веб-приложения в службе приложений Azure](app-service-web-tutorial-custom-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="9fdf9-127">See [Enable HTTPS for a web app in Azure App Service](app-service-web-tutorial-custom-ssl.md).</span></span>
* <span data-ttu-id="9fdf9-128">**Имя личного домена**.</span><span class="sxs-lookup"><span data-stu-id="9fdf9-128">**Custom domain name.**</span></span> <span data-ttu-id="9fdf9-129">Вашему веб-приложению автоматически присваивается дочерний домен в azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="9fdf9-129">Your web app automatically has a subdomain under azurewebsites.net.</span></span> <span data-ttu-id="9fdf9-130">Вы можете связать сайт с пользовательским доменным именем, например contoso.com. Ознакомьтесь со статьей [Настройка личного доменного имени для службы приложений Azure](app-service-web-tutorial-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="9fdf9-130">You can associate a custom domain name, such as contoso.com. See [Configure a custom domain name in Azure App Service](app-service-web-tutorial-custom-domain.md).</span></span>

<span data-ttu-id="9fdf9-131">Настройка для определенных языков программирования:</span><span class="sxs-lookup"><span data-stu-id="9fdf9-131">Language-specific configuration:</span></span>

* <span data-ttu-id="9fdf9-132">**PHP**: статья [Настройка PHP в веб-приложениях службы приложений Azure](web-sites-php-configure.md).</span><span class="sxs-lookup"><span data-stu-id="9fdf9-132">**PHP**: [Configure PHP in Azure App Service Web Apps](web-sites-php-configure.md).</span></span>
* <span data-ttu-id="9fdf9-133">**Python**: статья [Настройка Python в веб-приложениях службы приложений Azure](web-sites-python-configure.md)</span><span class="sxs-lookup"><span data-stu-id="9fdf9-133">**Python**: [Configuring Python with Azure App Service Web Apps](web-sites-python-configure.md)</span></span>

## <a name="while-your-web-app-is-running"></a><span data-ttu-id="9fdf9-134">В ходе эксплуатации веб-приложения</span><span class="sxs-lookup"><span data-stu-id="9fdf9-134">While your web app is running</span></span>
<span data-ttu-id="9fdf9-135">Во время веб-приложения необходимо убедиться, что он доступен и является toomeet пользовательский трафик toomake.</span><span class="sxs-lookup"><span data-stu-id="9fdf9-135">While your web app is running, you want toomake sure it is available, and that it scales toomeet user traffic.</span></span> <span data-ttu-id="9fdf9-136">Может также потребоваться tootroubleshoot ошибок.</span><span class="sxs-lookup"><span data-stu-id="9fdf9-136">You may also need tootroubleshoot errors.</span></span>

### <a name="monitoring"></a><span data-ttu-id="9fdf9-137">Мониторинг</span><span class="sxs-lookup"><span data-stu-id="9fdf9-137">Monitoring</span></span>
* <span data-ttu-id="9fdf9-138">Через hello портал Azure, вы можете [добавить метрики производительности](web-sites-monitor.md) как ЦП и число запросов клиентов.</span><span class="sxs-lookup"><span data-stu-id="9fdf9-138">Through hello Azure Portal, you can [add performance metrics](web-sites-monitor.md) such as CPU usage and number of client requests.</span></span>
* <span data-ttu-id="9fdf9-139">[Масштабирование веб-приложения](web-sites-scale.md) в tootraffic ответа.</span><span class="sxs-lookup"><span data-stu-id="9fdf9-139">[Scale your web app](web-sites-scale.md) in response tootraffic.</span></span> <span data-ttu-id="9fdf9-140">В зависимости от вашего уровня можно масштабировать число hello виртуальных машин и размер hello hello экземпляров виртуальных Машин.</span><span class="sxs-lookup"><span data-stu-id="9fdf9-140">Depending on your tier, you can scale hello number of VMs and/or hello size of hello VM instances.</span></span> <span data-ttu-id="9fdf9-141">В hello Standard и Premium уровней вы можно также настроить автоматическое масштабирование, поэтому веб-приложения автоматически масштабируется по фиксированному расписанию или в ответ tooload.</span><span class="sxs-lookup"><span data-stu-id="9fdf9-141">In hello Standard and Premium tiers, you can also set up autoscaling, so your web app scales automatically, either on a fixed schedule, or in response tooload.</span></span>  

### <a name="backups"></a><span data-ttu-id="9fdf9-142">Резервные копии</span><span class="sxs-lookup"><span data-stu-id="9fdf9-142">Backups</span></span>
* <span data-ttu-id="9fdf9-143">Настройка [автоматизированной архивации](web-sites-backup.md) для веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="9fdf9-143">Set [automatic backups](web-sites-backup.md) of your web app.</span></span> <span data-ttu-id="9fdf9-144">Дополнительные сведения об архивации см. в [этом видео](https://azure.microsoft.com/documentation/videos/azure-websites-automatic-and-easy-backup/).</span><span class="sxs-lookup"><span data-stu-id="9fdf9-144">Learn more about backups in [this video](https://azure.microsoft.com/documentation/videos/azure-websites-automatic-and-easy-backup/).</span></span>
* <span data-ttu-id="9fdf9-145">Сведения о способах hello [восстановление базы данных](../sql-database/sql-database-business-continuity.md) в базе данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="9fdf9-145">Learn about hello options for [database recovery](../sql-database/sql-database-business-continuity.md) in Azure SQL Database.</span></span>

### <a name="troubleshooting"></a><span data-ttu-id="9fdf9-146">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="9fdf9-146">Troubleshooting</span></span>
* <span data-ttu-id="9fdf9-147">Если что-то пойдет не так, вы можете [Устранение неполадок в Visual Studio](web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug), с помощью журналов диагностики и отладки в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="9fdf9-147">If something goes wrong, you can [troubleshoot in Visual Studio](web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug), using diagnostic logs and live debugging in hello cloud.</span></span> 
* <span data-ttu-id="9fdf9-148">За пределами Visual Studio существуют различные способы журналы диагностики toocollect.</span><span class="sxs-lookup"><span data-stu-id="9fdf9-148">Outside of Visual Studio, there are various ways toocollect diagnostic logs.</span></span> <span data-ttu-id="9fdf9-149">Ознакомьтесь со статьей [Включение ведения журнала диагностики для веб-приложений в службе приложений Azure](web-sites-enable-diagnostic-log.md).</span><span class="sxs-lookup"><span data-stu-id="9fdf9-149">See [Enable diagnostics logging for web apps in Azure App Service](web-sites-enable-diagnostic-log.md).</span></span>
* <span data-ttu-id="9fdf9-150">Для приложений Node.js. в разделе [как toodebug Node.js веб-приложения в службе приложений Azure](web-sites-nodejs-debug.md).</span><span class="sxs-lookup"><span data-stu-id="9fdf9-150">For Node.js applications, see [How toodebug a Node.js web app in Azure App Service](web-sites-nodejs-debug.md).</span></span>

### <a name="restoring-data"></a><span data-ttu-id="9fdf9-151">Восстановление данных</span><span class="sxs-lookup"><span data-stu-id="9fdf9-151">Restoring Data</span></span>
* <span data-ttu-id="9fdf9-152">[восстанавливать](web-sites-restore.md) из ранее созданных резервных копий.</span><span class="sxs-lookup"><span data-stu-id="9fdf9-152">[Restore](web-sites-restore.md) a web app that was previously backed up.</span></span>

## <a name="when-you-update-your-web-app"></a><span data-ttu-id="9fdf9-153">При обновлении веб-приложения</span><span class="sxs-lookup"><span data-stu-id="9fdf9-153">When you update your web app</span></span>
<span data-ttu-id="9fdf9-154">Если вы не включили автоматическое резервное копирование, то можете создавать резервные копии [вручную](web-sites-backup.md).</span><span class="sxs-lookup"><span data-stu-id="9fdf9-154">If you have not enabled automatic backups, you can create a [manual backup](web-sites-backup.md).</span></span>

<span data-ttu-id="9fdf9-155">Возможно, вас также заинтересует [промежуточное развертывание](web-sites-staged-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="9fdf9-155">Consider using [staged deployment](web-sites-staged-publishing.md).</span></span> <span data-ttu-id="9fdf9-156">Этот параметр позволяет публиковать обновления tooa промежуточное развертывание запускаемую side-by-side с производственного развертывания.</span><span class="sxs-lookup"><span data-stu-id="9fdf9-156">This option lets you publish updates tooa staging deployment that runs side-by-side with your production deployment.</span></span> 


<!-- Anchors. -->

[Before you deploy your site tooproduction]: #before-you-deploy-your-site-to-production
[While your website is running]: #while-your-website-is-running
[When you update your website]: #when-you-update-your-website


