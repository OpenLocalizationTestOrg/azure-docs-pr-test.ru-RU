---
title: "aaaSet предупреждений выставления счетов или кредит для подписки Azure | Документы Microsoft"
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
ms.openlocfilehash: 711b9c72c59874792b0e229cdc5ec0fa517c24c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-billing-or-credit-alerts-for-your-microsoft-azure-subscriptions"></a><span data-ttu-id="b77bf-104">Настройка оповещений о выставлении счетов или предоставлении кредитов для подписок Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="b77bf-104">Set up billing or credit alerts for your Microsoft Azure subscriptions</span></span>
<span data-ttu-id="b77bf-105">Если вы hello администратора учетной записи для подписки Azure, можно использовать hello Azure выставления счетов службы оповещений выставления счетов toocreate настроить оповещения, помогающие отслеживать и управлять выставления счетов действия для учетных записей Azure.</span><span class="sxs-lookup"><span data-stu-id="b77bf-105">If you’re hello Account Admin for an Azure subscription, you can use hello Azure Billing Alert Service toocreate customized billing alerts that help you monitor and manage billing activity for your Azure accounts.</span></span>

<span data-ttu-id="b77bf-106">Эта служба является в предварительной версии, поэтому вам необходимо tooenable его странице предварительные версии функций hello сначала.</span><span class="sxs-lookup"><span data-stu-id="b77bf-106">This service is in preview, so you need tooenable it in hello Preview Features page first.</span></span>

