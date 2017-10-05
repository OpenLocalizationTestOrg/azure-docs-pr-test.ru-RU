---
title: "Уязвимости, обнаруживаемые защитой идентификации Azure Active Directory | Документация Майкрософт"
description: "Обзор уязвимостей, обнаруживаемых защитой идентификации Azure Active Directory."
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
ms.openlocfilehash: 364873ff54099a6123e40b12e819d1745751f285
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="vulnerabilities-detected-by-azure-active-directory-identity-protection"></a><span data-ttu-id="00f57-104">Уязвимости, обнаруживаемые защитой идентификации Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="00f57-104">Vulnerabilities detected by Azure Active Directory Identity Protection</span></span>
<span data-ttu-id="00f57-105">Уязвимости — это слабые стороны среды, которыми могут воспользоваться злоумышленники.</span><span class="sxs-lookup"><span data-stu-id="00f57-105">Vulnerabilities are weaknesses in your environment that can be exploited by an attacker.</span></span> <span data-ttu-id="00f57-106">Мы рекомендуем устранить эти уязвимости, чтобы улучшить систему безопасности своей организации и предотвратить использование уязвимостей злоумышленниками.</span><span class="sxs-lookup"><span data-stu-id="00f57-106">We recommend that you address these vulnerabilities to improve the security posture of your organization, and prevent attackers from exploiting them.</span></span>


<span data-ttu-id="00f57-107">![уязвимости](./media/active-directory-identityprotection-vulnerabilities/101.png "уязвимости")</span><span class="sxs-lookup"><span data-stu-id="00f57-107">![vulnerabilities](./media/active-directory-identityprotection-vulnerabilities/101.png "vulnerabilities")</span></span>



<span data-ttu-id="00f57-108">В следующих разделах представлен обзор уязвимостей, о которых сообщает защита идентификации.</span><span class="sxs-lookup"><span data-stu-id="00f57-108">The following sections provide you with an overview of the vulnerabilities reported by Identity Protection.</span></span>

## <a name="multi-factor-authentication-registration-not-configured"></a><span data-ttu-id="00f57-109">Регистрация с многофакторной проверкой подлинности не настроена</span><span class="sxs-lookup"><span data-stu-id="00f57-109">Multi-factor authentication registration not configured</span></span>
<span data-ttu-id="00f57-110">Эта уязвимость позволяет контролировать развертывание Azure Multi-Factor Authentication в организации.</span><span class="sxs-lookup"><span data-stu-id="00f57-110">This vulnerability helps you control the deployment of Azure Multi-Factor Authentication in your organization.</span></span> 

<span data-ttu-id="00f57-111">Azure Multi-Factor Authentication обеспечивает второй уровень безопасности для проверки подлинности пользователей.</span><span class="sxs-lookup"><span data-stu-id="00f57-111">Azure multi-factor authentication provides a second layer of security to user authentication.</span></span> <span data-ttu-id="00f57-112">Она помогает защитить доступ к данным и приложениям, при этом не усложняя процесс входа пользователя в систему.</span><span class="sxs-lookup"><span data-stu-id="00f57-112">It helps safeguard access to data and applications while meeting user demand for a simple sign-in process.</span></span> <span data-ttu-id="00f57-113">Служба обеспечивает строгую проверку подлинности с помощью простых способов проверки — телефонного звонка, текстового сообщения, уведомления в мобильном приложении, кода подтверждения или OATH-токенов третьей стороны.</span><span class="sxs-lookup"><span data-stu-id="00f57-113">It delivers strong authentication via a range of easy verification options—phone call, text message, or mobile app notification or verification code and 3rd party OATH tokens.</span></span>

<span data-ttu-id="00f57-114">Мы рекомендуем настроить обязательную проверку Azure Multi-Factor Authentication при входе пользователей.</span><span class="sxs-lookup"><span data-stu-id="00f57-114">We recommend that you require Azure Multi-Factor Authentication for user sign-ins.</span></span> <span data-ttu-id="00f57-115">Multi-Factor Authentication играет основную роль в основанных на рисках политиках условного доступа в защите идентификации.</span><span class="sxs-lookup"><span data-stu-id="00f57-115">Multi-factor authentication plays a key role in risk-based conditional access policies available through Identity Protection.</span></span>

