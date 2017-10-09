---
title: "aaaUnderstand Azure взимает плату внешней службы | Документы Microsoft"
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
ms.openlocfilehash: 1d2cb28319e2ab4eff753177220993cbf94c96ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="understand-your-azure-billing-for-external-service-charges"></a><span data-ttu-id="05ca3-103">Основные сведения о выставлении счетов за использование внешних служб в Azure</span><span class="sxs-lookup"><span data-stu-id="05ca3-103">Understand your Azure billing for external service charges</span></span>
<span data-ttu-id="05ca3-104">Внешние службы используется toobe вызывается Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="05ca3-104">External services used toobe called Azure Marketplace.</span></span> <span data-ttu-id="05ca3-105">Обычно это службы, публикуемые сторонними поставщиками для использования в Azure, но при этом они полностью интегрируются в Azure.</span><span class="sxs-lookup"><span data-stu-id="05ca3-105">Generally, they're services published by third-parties available for Azure but are integrated completely within Azure.</span></span> <span data-ttu-id="05ca3-106">Например, ClearDB и SendGrid — это внешние службы, которые можно приобрести в Azure, но которые не опубликованы корпорацией Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="05ca3-106">For example, ClearDB and SendGrid are external services that you can purchase in Azure, but are not published by Microsoft.</span></span>

<span data-ttu-id="05ca3-107">При подготовке новой внешней службы или ресурса отображается предупреждение.</span><span class="sxs-lookup"><span data-stu-id="05ca3-107">When you provision a new external service or resource, a warning is shown:</span></span>

![Предупреждение о покупке Marketplace](./media/billing-understand-your-azure-marketplace-charges/marketplace-warning.PNG)

> [!NOTE]
> <span data-ttu-id="05ca3-109">Внешние службы публикуются компаниями, не принадлежащими корпорации Майкрософт, но иногда продукты Майкрософт также относят к внешним службам.</span><span class="sxs-lookup"><span data-stu-id="05ca3-109">External services are published by companies that are not Microsoft, but sometimes Microsoft products are also categorized as external services.</span></span>
> 
> 

## <a name="how-external-services-are-billed"></a><span data-ttu-id="05ca3-110">Как выставляются счета за внешние службы</span><span class="sxs-lookup"><span data-stu-id="05ca3-110">How external services are billed</span></span>
- <span data-ttu-id="05ca3-111">Счета за внешние службы выставляются отдельно.</span><span class="sxs-lookup"><span data-stu-id="05ca3-111">External services are billed separately.</span></span> <span data-ttu-id="05ca3-112">Они обрабатываются как отдельные заказы в подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="05ca3-112">They are treated as individual orders within your Azure subscription.</span></span> <span data-ttu-id="05ca3-113">Hello расчетного периода для каждой службы задается при покупке hello службы.</span><span class="sxs-lookup"><span data-stu-id="05ca3-113">hello billing period for each service is set when you purchase hello service.</span></span> <span data-ttu-id="05ca3-114">Не toobe путать с hello расчетного периода подписки hello, под которой он был приобретен.</span><span class="sxs-lookup"><span data-stu-id="05ca3-114">Not toobe confused with hello billing period of hello subscription under which you purchased it.</span></span> <span data-ttu-id="05ca3-115">Вы будете получать отдельные счета, плата за которые будет отдельно взиматься с кредитной карты.</span><span class="sxs-lookup"><span data-stu-id="05ca3-115">You also receive separate bills and your credit card is charged separately.</span></span>
- <span data-ttu-id="05ca3-116">У каждой внешней службы своя модель выставления счетов.</span><span class="sxs-lookup"><span data-stu-id="05ca3-116">Each external service has a different billing model.</span></span> <span data-ttu-id="05ca3-117">Одни службы используют модель с оплатой по мере использования, другие — модель с ежемесячными платежами.</span><span class="sxs-lookup"><span data-stu-id="05ca3-117">Some services are billed in a pay-as-you-go fashion while others use a monthly based payment model.</span></span> <span data-ttu-id="05ca3-118">Для оплаты внешних служб Azure нужна кредитная карта, их нельзя приобрести посредством оплаты счета.</span><span class="sxs-lookup"><span data-stu-id="05ca3-118">You need a credit card for Azure external services, you can't buy external services with invoice pay.</span></span>
- <span data-ttu-id="05ca3-119">Для оплаты внешних служб невозможно использовать бесплатные кредитные средства.</span><span class="sxs-lookup"><span data-stu-id="05ca3-119">You can't use monthly free credits for external services.</span></span> <span data-ttu-id="05ca3-120">Если вы используете подписка Azure, которая включает [освободить кредиты](https://azure.microsoft.com/pricing/spending-limits/), они не может быть применен tooexternal службы спецификаций.</span><span class="sxs-lookup"><span data-stu-id="05ca3-120">If you are using an Azure subscription that includes [free credits](https://azure.microsoft.com/pricing/spending-limits/), they can't be applied tooexternal service bills.</span></span> <span data-ttu-id="05ca3-121">С помощью внешних служб toopurchase кредитной карты.</span><span class="sxs-lookup"><span data-stu-id="05ca3-121">Use a credit card toopurchase external services.</span></span>


