---
title: "Руководство. Интеграция Azure Active Directory с GitHub | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и GitHub."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4395bd95-05de-4deb-87a5-dc3bc8ac4d95
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 688779de4e6627e49c0e3e8a7576f2f8c7a81ab1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-github"></a>Руководство. Интеграция Azure Active Directory с GitHub

В этом учебнике вы узнаете, как toointegrate GitHub с Azure Active Directory (Azure AD).

Интеграция GitHub с Azure AD предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooGitHub
- Можно включить на пользователей tooautomatically get вошедшего tooGitHub (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал управления Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с GitHub требуется hello следующих элементов:

- подписка Azure AD;
- подписка GitHub с поддержкой единого входа.


> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.


tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не следует использовать рабочую среду при отсутствии необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).


## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление GitHub из галереи hello
2. Настройка и проверка единого входа в Azure AD


## <a name="adding-github-from-hello-gallery"></a>Добавление GitHub из галереи hello
tooconfigure hello интеграции GitHub в Azure AD, вы должны tooadd GitHub из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd GitHub из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портала управления Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. Нажмите кнопку **добавить** кнопку в верхней части hello диалогового окна "hello".

    ![Приложения][3]

4. Введите в поле поиска hello **GitHub.com**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-github-tutorial/tutorial_github_search02.png)

5. В панели результатов hello выберите **GitHub**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-github-tutorial/tutorial_github_search_result02.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описано, как настроить и проверить единый вход Azure AD в GitHub с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow какой пользователь hello аналога в GitHub — tooa пользователя в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в GitHub должен установить toobe.

Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в GitHub.

tooconfigure и теста Azure AD единого входа с GitHub, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя GitHub](#creating-a-GitHub-test-user)**  -toohave аналог Саймон Britta в GitHub, представление связанных toohello Azure AD ей.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал управления Azure hello и настройки единого входа в приложение GitHub.

**tooconfigure Azure AD единого входа с GitHub, выполните следующие шаги hello.**

1. На портале управления Azure hello на hello **GitHub** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна, как **режим** выберите **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-github-tutorial/tutorial_github_01.png)

3. На hello **URL-адреса и домена GitHub** выполните следующие шаги hello:

    ![Настройка единого входа](./media/active-directory-saas-github-tutorial/tutorial_github_saml011.png)

    а. В hello **URL-адрес входа** текстовое поле, значение типа hello как:`https://github.com/orgs/<entity-id>/sso`

    b. В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://github.com/orgs/<entity-id>`

    > [!NOTE] 
    > Обратите внимание на то, что они не hello реальные значения. У вас tooupdate эти значения с hello фактический ющего на URL-адрес и идентификатор. Здесь мы предлагаем вам toouse hello уникальное значение строки в hello идентификатор. Перейдите в раздел tooretrieve tooGitHub Admin эти значения. 

4. На hello **атрибуты пользователя** выберите **идентификатор пользователя** как user.mail.

    ![Настройка единого входа](./media/active-directory-saas-github-tutorial/tutorial_github_attribute_new01.png)
    
5. На hello **сертификат подписи SAML** щелкните **Создание нового сертификата**.

    ![Настройка единого входа](./media/active-directory-saas-github-tutorial/tutorial_github_03.png)

6. На hello **создать новый сертификат** диалоговое окно, щелкните значок календаря hello и выберите **даты истечения срока действия**. Затем нажмите кнопку **Сохранить**.

    ![Настройка единого входа](./media/active-directory-saas-github-tutorial/tutorial_general_300.png)

7. На hello **сертификат подписи SAML** выберите **активировать новый сертификат** и нажмите кнопку **Сохранить** кнопки.

    ![Настройка единого входа](./media/active-directory-saas-github-tutorial/tutorial_github_04.png)

8. На всплывающее окно hello **сертификат продолжения** окно, нажмите кнопку **ОК**.

    ![Настройка единого входа](./media/active-directory-saas-github-tutorial/tutorial_general_400.png)

