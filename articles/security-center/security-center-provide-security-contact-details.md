---
title: "aaaProvide контактные сведения о безопасности в центр безопасности Azure | Документы Microsoft"
description: "В этом документе показано, как tooprovide безопасности контактные данные в центр безопасности Azure."
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
ms.openlocfilehash: 6c378c9c84c6e4fce70b2541e4cc121018700269
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="provide-security-contact-details-in-azure-security-center"></a><span data-ttu-id="b10e7-103">Предоставление сведений о контактных лицах по вопросам безопасности в центре безопасности Azure</span><span class="sxs-lookup"><span data-stu-id="b10e7-103">Provide security contact details in Azure Security Center</span></span>
<span data-ttu-id="b10e7-104">Центр безопасности Azure порекомендует вам предоставить сведения о контактных лицах по вопросам безопасности для подписки Azure, если это еще не сделано.</span><span class="sxs-lookup"><span data-stu-id="b10e7-104">Azure Security Center will recommend that you provide security contact details for your Azure subscription if you haven’t already.</span></span> <span data-ttu-id="b10e7-105">Эта информация будет использоваться Microsoft toocontact Если hello Microsoft Security Response Center (MSRC) обнаруживает, что стороной незаконной или несанкционированного осуществлялся данных клиента.</span><span class="sxs-lookup"><span data-stu-id="b10e7-105">This information will be used by Microsoft toocontact you if hello Microsoft Security Response Center (MSRC) discovers that your customer data has been accessed by an unlawful or unauthorized party.</span></span> <span data-ttu-id="b10e7-106">MSRC выполняет мониторинг выберите безопасности hello сети Azure и инфраструктуры и получает угроз аналитики и о нарушении жалобы сторонних производителей.</span><span class="sxs-lookup"><span data-stu-id="b10e7-106">MSRC performs select security monitoring of hello Azure network and infrastructure and receives threat intelligence and abuse complaints from third parties.</span></span>

<span data-ttu-id="b10e7-107">Уведомление по электронной почте отправляется на hello ежедневного первое предупреждение и только для высокого уровня серьезности предупреждения.</span><span class="sxs-lookup"><span data-stu-id="b10e7-107">An email notification is sent on hello first daily occurrence of an alert and only for high severity alerts.</span></span> <span data-ttu-id="b10e7-108">Параметры электронной почты можно настроить только для политик подписки.</span><span class="sxs-lookup"><span data-stu-id="b10e7-108">Email preferences can only be configured for subscription policies.</span></span> <span data-ttu-id="b10e7-109">Группы ресурсов в подписке унаследуют эти параметры.</span><span class="sxs-lookup"><span data-stu-id="b10e7-109">Resource groups within a subscription will inherit these settings.</span></span>

> [!NOTE]
> <span data-ttu-id="b10e7-110">В этом документе представлены hello службы с помощью пример развертывания.</span><span class="sxs-lookup"><span data-stu-id="b10e7-110">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="b10e7-111">Он не является пошаговым руководством.</span><span class="sxs-lookup"><span data-stu-id="b10e7-111">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="b10e7-112">Реализация рекомендаций hello</span><span class="sxs-lookup"><span data-stu-id="b10e7-112">Implement hello recommendation</span></span>
1. <span data-ttu-id="b10e7-113">В hello **рекомендации** колонке выберите **предоставить контактные сведения безопасности**.</span><span class="sxs-lookup"><span data-stu-id="b10e7-113">In hello **Recommendations** blade, select **Provide security contact details**.</span></span>
   <span data-ttu-id="b10e7-114">![Предоставление сведений о контактных лицах по вопросам безопасности][1]</span><span class="sxs-lookup"><span data-stu-id="b10e7-114">![Provide security contact][1]</span></span>
2. <span data-ttu-id="b10e7-115">Это открывает колонку hello **предоставить контактные сведения безопасности**.</span><span class="sxs-lookup"><span data-stu-id="b10e7-115">This opens hello blade **Provide security contact details**.</span></span> <span data-ttu-id="b10e7-116">Выберите hello подписки Azure tooprovide контактные данные.</span><span class="sxs-lookup"><span data-stu-id="b10e7-116">Select hello Azure subscription tooprovide contact information on.</span></span>
   <span data-ttu-id="b10e7-117">![Предоставление сведений о контактном лице по вопросам безопасности][2]</span><span class="sxs-lookup"><span data-stu-id="b10e7-117">![Provide security contact details][2]</span></span>
