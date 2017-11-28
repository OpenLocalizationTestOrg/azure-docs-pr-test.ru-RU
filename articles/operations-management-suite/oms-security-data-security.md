---
title: "aaaOperations Management Suite и безопасность данных аудита решения | Документы Microsoft"
description: "В этой статье объясняются методы управления данными и обеспечения их безопасности в решении \"Безопасность и аудит\" Operations Management Suite."
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 9cdf7deb-2a30-4672-b89f-71179ee8326a
ms.service: operations-management-suite
ms.custom: oms-security
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: yurid
ms.openlocfilehash: 9c4181b3b491e4f7f0c57d7252eca78a819722d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="operations-management-suite-security-and-audit-solution-data-security"></a><span data-ttu-id="fc22e-103">Защита данных с помощью решения "Безопасность и аудит" Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="fc22e-103">Operations Management Suite Security and Audit solution data security</span></span>
<span data-ttu-id="fc22e-104">предотвратить toohelp клиентов, обнаружения и отвечать toothreats, [решение аудита и безопасности Operations Management Suite (OMS)](operations-management-suite-overview.md) собирает и обрабатывает данные о ресурсах, которые включают:</span><span class="sxs-lookup"><span data-stu-id="fc22e-104">toohelp customers prevent, detect, and respond toothreats, [Operations Management Suite  (OMS) Security and Audit Solution](operations-management-suite-overview.md) collects and processes data about your resources, which includes:</span></span>

* <span data-ttu-id="fc22e-105">журналы событий безопасности;</span><span class="sxs-lookup"><span data-stu-id="fc22e-105">Security event log</span></span>
* <span data-ttu-id="fc22e-106">Трассировка событий Windows (ETW)</span><span class="sxs-lookup"><span data-stu-id="fc22e-106">Event Tracing for Windows (ETW) events</span></span>
* <span data-ttu-id="fc22e-107">события аудита, собранные с помощью AppLocker;</span><span class="sxs-lookup"><span data-stu-id="fc22e-107">AppLocker auditing events</span></span>
* <span data-ttu-id="fc22e-108">журналы брандмауэра Windows;</span><span class="sxs-lookup"><span data-stu-id="fc22e-108">Windows Firewall log</span></span>
* <span data-ttu-id="fc22e-109">события Advanced Threat Analytics;</span><span class="sxs-lookup"><span data-stu-id="fc22e-109">Advanced Threat Analytics events</span></span>
* <span data-ttu-id="fc22e-110">результаты оценки базовых показателей;</span><span class="sxs-lookup"><span data-stu-id="fc22e-110">Results of baseline assessment</span></span>
* <span data-ttu-id="fc22e-111">результаты оценки защиты от вредоносных программ;</span><span class="sxs-lookup"><span data-stu-id="fc22e-111">Results of antimalware assessment</span></span>
* <span data-ttu-id="fc22e-112">результаты оценки обновлений и исправлений;</span><span class="sxs-lookup"><span data-stu-id="fc22e-112">Results of update/patch assessment</span></span>
* <span data-ttu-id="fc22e-113">Необходимые потоки, которые явно включено в агенте hello</span><span class="sxs-lookup"><span data-stu-id="fc22e-113">Syslogs streams that are explicitly enabled on hello agent</span></span>

<span data-ttu-id="fc22e-114">Сделан строгого обязательства tooprotect hello конфиденциальность и безопасность данных.</span><span class="sxs-lookup"><span data-stu-id="fc22e-114">We make strong commitments tooprotect hello privacy and security of this data.</span></span> <span data-ttu-id="fc22e-115">Корпорация Майкрософт придерживается toostrict соответствия требованиям и указаниям по безопасности — от написания кода toooperating службы.</span><span class="sxs-lookup"><span data-stu-id="fc22e-115">Microsoft adheres toostrict compliance and security guidelines—from coding toooperating a service.</span></span>
<span data-ttu-id="fc22e-116">В этой статье объясняются методы управления данными и обеспечения их безопасности в решении OMS "Безопасность и аудит".</span><span class="sxs-lookup"><span data-stu-id="fc22e-116">This article explains how data is managed and safeguarded in OMS Security and Audit Solution.</span></span>

## <a name="data-sources"></a><span data-ttu-id="fc22e-117">Источники данных</span><span class="sxs-lookup"><span data-stu-id="fc22e-117">Data sources</span></span>
<span data-ttu-id="fc22e-118">Решение аудита и безопасности OMS анализировать данные из вашей виртуальных машин и физических компьютеров, где установлен агент OMS hello.</span><span class="sxs-lookup"><span data-stu-id="fc22e-118">OMS Security and Audit Solution analyze data from your Virtual Machines and physical computers where hello OMS Agent is installed.</span></span> <span data-ttu-id="fc22e-119">Это решение может собирать сведения о конфигурации событий безопасности, таких как события Windows, журналы аудита, журналы IIS и сообщения системного журнала.</span><span class="sxs-lookup"><span data-stu-id="fc22e-119">OMS Security and Audit Solution can collect configuration information about security events, such as Windows event, audit logs, IIS logs and syslog messages.</span></span> <span data-ttu-id="fc22e-120">Примеры таких данных: тип и версия операционной системы, выполняющиеся процессы, имя компьютера, IP-адреса, имя пользователя, выполнившего вход, и идентификатор клиента.</span><span class="sxs-lookup"><span data-stu-id="fc22e-120">Examples of such data are: operating system type and version, running processes, machine name, IP addresses, logged in user, and tenant ID.</span></span>  

