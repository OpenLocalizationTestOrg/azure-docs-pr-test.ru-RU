---
title: "aaaHow работает служба приложений Azure"
description: "Принцип работы службы приложений"
keywords: "служба приложений, служба приложений azure, масштабировать, масштабируемый, план службы приложений, стоимость службы приложений"
services: app-service
documentationcenter: 
author: yochay
manager: erikre
editor: 
ms.assetid: ae74fc32-969e-4580-8d61-02c922f1f184
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 02/23/2017
ms.author: yochayk
ms.openlocfilehash: b20733ec8844773d063e2b6918605c4a48db1f5c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-app-service-works"></a><span data-ttu-id="a845c-104">Принцип работы службы приложений</span><span class="sxs-lookup"><span data-stu-id="a845c-104">How App Service works</span></span>
<span data-ttu-id="a845c-105">Служба приложений Azure — облачной службы, спроектированный toosolve hello практические неполадкам повседневных инженеров.</span><span class="sxs-lookup"><span data-stu-id="a845c-105">Azure App Service is a cloud service that's designed toosolve hello practical problems that engineers face today.</span></span>
<span data-ttu-id="a845c-106">Службы приложений основное внимание уделяется предоставление высокому уровню продуктивности разработки без влияния на hello должны toodeliver приложений в масштабе облака.</span><span class="sxs-lookup"><span data-stu-id="a845c-106">App Service focuses on providing superior developer productivity without compromising on hello need toodeliver applications at cloud scale.</span></span> 

<span data-ttu-id="a845c-107">Службы приложений также предоставляет функции hello и платформ, которые необходимы для создания корпоративных бизнес-приложений.</span><span class="sxs-lookup"><span data-stu-id="a845c-107">App Service also provides hello features and frameworks that are necessary for creating enterprise line-of-business applications.</span></span> <span data-ttu-id="a845c-108">Приложение службы можно разрабатывать приложения в наиболее популярных языках программирования, включая Java, PHP, Node.js, Python и языках Microsoft .NET hello.</span><span class="sxs-lookup"><span data-stu-id="a845c-108">App Service lets you develop apps in most popular development languages, including Java, PHP, Node.js, Python, and hello Microsoft .NET languages.</span></span> <span data-ttu-id="a845c-109">С помощью службы приложений вы можете делать следующее.</span><span class="sxs-lookup"><span data-stu-id="a845c-109">With App Service, you can:</span></span>

* <span data-ttu-id="a845c-110">создавать веб-приложения с высоким уровнем масштабируемости;</span><span class="sxs-lookup"><span data-stu-id="a845c-110">Build highly scalable web apps.</span></span>
* <span data-ttu-id="a845c-111">быстро создавать серверную часть мобильных приложений с такими удобными возможностями, как серверная часть данных, проверка подлинности пользователей и push-уведомления;</span><span class="sxs-lookup"><span data-stu-id="a845c-111">Quickly build Mobile Apps back ends with a set of easy-to-use mobile capabilities such as data back ends, user authentication, and push notifications.</span></span>
* <span data-ttu-id="a845c-112">создавать, развертывать и публиковать API с помощью служб API;</span><span class="sxs-lookup"><span data-stu-id="a845c-112">Implement, deploy, and publish APIs with API Apps.</span></span>
* <span data-ttu-id="a845c-113">объединять бизнес-приложения в рабочие процессы и преобразовывать данные, используя приложения логики.</span><span class="sxs-lookup"><span data-stu-id="a845c-113">Tie business applications together into workflows and transform data with Logic Apps.</span></span>

> [!INCLUDE [app-service-linux](../../includes/app-service-linux.md)]
> 
> 

<span data-ttu-id="a845c-114">Все типы приложений используют hello масштабируемая и гибкая веб-приложений платформе, которая позволяет разработчикам toohave возникнуть оптимизированного весь жизненный цикл из обслуживания tooapp разработки приложения.</span><span class="sxs-lookup"><span data-stu-id="a845c-114">All app types rely on hello scalable and flexible Web Apps platform, which enables developers toohave an optimized full lifecycle experience from app design tooapp maintenance.</span></span> <span data-ttu-id="a845c-115">функции Hello жизненным циклом обеспечивают hello следующее:</span><span class="sxs-lookup"><span data-stu-id="a845c-115">hello lifecycle capabilities enable hello following:</span></span>

