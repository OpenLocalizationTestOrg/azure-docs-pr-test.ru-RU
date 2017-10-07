---
title: "aaaError на странице приложения после входа в систему | Документы Microsoft"
description: "Как tooresolve проблемы, связанные с Azure AD выполнять вход при само приложение hello выдает ошибку"
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
ms.openlocfilehash: 317b6f8e6417520ead80ae4e26c591ba6b134683
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="error-on-an-applications-page-after-signing-in"></a>Ошибка на странице приложения после входа

В этом случае вход пользователя hello в Azure AD, но приложение hello отображает ошибку, не допускающей hello пользователя toosuccessfully Готово hello знак в поток. В этом сценарии приложение hello не принимает hello ответа проблему по Azure AD.

Существуют некоторые возможные причины, почему приложение hello не приняли hello ответа от Azure AD. Если ошибка hello в приложении hello не является достаточно tooknow что отсутствует в ответе hello затем:

-   Если приложение hello коллекции hello Azure AD, проверьте, были выполнены все шаги hello в статье hello [как toodebug на основе SAML единого входа tooapplications в Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saml-debugging).

-   Использование таких средств, как [Fiddler](http://www.telerik.com/fiddler) toocapture SAML запрос, ответ SAML и маркера SAML.

-   Предоставить ответ SAML hello tooknow поставщика приложения hello недостатков.

## <a name="missing-attributes-in-hello-saml-response"></a>Недостающие атрибуты в ответе SAML hello

tooadd атрибута в конфигурации toobe hello Azure AD, отправляемый в ответ hello Azure AD, выполните шаги hello.

1.  Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора** или **Co-администратору.**

2.  Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.

3.  Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.

4.  Нажмите кнопку **корпоративных приложений** из Azure Active Directory hello левого меню навигации.

5.  Нажмите кнопку **все приложения** tooview список всех приложений.

   * Используйте hello, если нужно показать здесь приложения hello не отображается, **фильтра** управления вверху hello hello **список всех приложений** и набор hello **Показать** параметр слишком **Все приложения.**

6.  Выберите приложение hello, требуется tooconfigure единого входа.

7.  После загрузки приложения hello щелкните hello **единого входа** из приложения hello левого меню навигации.

8.  Нажмите кнопку **Просмотр и изменение атрибутов всех других пользователей в группе** hello **атрибуты пользователя** hello tooedit разделе атрибуты приложения toohello toobe отправляются в маркере SAML hello при входе пользователя.

   tooadd атрибута:

   * Нажмите кнопку **Добавить атрибут**. Введите hello **имя** и выберите hello hello **значение** из раскрывающегося списка hello.

   * Нажмите кнопку **Сохранить**. Вы увидите новый атрибут hello в таблице hello.

9.  Сохранение конфигурации hello.

Очередном входе hello в приложении toohello Azure AD отправляет новый атрибут hello в hello ответ SAML.

## <a name="hello-application-expects-a-different-user-identifier-value-or-format"></a>приложение Hello ожидает другое значение идентификатора пользователя или в другом формате

Hello toohello входа в приложения происходит сбой, так как hello ответ SAML отсутствует атрибуты, такие как роли или приложение hello ожидает один из форматов для атрибута EntityID hello.

## <a name="add-an-attribute-in-hello-azure-ad-application-configuration"></a>Добавьте атрибут в конфигурации приложения hello Azure AD:

hello toochange значение идентификатора пользователя, выполните шаги hello.

1.  Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора** или **Co-администратору.**

2.  Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.

3.  Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.

4.  Нажмите кнопку **корпоративных приложений** из Azure Active Directory hello левого меню навигации.

5.  Нажмите кнопку **все приложения** tooview список всех приложений.

   * Используйте hello, если нужно показать здесь приложения hello не отображается, **фильтра** управления вверху hello hello **список всех приложений** и набор hello **Показать** параметр слишком **Все приложения.**

6.  Выберите приложение hello, требуется tooconfigure единого входа.

7.  После загрузки приложения hello щелкните hello **единого входа** из приложения hello левого меню навигации.

8.  В разделе hello **атрибуты пользователя**, выберите hello уникальный идентификатор для пользователей в hello **идентификатор пользователя** раскрывающегося списка.

## <a name="change-entityid-user-identifier-format"></a>Изменение формата идентификатора EntityID (идентификатора пользователя)

Если приложение hello и ожидает другого формата для атрибута EntityID hello. Затем не будет возможности tooselect hello EntityID (идентификатор пользователя) формат, что Azure AD отправляет toohello приложения hello ответа после проверки подлинности пользователя.

Azure AD выберите hello формат hello идентификатора имени атрибута (идентификатор пользователя) на основе выбранного значения hello или hello формат, запрошенный приложением hello в hello SAML AuthRequest. Дополнительные сведения можно найти в статье hello [протокола SAML](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) под hello статьи политики идентификатора имени.

## <a name="hello-application-expects-a-different-signature-method-for-hello-saml-response"></a>приложение Hello ожидает другой сигнатурой метода для hello ответ SAML

toochange того, какие части маркера SAML hello цифровой подписи Azure Active Directory. Выполните следующие действия hello.

1.  Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора** или **Co-администратору.**

2.  Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.

3.  Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.

4.  Нажмите кнопку **корпоративных приложений** из Azure Active Directory hello левого меню навигации.

5.  Нажмите кнопку **все приложения** tooview список всех приложений.

  * Используйте hello, если нужно показать здесь приложения hello не отображается, **фильтра** управления вверху hello hello **список всех приложений** и набор hello **Показать** параметр слишком **Все приложения.**

6.  Выберите приложение hello, требуется tooconfigure единого входа.

7.  После загрузки приложения hello щелкните hello **единого входа** из приложения hello левого меню навигации.

8.  Нажмите кнопку **Показывать дополнительные параметры подписи сертификата** под hello **сертификат подписи SAML** раздела.

9.  Выберите hello соответствующие **подписи параметр** ожидаемый приложения hello:

  * Ответ знака SAML

  * Ответ знака SAML и утверждение

  * Утверждение знака SAML

Очередном входе hello в приложении toohello входа Azure AD hello часть выбран ответ SAML hello.

## <a name="hello-application-expects-hello-signing-algorithm-toobe-sha-1"></a>приложение Hello ожидает hello подписи toobe алгоритм SHA-1

По умолчанию Azure AD подписывает маркер SAML hello, с помощью hello большинство алгоритмов безопасности. Изменение алгоритма входа hello tooSHA-1 не рекомендуется, если только приложение hello.

toochange hello алгоритм подписи, выполните следующие действия hello.

1.  Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора** или **Co-администратору.**

2.  Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.

3.  Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.

4.  Нажмите кнопку **корпоративных приложений** из Azure Active Directory hello левого меню навигации.

5.  Нажмите кнопку **все приложения** tooview список всех приложений.

   * Используйте hello, если нужно показать здесь приложения hello не отображается, **фильтра** управления вверху hello hello **список всех приложений** и набор hello **Показать** параметр слишком **Все приложения.**

6.  Выберите приложение hello, требуется tooconfigure единого входа.

7.  После загрузки приложения hello щелкните hello **единого входа** из приложения hello левого меню навигации.

8.  Нажмите кнопку **Показывать дополнительные параметры подписи сертификата** под hello **сертификат подписи SAML** раздела.

9.  Выберите алгоритм SHA-1, в hello **алгоритм подписи**.

При очередном Здравствуйте, которым пользователь входит в приложении toohello, входа Azure AD hello маркер SAML с помощью алгоритма SHA-1.

## <a name="next-steps"></a>Дальнейшие действия
[Как toodebug на основе SAML единого входа tooapplications в Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saml-debugging)
