---
title: "aaaGuide toocreating шаблон решения для hello Marketplace | Документы Microsoft"
description: "Подробные инструкции, как toocreate, сертификации и развернуть решение шаблон изображения нескольких виртуальных Машин для покупки в Azure Marketplace hello."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: e14e05f2-2385-4ce0-b351-0747cb74ba19
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/27/2016
ms.author: hascipio; v-divte
ms.openlocfilehash: b0e7067176337dd0d3f6f6ec04c963f80f706ab0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="guide-toocreate-a-solution-template-for-azure-marketplace"></a><span data-ttu-id="fb822-103">Руководство по toocreate шаблон решения для Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="fb822-103">Guide toocreate a solution template for Azure Marketplace</span></span>
<span data-ttu-id="fb822-104">После завершения шага 1, [создания и регистрации учетной записи][link-acct-creation], вы интерактивной при создании hello шаблона решения Azure совместимой во [технические предварительные условия для создания шаблон решения](marketplace-publishing-solution-template-creation-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="fb822-104">After completing step 1, [Account creation and registration][link-acct-creation], we guided you on hello creation of an Azure-compatible solution template at [Technical prerequisites for creating a solution template](marketplace-publishing-solution-template-creation-prerequisites.md).</span></span> <span data-ttu-id="fb822-105">Теперь мы поможет hello действия по созданию шаблона решения для нескольких виртуальных машин на hello [портал публикации] [ link-pubportal] для hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="fb822-105">Now we will walk you through hello steps for creating a solution template for multiple VMs on hello [Publishing Portal][link-pubportal] for hello Azure Marketplace.</span></span>

## <a name="create-your-solution-template-offer-in-hello-publishing-portal"></a><span data-ttu-id="fb822-106">Создание шаблона ваше решение предложение в hello портал публикации</span><span class="sxs-lookup"><span data-stu-id="fb822-106">Create your solution template offer in hello Publishing Portal</span></span>
<span data-ttu-id="fb822-107">Go слишком [https://publish.windowsazure.com](http://publish.windowsazure.com). При входе для hello первый раз toohello [портал публикации](https://publish.windowsazure.com/), используйте hello же учетной записи, под которым было зарегистрировано профиль продавца вашей компании.</span><span class="sxs-lookup"><span data-stu-id="fb822-107">Go too [https://publish.windowsazure.com](http://publish.windowsazure.com). When signing in for hello first time toohello [Publishing Portal](https://publish.windowsazure.com/), use hello same account with which your company’s seller profile was registered.</span></span> <span data-ttu-id="fb822-108">Позже в качестве соадминистратора в hello портал публикации можно добавить любой сотрудник вашей компании.</span><span class="sxs-lookup"><span data-stu-id="fb822-108">Later, you can add any employee of your company as a co-admin in hello Publishing Portal.</span></span>

### <a name="1-select-solution-templates"></a><span data-ttu-id="fb822-109">1. Выберите "Шаблоны решений"</span><span class="sxs-lookup"><span data-stu-id="fb822-109">1. Select "Solution templates"</span></span>
  ![рисунок][img-pubportal-menu-sol-templ]

### <a name="2-create-a-new-solution-template"></a><span data-ttu-id="fb822-111">2. Создайте новый шаблон решения</span><span class="sxs-lookup"><span data-stu-id="fb822-111">2. Create a new solution template</span></span>
  ![рисунок][img-pubportal-sol-templ-new]

### <a name="3-start-with-topologies"></a><span data-ttu-id="fb822-113">3. Начните с топологий</span><span class="sxs-lookup"><span data-stu-id="fb822-113">3. Start with topologies</span></span>
<span data-ttu-id="fb822-114">Шаблон решения — «родительский» tooall его топологий.</span><span class="sxs-lookup"><span data-stu-id="fb822-114">A solution template is a "parent" tooall of its topologies.</span></span> <span data-ttu-id="fb822-115">В одном шаблоне предложений или решения можно определить сразу несколько топологий.</span><span class="sxs-lookup"><span data-stu-id="fb822-115">You can define multiple topologies in one offer/solution template.</span></span> <span data-ttu-id="fb822-116">При передаче toostaging предложение, то при переносе со всеми его топологии.</span><span class="sxs-lookup"><span data-stu-id="fb822-116">When an offer is pushed toostaging, it is pushed with all of its topologies.</span></span> <span data-ttu-id="fb822-117">Выполните действия hello ниже toodefine ваше предложение.</span><span class="sxs-lookup"><span data-stu-id="fb822-117">Follow hello steps below toodefine your offer:</span></span>     

* <span data-ttu-id="fb822-118">Создание топологии: «Идентификатор топологии» обычно — имя hello hello топологии для шаблона решения hello.</span><span class="sxs-lookup"><span data-stu-id="fb822-118">Create a Topology: “Topology Identifier” is typically hello name of hello topology for hello solution template.</span></span> <span data-ttu-id="fb822-119">Идентификатор Hello топологии используется в URL-адрес hello, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="fb822-119">hello topology identifier is used in hello URL as shown below:</span></span>

  <span data-ttu-id="fb822-120">Azure Marketplace: http://azure.microsoft.com/marketplace/partners/{пространство_имен_издателя}/{идентификатор_заказа}{идентификатор_топологии};</span><span class="sxs-lookup"><span data-stu-id="fb822-120">Azure Marketplace: http://azure.microsoft.com/marketplace/partners/{PublisherNamespace}/{OfferIdentifier}{TopologyIdentifier}</span></span>

  <span data-ttu-id="fb822-121">портал Azure: https://portal.azure.com/#gallery/{пространство_имен_издателя}.{идентификатор_заказа}{идентификатор_топологии}.</span><span class="sxs-lookup"><span data-stu-id="fb822-121">Azure Portal: https://portal.azure.com/#gallery/{PublisherNamespace}.{OfferIdentifier}{TopologyIdentifier}</span></span>
* <span data-ttu-id="fb822-122">Добавьте новую версию.</span><span class="sxs-lookup"><span data-stu-id="fb822-122">Add a new version.</span></span>

### <a name="4-get-your-topology-versions-certified"></a><span data-ttu-id="fb822-123">4. Сертифицируйте версии топологии</span><span class="sxs-lookup"><span data-stu-id="fb822-123">4. Get your topology versions certified</span></span>
<span data-ttu-id="fb822-124">Отправка ZIP-файл, содержащий все требуемые файлы tooprovision конкретную версию hello топологии.</span><span class="sxs-lookup"><span data-stu-id="fb822-124">Upload a zip file that contains all required files tooprovision that particular version of hello topology.</span></span> <span data-ttu-id="fb822-125">Этот ZIP-файл должен содержать hello следующее:</span><span class="sxs-lookup"><span data-stu-id="fb822-125">This zip file must contain hello following:</span></span>

* <span data-ttu-id="fb822-126">файлы *mainTemplate.json* и *createUiDefinition.json* в корневом каталоге;</span><span class="sxs-lookup"><span data-stu-id="fb822-126">*mainTemplate.json* and *createUiDefinition.json* file at its root directory.</span></span>
* <span data-ttu-id="fb822-127">связанные шаблоны и все необходимые сценарии.</span><span class="sxs-lookup"><span data-stu-id="fb822-127">Any linked templates and all required scripts.</span></span>

  > [!TIP]
  > <span data-ttu-id="fb822-128">Во время работы разработчиков по созданию решения hello топологии шаблона и их Сертифицирован бизнеса hello, маркетинга и/или юридических отделов компании могут работать hello маркетинговые и юридические материалы.</span><span class="sxs-lookup"><span data-stu-id="fb822-128">While your developers work on creating hello solution template topologies and getting them certified, hello business, marketing, and/or legal departments of your company can work on hello marketing and legal content.</span></span>
  >
  >

## <a name="next-steps"></a><span data-ttu-id="fb822-129">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fb822-129">Next steps</span></span>
<span data-ttu-id="fb822-130">Теперь, когда создан шаблон решения и отправлены hello ZIP-файл, следуйте инструкциям hello hello [руководство по содержимому маркетинга Marketplace](marketplace-publishing-push-to-staging.md) до отправки toostaging предложение hello.</span><span class="sxs-lookup"><span data-stu-id="fb822-130">Now that you created your solution template and uploaded hello zip file, please follow hello instructions in hello [Marketplace marketing content guide](marketplace-publishing-push-to-staging.md) before pushing hello offer toostaging.</span></span> <span data-ttu-id="fb822-131">Посетите toosee hello полный набор marketplace публикация статей, [Приступая к работе: как toopublish toohello предложение Azure Marketplace](marketplace-publishing-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="fb822-131">toosee hello full set of marketplace publishing articles, visit [Getting started: How toopublish an offer toohello Azure Marketplace](marketplace-publishing-getting-started.md).</span></span>

<span data-ttu-id="fb822-132">Вас также могут заинтересовать следующие связанные статьи:</span><span class="sxs-lookup"><span data-stu-id="fb822-132">You might also be interested in these related articles:</span></span>

* <span data-ttu-id="fb822-133">Образы виртуальных машин: [Об образах виртуальных машин в Azure](https://msdn.microsoft.com/library/azure/dn790290.aspx)</span><span class="sxs-lookup"><span data-stu-id="fb822-133">VM images: [About Virtual Machine Images in Azure](https://msdn.microsoft.com/library/azure/dn790290.aspx)</span></span>
* <span data-ttu-id="fb822-134">Расширения виртуальных машин: [общие сведения об агенте, расширениях](https://msdn.microsoft.com/library/azure/dn832621.aspx) и [компонентах виртуальных машин Azure](https://msdn.microsoft.com/library/azure/dn606311.aspx)</span><span class="sxs-lookup"><span data-stu-id="fb822-134">VM extensions: [VM Agent and VM Extensions Overview](https://msdn.microsoft.com/library/azure/dn832621.aspx) and [Azure VM Extensions and Features](https://msdn.microsoft.com/library/azure/dn606311.aspx)</span></span>
* <span data-ttu-id="fb822-135">Azure Resource Manager: [Создание шаблонов Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) и [простые примеры шаблонов](https://github.com/rjmax/ArmExamples)</span><span class="sxs-lookup"><span data-stu-id="fb822-135">Azure Resource Manager: [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md) and [Simple Template Examples](https://github.com/rjmax/ArmExamples)</span></span>
* <span data-ttu-id="fb822-136">Регулирует учетной записи хранилища: [как tooMonitor для регулирования учетной записи хранилища](http://blogs.msdn.com/b/mast/archive/2014/08/02/how-to-monitor-for-storage-account-throttling.aspx) и [хранилища Premium](../storage/common/storage-premium-storage.md#scalability-and-performance-targets)</span><span class="sxs-lookup"><span data-stu-id="fb822-136">Storage account throttles: [How tooMonitor for Storage Account Throttling](http://blogs.msdn.com/b/mast/archive/2014/08/02/how-to-monitor-for-storage-account-throttling.aspx) and [Premium storage](../storage/common/storage-premium-storage.md#scalability-and-performance-targets)</span></span>

[img-pubportal-menu-sol-templ]:media/marketplace-publishing-solution-template-creation/pubportal-menu-solution-templates.png
[img-pubportal-sol-templ-new]:media/marketplace-publishing-solution-template-creation/pubportal-solution-template-new.png
[link-acct-creation]:marketplace-publishing-accounts-creation-registration.md
[link-pubportal]:https://publish.windowsazure.com
