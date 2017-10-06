---
title: "Руководство. Интеграция Azure Active Directory с Ceridian Dayforce HCM | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Ceridian Dayforce HCM."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 7adf1eb3-d063-45d6-96a8-fd53b329b3f3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 4d72f29b4e5e30ef8881806d789f6676fc541e2e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ceridian-dayforce-hcm"></a>Учебник. Интеграция Azure Active Directory с Ceridian Dayforce HCM

В этом учебнике вы узнаете, как toointegrate HCM Dayforce Ceridian с Azure Active Directory (Azure AD).

Интеграция с Azure AD Ceridian Dayforce HCM предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooCeridian Dayforce HCM.
- Вы можете включить учетные записи Azure AD вашей пользователей tooautomatically get вошедшего tooCeridian HCM Dayforce (Single Sign-On).
- Вы можете управлять учетными записями в одном централизованном месте - hello портал Azure.

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с Ceridian Dayforce HCM требуется hello следующих элементов:

- подписка Azure AD;
- подписка Ceridian Dayforce HCM с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление Ceridian Dayforce HCM из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-ceridian-dayforce-hcm-from-hello-gallery"></a>Добавление Ceridian Dayforce HCM из галереи hello
tooconfigure hello интеграции Ceridian Dayforce HCM в Azure AD, вы должны tooadd Ceridian Dayforce HCM из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd HCM Dayforce Ceridian из галереи hello выполните hello следующие шаги.**

1. В hello ** [портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Кнопка Hello Azure Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Hello корпоративных приложений колонку][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Кнопка нового приложения Hello][3]

