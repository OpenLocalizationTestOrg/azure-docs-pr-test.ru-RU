---
title: "Руководство по интеграции Azure Active Directory с Picturepark | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Picturepark."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 31c21cd4-9c00-4cad-9538-a13996dc872f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2017
ms.author: jeedes
ms.openlocfilehash: 3d826d3f73aad2f0d123f8697c6caafad7bc926a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-picturepark"></a>Руководство по интеграции Azure Active Directory с Picturepark

В этом учебнике вы узнаете, как toointegrate Picturepark с Azure Active Directory (Azure AD).

Интеграция Picturepark с Azure AD предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooPicturepark
- Можно включить на пользователей tooautomatically get вошедшего tooPicturepark (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с Picturepark требуется hello следующих элементов:

- подписка Azure AD;
- подписка Picturepark с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление Picturepark из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-picturepark-from-hello-gallery"></a>Добавление Picturepark из галереи hello
tooconfigure hello интеграции Picturepark в Azure AD, вы должны tooadd Picturepark из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd Picturepark из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Приложения][3]

4. Введите в поле поиска hello **Picturepark**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_search.png)

5. В панели результатов hello выберите **Picturepark**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в Picturepark с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Picturepark является tooa в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в Picturepark должен установить toobe.

В Picturepark, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.

tooconfigure и теста Azure AD единого входа с Picturepark, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя Picturepark](#creating-a-picturepark-test-user)**  -toohave аналог Саймон Britta в Picturepark, который представляет связанный toohello Azure AD пользователя.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в Picturepark приложения.

**tooconfigure Azure AD единого входа с Picturepark, выполните следующие шаги hello.**

1. В hello в hello портала Azure **Picturepark** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_samlbase.png)

3. На hello **URL-адреса и домена Picturepark** выполните следующие шаги hello:

    ![Настройка единого входа](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_url.png)

    а. В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<companyname>.picturepark.com`

    b. В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello: 
    
    |  |
    |--|
    | `https://<companyname>.current-picturepark.com`|
    | `https://<companyname>.picturepark.com`|
    | `https://<companyname>.next-picturepark.com`|
    | |

    > [!NOTE] 
    > Эти значения приведены в качестве примера. Обновить значения hello фактический URL-адрес входа и идентификатор. Обратитесь к [группа поддержки клиент Picturepark](https://picturepark.com/about/contact/) tooget эти значения. 
 
4. На hello **сертификат подписи SAML** раздел, hello копирования **ОТПЕЧАТОК** значение сертификата.

    ![Настройка единого входа](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-picturepark-tutorial/tutorial_general_400.png)

6. На hello **конфигурации Picturepark** щелкните **Настройка Picturepark** tooopen **Настройка входа** окна. Копировать hello **SAML единого входа URL-адрес службы** из hello **краткий справочник.**

    ![Настройка единого входа](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_configure.png) 

7. В другом окне веб-браузера войдите на сайт Picturepark своей компании в качестве администратора.

8. Щелкните hello панели инструментов в верхней части hello **Администрирование**, а затем нажмите кнопку **консоли управления**.
   
    ![Консоль управления](./media/active-directory-saas-picturepark-tutorial/ic795062.png "Консоль управления")

9. Щелкните **Authentication** (Аутентификация), а затем выберите **Identity providers** (Поставщики удостоверений).
   
    ![Аутентификация](./media/active-directory-saas-picturepark-tutorial/ic795063.png "Аутентификация")

10. В hello **конфигурация поставщика удостоверений** выполните следующие шаги hello:
   
    ![Конфигурация поставщика удостоверений](./media/active-directory-saas-picturepark-tutorial/ic795064.png "Конфигурация поставщика удостоверений")
   
    а. Щелкните **Добавить**.
  
    b. Введите имя конфигурации.
   
    c. Выберите **По умолчанию**.
   
    d. В **URI издателя** текстовое значение hello вставить **SAML единого входа URL-адрес службы** скопирован из портала Azure.
   
    д. В **отпечаток доверенного издателя** текстовое значение hello вставить **отпечаток** скопирован из **сертификат подписи SAML** раздела. 

11. Щелкните **JoinDefaultUsersGroup**.

12. tooset hello **Emailaddress** атрибута в hello **утверждения** введите `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress` и нажмите кнопку **Сохранить**.

      ![Конфигурация](./media/active-directory-saas-picturepark-tutorial/ic795065.png "Конфигурация")

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-picturepark-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-picturepark-tutorial/create_aaduser_02.png) 

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-picturepark-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-picturepark-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-a-picturepark-test-user"></a>Создание тестового пользователя Picturepark

В порядке tooenable toolog пользователей Azure AD в Picturepark их необходимо подготовить в Picturepark. В случае hello Picturepark Подготовка выполняется вручную.

**tooprovision учетной записи пользователя, выполните следующие шаги hello.**

1. Войдите в tooyour **Picturepark** клиента.

2. Щелкните hello панели инструментов в верхней части hello **Администрирование**, а затем нажмите кнопку **пользователей**.
   
    ![Пользователи](./media/active-directory-saas-picturepark-tutorial/ic795067.png "Пользователи")

3. В hello **Обзор пользователей** щелкните **New**.
   
    ![Управление пользователями](./media/active-directory-saas-picturepark-tutorial/ic795068.png "Управление пользователями")

4. На hello **Create User** диалогового окна hello выполните следующие действия действительного пользователя Active Directory Azure требуется tooprovision:
   
    ![Создание пользователя](./media/active-directory-saas-picturepark-tutorial/ic795069.png "Создание пользователя")
   
    а. В hello **адрес электронной почты** в текстовое поле типа hello **адрес электронной почты** пользователя hello  **BrittaSimon@contoso.com** .  
   
    b. В hello **пароль** и **подтверждение пароля** текстовые поля, типа hello **пароль** из BrittaSimon. 
   
    c. В hello **имя** в текстовое поле типа hello **имя** пользователя hello **Britta**. 
   
    d. В hello **Фамилия** в текстовое поле типа hello **Фамилия** пользователя hello **Simon**.
   
    д. В hello **компании** в текстовое поле типа hello **название компании** hello пользователя. 
   
    f. В hello **страны** текстового поля, выберите hello **страны** hello пользователя.
  
    ж. В hello **ZIP** в текстовое поле типа hello **ПОЧТОВЫЙ индекс** hello города.
   
    h. В hello **Город** в текстовое поле типа hello **название города** hello пользователя.

    i. В поле **Язык**укажите язык.
   
    j. Щелкните **Создать**.

>[!NOTE]
>Можно использовать любые другие Picturepark пользователя средства создания учетных записей или интерфейсы API, предоставляемые Picturepark tooprovision учетных записей пользователей Azure AD.
> 

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooPicturepark доступа.

![Назначение пользователя][200] 

**tooassign tooPicturepark Britta Simon выполните следующие шаги hello.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **Picturepark**.

    ![Настройка единого входа](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.

При нажатии кнопки hello Picturepark плитки в панели доступа hello, вы должны получить tooyour автоматически подписан на Picturepark приложения. Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_203.png

