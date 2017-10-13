---
title: "Создать предложение в стек Azure | Документы Microsoft"
description: "Администратору облака Узнайте, как создать предложение для пользователей в Azure стека."
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
ms.openlocfilehash: 269a6106f657536ba74be366f842b2f9cd86c5dc
ms.sourcegitcommit: 90e2cced6a773b1b52f999ba73cd8877305d270b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="create-an-offer-in-azure-stack"></a><span data-ttu-id="83869-103">Создание предложения в Azure Stack</span><span class="sxs-lookup"><span data-stu-id="83869-103">Create an offer in Azure Stack</span></span>

<span data-ttu-id="83869-104">*Применяется к: стек Azure интегрированных систем и пакет средств разработки стек Azure*</span><span class="sxs-lookup"><span data-stu-id="83869-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

<span data-ttu-id="83869-105">[Предлагает](azure-stack-key-features.md) — это группы один или несколько планов, поставщики представления пользователям для покупки или подписки.</span><span class="sxs-lookup"><span data-stu-id="83869-105">[Offers](azure-stack-key-features.md) are groups of one or more plans that providers present to users to purchase or subscribe to.</span></span> <span data-ttu-id="83869-106">В этом документе показано, как создать предложение, включающее [план, созданный](azure-stack-create-plan.md) на предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="83869-106">This document shows you how to create an offer that includes the [plan that you created](azure-stack-create-plan.md) in the last step.</span></span> <span data-ttu-id="83869-107">Это предложение позволяет подписчикам для подготовки виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="83869-107">This offer gives subscribers the ability to provision virtual machines.</span></span>