* <span data-ttu-id="a845c-116">**Быстро создавать приложения.**</span><span class="sxs-lookup"><span data-stu-id="a845c-116">**Quick app creation**.</span></span> <span data-ttu-id="a845c-117">С самого начала или выбора пакета оперативной поддержки системы (ОС) из hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="a845c-117">Start from scratch or pick an operational support system (OSS) package from hello Azure Marketplace.</span></span>
* <span data-ttu-id="a845c-118">**Осуществлять непрерывное развертывание.**</span><span class="sxs-lookup"><span data-stu-id="a845c-118">**Continuous deployment**.</span></span> <span data-ttu-id="a845c-119">Автоматически развертывать новый код из таких популярных решений управления версиями, как TFS, GitHub и BitBucket, и синхронизировать содержимое с такими службами онлайн-хранилищ, как OneDrive и DropBox.</span><span class="sxs-lookup"><span data-stu-id="a845c-119">Automatically deploy new code from popular source control solutions such as TFS, GitHub, and Bitbucket, and sync content from online storage services such as OneDrive and Dropbox.</span></span>
* <span data-ttu-id="a845c-120">**Тестировать приложение в рабочей среде.**</span><span class="sxs-lookup"><span data-stu-id="a845c-120">**Test in production**.</span></span> <span data-ttu-id="a845c-121">Плавно создания предварительной рабочей среде и управления ими hello объем трафика, который будет toothem.</span><span class="sxs-lookup"><span data-stu-id="a845c-121">Smoothly create pre-production environments and manage hello amount of traffic that's going toothem.</span></span> <span data-ttu-id="a845c-122">Отладка в облаке hello при необходимости и накат при обнаружении ошибок.</span><span class="sxs-lookup"><span data-stu-id="a845c-122">Debug in hello cloud when needed, and roll back when issues are found.</span></span>
* <span data-ttu-id="a845c-123">**Выполнять асинхронные задачи и пакетные задания.**</span><span class="sxs-lookup"><span data-stu-id="a845c-123">**Running asynchronous tasks and batch jobs**.</span></span> <span data-ttu-id="a845c-124">Выполнять код в фоновом режиме или активировать его на основе событий (например, при поступлении сообщений в очередь хранилища Azure) или в определенное время (CRON).</span><span class="sxs-lookup"><span data-stu-id="a845c-124">Run code in a background process or activate your code based on events (such as messages landing in an Azure Storage queue) and scheduled times (CRON).</span></span>
* <span data-ttu-id="a845c-125">**Масштабирование приложения hello**.</span><span class="sxs-lookup"><span data-stu-id="a845c-125">**Scaling hello app**.</span></span> <span data-ttu-id="a845c-126">Используйте одну из многих вариантов tooautomatically масштабировать службу по горизонтали и вертикали в зависимости от трафика и использовании ресурсов.</span><span class="sxs-lookup"><span data-stu-id="a845c-126">Use one of many options tooautomatically scale your service horizontally and vertically based on traffic and resource utilization.</span></span> <span data-ttu-id="a845c-127">Настройка частного сред, выделенный tooyour приложений.</span><span class="sxs-lookup"><span data-stu-id="a845c-127">Configure private environments that are dedicated tooyour apps.</span></span>   
* <span data-ttu-id="a845c-128">**Обслуживание приложения hello**.</span><span class="sxs-lookup"><span data-stu-id="a845c-128">**Maintaining hello app**.</span></span> <span data-ttu-id="a845c-129">Использовать многие отладки hello и toostay функции диагностики опережает проблем и tooefficiently устранить их, либо в режиме реального времени (с такими функциями как автоматическое восстановление и динамической отладки) или после проведения hello путем анализа памяти и журналы дампов.</span><span class="sxs-lookup"><span data-stu-id="a845c-129">Use many of hello debugging and diagnostics features toostay ahead of problems and tooefficiently resolve them either in real time (with features such as auto-healing and live debugging) or after hello fact by analyzing logs and memory dumps.</span></span>

