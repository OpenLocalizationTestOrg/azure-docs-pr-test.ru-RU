---
title: "приложения SaaS aaaConfigure B2B совместной работы в Azure Active Directory | Документы Microsoft"
description: "Примеры кода и команд PowerShell для службы совместной работы Azure Active Directory B2B."
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
ms.openlocfilehash: c3f22f81567c04ac23ef2316c09de718ecb15d26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-saas-apps-for-b2b-collaboration"></a>Настройка приложений SaaS для службы совместной работы B2B

Служба совместной работы Azure Active Directory (Azure AD) B2B работает с большинством приложений, которые интегрируются с Azure AD. Этот раздел содержит пошаговые инструкции по настройке некоторых популярных приложений SAS для использования со службой Azure AD B2B.

Прежде чем рассматривать инструкции для конкретного приложения, ознакомьтесь с общими правилами.

* Для большинства приложений hello установки пользователь должен toohappen вручную. То есть пользователи должны создаваться вручную в также приложение hello.

* Для приложений, которые поддерживают автоматическую установку, например Dropbox различные приглашения создаются из приложения hello. Пользователям необходимо убедиться, что tooaccept каждое приглашение.

* В атрибутах пользователя hello, любые проблемы, связанные с диска профиля пользователя искаженное (UPD) в гостевых пользователей toomitigate всегда значение **идентификатор пользователя** слишком**user.mail**.


## <a name="dropbox-business"></a>Dropbox для бизнеса

tooenable toosign пользователей с помощью их учетных записей организации, необходимо вручную настроить toouse Dropbox бизнес Azure AD как поставщика удостоверений Security Assertion Markup Language (SAML). Если Business общего банка данных не было настроенных toodo таким образом, оно не может запрашивать или разрешил toosign пользователей с помощью Azure AD.

1. tooadd hello общего банка данных приложения в Azure AD, выберите **корпоративных приложений** в hello левой панели, затем щелкните **добавить**.

  ![Кнопка «Добавить» Hello, на странице приложения hello предприятия](media/active-directory-b2b-configure-saas-apps/add-dropbox.png)

2. В hello **добавить приложение** окно, введите **dropbox** в hello поле поиска, а затем выберите **Dropbox для бизнеса** в списке результатов hello.

  ![Поиск «dropbox» на hello Добавление страницы приложения](media/active-directory-b2b-configure-saas-apps/add-app-dialog.png)

3. На hello **единого входа** выберите **единого входа** в hello левой панели, а затем введите **user.mail** в hello **идентификатор пользователя** поле. (Этот идентификатор задан как имя участника-пользователя по умолчанию).

  ![Настройка единого входа для приложения hello](media/active-directory-b2b-configure-saas-apps/configure-app-sso.png)

4. toouse сертификат hello toodownload для общего банка данных конфигурации, выберите **настроить DropBox**и выберите **SAML на адрес службы единого** в списке hello.

  ![Загрузка сертификата hello для общего банка данных конфигурации](media/active-directory-b2b-configure-saas-apps/download-certificate.png)

5. Вход tooDropbox с hello входа URL-адрес из hello **единого входа** страницы.

  ![Страница приветствия входа в Dropbox](media/active-directory-b2b-configure-saas-apps/sign-in-to-dropbox.png)

6. Выберите меню hello **консоли администрирования**.

  ![ссылка «Консоли администрирования» Hello меню Dropbox hello](media/active-directory-b2b-configure-saas-apps/dropbox-menu.png)

7. В hello **проверки подлинности** выберите **дополнительные**, отправьте сертификат hello и затем в hello **URL-адрес входа** введите URL-адрес hello SAML единого входа.

  ![Hello ссылку «Дополнительные» в hello Свернуть диалоговое окно проверки подлинности](media/active-directory-b2b-configure-saas-apps/dropbox-auth-01.png)

  ![Hello «В URL-адрес входа» в hello развернуть диалоговое окно проверки подлинности](media/active-directory-b2b-configure-saas-apps/paste-single-sign-on-URL.png)

8. Настройка автоматического пользователя tooconfigure в hello портал Azure, выберите **Provisioning** hello левой панели выберите **автоматического** в hello **режим подготовки** поле, а затем выберите **Авторизовать**.

  ![Настройка автоматической подготовки пользователей в hello портал Azure](media/active-directory-b2b-configure-saas-apps/set-up-automatic-provisioning.png)

После гостя или член пользователей были настроены в общий банк данных приложение hello, они получают отдельных приглашение из общего банка данных. toouse общего банка данных единого входа, приглашенным необходимо принять приглашение hello, щелкнув ссылку в нем.

## <a name="box"></a>Box
Пользователи tooauthenticate поле гостевых пользователей с учетной записью Azure AD можно включить с помощью федерации на основании hello протокола SAML. В этой процедуре необходимо отправить tooBox.com метаданных.

1. Добавьте поле приложение hello из hello корпоративных приложений.

2. Настройка единого входа в hello следующий порядок:

  ![Настройте единый вход в Box.](media/active-directory-b2b-configure-saas-apps/configure-box-sso.png)

 а. В hello **URL-адрес входа** убедитесь, что hello URL-адрес входа правильно задан для поля в hello портал Azure. Этот URL-адрес является hello URL-адреса клиента Box.com. Он должен соответствовать соглашению об именовании hello *https://.box.com*.  
 Hello **идентификатор** не применяется toothis приложения, но она по-прежнему отображается как поле является обязательным.

 b. В hello **идентификатор пользователя** введите **user.mail** (для единого входа для учетной записи гостя).

 c. В разделе **Сертификат подписи SAML** щелкните **Создать сертификат**.

 d. toobegin Настройка вашей toouse клиента Box.com Azure AD в качестве поставщика удостоверений скачать файл метаданных hello и сохраните его в локальный диск tooyour.

 д. Пересылка hello метаданных файла toohello поле Группа поддержки, который выполняет настройку единого входа для вас.

3. Для установки автоматического пользователя Azure AD, hello левой панели выберите **Provisioning**и выберите **авторизовать**.

  ![Авторизовать панель инструментов tooconnect Azure AD](media/active-directory-b2b-configure-saas-apps/auth-azure-ad-to-connect-to-box.png)

Как приглашенным Dropbox приглашенным поле необходимо активировать их приглашения приложение hello поле.

## <a name="next-steps"></a>Дальнейшие действия

См. следующие статьи, посвященные совместной работы Azure AD B2B hello.

* [Что такое служба совместной работы Azure AD B2B?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Свойства пользователя службы совместной работы Azure Active Directory B2B](active-directory-b2b-user-properties.md)
* [Добавление роли пользователя tooa B2B совместной работы](active-directory-b2b-add-guest-to-role.md)
* [Делегирование приглашений для службы совместной работы Azure Active Directory B2B](active-directory-b2b-delegate-invitations.md)
* [Динамические группы и служба совместной работы Azure Active Directory B2B](active-directory-b2b-dynamic-groups.md)
* [Примеры кода и команд PowerShell для службы совместной работы Azure Active Directory B2B](active-directory-b2b-code-samples.md)
* [Основные сведения о токенах пользователей в службе совместной работы Azure Active Directory B2B](active-directory-b2b-user-token.md)
* [Сопоставление утверждений пользователя службы совместной работы B2B в Azure Active Directory](active-directory-b2b-claims-mapping.md)
* [Доступ внешних пользователей к Office 365](active-directory-b2b-o365-external-user.md)
* [Текущие ограничения службы совместной работы Azure Active Directory B2B](active-directory-b2b-current-limitations.md)
