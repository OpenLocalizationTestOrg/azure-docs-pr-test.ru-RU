---
title: "aaaTroubleshooting совместной работы Azure Active Directory B2B | Документы Microsoft"
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
ms.openlocfilehash: 6fcfd7e543cd7bb833225f8aa56e332e7a989faf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-active-directory-b2b-collaboration"></a><span data-ttu-id="505e5-103">Устранение неполадок службы совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="505e5-103">Troubleshooting Azure Active Directory B2B collaboration</span></span>

<span data-ttu-id="505e5-104">В этой статье описаны способы устранения распространенных проблем, возникающих в службе совместной работы Azure Active Directory (Azure AD) B2B.</span><span class="sxs-lookup"><span data-stu-id="505e5-104">Here are some remedies for common problems with Azure Active Directory (Azure AD) B2B collaboration.</span></span>


## <a name="ive-added-an-external-user-but-do-not-see-them-in-my-global-address-book-or-in-hello-people-picker"></a><span data-ttu-id="505e5-105">Были добавлены внешнего пользователя, но они отсутствуют в адресной книге глобальных или Выбор людей hello</span><span class="sxs-lookup"><span data-stu-id="505e5-105">I’ve added an external user but do not see them in my Global Address Book or in hello people picker</span></span>

<span data-ttu-id="505e5-106">В случаях, где внешних пользователей не заполнены в списке hello hello объекта может занять несколько минут tooreplicate.</span><span class="sxs-lookup"><span data-stu-id="505e5-106">In cases where external users are not populated in hello list, hello object might take a few minutes tooreplicate.</span></span>

## <a name="a-b2b-guest-user-is-not-showing-up-in-sharepoint-onlineonedrive-people-picker"></a><span data-ttu-id="505e5-107">Гостевой пользователь B2B не отображается в средстве выбора людей SharePoint Online или OneDrive</span><span class="sxs-lookup"><span data-stu-id="505e5-107">A B2B guest user is not showing up in SharePoint Online/OneDrive people picker</span></span> 
 
<span data-ttu-id="505e5-108">по умолчанию toomatch устаревшее поведение Hello toosearch возможности для существующих пользователей гостя в средство выбора hello SharePoint Online (SPO) имеет значение OFF.</span><span class="sxs-lookup"><span data-stu-id="505e5-108">hello ability toosearch for existing guest users in hello SharePoint Online (SPO) people picker is OFF by default toomatch legacy behavior.</span></span>

<span data-ttu-id="505e5-109">Эту функцию можно включить с помощью hello уровень «ShowPeoplePickerSuggestionsForGuestUsers» на приветствия клиента и коллекции сайтов.</span><span class="sxs-lookup"><span data-stu-id="505e5-109">You can enable this feature by using hello setting 'ShowPeoplePickerSuggestionsForGuestUsers' at hello tenant and site collection level.</span></span> <span data-ttu-id="505e5-110">Можно задать с помощью командлетов hello набор SPOTenant и SPOSite набор, который позволяет членам функции hello toosearch всех существующих пользователей на виртуальной машине в каталоге hello.</span><span class="sxs-lookup"><span data-stu-id="505e5-110">You can set hello feature using hello Set-SPOTenant and Set-SPOSite cmdlets, which allow members toosearch all existing guest users in hello directory.</span></span> <span data-ttu-id="505e5-111">В области клиента hello не влияет на уже подготовленных Смоделированный сайтов.</span><span class="sxs-lookup"><span data-stu-id="505e5-111">Changes in hello tenant scope do not affect already provisioned SPO sites.</span></span>

## <a name="invitations-have-been-disabled-for-directory"></a><span data-ttu-id="505e5-112">Приглашения отключены для каталога</span><span class="sxs-lookup"><span data-stu-id="505e5-112">Invitations have been disabled for directory</span></span>

<span data-ttu-id="505e5-113">Если уведомление о том, что у вас разрешения tooinvite пользователей, убедитесь, что ваша учетная запись пользователя является авторизованным tooinvite внешних пользователей в группе параметров пользователя:</span><span class="sxs-lookup"><span data-stu-id="505e5-113">If you are notified that you do not have permissions tooinvite users, verify that your user account is authorized tooinvite external users under User Settings:</span></span>

![](media/active-directory-b2b-troubleshooting/external-user-settings.png)

<span data-ttu-id="505e5-114">Если вы недавно изменяли эти параметры или назначены роли tooa hello приглашающего гостевой пользователь, возможны задержки 15 – 60 минут hello изменения вступили в силу.</span><span class="sxs-lookup"><span data-stu-id="505e5-114">If you have recently modified these settings or assigned hello Guest Inviter role tooa user, there might be a 15-60 minute delay before hello changes take effect.</span></span>

