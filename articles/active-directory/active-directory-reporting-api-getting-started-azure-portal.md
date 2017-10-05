---
title: "Начало работы с API отчетов Azure AD | Документация Майкрософт"
description: "Как начать работу с API отчетов Azure Active Directory"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 8813b911-a4ec-4234-8474-2eef9afea11e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/18/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 9944cbd2b1b7c4acb18d37da1394c0bbc170f77d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="getting-started-with-the-azure-active-directory-reporting-api"></a><span data-ttu-id="bb8f3-103">Приступая к работе с API отчетов Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bb8f3-103">Getting started with the Azure Active Directory reporting API</span></span>

<span data-ttu-id="bb8f3-104">Azure Active Directory предоставляет разнообразные отчеты.</span><span class="sxs-lookup"><span data-stu-id="bb8f3-104">Azure Active Directory provides you with a variety of reports.</span></span> <span data-ttu-id="bb8f3-105">Данные этих отчетов могут быть очень полезными для приложений, например систем SIEM, а также инструментов аудита и бизнес-аналитики.</span><span class="sxs-lookup"><span data-stu-id="bb8f3-105">The data of these reports can be very useful to your applications, such as SIEM systems, audit, and business intelligence tools.</span></span> <span data-ttu-id="bb8f3-106">Интерфейсы API отчетов Azure AD предоставляют программный доступ к данным с помощью набора интерфейсов API на базе REST.</span><span class="sxs-lookup"><span data-stu-id="bb8f3-106">The Azure AD reporting APIs provide programmatic access to the data through a set of REST-based APIs.</span></span> <span data-ttu-id="bb8f3-107">Эти интерфейсы API можно вызвать, используя различные языки и инструменты программирования.</span><span class="sxs-lookup"><span data-stu-id="bb8f3-107">You can call these APIs from a variety of programming languages and tools.</span></span>

<span data-ttu-id="bb8f3-108">В этой статье содержатся сведения, необходимые для начала работы с интерфейсами API отчетов Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bb8f3-108">This article provides you with the information you need to get started with the Azure AD reporting APIs.</span></span>
<span data-ttu-id="bb8f3-109">В следующем разделе представлены дополнительные сведения об использовании интерфейсов API аудита и входа.</span><span class="sxs-lookup"><span data-stu-id="bb8f3-109">In the next section, you find more details about using the audit and sign-in APIs.</span></span> 

<span data-ttu-id="bb8f3-110">Ответы на вопросы см. в разделе [Часто задаваемые вопросы](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-reporting-faq).</span><span class="sxs-lookup"><span data-stu-id="bb8f3-110">For frequently asked questions,read our [FAQ](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-reporting-faq).</span></span> <span data-ttu-id="bb8f3-111">При возникновении проблем [создайте запрос в службу поддержки](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-troubleshooting-support-howto)</span><span class="sxs-lookup"><span data-stu-id="bb8f3-111">For issues, please [file a support ticket](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-troubleshooting-support-howto)</span></span>

## <a name="learning-map"></a><span data-ttu-id="bb8f3-112">Карта обучения</span><span class="sxs-lookup"><span data-stu-id="bb8f3-112">Learning map</span></span>
1. <span data-ttu-id="bb8f3-113">**Подготовка.** Перед тестированием примеров API нужно выполнить [предварительные требования для доступа к API отчетов Azure AD](active-directory-reporting-api-prerequisites-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="bb8f3-113">**Prepare** - Before you can test your API samples, you need to complete the [prerequisites to access the Azure AD reporting API](active-directory-reporting-api-prerequisites-azure-portal.md).</span></span>
2. <span data-ttu-id="bb8f3-114">**Изучение.** Ознакомьтесь с интерфейсами API отчетов:</span><span class="sxs-lookup"><span data-stu-id="bb8f3-114">**Explore** - Get a first impression of the reporting APIs:</span></span>
   
   * [<span data-ttu-id="bb8f3-115">Использование примеров для API аудита</span><span class="sxs-lookup"><span data-stu-id="bb8f3-115">Using the samples for the audit API</span></span>](active-directory-reporting-api-audit-samples.md) 
   * [<span data-ttu-id="bb8f3-116">Использование примеров для API отчетов о действиях при входе</span><span class="sxs-lookup"><span data-stu-id="bb8f3-116">Using the samples for the sign-in activity report API</span></span>](active-directory-reporting-api-sign-in-activity-samples.md)
3. <span data-ttu-id="bb8f3-117">**Настройка.** Создайте свое решение:</span><span class="sxs-lookup"><span data-stu-id="bb8f3-117">**Customize** -  Create your own solution:</span></span> 
   
   * [<span data-ttu-id="bb8f3-118">Справочник по использованию API аудита</span><span class="sxs-lookup"><span data-stu-id="bb8f3-118">Using the audit API reference</span></span>](active-directory-reporting-api-audit-reference.md) 
   * [<span data-ttu-id="bb8f3-119">Справочник по использованию API отчетов о действиях при входе</span><span class="sxs-lookup"><span data-stu-id="bb8f3-119">Using the sign-in activity report API reference</span></span>](active-directory-reporting-api-sign-in-activity-reference.md)

## <a name="next-steps"></a><span data-ttu-id="bb8f3-120">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="bb8f3-120">Next Steps</span></span>
<span data-ttu-id="bb8f3-121">Если вы хотите ознакомиться со всеми доступными конечными точками API Graph Azure AD, воспользуйтесь этой ссылкой: [https://graph.windows.net/tenant-name/activities/$metadata?api-version=beta](https://graph.windows.net/tenant-name/activities/$metadata?api-version=beta).</span><span class="sxs-lookup"><span data-stu-id="bb8f3-121">If you are curious to see all available Azure AD Graph API endpoints, use this link: [https://graph.windows.net/tenant-name/activities/$metadata?api-version=beta](https://graph.windows.net/tenant-name/activities/$metadata?api-version=beta).</span></span>

