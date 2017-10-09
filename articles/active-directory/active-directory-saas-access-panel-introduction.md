---
title: "aaaWhat находится панель доступа hello в Azure Active Directory? | Документация Майкрософт"
description: "Узнайте, как toouse различные виды hello доступ к панели (веб-браузера, приложения Android, приложение iPhone и iPad) tooaccess приложений SaaS."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: c0252d01-7e6e-4f79-a70e-600479577dfd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: markvi
ms.reviewer: asteen
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 800be6a69f13978c5b88e2fe28a416d4b763656c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-hello-access-panel"></a>Что такое hello панель доступа?

панель доступа Hello — веб-портал. Он позволяет пользователю с помощью рабочей или рабочую учетную запись в Azure Active Directory tooview и начала облачные приложения, что администратор Azure AD предоставил им доступ к. Можно также использовать группы самообслуживания и возможности управления приложениями через панель доступа hello.

панель доступа Hello отделен от hello портал Azure и выполняет не вы toohave подписки Azure.

![Панель доступа][1]

панель доступа Hello обеспечивает некоторые параметры профиля, включая hello возможность tooedit:

- Измените пароль hello, связанный с рабочей или учебной учетной записи

- изменение параметров сброса пароля;

- Изменение контактных данных и настройки параметров связанных toomulti двухфакторной проверки подлинности (для учетных записей, которые были необходимые toouse его администратором)

- просмотр сведений учетной записи, например идентификатора пользователя, дополнительного адреса электронной почты, номеров мобильного и рабочего телефонов, устройств;

- Просмотр и запуск облачных приложений, Здравствуйте, администратор Azure AD предоставил им доступ к. Дополнительные сведения о панели доступа hello с точки зрения пользователей hello см. с помощью панели доступа hello. 

- Самостоятельное управление группами. В частности Здравствуйте, администратор можно создавать и управлять группами безопасности и членство в группах безопасности запроса в Azure AD. Дополнительные сведения можно найти в разделах [Самостоятельное управление группами для пользователей в Azure AD](active-directory-accessmanagement-self-service-group-management.md) и [Управление группами](active-directory-manage-groups.md).




## <a name="accessing-hello-access-panel"></a>Доступ к панели доступа hello

Вы можете использовать панель доступа hello, посетив следующий URL-адрес в веб-браузере hello:`http://myapps.microsoft.com`

Если вы настроили пользовательскую фирменную символику страницы входа, вы можете загружать эту символику путем добавления организации домена toohello конец hello URL-адреса:`http://myapps.microsoft.com/<your domain>.com`

В этом случае можно использовать любое активное или проверенное доменное имя, настроенное на портале Azure.

![Wingtip Toys — имя домена][2]  

Необходимо toodistribute hello URL-адрес tooall пользователи будут входить в tooapplications, интегрированную с Azure AD.

## <a name="authentication"></a>Аутентификация

панель доступа tooreach hello, вы должны пройти проверку подлинности через рабочую или учебную учетную запись в Azure AD. Может быть прошедшего проверку подлинности tooAzure AD напрямую. Если в организации для настройки федерации использовались службы федерации Active Directory (AD FS) или другие технологии, аутентификацию можно выполнять с помощью Windows Server Active Directory.

При наличии подписки для Azure или Office 365 и вы использовали hello портал Azure или приложения Office 365, вы увидите список hello приложений без подписи в систему. Если не проходят проверку подлинности, запрашиваемые toosign в с помощью hello имя пользователя и пароль для учетной записи в Azure AD. Если в вашей организации есть настроенная служба федерации, достаточно ввести имя пользователя hello.

При проверке подлинности, вы можете взаимодействовать с приложениями hello, интегрированное с каталогом hello администратору. toointegrate приложений с Azure AD, в статье toolearn [доступ к приложению и единый вход в Azure Active Directory?](active-directory-appssoaccess-whatis.md).

## <a name="web-browser-requirements"></a>Требования к веб-браузеру

Как минимум hello панели доступа требуется браузер, поддерживающий JavaScript и CSS включения. Toobe пользователя hello вход tooapplications по паролю единого входа (SSO) расширение панели доступа hello должен устанавливаться в браузере. Hello расширение автоматически загружается при выборе приложения, настроенного для единого входа по паролю.

