---
title: "Устранение неполадок службы совместной работы Azure Active Directory B2B | Документация Майкрософт"
description: "Способы устранения распространенных проблем со службой совместной работы Azure Active Directory B2B."
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
ms.date: 05/25/2017
ms.author: sasubram
ms.openlocfilehash: 2009cfc956a2703e268c9364996aa2d0fbd8f279
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-azure-active-directory-b2b-collaboration"></a><span data-ttu-id="8f7fa-103">Устранение неполадок службы совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="8f7fa-103">Troubleshooting Azure Active Directory B2B collaboration</span></span>

<span data-ttu-id="8f7fa-104">В этой статье описаны способы устранения распространенных проблем, возникающих в службе совместной работы Azure Active Directory (Azure AD) B2B.</span><span class="sxs-lookup"><span data-stu-id="8f7fa-104">Here are some remedies for common problems with Azure Active Directory (Azure AD) B2B collaboration.</span></span>


## <a name="ive-added-an-external-user-but-do-not-see-them-in-my-global-address-book-or-in-the-people-picker"></a><span data-ttu-id="8f7fa-105">После добавления внешнего пользователя он не отображается в глобальной адресной книге или в средстве выбора пользователей</span><span class="sxs-lookup"><span data-stu-id="8f7fa-105">I’ve added an external user but do not see them in my Global Address Book or in the people picker</span></span>

<span data-ttu-id="8f7fa-106">В тех случаях, когда данные внешних пользователей не заполняются в списке, репликация объекта может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="8f7fa-106">In cases where external users are not populated in the list, the object might take a few minutes to replicate.</span></span>

## <a name="a-b2b-guest-user-is-not-showing-up-in-sharepoint-onlineonedrive-people-picker"></a><span data-ttu-id="8f7fa-107">Гостевой пользователь B2B не отображается в средстве выбора людей SharePoint Online или OneDrive</span><span class="sxs-lookup"><span data-stu-id="8f7fa-107">A B2B guest user is not showing up in SharePoint Online/OneDrive people picker</span></span> 
 
<span data-ttu-id="8f7fa-108">Возможность поиска существующих гостевых пользователей в средстве выбора пользователей SharePoint Online (SPO) отключена по умолчанию для согласования с поведением предыдущих версий.</span><span class="sxs-lookup"><span data-stu-id="8f7fa-108">The ability to search for existing guest users in the SharePoint Online (SPO) people picker is OFF by default to match legacy behavior.</span></span>

<span data-ttu-id="8f7fa-109">Вы можете включить эту функцию, используя параметр ShowPeoplePickerSuggestionsForGuestUsers на уровне семейства веб-сайтов и коллекции клиентов.</span><span class="sxs-lookup"><span data-stu-id="8f7fa-109">You can enable this feature by using the setting 'ShowPeoplePickerSuggestionsForGuestUsers' at the tenant and site collection level.</span></span> <span data-ttu-id="8f7fa-110">Задать параметр этой функции можно с помощью командлетов SPOTenant и SPOSite, которые позволяют участникам искать всех существующих гостевых пользователей в каталоге.</span><span class="sxs-lookup"><span data-stu-id="8f7fa-110">You can set the feature using the Set-SPOTenant and Set-SPOSite cmdlets, which allow members to search all existing guest users in the directory.</span></span> <span data-ttu-id="8f7fa-111">Изменения в области клиента не влияют на уже подготовленные сайты SPO.</span><span class="sxs-lookup"><span data-stu-id="8f7fa-111">Changes in the tenant scope do not affect already provisioned SPO sites.</span></span>

## <a name="invitations-have-been-disabled-for-directory"></a><span data-ttu-id="8f7fa-112">Приглашения отключены для каталога</span><span class="sxs-lookup"><span data-stu-id="8f7fa-112">Invitations have been disabled for directory</span></span>

<span data-ttu-id="8f7fa-113">Если появляется уведомление, указывающее, что у вас нет разрешений на приглашение пользователей, проверьте в разделе "Параметры пользователей", есть ли у вашей учетной записи полномочия на приглашение внешних пользователей.</span><span class="sxs-lookup"><span data-stu-id="8f7fa-113">If you are notified that you do not have permissions to invite users, verify that your user account is authorized to invite external users under User Settings:</span></span>

![](media/active-directory-b2b-troubleshooting/external-user-settings.png)

<span data-ttu-id="8f7fa-114">Если вы недавно изменили эти параметры или назначили пользователю роль лица, приглашающего гостей, то изменения вступят в силу примерно через 15–60 минут.</span><span class="sxs-lookup"><span data-stu-id="8f7fa-114">If you have recently modified these settings or assigned the Guest Inviter role to a user, there might be a 15-60 minute delay before the changes take effect.</span></span>

