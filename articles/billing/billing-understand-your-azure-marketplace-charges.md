---
title: "Основная информация о расходах на внешние службы в Azure | Документация Майкрософт"
description: "Узнайте больше о выставлении счетов за использование внешних служб, ранее известных как Marketplace, в Azure."
services: 
documentationcenter: 
author: adpick
manager: tonguyen
editor: 
tags: billing
ms.assetid: 5e0e2a3c-d111-4054-8508-0c111c1b749b
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: adpick
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 11701ce0162113ef6c8e056d3a30fe1d8f702f92
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="understand-your-azure-billing-for-external-service-charges"></a><span data-ttu-id="af2ea-103">Основные сведения о выставлении счетов за использование внешних служб в Azure</span><span class="sxs-lookup"><span data-stu-id="af2ea-103">Understand your Azure billing for external service charges</span></span>
<span data-ttu-id="af2ea-104">Ранее внешние службы назывались заказами Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="af2ea-104">External services used to be called Azure Marketplace.</span></span> <span data-ttu-id="af2ea-105">Обычно это службы, публикуемые сторонними поставщиками для использования в Azure, но при этом они полностью интегрируются в Azure.</span><span class="sxs-lookup"><span data-stu-id="af2ea-105">Generally, they're services published by third-parties available for Azure but are integrated completely within Azure.</span></span> <span data-ttu-id="af2ea-106">Например, ClearDB и SendGrid — это внешние службы, которые можно приобрести в Azure, но которые не опубликованы корпорацией Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="af2ea-106">For example, ClearDB and SendGrid are external services that you can purchase in Azure, but are not published by Microsoft.</span></span>

<span data-ttu-id="af2ea-107">При подготовке новой внешней службы или ресурса отображается предупреждение.</span><span class="sxs-lookup"><span data-stu-id="af2ea-107">When you provision a new external service or resource, a warning is shown:</span></span>

![Предупреждение о покупке Marketplace](./media/billing-understand-your-azure-marketplace-charges/marketplace-warning.PNG)

> [!NOTE]
> <span data-ttu-id="af2ea-109">Внешние службы публикуются компаниями, не принадлежащими корпорации Майкрософт, но иногда продукты Майкрософт также относят к внешним службам.</span><span class="sxs-lookup"><span data-stu-id="af2ea-109">External services are published by companies that are not Microsoft, but sometimes Microsoft products are also categorized as external services.</span></span>
> 
> 

## <a name="how-external-services-are-billed"></a><span data-ttu-id="af2ea-110">Как выставляются счета за внешние службы</span><span class="sxs-lookup"><span data-stu-id="af2ea-110">How external services are billed</span></span>
- <span data-ttu-id="af2ea-111">Счета за внешние службы выставляются отдельно.</span><span class="sxs-lookup"><span data-stu-id="af2ea-111">External services are billed separately.</span></span> <span data-ttu-id="af2ea-112">Они обрабатываются как отдельные заказы в подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="af2ea-112">They are treated as individual orders within your Azure subscription.</span></span> <span data-ttu-id="af2ea-113">Расчетный период для каждой службы задается при ее покупке.</span><span class="sxs-lookup"><span data-stu-id="af2ea-113">The billing period for each service is set when you purchase the service.</span></span> <span data-ttu-id="af2ea-114">Его не следует путать с расчетным периодом подписки, в которой вы приобрели службу.</span><span class="sxs-lookup"><span data-stu-id="af2ea-114">Not to be confused with the billing period of the subscription under which you purchased it.</span></span> <span data-ttu-id="af2ea-115">Вы будете получать отдельные счета, плата за которые будет отдельно взиматься с кредитной карты.</span><span class="sxs-lookup"><span data-stu-id="af2ea-115">You also receive separate bills and your credit card is charged separately.</span></span>
- <span data-ttu-id="af2ea-116">У каждой внешней службы своя модель выставления счетов.</span><span class="sxs-lookup"><span data-stu-id="af2ea-116">Each external service has a different billing model.</span></span> <span data-ttu-id="af2ea-117">Одни службы используют модель с оплатой по мере использования, другие — модель с ежемесячными платежами.</span><span class="sxs-lookup"><span data-stu-id="af2ea-117">Some services are billed in a pay-as-you-go fashion while others use a monthly based payment model.</span></span> <span data-ttu-id="af2ea-118">Для оплаты внешних служб Azure нужна кредитная карта, их нельзя приобрести посредством оплаты счета.</span><span class="sxs-lookup"><span data-stu-id="af2ea-118">You need a credit card for Azure external services, you can't buy external services with invoice pay.</span></span>
- <span data-ttu-id="af2ea-119">Для оплаты внешних служб невозможно использовать бесплатные кредитные средства.</span><span class="sxs-lookup"><span data-stu-id="af2ea-119">You can't use monthly free credits for external services.</span></span> <span data-ttu-id="af2ea-120">Если вы используете подписку Azure, которая включает в себя [бесплатные деньги на счете](https://azure.microsoft.com/pricing/spending-limits/), то ими невозможно оплачивать счета за внешние службы.</span><span class="sxs-lookup"><span data-stu-id="af2ea-120">If you are using an Azure subscription that includes [free credits](https://azure.microsoft.com/pricing/spending-limits/), they can't be applied to external service bills.</span></span> <span data-ttu-id="af2ea-121">Для покупки внешних служб используйте кредитную карту.</span><span class="sxs-lookup"><span data-stu-id="af2ea-121">Use a credit card to purchase external services.</span></span>