## <a name="data-protection"></a><span data-ttu-id="fc22e-121">Защита данных</span><span class="sxs-lookup"><span data-stu-id="fc22e-121">Data protection</span></span>
<span data-ttu-id="fc22e-122">**Разделение данных**: данные логическим образом отделяются для каждого компонента службы hello.</span><span class="sxs-lookup"><span data-stu-id="fc22e-122">**Data segregation**: Data is kept logically separate on each component throughout hello service.</span></span> <span data-ttu-id="fc22e-123">Все данные отмечаются тегами по организациям.</span><span class="sxs-lookup"><span data-stu-id="fc22e-123">All data is tagged per organization.</span></span> <span data-ttu-id="fc22e-124">Эти теги существуют в течение всего жизненного цикла данных hello и используются на каждом уровне службы hello.</span><span class="sxs-lookup"><span data-stu-id="fc22e-124">This tagging persists throughout hello data lifecycle, and it is enforced at each layer of hello service.</span></span> 

<span data-ttu-id="fc22e-125">**Доступ к данным**: tooprovide рекомендации по обеспечению безопасности и потенциальные угрозы безопасности, а также персонал корпорации Майкрософт могут получать доступ к данные собираются и анализировать по службами.</span><span class="sxs-lookup"><span data-stu-id="fc22e-125">**Data access**: tooprovide security recommendations and investigate potential security threats, Microsoft personnel may access information collected or analyzed by services.</span></span> <span data-ttu-id="fc22e-126">Мы следовать toohello [Microsoft Online Services условия](http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31) и [заявление о конфиденциальности](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx), которой состояние, Майкрософт не будет использовать данные клиента или извлечения сведений из него для объявлений или аналогичные коммерческих целей.</span><span class="sxs-lookup"><span data-stu-id="fc22e-126">We adhere toohello [Microsoft Online Services Terms](http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31) and [Privacy Statement](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx), which state that Microsoft will not use Customer Data or derive information from it for any advertising or similar commercial purposes.</span></span> <span data-ttu-id="fc22e-127">рекомендации по обеспечению безопасности tooprovide и потенциальные угрозы безопасности, а также персонал корпорации Майкрософт могут получать доступ к данные собираются и анализировать по службами.</span><span class="sxs-lookup"><span data-stu-id="fc22e-127">tooprovide security recommendations and investigate potential security threats, Microsoft personnel may access information collected or analyzed by services.</span></span> <span data-ttu-id="fc22e-128">Только мы используем данные клиента как необходимые tooprovide, можно с помощью Azure служб, включая целей, совместимые с предоставлением этих служб.</span><span class="sxs-lookup"><span data-stu-id="fc22e-128">We only use Customer Data as needed tooprovide you with Azure services, including purposes compatible with providing those services.</span></span> <span data-ttu-id="fc22e-129">Все права tooyour собственные данные сохраняются.</span><span class="sxs-lookup"><span data-stu-id="fc22e-129">You retain all rights tooyour own data.</span></span>

<span data-ttu-id="fc22e-130">**Использование данных**: Корпорация Майкрософт использует шаблоны и анализ угроз, видны в нескольких клиентов tooenhance наши возможности обнаружения и предотвращения; мы делаем в соответствии с hello обязательства по конфиденциальности, описано в нашем [конфиденциальности Инструкция](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx).</span><span class="sxs-lookup"><span data-stu-id="fc22e-130">**Data use**: Microsoft uses patterns and threat intelligence seen across multiple tenants tooenhance our prevention and detection capabilities; we do so in accordance with hello privacy commitments described in our [Privacy Statement](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="fc22e-131">Расположение данных настраивается на уровне рабочей области OMS hello, во время создания рабочей области hello, который является частью hello начальной OMS безопасность и аудит процесса настройки.</span><span class="sxs-lookup"><span data-stu-id="fc22e-131">Data location is configured at hello OMS workspace level, during hello workspace creation, which is part of hello initial OMS Security and Audit configuration process.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="fc22e-132">См. также</span><span class="sxs-lookup"><span data-stu-id="fc22e-132">See also</span></span>
<span data-ttu-id="fc22e-133">Из этой статьи вы узнали, каким образом обеспечивается управление данными и обеспечение их безопасности в OMS.</span><span class="sxs-lookup"><span data-stu-id="fc22e-133">In this document, you learned how data is managed and safeguarded in OMS.</span></span> <span data-ttu-id="fc22e-134">toolearn Дополнительные сведения о безопасности OMS и решения аудита, см.:</span><span class="sxs-lookup"><span data-stu-id="fc22e-134">toolearn more about OMS Security and Audit solution, see:</span></span>

* [<span data-ttu-id="fc22e-135">Общие сведения об Operations Management Suite (OMS)</span><span class="sxs-lookup"><span data-stu-id="fc22e-135">Operations Management Suite (OMS) overview</span></span>](operations-management-suite-overview.md)
* [<span data-ttu-id="fc22e-136">Мониторинг и реагирование tooSecurity оповещения в Operations Management Suite безопасности и аудита решения</span><span class="sxs-lookup"><span data-stu-id="fc22e-136">Monitoring and Responding tooSecurity Alerts in Operations Management Suite Security and Audit Solution</span></span>](oms-security-responding-alerts.md)
* [<span data-ttu-id="fc22e-137">Мониторинг ресурсов в решении "Безопасность и аудит" Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="fc22e-137">Monitoring Resources in Operations Management Suite Security and Audit Solution</span></span>](oms-security-monitoring-resources.md)

