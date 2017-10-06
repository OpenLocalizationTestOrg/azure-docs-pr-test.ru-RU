---
title: "aaaFinding неуправляемого облачных приложений с Cloud App Discovery | Документы Microsoft"
description: "Сведения о поиске и управление приложениями с помощью Cloud App Discovery, Каковы преимущества hello и как он работает."
services: active-directory
keywords: "cloud app discovery, управление приложениями"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: db968bf5-22ae-489f-9c3e-14df6e1fef0a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 50c24af9bb400e4be11f4ad2d1de13d26f5467bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="finding-unmanaged-cloud-applications-with-cloud-app-discovery"></a><span data-ttu-id="79137-104">Поиск неуправляемых облачных приложений с помощью Cloud App Discovery</span><span class="sxs-lookup"><span data-stu-id="79137-104">Finding unmanaged cloud applications with Cloud App Discovery</span></span>
## <a name="overview"></a><span data-ttu-id="79137-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="79137-105">Overview</span></span>
<span data-ttu-id="79137-106">На современных предприятиях ИТ-отделы, часто не знают все hello облачных приложений, что члены организации используют toodo свою работу.</span><span class="sxs-lookup"><span data-stu-id="79137-106">In modern enterprises, IT departments are often not aware of all hello cloud applications that members of their organization use toodo their work.</span></span> <span data-ttu-id="79137-107">Это легко toosee, почему Администраторы бы обеспокоены toocorporate несанкционированного доступа к данным, возможными утечками данных и других угроз безопасности.</span><span class="sxs-lookup"><span data-stu-id="79137-107">It is easy toosee why administrators would have concerns about unauthorized access toocorporate data, possible data leakage and other security risks.</span></span> <span data-ttu-id="79137-108">Эта недостаточная осведомленность может сильно усложнить разработку плана по борьбе с этими угрозами безопасности.</span><span class="sxs-lookup"><span data-stu-id="79137-108">This lack of awareness can make creating a plan for dealing with these security risks seem daunting.</span></span>

<span data-ttu-id="79137-109">Cloud App Discovery — это функция Azure Active Directory (AD) Premium, благодаря которой вы toodiscover облачных приложений, используемых hello сотрудниками вашей организации.</span><span class="sxs-lookup"><span data-stu-id="79137-109">Cloud App Discovery is a feature of Azure Active Directory (AD) Premium that enables you toodiscover cloud applications being used by hello people in your organization.</span></span>

<span data-ttu-id="79137-110">**С помощью Cloud App Discovery вы сможете:**</span><span class="sxs-lookup"><span data-stu-id="79137-110">**With Cloud App Discovery, you can:**</span></span>

* <span data-ttu-id="79137-111">Найдите hello облачные приложения используются и мера такого использования, по количеству пользователей, объему трафика или количество toohello запросов веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="79137-111">Find hello cloud applications being used and measure that usage by number of users, volume of traffic or number of web requests toohello application.</span></span>
* <span data-ttu-id="79137-112">Определите hello пользователей, использующих приложения.</span><span class="sxs-lookup"><span data-stu-id="79137-112">Identify hello users that are using an application.</span></span>
* <span data-ttu-id="79137-113">Экспортировать данные для автономного анализа.</span><span class="sxs-lookup"><span data-stu-id="79137-113">Export data for offline analysis.</span></span>
* <span data-ttu-id="79137-114">Получить контроль над этими приложениями с помощью средств ИТ и включить доступ с единым входом для управления пользователями.</span><span class="sxs-lookup"><span data-stu-id="79137-114">Bring these applications under IT control and enable single sign on for user management.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="79137-115">Принцип работы</span><span class="sxs-lookup"><span data-stu-id="79137-115">How it works</span></span>
1. <span data-ttu-id="79137-116">На компьютерах пользователей устанавливаются агенты использования приложения.</span><span class="sxs-lookup"><span data-stu-id="79137-116">Application usage agents are installed on user's computers.</span></span>
2. <span data-ttu-id="79137-117">сведения об использовании приложения Hello, записанные агентами hello передаются через служба безопасный, зашифрованный канал toohello cloud app discovery.</span><span class="sxs-lookup"><span data-stu-id="79137-117">hello application usage information captured by hello agents is sent over a secure, encrypted channel toohello cloud app discovery service.</span></span>
3. <span data-ttu-id="79137-118">Hello службы Cloud App Discovery оценивает данные hello и создает отчеты.</span><span class="sxs-lookup"><span data-stu-id="79137-118">hello Cloud App Discovery service evaluates hello data and generates reports.</span></span>

![Схема Cloud App Discovery](./media/active-directory-cloudappdiscovery/cad01.png)

<span data-ttu-id="79137-120">tooget работы с Cloud App Discovery см [Приступая к работе с Cloud App Discovery](http://social.technet.microsoft.com/wiki/contents/articles/30962.getting-started-with-cloud-app-discovery.aspx)</span><span class="sxs-lookup"><span data-stu-id="79137-120">tooget started with Cloud App Discovery, see [Getting Started With Cloud App Discovery](http://social.technet.microsoft.com/wiki/contents/articles/30962.getting-started-with-cloud-app-discovery.aspx)</span></span>

## <a name="related-articles"></a><span data-ttu-id="79137-121">Связанные статьи</span><span class="sxs-lookup"><span data-stu-id="79137-121">Related articles</span></span>
* [<span data-ttu-id="79137-122">Вопросы безопасности и конфиденциальности Cloud App Discovery</span><span class="sxs-lookup"><span data-stu-id="79137-122">Cloud App Discovery Security and Privacy Considerations</span></span>](active-directory-cloudappdiscovery-security-and-privacy-considerations.md)  
* [<span data-ttu-id="79137-123">Руководство по развертыванию групповой политики Cloud App Discovery</span><span class="sxs-lookup"><span data-stu-id="79137-123">Cloud App Discovery Group Policy Deployment Guide</span></span>](http://social.technet.microsoft.com/wiki/contents/articles/30965.cloud-app-discovery-group-policy-deployment-guide.aspx)
* [<span data-ttu-id="79137-124">Руководство по развертыванию центра Cloud App Discovery</span><span class="sxs-lookup"><span data-stu-id="79137-124">Cloud App Discovery System Center Deployment Guide</span></span>](http://social.technet.microsoft.com/wiki/contents/articles/30968.cloud-app-discovery-system-center-deployment-guide.aspx)
* [<span data-ttu-id="79137-125">Параметры реестра для настройки Cloud App Discovery для прокси-серверов с пользовательскими портами</span><span class="sxs-lookup"><span data-stu-id="79137-125">Cloud App Discovery Registry Settings for Proxy Servers with Custom Ports</span></span>](active-directory-cloudappdiscovery-registry-settings-for-proxy-services.md)
* [<span data-ttu-id="79137-126">Журнал изменений агента Cloud App Discovery </span><span class="sxs-lookup"><span data-stu-id="79137-126">Cloud App Discovery Agent Changelog </span></span>](http://social.technet.microsoft.com/wiki/contents/articles/24616.cloud-app-discovery-agent-changelog.aspx)
* [<span data-ttu-id="79137-127">Часто задаваемые вопросы по Cloud App Discovery</span><span class="sxs-lookup"><span data-stu-id="79137-127">Cloud App Discovery Frequently Asked Questions</span></span>](http://social.technet.microsoft.com/wiki/contents/articles/24037.cloud-app-discovery-frequently-asked-questions.aspx)
* [<span data-ttu-id="79137-128">Указатель статьей по управлению приложениями в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="79137-128">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)

