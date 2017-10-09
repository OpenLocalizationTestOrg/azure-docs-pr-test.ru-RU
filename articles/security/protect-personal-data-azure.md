---
title: "aaaProtect персональные данные в Microsoft Azure | Документы Microsoft"
description: "Вначале статьи в серии статей toohelp использовать Azure tooprotect персональные данные"
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: cbffd3872552cbd0f12539535898c41ecf7789e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="protect-personal-data-in-microsoft-azure"></a><span data-ttu-id="8df6e-103">Защита персональных данных в Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="8df6e-103">Protect personal data in Microsoft Azure</span></span>

<span data-ttu-id="8df6e-104">В этой статье описывается ряд статей, которые позволяют использовать Azure технологий и служб tooprotect личных данных безопасности.</span><span class="sxs-lookup"><span data-stu-id="8df6e-104">This article introduces a series of articles that help you use Azure security technologies and services tooprotect personal data.</span></span> <span data-ttu-id="8df6e-105">Таково основное требование многих корпоративных и промышленных стандартов соответствия нормам.</span><span class="sxs-lookup"><span data-stu-id="8df6e-105">This is a key requirement for many corporate and industry compliance and governance initiatives.</span></span> <span data-ttu-id="8df6e-106">сценарий Hello проблема инструкции и компании цели Сюда включены.</span><span class="sxs-lookup"><span data-stu-id="8df6e-106">hello scenario, problem statement and company goals are included here.</span></span>

## <a name="scenario-and-problem-statement"></a><span data-ttu-id="8df6e-107">Сценарий и постановка проблемы</span><span class="sxs-lookup"><span data-stu-id="8df6e-107">Scenario and problem statement</span></span>

<span data-ttu-id="8df6e-108">Компании больших прогулка по, рядом с офисом в Соединенных Штатах Америки hello, развернут расписаниям toooffer его операций в морская hello, Adriatic и Балтийский компании seas, а также Британские острова hello.</span><span class="sxs-lookup"><span data-stu-id="8df6e-108">A large cruise company, headquartered in hello United States, is expanding its operations toooffer itineraries in hello Mediterranean, Adriatic, and Baltic seas, as well as hello British Isles.</span></span> <span data-ttu-id="8df6e-109">toosupport эти усилия, он получил несколько небольших строк прогулка по в Италии, Германии, Дания и hello Великобритания</span><span class="sxs-lookup"><span data-stu-id="8df6e-109">toosupport those efforts, it has acquired several smaller cruise lines based in Italy, Germany, Denmark and hello U.K.</span></span>

<span data-ttu-id="8df6e-110">Hello компания использует Microsoft Azure toostore корпоративных данных в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="8df6e-110">hello company uses Microsoft Azure toostore corporate data in hello cloud.</span></span> <span data-ttu-id="8df6e-111">Это может включать сотрудников и/или сведения о заказчике такие как:</span><span class="sxs-lookup"><span data-stu-id="8df6e-111">This may include employee and/or customer information such as:</span></span>

- <span data-ttu-id="8df6e-112">адреса;</span><span class="sxs-lookup"><span data-stu-id="8df6e-112">addresses</span></span>
- <span data-ttu-id="8df6e-113">номера телефонов;</span><span class="sxs-lookup"><span data-stu-id="8df6e-113">phone numbers</span></span>
- <span data-ttu-id="8df6e-114">идентификационные номера налогоплательщиков;</span><span class="sxs-lookup"><span data-stu-id="8df6e-114">tax identification numbers</span></span>
- <span data-ttu-id="8df6e-115">медицинские сведения</span><span class="sxs-lookup"><span data-stu-id="8df6e-115">medical information</span></span>
- <span data-ttu-id="8df6e-116">данные кредитной карты.</span><span class="sxs-lookup"><span data-stu-id="8df6e-116">credit card information</span></span>

<span data-ttu-id="8df6e-117">Hello компании должны защищать конфиденциальность hello данных сотрудников и клиентов во время внесения данных доступны toothose отделов, которым она необходима.</span><span class="sxs-lookup"><span data-stu-id="8df6e-117">hello company must protect hello privacy of employee and customer data while making data accessible toothose departments that need it.</span></span> <span data-ttu-id="8df6e-118">(например, отделах заработной платы и бронирования).</span><span class="sxs-lookup"><span data-stu-id="8df6e-118">(such as payroll and reservations departments)</span></span>

## <a name="company-goals"></a><span data-ttu-id="8df6e-119">Цели компании</span><span class="sxs-lookup"><span data-stu-id="8df6e-119">Company goals</span></span> 

- <span data-ttu-id="8df6e-120">Источники данных с персональными данными шифруются, если находятся в облачном хранилище.</span><span class="sxs-lookup"><span data-stu-id="8df6e-120">Data sources that contain personal data are encrypted when residing in cloud storage.</span></span>

