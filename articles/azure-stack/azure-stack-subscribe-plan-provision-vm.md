---
title: "Подписаться на предложение | Документы Microsoft"
description: "Пользователь Узнайте, как подписаться на предложение."
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: byronr
editor: 
ms.assetid: 7f3f8683-ef09-4838-92ed-41f2fddbbbed
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 7/03/2017
ms.author: erikje
ms.openlocfilehash: f70815b5e89753a4b0083ffbe10d9920062d1ff0
ms.sourcegitcommit: 90e2cced6a773b1b52f999ba73cd8877305d270b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2017
---
# <a name="subscribe-to-an-offer"></a><span data-ttu-id="60edf-103">Подписка на предложение</span><span class="sxs-lookup"><span data-stu-id="60edf-103">Subscribe to an offer</span></span>

<span data-ttu-id="60edf-104">*Применяется к: стек Azure интегрированных систем и пакет средств разработки стек Azure*</span><span class="sxs-lookup"><span data-stu-id="60edf-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

<span data-ttu-id="60edf-105">После запуска [создать предложение](azure-stack-create-offer.md), проверить, что пользователи могут создать подписку.</span><span class="sxs-lookup"><span data-stu-id="60edf-105">Now that you've [created an offer](azure-stack-create-offer.md), test that your users can create a subscription.</span></span>

1. <span data-ttu-id="60edf-106">[Войдите в](azure-stack-connect-azure-stack.md) в пользовательский портал Azure стека (https://portal.local.azurestack.external) и нажмите **получить подписку**.</span><span class="sxs-lookup"><span data-stu-id="60edf-106">[Sign in](azure-stack-connect-azure-stack.md) to the Azure Stack user portal (https://portal.local.azurestack.external) and click **Get a Subscription**.</span></span>

   ![](media/azure-stack-subscribe-plan-provision-vm/image01.png)
2. <span data-ttu-id="60edf-107">В **отображаемое имя** поле введите имя для вашей подписки, щелкните **предлагают**, выберите один из предложения в **выберите предложение** и, при необходимости нажмите кнопку  **Создание**.</span><span class="sxs-lookup"><span data-stu-id="60edf-107">In the **Display Name** field, type a name for your subscription, click **Offer**, click one of the offers in the **Choose an offer** blade, and then click **Create**.</span></span>

   ![](media/azure-stack-subscribe-plan-provision-vm/image02.png)
3. <span data-ttu-id="60edf-108">Чтобы просмотреть созданную подписку, щелкните **дополнительные службы**, нажмите кнопку **подписки**, затем нажмите кнопку в новую подписку.</span><span class="sxs-lookup"><span data-stu-id="60edf-108">To view the subscription you created, click **More services**, click **Subscriptions**, then click your new subscription.</span></span>  

<span data-ttu-id="60edf-109">После оформления подписки на предложение, обновите портал, чтобы узнать, какие службы являются частью новой подписки.</span><span class="sxs-lookup"><span data-stu-id="60edf-109">After you subscribe to an offer, refresh the portal to see which services are part of the new subscription.</span></span>

## <a name="subscribe-to-an-add-on-plan"></a><span data-ttu-id="60edf-110">Подписаться на план надстройку</span><span class="sxs-lookup"><span data-stu-id="60edf-110">Subscribe to an add-on plan</span></span>
<span data-ttu-id="60edf-111">Если предложение план надстройку, пользователи могут добавлять их в свою подписку в любое время.</span><span class="sxs-lookup"><span data-stu-id="60edf-111">If the offer has an add-on plan, users can add them to their subscription at any time.</span></span>  

1. <span data-ttu-id="60edf-112">На портале пользователей выберите **дополнительные службы** > **подписки**.</span><span class="sxs-lookup"><span data-stu-id="60edf-112">In the user portal, select **More services** > **Subscriptions**.</span></span>

2. <span data-ttu-id="60edf-113">Щелкните подписку > **добавить план** и выберите план надстройку.</span><span class="sxs-lookup"><span data-stu-id="60edf-113">Click on the subscription > **Add Plan** button, and select the add-on plan.</span></span>



## <a name="next-steps"></a><span data-ttu-id="60edf-114">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="60edf-114">Next steps</span></span>
[<span data-ttu-id="60edf-115">Подготовка виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="60edf-115">Provision a virtual machine</span></span>](azure-stack-provision-vm.md)
