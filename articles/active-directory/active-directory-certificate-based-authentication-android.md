---
title: "aaaAzure на основе сертификатов проверки подлинности Active Directory на Android | Документы Microsoft"
description: "Дополнительные сведения о сценарии hello поддерживается и hello требования для настройки проверки подлинности на основе сертификата в решениях с устройства Android"
services: active-directory
author: MarkusVi
documentationcenter: na
manager: femila
ms.assetid: c6ad7640-8172-4541-9255-770f39ecce0e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/28/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 148275fa3da610530c278fcd57e02e907f735d9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-certificate-based-authentication-on-android"></a>Аутентификация на основе сертификата в Azure Active Directory на устройстве Android


Проверку подлинности на основе сертификатов (CBA) обеспечивает проверку подлинности Azure Active Directory с помощью сертификата клиента на устройстве Windows, Android или iOS при подключении учетную Exchange online с toobe: 

* мобильным приложениям Office, таким как Microsoft Outlook и Microsoft Word;   
* клиентам Exchange ActiveSync (EAS). 

Эта настройка устраняет необходимость hello tooenter имя пользователя и пароль к нему в определенных почты и приложения Microsoft Office на мобильных устройствах. 

В этом разделе приведены с hello требований и сценариев hello поддерживается настройка CBA на устройстве iOS(Android) для пользователей клиентов в Office 365 Enterprise, Business, образование, правительства США, Китае, и Германии планов.



В тарифных планах Office 365 US Government Defense и Federal доступна предварительная версия этой функции.


## <a name="office-mobile-applications-support"></a>Поддержка мобильных приложений Office
| Приложения | Поддержка |
| --- | --- |
| Приложение Azure Information Protection |![Проверка][1] |
| Microsoft Teams |![Проверка][1] |
| OneNote |![Проверка][1] |
| OneDrive |![Проверка][1] |
| Outlook |![Проверка][1] |
| Мобильные приложения Power BI |![Проверка][1] |
| Skype для бизнеса |![Проверка][1] |
| Word/Excel/PowerPoint |![Проверка][1] |
| Yammer |![Проверка][1] |


### <a name="implementation-requirements"></a>Требования к реализации

Hello версия ОС устройства должны быть Android 5.0 (без описания операций) и более поздних версий. 

Необходимо настроить сервер федерации.  

Для Azure Active Directory toorevoke сертификат клиента маркер hello служб федерации Active Directory должен иметь hello следующих утверждений:  

* `http://schemas.microsoft.com/ws/2008/06/identity/claims/<serialnumber>`  
  (hello серийный номер сертификата клиента hello) 
* `http://schemas.microsoft.com/2012/12/certificatecontext/field/<issuer>`  
  (строка hello для hello издателя сертификата клиента hello) 

Azure Active Directory добавляет маркер обновления toohello эти утверждения, если они доступны в маркере ADFS hello (или любой другой маркер SAML). Когда токен обновления hello должен проверить toobe, информация, которая используется toocheck hello отзыва. 

Рекомендуется, следует обновить страницы ошибок hello ADFS с инструкциями о том, как tooget сертификат пользователя.  
Дополнительные сведения см. в разделе [настройка страниц hello AD FS Sign-in](https://technet.microsoft.com/library/dn280950.aspx).  

Некоторые приложения Office (с включена современная проверка подлинности) отправлять "*prompt = имя входа*" tooAzure AD в свой запрос. По умолчанию, Azure AD преобразует это в tooADFS hello запроса слишком "*wauth = usernamepassworduri*" (запрашивает auth U и P toodo ADFS) и "*wfresh = 0*" (запрашивает состояние единого входа tooignore служб федерации Active Directory и сделать дополнительной проверки подлинности) . Если вы хотите tooenable на основе сертификатов проверки подлинности для этих приложений, необходимо toomodify hello по умолчанию Azure AD. Просто набор hello "*PromptLoginBehavior*" в параметрах федеративного домена слишком "*отключено*". Можно использовать hello [MSOLDomainFederationSettings](/powershell/module/msonline/set-msoldomainfederationsettings?view=azureadps-1.0) tooperform командлет этой задачи:

`Set-MSOLDomainFederationSettings -domainname <domain> -PromptLoginBehavior Disabled`



## <a name="exchange-activesync-clients-support"></a>Поддержка клиентов Exchange ActiveSync
Поддерживаются некоторые приложения Exchange ActiveSync, работающие на Android 5.0 (Lollipop) или более поздней версии. toodetermine при приложение электронной почты поддерживают эту функцию, обратитесь к разработчику вашего приложения. 


## <a name="next-steps"></a>Дальнейшие действия

Если требуется проверка подлинности на основе tooconfigure в вашей среде, см. раздел [приступить к работе с проверкой подлинности на основе сертификатов в Android](active-directory-certificate-based-authentication-get-started.md) инструкции.

<!--Image references-->
[1]: ./media/active-directory-certificate-based-authentication-android/ic195031.png
