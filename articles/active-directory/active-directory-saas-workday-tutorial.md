---
title: "Руководство. Интеграция Azure Active Directory с Workday | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и рабочего дня."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e9da692e-4a65-4231-8ab3-bc9a87b10bca
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: aaa41e372e45f464c4540a70fc79c98dbc06d6b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workday"></a>Руководство. Интеграция Azure Active Directory с Workday

В этом учебнике вы узнаете, как toointegrate дня с помощью Azure Active Directory (Azure AD).

Интеграция рабочего дня с Azure AD предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooWorkday
- Можно включить на пользователей tooautomatically get вошедшего tooWorkday (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с Workday требуется hello следующих элементов:

- подписка Azure AD;
- подписка Workday с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление рабочего дня из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-workday-from-hello-gallery"></a>Добавление рабочего дня из галереи hello
tooconfigure hello интеграции рабочего дня в Azure AD, вы должны tooadd рабочего дня из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd рабочего дня из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Приложения][3]

4. Введите в поле поиска hello **Workday**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-workday-tutorial/tutorial_workday_search.png)

5. В панели результатов hello, выберите **Workday**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-workday-tutorial/tutorial_workday_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в Workday с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в рабочий день является tooa в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в рабочий день должен установить toobe.

Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в рабочий день.

tooconfigure и теста Azure AD единого входа с рабочего дня, необходимы следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя Workday](#creating-a-workday-test-user)**  -toohave аналог Саймон Britta в рабочий день, представление связанных toohello Azure AD пользователя.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении рабочего дня.

**tooconfigure Azure AD единого входа с Workday, выполните следующие шаги hello.**

1. В hello в hello портала Azure **Workday** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-workday-tutorial/tutorial_workday_samlbase.png)

3. На hello **URL-адреса и домена рабочий день** выполните следующие шаги hello:

    ![Настройка единого входа](./media/active-directory-saas-workday-tutorial/tutorial_workday_url.png)

    а. В hello **URL-адрес входа** текстовое поле, значение типа hello как:`https://impl.workday.com/<tenant>/login-saml2.htmld`

    b. В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://impl.workday.com/<tenant>/login-saml.htmld`

    > [!NOTE] 
    > Эти значения не являются реальными hello. Обновите эти значения с hello фактический URL-адрес входа и URL-адрес ответа. URL-адрес ответа должен содержать поддомен (например, www, wd2, wd3, wd3-impl, wd5, wd5-impl). Можно указать адрес вида *http://www.myworkday.com*, но формат *http://myworkday.com* не поддерживается. Обратитесь к [группа поддержки клиента Workday](https://www.workday.com/en-us/partners-services/services/support.html) tooget эти значения. 
 

4. На hello **сертификат подписи SAML** щелкните **сертификата (Base64)** и затем сохраните файл сертификата hello на вашем компьютере.

    ![Настройка единого входа](./media/active-directory-saas-workday-tutorial/tutorial_workday_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-workday-tutorial/tutorial_general_400.png)

6. На hello **конфигурации рабочего дня** щелкните **Настройка Workday** tooopen **Настройка входа** окна. Копировать hello **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**

    ![Настройка единого входа](./media/active-directory-saas-workday-tutorial/tutorial_workday_configure.png) 
<CS>
7. В другом окне браузера войти в корпоративный сайт Workday tooyour с правами администратора.

8. Go слишком**меню \> Workbench**.
   
    ![Workbench](./media/active-directory-saas-workday-tutorial/IC782923.png "Workbench")

9. Go слишком**Администрирование учетной записи**.
   
    ![Администрирование учетной записи](./media/active-directory-saas-workday-tutorial/IC782924.png "Администрирование учетной записи")

10. Go слишком**изменение настройки клиента — безопасность**.
   
    ![Изменение параметров безопасности клиента](./media/active-directory-saas-workday-tutorial/IC782925.png "Изменение параметров безопасности клиента")

