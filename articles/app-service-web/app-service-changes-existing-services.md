---
title: "aaaAzure приложения службы и ее влияние на существующие службы Azure"
description: "Объясняет, как hello новые службы приложений Azure и его возможности повлиять на существующие службы в Azure."
services: app-service
documentationcenter: 
author: yochay
manager: nirma
editor: 
ms.assetid: 86c6a292-3c33-49f4-890c-89cc0321b397
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/12/2016
ms.author: yochaykk
ms.openlocfilehash: a831a88fee38465e5b0b7c2c2340cf8a0d64c864
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-and-existing-azure-services"></a><span data-ttu-id="4dd7b-103">Служба приложений Azure и существующие службы Azure</span><span class="sxs-lookup"><span data-stu-id="4dd7b-103">Azure App Service and existing Azure services</span></span>
<span data-ttu-id="4dd7b-104">В этой статье рассматриваются службы Azure в рамках toobring изменение hello вместе несколько служб Azure в tooexisting изменения hello [службе приложений Azure](https://azure.microsoft.com/services/app-service/), новое предложение интеграции.</span><span class="sxs-lookup"><span data-stu-id="4dd7b-104">This article outlines hello changes tooexisting Azure services as part of hello change toobring together several Azure services into [Azure App Service](https://azure.microsoft.com/services/app-service/), a new integrated offering.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="overview"></a><span data-ttu-id="4dd7b-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="4dd7b-105">Overview</span></span>
<span data-ttu-id="4dd7b-106">[Служба приложений Azure](https://azure.microsoft.com/services/app-service/) — это новыми и уникальными облачная служба, которая позволяет разработчикам toocreate web и мобильных приложений для любых платформ и с любого устройства.</span><span class="sxs-lookup"><span data-stu-id="4dd7b-106">[Azure App Service](https://azure.microsoft.com/services/app-service/) is a new and unique cloud service that enables developers toocreate web and mobile apps for any platform and any device.</span></span> <span data-ttu-id="4dd7b-107">Служба приложений — toostreamline интегрированного решения предназначены повторные кодирования функции, интегрировать с enterprise и системой SaaS и автоматизации бизнес-процессов, обеспечивая соответствие требованиям к безопасности, надежность и масштабируемость.</span><span class="sxs-lookup"><span data-stu-id="4dd7b-107">App Service is an integrated solution designed toostreamline repeated coding functions, integrate with enterprise and SaaS systems, and automate business processes while meeting your needs for security, reliability, and scalability.</span></span>

<span data-ttu-id="4dd7b-108">Службы приложений объединяет в себе hello следующие существующие Azure службы - [веб-сайтов](https://azure.microsoft.com/services/websites/), [мобильных служб](https://azure.microsoft.com/services/mobile-services/), и [службы Biztalk](https://azure.microsoft.com/services/biztalk-services/) в одном сочетании службы, во время Добавление новой возможности.</span><span class="sxs-lookup"><span data-stu-id="4dd7b-108">App Service brings together hello following existing Azure services - [Websites](https://azure.microsoft.com/services/websites/), [Mobile Services](https://azure.microsoft.com/services/mobile-services/), and [Biztalk Services](https://azure.microsoft.com/services/biztalk-services/) into a single combined service, while adding powerful new capabilities.</span></span>  <span data-ttu-id="4dd7b-109">Службы приложений позволяет hello toohost следующие типы приложения:</span><span class="sxs-lookup"><span data-stu-id="4dd7b-109">App Service allows you toohost hello following app types:</span></span>

* <span data-ttu-id="4dd7b-110">Веб-приложения</span><span class="sxs-lookup"><span data-stu-id="4dd7b-110">Web Apps</span></span>
* <span data-ttu-id="4dd7b-111">Мобильные приложения</span><span class="sxs-lookup"><span data-stu-id="4dd7b-111">Mobile Apps</span></span>
* <span data-ttu-id="4dd7b-112">Приложения API</span><span class="sxs-lookup"><span data-stu-id="4dd7b-112">API Apps</span></span>
* <span data-ttu-id="4dd7b-113">Logic Apps</span><span class="sxs-lookup"><span data-stu-id="4dd7b-113">Logic Apps</span></span>

<span data-ttu-id="4dd7b-114">Hello следующей таблице объясняется, как существующие Azure службы сопоставления tooApp службы и hello приложения типы, доступные в нем.</span><span class="sxs-lookup"><span data-stu-id="4dd7b-114">hello following table explains how existing Azure services map tooApp Service and hello app types available within it.</span></span>

<table>
<thead>
<tr class="header">
<th align="left", style="width:10%"><span data-ttu-id="4dd7b-115">Существующая служба Azure</span><span class="sxs-lookup"><span data-stu-id="4dd7b-115">Existing Azure Service</span></span></th>
<th align="left", style="width:10%"><span data-ttu-id="4dd7b-116">Служба приложений Azure</span><span class="sxs-lookup"><span data-stu-id="4dd7b-116">Azure App Service</span></span></th>
<th align="left", style="width:80%"><span data-ttu-id="4dd7b-117">Изменения</span><span class="sxs-lookup"><span data-stu-id="4dd7b-117">What changed</span></span></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><span data-ttu-id="4dd7b-118">Веб-сайты Azure</span><span class="sxs-lookup"><span data-stu-id="4dd7b-118">Azure Websites</span></span></td>
<td align="left"><span data-ttu-id="4dd7b-119">Веб-приложения</span><span class="sxs-lookup"><span data-stu-id="4dd7b-119">Web Apps</span></span></td>
<td align="left"><li><span data-ttu-id="4dd7b-120">Для веб-сайтов Azure службы приложений — строго ограниченный toochanging hello имя веб-сайтов tooWeb приложений.</span><span class="sxs-lookup"><span data-stu-id="4dd7b-120">For Azure Websites, App Service is strictly limited toochanging hello name  Websites tooWeb Apps.</span></span>
<p><li><span data-ttu-id="4dd7b-121">Это касается всех существующих экземпляров веб-сайтов в службе приложений.</span><span class="sxs-lookup"><span data-stu-id="4dd7b-121">All your existing instances of Websites are now Web Apps in App Service.</span></span></p>
<p><li><span data-ttu-id="4dd7b-122">Можно открыть существующий веб-сайтов через hello <a href="http://go.microsoft.com/fwlink/?LinkId=529715">портала Azure</a>, где вы найдете всех существующих узлов под <em>веб-приложений</em>.</span><span class="sxs-lookup"><span data-stu-id="4dd7b-122">You can access your existing websites via hello <a href="http://go.microsoft.com/fwlink/?LinkId=529715">Azure Portal</a>, where you will find all your existing sites under <em>Web Apps</em>.</span></span></p>
<p><li><span data-ttu-id="4dd7b-123"><em>Веб-план хостинга</em> теперь <em>план служб приложений</em>.</span><span class="sxs-lookup"><span data-stu-id="4dd7b-123"><em>Web Hosting Plan</em> is now <em>App Service Plan</em>.</span></span> <span data-ttu-id="4dd7b-124"><em>План службы приложений</em> может размещать любые типы приложений службы приложений, такие как веб-приложения, мобильные приложения, приложения логики или приложения API.</span><span class="sxs-lookup"><span data-stu-id="4dd7b-124">An <em>App Service Plan</em> can host any app type of App Service, such as Web, Mobile, Logic, or API apps.</span></span></p>
<p><li><span data-ttu-id="4dd7b-125">Веб-приложения службы приложений Azure находятся в состоянии общедоступной версии.</span><span class="sxs-lookup"><span data-stu-id="4dd7b-125">Azure App Service Web Apps is in General Availability.</span></span></p>
<p><li><span data-ttu-id="4dd7b-126"><a href="http://azure.microsoft.com/services/app-service/web/">Дополнительные сведения о веб-приложений</a>.</span><span class="sxs-lookup"><span data-stu-id="4dd7b-126"><a href="http://azure.microsoft.com/services/app-service/web/">Learn more about Web Apps</a>.</span></span></p></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="4dd7b-127">Мобильные службы Azure</span><span class="sxs-lookup"><span data-stu-id="4dd7b-127">Azure Mobile Services</span></span></td>
<td align="left"><span data-ttu-id="4dd7b-128">Мобильные приложения</span><span class="sxs-lookup"><span data-stu-id="4dd7b-128">Mobile Apps</span></span></td>
<td align="left"><p><li><span data-ttu-id="4dd7b-129">Мобильные службы продолжить toobe доступен в качестве автономной службы и остаются полностью поддерживается.</span><span class="sxs-lookup"><span data-stu-id="4dd7b-129">Mobile Services continue toobe available as a standalone service and remain fully supported.</span></span></p>
<p><li><span data-ttu-id="4dd7b-130">Мобильные приложения — это тип приложения в службе приложений, который интегрирует все функции hello мобильных служб и многое другое.</span><span class="sxs-lookup"><span data-stu-id="4dd7b-130">Mobile Apps is an app type in App Service, which integrates all of hello functionality of Mobile Services and more.</span></span></p>
<p><li><span data-ttu-id="4dd7b-131">Можно легко слишком<a href="http://go.microsoft.com/fwlink/?LinkID=724279&clcid=0x409">миграции из мобильных служб tooMobile приложения</a>.</span><span class="sxs-lookup"><span data-stu-id="4dd7b-131">It is easy too<a href="http://go.microsoft.com/fwlink/?LinkID=724279&clcid=0x409">migrate from Mobile Services tooMobile Apps</a>.</span></span></p>
<p><li><span data-ttu-id="4dd7b-132">В составе службы приложений мобильные приложения получили новые возможности за рамками мобильных служб, такие как интеграция с локальной системой и системой SaaS, промежуточные слоты, веб-задания, улучшенные варианты масштабирования и многое другое.</span><span class="sxs-lookup"><span data-stu-id="4dd7b-132">As part of App Service, Mobile Apps get new capabilities beyond Mobile Services, such as  integration with on-premises and SaaS systems, staging slots, WebJobs, better scaling options, and more.</span></span></p>
<p><li><span data-ttu-id="4dd7b-133"><a href="http://azure.microsoft.com/services/app-service/mobile/">Дополнительные сведения о мобильных приложениях</a>.</span><span class="sxs-lookup"><span data-stu-id="4dd7b-133"><a href="http://azure.microsoft.com/services/app-service/mobile/">Learn more about Mobile Apps</a>.</span></span></p>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"><span data-ttu-id="4dd7b-134">Приложения API</span><span class="sxs-lookup"><span data-stu-id="4dd7b-134">API Apps</span></span></td>
<td align="left">
<p><li><span data-ttu-id="4dd7b-135">Приложения API — это новый тип приложения, в службе приложений, который позволяет легко создавать и использовать интерфейсы API в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="4dd7b-135">API Apps is a new app type in App Service that lets you easily build and consume APIs in hello cloud.</span></span></p>
<p><li><span data-ttu-id="4dd7b-136"><a href="http://azure.microsoft.com/services/app-service/api/">Узнайте больше о приложениях API</a>.</span><span class="sxs-lookup"><span data-stu-id="4dd7b-136"><a href="http://azure.microsoft.com/services/app-service/api/">Learn more about API Apps</a>.</span></span></p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><span data-ttu-id="4dd7b-137">Logic Apps</span><span class="sxs-lookup"><span data-stu-id="4dd7b-137">Logic Apps</span></span></td>
<td align="left">
<p><li><span data-ttu-id="4dd7b-138">Приложения логики представляют новый тип приложений в службе приложений, позволяющий легко автоматизировать бизнес-процесс.</span><span class="sxs-lookup"><span data-stu-id="4dd7b-138">Logic Apps is a new app type in App Service that lets you easily automate business processes.</span></span></p>
<p><li><span data-ttu-id="4dd7b-139"><a href="http://azure.microsoft.com/services/app-service/logic/">Дополнительные сведения о приложении логики</a>.</span><span class="sxs-lookup"><span data-stu-id="4dd7b-139"><a href="http://azure.microsoft.com/services/app-service/logic/">Learn more about Logic Apps</a>.</span></span></p></td>
</tr>
<tr class="odd">
<td align="left"><span data-ttu-id="4dd7b-140">Службы Azure BizTalk</span><span class="sxs-lookup"><span data-stu-id="4dd7b-140">Azure BizTalk Services</span></span></td>
<td align="left"><span data-ttu-id="4dd7b-141">Приложения API BizTalk</span><span class="sxs-lookup"><span data-stu-id="4dd7b-141">BizTalk API Apps</span></span></td>
<td align="left">
<li><p><span data-ttu-id="4dd7b-142">Службы BizTalk продолжить toobe доступен в качестве автономной службы и остаются полностью поддерживается.</span><span class="sxs-lookup"><span data-stu-id="4dd7b-142">BizTalk Services continue toobe available as a standalone service and remain fully supported.</span></span></p>
<li><p><span data-ttu-id="4dd7b-143">Все возможности hello служб BizTalk интегрированы в службы приложения как приложения API Включение пользователей tooperform интеграция приложений и сценариев интеграции B2B с одним из типов приложения hello в службе приложений.</span><span class="sxs-lookup"><span data-stu-id="4dd7b-143">All hello capabilities of BizTalk Services are integrated into App Service as API Apps enabling users tooperform enterprise application integration and B2B integration scenarios with any of hello app types in App Service.</span></span></p>
<li><p><span data-ttu-id="4dd7b-144">С приложениями логики теперь можно автоматизировать бизнес-процессов с помощью рабочих процессов toocreate визуального проектирования качества.</span><span class="sxs-lookup"><span data-stu-id="4dd7b-144">With Logic Apps, you can now automate business processes using a visual design experience toocreate workflows.</span></span></p></td>
</tr>
</tbody>
</table>

<span data-ttu-id="4dd7b-145">toolearn более, перейдите на страницу [документации службы приложений](https://azure.microsoft.com/documentation/services/app-service/).</span><span class="sxs-lookup"><span data-stu-id="4dd7b-145">toolearn more, please visit [App Service documentation](https://azure.microsoft.com/documentation/services/app-service/).</span></span>