1. <span data-ttu-id="83869-108">Войдите в портал администратора Azure стека (https://adminportal.local.azurestack.external) > щелкните **New** > **клиента предлагает + планы**  >   **Предложить**.</span><span class="sxs-lookup"><span data-stu-id="83869-108">Sign in to the Azure Stack administrator portal (https://adminportal.local.azurestack.external) > click **New** > **Tenant Offers + Plans** > **Offer**.</span></span>

   ![](media/azure-stack-create-offer/image01.png)
2. <span data-ttu-id="83869-109">В **новое предложение** колонки, заполните **отображаемое имя** и **имя ресурса**и затем выберите новую или существующую **группы ресурсов**.</span><span class="sxs-lookup"><span data-stu-id="83869-109">In the **New Offer** blade, fill in **Display Name** and **Resource Name**, and then select a new or existing **Resource Group**.</span></span> <span data-ttu-id="83869-110">Отображаемое имя — предложение понятное имя и сведения о предложении, которое будут видеть при подписке.</span><span class="sxs-lookup"><span data-stu-id="83869-110">The Display Name is the offer's friendly name and is the only information about the offer that the users will see when subscribing.</span></span> <span data-ttu-id="83869-111">Таким образом необходимо с помощью интуитивно имя, которое помогает пользователю понять, что следует с предложением.</span><span class="sxs-lookup"><span data-stu-id="83869-111">Therefore, be sure to use an intuitive name that helps the user understand what comes with the offer.</span></span> <span data-ttu-id="83869-112">Только администратор может видеть имя ресурса.</span><span class="sxs-lookup"><span data-stu-id="83869-112">Only the admin can see the Resource Name.</span></span> <span data-ttu-id="83869-113">Это имя, которое администраторы используют для работы с предложением в качестве ресурса диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="83869-113">It's the name that admins use to work with the offer as an Azure Resource Manager resource.</span></span>

   ![](media/azure-stack-create-offer/image01a.png)
3. <span data-ttu-id="83869-114">Нажмите кнопку **базовые планы** и в **планирование** колонке выберите планы, которые требуется включить в предложение, а затем нажмите кнопку **выберите**.</span><span class="sxs-lookup"><span data-stu-id="83869-114">Click **Base plans** and, in the **Plan** blade, select the plans you want to include in the offer, and then click **Select**.</span></span> <span data-ttu-id="83869-115">Нажмите кнопку **создать** для создания предложения.</span><span class="sxs-lookup"><span data-stu-id="83869-115">Click **Create** to create the offer.</span></span>

   ![](media/azure-stack-create-offer/image02.png)
4. <span data-ttu-id="83869-116">Нажмите кнопку **все ресурсы**, поиск новое предложение, щелкните на новое предложение, **изменению состояния**и нажмите кнопку **открытый**.</span><span class="sxs-lookup"><span data-stu-id="83869-116">Click **All Resources**, search for your new offer, click on the new offer, click **Change State**, and then click **Public**.</span></span>

   ![](media/azure-stack-create-offer/image03.png)

<span data-ttu-id="83869-117">Предложения необходимо сделать доступным для пользователей получить полное представление при подписке.</span><span class="sxs-lookup"><span data-stu-id="83869-117">Offers must be made public for users to get the full view when subscribing.</span></span> <span data-ttu-id="83869-118">Предложения можно:</span><span class="sxs-lookup"><span data-stu-id="83869-118">Offers can be:</span></span>

* <span data-ttu-id="83869-119">**Открытый**: видны пользователям.</span><span class="sxs-lookup"><span data-stu-id="83869-119">**Public**: Visible to users.</span></span>
* <span data-ttu-id="83869-120">**Закрытый**: доступно только для администраторов облака.</span><span class="sxs-lookup"><span data-stu-id="83869-120">**Private**: Only visible to the cloud administrators.</span></span> <span data-ttu-id="83869-121">Полезно во время проектирования в план или предложение, или если администратор облака утверждение каждой подписки.</span><span class="sxs-lookup"><span data-stu-id="83869-121">Useful while drafting the plan or offer, or if the cloud administrator wants to approve every subscription.</span></span>
* <span data-ttu-id="83869-122">**Списать**: замкнуты для новых подписчиков.</span><span class="sxs-lookup"><span data-stu-id="83869-122">**Decommissioned**: Closed to new subscribers.</span></span> <span data-ttu-id="83869-123">Администратору облака можно использовать выводится из эксплуатации, чтобы предотвратить будущие подписки, но оставить без изменений текущие подписчики.</span><span class="sxs-lookup"><span data-stu-id="83869-123">The cloud administrator can use decommissioned to prevent future subscriptions, but leave current subscribers untouched.</span></span>

<span data-ttu-id="83869-124">Изменения на предложение не сразу же отображается для пользователя.</span><span class="sxs-lookup"><span data-stu-id="83869-124">Changes to the offer are not immediately visible to the user.</span></span> <span data-ttu-id="83869-125">Для просмотра изменений, может потребоваться выхода и входа в систему для просмотра новой подписки в «средством выбора подписки» при создании групп ресурсов и ресурсов.</span><span class="sxs-lookup"><span data-stu-id="83869-125">To see the changes, you might have to logout/login to see the new subscription in the “Subscription picker” when creating resources/resource groups.</span></span>

> [!NOTE]
><span data-ttu-id="83869-126">Предложения по умолчанию, планы и квоты также можно создать с помощью PowerShell, как описано в [файл сведений для администратора службы Azure стека](https://github.com/Azure/AzureStack-Tools/tree/master/ServiceAdmin).</span><span class="sxs-lookup"><span data-stu-id="83869-126">You can also create default offers, plans, and quotas by using PowerShell as explained in the [Azure Stack Service Administrator readme](https://github.com/Azure/AzureStack-Tools/tree/master/ServiceAdmin).</span></span>
>


### <a name="next-steps"></a><span data-ttu-id="83869-127">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="83869-127">Next steps</span></span>
[<span data-ttu-id="83869-128">Подписка на предложение и последующая подготовка виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="83869-128">Subscribe to an offer and then provision a VM</span></span>](azure-stack-subscribe-plan-provision-vm.md)
