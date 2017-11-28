---
title: "aaaUsing New Relic с помощью Azure | Документы Microsoft"
description: "Узнайте, как toouse hello toomanage службу New Relic и наблюдать за приложением Azure."
services: 
documentationcenter: .net
author: nickfloyd
manager: timlt
editor: 
ms.assetid: b01011be-c344-4e33-987d-c93dac1971fb
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/23/2016
ms.author: nickfloyd@newrelic.com
ms.openlocfilehash: 81e5f1b694264e3586ac75d40edd8afe185493d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="new-relic-application-performance-management-on-azure"></a><span data-ttu-id="90542-103">Инструмент управления производительностью приложений New Relic для Azure</span><span class="sxs-lookup"><span data-stu-id="90542-103">New Relic Application Performance Management on Azure</span></span>
<span data-ttu-id="90542-104">Можно добавить New Relic мирового уровня производительности мониторинга tooyour Azure размещенных приложениях.</span><span class="sxs-lookup"><span data-stu-id="90542-104">You can add New Relic's world-class performance monitoring tooyour Azure hosted applications.</span></span> <span data-ttu-id="90542-105">Вместе с широкими возможностями мониторинга, поиска и устранения неисправностей, а также настройки приложений Azure вы получаете специальное предложение о покупке продуктов New Relic со скидкой с помощью Azure.</span><span class="sxs-lookup"><span data-stu-id="90542-105">Along with comprehensive capabilities for monitoring, troubleshooting, and tuning your Azure apps, you are also eligible for a discounted price for New Relic products by using Azure.</span></span>

