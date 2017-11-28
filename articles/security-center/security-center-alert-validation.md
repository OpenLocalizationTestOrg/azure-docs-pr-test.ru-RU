---
title: "Проверка оповещений в центре безопасности Azure | Документация Майкрософт"
description: "В этом документе вы ознакомитесь с процедурой проверки оповещений безопасности в Центре безопасности Azure."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: f8f17a55-e672-4d86-8ba9-6c3ce2e71a57
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/11/2017
ms.author: yurid
ms.openlocfilehash: 121b5d8f023a9b663d0e7af26dce8f81db27672c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="alerts-validation-in-azure-security-center"></a><span data-ttu-id="56095-103">Проверка оповещений в центре безопасности Azure</span><span class="sxs-lookup"><span data-stu-id="56095-103">Alerts Validation in Azure Security Center</span></span>
<span data-ttu-id="56095-104">Этот документ содержит информацию о том, как убедиться, что ваша система правильно настроена для оповещений центра безопасности Azure.</span><span class="sxs-lookup"><span data-stu-id="56095-104">This document helps you learn how to verify if your system is properly configured for Azure Security Center alerts.</span></span>

## <a name="what-are-security-alerts"></a><span data-ttu-id="56095-105">Что такое оповещения системы безопасности?</span><span class="sxs-lookup"><span data-stu-id="56095-105">What are security alerts?</span></span>
<span data-ttu-id="56095-106">Центр безопасности автоматически собирает, анализирует и объединяет данные журналов, поступающие от ресурсов Azure, сети и подключенных решений партнеров, таких как брандмауэры и решения для защиты конечных точек, для выявления и оповещения об угрозах.</span><span class="sxs-lookup"><span data-stu-id="56095-106">Security Center automatically collects, analyzes, and integrates log data from your Azure resources, the network, and connected partner solutions, like firewall and endpoint protection solutions, to detect and alert you to threats.</span></span> <span data-ttu-id="56095-107">Дополнительные сведения об оповещениях безопасности и их типах см. в статье [Управление оповещениями безопасности в Центре безопасности Azure и реагирование на них](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts) и [Основные сведения об оповещениях системы безопасности в центре безопасности Azure](https://docs.microsoft.com/azure/security-center/security-center-alerts-type).</span><span class="sxs-lookup"><span data-stu-id="56095-107">Read [Managing and responding to security alerts in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts) for more information about security alerts, and read [Understanding security alerts in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-alerts-type) to learn more about the different types of alerts.</span></span>

## <a name="alert-validation"></a><span data-ttu-id="56095-108">Проверка оповещений</span><span class="sxs-lookup"><span data-stu-id="56095-108">Alert validation</span></span>
<span data-ttu-id="56095-109">После установки агента центра безопасности на свой компьютер выполните следующие шаги на компьютере, где находится атакованный ресурс оповещения:</span><span class="sxs-lookup"><span data-stu-id="56095-109">After Security Center agent is installed on your computer, follow the steps below from the computer where you want to be the attacked resource of the alert:</span></span>

1. <span data-ttu-id="56095-110">Скопируйте исполняемый файл (например, calc.exe) на рабочий стол компьютера или в другой каталог.</span><span class="sxs-lookup"><span data-stu-id="56095-110">Copy an executable (for example calc.exe) to the computer’s desktop, or other directory of your convenience.</span></span>
2. <span data-ttu-id="56095-111">Переименуйте этот файл на **ASC_AlertTest_662jfi039N.exe**.</span><span class="sxs-lookup"><span data-stu-id="56095-111">Rename this file to **ASC_AlertTest_662jfi039N.exe**.</span></span>
3. <span data-ttu-id="56095-112">Откройте командную строку и выполните этот файл с аргументом (фиктивное имя аргумента), таким как *ASC_AlertTest_662jfi039N.exe -foo*.</span><span class="sxs-lookup"><span data-stu-id="56095-112">Open the command prompt and execute this file with an argument (just a fake argument name), such as: *ASC_AlertTest_662jfi039N.exe -foo*</span></span>
4. <span data-ttu-id="56095-113">Подождите 5–10 минут и откройте оповещения центра безопасности.</span><span class="sxs-lookup"><span data-stu-id="56095-113">Wait 5 to 10 minutes and open Security Center Alerts.</span></span> <span data-ttu-id="56095-114">Там можно найти оповещение, аналогичное следующему:</span><span class="sxs-lookup"><span data-stu-id="56095-114">There you should find an alert similar to following one:</span></span>

    ![Проверка оповещений](./media/security-center-alert-validation/security-center-alert-validation-fig1.png)

<span data-ttu-id="56095-116">При просмотре этого оповещения убедитесь, что в поле Arguments Auditing Enabled (Включен аудит аргументов) задано значение true.</span><span class="sxs-lookup"><span data-stu-id="56095-116">When reviewing this alert, make sure the field Arguments Auditing Enabled appears as true.</span></span> <span data-ttu-id="56095-117">Если оно содержит значение false, необходимо включить аудит аргументов командной строки.</span><span class="sxs-lookup"><span data-stu-id="56095-117">If it shows false, you need to enable command-line arguments auditing.</span></span> <span data-ttu-id="56095-118">Этот параметр можно включить с помощью командной строки:</span><span class="sxs-lookup"><span data-stu-id="56095-118">You can enable this option using the following command line:</span></span>

<span data-ttu-id="56095-119">*reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\system\Audit" /f /v "ProcessCreationIncludeCmdLine_Enabled"*</span><span class="sxs-lookup"><span data-stu-id="56095-119">*reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\system\Audit" /f /v "ProcessCreationIncludeCmdLine_Enabled"*</span></span>


## <a name="see-also"></a><span data-ttu-id="56095-120">См. также</span><span class="sxs-lookup"><span data-stu-id="56095-120">See also</span></span>
<span data-ttu-id="56095-121">В этой статье представлен процесс проверки оповещений.</span><span class="sxs-lookup"><span data-stu-id="56095-121">This article introduced you to the alerts validation process.</span></span> <span data-ttu-id="56095-122">Теперь, когда вы знакомы с проверкой, ознакомьтесь с такими статьями:</span><span class="sxs-lookup"><span data-stu-id="56095-122">Now that you're familiar with this validation, try the following articles:</span></span>

* <span data-ttu-id="56095-123">[Управление оповещениями безопасности в Центре безопасности Azure и реагирование на них](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts).</span><span class="sxs-lookup"><span data-stu-id="56095-123">[Managing and responding to security alerts in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts).</span></span> <span data-ttu-id="56095-124">Узнайте, как управлять оповещениями и реагировать на угрозы безопасности в центре безопасности.</span><span class="sxs-lookup"><span data-stu-id="56095-124">Learn how to manage alerts, and respond to security incidents in Security Center.</span></span>
* <span data-ttu-id="56095-125">[Наблюдение за работоспособностью системы безопасности в Центре безопасности Azure](security-center-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="56095-125">[Security health monitoring in Azure Security Center](security-center-monitoring.md).</span></span> <span data-ttu-id="56095-126">Узнайте, как отслеживать работоспособность ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="56095-126">Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="56095-127">[Основные сведения об оповещениях системы безопасности в центре безопасности Azure](https://docs.microsoft.com/azure/security-center/security-center-alerts-type).</span><span class="sxs-lookup"><span data-stu-id="56095-127">[Understanding security alerts in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-alerts-type).</span></span> <span data-ttu-id="56095-128">Дополнительные сведения о различных типах оповещений безопасности.</span><span class="sxs-lookup"><span data-stu-id="56095-128">Learn about the different types of security alerts.</span></span>
* <span data-ttu-id="56095-129">[Руководство по устранению неполадок в центре безопасности Azure](https://docs.microsoft.com/azure/security-center/security-center-troubleshooting-guide).</span><span class="sxs-lookup"><span data-stu-id="56095-129">[Azure Security Center Troubleshooting Guide](https://docs.microsoft.com/azure/security-center/security-center-troubleshooting-guide).</span></span> <span data-ttu-id="56095-130">Узнайте, как устранять типичные неполадки в центре безопасности.</span><span class="sxs-lookup"><span data-stu-id="56095-130">Learn how to troubleshoot common issues in Security Center.</span></span> 
* <span data-ttu-id="56095-131">[Центр безопасности Azure: часто задаваемые вопросы](security-center-faq.md).</span><span class="sxs-lookup"><span data-stu-id="56095-131">[Azure Security Center FAQ](security-center-faq.md).</span></span> <span data-ttu-id="56095-132">Часто задаваемые вопросы об использовании этой службы.</span><span class="sxs-lookup"><span data-stu-id="56095-132">Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="56095-133">[Блог по безопасности Azure](http://blogs.msdn.com/b/azuresecurity/).</span><span class="sxs-lookup"><span data-stu-id="56095-133">[Azure Security Blog](http://blogs.msdn.com/b/azuresecurity/).</span></span> <span data-ttu-id="56095-134">Записи блога, посвященные безопасности и соответствию требованиям в Azure.</span><span class="sxs-lookup"><span data-stu-id="56095-134">Find blog posts about Azure security and compliance.</span></span>

