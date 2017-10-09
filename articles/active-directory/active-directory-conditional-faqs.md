---
title: "aaaAzure условного доступа к Active Directory часто задаваемые вопросы | Документы Microsoft"
description: "Получите ответы toofrequently вопросы и ответы о условного доступа в Azure Active Directory."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 14f7fc83-f4bb-41bf-b6f1-a9bb97717c34
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: d23acbb01217d7e9717d1a43de1b46a929404118
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-conditional-access-faqs"></a><span data-ttu-id="a0988-103">Условный доступ к Azure Active Directory: часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="a0988-103">Azure Active Directory conditional access FAQs</span></span>

## <a name="which-applications-work-with-conditional-access-policies"></a><span data-ttu-id="a0988-104">Какие приложения работают с политиками условного доступа?</span><span class="sxs-lookup"><span data-stu-id="a0988-104">Which applications work with conditional access policies?</span></span>

<span data-ttu-id="a0988-105">Дополнительные сведения о приложениях, которые работают с политиками условного доступа, см. в статье [Приложения и браузеры, использующие правила условного доступа в Azure Active Directory](active-directory-conditional-access-supported-apps.md).</span><span class="sxs-lookup"><span data-stu-id="a0988-105">For information about applications that work with conditional access policies, see [Applications and browsers that use conditional access rules in Azure Active Directory](active-directory-conditional-access-supported-apps.md).</span></span>

## <a name="are-conditional-access-policies-enforced-for-b2b-collaboration-and-guest-users"></a><span data-ttu-id="a0988-106">Являются ли политики условного доступа обязательными для службы совместной работы B2B и гостевых пользователей?</span><span class="sxs-lookup"><span data-stu-id="a0988-106">Are conditional access policies enforced for B2B collaboration and guest users?</span></span>

<span data-ttu-id="a0988-107">Политики применяются для пользователей службы совместной работы B2B.</span><span class="sxs-lookup"><span data-stu-id="a0988-107">Policies are enforced for business-to-business (B2B) collaboration users.</span></span> <span data-ttu-id="a0988-108">Однако в некоторых случаях пользователь может быть требованиям политики может toosatisfy hello.</span><span class="sxs-lookup"><span data-stu-id="a0988-108">However, in some cases, a user might not be able toosatisfy hello policy requirements.</span></span> <span data-ttu-id="a0988-109">Например, организация гостевого пользователя может не поддерживать многофакторную проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="a0988-109">For example, a guest user's organization might not support multi-factor authentication.</span></span> 



## <a name="does-a-sharepoint-online-policy-also-apply-tooonedrive-for-business"></a><span data-ttu-id="a0988-110">Политика SharePoint Online также применять tooOneDrive для бизнеса?</span><span class="sxs-lookup"><span data-stu-id="a0988-110">Does a SharePoint Online policy also apply tooOneDrive for Business?</span></span>

<span data-ttu-id="a0988-111">Да.</span><span class="sxs-lookup"><span data-stu-id="a0988-111">Yes.</span></span> <span data-ttu-id="a0988-112">Политика SharePoint Online также применяется tooOneDrive для бизнеса.</span><span class="sxs-lookup"><span data-stu-id="a0988-112">A SharePoint Online policy also applies tooOneDrive for Business.</span></span>


## <a name="why-cant-i-set-a-policy-on-client-apps-like-word-or-outlook"></a><span data-ttu-id="a0988-113">Почему не удается задать политику для клиентских приложений, таких как Word или Outlook?</span><span class="sxs-lookup"><span data-stu-id="a0988-113">Why can’t I set a policy on client apps, like Word or Outlook?</span></span>

<span data-ttu-id="a0988-114">Политика условного доступа устанавливает требования для доступа к службе.</span><span class="sxs-lookup"><span data-stu-id="a0988-114">A conditional access policy sets requirements for accessing a service.</span></span> <span data-ttu-id="a0988-115">Происходит при возникновении toothat службы проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="a0988-115">It's enforced when authentication toothat service occurs.</span></span> <span data-ttu-id="a0988-116">не задана политика Hello непосредственно в клиентском приложении.</span><span class="sxs-lookup"><span data-stu-id="a0988-116">hello policy is not set directly on a client application.</span></span> <span data-ttu-id="a0988-117">Вместо этого она применяется, когда клиент вызывает службу.</span><span class="sxs-lookup"><span data-stu-id="a0988-117">Instead, it is applied when a client calls a service.</span></span> <span data-ttu-id="a0988-118">Например установленная на сервере SharePoint политика применяется tooclients вызов SharePoint.</span><span class="sxs-lookup"><span data-stu-id="a0988-118">For example, a policy set on SharePoint applies tooclients calling SharePoint.</span></span> <span data-ttu-id="a0988-119">Установленная на сервере Exchange политика применяется tooOutlook.</span><span class="sxs-lookup"><span data-stu-id="a0988-119">A policy set on Exchange applies tooOutlook.</span></span>

## <a name="does-a-conditional-access-policy-apply-tooservice-accounts"></a><span data-ttu-id="a0988-120">Политики условного доступа применяется tooservice учетные записи?</span><span class="sxs-lookup"><span data-stu-id="a0988-120">Does a conditional access policy apply tooservice accounts?</span></span>

