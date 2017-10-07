---
title: "Руководство по интеграции Azure Active Directory с Kantega SSO for Confluence | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Kantega SSO является точка пересечения."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d0d99c14-a6ca-45f2-bb84-633126095e7a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: b35eb8757e41e86228a3a9ee10869086cc801c9b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kantega-sso-for-confluence"></a>Руководство по интеграции Azure Active Directory с Kantega SSO for Confluence

В этом учебнике вы узнаете, как toointegrate Kantega SSO является точка пересечения с Azure Active Directory (Azure AD).

Интеграция Kantega SSO является точка пересечения с Azure AD предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooKantega единого входа для является точка пересечения
- Можно включить на пользователей tooautomatically get вошедшего tooKantega единого входа для является точка пересечения (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с помощью единого входа Kantega для является точка пересечения требуется hello следующих элементов:

- подписка Azure AD;
- подписка Kantega SSO for Confluence с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление Kantega SSO является точка пересечения из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-kantega-sso-for-confluence-from-hello-gallery"></a>Добавление Kantega SSO является точка пересечения из галереи hello
интеграции hello tooconfigure Kantega SSO является точка пересечения в Azure AD, необходима tooadd Kantega единого входа является точка пересечения из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd Kantega SSO является точка пересечения из галереи hello выполните hello следующие шаги.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Приложения][3]

4. Введите в поле поиска hello **Kantega SSO является точка пересечения**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_kantegassoforconfluence_search.png)

5. В панели результатов hello выберите **Kantega SSO является точка пересечения**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_kantegassoforconfluence_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в Kantega SSO for Confluence с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в SSO Kantega является точка пересечения является tooa в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в SSO Kantega является точка пересечения должен установить toobe.

В Kantega единого входа для является точка пересечения, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.

tooconfigure и выполнить проверку Azure AD единого входа с помощью единого входа Kantega является точка пересечения, необходимы следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание Kantega единого входа для тестового пользователя является точка пересечения](#creating-a-kantega-sso-for-confluence-test-user)**  -toohave аналог Саймон Britta в Kantega SSO является точка пересечения, который представляет связанный toohello Azure AD пользователя.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в вашей Kantega SSO для приложения является точка пересечения.

**tooconfigure Azure AD единого входа с помощью единого входа Kantega для является точка пересечения, выполните следующие шаги hello.**

1. В hello в hello портала Azure **Kantega SSO является точка пересечения** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_kantegassoforconfluence_samlbase.png)

3. В **IDP** инициировал режим на hello **Kantega единого входа является точка пересечения доменов и URL-адреса** выполните следующий шаг hello:

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_kantegassoforconfluence_url1.png)

    а. В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`

    b. В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`