расширение панели доступа Hello в настоящее время доступен для Internet Explorer 8 и более поздних версий, Edge, Chrome и Firefox браузеров.

## <a name="mobile-app-support"></a>Поддержка мобильных приложений

Команда Hello Azure Active Directory публикует hello мобильное приложение my apps. При установке приложения hello, вы можете войти в приложения SSO на основе toopassword на устройствах iOS и Android.

> [!NOTE]
> Вы может войти в tooapplications, поддерживающие федерацию с Azure AD (включая Salesforce, Google Apps, Dropbox, поле, Concur, Workday, Office 365 и более 70 других) практически в любой веб-браузер на любом устройстве, без необходимости подключаемого модуля или мобильного приложения. Все остальные [доступ к панели взаимодействия](https://myapps.microsoft.com/) также не требуют hello toobe мобильное приложение my приложений, используемый на мобильном устройстве.
>
>

### <a name="my-apps-for-android"></a>My Apps для Android

Приложение My Apps для Android поддерживается на любом устройстве Android версии 4.1 и более поздней.  
Она доступна в hello [магазина Google Play](https://play.google.com/store/apps/details?id=com.microsoft.myapps).

![My Apps для Android][3]   

### <a name="my-apps-for-iphone-and-ipad"></a>My Apps для iPhone и iPad

Приложение My Apps для iOS поддерживается на всех устройствах iPhone или iPad с iOS версии 7 и более поздней.  
Она доступна в hello [Apple App Store](https://itunes.apple.com/us/app/my-apps-azure-active-directory/id824048653?mt=8).

![My Apps для iOS][4]    



## <a name="managed-browser-for-my-apps"></a>Управляемый браузер для My Apps

Мои приложения также интегрируется в hello Intune Managed Browser. Hello Intune Managed Browser для iOS и Android играет ключевую роль в обеспечении данных на мобильных устройствах обеспечивают необходимый уровень безопасности. Он позволяет безопасно просматривать и использовать веб-страницы, которые могут содержать сведения об организации, и обеспечивает безопасную работу в Интернете.  
Можно найти приложения toomy быстрого доступа на главной странице управляемого браузера и в закладки, предоставляя меньше щелкает tooreach любое приложение, tooaccess.

Она доступна в hello [Apple App Store](https://itunes.apple.com/us/app/microsoft-intune-managed-browser/id943264951?mt=8) и [магазина Google Play](https://play.google.com/store/apps/details?id=com.microsoft.intune.mam.managedbrowser&hl=en).

![Управляемый браузер для My Apps][5]    





## <a name="tips-for-testing-hello-user-experience"></a>Советы для тестирования работы пользователей hello

Если вы являетесь администратором Azure и вы вошли в toohello портал Azure, используя учетную запись в каталоге hello, вы автоматически войдете в панель доступа toohello как текущей учетной записи. В этом случае вы увидите все приложения, которые были назначены tooyou.

**tootest как *другой* учетной записи пользователя:**

1. Щелкните меню пользователя hello в правом верхнем углу hello hello портал Azure или панели доступа hello, а затем выберите **выйти**. 
2. Go toohello [панели доступа](http://myapps.microsoft.com).
3. На приветствия на странице входа, имя типа hello пользователя и пароль для учетной записи hello в вашем каталоге будет tootest.


## <a name="starting-applications"></a>Запуск приложений

На панели доступа hello можно указать несколько типов приложений.

### <a name="office-365-applications"></a>Приложения Office 365

Если ваша организация использует Office 365 приложений, лицензируются для них приложения hello Office 365 отображаются на панели доступа.

Если щелкнуть плитку приложения Office 365, их перенаправленный toohello приложений и автоматически выполнен вход.

### <a name="microsoft-and-third-party-applications-configured-with-federation-based-sso"></a>приложения Майкрософт и сторонние приложения с единым входом на основе федерации;

Администратору можно добавить приложения hello раздел hello портал Azure Active Directory с hello SSO режимом слишком**Azure AD Single Sign-On**. Эти приложения могут видеть только в том случае, если администратору явно предоставил вам доступ toohello приложений.

Если щелкнуть плитку для одного из этих приложений, вы перенаправляются и автоматический вход в приложение toohello.

### <a name="password-based-sso-without-identity-provisioning"></a>Единый вход по паролю без предоставления идентификатора

Администратору можно добавить приложения hello раздел hello портал Azure Active Directory с hello SSO режимом слишком**паролю Single Sign-On**. Все приложения, которые были настроены в этом режиме видно всем пользователям в каталоге hello.

Hello впервые, можно щелкнуть плитку для одного из этих приложений, запрашиваемые tooinstall hello единым ВХОДОМ и паролем для Internet Explorer или Chrome подключаемый модуль. Hello установки может потребоваться вы toorestart веб-браузере. Вернуть панель доступа toohello при нажатии плитку приложения hello снова появится имя пользователя и пароль для приложения hello. После ввода имени пользователя и пароля эти учетные данные безопасно хранятся и связанный tooyour учетной записи в Azure AD.

Здравствуйте, щелкните плитку приложения hello, выполняется автоматический вход в приложение toohello следующий раз.  
Не tooenter свои учетные данные снова и или установки hello единым ВХОДОМ и паролем подключаемого модуля.

Если учетные данные были изменены в hello целевого приложения сторонних разработчиков, необходимо также обновить учетные данные, хранящиеся в Azure AD. 

**tooupdate учетные данные:**

1. Выберите значок hello на плитке приложения hello.
2. Выберите **обновить учетные данные** tooreenter hello пользователя и пароль для hello приложения.


### <a name="password-based-sso-with-identity-provisioning"></a>Единый вход с помощью пароля с предоставлением идентификатора

Ваш администратор может добавлять приложения в hello **Active Directory** раздел из hello портал Azure с режимом единого входа hello установлен слишком**паролю Single Sign-On**, вместе с предоставления идентификатора.

Hello первый раз щелкнуть Плитка приложения для одного из этих приложений, то запрос tooinstall hello **подключаемый модуль для Internet Explorer или Chrome SSO на ОСНОВЕ пароля**. Hello установки может потребоваться вы toorestart веб-браузере.  
Возвращать toohello панели доступа при нажатии hello плитку приложения снова, выполняется автоматический вход в приложение toohello.

Некоторых приложений может потребоваться вы toochange пароля на hello первый вход в систему. Если учетные данные были изменены в hello целевого приложения сторонних разработчиков, необходимо также обновить hello учетные данные, хранящиеся в Azure AD. 

**tooupdate учетные данные:**

1. Выберите значок hello на плитке приложения hello.
2. Выберите **обновить учетные данные** tooreenter hello пользователя и пароль для hello приложения.


### <a name="application-with-existing-sso-solutions"></a>Приложения с существующими решениями единого входа

tooconfigure единого входа для приложения hello портал Azure предоставляет третий вариант, называемый **существующие Single Sign-On**. Этот параметр позволяет toocreate ваш администратор приложения tooan связи и поместите его на панели hello доступа для выбранных пользователей.

Например, если приложение поддерживает настроенное tooauthenticate пользователей с помощью AD FS 2.0, администратор может использовать hello **существующие Single Sign-On** toocreate параметр tooit ссылку на панели доступа hello. При доступе к связи hello, проходят проверку подлинности через AD FS 2.0 или предоставляет любое существующее приложение hello решение единого входа.


## <a name="next-steps"></a>Дальнейшие действия

- список всех разделов, управления связанные tooapplication toosee разделе hello [статей, посвященных для управления приложениями в Azure Active Directory](active-directory-apps-index.md).
 
- toolearn toointegrate приложению SaaS в Azure AD в статье hello [список учебников по приложений SaaS toointegrate](active-directory-saas-tutorial-list.md).
 
- toolearn Дополнительные сведения о управление приложениями с помощью Azure AD см. hello [введение toosingle входа и управление доступом приложений с Azure Active Directory](active-directory-appssoaccess-whatis.md).
 
- toolearn Дополнительные сведения о Подготовка пользователей, в разделе [автоматизировать подготовку пользователей и их отзыв tooSaaS приложений](active-directory-saas-app-provisioning.md).

<!--Image references-->
[1]: ./media/active-directory-saas-access-panel-introduction/01.png
[2]: ./media/active-directory-saas-access-panel-introduction/02.png
[3]: ./media/active-directory-saas-access-panel-introduction/03.png
[4]: ./media/active-directory-saas-access-panel-introduction/04.png
[5]: ./media/active-directory-saas-access-panel-introduction/05.png
