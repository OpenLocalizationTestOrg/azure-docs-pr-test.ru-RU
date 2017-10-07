---
title: "Учебник. Интеграция Azure Active Directory с EverBridge | Документы Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и EverBridge."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 58d7cd22-98c0-4606-9ce5-8bdb22ee8b3e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: a260298279407ed709bc2e685a104410f9836a74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-everbridge"></a>Руководство по интеграции Azure Active Directory с Everbridge

В этом учебнике вы узнаете, как toointegrate EverBridge с Azure Active Directory (Azure AD).

Интеграция с Azure AD EverBridge предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooEverBridge
- Можно включить на пользователей tooautomatically get вошедшего tooEverBridge (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с EverBridge требуется hello следующих элементов:

- подписка Azure AD;
- подписка EverBridge с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление EverBridge из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-everbridge-from-hello-gallery"></a>Добавление EverBridge из галереи hello
tooconfigure hello интеграции EverBridge в Azure AD, вы должны tooadd EverBridge из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd EverBridge из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Приложения][3]

4. Введите в поле поиска hello **EverBridge**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_search.png)

5. В панели результатов hello выберите **EverBridge**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в приложение EverBridge с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в EverBridge является tooa в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в EverBridge должен установить toobe.

В EverBridge, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.

tooconfigure и теста Azure AD единого входа с EverBridge, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя, прошедшего EverBridge](#creating-an-everbridge-test-user)**  -toohave аналог Саймон Britta в EverBridge, который представляет связанный toohello Azure AD пользователя.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении EverBridge.

**tooconfigure Azure AD единого входа с EverBridge, выполните следующие шаги hello.**

1. В hello в hello портала Azure **EverBridge** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_samlbase.png)

3. На hello **URL-адреса и домена EverBridge** выполните следующие шаги hello:

    ![Настройка единого входа](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_url.png)

    а. В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://sso.everbridge.net/<companyname>`

    b. В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://manager.everbridge.net/saml/SSO/<companyname>/alias/defaultAlias`

    > [!NOTE] 
    > Эти значения приведены в качестве примера. Обновите эти значения с hello фактический идентификатор и ответ URL-адрес. Обратитесь к [EverBridge поддержки](mailto:support@everbridge.com) tooget эти значения.
 
4. На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.

    ![Настройка единого входа](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-everbridge-tutorial/tutorial_general_400.png)

6. На hello **конфигурации EverBridge** щелкните **Настройка EverBridge** tooopen **Настройка входа** окна. Копировать hello **SAML единого входа URL-адрес службы** из hello **краткий справочник.**

    ![Настройка единого входа](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_configure.png) 

6. tooget единого входа, настроенному для вашего приложения, необходимо клиента Everbridge tooyour toosign вход в систему с правами администратора.

7. В меню в верхней части hello hello щелкните hello **параметры** и выберите **Single Sign-On** под **безопасности**.
   
    ![Настройка единого входа](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_002.png)
   
    а. В hello **имя** текстовое поле, имя типа hello идентификатор поставщика (например: название вашей компании).
   
    b. В hello **имя API** в текстовое поле имя типа hello API.
   
    c. Нажмите кнопку **выбрать файл** файл метаданных hello tooupload кнопку загруженного с портала Azure.
   
    d. В hello расположения удостоверения SAML, выберите **удостоверение находится в элемент hello NameIdentifier оператора Subject hello**.
   
    д. В hello **URL-адрес входа поставщика удостоверений** текстовое значение hello вставьте URL-адрес единого входа SAML в Azure AD.
   
    ![Настройка единого входа](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_003.png)
   
    f. В службе поставщика привязка запроса, инициированного hello, выберите **перенаправления HTTP**.

    ж. Нажмите кнопку **Сохранить**

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-everbridge-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-everbridge-tutorial/create_aaduser_02.png) 

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-everbridge-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-everbridge-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-an-everbridge-test-user"></a>Создание тестового пользователя EverBridge

В этом разделе описано, как создать пользователя Britta Simon в приложении Everbridge. Работать с [EverBridge поддержки](mailto:support@everbridge.com) tooadd hello пользователей на платформе Everbridge hello.

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooEverBridge доступа.

![Назначение пользователя][200] 

**tooassign tooEverBridge Britta Simon выполните следующие шаги hello.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **EverBridge**.

    ![Настройка единого входа](./media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

Цель этого раздела Hello является tootest настройки единого входа Azure AD с помощью панели доступа "hello".

При нажатии кнопки hello Everbridge плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour Everbridge приложения.

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_203.png