## <a name="view-external-service-spending-and-history-in-hello-azure-portal"></a><span data-ttu-id="05ca3-122">Просмотр расходов внешней службы и журналом hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="05ca3-122">View external service spending and history in hello Azure portal</span></span>
<span data-ttu-id="05ca3-123">Можно просмотреть список hello внешних служб, которые находятся на каждой подписки в hello [портал Azure](https://portal.azure.com/):</span><span class="sxs-lookup"><span data-stu-id="05ca3-123">You can view a list of hello external services that are on each subscription within hello [Azure portal](https://portal.azure.com/):</span></span> 

1. <span data-ttu-id="05ca3-124">Войдите в toohello [портал Azure](https://portal.azure.com/) от имени учетной записи администратора hello.</span><span class="sxs-lookup"><span data-stu-id="05ca3-124">Sign in toohello [Azure portal](https://portal.azure.com/) as hello account administrator.</span></span>
2. <span data-ttu-id="05ca3-125">В главном меню hello, выберите **подписки**.</span><span class="sxs-lookup"><span data-stu-id="05ca3-125">In hello Hub menu, select **Subscriptions**.</span></span>
   
    ![Выберите в главном меню hello подписки](./media/billing-understand-your-azure-marketplace-charges/sub-button.png) 
3. <span data-ttu-id="05ca3-127">В hello **подписки** колонки, выберите hello подписки требуется tooview, а затем выберите **внешних служб**.</span><span class="sxs-lookup"><span data-stu-id="05ca3-127">In hello **Subscriptions** blade, select hello subscription that you want tooview, and then select **External services**.</span></span>
   
    ![Выберите подписку, в колонке выставления счетов hello](./media/billing-understand-your-azure-marketplace-charges/select-sub-external-services.png)
4. <span data-ttu-id="05ca3-129">Необходимо просмотреть заказы внешней службы, имя издателя hello, уровня службы, которые вы приобрели, названием ресурса hello и текущее состояние заказа hello.</span><span class="sxs-lookup"><span data-stu-id="05ca3-129">You should see each of your external service orders, hello publisher name, service tier you bought, name you gave hello resource, and hello current order status.</span></span> <span data-ttu-id="05ca3-130">toosee за счета, установите внешней службы.</span><span class="sxs-lookup"><span data-stu-id="05ca3-130">toosee past bills, select an external service.</span></span>
   
    ![Выберите внешнюю службу.](./media/billing-understand-your-azure-marketplace-charges/external-service-blade2.png)
5. <span data-ttu-id="05ca3-132">Здесь можно просмотреть за суммы счета, включая декомпозиции налога hello.</span><span class="sxs-lookup"><span data-stu-id="05ca3-132">From here, you can view past bill amounts including hello tax breakdown.</span></span>
   
    ![Просмотрите журнал выставленных счетов за внешние службы.](./media/billing-understand-your-azure-marketplace-charges/billing-overview-blade.png)

## <a name="view-external-service-spending-for-enterprise-agreement-ea-customers"></a><span data-ttu-id="05ca3-134">Просмотр расходов на внешние службы для клиентов с соглашением Enterprise (EA)</span><span class="sxs-lookup"><span data-stu-id="05ca3-134">View external service spending for Enterprise Agreement (EA) customers</span></span>
<span data-ttu-id="05ca3-135">EA клиенты могут увидеть тратит внешнюю службу и загрузить отчет в портале EA hello.</span><span class="sxs-lookup"><span data-stu-id="05ca3-135">EA customers can see external service spending and download reports in hello EA portal.</span></span> <span data-ttu-id="05ca3-136">В разделе [Azure Marketplace для клиентов EA](https://ea.azure.com/helpdocs/azureMarketplace) tooget работы.</span><span class="sxs-lookup"><span data-stu-id="05ca3-136">See [Azure Marketplace for EA Customers](https://ea.azure.com/helpdocs/azureMarketplace) tooget started.</span></span>

## <a name="manage-payment-methods-for-external-service-orders"></a><span data-ttu-id="05ca3-137">Управление способами оплаты заказов внешних служб</span><span class="sxs-lookup"><span data-stu-id="05ca3-137">Manage payment methods for external service orders</span></span>
<span data-ttu-id="05ca3-138">Обновление методов оплаты для внешней службы заказами hello [центр учетных записей](https://account.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="05ca3-138">Update your payment methods for external service orders from hello [Account Center](https://account.windowsazure.com/).</span></span>

> [!NOTE]
> <span data-ttu-id="05ca3-139">Если вы приобрели подписку с помощью учетной записи рабочего или учебного заведения, [обратитесь в службу поддержки](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) toomake изменяет способ оплаты tooyour.</span><span class="sxs-lookup"><span data-stu-id="05ca3-139">If you purchased your subscription with a Work or School account, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) toomake changes tooyour payment method.</span></span>
> 
> 

1. <span data-ttu-id="05ca3-140">Войдите в toohello [центр учетных записей](https://account.windowsazure.com/) и [перехода toohello **marketplace** вкладка](https://account.windowsazure.com/Store)</span><span class="sxs-lookup"><span data-stu-id="05ca3-140">Sign in toohello [Account Center](https://account.windowsazure.com/) and [navigate toohello **marketplace** tab](https://account.windowsazure.com/Store)</span></span>
   
    ![Выберите marketplace в центре учетных записей hello](./media/billing-understand-your-azure-marketplace-charges/select-marketplace.png)
2. <span data-ttu-id="05ca3-142">Выберите внешнюю службу hello требуется toomanage</span><span class="sxs-lookup"><span data-stu-id="05ca3-142">Select hello external service you want toomanage</span></span>
   
    ![Выберите внешнюю службу hello требуется toomanage](./media/billing-understand-your-azure-marketplace-charges/select-ext-service.png)
3. <span data-ttu-id="05ca3-144">Нажмите кнопку **изменить метод оплаты** hello правой части страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="05ca3-144">Click **Change payment method** on hello right side of hello page.</span></span> <span data-ttu-id="05ca3-145">Эта ссылка переводит вы tooa различных портала toomanage метод оплаты.</span><span class="sxs-lookup"><span data-stu-id="05ca3-145">This link brings you tooa different portal toomanage your payment method.</span></span>
   
    ![Сводка заказов](./media/billing-understand-your-azure-marketplace-charges/change-payment.PNG)
4. <span data-ttu-id="05ca3-147">Нажмите кнопку **изменить сведения о** и следуйте инструкциям tooupdate платежную информацию.</span><span class="sxs-lookup"><span data-stu-id="05ca3-147">Click **Edit info** and follow instructions tooupdate your payment information.</span></span>
   
    ![Выберите "Изменить информацию".](./media/billing-understand-your-azure-marketplace-charges/edit-info.png)

## <a name="cancel-an-external-service-order"></a><span data-ttu-id="05ca3-149">Отмена заказа внешней службы</span><span class="sxs-lookup"><span data-stu-id="05ca3-149">Cancel an external service order</span></span>
<span data-ttu-id="05ca3-150">Toocancel ваш заказ внешней службы, удалить ресурс hello в hello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="05ca3-150">If you want toocancel your external service order, delete hello resource in hello [Azure portal](https://portal.azure.com).</span></span>

![Удалите ресурс.](./media/billing-understand-your-azure-marketplace-charges/deleteMarketplaceOrder.PNG)

## <a name="need-help-contact-support"></a><span data-ttu-id="05ca3-152">Требуется помощь?</span><span class="sxs-lookup"><span data-stu-id="05ca3-152">Need help?</span></span> <span data-ttu-id="05ca3-153">Обратитесь в службу поддержки.</span><span class="sxs-lookup"><span data-stu-id="05ca3-153">Contact support.</span></span>
<span data-ttu-id="05ca3-154">Если у вас есть вопросы, [обратитесь в службу поддержки](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget быстро устранить проблему.</span><span class="sxs-lookup"><span data-stu-id="05ca3-154">If you still have questions, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget your issue resolved quickly.</span></span>

