---
title: "aaaScale квоты и ограничения в лаборатории в Azure DevTest Labs | Документы Microsoft"
description: "Узнайте, как tooscale лаборатории в Azure DevTest Labs"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: ae624155-9181-45fa-bd2b-1983339b7e0e
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: tarcher
ms.openlocfilehash: 7fb429c0aabdfbce3a4a5aa6d9259daa2ee270d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="scale-quotas-and-limits-in-devtest-labs"></a><span data-ttu-id="49218-103">Масштабирование квот и ограничений в DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="49218-103">Scale quotas and limits in DevTest Labs</span></span>
<span data-ttu-id="49218-104">При работе в DevTest Labs, можно заметить, что отсутствуют определенные toosome ограничения по умолчанию ресурсы Azure, что может повлиять на службы DevTest Labs hello.</span><span class="sxs-lookup"><span data-stu-id="49218-104">As you work in DevTest Labs, you might notice that there are certain default limits toosome Azure resources, which can affect hello DevTest Labs service.</span></span> <span data-ttu-id="49218-105">Эти ограничения, который ссылается tooas **квоты**.</span><span class="sxs-lookup"><span data-stu-id="49218-105">These limits are referred tooas **quotas**.</span></span>

> [!NOTE]
> <span data-ttu-id="49218-106">Hello DevTest Labs службы не задать все квоты.</span><span class="sxs-lookup"><span data-stu-id="49218-106">hello DevTest Labs service doesn't impose any quotas.</span></span> <span data-ttu-id="49218-107">Квоты, которые могут возникнуть, ограничения по умолчанию hello в целом Azure подписки.</span><span class="sxs-lookup"><span data-stu-id="49218-107">Any quotas you might encounter are default constraints of hello overall Azure subscription.</span></span>

<span data-ttu-id="49218-108">Каждый ресурс Azure можно использовать, пока не достигнута его квота.</span><span class="sxs-lookup"><span data-stu-id="49218-108">You can use each Azure resource until you reach its quota.</span></span> <span data-ttu-id="49218-109">Каждая подписка имеет свои квоты, а процесс использования отслеживается отдельно для каждой подписки.</span><span class="sxs-lookup"><span data-stu-id="49218-109">Each subscription has separate quotas and usage is tracked per subscription.</span></span>

<span data-ttu-id="49218-110">Например, что каждой подписки задана квота по умолчанию в 20 ядер.</span><span class="sxs-lookup"><span data-stu-id="49218-110">For example, each subscription has a default quota of 20 cores.</span></span> <span data-ttu-id="49218-111">Таким образом, при создании в лаборатории виртуальных машин, каждая из которых имеет четыре ядра, можно создать только пять виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="49218-111">So, if you are creating VMs in your lab with four cores each, then you can only create five VMs.</span></span> 

