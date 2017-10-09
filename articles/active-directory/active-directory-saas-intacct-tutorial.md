---
title: "Учебник. Интеграция Azure Active Directory с Intacct | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Intacct."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 92518e02-a62c-4b1b-a8e9-2803eb2b49ac
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 3500039615166c2f61fb408d85bb82dfaefba134
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-intacct"></a>Руководство. Интеграция Azure Active Directory с Intacct

В этом учебнике вы узнаете, как toointegrate Intacct с Azure Active Directory (Azure AD).

Интеграция Intacct с Azure AD предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooIntacct
- Можно включить на пользователей tooautomatically get вошедшего tooIntacct (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с Intacct требуется hello следующих элементов:

- подписка Azure AD;
- подписка с поддержкой единого входа Intacct.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление Intacct из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-intacct-from-hello-gallery"></a>Добавление Intacct из галереи hello
tooconfigure hello интеграции Intacct в Azure AD, вы должны tooadd Intacct из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd Intacct из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Приложения][3]

4. Введите в поле поиска hello **Intacct**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_search.png)

5. В панели результатов hello выберите **Intacct**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в Intacct с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Intacct является tooa в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в Intacct должен установить toobe.

В Intacct, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.

tooconfigure и теста Azure AD единого входа с Intacct, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя, прошедшего Intacct](#creating-an-intacct-test-user)**  -toohave аналог Саймон Britta в Intacct, который представляет связанный toohello Azure AD пользователя.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Intacct.

**tooconfigure Azure AD единого входа с Intacct, выполните следующие шаги hello.**

1. В hello в hello портала Azure **Intacct** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_samlbase.png)

3. На hello **URL-адреса и домена Intacct** выполните следующие шаги hello:

    ![Настройка единого входа](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_url.png)

    В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:
    | |
    |--|
    | `https://<companyname>.intacct.com/ia/acct/sso_response.phtml`|
    | `https://www.intacct.com/ia/acct/sso_response.phtml` |

    > [!NOTE] 
    > Это значение приведено для справки. Измените значение этого параметра hello фактический URL-адрес ответа. Обратитесь к [Intacct поддержки](https://us.intacct.com/support) tooget это значение.

4. На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.

    ![Настройка единого входа](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-intacct-tutorial/tutorial_general_400.png)

6. На hello **конфигурации Intacct** щелкните **Настройка Intacct** tooopen **Настройка входа** окна. Копировать hello **идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**

    ![Настройка единого входа](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_configure.png) 

7. В другом окне браузера Войдите на сайте компании tooyour Intacct с правами администратора.

8. Нажмите кнопку hello **компании** , а затем щелкните **сведения о компании**.

    ![Организация](./media/active-directory-saas-intacct-tutorial/ic790037.png "Организация")

9. Нажмите кнопку hello **безопасности** , а затем щелкните **изменить**.

    ![Безопасность](./media/active-directory-saas-intacct-tutorial/ic790038.png "Безопасность")

10. В hello **единого входа (SSO)** выполните следующие шаги hello:

    ![Единый вход](./media/active-directory-saas-intacct-tutorial/ic790039.png "Единый вход")

    а. Установите флажок **Включить единый вход**.

    b. Выберите для параметра **Identity provider type** (Тип поставщика удостоверений) значение **SAML 2.0**.

    c. В **URL-адрес издателя** текстовое значение hello вставить **идентификатор сущности SAML** скопирован из портала Azure.
   
    d. В **URL-адрес входа** текстовое значение hello вставить **SAML единого входа URL-адрес службы** скопирован из портала Azure.

    д. Откройте ваш **base-64** закодированный сертификат в блокноте, hello копирования содержимого его в буфер обмена, а затем вставьте его toohello **сертификат** поле.
   
    f. Щелкните **Сохранить**.

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-intacct-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-intacct-tutorial/create_aaduser_02.png) 

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-intacct-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-intacct-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-an-intacct-test-user"></a>Создание тестового пользователя Intacct

tooset пользователей Azure AD, они смогут войти в tooIntacct, их необходимо подготовить в Intacct. Эта подготовка для Intacct выполняется вручную.

**tooprovision учетных записей пользователей, выполните следующие шаги hello.**

1. Войдите в tooyour **Intacct** клиента.

2. Нажмите кнопку hello **компании** , а затем щелкните **пользователей**.

    ![Пользователи](./media/active-directory-saas-intacct-tutorial/ic790041.png "Пользователи")
3. Нажмите кнопку hello **добавить** вкладки.

    ![Добавление](./media/active-directory-saas-intacct-tutorial/ic790042.png "Добавление")
4. В hello **сведения о пользователе** выполните следующие шаги hello:

    ![Сведения о пользователе](./media/active-directory-saas-intacct-tutorial/ic790043.png "Сведения о пользователе")

    а. Введите hello **идентификатор пользователя**, hello **Фамилия**, **имя**, hello **адрес электронной почты**, hello **заголовка**, и hello **Phone** учетной записи Azure AD, которые должны tooprovision hello **сведения о пользователе** раздела.

    b. Выберите hello **права доступа администратора** нужных tooprovision учетной записи Azure AD.
   
    c. Щелкните **Сохранить**. Hello владельцем учетной записи Azure AD получает сообщение электронной почты и следует tooconfirm ссылку свою учетную запись, чтобы она стала активной.

>[!NOTE]
>tooprovision учетных записей пользователей Azure AD, можно использовать другие инструменты создания учетных записей Intacct или API-интерфейсы, предоставляемые Intacct.
        
### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooIntacct доступа.

![Назначение пользователя][200] 

**tooassign tooIntacct Britta Simon выполните следующие шаги hello.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **Intacct**.

    ![Настройка единого входа](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.

Если щелкнуть плитку Intacct hello в hello панели доступа, вы должны автоматически входить в tooyour Intacct приложения.

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_203.png