## <a name="view-external-service-spending-and-history-in-the-azure-portal"></a><span data-ttu-id="af2ea-122">Просмотр расходов на внешние службы и журнала на портале Azure</span><span class="sxs-lookup"><span data-stu-id="af2ea-122">View external service spending and history in the Azure portal</span></span>
<span data-ttu-id="af2ea-123">Можно просмотреть список внешних служб для каждой подписки на [портале Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="af2ea-123">You can view a list of the external services that are on each subscription within the [Azure portal](https://portal.azure.com/):</span></span> 

1. <span data-ttu-id="af2ea-124">Войдите на [портал Azure](https://portal.azure.com/) в качестве администратора учетной записи.</span><span class="sxs-lookup"><span data-stu-id="af2ea-124">Sign in to the [Azure portal](https://portal.azure.com/) as the account administrator.</span></span>
2. <span data-ttu-id="af2ea-125">В главном меню выберите **Подписки**.</span><span class="sxs-lookup"><span data-stu-id="af2ea-125">In the Hub menu, select **Subscriptions**.</span></span>
   
    ![Выбор пункта "Подписки" в главном меню](./media/billing-understand-your-azure-marketplace-charges/sub-button.png) 
3. <span data-ttu-id="af2ea-127">В колонке **Подписки** выберите подписку, которую нужно просмотреть, а затем щелкните **Внешние службы**.</span><span class="sxs-lookup"><span data-stu-id="af2ea-127">In the **Subscriptions** blade, select the subscription that you want to view, and then select **External services**.</span></span>
   
    ![Выберите подписку в колонке "Выставление счетов".](./media/billing-understand-your-azure-marketplace-charges/select-sub-external-services.png)
4. <span data-ttu-id="af2ea-129">Должны отобразиться все заказы внешних служб, включая имя издателя, приобретенный уровень служб, имя, присвоенное ресурсу, и текущее состояние заказа.</span><span class="sxs-lookup"><span data-stu-id="af2ea-129">You should see each of your external service orders, the publisher name, service tier you bought, name you gave the resource, and the current order status.</span></span> <span data-ttu-id="af2ea-130">Чтобы просмотреть предыдущие счета, выберите внешнюю службу.</span><span class="sxs-lookup"><span data-stu-id="af2ea-130">To see past bills, select an external service.</span></span>
   
    ![Выберите внешнюю службу.](./media/billing-understand-your-azure-marketplace-charges/external-service-blade2.png)
5. <span data-ttu-id="af2ea-132">Здесь можно просмотреть прошлые суммы счетов, включая разделение налога.</span><span class="sxs-lookup"><span data-stu-id="af2ea-132">From here, you can view past bill amounts including the tax breakdown.</span></span>
   
    ![Просмотрите журнал выставленных счетов за внешние службы.](./media/billing-understand-your-azure-marketplace-charges/billing-overview-blade.png)

## <a name="view-external-service-spending-for-enterprise-agreement-ea-customers"></a><span data-ttu-id="af2ea-134">Просмотр расходов на внешние службы для клиентов с соглашением Enterprise (EA)</span><span class="sxs-lookup"><span data-stu-id="af2ea-134">View external service spending for Enterprise Agreement (EA) customers</span></span>
<span data-ttu-id="af2ea-135">Клиенты с соглашением Enterprise могут просматривать данные о расходах на внешние службы и скачивать отчеты на портале EA.</span><span class="sxs-lookup"><span data-stu-id="af2ea-135">EA customers can see external service spending and download reports in the EA portal.</span></span> <span data-ttu-id="af2ea-136">Чтобы приступить к работе, см. статью [Azure Marketplace for EA Customers](https://ea.azure.com/helpdocs/azureMarketplace) (Azure Marketplace для клиентов с соглашением Enterprise).</span><span class="sxs-lookup"><span data-stu-id="af2ea-136">See [Azure Marketplace for EA Customers](https://ea.azure.com/helpdocs/azureMarketplace) to get started.</span></span>

## <a name="manage-payment-methods-for-external-service-orders"></a><span data-ttu-id="af2ea-137">Управление способами оплаты заказов внешних служб</span><span class="sxs-lookup"><span data-stu-id="af2ea-137">Manage payment methods for external service orders</span></span>
<span data-ttu-id="af2ea-138">Измените метод оплаты заказов внешних служб в [Центре управления учетной записью](https://account.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="af2ea-138">Update your payment methods for external service orders from the [Account Center](https://account.windowsazure.com/).</span></span>

> [!NOTE]
> <span data-ttu-id="af2ea-139">Если вы приобрели подписку с рабочей или учебной учетной записью, то [обратитесь в службу поддержки](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade), чтобы изменить метод оплаты.</span><span class="sxs-lookup"><span data-stu-id="af2ea-139">If you purchased your subscription with a Work or School account, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to make changes to your payment method.</span></span>
> 
> 

1. <span data-ttu-id="af2ea-140">Войдите в [Центр управления учетной записью](https://account.windowsazure.com/) и [перейдите на вкладку **Marketplace**](https://account.windowsazure.com/Store).</span><span class="sxs-lookup"><span data-stu-id="af2ea-140">Sign in to the [Account Center](https://account.windowsazure.com/) and [navigate to the **marketplace** tab](https://account.windowsazure.com/Store)</span></span>
   
    ![Выберите вкладку "Marketplace" в Центре управления учетной записью.](./media/billing-understand-your-azure-marketplace-charges/select-marketplace.png)
2. <span data-ttu-id="af2ea-142">Выберите внешнюю службу для управления.</span><span class="sxs-lookup"><span data-stu-id="af2ea-142">Select the external service you want to manage</span></span>
   
    ![Выберите внешнюю службу для управления.](./media/billing-understand-your-azure-marketplace-charges/select-ext-service.png)
3. <span data-ttu-id="af2ea-144">В правой части страницы щелкните **Изменить метод оплаты**.</span><span class="sxs-lookup"><span data-stu-id="af2ea-144">Click **Change payment method** on the right side of the page.</span></span> <span data-ttu-id="af2ea-145">Эта ссылка позволяет открыть другой портал для управления методом оплаты.</span><span class="sxs-lookup"><span data-stu-id="af2ea-145">This link brings you to a different portal to manage your payment method.</span></span>
   
    ![Сводка заказов](./media/billing-understand-your-azure-marketplace-charges/change-payment.PNG)
4. <span data-ttu-id="af2ea-147">Щелкните **Изменить информацию** и следуйте инструкциям, чтобы обновить платежную информацию.</span><span class="sxs-lookup"><span data-stu-id="af2ea-147">Click **Edit info** and follow instructions to update your payment information.</span></span>
   
    ![Выберите "Изменить информацию".](./media/billing-understand-your-azure-marketplace-charges/edit-info.png)

## <a name="cancel-an-external-service-order"></a><span data-ttu-id="af2ea-149">Отмена заказа внешней службы</span><span class="sxs-lookup"><span data-stu-id="af2ea-149">Cancel an external service order</span></span>
<span data-ttu-id="af2ea-150">Если вы хотите отменить заказ внешней службы, то удалите соответствующий ресурс на [портале Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="af2ea-150">If you want to cancel your external service order, delete the resource in the [Azure portal](https://portal.azure.com).</span></span>

![Удалите ресурс.](./media/billing-understand-your-azure-marketplace-charges/deleteMarketplaceOrder.PNG)

## <a name="need-help-contact-support"></a><span data-ttu-id="af2ea-152">Требуется помощь?</span><span class="sxs-lookup"><span data-stu-id="af2ea-152">Need help?</span></span> <span data-ttu-id="af2ea-153">Обратитесь в службу поддержки.</span><span class="sxs-lookup"><span data-stu-id="af2ea-153">Contact support.</span></span>
<span data-ttu-id="af2ea-154">Если у вас есть дополнительные вопросы, [обратитесь в службу поддержки](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade), которая поможет быстро устранить проблему.</span><span class="sxs-lookup"><span data-stu-id="af2ea-154">If you still have questions, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to get your issue resolved quickly.</span></span>