## <a name="the-user-that-i-invited-is-receiving-an-error-during-redemption"></a><span data-ttu-id="8f7fa-115">Пользователь, которого я пригласил, в процессе активации получает сообщение об ошибке</span><span class="sxs-lookup"><span data-stu-id="8f7fa-115">The user that I invited is receiving an error during redemption</span></span>

<span data-ttu-id="8f7fa-116">Ниже перечислены распространенные ошибки.</span><span class="sxs-lookup"><span data-stu-id="8f7fa-116">Common errors include:</span></span>

### <a name="invitees-admin-has-disallowed-emailverified-users-from-being-created-in-their-tenant"></a><span data-ttu-id="8f7fa-117">Администратор приглашенного пользователя запретил создавать в клиенте пользователей с атрибутом EmailVerified</span><span class="sxs-lookup"><span data-stu-id="8f7fa-117">Invitee’s Admin has disallowed EmailVerified Users from being created in their tenant</span></span>

<span data-ttu-id="8f7fa-118">Если приглашаются пользователи из организации, в которой используется каталог Azure Active Directory, где отсутствует учетная запись определенного пользователя (например, пользователь не существует в каталоге AAD contoso.com).</span><span class="sxs-lookup"><span data-stu-id="8f7fa-118">When inviting users whose organization is using Azure Active Directory, but where the specific user’s account does not exist (for example, the user does not exist in Azure AD contoso.com).</span></span> <span data-ttu-id="8f7fa-119">Администратор contoso.com мог настроить политику, которая запрещает создавать пользователей.</span><span class="sxs-lookup"><span data-stu-id="8f7fa-119">The administrator of contoso.com may have a policy in place preventing users from being created.</span></span> <span data-ttu-id="8f7fa-120">Пользователь должен уточнить у администратора, разрешается ли приглашать внешних пользователей.</span><span class="sxs-lookup"><span data-stu-id="8f7fa-120">The user must check with their admin to determine if external users are allowed.</span></span> <span data-ttu-id="8f7fa-121">Администратору внешнего пользователя может потребоваться разрешить в своем домене пользователей с проверенным адресом электронной почты (сведения о разрешении пользователей с проверенным адресом электронной почты см. в этой [статье](/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0)).</span><span class="sxs-lookup"><span data-stu-id="8f7fa-121">The external user’s admin may need to allow Email Verified users in their domain (see this [article](/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0) on allowing Email Verified Users).</span></span>

![](media/active-directory-b2b-troubleshooting/allow-email-verified-users.png)

### <a name="external-user-does-not-exist-already-in-a-federated-domain"></a><span data-ttu-id="8f7fa-122">Внешний пользователь уже не существует в федеративном домене</span><span class="sxs-lookup"><span data-stu-id="8f7fa-122">External user does not exist already in a federated domain</span></span>

<span data-ttu-id="8f7fa-123">Если используется проверка подлинности федерации, и пользователь уже не существует в Azure Active Directory, пригласить его невозможно.</span><span class="sxs-lookup"><span data-stu-id="8f7fa-123">If you are using federation authentication and the user does not already exist in Azure Active Directory, the user cannot be invited.</span></span>

<span data-ttu-id="8f7fa-124">Для устранения этой проблемы администратор внешнего пользователя должен синхронизировать учетную запись этого пользователя с Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8f7fa-124">To resolve this issue, the external user’s admin must synchronize the user’s account to Azure Active Directory.</span></span>

## <a name="how-does--which-is-not-normally-a-valid-character-sync-with-azure-ad"></a><span data-ttu-id="8f7fa-125">Как символ "\#", который обычно является недопустимым, синхронизируется с Azure AD?</span><span class="sxs-lookup"><span data-stu-id="8f7fa-125">How does ‘\#’, which is not normally a valid character, sync with Azure AD?</span></span>