- <span data-ttu-id="8df6e-121">Персональные данные, которые переносятся из одного расположения tooanother шифроваться, если во время передачи.</span><span class="sxs-lookup"><span data-stu-id="8df6e-121">Personal data that is transferred from one location tooanother is encrypted while in-transit.</span></span> <span data-ttu-id="8df6e-122">Это значение true, если данные hello проходящих между hello виртуальной сети или в Интернете hello между hello корпоративном центре обработки данных и hello облако Azure.</span><span class="sxs-lookup"><span data-stu-id="8df6e-122">This is true if hello data is traveling across hello virtual network or across hello Internet between hello corporate datacenter and hello Azure cloud.</span></span>

- <span data-ttu-id="8df6e-123">Конфиденциальность и целостность персональных данных обеспечивается с помощью надежных технологий управления удостоверениями и доступом.</span><span class="sxs-lookup"><span data-stu-id="8df6e-123">Confidentiality and integrity of personal data is protected from unauthorized access by strong identity management and access control technologies.</span></span>

- <span data-ttu-id="8df6e-124">Персональные данные защищены от разглашения из-за бреши в системе безопасности благодаря мониторингу уязвимостей и угроз.</span><span class="sxs-lookup"><span data-stu-id="8df6e-124">Personal data is protected from exposure via data breach via monitoring for vulnerabilities and threats.</span></span>

- <span data-ttu-id="8df6e-125">Hello состояния безопасности служб Azure, которые хранить или передавать данные о личных оценивается toobetter tooidentify возможности защиты личных данных.</span><span class="sxs-lookup"><span data-stu-id="8df6e-125">hello security state of Azure services that store or transmit personal data is assessed tooidentify opportunities toobetter protect personal data.</span></span>

## <a name="data-protection-guidance"></a><span data-ttu-id="8df6e-126">Руководства по защите данных</span><span class="sxs-lookup"><span data-stu-id="8df6e-126">Data protection guidance</span></span>

<span data-ttu-id="8df6e-127">Привет, следующие статьи содержат технические как tooguidance, которые помогут достичь целей защиты личных данных hello, перечисленных выше:</span><span class="sxs-lookup"><span data-stu-id="8df6e-127">hello following articles contain technical how-tooguidance that will help you attain hello personal data protection goals listed above:</span></span>

- [<span data-ttu-id="8df6e-128">Технологии шифрования Azure. Защита персональных данных при передаче с помощью шифрования</span><span class="sxs-lookup"><span data-stu-id="8df6e-128">Azure encryption technologies</span></span>](protect-personal-data-at-rest.md)

- [<span data-ttu-id="8df6e-129">Технологии шифрования Azure. Защита персональных данных при передаче с помощью шифрования</span><span class="sxs-lookup"><span data-stu-id="8df6e-129">Azure encryption technologies</span></span>](protect-personal-data-in-transit-encryption.md)

- [<span data-ttu-id="8df6e-130">Azure Active Directory и Многофакторная идентификация. Защита персональных данных с помощью управления удостоверениями и доступом</span><span class="sxs-lookup"><span data-stu-id="8df6e-130">Azure identity and access technologies</span></span>](protect-personal-data-identity-access-controls.md)

- [<span data-ttu-id="8df6e-131">Защита персональных данных с помощью функций безопасности сети Azure: шлюз приложений и группы безопасности сети Azure</span><span class="sxs-lookup"><span data-stu-id="8df6e-131">Azure network security technologies</span></span>](protect-personal-data-network-security.md)

- [<span data-ttu-id="8df6e-132">Центр безопасности Azure</span><span class="sxs-lookup"><span data-stu-id="8df6e-132">Azure Security Center</span></span>](protect-personal-data-azure-security-center.md)



## <a name="next-steps"></a><span data-ttu-id="8df6e-133">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8df6e-133">Next steps</span></span>

- [<span data-ttu-id="8df6e-134">Документация по системе безопасности</span><span class="sxs-lookup"><span data-stu-id="8df6e-134">Azure Security Information Site</span></span>](https://aka.ms/AzureSecInfo)

- [<span data-ttu-id="8df6e-135">Центр управления безопасностью Майкрософт</span><span class="sxs-lookup"><span data-stu-id="8df6e-135">Microsoft Trust Center</span></span>](https://www.microsoft.com/TrustCenter/default.aspx)

- [<span data-ttu-id="8df6e-136">Центр безопасности Azure</span><span class="sxs-lookup"><span data-stu-id="8df6e-136">Azure Security Center</span></span>](https://azure.microsoft.com/services/security-center/)

- [<span data-ttu-id="8df6e-137">Блог группы безопасности Azure</span><span class="sxs-lookup"><span data-stu-id="8df6e-137">Azure Security Team Blog</span></span>](https://www.azuresecurityorg)

- [<span data-ttu-id="8df6e-138">Блог Azure.com, посвященный вопросам безопасности</span><span class="sxs-lookup"><span data-stu-id="8df6e-138">Azure.com Blog - Security</span></span>](https://azure.microsoft.com/blog/topics/security/)
