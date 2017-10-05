---
title: "Масштабирование квот и ограничений в лаборатории в Azure DevTest Labs | Документация Майкрософт"
description: "Узнайте, как масштабировать лабораторию в Azure DevTest Labs."
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
ms.openlocfilehash: f11ed42b474e4f208eac92689bfa33fb188d15a1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="scale-quotas-and-limits-in-devtest-labs"></a><span data-ttu-id="07c84-103">Масштабирование квот и ограничений в DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="07c84-103">Scale quotas and limits in DevTest Labs</span></span>
<span data-ttu-id="07c84-104">При работе в DevTest Labs вы, вероятно, замечали, что для некоторых ресурсов Azure существуют определенные ограничения по умолчанию, которые могут влиять на работу службы DevTest Labs.</span><span class="sxs-lookup"><span data-stu-id="07c84-104">As you work in DevTest Labs, you might notice that there are certain default limits to some Azure resources, which can affect the DevTest Labs service.</span></span> <span data-ttu-id="07c84-105">Такие ограничения называют **квотами**.</span><span class="sxs-lookup"><span data-stu-id="07c84-105">These limits are referred to as **quotas**.</span></span>

> [!NOTE]
> <span data-ttu-id="07c84-106">Служба DevTest Labs не устанавливает каких-либо квот.</span><span class="sxs-lookup"><span data-stu-id="07c84-106">The DevTest Labs service doesn't impose any quotas.</span></span> <span data-ttu-id="07c84-107">Любые квоты, которые вам могут встретиться, — это ограничения по умолчанию, действующие на уровне всей подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="07c84-107">Any quotas you might encounter are default constraints of the overall Azure subscription.</span></span>

<span data-ttu-id="07c84-108">Каждый ресурс Azure можно использовать, пока не достигнута его квота.</span><span class="sxs-lookup"><span data-stu-id="07c84-108">You can use each Azure resource until you reach its quota.</span></span> <span data-ttu-id="07c84-109">Каждая подписка имеет свои квоты, а процесс использования отслеживается отдельно для каждой подписки.</span><span class="sxs-lookup"><span data-stu-id="07c84-109">Each subscription has separate quotas and usage is tracked per subscription.</span></span>

<span data-ttu-id="07c84-110">Например, что каждой подписки задана квота по умолчанию в 20 ядер.</span><span class="sxs-lookup"><span data-stu-id="07c84-110">For example, each subscription has a default quota of 20 cores.</span></span> <span data-ttu-id="07c84-111">Таким образом, при создании в лаборатории виртуальных машин, каждая из которых имеет четыре ядра, можно создать только пять виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="07c84-111">So, if you are creating VMs in your lab with four cores each, then you can only create five VMs.</span></span> 

