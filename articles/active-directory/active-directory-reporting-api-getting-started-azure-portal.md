---
title: "aaaGetting к работе с API отчетов Azure AD hello | Документы Microsoft"
description: "Как tooget работу с hello API отчетов Azure Active Directory"
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
ms.openlocfilehash: bb7d72ba445daa367d7502889c38a605a16f26d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-hello-azure-active-directory-reporting-api"></a><span data-ttu-id="e6d06-103">Приступая к работе с API отчетов Azure Active Directory "hello"</span><span class="sxs-lookup"><span data-stu-id="e6d06-103">Getting started with hello Azure Active Directory reporting API</span></span>

<span data-ttu-id="e6d06-104">Azure Active Directory предоставляет разнообразные отчеты.</span><span class="sxs-lookup"><span data-stu-id="e6d06-104">Azure Active Directory provides you with a variety of reports.</span></span> <span data-ttu-id="e6d06-105">Hello данные этих отчетов могут быть очень полезным tooyour приложения, такие как системы SIEM, аудита и средства бизнес-аналитики.</span><span class="sxs-lookup"><span data-stu-id="e6d06-105">hello data of these reports can be very useful tooyour applications, such as SIEM systems, audit, and business intelligence tools.</span></span> <span data-ttu-id="e6d06-106">Hello Azure AD сообщивший об API обеспечивают программный доступ к данным toohello через набор API на основе REST.</span><span class="sxs-lookup"><span data-stu-id="e6d06-106">hello Azure AD reporting APIs provide programmatic access toohello data through a set of REST-based APIs.</span></span> <span data-ttu-id="e6d06-107">Эти интерфейсы API можно вызвать, используя различные языки и инструменты программирования.</span><span class="sxs-lookup"><span data-stu-id="e6d06-107">You can call these APIs from a variety of programming languages and tools.</span></span>

<span data-ttu-id="e6d06-108">В этой статье приводятся hello информацию, необходимую tooget работы с отчетами hello Azure AD API-интерфейсы.</span><span class="sxs-lookup"><span data-stu-id="e6d06-108">This article provides you with hello information you need tooget started with hello Azure AD reporting APIs.</span></span>
<span data-ttu-id="e6d06-109">В следующем разделе hello можно найти дополнительные сведения об использовании hello аудита и входа в API-интерфейсы.</span><span class="sxs-lookup"><span data-stu-id="e6d06-109">In hello next section, you find more details about using hello audit and sign-in APIs.</span></span> 

<span data-ttu-id="e6d06-110">Ответы на вопросы см. в разделе [Часто задаваемые вопросы](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-reporting-faq).</span><span class="sxs-lookup"><span data-stu-id="e6d06-110">For frequently asked questions,read our [FAQ](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-reporting-faq).</span></span> <span data-ttu-id="e6d06-111">При возникновении проблем [создайте запрос в службу поддержки](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-troubleshooting-support-howto)</span><span class="sxs-lookup"><span data-stu-id="e6d06-111">For issues, please [file a support ticket](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-troubleshooting-support-howto)</span></span>

## <a name="learning-map"></a><span data-ttu-id="e6d06-112">Карта обучения</span><span class="sxs-lookup"><span data-stu-id="e6d06-112">Learning map</span></span>
1. <span data-ttu-id="e6d06-113">**Подготовка** -перед тестированием ваших примеров API необходимо toocomplete hello [API отчетов hello Azure AD tooaccess необходимых компонентов](active-directory-reporting-api-prerequisites-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e6d06-113">**Prepare** - Before you can test your API samples, you need toocomplete hello [prerequisites tooaccess hello Azure AD reporting API](active-directory-reporting-api-prerequisites-azure-portal.md).</span></span>
2. <span data-ttu-id="e6d06-114">**Просмотр** -получить первое впечатление hello reporting API-интерфейсы:</span><span class="sxs-lookup"><span data-stu-id="e6d06-114">**Explore** - Get a first impression of hello reporting APIs:</span></span>
   
   * [<span data-ttu-id="e6d06-115">С помощью hello образцы для аудита hello API</span><span class="sxs-lookup"><span data-stu-id="e6d06-115">Using hello samples for hello audit API</span></span>](active-directory-reporting-api-audit-samples.md) 
   * [<span data-ttu-id="e6d06-116">С помощью hello образцы для API отчетов hello действия при входе</span><span class="sxs-lookup"><span data-stu-id="e6d06-116">Using hello samples for hello sign-in activity report API</span></span>](active-directory-reporting-api-sign-in-activity-samples.md)
3. <span data-ttu-id="e6d06-117">**Настройка.** Создайте свое решение:</span><span class="sxs-lookup"><span data-stu-id="e6d06-117">**Customize** -  Create your own solution:</span></span> 
   
   * [<span data-ttu-id="e6d06-118">Справочник по API hello аудита с помощью</span><span class="sxs-lookup"><span data-stu-id="e6d06-118">Using hello audit API reference</span></span>](active-directory-reporting-api-audit-reference.md) 
   * [<span data-ttu-id="e6d06-119">С помощью отчетов действия при входе hello Справочник</span><span class="sxs-lookup"><span data-stu-id="e6d06-119">Using hello sign-in activity report API reference</span></span>](active-directory-reporting-api-sign-in-activity-reference.md)

## <a name="next-steps"></a><span data-ttu-id="e6d06-120">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e6d06-120">Next Steps</span></span>
<span data-ttu-id="e6d06-121">Если вы хотите toosee все доступные API Azure AD Graph конечные точки, используйте эту ссылку: [https://graph.windows.net/tenant-name/activities/$ метаданных? api-version = beta](https://graph.windows.net/tenant-name/activities/$metadata?api-version=beta).</span><span class="sxs-lookup"><span data-stu-id="e6d06-121">If you are curious toosee all available Azure AD Graph API endpoints, use this link: [https://graph.windows.net/tenant-name/activities/$metadata?api-version=beta](https://graph.windows.net/tenant-name/activities/$metadata?api-version=beta).</span></span>

