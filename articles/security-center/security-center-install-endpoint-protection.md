---
title: "Установка Endpoint Protection в центре безопасности Azure | Документация Майкрософт"
description: "В этом документе объясняется, как выполнить рекомендацию центра безопасности Azure **Установить Endpoint Protection**."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 1599ad5f-d810-421d-aafc-892e831b403f
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: terrylan
ms.openlocfilehash: efb86a0ae362c30a6772c391a499154b7ae2a697
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="install-endpoint-protection-in-azure-security-center"></a><span data-ttu-id="c2ef2-103">Установка Endpoint Protection в центре безопасности Azure</span><span class="sxs-lookup"><span data-stu-id="c2ef2-103">Install Endpoint Protection in Azure Security Center</span></span>
<span data-ttu-id="c2ef2-104">Центр безопасности Azure рекомендует установить решение для защиты конечных точек на виртуальных машинах Azure, если оно еще не включено.</span><span class="sxs-lookup"><span data-stu-id="c2ef2-104">Azure Security Center recommends that you install endpoint protection on your Azure virtual machines (VMs) if endpoint protection is not already enabled.</span></span> <span data-ttu-id="c2ef2-105">Эта рекомендация относится только к виртуальным машинам Windows.</span><span class="sxs-lookup"><span data-stu-id="c2ef2-105">This recommendation applies to Windows VMs only.</span></span>

