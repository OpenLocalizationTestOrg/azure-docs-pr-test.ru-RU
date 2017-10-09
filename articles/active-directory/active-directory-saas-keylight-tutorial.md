---
title: "Руководство по интеграции Azure Active Directory с LockPath Keylight | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и LockPath Keylight."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 234a32f1-9f56-4650-9e31-7b38ad734b1a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: 5485aeb068ba6fbdb4ea9bfc89d401e00c5b1d29
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lockpath-keylight"></a>Руководство по интеграции Azure Active Directory с LockPath Keylight

В этом учебнике вы узнаете, как toointegrate LockPath Keylight с Azure Active Directory (Azure AD).

Интеграция с Azure AD LockPath Keylight предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooLockPath Keylight
- Можно включить на пользователей tooautomatically get вошедшего tooLockPath Keylight (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с LockPath Keylight требуется hello следующих элементов:

- подписка Azure AD;
- подписка LockPath Keylight с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление LockPath Keylight из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-lockpath-keylight-from-hello-gallery"></a>Добавление LockPath Keylight из галереи hello
tooconfigure hello интеграции LockPath Keylight в Azure AD, вы должны tooadd LockPath Keylight из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd LockPath Keylight из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Приложения][3]

4. Введите в поле поиска hello **LockPath Keylight**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_search.png)

5. В панели результатов hello выберите **LockPath Keylight**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в LockPath Keylight с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в LockPath Keylight является tooa в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в LockPath Keylight должен установить toobe.

В LockPath Keylight, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.

tooconfigure и теста Azure AD единого входа с LockPath Keylight, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя LockPath Keylight](#creating-a-lockpath-keylight-test-user)**  -toohave аналог Саймон Britta в LockPath Keylight, который представляет связанный toohello Azure AD пользователя.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении LockPath Keylight.

**tooconfigure Azure AD единого входа с LockPath Keylight выполните следующие шаги hello.**

1. В hello в hello портала Azure **LockPath Keylight** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_samlbase.png)

3. На hello **URL-адреса и домена Keylight LockPath** выполните следующие шаги hello::

    ![Настройка единого входа](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_url.png)

    а. В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<company name>.keylightgrc.com/`

    b. В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<company name>.keylightgrc.com`

    c. В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<company name>.keylightgrc.com/Login.aspx`
    
    > [!NOTE] 
    > Эти значения приведены в качестве примера. Обновить значения hello фактический идентификатор, URL-адрес ответа и URL-адрес входа. Обратитесь к [группа поддержки клиента Keylight LockPath](https://www.lockpath.com/contact/) tooget эти значения. 

4. На hello **сертификат подписи SAML** щелкните **Certificate(Raw)** и затем сохраните файл сертификата hello на вашем компьютере.

    ![Настройка единого входа](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-keylight-tutorial/tutorial_general_400.png)
    
6. На hello **конфигурации Keylight LockPath** щелкните **Настройка LockPath Keylight** tooopen **Настройка входа** окна. Копировать hello **URL-адрес выхода и SAML единого входа URL-адрес службы** из hello **краткий справочник.**

    ![Настройка единого входа](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_configure.png) 

7. tooenable единого входа в LockPath Keylight выполните следующие шаги hello.
   
    а. Вход tooyour LockPath Keylight учетной записи, от имени администратора.
    
    b. В меню в верхней части hello hello выберите **лицо**и выберите **Keylight установки**.
   
    ![Настройка единого входа](./media/active-directory-saas-keylight-tutorial/401.png) 

    c. В treeview hello hello левой части экрана, нажмите кнопку **SAML**.
   
    ![Настройка единого входа](./media/active-directory-saas-keylight-tutorial/402.png) 

    d. На hello **параметры SAML** диалоговое окно, нажмите кнопку **изменить**.
   
    ![Настройка единого входа](./media/active-directory-saas-keylight-tutorial/404.png) 

8. На hello **изменение параметров SAML** диалогового окна выполните следующие шаги hello:
   
    ![Настройка единого входа](./media/active-directory-saas-keylight-tutorial/405.png) 
   
    а. Задать **проверку подлинности SAML** слишком**Active**.

    b. Вставить hello **SAML единого входа URL-адрес службы** значение, которое было скопировано из hello портал Azure в hello **URL-адрес входа поставщика удостоверений** текстового поля.

    c. Вставить hello **URL-адрес службы единого выхода** значение, которое было скопировано из hello портал Azure в hello **URL-адрес выхода поставщика удостоверений** текстового поля.

    d. Нажмите кнопку **выбрать файл** tooselect вашей загруженный LockPath Keylight сертификатов и нажмите кнопку **откройте** tooupload hello сертификата.

    д. Задать **местоположение идентификатора пользователя SAML** слишком**элемент NameIdentifier оператора subject hello**.
    
    f. Укажите hello **поставщика услуг Keylight** с помощью hello следующий шаблон: **https://&lt;CompanyName&gt;. keylightgrc.com**.
    
    ж. Задать **автоматической подготовки пользователей** слишком**Active**.

    h. Задать **тип учетной записи Автоматическая подготовка к работе** слишком**полноправный пользователь**.

    i. Задайте для параметра **Auto-provision security role** (Роль безопасности для автоматической подготовки) значение **Standard User with SAML** (Права обычного пользователя с SAML).
    
    j. Задайте для параметра **Auto-provision security config** (Конфигурация безопасности для автоматической подготовки) значение **Standard User Configuration** (Конфигурация обычного пользователя).
     
    k. В hello **атрибут адреса электронной почты** введите `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.
    
    l. В hello **атрибут имени** введите `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.
    
    m. В hello **атрибут фамилии** введите `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.
    
    n. Щелкните **Сохранить**.

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-keylight-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-keylight-tutorial/create_aaduser_02.png) 

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-keylight-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-keylight-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-a-lockpath-keylight-test-user"></a>Создание тестового пользователя LockPath Keylight

В этом разделе описано, как создать пользователя Britta Simon в приложении LockPath Keylight. LockPath Keylight поддерживает JIT-подготовку. Эта функция включена по умолчанию.

В этом разделе никакие действия с вашей стороны не требуются. При доступе к LockPath Keylight, если пользователь hello еще не существует, создается новый пользователь. 

>[!NOTE]
>Если требуется toocreate пользователя вручную, необходимо toocontact hello [LockPath Keylight клиента поддержки](https://www.lockpath.com/contact/). 

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooLockPath Keylight.

![Назначение пользователя][200] 

**tooassign Britta Simon tooLockPath Keylight, выполните следующие шаги hello.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **LockPath Keylight**.

    ![Настройка единого входа](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.

При нажатии кнопки LockPath Keylight плитки в панели доступа hello hello, вы должны получить автоматически вошедшего tooyour LockPath Keylight приложения. 

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_203.png

