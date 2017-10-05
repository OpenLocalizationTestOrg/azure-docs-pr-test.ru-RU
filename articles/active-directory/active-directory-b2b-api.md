---
title: "API службы совместной работы Azure Active Directory B2B и настройка | Документация Майкрософт"
description: "Служба совместной работы Azure Active Directory B2B поддерживает взаимодействие между компаниями, позволяя предоставлять бизнес-партнерам выборочный доступ к вашим корпоративным приложениям."
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
ms.date: 04/11/2017
ms.author: sasubram
ms.openlocfilehash: c85e05b38b4a9525e13ec510a17b7ef4841198d7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-b2b-collaboration-api-and-customization"></a><span data-ttu-id="f981c-103">API службы совместной работы Azure Active Directory B2B и настройка</span><span class="sxs-lookup"><span data-stu-id="f981c-103">Azure Active Directory B2B collaboration API and customization</span></span>

<span data-ttu-id="f981c-104">Очень многие клиенты высказали пожелание, чтобы процесс приглашения был более индивидуальным и соответствовал потребностям конкретной организации.</span><span class="sxs-lookup"><span data-stu-id="f981c-104">We've had many customers tell us that they want to customize the invitation process in a way that works best for their organizations.</span></span> <span data-ttu-id="f981c-105">С помощью нашего интерфейса API это можно сделать.</span><span class="sxs-lookup"><span data-stu-id="f981c-105">With our API, you can do just that.</span></span> [<span data-ttu-id="f981c-106">https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation</span><span class="sxs-lookup"><span data-stu-id="f981c-106">https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation</span></span>](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation)

## <a name="capabilities-of-the-invitation-api"></a><span data-ttu-id="f981c-107">Возможности API приглашения</span><span class="sxs-lookup"><span data-stu-id="f981c-107">Capabilities of the invitation API</span></span>
<span data-ttu-id="f981c-108">Интерфейс API предоставляет следующие возможности:</span><span class="sxs-lookup"><span data-stu-id="f981c-108">The API offers the following capabilities:</span></span>

1. <span data-ttu-id="f981c-109">Пригласите внешнего пользователя, используя *любой* адрес электронной почты.</span><span class="sxs-lookup"><span data-stu-id="f981c-109">Invite an external user with *any* email address.</span></span>

    ```
    "invitedUserDisplayName": "Sam"
    "invitedUserEmailAddress": "gsamoogle@gmail.com"
    ```

2. <span data-ttu-id="f981c-110">Настройте, куда будет перенаправляться пользователь после принятия приглашения.</span><span class="sxs-lookup"><span data-stu-id="f981c-110">Customize where you want your users to land after they accept their invitation.</span></span>

    ```
    "inviteRedirectUrl": "https://myapps.microsoft.com/"
    ```

3. <span data-ttu-id="f981c-111">Выберите отправку стандартного приглашения через нас</span><span class="sxs-lookup"><span data-stu-id="f981c-111">Choose to send the standard invitation mail through us</span></span>

    ```
    "sendInvitationMessage": true
    ```

  <span data-ttu-id="f981c-112">с сообщением для получателя, которое можно настроить.</span><span class="sxs-lookup"><span data-stu-id="f981c-112">with a message to the recipient that you can customize</span></span>

    ```
    "customizedMessageBody": "Hello Sam, let's collaborate!"
    ```

4. <span data-ttu-id="f981c-113">Выберите также, кому отправить копию. Это могут быть пользователи, которых вы хотите известить о приглашении данного сотрудника.</span><span class="sxs-lookup"><span data-stu-id="f981c-113">And choose to cc: people you want to keep in the loop about your inviting this collaborator.</span></span>

5. <span data-ttu-id="f981c-114">Или полностью настройте свой вариант приглашения и рабочего процесса регистрации сотрудников. При этом уведомления через Azure AD не будут отсылаться.</span><span class="sxs-lookup"><span data-stu-id="f981c-114">Or completely customize your invitation and onboarding workflow by choosing not to send notifications through Azure AD.</span></span>

    ```
    "sendInvitationMessage": false
    ```

  <span data-ttu-id="f981c-115">В этом случае вы получите URL-адрес активации из API, который можно вставить в шаблон электронного сообщения, отправить в мгновенном сообщении или распространить другим способом на свое усмотрение.</span><span class="sxs-lookup"><span data-stu-id="f981c-115">In this case, you get back a redemption URL from the API that you can embed in an email template, IM, or other distribution method of your choice.</span></span>

6. <span data-ttu-id="f981c-116">Наконец, если вы являетесь администратором, то вы можете пригласить пользователя в качестве участника.</span><span class="sxs-lookup"><span data-stu-id="f981c-116">Finally, if you are an admin, you can choose to invite the user as member.</span></span>

    ```
    "invitedUserType": "Member"
    ```


## <a name="authorization-model"></a><span data-ttu-id="f981c-117">Модель авторизации</span><span class="sxs-lookup"><span data-stu-id="f981c-117">Authorization model</span></span>
<span data-ttu-id="f981c-118">API можно запустить в следующих режимах авторизации:</span><span class="sxs-lookup"><span data-stu-id="f981c-118">The API can be run in the following authorization modes:</span></span>

