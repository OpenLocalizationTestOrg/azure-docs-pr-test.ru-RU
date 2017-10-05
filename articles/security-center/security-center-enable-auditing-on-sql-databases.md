---
title: "Включение аудита и обнаружения угроз для баз данных SQL в центре безопасности Azure | Документация Майкрософт"
description: "В этом документе показано, как реализовать рекомендацию центра безопасности Azure ** включить обнаружение аудита и угроз для базы данных SQL **."
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
ms.openlocfilehash: 8f4febdaa4497fee0dc690b59cd6eaa415c5e5cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="enable-auditing-and-threat-detection-on-sql-databases-in-azure-security-center"></a><span data-ttu-id="cdefe-103">Включение аудита и обнаружения угроз для баз данных SQL в центре безопасности Azure</span><span class="sxs-lookup"><span data-stu-id="cdefe-103">Enable auditing and threat detection on SQL databases in Azure Security Center</span></span>
<span data-ttu-id="cdefe-104">Центр безопасности Azure порекомендует включить аудит и обнаружение угроз для всех баз данных SQL, если эти функции еще не включены.</span><span class="sxs-lookup"><span data-stu-id="cdefe-104">Azure Security Center will recommend that you turn on auditing and threat detection for all SQL databases if auditing and threat detection is not already enabled.</span></span> <span data-ttu-id="cdefe-105">Аудит и обнаружение угроз могут помочь вам соблюсти стандарты, проанализировать работу с базой данных и получить представление о расхождениях и аномалиях, которые могут указывать на бизнес-проблемы или предполагаемые нарушения безопасности.</span><span class="sxs-lookup"><span data-stu-id="cdefe-105">Auditing and threat detection can help you maintain regulatory compliance, understand database activity, and gain insight into discrepancies and anomalies that could indicate business concerns or suspected security violations.</span></span>

<span data-ttu-id="cdefe-106">После включения аудита можно настроить параметры обнаружения угроз и электронных сообщений для получения оповещений системы безопасности.</span><span class="sxs-lookup"><span data-stu-id="cdefe-106">Once you’ve turned on auditing you can configure Threat Detection settings and emails to receive security alerts.</span></span> <span data-ttu-id="cdefe-107">Система обнаружения угроз обнаруживает подозрительную активность в базе данных, указывающую на наличие потенциальных угроз безопасности.</span><span class="sxs-lookup"><span data-stu-id="cdefe-107">Threat Detection detects anomalous database activities indicating potential security threats to the database.</span></span> <span data-ttu-id="cdefe-108">Это позволяет выявлять потенциальные угрозы и соответствующим образом реагировать при их возникновении.</span><span class="sxs-lookup"><span data-stu-id="cdefe-108">This enables you to detect and respond to potential threats as they occur.</span></span>

<span data-ttu-id="cdefe-109">Данная рекомендация относится только к службе SQL Azure и не охватывает службы SQL, работающие на виртуальных машинах.</span><span class="sxs-lookup"><span data-stu-id="cdefe-109">This recommendation applies to the Azure SQL service only; it doesn't include SQL running on your virtual machines.</span></span>

> [!NOTE]
> <span data-ttu-id="cdefe-110">В документе приводится обзор службы с помощью примера развертывания.</span><span class="sxs-lookup"><span data-stu-id="cdefe-110">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="cdefe-111">Он не является пошаговым руководством.</span><span class="sxs-lookup"><span data-stu-id="cdefe-111">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="cdefe-112">Выполнение рекомендаций</span><span class="sxs-lookup"><span data-stu-id="cdefe-112">Implement the recommendation</span></span>
1. <span data-ttu-id="cdefe-113">В колонке **Рекомендации** выберите **Включить аудит и обнаружение угроз для баз данных SQL**.</span><span class="sxs-lookup"><span data-stu-id="cdefe-113">In the **Recommendations** blade, select **Enable Auditing & Threat detection on SQL databases**.</span></span>  <span data-ttu-id="cdefe-114">Откроется колонка **Включение аудита и обнаружения угроз для баз данных SQL**.</span><span class="sxs-lookup"><span data-stu-id="cdefe-114">This opens the **Enable Auditing & Threat detection on SQL databases** blade.</span></span>

   ![Включение аудита для баз данных SQL][1]
