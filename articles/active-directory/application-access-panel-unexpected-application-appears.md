---
title: "aaaHow приложения отображаются на панели доступа hello | Документы Microsoft"
description: "Устранение неполадок, поэтому приложения, отображаются в панели доступа hello"
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
ms.reviewr: japere
ms.openlocfilehash: 14ee732c4ed5260cba878e949cf9d90877aee67e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-applications-appear-on-hello-access-panel"></a>Как приложения отображаются на панели доступа hello

Hello панель доступа является Интернет-порталом, который позволяет пользователю с помощью рабочей или рабочую учетную запись в Azure Active Directory (Azure AD) tooview и запуск облачных приложений, hello администратор Azure AD им предоставлен доступ. Эти приложения настроены от имени пользователя hello hello портала Azure AD. Здравствуйте, администратор может подготовить пользователя toohello приложения hello напрямую или пользователь является частью приведет к приложения hello, отображаемых на панели доступа пользователя hello tooa группы.

## <a name="general-issues-toocheck-first"></a>Общие проблемы toocheck сначала

-   Если приложение только что был удален из пользователь или группа hello пользователь является членом, повторите toosign и выхода из системы в hello пользовательской панели доступа после нескольких минут toosee при удалении приложения hello.

-   Если лицензия только что был удален из пользователь или группа hello пользователь является членом это может занять много времени, в зависимости от hello размера и сложности hello группы для toobe изменения внесены. Разрешить дополнительное время, прежде чем войти в панель доступа hello.

## <a name="problems-related-tooassigning-applications-toousers"></a>Проблемы tooassigning связанных приложений toousers

Пользователь может отображается приложения на своей панели доступа потому, что они ей ранее была назначена tooit. Ниже приведены некоторые способы toocheck.

-   [Проверьте, если пользователю назначено toohello приложения](#check-if-a-user-is-assigned-to-the-application)

-   [Проверьте, является ли пользователь по лицензии связанных toohello приложения](#check-if-a-user-is-under-a-license-related-to-the-application)


### <a name="check-if-a-user-is-assigned-toohello-application"></a>Проверьте, если пользователю назначено toohello приложения

toocheck, если пользователю назначено toohello приложения, следуйте инструкциям hello:

1.  Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора.**

2.  Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.

3.  Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.

4.  Нажмите кнопку **корпоративных приложений** из Azure Active Directory hello левого меню навигации.

5.  Нажмите кнопку **все приложения** tooview список всех приложений.

6.  **Поиск** для hello имя приложения hello в вопросе.

7.  Выберите пункт **Пользователи и группы**.

8.  Проверьте toosee, если пользователю назначено toohello приложения.

  * Если требуется, чтобы пользователь hello tooremove из приложения hello **щелкните строку hello** пользователя hello и выберите **удалить**.

### <a name="check-if-a-user-is-under-a-license-related-toohello-application"></a>Проверьте, является ли пользователь по лицензии связанных toohello приложения

toocheck пользователя назначить лицензии, выполните следующие действия hello:

1.  Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора.**

2.  Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.

3.  Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.

4.  Нажмите кнопку **пользователей и групп** в меню навигации hello.

5.  Щелкните **Все пользователи**.

6.  **Поиск** для вас интересуют пользователя hello и **щелкните строку hello** tooselect.

7.  Нажмите кнопку **лицензий** toosee hello какие лицензии пользователя в настоящее время назначено.

   * Здравствуйте, если hello пользователю назначается лицензия Office tooan это включить tooappear приложений первой стороной Office на панели доступа пользователя.

## <a name="problems-related-tooassigning-applications-toogroups"></a>Проблемы tooassigning связанных приложений toogroups

Пользователь видите приложения на своей панели доступа, так как они являются частью группы, имеющей разрешение приложения hello. Ниже приведены некоторые способы toocheck.

-   [Проверка членства пользователя в группах](#check-a-users-group-memberships)

-   [Установите флажок, если пользователь является членом группы, назначает tooa лицензию](#check-if-a-user-is-a-member-of-a-group-assigned-to-a-license)

### <a name="check-a-users-group-memberships"></a>Проверка членства пользователя в группах

toocheck членство в группе, выполните следующие действия hello:

1.  Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора.**

2.  Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.

3.  Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.

4.  Нажмите кнопку **пользователей и групп** в меню навигации hello.

5.  Щелкните **Все пользователи**.

6.  **Поиск** для вас интересуют пользователя hello и **щелкните строку hello** tooselect.

7.  Щелкните **Группы**.

8.  Проверка toosee, если пользователь входит в состав группы назначить toohello приложения.

   * Если требуется, чтобы tooremove hello пользователя из группы hello **щелкните строку hello** hello группы и выберите Удалить.

### <a name="check-if-a-user-is-a-member-of-a-group-assigned-tooa-license"></a>Установите флажок, если пользователь является членом группы, назначает tooa лицензию

1.  Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора.**

2.  Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.

3.  Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.

4.  Нажмите кнопку **пользователей и групп** в меню навигации hello.

5.  Щелкните **Все пользователи**.

6.  **Поиск** для вас интересуют пользователя hello и **щелкните строку hello** tooselect.

7.  Щелкните **Группы**.

8.  Щелкните строку hello в определенную группу.

9.  Нажмите кнопку **лицензий** toosee, какую группу лицензий hello назначила tooit.

  * Здравствуйте, если группа hello назначена лицензия Office tooan, это может включить определенные tooappear приложений первой стороной Office на панели доступа пользователя.


## <a name="if-these-troubleshooting-steps-do-not-hello-resolve-hello-issue"></a>Если эти действия по устранению неполадок не hello устраните проблему hello

Откройте запрос в службу поддержки с hello следующую информацию, если они доступны:

-   идентификатор ошибки корреляции;

-   имя участника-пользователя (адрес электронной почты пользователя);

-   Tenant ID

-   тип браузера;

-   часовой пояс и время или отрезок времени возникновения ошибки;

-   трассировки Fiddler.

## <a name="next-steps"></a>Дальнейшие действия
[Управление приложениями с помощью Azure Active Directory](active-directory-enable-sso-scenario.md)
