---
title: "aaaInstall Endpoint Protection в центр безопасности Azure | Документы Microsoft"
description: "В этом документе показано, как tooimplement hello рекомендации центра безопасности Azure ** установить Endpoint Protection **."
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
ms.openlocfilehash: fea891810e042e4d4f6e55094c0cd4de013ba68a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="install-endpoint-protection-in-azure-security-center"></a><span data-ttu-id="181a2-103">Установка Endpoint Protection в центре безопасности Azure</span><span class="sxs-lookup"><span data-stu-id="181a2-103">Install Endpoint Protection in Azure Security Center</span></span>
<span data-ttu-id="181a2-104">Центр безопасности Azure рекомендует установить решение для защиты конечных точек на виртуальных машинах Azure, если оно еще не включено.</span><span class="sxs-lookup"><span data-stu-id="181a2-104">Azure Security Center recommends that you install endpoint protection on your Azure virtual machines (VMs) if endpoint protection is not already enabled.</span></span> <span data-ttu-id="181a2-105">Данная рекомендация применяется tooWindows только для виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="181a2-105">This recommendation applies tooWindows VMs only.</span></span>

> [!NOTE]
> <span data-ttu-id="181a2-106">В этом примере развертывания используется антивредоносное ПО Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="181a2-106">This example deployment uses Microsoft Antimalware.</span></span> <span data-ttu-id="181a2-107">Список партнеров, решения которых интегрированы с центром безопасности, см. в статье [Интеграция партнеров в центре безопасности Azure](security-center-partner-integration.md#partners-that-integrate-with-security-center).</span><span class="sxs-lookup"><span data-stu-id="181a2-107">See [Partner Integration in Azure Security Center](security-center-partner-integration.md#partners-that-integrate-with-security-center) for a list of partners integrated with Security Center.</span></span>  
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="181a2-108">Реализация рекомендаций hello</span><span class="sxs-lookup"><span data-stu-id="181a2-108">Implement hello recommendation</span></span>

> [!NOTE]
> <span data-ttu-id="181a2-109">В этом документе представлены hello службы с помощью пример развертывания.</span><span class="sxs-lookup"><span data-stu-id="181a2-109">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="181a2-110">Этот документ не является пошаговым руководством.</span><span class="sxs-lookup"><span data-stu-id="181a2-110">This document is not a step-by-step guide.</span></span>
>
>

1. <span data-ttu-id="181a2-111">В hello **рекомендации** колонке выберите **установить Endpoint Protection**.</span><span class="sxs-lookup"><span data-stu-id="181a2-111">In hello **Recommendations** blade, select **Install Endpoint Protection**.</span></span>
   <span data-ttu-id="181a2-112">![Выберите "Установить Endpoint Protection"][1]</span><span class="sxs-lookup"><span data-stu-id="181a2-112">![Select Install Endpoint Protection][1]</span></span>
2. <span data-ttu-id="181a2-113">Hello **установить Endpoint Protection** открывается колонка, отображающая список виртуальных машин без защиты конечной точки.</span><span class="sxs-lookup"><span data-stu-id="181a2-113">hello **Install Endpoint Protection** blade opens displaying a list of VMs without endpoint protection.</span></span> <span data-ttu-id="181a2-114">Выберите из списка hello hello виртуальных машин, которые требуются tooinstall endpoint protection и нажмите кнопку **установить на виртуальных машинах**.</span><span class="sxs-lookup"><span data-stu-id="181a2-114">Select from hello list hello VMs that you want tooinstall endpoint protection on and click **Install on VMs**.</span></span>
   <span data-ttu-id="181a2-115">![Выберите виртуальные машины tooinstall Endpoint Protection на][2]</span><span class="sxs-lookup"><span data-stu-id="181a2-115">![Select VMs tooinstall Endpoint Protection on][2]</span></span>
3. <span data-ttu-id="181a2-116">Hello **выберите Endpoint Protection** tooallow открывает колонку вы tooselect hello endpoint protection решения, нужно toouse.</span><span class="sxs-lookup"><span data-stu-id="181a2-116">hello **Select Endpoint Protection** blade opens tooallow you tooselect hello endpoint protection solution you want toouse.</span></span> <span data-ttu-id="181a2-117">В этом примере мы выберем **Антивредоносное ПО Майкрософт**.</span><span class="sxs-lookup"><span data-stu-id="181a2-117">In this example, let's select **Microsoft Antimalware**.</span></span>
   <span data-ttu-id="181a2-118">![Select Endpoint Protection][3]</span><span class="sxs-lookup"><span data-stu-id="181a2-118">![Select Endpoint Protection][3]</span></span>
4. <span data-ttu-id="181a2-119">Дополнительные сведения о hello решение для защиты конечной точки отображаются.</span><span class="sxs-lookup"><span data-stu-id="181a2-119">Additional information about hello endpoint protection solution is displayed.</span></span> <span data-ttu-id="181a2-120">Нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="181a2-120">Select **Create**.</span></span>
   <span data-ttu-id="181a2-121">![Создание решения для защиты от вредоносных программ][4]</span><span class="sxs-lookup"><span data-stu-id="181a2-121">![Create antimalware solution][4]</span></span>
5. <span data-ttu-id="181a2-122">Введите hello необходимые параметры конфигурации на hello **расширения Add** колонки, а затем выберите **ОК**.</span><span class="sxs-lookup"><span data-stu-id="181a2-122">Enter hello required configuration settings on hello **Add Extension** blade, and then select **OK**.</span></span> <span data-ttu-id="181a2-123">в разделе toolearn Дополнительные сведения о параметрах конфигурации hello, [по умолчанию и защиты от вредоносных программ Настраиваемая конфигурация](../security/azure-security-antimalware.md#default-and-custom-antimalware-configuration).</span><span class="sxs-lookup"><span data-stu-id="181a2-123">toolearn more about hello configuration settings, see [Default and Custom Antimalware Configuration](../security/azure-security-antimalware.md#default-and-custom-antimalware-configuration).</span></span>

<span data-ttu-id="181a2-124">[Microsoft Antimalware](../security/azure-security-antimalware.md) теперь активно hello выбранные виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="181a2-124">[Microsoft Antimalware](../security/azure-security-antimalware.md) is now active on hello selected VMs.</span></span>

## <a name="see-also"></a><span data-ttu-id="181a2-125">См. также</span><span class="sxs-lookup"><span data-stu-id="181a2-125">See also</span></span>
<span data-ttu-id="181a2-126">В этой статье показано, как tooimplement hello рекомендации центра обеспечения безопасности «Установить Endpoint Protection».</span><span class="sxs-lookup"><span data-stu-id="181a2-126">This article showed you how tooimplement hello Security Center recommendation "Install Endpoint Protection."</span></span> <span data-ttu-id="181a2-127">toolearn Дополнительные сведения о включении защиты от вредоносных программ Майкрософт в Azure, см. следующий документ hello.</span><span class="sxs-lookup"><span data-stu-id="181a2-127">toolearn more about enabling Microsoft Antimalware in Azure, see hello following document:</span></span>

* <span data-ttu-id="181a2-128">[Microsoft Antimalware для облачных служб и виртуальных машин](../security/azure-security-antimalware.md) — Узнайте, как toodeploy Майкрософт защиты от вредоносных программ.</span><span class="sxs-lookup"><span data-stu-id="181a2-128">[Microsoft Antimalware for Cloud Services and Virtual Machines](../security/azure-security-antimalware.md) -- Learn how toodeploy Microsoft Antimalware.</span></span>

<span data-ttu-id="181a2-129">toolearn Дополнительные сведения о центра обеспечения безопасности, см. следующие документы hello.</span><span class="sxs-lookup"><span data-stu-id="181a2-129">toolearn more about Security Center, see hello following documents:</span></span>

* <span data-ttu-id="181a2-130">[Установка политики безопасности в центр безопасности Azure](security-center-policies.md) — Узнайте, как tooconfigure политики безопасности.</span><span class="sxs-lookup"><span data-stu-id="181a2-130">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies.</span></span>
* <span data-ttu-id="181a2-131">[Управление рекомендациями по безопасности в Центре безопасности Azure](security-center-recommendations.md) — узнайте, как рекомендации могут помочь вам защитить ресурсы Azure.</span><span class="sxs-lookup"><span data-stu-id="181a2-131">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="181a2-132">[Наблюдение за работоспособностью системы безопасности в центр безопасности Azure](security-center-monitoring.md) — Узнайте, как toomonitor hello работоспособности ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="181a2-132">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="181a2-133">[Управление и отвечает на запросы toosecurity предупреждения в центр безопасности Azure](security-center-managing-and-responding-alerts.md) --Узнайте, как предупреждения toosecurity toomanage и отправки ответа.</span><span class="sxs-lookup"><span data-stu-id="181a2-133">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="181a2-134">[Мониторинг решений партнера с центром обеспечения безопасности Azure](security-center-partner-solutions.md) — Узнайте, как toomonitor hello состояние работоспособности решений для партнера.</span><span class="sxs-lookup"><span data-stu-id="181a2-134">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="181a2-135">[Центр безопасности Azure часто задаваемые вопросы о](security-center-faq.md) — часто задаваемые вопросы об использовании hello службы поиска.</span><span class="sxs-lookup"><span data-stu-id="181a2-135">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="181a2-136">[Блог по безопасности Azure](http://blogs.msdn.com/b/azuresecurity/) — публикации блога, посвященные безопасности и соответствию требованиям в Azure.</span><span class="sxs-lookup"><span data-stu-id="181a2-136">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]:./media/security-center-install-endpoint-protection/select-install-endpoint-protection.png
[2]:./media/security-center-install-endpoint-protection/install-endpoint-protection-blade.png
[3]:./media/security-center-install-endpoint-protection/select-endpoint-protection.png
[4]:./media/security-center-install-endpoint-protection/create-antimalware-solution.png
