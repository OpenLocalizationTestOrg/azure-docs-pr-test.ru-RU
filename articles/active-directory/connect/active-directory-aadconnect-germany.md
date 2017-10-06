---
title: "aaaAzure AD Connect в Германии облака Майкрософт"
description: "Azure AD Connect интегрирует локальные каталоги с Azure Active Directory. Это позволяет tooprovide общего удостоверения для приложений Office 365, Azure и SaaS интегрированы с Azure AD."
keywords: "Введение tooAzure AD Connect, общие сведения о Azure AD Connect, что такое Azure AD Connect установки active directory, Германии, черный леса"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 2bcb0caf-5d97-46cb-8c32-bda66cc22dad
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: f32194fa6c365614f68e5d1ddcf0dac44d223292
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-in-microsoft-cloud-germany---public-preview"></a><span data-ttu-id="dea43-105">Общедоступная предварительная версия Azure AD Connect в Microsoft Cloud для Германии</span><span class="sxs-lookup"><span data-stu-id="dea43-105">Azure AD Connect in Microsoft Cloud Germany - Public Preview</span></span>
## <a name="introduction"></a><span data-ttu-id="dea43-106">Введение</span><span class="sxs-lookup"><span data-stu-id="dea43-106">Introduction</span></span>
<span data-ttu-id="dea43-107">Azure AD Connect обеспечивает синхронизацию локальных каталогов Active Directory с каталогами Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="dea43-107">Azure AD Connect provides synchronization between your on-premises Active Directory and Azure Active Directory.</span></span>
<span data-ttu-id="dea43-108">В настоящее время многие сценарии hello в [Германия Microsoft Cloud](https://www.microsoft.com/de-de/cloud/deutschland/default.aspx) должна быть выполнена путем оператор hello.</span><span class="sxs-lookup"><span data-stu-id="dea43-108">Currently, many of hello scenarios in [Microsoft Cloud Germany](https://www.microsoft.com/de-de/cloud/deutschland/default.aspx) must be done by hello operator.</span></span> <span data-ttu-id="dea43-109">При использовании Microsoft Cloud Германии, необходимо помнить о следующих hello:</span><span class="sxs-lookup"><span data-stu-id="dea43-109">When using Microsoft Cloud Germany, you must be aware of hello following:</span></span>

* <span data-ttu-id="dea43-110">Hello следующие URL-адреса должен быть открыт на прокси-сервер для синхронизации toooccur успешно:</span><span class="sxs-lookup"><span data-stu-id="dea43-110">hello following URLs must be opened on a proxy server for synchronization toooccur successfully:</span></span>
  
  * <span data-ttu-id="dea43-111">*.microsoftonline.de</span><span class="sxs-lookup"><span data-stu-id="dea43-111">*.microsoftonline.de</span></span>
  * <span data-ttu-id="dea43-112">*.windows.net</span><span class="sxs-lookup"><span data-stu-id="dea43-112">*.windows.net</span></span>
  * * <span data-ttu-id="dea43-113">списки отзыва сертификатов.</span><span class="sxs-lookup"><span data-stu-id="dea43-113">Certificate Revocation Lists</span></span>
* <span data-ttu-id="dea43-114">Когда вы войдете в каталоге Azure AD tooyour, необходимо использовать учетную запись в домене onmicrosoft.de hello.</span><span class="sxs-lookup"><span data-stu-id="dea43-114">When you sign in tooyour Azure AD directory, you must use an account in hello onmicrosoft.de domain.</span></span>
* <span data-ttu-id="dea43-115">Привет, следующие функции будут недоступны.</span><span class="sxs-lookup"><span data-stu-id="dea43-115">hello following features are not available:</span></span>
  * <span data-ttu-id="dea43-116">Azure AD Connect Health</span><span class="sxs-lookup"><span data-stu-id="dea43-116">Azure AD Connect Health</span></span>
  * <span data-ttu-id="dea43-117">Автоматическое обновление</span><span class="sxs-lookup"><span data-stu-id="dea43-117">Automatic updates</span></span>
 
## <a name="download"></a><span data-ttu-id="dea43-118">Загрузить</span><span class="sxs-lookup"><span data-stu-id="dea43-118">Download</span></span>
<span data-ttu-id="dea43-119">Azure AD Connect можно загрузить из колонки hello Azure AD Connect на портале hello.</span><span class="sxs-lookup"><span data-stu-id="dea43-119">You can download Azure AD Connect from hello Azure AD Connect blade within hello portal.</span></span>  <span data-ttu-id="dea43-120">Используйте инструкции hello ниже toolocate hello Azure AD Connect колонку.</span><span class="sxs-lookup"><span data-stu-id="dea43-120">Use hello instructions below toolocate hello Azure AD Connect blade.</span></span>

### <a name="hello-azure-ad-connect-blade"></a><span data-ttu-id="dea43-121">Hello Azure AD Connect колонку</span><span class="sxs-lookup"><span data-stu-id="dea43-121">hello Azure AD Connect Blade</span></span>
<span data-ttu-id="dea43-122">После входа в портал Azure toohello hello следующие:</span><span class="sxs-lookup"><span data-stu-id="dea43-122">Once you have signed in toohello Azure portal, do hello following:</span></span>

1. <span data-ttu-id="dea43-123">Go tooBrowse</span><span class="sxs-lookup"><span data-stu-id="dea43-123">Go tooBrowse</span></span>
2. <span data-ttu-id="dea43-124">Выберите Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="dea43-124">Select Azure Active Directory</span></span>
3. <span data-ttu-id="dea43-125">Затем выберите Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="dea43-125">Then select Azure AD Connect</span></span>

<span data-ttu-id="dea43-126">Вы должны увидеть следующие hello.</span><span class="sxs-lookup"><span data-stu-id="dea43-126">You should see hello following:</span></span>

![Колонка Azure AD Connect](media/active-directory-aadconnect-germany/germany1.png)

<span data-ttu-id="dea43-128">Hello следующей таблице описаны возможности hello, показанные в колонке hello.</span><span class="sxs-lookup"><span data-stu-id="dea43-128">hello following table describes hello features shown in hello blade.</span></span>

| <span data-ttu-id="dea43-129">Название</span><span class="sxs-lookup"><span data-stu-id="dea43-129">Title</span></span> | <span data-ttu-id="dea43-130">Описание</span><span class="sxs-lookup"><span data-stu-id="dea43-130">Description</span></span> |
| --- | --- |
| <span data-ttu-id="dea43-131">Состояние синхронизации</span><span class="sxs-lookup"><span data-stu-id="dea43-131">SYNC STATUS</span></span> |<span data-ttu-id="dea43-132">Сообщает, включена ли синхронизация.</span><span class="sxs-lookup"><span data-stu-id="dea43-132">Let's you know whether synchronization is enabled or disabled.</span></span> |
| <span data-ttu-id="dea43-133">Последняя синхронизация</span><span class="sxs-lookup"><span data-stu-id="dea43-133">LAST SYNC</span></span> |<span data-ttu-id="dea43-134">Здравствуйте, время последней успешной синхронизации завершена.</span><span class="sxs-lookup"><span data-stu-id="dea43-134">hello last time a successful sync completed.</span></span> |
| <span data-ttu-id="dea43-135">Федеративные домены</span><span class="sxs-lookup"><span data-stu-id="dea43-135">FEDERATED DOMAINS</span></span> |<span data-ttu-id="dea43-136">Показывает количество hello федеративные домены, настроенные в данный момент.</span><span class="sxs-lookup"><span data-stu-id="dea43-136">Shows hello number of federated domains currently configured.</span></span> |

## <a name="installation"></a><span data-ttu-id="dea43-137">Установка</span><span class="sxs-lookup"><span data-stu-id="dea43-137">Installation</span></span>
<span data-ttu-id="dea43-138">tooinstall Azure AD Connect, вы можете использовать документацию hello [здесь](active-directory-aadconnect.md#install-azure-ad-connect).</span><span class="sxs-lookup"><span data-stu-id="dea43-138">tooinstall Azure AD Connect, you can use hello documentation [here](active-directory-aadconnect.md#install-azure-ad-connect).</span></span>

## <a name="advanced-features-and-additional-information"></a><span data-ttu-id="dea43-139">Дополнительные функции и дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="dea43-139">Advanced features and Additional Information</span></span>
<span data-ttu-id="dea43-140">Для начала ознакомьтесь со статьей [Интеграция локальных удостоверений с Azure Active Directory](active-directory-aadconnect.md), чтобы получить подробные сведения и рекомендации по пользовательским и расширенным настройкам.</span><span class="sxs-lookup"><span data-stu-id="dea43-140">For additional information and guidance on custom settings or advanced configurations, start with [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>  <span data-ttu-id="dea43-141">Эта страница содержит сведения и ссылки на руководство по tooadditional.</span><span class="sxs-lookup"><span data-stu-id="dea43-141">This page provides information and links tooadditional guidance.</span></span>

