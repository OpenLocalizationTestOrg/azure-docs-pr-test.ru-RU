---
title: "Руководство по интеграции Azure Active Directory с Salesforce | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Salesforce."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2d7d420-dc91-41b8-a6b3-59579e043b35
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 1d848518ee30910e051cdc4746c599219f3b5a3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-salesforce"></a>Руководство по интеграции Azure Active Directory с Salesforce

В этом учебнике вы узнаете, как toointegrate Salesforce с Azure Active Directory (Azure AD).

Интеграция Salesforce с Azure AD предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooSalesforce
- Можно включить на пользователей tooautomatically get вошедшего tooSalesforce (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с Salesforce требуется hello следующих элементов:

- подписка Azure AD;
- подписка Salesforce с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление Salesforce из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-salesforce-from-hello-gallery"></a>Добавление Salesforce из галереи hello
tooconfigure hello интеграция Salesforce в Azure AD, вы должны tooadd Salesforce из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd Salesforce из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. Нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна "hello".

    ![Приложения][3]

4. Введите в поле поиска hello **Salesforce**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_search.png)

5. В панели результатов hello выберите **Salesforce**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в приложение Salesforce с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow hello аналог пользователя в Salesforce — tooa пользователя в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в Salesforce должен установить toobe.

Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в Salesforce.

tooconfigure и теста Azure AD единого входа с Salesforce, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя Salesforce](#creating-a-salesforce-test-user)**  -toohave аналог Саймон Britta в Salesforce, который представляет связанный toohello Azure AD пользователя.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе вы включите Azure AD единым входом в портал Azure hello и настроить единый вход в приложение Salesforce.

**tooconfigure Azure AD единого входа с Salesforce, выполните следующие шаги hello.**

1. В hello в hello портала Azure **Salesforce** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_samlbase.png)

