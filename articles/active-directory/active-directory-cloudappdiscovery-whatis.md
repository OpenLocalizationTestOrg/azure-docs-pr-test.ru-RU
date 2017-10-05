---
title: "Поиск неуправляемых облачных приложений с помощью Cloud App Discovery | Документация Майкрософт"
description: "Содержит сведения о поиске приложений и управлении ими с помощью Cloud App Discovery, а также преимуществах и принципах работы Cloud App Discovery."
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
ms.openlocfilehash: 6284ff5bac8edbc19561d0916adef153526dfbe3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="finding-unmanaged-cloud-applications-with-cloud-app-discovery"></a><span data-ttu-id="c7d0b-104">Поиск неуправляемых облачных приложений с помощью Cloud App Discovery</span><span class="sxs-lookup"><span data-stu-id="c7d0b-104">Finding unmanaged cloud applications with Cloud App Discovery</span></span>
## <a name="overview"></a><span data-ttu-id="c7d0b-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="c7d0b-105">Overview</span></span>
<span data-ttu-id="c7d0b-106">На современных предприятиях ИТ-специалисты часто не знают обо всех облачных приложениях, при помощи которых пользователи выполняют свои задачи.</span><span class="sxs-lookup"><span data-stu-id="c7d0b-106">In modern enterprises, IT departments are often not aware of all the cloud applications that members of their organization use to do their work.</span></span> <span data-ttu-id="c7d0b-107">Легко понять, почему администраторов беспокоят несанкционированный доступ к корпоративным данным, возможная утечка данных и другие угрозы безопасности.</span><span class="sxs-lookup"><span data-stu-id="c7d0b-107">It is easy to see why administrators would have concerns about unauthorized access to corporate data, possible data leakage and other security risks.</span></span> <span data-ttu-id="c7d0b-108">Эта недостаточная осведомленность может сильно усложнить разработку плана по борьбе с этими угрозами безопасности.</span><span class="sxs-lookup"><span data-stu-id="c7d0b-108">This lack of awareness can make creating a plan for dealing with these security risks seem daunting.</span></span>

<span data-ttu-id="c7d0b-109">Cloud App Discovery — это функция службы Azure Active Directory (AD) уровня Премиум, которая позволяет обнаруживать облачные приложения, используемые сотрудниками организации.</span><span class="sxs-lookup"><span data-stu-id="c7d0b-109">Cloud App Discovery is a feature of Azure Active Directory (AD) Premium that enables you to discover cloud applications being used by the people in your organization.</span></span>

<span data-ttu-id="c7d0b-110">**С помощью Cloud App Discovery вы сможете:**</span><span class="sxs-lookup"><span data-stu-id="c7d0b-110">**With Cloud App Discovery, you can:**</span></span>

* <span data-ttu-id="c7d0b-111">Обнаруживать используемые облачные приложения и оценивать их использование по числу пользователей, объему трафика или числу веб-запросов к приложению.</span><span class="sxs-lookup"><span data-stu-id="c7d0b-111">Find the cloud applications being used and measure that usage by number of users, volume of traffic or number of web requests to the application.</span></span>
* <span data-ttu-id="c7d0b-112">Идентифицировать пользователей, использующих приложение.</span><span class="sxs-lookup"><span data-stu-id="c7d0b-112">Identify the users that are using an application.</span></span>
* <span data-ttu-id="c7d0b-113">Экспортировать данные для автономного анализа.</span><span class="sxs-lookup"><span data-stu-id="c7d0b-113">Export data for offline analysis.</span></span>
* <span data-ttu-id="c7d0b-114">Получить контроль над этими приложениями с помощью средств ИТ и включить доступ с единым входом для управления пользователями.</span><span class="sxs-lookup"><span data-stu-id="c7d0b-114">Bring these applications under IT control and enable single sign on for user management.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="c7d0b-115">Принцип работы</span><span class="sxs-lookup"><span data-stu-id="c7d0b-115">How it works</span></span>
1. <span data-ttu-id="c7d0b-116">На компьютерах пользователей устанавливаются агенты использования приложения.</span><span class="sxs-lookup"><span data-stu-id="c7d0b-116">Application usage agents are installed on user's computers.</span></span>
2. <span data-ttu-id="c7d0b-117">Информация об использовании приложения, записанная агентами, отправляется по безопасному зашифрованному каналу в службу Cloud App Discovery.</span><span class="sxs-lookup"><span data-stu-id="c7d0b-117">The application usage information captured by the agents is sent over a secure, encrypted channel to the cloud app discovery service.</span></span>
3. <span data-ttu-id="c7d0b-118">Служба Cloud App Discovery оценивает данные и создает отчеты.</span><span class="sxs-lookup"><span data-stu-id="c7d0b-118">The Cloud App Discovery service evaluates the data and generates reports.</span></span>

