---
title: "Руководство по интеграции Azure Active Directory с Menlo Security | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Menlo безопасности."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9e63fe6b-0ad0-405d-9e41-6a1a40a41df8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: jeedes
ms.openlocfilehash: 193d12eedf31f4f08e1d141936d6e918c36a2109
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-menlo-security"></a>Руководство по интеграции Azure Active Directory с Menlo Security

В этом учебнике вы узнаете, как toointegrate Menlo безопасности в Azure Active Directory (Azure AD).

Интеграция безопасности Menlo с Azure AD предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooMenlo безопасности
- Можно включить на пользователей tooautomatically get вошедшего tooMenlo безопасности (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если необходимо, чтобы tooknow см. Дополнительные сведения об интеграции приложений SaaS в Azure AD. [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с Menlo безопасности необходимо hello следующих элементов:

- подписка Azure AD;
- подписка Menlo Security с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление Menlo безопасности из коллекции hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-menlo-security-from-hello-gallery"></a>Добавление Menlo безопасности из коллекции hello
tooconfigure hello интеграции Menlo безопасности в Azure AD, вы должны tooadd Menlo безопасности из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd Menlo безопасности из коллекции hello, выполните следующие шаги hello.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Приложения][3]

4. Введите в поле поиска hello **Menlo безопасности**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_search.png)

5. В панели результатов hello выберите **безопасности Menlo**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в Menlo Security с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Menlo безопасности является tooa в Azure AD. Другими словами связи между пользователя Azure AD и hello связанных пользователей в системе безопасности Menlo должен установить toobe.

Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** Menlo безопасности.

tooconfigure и теста Azure AD единого входа с Menlo безопасности, необходимые hello toocomplete следующие стандартные блоки.

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя безопасности Menlo](#creating-a-menlo-security-test-user)**  -toohave аналог Саймон Britta в Menlo безопасности, который представляет связанный toohello Azure AD пользователя.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Menlo безопасности.

**tooconfigure Azure AD единого входа с безопасностью Menlo выполните следующие шаги hello.**

1. В hello в hello портала Azure **безопасности Menlo** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_samlbase.png)

3. На hello **Menlo безопасности домена и URL-адреса** выполните следующие шаги hello:

    ![Настройка единого входа](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_url.png)

    а. В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<subdomain>.menlosecurity.com/account/login`

    b. В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<subdomain>.menlosecurity.com/safeview-auth-server/saml/metadata`

    > [!NOTE] 
    > Эти значения не являются реальными hello. Обновить значения hello фактический URL-адрес входа и идентификатор. Обратитесь к [Menlo безопасности клиента поддержки](https://www.menlosecurity.com/menlo-contact) tooget эти значения. 
 
4. На hello **сертификат подписи SAML** щелкните **сертификата (Base64)** и затем сохраните файл сертификата hello на вашем компьютере.

    ![Настройка единого входа](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_400.png)

6. На hello **конфигурация безопасности Menlo** щелкните **Настройка безопасности Menlo** tooopen **Настройка входа** окна. Копировать hello **идентификатор сущности SAML**, и **SAML единого входа URL-адрес службы** из hello **краткий справочник.**

    ![Настройка единого входа](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_configure.png) 

7. tooconfigure единого входа на **безопасности Menlo** стороны, toohello входа **Menlo безопасности** веб-сайта от имени администратора.

8. В разделе **параметры** go слишком**проверки подлинности** и выполнять следующие действия:
    
    ![Настройка единого входа](./media/active-directory-saas-menlosecurity-tutorial/menlo_user_setup.png)

    а. Деления hello флажок **включить проверку подлинности пользователя с помощью SAML**.

    b. Выберите **разрешить внешний доступ** слишком**Да**.

    c. В разделе **SAML Provider** (Поставщик SAML) выберите **Azure Active Directory**.

    d. **Конечная точка SAML 2.0** : hello вставить **SAML единого входа URL-адрес службы** скопирован из портала Azure.

    д. **Идентификатор службы (издатель)** : hello вставить **идентификатор сущности SAML** скопирован из портала Azure.

    f. **Сертификат X.509** : Привет открыть **сертификата (Base64)** загружаются из hello портала Azure в Блокнот и вставьте его в этом поле.

    ж. Нажмите кнопку **Сохранить** toosave hello параметры.

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
 

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-menlosecurity-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-menlosecurity-tutorial/create_aaduser_02.png) 

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-menlosecurity-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-menlosecurity-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-a-menlo-security-test-user"></a>Создание тестового пользователя Menlo Security
 
В этом разделе описано, как создать пользователя Britta Simon в приложении Menlo Security. Работать с [Menlo безопасности клиента поддержки](https://www.menlosecurity.com/menlo-contact) tooadd пользователей hello hello Menlo безопасности платформы. Перед использованием единого входа необходимо создать и активировать пользователей. 

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooMenlo безопасности.

![Назначение пользователя][200] 

**tooassign tooMenlo Britta Simon безопасности, выполните hello следующие шаги.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **Menlo безопасности**.

    ![Настройка единого входа](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

В этом разделе описано, как проверить конфигурацию единого входа Azure AD.

Откройте окно браузера в «InPrivate» или «Анонимный» режим tootrigger новыми параметрами проверки подлинности.  В Internet Explorer нажмите клавиши CTRL+SHIFT+P.  В Chrome нажмите клавиши CTRL+SHIFT+N.  В hello закрытого просмотра окне обзора tooa защищенный ресурс и выполнения входа Azure AD.  После успешного входа в сеансе изоляции будет взят toohello запрошенного узла.

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_203.png

