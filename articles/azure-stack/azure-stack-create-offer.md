---
title: "Создать предложение в стек Azure | Документы Microsoft"
description: "Как администратор облака научиться создавать предложение для клиентов в Azure стека."
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: byronr
editor: 
ms.assetid: 96b080a4-a9a5-407c-ba54-111de2413d59
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: erikje
ms.openlocfilehash: 3d7360a1fb1c0cf42d77b3f39bf92c30438c2e01
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-offer-in-azure-stack"></a><span data-ttu-id="5ed5d-103">Создание предложения в Azure Stack</span><span class="sxs-lookup"><span data-stu-id="5ed5d-103">Create an offer in Azure Stack</span></span>
<span data-ttu-id="5ed5d-104">[Предлагает](azure-stack-key-features.md) — это группы один или несколько планов, предоставляющие поставщиков для клиентов для покупки или подписки.</span><span class="sxs-lookup"><span data-stu-id="5ed5d-104">[Offers](azure-stack-key-features.md) are groups of one or more plans that providers present to tenants to purchase or subscribe to.</span></span> <span data-ttu-id="5ed5d-105">В этом документе показано, как создать предложение, включающее [план, созданный](azure-stack-create-plan.md) на предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="5ed5d-105">This document shows you how to create an offer that includes the [plan that you created](azure-stack-create-plan.md) in the last step.</span></span> <span data-ttu-id="5ed5d-106">Это предложение позволяет подписчикам для подготовки виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="5ed5d-106">This offer gives subscribers the ability to provision virtual machines.</span></span>