3. На hello **URL-адреса и домена Salesforce** выполните следующие шаги hello:

    ![Настройка единого входа](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_url.png)

    В hello **URL-адрес входа** текстовое значение hello типа, используя следующий шаблон hello: 
   * Учетная запись предприятия: `https://<subdomain>.my.salesforce.com`
   * Учетная запись разработчика: `https://<subdomain>-dev-ed.my.salesforce.com`

    > [!NOTE] 
    > Эти значения не являются реальными hello. Обновите эти значения с hello фактический URL-адрес входа. Обратитесь к [группа поддержки клиента Salesforce](https://help.salesforce.com/support) tooget эти значения. 
 
4. На hello **сертификат подписи SAML** щелкните **сертификат** и затем сохраните файл сертификата hello на вашем компьютере.

    ![Настройка единого входа](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-salesforce-tutorial/tutorial_general_400.png)

6. На hello **конфигурации Salesforce** щелкните **Настройка Salesforce** tooopen **Настройка входа** окна. Копировать hello **идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.** 

    ![Настройка единого входа](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_configure.png) 
<CS>
7.  Откройте новую вкладку в браузере и войдите в учетную запись администратора Salesforce tooyour.

8.  Под hello **администратора** панели навигации щелкните **управления безопасностью** tooexpand hello связанных разделов. Затем щелкните **Параметры единого входа**.

    ![Настройка единого входа](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso.png)

9.  На hello **параметры единого входа** щелкните hello **изменить** кнопки.
    ![Настройка единого входа](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso-edit.png)

      > [!NOTE]
      > Если не удается tooenable параметры единого входа для учетной записи Salesforce, может потребоваться toocontact [группа поддержки клиента Salesforce](https://help.salesforce.com/support). 

10. Выберите **SAML Enabled** (SAML включен), а затем щелкните **Save** (Сохранить).

      ![Настройка единого входа](./media/active-directory-saas-salesforce-tutorial/sf-enable-saml.png)
11. tooconfigure единого входа параметры SAML, нажмите кнопку **New**.

    ![Настройка единого входа](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso-new.png)

12. На hello **SAML единого входа для изменения настроек** задайте hello конфигурации:

    ![Настройка единого входа](./media/active-directory-saas-salesforce-tutorial/sf-saml-config.png)

    а. Для hello **имя** введите понятное имя для этой конфигурации. Предоставить значение для **имя** автоматически заполнять hello **имя API** текстового поля.

    b. Вставить **идентификатор сущности SMAL** значение в hello **издателя** в Salesforce.

    c. В hello **идентификатор сущности textbox**, введите доменное имя Salesforce с помощью hello следующий шаблон:
      
      * Учетная запись предприятия: `https://<subdomain>.my.salesforce.com`
      * Учетная запись разработчика: `https://<subdomain>-dev-ed.my.salesforce.com`
      
    d. Нажмите кнопку **Обзор** или **выбрать файл** tooopen hello **tooUpload выбрать файл** диалоговое окно, выберите сертификат Salesforce и нажмите кнопку **откройте**tooupload hello сертификата.

    д. В поле **SAML Identity Type** (Тип удостоверения SAML) выберите значение **Assertion contains User's salesforce.com username** (Утверждение содержит имя пользователя salesforce.com).

    f. Для **расположения удостоверения SAML**выберите **удостоверение находится в элемент hello NameIdentifier оператора Subject hello**

    ж. Вставить **единого входа URL-адрес службы** в hello **URL-адрес входа поставщика удостоверений** в Salesforce.
    
    h. В поле **Service Provider Initiated Request Binding** (Связывание запросов, инициируемых поставщиком услуг) выберите значение **HTTP Redirect** (Перенаправление HTTP).
    
    i. Наконец, нажмите кнопку **Сохранить** tooapply единого входа параметры SAML.

13. На панели навигации слева hello в Salesforce щелкните **Управление доменами** tooexpand hello соответствующий раздел и нажмите кнопку **Мой домен**.

    ![Настройка единого входа](./media/active-directory-saas-salesforce-tutorial/sf-my-domain.png)

14. Прокрутите вниз toohello **настройки проверки подлинности** и нажмите кнопку hello **изменить** кнопки.

    ![Настройка единого входа](./media/active-directory-saas-salesforce-tutorial/sf-edit-auth-config.png)

15. В hello **службы проверки подлинности** статьи hello понятное имя конфигурации единого входа SAML и нажмите кнопку **Сохранить**.

    ![Настройка единого входа](./media/active-directory-saas-salesforce-tutorial/sf-auth-config.png)

    > [!NOTE]
    > Если выбрано более одной службы проверки подлинности, пользователи не запрошенные tooselect, какие службы проверки подлинности угодно toosign в систему при запуске среда tooyour Salesforce. Если вы не хотите toohappen, то следует **все остальные службы проверки подлинности не устанавливайте флажок**.
<CE>    
> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)


### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. На панели навигации слева hello в hello **портал Azure**, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-salesforce-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-salesforce-tutorial/create_aaduser_02.png) 

3. Вверху hello hello диалоговое окно, нажмите кнопку **добавить** tooopen hello **пользователя** диалогового окна.
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-salesforce-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-salesforce-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-a-salesforce-test-user"></a>Создание тестового пользователя Salesforce

В этом разделе вы создадите в Salesforce пользователя с именем Britta Simon. Приложение Salesforce поддерживает JIT-подготовку. Эта функция включена по умолчанию.
В этом разделе никакие действия с вашей стороны не требуются. Если пользователь еще не существует в Salesforce, создается новый, при попытке tooaccess Salesforce.

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooSalesforce доступа.

![Назначение пользователя][200] 

**tooassign tooSalesforce Britta Simon выполните следующие шаги hello.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **Salesforce**.

    ![Настройка единого входа](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

tootest входа параметры единого, откройте hello панель доступа по адресу [https://myapps.microsoft.com](https://myapps.microsoft.com/), затем войдите в hello тестовую учетную запись и нажмите кнопку **Salesforce**.

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Руководство по настройке Google Apps для автоматической подготовки пользователей](active-directory-saas-salesforce-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_203.png

