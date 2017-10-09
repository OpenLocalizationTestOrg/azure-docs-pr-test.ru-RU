---
title: "Руководство по интеграции Azure Active Directory с TimeOffManager | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и TimeOffManager."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 3685912f-d5aa-4730-ab58-35a088fc1cc3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: c871257bfb49883e31b1c4860a9d7faa70e9ab48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-timeoffmanager"></a>Учебник. Интеграция Azure Active Directory с TimeOffManager

В этом учебнике вы узнаете, как toointegrate TimeOffManager с Azure Active Directory (Azure AD).

Интеграция TimeOffManager с Azure AD предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooTimeOffManager
- Можно включить на пользователей tooautomatically get вошедшего tooTimeOffManager (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с TimeOffManager требуется hello следующих элементов:

- подписка Azure AD;
- Подписка с поддержкой единого входа TimeOffManager

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление TimeOffManager из коллекции hello
2. Настройка и проверка единого входа в Azure AD

## <a name="add-timeoffmanager-from-hello-gallery"></a>Добавление TimeOffManager из коллекции hello
tooconfigure hello интеграции TimeOffManager в Azure AD, вы должны tooadd TimeOffManager из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd TimeOffManager из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Приложения][3]

4. Введите в поле поиска hello **TimeOffManager**выберите **TimeOffManager** на панели «результат» и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Добавление из коллекции](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в TimeOffManager с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в TimeOffManager является tooa в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в TimeOffManager должен установить toobe.

В TimeOffManager, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.

tooconfigure и теста Azure AD единого входа с TimeOffManager, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя TimeOffManager](#create-a-timeoffmanager-test-user)**  -toohave аналог Саймон Britta в TimeOffManager, который представляет связанный toohello Azure AD пользователя.
4. **[Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#test-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configure-azure-ad-single-sign-on"></a>Настройка единого входа Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении TimeOffManager.

**Azure AD tooconfigure единого входа с TimeOffManager, выполните следующие шаги hello.**

1. В hello в hello портала Azure **TimeOffManager** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Вход на основе SAML](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_samlbase.png)

3. На hello **URL-адреса и домена TimeOffManager** выполните hello следующее:

     ![Раздел "Домены и URL-адреса приложения TimeOffManager"](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_url.png)

    В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://www.timeoffmanager.com/cpanel/sso/consume.aspx?company_id=<companyid>`

    > [!NOTE] 
    > Это значение приведено для справки. Измените значение этого параметра hello фактический URL-адрес ответа. Можно получить это значение из **на страницу параметров единого входа** описанной далее в учебнике hello или обратитесь к [TimeOffManager поддержки](http://www.timeoffmanager.com/contact-us.aspx).
 
4. На hello **сертификат подписи SAML** щелкните **сертификата (Base64)** и затем сохраните файл сертификата hello на вашем компьютере.

    ![Раздел "Сертификат подписи SAML"](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_certificate.png) 

5. Цель этого раздела Hello — toooutline как tooTimeOffManger tooauthenticate tooenable пользователей с учетной записью в Azure AD, используя федерацию на основе hello SAML протокола.
    
    Приложение TimeOffManger ожидает утверждения SAML hello в определенном формате, требующий вы tooadd настраиваемого атрибута сопоставления tooyour атрибутов токена конфигурация SAML. пример Hello следующий снимок экрана для этого.

    ![Атрибуты токена SAML](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_attrb.png "Атрибуты токена SAML")
    
    | Имя атрибута | Значение атрибута |
    | --- | --- |
    | Firstname |User.givenname |
    | Lastname |User.surname |
    | Email |User.mail |
    
    а.  Для каждой строки данных в таблице hello выше, щелкните **добавить атрибут пользователя**.
    
    ![Атрибуты токена SAML](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addattrb.png "Атрибуты токена SAML")
    
    ![Атрибуты токена SAML](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addattrb1.png "Атрибуты токена SAML")
    
    b.  В hello **имя атрибута** в текстовое поле имя атрибута типа hello, показанный для этой строки.
    
    c.  В hello **значение атрибута** текстовое поле, значение атрибута выберите hello, показанный для этой строки.
    
    d.  Нажмите кнопку **ОК**.
    
6. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_400.png)

7. На hello **конфигурации TimeOffManager** щелкните **Настройка TimeOffManager** tooopen **Настройка входа** окна. Копировать hello **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**

    ![Раздел "Конфигурация TimeOffManager"](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_configure.png) 

8. В другом окне веб-браузера войдите на свой корпоративный веб-сайт TimeOffManager в качестве администратора.

9. Go слишком**учетной записи \> параметры учетной записи \> параметры единого входа**.
   
   ![Параметры единого входа](./media/active-directory-saas-timeoffmanager-tutorial/ic795917.png "Параметры единого входа")
7. В hello **параметры единого входа** выполните следующие шаги hello:
   
   ![Параметры единого входа](./media/active-directory-saas-timeoffmanager-tutorial/ic795918.png "Параметры единого входа")
   
   а. Откройте сертификат в кодировке base-64 в блокноте, hello копирования содержимого его в буфер обмена, а затем вставьте весь сертификат в hello **сертификат X.509** текстового поля.
   
   b. В **издатель Idp** текстовое значение hello вставить **идентификатор сущности SAML** скопирован из портала Azure.
   
   c. В **URL-адрес конечной точки поставщика удостоверений** текстовое значение hello вставить **SAML единого входа URL-адрес службы** скопирован из портала Azure.
   
   d. Для параметра **Enforce SAML** (Применить SAML) выберите значение **No** (Нет).
   
   д. Для параметра **Auto-Create Users** (Автосоздание пользователей) выберите значение **Yes** (Да).
   
   f. В **URL-адрес выхода** текстовое значение hello вставить **URL-адрес выхода** скопирован из портала Azure.
   
   ж. Нажмите кнопку **Save Changes** (Сохранить изменения).

11. В **параметры единого входа** страницы значение hello копирования **URL-адрес службы утверждения потребителя** и вставьте его в hello **URL-адрес ответа** текстовое поле под **TimeOffManager URL-адреса и домена** раздела на портале Azure. 

      ![Параметры единого входа](./media/active-directory-saas-timeoffmanager-tutorial/ic795915.png "Параметры единого входа")

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    !["Пользователи и группы" > "Все пользователи"](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_02.png) 

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".
 
    ![Кнопка "Добавить"](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Диалоговое окно "Пользователь"](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="create-a-timeoffmanager-test-user"></a>Создание тестового пользователя TimeOffManager

В порядке tooenable toolog пользователей Azure AD в TimeOffManager они должны быть подготовленных tooTimeOffManager.  

TimeOffManager поддерживает автоматическую подготовку пользователей. С вашей стороны никакие действия не требуются.  

Hello пользователи добавляются автоматически во время первого входа hello единого входа.

>[!NOTE]
>Можно использовать любые другие TimeOffManager пользователя средства создания учетных записей или интерфейсы API, предоставляемые TimeOffManager tooprovision учетных записей пользователей Azure AD.
> 

### <a name="assign-hello-azure-ad-test-user"></a>Назначить hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooTimeOffManager доступа.

![Назначение пользователя][200] 

**tooassign tooTimeOffManager Britta Simon выполните следующие шаги hello.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **TimeOffManager**.

    ![TimeOffManager в списке приложений](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="test-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.

При нажатии кнопки hello TimeOffManager плитки в панели доступа hello, вы должны получить приложение автоматически вошедшего tooyour TimeOffManager. Дополнительные сведения о панели доступа см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_203.png