3. <span data-ttu-id="b10e7-118">Откроется вторая колонка **Укажите сведения о контактных лицах по вопросам безопасности** .</span><span class="sxs-lookup"><span data-stu-id="b10e7-118">A second **Provide security contact details** blade opens.</span></span>

   * <span data-ttu-id="b10e7-119">Введите hello безопасности контактный адрес электронной почты или адреса, разделенных запятыми.</span><span class="sxs-lookup"><span data-stu-id="b10e7-119">Enter hello security contact email address or addresses separated by commas.</span></span> <span data-ttu-id="b10e7-120">Не toohello ограничить количество адресов электронной почты, которые могут быть введены.</span><span class="sxs-lookup"><span data-stu-id="b10e7-120">There is not a limit toohello number of email addresses that you can enter.</span></span>
   * <span data-ttu-id="b10e7-121">Введите один международный телефонный номер контактного лица по вопросам безопасности.</span><span class="sxs-lookup"><span data-stu-id="b10e7-121">Enter one security contact international phone number.</span></span>
   * <span data-ttu-id="b10e7-122">tooreceive по электронной почте о предупреждения высокого уровня серьезности, включите параметр hello **отправить мне сообщение электронной почты об оповещениях**.</span><span class="sxs-lookup"><span data-stu-id="b10e7-122">tooreceive emails about high severity alerts, turn on hello option **Send me emails about alerts**.</span></span>
   * <span data-ttu-id="b10e7-123">В будущем hello будет иметь hello параметр toosend по электронной почте уведомления toosubscription владельцев.</span><span class="sxs-lookup"><span data-stu-id="b10e7-123">In hello future, you will have hello option toosend email notifications toosubscription owners.</span></span> <span data-ttu-id="b10e7-124">В настоящее время соответствующий параметр неактивен.</span><span class="sxs-lookup"><span data-stu-id="b10e7-124">This option is currently grayed out.</span></span>
   * <span data-ttu-id="b10e7-125">Выберите **ОК** tooapply hello безопасности обратитесь в службу подписки tooyour сведения.</span><span class="sxs-lookup"><span data-stu-id="b10e7-125">Select **OK** tooapply hello security contact information tooyour subscription.</span></span>

## <a name="see-also"></a><span data-ttu-id="b10e7-126">См. также</span><span class="sxs-lookup"><span data-stu-id="b10e7-126">See also</span></span>
<span data-ttu-id="b10e7-127">toolearn Дополнительные сведения о центра обеспечения безопасности, см. ниже hello:</span><span class="sxs-lookup"><span data-stu-id="b10e7-127">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="b10e7-128">[Установка политики безопасности в центр безопасности Azure](security-center-policies.md) — Узнайте, как tooconfigure политики безопасности для вашей подписки Azure и группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="b10e7-128">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="b10e7-129">[Управление рекомендациями по безопасности в Центре безопасности Azure](security-center-recommendations.md) — узнайте, как рекомендации могут помочь вам защитить ресурсы Azure.</span><span class="sxs-lookup"><span data-stu-id="b10e7-129">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="b10e7-130">[Наблюдение за работоспособностью системы безопасности в центр безопасности Azure](security-center-monitoring.md) — Узнайте, как toomonitor hello работоспособности ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="b10e7-130">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="b10e7-131">[Управление и отвечает на запросы toosecurity предупреждения в центр безопасности Azure](security-center-managing-and-responding-alerts.md) --Узнайте, как предупреждения toosecurity toomanage и отправки ответа.</span><span class="sxs-lookup"><span data-stu-id="b10e7-131">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="b10e7-132">[Мониторинг решений партнера с центром обеспечения безопасности Azure](security-center-partner-solutions.md) — Узнайте, как toomonitor hello состояние работоспособности решений для партнера.</span><span class="sxs-lookup"><span data-stu-id="b10e7-132">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="b10e7-133">[Центр безопасности Azure часто задаваемые вопросы о](security-center-faq.md) — часто задаваемые вопросы об использовании hello службы поиска.</span><span class="sxs-lookup"><span data-stu-id="b10e7-133">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="b10e7-134">[Блог Azure безопасности](http://blogs.msdn.com/b/azuresecurity/) --получить последние новости безопасности Azure hello и информацию.</span><span class="sxs-lookup"><span data-stu-id="b10e7-134">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get hello latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-provide-security-contacts/provide-contacts.png
[2]:./media/security-center-provide-security-contacts/provide-contact-details.png
