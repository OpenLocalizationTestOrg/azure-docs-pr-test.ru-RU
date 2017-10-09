---
title: "Руководство по интеграции Azure Active Directory с 123ContactForm | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и 123ContactForm."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5211910a-ab96-4709-959a-524c4d57c43e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 931255887845edd1aa7f53b9051a82a2f898e055
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-123contactform"></a>Руководство по интеграции Azure Active Directory с 123ContactForm

В этом учебнике вы узнаете, как 123ContactForm toointegrate с Azure Active Directory (Azure AD).

Интеграция с Azure AD 123ContactForm предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ too123ContactForm
- Можно включить на пользователей tooautomatically get вошедшего too123ContactForm (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с 123ContactForm требуется hello следующих элементов:

- подписка Azure AD;
- подписка 123ContactForm с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление 123ContactForm из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-123contactform-from-hello-gallery"></a>Добавление 123ContactForm из галереи hello
tooconfigure hello интеграции 123ContactForm в Azure AD, вы должны 123ContactForm tooadd из списка tooyour коллекции hello управляемых приложений SaaS.

**123ContactForm tooadd из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Приложения][3]

4. Введите в поле поиска hello **123ContactForm**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_search.png)

5. В панели результатов hello выберите **123ContactForm**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в 123ContactForm с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в 123ContactForm является tooa в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в 123ContactForm должен установить toobe.

В 123ContactForm, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.

tooconfigure и теста Azure AD единого входа с 123ContactForm, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя 123ContactForm](#creating-a-123contactform-test-user)**  -toohave аналог Саймон Britta в 123ContactForm, который представляет связанный toohello Azure AD пользователя.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении 123ContactForm.

**tooconfigure Azure AD единого входа с 123ContactForm, выполните следующие шаги hello.**

1. В hello в hello портала Azure **123ContactForm** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_samlbase.png)

3. На hello **123ContactForm URL-адреса и домена** статьи, при желании tooconfigure приложения hello в **режиме, инициированный IDP**, выполните следующие шаги hello:

    ![Настройка единого входа](./media/active-directory-saas-123contactform-tutorial/url1.png)

    а. В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://www.123contactform.com/saml/azure_ad/<tenant_id>/metadata`

    b. В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://www.123contactform.com/saml/azure_ad/<tenant_id>/acs`

4. При необходимости приложение hello tooconfigure в **режиме, инициируемая SP**, выполните следующие шаги hello:

    ![Настройка единого входа](./media/active-directory-saas-123contactform-tutorial/url2.png)

    а. Нажмите кнопку hello **Показывать дополнительные параметры URL-адреса** параметр

    b. В hello **на URL-адрес входа** текстовом поле введите URL-адрес как:`https://www.123contactform.com/saml/azure_ad/<tenant_id>/sso`

    > [!NOTE] 
    > Эти значения приведены в качестве примера. Вам потребуется tooupdate эти значения из фактический URL-адреса и идентификатор, который описывается далее в учебнике hello.
    
5. На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.

    ![Настройка единого входа](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_certificate.png) 

6. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-123contactform-tutorial/tutorial_general_400.png)

7. tooconfigure единого входа на **123ContactForm** стороны, слишком перейдите[https://www.123contactform.com/form-2709121/](https://www.123contactform.com/form-2709121/) и выполнять hello следующие шаги:

    ![Настройка единого входа](./media/active-directory-saas-123contactform-tutorial/submit.png) 

    а. В hello **электронной почты** в текстовое поле адрес электронной почты пользователя hello т. е. для hello типа **BrittaSimon@Contoso.com**.

    b. Нажмите кнопку **отправить** и обзор hello метаданных XML-файл, который вы скачали из портала Azure.

    c. Щелкните **SUBMIT FORM** (Отправить форму).

8. На hello **Настройка параметров приложения Microsoft Azure AD единого входа -** выполнения hello следующие шаги:
    
    ![Настройка единого входа](./media/active-directory-saas-123contactform-tutorial/url3.png)

    а. При необходимости приложение hello tooconfigure в **режим, инициированный IDP**, hello копирования **идентификатор** значение для экземпляра и вставьте его в **идентификатор** текстовое поле в **123ContactForm URL-адреса и домена** раздела на портале Azure.
    
    b. При необходимости приложение hello tooconfigure в **режим, инициированный IDP**, hello копирования **URL-адрес ОТВЕТА** значение для экземпляра и вставьте его в **URL-адрес ответа** текстовое поле в **123ContactForm URL-адреса и домена** раздела на портале Azure.

    c. При необходимости приложение hello tooconfigure в **режим, инициируемая SP**, hello копирования **URL-адрес входа ON** значение для экземпляра и вставьте его в **на URL-адрес входа** текстовое поле в **123ContactForm URL-адреса и домена** раздела на портале Azure.

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-123contactform-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-123contactform-tutorial/create_aaduser_02.png) 

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-123contactform-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-123contactform-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-a-123contactform-test-user"></a>Создание тестового пользователя 123ContactForm

В время подготовки пользователей и после проверки подлинности пользователей в приложении hello автоматически создаются непосредственно поддерживает приложение.

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления too123ContactForm доступа.

![Назначение пользователя][200] 

**tooassign too123ContactForm Britta Simon выполните следующие шаги hello.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **123ContactForm**.

    ![Настройка единого входа](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.

При нажатии кнопки hello 123ContactForm плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour 123ContactForm приложения.
Дополнительные сведения о панели доступа см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_203.png