<span data-ttu-id="07c84-112">В статье [Подписка Azure, границы, квоты и ограничения службы](https://docs.microsoft.com/azure/azure-subscription-service-limits) перечислены некоторые наиболее распространенные квоты для ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="07c84-112">[Azure Subscription and Service Limits](https://docs.microsoft.com/azure/azure-subscription-service-limits) lists some of the most common quotas for Azure resources.</span></span> <span data-ttu-id="07c84-113">К ресурсам, которые чаще всего используются в лаборатории и для которых могут быть квоты, относятся ядра виртуальных машин, общедоступные IP-адреса, сетевой интерфейс, управляемые диски, назначение ролей RBAC и каналы ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="07c84-113">The resources most commonly used in a lab, and for which you might encounter quotas, include VM cores, public IP addresses, network interface, managed disks, RBAC role assignment, and ExpressRoute circuits.</span></span>

## <a name="view-your-usage-and-quotas"></a><span data-ttu-id="07c84-114">Просмотр сведений об использовании и квотах</span><span class="sxs-lookup"><span data-stu-id="07c84-114">View your usage and quotas</span></span>
<span data-ttu-id="07c84-115">Следующие шаги показывают, как просмотреть сведения о текущих квотах в подписке на определенные ресурсы Azure, а также как узнать, какой процент каждой квоты уже использован.</span><span class="sxs-lookup"><span data-stu-id="07c84-115">These steps show you how to view the current quotas in your subscription for specific Azure resources, and to see what percentage of each quota you have used.</span></span>

1. <span data-ttu-id="07c84-116">Выполните вход на [портал Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="07c84-116">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="07c84-117">Щелкните **Больше служб**, а затем выберите в списке **Выставление счетов**.</span><span class="sxs-lookup"><span data-stu-id="07c84-117">Select **More Services**, and then select **Billing** from the list.</span></span>
1. <span data-ttu-id="07c84-118">В колонке "Выставление счетов" выберите подписку.</span><span class="sxs-lookup"><span data-stu-id="07c84-118">In the Billing blade, select a subscription.</span></span>
4. <span data-ttu-id="07c84-119">Выберите **Использование и квоты**.</span><span class="sxs-lookup"><span data-stu-id="07c84-119">Select **Usage + quotas**.</span></span>

   ![Кнопка "Использование и квоты"](./media/devtest-lab-scale-lab/devtestlab-usage-and-quotas.png)

   <span data-ttu-id="07c84-121">Появится колонка "Использование и квоты" , в которой отображаются различные ресурсы, доступные в данной подписке, и процент квоты, используемый каждым ресурсом.</span><span class="sxs-lookup"><span data-stu-id="07c84-121">The Usage + quotas blade appears, listing different resources available in that subscription and the percentage of the quota that is being used per resource.</span></span>

   ![Квоты и использование](./media/devtest-lab-scale-lab/devtestlab-view-quotas.png)

## <a name="requesting-more-resources-in-your-subscription"></a><span data-ttu-id="07c84-123">Запрос дополнительных ресурсов в подписке</span><span class="sxs-lookup"><span data-stu-id="07c84-123">Requesting more resources in your subscription</span></span>
<span data-ttu-id="07c84-124">При достижении ограничения квоты ресурса предельное значение по умолчанию в подписке можно увеличить до максимального предела, как описано в статье [Подписка Azure, границы, квоты и ограничения службы](https://docs.microsoft.com/azure/azure-subscription-service-limits).</span><span class="sxs-lookup"><span data-stu-id="07c84-124">If you reach a quota cap, the default limit of a resource in a subscription can be increased up to a maximum limit, as described in [Azure Subscription and Service Limits](https://docs.microsoft.com/azure/azure-subscription-service-limits).</span></span>

<span data-ttu-id="07c84-125">Следующие действия помогут вам запросить увеличение квоты с помощью [портала Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="07c84-125">These steps show you how to request a quota increase through the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="07c84-126">Щелкните **Больше служб**, выберите **Выставление счетов**, а затем — **Использование и квоты**.</span><span class="sxs-lookup"><span data-stu-id="07c84-126">Select **More Services**, select **Billing**, and then select **Usage + quotas**.</span></span>
1. <span data-ttu-id="07c84-127">В колонке "Использование и квоты" нажмите кнопку **Запросить увеличение**.</span><span class="sxs-lookup"><span data-stu-id="07c84-127">In the Usage + quotas blade, select the **Request Increase** button.</span></span>

   ![Кнопка "Запросить увеличение"](./media/devtest-lab-scale-lab/devtestlab-request-increase.png)

1. <span data-ttu-id="07c84-129">Чтобы заполнить и отправить запрос, введите необходимые сведения на всех трех вкладках формы **Новый запрос в службу поддержки**.</span><span class="sxs-lookup"><span data-stu-id="07c84-129">To complete and submit the request, fill out the required information on all three tabs of the **New support request** form.</span></span>

   ![Форма запроса на увеличение](./media/devtest-lab-scale-lab/devtestlab-support-form.png)

<span data-ttu-id="07c84-131">В записи блога [Understanding Azure Limits and Increases](https://azure.microsoft.com/blog/azure-limits-quotas-increase-requests/) (Основные сведения об ограничениях и увеличении квот Azure) предоставлены дополнительные сведения об обращении в службу поддержки Azure с запросом на увеличение квоты.</span><span class="sxs-lookup"><span data-stu-id="07c84-131">[Understanding Azure Limits and Increases](https://azure.microsoft.com/blog/azure-limits-quotas-increase-requests/) provides more information about contacting Azure support to request a quota increase.</span></span>



[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

### <a name="next-steps"></a><span data-ttu-id="07c84-132">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="07c84-132">Next steps</span></span>
* <span data-ttu-id="07c84-133">Изучите [коллекцию шаблонов быстрого запуска Azure Resource Manager для DevTest Labs](https://github.com/Azure/azure-devtestlab/tree/master/Samples).</span><span class="sxs-lookup"><span data-stu-id="07c84-133">Explore the [DevTest Labs Azure Resource Manager QuickStart template gallery](https://github.com/Azure/azure-devtestlab/tree/master/Samples).</span></span>
