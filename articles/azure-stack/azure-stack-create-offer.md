---
title: "предложение Azure стека aaaCreate | Документы Microsoft"
description: "Как администратор облака, узнайте, как toocreate предложение для клиентов в Azure стека."
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
ms.openlocfilehash: 924526a0ff1c634b7c127c03a4572057c35b497b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-offer-in-azure-stack"></a><span data-ttu-id="b69fa-103">Создание предложения в Azure Stack</span><span class="sxs-lookup"><span data-stu-id="b69fa-103">Create an offer in Azure Stack</span></span>
<span data-ttu-id="b69fa-104">[Предлагает](azure-stack-key-features.md) — это группы один или несколько планов, поставщики присутствует tootenants toopurchase или подписаться на него.</span><span class="sxs-lookup"><span data-stu-id="b69fa-104">[Offers](azure-stack-key-features.md) are groups of one or more plans that providers present tootenants toopurchase or subscribe to.</span></span> <span data-ttu-id="b69fa-105">В этом документе показано, как предложение, включающее hello toocreate [план, созданный](azure-stack-create-plan.md) на последнем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="b69fa-105">This document shows you how toocreate an offer that includes hello [plan that you created](azure-stack-create-plan.md) in hello last step.</span></span> <span data-ttu-id="b69fa-106">Это предложение обеспечивает подписчиков hello возможность tooprovision виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="b69fa-106">This offer gives subscribers hello ability tooprovision virtual machines.</span></span>

