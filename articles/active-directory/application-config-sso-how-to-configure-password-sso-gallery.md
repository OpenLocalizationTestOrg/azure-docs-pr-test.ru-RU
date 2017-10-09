---
title: "aaaHow tooconfigure пароля единого входа для приложения Azure AD коллекции | Документы Microsoft"
description: "Как tooconfigure приложения для защиты на основе пароля единого входа при уже присутствует в коллекции приложений Azure AD hello"
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
ms.openlocfilehash: 7a93bff119b477d946368686fc2d9006ca2722a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-password-single-sign-on-for-an-azure-ad-gallery-application"></a>Как tooconfigure пароля единого входа для приложения Azure AD коллекции

При добавлении приложения из hello [коллекции приложений Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery), у вас есть выбор способа вашей toosign пользователей в приложении toothat hello. Этот выбор можно настроить в любое время, выбрав hello **Single Sign-on** элемент навигации в приложении предприятия в hello [портала Azure](https://portal.azure.com/).

Один из доступных tooyou методы-hello — hello [паролю Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) параметр. Это отличный способ tooget запущен быстро интеграция приложений в Azure AD и позволяет:

-   Включить **единого входа для пользователей** с помощью безопасного хранения и воспроизведения, имена пользователей и пароли для приложения hello интегрированы с Azure AD

-   **Поддерживает приложения, которые требуют нескольких полей** для приложений, требующих больше, чем просто имя пользователя и пароль поля toosign в

-   **Настройка меток hello** hello имя пользователя и пароль полей ввода видят пользователи на hello [панели доступа приложений](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) при вводе учетных данных

-   Разрешить вашей **пользователей** tooprovide свои имена пользователей и пароли для любых существующих учетных записей приложения вводе в вручную на hello [приложения панели доступа](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)

-   Разрешить **членом hello бизнес-группы** toospecify hello пользователя и пароль назначенный пользователь tooa с помощью hello [самообслуживания доступ к приложению](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) функции

-   Разрешить **администратора** toospecify hello пользователя и пароль, назначенный пользователь tooa, используя учетные данные обновления hello компонент при [назначения пользовательского приложения tooan](#assign-a-user-to-an-application-directly)

-   Разрешить **администратора** toospecify hello общего пользователя или пароль, используемый группой пользователей, используя учетные данные обновления hello компонент при [назначение приложении tooan группы](#assign-an-application-to-a-group-directly)

Ниже описывается, как включить [паролю Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) tooan приложение, которое уже находится в hello [коллекции приложений Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery).

## <a name="overview-of-steps-required"></a>Обзор необходимых действий
tooconfigure приложение из коллекции hello Azure AD необходимо:

-   [Добавить приложение из коллекции hello Azure AD.](#add-an-application-from-the-azure-ad-gallery)

-   [Настройка приложения hello для пароля единого входа](#configure-the-application-for-password-single-sign-on)

-   [Назначить hello приложения tooa пользователя или группы](#assign-the-application-to-a-user-or-a-group)

    -   [Назначение приложения tooan пользователя напрямую](#assign-a-user-to-an-application-directly)

    -   [Назначение группе tooa приложения напрямую](#assign-an-application-to-a-group-directly)

## <a name="add-an-application-from-hello-azure-ad-gallery"></a>Добавить приложение из коллекции hello Azure AD.

tooadd приложения hello коллекции Azure AD, выполните шаги hello.

1.  Откройте hello [портала Azure](https://portal.azure.com) и войдите как **глобального администратора** или **соадминистратору**

2.  Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.

3.  Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.

4.  Нажмите кнопку **корпоративных приложений** из Azure Active Directory hello левого меню навигации.

5.  Нажмите кнопку hello **добавить** кнопку в правом верхнем углу hello на hello **корпоративных приложений** колонку

6.  В hello **введите имя** текстового поля из hello **добавить из галереи hello** раздел, имя типа hello приложения hello

7.  Выберите hello приложение tooconfigure для единого входа

8.  Перед добавлением приложения hello, можно изменить его имя из hello **имя** текстового поля.

9.  Нажмите кнопку **добавить** кнопки, приложение hello tooadd.

После краткого периода быть колонке конфигурации приложения может toosee hello.

## <a name="configure-hello-application-for-password-single-sign-on"></a>Настройка приложения hello для пароля единого входа

tooconfigure единого входа для приложения, выполните следующие действия hello.

1.  Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора** или **Co-администратору.**

2.  Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.

3.  Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.

4.  Нажмите кнопку **корпоративных приложений** из Azure Active Directory hello левого меню навигации.

5.  Нажмите кнопку **все приложения** tooview список всех приложений.

  * Используйте hello, если нужно показать здесь приложения hello не отображается, **фильтра** управления вверху hello hello **список всех приложений** и набор hello **Показать** параметр слишком **Все приложения.**

6.  Выберите hello приложение tooconfigure единого входа

7.  После загрузки приложения hello щелкните hello **единого входа** из приложения hello левого меню навигации.

8.  Режим выбора hello **входа на базе пароля.**

9.  [Назначить пользователей приложения toohello](#assign-a-user-to-an-application-directly).

10. Кроме того, можно также ввести учетные данные имени пользователя, hello, при выборе строк hello пользователей hello и выбрав **учетные данные обновления** и введя hello имя пользователя и пароль от лица пользователей hello. В противном случае пользователи быть запрашиваемые tooenter hello учетные данные сами при запуске.

## <a name="assign-a-user-tooan-application-directly"></a>Назначение приложения tooan пользователя напрямую

tooassign один или несколько приложений пользователи tooan напрямую, выполните шаги hello:

1.  Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора.**

2.  Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.

3.  Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.

4.  Нажмите кнопку **корпоративных приложений** из Azure Active Directory hello левого меню навигации.

5.  Нажмите кнопку **все приложения** tooview список всех приложений.

  * Используйте hello, если нужно показать здесь приложения hello не отображается, **фильтра** управления вверху hello hello **список всех приложений** и набор hello **Показать** параметр слишком **Все приложения.**

6.  Выберите hello приложение tooassign список пользователей toofrom hello.

7.  После загрузки приложения hello щелкните **пользователей и групп** из приложения hello левого меню навигации.

8.  Щелкните hello **добавить** кнопки на hello **пользователей и групп** hello список tooopen **добавить назначение** колонку.

9.  Нажмите кнопку hello **пользователей и групп** селектор из hello **добавить назначение** колонку.

10. Тип в hello **полное имя** или **адрес электронной почты** hello пользователя вы заинтересованы в назначение в hello **поиск по имени или адресу электронной почты** поле поиска.

11. Наведите указатель мыши на hello **пользователя** в список tooreveal hello **флажок**. Щелкните tooadd логотипа или фотографию профиля hello флажок Далее toohello пользователя вашего пользователя toohello **выбранные** списка.

12. **Необязательно:** при желании слишком**добавить более одного пользователя**, тип в другой **полное имя** или **адрес электронной почты** в hello **поиск по имени или адрес электронной почты** поле поиска, щелкните флажок tooadd hello этого пользователя toohello **выбранные** списка.

13. После завершения выбора пользователей, нажмите кнопку hello **выберите** кнопку tooadd их toohello список пользователей и групп toobe назначенное toohello приложение.

14. **Необязательно:** щелкните hello **выберите роль** селектора в hello **добавить назначение** tooselect колонке роли пользователей toohello tooassign выбора.

15. Нажмите кнопку hello **назначить** toohello приложения hello tooassign кнопку выбранных пользователей.

## <a name="assign-an-application-tooa-group-directly"></a>Назначение группе tooa приложения напрямую

tooassign один или несколько групп tooan приложению напрямую, выполните следующие действия hello.

1.  Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора.**

2.  Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.

3.  Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.

4.  Нажмите кнопку **корпоративных приложений** из Azure Active Directory hello левого меню навигации.

5.  Нажмите кнопку **все приложения** tooview список всех приложений.

  * Используйте hello, если нужно показать здесь приложения hello не отображается, **фильтра** управления вверху hello hello **список всех приложений** и набор hello **Показать** параметр слишком **Все приложения.**

6.  Выберите hello приложение tooassign список пользователей toofrom hello.

7.  После загрузки приложения hello щелкните **пользователей и групп** из приложения hello левого меню навигации.

8.  Щелкните hello **добавить** кнопки на hello **пользователей и групп** hello список tooopen **добавить назначение** колонку.

9.  Нажмите кнопку hello **пользователей и групп** селектор из hello **добавить назначение** колонку.

10. Тип в hello **имя полного группы** вы заинтересованы в назначение в hello группы hello **поиск по имени или адресу электронной почты** поле поиска.

11. Наведите указатель мыши на hello **группы** в список tooreveal hello **флажок**. Нажмите кнопку tooadd hello флажок Далее toohello группы профиля фотографию или логотип вашей toohello пользователя **выбранные** списка.

12. **Необязательно:** при желании слишком**добавить несколько групп**, тип в другой **имя полного группы** в hello **поиск по имени или адресу электронной почты** поле поиска и нажмите кнопку флажок tooadd hello этой группы toohello **выбранные** списка.

13. После завершения выбора групп, нажмите кнопку hello **выберите** кнопку tooadd их toohello список пользователей и групп toobe назначенное toohello приложение.

14. **Необязательно:** щелкните hello **выберите роль** селектора в hello **добавить назначение** вами группах колонке tooselect toohello tooassign роли выбранных.

15. Нажмите кнопку hello **назначить** toohello приложения hello tooassign кнопку выбранные группы.

После краткого периода hello пользователей, которые вы выбрали может toolaunch эти приложения в hello панели доступа.

## <a name="next-steps"></a>Дальнейшие действия
[Создавайте приложения tooyour, прокси-сервера приложений](active-directory-application-proxy-sso-using-kcd.md)
