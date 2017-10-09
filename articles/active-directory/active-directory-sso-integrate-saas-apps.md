---
title: "aaaIntegrate Azure Active Directory единого входа для приложений SaaS | Документы Microsoft"
description: "Управляйте централизованным доступом к приложениям SaaS, реализовав проверку подлинности единого входа и подготовку пользователей в Azure Active Directory. Общие сведения о том, как приложения tooSaaS toointegrate Azure Active Directory."
services: active-directory
keywords: "Интеграция Azure AD с приложениями SaaS"
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 53b9d341-d1fc-4bbb-ac7c-3f4c68fcf00a
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/17/2017
ms.author: curtand
ms.reviewer: aaronsm
ms.openlocfilehash: fe621a30429c81c32470635d105ae3e95184efa1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-active-directory-single-sign-on-with-saas-apps"></a>Интеграция единого входа Azure Active Directory с приложениями SaaS
> [!div class="op_single_selector"]
> * [Портал Azure](active-directory-enterprise-apps-manage-sso.md)
> * [классическом портале Azure](active-directory-sso-integrate-saas-apps.md)
>
>

[!INCLUDE [active-directory-sso-use-case-intro](../../includes/active-directory-sso-use-case-intro.md)]

tooget запущена Настройка единого входа для приложения, которое перенос в вашей организации, можно будет использовать существующий каталог в Azure Active Directory (Azure AD). Можно использовать каталог Azure AD, полученный через Microsoft Azure, Office 365 или Windows Intune. При наличии двух или более из этих, [администрирование каталога Azure AD](active-directory-administer.md) toodetermine какие один toouse.

> [!IMPORTANT]
> Корпорация Майкрософт рекомендует управлять Azure AD, используя hello [Центр администрирования Azure AD](https://aad.portal.azure.com) в hello портал Azure, вместо использования hello классический портал Azure, в этой статье. Как центру tooassign ролей администратора в Azure AD Здравствуйте, администратор, в разделе [назначение ролей администратора в Azure Active Directory](active-directory-enterprise-apps-manage-sso.md).

## <a name="authentication"></a>Аутентификация
Для приложений, которые поддерживают hello SAML 2.0 WS-Federation или OpenID Connect протоколы, подписи отношений доверия сертификатов tooestablish использует Azure Active Directory. Дополнительные сведения об этом см. в статье [Управление сертификатами для федеративного единого входа в Azure Active Directory](active-directory-sso-certs.md).

Для приложений, поддерживающих только HTML на основе форм вход, отношения доверия tooestablish «vaulting пароль» использует Azure Active Directory. Это позволяет hello пользователям в вашей организации toobe автоматически входить в tooa приложения SaaS с Azure AD, используя hello учетных записей пользователей из hello приложения SaaS. Azure AD собирает и надежно сохраняет сведения об учетной записи пользователя hello и связанные пароли hello. Дополнительные сведения см. в статье [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md#password-based-single-sign-on)

## <a name="authorization"></a>Авторизация
Учетной записи подготовленного позволяет toouse toobe авторизованных пользователей приложения после прошли проверку подлинности через единый вход. Подготовка пользователей можно сделать вручную или в некоторых случаях можно добавлять и удалять сведения о пользователе из приложения hello SaaS с учетом изменений, внесенных в Azure Active Directory. Дополнительные сведения об использовании имеющихся соединителей Azure AD для автоматической подготовки см. в статье [Автоматическая подготовка пользователей и ее отзыв для приложений SaaS в Azure Active Directory](active-directory-saas-app-provisioning.md).

В противном случае можно вручную добавить приложение tooan сведения пользователя, или использовать другие решения подготовки, доступных на рынке hello.

## <a name="access"></a>Access
Azure AD предоставляет несколько способов настраиваемые toodeploy приложений tooend пользователей в вашей организации. Вы не привязаны к конкретному решению развертывания или доступа. Можно использовать [hello решение, которое наилучшим образом соответствует вашим потребностям](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users).

## <a name="additional-considerations-for-applications-already-in-use"></a>Дополнительные замечания для приложений, которые уже используются
Настройка единого входа на приложение, использующее вашей организации уже выполняется процесс отличается от процесса создания новых учетных записей для нового приложения hello. Существуют несколько шагов, в том числе: сопоставление удостоверения пользователя из удостоверения tooAzure AD приложения hello и основные сведения о том, как пользователи столкнутся с ведения журналов в tooan приложения после его интеграции.

> [!NOTE]
> tooset копирование единого входа для существующего приложения требуются права глобального администратора toohave в обоих Azure AD и hello приложения SaaS.
>
>

### <a name="mapping-user-accounts"></a>Сопоставление учетных записей пользователей
Удостоверение пользователя обычно имеет уникальный идентификатор, в качестве которого может выступать адрес электронной почты или имя участника-пользователя (UPN). Вам потребуется toolink (map) удостоверение tootheir соответствующих Azure AD identity каждого пользователя приложения. Существует несколько способов tooaccomplish это в зависимости от того, как требование проверки подлинности приложения hello.

Дополнительные сведения о сопоставлении удостоверений приложений с удостоверениями Azure AD см. в разделе [настройка утверждений, выданных в токене SAML hello](http://social.technet.microsoft.com/wiki/contents/articles/31257.azure-active-directory-customizing-claims-issued-in-the-saml-token-for-pre-integrated-apps.aspx) и [Настройка сопоставлений атрибутов для подготовки](active-directory-saas-customizing-attribute-mappings.md).

### <a name="understanding-hello-users-log-in-experience"></a>Основные сведения о входе этого пользователя hello в качества
При интеграции единого входа для приложения, которое уже используется, очень важно, что повлияет на toorealize, hello взаимодействие с пользователем. Для всех приложений пользователи начнут их toosign учетные данные Azure AD в. Также возможно, они должны использовать приложения hello различных tooaccess портала.

Единый вход для некоторых приложений может выполняться при входе в приложение hello интерфейс, но для других приложений hello пользователя будет иметь такие как toogo через центральный портал ([Мои приложения](http://myapps.microsoft.com) или [Office 365](http://portal.office.com/myapps)) toosign в. Дополнительные сведения о различных типах hello единого входа и их взаимодействий с пользователем в [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

Еще одним ценным ресурсом является *подавление согласие пользователя* в hello [Guiding разработчики](active-directory-applications-guiding-developers-for-lob-applications.md) статьи.

## <a name="next-steps"></a>Дальнейшие действия
Для приложений SaaS, которые можно найти в коллекции приложений hello, Azure AD предоставляет ряд [учебники по приложениям SaaS toointegrate](active-directory-saas-tutorial-list.md).

Если приложение не существует в коллекции приложений, вы можете [добавить toohello коллекции приложений Azure AD как пользовательское приложение](http://blogs.technet.com/b/ad/archive/2015/06/17/bring-your-own-app-with-azure-ad-self-service-saml-configuration-gt-now-in-preview.aspx).

Есть гораздо более подробно описывается все эти проблемы в библиотеке Azure.com hello, начиная с версии [доступ к приложению и единый вход в Azure Active Directory?](active-directory-appssoaccess-whatis.md).

Кроме того, не пропустите hello [статей, посвященных для управления приложениями в Azure Active Directory](active-directory-apps-index.md).