4. В **SP** инициируемых режим, проверка **Показывать дополнительные параметры URL-адреса** и выполните следующий шаг hello:

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_kantegassoforconfluence_url2.png)

    В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`

    > [!NOTE] 
    > Эти значения приведены в качестве примера. Обновить значения hello фактический идентификатор, URL-адрес ответа и URL-адрес входа. Эти значения будут получены во время настройки hello является точка пересечения подключаемого модуля, который описывается далее в учебнике hello.

5. На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_kantegassoforconfluence_certificate.png) 

6. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_general_400.png)
    
7. В другом окне браузера, войдите в tooyour **портал администрирования является точка пересечения** с правами администратора.

8. Наведите указатель мыши на шестеренки и выберите hello **надстройки**.
    
    ![Настройка единого входа](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon1.png)

9. В разделе **ATLASSIAN MARKETPLACE** щелкните **Find new add-ons** (Найти новые надстройки). 

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon.png)

10. Поиск **Kantega единого входа проверки подлинности Kerberos является точка пересечения SAML** и нажмите кнопку **установить** tooinstall кнопку hello нового подключаемого модуля SAML.

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon2.png)

11. запускает Hello установки подключаемого модуля.

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon3.png)

12. После завершения установки hello. Нажмите кнопку **Закрыть**

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon33.png)

13. Нажмите кнопку **Управление**.

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon34.png)
    
14. Нажмите кнопку **Настройка** tooconfigure hello нового подключаемого модуля.

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon35.png)

15. Этот новый подключаемый модуль можно также найти на вкладке **USERS & SECURITY** (Пользователи и безопасность).

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon36.png)
    
16. В hello **SAML** раздела. Выберите **Azure Active Directory (Azure AD)** из hello **добавить поставщик удостоверений** раскрывающегося списка.

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon4.png)

17. Выберите уровень подписки **Базовый**.

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon5.png)       

18. На hello **свойства приложения** статьи, выполните следующие шаги: 

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon6.png)

    а. Копировать hello **URI идентификатора приложения** и использовать его как **идентификатор, URL-адрес ответа и URL-адрес входа** на hello **Kantega единого входа является точка пересечения доменов и URL-адреса** раздела на портале Azure.

    b. Щелкните **Далее**.

19. На hello **импорта метаданных** статьи, выполните следующие шаги: 

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon7.png)

    а. Щелкните **Metadata file on my computer** (Файл метаданных на моем компьютере) и передайте файл метаданных, который вы скачали с портала Azure.

    b. Щелкните **Далее**.

20. На hello **расположение единого входа и имя** статьи, выполните следующие шаги:

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon8.png)
    
    а. Добавьте имя hello поставщика удостоверений в **имя поставщика удостоверений** текстового поля (например, Azure AD).

    b. Щелкните **Далее**.

21. Проверьте сертификат подписи hello и нажмите кнопку **Далее**.

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon9.png)

22. На hello **учетных записей пользователей является точка пересечения** статьи, выполните следующие шаги:

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon10.png)

    а. Выберите **при необходимости создайте пользователей в каталоге внутреннего элемента является точка пересечения** и введите соответствующее имя hello hello группы для пользователей (может быть несколько нет. разделенных запятой).

    b. Щелкните **Далее**.

23. Нажмите кнопку **Готово**   

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon11.png)

24. На hello **известные доменов для Azure AD** статьи, выполните следующие шаги: 

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforconfluence-tutorial/addon12.png)

    а. Выберите **известные домены** из hello левой панели страницы приветствия.

    b. Введите имя домена в hello **известные домены** текстового поля.

    c. Щелкните **Сохранить**. 

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-kantegassoforconfluence-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-kantegassoforconfluence-tutorial/create_aaduser_02.png) 

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-kantegassoforconfluence-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-kantegassoforconfluence-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-a-kantega-sso-for-confluence-test-user"></a>Создание тестового пользователя Kantega SSO for Confluence

Пользователи toolog tooenable Azure AD в tooConfluence, их необходимо подготовить в является точка пересечения. В случае hello SSO Kantega является точка пересечения Подготовка выполняется вручную.

**tooprovision учетной записи пользователя, выполните следующие шаги hello.**

1. Войдите в tooyour Kantega единого входа для веб-узла компании является точка пересечения с правами администратора.

2. Наведите указатель мыши на шестеренки и выберите hello **Управление пользователями**.

    ![Добавление сотрудника](./media/active-directory-saas-kantegassoforconfluence-tutorial/user1.png) 

3. В разделе "Users" (Пользователи) выберите вкладку **Add Users** (Добавление пользователей). На hello **«Добавить пользователя»** диалогового окна выполните следующие шаги hello:

    ![Добавление сотрудника](./media/active-directory-saas-kantegassoforconfluence-tutorial/user2.png) 

    а. В hello **Username** электронной почты hello тип пользователя в текстовое поле, например Brittasimon@contoso.com.

    b. В hello **полное имя** текстового поля, типа hello полное имя пользователя как Саймон Britta.

    c. В hello **электронной почты** в текстовое поле типа hello адрес электронной почты пользователя, например Brittasimon@contoso.com.

    d. В hello **пароль** текстового поля, типа hello пароль для пользователя.

    д. Нажмите кнопку **подтверждение пароля** вводить пароль hello.
    
    f. Нажмите кнопку **Добавить**.

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooKantega единого входа для является точка пересечения.

![Назначение пользователя][200] 

**tooassign tooKantega Britta Simon единого входа для является точка пересечения, выполните следующие шаги hello.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **Kantega SSO является точка пересечения**.

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_kantegassoforconfluence_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.

При нажатии кнопки hello Kantega единого входа для является точка пересечения плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour Kantega единого входа для приложения является точка пересечения.
Дополнительные сведения о панели доступа см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kantegassoforconfluence-tutorial/tutorial_general_203.png

