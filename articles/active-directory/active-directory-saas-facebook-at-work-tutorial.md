---
title: "Руководство по интеграции Azure Active Directory с Workplace by Facebook | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и рабочей области с Facebook."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 30f2ee64-95d3-44ef-b832-8a0a27e2967c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: jeedes
ms.openlocfilehash: fd19b3f178a2aee7dd2f204d6d3cf6df8fe6b444
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workplace-by-facebook"></a>Руководство по интеграции Azure Active Directory с Workplace by Facebook

В этом учебнике вы узнаете, как toointegrate рабочему месту с Facebook с Azure Active Directory (Azure AD).

Интеграция рабочему месту с Facebook с Azure AD предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooWorkplace с Facebook.
- Можно включить пользователей tooautomatically получить вход tooWorkplace с Facebook (единый вход) с помощью своих учетных записей Azure AD.
- Можно управлять учетными записями в одном централизованном месте: hello портал Azure.

Дополнительные сведения об интеграции приложения SaaS с Azure AD см. в статье [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD в рабочей области с Facebook, требуется hello следующих элементов:

- подписка Azure AD;
- подписка Workplace by Facebook с поддержкой единого входа.

tootest hello шаги в этом учебнике, придерживайтесь следующих рекомендаций:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление рабочей области с Facebook из коллекции hello.
2. Настройка и проверка единого входа в Azure AD.

## <a name="add-workplace-by-facebook-from-hello-gallery"></a>Добавление рабочей области с Facebook из коллекции hello
tooconfigure интеграция рабочему месту с Facebook hello в Azure AD, добавить рабочему месту с Facebook из hello коллекции tooyour список управляемых приложений SaaS.

1. В hello [портал Azure](https://portal.azure.com)в левой области hello, выберите **Azure Active Directory**. 

    ![Кнопка Hello Azure Active Directory][1]

2. Обзор слишком**корпоративных приложений** > **все приложения**.

    ![Hello корпоративных приложений колонку][2]
    
3. tooadd hello новые приложения, выберите **новое приложение** в верхней части hello диалогового окна «hello».

    ![Кнопка нового приложения Hello][3]

4. Введите в поле поиска hello **рабочему месту с Facebook**и выберите **рабочему месту с Facebook** из результатов. Выберите **добавить**, tooadd приложения hello.

    ![Рабочая область с Facebook в списке результатов hello](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_search.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в Workplace by Facebook с использованием тестового пользователя Britta Simon.

Для toowork единого входа Azure AD необходима tooknow пользователь аналог какие hello в рабочей области с Facebook является tooa в Azure AD. Другими словами следует установить ссылочного отношения между пользователя Azure AD и связанных пользователей hello в рабочей области с Facebook.

Установить это отношение, назначив значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в рабочей области с Facebook.

### <a name="configure-azure-ad-single-sign-on"></a>Настройка единого входа Azure AD

В этом разделе Включить единый вход Azure AD в hello портал Azure и настроить единый вход в рабочую область с помощью приложения Facebook.

1. В hello в hello портала Azure **рабочему месту с Facebook** странице интеграции приложений выберите **единого входа**.

    ![Ссылка "Настройка единого входа"][4]

2. В hello **единого входа** выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_samlbase.png)

3. В hello **рабочему месту с URL-адреса и домена Facebook** статьи, hello следующие:

    а. В hello **URL-адрес входа** текстовом поле введите URL-адрес, использующий hello следующий шаблон:`https://<company subdomain>.facebook.com`

    b. В hello **идентификатор** текстовом поле введите URL-адрес, использующий hello следующий шаблон:`https://www.facebook.com/company/<scim company id>`

    > [!NOTE]
    > Эти значения приведены только для примера. Обновите эти значения с hello фактический URL-адрес входа и идентификатором. Обратитесь в службу hello [рабочей группой поддержки клиент Facebook](https://workplace.fb.com/faq/) tooget эти значения. 

4. В hello **сертификат подписи SAML** выберите **сертификата (Base64)**, а затем сохраните файл сертификата hello на компьютере.

    ![ссылку для скачивания сертификата Hello](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_certificate.png) 

5. Щелкните **Сохранить**.

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_400.png)

6. В hello **рабочему месту конфигурацией Facebook** выберите **Настройка рабочей области с Facebook** tooopen hello **Настройка входа** окна. Копировать hello **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник** раздела.

    ![Конфигурация Workplace by Facebook](./media/active-directory-saas-facebook-at-work-tutorial/config.png) 

7. В другом окне браузера войдите в рабочей области с Facebook корпоративный сайт tooyour с правами администратора.
  
   > [!NOTE] 
   > Как часть процесса проверки подлинности SAML hello рабочей области можно использовать строки запроса из копии too2.5 килобайт размер в порядке toopass параметры tooAzure AD.

8. В hello **панели мониторинга компании**, go toohello **проверки подлинности** вкладки.

9. В разделе **проверку подлинности SAML**выберите **SSO только** из раскрывающегося списка hello.

10. Введите hello значения, скопированные из hello **рабочему месту конфигурацией Facebook** раздел hello портал Azure в соответствующие поля hello:

    *   В **URL-адрес SAML** текстовое поле, вставить значение hello **единого входа URL-адрес службы**, который вы скопировали из hello портал Azure.
    *   В **URL-адрес издателя SAML** текстовое поле, вставить значение hello **идентификатор сущности SAML**, который вы скопировали из hello портал Azure.
    *   В **SAML выхода перенаправления (необязательно)**, вставьте значение hello **URL-адрес выхода**, который вы скопировали из hello портал Azure.
    *   Откройте ваш **сертификат в кодировке base-64** в блокноте, загружаются из hello портал Azure. Скопируйте содержимое hello в буфер обмена и вставьте его в toothe **сертификат SAML** текстовое поле.

11. Может потребоваться аудитории hello tooenter URL-адрес, URL-адрес получателя и ACS (службы обработчика утверждений) URL-адрес, перечисленных в разделе hello **конфигурация SAML** раздела.

12. Прокрутите toohello нижней части раздела hello и выберите **тестирования единого входа**. Появится всплывающее окно с hello Azure AD на странице входа. tooauthenticate, введите свои учетные данные в обычном режиме. Убедитесь, Здравствуйте hello адрес электронной почты, возвращенный Azure AD, так же, как hello рабочей учетной записи, которой вы вошли в систему.

13. Если hello тестирования успешно завершено, прокрутите toohello нижней части страницы hello и выберите **Сохранить**.

14. Теперь для аутентификации всех пользователей Workplace будет отображаться страница входа в Azure AD.

Вы можете tooconfigure выхода SAML в URL-адрес, который можно использовать toopoint на страницы выхода hello Azure AD. Если этот параметр включен и настроен, hello пользователь больше не страницы выхода направленной toohello рабочей области. Вместо этого пользователь hello является перенаправленный toohello URL-адрес, которое было добавлено в параметр перенаправления выхода SAML hello.


> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello. После добавления этого приложения из hello **Active Directory** > **корпоративных приложений** просто выберите hello **Single Sign-On** вкладку и hello доступа внедренные документации с помощью hello **конфигурации** раздела внизу hello. Вы можете прочитать больше о документации embedded hello в hello [Azure AD внедренных документации]( https://go.microsoft.com/fwlink/?linkid=845985).

### <a name="configure-reauthentication-frequency"></a>Настройка частоты повторной аутентификации

Можно настроить tooprompt рабочему месту для проверки SAML каждый день, в течение трех дней, одна неделя, две недели, один месяц или никогда.

> [!NOTE] 
>Hello минимальное значение для проверки SAML hello мобильных приложений имеет значение tooone недели.

Можно также принудительно применить SAML для всех пользователей. toodo это, используйте hello **требуется проверка подлинности SAML для всех пользователей теперь** кнопки.


### <a name="create-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

1. В hello **портал Azure**в левой области hello, выберите **Azure Active Directory**.

    ![Кнопка Hello Azure Active Directory](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей, перейдите в слишком**пользователей и групп**и выберите **всех пользователей**.
    
    ![Здравствуйте, «Пользователи и группы» и «Все пользователи» ссылки](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_02.png) 

3. tooopen hello **пользователя** выберите **добавить**.
 
    ![Кнопка "Добавить" Hello](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_03.png) 

4. В hello **пользователя** диалогового окна поле, hello следующие:
 
    ![диалоговое окно приветствия пользователя](./media/active-directory-saas-facebook-at-work-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** текстовое поле, тип hello **адрес электронной почты** из BrittaSimon.

    c. Щелкните **Показать пароль** и запишите пароль.

    d. Нажмите кнопку **Создать**.
 
### <a name="create-a-workplace-by-facebook-test-user"></a>Создание тестового пользователя Workplace by Facebook

В этом разделе вы создадите в Workplace by Facebook пользователя с именем Britta Simon. Workplace by Facebook поддерживает JIT-подготовку. Эта функция включена по умолчанию.

В этом разделе никакие действия с вашей стороны не требуются. Если пользователь не существует в рабочей области с Facebook, новый созданный при попытке tooaccess рабочему месту Facebook.

>[!Note]
>Если вам требуется toocreate пользователя вручную, обратитесь в службу hello [рабочей группой поддержки клиент Facebook](https://workplace.fb.com/faq/).

### <a name="assign-hello-azure-ad-test-user"></a>Назначить hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooWorkplace с Facebook.

![Назначение пользователя][200] 

1. В hello Azure просмотрите приложений портала, откройте hello. Перейдите в представление каталога toohello, перейдите в слишком**корпоративных приложений**, а затем выберите **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **рабочему месту с Facebook**.

    ![Hello рабочему месту с Facebook ссылку в списке приложений hello](./media/active-directory-saas-facebook-at-work-tutorial/tutorial_workplacebyfacebook_app.png) 

3. Выберите в меню hello слева hello, **пользователей и групп**.

    ![Hello ссылку «Пользователи и группы»][202] 

4. Выберите **Добавить**. Затем в hello **добавить назначение** выберите **пользователей и групп**.

    ![область назначения, добавьте Hello][203]

5. В hello **пользователей и групп** выберите **Britta Simon** в список пользователей hello.

6. В hello **пользователей и групп** выберите **выберите**.

7. В hello **добавить назначение** выберите **назначить**.
    
### <a name="test-single-sign-on"></a>Проверка единого входа

Tootest параметры единого входа, откройте панель доступа hello.
Дополнительные сведения см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).


## <a name="next-steps"></a>Дальнейшие действия

* В разделе hello [список учебников по toointegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md).
* Прочитайте статью [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* Дополнительные сведения о том, как слишком[Настройка подготовки пользователя](active-directory-saas-facebook-at-work-provisioning-tutorial.md).



<!--Image references-->

[1]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-facebook-at-work-tutorial/tutorial_general_203.png