4. Введите в поле поиска hello **Ceridian Dayforce HCM**выберите **Ceridian Dayforce HCM** из панели результатов щелкните **добавить** кнопку tooadd приложения hello.

    ![HCM Dayforce Ceridian в списке результатов hello](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD

В этом разделе описана настройка и проверка единого входа Azure AD в Ceridian Dayforce HCM с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Ceridian Dayforce HCM является tooa в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в Ceridian Dayforce HCM должен установить toobe.

В Ceridian Dayforce HCM, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.

tooconfigure и теста Azure AD единого входа с Ceridian Dayforce HCM, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configure-azure-ad-single-sign-on) ** -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user) ** -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя Ceridian Dayforce HCM](#create-a-ceridian-dayforce-hcm-test-user) ** -toohave аналог Саймон Britta в Ceridian Dayforce HCM, который представляет связанный toohello Azure AD пользователя.
4. **[Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#test-single-sign-on) ** -tooverify ли hello works конфигурации.

### <a name="configure-azure-ad-single-sign-on"></a>Настройка единого входа Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Ceridian Dayforce HCM.

**tooconfigure Azure AD единого входа с Ceridian Dayforce HCM, выполните следующие шаги hello.**

1. В hello в hello портала Azure **Ceridian Dayforce HCM** странице интеграции приложения щелкните **единого входа**.

    ![Ссылка "Настройка единого входа"][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_samlbase.png)

3. На hello **URL-адреса и домена HCM Dayforce Ceridian** выполните следующие шаги hello:

    ![Настройка единого входа](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_url.png)
    
    а. В hello **на URL-адрес входа** textbox hello введите URL-адрес, используемый вашей пользователей на toosign tooyour Ceridian Dayforce HCM приложения.
    
    | Среда | URL-адрес |
    | :-- | :-- |
    | Рабочая среда | `https://sso.dayforcehcm.com/<DayforcehcmNamespace>` |
    | Тестирование | `https://ssotest.dayforcehcm.com/<DayforcehcmNamespace>` |
    
    b. В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:
    
    | Среда | URL-адрес |
    | :-- | :-- |
    | Рабочая среда | `https://ncpingfederate.dayforcehcm.com/sp` |
    | Тестирование | `https://fs-test.dayforcehcm.com/sp` |
    
    c. В hello **URL-адрес ответа** textbox hello введите URL-адрес, используемый Azure AD toopost hello ответа.
    
    | Среда | URL-адрес |
    | :-- | :-- |
    | Рабочая среда | `https://ncpingfederate.dayforcehcm.com/sp/ACS.saml2` |
    | Тестирование | `https://fs-test.dayforcehcm.com/sp/ACS.saml2` |
    
    > [!NOTE] 
    > Эти значения приведены в качестве примера. Обновить значения hello фактический идентификатор, URL-адрес ответа и URL-адрес входа. Обратитесь к [группа поддержки клиента HCM Dayforce Ceridian](https://www.ceridian.com/contact-us/index.html) tooget эти значения.

4. На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.

    ![ссылку для скачивания сертификата Hello](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_certificate.png) 

5. Приложение Ceridian Dayforce HCM ожидает утверждения SAML hello в определенном формате. Работать с [Ceridian Dayforce HCM поддержки](https://www.ceridian.com/contact-us/index.html) первый идентификатор пользователя hello tooidentify. Корпорация Майкрософт рекомендует использовать hello **«name»** атрибут в качестве идентификатора пользователя. Вы можете управлять hello значения этих атрибутов из hello **атрибуты пользователя** раздел на странице интеграции приложений. пример Hello следующий снимок экрана для этого.  

    ![Настройка единого входа](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_07.png)

6. В hello **атрибуты пользователя** раздела, посвященного hello **единого входа** диалогового окна, настроить атрибутов токена SAML, как показано в приведенном выше рисунке hello и выполнять hello следующие шаги:
    
    | Имя атрибута  | Значение атрибута |
    | --------------- | -------------------- |    
    | name  | user.extensionattribute2 |    

    а. Нажмите кнопку **добавить атрибут** tooopen hello **Добавление атрибута** диалогового окна.

    ![Настройка единого входа](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_attribute_04.png)

    ![Настройка единого входа](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_attribute_05.png)
    
    b. В hello **имя** в текстовое поле имя атрибута типа hello, показанный для этой строки.

    c. В hello **значение** список, атрибут пользователя выберите hello требуется toouse вашей реализации.
    Например, если нужно toouse hello EmployeeID как уникальный идентификатор пользователя, и значение атрибута hello были сохранены в hello ExtensionAttribute2, выберите **user.extensionattribute2**.
    
    d. Нажмите кнопку **ОК**.

7. Нажмите кнопку **Сохранить** .

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_400.png)
    
8. На hello **Ceridian Dayforce HCM конфигурации** щелкните **Настройка HCM Dayforce Ceridian** tooopen **Настройка входа** окна. Копировать hello **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**

    ![Настройка Ceridian Dayforce HCM](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_configure.png) 

9. tooconfigure единого входа на **Ceridian Dayforce HCM** стороны, необходимо загрузить hello toosend **метаданные в формате XML** и **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** слишком[Ceridian Dayforce HCM поддержки](https://www.ceridian.com/contact-us/index.html).

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello ** Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD

Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

   ![Создание тестового пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello hello левой панели портала Azure щелкните hello **Azure Active Directory** кнопки.

    ![Кнопка Hello Azure Active Directory](./media/active-directory-saas-ceridiandayforcehcm-tutorial/create_aaduser_01.png)

2. слишком go toodisplay hello список пользователей,**пользователей и групп**, а затем нажмите кнопку **всех пользователей**.

    ![Здравствуйте, «Пользователи и группы» и «Все пользователи» ссылки](./media/active-directory-saas-ceridiandayforcehcm-tutorial/create_aaduser_02.png)

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** вверху hello hello **всех пользователей** диалоговое окно.

    ![Кнопка "Добавить" Hello](./media/active-directory-saas-ceridiandayforcehcm-tutorial/create_aaduser_03.png)

4. В hello **пользователя** диалогового окна выполните следующие шаги hello:

    ![диалоговое окно приветствия пользователя](./media/active-directory-saas-ceridiandayforcehcm-tutorial/create_aaduser_04.png)

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** поле типа hello адрес электронной почты пользователя Саймон Britta.

    c. Выберите hello **Показать пароль** флажок и запишите значение hello, отображаемый в hello **пароль** поле.

    d. Щелкните **Создать**.
 
### <a name="create-a-ceridian-dayforce-hcm-test-user"></a>Создание тестового пользователя Ceridian Dayforce HCM

Цель этого раздела Hello — toocreate пользователя с именем Саймон Britta в Ceridian Dayforce HCM. Работать с hello [Ceridian Dayforce HCM поддержки](https://www.ceridian.com/contact-us/index.html) tooget пользователей, добавленных в hello Ceridian Dayforce HCM приложения. 

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooCeridian Dayforce HCM.

![Назначение пользователя][200] 

**tooassign Britta Simon tooCeridian Dayforce HCM выполните hello следующие шаги.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **Ceridian Dayforce HCM**.

    ![Настройка единого входа](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.

### <a name="assign-hello-azure-ad-test-user"></a>Назначить hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooCeridian Dayforce HCM.

![Назначение пользователям ролей hello][200] 

**tooassign Britta Simon tooCeridian Dayforce HCM выполните hello следующие шаги.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **Ceridian Dayforce HCM**.

    ![ссылка Ceridian Dayforce HCM Hello в списке приложений hello](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_app.png)  

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Hello ссылку «Пользователи и группы»][202]

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![область назначения, добавьте Hello][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="test-single-sign-on"></a>Проверка единого входа

Цель этого раздела Hello является tootest настройки единого входа Azure AD с помощью панели доступа "hello".  
При нажатии кнопки hello Ceridian Dayforce HCM плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour Ceridian Dayforce HCM приложения. 

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_203.png

