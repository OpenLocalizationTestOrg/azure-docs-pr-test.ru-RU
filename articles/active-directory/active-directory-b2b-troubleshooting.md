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
# <a name="troubleshooting-azure-active-directory-b2b-collaboration"></a>Устранение неполадок службы совместной работы Azure Active Directory B2B

В этой статье описаны способы устранения распространенных проблем, возникающих в службе совместной работы Azure Active Directory (Azure AD) B2B.


## <a name="ive-added-an-external-user-but-do-not-see-them-in-my-global-address-book-or-in-hello-people-picker"></a>Были добавлены внешнего пользователя, но они отсутствуют в адресной книге глобальных или Выбор людей hello

В случаях, где внешних пользователей не заполнены в списке hello hello объекта может занять несколько минут tooreplicate.

## <a name="a-b2b-guest-user-is-not-showing-up-in-sharepoint-onlineonedrive-people-picker"></a>Гостевой пользователь B2B не отображается в средстве выбора людей SharePoint Online или OneDrive 
 
по умолчанию toomatch устаревшее поведение Hello toosearch возможности для существующих пользователей гостя в средство выбора hello SharePoint Online (SPO) имеет значение OFF.

Эту функцию можно включить с помощью hello уровень «ShowPeoplePickerSuggestionsForGuestUsers» на приветствия клиента и коллекции сайтов. Можно задать с помощью командлетов hello набор SPOTenant и SPOSite набор, который позволяет членам функции hello toosearch всех существующих пользователей на виртуальной машине в каталоге hello. В области клиента hello не влияет на уже подготовленных Смоделированный сайтов.

## <a name="invitations-have-been-disabled-for-directory"></a>Приглашения отключены для каталога

Если уведомление о том, что у вас разрешения tooinvite пользователей, убедитесь, что ваша учетная запись пользователя является авторизованным tooinvite внешних пользователей в группе параметров пользователя:

![](media/active-directory-b2b-troubleshooting/external-user-settings.png)

Если вы недавно изменяли эти параметры или назначены роли tooa hello приглашающего гостевой пользователь, возможны задержки 15 – 60 минут hello изменения вступили в силу.

## <a name="hello-user-that-i-invited-is-receiving-an-error-during-redemption"></a>пользователь Hello, я приглашены Получает ошибку во время активации

Ниже перечислены распространенные ошибки.

### <a name="invitees-admin-has-disallowed-emailverified-users-from-being-created-in-their-tenant"></a>Администратор приглашенного пользователя запретил создавать в клиенте пользователей с атрибутом EmailVerified

Если приглашение пользователей которого организация использует Azure Active Directory, но Здравствуйте учетной записи определенного пользователя, где отсутствуют (например, hello пользователь не существует в домене contoso.com Azure AD). Здравствуйте, администратор домена contoso.com может иметь политику на месте, предотвращая пользователей. Hello пользователь должен проверять с их toodetermine admin, если разрешен внешних пользователей. Hello внешнего пользователя администратора может потребоваться tooallow проверки электронной почты пользователей в своем домене (см. в этом [статьи](/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0) на предоставление пользователям проверки электронной почты).

![](media/active-directory-b2b-troubleshooting/allow-email-verified-users.png)

### <a name="external-user-does-not-exist-already-in-a-federated-domain"></a>Внешний пользователь уже не существует в федеративном домене

Если используется проверка подлинности федерации и hello пользователя еще не существует в Azure Active Directory, невозможно пригласить пользователя hello.

эту проблему, hello tooresolve внешнего пользователя admin необходимо синхронизировать tooAzure hello пользователя учетной записи Active Directory.

## <a name="how-does--which-is-not-normally-a-valid-character-sync-with-azure-ad"></a>Как символ "\#", который обычно является недопустимым, синхронизируется с Azure AD?

«\#» является зарезервированным символом в имена участников-пользователей для совместной работы Azure AD B2B или внешних пользователей, так как hello приглашены учетной записи user@contoso.com становится user_contoso.com#EXT@fabrikam.onmicrosoft.com. Таким образом \# в имена участников-пользователей из локальной запрещены toosign в toohello портал Azure. 

## <a name="i-receive-an-error-when-adding-external-users-tooa-synchronized-group"></a>Ошибка при добавлении внешних пользователей tooa синхронизации группы

Внешние пользователи могут быть добавлены только слишком «назначенные» или группы «Безопасность» и не toogroups, хозяин в локальной среде.

## <a name="my-external-user-did-not-receive-an-email-tooredeem"></a>Мои внешних пользователей не получил tooredeem электронной почты

Приглашенный Hello удостоверьтесь у поставщика услуг Интернета или разрешена tooensure фильтр нежелательной почты, hello следующий адрес:Invites@microsoft.com

## <a name="i-notice-that-hello-custom-message-does-not-get-included-with-invitation-messages-at-times"></a>Я Обратите внимание, что пользовательские сообщения hello не получает входят в состав приглашения сообщения во время

toocomply с законодательством по защите конфиденциальности нашими API, не входят пользовательские сообщения hello приглашение по электронной почте при:

- приглашающего Hello не использует адрес электронной почты в приглашении клиента hello
- Когда участник службы приложений отправляет приглашение hello

Этот сценарий является важным tooyou, можно подавлять электронное приглашение наш API и отправить его через механизм hello электронной почты, по своему усмотрению. См. в том, что сообщения электронной почты, отправляемых таким образом, а также соответствует законодательством по защите конфиденциальности toomake юридических советника вашей организации.

## <a name="next-steps"></a>Дальнейшие действия

Другие статьи о службе совместной работы Azure AD B2B:

* [Что такое служба совместной работы Azure AD B2B?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Как администраторы Azure Active Directory могут добавить пользователей службы совместной работы B2B?](active-directory-b2b-admin-add-users.md)
* [Как информационные работники могут добавить пользователей службы совместной работы B2B в Azure Active Directory?](active-directory-b2b-iw-add-users.md)
* [элементы Hello hello электронное приглашение B2B совместной работы](active-directory-b2b-invitation-email.md)
* [Активация приглашения службы совместной работы B2B](active-directory-b2b-redemption-experience.md)
* [Руководство по лицензированию службы совместной работы Azure Active Directory B2B](active-directory-b2b-licensing.md)
* [Часто задаваемые вопросы о службе совместной работы Azure Active Directory B2B](active-directory-b2b-faq.md)
* [API службы совместной работы Azure Active Directory B2B и настройка](active-directory-b2b-api.md)
* [Многофакторная идентификация для пользователей службы совместной работы B2B](active-directory-b2b-mfa-instructions.md)
* [Добавление пользователей службы совместной работы B2B без приглашения](active-directory-b2b-add-user-without-invite.md)
* [Указатель статьей по управлению приложениями в Azure Active Directory](active-directory-apps-index.md)
