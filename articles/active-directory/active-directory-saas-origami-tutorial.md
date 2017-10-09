---
title: "Руководство по интеграции Azure Active Directory с Origami | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Оригами."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a28bb0ba-b564-46ba-accc-e587699295d4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: a45f2d2b8d2271cf0fc58cb8fad92f007cb5e691
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-origami"></a>Руководство. Интеграция Azure Active Directory с Origami

В этом учебнике вы узнаете, как toointegrate оригами с Azure Active Directory (Azure AD).

Интеграция с Azure AD оригами предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooOrigami
- Можно включить на пользователей tooautomatically get вошедшего tooOrigami (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с оригами требуется hello следующих элементов:

- подписка Azure AD;
- подписка Origami с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление оригами из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-origami-from-hello-gallery"></a>Добавление оригами из галереи hello
tooconfigure hello интеграции оригами в Azure AD, вы должны tooadd оригами из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd оригами из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Приложения][3]

4. Введите в поле поиска hello **оригами**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-origami-tutorial/tutorial_origami_search.png)

5. В панели результатов hello выберите **оригами**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-origami-tutorial/tutorial_origami_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в Origami с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в оригами является tooa в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в оригами должен установить toobe.

В оригами, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.

tooconfigure и теста Azure AD единого входа с оригами, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя, прошедшего оригами](#creating-an-origami-test-user)**  -toohave аналог Саймон Britta в оригами, представление связанных toohello Azure AD пользователя.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Оригами.

**tooconfigure Azure AD единого входа с оригами, выполните следующие шаги hello.**

1. В hello в hello портала Azure **оригами** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-origami-tutorial/tutorial_origami_samlbase.png)

3. На hello **URL-адреса и домена оригами** выполните следующие шаги hello:

    ![Настройка единого входа](./media/active-directory-saas-origami-tutorial/tutorial_origami_url.png)

    В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://live.origamirisk.com/origami/account/login?account=<companyname>`

    > [!NOTE] 
    > значение Hello не является вещественным числом. Значение hello обновления с hello фактический URL-адрес входа. Обратитесь к [группа поддержки клиента оригами](https://wordpress.org/support/theme/origami) tooget значение hello. 
 
4. На hello **сертификат подписи SAML** щелкните **сертификата (Base64)** и затем сохраните файл сертификата hello на вашем компьютере.

    ![Настройка единого входа](./media/active-directory-saas-origami-tutorial/tutorial_origami_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-origami-tutorial/tutorial_general_400.png)

6. На hello **конфигурации оригами** щелкните **Настройка оригами** tooopen **Настройка входа** окна. Копировать hello **URL-адрес выхода и SAML единого входа URL-адрес службы** из hello **краткий справочник.**

    ![Настройка единого входа](./media/active-directory-saas-origami-tutorial/tutorial_origami_configure.png) 

7. Войдите в toohello оригами учетной записи с правами администратора.

8. В меню в верхней части hello hello выберите **администратора**.
   
    ![Настройка единого входа](./media/active-directory-saas-origami-tutorial/tutorial_origami_51.png)

9. На странице диалогового окна hello единого входа в программу установки выполните следующие шаги hello.
   
    ![Настройка единого входа](./media/active-directory-saas-origami-tutorial/tutorial_origami_531.png)

    а. Выберите пункт **Включить единый вход**.

    b. В hello **поставщика удостоверений вход URL-адрес страницы** текстовое значение hello вставить **SAML единого входа URL-адрес службы**, который вы скопировали из портала Azure.

    c. В hello **URL-адрес страницы выхода поставщика удостоверений** текстовое значение hello вставить **URL-адрес выхода**, который вы скопировали из портала Azure.

    d. Нажмите кнопку **Обзор** tooupload hello сертификат, загруженный с портала Azure hello.

    д. Нажмите кнопку **Сохранить изменения**.

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-origami-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-origami-tutorial/create_aaduser_02.png) 

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-origami-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-origami-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-an-origami-test-user"></a>Создание тестового пользователя Origami

В этом разделе описано, как создать пользователя Britta Simon в приложении Origami. 

1. Войдите в toohello оригами учетной записи с правами администратора.

2. В меню в верхней части hello hello выберите **администратора**.
   
    ![Настройка единого входа](./media/active-directory-saas-origami-tutorial/tutorial_origami_51.png)

3. На hello **пользователей и безопасности** диалоговое окно, нажмите кнопку **пользователей**.
   
    ![Настройка единого входа](./media/active-directory-saas-origami-tutorial/tutorial_origami_54.png)

4. Нажмите кнопку **Add New User**(Добавить нового пользователя).
   
    ![Настройка единого входа](./media/active-directory-saas-origami-tutorial/tutorial_origami_55.png)

5. В диалоговом окне Добавить пользователя hello выполните следующие шаги hello.
   
    ![Настройка единого входа](./media/active-directory-saas-origami-tutorial/tutorial_origami_56.png)

    а. В hello **имя пользователя** текстовом поле введите адрес электронной почты hello пользователя как  **brittasimon@contoso.com** .

    b. В hello **пароль** введите пароль.

    c. В hello **подтверждение пароля** textbox hello введите пароль еще раз.

    d. В hello **имя** текстовом поле введите имя пользователя, такие как hello **Britta**.

    д. В hello **Фамилия** текстовом поле введите фамилию пользователя как hello **Simon**.

    f. Щелкните **Сохранить**.
   
    ![Настройка единого входа](./media/active-directory-saas-origami-tutorial/tutorial_origami_57.png)

6. Назначьте **роли пользователей** и **клиентского доступа** toohello пользователя. 
   
    ![Настройка единого входа](./media/active-directory-saas-origami-tutorial/tutorial_origami_58.png)

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooOrigami доступа.

![Назначение пользователя][200] 

**tooassign tooOrigami Britta Simon выполните следующие шаги hello.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **оригами**.

    ![Настройка единого входа](./media/active-directory-saas-origami-tutorial/tutorial_origami_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.

При выборе плитки оригами hello в hello панели доступа, следует получать автоматически вошедшего tooyour оригами приложения.

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-origami-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-origami-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-origami-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-origami-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-origami-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-origami-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-origami-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-origami-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-origami-tutorial/tutorial_general_203.png

