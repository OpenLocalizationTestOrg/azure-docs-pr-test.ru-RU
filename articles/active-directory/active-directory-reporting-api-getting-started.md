---
title: "Начало работы с API отчетов Azure AD на классическом портале Azure AD | Документация Майкрософт"
description: "Как начать работу с API отчетов Azure Active Directory"
services: active-directory
documentationcenter: 
author: dhanyahk
manager: femila
editor: 
ms.assetid: 8813b911-a4ec-4234-8474-2eef9afea11e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/18/2017
ms.author: dhanyahk;markvi
ms.openlocfilehash: 5e98b660fe19bb8abebf1c3b996b6295a6c4e728
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-the-azure-active-directory-reporting-api-on-the-azure-ad-classic-portal"></a><span data-ttu-id="17b48-103">Начало работы с API отчетов Azure Active Directory на классическом портале Azure AD</span><span class="sxs-lookup"><span data-stu-id="17b48-103">Getting started with the Azure Active Directory reporting API on the Azure AD classic portal</span></span>
<span data-ttu-id="17b48-104">*Эта тема входит в состав [руководства по отчетам Azure Active Directory](active-directory-reporting-guide.md).*</span><span class="sxs-lookup"><span data-stu-id="17b48-104">*This topic is part of the [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).*</span></span>

<span data-ttu-id="17b48-105">Azure Active Directory предоставляет разнообразные отчеты.</span><span class="sxs-lookup"><span data-stu-id="17b48-105">Azure Active Directory provides you with a variety of reports.</span></span> <span data-ttu-id="17b48-106">Данные этих отчетов могут быть очень полезными для приложений, например систем SIEM, а также инструментов аудита и бизнес-аналитики.</span><span class="sxs-lookup"><span data-stu-id="17b48-106">The data of these reports can be very useful to your applications, such as SIEM systems, audit, and business intelligence tools.</span></span> <span data-ttu-id="17b48-107">Интерфейсы API отчетов Azure AD предоставляют программный доступ к данным с помощью набора интерфейсов API на базе REST.</span><span class="sxs-lookup"><span data-stu-id="17b48-107">The Azure AD reporting APIs provide programmatic access to the data through a set of REST-based APIs.</span></span> <span data-ttu-id="17b48-108">Эти интерфейсы API можно вызвать, используя различные языки и инструменты программирования.</span><span class="sxs-lookup"><span data-stu-id="17b48-108">You can call these APIs from a variety of programming languages and tools.</span></span>

<span data-ttu-id="17b48-109">В этой статье содержатся сведения, необходимые для начала работы с интерфейсами API отчетов Azure AD.</span><span class="sxs-lookup"><span data-stu-id="17b48-109">This article provides you with the information you need to get started with the Azure AD reporting APIs.</span></span>
<span data-ttu-id="17b48-110">В следующем разделе представлены дополнительные сведения об использовании интерфейсов API аудита и входа.</span><span class="sxs-lookup"><span data-stu-id="17b48-110">In the next section, you find more details about using the audit and sign-in APIs.</span></span> <span data-ttu-id="17b48-111">Дополнительные сведения о других интерфейсах API см. в статье [Отчеты и события (предварительная версия)](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-reports-and-events-preview).</span><span class="sxs-lookup"><span data-stu-id="17b48-111">For all other APIs, see the [Azure AD reports and events(preview)](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-reports-and-events-preview) article.</span></span>

<span data-ttu-id="17b48-112">Чтобы задать вопросы, обговорить проблемы или предоставить отзыв, обратитесь в [службу поддержки по инструментам создания отчетов AAD](mailto:aadreportinghelp@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="17b48-112">For questions, issues or feedback, please contact [AAD Reporting Help](mailto:aadreportinghelp@microsoft.com).</span></span>

## <a name="learning-map"></a><span data-ttu-id="17b48-113">Карта обучения</span><span class="sxs-lookup"><span data-stu-id="17b48-113">Learning map</span></span>
1. <span data-ttu-id="17b48-114">**Подготовка.** Перед тестированием примеров API нужно выполнить [предварительные требования для доступа к API отчетов Azure AD](active-directory-reporting-api-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="17b48-114">**Prepare** - Before you can test your API samples, you need to complete the [prerequisites to access the Azure AD reporting API](active-directory-reporting-api-prerequisites.md).</span></span>
2. <span data-ttu-id="17b48-115">**Изучение.** Ознакомьтесь с интерфейсами API отчетов:</span><span class="sxs-lookup"><span data-stu-id="17b48-115">**Explore** - Get a first impression of the reporting APIs:</span></span>
   
   * [<span data-ttu-id="17b48-116">Использование примеров для API аудита</span><span class="sxs-lookup"><span data-stu-id="17b48-116">Using the samples for the audit API</span></span>](active-directory-reporting-api-audit-samples.md) 
   * [<span data-ttu-id="17b48-117">Использование примеров для API отчетов о действиях при входе</span><span class="sxs-lookup"><span data-stu-id="17b48-117">Using the samples for the sign-in activity report API</span></span>](active-directory-reporting-api-sign-in-activity-samples.md)
3. <span data-ttu-id="17b48-118">**Настройка.** Создайте свое решение:</span><span class="sxs-lookup"><span data-stu-id="17b48-118">**Customize** -  Create your own solution:</span></span> 
   
   * [<span data-ttu-id="17b48-119">Справочник по использованию API аудита</span><span class="sxs-lookup"><span data-stu-id="17b48-119">Using the audit API reference</span></span>](active-directory-reporting-api-audit-reference.md) 
   * [<span data-ttu-id="17b48-120">Справочник по использованию API отчетов о действиях при входе</span><span class="sxs-lookup"><span data-stu-id="17b48-120">Using the sign-in activity report API reference</span></span>](active-directory-reporting-api-sign-in-activity-reference.md)

## <a name="next-steps"></a><span data-ttu-id="17b48-121">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="17b48-121">Next Steps</span></span>
<span data-ttu-id="17b48-122">Если вы хотите просмотреть все доступные конечные точки API Graph Azure AD, перейдите по адресу [https://graph.windows.net/tenant-name/reports/$metadata?api-version=beta](https://graph.windows.net/tenant-name/reports/$metadata?api-version=beta).</span><span class="sxs-lookup"><span data-stu-id="17b48-122">If you are curious to see all of the available Azure AD Graph API endpoints by navigating to [https://graph.windows.net/tenant-name/reports/$metadata?api-version=beta](https://graph.windows.net/tenant-name/reports/$metadata?api-version=beta).</span></span>

