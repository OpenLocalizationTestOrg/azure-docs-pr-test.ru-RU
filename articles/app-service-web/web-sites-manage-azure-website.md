---
title: "Управление веб-приложением в службе приложений Azure"
description: "Ссылки на ресурсы, посвященные управлению веб-приложением в службе приложений Azure."
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
ms.openlocfilehash: 9e19618a1b24bbdf3163ddfc3423c5c932dcd7af
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="manage-a-web-app-in-azure-app-service"></a><span data-ttu-id="e6219-103">Управление веб-приложением в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="e6219-103">Manage a web app in Azure App Service</span></span>
<span data-ttu-id="e6219-104">В этом разделе представлены ссылки на ресурсы, посвященные управлению веб-приложением в [службе приложений Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="e6219-104">This topic contains links to resources for managing a web app in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="e6219-105">Под управлением подразумеваются все задачи, направленные на обеспечение стабильной работы веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="e6219-105">Management includes all of the tasks that keep your web app running smoothly.</span></span> 

<span data-ttu-id="e6219-106">На различных этапах существования веб-приложения вам придется выполнять разные задачи управления, от первоначального развертывания до обычной эксплуатации, обслуживания и применения обновлений.</span><span class="sxs-lookup"><span data-stu-id="e6219-106">Over the lifetime of a web app, you will perform different management tasks, as you move from initial deployment to normal operation, maintenance, and updates.</span></span>

<span data-ttu-id="e6219-107">Многие задачи, связанные с управлением веб-приложением, можно выполнять на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="e6219-107">Many web app management tasks can be performed in the Azure Portal.</span></span>

## <a name="before-you-deploy-your-web-app-to-production"></a><span data-ttu-id="e6219-108">Перед развертыванием веб-приложения в рабочей среде</span><span class="sxs-lookup"><span data-stu-id="e6219-108">Before you deploy your web app to production</span></span>
### <a name="choose-a-tier"></a><span data-ttu-id="e6219-109">Выберите уровень.</span><span class="sxs-lookup"><span data-stu-id="e6219-109">Choose a tier</span></span>
<span data-ttu-id="e6219-110">Служба приложений Azure доступна для 5 уровней: Free, Shared, Basic, Standard и Premium.</span><span class="sxs-lookup"><span data-stu-id="e6219-110">Azure App Service is offered in five tiers: Free, Shared, Basic, Standard, and Premium.</span></span> <span data-ttu-id="e6219-111">Информацию о функциях и ценах для каждого уровня см. в разделе [Сведения о ценах](https://azure.microsoft.com/pricing/details/app-service/).</span><span class="sxs-lookup"><span data-stu-id="e6219-111">For information about the features and pricing for each tier, see [Pricing details](https://azure.microsoft.com/pricing/details/app-service/).</span></span> 

* <span data-ttu-id="e6219-112">[Планы службы приложений](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) позволяют группировать несколько веб-приложений на одном уровне.</span><span class="sxs-lookup"><span data-stu-id="e6219-112">[App Service plans](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) let you group multiple web apps under the same tier.</span></span>
* <span data-ttu-id="e6219-113">Всегда можно [сменить уровень](web-sites-scale.md) после создания веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="e6219-113">You can always [switch tiers](web-sites-scale.md) after you create your web app.</span></span>

### <a name="configuration"></a><span data-ttu-id="e6219-114">Конфигурация</span><span class="sxs-lookup"><span data-stu-id="e6219-114">Configuration</span></span>
<span data-ttu-id="e6219-115">На [портале Azure](https://portal.azure.com/) можно задать различные параметры конфигурации.</span><span class="sxs-lookup"><span data-stu-id="e6219-115">Use the [Azure Portal](https://portal.azure.com/) to set various configuration options.</span></span> <span data-ttu-id="e6219-116">Подробные сведения см. в разделе [Настройка веб-приложений в службе приложений Azure](web-sites-configure.md).</span><span class="sxs-lookup"><span data-stu-id="e6219-116">For details, see [Configure web apps in Azure App Service](web-sites-configure.md).</span></span> <span data-ttu-id="e6219-117">Вот краткий контрольный список:</span><span class="sxs-lookup"><span data-stu-id="e6219-117">Here is a quick checklist:</span></span>

* <span data-ttu-id="e6219-118">При необходимости выберите **версии сред выполнения** для .NET, PHP, Java или Python.</span><span class="sxs-lookup"><span data-stu-id="e6219-118">Select **runtime versions** for .NET, PHP, Java, or Python, if needed.</span></span>
* <span data-ttu-id="e6219-119">Если в веб-приложении используется протокол **WebSockets**, включите его поддержку.</span><span class="sxs-lookup"><span data-stu-id="e6219-119">Enable **WebSockets** if your web app uses the WebSocket protocol.</span></span> <span data-ttu-id="e6219-120">(Это относится к приложениям, которые используют [ASP.NET SignalR](http://www.asp.net/signalr) или [socket.io](web-sites-nodejs-chat-app-socketio.md).)</span><span class="sxs-lookup"><span data-stu-id="e6219-120">(This includes apps that use [ASP.NET SignalR](http://www.asp.net/signalr) or [socket.io](web-sites-nodejs-chat-app-socketio.md).)</span></span>
* <span data-ttu-id="e6219-121">Вы используете непрерывные веб-задания?</span><span class="sxs-lookup"><span data-stu-id="e6219-121">Are you running continuous web jobs?</span></span> <span data-ttu-id="e6219-122">Если да, то выберите параметр **Always On**(Всегда включено).</span><span class="sxs-lookup"><span data-stu-id="e6219-122">If so, enable **Always On**.</span></span>
* <span data-ttu-id="e6219-123">Задайте **документ по умолчанию**, например index.html.</span><span class="sxs-lookup"><span data-stu-id="e6219-123">Set the **default document**, such as index.html.</span></span>

<span data-ttu-id="e6219-124">Помимо этих базовых параметров конфигурации, вы также можете настроить следующее:</span><span class="sxs-lookup"><span data-stu-id="e6219-124">In addition to these basic configuration settings, you may want to configure the following:</span></span>

* <span data-ttu-id="e6219-125">Шифрование **SSL**.</span><span class="sxs-lookup"><span data-stu-id="e6219-125">**Secure Socket Layer (SSL)** encryption.</span></span> <span data-ttu-id="e6219-126">Чтобы использовать SSL с пользовательским доменным именем, вам необходимо получить SSL-сертификат и настроить веб-приложение для работы с ним.</span><span class="sxs-lookup"><span data-stu-id="e6219-126">To use SSL with a custom domain name, you must get an SSL certificate and configure your web app to use it.</span></span> <span data-ttu-id="e6219-127">Ознакомьтесь со статьей [Включение протокола HTTPS для веб-приложения в службе приложений Azure](app-service-web-tutorial-custom-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="e6219-127">See [Enable HTTPS for a web app in Azure App Service](app-service-web-tutorial-custom-ssl.md).</span></span>
* <span data-ttu-id="e6219-128">**Имя личного домена**.</span><span class="sxs-lookup"><span data-stu-id="e6219-128">**Custom domain name.**</span></span> <span data-ttu-id="e6219-129">Вашему веб-приложению автоматически присваивается дочерний домен в azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="e6219-129">Your web app automatically has a subdomain under azurewebsites.net.</span></span> <span data-ttu-id="e6219-130">Вы можете связать сайт с пользовательским доменным именем, например contoso.com.</span><span class="sxs-lookup"><span data-stu-id="e6219-130">You can associate a custom domain name, such as contoso.com.</span></span> <span data-ttu-id="e6219-131">Ознакомьтесь со статьей [Настройка личного доменного имени для службы приложений Azure](app-service-web-tutorial-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="e6219-131">See [Configure a custom domain name in Azure App Service](app-service-web-tutorial-custom-domain.md).</span></span>

<span data-ttu-id="e6219-132">Настройка для определенных языков программирования:</span><span class="sxs-lookup"><span data-stu-id="e6219-132">Language-specific configuration:</span></span>

* <span data-ttu-id="e6219-133">**PHP**: статья [Настройка PHP в веб-приложениях службы приложений Azure](web-sites-php-configure.md).</span><span class="sxs-lookup"><span data-stu-id="e6219-133">**PHP**: [Configure PHP in Azure App Service Web Apps](web-sites-php-configure.md).</span></span>
* <span data-ttu-id="e6219-134">**Python**: статья [Настройка Python в веб-приложениях службы приложений Azure](web-sites-python-configure.md)</span><span class="sxs-lookup"><span data-stu-id="e6219-134">**Python**: [Configuring Python with Azure App Service Web Apps](web-sites-python-configure.md)</span></span>

## <a name="while-your-web-app-is-running"></a><span data-ttu-id="e6219-135">В ходе эксплуатации веб-приложения</span><span class="sxs-lookup"><span data-stu-id="e6219-135">While your web app is running</span></span>
<span data-ttu-id="e6219-136">В ходе эксплуатации веб-приложения важно, чтобы оно всегда было доступно, а его ресурсы масштабировались с учетом пользовательского трафика.</span><span class="sxs-lookup"><span data-stu-id="e6219-136">While your web app is running, you want to make sure it is available, and that it scales to meet user traffic.</span></span> <span data-ttu-id="e6219-137">Кроме того, возможно, вам придется устранять возникающие неполадки.</span><span class="sxs-lookup"><span data-stu-id="e6219-137">You may also need to troubleshoot errors.</span></span>

### <a name="monitoring"></a><span data-ttu-id="e6219-138">Мониторинг</span><span class="sxs-lookup"><span data-stu-id="e6219-138">Monitoring</span></span>
* <span data-ttu-id="e6219-139">На портале Azure можно [добавить показатели производительности](web-sites-monitor.md) , например показатель использования ЦП и количество запросов от клиентов.</span><span class="sxs-lookup"><span data-stu-id="e6219-139">Through the Azure Portal, you can [add performance metrics](web-sites-monitor.md) such as CPU usage and number of client requests.</span></span>
* <span data-ttu-id="e6219-140">[Ресурсы веб-сайта можно масштабировать](web-sites-scale.md) с учетом трафика.</span><span class="sxs-lookup"><span data-stu-id="e6219-140">[Scale your web app](web-sites-scale.md) in response to traffic.</span></span> <span data-ttu-id="e6219-141">В зависимости от уровня плана размещения можно изменять количество виртуальных машин и (или) размер экземпляров виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="e6219-141">Depending on your tier, you can scale the number of VMs and/or the size of the VM instances.</span></span> <span data-ttu-id="e6219-142">На уровнях Standard и Premium вы также можете настроить автоматическое масштабирование веб-приложения по заданному графику или с учетом нагрузки.</span><span class="sxs-lookup"><span data-stu-id="e6219-142">In the Standard and Premium tiers, you can also set up autoscaling, so your web app scales automatically, either on a fixed schedule, or in response to load.</span></span>  

### <a name="backups"></a><span data-ttu-id="e6219-143">Резервные копии</span><span class="sxs-lookup"><span data-stu-id="e6219-143">Backups</span></span>
* <span data-ttu-id="e6219-144">Настройка [автоматизированной архивации](web-sites-backup.md) для веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="e6219-144">Set [automatic backups](web-sites-backup.md) of your web app.</span></span> <span data-ttu-id="e6219-145">Дополнительные сведения об архивации см. в [этом видео](https://azure.microsoft.com/documentation/videos/azure-websites-automatic-and-easy-backup/).</span><span class="sxs-lookup"><span data-stu-id="e6219-145">Learn more about backups in [this video](https://azure.microsoft.com/documentation/videos/azure-websites-automatic-and-easy-backup/).</span></span>
* <span data-ttu-id="e6219-146">Ознакомьтесь с параметрами [восстановления базы данных](../sql-database/sql-database-business-continuity.md) SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="e6219-146">Learn about the options for [database recovery](../sql-database/sql-database-business-continuity.md) in Azure SQL Database.</span></span>

### <a name="troubleshooting"></a><span data-ttu-id="e6219-147">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="e6219-147">Troubleshooting</span></span>
* <span data-ttu-id="e6219-148">Возникающие неполадки можно [устранять в Visual Studio](web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug)с помощью журналов диагностики и отладки в облаке в режиме реального времени.</span><span class="sxs-lookup"><span data-stu-id="e6219-148">If something goes wrong, you can [troubleshoot in Visual Studio](web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug), using diagnostic logs and live debugging in the cloud.</span></span> 
* <span data-ttu-id="e6219-149">Кроме того, журналы диагностики можно собирать различными способами не только в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e6219-149">Outside of Visual Studio, there are various ways to collect diagnostic logs.</span></span> <span data-ttu-id="e6219-150">Ознакомьтесь со статьей [Включение ведения журнала диагностики для веб-приложений в службе приложений Azure](web-sites-enable-diagnostic-log.md).</span><span class="sxs-lookup"><span data-stu-id="e6219-150">See [Enable diagnostics logging for web apps in Azure App Service](web-sites-enable-diagnostic-log.md).</span></span>
* <span data-ttu-id="e6219-151">Работа с приложениями Node.js описана в разделе [Отладка веб-приложения Node.js в службе приложений Azure](web-sites-nodejs-debug.md).</span><span class="sxs-lookup"><span data-stu-id="e6219-151">For Node.js applications, see [How to debug a Node.js web app in Azure App Service](web-sites-nodejs-debug.md).</span></span>

### <a name="restoring-data"></a><span data-ttu-id="e6219-152">Восстановление данных</span><span class="sxs-lookup"><span data-stu-id="e6219-152">Restoring Data</span></span>
* <span data-ttu-id="e6219-153">[восстанавливать](web-sites-restore.md) из ранее созданных резервных копий.</span><span class="sxs-lookup"><span data-stu-id="e6219-153">[Restore](web-sites-restore.md) a web app that was previously backed up.</span></span>

## <a name="when-you-update-your-web-app"></a><span data-ttu-id="e6219-154">При обновлении веб-приложения</span><span class="sxs-lookup"><span data-stu-id="e6219-154">When you update your web app</span></span>
<span data-ttu-id="e6219-155">Если вы не включили автоматическое резервное копирование, то можете создавать резервные копии [вручную](web-sites-backup.md).</span><span class="sxs-lookup"><span data-stu-id="e6219-155">If you have not enabled automatic backups, you can create a [manual backup](web-sites-backup.md).</span></span>

<span data-ttu-id="e6219-156">Возможно, вас также заинтересует [промежуточное развертывание](web-sites-staged-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="e6219-156">Consider using [staged deployment](web-sites-staged-publishing.md).</span></span> <span data-ttu-id="e6219-157">С его помощью вы сможете публиковать обновления в промежуточной среде, функционирующей параллельно с рабочей.</span><span class="sxs-lookup"><span data-stu-id="e6219-157">This option lets you publish updates to a staging deployment that runs side-by-side with your production deployment.</span></span> 


<!-- Anchors. -->

[Before you deploy your site to production]: #before-you-deploy-your-site-to-production
[While your website is running]: #while-your-website-is-running
[When you update your website]: #when-you-update-your-website


