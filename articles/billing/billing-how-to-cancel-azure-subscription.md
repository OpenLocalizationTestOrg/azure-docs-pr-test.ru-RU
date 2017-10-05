---
title: "Отмена подписки Azure | Документация Майкрософт"
description: "В этой статьей объясняется, как отменить подписку Azure, например бесплатную пробную версию подписки."
services: 
documentationcenter: 
author: genlin
manager: jlian
editor: 
tags: billing
ms.assetid: 3051d6b0-179f-4e3a-bda4-3fee7135eac5
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: genli
ms.openlocfilehash: c415fada30aa0b0bd9b9d1e416bc37ef30653f68
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="cancel-your-subscription-for-azure"></a><span data-ttu-id="7017d-103">Отмена подписки в Azure</span><span class="sxs-lookup"><span data-stu-id="7017d-103">Cancel your subscription for Azure</span></span>

<span data-ttu-id="7017d-104">[Администратор учетной записи](billing-subscription-transfer.md#whoisaa) может отменить подписку Azure.</span><span class="sxs-lookup"><span data-stu-id="7017d-104">You can cancel your Azure subscription as the [Account Administrator](billing-subscription-transfer.md#whoisaa).</span></span> <span data-ttu-id="7017d-105">После отмены подписки вы больше не сможете получать доступ к службам и ресурсам Azure.</span><span class="sxs-lookup"><span data-stu-id="7017d-105">After you cancel the subscription, your access to Azure services and resources ends.</span></span>

<span data-ttu-id="7017d-106">Прежде чем отменить подписку, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="7017d-106">Before you cancel your subscription:</span></span>

* <span data-ttu-id="7017d-107">Создайте резервную копию данных.</span><span class="sxs-lookup"><span data-stu-id="7017d-107">Back up your data.</span></span> <span data-ttu-id="7017d-108">Например, если вы храните данные в хранилище Azure или SQL, скачайте копию.</span><span class="sxs-lookup"><span data-stu-id="7017d-108">For example, if you're storing data in Azure storage or SQL, download a copy.</span></span> <span data-ttu-id="7017d-109">При наличии виртуальной машины сохраните ее образ локально.</span><span class="sxs-lookup"><span data-stu-id="7017d-109">If you have a virtual machine, save an image of it locally.</span></span>
* <span data-ttu-id="7017d-110">Завершите работу служб.</span><span class="sxs-lookup"><span data-stu-id="7017d-110">Shut down your services.</span></span> <span data-ttu-id="7017d-111">Перейдите на [страницу ресурсов на портале управления](https://ms.portal.azure.com/?flight=1#blade/HubsExtension/Resources/resourceType/Microsoft.Resources%2Fresources) и выберите команду **Остановить**, чтобы остановить работу всех запущенных виртуальных машин, приложений или других служб.</span><span class="sxs-lookup"><span data-stu-id="7017d-111">Go to the [resources page in the management portal](https://ms.portal.azure.com/?flight=1#blade/HubsExtension/Resources/resourceType/Microsoft.Resources%2Fresources), and **Stop** any running virtual machines, applications, or other services.</span></span>
* <span data-ttu-id="7017d-112">Перенесите данные.</span><span class="sxs-lookup"><span data-stu-id="7017d-112">Consider migrating your data.</span></span> <span data-ttu-id="7017d-113">Ознакомьтесь со статьей [Move resources to new resource group or subscription](../azure-resource-manager/resource-group-move-resources.md) (Перемещение ресурсов в новую группу ресурсов или подписку).</span><span class="sxs-lookup"><span data-stu-id="7017d-113">See [Move resources to new resource group or subscription](../azure-resource-manager/resource-group-move-resources.md).</span></span>

<span data-ttu-id="7017d-114">Если вы отмените подписку на платный [план поддержки Azure](https://azure.microsoft.com/support/plans/), вам по-прежнему ежемесячно будет выставляться счет за оставшуюся часть 6-месячного срока действия.</span><span class="sxs-lookup"><span data-stu-id="7017d-114">If you cancel a paid [Azure Support plan](https://azure.microsoft.com/support/plans/), you are still billed monthly for the rest of the 6-months term.</span></span>

## <a name="cancel-subscription-using-the-azure-portal"></a><span data-ttu-id="7017d-115">Отмена подписки с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="7017d-115">Cancel subscription using the Azure portal</span></span>

1. <span data-ttu-id="7017d-116">Выберите свою подписку на [странице подписок](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade).</span><span class="sxs-lookup"><span data-stu-id="7017d-116">Select your subscription from the [Subscriptions page](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade).</span></span>

1. <span data-ttu-id="7017d-117">Выберите подписку, которую нужно отменить, и щелкните **Отменить подписку**.</span><span class="sxs-lookup"><span data-stu-id="7017d-117">Select the subscription that you want to cancel and click **Cancel subscription**.</span></span>

    ![Снимок экрана, на котором показана кнопка "Отмена"](./media/billing-how-to-cancel-azure-subscription/cancel_ibiza.png)

1. <span data-ttu-id="7017d-119">Следуйте инструкциям и завершите отмену.</span><span class="sxs-lookup"><span data-stu-id="7017d-119">Follow prompts and finish cancellation.</span></span>

## <a name="cancel-subscription-using-the-azure-account-center"></a><span data-ttu-id="7017d-120">Отмена подписки с помощью Центра управления учетной записью Azure</span><span class="sxs-lookup"><span data-stu-id="7017d-120">Cancel subscription using the Azure Account Center</span></span>

1. <span data-ttu-id="7017d-121">Войдите в [Центр управления учетной записью Azure](https://account.windowsazure.com/subscriptions) в качестве администратора учетной записи.</span><span class="sxs-lookup"><span data-stu-id="7017d-121">Sign in to the [Azure Account Center](https://account.windowsazure.com/subscriptions) as the Account Administrator.</span></span>

1. <span data-ttu-id="7017d-122">В разделе **Щелкните подписку для просмотра информации и сведений об использовании**выберите подписку, которую нужно отменить.</span><span class="sxs-lookup"><span data-stu-id="7017d-122">Under **Click a subscription to view details and usage**, select the subscription that you want to cancel.</span></span>

    ![Снимок экрана, на котором показан выбранный пример подписки](./media/billing-how-to-cancel-azure-subscription/Selectsub.png)

1. <span data-ttu-id="7017d-124">В правой части страницы выберите **Отменить подписку**.</span><span class="sxs-lookup"><span data-stu-id="7017d-124">On the right side of the page, select **Cancel Subscription**.</span></span>

    ![Снимок экрана, на котором показана кнопка "Отменить подписку"](./media/billing-how-to-cancel-azure-subscription/cancelsub.png)

1. <span data-ttu-id="7017d-126">Выберите **Да, отменить мою подписку**.</span><span class="sxs-lookup"><span data-stu-id="7017d-126">Select **Yes, cancel my subscription**.</span></span>

    ![Снимок экрана, на котором показано диалоговое окно "Отмена"](./media/billing-how-to-cancel-azure-subscription/cancelbox.png)

1. <span data-ttu-id="7017d-128">Щелкните </span><span class="sxs-lookup"><span data-stu-id="7017d-128">Click</span></span> ![Кнопка со знаком проверки](./media/billing-how-to-cancel-azure-subscription/checkbutton.png) <span data-ttu-id="7017d-130">, чтобы закрыть диалоговое окно и вернуться к странице подписки.</span><span class="sxs-lookup"><span data-stu-id="7017d-130">to close the dialog window and return to your subscription page.</span></span>

## <a name="what-happens-after-i-cancel-my-subscription"></a><span data-ttu-id="7017d-131">Что происходит после отмены подписки?</span><span class="sxs-lookup"><span data-stu-id="7017d-131">What happens after I cancel my subscription?</span></span>

<span data-ttu-id="7017d-132">После отмены подписки немедленно прекратится выставление счетов.</span><span class="sxs-lookup"><span data-stu-id="7017d-132">Once you cancel, billing is stopped immediately.</span></span> <span data-ttu-id="7017d-133">Однако, отображение отмены на портале может занять до 10 минут.</span><span class="sxs-lookup"><span data-stu-id="7017d-133">However, it can take up to 10 minutes for the cancellation show in the portal.</span></span>

<span data-ttu-id="7017d-134">После этого службы будут отключены.</span><span class="sxs-lookup"><span data-stu-id="7017d-134">After that, your services are disabled.</span></span> <span data-ttu-id="7017d-135">Это означает, что виртуальные машины и временные IP-адреса освобождаются, а хранилище становится доступным только для чтения.</span><span class="sxs-lookup"><span data-stu-id="7017d-135">That means your virtual machines are deallocated, temporary IP addresses are freed, and storage is read-only.</span></span>

<span data-ttu-id="7017d-136">Если у вас нет бесплатной пробной версии или доступного кредита, вам будет выставлен счет за любые непогашенные задолженности за использование, которые появились за время с начала цикла выставления счетов до даты отмены подписки.</span><span class="sxs-lookup"><span data-stu-id="7017d-136">Unless you’re on a Free Trial or have credits available, you’re billed for any outstanding usage charges generated between your last billing cycle and the cancellation date.</span></span> <span data-ttu-id="7017d-137">Свой последний счет вы получите в конце цикла выставления счетов.</span><span class="sxs-lookup"><span data-stu-id="7017d-137">You get your last bill at the end of the billing cycle.</span></span>

<span data-ttu-id="7017d-138">Мы окончательно удаляем данные через 90 дней после отмены подписки на случай, если они вам понадобятся или вы измените свое решение.</span><span class="sxs-lookup"><span data-stu-id="7017d-138">After you cancel your subscription, we wait 90 days before permanently deleting your data in case you need to access it or you change your mind.</span></span> <span data-ttu-id="7017d-139">Мы не взимаем плату за хранение данных.</span><span class="sxs-lookup"><span data-stu-id="7017d-139">We don't charge you for retaining the data.</span></span> <span data-ttu-id="7017d-140">Дополнительные сведения см. в разделе [What happens to your data if you leave the service](https://go.microsoft.com/fwLink/p/?LinkID=822930&clcid=0x409) (Что происходит с данными, когда вы прекращаете использовать службу).</span><span class="sxs-lookup"><span data-stu-id="7017d-140">To learn more, see [Microsoft Trust Center - How we manage your data](https://go.microsoft.com/fwLink/p/?LinkID=822930&clcid=0x409).</span></span>

## <a name="reactivate-subscription"></a><span data-ttu-id="7017d-141">Повторная активация подписки</span><span class="sxs-lookup"><span data-stu-id="7017d-141">Reactivate subscription</span></span>

<span data-ttu-id="7017d-142">Если вы случайно отменили подписку с оплатой по мере использования, можно [повторно активировать ее в Центре управления учетной записью](billing-subscription-become-disable.md).</span><span class="sxs-lookup"><span data-stu-id="7017d-142">If you cancel your Pay-As-You-Go subscription accidentally, you can [reactivate it in the Accounts Center](billing-subscription-become-disable.md).</span></span>

<span data-ttu-id="7017d-143">Если у вас подписка не по мере использования, обратитесь в службу поддержки в течение 90 дней после отмены подписки для повторной активации.</span><span class="sxs-lookup"><span data-stu-id="7017d-143">If your subscription is not Pay-As-You-Go, contact support within 90 days of cancellation to reactivate your subscription.</span></span>

## <a name="need-help-contact-support"></a><span data-ttu-id="7017d-144">Требуется помощь?</span><span class="sxs-lookup"><span data-stu-id="7017d-144">Need help?</span></span> <span data-ttu-id="7017d-145">Обратитесь в службу поддержки.</span><span class="sxs-lookup"><span data-stu-id="7017d-145">Contact support.</span></span>

<span data-ttu-id="7017d-146">Если у вас есть дополнительные вопросы, [обратитесь в службу поддержки](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade), которая поможет быстро устранить проблему.</span><span class="sxs-lookup"><span data-stu-id="7017d-146">If you still have questions, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to get your issue resolved quickly.</span></span>