## <a name="hello-user-that-i-invited-is-receiving-an-error-during-redemption"></a><span data-ttu-id="505e5-115">пользователь Hello, я приглашены Получает ошибку во время активации</span><span class="sxs-lookup"><span data-stu-id="505e5-115">hello user that I invited is receiving an error during redemption</span></span>

<span data-ttu-id="505e5-116">Ниже перечислены распространенные ошибки.</span><span class="sxs-lookup"><span data-stu-id="505e5-116">Common errors include:</span></span>

### <a name="invitees-admin-has-disallowed-emailverified-users-from-being-created-in-their-tenant"></a><span data-ttu-id="505e5-117">Администратор приглашенного пользователя запретил создавать в клиенте пользователей с атрибутом EmailVerified</span><span class="sxs-lookup"><span data-stu-id="505e5-117">Invitee’s Admin has disallowed EmailVerified Users from being created in their tenant</span></span>

<span data-ttu-id="505e5-118">Если приглашение пользователей которого организация использует Azure Active Directory, но Здравствуйте учетной записи определенного пользователя, где отсутствуют (например, hello пользователь не существует в домене contoso.com Azure AD).</span><span class="sxs-lookup"><span data-stu-id="505e5-118">When inviting users whose organization is using Azure Active Directory, but where hello specific user’s account does not exist (for example, hello user does not exist in Azure AD contoso.com).</span></span> <span data-ttu-id="505e5-119">Здравствуйте, администратор домена contoso.com может иметь политику на месте, предотвращая пользователей.</span><span class="sxs-lookup"><span data-stu-id="505e5-119">hello administrator of contoso.com may have a policy in place preventing users from being created.</span></span> <span data-ttu-id="505e5-120">Hello пользователь должен проверять с их toodetermine admin, если разрешен внешних пользователей.</span><span class="sxs-lookup"><span data-stu-id="505e5-120">hello user must check with their admin toodetermine if external users are allowed.</span></span> <span data-ttu-id="505e5-121">Hello внешнего пользователя администратора может потребоваться tooallow проверки электронной почты пользователей в своем домене (см. в этом [статьи](/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0) на предоставление пользователям проверки электронной почты).</span><span class="sxs-lookup"><span data-stu-id="505e5-121">hello external user’s admin may need tooallow Email Verified users in their domain (see this [article](/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0) on allowing Email Verified Users).</span></span>

![](media/active-directory-b2b-troubleshooting/allow-email-verified-users.png)

### <a name="external-user-does-not-exist-already-in-a-federated-domain"></a><span data-ttu-id="505e5-122">Внешний пользователь уже не существует в федеративном домене</span><span class="sxs-lookup"><span data-stu-id="505e5-122">External user does not exist already in a federated domain</span></span>

<span data-ttu-id="505e5-123">Если используется проверка подлинности федерации и hello пользователя еще не существует в Azure Active Directory, невозможно пригласить пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="505e5-123">If you are using federation authentication and hello user does not already exist in Azure Active Directory, hello user cannot be invited.</span></span>

<span data-ttu-id="505e5-124">эту проблему, hello tooresolve внешнего пользователя admin необходимо синхронизировать tooAzure hello пользователя учетной записи Active Directory.</span><span class="sxs-lookup"><span data-stu-id="505e5-124">tooresolve this issue, hello external user’s admin must synchronize hello user’s account tooAzure Active Directory.</span></span>

## <a name="how-does--which-is-not-normally-a-valid-character-sync-with-azure-ad"></a><span data-ttu-id="505e5-125">Как символ "\#", который обычно является недопустимым, синхронизируется с Azure AD?</span><span class="sxs-lookup"><span data-stu-id="505e5-125">How does ‘\#’, which is not normally a valid character, sync with Azure AD?</span></span>

<span data-ttu-id="505e5-126">«\#» является зарезервированным символом в имена участников-пользователей для совместной работы Azure AD B2B или внешних пользователей, так как hello приглашены учетной записи user@contoso.com становится user_contoso.com#EXT@fabrikam.onmicrosoft.com. Таким образом \# в имена участников-пользователей из локальной запрещены toosign в toohello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="505e5-126">“\#” is a reserved character in UPNs for Azure AD B2B collaboration or external users, because hello invited account user@contoso.com becomes user_contoso.com#EXT@fabrikam.onmicrosoft.com. Therefore, \# in UPNs coming from on-premises aren't allowed toosign in toohello Azure portal.</span></span> 

## <a name="i-receive-an-error-when-adding-external-users-tooa-synchronized-group"></a><span data-ttu-id="505e5-127">Ошибка при добавлении внешних пользователей tooa синхронизации группы</span><span class="sxs-lookup"><span data-stu-id="505e5-127">I receive an error when adding external users tooa synchronized group</span></span>