<span data-ttu-id="8f7fa-126">Знак "\#" зарезервирован для имен участников-пользователей службы совместной работы Azure AD B2B или внешних пользователей (имя учетной записи приглашенного пользователя user@contoso.com преобразуется в user_contoso.com#EXT@fabrikam.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="8f7fa-126">“\#” is a reserved character in UPNs for Azure AD B2B collaboration or external users, because the invited account user@contoso.com becomes user_contoso.com#EXT@fabrikam.onmicrosoft.com.</span></span> <span data-ttu-id="8f7fa-127">Поэтому при входе на портал Azure не разрешается использовать знак "\#" в именах участников-пользователей из локальной среды.</span><span class="sxs-lookup"><span data-stu-id="8f7fa-127">Therefore, \# in UPNs coming from on-premises aren't allowed to sign in to the Azure portal.</span></span> 

## <a name="i-receive-an-error-when-adding-external-users-to-a-synchronized-group"></a><span data-ttu-id="8f7fa-128">При добавлении внешних пользователей в синхронизированную группу появляется сообщение об ошибке</span><span class="sxs-lookup"><span data-stu-id="8f7fa-128">I receive an error when adding external users to a synchronized group</span></span>

<span data-ttu-id="8f7fa-129">Внешних пользователей можно добавлять только в "назначенные" группы или группы "безопасности", а не в локально управляемые группы.</span><span class="sxs-lookup"><span data-stu-id="8f7fa-129">External users can be added only to “assigned” or “Security” groups and not to groups that are mastered on-premises.</span></span>

## <a name="my-external-user-did-not-receive-an-email-to-redeem"></a><span data-ttu-id="8f7fa-130">Внешний пользователь не получил оправленное ему сообщение для активации</span><span class="sxs-lookup"><span data-stu-id="8f7fa-130">My external user did not receive an email to redeem</span></span>

<span data-ttu-id="8f7fa-131">Приглашенному пользователю следует обратиться к своему поставщику услуг Интернета или проверить настройки фильтра нежелательной почты и убедиться, что этот адрес разрешен: Invites@microsoft.com</span><span class="sxs-lookup"><span data-stu-id="8f7fa-131">The invitee should check with their ISP or spam filter to ensure that the following address is allowed: Invites@microsoft.com</span></span>

## <a name="i-notice-that-the-custom-message-does-not-get-included-with-invitation-messages-at-times"></a><span data-ttu-id="8f7fa-132">Пользовательское сообщение иногда не включаются в сообщение с приглашением</span><span class="sxs-lookup"><span data-stu-id="8f7fa-132">I notice that the custom message does not get included with invitation messages at times</span></span>

<span data-ttu-id="8f7fa-133">Для соблюдения требований законов о защите конфиденциальности данных наши API-интерфейсы не включают пользовательские сообщения в текст сообщений с приглашением:</span><span class="sxs-lookup"><span data-stu-id="8f7fa-133">To comply with privacy laws, our APIs do not include custom messages in the email invitation when:</span></span>

- <span data-ttu-id="8f7fa-134">если в приглашающем клиенте не указан адрес электронной почты приглашающего;</span><span class="sxs-lookup"><span data-stu-id="8f7fa-134">The inviter doesn’t have an email address in the inviting tenant</span></span>
- <span data-ttu-id="8f7fa-135">если приглашение отправляет субъект-служба приложения.</span><span class="sxs-lookup"><span data-stu-id="8f7fa-135">When an appservice principal sends the invitation</span></span>

<span data-ttu-id="8f7fa-136">Если вам важно использовать именно этот сценарий, вы можете запретить отправку сообщения с приглашением из API-интерфейса, и отправить его через любой другой механизм отправки электронной почты.</span><span class="sxs-lookup"><span data-stu-id="8f7fa-136">If this scenario is important to you, you can suppress our API invitation email, and send it through the email mechanism of your choice.</span></span> <span data-ttu-id="8f7fa-137">Проконсультируйтесь к юристом своей организации, чтобы убедиться, что отправляемые таким образом сообщения не нарушают требования законов о защите конфиденциальности данных.</span><span class="sxs-lookup"><span data-stu-id="8f7fa-137">Consult your organization’s legal counsel to make sure any email you send this way also complies with privacy laws.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8f7fa-138">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8f7fa-138">Next steps</span></span>

<span data-ttu-id="8f7fa-139">Другие статьи о службе совместной работы Azure AD B2B:</span><span class="sxs-lookup"><span data-stu-id="8f7fa-139">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="8f7fa-140">Что такое служба совместной работы Azure AD B2B?</span><span class="sxs-lookup"><span data-stu-id="8f7fa-140">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="8f7fa-141">Как администраторы Azure Active Directory могут добавить пользователей службы совместной работы B2B?</span><span class="sxs-lookup"><span data-stu-id="8f7fa-141">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="8f7fa-142">Как информационные работники могут добавить пользователей службы совместной работы B2B в Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8f7fa-142">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="8f7fa-143">Элементы сообщения с приглашением в службу совместной работы B2B</span><span class="sxs-lookup"><span data-stu-id="8f7fa-143">The elements of the B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="8f7fa-144">Активация приглашения службы совместной работы B2B</span><span class="sxs-lookup"><span data-stu-id="8f7fa-144">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="8f7fa-145">Руководство по лицензированию службы совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="8f7fa-145">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="8f7fa-146">Часто задаваемые вопросы о службе совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="8f7fa-146">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="8f7fa-147">API службы совместной работы Azure Active Directory B2B и настройка</span><span class="sxs-lookup"><span data-stu-id="8f7fa-147">Azure Active Directory B2B collaboration API and customization</span></span>](active-directory-b2b-api.md)
* [<span data-ttu-id="8f7fa-148">Многофакторная идентификация для пользователей службы совместной работы B2B</span><span class="sxs-lookup"><span data-stu-id="8f7fa-148">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* [<span data-ttu-id="8f7fa-149">Добавление пользователей службы совместной работы B2B без приглашения</span><span class="sxs-lookup"><span data-stu-id="8f7fa-149">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* [<span data-ttu-id="8f7fa-150">Указатель статьей по управлению приложениями в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8f7fa-150">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