> [!NOTE]
> <span data-ttu-id="c2ef2-106">В этом примере развертывания используется антивредоносное ПО Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="c2ef2-106">This example deployment uses Microsoft Antimalware.</span></span> <span data-ttu-id="c2ef2-107">Список партнеров, решения которых интегрированы с центром безопасности, см. в статье [Интеграция партнеров в центре безопасности Azure](security-center-partner-integration.md#partners-that-integrate-with-security-center).</span><span class="sxs-lookup"><span data-stu-id="c2ef2-107">See [Partner Integration in Azure Security Center](security-center-partner-integration.md#partners-that-integrate-with-security-center) for a list of partners integrated with Security Center.</span></span>  
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="c2ef2-108">Выполнение рекомендаций</span><span class="sxs-lookup"><span data-stu-id="c2ef2-108">Implement the recommendation</span></span>

> [!NOTE]
> <span data-ttu-id="c2ef2-109">В документе приводится обзор службы с помощью примера развертывания.</span><span class="sxs-lookup"><span data-stu-id="c2ef2-109">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="c2ef2-110">Этот документ не является пошаговым руководством.</span><span class="sxs-lookup"><span data-stu-id="c2ef2-110">This document is not a step-by-step guide.</span></span>
>
>

1. <span data-ttu-id="c2ef2-111">В колонке **Рекомендации** выберите **Установить Endpoint Protection**.</span><span class="sxs-lookup"><span data-stu-id="c2ef2-111">In the **Recommendations** blade, select **Install Endpoint Protection**.</span></span>
   <span data-ttu-id="c2ef2-112">![Выберите "Установить Endpoint Protection"][1]</span><span class="sxs-lookup"><span data-stu-id="c2ef2-112">![Select Install Endpoint Protection][1]</span></span>
2. <span data-ttu-id="c2ef2-113">Откроется колонка **Установить Endpoint Protection** со списком виртуальных машин, на которых нет решения для защиты конечных точек.</span><span class="sxs-lookup"><span data-stu-id="c2ef2-113">The **Install Endpoint Protection** blade opens displaying a list of VMs without endpoint protection.</span></span> <span data-ttu-id="c2ef2-114">Выберите в списке виртуальные машины, на которых нужно установить решение для защиты конечных точек, и щелкните **Установить на виртуальных машинах**.</span><span class="sxs-lookup"><span data-stu-id="c2ef2-114">Select from the list the VMs that you want to install endpoint protection on and click **Install on VMs**.</span></span>
   <span data-ttu-id="c2ef2-115">![Выбор виртуальных машин для установки решения для защиты конечных точек][2]</span><span class="sxs-lookup"><span data-stu-id="c2ef2-115">![Select VMs to install Endpoint Protection on][2]</span></span>
3. <span data-ttu-id="c2ef2-116">Откроется колонка **Выбор Endpoint Protection**, в которой вы можете выбрать необходимое решение для защиты конечных точек.</span><span class="sxs-lookup"><span data-stu-id="c2ef2-116">The **Select Endpoint Protection** blade opens to allow you to select the endpoint protection solution you want to use.</span></span> <span data-ttu-id="c2ef2-117">В этом примере мы выберем **Антивредоносное ПО Майкрософт**.</span><span class="sxs-lookup"><span data-stu-id="c2ef2-117">In this example, let's select **Microsoft Antimalware**.</span></span>
   <span data-ttu-id="c2ef2-118">![Select Endpoint Protection][3]</span><span class="sxs-lookup"><span data-stu-id="c2ef2-118">![Select Endpoint Protection][3]</span></span>
4. <span data-ttu-id="c2ef2-119">Будут выведены дополнительные сведения о решении для защиты конечных точек.</span><span class="sxs-lookup"><span data-stu-id="c2ef2-119">Additional information about the endpoint protection solution is displayed.</span></span> <span data-ttu-id="c2ef2-120">Нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="c2ef2-120">Select **Create**.</span></span>
   <span data-ttu-id="c2ef2-121">![Создание решения для защиты от вредоносных программ][4]</span><span class="sxs-lookup"><span data-stu-id="c2ef2-121">![Create antimalware solution][4]</span></span>
5. <span data-ttu-id="c2ef2-122">В колонке **Добавить расширение** введите необходимые параметры конфигурации и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="c2ef2-122">Enter the required configuration settings on the **Add Extension** blade, and then select **OK**.</span></span> <span data-ttu-id="c2ef2-123">Дополнительные сведения о параметрах конфигурации см. в статье [Антивредоносное ПО Майкрософт для облачных служб и виртуальных машин Azure](../security/azure-security-antimalware.md#default-and-custom-antimalware-configuration).</span><span class="sxs-lookup"><span data-stu-id="c2ef2-123">To learn more about the configuration settings, see [Default and Custom Antimalware Configuration](../security/azure-security-antimalware.md#default-and-custom-antimalware-configuration).</span></span>

<span data-ttu-id="c2ef2-124">Теперь на выбранных виртуальных машинах включено [антивредоносное ПО Майкрософт](../security/azure-security-antimalware.md).</span><span class="sxs-lookup"><span data-stu-id="c2ef2-124">[Microsoft Antimalware](../security/azure-security-antimalware.md) is now active on the selected VMs.</span></span>

## <a name="see-also"></a><span data-ttu-id="c2ef2-125">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="c2ef2-125">See also</span></span>
<span data-ttu-id="c2ef2-126">В этой статье объясняется, как выполнить рекомендацию центра безопасности по установке Endpoint Protection.</span><span class="sxs-lookup"><span data-stu-id="c2ef2-126">This article showed you how to implement the Security Center recommendation "Install Endpoint Protection."</span></span> <span data-ttu-id="c2ef2-127">Дополнительные сведения о включении антивредоносного ПО Майкрософт в Azure см. в следующей статье:</span><span class="sxs-lookup"><span data-stu-id="c2ef2-127">To learn more about enabling Microsoft Antimalware in Azure, see the following document:</span></span>

* <span data-ttu-id="c2ef2-128">[Антивредоносное ПО Майкрософт для облачных служб и виртуальных машин Azure](../security/azure-security-antimalware.md) — узнайте, как развернуть антивредоносное ПО Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="c2ef2-128">[Microsoft Antimalware for Cloud Services and Virtual Machines](../security/azure-security-antimalware.md) -- Learn how to deploy Microsoft Antimalware.</span></span>

<span data-ttu-id="c2ef2-129">Дополнительные сведения о центре безопасности см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="c2ef2-129">To learn more about Security Center, see the following documents:</span></span>

* <span data-ttu-id="c2ef2-130">[Настройка политик безопасности в Центре безопасности Azure](security-center-policies.md) — узнайте, как настраивать политики безопасности.</span><span class="sxs-lookup"><span data-stu-id="c2ef2-130">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies.</span></span>
* <span data-ttu-id="c2ef2-131">[Управление рекомендациями по безопасности в Центре безопасности Azure](security-center-recommendations.md) — узнайте, как рекомендации могут помочь вам защитить ресурсы Azure.</span><span class="sxs-lookup"><span data-stu-id="c2ef2-131">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="c2ef2-132">[Наблюдение за работоспособностью системы безопасности в Центре безопасности Azure](security-center-monitoring.md) — узнайте, как наблюдать за работоспособностью ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="c2ef2-132">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="c2ef2-133">[Управление оповещениями безопасности в Центре безопасности Azure и реагирование на них](security-center-managing-and-responding-alerts.md) — узнайте, как управлять оповещениями системы безопасности и реагировать на них.</span><span class="sxs-lookup"><span data-stu-id="c2ef2-133">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="c2ef2-134">[Мониторинг решений партнеров с помощью центра безопасности Azure](security-center-partner-solutions.md) — узнайте, как отслеживать состояние работоспособности решений партнеров.</span><span class="sxs-lookup"><span data-stu-id="c2ef2-134">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="c2ef2-135">[Центр безопасности Azure: часто задаваемые вопросы](security-center-faq.md) — часто задаваемые вопросы об использовании этой службы.</span><span class="sxs-lookup"><span data-stu-id="c2ef2-135">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="c2ef2-136">[Блог по безопасности Azure](http://blogs.msdn.com/b/azuresecurity/) — публикации блога, посвященные безопасности и соответствию требованиям в Azure.</span><span class="sxs-lookup"><span data-stu-id="c2ef2-136">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]:./media/security-center-install-endpoint-protection/select-install-endpoint-protection.png
[2]:./media/security-center-install-endpoint-protection/install-endpoint-protection-blade.png
[3]:./media/security-center-install-endpoint-protection/select-endpoint-protection.png
[4]:./media/security-center-install-endpoint-protection/create-antimalware-solution.png
