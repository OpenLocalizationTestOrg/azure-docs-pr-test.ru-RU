---
title: "aaaPay для подписок Azure с накладной | Документы Microsoft"
description: "Описывает способ toopay для подписок Azure с накладной"
services: 
documentationcenter: 
author: genlin
manager: jlian
editor: 
tags: billing
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: genli
ms.openlocfilehash: 416890cc1e5109ef4d2bf6a9c2a779ba835f410c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="submit-a-request-toopay-azure-subscription-by-invoice"></a><span data-ttu-id="1733f-103">Отправка запроса toopay подписки Azure с накладной</span><span class="sxs-lookup"><span data-stu-id="1733f-103">Submit a request toopay Azure subscription by invoice</span></span>

<span data-ttu-id="1733f-104">Можно изменить метод оплаты hello для вашей подписки Azure tooinvoice путем отправки запроса tooAzure поддержки.</span><span class="sxs-lookup"><span data-stu-id="1733f-104">You can change hello payment method for your Azure subscription tooinvoice by submitting a request tooAzure support.</span></span> <span data-ttu-id="1733f-105">После утверждения запроса будут предложены инструкции о том, как tooset копирование подписку на метод оплаты счета hello.</span><span class="sxs-lookup"><span data-stu-id="1733f-105">Once your request is approved, you are provided instructions on how tooset up your subscription for hello invoice payment method.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="1733f-106">Оплата по счету доступна только для учетных записей организаций.</span><span class="sxs-lookup"><span data-stu-id="1733f-106">Invoice pay is only available for business accounts.</span></span>
> * <span data-ttu-id="1733f-107">[Сторонние и внешние службы](billing-understand-your-azure-marketplace-charges.md) не могут приобретаться или оплачиваться с помощью оплаты по счету.</span><span class="sxs-lookup"><span data-stu-id="1733f-107">[Third party and external services](billing-understand-your-azure-marketplace-charges.md) cannot be purchased or paid for using invoice pay.</span></span> <span data-ttu-id="1733f-108">Подписки содержит ресурсы из внешних служб, таких как ClearDB или SendGrid, они должны быть удалены перед изменением tooinvoice оплаты.</span><span class="sxs-lookup"><span data-stu-id="1733f-108">If your subscription contains resources from external services like ClearDB or SendGrid, they need be deleted before changing tooinvoice pay.</span></span> <span data-ttu-id="1733f-109">toopurchase внешних служб после переключения tooinvoice оплаты, вам потребуется отдельный подписка с кредитной или дебетовой картой.</span><span class="sxs-lookup"><span data-stu-id="1733f-109">toopurchase external services after switching tooinvoice pay, you need a separate subscription with a credit or debit card.</span></span>
> * <span data-ttu-id="1733f-110">При переключении tooinvoice оплаты не удастся переключиться назад toocredit или дебетовой карты платежа.</span><span class="sxs-lookup"><span data-stu-id="1733f-110">Once you switch tooinvoice pay, you can't switch back toocredit or debit card payment.</span></span>

## <a name="request-pay-by-invoice"></a><span data-ttu-id="1733f-111">Запрос оплаты по счету</span><span class="sxs-lookup"><span data-stu-id="1733f-111">Request pay by invoice</span></span>

1. <span data-ttu-id="1733f-112">Вход в hello [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="1733f-112">Sign into hello [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="1733f-113">Выберите **Справка и поддержка** > **Новый запрос на получение поддержки**.</span><span class="sxs-lookup"><span data-stu-id="1733f-113">Select **Help + support** > **New support request**.</span></span>

    ![Кнопка "Справка и поддержка"](./media/billing-how-to-pay-by-invoice/helpandsupport.png)
1. <span data-ttu-id="1733f-115">Выберите **выставления счетов** как тип проблемы hello, выберите подписку hello, для которого хотите toopay с накладной, выберите план поддержки и выберите **Далее**.</span><span class="sxs-lookup"><span data-stu-id="1733f-115">Select **Billing** as hello issue type, select hello subscription for which you want toopay by invoice, select a support plan, and then select **Next**.</span></span>
1. <span data-ttu-id="1733f-116">В hello **проблема** колонке выберите **производить оплату за счет** в hello **тип проблемы** поле.</span><span class="sxs-lookup"><span data-stu-id="1733f-116">In hello **Problem** blade, select **Pay by Invoice** in hello **Problem Type** box.</span></span>
1. <span data-ttu-id="1733f-117">Введите следующую информацию в hello hello **сведения** поле, а затем выберите **Далее**.</span><span class="sxs-lookup"><span data-stu-id="1733f-117">Enter hello following information in hello **Details** box, and then select **Next**.</span></span>

    * <span data-ttu-id="1733f-118">название компании;</span><span class="sxs-lookup"><span data-stu-id="1733f-118">Company name</span></span>
    * <span data-ttu-id="1733f-119">адрес выставления счетов;</span><span class="sxs-lookup"><span data-stu-id="1733f-119">Billing address</span></span>
    * [<span data-ttu-id="1733f-120">Адрес электронной почты администратора учетной записи</span><span class="sxs-lookup"><span data-stu-id="1733f-120">Account administrator's email address</span></span>](billing-add-change-azure-subscription-administrator.md#check-the-account-administrator-of-the-subscription)

1. <span data-ttu-id="1733f-121">Проверьте свои контактные данные и предпочтительный способ связи и нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="1733f-121">Verify your contact information and preferred contact method, and then click **Create**.</span></span>

<span data-ttu-id="1733f-122">Если необходимо toorun кредит проверить из-за hello сумма кредита, необходимые вам отправлено приложении проверки кредита.</span><span class="sxs-lookup"><span data-stu-id="1733f-122">If we need toorun a credit check because of hello amount of credit that you need, we send you a credit check application.</span></span> <span data-ttu-id="1733f-123">После отправки приложения hello hello кредит приложение может выполнять tooprocess 5 – 7 дней.</span><span class="sxs-lookup"><span data-stu-id="1733f-123">After you submit hello application, hello credit application can take 5-7 days tooprocess.</span></span>

## <a name="need-help-contact-support"></a><span data-ttu-id="1733f-124">Требуется помощь?</span><span class="sxs-lookup"><span data-stu-id="1733f-124">Need help?</span></span> <span data-ttu-id="1733f-125">Обратитесь в службу поддержки.</span><span class="sxs-lookup"><span data-stu-id="1733f-125">Contact support.</span></span>

<span data-ttu-id="1733f-126">Если вы по-прежнему нужна помощь, [обратитесь в службу поддержки](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget быстро устранить проблему.</span><span class="sxs-lookup"><span data-stu-id="1733f-126">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget your issue resolved quickly.</span></span>
