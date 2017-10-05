---
title: "Предоставление сведений о контактных лицах по вопросам безопасности в центре безопасности Azure | Документация Майкрософт"
description: "В этом документе показано, как указать сведения о контактных лицах по вопросам безопасности в центре безопасности Azure."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 26b5dcb4-ce3f-4f22-8d56-d2bf743cfc90
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 1a6e5e915745dd3588fbc54b353daa947b1c4289
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="provide-security-contact-details-in-azure-security-center"></a><span data-ttu-id="359e9-103">Предоставление сведений о контактных лицах по вопросам безопасности в центре безопасности Azure</span><span class="sxs-lookup"><span data-stu-id="359e9-103">Provide security contact details in Azure Security Center</span></span>
<span data-ttu-id="359e9-104">Центр безопасности Azure порекомендует вам предоставить сведения о контактных лицах по вопросам безопасности для подписки Azure, если это еще не сделано.</span><span class="sxs-lookup"><span data-stu-id="359e9-104">Azure Security Center will recommend that you provide security contact details for your Azure subscription if you haven’t already.</span></span> <span data-ttu-id="359e9-105">Корпорация Майкрософт будет использовать эту информацию для связи с вами, если центр Microsoft Security Response Center (MSRC) обнаружит, что к вашим пользовательским данным был получен незаконный или несанкционированный доступ.</span><span class="sxs-lookup"><span data-stu-id="359e9-105">This information will be used by Microsoft to contact you if the Microsoft Security Response Center (MSRC) discovers that your customer data has been accessed by an unlawful or unauthorized party.</span></span> <span data-ttu-id="359e9-106">Центр Microsoft Security Response Center (MSRC) осуществляет выборочный мониторинг безопасности сети и инфраструктуры Azure, а также получает аналитические данные об угрозах и жалобы о нарушениях от третьих лиц.</span><span class="sxs-lookup"><span data-stu-id="359e9-106">MSRC performs select security monitoring of the Azure network and infrastructure and receives threat intelligence and abuse complaints from third parties.</span></span>

<span data-ttu-id="359e9-107">Уведомление по электронной почте отправляется для первого за день оповещения и только тогда, когда у него высокий уровень серьезности.</span><span class="sxs-lookup"><span data-stu-id="359e9-107">An email notification is sent on the first daily occurrence of an alert and only for high severity alerts.</span></span> <span data-ttu-id="359e9-108">Параметры электронной почты можно настроить только для политик подписки.</span><span class="sxs-lookup"><span data-stu-id="359e9-108">Email preferences can only be configured for subscription policies.</span></span> <span data-ttu-id="359e9-109">Группы ресурсов в подписке унаследуют эти параметры.</span><span class="sxs-lookup"><span data-stu-id="359e9-109">Resource groups within a subscription will inherit these settings.</span></span>

> [!NOTE]
> <span data-ttu-id="359e9-110">В документе приводится обзор службы с помощью примера развертывания.</span><span class="sxs-lookup"><span data-stu-id="359e9-110">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="359e9-111">Он не является пошаговым руководством.</span><span class="sxs-lookup"><span data-stu-id="359e9-111">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="359e9-112">Выполнение рекомендаций</span><span class="sxs-lookup"><span data-stu-id="359e9-112">Implement the recommendation</span></span>
1. <span data-ttu-id="359e9-113">В колонке **Рекомендации** выберите **Указать сведения о контактных лицах по вопросам безопасности**.</span><span class="sxs-lookup"><span data-stu-id="359e9-113">In the **Recommendations** blade, select **Provide security contact details**.</span></span>
   <span data-ttu-id="359e9-114">![Предоставление сведений о контактных лицах по вопросам безопасности][1]</span><span class="sxs-lookup"><span data-stu-id="359e9-114">![Provide security contact][1]</span></span>
2. <span data-ttu-id="359e9-115">Откроется колонка **Укажите сведения о контактных лицах по вопросам безопасности**.</span><span class="sxs-lookup"><span data-stu-id="359e9-115">This opens the blade **Provide security contact details**.</span></span> <span data-ttu-id="359e9-116">Выберите подписку Azure для предоставления контактных данных.</span><span class="sxs-lookup"><span data-stu-id="359e9-116">Select the Azure subscription to provide contact information on.</span></span>
   <span data-ttu-id="359e9-117">![Указать сведения о контактных лицах по вопросам безопасности][2]</span><span class="sxs-lookup"><span data-stu-id="359e9-117">![Provide security contact details][2]</span></span>
