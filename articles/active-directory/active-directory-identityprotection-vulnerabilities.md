---
title: "aaaVulnerabilities, обнаруживаемые службой защиты идентификации Active Directory Azure | Документы Microsoft"
description: "Обзор hello уязвимостей, обнаруживаемые службой защиты идентификации Active Directory Azure."
services: active-directory
keywords: "защита удостоверений Azure Active Directory, Cloud App Discovery, управление приложениями, безопасность, риск, уровень риска, уязвимость, политика безопасности"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 92233a5b-cb34-4d28-88cc-d5d29c0f3256
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 5e1cb401f8b566a180eb46e3420a090bcfc66767
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="vulnerabilities-detected-by-azure-active-directory-identity-protection"></a><span data-ttu-id="96381-104">Уязвимости, обнаруживаемые защитой идентификации Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="96381-104">Vulnerabilities detected by Azure Active Directory Identity Protection</span></span>
<span data-ttu-id="96381-105">Уязвимости — это слабые стороны среды, которыми могут воспользоваться злоумышленники.</span><span class="sxs-lookup"><span data-stu-id="96381-105">Vulnerabilities are weaknesses in your environment that can be exploited by an attacker.</span></span> <span data-ttu-id="96381-106">Корпорация Майкрософт рекомендует устранить эти уязвимости tooimprove hello уровня безопасности вашей организации и предотвратить их использование злоумышленниками.</span><span class="sxs-lookup"><span data-stu-id="96381-106">We recommend that you address these vulnerabilities tooimprove hello security posture of your organization, and prevent attackers from exploiting them.</span></span>


<span data-ttu-id="96381-107">![уязвимости](./media/active-directory-identityprotection-vulnerabilities/101.png "уязвимости")</span><span class="sxs-lookup"><span data-stu-id="96381-107">![vulnerabilities](./media/active-directory-identityprotection-vulnerabilities/101.png "vulnerabilities")</span></span>



<span data-ttu-id="96381-108">Hello следующие разделы предоставляют обзор hello уязвимостей, сообщаемые защиту учетных данных.</span><span class="sxs-lookup"><span data-stu-id="96381-108">hello following sections provide you with an overview of hello vulnerabilities reported by Identity Protection.</span></span>

## <a name="multi-factor-authentication-registration-not-configured"></a><span data-ttu-id="96381-109">Регистрация с многофакторной проверкой подлинности не настроена</span><span class="sxs-lookup"><span data-stu-id="96381-109">Multi-factor authentication registration not configured</span></span>
<span data-ttu-id="96381-110">Эта уязвимость позволяет контролировать развертывание hello многофакторной проверки подлинности Azure в вашей организации.</span><span class="sxs-lookup"><span data-stu-id="96381-110">This vulnerability helps you control hello deployment of Azure Multi-Factor Authentication in your organization.</span></span> 

<span data-ttu-id="96381-111">Azure Multi-factor authentication предоставляет второго уровня проверки подлинности, toouser.</span><span class="sxs-lookup"><span data-stu-id="96381-111">Azure multi-factor authentication provides a second layer of security toouser authentication.</span></span> <span data-ttu-id="96381-112">Помогает toodata защиты доступа и приложений удовлетворением спроса на простой процесс входа в систему.</span><span class="sxs-lookup"><span data-stu-id="96381-112">It helps safeguard access toodata and applications while meeting user demand for a simple sign-in process.</span></span> <span data-ttu-id="96381-113">Служба обеспечивает строгую проверку подлинности с помощью простых способов проверки — телефонного звонка, текстового сообщения, уведомления в мобильном приложении, кода подтверждения или OATH-токенов третьей стороны.</span><span class="sxs-lookup"><span data-stu-id="96381-113">It delivers strong authentication via a range of easy verification options—phone call, text message, or mobile app notification or verification code and 3rd party OATH tokens.</span></span>

<span data-ttu-id="96381-114">Мы рекомендуем настроить обязательную проверку Azure Multi-Factor Authentication при входе пользователей. Multi-Factor Authentication играет основную роль в основанных на рисках политиках условного доступа в защите идентификации.</span><span class="sxs-lookup"><span data-stu-id="96381-114">We recommend that you require Azure Multi-Factor Authentication for user sign-ins. Multi-factor authentication plays a key role in risk-based conditional access policies available through Identity Protection.</span></span>