![Схема Cloud App Discovery](./media/active-directory-cloudappdiscovery/cad01.png)

<span data-ttu-id="c7d0b-120">Дополнительную информацию о работе Cloud App Discovery см. в статье [Getting Started With Cloud App Discovery](http://social.technet.microsoft.com/wiki/contents/articles/30962.getting-started-with-cloud-app-discovery.aspx) (Начало работы с Cloud App Discovery).</span><span class="sxs-lookup"><span data-stu-id="c7d0b-120">To get started with Cloud App Discovery, see [Getting Started With Cloud App Discovery](http://social.technet.microsoft.com/wiki/contents/articles/30962.getting-started-with-cloud-app-discovery.aspx)</span></span>

## <a name="related-articles"></a><span data-ttu-id="c7d0b-121">Связанные статьи</span><span class="sxs-lookup"><span data-stu-id="c7d0b-121">Related articles</span></span>
* [<span data-ttu-id="c7d0b-122">Вопросы безопасности и конфиденциальности Cloud App Discovery</span><span class="sxs-lookup"><span data-stu-id="c7d0b-122">Cloud App Discovery Security and Privacy Considerations</span></span>](active-directory-cloudappdiscovery-security-and-privacy-considerations.md)  
* [<span data-ttu-id="c7d0b-123">Руководство по развертыванию групповой политики Cloud App Discovery</span><span class="sxs-lookup"><span data-stu-id="c7d0b-123">Cloud App Discovery Group Policy Deployment Guide</span></span>](http://social.technet.microsoft.com/wiki/contents/articles/30965.cloud-app-discovery-group-policy-deployment-guide.aspx)
* [<span data-ttu-id="c7d0b-124">Руководство по развертыванию центра Cloud App Discovery</span><span class="sxs-lookup"><span data-stu-id="c7d0b-124">Cloud App Discovery System Center Deployment Guide</span></span>](http://social.technet.microsoft.com/wiki/contents/articles/30968.cloud-app-discovery-system-center-deployment-guide.aspx)
* [<span data-ttu-id="c7d0b-125">Параметры реестра для настройки Cloud App Discovery для прокси-серверов с пользовательскими портами</span><span class="sxs-lookup"><span data-stu-id="c7d0b-125">Cloud App Discovery Registry Settings for Proxy Servers with Custom Ports</span></span>](active-directory-cloudappdiscovery-registry-settings-for-proxy-services.md)
* [<span data-ttu-id="c7d0b-126">Журнал изменений агента Cloud App Discovery </span><span class="sxs-lookup"><span data-stu-id="c7d0b-126">Cloud App Discovery Agent Changelog </span></span>](http://social.technet.microsoft.com/wiki/contents/articles/24616.cloud-app-discovery-agent-changelog.aspx)
* [<span data-ttu-id="c7d0b-127">Часто задаваемые вопросы по Cloud App Discovery</span><span class="sxs-lookup"><span data-stu-id="c7d0b-127">Cloud App Discovery Frequently Asked Questions</span></span>](http://social.technet.microsoft.com/wiki/contents/articles/24037.cloud-app-discovery-frequently-asked-questions.aspx)
* [<span data-ttu-id="c7d0b-128">Указатель статьей по управлению приложениями в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c7d0b-128">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)

