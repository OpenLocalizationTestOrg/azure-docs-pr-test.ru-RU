---
title: "Руководство по интеграции Azure Active Directory с Canvas LMS | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Canvas LMS."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bfed291c-a33e-410d-b919-5b965a631d45
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/08/2017
ms.author: jeedes
ms.openlocfilehash: 8f4a09266a108e2c92326b0909dd0650b1c84d6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-canvas-lms"></a>Руководство по интеграции Azure Active Directory с Canvas LMS

В этом учебнике вы узнаете, как toointegrate холст с Azure Active Directory (Azure AD).

Интеграция с Azure AD Canvas предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooCanvas
- Можно включить на пользователей tooautomatically get вошедшего tooCanvas (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с Canvas, необходимо hello следующих элементов:

- подписка Azure AD;
- подписка Canvas с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление холст из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-canvas-from-hello-gallery"></a>Добавление холст из галереи hello
tooconfigure hello интеграции холста в Azure AD, вы должны tooadd холст из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd холст из галереи hello выполните hello следующие шаги.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Приложения][3]

4. Введите в поле поиска hello **холст**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_search.png)

5. В панели результатов hello выберите **холст**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в Canvas с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello на холсте является tooa в Azure AD. Другими словами связи между пользователя Azure AD и hello связанных пользователей на холсте должен установить toobe.

На холсте, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.

tooconfigure и теста Azure AD единого входа с Canvas, необходимо hello toocomplete следующие компоненты:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя холст](#creating-a-canvas-test-user)**  -toohave аналог Саймон Britta визуальный элемент, который представляет связанный toohello Azure AD пользователя.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении холста.

**tooconfigure Azure AD единого входа с Canvas, выполните следующие шаги hello.**

1. В hello в hello портала Azure **холст** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_samlbase.png)

3. На hello **URL-адреса и домена холст** выполните следующие шаги hello:

    ![Настройка единого входа](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_url.png)

    а. В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<tenant-name>.instructure.com`

    b. В hello **идентификатор** текстовое значение hello типа, используя следующий шаблон hello:`https://<tenant-name>.instructure.com/saml2`

    > [!NOTE] 
    > Эти значения приведены в качестве примера. Обновить значения hello фактический URL-адрес входа и идентификатор. Обратитесь к [группа поддержки клиент Canvas](https://community.canvaslms.com/community/help) tooget эти значения. 
 
4. На hello **сертификат подписи SAML** раздел, hello копирования **ОТПЕЧАТОК** значение сертификата.

    ![Настройка единого входа](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_400.png)

6. На hello **холст конфигурации** щелкните **Настройка холст** tooopen **Настройка входа** окна. Копировать hello **URL-адрес изменения пароля, URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**

    ![Настройка единого входа](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_configure.png) 
 
7. В другом окне браузера войдите в tooyour сайте компании с Canvas в качестве администратора.

8. Go слишком**курсы \> управляемых учетных записей \> Microsoft**.
   
    ![Canvas](./media/active-directory-saas-canvas-lms-tutorial/IC775990.png "Canvas")

9. Hello hello левой панели навигации выберите **проверки подлинности**, а затем нажмите кнопку **аутентификация**.
   
    ![Аутентификация](./media/active-directory-saas-canvas-lms-tutorial/IC775991.png "Аутентификация")

10. На странице текущая интеграция hello выполните следующие шаги hello.
   
    ![Текущая интеграция](./media/active-directory-saas-canvas-lms-tutorial/IC775992.png "Текущая интеграция")

    а. В **идентификатор сущности поставщика удостоверений** текстовое значение hello вставить **идентификатор сущности SAML** скопирован из портала Azure.

    b. В **на URL-адрес** текстовое значение hello вставить **SAML единого входа URL-адрес службы** скопирован из портала Azure.

    c. В **журнала URL-адреса выхода** текстовое значение hello вставить **URL-адрес выхода** скопирован из портала Azure.

    d. В **ссылка для изменения пароля** текстовое значение hello вставить **URL-адрес изменения пароля** скопирован из портала Azure. 

    д. В **отпечаток сертификата** текстовое поле, вставить hello **отпечаток** значение сертификата, который вы скопировали из портала Azure.      
        
    f. Из hello **входа атрибут** выберите **NameID**.

    ж. Из hello **формат идентификатора** выберите **emailAddress**.

    h. Нажмите кнопку **Сохранить параметры проверки подлинности**.

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-canvas-lms-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-canvas-lms-tutorial/create_aaduser_02.png) 

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-canvas-lms-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-canvas-lms-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-a-canvas-test-user"></a>Создание тестового пользователя Canvas

Пользователи toolog tooenable Azure AD в tooCanvas, их необходимо подготовить в Canvas.

В случае Canvas подготовка выполняется вручную.

**tooprovision учетной записи пользователя, выполните следующие шаги hello.**

1. Войдите в tooyour **холст** клиента.

2. Go слишком**курсы \> управляемых учетных записей \> Microsoft**.
   
   ![Canvas](./media/active-directory-saas-canvas-lms-tutorial/IC775990.png "Canvas")

3. Выберите раздел **Пользователи**.
   
   ![Пользователи](./media/active-directory-saas-canvas-lms-tutorial/IC775995.png "Пользователи")

4. Нажмите кнопку **Add New User**(Добавить нового пользователя).
   
   ![Пользователи](./media/active-directory-saas-canvas-lms-tutorial/IC775996.png "Пользователи")

5. На hello добавить диалоговое окно нового пользователя выполните следующие шаги hello.
   
   ![Добавление пользователя](./media/active-directory-saas-canvas-lms-tutorial/IC775997.png "Добавление пользователя")
   
   а. В hello **полное имя** текстовом поле введите имя пользователя, такие как hello **BrittaSimon**.

   b. В hello **электронной почты** текстовом поле введите адрес электронной почты hello пользователя как  **brittasimon@contoso.com** .

   c. В hello **входа** текстовом поле введите адрес электронной почты пользователя hello Azure AD как  **brittasimon@contoso.com** .

   d. Выберите **пользователя hello по электронной почте о создании этой учетной записи**.

   д. Нажмите кнопку **Add User**(Добавить пользователя).

>[!NOTE]
>Можно использовать любые другие холст пользователя средства создания учетных записей или интерфейсы API, предоставляемые холст tooprovision учетных записей пользователей AAD.

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooCanvas доступа.

![Назначение пользователя][200] 

**tooassign tooCanvas Britta Simon выполните следующие шаги hello.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **холст**.

    ![Настройка единого входа](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.

При выборе плитки холст hello в hello панели доступа, вы должны получить приложения tooyour автоматически подписан на холсте.
Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_203.png