<span data-ttu-id="a845c-130">В целом возможности службы приложения включите toofocus разработчиков для своего кода и быстро достичь состояния стабильными и высокой степенью масштабирования рабочей.</span><span class="sxs-lookup"><span data-stu-id="a845c-130">As a whole, App Service capabilities enable developers toofocus on their code and quickly reach a stable and highly scalable production state.</span></span> <span data-ttu-id="a845c-131">Hello API приложения и компоненты приложения логики разработчики могут создавать реальных корпоративных приложений, мост барьеров между бизнес-решений и локальная интеграция toocloud.</span><span class="sxs-lookup"><span data-stu-id="a845c-131">With hello API Apps and Logic Apps features, developers can build real-world enterprise applications that bridge barriers between business solutions and on-premises toocloud integration.</span></span> 

## <a name="videos"></a><span data-ttu-id="a845c-132">Видеоролики</span><span class="sxs-lookup"><span data-stu-id="a845c-132">Videos</span></span>
* <span data-ttu-id="a845c-133">[Why Azure Web Sites? Web Sites Architecture — with Stefan Schackow](https://azure.microsoft.com/documentation/videos/why-azure-web-sites-plus-architecture/) (Зачем использовать именно веб-сайты Azure? Архитектура веб-сайтов со Стефаном Шашковым)</span><span class="sxs-lookup"><span data-stu-id="a845c-133">[Azure App Service Architecture](https://azure.microsoft.com/documentation/videos/why-azure-web-sites-plus-architecture/)</span></span>

## <a name="next-steps"></a><span data-ttu-id="a845c-134">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a845c-134">Next steps</span></span>

<span data-ttu-id="a845c-135">Дополнительные сведения о службе приложений в одном hello следующие вопросы:</span><span class="sxs-lookup"><span data-stu-id="a845c-135">Learn more about App Service in one of hello following topics:</span></span>

* [<span data-ttu-id="a845c-136">Что такое служба приложений Azure?</span><span class="sxs-lookup"><span data-stu-id="a845c-136">What is Azure App Service?</span></span>](app-service-value-prop-what-is.md)
  * [<span data-ttu-id="a845c-137">Веб-приложение</span><span class="sxs-lookup"><span data-stu-id="a845c-137">Web App</span></span>](../app-service-web/app-service-web-overview.md)
  * [<span data-ttu-id="a845c-138">Мобильное приложение</span><span class="sxs-lookup"><span data-stu-id="a845c-138">Mobile App</span></span>](../app-service-mobile/app-service-mobile-value-prop.md)
  * [<span data-ttu-id="a845c-139">Приложение API</span><span class="sxs-lookup"><span data-stu-id="a845c-139">API App</span></span>](../app-service-api/app-service-api-apps-why-best-platform.md)
* [<span data-ttu-id="a845c-140">Windows Azure Web Sites - Things they don’t teach kids in school</span><span class="sxs-lookup"><span data-stu-id="a845c-140">Azure App Service Architecture (presentation)</span></span>](http://www.slideshare.net/maartenba/windows-azure-web-sites-things-they-dont-teach-kids-in-school-comunity-day-2013)
* [<span data-ttu-id="a845c-141">Сравнение службы приложений, облачных служб и виртуальных машин Azure</span><span class="sxs-lookup"><span data-stu-id="a845c-141">Azure App Service, Cloud Services, and Virtual Machines comparison</span></span>](../app-service-web/choose-web-site-cloud-service-vm.md)
* [<span data-ttu-id="a845c-142">Подробный обзор планов службы приложений Azure</span><span class="sxs-lookup"><span data-stu-id="a845c-142">Understanding App Service Plans</span></span>](azure-web-sites-web-hosting-plans-in-depth-overview.md)
* [<span data-ttu-id="a845c-143">Введение tooApp среды службы</span><span class="sxs-lookup"><span data-stu-id="a845c-143">Introduction tooApp Service Environment</span></span>](../app-service-web/app-service-app-service-environment-intro.md)
  * [<span data-ttu-id="a845c-144">Создание среды службы приложений</span><span class="sxs-lookup"><span data-stu-id="a845c-144">Exercise: Create an App Service Environment</span></span>](../app-service-web/app-service-web-how-to-create-an-app-service-environment.md)
* [<span data-ttu-id="a845c-145">Windows Azure Websites Development Stacks Support (Поддержка стеков разработки веб-сайтов Windows Azure)</span><span class="sxs-lookup"><span data-stu-id="a845c-145">Azure App Service Development Stacks Support</span></span>](https://azure.microsoft.com/blog/windows-azure-websites-development-stacks-support/)



