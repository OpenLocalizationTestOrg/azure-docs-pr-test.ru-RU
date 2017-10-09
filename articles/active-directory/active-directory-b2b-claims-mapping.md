---
title: "сопоставление в Azure Active Directory выдает совместной работы aaaB2B | Документы Microsoft"
description: "Справочные материалы по сопоставлению утверждений для службы совместной работы Azure Active Directory B2B."
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 03/15/2017
ms.author: sasubram
ms.openlocfilehash: 9e26085e91a6004b2f11286ae9c1df133bd47341
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="b2b-collaboration-user-claims-mapping-in-azure-active-directory"></a><span data-ttu-id="52458-103">Сопоставление утверждений пользователя службы совместной работы B2B в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="52458-103">B2B collaboration user claims mapping in Azure Active Directory</span></span>

<span data-ttu-id="52458-104">Azure Active Directory (Azure AD) поддерживает Настройка hello утверждений, выданных в токене SAML hello B2B совместной работы пользователей.</span><span class="sxs-lookup"><span data-stu-id="52458-104">Azure Active Directory (Azure AD) supports customizing hello claims issued in hello SAML token for B2B collaboration users.</span></span> <span data-ttu-id="52458-105">При прохождении пользователем проверки подлинности приложения toohello, Azure AD выдает приложение toohello маркера SAML, которое содержит сведения (или утверждения) о пользователе hello, которое однозначно определяет их.</span><span class="sxs-lookup"><span data-stu-id="52458-105">When a user authenticates toohello application, Azure AD issues a SAML token toohello app that contains information (or claims) about hello user that uniquely identifies them.</span></span> <span data-ttu-id="52458-106">По умолчанию в нем имя пользователя, адрес электронной почты, имя и Фамилия пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="52458-106">By default, this includes hello user's user name, email address, first name, and last name.</span></span> <span data-ttu-id="52458-107">Можно просмотреть или изменить hello утверждения, отправляемые в hello приложения toohello маркера SAML вкладка атрибуты "hello".</span><span class="sxs-lookup"><span data-stu-id="52458-107">You can view or edit hello claims sent in hello SAML token toohello application under hello Attributes tab.</span></span>

<span data-ttu-id="52458-108">Существуют две возможные причины, почему вам необходимо tooedit hello утверждений, выданных в маркер SAML hello.</span><span class="sxs-lookup"><span data-stu-id="52458-108">There are two possible reasons why you might need tooedit hello claims issued in hello SAML token.</span></span>

1. <span data-ttu-id="52458-109">Hello приложение было написано toorequire другой набор утверждений идентификаторы URI или значения утверждений</span><span class="sxs-lookup"><span data-stu-id="52458-109">hello application has been written toorequire a different set of claim URIs or claim values</span></span>

2. <span data-ttu-id="52458-110">Приложение требует toobe утверждения NameIdentifier hello, отличные от hello имя участника-пользователя в Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="52458-110">Your application requires hello NameIdentifier claim toobe something other than hello user principal name stored in Azure Active Directory.</span></span>

  ![Просмотр утверждений в токене SAML](media/active-directory-b2b-claims-mapping/view-claims-in-saml-token.png)

<span data-ttu-id="52458-112">Сведения о как tooadd и изменения утверждений, см. в этой статье, для настройки утверждений [настройка утверждений, выданных в токене SAML hello для предварительно интегрированных приложений в Azure Active Directory](develop/active-directory-saml-claims-customization.md).</span><span class="sxs-lookup"><span data-stu-id="52458-112">For information on how tooadd and edit claims, check out this article on claims customization, [Customizing claims issued in hello SAML token for pre-integrated apps in Azure Active Directory](develop/active-directory-saml-claims-customization.md).</span></span> <span data-ttu-id="52458-113">По соображениям безопасности сопоставление NameID и имени участника-пользователя между клиентами для пользователей службы совместной работы B2B запрещено.</span><span class="sxs-lookup"><span data-stu-id="52458-113">For B2B collaboration users, mapping NameID and UPN cross-tenant are prevented for security reasons.</span></span>


## <a name="next-steps"></a><span data-ttu-id="52458-114">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="52458-114">Next steps</span></span>

<span data-ttu-id="52458-115">Другие статьи о службе совместной работы Azure AD B2B:</span><span class="sxs-lookup"><span data-stu-id="52458-115">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="52458-116">Что такое служба совместной работы Azure AD B2B?</span><span class="sxs-lookup"><span data-stu-id="52458-116">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="52458-117">Свойства пользователя службы совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="52458-117">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="52458-118">Добавление роли пользователя tooa B2B совместной работы</span><span class="sxs-lookup"><span data-stu-id="52458-118">Adding a B2B collaboration user tooa role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="52458-119">Делегирование приглашений для службы совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="52458-119">Delegate B2bB collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="52458-120">Динамические группы и служба совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="52458-120">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="52458-121">Примеры кода и команд PowerShell для службы совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="52458-121">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="52458-122">Настройка приложений SaaS для службы совместной работы B2B</span><span class="sxs-lookup"><span data-stu-id="52458-122">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="52458-123">Доступ внешних пользователей к Office 365</span><span class="sxs-lookup"><span data-stu-id="52458-123">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="52458-124">Основные сведения о токенах пользователей в службе совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="52458-124">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="52458-125">Текущие ограничения службы совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="52458-125">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
