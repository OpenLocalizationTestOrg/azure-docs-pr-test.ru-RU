---
title: "aaaResolve оповещений о работоспособности endpoint protection в центр безопасности Azure | Документы Microsoft"
description: "В этом документе показано, как tooimplement hello рекомендации центра безопасности Azure ** разрешить Endpoint Protection работоспособности оповещения **."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 4050f453-98fc-4314-8438-d476469757fb
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/01/2016
ms.author: terrylan
ms.openlocfilehash: 9631d15aa1dfa9003d56332363ae7911061ed0b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="resolve-endpoint-protection-health-alerts-in-azure-security-center"></a><span data-ttu-id="5e97e-103">Разрешение оповещений о работоспособности Endpoint Protection в центре безопасности Azure</span><span class="sxs-lookup"><span data-stu-id="5e97e-103">Resolve endpoint protection health alerts in Azure Security Center</span></span>
<span data-ttu-id="5e97e-104">Центр безопасности Azure будет рекомендовать разрешить выявленные оповещения о работоспособности Endpoint Protection.</span><span class="sxs-lookup"><span data-stu-id="5e97e-104">Azure Security Center will recommend that you resolve detected endpoint protection health alerts.</span></span>  <span data-ttu-id="5e97e-105">Центр обеспечения безопасности позволяет toosee виртуальных машин (ВМ) имеют сбоям защиты конечной точки и сколько.</span><span class="sxs-lookup"><span data-stu-id="5e97e-105">Security Center enables you toosee which virtual machines (VMs) have endpoint protection failures and how many failures.</span></span>

> [!NOTE]
> <span data-ttu-id="5e97e-106">В этом документе представлены hello службы с помощью пример развертывания.</span><span class="sxs-lookup"><span data-stu-id="5e97e-106">This document introduces hello service by using an example deployment.</span></span> <span data-ttu-id="5e97e-107">Он не является пошаговым руководством.</span><span class="sxs-lookup"><span data-stu-id="5e97e-107">This is not a step-by-step guide.</span></span>
> 
> 

## <a name="implement-hello-recommendation"></a><span data-ttu-id="5e97e-108">Реализация рекомендаций hello</span><span class="sxs-lookup"><span data-stu-id="5e97e-108">Implement hello recommendation</span></span>
1. <span data-ttu-id="5e97e-109">В hello **колонке рекомендации**выберите **оповещения о работоспособности Endpoint Protection Разрешить**.</span><span class="sxs-lookup"><span data-stu-id="5e97e-109">In hello **Recommendations blade**, select **Resolve Endpoint Protection health alerts**.</span></span>
   <span data-ttu-id="5e97e-110">![Разрешение оповещений о работоспособности Endpoint Protection][1]</span><span class="sxs-lookup"><span data-stu-id="5e97e-110">![Resolve endpoint protection health alerts][1]</span></span>
2. <span data-ttu-id="5e97e-111">Это открывает колонку hello **сбоя Endpoint Protection** в котором перечислены виртуальные машины с ошибками и hello количество отказов для каждой виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="5e97e-111">This opens hello blade **Endpoint Protection failure** which lists VMs with failures and hello number of failures for each VM.</span></span> <span data-ttu-id="5e97e-112">Выберите виртуальную Машину из списка hello.</span><span class="sxs-lookup"><span data-stu-id="5e97e-112">Select a VM from hello list.</span></span>
   <span data-ttu-id="5e97e-113">![Endpoint protection failure][2]</span><span class="sxs-lookup"><span data-stu-id="5e97e-113">![Endpoint protection failure][2]</span></span>
3. <span data-ttu-id="5e97e-114">Объект **список сбоев** открывает колонку для hello выбранных виртуальных Машин, отображается список ошибок.</span><span class="sxs-lookup"><span data-stu-id="5e97e-114">A **Failures List** blade opens for hello selected VM, displaying a list of failures.</span></span> <span data-ttu-id="5e97e-115">Выберите дополнительные toolearn список hello сбоя.</span><span class="sxs-lookup"><span data-stu-id="5e97e-115">Select a failure from hello list toolearn more.</span></span> <span data-ttu-id="5e97e-116">Откроется панель с информацией о сбое hello выбран.</span><span class="sxs-lookup"><span data-stu-id="5e97e-116">This opens a blade with information about hello selected failure.</span></span>
   <span data-ttu-id="5e97e-117">![Список сбоев][3]
   ![Событие сбоя][4]</span><span class="sxs-lookup"><span data-stu-id="5e97e-117">![Failures list][3]
![Failure event][4]</span></span>

## <a name="see-also"></a><span data-ttu-id="5e97e-118">См. также</span><span class="sxs-lookup"><span data-stu-id="5e97e-118">See also</span></span>
<span data-ttu-id="5e97e-119">toolearn Дополнительные сведения о центра обеспечения безопасности, см. ниже hello:</span><span class="sxs-lookup"><span data-stu-id="5e97e-119">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="5e97e-120">[Установка политики безопасности в центр безопасности Azure](security-center-policies.md)— Узнайте, как tooconfigure политики безопасности для вашей подписки Azure и группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="5e97e-120">[Setting security policies in Azure Security Center](security-center-policies.md)--Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="5e97e-121">[Управление рекомендациями по безопасности в Центре безопасности Azure](security-center-recommendations.md)— узнайте, как рекомендации могут помочь вам защитить ресурсы Azure.</span><span class="sxs-lookup"><span data-stu-id="5e97e-121">[Managing security recommendations in Azure Security Center](security-center-recommendations.md)--Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="5e97e-122">[Наблюдение за работоспособностью системы безопасности в центр безопасности Azure](security-center-monitoring.md)— Узнайте, как toomonitor hello работоспособности ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="5e97e-122">[Security health monitoring in Azure Security Center](security-center-monitoring.md)--Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="5e97e-123">[Управление и отвечает на запросы toosecurity предупреждения в центр безопасности Azure](security-center-managing-and-responding-alerts.md)--Узнайте, как предупреждения toosecurity toomanage и отправки ответа.</span><span class="sxs-lookup"><span data-stu-id="5e97e-123">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md)--Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="5e97e-124">[Мониторинг решений партнера с центром обеспечения безопасности Azure](security-center-partner-solutions.md) — Узнайте, как toomonitor hello состояние работоспособности решений для партнера.</span><span class="sxs-lookup"><span data-stu-id="5e97e-124">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="5e97e-125">[Центр безопасности Azure часто задаваемые вопросы о](security-center-faq.md)— часто задаваемые вопросы об использовании hello службы поиска.</span><span class="sxs-lookup"><span data-stu-id="5e97e-125">[Azure Security Center FAQ](security-center-faq.md)--Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="5e97e-126">[Блог Azure безопасности](http://blogs.msdn.com/b/azuresecurity/)--получить последние новости безопасности Azure hello и информацию.</span><span class="sxs-lookup"><span data-stu-id="5e97e-126">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/)--Get hello latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-resolve-endpoint-protection/resolve-endpoint-protection.png
[2]: ./media/security-center-resolve-endpoint-protection/endpoint-protection-failure.png
[3]: ./media/security-center-resolve-endpoint-protection/failure-list.png
[4]: ./media/security-center-resolve-endpoint-protection/failure-event.png
