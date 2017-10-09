---
title: "Руководство по интеграции Azure Active Directory с Mozy Enterprise | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory с Mozy Enterprise."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 489b5e62-85c2-45c9-8766-326632d48114
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: jeedes
ms.openlocfilehash: bab0df4f3621b784cd8edfda3c8e10fe5a7ced9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mozy-enterprise"></a>Учебник. Интеграция Azure Active Directory с Mozy Enterprise

В этом учебнике вы узнаете, как toointegrate Mozy Enterprise с Azure Active Directory (Azure AD).

Интеграция Mozy Enterprise с Azure AD предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooMozy предприятия
- Можно включить на пользователей tooautomatically get вошедшего tooMozy предприятия (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с Mozy Enterprise, нужно hello следующих элементов:

- подписка Azure AD;
- подписка с поддержкой единого входа Mozy Enterprise.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление Mozy Enterprise из коллекции hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-mozy-enterprise-from-hello-gallery"></a>Добавление Mozy Enterprise из коллекции hello
tooconfigure hello интеграции Mozy Enterprise в Azure AD, вы должны tooadd Mozy Enterprise из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd Mozy Enterprise из коллекции hello, выполните следующие шаги hello.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Приложения][3]

4. Введите в поле поиска hello **Mozy Enterprise**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_search.png)

5. В панели результатов hello выберите **Mozy Enterprise**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описаны настройка и проверка единого входа Azure AD в Mozy Enterprise с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователя аналог hello в Mozy Enterprise — tooa пользователя в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в Mozy Enterprise должен установить toobe.

В Mozy Enterprise, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.

tooconfigure и теста Azure AD единого входа с Mozy Enterprise, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя Mozy Enterprise](#creating-a-mozy-enterprise-test-user)**  -toohave аналог Саймон Britta в Mozy Enterprise, который представляет связанный toohello Azure AD пользователя.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Mozy Enterprise.

**tooconfigure Azure AD единого входа с Mozy Enterprise, выполните следующие шаги hello.**

1. В hello в hello портала Azure **Mozy Enterprise** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_samlbase.png)

3. На hello **Mozy Enterprise доменов и URL-адреса** выполните следующие шаги hello:

    ![Настройка единого входа](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_url.png)

    В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<tenantname>.Mozyenterprise.com`

    > [!NOTE] 
    > Это значение приведено для справки. Измените значение этого параметра hello фактический URL-адрес входа. Обратитесь к [группа поддержки клиент Mozy Enterprise](http://support.mozy.com/) tooget это значение.

4. На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.

    ![Настройка единого входа](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_400.png)

6. На hello **Mozy Enterprise конфигурации** щелкните **Настройка Mozy Enterprise** tooopen **Настройка входа** окна. Копировать hello **идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**

    ![Настройка единого входа](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_configure.png) 

7. В другом окне веб-браузера войдите на сайт Mozy Enterprise компании в качестве администратора.

8. В hello **конфигурации** щелкните **политика проверки подлинности**.
   
   ![Политика аутентификации](./media/active-directory-saas-mozy-enterprise-tutorial/ic777314.png "Политика аутентификации")

9. На hello **политика проверки подлинности** выполните следующие шаги hello:
   
   ![Политика аутентификации](./media/active-directory-saas-mozy-enterprise-tutorial/ic777315.png "Политика аутентификации")
   
   а. Для параметра **Поставщик** выберите значение **Служба каталогов**.
   
   b. Выберите **Использовать LDAP для отправки**.
   
   c. Нажмите кнопку hello **проверку подлинности SAML** вкладки.
   
   d. Вставить **SAML единого входа URL-адрес службы**, которого вы скопировали из портала Azure hello в hello **URL-адрес проверки подлинности** текстового поля.
   
   д. Вставить **идентификатор сущности SAML**, которой копируются hello портал Azure в hello **конечная точка SAML** текстового поля.
   
   f. Откройте загруженный сертификат в кодировке base-64 в блокноте, hello копирования содержимого его в буфер обмена, а затем вставьте весь сертификат в hello **сертификат SAML** текстового поля.
   
   ж. Выберите **Включить единый вход для администраторов toolog вход с помощью своих сетевых учетных данных**.
   
   h. Нажмите кнопку **Сохранить изменения**.

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-mozy-enterprise-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-mozy-enterprise-tutorial/create_aaduser_02.png) 

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-mozy-enterprise-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-mozy-enterprise-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-a-mozy-enterprise-test-user"></a>Создание тестового пользователя Mozy Enterprise

В порядке tooenable toolog пользователей Azure AD в Mozy Enterprise их необходимо подготовить в Mozy Enterprise. В случае hello Mozy Enterprise Подготовка выполняется вручную.

>[!NOTE]
>Можно использовать любые другие Mozy Enterprise пользователя средства создания учетных записей или интерфейсы API, предоставляемые Mozy Enterprise tooprovision учетных записей пользователей AAD.

**tooprovision учетных записей пользователей, выполните следующие действия hello:**

1. Войдите в tooyour **Mozy Enterprise** клиента.

2. Щелкните **Users** (Пользователи), а затем — **Add New User** (Добавить нового пользователя).
   
   ![Пользователи](./media/active-directory-saas-mozy-enterprise-tutorial/ic777317.png "Пользователи")
   
   >[!NOTE]
   >Hello **добавить пользователя** параметр отображается только в том случае, если **Mozy** выбран в качестве поставщика hello под **политика проверки подлинности**. Если настроена проверка подлинности SAML, затем hello пользователи добавляются автоматически при их первом входе с использованием единого входа на.
    
3. На hello пользователя диалоговое окно создания выполните следующие шаги hello.
   
   ![Добавление пользователей](./media/active-directory-saas-mozy-enterprise-tutorial/ic777318.png "добавление пользователей")
   
   а. Из hello **выберите группу** выберите группу.
   
   b. Из hello **выборе типа создаваемого пользователя** выберите тип.
   
   c. В hello **Username** текстовое поле, имя типа hello hello Azure AD пользователя.
   
   d. В hello **электронной почты** в текстовое поле адрес электронной почты типа hello hello Azure AD пользователя.
   
   д. Выберите **Отправить пользователю электронное сообщение с указаниями**.
   
   f. Щелкните **Добавить пользователей**.

     >[!NOTE]
     > После создания пользователя hello, сообщение электронной почты будет отправлено toohello пользователя Azure AD, который включает учетную запись hello tooconfirm ссылку, чтобы она стала активной.

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooMozy предприятия.

![Назначение пользователя][200] 

**tooassign Britta Simon tooMozy Enterprise, выполните следующие шаги hello.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **Mozy Enterprise**.

    ![Настройка единого входа](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.

При нажатии кнопки Mozy Enterprise плитки в панели доступа hello hello, должно появиться страница входа приложения Mozy Enterprise.
Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_203.png

