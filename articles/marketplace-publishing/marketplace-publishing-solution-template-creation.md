---
title: "Руководство по созданию шаблона решения для Marketplace | Документация Майкрософт"
description: "Подробные инструкции по созданию, сертификации и развертыванию шаблона решения с поддержкой нескольких образов виртуальных машин для продажи в Azure Marketplace."
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
ms.openlocfilehash: b753bfb4bd69bd9aacf4eebd8999397394c28bc4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="guide-to-create-a-solution-template-for-azure-marketplace"></a><span data-ttu-id="4bd29-103">Руководство по созданию шаблона решения для Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="4bd29-103">Guide to create a solution template for Azure Marketplace</span></span>
<span data-ttu-id="4bd29-104">Выполнив шаг 1 [Создание учетной записи разработчика Майкрософт][link-acct-creation], вы перейдете к статье [Технические компоненты, необходимые для создания шаблона решения для Azure Marketplace](marketplace-publishing-solution-template-creation-prerequisites.md) с инструкциями по созданию шаблона решения, совместимого с Azure.</span><span class="sxs-lookup"><span data-stu-id="4bd29-104">After completing step 1, [Account creation and registration][link-acct-creation], we guided you on the creation of an Azure-compatible solution template at [Technical prerequisites for creating a solution template](marketplace-publishing-solution-template-creation-prerequisites.md).</span></span> <span data-ttu-id="4bd29-105">Рассмотрим процедуру создания шаблона решения для нескольких виртуальных машин на [портале публикации][link-pubportal] для Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="4bd29-105">Now we will walk you through the steps for creating a solution template for multiple VMs on the [Publishing Portal][link-pubportal] for the Azure Marketplace.</span></span>

