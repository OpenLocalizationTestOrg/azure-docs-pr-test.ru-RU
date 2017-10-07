---
title: "Учебник. Интеграция Azure Active Directory с Jitbit Helpdesk | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Jitbit Helpdesk."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 15ce27d4-0621-4103-8a34-e72c98d72ec3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 0f6c837bbb910c1e84f7ed9da676c5ab40f75338
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jitbit-helpdesk"></a>Руководство. Интеграция Azure Active Directory с Jitbit Helpdesk

В этом учебнике вы узнаете, как toointegrate Jitbit Helpdesk с Azure Active Directory (Azure AD).

Интеграция Jitbit Helpdesk с Azure AD предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooJitbit службы технической поддержки
- Можно включить на пользователей tooautomatically get вошедшего tooJitbit службы технической поддержки (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с Jitbit Helpdesk, требуется hello следующих элементов:

- подписка Azure AD;
- подписка с поддержкой единого входа Jitbit Helpdesk.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление Jitbit Helpdesk из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-jitbit-helpdesk-from-hello-gallery"></a>Добавление Jitbit Helpdesk из галереи hello
tooconfigure hello интеграции Jitbit Helpdesk в Azure AD, вы должны tooadd Jitbit Helpdesk из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd Jitbit Helpdesk из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Приложения][3]

4. Введите в поле поиска hello **Jitbit Helpdesk**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_search.png)

5. В панели результатов hello выберите **Jitbit Helpdesk**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описаны настройка и проверка единого входа Azure AD в Jitbit Helpdesk с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Jitbit Helpdesk является tooa в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в Jitbit Helpdesk должен установить toobe.

В Jitbit Helpdesk, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.

tooconfigure и теста Azure AD единого входа с Jitbit Helpdesk, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя Jitbit Helpdesk](#creating-a-jitbit-helpdesk-test-user)**  -toohave аналог Саймон Britta в Jitbit Helpdesk, представление связанных toohello Azure AD пользователя.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в Jitbit Helpdesk приложения.

**tooconfigure Azure AD единого входа с Jitbit Helpdesk, выполните следующие шаги hello.**

1. В hello в hello портала Azure **Jitbit Helpdesk** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_samlbase.png)

3. На hello **Jitbit Helpdesk доменов и URL-адреса** выполните следующие шаги hello:

    ![Настройка единого входа](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_url.png)

    а. В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello: 
    | |     
    | ----------------------------------------|
    | `https://<hostname>/helpdesk/User/Login`|
    | `https://<tenant-name>.Jitbit.com`|
    | |
    
    > [!NOTE] 
    > Это значение приведено для справки. Измените значение этого параметра hello фактический URL-адрес входа. Обратитесь к [группа поддержки Jitbit Helpdesk клиента](https://www.jitbit.com/support/) tooget это значение. 
    
    b.  В hello **идентификатор** текстовом поле введите URL-адрес, следующим образом:`https://www.jitbit.com/web-helpdesk/`

    
 


4. На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.

    ![Настройка единого входа](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_400.png)

6. На hello **Jitbit Helpdesk конфигурации** щелкните **Настройка Jitbit Helpdesk** tooopen **Настройка входа** окна. Копировать hello **SAML единого входа URL-адрес службы** из hello **краткий справочник.**

    ![Настройка единого входа](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_configure.png) 

7. В другом окне браузера войдите на свой корпоративный веб-сайт Jitbit Helpdesk в качестве администратора.

8. Щелкните hello панели инструментов в верхней части hello **администрирования**.
   
    ![Администрирование](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777681.png "Администрирование")

9. Щелкните **Общие параметры**.
   
    ![Пользователи, организации и разрешения](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777680.png "Пользователи, организации и разрешения")

10. В hello **параметры проверки подлинности** конфигурации выполните следующие шаги hello:
   
    ![Параметры аутентификации](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777683.png "Параметры аутентификации")
    
    а. Выберите **включить SAML 2.0 единого входа в**, toosign использовать единый вход (SSO), с **OneLogin**.

    b. В hello **URL-адрес конечной точки** текстовое значение hello вставить **SAML единого входа URL-адрес службы** скопирован из портала Azure.

    c. Откройте ваш **base-64** закодированный сертификат в блокноте, hello копирования содержимого его в буфер обмена, а затем вставьте его toohello **сертификат X.509** текстового поля

    d. Нажмите кнопку **Сохранить изменения**.

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-jitbit-helpdesk-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-jitbit-helpdesk-tutorial/create_aaduser_02.png) 

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-jitbit-helpdesk-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-jitbit-helpdesk-tutorial/create_aaduser_04.png) 

    а. В hello **имя** в текстовое поле имя типа как **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-a-jitbit-helpdesk-test-user"></a>Создание тестового пользователя Jitbit Helpdesk

В порядке tooenable toolog пользователей Azure AD в Jitbit Helpdesk их необходимо подготовить в Jitbit Helpdesk.  В случае Jitbit Helpdesk hello Подготовка выполняется вручную.

**tooprovision учетной записи пользователя, выполните следующие шаги hello.**

1. Войдите в tooyour **Jitbit Helpdesk** клиента.

2. В меню в верхней части hello hello выберите **администрирования**.
   
    ![Администрирование](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777681.png "Администрирование")

3. Нажмите кнопку **Пользователи, компании и разрешения**.
   
    ![Пользователи, организации и разрешения](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777682.png "Пользователи, организации и разрешения")

4. Нажмите кнопку **Добавить пользователя**.
   
    ![Добавление пользователя](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777685.png "Добавление пользователя")
   
5. Hello создать раздел введите данные hello hello Azure AD от имени учетной записи требуется tooprovision следующим образом:

    ![Создание](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777686.png "Создание")
   
   а. В hello **Username** введите **BrittaSimon**, имя пользователя hello как hello портал Azure.

   b. В hello **электронной почты** текстовое поле, такие как тип адреса электронной почты пользователя hello  **BrittaSimon@contoso.com** .

   c. В hello **имя** в текстовое поле имя первого типа hello пользователя как **Britta**.

   d. В hello **Фамилия** текстовое поле, тип фамилию пользователя hello как **Simon**.
   
   д. Щелкните **Создать**.

>[!NOTE]
>Можно использовать любые другие Jitbit Helpdesk пользователя средства создания учетных записей или интерфейсы API, предоставляемые Jitbit Helpdesk tooprovision учетных записей пользователей Azure AD.
> 
        

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooJitbit службы технической поддержки.

![Назначение пользователя][200] 

**tooassign tooJitbit Britta Simon службы технической поддержки, выполните hello следующие шаги.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **Jitbit Helpdesk**.

    ![Настройка единого входа](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.

При нажатии кнопки Jitbit Helpdesk плитки в панели доступа hello hello, должно появиться страница входа приложения Jitbit Helpdesk.
Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_203.png

