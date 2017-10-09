---
title: "Прозрачное шифрование данных в центр безопасности Azure aaaEnable | Документы Microsoft"
description: "В этом документе показано, как tooimplement hello рекомендации центра безопасности Azure ** включить прозрачное данных шифрования **."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: e4be8a0e-2118-4ee9-a266-69e52d9f7f8e
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 94c6e9a1feddaa48faac6c835d416c4d131cd5c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="enable-transparent-data-encryption-in-azure-security-center"></a><span data-ttu-id="5eb57-103">Включение прозрачного шифрования данных в центре безопасности Azure</span><span class="sxs-lookup"><span data-stu-id="5eb57-103">Enable Transparent Data Encryption in Azure Security Center</span></span>
<span data-ttu-id="5eb57-104">Центр безопасности Azure порекомендует включить прозрачное шифрование данных (TDE) для баз данных SQL, если оно еще не включено.</span><span class="sxs-lookup"><span data-stu-id="5eb57-104">Azure Security Center will recommend that you enable Transparent Data Encryption (TDE) on SQL databases if TDE is not already enabled.</span></span> <span data-ttu-id="5eb57-105">Прозрачное шифрование данных защищает данные и помогает соответствие требованиям путем шифрования вашей базы данных, связанных резервных копий и файлов журнала транзакций в rest, не требуя внесения изменений tooyour приложения.</span><span class="sxs-lookup"><span data-stu-id="5eb57-105">TDE protects your data and helps you meet compliance requirements by encrypting your database, associated backups, and transaction log files at rest, without requiring changes tooyour application.</span></span> <span data-ttu-id="5eb57-106">более разделе toolearn [прозрачное шифрование данных с базой данных SQL Azure](https://msdn.microsoft.com/library/dn948096).</span><span class="sxs-lookup"><span data-stu-id="5eb57-106">toolearn more see [Transparent Data Encryption with Azure SQL Database](https://msdn.microsoft.com/library/dn948096).</span></span>

<span data-ttu-id="5eb57-107">Данная рекомендация применяется toohello службой Azure SQL. не содержит SQL, работающих на виртуальных машинах.</span><span class="sxs-lookup"><span data-stu-id="5eb57-107">This recommendation applies toohello Azure SQL service only; doesn't include SQL running on your virtual machines.</span></span>

> [!NOTE]
> <span data-ttu-id="5eb57-108">В этом документе представлены hello службы с помощью пример развертывания.</span><span class="sxs-lookup"><span data-stu-id="5eb57-108">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="5eb57-109">Он не является пошаговым руководством.</span><span class="sxs-lookup"><span data-stu-id="5eb57-109">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="5eb57-110">Реализация рекомендаций hello</span><span class="sxs-lookup"><span data-stu-id="5eb57-110">Implement hello recommendation</span></span>
1. <span data-ttu-id="5eb57-111">В hello **рекомендации** колонке выберите **Включение прозрачного шифрования данных**.</span><span class="sxs-lookup"><span data-stu-id="5eb57-111">In hello **Recommendations** blade, select **Enable Transparent Data Encryption**.</span></span>
   <span data-ttu-id="5eb57-112">![Включение прозрачного шифрования данных][1]</span><span class="sxs-lookup"><span data-stu-id="5eb57-112">![Enable Transparent Data Encryption][1]</span></span>
2. <span data-ttu-id="5eb57-113">При этом откроется hello **Включение прозрачного шифрования данных в базах данных SQL** колонку.</span><span class="sxs-lookup"><span data-stu-id="5eb57-113">This opens hello **Enable Transparent Data Encryption on SQL databases** blade.</span></span> <span data-ttu-id="5eb57-114">Выберите tooenable базы данных SQL прозрачного шифрования данных.</span><span class="sxs-lookup"><span data-stu-id="5eb57-114">Select a SQL database tooenable TDE on.</span></span>
   <span data-ttu-id="5eb57-115">![Выбор баз данных SQL Server tooenable прозрачное шифрование данных на][2]</span><span class="sxs-lookup"><span data-stu-id="5eb57-115">![Select SQL DB tooenable TDE on][2]</span></span>
3. <span data-ttu-id="5eb57-116">На hello **прозрачное шифрование данных** колонке выберите **ON** под шифрование данных и выберите **Сохранить** в верхней ленте hello колонка hello.</span><span class="sxs-lookup"><span data-stu-id="5eb57-116">On hello **Transparent data encryption** blade, select **ON** under Data encryption and select **Save** in hello top ribbon of hello blade.</span></span>
   <span data-ttu-id="5eb57-117">![Включение прозрачного шифрования данных][3]</span><span class="sxs-lookup"><span data-stu-id="5eb57-117">![Turn on TDE][3]</span></span>

   <span data-ttu-id="5eb57-118">После включения прозрачного шифрования данных в hello выбранной базы данных SQL, hello **состояние шифрования** изменится слишком**шифрование**.</span><span class="sxs-lookup"><span data-stu-id="5eb57-118">Once TDE is enabled on hello selected SQL database, hello **Encryption status** will change too**Encrypted**.</span></span>    

   ![Состояние шифрования][4]

## <a name="see-also"></a><span data-ttu-id="5eb57-120">См. также</span><span class="sxs-lookup"><span data-stu-id="5eb57-120">See also</span></span>
<span data-ttu-id="5eb57-121">В этой статье показано, как tooimplement hello рекомендации центра обеспечения безопасности «Включить прозрачное шифрование данных.»</span><span class="sxs-lookup"><span data-stu-id="5eb57-121">This article showed you how tooimplement hello Security Center recommendation "Enable Transparent Data Encryption."</span></span> <span data-ttu-id="5eb57-122">toolearn Дополнительные сведения о прозрачном шифровании данных SQL см. ниже hello:</span><span class="sxs-lookup"><span data-stu-id="5eb57-122">toolearn more about SQL TDE, see hello following:</span></span>

* [<span data-ttu-id="5eb57-123">Прозрачное шифрование данных в Базе данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="5eb57-123">Transparent Data Encryption with Azure SQL Database</span></span>](https://msdn.microsoft.com/library/dn948096)
* [<span data-ttu-id="5eb57-124">Начало работы с прозрачным шифрованием данных (TDE)</span><span class="sxs-lookup"><span data-stu-id="5eb57-124">Get started with Transparent Data Encryption (TDE)</span></span>](../sql-data-warehouse/sql-data-warehouse-encryption-tde.md)

<span data-ttu-id="5eb57-125">toolearn Дополнительные сведения о центра обеспечения безопасности, см. ниже hello:</span><span class="sxs-lookup"><span data-stu-id="5eb57-125">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="5eb57-126">[Установка политики безопасности в центр безопасности Azure](security-center-policies.md) — Узнайте, как tooconfigure политики безопасности для вашей подписки Azure и группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="5eb57-126">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="5eb57-127">[Управление рекомендациями по безопасности в Центре безопасности Azure](security-center-recommendations.md) — узнайте, как рекомендации могут помочь вам защитить ресурсы Azure.</span><span class="sxs-lookup"><span data-stu-id="5eb57-127">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="5eb57-128">[Наблюдение за работоспособностью системы безопасности в центр безопасности Azure](security-center-monitoring.md) — Узнайте, как toomonitor hello работоспособности ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="5eb57-128">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="5eb57-129">[Управление и отвечает на запросы toosecurity предупреждения в центр безопасности Azure](security-center-managing-and-responding-alerts.md) --Узнайте, как предупреждения toosecurity toomanage и отправки ответа.</span><span class="sxs-lookup"><span data-stu-id="5eb57-129">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="5eb57-130">[Мониторинг решений партнера с центром обеспечения безопасности Azure](security-center-partner-solutions.md) — Узнайте, как toomonitor hello состояние работоспособности решений для партнера.</span><span class="sxs-lookup"><span data-stu-id="5eb57-130">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="5eb57-131">[Центр безопасности Azure часто задаваемые вопросы о](security-center-faq.md) — часто задаваемые вопросы об использовании hello службы поиска.</span><span class="sxs-lookup"><span data-stu-id="5eb57-131">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="5eb57-132">[Блог Azure безопасности](http://blogs.msdn.com/b/azuresecurity/) --получить последние новости безопасности Azure hello и информацию.</span><span class="sxs-lookup"><span data-stu-id="5eb57-132">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get hello latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-tde-on-sql-databases/enable-tde.png
[2]:./media/security-center-enable-tde-on-sql-databases/transparent-data-encryption-blade.png
[3]: ./media/security-center-enable-tde-on-sql-databases/turn-on-tde.png
[4]: ./media/security-center-enable-tde-on-sql-databases/encrypted.png
