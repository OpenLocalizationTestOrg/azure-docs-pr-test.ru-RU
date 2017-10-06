---
title: "aaaUnexpected приложения в списке приложений | Документы Microsoft"
description: "Как toosee все приложения в клиенте и понять, как приложения отображаются в списке всех приложений в группе корпоративных приложений"
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
ms.openlocfilehash: 2f974046b655bc36a05f002c56511a8a988cd01c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="unexpected-application-in-my-applications-list"></a>Неожиданные приложения в списке приложений

В этой статье помогут toounderstand отображением приложений в вашей **все приложения** в разделе **корпоративных приложений**. 

## <a name="how-toosee-all-applications-in-your-tenant"></a>Как toosee все приложения в клиенте

toosee все Здравствуйте приложения в клиенте, необходимо toouse hello **фильтра** управления tooshow **все приложения** под hello **всех приложений** списка. toodo это, выполните hello шаги:

1.  Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора** или **Co-администратору.**

2.  Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.

3.  Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.

4.  Нажмите кнопку **корпоративных приложений** из Azure Active Directory hello левого меню навигации.

5.  Нажмите кнопку **все приложения** tooview список всех приложений.

6.  Нажмите кнопку hello используйте hello **фильтра** управления вверху hello hello **список всех приложений**.

7.  На hello **фильтра** колонки, набор hello **Показать** параметр слишком**всех приложений.**

## <a name="why-does-a-specific-application-appear-in-my-all-applications-list"></a>Почему приложение появляется в моем списке всех приложений?

При фильтрации слишком**все приложения**, hello **все приложения** **списка** отображается каждый объект субъекта-службы в клиенте. Объекты участников-служб могут попадать в этот список разными способами.

1.  При добавлении любого приложения из галереи приложения hello, включая:

   1. **Приложения из коллекции Azure AD** — это предварительно интегрированные приложения для единого входа через Azure AD.

   2. **Прокси-сервер приложений-приложения** — приложения, работающего в локальной среде, которые должны tooprovide безопасный единый вход в tooexternally.

   3. **Сторонних разрабатываемых приложений** — приложение, ваша организация хочет toodevelop на hello платформы разработки приложений Azure AD, но который еще не существует.

   4. **Приложения не из коллекции** — собственные приложения. Любой веб-ссылка нужные или любого приложения, в которой отображается поле имени пользователя и пароля, поддерживает протокол SAML или OpenID Connect или поддерживает SCIM, который вы хотите toointegrate для единого входа в Azure AD.

2.  При регистрации или входе в систему<sup> в п</sup>риложении стороннего разработчика, интегрированном с Azure Active Directory. Примерами таких приложений являются [Smartsheet](https://app.smartsheet.com/b/home) или [DocuSign](https://www.docusign.net/member/MemberLogin.aspx).

3.  При регистрации, или добавление tooa лицензии пользователя или группы tooa первой стороной приложения, таких как [Microsoft Office 365](http://products.office.com/).

4.  При добавлении новой записи регистрации приложения, создав сторонних разрабатываемых приложений, с помощью hello [Application Registry](https://docs.microsoft.com/azure/active-directory/active-directory-app-registration).

5.  При добавлении новой записи регистрации приложения, создав сторонних разрабатываемых приложений, с помощью hello [портала регистрации приложения V2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-app-registration#visit-the-microsoft-app-registration-portal).

6.  При добавлении приложения, которое вы разрабатываете с помощью [методов аутентификации ASP.net](http://www.asp.net/visual-studio/overview/2013/creating-web-projects-in-visual-studio#orgauthoptions) или [подключенных служб](http://blogs.msdn.com/b/visualstudio/archive/2014/11/19/connecting-to-cloud-services.aspx) Visual Studio.

7.  При создании объекта участника службы с помощью hello [модуля Azure AD PowerShell](/powershell/azure/install-adv2?view=azureadps-2.0).

8.  Когда вы [согласия приложения tooan](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) виде toouse администратора в клиенте.

9.  Когда [согласии пользователя приложение tooan](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) toouse данных в клиенте.

10. При включении определенных служб, которые хранят данные в клиенте. Примером этого может сбросить пароль, который моделируется как toostore участника службы для сброса пароля политики безопасно.

прочитать дополнительные сведения о приложениях способ добавления каталога tooyour tooget [как и почему приложения добавляются tooAzure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-how-applications-are-added).

## <a name="i-want-tooremove-a-specific-users-or-groups-assignment-tooan-application"></a>Я хочу tooremove приложения tooan назначения определенного пользователя или группы

tooremove пользователь или группа назначения tooan приложении, выполните действия hello, перечисленные в hello [удалить назначение пользователя или группу из корпоративного приложения в Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) статьи.

## <a name="i-want-toodisable-all-access-tooan-application-for-every-user"></a>Я хочу toodisable все приложения tooan доступа для каждого пользователя

toodisable все приложение tooan входа в систему пользователя, выполните шаги hello, указанные в hello [отключить пользователя войти в приложение в Azure Active Directory предприятия](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) статьи.

## <a name="i-want-toodelete-an-application-entirely"></a>Я хочу toodelete приложение полностью

слишком**удалить приложение**, следуйте приведенным ниже инструкциям hello:

1.  Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора** или **Co-администратору.**

2.  Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.

3.  Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.

4.  Нажмите кнопку **корпоративных приложений** из Azure Active Directory hello левого меню навигации.

5.  Нажмите кнопку **все приложения** tooview список всех приложений.

  * Используйте hello, если нужно показать здесь приложения hello не отображается, **фильтра** управления вверху hello hello **список всех приложений** и набор hello **Показать** параметр слишком **Все приложения.**

6.  Выберите hello приложение toodelete.

7.  После загрузки приложения hello щелкните **удалить** значок в верхнем приложения hello **Обзор** колонку.

## <a name="i-want-toodisable-all-future-user-consent-operations-tooany-application"></a>Я хочу toodisable все будущие пользовательского согласия операций tooany приложения

Отключение согласие пользователя для конечных пользователей из приложения tooany соглашаетесь предотвратить всего каталога. Администратор сохранит возможность предоставлять согласие от имени пользователя. согласие toolearn Дополнительные сведения о приложении, и почему может или не можете toodo, прочитайте [пользователя понимание и согласие администратора](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent).

слишком**отключить все операции согласия будущих пользователя в каталоге всей**, следуйте приведенным ниже инструкциям hello:

1.  Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора.**

2.  Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.

3.  Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.

4.  Нажмите кнопку **пользователей и групп** в меню навигации hello.

5.  Щелкните **Параметры пользователя**.

6.  Отключите все операции согласия пользователя в будущем, установка hello **пользователи разрешают приложениям tooaccess свои данные** переключения слишком**нет** и нажмите кнопку hello **Сохранить** кнопки.

## <a name="next-steps"></a>Дальнейшие действия
[Управление приложениями с помощью Azure Active Directory](active-directory-enable-sso-scenario.md)
