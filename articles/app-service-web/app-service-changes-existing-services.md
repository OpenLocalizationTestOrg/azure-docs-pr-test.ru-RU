---
title: "Служба приложений Azure и ее влияние на существующие службы Azure"
description: "В этом разделе объясняется, как новая служба приложений Azure и ее функциональные возможности влияют на существующие службы в Azure."
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
ms.openlocfilehash: ed967fda7a216ed49532be54228ebe888cf16b6f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="azure-app-service-and-existing-azure-services"></a><span data-ttu-id="2a7b1-103">Служба приложений Azure и существующие службы Azure</span><span class="sxs-lookup"><span data-stu-id="2a7b1-103">Azure App Service and existing Azure services</span></span>
<span data-ttu-id="2a7b1-104">В этой статье описаны изменения в существующих службах Azure, возникающие в процессе объединения нескольких служб Azure в [службу приложений Azure](https://azure.microsoft.com/services/app-service/), представляющую собой новое интегрированное решение.</span><span class="sxs-lookup"><span data-stu-id="2a7b1-104">This article outlines the changes to existing Azure services as part of the change to bring together several Azure services into [Azure App Service](https://azure.microsoft.com/services/app-service/), a new integrated offering.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="overview"></a><span data-ttu-id="2a7b1-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="2a7b1-105">Overview</span></span>
<span data-ttu-id="2a7b1-106">[Служба приложений Azure](https://azure.microsoft.com/services/app-service/) — это новая и уникальная облачная служба, которая позволяет разработчикам создавать веб-приложения и мобильные приложения для любой платформы и любого устройства.</span><span class="sxs-lookup"><span data-stu-id="2a7b1-106">[Azure App Service](https://azure.microsoft.com/services/app-service/) is a new and unique cloud service that enables developers to create web and mobile apps for any platform and any device.</span></span> <span data-ttu-id="2a7b1-107">Служба приложений — это интегрированное решение, призванное упростить повторное использование функций в коде, реализовать интеграцию с системами SaaS и корпоративными системами, обеспечить автоматизацию бизнес-процессов, одновременно удовлетворяя ваши потребности в безопасности, надежности и масштабируемости.</span><span class="sxs-lookup"><span data-stu-id="2a7b1-107">App Service is an integrated solution designed to streamline repeated coding functions, integrate with enterprise and SaaS systems, and automate business processes while meeting your needs for security, reliability, and scalability.</span></span>

<span data-ttu-id="2a7b1-108">Служба приложений объединяет следующие существующие службы Azure — [Веб-сайты](https://azure.microsoft.com/services/websites/), [мобильные службы](https://azure.microsoft.com/services/mobile-services/) и [службы Biztalk](https://azure.microsoft.com/services/biztalk-services/) — в единую службу, а также добавляет новые эффективные возможности.</span><span class="sxs-lookup"><span data-stu-id="2a7b1-108">App Service brings together the following existing Azure services - [Websites](https://azure.microsoft.com/services/websites/), [Mobile Services](https://azure.microsoft.com/services/mobile-services/), and [Biztalk Services](https://azure.microsoft.com/services/biztalk-services/) into a single combined service, while adding powerful new capabilities.</span></span>  <span data-ttu-id="2a7b1-109">Служба приложений позволяет разместить следующие типы приложений.</span><span class="sxs-lookup"><span data-stu-id="2a7b1-109">App Service allows you to host the following app types:</span></span>

* <span data-ttu-id="2a7b1-110">Веб-приложения</span><span class="sxs-lookup"><span data-stu-id="2a7b1-110">Web Apps</span></span>
* <span data-ttu-id="2a7b1-111">Мобильные приложения</span><span class="sxs-lookup"><span data-stu-id="2a7b1-111">Mobile Apps</span></span>
* <span data-ttu-id="2a7b1-112">Приложения API</span><span class="sxs-lookup"><span data-stu-id="2a7b1-112">API Apps</span></span>
* <span data-ttu-id="2a7b1-113">Приложения логики</span><span class="sxs-lookup"><span data-stu-id="2a7b1-113">Logic Apps</span></span>

<span data-ttu-id="2a7b1-114">В следующей таблице показано, как существующие службы Azure сопоставляются со службой приложений, а также описаны все доступные в ней типы приложений.</span><span class="sxs-lookup"><span data-stu-id="2a7b1-114">The following table explains how existing Azure services map to App Service and the app types available within it.</span></span>

<table>
<thead>
<tr class="header">
<th align="left", style="width:10%"><span data-ttu-id="2a7b1-115">Существующая служба Azure</span><span class="sxs-lookup"><span data-stu-id="2a7b1-115">Existing Azure Service</span></span></th>
<th align="left", style="width:10%"><span data-ttu-id="2a7b1-116">Служба приложений Azure</span><span class="sxs-lookup"><span data-stu-id="2a7b1-116">Azure App Service</span></span></th>
<th align="left", style="width:80%"><span data-ttu-id="2a7b1-117">Изменения</span><span class="sxs-lookup"><span data-stu-id="2a7b1-117">What changed</span></span></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><span data-ttu-id="2a7b1-118">Веб-сайты Azure</span><span class="sxs-lookup"><span data-stu-id="2a7b1-118">Azure Websites</span></span></td>
<td align="left"><span data-ttu-id="2a7b1-119">Веб-приложения</span><span class="sxs-lookup"><span data-stu-id="2a7b1-119">Web Apps</span></span></td>
<td align="left"><li><span data-ttu-id="2a7b1-120">Для веб-сайтов Azure влияние службы приложений ограничено лишь изменением названия "Веб-сайты" на "Веб-приложения".</span><span class="sxs-lookup"><span data-stu-id="2a7b1-120">For Azure Websites, App Service is strictly limited to changing the name  Websites to Web Apps.</span></span>
<p><li><span data-ttu-id="2a7b1-121">Это касается всех существующих экземпляров веб-сайтов в службе приложений.</span><span class="sxs-lookup"><span data-stu-id="2a7b1-121">All your existing instances of Websites are now Web Apps in App Service.</span></span></p>
<p><li><span data-ttu-id="2a7b1-122">Вы можете получить доступ к своим существующим веб-сайтам через <a href="http://go.microsoft.com/fwlink/?LinkId=529715">портал Azure</a>, где можно найти все существующие сайты в разделе <em>Веб-приложения</em>.</span><span class="sxs-lookup"><span data-stu-id="2a7b1-122">You can access your existing websites via the <a href="http://go.microsoft.com/fwlink/?LinkId=529715">Azure Portal</a>, where you will find all your existing sites under <em>Web Apps</em>.</span></span></p>
<p><li><span data-ttu-id="2a7b1-123"><em>Веб-план хостинга</em> теперь <em>план служб приложений</em>.</span><span class="sxs-lookup"><span data-stu-id="2a7b1-123"><em>Web Hosting Plan</em> is now <em>App Service Plan</em>.</span></span> <span data-ttu-id="2a7b1-124"><em>План службы приложений</em> может размещать любые типы приложений службы приложений, такие как веб-приложения, мобильные приложения, приложения логики или приложения API.</span><span class="sxs-lookup"><span data-stu-id="2a7b1-124">An <em>App Service Plan</em> can host any app type of App Service, such as Web, Mobile, Logic, or API apps.</span></span></p>
<p><li><span data-ttu-id="2a7b1-125">Веб-приложения службы приложений Azure находятся в состоянии общедоступной версии.</span><span class="sxs-lookup"><span data-stu-id="2a7b1-125">Azure App Service Web Apps is in General Availability.</span></span></p>
<p><li><span data-ttu-id="2a7b1-126"><a href="http://azure.microsoft.com/services/app-service/web/">Дополнительные сведения о веб-приложений</a>.</span><span class="sxs-lookup"><span data-stu-id="2a7b1-126"><a href="http://azure.microsoft.com/services/app-service/web/">Learn more about Web Apps</a>.</span></span></p></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="2a7b1-127">Мобильные службы Azure</span><span class="sxs-lookup"><span data-stu-id="2a7b1-127">Azure Mobile Services</span></span></td>
<td align="left"><span data-ttu-id="2a7b1-128">Мобильные приложения</span><span class="sxs-lookup"><span data-stu-id="2a7b1-128">Mobile Apps</span></span></td>
<td align="left"><p><li><span data-ttu-id="2a7b1-129">Мобильные службы по-прежнему доступны в качестве автономной службы и полностью поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="2a7b1-129">Mobile Services continue to be available as a standalone service and remain fully supported.</span></span></p>
<p><li><span data-ttu-id="2a7b1-130">Мобильные приложения — это приложения службы приложений, которые включают в себя все функциональные возможности мобильных служб и многое другое.</span><span class="sxs-lookup"><span data-stu-id="2a7b1-130">Mobile Apps is an app type in App Service, which integrates all of the functionality of Mobile Services and more.</span></span></p>
<p><li><span data-ttu-id="2a7b1-131">Вы можете легко <a href="http://go.microsoft.com/fwlink/?LinkID=724279&clcid=0x409">перейти от мобильных служб к мобильным приложениям</a>.</span><span class="sxs-lookup"><span data-stu-id="2a7b1-131">It is easy to <a href="http://go.microsoft.com/fwlink/?LinkID=724279&clcid=0x409">migrate from Mobile Services to Mobile Apps</a>.</span></span></p>
<p><li><span data-ttu-id="2a7b1-132">В составе службы приложений мобильные приложения получили новые возможности за рамками мобильных служб, такие как интеграция с локальной системой и системой SaaS, промежуточные слоты, веб-задания, улучшенные варианты масштабирования и многое другое.</span><span class="sxs-lookup"><span data-stu-id="2a7b1-132">As part of App Service, Mobile Apps get new capabilities beyond Mobile Services, such as  integration with on-premises and SaaS systems, staging slots, WebJobs, better scaling options, and more.</span></span></p>
<p><li><span data-ttu-id="2a7b1-133"><a href="http://azure.microsoft.com/services/app-service/mobile/">Дополнительные сведения о мобильных приложениях</a>.</span><span class="sxs-lookup"><span data-stu-id="2a7b1-133"><a href="http://azure.microsoft.com/services/app-service/mobile/">Learn more about Mobile Apps</a>.</span></span></p>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"><span data-ttu-id="2a7b1-134">Приложения API</span><span class="sxs-lookup"><span data-stu-id="2a7b1-134">API Apps</span></span></td>
<td align="left">
<p><li><span data-ttu-id="2a7b1-135">Приложения API представляют новый тип приложений в службе приложений, позволяющий легко создавать и использовать интерфейсы API в облаке.</span><span class="sxs-lookup"><span data-stu-id="2a7b1-135">API Apps is a new app type in App Service that lets you easily build and consume APIs in the cloud.</span></span></p>
<p><li><span data-ttu-id="2a7b1-136"><a href="http://azure.microsoft.com/services/app-service/api/">Узнайте больше о приложениях API</a>.</span><span class="sxs-lookup"><span data-stu-id="2a7b1-136"><a href="http://azure.microsoft.com/services/app-service/api/">Learn more about API Apps</a>.</span></span></p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><span data-ttu-id="2a7b1-137">Logic Apps</span><span class="sxs-lookup"><span data-stu-id="2a7b1-137">Logic Apps</span></span></td>
<td align="left">
<p><li><span data-ttu-id="2a7b1-138">Приложения логики представляют новый тип приложений в службе приложений, позволяющий легко автоматизировать бизнес-процесс.</span><span class="sxs-lookup"><span data-stu-id="2a7b1-138">Logic Apps is a new app type in App Service that lets you easily automate business processes.</span></span></p>
<p><li><span data-ttu-id="2a7b1-139"><a href="http://azure.microsoft.com/services/app-service/logic/">Дополнительные сведения о приложении логики</a>.</span><span class="sxs-lookup"><span data-stu-id="2a7b1-139"><a href="http://azure.microsoft.com/services/app-service/logic/">Learn more about Logic Apps</a>.</span></span></p></td>
</tr>
<tr class="odd">
<td align="left"><span data-ttu-id="2a7b1-140">Службы Azure BizTalk</span><span class="sxs-lookup"><span data-stu-id="2a7b1-140">Azure BizTalk Services</span></span></td>
<td align="left"><span data-ttu-id="2a7b1-141">Приложения API BizTalk</span><span class="sxs-lookup"><span data-stu-id="2a7b1-141">BizTalk API Apps</span></span></td>
<td align="left">
<li><p><span data-ttu-id="2a7b1-142">Службы BizTalk по-прежнему доступны в качестве автономной службы и полностью поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="2a7b1-142">BizTalk Services continue to be available as a standalone service and remain fully supported.</span></span></p>
<li><p><span data-ttu-id="2a7b1-143">Все возможности служб BizTalk интегрированы в службу приложений как приложения API, предоставляющие пользователям возможность выполнять интеграцию корпоративных приложений и реализовывать сценарии интеграции B2B с приложениями любых типов в службе приложений.</span><span class="sxs-lookup"><span data-stu-id="2a7b1-143">All the capabilities of BizTalk Services are integrated into App Service as API Apps enabling users to perform enterprise application integration and B2B integration scenarios with any of the app types in App Service.</span></span></p>
<li><p><span data-ttu-id="2a7b1-144">Благодаря Logic Apps теперь можно автоматизировать бизнес-процессы, используя возможности визуального проектирования для создания рабочих процессов.</span><span class="sxs-lookup"><span data-stu-id="2a7b1-144">With Logic Apps, you can now automate business processes using a visual design experience to create workflows.</span></span></p></td>
</tr>
</tbody>
</table>

<span data-ttu-id="2a7b1-145">Дополнительные сведения см. в [документации по службе приложений](https://azure.microsoft.com/documentation/services/app-service/).</span><span class="sxs-lookup"><span data-stu-id="2a7b1-145">To learn more, please visit [App Service documentation](https://azure.microsoft.com/documentation/services/app-service/).</span></span>

