---
title: "aaaAzure совместной работы Active Directory B2B часто задаваемые вопросы | Документы Microsoft"
description: "Получите ответы toofrequently вопросы и ответы о совместной работы Azure Active Directory B2B."
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
ms.date: 05/23/2017
ms.author: sasubram
ms.openlocfilehash: 4412bbc65274ff01782db81dfcc8818a6362ea7c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2b-collaboration-faqs"></a>Часто задаваемые вопросы о службе совместной работы Azure Active Directory B2B

Часто задаваемые вопросы (FAQ) о совместной работы Azure Active Directory (Azure AD) бизнес бизнес (B2B) это периодически обновляемые tooinclude новые разделы.

### <a name="is-azure-ad-b2b-collaboration-available-in-hello-azure-classic-portal"></a>Совместной работы Azure AD B2B доступен в hello классический портал Azure?
Нет. Функции совместной работы Azure AD B2B доступны только в hello [портал Azure](https://portal.azure.com) и в hello [панели доступа](https://myapps.microsoft.com/). 

### <a name="can-we-customize-our-sign-in-page-so-it-is-more-intuitive-for-our-b2b-collaboration-guest-users"></a>Можно ли настроить более интуитивно понятную страницу входа для гостевых пользователей службы совместной работы B2B?
Конечно. Ознакомьтесь с [записью блога об этой функции](https://blogs.technet.microsoft.com/enterprisemobility/2017/04/07/improving-the-branding-logic-of-azure-ad-login-pages/). Дополнительные сведения о как toocustomize вашей организации входа см. в разделе [добавить корпоративную фирменную символику страниц панели доступа и toosign в](active-directory-add-company-branding.md).

### <a name="can-b2b-collaboration-users-access-sharepoint-online-and-onedrive"></a>Имеют ли пользователи службы совместной работы B2B доступ к SharePoint Online и OneDrive?
Да. Тем не менее, является toosearch hello возможности для существующих гостевых пользователей в SharePoint Online с помощью функции выбора людей hello **Off** по умолчанию. задать tooturn на toosearch параметр hello для гостевых пользователей **ShowPeoplePickerSuggestionsForGuestUsers** слишком**на**. Этот параметр можно включить на уровне клиента hello, или на уровне семейства сайтов hello. Этот параметр можно изменить с помощью командлетов Set-SPOTenant и SPOSite набор hello. С этими командлетами члены можно найти в каталоге hello всех существующих пользователей на виртуальной машине. В области клиента hello не влияет на сайты SharePoint Online, которые уже были подготовлены.

### <a name="is-hello-csv-upload-feature-still-supported"></a>— Hello CSV передать функции по-прежнему поддерживаются?
Да. Дополнительные сведения об использовании функции передачи файлов hello CSV-файл см. в разделе [в этом примере PowerShell](active-directory-b2b-code-samples.md).

### <a name="how-can-i-customize-my-invitation-emails"></a>Как можно настроить сообщения с приглашением?
Почти все данные о процессе приглашающего hello можно настроить с помощью hello [B2B приглашения API-интерфейсы](active-directory-b2b-api.md).

### <a name="can-an-invited-external-user-leave-hello-organization-after-being-invited"></a>Hello организации после приглашаемых оставить приглашенных внешнего пользователя?
приглашение Здравствуйте, администратор организации может удалить пользователя guest B2B совместной работы из каталогов, но hello пользователь-Гость не может быть передано hello приглашении каталогом организации сами по себе. 

### <a name="can-guest-users-reset-their-multi-factor-authentication-method"></a>Могут ли гостевые пользователи сбросить настройки метода Многофакторной идентификации?
Да. Гостевые пользователи могут сбросить их hello метод многофакторной проверки подлинности, такой же, каким образом у обычных пользователей.

### <a name="which-organization-is-responsible-for-multi-factor-authentication-licenses"></a>Какая организация отвечает за лицензии Многофакторной идентификации?
Организация приглашению Hello выполняет многофакторной проверки подлинности. Hello приглашении организации необходимо убедиться, что hello организации имеется достаточное количество лицензий для пользователей, использующих многофакторной проверки подлинности B2B.

### <a name="what-if-a-partner-organization-already-has-multi-factor-authentication-set-up-can-we-trust-their-multi-factor-authentication-and-not-use-our-own-multi-factor-authentication"></a>Что делать, если в партнерской организации уже настроена Многофакторная идентификация? Можно ли доверять их MFA и не применять собственную?
Эта функция планируется в будущих выпусках так, выберите tooexclude конкретных партнеров из многофакторной проверки подлинности (hello приглашению организации).

### <a name="how-can-i-use-delayed-invitations"></a>Как настроить оправку приглашений с отложенной доставкой?
Организации может отображаться tooadd B2B совместной работы, подготовить tooapplications, при необходимости и затем отправить приглашения. Можно использовать hello B2B совместной работы приглашения API toocustomize hello адаптации рабочего процесса.

### <a name="can-i-make-a-guest-user-a-limited-administrator"></a>Можно ли назначить гостевого пользователя администратором с ограниченными правами?
Конечно. Дополнительные сведения см. в разделе [Добавление гостевых пользователей tooa роли](active-directory-users-assign-role-azure-portal.md).

### <a name="does-azure-ad-b2b-collaboration-allow-b2b-users-tooaccess-hello-azure-portal"></a>Допускает совместной работы Azure AD B2B hello tooaccess B2B пользователей портала Azure?
Если пользователю назначено hello роли глобального администратора или ограниченные Администраторы, B2B совместная работа пользователей не требуется toohello доступа к порталу Azure. Однако B2B совместной работы пользователей, назначенных hello роли глобального администратора или ограниченные администраторы могут доступ к порталу hello. Кроме того, если существование пользователя guest, не назначенным одной из этих ролей администратора обращается к порталу hello, hello пользователь может входить может tooaccess определенные части hello качества. роль пользователя гостевой Hello имеет некоторые разрешения в каталоге hello.

### <a name="can-i-block-access-toohello-azure-portal-for-guest-users"></a>Можно заблокировать доступ toohello портал Azure для гостевых пользователей?
Да! При настройке этой политики, быть случайно блокировки доступа toomembers tooavoid соблюдать осторожность и "Администраторы".
tooblock существование пользователя guest доступ к toohello [портал Azure](https://portal.azure.com), с помощью политики условного доступа в hello API модели классическое развертывание Windows Azure:
1. Изменение hello **всех пользователей** группы, чтобы он содержал только элементы.
  ![Измените снимок экрана приветствия группы](media/active-directory-b2b-faq/modify-all-users-group.png)
2. Создайте динамическую группу, в которую входят гостевые пользователи.
  ![Снимок экрана создания группы](media/active-directory-b2b-faq/group-with-guest-users.png)
3. Настройка условного доступа политики tooblock гостевой доступ пользователей к порталу hello, как показано в следующих hello видео:
  
  > [!VIDEO https://channel9.msdn.com/Blogs/Azure/b2b-block-guest-user/Player] 

### <a name="does-azure-ad-b2b-collaboration-support-multi-factor-authentication-and-consumer-email-accounts"></a>Поддерживает ли служба совместной работы Azure AD B2B Многофакторную идентификацию и учетные записи электронной почты потребителей?
Да. В этой службе реализована поддержка MFA и учетных записей электронной почты потребителей.

### <a name="do-you-plan-toosupport-password-reset-for-azure-ad-b2b-collaboration-users"></a>Планируется ли toosupport сброса паролей для пользователей Azure AD B2B совместной работы?
Да. Ниже приведены важные сведения hello для самостоятельного сброса паролей (SSPR) для пользователя B2B приглашены из партнерской организации.
 
* SSPR возникает только в клиенте удостоверение hello hello B2B пользователя.
* Если hello удостоверения клиента является учетной записью Майкрософт, используется учетная запись Майкрософт SSPR механизм hello.
* Если удостоверение клиента hello just-in-time (JIT) или «популярный» клиента, отправляется электронной почты для сброса пароля.
* Для других клиентов для B2B пользователей следует стандартный процесс SSPR hello. Как член SSPR для B2B пользователей, в контексте hello ресурса hello блокируется аренды. 

### <a name="is-password-reset-available-for-guest-users-in-a-just-in-time-jit-or-viral-tenant-who-accepted-invitations-with-a-work-or-school-email-address-but-who-didnt-have-a-pre-existing-azure-ad-account"></a>Доступен ли сброс паролей в JIT- или вирусном клиенте для пользователей, принявших приглашения через рабочий или учебный электронный адрес, но у которых нет учетной записи Azure AD?
Да. Пароль сброса почта может отправляться, который позволяет tooreset пользователя пароль в режим JIT-компилятора hello.

### <a name="does-microsoft-dynamics-crm-provide-online-support-for-azure-ad-b2b-collaboration"></a>Предоставляет ли Microsoft Dynamics CRM поддержку через Интернет для пользователей службы совместной работы Azure AD B2B?
Сейчас эта поддержка не предоставляется. Тем не менее мы планируем toosupport это в будущем hello.

### <a name="what-is-hello-lifetime-of-an-initial-password-for-a-newly-created-b2b-collaboration-user"></a>Что такое время существования hello начального пароля для только что созданного пользователя совместной работы B2B
Azure AD имеет фиксированный набор символов, надежности паролей и блокировки требования к учетной записи, которые также применяются облачным учетным записям пользователей tooall Azure AD. Облачные учетные записи — это учетные записи, которые не входят в федерацию с другими поставщиками удостоверений, такими как: 
* Учетная запись Майкрософт
* Facebook
* службы федерации Active Directory;
* другой облачный клиент (в случае службы совместной работы B2B).

Для федерации учетных записей политики паролей зависит от hello политику, примененную в параметрах учетной записи Microsoft hello локальной аренды и hello пользователя.

### <a name="an-organization-might-want-toohave-different-experiences-in-their-applications-for-tenant-users-and-guest-users-is-there-standard-guidance-for-this-is-hello-presence-of-hello-identity-provider-claim-hello-correct-model-toouse"></a>Организации может потребоваться toohave различных возможностей по работе в своих приложениях для пользователей клиента и гостевых пользователей. Есть ли стандартные рекомендации для этого? Является наличие hello hello удостоверение поставщика утверждений hello правильную модель toouse?
 Существование пользователя guest можно использовать любой tooauthenticate поставщика удостоверений. Дополнительные сведения см. в статье [Свойства пользователя службы совместной работы Azure Active Directory B2B](active-directory-b2b-user-properties.md). Используйте hello **UserType** взаимодействие с пользователем toodetermine свойство. Hello **UserType** утверждений не включены в токен hello. Приложения должны использовать hello Graph API tooquery hello каталог пользователя hello и tooget hello UserType.

### <a name="where-can-i-find-a-b2b-collaboration-community-tooshare-solutions-and-toosubmit-ideas"></a>Где можно найти tooshare сообщества B2B совместной работы решения и toosubmit идеи?
Мы слушаем постоянно tooyour отзывов, tooimprove B2B совместной работы. Мы приглашаем вас tooshare пользователей сценарии, рекомендации и что вам понравилось совместной работы Azure AD B2B. Присоединение hello-обсуждений в hello [Технический сообщества Майкрософт](https://techcommunity.microsoft.com/t5/Azure-Active-Directory-B2B/bd-p/AzureAD_B2b).
 
Также приглашаем вас toosubmit ваши идеи и голосования для будущих компонентов на [идеи совместной работы B2B](https://techcommunity.microsoft.com/t5/Azure-Active-Directory-B2B-Ideas/idb-p/AzureAD_B2B_Ideas).

### <a name="can-we-send-an-invitation-that-is-automatically-redeemed-so-that-hello-user-is-just-ready-toogo-or-does-hello-user-always-have-tooclick-through-toohello-redemption-url"></a>Можно отправить приглашение, автоматически активированы, таким образом, Здравствуйте, пользователь не является просто «готовность toogo»? Или hello пользователя всегда tooclick через URL-адрес активации toohello?
Приглашения, отправляемые с пользователем в приглашении организации, который также является членом hello партнерской организации hello не требуют активации пользователем B2B hello.

Мы рекомендуем, что вы пригласить одного пользователя от приглашении организации toojoin hello hello партнерской организации. [Добавление этой роли пользователя toohello гостевой приглашающего в организации по ресурсам hello](active-directory-b2b-add-guest-to-role.md). Этот пользователь приглашать других пользователей в организации партнера hello с помощью вход hello пользовательского интерфейса, скрипты PowerShell или API-интерфейсы. Затем B2B совместной работы пользователей из этой организации не требуется tooredeem приглашения.

### <a name="how-does-b2b-collaboration-work-when-hello-invited-partner-is-using-federation-tooadd-their-own-on-premises-authentication"></a>Как работает совместной работы B2B когда партнера hello приглашены использует tooadd федерации своей собственной локальной проверки подлинности
Если партнер hello имеет клиент Azure AD, который входит в федерацию toohello локальной инфраструктуры проверки подлинности, из локального единого входа (SSO) автоматически достигается. Если партнер hello нет клиента Azure AD, учетной записи Azure AD создается для новых пользователей. 

### <a name="i-thought-azure-ad-b2b-didnt-accept-gmailcom-and-outlookcom-email-addresses-and-that-b2c-was-used-for-those-kinds-of-accounts"></a>Действительно ли служба Azure AD B2B не поддерживает электронные адреса gmail.com и outlook.com, ведь для этих типов учетных записей используется служба B2C?
Мы удаляем hello различия между B2B и совместной работы бизнеса для компании (B2C), с учетом поддерживаются удостоверения. использовать удостоверение Hello не toochoose существенная B2B использовать или B2C. Дополнительные сведения о выборе варианта совместной работы см. в статье [Сравнение службы совместной работы B2B и B2C в Azure Active Directory](active-directory-b2b-compare-b2c.md).

### <a name="what-applications-and-services-support-azure-b2b-guest-users"></a>Какие приложения и службы поддерживают гостевых пользователей Azure B2B?
Все приложения, интегрированные с Azure AD, поддерживают гостевых пользователей Azure B2B. 

### <a name="can-we-force-multi-factor-authentication-for-b2b-guest-users-if-our-partners-dont-have-multi-factor-authentication"></a>Можно ли принудительно выполнять Многофакторную идентификацию для гостевых пользователей B2B, если эта функция не включена у партнеров?
Да. Дополнительные сведения см. в статье [Условный доступ пользователей в службе совместной работы B2B](active-directory-b2b-mfa-instructions.md).

### <a name="in-sharepoint-you-can-define-an-allow-or-deny-list-for-external-users-can-we-do-this-in-azure"></a>С помощью SharePoint можно определить список разрешений и запретов для внешних пользователей. Возможно ли это сделать в Azure?
Да. Служба совместной работы Azure AD B2B поддерживает списки разрешений и запретов. 

### <a name="what-licenses-do-we-need-toouse-azure-ad-b2b"></a>Выполните лицензий необходимо toouse Azure AD B2B?
Сведения о новые лицензии организации должен toouse Azure AD B2B, см. в разделе [совместной работы Azure Active Directory B2B лицензирования руководство](active-directory-b2b-licensing.md).

### <a name="next-steps"></a>Дальнейшие действия

Другие статьи о службе совместной работы Azure AD B2B:

* [Что такое служба совместной работы Azure AD B2B?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Как администраторы Azure Active Directory могут добавить пользователей службы совместной работы B2B?](active-directory-b2b-admin-add-users.md)
* [Как информационные работники могут добавить пользователей службы совместной работы B2B в Azure Active Directory?](active-directory-b2b-iw-add-users.md)
* [элементы Hello hello электронное приглашение B2B совместной работы](active-directory-b2b-invitation-email.md)
* [Активация приглашения службы совместной работы B2B](active-directory-b2b-redemption-experience.md)
* [Руководство по лицензированию службы совместной работы Azure Active Directory B2B](active-directory-b2b-licensing.md)
* [Устранение неполадок службы совместной работы Azure Active Directory B2B](active-directory-b2b-troubleshooting.md)
* [API службы совместной работы Azure Active Directory B2B и настройка](active-directory-b2b-api.md)
* [Многофакторная идентификация для пользователей службы совместной работы B2B](active-directory-b2b-mfa-instructions.md)
* [Добавление пользователей службы совместной работы B2B без приглашения](active-directory-b2b-add-user-without-invite.md)
* [Указатель статьей по управлению приложениями в Azure Active Directory](active-directory-apps-index.md)
