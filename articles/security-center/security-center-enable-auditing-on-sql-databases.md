---
title: "aaaEnable аудита и угрозы обнаружения на SQL базы данных в центр безопасности Azure | Документы Microsoft"
description: "В этом документе показано, как tooimplement hello рекомендации центра безопасности Azure ** включить обнаружение аудита и угроз для базы данных SQL **."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 224b6755-2b36-4ecd-9af8-139a198e0df1
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: terrylan
ms.openlocfilehash: c94140acf37cabaca3e681ba5db79d6827e7b9db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="enable-auditing-and-threat-detection-on-sql-databases-in-azure-security-center"></a><span data-ttu-id="f2185-103">Включение аудита и обнаружения угроз для баз данных SQL в центре безопасности Azure</span><span class="sxs-lookup"><span data-stu-id="f2185-103">Enable auditing and threat detection on SQL databases in Azure Security Center</span></span>
<span data-ttu-id="f2185-104">Центр безопасности Azure порекомендует включить аудит и обнаружение угроз для всех баз данных SQL, если эти функции еще не включены.</span><span class="sxs-lookup"><span data-stu-id="f2185-104">Azure Security Center will recommend that you turn on auditing and threat detection for all SQL databases if auditing and threat detection is not already enabled.</span></span> <span data-ttu-id="f2185-105">Аудит и обнаружение угроз могут помочь вам соблюсти стандарты, проанализировать работу с базой данных и получить представление о расхождениях и аномалиях, которые могут указывать на бизнес-проблемы или предполагаемые нарушения безопасности.</span><span class="sxs-lookup"><span data-stu-id="f2185-105">Auditing and threat detection can help you maintain regulatory compliance, understand database activity, and gain insight into discrepancies and anomalies that could indicate business concerns or suspected security violations.</span></span>

<span data-ttu-id="f2185-106">После включения аудита можно настроить для обнаружения угроз параметры и сообщения электронной почты tooreceive оповещений системы безопасности.</span><span class="sxs-lookup"><span data-stu-id="f2185-106">Once you’ve turned on auditing you can configure Threat Detection settings and emails tooreceive security alerts.</span></span> <span data-ttu-id="f2185-107">Обнаружение угроз обнаруживает аномальные действия базы данных, указывающее базу данных toohello потенциальные угрозы безопасности.</span><span class="sxs-lookup"><span data-stu-id="f2185-107">Threat Detection detects anomalous database activities indicating potential security threats toohello database.</span></span> <span data-ttu-id="f2185-108">Это позволяет toodetect и отвечать toopotential угроз, как только они происходят.</span><span class="sxs-lookup"><span data-stu-id="f2185-108">This enables you toodetect and respond toopotential threats as they occur.</span></span>

<span data-ttu-id="f2185-109">Данная рекомендация применяется toohello службой Azure SQL. они не включают SQL, работающих на виртуальных машинах.</span><span class="sxs-lookup"><span data-stu-id="f2185-109">This recommendation applies toohello Azure SQL service only; it doesn't include SQL running on your virtual machines.</span></span>

> [!NOTE]
> <span data-ttu-id="f2185-110">В этом документе представлены hello службы с помощью пример развертывания.</span><span class="sxs-lookup"><span data-stu-id="f2185-110">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="f2185-111">Он не является пошаговым руководством.</span><span class="sxs-lookup"><span data-stu-id="f2185-111">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="f2185-112">Реализация рекомендаций hello</span><span class="sxs-lookup"><span data-stu-id="f2185-112">Implement hello recommendation</span></span>
1. <span data-ttu-id="f2185-113">В hello **рекомендации** колонке выберите **включить аудит & угроз обнаружения на базах данных SQL**.</span><span class="sxs-lookup"><span data-stu-id="f2185-113">In hello **Recommendations** blade, select **Enable Auditing & Threat detection on SQL databases**.</span></span>  <span data-ttu-id="f2185-114">При этом откроется hello **включить аудит & угроз обнаружения на базах данных SQL** колонку.</span><span class="sxs-lookup"><span data-stu-id="f2185-114">This opens hello **Enable Auditing & Threat detection on SQL databases** blade.</span></span>

   ![Включение аудита для баз данных SQL][1]
