---
title: "Настройка оповещений о выставлении счетов или предоставлении кредитов для подписок Azure | Документация Майкрософт"
description: "Описывает процесс настройки предупреждений на счете Azure, помогая избежать непредвиденных счетов."
keywords: "оповещение о предоставлении кредита,оповещение о выставлении счета"
services: 
documentationcenter: 
author: vikdesai
manager: tonguyen
editor: 
tags: billing
ms.assetid: 9b7b3eeb-cd9d-4690-86a3-51b1e2a8974f
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/28/2017
ms.author: vikdesai
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7a1b579fdde831fdc3afa0a2aee4c24890216ed1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-billing-or-credit-alerts-for-your-microsoft-azure-subscriptions"></a><span data-ttu-id="6e8d2-104">Настройка оповещений о выставлении счетов или предоставлении кредитов для подписок Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="6e8d2-104">Set up billing or credit alerts for your Microsoft Azure subscriptions</span></span>
<span data-ttu-id="6e8d2-105">Если вы являетесь администратором учетной записи для подписки Azure, с помощью службы оповещений о выставлении счетов Azure можно создать пользовательские оповещения, которые помогут отслеживать и контролировать действия по выставлению счетов для учетных записей Azure.</span><span class="sxs-lookup"><span data-stu-id="6e8d2-105">If you’re the Account Admin for an Azure subscription, you can use the Azure Billing Alert Service to create customized billing alerts that help you monitor and manage billing activity for your Azure accounts.</span></span>

<span data-ttu-id="6e8d2-106">Эта служба доступна в предварительной версии, поэтому сначала ее нужно включить на странице "Функции предварительной версии".</span><span class="sxs-lookup"><span data-stu-id="6e8d2-106">This service is in preview, so you need to enable it in the Preview Features page first.</span></span>