1. <span data-ttu-id="b69fa-107">Войдите в портал администратора Azure стека toohello (https://adminportal.local.azurestack.external) > щелкните **New** > **клиента предлагает + планы**  >   **Предложить**.</span><span class="sxs-lookup"><span data-stu-id="b69fa-107">Sign in toohello Azure Stack administrator portal (https://adminportal.local.azurestack.external) > click **New** > **Tenant Offers + Plans** > **Offer**.</span></span>

   ![](media/azure-stack-create-offer/image01.png)
2. <span data-ttu-id="b69fa-108">В hello **новое предложение** колонки, заполните **отображаемое имя** и **имя ресурса**и затем выберите новую или существующую **группы ресурсов**.</span><span class="sxs-lookup"><span data-stu-id="b69fa-108">In hello **New Offer** blade, fill in **Display Name** and **Resource Name**, and then select a new or existing **Resource Group**.</span></span> <span data-ttu-id="b69fa-109">Hello отображаемое имя является hello предложение понятное имя и hello только сведения о предложение hello, hello пользователи будут видеть при подписке.</span><span class="sxs-lookup"><span data-stu-id="b69fa-109">hello Display Name is hello offer's friendly name and is hello only information about hello offer that hello users will see when subscribing.</span></span> <span data-ttu-id="b69fa-110">Таким образом будет убедиться, что toouse интуитивно имя, которое помогает понять, что следует предложение hello пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="b69fa-110">Therefore, be sure toouse an intuitive name that helps hello user understand what comes with hello offer.</span></span> <span data-ttu-id="b69fa-111">Только администратор hello можно увидеть hello имя ресурса.</span><span class="sxs-lookup"><span data-stu-id="b69fa-111">Only hello admin can see hello Resource Name.</span></span> <span data-ttu-id="b69fa-112">Он является hello имя, "Администраторы" использовать toowork с hello предложения в качестве ресурса диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="b69fa-112">It's hello name that admins use toowork with hello offer as an Azure Resource Manager resource.</span></span>

   ![](media/azure-stack-create-offer/image01a.png)
3. <span data-ttu-id="b69fa-113">Нажмите кнопку **базовые планы** и в hello **планирование** колонки, выберите hello планы tooinclude в предложение hello и нажмите кнопку **выберите**.</span><span class="sxs-lookup"><span data-stu-id="b69fa-113">Click **Base plans** and, in hello **Plan** blade, select hello plans you want tooinclude in hello offer, and then click **Select**.</span></span> <span data-ttu-id="b69fa-114">Нажмите кнопку **создать** toocreate hello предложения.</span><span class="sxs-lookup"><span data-stu-id="b69fa-114">Click **Create** toocreate hello offer.</span></span>

   ![](media/azure-stack-create-offer/image02.png)
4. <span data-ttu-id="b69fa-115">Нажмите кнопку **все ресурсы**, поиск новое предложение, щелкните на новое предложение hello, **изменению состояния**и нажмите кнопку **открытый**.</span><span class="sxs-lookup"><span data-stu-id="b69fa-115">Click **All Resources**, search for your new offer, click on hello new offer, click **Change State**, and then click **Public**.</span></span>

   ![](media/azure-stack-create-offer/image03.png)

<span data-ttu-id="b69fa-116">Предложения должны выполняться открытым и позволить клиентам tooget hello полное представление при подписке.</span><span class="sxs-lookup"><span data-stu-id="b69fa-116">Offers must be made public for tenants tooget hello full view when subscribing.</span></span> <span data-ttu-id="b69fa-117">Предложения можно:</span><span class="sxs-lookup"><span data-stu-id="b69fa-117">Offers can be:</span></span>

* <span data-ttu-id="b69fa-118">**Открытый**: tootenants видимым.</span><span class="sxs-lookup"><span data-stu-id="b69fa-118">**Public**: Visible tootenants.</span></span>
* <span data-ttu-id="b69fa-119">**Закрытый**: только администраторы видимым toohello облака.</span><span class="sxs-lookup"><span data-stu-id="b69fa-119">**Private**: Only visible toohello cloud administrators.</span></span> <span data-ttu-id="b69fa-120">Полезно при набора hello план или предложение, или если администратор облака hello хочет tooapprove каждую подписку.</span><span class="sxs-lookup"><span data-stu-id="b69fa-120">Useful while drafting hello plan or offer, or if hello cloud administrator wants tooapprove every subscription.</span></span>
* <span data-ttu-id="b69fa-121">**Списать**: закрыто toonew подписчиков.</span><span class="sxs-lookup"><span data-stu-id="b69fa-121">**Decommissioned**: Closed toonew subscribers.</span></span> <span data-ttu-id="b69fa-122">Здравствуйте, администратор облака можно использовать списанные tooprevent будущие подписки, но оставьте текущие подписчики без изменений.</span><span class="sxs-lookup"><span data-stu-id="b69fa-122">hello cloud administrator can use decommissioned tooprevent future subscriptions, but leave current subscribers untouched.</span></span>

<span data-ttu-id="b69fa-123">Предложение toohello изменения не являются видимыми toohello клиента.</span><span class="sxs-lookup"><span data-stu-id="b69fa-123">Changes toohello offer are not immediately visible toohello tenant.</span></span> <span data-ttu-id="b69fa-124">изменения toosee hello, может потребоваться toologout/входа toosee hello новую подписку в hello «Средством выбора подписки» при создании групп ресурсов и ресурсов.</span><span class="sxs-lookup"><span data-stu-id="b69fa-124">toosee hello changes, you might have toologout/login toosee hello new subscription in hello “Subscription picker” when creating resources/resource groups.</span></span>

> [!NOTE]
><span data-ttu-id="b69fa-125">Предложения по умолчанию, планы и квоты также можно создать с помощью PowerShell, как описано в hello [файл сведений для администратора службы Azure стека](https://github.com/Azure/AzureStack-Tools/tree/master/ServiceAdmin).</span><span class="sxs-lookup"><span data-stu-id="b69fa-125">You can also create default offers, plans, and quotas by using PowerShell as explained in hello [Azure Stack Service Administrator readme](https://github.com/Azure/AzureStack-Tools/tree/master/ServiceAdmin).</span></span>
>


## <a name="next-steps"></a><span data-ttu-id="b69fa-126">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b69fa-126">Next steps</span></span>
[<span data-ttu-id="b69fa-127">Подписаться на предложение tooan и затем подготовьте виртуальную Машину</span><span class="sxs-lookup"><span data-stu-id="b69fa-127">Subscribe tooan offer and then provision a VM</span></span>](azure-stack-subscribe-plan-provision-vm.md)
