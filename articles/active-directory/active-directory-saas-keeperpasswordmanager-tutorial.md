---
title: "Руководство по интеграции Azure Active Directory с Keeper Password Manager & Digital Vault | Документы Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и диспетчер паролей хранителю & цифровой хранилища."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e1a98f6a-2dae-4734-bdbf-4fba742a61d2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 01e59004e6bdccfca08094f9da6f82270d5028d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-keeper-password-manager--digital-vault"></a>Руководство по интеграции Azure Active Directory с Keeper Password Manager & Digital Vault

В этом учебнике вы узнаете, как toointegrate диспетчер паролей хранителю & цифровой хранилища в Azure Active Directory (Azure AD).

Интеграция с Azure AD диспетчер паролей хранителю & цифровой хранилища предоставляет следующие преимущества hello:

- Можно управлять в Azure AD, имеющего доступ к tooKeeper диспетчер паролей & цифровой хранилища
- Вы можете включить их учетные записи Azure AD вашей пользователей tooautomatically get вошедшего tooKeeper диспетчер паролей & цифровой хранилища (Single Sign-On)
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с диспетчер паролей хранителю & цифровой хранилища необходимо hello следующих элементов:

- подписка Azure AD;
- подписка на Keeper Password Manager & Digital Vault с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление диспетчера паролей хранителю & цифровой хранилища из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-keeper-password-manager--digital-vault-from-hello-gallery"></a>Добавление диспетчера паролей хранителю & цифровой хранилища из галереи hello
tooconfigure hello интеграции диспетчер паролей хранителю & цифровой хранилища в Azure AD, вы должны tooadd диспетчер паролей хранителю & цифровой хранилища из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd диспетчер паролей хранителю & цифровой хранилища из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Приложения][3]

4. Введите в поле поиска hello **диспетчер паролей хранителю & хранилище цифровых**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_search.png)

5. В панели результатов hello выберите **диспетчер паролей хранителю & цифровой хранилище**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в Keeper Password Manager & Digital Vault с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в диспетчер паролей хранителю & цифровой хранилища является tooa в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в диспетчер паролей хранителю & цифровой хранилища должен установить toobe.

В диспетчер паролей хранителю & цифровой хранилища, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.

tooconfigure и теста Azure AD единого входа с диспетчер паролей хранителю & цифровой хранилище, необходимые hello toocomplete следующие стандартные блоки.

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя диспетчер паролей хранителю & цифровой хранилище](#creating-a-keeperpasswordmanager-test-user)**  -toohave аналог Саймон Britta в диспетчер паролей хранителю & цифровой хранилища, которое представляет связанный toohello Azure AD пользователя.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе Azure AD единым входом в портал Azure hello включить и настроить единый вход в приложение диспетчер паролей хранителю & цифровой хранилища.

**tooconfigure Azure AD единого входа с диспетчер паролей хранителю & цифровой хранилища выполните hello следующие шаги.**

1. В hello в hello портала Azure **диспетчер паролей хранителю & цифровой хранилище** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_samlbase.png)

3. На hello **диспетчер паролей хранителю & цифровой хранилище домена и URL-адреса** выполните следующие шаги hello:

    ![Настройка единого входа](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_url.png)

    а. В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://{SSO CONNECT SERVER}/sso-connect/saml/login`

    b. В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://{SSO CONNECT SERVER}/sso-connect/saml/sso`

    c. В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://{SSO CONNECT SERVER}/sso-connect`

    > [!NOTE] 
    > Эти значения приведены в качестве примера. Обновите эти значения с hello фактический URL-адрес ответа и URL-адрес входа. Обратитесь к [диспетчер паролей хранителю & цифровой клиентов хранилища поддержки](https://keepersecurity.com/contact.html) tooget эти значения. 

4. На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.

    ![Настройка единого входа](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_400.png)
    
6. На hello **диспетчер паролей хранителю & цифровой настройки хранилища** щелкните **настроить диспетчер паролей хранителю & цифровой хранилище** tooopen **Настройкавхода**окна. Копировать hello **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**

    ![Настройка единого входа](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_configure.png) 

7. tooconfigure единого входа на **диспетчер паролей хранителю & цифровой настройки хранилища** стороны, выполните рекомендации hello, предоставленных во [хранителю руководство](https://keepersecurity.com/assets/pdf/SettingupAzurewithKeeperSSOConnect.pdf)

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-keeperpasswordmanager-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-keeperpasswordmanager-tutorial/create_aaduser_02.png) 

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-keeperpasswordmanager-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-keeperpasswordmanager-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-a-keeper-password-manager--digital-vault-test-user"></a>Создание тестового пользователя Keeper Password Manager & Digital Vault

Пользователи toolog tooenable Azure AD в tooKeeper диспетчер паролей & цифровой хранилища, их необходимо подготовить в диспетчер паролей хранителю & цифровой хранилища. В время подготовки пользователей и после проверки подлинности пользователей в приложении hello автоматически создаются непосредственно поддерживает приложение. Вы можете связаться [поддержки хранителю](https://keepersecurity.com/contact.html), если пользователи toosetup вручную.

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа к tooKeeper диспетчер паролей & цифровой хранилища.

![Назначение пользователя][200] 

**tooassign tooKeeper Britta Simon диспетчер паролей & цифровой хранилища выполните hello следующие шаги.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **диспетчер паролей хранителю & хранилище цифровых**.

    ![Настройка единого входа](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.

При нажатии кнопки hello диспетчер паролей хранителю & цифровой хранилище плитки в панели доступа hello, вы должны получить страницы входа диспетчер паролей хранителю & цифровой хранилища приложения. После успешной проверки подлинности должно появиться в приложение hello. Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_203.png