## <a name="create-your-solution-template-offer-in-the-publishing-portal"></a><span data-ttu-id="4bd29-106">Создание шаблона решения на портале публикации</span><span class="sxs-lookup"><span data-stu-id="4bd29-106">Create your solution template offer in the Publishing Portal</span></span>
<span data-ttu-id="4bd29-107">Откройте страницу [https://publish.windowsazure.com](http://publish.windowsazure.com). При первом входе в [портал публикации](https://publish.windowsazure.com/)укажите учетную запись, под которой зарегистрирован профиль продавца для вашей компании.</span><span class="sxs-lookup"><span data-stu-id="4bd29-107">Go to  [https://publish.windowsazure.com](http://publish.windowsazure.com). When signing in for the first time to the [Publishing Portal](https://publish.windowsazure.com/), use the same account with which your company’s seller profile was registered.</span></span> <span data-ttu-id="4bd29-108">Впоследствии вы сможете добавить в качестве соадминистратора на портале публикации любого сотрудника своей компании.</span><span class="sxs-lookup"><span data-stu-id="4bd29-108">Later, you can add any employee of your company as a co-admin in the Publishing Portal.</span></span>

### <a name="1-select-solution-templates"></a><span data-ttu-id="4bd29-109">1. Выберите "Шаблоны решений"</span><span class="sxs-lookup"><span data-stu-id="4bd29-109">1. Select "Solution templates"</span></span>
  ![рисунок][img-pubportal-menu-sol-templ]

### <a name="2-create-a-new-solution-template"></a><span data-ttu-id="4bd29-111">2. Создайте новый шаблон решения</span><span class="sxs-lookup"><span data-stu-id="4bd29-111">2. Create a new solution template</span></span>
  ![рисунок][img-pubportal-sol-templ-new]

### <a name="3-start-with-topologies"></a><span data-ttu-id="4bd29-113">3. Начните с топологий</span><span class="sxs-lookup"><span data-stu-id="4bd29-113">3. Start with topologies</span></span>
<span data-ttu-id="4bd29-114">Шаблон решения служит родительским элементом для всех своих топологий.</span><span class="sxs-lookup"><span data-stu-id="4bd29-114">A solution template is a "parent" to all of its topologies.</span></span> <span data-ttu-id="4bd29-115">В одном шаблоне предложений или решения можно определить сразу несколько топологий.</span><span class="sxs-lookup"><span data-stu-id="4bd29-115">You can define multiple topologies in one offer/solution template.</span></span> <span data-ttu-id="4bd29-116">Когда предложение переходит к стадии промежуточного развертывания, вместе с ним отправляются все его топологии.</span><span class="sxs-lookup"><span data-stu-id="4bd29-116">When an offer is pushed to staging, it is pushed with all of its topologies.</span></span> <span data-ttu-id="4bd29-117">Выполните следующее, чтобы определить предложение:</span><span class="sxs-lookup"><span data-stu-id="4bd29-117">Follow the steps below to define your offer:</span></span>     

* <span data-ttu-id="4bd29-118">Создайте топологию (как правило, в качестве имени топологии для шаблона решения используется "идентификатор топологии").</span><span class="sxs-lookup"><span data-stu-id="4bd29-118">Create a Topology: “Topology Identifier” is typically the name of the topology for the solution template.</span></span> <span data-ttu-id="4bd29-119">Идентификатор топологии включается в URL-адрес, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="4bd29-119">The topology identifier is used in the URL as shown below:</span></span>

  <span data-ttu-id="4bd29-120">Azure Marketplace: http://azure.microsoft.com/marketplace/partners/{пространство_имен_издателя}/{идентификатор_заказа}{идентификатор_топологии};</span><span class="sxs-lookup"><span data-stu-id="4bd29-120">Azure Marketplace: http://azure.microsoft.com/marketplace/partners/{PublisherNamespace}/{OfferIdentifier}{TopologyIdentifier}</span></span>

  <span data-ttu-id="4bd29-121">портал Azure: https://portal.azure.com/#gallery/{пространство_имен_издателя}.{идентификатор_заказа}{идентификатор_топологии}.</span><span class="sxs-lookup"><span data-stu-id="4bd29-121">Azure Portal: https://portal.azure.com/#gallery/{PublisherNamespace}.{OfferIdentifier}{TopologyIdentifier}</span></span>
* <span data-ttu-id="4bd29-122">Добавьте новую версию.</span><span class="sxs-lookup"><span data-stu-id="4bd29-122">Add a new version.</span></span>

### <a name="4-get-your-topology-versions-certified"></a><span data-ttu-id="4bd29-123">4. Сертифицируйте версии топологии</span><span class="sxs-lookup"><span data-stu-id="4bd29-123">4. Get your topology versions certified</span></span>
<span data-ttu-id="4bd29-124">Передайте ZIP-файл, содержащий все файлы, необходимые для подготовки соответствующей версии топологии.</span><span class="sxs-lookup"><span data-stu-id="4bd29-124">Upload a zip file that contains all required files to provision that particular version of the topology.</span></span> <span data-ttu-id="4bd29-125">Этот ZIP-файл должен содержать следующее:</span><span class="sxs-lookup"><span data-stu-id="4bd29-125">This zip file must contain the following:</span></span>

* <span data-ttu-id="4bd29-126">файлы *mainTemplate.json* и *createUiDefinition.json* в корневом каталоге;</span><span class="sxs-lookup"><span data-stu-id="4bd29-126">*mainTemplate.json* and *createUiDefinition.json* file at its root directory.</span></span>
* <span data-ttu-id="4bd29-127">связанные шаблоны и все необходимые сценарии.</span><span class="sxs-lookup"><span data-stu-id="4bd29-127">Any linked templates and all required scripts.</span></span>

  > [!TIP]
  > <span data-ttu-id="4bd29-128">Создание и сертификацию топологий шаблонов решений осуществляют ваши разработчики, а разработкой маркетинговых и юридических материалов может заняться коммерческий, маркетинговый или юридический отдел вашей компании.</span><span class="sxs-lookup"><span data-stu-id="4bd29-128">While your developers work on creating the solution template topologies and getting them certified, the business, marketing, and/or legal departments of your company can work on the marketing and legal content.</span></span>
  >
  >

## <a name="next-steps"></a><span data-ttu-id="4bd29-129">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4bd29-129">Next steps</span></span>
<span data-ttu-id="4bd29-130">После создания шаблона решения и отправки ZIP-файла выполните инструкции в статье [Завершение создания предложения с маркетинговыми материалами](marketplace-publishing-push-to-staging.md), прежде чем перемещать предложение в промежуточную среду.</span><span class="sxs-lookup"><span data-stu-id="4bd29-130">Now that you created your solution template and uploaded the zip file, please follow the instructions in the [Marketplace marketing content guide](marketplace-publishing-push-to-staging.md) before pushing the offer to staging.</span></span> <span data-ttu-id="4bd29-131">Полный список статей о публикации в Marketplace см. в статье [Как опубликовать предложение и управлять им в Azure Marketplace](marketplace-publishing-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="4bd29-131">To see the full set of marketplace publishing articles, visit [Getting started: How to publish an offer to the Azure Marketplace](marketplace-publishing-getting-started.md).</span></span>

<span data-ttu-id="4bd29-132">Вас также могут заинтересовать следующие связанные статьи:</span><span class="sxs-lookup"><span data-stu-id="4bd29-132">You might also be interested in these related articles:</span></span>

* <span data-ttu-id="4bd29-133">Образы виртуальных машин: [Об образах виртуальных машин в Azure](https://msdn.microsoft.com/library/azure/dn790290.aspx)</span><span class="sxs-lookup"><span data-stu-id="4bd29-133">VM images: [About Virtual Machine Images in Azure](https://msdn.microsoft.com/library/azure/dn790290.aspx)</span></span>
* <span data-ttu-id="4bd29-134">Расширения виртуальных машин: [общие сведения об агенте, расширениях](https://msdn.microsoft.com/library/azure/dn832621.aspx) и [компонентах виртуальных машин Azure](https://msdn.microsoft.com/library/azure/dn606311.aspx)</span><span class="sxs-lookup"><span data-stu-id="4bd29-134">VM extensions: [VM Agent and VM Extensions Overview](https://msdn.microsoft.com/library/azure/dn832621.aspx) and [Azure VM Extensions and Features](https://msdn.microsoft.com/library/azure/dn606311.aspx)</span></span>
* <span data-ttu-id="4bd29-135">Azure Resource Manager: [Создание шаблонов Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) и [простые примеры шаблонов](https://github.com/rjmax/ArmExamples)</span><span class="sxs-lookup"><span data-stu-id="4bd29-135">Azure Resource Manager: [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md) and [Simple Template Examples](https://github.com/rjmax/ArmExamples)</span></span>
* <span data-ttu-id="4bd29-136">Регулирование учетной записи хранения: [How to Monitor for Storage Account Throttling](http://blogs.msdn.com/b/mast/archive/2014/08/02/how-to-monitor-for-storage-account-throttling.aspx) (Отслеживание регулирования учетной записи хранения) и [Хранилище класса "Премиум": высокопроизводительная служба хранилища для рабочих нагрузок виртуальных машин Azure](../storage/common/storage-premium-storage.md#scalability-and-performance-targets)</span><span class="sxs-lookup"><span data-stu-id="4bd29-136">Storage account throttles: [How to Monitor for Storage Account Throttling](http://blogs.msdn.com/b/mast/archive/2014/08/02/how-to-monitor-for-storage-account-throttling.aspx) and [Premium storage](../storage/common/storage-premium-storage.md#scalability-and-performance-targets)</span></span>

[img-pubportal-menu-sol-templ]:media/marketplace-publishing-solution-template-creation/pubportal-menu-solution-templates.png
[img-pubportal-sol-templ-new]:media/marketplace-publishing-solution-template-creation/pubportal-solution-template-new.png
[link-acct-creation]:marketplace-publishing-accounts-creation-registration.md
[link-pubportal]:https://publish.windowsazure.com
