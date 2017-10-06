---
title: "приложение, в котором тип toouse при добавлении приложения toochoose aaaHow | Документы Microsoft"
description: "Понимать типы hello поддерживается приложений можно интегрировать с Azure AD и их соответствующие параметры настройки"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 46e3672e7f5048b0fa54171f0fc169362c9d5ac6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toochoose-which-application-type-toouse-when-adding-an-application"></a>Как toochoose приложение, в котором тип toouse при добавлении приложения

В этой статье, чтобы toounderstand hello четыре основных типа приложений, которые можно интегрировать с Azure AD:

* что они поддерживают;
* какой тип приложения следует выбирать;
* Tooconfigure основные свойства этих приложений, как пользователи знакомы **подготовить**, или что **единого входа** toouse технологии.

## <a name="supported-application-types-in-azure-ad"></a>Поддерживаемые типы приложений в Azure AD

Здравствуйте, Azure AD поддерживает четыре основных типах приложений, которые можно добавить с помощью **добавить** вложенной функции **корпоративных приложений**. В частности, описаны такие возможности:

-   **Приложения из коллекции Azure AD** — это предварительно интегрированные приложения для единого входа через Azure AD.

-   **Прокси-сервер приложений-приложения** — приложения, работающего в локальной среде, которые должны tooprovide безопасный единый вход в tooexternally.

-   **Сторонних разрабатываемых приложений** — приложение, ваша организация хочет toodevelop на hello платформы разработки приложений Azure AD, но который еще не существует.

-   **Приложения не из коллекции** — собственные приложения. Любой веб-ссылка нужные или любого приложения, в которой отображается поле имени пользователя и пароля, поддерживает протокол SAML или OpenID Connect или поддерживает SCIM, который вы хотите toointegrate для единого входа в Azure AD.

## <a name="features-and-capabilities-supported-by-all-hello-above-application-types"></a>Функции и возможности, поддерживаемые все hello выше типы приложений

Hello поддерживаются следующие функции по любому hello выше 4 типа приложения в Azure AD:

