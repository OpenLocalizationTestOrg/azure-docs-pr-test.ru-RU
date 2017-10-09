---
title: "aaaEnable агент виртуальной Машины в центр безопасности Azure | Документы Microsoft"
description: "В этом документе показано, как tooimplement hello рекомендации центра безопасности Azure ** включить ВМ агента **."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 5b431c25-4241-45b7-9556-cf2a1956f3da
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 9bd71e638b020780537da25fd4cf7baf34d3e11a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="enable-vm-agent-in-azure-security-center"></a><span data-ttu-id="d861e-103">Включение агента виртуальной машины в центре безопасности Azure</span><span class="sxs-lookup"><span data-stu-id="d861e-103">Enable VM Agent in Azure Security Center</span></span>
<span data-ttu-id="d861e-104">Hello ВМ должен быть установлен агент на виртуальных машинах (ВМ) в порядке слишком[включить сбор данных](security-center-enable-data-collection.md).</span><span class="sxs-lookup"><span data-stu-id="d861e-104">hello VM Agent must be installed on virtual machines (VMs) in order too[enable data collection](security-center-enable-data-collection.md).</span></span>  <span data-ttu-id="d861e-105">Центр безопасности Azure позволяет вам toosee которого требуются виртуальные машины hello агент виртуальной Машины и рекомендует включить hello агент виртуальной Машины на этих виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="d861e-105">Azure Security Center enables you toosee which VMs require hello VM Agent and will recommend that you enable hello VM Agent on those VMs.</span></span>

<span data-ttu-id="d861e-106">Hello агент виртуальной Машины устанавливается по умолчанию для виртуальных машин, развернутых из hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="d861e-106">hello VM Agent is installed by default for VMs that are deployed from hello Azure Marketplace.</span></span> <span data-ttu-id="d861e-107">статья Hello [агент ВМ и расширения – часть 2](https://azure.microsoft.com/blog/vm-agent-and-extensions-part-2/) рассматривается как tooinstall hello агент виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="d861e-107">hello article [VM Agent and Extensions – Part 2](https://azure.microsoft.com/blog/vm-agent-and-extensions-part-2/) provides information on how tooinstall hello VM Agent.</span></span>

> [!NOTE]
> <span data-ttu-id="d861e-108">В этом документе представлены hello службы с помощью пример развертывания.</span><span class="sxs-lookup"><span data-stu-id="d861e-108">This document introduces hello service by using an example deployment.</span></span> <span data-ttu-id="d861e-109">Он не является пошаговым руководством.</span><span class="sxs-lookup"><span data-stu-id="d861e-109">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="d861e-110">Реализация рекомендаций hello</span><span class="sxs-lookup"><span data-stu-id="d861e-110">Implement hello recommendation</span></span>
1. <span data-ttu-id="d861e-111">В hello **колонке рекомендации**выберите **включить агент виртуальной Машины**.</span><span class="sxs-lookup"><span data-stu-id="d861e-111">In hello **Recommendations blade**, select **Enable VM Agent**.</span></span>
   <span data-ttu-id="d861e-112">![Включение агента виртуальной машины][1]</span><span class="sxs-lookup"><span data-stu-id="d861e-112">![Enable VM Agent][1]</span></span>
2. <span data-ttu-id="d861e-113">Это открывает колонку hello **виртуальной Машины отсутствует или не отвечает агент**.</span><span class="sxs-lookup"><span data-stu-id="d861e-113">This opens hello blade **VM Agent Is Missing Or Not Responding**.</span></span> <span data-ttu-id="d861e-114">Эта колонка перечислены hello виртуальных машин, требующих hello агент виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="d861e-114">This blade lists hello VMs that require hello VM Agent.</span></span> <span data-ttu-id="d861e-115">Следуйте инструкциям hello на агент виртуальной Машины hello tooinstall колонке hello.</span><span class="sxs-lookup"><span data-stu-id="d861e-115">Follow hello instructions on hello blade tooinstall hello VM agent.</span></span>
   <span data-ttu-id="d861e-116">![Агент виртуальной машины отсутствует][2]</span><span class="sxs-lookup"><span data-stu-id="d861e-116">![VM Agent is missing][2]</span></span>

## <a name="see-also"></a><span data-ttu-id="d861e-117">См. также</span><span class="sxs-lookup"><span data-stu-id="d861e-117">See also</span></span>
<span data-ttu-id="d861e-118">toolearn Дополнительные сведения о центра обеспечения безопасности, см. ниже hello:</span><span class="sxs-lookup"><span data-stu-id="d861e-118">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="d861e-119">[Установка политики безопасности в центр безопасности Azure](security-center-policies.md)— Узнайте, как tooconfigure политики безопасности для вашей подписки Azure и группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="d861e-119">[Setting security policies in Azure Security Center](security-center-policies.md)--Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="d861e-120">[Управление рекомендациями по безопасности в Центре безопасности Azure](security-center-recommendations.md)— узнайте, как рекомендации могут помочь вам защитить ресурсы Azure.</span><span class="sxs-lookup"><span data-stu-id="d861e-120">[Managing security recommendations in Azure Security Center](security-center-recommendations.md)--Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="d861e-121">[Наблюдение за работоспособностью системы безопасности в центр безопасности Azure](security-center-monitoring.md)— Узнайте, как toomonitor hello работоспособности ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="d861e-121">[Security health monitoring in Azure Security Center](security-center-monitoring.md)--Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="d861e-122">[Управление и отвечает на запросы toosecurity предупреждения в центр безопасности Azure](security-center-managing-and-responding-alerts.md)--Узнайте, как предупреждения toosecurity toomanage и отправки ответа.</span><span class="sxs-lookup"><span data-stu-id="d861e-122">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md)--Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="d861e-123">[Мониторинг решений партнера с центром обеспечения безопасности Azure](security-center-partner-solutions.md) — Узнайте, как toomonitor hello состояние работоспособности решений для партнера.</span><span class="sxs-lookup"><span data-stu-id="d861e-123">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="d861e-124">[Центр безопасности Azure часто задаваемые вопросы о](security-center-faq.md)— часто задаваемые вопросы об использовании hello службы поиска.</span><span class="sxs-lookup"><span data-stu-id="d861e-124">[Azure Security Center FAQ](security-center-faq.md)--Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="d861e-125">[Блог Azure безопасности](http://blogs.msdn.com/b/azuresecurity/)--получить последние новости безопасности Azure hello и информацию.</span><span class="sxs-lookup"><span data-stu-id="d861e-125">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/)--Get hello latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-vm-agent/enable-vm-agent.png
[2]: ./media/security-center-enable-vm-agent/vm-agent-is-missing.png
