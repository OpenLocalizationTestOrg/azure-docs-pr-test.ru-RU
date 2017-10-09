---
title: "Руководство по интеграции Azure Active Directory с приложением Slack | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Slack."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ffc5e73f-6c38-4bbb-876a-a7dd269d4e1c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 7f0151401af4dc63d2f714d4b4f66380c4b51e0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-slack"></a>Учебник. Интеграция Azure Active Directory с Slack

В этом учебнике вы узнаете, как toointegrate временных резервов в Azure Active Directory (Azure AD).

Интеграция Slack с Azure AD предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooSlack
- Можно включить на пользователей tooautomatically get вошедшего tooSlack (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с Slack требуется hello следующих элементов:

- подписка Azure AD;
- подписка Slack с активированной функцией единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление Slack из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-slack-from-hello-gallery"></a>Добавление Slack из галереи hello
Интеграция hello tooconfigure резерва в Azure AD, необходимо tooadd Slack из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd Slack из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Приложения][3]

4. Введите в поле поиска hello **Slack**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-slack-tutorial/tutorial_slack_search.png)

5. В панели результатов hello выберите **Slack**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-slack-tutorial/tutorial_slack_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в Slack с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow какой пользователь hello аналога в Slack — tooa пользователя в Azure AD. Другими словами связи между пользователя Azure AD и hello связанных пользователей в Slack должен установить toobe.

В Slack, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.

tooconfigure и теста Azure AD единого входа с Slack, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание резерв тестового пользователя](#creating-a-slack-test-user)**  -toohave аналог Саймон Britta в Slack, который представляет связанный toohello Azure AD пользователя.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении резерв.

**tooconfigure Azure AD единого входа с Slack, выполните следующие шаги hello.**

1. В hello в hello портала Azure **Slack** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-slack-tutorial/tutorial_slack_samlbase.png)

3. На hello **URL-адреса и домена Slack** выполните следующие шаги hello:

    ![Настройка единого входа](./media/active-directory-saas-slack-tutorial/tutorial_slack_url.png)

    а. В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<companyname>.slack.com`

    b. В hello **идентификатор** текстовом поле введите URL-адрес hello:`https://slack.com`

    > [!NOTE] 
    > значение Hello не является вещественным числом. У вас есть tooupdate hello значение hello фактическое на URL-адрес входа. Обратитесь к [Slack поддержки](https://slack.com/help/contact) значение tooget hello
     
4. Резерв приложение ожидает утверждения SAML hello в определенном формате. Настройка следующих утверждений для этого приложения hello. Вы можете управлять hello значения этих атрибутов из hello»**атрибуты пользователя**» на странице интеграции приложения. пример Hello следующий снимок экрана для этого.
    
    ![Настройка единого входа](./media/active-directory-saas-slack-tutorial/tutorial_slack_attribute.png)

5. В hello **атрибуты пользователя** раздела, посвященного hello **единого входа** диалогового окна выберите **user.mail** как **идентификатор пользователя** и для каждой строки показано в следующей таблице hello выполните следующие шаги hello.
    
    | Имя атрибута | Значение атрибута |
    | --- | --- |
    | first_name | user.givenname |
    | last_name | user.surname |
    | User.Email | user.mail |  
    | User.Username | user.userprincipalname |

    а. Щелкните **атрибута** tooopen **изменение атрибута** диалогового окна введите и выполните следующие шаги hello:

    ![Настройка единого входа](./media/active-directory-saas-slack-tutorial/tutorial_slack_attribute1.png)

    а. В hello **имя** в текстовое поле имя атрибута типа hello, показанный для этой строки.
    
    b. Из hello **значение** список, выберите hello значение атрибута, отображаемое для этой строки.
    
    c. Щелкните **ОК**

6. На hello **сертификат подписи SAML** щелкните **сертификата (Base64)** и затем сохраните файл сертификата hello на вашем компьютере.

    ![Настройка единого входа](./media/active-directory-saas-slack-tutorial/tutorial_slack_certificate.png)

7. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-slack-tutorial/tutorial_general_400.png)

8. На hello **конфигурации Slack** щелкните **Настройка Slack** tooopen **Настройка входа** окна. Копировать hello **идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**

    ![Настройка единого входа](./media/active-directory-saas-slack-tutorial/tutorial_slack_configure.png) 

9.  В другом окне браузера войдите в tooyour корпоративный сайт Slack в качестве администратора.

10.  Перейдите в слишком**Microsoft Azure AD** перейдите слишком**параметры командного**.

     ![Настройка единого входа на стороне приложения](./media/active-directory-saas-slack-tutorial/tutorial_slack_001.png)

11.  В hello **параметры командного** щелкните hello **проверки подлинности** , а затем щелкните **изменение параметров**.

     ![Настройка единого входа на стороне приложения](./media/active-directory-saas-slack-tutorial/tutorial_slack_002.png)

12. На hello **параметры проверки подлинности SAML** диалоговое окно, выполните следующие шаги hello:

    ![Настройка единого входа на стороне приложения](./media/active-directory-saas-slack-tutorial/tutorial_slack_003.png)

    а.  В hello **конечная точка SAML 2.0 (HTTP)** текстовое значение hello вставить **SAML единого входа URL-адрес службы**, который вы скопировали из портала Azure.

    b.  В hello **издатель поставщика удостоверений** текстовое значение hello вставить **идентификатор сущности SAML**, который вы скопировали из портала Azure.

    c.  Откройте загруженный сертификат файл в блокноте, hello копирования содержимого его в буфер обмена, а затем вставьте его toohello **открытый сертификат** текстового поля.

    d. Задайте нужные команды резерв hello выше три параметра. Дополнительные сведения о параметрах hello приведено hello **руководство по выбору конфигурации единого входа в Slack** здесь. `https://get.slack.help/hc/articles/220403548-Guide-to-single-sign-on-with-Slack%60`

    д.  Щелкните **Сохранить конфигурацию**.
     
    <!-- Deselect **Allow users toochange their email address**.

    e.  Select **Allow users toochoose their own username**.

    f.  As **Authentication for your team must be used by**, select **It’s optional**. -->

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-slack-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-slack-tutorial/create_aaduser_02.png) 

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-slack-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-slack-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-a-slack-test-user"></a>Создание тестового пользователя Slack

Цель этого раздела Hello — toocreate пользователя с именем Саймон Britta в Slack. Приложение Slack поддерживает JIT подготовку. Эта функция включена по умолчанию.

В этом разделе никакие действия с вашей стороны не требуются. Новый пользователь создается во время попытки tooaccess Slack, если он еще не существует.

> [!NOTE]
> Если требуется toocreate пользователя вручную, необходимо tooContact [Slack поддержки](https://slack.com/help/contact).

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooSlack доступа.

![Назначение пользователя][200] 

**tooassign tooSlack Britta Simon выполните следующие шаги hello.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **Slack**.

    ![Настройка единого входа](./media/active-directory-saas-slack-tutorial/tutorial_slack_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.

При нажатии кнопки hello резерв плитки в Здравствуйте панели доступа, вы должны получить автоматически вошедшего tooyour резерв приложения.

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-slack-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-slack-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-slack-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-slack-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-slack-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-slack-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-slack-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-slack-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-slack-tutorial/tutorial_general_203.png