<span data-ttu-id="505e5-128">Внешние пользователи могут быть добавлены только слишком «назначенные» или группы «Безопасность» и не toogroups, хозяин в локальной среде.</span><span class="sxs-lookup"><span data-stu-id="505e5-128">External users can be added only too“assigned” or “Security” groups and not toogroups that are mastered on-premises.</span></span>

## <a name="my-external-user-did-not-receive-an-email-tooredeem"></a><span data-ttu-id="505e5-129">Мои внешних пользователей не получил tooredeem электронной почты</span><span class="sxs-lookup"><span data-stu-id="505e5-129">My external user did not receive an email tooredeem</span></span>

<span data-ttu-id="505e5-130">Приглашенный Hello удостоверьтесь у поставщика услуг Интернета или разрешена tooensure фильтр нежелательной почты, hello следующий адрес:Invites@microsoft.com</span><span class="sxs-lookup"><span data-stu-id="505e5-130">hello invitee should check with their ISP or spam filter tooensure that hello following address is allowed: Invites@microsoft.com</span></span>

## <a name="i-notice-that-hello-custom-message-does-not-get-included-with-invitation-messages-at-times"></a><span data-ttu-id="505e5-131">Я Обратите внимание, что пользовательские сообщения hello не получает входят в состав приглашения сообщения во время</span><span class="sxs-lookup"><span data-stu-id="505e5-131">I notice that hello custom message does not get included with invitation messages at times</span></span>

<span data-ttu-id="505e5-132">toocomply с законодательством по защите конфиденциальности нашими API, не входят пользовательские сообщения hello приглашение по электронной почте при:</span><span class="sxs-lookup"><span data-stu-id="505e5-132">toocomply with privacy laws, our APIs do not include custom messages in hello email invitation when:</span></span>

- <span data-ttu-id="505e5-133">приглашающего Hello не использует адрес электронной почты в приглашении клиента hello</span><span class="sxs-lookup"><span data-stu-id="505e5-133">hello inviter doesn’t have an email address in hello inviting tenant</span></span>
- <span data-ttu-id="505e5-134">Когда участник службы приложений отправляет приглашение hello</span><span class="sxs-lookup"><span data-stu-id="505e5-134">When an appservice principal sends hello invitation</span></span>

<span data-ttu-id="505e5-135">Этот сценарий является важным tooyou, можно подавлять электронное приглашение наш API и отправить его через механизм hello электронной почты, по своему усмотрению.</span><span class="sxs-lookup"><span data-stu-id="505e5-135">If this scenario is important tooyou, you can suppress our API invitation email, and send it through hello email mechanism of your choice.</span></span> <span data-ttu-id="505e5-136">См. в том, что сообщения электронной почты, отправляемых таким образом, а также соответствует законодательством по защите конфиденциальности toomake юридических советника вашей организации.</span><span class="sxs-lookup"><span data-stu-id="505e5-136">Consult your organization’s legal counsel toomake sure any email you send this way also complies with privacy laws.</span></span>

## <a name="next-steps"></a><span data-ttu-id="505e5-137">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="505e5-137">Next steps</span></span>

<span data-ttu-id="505e5-138">Другие статьи о службе совместной работы Azure AD B2B:</span><span class="sxs-lookup"><span data-stu-id="505e5-138">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="505e5-139">Что такое служба совместной работы Azure AD B2B?</span><span class="sxs-lookup"><span data-stu-id="505e5-139">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="505e5-140">Как администраторы Azure Active Directory могут добавить пользователей службы совместной работы B2B?</span><span class="sxs-lookup"><span data-stu-id="505e5-140">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="505e5-141">Как информационные работники могут добавить пользователей службы совместной работы B2B в Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="505e5-141">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="505e5-142">элементы Hello hello электронное приглашение B2B совместной работы</span><span class="sxs-lookup"><span data-stu-id="505e5-142">hello elements of hello B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="505e5-143">Активация приглашения службы совместной работы B2B</span><span class="sxs-lookup"><span data-stu-id="505e5-143">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="505e5-144">Руководство по лицензированию службы совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="505e5-144">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="505e5-145">Часто задаваемые вопросы о службе совместной работы Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="505e5-145">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="505e5-146">API службы совместной работы Azure Active Directory B2B и настройка</span><span class="sxs-lookup"><span data-stu-id="505e5-146">Azure Active Directory B2B collaboration API and customization</span></span>](active-directory-b2b-api.md)
* [<span data-ttu-id="505e5-147">Многофакторная идентификация для пользователей службы совместной работы B2B</span><span class="sxs-lookup"><span data-stu-id="505e5-147">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* [<span data-ttu-id="505e5-148">Добавление пользователей службы совместной работы B2B без приглашения</span><span class="sxs-lookup"><span data-stu-id="505e5-148">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* [<span data-ttu-id="505e5-149">Указатель статьей по управлению приложениями в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="505e5-149">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