### <a name="app--user-mode"></a><span data-ttu-id="f981c-119">Приложение + пользователь</span><span class="sxs-lookup"><span data-stu-id="f981c-119">App + User mode</span></span>
<span data-ttu-id="f981c-120">В этом режиме приложение или пользователь, использующий API, должен иметь разрешения на создание приглашений в службу B2B.</span><span class="sxs-lookup"><span data-stu-id="f981c-120">In this mode, whoever is using the API needs to have the permissions to be create B2B invitations.</span></span>

### <a name="app-only-mode"></a><span data-ttu-id="f981c-121">Только приложение</span><span class="sxs-lookup"><span data-stu-id="f981c-121">App only mode</span></span>
<span data-ttu-id="f981c-122">В контексте "только приложение" для успешного выполнения приглашения приложению требуется область User.ReadWrite.All или Directory.ReadWrite.All.</span><span class="sxs-lookup"><span data-stu-id="f981c-122">In app only context, the app needs the User.ReadWrite.All or Directory.ReadWrite.All scopes for the invitation to succeed.</span></span>

<span data-ttu-id="f981c-123">Дополнительные сведения: https://graph.microsoft.io/docs/authorization/permission_scopes</span><span class="sxs-lookup"><span data-stu-id="f981c-123">For more information, refer to: https://graph.microsoft.io/docs/authorization/permission_scopes</span></span>


## <a name="powershell"></a><span data-ttu-id="f981c-124">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f981c-124">PowerShell</span></span>
<span data-ttu-id="f981c-125">Чтобы с легкостью добавлять и приглашать в организацию внешних пользователей, теперь можно использовать PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f981c-125">It is now possible to use PowerShell to add and invite external users to an organization easily.</span></span> <span data-ttu-id="f981c-126">Создайте новое приглашение, используя приведенный ниже командлет.</span><span class="sxs-lookup"><span data-stu-id="f981c-126">Create an invitation using the cmdlet:</span></span>

```
New-AzureADMSInvitation
```

<span data-ttu-id="f981c-127">Можно использовать приведенные ниже параметры.</span><span class="sxs-lookup"><span data-stu-id="f981c-127">You can use the following options:</span></span>

* <span data-ttu-id="f981c-128">-InvitedUserDisplayName</span><span class="sxs-lookup"><span data-stu-id="f981c-128">-InvitedUserDisplayName</span></span>
* <span data-ttu-id="f981c-129">-InvitedUserEmailAddress</span><span class="sxs-lookup"><span data-stu-id="f981c-129">-InvitedUserEmailAddress</span></span>
* <span data-ttu-id="f981c-130">-SendInvitationMessage</span><span class="sxs-lookup"><span data-stu-id="f981c-130">-SendInvitationMessage</span></span>
* <span data-ttu-id="f981c-131">-InvitedUserMessageInfo</span><span class="sxs-lookup"><span data-stu-id="f981c-131">-InvitedUserMessageInfo</span></span>

<span data-ttu-id="f981c-132">Можно также ознакомиться со справочником по API приглашения: [https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation)</span><span class="sxs-lookup"><span data-stu-id="f981c-132">You can also check out the invitation API reference in [https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation)</span></span>

## <a name="next-steps"></a><span data-ttu-id="f981c-133">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f981c-133">Next steps</span></span>

<span data-ttu-id="f981c-134">Другие статьи о службе совместной работы Azure AD B2B:</span><span class="sxs-lookup"><span data-stu-id="f981c-134">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="f981c-135">Что такое служба совместной работы Azure AD B2B?</span><span class="sxs-lookup"><span data-stu-id="f981c-135">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="f981c-136">Как администраторы Azure Active Directory могут добавить пользователей службы совместной работы B2B?</span><span class="sxs-lookup"><span data-stu-id="f981c-136">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="f981c-137">Как информационные работники могут добавить пользователей службы совместной работы B2B в Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f981c-137">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="f981c-138">Элементы сообщения с приглашением в службу совместной работы B2B</span><span class="sxs-lookup"><span data-stu-id="f981c-138">The elements of the B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="f981c-139">Активация приглашения службы совместной работы B2B</span><span class="sxs-lookup"><span data-stu-id="f981c-139">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="f981c-140">Руководство по лицензированию службы совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="f981c-140">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="f981c-141">Устранение неполадок службы совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="f981c-141">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="f981c-142">Часто задаваемые вопросы о службе совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="f981c-142">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="f981c-143">Многофакторная идентификация для пользователей службы совместной работы B2B</span><span class="sxs-lookup"><span data-stu-id="f981c-143">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* [<span data-ttu-id="f981c-144">Добавление пользователей службы совместной работы B2B без приглашения</span><span class="sxs-lookup"><span data-stu-id="f981c-144">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* [<span data-ttu-id="f981c-145">Указатель статьей по управлению приложениями в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f981c-145">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