<span data-ttu-id="49218-112">[Azure подписка и ограничения служб](https://docs.microsoft.com/azure/azure-subscription-service-limits) перечислены некоторые наиболее распространенные квот hello для ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="49218-112">[Azure Subscription and Service Limits](https://docs.microsoft.com/azure/azure-subscription-service-limits) lists some of hello most common quotas for Azure resources.</span></span> <span data-ttu-id="49218-113">Здравствуйте, ресурсы, которые наиболее часто используются в лабораторной среде и для которой могут возникнуть квоты, включают Виртуальных машинах, общих IP-адресов, сетевого интерфейса, управляемого дисков, назначение роли RBAC и каналы ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="49218-113">hello resources most commonly used in a lab, and for which you might encounter quotas, include VM cores, public IP addresses, network interface, managed disks, RBAC role assignment, and ExpressRoute circuits.</span></span>

## <a name="view-your-usage-and-quotas"></a><span data-ttu-id="49218-114">Просмотр сведений об использовании и квотах</span><span class="sxs-lookup"><span data-stu-id="49218-114">View your usage and quotas</span></span>
<span data-ttu-id="49218-115">Следующие шаги показывают, как tooview hello текущие квоты в вашей подписке для определенных ресурсов Azure и toosee использовали какой процент каждой из квот.</span><span class="sxs-lookup"><span data-stu-id="49218-115">These steps show you how tooview hello current quotas in your subscription for specific Azure resources, and toosee what percentage of each quota you have used.</span></span>

1. <span data-ttu-id="49218-116">Войдите в toohello [портал Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="49218-116">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="49218-117">Выберите **более служб**, а затем выберите **выставления счетов** из списка hello.</span><span class="sxs-lookup"><span data-stu-id="49218-117">Select **More Services**, and then select **Billing** from hello list.</span></span>
1. <span data-ttu-id="49218-118">В колонке hello выставления счетов выберите подписку.</span><span class="sxs-lookup"><span data-stu-id="49218-118">In hello Billing blade, select a subscription.</span></span>
4. <span data-ttu-id="49218-119">Выберите **Использование и квоты**.</span><span class="sxs-lookup"><span data-stu-id="49218-119">Select **Usage + quotas**.</span></span>

   ![Кнопка "Использование и квоты"](./media/devtest-lab-scale-lab/devtestlab-usage-and-quotas.png)

   <span data-ttu-id="49218-121">Здравствуйте, использование + квоты колонке отображается список различных ресурсах, доступных в такой подписки и hello процент квоты hello, который используется для каждого ресурса.</span><span class="sxs-lookup"><span data-stu-id="49218-121">hello Usage + quotas blade appears, listing different resources available in that subscription and hello percentage of hello quota that is being used per resource.</span></span>

   ![Квоты и использование](./media/devtest-lab-scale-lab/devtestlab-view-quotas.png)

## <a name="requesting-more-resources-in-your-subscription"></a><span data-ttu-id="49218-123">Запрос дополнительных ресурсов в подписке</span><span class="sxs-lookup"><span data-stu-id="49218-123">Requesting more resources in your subscription</span></span>
<span data-ttu-id="49218-124">По достижении конца квоты, ограничение по умолчанию hello ресурса в подписке можно увеличить вверх tooa максимальный предел, как описано в [подписка Azure и ограничения служб](https://docs.microsoft.com/azure/azure-subscription-service-limits).</span><span class="sxs-lookup"><span data-stu-id="49218-124">If you reach a quota cap, hello default limit of a resource in a subscription can be increased up tooa maximum limit, as described in [Azure Subscription and Service Limits](https://docs.microsoft.com/azure/azure-subscription-service-limits).</span></span>

<span data-ttu-id="49218-125">Следующие шаги показывают, как toorequest квоты увеличивать через hello [портал Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="49218-125">These steps show you how toorequest a quota increase through hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="49218-126">Щелкните **Больше служб**, выберите **Выставление счетов**, а затем — **Использование и квоты**.</span><span class="sxs-lookup"><span data-stu-id="49218-126">Select **More Services**, select **Billing**, and then select **Usage + quotas**.</span></span>
1. <span data-ttu-id="49218-127">Здравствуйте, использование + колонке квоты, выберите hello **запросить увеличение** кнопки.</span><span class="sxs-lookup"><span data-stu-id="49218-127">In hello Usage + quotas blade, select hello **Request Increase** button.</span></span>

   ![Кнопка "Запросить увеличение"](./media/devtest-lab-scale-lab/devtestlab-request-increase.png)

1. <span data-ttu-id="49218-129">toocomplete и отправить запрос hello, заполните hello необходимые сведения на всех трех вкладках hello **New поддерживает запрос** формы.</span><span class="sxs-lookup"><span data-stu-id="49218-129">toocomplete and submit hello request, fill out hello required information on all three tabs of hello **New support request** form.</span></span>

   ![Форма запроса на увеличение](./media/devtest-lab-scale-lab/devtestlab-support-form.png)

<span data-ttu-id="49218-131">[Основные сведения о Azure ограничения и увеличивая степень](https://azure.microsoft.com/blog/azure-limits-quotas-increase-requests/) предоставляет дополнительные сведения об обращении в службу поддержки Azure toorequest квоты увеличение.</span><span class="sxs-lookup"><span data-stu-id="49218-131">[Understanding Azure Limits and Increases](https://azure.microsoft.com/blog/azure-limits-quotas-increase-requests/) provides more information about contacting Azure support toorequest a quota increase.</span></span>



[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

### <a name="next-steps"></a><span data-ttu-id="49218-132">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="49218-132">Next steps</span></span>
* <span data-ttu-id="49218-133">Просмотр hello [коллекции шаблонов Azure Resource Manager DevTest Labs QuickStart](https://github.com/Azure/azure-devtestlab/tree/master/Samples).</span><span class="sxs-lookup"><span data-stu-id="49218-133">Explore hello [DevTest Labs Azure Resource Manager QuickStart template gallery](https://github.com/Azure/azure-devtestlab/tree/master/Samples).</span></span>
