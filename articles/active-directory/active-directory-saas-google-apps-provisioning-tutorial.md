---
title: "Руководство по настройке Google Apps для автоматической подготовки пользователей в Azure | Документация Майкрософт"
description: "Узнайте, как tooautomatically подготовки и Отмена подготовки учетные записи из Azure AD tooGoogle приложений."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6dbd50b5-589f-4132-b9eb-a53a318a64e5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: d1fa8449bd6013d1627b3552aaa19db1c0f4f46f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-google-apps-for-automatic-user-provisioning"></a>Руководство по настройке Google Apps для автоматической подготовки пользователей

Цель этого учебника Hello — tooshow hello шаги требуются tooperform в Google Apps и Azure AD tooautomatically подготовки и отменять подготовки учетных записей пользователей из Azure AD tooGoogle приложений.

## <a name="prerequisites"></a>Предварительные требования

Hello сценарий, описанный в этом руководстве предполагается, что уже hello следующих элементов:

*   клиент Azure Active Directory;
*   Действительный клиент для Google Apps for Work или Google Apps for Education. Для любой из этих служб можно воспользоваться бесплатной пробной учетной записью.
*   Учетная запись пользователя Google Apps с разрешениями администратора команды.

## <a name="assigning-users-toogoogle-apps"></a>Назначение пользователей tooGoogle приложений

Azure Active Directory использует называемый «назначения» toodetermine пользователей, которые должны получать доступ tooselected приложений. В контексте hello автоматический подготовки пользователей. учетной записи синхронизируются только hello пользователей и групп, назначенных» «tooan приложения в Azure AD.

