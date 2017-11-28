---
title: "Сопоставление утверждений пользователя службы совместной работы B2B в Azure Active Directory | Документация Майкрософт"
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
ms.openlocfilehash: 5f8559450b24effd40a38879aeae3a8dd03944a3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="b2b-collaboration-user-claims-mapping-in-azure-active-directory"></a><span data-ttu-id="3bc5d-103">Сопоставление утверждений пользователя службы совместной работы B2B в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3bc5d-103">B2B collaboration user claims mapping in Azure Active Directory</span></span>

<span data-ttu-id="3bc5d-104">Azure Active Directory (Azure AD) поддерживает настройку утверждений, которые передаются в токене SAML для пользователей службы совместной работы B2B.</span><span class="sxs-lookup"><span data-stu-id="3bc5d-104">Azure Active Directory (Azure AD) supports customizing the claims issued in the SAML token for B2B collaboration users.</span></span> <span data-ttu-id="3bc5d-105">Когда пользователь проходит аутентификацию в приложении, Azure AD выдает токен SAML для приложения. В токене собрана информация (утверждения), которая однозначно идентифицирует пользователя.</span><span class="sxs-lookup"><span data-stu-id="3bc5d-105">When a user authenticates to the application, Azure AD issues a SAML token to the app that contains information (or claims) about the user that uniquely identifies them.</span></span> <span data-ttu-id="3bc5d-106">По умолчанию здесь указаны имя пользователя, адрес электронной почты, имя и фамилия пользователя.</span><span class="sxs-lookup"><span data-stu-id="3bc5d-106">By default, this includes the user's user name, email address, first name, and last name.</span></span> <span data-ttu-id="3bc5d-107">На вкладке "Атрибуты" можно просмотреть или изменить утверждения, которые передаются приложению в токене SAML.</span><span class="sxs-lookup"><span data-stu-id="3bc5d-107">You can view or edit the claims sent in the SAML token to the application under the Attributes tab.</span></span>

<span data-ttu-id="3bc5d-108">Изменение утверждений, выданных в токене SAML, может потребоваться по двум основным причинам:</span><span class="sxs-lookup"><span data-stu-id="3bc5d-108">There are two possible reasons why you might need to edit the claims issued in the SAML token.</span></span>

1. <span data-ttu-id="3bc5d-109">Приложение требует другого набора URI утверждений или значений утверждений.</span><span class="sxs-lookup"><span data-stu-id="3bc5d-109">The application has been written to require a different set of claim URIs or claim values</span></span>

2. <span data-ttu-id="3bc5d-110">Приложение требует, чтобы утверждение NameIdentifier содержало данные, отличные от имени участника-пользователя, которое хранится в Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3bc5d-110">Your application requires the NameIdentifier claim to be something other than the user principal name stored in Azure Active Directory.</span></span>

  ![Просмотр утверждений в токене SAML](media/active-directory-b2b-claims-mapping/view-claims-in-saml-token.png)

<span data-ttu-id="3bc5d-112">Сведения о том, как добавлять и редактировать утверждения, см. в статье [Настройка утверждений, выпущенных в маркере SAML для предварительно интегрированных приложений в Azure Active Directory](develop/active-directory-saml-claims-customization.md).</span><span class="sxs-lookup"><span data-stu-id="3bc5d-112">For information on how to add and edit claims, check out this article on claims customization, [Customizing claims issued in the SAML token for pre-integrated apps in Azure Active Directory](develop/active-directory-saml-claims-customization.md).</span></span> <span data-ttu-id="3bc5d-113">По соображениям безопасности сопоставление NameID и имени участника-пользователя между клиентами для пользователей службы совместной работы B2B запрещено.</span><span class="sxs-lookup"><span data-stu-id="3bc5d-113">For B2B collaboration users, mapping NameID and UPN cross-tenant are prevented for security reasons.</span></span>


## <a name="next-steps"></a><span data-ttu-id="3bc5d-114">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3bc5d-114">Next steps</span></span>

<span data-ttu-id="3bc5d-115">Другие статьи о службе совместной работы Azure AD B2B:</span><span class="sxs-lookup"><span data-stu-id="3bc5d-115">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="3bc5d-116">Что такое служба совместной работы Azure AD B2B?</span><span class="sxs-lookup"><span data-stu-id="3bc5d-116">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="3bc5d-117">Свойства пользователя службы совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="3bc5d-117">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="3bc5d-118">Добавление пользователя службы совместной работы Azure Active Directory B2B в роль</span><span class="sxs-lookup"><span data-stu-id="3bc5d-118">Adding a B2B collaboration user to a role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="3bc5d-119">Делегирование приглашений для службы совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="3bc5d-119">Delegate B2bB collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="3bc5d-120">Динамические группы и служба совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="3bc5d-120">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="3bc5d-121">Примеры кода и команд PowerShell для службы совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="3bc5d-121">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="3bc5d-122">Настройка приложений SaaS для службы совместной работы B2B</span><span class="sxs-lookup"><span data-stu-id="3bc5d-122">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="3bc5d-123">Доступ внешних пользователей к Office 365</span><span class="sxs-lookup"><span data-stu-id="3bc5d-123">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="3bc5d-124">Основные сведения о токенах пользователей в службе совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="3bc5d-124">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="3bc5d-125">Текущие ограничения службы совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="3bc5d-125">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
