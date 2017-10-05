---
title: "Условный доступ к Azure Active Directory: часто задаваемые вопросы | Документация Майкрософт"
description: "Ознакомьтесь с ответами на часто задаваемые вопросы об условном доступе к Azure Active Directory."
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
ms.openlocfilehash: e9a5af41b08b593e4d97475f29da4e5fe8df7042
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-conditional-access-faqs"></a><span data-ttu-id="0547a-103">Условный доступ к Azure Active Directory: часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="0547a-103">Azure Active Directory conditional access FAQs</span></span>

## <a name="which-applications-work-with-conditional-access-policies"></a><span data-ttu-id="0547a-104">Какие приложения работают с политиками условного доступа?</span><span class="sxs-lookup"><span data-stu-id="0547a-104">Which applications work with conditional access policies?</span></span>

<span data-ttu-id="0547a-105">Дополнительные сведения о приложениях, которые работают с политиками условного доступа, см. в статье [Приложения и браузеры, использующие правила условного доступа в Azure Active Directory](active-directory-conditional-access-supported-apps.md).</span><span class="sxs-lookup"><span data-stu-id="0547a-105">For information about applications that work with conditional access policies, see [Applications and browsers that use conditional access rules in Azure Active Directory](active-directory-conditional-access-supported-apps.md).</span></span>

## <a name="are-conditional-access-policies-enforced-for-b2b-collaboration-and-guest-users"></a><span data-ttu-id="0547a-106">Являются ли политики условного доступа обязательными для службы совместной работы B2B и гостевых пользователей?</span><span class="sxs-lookup"><span data-stu-id="0547a-106">Are conditional access policies enforced for B2B collaboration and guest users?</span></span>

<span data-ttu-id="0547a-107">Политики применяются для пользователей службы совместной работы B2B.</span><span class="sxs-lookup"><span data-stu-id="0547a-107">Policies are enforced for business-to-business (B2B) collaboration users.</span></span> <span data-ttu-id="0547a-108">Однако в некоторых случаях пользователь может не иметь возможности соответствовать требованиям политики.</span><span class="sxs-lookup"><span data-stu-id="0547a-108">However, in some cases, a user might not be able to satisfy the policy requirements.</span></span> <span data-ttu-id="0547a-109">Например, организация гостевого пользователя может не поддерживать многофакторную проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="0547a-109">For example, a guest user's organization might not support multi-factor authentication.</span></span> 



## <a name="does-a-sharepoint-online-policy-also-apply-to-onedrive-for-business"></a><span data-ttu-id="0547a-110">Распространяется ли политика SharePoint Online на OneDrive для бизнеса?</span><span class="sxs-lookup"><span data-stu-id="0547a-110">Does a SharePoint Online policy also apply to OneDrive for Business?</span></span>

<span data-ttu-id="0547a-111">Да.</span><span class="sxs-lookup"><span data-stu-id="0547a-111">Yes.</span></span> <span data-ttu-id="0547a-112">Политика SharePoint Online также распространяется на OneDrive для бизнеса.</span><span class="sxs-lookup"><span data-stu-id="0547a-112">A SharePoint Online policy also applies to OneDrive for Business.</span></span>


## <a name="why-cant-i-set-a-policy-on-client-apps-like-word-or-outlook"></a><span data-ttu-id="0547a-113">Почему не удается задать политику для клиентских приложений, таких как Word или Outlook?</span><span class="sxs-lookup"><span data-stu-id="0547a-113">Why can’t I set a policy on client apps, like Word or Outlook?</span></span>

<span data-ttu-id="0547a-114">Политика условного доступа устанавливает требования для доступа к службе.</span><span class="sxs-lookup"><span data-stu-id="0547a-114">A conditional access policy sets requirements for accessing a service.</span></span> <span data-ttu-id="0547a-115">Она применяется, когда происходит проверка подлинности для этой службы.</span><span class="sxs-lookup"><span data-stu-id="0547a-115">It's enforced when authentication to that service occurs.</span></span> <span data-ttu-id="0547a-116">Политика не устанавливается напрямую в клиентском приложении.</span><span class="sxs-lookup"><span data-stu-id="0547a-116">The policy is not set directly on a client application.</span></span> <span data-ttu-id="0547a-117">Вместо этого она применяется, когда клиент вызывает службу.</span><span class="sxs-lookup"><span data-stu-id="0547a-117">Instead, it is applied when a client calls a service.</span></span> <span data-ttu-id="0547a-118">Например, политика, заданная в SharePoint, применяется к клиентам, вызывающим SharePoint.</span><span class="sxs-lookup"><span data-stu-id="0547a-118">For example, a policy set on SharePoint applies to clients calling SharePoint.</span></span> <span data-ttu-id="0547a-119">Политика, заданная в Exchange, применяется к Outlook.</span><span class="sxs-lookup"><span data-stu-id="0547a-119">A policy set on Exchange applies to Outlook.</span></span>

## <a name="does-a-conditional-access-policy-apply-to-service-accounts"></a><span data-ttu-id="0547a-120">Распространяется ли политика условного доступа на учетные записи служб?</span><span class="sxs-lookup"><span data-stu-id="0547a-120">Does a conditional access policy apply to service accounts?</span></span>

