---
title: "Учебник. Интеграция Azure Active Directory с Igloo Software | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Igloo Software."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2eb625c1-d3fc-4ae1-a304-6a6733a10e6e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 406405d4faa6e56f1005a61e69a29ef2ef2eb34b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-igloo-software"></a>Учебник. Интеграция Azure Active Directory с Igloo Software

В этом учебнике вы узнаете, как toointegrate Igloo Software с Azure Active Directory (Azure AD).

Интеграция Igloo Software с Azure AD предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooIgloo программного обеспечения
- Можно включить на пользователей tooautomatically get вошедшего tooIgloo программного обеспечения (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с Igloo Software необходимо hello следующих элементов:

- подписка Azure AD;
- подписка Igloo Software с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление Igloo Software из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-igloo-software-from-hello-gallery"></a>Добавление Igloo Software из галереи hello
tooconfigure hello интеграции Igloo Software в Azure AD, вы должны tooadd Igloo Software из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd Igloo Software из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Приложения][3]

4. Введите в поле поиска hello **Igloo Software**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_search.png)

5. В панели результатов hello выберите **Igloo Software**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в Igloo Software для тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Igloo Software является tooa в Azure AD. Другими словами связи между пользователя Azure AD и hello связанных пользователей в Igloo Software должен установить toobe.

В Igloo Software, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.

tooconfigure и теста Azure AD единого входа с Igloo Software, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя, прошедшего Igloo Software](#creating-an-igloo-software-test-user)**  -toohave аналог Саймон Britta в Igloo Software, представление связанных toohello Azure AD пользователя.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Igloo Software.

**tooconfigure Azure AD единого входа с Igloo Software, выполните следующие шаги hello.**

1. В hello в hello портала Azure **Igloo Software** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_samlbase.png)

3. На hello **URL-адреса и домена программного обеспечения Igloo** выполните следующие шаги hello:

    ![Настройка единого входа](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_url.png)
    
    а. В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<company name>.igloocommmunities.com`

    b. В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<company name>.igloocommmunities.com/saml.digest`

    c. В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<company name>.igloocommmunities.com/saml.digest`

    > [!NOTE] 
    > Эти значения приведены в качестве примера. Обновить значения hello фактический идентификатор, URL-адрес ответа и URL-адрес входа. Обратитесь к [Igloo клиентское программное обеспечение поддержки](https://www.igloosoftware.com/services/support) tooget эти значения. 

4. На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.

    ![Настройка единого входа](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-igloo-software-tutorial/tutorial_general_400.png)
    
6. На hello **конфигурации программного обеспечения Igloo** щелкните **Настройка Igloo Software** tooopen **Настройка входа** окна. Копировать hello **URL-адрес выхода и SAML единого входа URL-адрес службы** из hello **краткий справочник.**

    ![Настройка единого входа](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_configure.png) 

7. В другом окне браузера Войдите на сайте компании Igloo Software tooyour в качестве администратора.

8. Go toohello **панели управления**.
   
     ![Панель управления](./media/active-directory-saas-igloo-software-tutorial/ic799949.png "Панель управления")

9. В hello **членства** щелкните **параметры входа**.
   
    ![Параметры входа](./media/active-directory-saas-igloo-software-tutorial/ic783968.png "Параметры входа")

10. В hello раздел конфигурации SAML, нажмите кнопку **Настройка проверки подлинности SAML**.
   
    ![Настройка SAML](./media/active-directory-saas-igloo-software-tutorial/ic783969.png "Настройка SAML")
   
11. В hello **Общая конфигурация** выполните следующие шаги hello:
   
    ![Общая конфигурация](./media/active-directory-saas-igloo-software-tutorial/ic783970.png "Общая конфигурация")

    а. В hello **имя подключения** текстовом поле введите имя файла для конфигурации.
   
    b. В hello **URL-адрес входа поставщика удостоверений** текстовое значение hello вставить **SAML единого входа URL-адрес службы** скопирован из портала Azure.
   
    c. В hello **URL-адрес выхода поставщика удостоверений** текстовое значение hello вставить **URL-адрес выхода** скопирован из портала Azure.
    
    d. Для параметра **Тип HTTP запроса и ответа о выходе** укажите значение **POST**.
   
    д. Откройте ваш **base-64** закодированный сертификат в блокноте, загруженные из портала Azure hello копирования содержимого его в буфер обмена, а затем вставьте его toohello **открытый сертификат** текстового поля.
    
12. В hello **Настройка ответа и аутентификации**, выполните следующие шаги hello:
    
    ![Конфигурация ответа и проверки подлинности](./media/active-directory-saas-igloo-software-tutorial/IC783971.png "Конфигурация ответа и проверки подлинности")
  
      а. Выберите для параметра **Поставщик удостоверений** значение **Microsoft ADFS**.
      
      b. Выберите для параметра **Тип идентификатора** значение **Адрес электронной почты**. 

      c. В hello **атрибут адреса электронной почты** введите **emailaddress**.

      d. В hello **атрибут имени** введите **givenname**.

      д. В hello **атрибут фамилии** введите **Фамилия**.

13. Выполните hello следующая конфигурация hello toocomplete действия.
    
    ![Создание пользователя при входе](./media/active-directory-saas-igloo-software-tutorial/IC783972.png "Создание пользователя при входе") 

     а. Выберите для параметра **Создание пользователя при входе** значение **Создать нового пользователя на веб-сайте при входе**.

     b. Выберите для параметра **Параметры входа** значение **Использовать кнопку SAML на экране входа**.

     c. Щелкните **Сохранить**.

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_02.png) 

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-an-igloo-software-test-user"></a>Создание тестового пользователя Igloo Software

Нет элемента действия для вас tooconfigure подготовки пользователей tooIgloo программного обеспечения.  

Когда назначенный пользователь пытается toolog в tooIgloo программного обеспечения с помощью панели доступа hello, Igloo Software проверяет, существует ли пользователь hello.  Если учетная запись пользователя отсутствует, Igloo Software автоматически создает ее.

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooIgloo программного обеспечения.

![Назначение пользователя][200] 

**tooassign tooIgloo Britta Simon программное обеспечение, выполните hello следующие шаги.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **Igloo Software**.

    ![Настройка единого входа](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.

При выборе плитки Igloo Software hello в hello панели доступа, вы должны получить приложения автоматически вошедшего tooyour Igloo Software.
Дополнительные сведения о панели доступа см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_203.png