2. <span data-ttu-id="cdefe-116">Выберите базу данных SQL для включения аудита.</span><span class="sxs-lookup"><span data-stu-id="cdefe-116">Select a SQL database to enable auditing on.</span></span> <span data-ttu-id="cdefe-117">Откроется колонка **Аудит и обнаружение угроз**.</span><span class="sxs-lookup"><span data-stu-id="cdefe-117">This opens the **Auditing & Threat Detection** blade.</span></span>

3. <span data-ttu-id="cdefe-118">В колонке **Аудит и обнаружение угроз** в разделе **Аудит** щелкните **Вкл.**</span><span class="sxs-lookup"><span data-stu-id="cdefe-118">On the **Auditing & Threat Detection** blade, select **ON** under **Auditing**.</span></span>

   ![Включение аудита и обнаружения угроз][2]
4. <span data-ttu-id="cdefe-120">Следуйте указаниям в разделе [Обнаружение угроз для базы данных SQL](../sql-database/sql-database-threat-detection-portal.md), чтобы включить и настроить обнаружение угроз, а также настроить список электронных адресов, на которые будут отправляться оповещения системы безопасности при обнаружении аномальных действий.</span><span class="sxs-lookup"><span data-stu-id="cdefe-120">Follow the steps in [SQL Database Threat Detection in the Azure portal](../sql-database/sql-database-threat-detection-portal.md) to turn on and configure Threat Detection and to configure the list of emails that will receive security alerts upon detection of anomalous activities.</span></span>

## <a name="see-also"></a><span data-ttu-id="cdefe-121">См. также</span><span class="sxs-lookup"><span data-stu-id="cdefe-121">See also</span></span>
<span data-ttu-id="cdefe-122">В этой статье показано, как выполнить рекомендацию центра безопасности по включению аудита и обнаружения угроз для баз данных SQL.</span><span class="sxs-lookup"><span data-stu-id="cdefe-122">This article showed you how to implement the Security Center recommendation "Enable Auditing & Threat detection on SQL databases."</span></span> <span data-ttu-id="cdefe-123">Чтобы узнать больше о защите базы данных SQL, ознакомьтесь со следующими статьями.</span><span class="sxs-lookup"><span data-stu-id="cdefe-123">To learn more about securing your SQL database, see the following:</span></span>

* [<span data-ttu-id="cdefe-124">Защита Базы данных SQL</span><span class="sxs-lookup"><span data-stu-id="cdefe-124">Securing your SQL Database</span></span>](../sql-database/sql-database-security-overview.md)

<span data-ttu-id="cdefe-125">Дополнительные сведения о Центре безопасности см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="cdefe-125">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="cdefe-126">[Настройка политик безопасности в Центре безопасности Azure](security-center-policies.md) — узнайте, как настроить политики безопасности для подписок и групп ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="cdefe-126">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="cdefe-127">[Управление рекомендациями по безопасности в Центре безопасности Azure](security-center-recommendations.md) — узнайте, как рекомендации могут помочь вам защитить ресурсы Azure.</span><span class="sxs-lookup"><span data-stu-id="cdefe-127">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="cdefe-128">[Наблюдение за работоспособностью системы безопасности в Центре безопасности Azure](security-center-monitoring.md) — узнайте, как наблюдать за работоспособностью ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="cdefe-128">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="cdefe-129">[Управление оповещениями безопасности в Центре безопасности Azure и реагирование на них](security-center-managing-and-responding-alerts.md) — узнайте, как управлять оповещениями системы безопасности и реагировать на них.</span><span class="sxs-lookup"><span data-stu-id="cdefe-129">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="cdefe-130">[Мониторинг решений партнеров с помощью центра безопасности Azure](security-center-partner-solutions.md) — узнайте, как отслеживать состояние работоспособности решений партнеров.</span><span class="sxs-lookup"><span data-stu-id="cdefe-130">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="cdefe-131">[Центр безопасности Azure: часто задаваемые вопросы](security-center-faq.md) — часто задаваемые вопросы об использовании этой службы.</span><span class="sxs-lookup"><span data-stu-id="cdefe-131">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="cdefe-132">[Блог по безопасности Azure](http://blogs.msdn.com/b/azuresecurity/) — последние новости и информация об обеспечении безопасности в Azure.</span><span class="sxs-lookup"><span data-stu-id="cdefe-132">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get the latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-auditing-on-sql-databases/enable-auditing-on-sql-databases.png
[2]: ./media/security-center-enable-auditing-on-sql-databases/auditing-threat-detection-blade.png