<span data-ttu-id="0547a-121">Политика условного доступа распространяется на все учетные записи пользователей.</span><span class="sxs-lookup"><span data-stu-id="0547a-121">Conditional access policies apply to all user accounts.</span></span> <span data-ttu-id="0547a-122">Это относится и к учетным записям пользователей, которые используются как учетные записи служб.</span><span class="sxs-lookup"><span data-stu-id="0547a-122">This includes user accounts that are used as service accounts.</span></span> <span data-ttu-id="0547a-123">Часто учетная запись службы, выполняемая автоматически, не может соответствовать требованиям политики условного доступа.</span><span class="sxs-lookup"><span data-stu-id="0547a-123">Often, a service account that runs unattended can't satisfy the requirements of a conditional access policy.</span></span> <span data-ttu-id="0547a-124">Например, может потребоваться многофакторная проверка подлинности.</span><span class="sxs-lookup"><span data-stu-id="0547a-124">For example, multi-factor authentication might be required.</span></span> <span data-ttu-id="0547a-125">Учетные записи служб можно исключить из политики с помощью параметров управления политикой условного доступа.</span><span class="sxs-lookup"><span data-stu-id="0547a-125">Service accounts can be excluded from a policy by using conditional access policy management settings.</span></span> 

## <a name="are-graph-apis-available-for-configuring-conditional-access-policies"></a><span data-ttu-id="0547a-126">Доступны ли API Graph для настройки политики условного доступа?</span><span class="sxs-lookup"><span data-stu-id="0547a-126">Are Graph APIs available for configuring conditional access policies?</span></span>

<span data-ttu-id="0547a-127">В настоящее время нет.</span><span class="sxs-lookup"><span data-stu-id="0547a-127">Currently, no.</span></span> 

## <a name="what-is-the-default-exclusion-policy-for-unsupported-device-platforms"></a><span data-ttu-id="0547a-128">Какова политика исключений по умолчанию для не поддерживаемых платформ?</span><span class="sxs-lookup"><span data-stu-id="0547a-128">What is the default exclusion policy for unsupported device platforms?</span></span>

<span data-ttu-id="0547a-129">В настоящее время политики условного доступа применяются избирательно к пользователям устройств iOS и Android.</span><span class="sxs-lookup"><span data-stu-id="0547a-129">Currently, conditional access policies are selectively enforced on users of iOS and Android devices.</span></span> <span data-ttu-id="0547a-130">На приложения на других платформах эти политики по умолчанию не влияют.</span><span class="sxs-lookup"><span data-stu-id="0547a-130">Applications on other device platforms are, by default, not affected by the conditional access policy for iOS and Android devices.</span></span> <span data-ttu-id="0547a-131">Администратор клиента может переопределить глобальную политику, чтобы запретить доступ пользователям на платформах, которые не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="0547a-131">A tenant admin can choose to override the global policy to disallow access to users on platforms that are not supported.</span></span>


## <a name="how-do-conditional-access-policies-work-for-microsoft-teams"></a><span data-ttu-id="0547a-132">Как работают политики условного доступа для Microsoft Teams?</span><span class="sxs-lookup"><span data-stu-id="0547a-132">How do conditional access policies work for Microsoft Teams?</span></span>  

<span data-ttu-id="0547a-133">Microsoft Teams в значительной степени зависит от Exchange Online и SharePoint Online в основных сценариях производительности, таких как собрания, календари и совместное использование файлов.</span><span class="sxs-lookup"><span data-stu-id="0547a-133">Microsoft Teams relies heavily on Exchange Online and SharePoint Online for core productivity scenarios, like meetings, calendars, and file sharing.</span></span> <span data-ttu-id="0547a-134">Политики условного доступа, заданные для этих облачных приложений, применяются к Microsoft Teams при входе в систему пользователя.</span><span class="sxs-lookup"><span data-stu-id="0547a-134">Conditional access policies that are set for these cloud apps apply to Microsoft Teams when a user signs in.</span></span>

<span data-ttu-id="0547a-135">Microsoft Teams также поддерживается отдельно в качестве облачного приложения в политиках условного доступа Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0547a-135">Microsoft Teams also is supported separately as a cloud app in Azure Active Directory conditional access policies.</span></span> <span data-ttu-id="0547a-136">Политики центра сертификации, которые установлены для облачного приложения, применяются к Microsoft Teams при входе в систему пользователя.</span><span class="sxs-lookup"><span data-stu-id="0547a-136">Certificate authority policies that are set for a cloud app apply to Microsoft Teams when a user signs in.</span></span>

<span data-ttu-id="0547a-137">Клиенты рабочего стола Microsoft Teams для Windows и Mac поддерживают современные методы проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="0547a-137">Microsoft Teams desktop clients for Windows and Mac support modern authentication.</span></span> <span data-ttu-id="0547a-138">Современные методы проверки подлинности используют вход на основе библиотеки проверки подлинности Active Directory (ADAL) для клиентских приложений Microsoft Office на всех платформах.</span><span class="sxs-lookup"><span data-stu-id="0547a-138">Modern authentication brings sign-in based on the Azure Active Directory Authentication Library (ADAL) to Microsoft Office client applications across platforms.</span></span> 