11. В hello **URL-адреса перенаправления** выполните следующие шаги hello:
   
    ![URL-адреса перенаправления](./media/active-directory-saas-workday-tutorial/IC7829581.png "URL-адреса перенаправления")
   
    а. Нажмите кнопку **Добавить строку**.
   
    b. В hello **URL-адрес перенаправления входа** текстового поля и hello **URL-адрес перенаправления Mobile** в текстовое поле типа hello **URL-адрес входа** , указанный на hello **домена рабочего дня и URL-адреса** раздел hello портал Azure.
   
    c. В hello в hello портала Azure **Настройка входа** окна, hello копирования **URL-адрес выхода**и вставьте его в hello **URL-адрес перенаправления выхода** текстового поля.
   
    d.  В **среды** в текстовое поле имя среды типа hello.  

    >[!NOTE]
    > Hello значение hello атрибута среды привязано значение toohello URL-адреса клиента hello:  
    >-Если hello доменное имя URL-адрес клиента Workday hello начинается с impl пример: *https://impl.workday.com/\<клиента\>/login-saml2.htmld*), hello **среды** атрибут должен иметь значение tooImplementation.  
    >-Если hello имя домена начинается по-другому, необходимо toocontact [группа поддержки клиента Workday](https://www.workday.com/en-us/partners-services/services/support.html) сопоставления hello tooget **среды** значение.

12. В hello **Настройка SAML** выполните следующие шаги hello:
   
    ![Настройка SAML](./media/active-directory-saas-workday-tutorial/IC782926.png "Настройка SAML")
   
    а.  Установите флажок **Включить проверку подлинности SAML**.
   
    b.  Нажмите кнопку **Добавить строку**.

13. В hello раздел Поставщики удостоверений SAML выполните следующие шаги hello.
   
    ![Поставщики удостоверений SAML](./media/active-directory-saas-workday-tutorial/IC7829271.png "Поставщики удостоверений SAML")
   
    а. В текстовом поле имя поставщика удостоверений hello, введите имя поставщика (например: *SPInitiatedSSO*).
   
    b. В hello в hello портала Azure **Настройка входа** окна, hello копирования **идентификатор сущности SAML** значение, а затем вставьте его в hello **издателя** текстовое поле.
   
    c. Установите флажок **Enable Workday Initiated Logout** (Включить выход, инициируемый Workday).
   
    d. В hello в hello портала Azure **Настройка входа** окна, hello копирования **URL-адрес выхода** значение, а затем вставьте его в hello **URL-адрес запроса выхода** текстового поля.

    д. Щелкните **Identity Provider Public Key Certificate** (Сертификат открытого ключа поставщика удостоверений), а затем нажмите кнопку **Создать**. 

    ![Создание](./media/active-directory-saas-workday-tutorial/IC782928.png "Создание")

    Е. Щелкните **Create x509 Public Key**(Создать открытый ключ x509). 

    ![Создание](./media/active-directory-saas-workday-tutorial/IC782929.png "Создание")


14. В hello **x509 Просмотр открытого ключа** выполните следующие шаги hello: 
   
    ![Просмотр открытого ключа x509](./media/active-directory-saas-workday-tutorial/IC782930.png "Просмотр открытого ключа x509") 
   
    а. В hello **имя** текстовом поле введите имя для сертификата (например: *PPE\_SP*).
   
    b. В hello **Valid From** текстового поля, типа hello значение сертификата.
   
    c.  В hello **Valid To** текстовое значение допустимым tooattribute hello типа сертификата.
   
    > [!NOTE]
    > Можно получить hello допустимые дату и hello допустимым toodate из сертификата загружен hello, дважды щелкнув его.  Hello даты будут указаны в списке hello **сведения** вкладки.
    > 
    >
   
    d.  Откройте сертификат в кодировке base-64 в блокноте, а затем hello копирования содержимого его.
   
    д.  В hello **сертификат** textbox hello вставить содержимое буфера обмена.
   
    f.  Нажмите кнопку **ОК**.

15. Выполните следующие шаги hello. 
   
    ![Настройка единого входа](./media/active-directory-saas-workday-tutorial/WorkdaySSOConfiguratio.png "Настройка единого входа")
   
    а.  Включить hello **x509 закрытого ключа**.
   
    b.  В hello **идентификатора поставщика услуг** введите **http://www.workday.com**.
   
    c.  Установите флажок **Включить проверку подлинности SAML, инициированную поставщиком услуг**.
   
    d.  В hello в hello портала Azure **Настройка входа** окна, hello копирования **SAML единого входа URL-адрес службы** значение, а затем вставьте его в hello **URL-адрес службы единого входа поставщика удостоверений** текстового поля.
   
    д. Выберите параметр **Не отклонять запрос проверки подлинности, инициированный поставщиком услуг**.
   
    Е. Для параметра **Authentication Request Signature Method** (Метод подписи запроса аутентификации) выберите значение **SHA256**. 
   
    ![Метод подписи запроса аутентификации](./media/active-directory-saas-workday-tutorial/WorkdaySSOConfiguration.png "Метод подписи запроса аутентификации") 
   
    g. Нажмите кнопку **ОК**. 
   
    ![ОК](./media/active-directory-saas-workday-tutorial/IC782933.png "ОК")
<CE>

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
>

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-workday-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-workday-tutorial/create_aaduser_02.png) 

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-workday-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-workday-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-a-workday-test-user"></a>Создание тестового пользователя Workday

tooget тестового пользователя, подготовленного в Workday, необходимо toocontact hello [группа поддержки клиента Workday](https://www.workday.com/en-us/partners-services/services/support.html).
Hello [группа поддержки клиента Workday](https://www.workday.com/en-us/partners-services/services/support.html) hello пользователя будет создан.

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooWorkday доступа.

![Назначение пользователя][200] 

**tooassign tooWorkday Britta Simon выполните следующие шаги hello.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **Workday**.

    ![Настройка единого входа](./media/active-directory-saas-workday-tutorial/tutorial_workday_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

Tootest параметры единого входа, откройте панель доступа hello. Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Руководство по настройке Google Apps для автоматической подготовки пользователей](active-directory-saas-workday-inbound-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-workday-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workday-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workday-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workday-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workday-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workday-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workday-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workday-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workday-tutorial/tutorial_general_203.png

