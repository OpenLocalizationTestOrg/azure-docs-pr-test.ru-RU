---
title: "Атрибуты, синхронизируемые службой Azure AD Connect | Документация Майкрософт"
description: "Списки hello атрибуты будут синхронизированы tooAzure Active Directory."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: c2bb36e0-5205-454c-b9b6-f4990bcedf51
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: billmath
ms.openlocfilehash: 2fe5b944a7fc832f245631416c265fb82eedeb15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-attributes-synchronized-tooazure-active-directory"></a>Синхронизация Azure AD Connect: атрибуты, синхронизированные tooAzure Active Directory
В этом разделе перечислены hello атрибуты, которые синхронизируются с Azure AD Connect sync.  
Hello атрибуты будут сгруппированы по hello связанные приложения Azure AD.

## <a name="attributes-toosynchronize"></a>Атрибуты toosynchronize
Часто вопрос *возможности hello список минимально атрибутов toosynchronize*. по умолчанию Hello и рекомендуемым является tookeep атрибуты по умолчанию hello, полный GAL (глобальный список адресов) может быть создан в hello облака и tooget всех возможностях Office 365 рабочих нагрузок. В некоторых случаях существуют атрибуты, которые вашей организации не хотите синхронизированные toohello облака, так как эти атрибуты содержат конфиденциальные или персональные данные (персональные данные) данных, как в этом примере:  
![Некорректные атрибуты](./media/active-directory-aadconnectsync-attributes-synchronized/badextensionattribute.png)