Для настройки и включения hello подготовки службы, требуется toodecide какие пользователи или группы в Azure AD представляют Привет пользователям требуется доступ к приложению tooyour Google Apps. После приняла решение, можно назначить эти приложения пользователям tooyour Google Apps, следуя инструкциям hello: [назначить пользователю или группе tooan корпоративного приложения](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

> [!IMPORTANT]
>*   Рекомендуется один назначить tooGoogle приложений tootest hello настройки подготовки пользователя Azure AD. Дополнительные пользователи и/или группы можно назначить позднее.
>*   При назначении tooGoogle пользователя приложения, необходимо выбрать hello пользователя или роли «Группа» в диалоговом окне приветствия назначения. роль «Доступ по умолчанию» Hello не работает для подготовки.

## <a name="enable-automated-user-provisioning"></a>Включение автоматической подготовки пользователей

Этот раздел поможет выполнить подключение подготовки API учетной записи пользователя приложения tooGoogle Azure AD и настройке подготовки службы toocreate hello, обновления и отключить учетные записи пользователей, назначенные в Google Apps, в зависимости от назначения пользователей и групп в Azure AD .

>[!Tip]
>Можно также выбрать tooenabled на основе SAML Single Sign-On для Google Apps, следуя инструкциям hello в [портал Azure](https://portal.azure.com). Единый вход можно настроить независимо от автоматической подготовки, хотя эти две возможности дополняют друг друга.

### <a name="configure-automatic-user-account-provisioning"></a>Настройка автоматической подготовки учетных записей пользователей

> [!NOTE]
> Другой возможных вариантов для автоматизации приложений tooGoogle подготовки пользователей – toouse [синхронизации каталогов Google Apps (GADS)](https://support.google.com/a/answer/106368?hl=en) которого подготавливает вашей локальной Active Directory удостоверения tooGoogle приложений. В отличие от этого решение hello в этом учебнике подготавливает Azure Active Directory (облако) пользователей и групп с включенной поддержкой почты tooGoogle приложений. 

1. Вход в hello [консоли администрирования приложения Google](http://admin.google.com/) с помощью учетной записи администратора и нажмите кнопку **безопасности**. Если вы не видите ссылку hello, они могут быть скрыты в hello **другие элементы** меню hello нижней части экрана приветствия.
   
    ![Выбор элемента "Безопасность"][10]

2. На hello **безопасности** щелкните **Справочник по API**.
   
    ![Выбор элемента "Справочник по API".][15]

3. Выберите команду **Enable API access**(Включить доступ через API).
   
    ![Выбор элемента "Справочник по API".][16]

    > [!IMPORTANT]
    > Для каждого пользователя, следует присвоить tooprovision tooGoogle приложений, их имена пользователей в Azure Active Directory *должен* быть равноценных tooa пользовательского домена. Например, такие имена пользователей, как bob@contoso.onmicrosoft.com, не будут приняты Google Apps, а bob@contoso.com — будут. Вы можете изменить текущий домен пользователя, изменив его свойства в Azure AD. Инструкции для как tooset пользовательского домена для Azure Active Directory и Google Apps включены в следующие действия.
      
4. Если еще не добавлены tooyour имя пользовательского домена Azure Active Directory, выполните следующие шаги hello:
  
    а. В hello [портал Azure](https://portal.azure.com), на левой панели навигации hello, нажмите кнопку **Active Directory**. В списке каталогов hello выберите свой каталог. 

    b. Нажмите кнопку **имя домена** на левой панели навигации hello и нажмите кнопку **добавить**.
     
     ![Домен](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_1.png)

     ![Добавление домена](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_2.png)

    c. Введите имя домена в hello **доменное имя** поля. Это имя домена должно быть hello таким же именем домена, требуется toouse Google Apps. Когда все будет готово, нажмите кнопку hello **добавить домен** кнопки.
     
     ![Доменное имя](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_3.png)

    d. Нажмите кнопку **Далее** toogo toohello проверки страницы. tooverify, что вы являетесь владельцем этого домена, необходимо изменить записи DNS домена hello в соответствии с toohello значения, представленные на этой странице. Вы можете с помощью tooverify **записей MX** или **записи TXT**, в зависимости от выбора для hello **тип записи** параметр. Более полные инструкции как tooverify имя домена по умолчанию в Azure AD, [добавить собственные tooAzure имя домена AD](https://go.microsoft.com/fwLink/?LinkID=278919&clcid=0x409).
     
     ![Домен](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_4.png)

    д. Повторите hello в предыдущих шагах, для всех доменов hello, следует присвоить tooadd tooyour каталога.

5. После подтверждения всех доменов в Azure AD необходимо подтвердить их в Google Apps. Для каждого домена, который еще не зарегистрирован с Google Apps выполните следующие шаги hello.
   
    а. В hello [консоли администрирования приложения Google](http://admin.google.com/), нажмите кнопку **домены**.
     
     ![Выбор элемента "Домены"][20]

    b. Щелкните **Add a domain or a domain alias**(Добавить домен или псевдоним домена).
     
     ![Добавление нового домена][21]

    c. Выберите **добавить другой домен**и введите имя hello, желательно tooadd домена hello.
     
     ![Ввод доменного имени][22]

    г) Щелкните **Continue and verify domain ownership** (Перейти к проверке владельца домена). Затем выполните шаги tooverify hello, что вы являетесь владельцем hello доменное имя. Для подробных инструкций на tooverify домена с Google Apps. в статье. [Как подтвердить право собственности на сайт](https://support.google.com/webmasters/answer/35179).

    д. Повторите предыдущих шагах для дополнительных доменов, следует присвоить tooadd tooGoogle приложения hello.
     
     > [!WARNING]
     > Если изменить основной домен hello для вашего клиента Google Apps, и если имеется уже настроены единый вход в Azure AD, то у вас есть toorepeat шаг #3 в разделе [два шага: Включение единого входа](#step-two-enable-single-sign-on).
       
6. В hello [консоли администрирования приложения Google](http://admin.google.com/), нажмите кнопку **роли администратора**.
   
     ![Выбор Google Apps][26]

7. Определить, какие администратора учетной записи, хотелось бы toouse toomanage подготовку учетных записей пользователей. Для hello **роли администратора** для этой учетной записи, изменять hello **права** для этой роли. Убедитесь, что она содержит все hello **права доступа администратора API** таким образом, эта учетная запись может использоваться для подготовки.
   
     ![Выбор Google Apps][27]
   
    > [!NOTE]
    > При настройке рабочей среде рекомендуется hello является toocreate учетной записи администратора в Google Apps специально для этого шага. Эти учетные записи должны иметь связанный с ним роли администратора, имеет необходимые привилегии API hello.
     
8. В hello [портал Azure](https://portal.azure.com), Обзор toohello **Azure Active Directory > корпоративных приложений > все приложения** раздела.

9. Если вы уже настроили Google Apps для единого входа, поиск экземпляра с помощью поля поиска hello Google Apps. В противном случае выберите **добавить** и выполните поиск **Google Apps** в галерее приложения hello. Выберите из результатов поиска hello Google Apps и добавьте его tooyour список приложений.

10. Выберите свой экземпляр Google Apps, а затем выберите hello **Provisioning** вкладки.

11. Набор hello **режим подготовки** слишком**автоматического**. 

     ![подготовка](./media/active-directory-saas-google-apps-provisioning-tutorial/provisioning.png)

12. В разделе hello **учетные данные администратора** щелкните **авторизовать**. В новом окне браузера откроется диалоговое окно авторизации Google Apps.

13. Убедитесь, что хотелось бы toogive Azure Active Directory разрешение toomake изменения клиента tooyour Google Apps. Нажмите кнопку **Принимаю**.
    
     ![Подтверждение разрешения][28]

14. В hello портал Azure, щелкните **проверить подключение** tooensure Azure AD можно подключить приложение tooyour Google Apps. При сбое подключения hello, убедитесь, ваша учетная запись Google Apps имеет разрешения администратора команды и повторите hello **«Авторизовать»** еще один шаг.

15. Введите адрес электронной почты hello пользователя или группы, которые должны получить уведомления о подготовке ошибки в hello **уведомление по электронной почте** поле и установите флажок "hello".

16. Нажмите кнопку **Сохранить**.

17. Установите hello сопоставлений **tooGoogle синхронизации Azure Active Directory — пользователи приложения.**

18. В hello **сопоставления атрибутов** просмотрите hello атрибутов пользователей, которые синхронизируются из Azure AD tooGoogle приложений. Здравствуйте, атрибуты, выбранные в качестве **сопоставление** свойства, используемые toomatch hello учетных записей пользователей в Google Apps для операций обновления. Выберите toocommit кнопку hello сохранить все изменения.

19. tooenable hello подготовки службы Azure AD для Google Apps, изменение hello **состояние подготовки** слишком**на** в разделе "Параметры" hello

20. Нажмите кнопку **Сохранить**.

Он запускает hello Первоначальная синхронизация всех пользователей и/или группам назначается tooGoogle приложений в разделе hello пользователей и групп. Начальная синхронизация Hello принимает tooperform больше времени, чем последующие синхронизации, которые происходят примерно каждые 20 минут при условии, что запущена служба hello. Можно использовать hello **сведения о синхронизации** статьи toomonitor хода выполнения и следуйте ссылки tooprovisioning отчеты о действиях, которые описывают все действия, выполняемые hello подготовки службы приложения Google Apps.

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Управление подготовкой учетных записей пользователей для корпоративных приложений](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Настройка единого входа](active-directory-saas-google-apps-tutorial.md)



<!--Image references-->

[10]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-security.png
[15]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-api.png
[16]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-api-enabled.png
[20]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-domains.png
[21]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-add-domain.png
[22]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-add-another.png
[24]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-provisioning.png
[25]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-provisioning-auth.png
[26]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-admin.png
[27]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-admin-privileges.png
[28]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-auth.png