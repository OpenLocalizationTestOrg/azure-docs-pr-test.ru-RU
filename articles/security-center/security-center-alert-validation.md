---
title: "aaaAlerts проверки в центр безопасности Azure | Документы Microsoft"
description: "Этот документ поможет вам оповещений системы безопасности toovalidate hello в центр безопасности Azure."
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
ms.openlocfilehash: 030e9e74303758192eedaf517f1cb0d2e4a7852e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="alerts-validation-in-azure-security-center"></a><span data-ttu-id="433bb-103">Проверка оповещений в центре безопасности Azure</span><span class="sxs-lookup"><span data-stu-id="433bb-103">Alerts Validation in Azure Security Center</span></span>
<span data-ttu-id="433bb-104">Этот документ поможет узнать, как tooverify, если система настроена должным образом для оповещения центра безопасности Azure.</span><span class="sxs-lookup"><span data-stu-id="433bb-104">This document helps you learn how tooverify if your system is properly configured for Azure Security Center alerts.</span></span>

## <a name="what-are-security-alerts"></a><span data-ttu-id="433bb-105">Что такое оповещения системы безопасности?</span><span class="sxs-lookup"><span data-stu-id="433bb-105">What are security alerts?</span></span>
<span data-ttu-id="433bb-106">Центр обеспечения безопасности автоматически собирает анализирует и производить сбор данных журнала из ресурсов Azure, сети hello и решения подключенных партнеров, как решения для защиты брандмауэра и конечной точки, toodetect и оповещения toothreats вы.</span><span class="sxs-lookup"><span data-stu-id="433bb-106">Security Center automatically collects, analyzes, and integrates log data from your Azure resources, hello network, and connected partner solutions, like firewall and endpoint protection solutions, toodetect and alert you toothreats.</span></span> <span data-ttu-id="433bb-107">Чтение [toosecurity управление и отвечает на запросы предупреждения в центр безопасности Azure](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts) Дополнительные сведения о оповещений системы безопасности и чтение [основные сведения об оповещениях безопасности в центр безопасности Azure](https://docs.microsoft.com/azure/security-center/security-center-alerts-type) toolearn Дополнительные о hello различных типов оповещений.</span><span class="sxs-lookup"><span data-stu-id="433bb-107">Read [Managing and responding toosecurity alerts in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts) for more information about security alerts, and read [Understanding security alerts in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-alerts-type) toolearn more about hello different types of alerts.</span></span>

## <a name="alert-validation"></a><span data-ttu-id="433bb-108">Проверка оповещений</span><span class="sxs-lookup"><span data-stu-id="433bb-108">Alert validation</span></span>
<span data-ttu-id="433bb-109">После установки агента центра обеспечения безопасности на компьютере, выполните действия hello ниже с компьютера hello место ресурсов hello атаке toobe hello предупреждения.</span><span class="sxs-lookup"><span data-stu-id="433bb-109">After Security Center agent is installed on your computer, follow hello steps below from hello computer where you want toobe hello attacked resource of hello alert:</span></span>

1. <span data-ttu-id="433bb-110">Скопируйте исполняемый файл (для примера calc.exe) toohello ПК или другим каталогом удобства.</span><span class="sxs-lookup"><span data-stu-id="433bb-110">Copy an executable (for example calc.exe) toohello computer’s desktop, or other directory of your convenience.</span></span>
2. <span data-ttu-id="433bb-111">Переименовать этот файл слишком**ASC_AlertTest_662jfi039N.exe**.</span><span class="sxs-lookup"><span data-stu-id="433bb-111">Rename this file too**ASC_AlertTest_662jfi039N.exe**.</span></span>
3. <span data-ttu-id="433bb-112">Откройте командную строку hello и выполнить этот файл с аргументом (просто имя фиктивное аргумент), например: *ASC_AlertTest_662jfi039N.exe - foo*</span><span class="sxs-lookup"><span data-stu-id="433bb-112">Open hello command prompt and execute this file with an argument (just a fake argument name), such as: *ASC_AlertTest_662jfi039N.exe -foo*</span></span>
4. <span data-ttu-id="433bb-113">Подождите 5 минут too10 и откройте оповещения центра безопасности.</span><span class="sxs-lookup"><span data-stu-id="433bb-113">Wait 5 too10 minutes and open Security Center Alerts.</span></span> <span data-ttu-id="433bb-114">Следует найти предупреждения toofollowing аналогично, один:</span><span class="sxs-lookup"><span data-stu-id="433bb-114">There you should find an alert similar toofollowing one:</span></span>

    ![Проверка оповещений](./media/security-center-alert-validation/security-center-alert-validation-fig1.png)

<span data-ttu-id="433bb-116">При просмотре этого предупреждения, убедитесь, что поле hello, аудит включен аргументы появляется как true.</span><span class="sxs-lookup"><span data-stu-id="433bb-116">When reviewing this alert, make sure hello field Arguments Auditing Enabled appears as true.</span></span> <span data-ttu-id="433bb-117">Если оно указано значение false, необходимые аргументы командной строки tooenable аудита.</span><span class="sxs-lookup"><span data-stu-id="433bb-117">If it shows false, you need tooenable command-line arguments auditing.</span></span> <span data-ttu-id="433bb-118">Можно включить этот параметр, с помощью следующей командной строкой hello:</span><span class="sxs-lookup"><span data-stu-id="433bb-118">You can enable this option using hello following command line:</span></span>

<span data-ttu-id="433bb-119">*reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\system\Audit" /f /v "ProcessCreationIncludeCmdLine_Enabled"*</span><span class="sxs-lookup"><span data-stu-id="433bb-119">*reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\system\Audit" /f /v "ProcessCreationIncludeCmdLine_Enabled"*</span></span>


## <a name="see-also"></a><span data-ttu-id="433bb-120">См. также</span><span class="sxs-lookup"><span data-stu-id="433bb-120">See also</span></span>
<span data-ttu-id="433bb-121">В этой статье представлена процесс проверки toohello предупреждения.</span><span class="sxs-lookup"><span data-stu-id="433bb-121">This article introduced you toohello alerts validation process.</span></span> <span data-ttu-id="433bb-122">Теперь, когда вы знакомы с этой проверкой, попробуйте hello в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="433bb-122">Now that you're familiar with this validation, try hello following articles:</span></span>

* <span data-ttu-id="433bb-123">[Управление и отвечает на запросы toosecurity предупреждения в центр безопасности Azure](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts).</span><span class="sxs-lookup"><span data-stu-id="433bb-123">[Managing and responding toosecurity alerts in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts).</span></span> <span data-ttu-id="433bb-124">Узнайте, как toomanage предупреждений и инцидентов toosecurity ответ в центр обеспечения безопасности.</span><span class="sxs-lookup"><span data-stu-id="433bb-124">Learn how toomanage alerts, and respond toosecurity incidents in Security Center.</span></span>
* <span data-ttu-id="433bb-125">[Наблюдение за работоспособностью системы безопасности в Центре безопасности Azure](security-center-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="433bb-125">[Security health monitoring in Azure Security Center](security-center-monitoring.md).</span></span> <span data-ttu-id="433bb-126">Узнайте, как toomonitor hello работоспособности ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="433bb-126">Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="433bb-127">[Основные сведения об оповещениях системы безопасности в центре безопасности Azure](https://docs.microsoft.com/azure/security-center/security-center-alerts-type).</span><span class="sxs-lookup"><span data-stu-id="433bb-127">[Understanding security alerts in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-alerts-type).</span></span> <span data-ttu-id="433bb-128">Дополнительные сведения о различных типах hello оповещений системы безопасности.</span><span class="sxs-lookup"><span data-stu-id="433bb-128">Learn about hello different types of security alerts.</span></span>
* <span data-ttu-id="433bb-129">[Руководство по устранению неполадок в центре безопасности Azure](https://docs.microsoft.com/azure/security-center/security-center-troubleshooting-guide).</span><span class="sxs-lookup"><span data-stu-id="433bb-129">[Azure Security Center Troubleshooting Guide](https://docs.microsoft.com/azure/security-center/security-center-troubleshooting-guide).</span></span> <span data-ttu-id="433bb-130">Узнайте, как tootroubleshoot распространенные проблемы в центре безопасности.</span><span class="sxs-lookup"><span data-stu-id="433bb-130">Learn how tootroubleshoot common issues in Security Center.</span></span> 
* <span data-ttu-id="433bb-131">[Центр безопасности Azure: часто задаваемые вопросы](security-center-faq.md).</span><span class="sxs-lookup"><span data-stu-id="433bb-131">[Azure Security Center FAQ](security-center-faq.md).</span></span> <span data-ttu-id="433bb-132">Найти часто задаваемые вопросы об использовании службы hello.</span><span class="sxs-lookup"><span data-stu-id="433bb-132">Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="433bb-133">[Блог по безопасности Azure](http://blogs.msdn.com/b/azuresecurity/).</span><span class="sxs-lookup"><span data-stu-id="433bb-133">[Azure Security Blog](http://blogs.msdn.com/b/azuresecurity/).</span></span> <span data-ttu-id="433bb-134">Записи блога, посвященные безопасности и соответствию требованиям в Azure.</span><span class="sxs-lookup"><span data-stu-id="433bb-134">Find blog posts about Azure security and compliance.</span></span>

