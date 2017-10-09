---
title: "aaaGetting к работе с API отчетов hello Azure AD на классический портал Azure AD hello | Документы Microsoft"
description: "Как tooget работу с hello API отчетов Azure Active Directory"
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
ms.openlocfilehash: 52e22d442650731fc6ed28991fc65f9182af0540
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-hello-azure-active-directory-reporting-api-on-hello-azure-ad-classic-portal"></a><span data-ttu-id="4e992-103">Приступая к работе с Azure Active Directory reporting API на классический портал Azure AD hello "hello"</span><span class="sxs-lookup"><span data-stu-id="4e992-103">Getting started with hello Azure Active Directory reporting API on hello Azure AD classic portal</span></span>
<span data-ttu-id="4e992-104">*Этот раздел является частью hello [Azure Active Directory руководство по отчетам](active-directory-reporting-guide.md).*</span><span class="sxs-lookup"><span data-stu-id="4e992-104">*This topic is part of hello [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).*</span></span>

<span data-ttu-id="4e992-105">Azure Active Directory предоставляет разнообразные отчеты.</span><span class="sxs-lookup"><span data-stu-id="4e992-105">Azure Active Directory provides you with a variety of reports.</span></span> <span data-ttu-id="4e992-106">Hello данные этих отчетов могут быть очень полезным tooyour приложения, такие как системы SIEM, аудита и средства бизнес-аналитики.</span><span class="sxs-lookup"><span data-stu-id="4e992-106">hello data of these reports can be very useful tooyour applications, such as SIEM systems, audit, and business intelligence tools.</span></span> <span data-ttu-id="4e992-107">Hello Azure AD сообщивший об API обеспечивают программный доступ к данным toohello через набор API на основе REST.</span><span class="sxs-lookup"><span data-stu-id="4e992-107">hello Azure AD reporting APIs provide programmatic access toohello data through a set of REST-based APIs.</span></span> <span data-ttu-id="4e992-108">Эти интерфейсы API можно вызвать, используя различные языки и инструменты программирования.</span><span class="sxs-lookup"><span data-stu-id="4e992-108">You can call these APIs from a variety of programming languages and tools.</span></span>

<span data-ttu-id="4e992-109">В этой статье приводятся hello информацию, необходимую tooget работы с отчетами hello Azure AD API-интерфейсы.</span><span class="sxs-lookup"><span data-stu-id="4e992-109">This article provides you with hello information you need tooget started with hello Azure AD reporting APIs.</span></span>
<span data-ttu-id="4e992-110">В следующем разделе hello можно найти дополнительные сведения об использовании hello аудита и входа в API-интерфейсы.</span><span class="sxs-lookup"><span data-stu-id="4e992-110">In hello next section, you find more details about using hello audit and sign-in APIs.</span></span> <span data-ttu-id="4e992-111">Все другие интерфейсы API в разделе hello [отчетов Azure AD и events(preview)](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-reports-and-events-preview) статьи.</span><span class="sxs-lookup"><span data-stu-id="4e992-111">For all other APIs, see hello [Azure AD reports and events(preview)](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-reports-and-events-preview) article.</span></span>

<span data-ttu-id="4e992-112">Чтобы задать вопросы, обговорить проблемы или предоставить отзыв, обратитесь в [службу поддержки по инструментам создания отчетов AAD](mailto:aadreportinghelp@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="4e992-112">For questions, issues or feedback, please contact [AAD Reporting Help](mailto:aadreportinghelp@microsoft.com).</span></span>

## <a name="learning-map"></a><span data-ttu-id="4e992-113">Карта обучения</span><span class="sxs-lookup"><span data-stu-id="4e992-113">Learning map</span></span>
1. <span data-ttu-id="4e992-114">**Подготовка** -перед тестированием ваших примеров API необходимо toocomplete hello [API отчетов hello Azure AD tooaccess необходимых компонентов](active-directory-reporting-api-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="4e992-114">**Prepare** - Before you can test your API samples, you need toocomplete hello [prerequisites tooaccess hello Azure AD reporting API](active-directory-reporting-api-prerequisites.md).</span></span>
2. <span data-ttu-id="4e992-115">**Просмотр** -получить первое впечатление hello reporting API-интерфейсы:</span><span class="sxs-lookup"><span data-stu-id="4e992-115">**Explore** - Get a first impression of hello reporting APIs:</span></span>
   
   * [<span data-ttu-id="4e992-116">С помощью hello образцы для аудита hello API</span><span class="sxs-lookup"><span data-stu-id="4e992-116">Using hello samples for hello audit API</span></span>](active-directory-reporting-api-audit-samples.md) 
   * [<span data-ttu-id="4e992-117">С помощью hello образцы для API отчетов hello действия при входе</span><span class="sxs-lookup"><span data-stu-id="4e992-117">Using hello samples for hello sign-in activity report API</span></span>](active-directory-reporting-api-sign-in-activity-samples.md)
3. <span data-ttu-id="4e992-118">**Настройка.** Создайте свое решение:</span><span class="sxs-lookup"><span data-stu-id="4e992-118">**Customize** -  Create your own solution:</span></span> 
   
   * [<span data-ttu-id="4e992-119">Справочник по API hello аудита с помощью</span><span class="sxs-lookup"><span data-stu-id="4e992-119">Using hello audit API reference</span></span>](active-directory-reporting-api-audit-reference.md) 
   * [<span data-ttu-id="4e992-120">С помощью отчетов действия при входе hello Справочник</span><span class="sxs-lookup"><span data-stu-id="4e992-120">Using hello sign-in activity report API reference</span></span>](active-directory-reporting-api-sign-in-activity-reference.md)

## <a name="next-steps"></a><span data-ttu-id="4e992-121">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4e992-121">Next Steps</span></span>
<span data-ttu-id="4e992-122">Если вы хотите toosee все hello доступные конечные точки API Azure AD Graph, перейдя по слишком[https://graph.windows.net/tenant-name/reports/$ метаданных? api-version = beta](https://graph.windows.net/tenant-name/reports/$metadata?api-version=beta).</span><span class="sxs-lookup"><span data-stu-id="4e992-122">If you are curious toosee all of hello available Azure AD Graph API endpoints by navigating too[https://graph.windows.net/tenant-name/reports/$metadata?api-version=beta](https://graph.windows.net/tenant-name/reports/$metadata?api-version=beta).</span></span>