<span data-ttu-id="a0988-121">Политики условного доступа применяются tooall учетных записей пользователей.</span><span class="sxs-lookup"><span data-stu-id="a0988-121">Conditional access policies apply tooall user accounts.</span></span> <span data-ttu-id="a0988-122">Это относится и к учетным записям пользователей, которые используются как учетные записи служб.</span><span class="sxs-lookup"><span data-stu-id="a0988-122">This includes user accounts that are used as service accounts.</span></span> <span data-ttu-id="a0988-123">Часто учетная запись службы, которая выполняется автоматически не может удовлетворить требования hello политики условного доступа.</span><span class="sxs-lookup"><span data-stu-id="a0988-123">Often, a service account that runs unattended can't satisfy hello requirements of a conditional access policy.</span></span> <span data-ttu-id="a0988-124">Например, может потребоваться многофакторная проверка подлинности.</span><span class="sxs-lookup"><span data-stu-id="a0988-124">For example, multi-factor authentication might be required.</span></span> <span data-ttu-id="a0988-125">Учетные записи служб можно исключить из политики с помощью параметров управления политикой условного доступа.</span><span class="sxs-lookup"><span data-stu-id="a0988-125">Service accounts can be excluded from a policy by using conditional access policy management settings.</span></span> 

## <a name="are-graph-apis-available-for-configuring-conditional-access-policies"></a><span data-ttu-id="a0988-126">Доступны ли API Graph для настройки политики условного доступа?</span><span class="sxs-lookup"><span data-stu-id="a0988-126">Are Graph APIs available for configuring conditional access policies?</span></span>

<span data-ttu-id="a0988-127">В настоящее время нет.</span><span class="sxs-lookup"><span data-stu-id="a0988-127">Currently, no.</span></span> 

## <a name="what-is-hello-default-exclusion-policy-for-unsupported-device-platforms"></a><span data-ttu-id="a0988-128">Какова политика исключения по умолчанию hello для неподдерживаемых платформ?</span><span class="sxs-lookup"><span data-stu-id="a0988-128">What is hello default exclusion policy for unsupported device platforms?</span></span>

<span data-ttu-id="a0988-129">В настоящее время политики условного доступа применяются избирательно к пользователям устройств iOS и Android.</span><span class="sxs-lookup"><span data-stu-id="a0988-129">Currently, conditional access policies are selectively enforced on users of iOS and Android devices.</span></span> <span data-ttu-id="a0988-130">На других платформах по умолчанию не влияет на приложения hello политику условного доступа для устройств iOS и Android.</span><span class="sxs-lookup"><span data-stu-id="a0988-130">Applications on other device platforms are, by default, not affected by hello conditional access policy for iOS and Android devices.</span></span> <span data-ttu-id="a0988-131">Администратор клиента можно выбрать toousers toooverride hello глобальной политики toodisallow доступ на платформах, которые не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="a0988-131">A tenant admin can choose toooverride hello global policy toodisallow access toousers on platforms that are not supported.</span></span>


## <a name="how-do-conditional-access-policies-work-for-microsoft-teams"></a><span data-ttu-id="a0988-132">Как работают политики условного доступа для Microsoft Teams?</span><span class="sxs-lookup"><span data-stu-id="a0988-132">How do conditional access policies work for Microsoft Teams?</span></span>  

<span data-ttu-id="a0988-133">Microsoft Teams в значительной степени зависит от Exchange Online и SharePoint Online в основных сценариях производительности, таких как собрания, календари и совместное использование файлов.</span><span class="sxs-lookup"><span data-stu-id="a0988-133">Microsoft Teams relies heavily on Exchange Online and SharePoint Online for core productivity scenarios, like meetings, calendars, and file sharing.</span></span> <span data-ttu-id="a0988-134">Политики условного доступа, заданные для этих облачных приложений применяются tooMicrosoft команды при входе в систему пользователя.</span><span class="sxs-lookup"><span data-stu-id="a0988-134">Conditional access policies that are set for these cloud apps apply tooMicrosoft Teams when a user signs in.</span></span>

<span data-ttu-id="a0988-135">Microsoft Teams также поддерживается отдельно в качестве облачного приложения в политиках условного доступа Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a0988-135">Microsoft Teams also is supported separately as a cloud app in Azure Active Directory conditional access policies.</span></span> <span data-ttu-id="a0988-136">Политики центр сертификатов, установленных для облачного приложения применяются tooMicrosoft команды при входе в систему пользователя.</span><span class="sxs-lookup"><span data-stu-id="a0988-136">Certificate authority policies that are set for a cloud app apply tooMicrosoft Teams when a user signs in.</span></span>

<span data-ttu-id="a0988-137">Клиенты рабочего стола Microsoft Teams для Windows и Mac поддерживают современные методы проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="a0988-137">Microsoft Teams desktop clients for Windows and Mac support modern authentication.</span></span> <span data-ttu-id="a0988-138">Современная проверка подлинности использует вход на основе hello Azure Active Directory Authentication библиотеки (ADAL) tooMicrosoft Office клиентских приложений на платформах.</span><span class="sxs-lookup"><span data-stu-id="a0988-138">Modern authentication brings sign-in based on hello Azure Active Directory Authentication Library (ADAL) tooMicrosoft Office client applications across platforms.</span></span> 