## <a name="set-the-alert-threshold-and-email-recipients"></a><span data-ttu-id="6e8d2-107">Укажите адресатов электронной почты и пороговое значение для отправки предупреждений</span><span class="sxs-lookup"><span data-stu-id="6e8d2-107">Set the alert threshold and email recipients</span></span>
1. <span data-ttu-id="6e8d2-108">Посетите [страницу "Функции предварительной версии"](https://account.windowsazure.com/PreviewFeatures) и включите **службы оповещений о выставлении счетов**.</span><span class="sxs-lookup"><span data-stu-id="6e8d2-108">Visit [the Preview Features page](https://account.windowsazure.com/PreviewFeatures) and enable **Billing Alert Service**.</span></span>

1. <span data-ttu-id="6e8d2-109">Получив по электронной почте подтверждение о том, что для вашей подписки включена служба выставления счетов, откройте страницу [Подписки](https://account.windowsazure.com/Subscriptions) на портале учетных записей.</span><span class="sxs-lookup"><span data-stu-id="6e8d2-109">After you receive the email confirmation that the billing service is turned on for your subscription, visit [the Subscriptions page](https://account.windowsazure.com/Subscriptions) in the account portal.</span></span> <span data-ttu-id="6e8d2-110">Выберите интересующую вас подписку и щелкните **Оповещения**.</span><span class="sxs-lookup"><span data-stu-id="6e8d2-110">Click the subscription you want to monitor, and then click **Alerts**.</span></span>

    ![Снимок экрана представления "Подписки" в Центре управления учетной записью Azure с выделенным элементом "Оповещения"][Image1]

2. <span data-ttu-id="6e8d2-112">Далее щелкните **Добавить оповещение**, чтобы создать первое из них.</span><span class="sxs-lookup"><span data-stu-id="6e8d2-112">Next, click **Add Alert** to create your first one.</span></span> <span data-ttu-id="6e8d2-113">Всего для каждой подписки можно настроить до пяти оповещений с различными пороговыми значениями и до двух адресатов электронной почты.</span><span class="sxs-lookup"><span data-stu-id="6e8d2-113">You can set up a total of five billing alerts per subscription, with a different threshold and up to two email recipients for each alert.</span></span>

    ![Снимок экрана представления "Оповещения", в котором можно добавить оповещение][Image2]

3. <span data-ttu-id="6e8d2-115">При добавлении оповещения присвойте ему уникальное имя, укажите пороговое значение расхода и выберите адреса электронной почты, куда будут отправляться оповещения.</span><span class="sxs-lookup"><span data-stu-id="6e8d2-115">When you add an alert, you give it a unique name, choose a spending threshold, and choose the email addresses where alerts are sent.</span></span> <span data-ttu-id="6e8d2-116">При настройке порогового значения можно выбрать либо **Счет всего**, либо **Денежный кредит** из списка **Оповещение для**.</span><span class="sxs-lookup"><span data-stu-id="6e8d2-116">When setting up the threshold, you can choose either a **Billing Total** or a **Monetary Credit** from the **Alert For** list.</span></span> <span data-ttu-id="6e8d2-117">Для общего счета предупреждение отправляется, когда затраты по подписке превышают пороговое значение.</span><span class="sxs-lookup"><span data-stu-id="6e8d2-117">For a billing total, an alert is sent when subscription spending exceeds the threshold.</span></span> <span data-ttu-id="6e8d2-118">Для денежного кредита предупреждение отправляется тогда, когда сумма денежного кредита стала ниже заданного предела.</span><span class="sxs-lookup"><span data-stu-id="6e8d2-118">For a monetary credit, an alert is sent when monetary credits drop below the limit.</span></span> <span data-ttu-id="6e8d2-119">Денежные кредиты обычно применяются к подпискам бесплатной пробной версии и Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6e8d2-119">Monetary credits usually apply to Free Trial and Visual Studio subscriptions.</span></span>

    ![Снимок экрана представления "Добавить оповещение", в котором можно настроить получателей][Image3]

<span data-ttu-id="6e8d2-121">Azure поддерживает любой адрес электронной почты, но не проверяет их работоспособность, поэтому дважды перепроверьте правильность адреса.</span><span class="sxs-lookup"><span data-stu-id="6e8d2-121">Azure supports any email address but doesn't verify that the email address works, so double-check for typos.</span></span>

## <a name="check-on-your-alerts"></a><span data-ttu-id="6e8d2-122">Проверка настроенных предупреждений</span><span class="sxs-lookup"><span data-stu-id="6e8d2-122">Check on your alerts</span></span>
<span data-ttu-id="6e8d2-123">После настройки предупреждения они появятся в центре учетных записей. Кроме того, там будет показано, сколько предупреждений еще можно добавить.</span><span class="sxs-lookup"><span data-stu-id="6e8d2-123">After you set up alerts, the Account Center lists them and shows how many more you can set up.</span></span> <span data-ttu-id="6e8d2-124">Показывается дата и время отправки каждого предупреждения, его тип (по общему счету или по денежному кредиту) и настроенное предельное значение.</span><span class="sxs-lookup"><span data-stu-id="6e8d2-124">For each alert, you see the date and time it was sent, whether it’s an alert for Billing Total or Monetary Credit, and the limit you set up.</span></span> <span data-ttu-id="6e8d2-125">Время показывается в 24-часовом формате (UTC), дата в формате "гггг-мм-дд".</span><span class="sxs-lookup"><span data-stu-id="6e8d2-125">The date and time format is 24-hour Universal Time Coordinate (UTC) and the date is yyyy-mm-dd format.</span></span> <span data-ttu-id="6e8d2-126">Щелкните значок "плюс" рядом с оповещением в списке, чтобы изменить его. Чтобы удалить, щелкните значок корзины.</span><span class="sxs-lookup"><span data-stu-id="6e8d2-126">Click the plus sign for an alert in the list to edit it, or click the trash-can to delete it.</span></span>

## <a name="billing-alerts-for-enterprise-agreement-ea-customers"></a><span data-ttu-id="6e8d2-127">Оповещения о выставлении счетов для клиентов с соглашением Enterprise (EA)</span><span class="sxs-lookup"><span data-stu-id="6e8d2-127">Billing alerts for Enterprise Agreement (EA) customers</span></span>
<span data-ttu-id="6e8d2-128">Клиенты с соглашением Enterprise могут получать оповещения по каждому зарегистрированному отделу, задав параметры квот на расход.</span><span class="sxs-lookup"><span data-stu-id="6e8d2-128">EA customers can get alerts for each department under an enrollment by setting spending quotas.</span></span> <span data-ttu-id="6e8d2-129">Для начала ознакомьтесь со статьей о [квотах на расход для отделов](https://ea.azure.com/helpdocs/departmentSpendingQuotas) на портале EA.</span><span class="sxs-lookup"><span data-stu-id="6e8d2-129">See [Department Spending Quotas](https://ea.azure.com/helpdocs/departmentSpendingQuotas) in the EA portal to get started.</span></span>

## <a name="learn-more-about-azure-cost-management"></a><span data-ttu-id="6e8d2-130">Дополнительные сведения об управлении расходами</span><span class="sxs-lookup"><span data-stu-id="6e8d2-130">Learn more about Azure cost management</span></span>
- <span data-ttu-id="6e8d2-131">Оцените затраты с помощью [калькулятора цен](https://azure.microsoft.com/pricing/calculator/) и [калькулятора совокупной стоимости владения](https://aka.ms/azure-tco-calculator), а затем добавляйте службу.</span><span class="sxs-lookup"><span data-stu-id="6e8d2-131">Estimate costs using the [pricing calculator](https://azure.microsoft.com/pricing/calculator/), [total cost of ownership calculator](https://aka.ms/azure-tco-calculator), and when you add a service.</span></span>
- <span data-ttu-id="6e8d2-132">[Регулярно просматривайте сведения об использовании и затратах на портале Azure](billing-getting-started.md#costs).</span><span class="sxs-lookup"><span data-stu-id="6e8d2-132">[Review your usage and costs regularly in Azure portal](billing-getting-started.md#costs).</span></span>
- <span data-ttu-id="6e8d2-133">Включите [рекомендации Azure Advisor по затратам](../advisor/advisor-cost-recommendations.md).</span><span class="sxs-lookup"><span data-stu-id="6e8d2-133">Turn on [Azure Advisor cost recommendations](../advisor/advisor-cost-recommendations.md).</span></span>

<span data-ttu-id="6e8d2-134">Дополнительные сведения см. в статье [Приступая к работе с выставлением счетов и управлением затратами в Azure](billing-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="6e8d2-134">To learn more, see [Azure cost management guidance](billing-getting-started.md).</span></span>

[Image1]: ./media/azure-billing-set-up-alerts/billingalert1.png 
[Image2]: ./media/azure-billing-set-up-alerts/billingalert2.png
[Image3]: ./media/azure-billing-set-up-alerts/billingalerts3.png 
