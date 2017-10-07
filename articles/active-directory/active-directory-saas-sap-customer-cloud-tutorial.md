---
title: "Руководство по интеграции Azure Active Directory с SAP Cloud for Customer | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и облаком SAP для клиента."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 90154dab-eba2-4563-bcf0-f2acc797ea97
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: 0525ea81122458ab3ac24a5bdb0b5f628405dd05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-cloud-for-customer"></a>Руководство по интеграции Azure Active Directory с SAP Cloud for Customer

В этом учебнике вы узнаете, как SAP toointegrate облака для клиента в Azure Active Directory (Azure AD).

Интеграция облака SAP для клиента в Azure AD предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooSAP облака для клиента
- Вы можете включить вашей пользователей tooautomatically get вошедшего tooSAP облака для клиента (Single Sign-On) учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с облаком SAP для клиента требуется hello следующих элементов:

- подписка Azure AD;
- подписка SAP Cloud for Customer с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление облака SAP для клиента из коллекции hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-sap-cloud-for-customer-from-hello-gallery"></a>Добавление облака SAP для клиента из коллекции hello
tooconfigure hello интеграции облачных SAP для клиента в Azure AD, необходимо tooadd облака SAP для клиента из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd облака SAP для клиента из коллекции hello выполните hello следующие шаги.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Приложения][3]

4. Введите в поле поиска hello **облака SAP для клиента**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_search.png)

5. В панели результатов hello выберите **облака SAP для клиента**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в SAP Cloud for Customer с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в облаке SAP для клиента является tooa в Azure AD. Другими словами связи между пользователя Azure AD и hello связанных пользователей в облаке SAP для клиента должен установить toobe.

В облаке SAP для клиента, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.

tooconfigure и тестирования Azure AD единого входа с облаком SAP для клиента, необходимы следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание облака SAP для тестового пользователя клиента](#creating-a-sap-cloud-for-customer-test-user)**  -toohave аналог Саймон Britta в облаке SAP для клиента, который представляет связанный toohello Azure AD пользователя.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в облаке SAP для клиентского приложения.

**tooconfigure Azure AD единого входа с облаком SAP для клиента, выполните следующие шаги hello.**

1. В hello в hello портала Azure **облака SAP для клиента** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_samlbase.png)

3. На hello **облако SAP для домена клиента и URL-адреса** выполните следующие шаги hello:

    ![Настройка единого входа](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_url.png)

    а. В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<server name>.crm.ondemand.com`

    b. В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<server name>.crm.ondemand.com`

    > [!NOTE] 
    > Эти значения приведены в качестве примера. Обновить значения hello фактический URL-адрес входа и идентификатор. Обратитесь к [облако SAP для поддержки клиента клиента](https://www.sap.com/about/agreements.sap-cloud-services-customers.html) tooget эти значения. 

4. На hello **атрибуты пользователя** выполните следующие шаги hello:

    ![Настройка единого входа](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_attribute.png)

    а. В **идентификатор пользователя** список, выберите hello **ExtractMailPrefix()** функции.

    b. Из hello **Mail** список, атрибут пользователя выберите hello требуется toouse вашей реализации.
    Например если требуется toouse hello EmployeeID как уникальный идентификатор пользователя и хранящимся в hello ExtensionAttribute2 значение атрибута hello, выберите user.extensionattribute2.  

5. На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.

    ![Настройка единого входа](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_certificate.png) 

6. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_400.png)

7. На hello **облако SAP для конфигурации клиента** щелкните **Настройка облака SAP для клиента** tooopen **Настройка входа** окна. Копировать hello **SAML единого входа URL-адрес службы** из hello **краткий справочник.**

    ![Настройка единого входа](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_configure.png) 

8. tooget SSO настроен, выполните следующие шаги hello.
   
    а. Войдите на портал SAP Cloud for Customer с правами администратора.
   
    b. Перейдите toohello **приложения и общие задачи управления пользователя** и нажмите кнопку hello **поставщика удостоверений** вкладки.
   
    c. Нажмите кнопку **нового поставщика удостоверений** и выберите hello метаданных XML-файл, загруженный с портала Azure hello. Путем импорта метаданных hello, hello системы автоматически отправляет сертификат подписи требуется указать hello и сертификат шифрования.
   
    ![Настройка единого входа](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_54.png)
   
    d. Azure Active Directory требуется элемент hello URL-адрес службы утверждения потребителя в запросе SAML hello, поэтому выберите hello **включает утверждение потребителя URL-адрес службы** флажок.
   
    д. Щелкните **Activate Single Sign-On**(Активировать единый вход).
   
    Е. Сохраните изменения.
   
    ж. Нажмите кнопку hello **Мои системы** вкладки.
   
    ![Настройка единого входа](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_52.png)
   
    h. В текстовое поле **Azure AD Sign On URL** (URL-адрес входа Azure AD) вставьте значение **SAML Single Sign-On Service URL** (URL-адрес службы единого входа SAML), скопированное на портале Azure.
   
    ![Настройка единого входа](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_53.png)
   
    i. Указать ли hello сотрудника можно вручную выбрать между войти с помощью идентификатора пользователя и пароль или единого входа, выбрав hello **Выбор поставщика удостоверений вручную**.
   
    j. В hello **URL-адрес SSO** статьи, укажите hello URL-адрес, который должен использоваться с вашей toosign сотрудников в системе toohello. 
    В hello **tooEmployee URL-адрес отправки** список, можно выбрать между hello следующие параметры:
   
    **Non-SSO URL**
   
    Hello система отправляет только hello нормальная URL-адрес toohello сотрудника. Сотрудник Hello не может войти в систему с помощью единого входа и должны использовать пароль или сертификат вместо.
   
    **SSO URL** 
   
    Hello система отправляет только hello сотрудник toohello URL-адрес единого входа. Сотрудник Hello можно войти в систему с помощью единого входа. Перенаправляет запрос проверки подлинности через hello поставщика удостоверений.
   
    **Automatic Selection**
   
    Если единый вход не активен, hello система отправляет hello нормальная URL-адрес toohello сотрудника. Если активен единого входа, hello система проверяет, содержит ли сотрудника hello пароль. Если пароль, URL-адрес единого входа и URL-адрес единого входа не отправляются toohello сотрудника. Тем не менее если сотрудник hello не имеет пароля, toohello сотрудника отправляется только hello URL-адрес единого входа.
   
    k. Сохраните изменения.

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_02.png) 

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-a-sap-cloud-for-customer-test-user"></a>Создание тестового пользователя в SAP Cloud for Customer

В этом разделе описано, как создать пользователя Britta Simon в приложении SAP Cloud for Customer. Можно работать с [облако SAP для поддержки клиентов](https://www.sap.com/about/agreements.sap-cloud-services-customers.html) tooadd пользователей hello в hello SAP облачной платформы клиента. 

> [!NOTE]
> Убедитесь, что значение идентификатора имени должен совпадать с hello поле имени пользователя в hello SAP облачной платформы клиента.

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooSAP облака для клиента.

![Назначение пользователя][200] 

**tooassign tooSAP Britta Simon облака для клиента, выполните hello следующие шаги.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **облака SAP для клиента**.

    ![Настройка единого входа](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.

При нажатии кнопки hello облака SAP для клиента плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour облака SAP для клиентского приложения.
Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_203.png