3. <span data-ttu-id="359e9-118">Откроется вторая колонка **Укажите сведения о контактных лицах по вопросам безопасности** .</span><span class="sxs-lookup"><span data-stu-id="359e9-118">A second **Provide security contact details** blade opens.</span></span>

   * <span data-ttu-id="359e9-119">Введите адрес или разделенные запятыми адреса электронной почты контактных лиц по вопросам безопасности.</span><span class="sxs-lookup"><span data-stu-id="359e9-119">Enter the security contact email address or addresses separated by commas.</span></span> <span data-ttu-id="359e9-120">Можно ввести неограниченное количество адресов электронной почты.</span><span class="sxs-lookup"><span data-stu-id="359e9-120">There is not a limit to the number of email addresses that you can enter.</span></span>
   * <span data-ttu-id="359e9-121">Введите один международный телефонный номер контактного лица по вопросам безопасности.</span><span class="sxs-lookup"><span data-stu-id="359e9-121">Enter one security contact international phone number.</span></span>
   * <span data-ttu-id="359e9-122">Чтобы получать по электронной почте оповещения с высоким уровнем серьезности, включите параметр **Send me emails about alerts**(Отправлять мне электронные сообщения об оповещениях).</span><span class="sxs-lookup"><span data-stu-id="359e9-122">To receive emails about high severity alerts, turn on the option **Send me emails about alerts**.</span></span>
   * <span data-ttu-id="359e9-123">В будущем появится возможность отправлять уведомления по электронной почте владельцам подписок.</span><span class="sxs-lookup"><span data-stu-id="359e9-123">In the future, you will have the option to send email notifications to subscription owners.</span></span> <span data-ttu-id="359e9-124">В настоящее время соответствующий параметр неактивен.</span><span class="sxs-lookup"><span data-stu-id="359e9-124">This option is currently grayed out.</span></span>
   * <span data-ttu-id="359e9-125">Нажмите кнопку **ОК** , чтобы применить сведения о контактных лицах по вопросам безопасности к своей подписке.</span><span class="sxs-lookup"><span data-stu-id="359e9-125">Select **OK** to apply the security contact information to your subscription.</span></span>

## <a name="see-also"></a><span data-ttu-id="359e9-126">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="359e9-126">See also</span></span>
<span data-ttu-id="359e9-127">Дополнительные сведения о Центре безопасности см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="359e9-127">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="359e9-128">[Настройка политик безопасности в Центре безопасности Azure](security-center-policies.md) — узнайте, как настроить политики безопасности для подписок и групп ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="359e9-128">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="359e9-129">[Управление рекомендациями по безопасности в Центре безопасности Azure](security-center-recommendations.md) — узнайте, как рекомендации могут помочь вам защитить ресурсы Azure.</span><span class="sxs-lookup"><span data-stu-id="359e9-129">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="359e9-130">[Наблюдение за работоспособностью системы безопасности в Центре безопасности Azure](security-center-monitoring.md) — узнайте, как наблюдать за работоспособностью ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="359e9-130">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="359e9-131">[Управление оповещениями безопасности в Центре безопасности Azure и реагирование на них](security-center-managing-and-responding-alerts.md) — узнайте, как управлять оповещениями системы безопасности и реагировать на них.</span><span class="sxs-lookup"><span data-stu-id="359e9-131">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="359e9-132">[Мониторинг решений партнеров с помощью центра безопасности Azure](security-center-partner-solutions.md) — узнайте, как отслеживать состояние работоспособности решений партнеров.</span><span class="sxs-lookup"><span data-stu-id="359e9-132">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="359e9-133">[Центр безопасности Azure: часто задаваемые вопросы](security-center-faq.md) — часто задаваемые вопросы об использовании этой службы.</span><span class="sxs-lookup"><span data-stu-id="359e9-133">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="359e9-134">[Блог по безопасности Azure](http://blogs.msdn.com/b/azuresecurity/) — последние новости и информация об обеспечении безопасности в Azure.</span><span class="sxs-lookup"><span data-stu-id="359e9-134">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get the latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-provide-security-contacts/provide-contacts.png
[2]:./media/security-center-provide-security-contacts/provide-contact-details.png