В этом случае начинаться с hello список атрибутов в этом разделе и определить те атрибуты, которые будет содержать учетом либо Персональных данных и не может быть синхронизирована. Отмените их выбор во время установки с помощью [фильтра приложений и атрибутов Azure AD](active-directory-aadconnect-get-started-custom.md#azure-ad-app-and-attribute-filtering).

> [!WARNING]
> Если Отмена выбора атрибутов, следует соблюдать осторожность и только отменить выбор абсолютно не возможные toosynchronize эти атрибуты. Отмена выбора других атрибутов может отрицательно повлиять на функции.
>
>

## <a name="office-365-proplus"></a>Office 365 профессиональный плюс.
| Имя атрибута | Пользователь | Комментарий |
| --- |:---:| --- |
| AccountEnabled |X |Определяет, включена ли учетная запись. |
| cn |X | |
| displayName |X | |
| objectSID |X |Механическое свойство. Идентификатор пользователя AD, используемый toomaintain синхронизации между Azure AD и AD. |
| pwdLastSet |X |Механическое свойство. Используется tooknow tooinvalidate уже выданных маркеров. Используется как в синхронизации паролей, так и в федерации. |
| sourceAnchor |X |Механическое свойство. Неизменяемый идентификатор toomaintain связи между ADDS и Azure AD. |
| usageLocation |X |Механическое свойство. Страна пользователя Hello. Используется для назначения лицензии. |
| userPrincipalName |X |Имя участника-пользователя является Идентификатором входа hello для пользователя hello. Чаще всего hello то же, что значение [почты]. |

## <a name="exchange-online"></a>Exchange Online
| Имя атрибута | Пользователь | Контакт | Группа | Комментарий |
| --- |:---:|:---:|:---:| --- |
| AccountEnabled |X | | |Определяет, включена ли учетная запись. |
| assistant |X |X | | |
| altRecipient |X | | |Требуется Azure AD Connect сборки 1.1.552.0 или более поздних версий. |
| authOrig |X |X |X | |
| c |X |X | | |
| cn |X | |X | |
| co |X |X | | |
| company |X |X | | |
| countryCode |X |X | | |
| department |X |X | | |
| description |X |X |X | |
| displayName |X |X |X | |
| dLMemRejectPerms |X |X |X | |
| dLMemSubmitPerms |X |X |X | |
| extensionAttribute1 |X |X |X | |
| extensionAttribute10 |X |X |X | |
| extensionAttribute11 |X |X |X | |
| extensionAttribute12 |X |X |X | |
| extensionAttribute13 |X |X |X | |
| extensionAttribute14 |X |X |X | |
| extensionAttribute15 |X |X |X | |
| extensionAttribute2 |X |X |X | |
| extensionAttribute3 |X |X |X | |
| extensionAttribute4 |X |X |X | |
| extensionAttribute5 |X |X |X | |
| extensionAttribute6 |X |X |X | |
| extensionAttribute7 |X |X |X | |
| extensionAttribute8 |X |X |X | |
| extensionAttribute9 |X |X |X | |
| facsimiletelephonenumber |X |X | | |
| givenName |X |X | | |
| homePhone |X |X | | |
| info |X |X |X |Сейчас этот атрибут не используется для групп. |
| Initials |X |X | | |
| l |X |X | | |
| legacyExchangeDN |X |X |X | |
| mailNickname |X |X |X | |
| mangedBy | | |X | |
| manager |X |X | | |
| member | | |X | |
| mobile |X |X | | |
| msDS-HABSeniorityIndex |X |X |X | |
| msDS-PhoneticDisplayName |X |X |X | |
| msExchArchiveGUID |X | | | |
| msExchArchiveName |X | | | |
| msExchAssistantName |X |X | | |
| msExchAuditAdmin |X | | | |
| msExchAuditDelegate |X | | | |
| msExchAuditDelegateAdmin |X | | | |
| msExchAuditOwner |X | | | |
| msExchBlockedSendersHash |X |X | | |
| msExchBypassAudit |X | | | |
| msExchBypassModerationLink | | |X |Доступно в версии в Azure AD Connect 1.1.524.0 |
| msExchCoManagedByLink | | |X | |
| msExchDelegateListLink |X | | | |
| msExchELCExpirySuspensionEnd |X | | | |
| msExchELCExpirySuspensionStart |X | | | |
| msExchELCMailboxFlags |X | | | |
| msExchEnableModeration |X | |X | |
| msExchExtensionCustomAttribute1 |X |X |X |Сейчас этот атрибут не используется Exchange Online. |
| msExchExtensionCustomAttribute2 |X |X |X |Сейчас этот атрибут не используется Exchange Online. |
| msExchExtensionCustomAttribute3 |X |X |X |Сейчас этот атрибут не используется Exchange Online. |
| msExchExtensionCustomAttribute4 |X |X |X |Сейчас этот атрибут не используется Exchange Online. |
| msExchExtensionCustomAttribute5 |X |X |X |Сейчас этот атрибут не используется Exchange Online. |
| msExchHideFromAddressLists |X |X |X | |
| msExchImmutableID |X | | | |
| msExchLitigationHoldDate |X |X |X | |
| msExchLitigationHoldOwner |X |X |X | |
| msExchMailboxAuditEnable |X | | | |
| msExchMailboxAuditLogAgeLimit |X | | | |
| msExchMailboxGuid |X | | | |
| msExchModeratedByLink |X |X |X | |
| msExchModerationFlags |X |X |X | |
| msExchRecipientDisplayType |X |X |X | |
| msExchRecipientTypeDetails |X |X |X | |
| msExchRemoteRecipientType |X | | | |
| msExchRequireAuthToSendTo |X |X |X | |
| msExchResourceCapacity |X | | | |
| msExchResourceDisplay |X | | | |
| msExchResourceMetaData |X | | | |
| msExchResourceSearchProperties |X | | | |
| msExchRetentionComment |X |X |X | |
| msExchRetentionURL |X |X |X | |
| msExchSafeRecipientsHash |X |X | | |
| msExchSafeSendersHash |X |X | | |
| msExchSenderHintTranslations |X |X |X | |
| msExchTeamMailboxExpiration |X | | | |
| msExchTeamMailboxOwners |X | | | |
| msExchTeamMailboxSharePointUrl |X | | | |
| msExchUserHoldPolicies |X | | | |
| msOrg-IsOrganizational | | |X | |
| objectSID |X | |X |Механическое свойство. Идентификатор пользователя AD, используемый toomaintain синхронизации между Azure AD и AD. |
| oOFReplyToOriginator | | |X | |
| otherFacsimileTelephone |X |X | | |
| otherHomePhone |X |X | | |
| otherTelephone |X |X | | |
| pager |X |X | | |
| physicalDeliveryOfficeName |X |X | | |
| postalCode |X |X | | |
| proxyAddresses |X |X |X | |
| publicDelegates |X |X |X | |
| pwdLastSet |X | | |Механическое свойство. Используется tooknow tooinvalidate уже выданных маркеров. Используется как в синхронизации паролей, так и в федерации. |
| reportToOriginator | | |X | |
| reportToOwner | | |X | |
| securityEnabled | | |X |Производный от groupType |
| sn |X |X | | |
| sourceAnchor |X |X |X |Механическое свойство. Неизменяемый идентификатор toomaintain связи между ADDS и Azure AD. |
| st |X |X | | |
| streetAddress |X |X | | |
| targetAddress |X |X | | |
| telephoneAssistant |X |X | | |
| TelephoneNumber |X |X | | |
| thumbnailphoto |X |X | | |
| title |X |X | | |
| unauthOrig |X |X |X | |
| usageLocation |X | | |Механическое свойство. Страна пользователя Hello. Используется для назначения лицензии. |
| userCertificate |X |X | | |
| userPrincipalName |X | | |Имя участника-пользователя является Идентификатором входа hello для пользователя hello. Чаще всего hello то же, что значение [почты]. |
| userSMIMECertificates |X |X | | |
| wWWHomePage |X |X | | |

## <a name="sharepoint-online"></a>SharePoint Online
| Имя атрибута | Пользователь | Контакт | Группа | Комментарий |
| --- |:---:|:---:|:---:| --- |
| AccountEnabled |X | | |Определяет, включена ли учетная запись. |
| authOrig |X |X |X | |
| c |X |X | | |
| cn |X | |X | |
| co |X |X | | |
| company |X |X | | |
| countryCode |X |X | | |
| department |X |X | | |
| description |X |X |X | |
| displayName |X |X |X | |
| dLMemRejectPerms |X |X |X | |
| dLMemSubmitPerms |X |X |X | |
| extensionAttribute1 |X |X |X | |
| extensionAttribute10 |X |X |X | |
| extensionAttribute11 |X |X |X | |
| extensionAttribute12 |X |X |X | |
| extensionAttribute13 |X |X |X | |
| extensionAttribute14 |X |X |X | |
| extensionAttribute15 |X |X |X | |
| extensionAttribute2 |X |X |X | |
| extensionAttribute3 |X |X |X | |
| extensionAttribute4 |X |X |X | |
| extensionAttribute5 |X |X |X | |
| extensionAttribute6 |X |X |X | |
| extensionAttribute7 |X |X |X | |
| extensionAttribute8 |X |X |X | |
| extensionAttribute9 |X |X |X | |
| facsimiletelephonenumber |X |X | | |
| givenName |X |X | | |
| hideDLMembership | | |X | |
| homePhone |X |X | | |
| info |X |X |X | |
| Initials |X |X | | |
| ipPhone |X |X | | |
| l |X |X | | |
| mail |X |X |X | |
| mailNickname |X |X |X | |
| managedBy | | |X | |
| manager |X |X | | |
| member | | |X | |
| middleName |X |X | | |
| mobile |X |X | | |
| msExchTeamMailboxExpiration |X | | | |
| msExchTeamMailboxOwners |X | | | |
| msExchTeamMailboxSharePointLinkedBy |X | | | |
| msExchTeamMailboxSharePointUrl |X | | | |
| objectSID |X | |X |Механическое свойство. Идентификатор пользователя AD, используемый toomaintain синхронизации между Azure AD и AD. |
| oOFReplyToOriginator | | |X | |
| otherFacsimileTelephone |X |X | | |
| otherHomePhone |X |X | | |
| otherIpPhone |X |X | | |
| otherMobile |X |X | | |
| otherPager |X |X | | |
| otherTelephone |X |X | | |
| pager |X |X | | |
| physicalDeliveryOfficeName |X |X | | |
| postalCode |X |X | | |
| postOfficeBox |X |X | | |
| preferredLanguage |X | | | |
| proxyAddresses |X |X |X | |
| pwdLastSet |X | | |Механическое свойство. Используется tooknow tooinvalidate уже выданных маркеров. Используется как в синхронизации паролей, так и в федерации. |
| reportToOriginator | | |X | |
| reportToOwner | | |X | |
| securityEnabled | | |X |Производный от groupType |
| sn |X |X | | |
| sourceAnchor |X |X |X |Механическое свойство. Неизменяемый идентификатор toomaintain связи между ADDS и Azure AD. |
| st |X |X | | |
| streetAddress |X |X | | |
| targetAddress |X |X | | |
| telephoneAssistant |X |X | | |
| TelephoneNumber |X |X | | |
| thumbnailphoto |X |X | | |
| title |X |X | | |
| unauthOrig |X |X |X | |
| url |X |X | | |
| usageLocation |X | | |Механическое свойство. Страна пользователя Hello. Используется для назначения лицензии. |
| userPrincipalName |X | | |Имя участника-пользователя является Идентификатором входа hello для пользователя hello. Чаще всего hello то же, что значение [почты]. |
| wWWHomePage |X |X | | |

## <a name="lync-online"></a>Lync Online
| Имя атрибута | Пользователь | Контакт | Группа | Комментарий |
| --- |:---:|:---:|:---:| --- |
| AccountEnabled |X | | |Определяет, включена ли учетная запись. |
| c |X |X | | |
| cn |X | |X | |
| co |X |X | | |
| company |X |X | | |
| department |X |X | | |
| description |X |X |X | |
| displayName |X |X |X | |
| facsimiletelephonenumber |X |X |X | |
| givenName |X |X | | |
| homePhone |X |X | | |
| ipPhone |X |X | | |
| l |X |X | | |
| mail |X |X |X | |
| mailNickname |X |X |X | |
| managedBy | | |X | |
| manager |X |X | | |
| member | | |X | |
| mobile |X |X | | |
| msExchHideFromAddressLists |X |X |X | |
| msRTCSIP-ApplicationOptions |X | | | |
| msRTCSIP-DeploymentLocator |X |X | | |
| msRTCSIP-Line |X |X | | |
| msRTCSIP-OptionFlags |X |X | | |
| msRTCSIP-OwnerUrn |X | | | |
| msRTCSIP-PrimaryUserAddress |X |X | | |
| msRTCSIP-UserEnabled |X |X | | |
| objectSID |X | |X |Механическое свойство. Идентификатор пользователя AD, используемый toomaintain синхронизации между Azure AD и AD. |
| otherTelephone |X |X | | |
| physicalDeliveryOfficeName |X |X | | |
| postalCode |X |X | | |
| preferredLanguage |X | | | |
| proxyAddresses |X |X |X | |
| pwdLastSet |X | | |Механическое свойство. Используется tooknow tooinvalidate уже выданных маркеров. Используется как в синхронизации паролей, так и в федерации. |
| securityEnabled | | |X |Производный от groupType |
| sn |X |X | | |
| sourceAnchor |X |X |X |Механическое свойство. Неизменяемый идентификатор toomaintain связи между ADDS и Azure AD. |
| st |X |X | | |
| streetAddress |X |X | | |
| TelephoneNumber |X |X | | |
| thumbnailphoto |X |X | | |
| title |X |X | | |
| usageLocation |X | | |Механическое свойство. Страна пользователя Hello. Используется для назначения лицензии. |
| userPrincipalName |X | | |Имя участника-пользователя является Идентификатором входа hello для пользователя hello. Чаще всего hello то же, что значение [почты]. |
| wWWHomePage |X |X | | |

## <a name="azure-rms"></a>Azure RMS
| Имя атрибута | Пользователь | Контакт | Группа | Комментарий |
| --- |:---:|:---:|:---:| --- |
| AccountEnabled |X | | |Определяет, включена ли учетная запись. |
| cn |X | |X |Общее имя или псевдоним. Чаще всего hello префикс значение [почты]. |
| displayName |X |X |X |Строка, представляющая имя hello часто отображается как hello понятное имя (имя и фамилия). |
| mail |X |X |X |Полный адрес электронной почты. |
| member | | |X | |
| objectSID |X | |X |Механическое свойство. Идентификатор пользователя AD, используемый toomaintain синхронизации между Azure AD и AD. |
| proxyAddresses |X |X |X |Механическое свойство. Используется в Azure AD. Содержит все дополнительные адреса электронной почты для пользователя hello. |
| pwdLastSet |X | | |Механическое свойство. Используется tooknow tooinvalidate уже выданных маркеров. |
| securityEnabled | | |X |Производный от groupType. |
| sourceAnchor |X |X |X |Механическое свойство. Неизменяемый идентификатор toomaintain связи между ADDS и Azure AD. |
| usageLocation |X | | |Механическое свойство. Страна пользователя Hello. Используется для назначения лицензии. |
| userPrincipalName |X | | |Это имя участника-пользователя является Идентификатором входа hello для пользователя hello. Чаще всего hello то же, что значение [почты]. |

## <a name="intune"></a>Intune
| Имя атрибута | Пользователь | Контакт | Группа | Комментарий |
| --- |:---:|:---:|:---:| --- |
| AccountEnabled |X | | |Определяет, включена ли учетная запись. |
| c |X |X | | |
| cn |X | |X | |
| description |X |X |X | |
| displayName |X |X |X | |
| mail |X |X |X | |
| mailNickname |X |X |X | |
| member | | |X | |
| objectSID |X | |X |Механическое свойство. Идентификатор пользователя AD, используемый toomaintain синхронизации между Azure AD и AD. |
| proxyAddresses |X |X |X | |
| pwdLastSet |X | | |Механическое свойство. Используется tooknow tooinvalidate уже выданных маркеров. Используется как в синхронизации паролей, так и в федерации. |
| securityEnabled | | |X |Производный от groupType |
| sourceAnchor |X |X |X |Механическое свойство. Неизменяемый идентификатор toomaintain связи между ADDS и Azure AD. |
| usageLocation |X | | |Механическое свойство. Страна пользователя Hello. Используется для назначения лицензии. |
| userPrincipalName |X | | |Имя участника-пользователя является Идентификатором входа hello для пользователя hello. Чаще всего hello то же, что значение [почты]. |

## <a name="dynamics-crm"></a>Dynamics CRM
| Имя атрибута | Пользователь | Контакт | Группа | Комментарий |
| --- |:---:|:---:|:---:| --- |
| AccountEnabled |X | | |Определяет, включена ли учетная запись. |
| c |X |X | | |
| cn |X | |X | |
| co |X |X | | |
| company |X |X | | |
| countryCode |X |X | | |
| description |X |X |X | |
| displayName |X |X |X | |
| facsimiletelephonenumber |X |X | | |
| givenName |X |X | | |
| l |X |X | | |
| managedBy | | |X | |
| manager |X |X | | |
| member | | |X | |
| mobile |X |X | | |
| objectSID |X | |X |Механическое свойство. Идентификатор пользователя AD, используемый toomaintain синхронизации между Azure AD и AD. |
| physicalDeliveryOfficeName |X |X | | |
| postalCode |X |X | | |
| preferredLanguage |X | | | |
| pwdLastSet |X | | |Механическое свойство. Используется tooknow tooinvalidate уже выданных маркеров. Используется как в синхронизации паролей, так и в федерации. |
| securityEnabled | | |X |Производный от groupType |
| sn |X |X | | |
| sourceAnchor |X |X |X |Механическое свойство. Неизменяемый идентификатор toomaintain связи между ADDS и Azure AD. |
| st |X |X | | |
| streetAddress |X |X | | |
| TelephoneNumber |X |X | | |
| title |X |X | | |
| usageLocation |X | | |Механическое свойство. Страна пользователя Hello. Используется для назначения лицензии. |
| userPrincipalName |X | | |Имя участника-пользователя является Идентификатором входа hello для пользователя hello. Чаще всего hello то же, что значение [почты]. |

## <a name="3rd-party-applications"></a>Сторонние приложения
Эта группа является набор атрибутов, которые используются как hello минимальной атрибутов, необходимых для универсального рабочей нагрузки или приложения. Он может использоваться для рабочей нагрузки, не указанной в другом разделе, или приложения стороннего производителя. Явно, он используется для hello следующее:

* Yammer (используется только пользователь);
* [гибридные сценарии межорганизационного взаимодействия бизнес-бизнес, обеспечиваемые такими ресурсами, как SharePoint.](http://go.microsoft.com/fwlink/?LinkId=747036)

Эта группа представляет собой набор атрибутов, которые можно использовать в том случае, если каталог Azure AD hello не используемых toosupport Office 365, Dynamics или Intune. Это небольшой набор основных атрибутов.

| Имя атрибута | Пользователь | Контакт | Группа | Комментарий |
| --- |:---:|:---:|:---:| --- |
| AccountEnabled |X | | |Определяет, включена ли учетная запись. |
| cn |X | |X | |
| displayName |X |X |X | |
| givenName |X |X | | |
| mail |X | |X | |
| managedBy | | |X | |
| mailNickname |X |X |X | |
| member | | |X | |
| objectSID |X | | |Механическое свойство. Идентификатор пользователя AD, используемый toomaintain синхронизации между Azure AD и AD. |
| proxyAddresses |X |X |X | |
| pwdLastSet |X | | |Механическое свойство. Используется tooknow tooinvalidate уже выданных маркеров. Используется как в синхронизации паролей, так и в федерации. |
| sn |X |X | | |
| sourceAnchor |X |X |X |Механическое свойство. Неизменяемый идентификатор toomaintain связи между ADDS и Azure AD. |
| usageLocation |X | | |Механическое свойство. Страна пользователя Hello. Используется для назначения лицензии. |
| userPrincipalName |X | | |Имя участника-пользователя является Идентификатором входа hello для пользователя hello. Чаще всего hello то же, что значение [почты]. |

## <a name="windows-10"></a>Windows 10
Windows 10, присоединенных к домену computer(device) синхронизирует некоторые атрибуты tooAzure AD. Дополнительные сведения о сценариях hello см. в разделе [подключения tooAzure устройств, присоединенных к домену AD, для Windows 10 возникает](../active-directory-azureadjoin-devices-group-policy.md). Эти атрибуты всегда синхронизируются, и Windows 10 отображается как приложение, выбор которого нельзя отменить. Компьютер к домену Windows 10 определяется по необходимости userCertificate атрибут hello заполнен.

| Имя атрибута | Устройство | Комментарий |
| --- |:---:| --- |
| AccountEnabled |X | |
| deviceTrustType |X |Жестко запрограммированное значение для компьютеров, присоединенных к домену. |
| displayName |X | |
| MS-DS-CreatorSID |X |Другое название registeredOwnerReference. |
| objectGUID |X |Другое название deviceID. |
| objectSID |X |Другое название onPremisesSecurityIdentifier. |
| operatingSystem |X |Другое название deviceOSType. |
| operatingSystemVersion |X |Другое название deviceOSVersion. |
| userCertificate |X | |

Эти атрибуты для **пользователя** являются Кроме toohello другие приложения, которые вы выбрали.  

| Имя атрибута | Пользователь | Комментарий |
| --- |:---:| --- |
| domainFQDN |X |Другое название dnsDomainName. Например, contoso.com. |
| domainNetBios |X |Другое название netBiosName. Например, CONTOSO. |

## <a name="exchange-hybrid-writeback"></a>Гибридная обратная запись Exchange
Эти атрибуты будут записаны из Azure AD tooon локальную службу Active Directory при выборе tooenable **гибридный Exchange**. В зависимости от установленной версии Exchange может синхронизироваться меньшее количество атрибутов.

| Имя атрибута | Пользователь | Контакт | Группа | Комментарий |
| --- |:---:|:---:|:---:| --- |
| msDS-ExternalDirectoryObjectID |X | | |Производный от cloudAnchor в Azure AD. Это новый атрибут в Exchange 2016 и Windows Server 2016 AD. |
| msExchArchiveStatus |X | | |Серверный архив: Позволяет клиентам tooarchive почты. |
| msExchBlockedSendersHash |X | | |Фильтрация: записывает обратно данные локальной фильтрации и сетевые данные о безопасных и заблокированных отправителях от клиентов. |
| msExchSafeRecipientsHash |X | | |Фильтрация: записывает обратно данные локальной фильтрации и сетевые данные о безопасных и заблокированных отправителях от клиентов. |
| msExchSafeSendersHash |X | | |Фильтрация: записывает обратно данные локальной фильтрации и сетевые данные о безопасных и заблокированных отправителях от клиентов. |
| msExchUCVoiceMailSettings |X | | |Включить единой системы обмена сообщениями (UM) - Online голосовую почту: используемые tooLync tooindicate интеграции Microsoft Lync Server локальной Server пользователь hello не голосовую почту в Интернет-служб. |
| msExchUserHoldPolicies |X | | |Удержание судебного процесса: Включает toodetermine облачных служб пользователей, находящихся в группе хранения судебного процесса. |
| proxyAddresses |X |X |X |Вставляется только hello x500 адрес из Exchange Online. |
| publicDelegates |X | | |Позволяет Exchange Online toobe почтовых ящиков предоставлены toousers права SendOnBehalfTo с почтовых ящиков Exchange в локальной среде. Требуется Azure AD Connect сборки 1.1.552.0 или более поздних версий. |

## <a name="exchange-mail-public-folder"></a>Общедоступная папка почты Exchange
Эти атрибуты синхронизируются из локальной Active Directory tooAzure AD, при выборе tooenable **общей папки почты Exchange**.

| Имя атрибута | PublicFolder | Комментарий |
| --- | :---:| --- |
| displayName | X |  |
| mail | X |  |
| msExchRecipientTypeDetails | X |  |
| objectGUID | X |  |
| proxyAddresses | X |  |
| targetAddress | X |  |

## <a name="device-writeback"></a>Обратная запись устройств
Объекты устройств создаются в Active Directory. Эти объекты можно устройства присоединены tooAzure AD или присоединенных к домену компьютеры Windows 10.

| Имя атрибута | Устройство | Комментарий |
| --- |:---:| --- |
| altSecurityIdentities |X | |
| displayName |X | |
| Различающееся имя |X | |
| msDS-CloudAnchor |X | |
| msDS-DeviceID |X | |
| msDS-DeviceObjectVersion |X | |
| msDS-DeviceOSType |X | |
| msDS-DeviceOSVersion |X | |
| msDS-DevicePhysicalIDs |X | |
| msDS-KeyCredentialLink |X |Только со схемой Windows Server 2016 AD |
| msDS-IsCompliant |X | |
| msDS-IsEnabled |X | |
| msDS-IsManaged |X | |
| msDS-RegisteredOwner |X | |

## <a name="notes"></a>Примечания
* Если с использованием альтернативного идентификатора hello локального атрибут userPrincipalName синхронизируется с onPremisesUserPrincipalName атрибут hello Azure AD. Здравствуйте, альтернативный идентификатор атрибута, например почты, синхронизируется с атрибут userPrincipalName hello Azure AD.
* В списках hello выше, hello объекта типа **пользователя** также применяется тип объекта toohello **iNetOrgPerson**.

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения о hello [синхронизации Azure AD Connect](active-directory-aadconnectsync-whatis.md) конфигурации.

Узнайте больше об [интеграции локальных удостоверений с Azure Active Directory](active-directory-aadconnect.md).