## <a name="what-is-new-relic"></a><span data-ttu-id="90542-106">Что такое New Relic?</span><span class="sxs-lookup"><span data-stu-id="90542-106">What is New Relic?</span></span>
<span data-ttu-id="90542-107">С [продуктов New Relic](https://newrelic.com/products), устранения ошибок приложения, максимальные потенциальные проблемы и понимать hello производительности всей среды.</span><span class="sxs-lookup"><span data-stu-id="90542-107">With [New Relic products](https://newrelic.com/products), you can solve app errors, stay ahead of potential issues, and understand hello performance of your entire environment.</span></span> <span data-ttu-id="90542-108">Это спроектированный toosave время, если для выявления и диагностики проблем с производительностью, и он помещает сведения hello необходимы toosolve эти проблемы под рукой.</span><span class="sxs-lookup"><span data-stu-id="90542-108">It is designed toosave you time when identifying and diagnosing performance issues, and it puts hello information you need toosolve these issues at your fingertips.</span></span>

<span data-ttu-id="90542-109">Новый hello отслеживает Relic загрузить времени и пропускной способности для вашего веб-транзакции, из сервера hello и браузеры пользователей.</span><span class="sxs-lookup"><span data-stu-id="90542-109">New Relic tracks hello load time and throughput for your web transactions, both from hello server and your users' browsers.</span></span> <span data-ttu-id="90542-110">Показывает, сколько времени тратят базы hello анализирует медленного выполнения запросов и веб-запросов, обеспечивает наблюдение за время работы и предупреждения, отслеживает исключения приложения и гораздо больше.</span><span class="sxs-lookup"><span data-stu-id="90542-110">It shows how much time you spend in hello database, analyzes slow queries and web requests, provides uptime monitoring and alerting, tracks application exceptions, and a whole lot more.</span></span> 

## <a name="special-pricing"></a><span data-ttu-id="90542-111">Специальные цены</span><span class="sxs-lookup"><span data-stu-id="90542-111">Special pricing</span></span>
<span data-ttu-id="90542-112">Новый стандартный Relic — свободное tooAzure пользователей.</span><span class="sxs-lookup"><span data-stu-id="90542-112">New Relic Standard is free tooAzure users.</span></span> <span data-ttu-id="90542-113">New Relic Pro предоставляется в зависимости от размера экземпляра для облачных служб Azure.</span><span class="sxs-lookup"><span data-stu-id="90542-113">New Relic Pro is offered based on instance size for Azure Cloud Services.</span></span> <span data-ttu-id="90542-114">Сведения о ценах см. в разделе hello [страницу New Relic](https://azure.microsoft.com/marketplace/partners/newrelic/newrelic/) в hello Azure Marketplace или обратитесь в службу New Relic (sales@newrelic.com) о ценах на уровне предприятия.</span><span class="sxs-lookup"><span data-stu-id="90542-114">For pricing information, see hello [New Relic page](https://azure.microsoft.com/marketplace/partners/newrelic/newrelic/) in hello Azure Marketplace or contact New Relic (sales@newrelic.com) for enterprise-level pricing.</span></span>

<span data-ttu-id="90542-115">Azure пользователи получают двухнедельной пробная подписка на новый Relic Pro при развертывании агента hello New Relic.</span><span class="sxs-lookup"><span data-stu-id="90542-115">Azure customers receive a two week trial subscription of New Relic Pro when they deploy hello New Relic agent.</span></span>

## <a name="sign-up-for-new-relic-using-hello-azure-store"></a><span data-ttu-id="90542-116">Зарегистрируйтесь для New Relic, с помощью хранилища Azure hello</span><span class="sxs-lookup"><span data-stu-id="90542-116">Sign up for New Relic using hello Azure Store</span></span>
<span data-ttu-id="90542-117">New Relic тесно интегрируется с веб-ролями и рабочими ролями Azure.</span><span class="sxs-lookup"><span data-stu-id="90542-117">New Relic integrates seamlessly with Azure Web Roles and Worker roles.</span></span> <span data-ttu-id="90542-118">Можно быстро и легко зарегистрироваться для New Relic непосредственно из hello хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="90542-118">You can quickly and easily sign up for New Relic directly from hello Azure Store.</span></span> <span data-ttu-id="90542-119">Инструкции см. в разделе hello [Azure хранения инструкции по регистрации](https://docs.newrelic.com/docs/agents/net-agent/azure-installation/azure-cloud-services#signup) из New Relic.</span><span class="sxs-lookup"><span data-stu-id="90542-119">For instructions, see hello [Azure store sign-up instructions](https://docs.newrelic.com/docs/agents/net-agent/azure-installation/azure-cloud-services#signup) from New Relic.</span></span>

## <a name="view-your-data"></a><span data-ttu-id="90542-120">Просмотр данных</span><span class="sxs-lookup"><span data-stu-id="90542-120">View your data</span></span>
<span data-ttu-id="90542-121">Сразу после регистрации вы сможете воспользоваться такими функциями New Relic, как эффективный мониторинг приложений и аналитика на основе данных.</span><span class="sxs-lookup"><span data-stu-id="90542-121">Once you've signed up, you can take advantage of New Relic's amazing application monitoring and data-driven analysis.</span></span> <span data-ttu-id="90542-122">toocheck производительность приложения в New Relic:</span><span class="sxs-lookup"><span data-stu-id="90542-122">toocheck your app's performance in New Relic:</span></span>

1. <span data-ttu-id="90542-123">Выберите Управление hello портала Azure.</span><span class="sxs-lookup"><span data-stu-id="90542-123">From hello Azure Portal, select Manage.</span></span>
2. <span data-ttu-id="90542-124">Выполните вход, используя адрес электронной почты и пароль для New Relic.</span><span class="sxs-lookup"><span data-stu-id="90542-124">Sign in with your New Relic account email and password.</span></span>
3. <span data-ttu-id="90542-125">Выберите приложение из tooview индекса приложения hello данные приложения в hello [страница обзора APM](https://docs.newrelic.com/docs/apm/applications-menu/monitoring/apm-overview-page).</span><span class="sxs-lookup"><span data-stu-id="90542-125">Select your app from hello Application index tooview all your app's data in hello [APM overview page](https://docs.newrelic.com/docs/apm/applications-menu/monitoring/apm-overview-page).</span></span>

## <a name="using-new-relic-with-azure"></a><span data-ttu-id="90542-126">Использование New Relic с Azure</span><span class="sxs-lookup"><span data-stu-id="90542-126">Using New Relic with Azure</span></span>
<span data-ttu-id="90542-127">Чтобы получить дополнительную информацию об использовании New Relic совместно с Azure, посетите [веб-сайт документации по New Relic](https://docs.newrelic.com/docs/agents/net-agent/azure-installation) и прочитайте такие статьи:</span><span class="sxs-lookup"><span data-stu-id="90542-127">For more information about using New Relic and Azure, see [New Relic's Documentation site](https://docs.newrelic.com/docs/agents/net-agent/azure-installation), including:</span></span> 

* [<span data-ttu-id="90542-128">New Relic for .NET</span><span class="sxs-lookup"><span data-stu-id="90542-128">New Relic for .NET</span></span>](https://docs.newrelic.com/docs/agents/net-agent/getting-started/new-relic-net)
* [<span data-ttu-id="90542-129">Instrument a .NET Worker Role on Azure Cloud service</span><span class="sxs-lookup"><span data-stu-id="90542-129">Instrument a .NET Worker Role on Azure Cloud service</span></span>](https://docs.newrelic.com/docs/agents/net-agent/azure-installation/instrument-net-worker-role-azure-cloud-service)
* [<span data-ttu-id="90542-130">New Relic для hello Microsoft Azure облачной платформы</span><span class="sxs-lookup"><span data-stu-id="90542-130">New Relic for hello Microsoft Azure Cloud platform</span></span>](https://docs.newrelic.com/docs/agents/net-agent/azure-installation/azure-cloud-services)
* [<span data-ttu-id="90542-131">New Relic для hello приложения служб Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="90542-131">New Relic for hello Microsoft Azure App Services</span></span>](https://docs.newrelic.com/docs/agents/net-agent/azure-installation/azure-portal)
* [<span data-ttu-id="90542-132">New Relic/Azure troubleshooting</span><span class="sxs-lookup"><span data-stu-id="90542-132">New Relic/Azure troubleshooting</span></span>](https://docs.newrelic.com/docs/agents/net-agent/azure-troubleshooting)

