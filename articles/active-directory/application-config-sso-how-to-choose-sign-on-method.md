---
title: "aaaHow toodetermine какие единого входа на метод toouse | Документы Microsoft"
description: "Понимать hello единого входа режимы, поддерживаемые Azure AD и как toopick приложения hello какие один toochoose для вас интересуют."
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
ms.openlocfilehash: 64f0bc1dc8281d1ab8222fd50eaceaf710704886
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodetermine-what-single-sign-on-method-toouse"></a>Как toodetermine какие единого входа на метод toouse

В этой статье помогут toounderstand hello единого входа режимы, поддерживаемые Azure AD и как toopick приложения hello какие один toochoose для вас интересуют.

## <a name="single-sign-on-and-provisioning-modes-supported-by-specific-application-types"></a>Режимы единого входа и подготовки, поддерживаемые конкретными типами приложений

в следующей таблице Hello описывает hello различных единого входа и подготовки режимов, поддерживаемых каждым hello выше типов приложений. Можно использовать этот toohelp таблицы toounderstand приложение, в котором требуется tooadd toosupport определенную задачу.

  ![Таблица типов приложений](./media/application-tables/table1.png)

## <a name="how-toochoose-a-single-sign-on-mode"></a>Как toochoose режима единого входа

Hello поддерживается **единого входа** режимы для приложения Azure AD, перечислены ниже.

-   **Azure AD единый вход отключен** — выберите Azure AD единый вход отключен **режим-** Если вы еще не готова toointegrate это приложение с единым входом в Azure AD, или производится проверка только его

-   **Связанные входа** — выберите hello [входа на связанный](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **режим-** при наличии приложения, который уже связан с существующего единого входа для решения, или если необходимо просто toopublish простой ссылки для пользователей в их [панели доступа приложения](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) или [запуска приложений Office 365](https://login.microsoftonline.com/common/oauth2/authorize?response_mode=form_post&response_type=id_token&scope=openid&nonce=d508a995-f6d6-4b8a-81b8-825c71f1be46.636253878097046923&state=https%3a%2f%2fsupport.office.com%2farticle%2fMeet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a%3fui%3den-US%26rs%3den-US%26ad%3dUS&client_id=4b233688-031c-404b-9a80-a4f3f2351f90&redirect_uri=https%3a%2f%2fsupport.office.com%2fauth%2fsignin&login_hint=asteen%40microsoft.com&prompt=none)

-   **Пароль входа на основе** — выберите hello [входа на базе пароля](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **режим-** Если приложение отображает HTML-поле имени пользователя и пароля и toostore, имя пользователя и пароль безопасно toobe в дополнительной воспроизведены toohello приложения позже

-   **На основе SAML единого входа** — выберите hello [входа на базе SAML](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) на основе ролей приложения toospecific единый вход в режим, если приложение поддерживает протокол SAML или OpenID Connect hello, или пользователи могут toomap toobe на правилах, определенных в вашей SAML утверждений *(**Примечание:** этот параметр недоступен при настройке прокси-сервера приложения hello для приложения) *

-   **Заголовок входа на основе** — выберите этот параметр, [входа на базе заголовок](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access#what-is-pingaccess-for-azure-ad) единого входа режим при наличии приложения с помощью PingAccess, которая поддерживает заголовок HTTP на основе проверки подлинности, на котором необходимо tooperform единого входа на слишком *(**Примечание:** этот параметр доступен только при настройке прокси-сервера приложения hello и PingAccess для приложения) *

-   **Встроенная проверка подлинности Windows** — выберите hello [встроенная проверка подлинности Windows](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd) единый вход в режим при предоставлении WIA приложения локально, на котором необходимо tooperform единого входа на слишком*()*  *Примечание:** этот параметр доступен только при настройке прокси-сервера приложения hello для приложения) *

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

6.  Выберите hello приложение tooconfigure единого входа

7.  После загрузки приложения hello щелкните **единого входа** из приложения hello левого меню навигации.

## <a name="next-steps"></a>Дальнейшие действия
[Создавайте приложения tooyour, прокси-сервера приложений](active-directory-application-proxy-sso-using-kcd.md)

