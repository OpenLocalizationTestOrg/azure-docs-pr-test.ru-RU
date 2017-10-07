---
title: "aaaEnable аудита и угрозы обнаружения на SQL Server в центр безопасности Azure | Документы Microsoft"
description: "В этом документе показано, как tooimplement hello рекомендации центра безопасности Azure ** включить аудит & угроз обнаружения на серверах SQL **."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 042fca4d-7dab-4172-8614-e8c21ccb4960
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: terrylan
ms.openlocfilehash: b082c48cdbc386f14e677f4e13a7f306f37fd0e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="enable-auditing-and-threat-detection-on-sql-servers-in-azure-security-center"></a><span data-ttu-id="733e8-103">Включение аудита и обнаружения угроз для серверов SQL в центре безопасности Azure</span><span class="sxs-lookup"><span data-stu-id="733e8-103">Enable auditing and threat detection on SQL servers in Azure Security Center</span></span>
<span data-ttu-id="733e8-104">Центр безопасности Azure порекомендует включить аудит и обнаружение угроз для всех баз данных на всех серверах SQL Azure, если аудит еще не включен.</span><span class="sxs-lookup"><span data-stu-id="733e8-104">Azure Security Center will recommend that you turn on auditing and threat detection for all databases on your Azure SQL servers if auditing is not already enabled.</span></span> <span data-ttu-id="733e8-105">Аудит и обнаружение угроз могут помочь вам соблюсти стандарты, проанализировать работу с базой данных и получить представление о расхождениях и аномалиях, которые могут указывать на бизнес-проблемы или предполагаемые нарушения безопасности.</span><span class="sxs-lookup"><span data-stu-id="733e8-105">Auditing and threat detection can help you maintain regulatory compliance, understand database activity, and gain insight into discrepancies and anomalies that could indicate business concerns or suspected security violations.</span></span>

<span data-ttu-id="733e8-106">После включения аудита можно настроить для обнаружения угроз параметры и сообщения электронной почты tooreceive оповещений системы безопасности.</span><span class="sxs-lookup"><span data-stu-id="733e8-106">Once you’ve turned on auditing you can configure Threat Detection settings and emails tooreceive security alerts.</span></span> <span data-ttu-id="733e8-107">Обнаружение угроз обнаруживает аномальные действия базы данных, указывающее базу данных toohello потенциальные угрозы безопасности.</span><span class="sxs-lookup"><span data-stu-id="733e8-107">Threat Detection detects anomalous database activities indicating potential security threats toohello database.</span></span> <span data-ttu-id="733e8-108">Это позволяет toodetect и отвечать toopotential угроз, как только они происходят.</span><span class="sxs-lookup"><span data-stu-id="733e8-108">This enables you toodetect and respond toopotential threats as they occur.</span></span>

<span data-ttu-id="733e8-109">Данная рекомендация применяется toohello службой Azure SQL. она не включает SQL Server, работающий на виртуальных машинах в службах инфраструктуры Azure (Azure IaaS).</span><span class="sxs-lookup"><span data-stu-id="733e8-109">This recommendation applies toohello Azure SQL service only; it doesn’t include SQL Server running on your virtual machines in Azure Infrastructure Services (Azure IaaS).</span></span>

> [!NOTE]
> <span data-ttu-id="733e8-110">В этом документе представлены hello службы с помощью пример развертывания.</span><span class="sxs-lookup"><span data-stu-id="733e8-110">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="733e8-111">Он не является пошаговым руководством.</span><span class="sxs-lookup"><span data-stu-id="733e8-111">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="733e8-112">Реализация рекомендаций hello</span><span class="sxs-lookup"><span data-stu-id="733e8-112">Implement hello recommendation</span></span>
1. <span data-ttu-id="733e8-113">В hello **рекомендации** колонке выберите **включить аудит & угроз обнаружения на серверах SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="733e8-113">In hello **Recommendations** blade, select **Enable Auditing & Threat detection on SQL servers**.</span></span>  <span data-ttu-id="733e8-114">При этом откроется hello **включить аудит & угроз обнаружения на серверах SQL Server** колонку.</span><span class="sxs-lookup"><span data-stu-id="733e8-114">This opens hello **Enable Auditing & Threat detection on SQL servers** blade.</span></span>

   ![Включение аудита для серверов SQL][1]
2. <span data-ttu-id="733e8-116">Установите SQL server tooenable аудита и угрозы обнаружения.</span><span class="sxs-lookup"><span data-stu-id="733e8-116">Select a SQL server tooenable auditing and threat detection on.</span></span> <span data-ttu-id="733e8-117">При этом откроется hello **аудита и обнаружения угроз** колонку.</span><span class="sxs-lookup"><span data-stu-id="733e8-117">This opens hello **Auditing & Threat Detection** blade.</span></span>