9. На hello **сертификат подписи SAML** щелкните **сертификата (Base64)** и затем сохраните файл сертификата hello на вашем компьютере.

    ![Настройка единого входа](./media/active-directory-saas-github-tutorial/tutorial_github_05.png) 

10. На hello **конфигурации GitHub** щелкните **настройки GitHub** tooopen **Настройка входа** окна.

    ![Настройка единого входа](./media/active-directory-saas-github-tutorial/tutorial_github_06.png) 

    ![Настройка единого входа](./media/active-directory-saas-github-tutorial/tutorial_github_07.png)

11. В другом окне веб-браузера войдите на свой корпоративный сайт GitHub в качестве администратора.

12. Перейдите в слишком**параметры** и нажмите кнопку **безопасности**

    ![данных](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_03.png)

13. Проверьте hello **включить проверку подлинности SAML** поле, отображая hello единым входом поля конфигурации. Затем с помощью hello единого входа URL-адреса значение tooupdate hello один URL-адрес входа в конфигурации Azure AD.

    ![данных](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_13.png)

14. Настройте hello следующие поля:

    а. **URL-адрес входа**: введите **SAML единого входа для URL-адрес службы** из hello **настройки GitHub** раздел в Azure AD

    b. **Издатель**: введите **идентификатор сущности SAML** из hello **настройки GitHub** раздел в Azure AD

    c. **Открытый сертификат**: Привет открыть загрузить сертификат из Azure AD в Блокноте и скопируйте содержимое hello, включая «BEGIN» и «END сертификата»

    ![данных](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_051.png)

15. Щелкните **конфигурация теста SAML** tooconfirm, без проверки ошибок или ошибок во время единого входа.

    ![данных](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_06.png)

16. Нажмите кнопку **Сохранить**

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя на портале управления Azure hello, вызывается Саймон Britta.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал управления Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-github-tutorial/create_aaduser_01.png) 

2. Go слишком**пользователей и групп** и нажмите кнопку **всех пользователей** toodisplay hello список пользователей.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-github-tutorial/create_aaduser_02.png) 

3. Вверху hello диалоговое окно приветствия щелкните **добавить** tooopen hello **пользователя** диалогового окна.
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-github-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-github-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**. 


### <a name="creating-a-github-test-user"></a>Создание тестового пользователя GitHub

В порядке tooenable toolog пользователей Azure AD в GitHub их необходимо подготовить в GitHub.  
В случае hello GitHub Подготовка выполняется вручную.

**tooprovision учетных записей пользователей, выполните следующие действия hello:**

1. Войдите в систему tooyour GitHub сайт компании как администратор.

2. Выберите параметр **Пользователи**.

    ![Люди](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_08.png "Люди")

3. Нажмите **Invite member** (Пригласить участника).

    ![Приглашение пользователей](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_09.png "приглашение пользователей")

4. На hello **приглашение элемент** диалогового окна выполните следующие шаги hello:

    а. В hello **электронной почты** текстовом поле введите адрес электронной почты hello Саймон Britta учетной записи.

    ![Приглашение участников](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_10.png "приглашение участников")
    
    b. Щелкните **Send Invitation** (Отправить приглашение).

    ![Приглашение участников](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_11.png "приглашение участников")

    > [!NOTE]
    > Hello владельцем учетной записи Azure Active Directory получит сообщение электронной почты и выполните их учетных записей tooconfirm ссылку, чтобы она стала активной.


### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления ее tooGitHub доступа.

![Назначение пользователя][200] 

**tooassign tooGitHub Britta Simon выполните следующие шаги hello.**

1. На портале управления Azure hello, открыть представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **GitHub.com**.

    ![Настройка единого входа](./media/active-directory-saas-github-tutorial/tutorial_github_search_result021.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    


### <a name="testing-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.

При нажатии кнопки hello GitHub плитки в панели доступа hello, вы должны получить вошедшего tooyour GitHub приложения. Вы сможете вход как учетная запись организации, но затем toolog необходимость личную учетную запись.


## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-github-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-github-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-github-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-github-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-github-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-github-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-github-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-github-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-github-tutorial/tutorial_general_203.png