2. <span data-ttu-id="f2185-116">Выберите аудита базы данных SQL tooenable на.</span><span class="sxs-lookup"><span data-stu-id="f2185-116">Select a SQL database tooenable auditing on.</span></span> <span data-ttu-id="f2185-117">При этом откроется hello **аудита и обнаружения угроз** колонку.</span><span class="sxs-lookup"><span data-stu-id="f2185-117">This opens hello **Auditing & Threat Detection** blade.</span></span>

3. <span data-ttu-id="f2185-118">На hello **аудита и обнаружения угроз** колонке выберите **ON** под **аудита**.</span><span class="sxs-lookup"><span data-stu-id="f2185-118">On hello **Auditing & Threat Detection** blade, select **ON** under **Auditing**.</span></span>

   ![Включение аудита и обнаружения угроз][2]
4. <span data-ttu-id="f2185-120">Следуйте указаниям hello [обнаружением угроз для базы данных SQL в hello портал Azure](../sql-database/sql-database-threat-detection-portal.md) tooturn на и настроить обнаружение угроз и tooconfigure hello список адресов электронной почты, которые будут получать предупреждения системы безопасности при обнаружении аномальных действий.</span><span class="sxs-lookup"><span data-stu-id="f2185-120">Follow hello steps in [SQL Database Threat Detection in hello Azure portal](../sql-database/sql-database-threat-detection-portal.md) tooturn on and configure Threat Detection and tooconfigure hello list of emails that will receive security alerts upon detection of anomalous activities.</span></span>

## <a name="see-also"></a><span data-ttu-id="f2185-121">См. также</span><span class="sxs-lookup"><span data-stu-id="f2185-121">See also</span></span>
<span data-ttu-id="f2185-122">В этой статье показано, как tooimplement hello центра обеспечения безопасности, рекомендации «Включение аудита и угрозы обнаружения на базах данных SQL.»</span><span class="sxs-lookup"><span data-stu-id="f2185-122">This article showed you how tooimplement hello Security Center recommendation "Enable Auditing & Threat detection on SQL databases."</span></span> <span data-ttu-id="f2185-123">toolearn Дополнительные сведения о защите базы данных SQL, см. ниже hello:</span><span class="sxs-lookup"><span data-stu-id="f2185-123">toolearn more about securing your SQL database, see hello following:</span></span>

* [<span data-ttu-id="f2185-124">Защита Базы данных SQL</span><span class="sxs-lookup"><span data-stu-id="f2185-124">Securing your SQL Database</span></span>](../sql-database/sql-database-security-overview.md)

<span data-ttu-id="f2185-125">toolearn Дополнительные сведения о центра обеспечения безопасности, см. ниже hello:</span><span class="sxs-lookup"><span data-stu-id="f2185-125">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="f2185-126">[Установка политики безопасности в центр безопасности Azure](security-center-policies.md) — Узнайте, как tooconfigure политики безопасности для вашей подписки Azure и группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="f2185-126">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="f2185-127">[Управление рекомендациями по безопасности в Центре безопасности Azure](security-center-recommendations.md) — узнайте, как рекомендации могут помочь вам защитить ресурсы Azure.</span><span class="sxs-lookup"><span data-stu-id="f2185-127">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="f2185-128">[Наблюдение за работоспособностью системы безопасности в центр безопасности Azure](security-center-monitoring.md) — Узнайте, как toomonitor hello работоспособности ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="f2185-128">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="f2185-129">[Управление и отвечает на запросы toosecurity предупреждения в центр безопасности Azure](security-center-managing-and-responding-alerts.md) --Узнайте, как предупреждения toosecurity toomanage и отправки ответа.</span><span class="sxs-lookup"><span data-stu-id="f2185-129">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="f2185-130">[Мониторинг решений партнера с центром обеспечения безопасности Azure](security-center-partner-solutions.md) — Узнайте, как toomonitor hello состояние работоспособности решений для партнера.</span><span class="sxs-lookup"><span data-stu-id="f2185-130">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="f2185-131">[Центр безопасности Azure часто задаваемые вопросы о](security-center-faq.md) — часто задаваемые вопросы об использовании hello службы поиска.</span><span class="sxs-lookup"><span data-stu-id="f2185-131">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="f2185-132">[Блог Azure безопасности](http://blogs.msdn.com/b/azuresecurity/) --получить последние новости безопасности Azure hello и информацию.</span><span class="sxs-lookup"><span data-stu-id="f2185-132">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get hello latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-auditing-on-sql-databases/enable-auditing-on-sql-databases.png
[2]: ./media/security-center-enable-auditing-on-sql-databases/auditing-threat-detection-blade.png
