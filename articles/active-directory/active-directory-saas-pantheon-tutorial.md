---
title: "Руководство по интеграции Azure Active Directory с Pantheon | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Pantheon."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2c965d1-666f-44c2-b08f-b73163096374
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 5c3e54aef1f64dbab77d40a8c098172d609bfec8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-pantheon"></a>Руководство по интеграции Azure Active Directory с Pantheon

В этом учебнике вы узнаете, как toointegrate Pantheon с Azure Active Directory (Azure AD).

Интеграция с Azure AD Pantheon предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooPantheon
- Можно включить на пользователей tooautomatically get вошедшего tooPantheon (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с Pantheon требуется hello следующих элементов:

- подписка Azure AD;
- подписка Pantheon с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление Pantheon из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-pantheon-from-hello-gallery"></a>Добавление Pantheon из галереи hello
tooconfigure hello интеграции Pantheon в Azure AD, вы должны tooadd Pantheon из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd Pantheon из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Приложения][3]

4. Введите в поле поиска hello **Pantheon**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_search.png)

5. В панели результатов hello выберите **Pantheon**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в Pantheon с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Pantheon является tooa в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в Pantheon должен установить toobe.

В Pantheon, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.

tooconfigure и теста Azure AD единого входа с Pantheon, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя Pantheon](#creating-a-pantheon-test-user)**  -toohave аналог Саймон Britta в Pantheon, который представляет связанный toohello Azure AD пользователя.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Pantheon.

**tooconfigure Azure AD единого входа с Pantheon, выполните следующие шаги hello.**

1. В hello в hello портала Azure **Pantheon** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_samlbase.png)

3. На hello **URL-адреса и домена Pantheon** выполните следующие шаги hello:

    ![Настройка единого входа](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_url.png)

    а. В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`urn:auth0:pantheon:<orgname>-SSO`

    b. В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://pantheon.auth0.com/login/callback?connection=<orgname>-SSO`

    > [!NOTE] 
    > Эти значения приведены в качестве примера. Обновите эти значения с hello фактический идентификатор и ответ URL-адрес. Обратитесь к [Pantheon поддержки](https://pantheon.io/docs/getting-support/) tooget эти значения.

4. Pantheon приложение ожидает утверждения SAML hello в определенном формате, поэтому требуется вы tooset hello значения атрибута идентификатор пользователя с помощью адреса электронной почты пользователя hello. По умолчанию Azure AD использует hello UserPrincipalName атрибута идентификатор пользователя. Однако для успешной интеграции требуют tooadjust toomatch это значение с адреса электронной почты пользователя. Интеграция Hello будет работать только после выполнения hello правильное сопоставление.

    ![Настройка единого входа](./media/active-directory-saas-pantheon-tutorial/tutorial_attribute.png)  


5. На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.

    ![Настройка единого входа](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_certificate.png)

6. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-pantheon-tutorial/tutorial_general_400.png)

7. На hello **конфигурации Pantheon** щелкните **Настройка Pantheon** tooopen **Настройка входа** окна. Копировать hello **SAML единого входа URL-адрес службы** из hello **краткий справочник.**

    ![Настройка единого входа](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_configure.png) 

8. tooconfigure единого входа на **Pantheon** стороны, необходимо загрузить hello toosend **сертификат** и **SAML единого входа URL-адрес службы** слишком[Pantheon поддержки](https://pantheon.io/docs/getting-support/).

     > [!Note]
     > Необходимо также tooprovide hello доменов электронной почты сведения и Дата и время при необходимости tooenable этого подключения. Дополнительные сведения см. [здесь](https://pantheon.io/docs/sso-organizations/).

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-pantheon-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-pantheon-tutorial/create_aaduser_02.png) 

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-pantheon-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-pantheon-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-a-pantheon-test-user"></a>Создание тестового пользователя Pantheon

В этом разделе описано, как создать пользователя Britta Simon в приложении Pantheon. Следуйте hello ниже шаги tooadd hello пользователя в Pantheon. 

>[!NOTE] 
>Для единого входа toowork пользователь должен сначала создается в Pantheon toobe.

1. TooPantheon входа в систему с учетными данными администратора.

2. Перейдите в слишком**организации** страницу панели мониторинга.
 
3. Выберите параметр **Пользователи**.

4. Нажмите кнопку **Добавить пользователя**.

5. Введите адрес электронной почты пользователя hello.

6. Выберите роль пользователя hello.

7. Нажмите кнопку **Добавить пользователя**.

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooPantheon доступа.

![Назначение пользователя][200] 

**tooassign tooPantheon Britta Simon выполните следующие шаги hello.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **Pantheon**.

    ![Настройка единого входа](./media/active-directory-saas-pantheon-tutorial/tutorial_pantheon_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.

При нажатии кнопки hello Pantheon плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour Pantheon приложения.
Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pantheon-tutorial/tutorial_general_203.png