## <a name="set-hello-alert-threshold-and-email-recipients"></a><span data-ttu-id="b77bf-107">Задать hello предупреждения пороговое значение и получателей электронной почты</span><span class="sxs-lookup"><span data-stu-id="b77bf-107">Set hello alert threshold and email recipients</span></span>
1. <span data-ttu-id="b77bf-108">Посетите [страницу предварительного просмотра функций hello](https://account.windowsazure.com/PreviewFeatures) и включить **выставления счетов службы оповещений**.</span><span class="sxs-lookup"><span data-stu-id="b77bf-108">Visit [hello Preview Features page](https://account.windowsazure.com/PreviewFeatures) and enable **Billing Alert Service**.</span></span>

1. <span data-ttu-id="b77bf-109">Получив подтверждение по электронной почте hello, служба выставления счетов hello включена для вашей подписки, посетите [hello страница «подписки»](https://account.windowsazure.com/Subscriptions) hello портала учетной записи.</span><span class="sxs-lookup"><span data-stu-id="b77bf-109">After you receive hello email confirmation that hello billing service is turned on for your subscription, visit [hello Subscriptions page](https://account.windowsazure.com/Subscriptions) in hello account portal.</span></span> <span data-ttu-id="b77bf-110">Щелкните подписку hello toomonitor и нажмите кнопку **предупреждения**.</span><span class="sxs-lookup"><span data-stu-id="b77bf-110">Click hello subscription you want toomonitor, and then click **Alerts**.</span></span>

    ![Снимок экрана: представление подписки hello центра учетную запись Azure с оповещений][Image1]

2. <span data-ttu-id="b77bf-112">Далее щелкните **Добавление оповещения** toocreate свое первое.</span><span class="sxs-lookup"><span data-stu-id="b77bf-112">Next, click **Add Alert** toocreate your first one.</span></span> <span data-ttu-id="b77bf-113">Можно задать копирование всего пять предупреждений о выставлении счета на подписку с различными порогами и копирование tootwo получателей электронной почты для каждого предупреждения.</span><span class="sxs-lookup"><span data-stu-id="b77bf-113">You can set up a total of five billing alerts per subscription, with a different threshold and up tootwo email recipients for each alert.</span></span>

    ![Снимок экрана: hello представлении "предупреждения", где можно добавлять оповещения][Image2]

3. <span data-ttu-id="b77bf-115">При добавлении оповещения, ей следует присвоить уникальное имя, выбрать порог оплаты и выберите hello адреса электронной почты, куда должны отправляться оповещения.</span><span class="sxs-lookup"><span data-stu-id="b77bf-115">When you add an alert, you give it a unique name, choose a spending threshold, and choose hello email addresses where alerts are sent.</span></span> <span data-ttu-id="b77bf-116">При настройке hello пороговое значение, можно выбрать либо **счет всего** или **денежный кредит** из hello **предупреждение для** списка.</span><span class="sxs-lookup"><span data-stu-id="b77bf-116">When setting up hello threshold, you can choose either a **Billing Total** or a **Monetary Credit** from hello **Alert For** list.</span></span> <span data-ttu-id="b77bf-117">Счет всего предупреждение отправляется, когда затраты по подписке превышает пороговое значение hello.</span><span class="sxs-lookup"><span data-stu-id="b77bf-117">For a billing total, an alert is sent when subscription spending exceeds hello threshold.</span></span> <span data-ttu-id="b77bf-118">Для «монетизированного кредита» предупреждение отправляется, когда монетизированные кредиты становятся ниже лимита hello.</span><span class="sxs-lookup"><span data-stu-id="b77bf-118">For a monetary credit, an alert is sent when monetary credits drop below hello limit.</span></span> <span data-ttu-id="b77bf-119">Денежные кредиты обычно применяются tooFree Visual Studio и пробной версии подписки.</span><span class="sxs-lookup"><span data-stu-id="b77bf-119">Monetary credits usually apply tooFree Trial and Visual Studio subscriptions.</span></span>

    ![Снимок экрана: hello предупреждения сложения представление, где можно настроить получателей][Image3]

<span data-ttu-id="b77bf-121">Azure поддерживает любой адрес электронной почты, но не убедитесь, что адрес электронной почты hello работает, поэтому следует внимательно опечаток.</span><span class="sxs-lookup"><span data-stu-id="b77bf-121">Azure supports any email address but doesn't verify that hello email address works, so double-check for typos.</span></span>

## <a name="check-on-your-alerts"></a><span data-ttu-id="b77bf-122">Проверка настроенных предупреждений</span><span class="sxs-lookup"><span data-stu-id="b77bf-122">Check on your alerts</span></span>
<span data-ttu-id="b77bf-123">После настройки предупреждения hello центр учетных записей их список и показывает, сколько более можно настроить.</span><span class="sxs-lookup"><span data-stu-id="b77bf-123">After you set up alerts, hello Account Center lists them and shows how many more you can set up.</span></span> <span data-ttu-id="b77bf-124">Для каждого предупреждения отображаются hello даты и времени, которое было отправлено, будь то оповещения счет всего или Денежный кредит, ограничение hello, которые вы настроили.</span><span class="sxs-lookup"><span data-stu-id="b77bf-124">For each alert, you see hello date and time it was sent, whether it’s an alert for Billing Total or Monetary Credit, and hello limit you set up.</span></span> <span data-ttu-id="b77bf-125">формат даты и времени Hello координации 24-часовом универсального времени (UTC), а hello дата имеет формат гггг мм дд.</span><span class="sxs-lookup"><span data-stu-id="b77bf-125">hello date and time format is 24-hour Universal Time Coordinate (UTC) and hello date is yyyy-mm-dd format.</span></span> <span data-ttu-id="b77bf-126">Щелкните hello, а также входа для оповещения в списке tooedit hello или hello Корзина toodelete его.</span><span class="sxs-lookup"><span data-stu-id="b77bf-126">Click hello plus sign for an alert in hello list tooedit it, or click hello trash-can toodelete it.</span></span>

## <a name="billing-alerts-for-enterprise-agreement-ea-customers"></a><span data-ttu-id="b77bf-127">Оповещения о выставлении счетов для клиентов с соглашением Enterprise (EA)</span><span class="sxs-lookup"><span data-stu-id="b77bf-127">Billing alerts for Enterprise Agreement (EA) customers</span></span>
<span data-ttu-id="b77bf-128">Клиенты с соглашением Enterprise могут получать оповещения по каждому зарегистрированному отделу, задав параметры квот на расход.</span><span class="sxs-lookup"><span data-stu-id="b77bf-128">EA customers can get alerts for each department under an enrollment by setting spending quotas.</span></span> <span data-ttu-id="b77bf-129">В разделе [квоты оплаты, отдел](https://ea.azure.com/helpdocs/departmentSpendingQuotas) в hello EA портала tooget работы.</span><span class="sxs-lookup"><span data-stu-id="b77bf-129">See [Department Spending Quotas](https://ea.azure.com/helpdocs/departmentSpendingQuotas) in hello EA portal tooget started.</span></span>

## <a name="learn-more-about-azure-cost-management"></a><span data-ttu-id="b77bf-130">Дополнительные сведения об управлении расходами</span><span class="sxs-lookup"><span data-stu-id="b77bf-130">Learn more about Azure cost management</span></span>
- <span data-ttu-id="b77bf-131">Оцените издержки с помощью hello [калькулятор](https://azure.microsoft.com/pricing/calculator/), [совокупную стоимость владения калькулятора](https://aka.ms/azure-tco-calculator), и при добавлении службы.</span><span class="sxs-lookup"><span data-stu-id="b77bf-131">Estimate costs using hello [pricing calculator](https://azure.microsoft.com/pricing/calculator/), [total cost of ownership calculator](https://aka.ms/azure-tco-calculator), and when you add a service.</span></span>
- <span data-ttu-id="b77bf-132">[Регулярно просматривайте сведения об использовании и затратах на портале Azure](billing-getting-started.md#costs).</span><span class="sxs-lookup"><span data-stu-id="b77bf-132">[Review your usage and costs regularly in Azure portal](billing-getting-started.md#costs).</span></span>
- <span data-ttu-id="b77bf-133">Включите [рекомендации Azure Advisor по затратам](../advisor/advisor-cost-recommendations.md).</span><span class="sxs-lookup"><span data-stu-id="b77bf-133">Turn on [Azure Advisor cost recommendations](../advisor/advisor-cost-recommendations.md).</span></span>

<span data-ttu-id="b77bf-134">toolearn более, в разделе [Azure стоимости руководства по управлению](billing-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="b77bf-134">toolearn more, see [Azure cost management guidance](billing-getting-started.md).</span></span>

[Image1]: ./media/azure-billing-set-up-alerts/billingalert1.png 
[Image2]: ./media/azure-billing-set-up-alerts/billingalert2.png
[Image3]: ./media/azure-billing-set-up-alerts/billingalerts3.png 