1. <span data-ttu-id="5ed5d-107">Войдите в портал администратора Azure стека (https://adminportal.local.azurestack.external) > щелкните **New** > **клиента предлагает + планы**  >   **Предложить**.</span><span class="sxs-lookup"><span data-stu-id="5ed5d-107">Sign in to the Azure Stack administrator portal (https://adminportal.local.azurestack.external) > click **New** > **Tenant Offers + Plans** > **Offer**.</span></span>

   ![](media/azure-stack-create-offer/image01.png)
2. <span data-ttu-id="5ed5d-108">В **новое предложение** колонки, заполните **отображаемое имя** и **имя ресурса**и затем выберите новую или существующую **группы ресурсов**.</span><span class="sxs-lookup"><span data-stu-id="5ed5d-108">In the **New Offer** blade, fill in **Display Name** and **Resource Name**, and then select a new or existing **Resource Group**.</span></span> <span data-ttu-id="5ed5d-109">Отображаемое имя — предложение понятное имя и сведения о предложении, которое будут видеть при подписке.</span><span class="sxs-lookup"><span data-stu-id="5ed5d-109">The Display Name is the offer's friendly name and is the only information about the offer that the users will see when subscribing.</span></span> <span data-ttu-id="5ed5d-110">Таким образом необходимо с помощью интуитивно имя, которое помогает пользователю понять, что следует с предложением.</span><span class="sxs-lookup"><span data-stu-id="5ed5d-110">Therefore, be sure to use an intuitive name that helps the user understand what comes with the offer.</span></span> <span data-ttu-id="5ed5d-111">Только администратор может видеть имя ресурса.</span><span class="sxs-lookup"><span data-stu-id="5ed5d-111">Only the admin can see the Resource Name.</span></span> <span data-ttu-id="5ed5d-112">Это имя, которое администраторы используют для работы с предложением в качестве ресурса диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="5ed5d-112">It's the name that admins use to work with the offer as an Azure Resource Manager resource.</span></span>

   ![](media/azure-stack-create-offer/image01a.png)
3. <span data-ttu-id="5ed5d-113">Нажмите кнопку **базовые планы** и в **планирование** колонке выберите планы, которые требуется включить в предложение, а затем нажмите кнопку **выберите**.</span><span class="sxs-lookup"><span data-stu-id="5ed5d-113">Click **Base plans** and, in the **Plan** blade, select the plans you want to include in the offer, and then click **Select**.</span></span> <span data-ttu-id="5ed5d-114">Нажмите кнопку **создать** для создания предложения.</span><span class="sxs-lookup"><span data-stu-id="5ed5d-114">Click **Create** to create the offer.</span></span>

   ![](media/azure-stack-create-offer/image02.png)
4. <span data-ttu-id="5ed5d-115">Нажмите кнопку **все ресурсы**, поиск новое предложение, щелкните на новое предложение, **изменению состояния**и нажмите кнопку **открытый**.</span><span class="sxs-lookup"><span data-stu-id="5ed5d-115">Click **All Resources**, search for your new offer, click on the new offer, click **Change State**, and then click **Public**.</span></span>

   ![](media/azure-stack-create-offer/image03.png)

<span data-ttu-id="5ed5d-116">Предложения необходимо сделать доступным для клиентов получить полное представление при подписке.</span><span class="sxs-lookup"><span data-stu-id="5ed5d-116">Offers must be made public for tenants to get the full view when subscribing.</span></span> <span data-ttu-id="5ed5d-117">Предложения можно:</span><span class="sxs-lookup"><span data-stu-id="5ed5d-117">Offers can be:</span></span>

* <span data-ttu-id="5ed5d-118">**Открытый**: видимыми для клиентов.</span><span class="sxs-lookup"><span data-stu-id="5ed5d-118">**Public**: Visible to tenants.</span></span>
* <span data-ttu-id="5ed5d-119">**Закрытый**: доступно только для администраторов облака.</span><span class="sxs-lookup"><span data-stu-id="5ed5d-119">**Private**: Only visible to the cloud administrators.</span></span> <span data-ttu-id="5ed5d-120">Полезно во время проектирования в план или предложение, или если администратор облака утверждение каждой подписки.</span><span class="sxs-lookup"><span data-stu-id="5ed5d-120">Useful while drafting the plan or offer, or if the cloud administrator wants to approve every subscription.</span></span>
* <span data-ttu-id="5ed5d-121">**Списать**: замкнуты для новых подписчиков.</span><span class="sxs-lookup"><span data-stu-id="5ed5d-121">**Decommissioned**: Closed to new subscribers.</span></span> <span data-ttu-id="5ed5d-122">Администратору облака можно использовать выводится из эксплуатации, чтобы предотвратить будущие подписки, но оставить без изменений текущие подписчики.</span><span class="sxs-lookup"><span data-stu-id="5ed5d-122">The cloud administrator can use decommissioned to prevent future subscriptions, but leave current subscribers untouched.</span></span>

<span data-ttu-id="5ed5d-123">Изменения на предложение не видны сразу для клиента.</span><span class="sxs-lookup"><span data-stu-id="5ed5d-123">Changes to the offer are not immediately visible to the tenant.</span></span> <span data-ttu-id="5ed5d-124">Для просмотра изменений, может потребоваться выхода и входа в систему для просмотра новой подписки в «средством выбора подписки» при создании групп ресурсов и ресурсов.</span><span class="sxs-lookup"><span data-stu-id="5ed5d-124">To see the changes, you might have to logout/login to see the new subscription in the “Subscription picker” when creating resources/resource groups.</span></span>

> [!NOTE]
><span data-ttu-id="5ed5d-125">Предложения по умолчанию, планы и квоты также можно создать с помощью PowerShell, как описано в [файл сведений для администратора службы Azure стека](https://github.com/Azure/AzureStack-Tools/tree/master/ServiceAdmin).</span><span class="sxs-lookup"><span data-stu-id="5ed5d-125">You can also create default offers, plans, and quotas by using PowerShell as explained in the [Azure Stack Service Administrator readme](https://github.com/Azure/AzureStack-Tools/tree/master/ServiceAdmin).</span></span>
>


## <a name="next-steps"></a><span data-ttu-id="5ed5d-126">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5ed5d-126">Next steps</span></span>
[<span data-ttu-id="5ed5d-127">Подписка на предложение и последующая подготовка виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="5ed5d-127">Subscribe to an offer and then provision a VM</span></span>](azure-stack-subscribe-plan-provision-vm.md)
