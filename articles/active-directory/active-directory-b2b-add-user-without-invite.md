---
title: "Совместная работа aaaAdd B2B пользователей tooAzure Active Directory без приглашения | Документы Microsoft"
description: "Можно добавить другие гостевых пользователей tooyour Azure AD не активирует приглашения в Azure Active Directory B2B совместной работы пользователя guest."
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
ms.openlocfilehash: 459d99b9f856a35973d1b2cbfabdc23fe40c8f44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-b2b-collaboration-guest-users-without-an-invitation"></a><span data-ttu-id="1653f-103">Добавление гостевых пользователей службы совместной работы B2B без приглашения</span><span class="sxs-lookup"><span data-stu-id="1653f-103">Add B2B collaboration guest users without an invitation</span></span>

<span data-ttu-id="1653f-104">Вы можете разрешить пользователя, например партнера репрезентативный tooadd пользователям tooyour hello партнерской организации по ресурсам без необходимости toobe приглашения активирован.</span><span class="sxs-lookup"><span data-stu-id="1653f-104">You can allow a user, such as a partner representative, tooadd users from hello partner tooyour organization without needing invitations toobe redeemed.</span></span> <span data-ttu-id="1653f-105">Все, что необходимо сделать — предоставить этому пользователю права перечисления в каталоге hello, которую вы используете для hello org. партнера</span><span class="sxs-lookup"><span data-stu-id="1653f-105">All you must do is grant that user enumeration privileges in hello directory you're using for hello partner org.</span></span> 

<span data-ttu-id="1653f-106">Предоставляйте эти привилегии в следующих случаях.</span><span class="sxs-lookup"><span data-stu-id="1653f-106">Grant these privileges when:</span></span>

1. <span data-ttu-id="1653f-107">Пользователь в организации hello узла (например, WoodGrove) приглашает один пользователь из партнерской организации hello (например, Sam@litware.com) как гости.</span><span class="sxs-lookup"><span data-stu-id="1653f-107">A user in hello host organization (for example, WoodGrove) invites one user from hello partner organization (for example, Sam@litware.com) as Guest.</span></span>
2. <span data-ttu-id="1653f-108">Здравствуйте, администратор в организации узла hello устанавливает политик, позволяющих Sam tooidentify и добавить других пользователей от организации-партнера hello (Litware).</span><span class="sxs-lookup"><span data-stu-id="1653f-108">hello admin in hello host organization sets up policies that allow Sam tooidentify and add other users from hello partner organization (Litware).</span></span>
3. <span data-ttu-id="1653f-109">Теперь Sam можно добавить другие пользователи из каталога WoodGrove toohello Litware, групп или приложений без необходимости toobe приглашения активирован.</span><span class="sxs-lookup"><span data-stu-id="1653f-109">Now Sam can add other users from Litware toohello WoodGrove directory, groups, or applications without needing invitations toobe redeemed.</span></span> <span data-ttu-id="1653f-110">Если Sam имеет привилегии соответствующее перечисление hello в Litware, это происходит автоматически.</span><span class="sxs-lookup"><span data-stu-id="1653f-110">If Sam has hello appropriate enumeration privileges in Litware, it happens automatically.</span></span>

### <a name="next-steps"></a><span data-ttu-id="1653f-111">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1653f-111">Next steps</span></span>

<span data-ttu-id="1653f-112">Другие статьи о службе совместной работы Azure AD B2B:</span><span class="sxs-lookup"><span data-stu-id="1653f-112">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="1653f-113">Что такое служба совместной работы Azure AD B2B?</span><span class="sxs-lookup"><span data-stu-id="1653f-113">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="1653f-114">Как администраторы Azure Active Directory могут добавить пользователей службы совместной работы B2B?</span><span class="sxs-lookup"><span data-stu-id="1653f-114">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="1653f-115">Как информационные работники могут добавить пользователей службы совместной работы B2B в Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1653f-115">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="1653f-116">элементы Hello hello электронное приглашение B2B совместной работы</span><span class="sxs-lookup"><span data-stu-id="1653f-116">hello elements of hello B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="1653f-117">Активация приглашения службы совместной работы B2B</span><span class="sxs-lookup"><span data-stu-id="1653f-117">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="1653f-118">Руководство по лицензированию службы совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="1653f-118">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="1653f-119">Устранение неполадок службы совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="1653f-119">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="1653f-120">Часто задаваемые вопросы о службе совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="1653f-120">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="1653f-121">API службы совместной работы Azure Active Directory B2B и настройка</span><span class="sxs-lookup"><span data-stu-id="1653f-121">Azure Active Directory B2B collaboration API and customization</span></span>](active-directory-b2b-api.md)
* [<span data-ttu-id="1653f-122">Многофакторная идентификация для пользователей службы совместной работы B2B</span><span class="sxs-lookup"><span data-stu-id="1653f-122">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* [<span data-ttu-id="1653f-123">Указатель статьей по управлению приложениями в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1653f-123">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)