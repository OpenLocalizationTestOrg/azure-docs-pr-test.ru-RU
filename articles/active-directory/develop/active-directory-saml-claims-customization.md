---
title: "aaaCustomizing утверждения, выданные в hello маркер SAML для предварительно интегрированных приложений в Azure Active Directory | Документы Microsoft"
description: "Узнайте, как toocustomize hello утверждений, выданных в hello маркер SAML для предварительно интегрированных приложений в Azure Active Directory"
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: f1daad62-ac8a-44cd-ac76-e97455e47803
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jeedes
ms.custom: aaddev
ms.openlocfilehash: a376318929472403e799f02fdd3fbddc91d0a70c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="customizing-claims-issued-in-hello-saml-token-for-pre-integrated-apps-in-azure-active-directory"></a>Настройка утверждений, выданных hello маркер SAML для предварительно интегрированных приложений в Azure Active Directory
Сегодня в Azure Active Directory поддерживает тысяч предварительно интегрированных приложений в hello коллекции приложений Azure AD, включая более 360, который поддерживает единый вход с использованием протокола hello SAML 2.0. При прохождении пользователем проверки подлинности tooan приложения с помощью Azure AD с помощью SAML, Azure AD отправляет токен toohello приложения (с помощью HTTP POST). И приложения hello проверяет и использует вместо запроса имени пользователя и пароля пользователя hello маркера toolog hello в. Эти маркеры SAML содержат части сведений о пользователе hello, называется «утверждения».

