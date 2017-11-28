---
title: "aaaProtecting Azure SQL службы и данных в центр безопасности Azure | Документы Microsoft"
description: "В этом документе рассматриваются рекомендации из центра безопасности Azure, которые помогают защитить ваши данные и службу SQL Azure, а также обеспечить соответствие политикам безопасности."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: bcae6987-05d0-4208-bca8-6a6ce7c9a1e3
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/03/2017
ms.author: terrylan
ms.openlocfilehash: 75d782d3c2418f9645139e4cd6ecb7765c488f91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="protecting-azure-sql-service-and-data-in-azure-security-center"></a><span data-ttu-id="d5efc-103">Защита службы SQL Azure и данных в центре безопасности Azure</span><span class="sxs-lookup"><span data-stu-id="d5efc-103">Protecting Azure SQL service and data in Azure Security Center</span></span>
<span data-ttu-id="d5efc-104">Центр безопасности Azure анализирует состояние безопасности hello ресурсам Azure.</span><span class="sxs-lookup"><span data-stu-id="d5efc-104">Azure Security Center analyzes hello security state of your Azure resources.</span></span> <span data-ttu-id="d5efc-105">Когда центр обеспечения безопасности выявляет потенциальные уязвимости системы безопасности, он создает рекомендации, которые hello процесс настройки hello необходимые элементы управления.</span><span class="sxs-lookup"><span data-stu-id="d5efc-105">When Security Center identifies potential security vulnerabilities, it creates recommendations that guide you through hello process of configuring hello needed controls.</span></span>  <span data-ttu-id="d5efc-106">Рекомендации относятся типы ресурсов tooAzure: виртуальных машин (ВМ), сети, SQL и данных и приложений.</span><span class="sxs-lookup"><span data-stu-id="d5efc-106">Recommendations apply tooAzure resource types: virtual machines (VMs), networking, SQL and data, and applications.</span></span>

<span data-ttu-id="d5efc-107">В этой статье рассматриваются рекомендации, которые применяются tooAzure службы SQL и данных.</span><span class="sxs-lookup"><span data-stu-id="d5efc-107">This article addresses recommendations that apply tooAzure SQL service and data.</span></span> <span data-ttu-id="d5efc-108">а также рекомендации включения аудита для серверов и баз данных SQL Azure, включения шифрования для баз данных SQL и включения шифрования учетной записи хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="d5efc-108">Recommendations center around enabling auditing for Azure SQL servers and databases, enabling encryption for SQL databases, and enabling encryption of your Azure storage account.</span></span>  <span data-ttu-id="d5efc-109">Использовать таблицу hello ниже как toohelp ссылку, вы понимаете hello доступных служб и данных рекомендации по SQL и назначение каждого из них при его применении.</span><span class="sxs-lookup"><span data-stu-id="d5efc-109">Use hello table below as a reference toohelp you understand hello available SQL service and data recommendations and what each one does if you apply it.</span></span>

## <a name="available-sql-service-and-data-recommendations"></a><span data-ttu-id="d5efc-110">Доступные рекомендации для службы SQL и данных</span><span class="sxs-lookup"><span data-stu-id="d5efc-110">Available SQL service and data recommendations</span></span>
| <span data-ttu-id="d5efc-111">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="d5efc-111">Recommendation</span></span> | <span data-ttu-id="d5efc-112">Описание</span><span class="sxs-lookup"><span data-stu-id="d5efc-112">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="d5efc-113">Включение аудита и обнаружения угроз на серверах SQL Server</span><span class="sxs-lookup"><span data-stu-id="d5efc-113">Enable auditing and threat detection on SQL servers</span></span>](security-center-enable-auditing-on-sql-servers.md) |<span data-ttu-id="d5efc-114">Рекомендует включить аудит и обнаружение угроз для серверов SQL Azure (только для службы SQL Azure, не включая экземпляры SQL, работающие на виртуальных машинах).</span><span class="sxs-lookup"><span data-stu-id="d5efc-114">Recommends that you turn on auditing and threat detection for Azure SQL servers (Azure SQL service only; doesn't include SQL running on your virtual machines).</span></span> |
| [<span data-ttu-id="d5efc-115">Включение аудита и обнаружения угроз для баз данных SQL</span><span class="sxs-lookup"><span data-stu-id="d5efc-115">Enable auditing and threat detection on SQL databases</span></span>](security-center-enable-auditing-on-sql-databases.md) |<span data-ttu-id="d5efc-116">Рекомендует включить аудит и обнаружение угроз для баз данных SQL в Azure (только для службы SQL Azure, не включая экземпляры SQL, работающие на виртуальных машинах).</span><span class="sxs-lookup"><span data-stu-id="d5efc-116">Recommends that you turn on auditing and threat detection for Azure SQL databases (Azure SQL service only; doesn't include SQL running on your virtual machines).</span></span> |
| [<span data-ttu-id="d5efc-117">Включение прозрачного шифрования данных в базах данных SQL</span><span class="sxs-lookup"><span data-stu-id="d5efc-117">Enable Transparent Data Encryption on SQL databases</span></span>](security-center-enable-transparent-data-encryption.md) |<span data-ttu-id="d5efc-118">Рекомендует включить шифрование для баз данных SQL (только для службы SQL Azure).</span><span class="sxs-lookup"><span data-stu-id="d5efc-118">Recommends that you enable encryption for SQL databases (Azure SQL service only).</span></span> |

## <a name="see-also"></a><span data-ttu-id="d5efc-119">См. также</span><span class="sxs-lookup"><span data-stu-id="d5efc-119">See also</span></span>
<span data-ttu-id="d5efc-120">Дополнительные сведения о рекомендации, которые применяются tooother типы ресурсов Azure см. в разделе ниже hello toolearn:</span><span class="sxs-lookup"><span data-stu-id="d5efc-120">toolearn more about recommendations that apply tooother Azure resource types, see hello following:</span></span>

* [<span data-ttu-id="d5efc-121">Защита виртуальных машин в центре безопасности Azure.</span><span class="sxs-lookup"><span data-stu-id="d5efc-121">Protecting your virtual machines in Azure Security Center</span></span>](security-center-virtual-machine-recommendations.md)
* [<span data-ttu-id="d5efc-122">Защита приложений в центре безопасности Azure</span><span class="sxs-lookup"><span data-stu-id="d5efc-122">Protecting your applications in Azure Security Center</span></span>](security-center-application-recommendations.md)
* [<span data-ttu-id="d5efc-123">Защита сети в центре безопасности Azure.</span><span class="sxs-lookup"><span data-stu-id="d5efc-123">Protecting your network in Azure Security Center</span></span>](security-center-network-recommendations.md)

<span data-ttu-id="d5efc-124">toolearn Дополнительные сведения о центра обеспечения безопасности, см. ниже hello:</span><span class="sxs-lookup"><span data-stu-id="d5efc-124">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="d5efc-125">[Установка политики безопасности в центр безопасности Azure](security-center-policies.md) — Узнайте, как tooconfigure политики безопасности для вашей подписки Azure и группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="d5efc-125">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="d5efc-126">[Управление и отвечает на запросы toosecurity предупреждения в центр безопасности Azure](security-center-managing-and-responding-alerts.md) --Узнайте, как предупреждения toosecurity toomanage и отправки ответа.</span><span class="sxs-lookup"><span data-stu-id="d5efc-126">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="d5efc-127">[Центр безопасности Azure часто задаваемые вопросы о](security-center-faq.md) — часто задаваемые вопросы об использовании hello службы поиска.</span><span class="sxs-lookup"><span data-stu-id="d5efc-127">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
