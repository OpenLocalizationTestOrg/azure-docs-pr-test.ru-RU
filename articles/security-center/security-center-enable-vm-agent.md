---
title: "Включение агента виртуальной машины в центре безопасности Azure | Документация Майкрософт"
description: "В этом документе объясняется, как выполнить рекомендацию центра безопасности Azure **Включить агент виртуальной машины**."
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
ms.openlocfilehash: 337a7adfd93c76882a749685702bea6d1524c96a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="enable-vm-agent-in-azure-security-center"></a><span data-ttu-id="5aa35-103">Включение агента виртуальной машины в центре безопасности Azure</span><span class="sxs-lookup"><span data-stu-id="5aa35-103">Enable VM Agent in Azure Security Center</span></span>
<span data-ttu-id="5aa35-104">Чтобы [включить сбор данных](security-center-enable-data-collection.md), нужно установить агент виртуальной машины на виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="5aa35-104">The VM Agent must be installed on virtual machines (VMs) in order to [enable data collection](security-center-enable-data-collection.md).</span></span>  <span data-ttu-id="5aa35-105">Центр безопасности Azure позволяет узнать, для каких виртуальных машин требуется агент виртуальной машины, и рекомендует включить его на них.</span><span class="sxs-lookup"><span data-stu-id="5aa35-105">Azure Security Center enables you to see which VMs require the VM Agent and will recommend that you enable the VM Agent on those VMs.</span></span>

<span data-ttu-id="5aa35-106">Агент виртуальной машины устанавливается по умолчанию на виртуальных машинах, развернутых из Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="5aa35-106">The VM Agent is installed by default for VMs that are deployed from the Azure Marketplace.</span></span> <span data-ttu-id="5aa35-107">В статье [Агент виртуальной машины и расширения. Часть 2](https://azure.microsoft.com/blog/vm-agent-and-extensions-part-2/) содержатся сведения об установке агента ВМ.</span><span class="sxs-lookup"><span data-stu-id="5aa35-107">The article [VM Agent and Extensions – Part 2](https://azure.microsoft.com/blog/vm-agent-and-extensions-part-2/) provides information on how to install the VM Agent.</span></span>

> [!NOTE]
> <span data-ttu-id="5aa35-108">В документе приводится обзор службы с помощью примера развертывания.</span><span class="sxs-lookup"><span data-stu-id="5aa35-108">This document introduces the service by using an example deployment.</span></span> <span data-ttu-id="5aa35-109">Он не является пошаговым руководством.</span><span class="sxs-lookup"><span data-stu-id="5aa35-109">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="5aa35-110">Выполнение рекомендаций</span><span class="sxs-lookup"><span data-stu-id="5aa35-110">Implement the recommendation</span></span>
1. <span data-ttu-id="5aa35-111">В колонке **Рекомендации** выберите **Включить агент виртуальной машины**.</span><span class="sxs-lookup"><span data-stu-id="5aa35-111">In the **Recommendations blade**, select **Enable VM Agent**.</span></span>
   <span data-ttu-id="5aa35-112">![Включение агента виртуальной машины][1]</span><span class="sxs-lookup"><span data-stu-id="5aa35-112">![Enable VM Agent][1]</span></span>
2. <span data-ttu-id="5aa35-113">Откроется колонка **Агент виртуальной машины отсутствует или не отвечает**.</span><span class="sxs-lookup"><span data-stu-id="5aa35-113">This opens the blade **VM Agent Is Missing Or Not Responding**.</span></span> <span data-ttu-id="5aa35-114">Этой колонке перечислены виртуальные машины, на которые требуется установить агент виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="5aa35-114">This blade lists the VMs that require the VM Agent.</span></span> <span data-ttu-id="5aa35-115">Следуйте инструкциям в колонке, чтобы установить агент виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="5aa35-115">Follow the instructions on the blade to install the VM agent.</span></span>
   <span data-ttu-id="5aa35-116">![Агент виртуальной машины отсутствует][2]</span><span class="sxs-lookup"><span data-stu-id="5aa35-116">![VM Agent is missing][2]</span></span>

## <a name="see-also"></a><span data-ttu-id="5aa35-117">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="5aa35-117">See also</span></span>
<span data-ttu-id="5aa35-118">Дополнительные сведения о Центре безопасности см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="5aa35-118">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="5aa35-119">[Настройка политик безопасности в Центре безопасности Azure](security-center-policies.md)— узнайте, как настроить политики безопасности для подписок и групп ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="5aa35-119">[Setting security policies in Azure Security Center](security-center-policies.md)--Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="5aa35-120">[Управление рекомендациями по безопасности в Центре безопасности Azure](security-center-recommendations.md)— узнайте, как рекомендации могут помочь вам защитить ресурсы Azure.</span><span class="sxs-lookup"><span data-stu-id="5aa35-120">[Managing security recommendations in Azure Security Center](security-center-recommendations.md)--Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="5aa35-121">[Наблюдение за работоспособностью системы безопасности в центре безопасности Azure](security-center-monitoring.md)— узнайте, как наблюдать за работоспособностью ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="5aa35-121">[Security health monitoring in Azure Security Center](security-center-monitoring.md)--Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="5aa35-122">[Управление оповещениями безопасности в Центре безопасности Azure и реагирование на них](security-center-managing-and-responding-alerts.md)— узнайте, как управлять оповещениями системы безопасности и реагировать на них.</span><span class="sxs-lookup"><span data-stu-id="5aa35-122">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md)--Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="5aa35-123">[Мониторинг решений партнеров с помощью центра безопасности Azure](security-center-partner-solutions.md) — узнайте, как отслеживать состояние работоспособности решений партнеров.</span><span class="sxs-lookup"><span data-stu-id="5aa35-123">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="5aa35-124">[Центр безопасности Azure: часто задаваемые вопросы](security-center-faq.md)— часто задаваемые вопросы об использовании этой службы.</span><span class="sxs-lookup"><span data-stu-id="5aa35-124">[Azure Security Center FAQ](security-center-faq.md)--Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="5aa35-125">[Блог по безопасности Azure](http://blogs.msdn.com/b/azuresecurity/)— последние новости и информация об обеспечении безопасности в Azure.</span><span class="sxs-lookup"><span data-stu-id="5aa35-125">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/)--Get the latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-vm-agent/enable-vm-agent.png
[2]: ./media/security-center-enable-vm-agent/vm-agent-is-missing.png