Сведения о том, поставщик удостоверений о пользователе в маркер hello ими для этого пользователя в удостоверения языком, «утверждения». В [маркер SAML](http://en.wikipedia.org/wiki/SAML_2.0), эти данные обычно содержится в hello оператор атрибута SAML. Hello уникальный идентификатор пользователя обычно представлено в приветствия субъекта SAML, который также называется как имя идентификатора.

По умолчанию для приложения tooyour маркера SAML, содержащего утверждения NameIdentifier, со значением hello пользователя (AKA имя участника-пользователя) в Azure AD выдает Azure Active Directory. Это значение может идентифицировать пользователя hello. маркер SAML Hello также содержит дополнительные утверждения, содержащего адрес электронной почты пользователя hello, имя и фамилию.

tooview или изменить hello утверждения выдаются в hello приложения toohello маркера SAML, откройте hello приложения на портале Azure. Выберите hello **представление и редактировать все остальные атрибуты пользователя** флажок в hello **атрибуты пользователя** раздела приложения hello.

![Раздел "Атрибуты пользователя"][1]

Существует две возможные причины, почему вам необходимо tooedit hello утверждений, выданных в маркер SAML hello.
* Hello приложение было написано toorequire другой набор утверждений идентификаторы URI или значения утверждений.
* в результате которого требуется toobe утверждения NameIdentifier hello нечто, отличное от имени пользователя hello (AKA имя участника-пользователя) в Azure Active Directory развертывания приложения Hello.

Можно изменять значения утверждений по умолчанию hello. Выберите строку hello утверждения в таблице атрибутов токена SAML hello. При этом откроется hello **изменение атрибута** раздела, а затем можно изменить имя утверждения, значение и пространство имен, связанное с утверждением hello.

![Изменение атрибута пользователя][2]

Можно также удалить утверждения (кроме NameIdentifier), с помощью hello контекстного меню, которое открывается щелчком hello **...**  значок.  Можно также добавить новые утверждения с помощью hello **добавить атрибут** кнопки.

![Изменение атрибута пользователя][3]

## <a name="editing-hello-nameidentifier-claim"></a>Редактирование утверждения NameIdentifier hello
проблема toosolve hello, где был развернут приложения hello с использованием различных имен пользователей, щелкайте hello **идентификатор пользователя** раскрывающийся список в hello **атрибуты пользователя** раздела. Это действие выводит диалоговое окно с несколькими различными параметрами:

![Изменение атрибута пользователя][4]

В hello раскрывающийся список, выберите **user.mail** tooset hello NameIdentifier утверждения адреса электронной почты пользователя toobe hello в каталоге hello. Также можно выбрать **user.onpremisessamaccountname** имя учетной записи SAM tooset toohello пользователя, который был синхронизирован из локальной Azure AD.

Можно также использовать специальные hello **ExtractMailPrefix()** суффикс домена hello tooremove функции hello адрес электронной почты, имя учетной записи SAM или имя участника-пользователя hello. После этого выполняется извлечение только первую часть hello hello пользователя имя, передаваемых через (например, «joe_smith» вместо joe_smith@contoso.com).

![Изменение атрибута пользователя][5]

Теперь также добавлена hello **join()** функция toojoin hello проверенного домена со значением идентификатора пользователя hello. При выборе функции join() hello в hello **идентификатор пользователя** сначала выберите Здравствуйте идентификатор пользователя, такие как электронная почта адреса или имени участника пользователя, а затем в hello второго раскрывающегося списка выберите проверенного домена. Если выбрать hello адрес электронной почты с hello проверенного домена, то Azure AD hello username извлекает из первого joe_smith значение hello из joe_smith@contoso.com и добавляет его к contoso.onmicrosoft.com. См. следующий пример hello.

![Изменение атрибута пользователя][6]

## <a name="adding-claims"></a>Добавление утверждений
При добавлении утверждения, можно указать имя атрибута hello (который не требует строго toofollow шаблон URI, согласно спецификации SAML hello). Задайте атрибут пользователя tooany значение hello, хранятся в каталоге hello.

![Добавление атрибута пользователя][7]

Например, нужно toosend отдела hello, hello пользователь принадлежит tooin своей организации в качестве утверждения (например, «продажи»). Введите имя утверждения hello, как ожидалось, приложение hello, а затем выберите **user.department** как значение hello.

> [!NOTE]
> Если для данного пользователя нет значения для выбранного атрибута, затем это утверждение уже не выдается в маркере hello.

> [!TIP]
> Hello **user.onpremisesecurityidentifier** и **user.onpremisesamaccountname** поддерживаются только в том случае, когда синхронизация данных пользователя из локальной Active Directory с помощью hello [Azure Средства AD Connect](../active-directory-aadconnect.md).

## <a name="restricted-claims"></a>Утверждения с ограниченным доступом

В SAML существует ряд утверждений с ограниченным доступом. Если добавить эти утверждения, то Azure AD не будет их отправлять. Ниже приведены hello SAML ограниченный набор утверждений:

    | Тип утверждения (URI) |
    | ------------------- |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/expiration |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/expired |
    | http://schemas.microsoft.com/identity/claims/accesstoken |
    | http://schemas.microsoft.com/identity/claims/openid2_id |
    | http://schemas.microsoft.com/identity/claims/identityprovider |
    | http://schemas.microsoft.com/identity/claims/objectidentifier |
    | http://schemas.microsoft.com/identity/claims/puid |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier[MR1] |
    | http://schemas.microsoft.com/identity/claims/tenantid |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationinstant |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod |
    | http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/groups |
    | http://schemas.microsoft.com/claims/groups.link |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/role |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/wids |
    | http://schemas.microsoft.com/2014/09/devicecontext/claims/iscompliant |
    | http://schemas.microsoft.com/2014/02/devicecontext/claims/isknown |
    | http://schemas.microsoft.com/2012/01/devicecontext/claims/ismanaged |
    | http://schemas.microsoft.com/2014/03/psso |
    | http://schemas.microsoft.com/claims/authnmethodsreferences |
    | http://schemas.xmlsoap.org/ws/2009/09/identity/claims/actor |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/samlissuername |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/confirmationkey |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/primarygroupsid |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/claims/authorizationdecision |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/claims/authentication |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/claims/sid |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/denyonlyprimarygroupsid |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/denyonlyprimarysid |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/claims/denyonlysid |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/denyonlywindowsdevicegroup |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsdeviceclaim |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsdevicegroup |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsfqbnversion |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/windowssubauthority |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsuserclaim |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/claims/x500distinguishedname |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/claims/spn |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/ispersistent |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/claims/privatepersonalidentifier |
    | http://schemas.microsoft.com/identity/claims/scope |

## <a name="next-steps"></a>Дальнейшие действия
* [Указатель статьей по управлению приложениями в Azure Active Directory](../active-directory-apps-index.md)
* [Настройка одного tooapplications входа, которых нет в коллекции приложений Azure Active Directory hello](../active-directory-saas-custom-apps.md)
* [Устранение неполадок единого входа на основе SAML](active-directory-saml-debugging.md)

<!--Image references-->
[1]: ./media/active-directory-saml-claims-customization/user-attribute-section.png
[2]: ./media/active-directory-saml-claims-customization/edit-claim-name-value.png
[3]: ./media/active-directory-saml-claims-customization/delete-claim.png
[4]: ./media/active-directory-saml-claims-customization/user-identifier.png
[5]: ./media/active-directory-saml-claims-customization/extractemailprefix-function.png
[6]: ./media/active-directory-saml-claims-customization/join-function.png
[7]: ./media/active-directory-saml-claims-customization/add-attribute.png