3. <span data-ttu-id="733e8-118">На hello **аудита и обнаружения угроз** колонке выберите **ON** под **аудита**.</span><span class="sxs-lookup"><span data-stu-id="733e8-118">On hello **Auditing & Threat Detection** blade, select **ON** under **Auditing**.</span></span>

   ![Включение параметров аудита][2]
4. <span data-ttu-id="733e8-120">Следуйте указаниям hello [аудита базы данных SQL в hello портал Azure](../sql-database/sql-database-auditing-portal.md) tooconfigure хранилище, где будет храниться журналов аудита.</span><span class="sxs-lookup"><span data-stu-id="733e8-120">Follow hello steps in [SQL database auditing in hello Azure portal](../sql-database/sql-database-auditing-portal.md) tooconfigure storage where your audit logs will be stored.</span></span> <span data-ttu-id="733e8-121">Hello подписки в учетной записи хранилища для сбора данных — учетная запись хранения по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="733e8-121">hello subscription's storage account for data collection is hello default storage account.</span></span>
5. <span data-ttu-id="733e8-122">Следуйте указаниям hello [Приступая к работе с обнаружением угроз для базы данных SQL](../sql-database/sql-database-threat-detection.md) tooturn на и настроить обнаружение угроз и tooconfigure hello список адресов электронной почты, которые будут получать предупреждения системы безопасности при обнаружении аномальных действий.</span><span class="sxs-lookup"><span data-stu-id="733e8-122">Follow hello steps in [Get started with SQL Database Threat Detection](../sql-database/sql-database-threat-detection.md) tooturn on and configure Threat Detection and tooconfigure hello list of emails that will receive security alerts upon detection of anomalous activities.</span></span>

## <a name="see-also"></a><span data-ttu-id="733e8-123">См. также</span><span class="sxs-lookup"><span data-stu-id="733e8-123">See also</span></span>
<span data-ttu-id="733e8-124">В этой статье показано, как tooimplement hello рекомендации центра обеспечения безопасности «Включение аудита и угрозы обнаружения на серверах SQL Server».</span><span class="sxs-lookup"><span data-stu-id="733e8-124">This article showed you how tooimplement hello Security Center recommendation "Enable auditing and threat detection on SQL servers."</span></span> <span data-ttu-id="733e8-125">toolearn Дополнительные сведения о защите базы данных SQL, см. ниже hello:</span><span class="sxs-lookup"><span data-stu-id="733e8-125">toolearn more about securing your SQL database, see hello following:</span></span>

* [<span data-ttu-id="733e8-126">Защита Базы данных SQL</span><span class="sxs-lookup"><span data-stu-id="733e8-126">Securing your SQL Database</span></span>](../sql-database/sql-database-security-overview.md)

<span data-ttu-id="733e8-127">toolearn Дополнительные сведения о центра обеспечения безопасности, см. ниже hello:</span><span class="sxs-lookup"><span data-stu-id="733e8-127">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="733e8-128">[Установка политики безопасности в центр безопасности Azure](security-center-policies.md) — Узнайте, как tooconfigure политики безопасности для вашей подписки Azure и группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="733e8-128">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="733e8-129">[Управление рекомендациями по безопасности в Центре безопасности Azure](security-center-recommendations.md) — узнайте, как рекомендации могут помочь вам защитить ресурсы Azure.</span><span class="sxs-lookup"><span data-stu-id="733e8-129">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="733e8-130">[Наблюдение за работоспособностью системы безопасности в центр безопасности Azure](security-center-monitoring.md) — Узнайте, как toomonitor hello работоспособности ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="733e8-130">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="733e8-131">[Управление и отвечает на запросы toosecurity предупреждения в центр безопасности Azure](security-center-managing-and-responding-alerts.md) --Узнайте, как предупреждения toosecurity toomanage и отправки ответа.</span><span class="sxs-lookup"><span data-stu-id="733e8-131">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="733e8-132">[Мониторинг решений партнера с центром обеспечения безопасности Azure](security-center-partner-solutions.md) — Узнайте, как toomonitor hello состояние работоспособности решений для партнера.</span><span class="sxs-lookup"><span data-stu-id="733e8-132">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="733e8-133">[Центр безопасности Azure часто задаваемые вопросы о](security-center-faq.md) — часто задаваемые вопросы об использовании hello службы поиска.</span><span class="sxs-lookup"><span data-stu-id="733e8-133">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="733e8-134">[Блог Azure безопасности](http://blogs.msdn.com/b/azuresecurity/) --получить последние новости безопасности Azure hello и информацию.</span><span class="sxs-lookup"><span data-stu-id="733e8-134">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get hello latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-auditing-on-sql-server/enable-auditing-on-sql-servers.png
[2]: ./media/security-center-enable-auditing-on-sql-server/auditing-settings-blade.png