<span data-ttu-id="96381-115">Дополнительные сведения см. в статье [Что такое Azure Multi-factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="96381-115">For more details, see [What is Azure Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md)</span></span>

## <a name="unmanaged-cloud-apps"></a><span data-ttu-id="96381-116">Неуправляемые облачные приложения</span><span class="sxs-lookup"><span data-stu-id="96381-116">Unmanaged cloud apps</span></span>
<span data-ttu-id="96381-117">Благодаря этой уязвимости можно выявить неуправляемые облачные приложения в организации.</span><span class="sxs-lookup"><span data-stu-id="96381-117">This vulnerability helps you identify unmanaged cloud apps in your organization.</span></span>

<span data-ttu-id="96381-118">На современных предприятиях ИТ-отделы часто не уведомлены о всех hello облачных приложений, пользователи в организации используется toodo свою работу.</span><span class="sxs-lookup"><span data-stu-id="96381-118">In modern enterprises, IT departments are often unaware of all hello cloud applications that users in their organization are using toodo their work.</span></span> <span data-ttu-id="96381-119">Это легко toosee, почему Администраторы бы обеспокоены toocorporate несанкционированного доступа к данным, возможными утечками данных и других угроз безопасности.</span><span class="sxs-lookup"><span data-stu-id="96381-119">It is easy toosee why administrators would have concerns about unauthorized access toocorporate data, possible data leakage and other security risks.</span></span> 

<span data-ttu-id="96381-120">Рекомендуется организации развертывание Cloud App Discovery toodiscover неуправляемого облачных приложений и toomanage эти приложения с помощью Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="96381-120">We recommend that your organization deploy Cloud App Discovery toodiscover unmanaged cloud applications, and toomanage these applications using Azure Active Directory.</span></span>

<span data-ttu-id="96381-121">Дополнительные сведения см. в статье [Поиск неуправляемых облачных приложений с помощью Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="96381-121">For more details, see [Finding unmanaged cloud applications with Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).</span></span>

## <a name="security-alerts-from-privileged-identity-management"></a><span data-ttu-id="96381-122">Оповещения системы безопасности в рамках управления привилегированными пользователями</span><span class="sxs-lookup"><span data-stu-id="96381-122">Security Alerts from Privileged Identity Management</span></span>
<span data-ttu-id="96381-123">Эта уязвимость способствует обнаружению и устранению оповещений о привилегированных удостоверениях в организации.</span><span class="sxs-lookup"><span data-stu-id="96381-123">This vulnerability helps you discover and resolve alerts about privileged identities in your organization.</span></span>  

<span data-ttu-id="96381-124">toocarry пользователи tooenable привилегированных операций, организациям необходимы временным или постоянным привилегированным доступом в Azure AD пользователи toogrant ресурсы Azure или Office 365 или другими приложениями SaaS.</span><span class="sxs-lookup"><span data-stu-id="96381-124">tooenable users toocarry out privileged operations, organizations need toogrant users temporary or permanent privileged access in Azure AD, Azure or Office 365 resources, or other SaaS apps.</span></span> <span data-ttu-id="96381-125">Каждый из этих привилегированных пользователей увеличивается hello возможных направлений атак вашей организации.</span><span class="sxs-lookup"><span data-stu-id="96381-125">Each of these privileged users increases hello attack surface of your organization.</span></span> <span data-ttu-id="96381-126">Эта уязвимость позволяет идентифицировать пользователей с ненужные уровнем доступа и принимать соответствующие меры tooreduce или избежать hello, они могут представлять.</span><span class="sxs-lookup"><span data-stu-id="96381-126">This vulnerability helps you identify users with unnecessary privileged access, and take appropriate action tooreduce or eliminate hello risk they pose.</span></span> 

<span data-ttu-id="96381-127">Корпорация Майкрософт рекомендует, чтобы ваша организация использует toomanage Azure AD Privileged Identity Management, управления и монитор привилегированных удостоверений и их tooresources доступа в Azure AD, а также другие Microsoft online services, например Office 365 или Microsoft Intune.</span><span class="sxs-lookup"><span data-stu-id="96381-127">We recommend that your organization uses Azure AD Privileged Identity Management toomanage, control, and monitor privileged identities and their access tooresources in Azure AD as well as other Microsoft online services like Office 365 or Microsoft Intune.</span></span>

<span data-ttu-id="96381-128">Дополнительные сведения см. в статье [Azure AD Privileged Identity Management](active-directory-privileged-identity-management-configure.md).</span><span class="sxs-lookup"><span data-stu-id="96381-128">For more details, see [Azure AD Privileged Identity Management](active-directory-privileged-identity-management-configure.md).</span></span> 

## <a name="see-also"></a><span data-ttu-id="96381-129">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="96381-129">See also</span></span>
* [<span data-ttu-id="96381-130">Защита идентификации Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="96381-130">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md)