-   **Быстрый запуск.** Быстро приступите к работе с приложением, выполнив [простые шаги по развертыванию](https://docs.microsoft.com/azure/active-directory/active-directory-integrating-applications-getting-started).

-   **Общие свойства управления** — получить [прямой прямой ссылки](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users) приложения tooan [Настройка фирменной символики hello](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-change-app-logo-user-azure-portal) приложения, или [отключить приложение hello](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) для всех пользователей.

-   **Управление пользователями и группами** — [назначить](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) или [удалить](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) tooan приложения пользователям и группам и при необходимости назначить hello определенные роли приложения эти пользователи и группы имеют доступ к

-   **Доступ к приложению самообслуживания** — включить вашей toorequest пользователей [доступа к приложению самообслуживания](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) панелями tooan приложения из их доступа к приложениям, либо путем добавления приложения непосредственно или [ присоединение группы включена самообслуживания](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management), при необходимости требования бизнеса утверждения вдоль hello способом

-   **Журналы вход** — в разделе [все hello приложения tooan входа в систему](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-sign-ins), или во всех приложениях

-   **Журналы аудита** — в разделе [подробные журналы аудита о приложении tooan изменения](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-audit-logs), или tooall приложений

-   **Основе риска и условного доступа** — мощный задайте [правила доступа на основе условий](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access) , применяются при обращении пользователей toosign в конкретном приложении tooa

-   **Просмотр разрешений** — просматривать любые hello [разрешения OAuth2](https://docs.microsoft.com/azure/active-directory/active-directory-apps-permissions-consent) приложение имеет доступ tooin каталог из одного места

## <a name="single-sign-on-and-provisioning-modes-supported-by-specific-application-types"></a>Режимы единого входа и подготовки, поддерживаемые конкретными типами приложений

в следующей таблице Hello описывает hello различных единого входа и подготовки режимов, поддерживаемых каждым hello выше типов приложений. Можно использовать этот toohelp таблицы toounderstand приложение, в котором требуется tooadd toosupport определенную задачу.

  ![Таблица типов приложений](./media/application-tables/table1.png)

## <a name="how-toochoose-a-single-sign-on-mode"></a>Как toochoose режима единого входа

Hello поддерживается **единого входа** режимы для приложения Azure AD, перечислены ниже.

-   **Azure AD единый вход отключен** — выберите Azure AD единый вход отключен **режим-** Если вы еще не готова toointegrate это приложение с единым входом в Azure AD, или производится проверка только его

-   **Связанные входа** — выберите hello [входа на связанный](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **режим-** при наличии приложения, который уже связан с существующего единого входа для решения, или если необходимо просто toopublish простой ссылки для пользователей в их [панели доступа приложения](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) или [запуска приложений Office 365](https://login.microsoftonline.com/common/oauth2/authorize?response_mode=form_post&response_type=id_token&scope=openid&nonce=d508a995-f6d6-4b8a-81b8-825c71f1be46.636253878097046923&state=https%3a%2f%2fsupport.office.com%2farticle%2fMeet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a%3fui%3den-US%26rs%3den-US%26ad%3dUS&client_id=4b233688-031c-404b-9a80-a4f3f2351f90&redirect_uri=https%3a%2f%2fsupport.office.com%2fauth%2fsignin&login_hint=asteen%40microsoft.com&prompt=none)

-   **Пароль входа на основе** — выберите hello [входа на базе пароля](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **режим-** Если приложение отображает HTML-поле имени пользователя и пароля и toostore, имя пользователя и пароль безопасно toobe в дополнительной воспроизведены toohello приложения позже

-   **На основе SAML единого входа** — выберите hello [входа на базе SAML](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) на основе ролей приложения toospecific единый вход в режим, если приложение поддерживает протокол SAML или OpenID Connect hello, или пользователи могут toomap toobe на правилах, определенных в вашей SAML утверждений *

   >[!NOTE]
   >Этот параметр недоступен при настройке прокси-сервера приложения hello для приложения.
   >
   >

-   **Заголовок входа на основе** — выберите этот параметр, [входа на базе заголовок](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access#what-is-pingaccess-for-azure-ad) единого входа режим при наличии приложения с помощью PingAccess, которая поддерживает заголовок HTTP на основе проверки подлинности, на котором необходимо tooperform единого входа на слишком

   >[!NOTE]
   >Этот параметр доступен только при настройке прокси-сервера приложения hello и PingAccess для приложения.
   >
   >

-   **Встроенная проверка подлинности Windows** — выберите hello [встроенная проверка подлинности Windows](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd) единый вход в режим при предоставлении WIA приложения локально, на котором необходимо tooperform единого входа на слишком

   >[!NOTE]
   >Этот параметр доступен только при настройке прокси-сервера приложения hello для приложения.
   >
   >

## <a name="single-sign-on-modes-for-custom-developed-applications"></a>Режимы единого входа для специально разработанных приложений

Приложения имеют пользовательский при hello [приложения, разработанного](#_Custom-Developed_Applications) качества также поддерживают дополнительных единого входа режима не перечисленные выше. В частности, описаны такие возможности:

-   единый вход на основе [OAuth 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-oauth-code);

-   единый вход на основе [OpenID Connect 1.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-openid-connect-code);

-   единый вход на основе [WS-Federation 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html);

-   единый вход на основе [SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference).

Чтение hello [руководство разработчика Azure Active Directory](https://docs.microsoft.com/azure/active-directory/develop/active-directory-developers-guide) toolearn Дополнительные сведения о как toocreate, разработанного приложения, который поддерживает эти единого входа режимов.

## <a name="how-tooset-an-applications-single-sign-on-mode"></a>Как tooset приложения одного режима входа

tooset приложения **единого входа** режим, выполните приведенные ниже инструкции hello:

1.  Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора** или **Co-администратору.**

2.  Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.

3.  Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.

4.  Нажмите кнопку **корпоративных приложений** из Azure Active Directory hello левого меню навигации.

5.  Нажмите кнопку **все приложения** tooview список всех приложений.

  * Используйте hello, если нужно показать здесь приложения hello не отображается, **фильтра** управления вверху hello hello **список всех приложений** и набор hello **Показать** параметр слишком **Все приложения.**

6.  Выберите приложение hello, для которого требуется tooconfigure единого входа.

7.  После загрузки приложения hello щелкните **единого входа** из приложения hello левого меню навигации.

## <a name="how-toochoose-a-provisioning-mode"></a>Как toochoose режим подготовки

-   **Идет подготовка вручную** — выберите hello [вручную](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning#provisioning-modes) режима подготовки, если имеются существующие учетные записи, или если нужна toomanage учетных записей для этого приложения за пределами Azure AD.

-   **Автоматическая подготовка** — выберите hello [автоматического](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning#configuring-automatic-user-account-provisioning) **режим подготовки** Если tooenable инициализации автоматического на основе API и/или отменить подготовку учетных записей пользователей toothis приложения 

   >[!NOTE]
   >Этот параметр доступен только для приложений в пределах hello **избранные** категории hello [коллекции приложений Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-whats-new-azure-portal#the-new-and-improved-application-gallery).
   >
   >

-   **На основе SCIM автоматическую подготовку** — использовать [на основе SCIM автоматическую подготовку](https://docs.microsoft.com/azure/active-directory/active-directory-scim-provisioning) Если приложение поддерживает протокол SCIM hello обнаружения изменений toousers и групп, которые создаются автоматически для изменения tooany приложения, интегрированного с Azure AD 

   >[!NOTE]
   >Этот параметр не является определенным режимом подготовки, но он включен по умолчанию для всех приложений, интегрированных с Azure AD.
   >
   >

## <a name="how-tooset-an-applications-provisioning-mode"></a>Способ подготовки режим tooset приложения

tooset приложения **Подготовка** режиме, выполните приведенные ниже инструкции hello:

tooset приложения **единого входа** режим, выполните приведенные ниже инструкции hello:

1.  Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора** или **Co-администратору.**

2.  Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.

3.  Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.

4.  Нажмите кнопку **корпоративных приложений** из Azure Active Directory hello левого меню навигации.

5.  Нажмите кнопку **все приложения** tooview список всех приложений.

  * Используйте hello, если нужно показать здесь приложения hello не отображается, **фильтра** управления вверху hello hello **список всех приложений** и набор hello **Показать** параметр слишком **Все приложения.**

6.  Выберите приложение hello, для которого требуется tooconfigure подготовки.

7.  После загрузки приложения hello щелкните **Provisioning** из приложения hello левого меню навигации.

## <a name="next-steps"></a>Дальнейшие действия
[Управление приложениями с помощью Azure Active Directory](active-directory-enable-sso-scenario.md)