<span data-ttu-id="00f57-116">Дополнительные сведения см. в статье [Что такое Azure Multi-factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="00f57-116">For more details, see [What is Azure Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md)</span></span>

## <a name="unmanaged-cloud-apps"></a><span data-ttu-id="00f57-117">Неуправляемые облачные приложения</span><span class="sxs-lookup"><span data-stu-id="00f57-117">Unmanaged cloud apps</span></span>
<span data-ttu-id="00f57-118">Благодаря этой уязвимости можно выявить неуправляемые облачные приложения в организации.</span><span class="sxs-lookup"><span data-stu-id="00f57-118">This vulnerability helps you identify unmanaged cloud apps in your organization.</span></span>

<span data-ttu-id="00f57-119">На современных предприятиях ИТ-специалисты часто не знают обо всех облачных приложениях, при помощи которых пользователи выполняют свои задачи.</span><span class="sxs-lookup"><span data-stu-id="00f57-119">In modern enterprises, IT departments are often unaware of all the cloud applications that users in their organization are using to do their work.</span></span> <span data-ttu-id="00f57-120">Легко понять, почему администраторов беспокоят несанкционированный доступ к корпоративным данным, возможная утечка данных и другие угрозы безопасности.</span><span class="sxs-lookup"><span data-stu-id="00f57-120">It is easy to see why administrators would have concerns about unauthorized access to corporate data, possible data leakage and other security risks.</span></span> 

<span data-ttu-id="00f57-121">Мы рекомендуем развернуть в организации Cloud App Discovery, чтобы можно было обнаруживать неуправляемые облачные приложения и управлять ими с помощью Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="00f57-121">We recommend that your organization deploy Cloud App Discovery to discover unmanaged cloud applications, and to manage these applications using Azure Active Directory.</span></span>

<span data-ttu-id="00f57-122">Дополнительные сведения см. в статье [Поиск неуправляемых облачных приложений с помощью Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="00f57-122">For more details, see [Finding unmanaged cloud applications with Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).</span></span>

## <a name="security-alerts-from-privileged-identity-management"></a><span data-ttu-id="00f57-123">Оповещения системы безопасности в рамках управления привилегированными пользователями</span><span class="sxs-lookup"><span data-stu-id="00f57-123">Security Alerts from Privileged Identity Management</span></span>
<span data-ttu-id="00f57-124">Эта уязвимость способствует обнаружению и устранению оповещений о привилегированных удостоверениях в организации.</span><span class="sxs-lookup"><span data-stu-id="00f57-124">This vulnerability helps you discover and resolve alerts about privileged identities in your organization.</span></span>  

<span data-ttu-id="00f57-125">Чтобы пользователи могли выполнять привилегированные операции, организациям необходимо предоставлять им временный или постоянный привилегированный доступ к Azure AD, ресурсам Azure или Office 365, а также другим приложениям SaaS.</span><span class="sxs-lookup"><span data-stu-id="00f57-125">To enable users to carry out privileged operations, organizations need to grant users temporary or permanent privileged access in Azure AD, Azure or Office 365 resources, or other SaaS apps.</span></span> <span data-ttu-id="00f57-126">С каждым из привилегированных пользователей повышается вероятность атаки организации.</span><span class="sxs-lookup"><span data-stu-id="00f57-126">Each of these privileged users increases the attack surface of your organization.</span></span> <span data-ttu-id="00f57-127">Эта уязвимость позволяет выявить пользователей, которым не нужен привилегированный доступ, и предпринять соответствующие действия по уменьшению или исключению представляемого ими риска.</span><span class="sxs-lookup"><span data-stu-id="00f57-127">This vulnerability helps you identify users with unnecessary privileged access, and take appropriate action to reduce or eliminate the risk they pose.</span></span> 

<span data-ttu-id="00f57-128">Мы рекомендуем настроить в организации управление привилегированными пользователями Azure AD, чтобы контролировать и отслеживать пользователей с привилегированными удостоверениями и их доступ к ресурсам в Azure AD и других веб-службах Майкрософт, таких как Office 365 или Microsoft Intune, а также управлять ими.</span><span class="sxs-lookup"><span data-stu-id="00f57-128">We recommend that your organization uses Azure AD Privileged Identity Management to manage, control, and monitor privileged identities and their access to resources in Azure AD as well as other Microsoft online services like Office 365 or Microsoft Intune.</span></span>

<span data-ttu-id="00f57-129">Дополнительные сведения см. в статье [Azure AD Privileged Identity Management](active-directory-privileged-identity-management-configure.md).</span><span class="sxs-lookup"><span data-stu-id="00f57-129">For more details, see [Azure AD Privileged Identity Management](active-directory-privileged-identity-management-configure.md).</span></span> 

## <a name="see-also"></a><span data-ttu-id="00f57-130">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="00f57-130">See also</span></span>
* [<span data-ttu-id="00f57-131">Защита идентификации Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="00f57-131">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md)

