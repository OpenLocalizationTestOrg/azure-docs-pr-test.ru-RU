---
title: "Руководство по интеграции Azure Active Directory с Bonusly | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Bonusly."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 29fea32a-fa20-47b2-9e24-26feb47b0ae6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 60ad06c028463af81a7901ab321c4ae9346798ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bonusly"></a>Руководство. Интеграция Azure Active Directory с Bonusly

В этом учебнике вы узнаете, как toointegrate Bonusly с Azure Active Directory (Azure AD).

Интеграция с Azure AD Bonusly предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooBonusly
- Можно включить на пользователей tooautomatically get вошедшего tooBonusly (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с Bonusly требуется hello следующих элементов:

- подписка Azure AD;
- подписка Bonusly с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление Bonusly из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-bonusly-from-hello-gallery"></a>Добавление Bonusly из галереи hello
tooconfigure hello интеграции Bonusly в Azure AD, вы должны tooadd Bonusly из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd Bonusly из галереи hello, выполните следующие шаги hello.**

1. В hello ** [портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Кнопка Hello Azure Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Hello корпоративных приложений колонку][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Кнопка нового приложения Hello][3]

4. Введите в поле поиска hello **Bonusly**выберите **Bonusly** из панели результатов щелкните **добавить** кнопку tooadd приложения hello.

    ![Bonusly в списке результатов hello](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в Bonusly с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Bonusly является tooa в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в Bonusly должен установить toobe.

В Bonusly, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.

tooconfigure и теста Azure AD единого входа с Bonusly, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configure-azure-ad-single-sign-on) ** -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user) ** -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание Bonusly тестового пользователя](#create-a-bonusly-test-user) ** -toohave аналог Саймон Britta в Bonusly, который представляет связанный toohello Azure AD пользователя.
4. **[Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#test-single-sign-on) ** -tooverify ли hello works конфигурации.

### <a name="configure-azure-ad-single-sign-on"></a>Настройка единого входа Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Bonusly.

**tooconfigure Azure AD единого входа с Bonusly, выполните следующие шаги hello.**

1. В hello в hello портала Azure **Bonusly** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_samlbase.png)

3. На hello **Bonusly доменов и URL-адреса** выполните следующие шаги hello:

    ![Сведения о домене и URL-адресах для единого входа в приложение Bonusly](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_url.png)

    В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://Bonus.ly/saml/<tenant-name>`

    > [!NOTE] 
    > значение Hello не является вещественным числом. Значение hello обновления с hello фактический URL-адрес ответа. Обратитесь к [Bonusly поддержки](https://Bonusly/contact) tooget значение hello.
 
4. На hello **сертификат подписи SAML** раздел, hello копирования **ОТПЕЧАТОК** значение на основе сертификата hello.

    ![ссылку для скачивания сертификата Hello](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-bonus-tutorial/tutorial_general_400.png)

6. На hello **Bonusly конфигурации** щелкните **Настройка Bonusly** tooopen **Настройка входа** окна. Копировать hello **идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**

    ![Конфигурация Bonusly](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_configure.png) 

7. В другом окне браузера войдите в tooyour **Bonusly** клиента.

8. Hello инструментов в верхней части hello, щелкните **параметры**, а затем выберите **интеграции и приложения**.
   
    ![Социальный раздел Bonusly](./media/active-directory-saas-bonus-tutorial/ic773686.png "Bonusly")
9. В разделе **Single Sign-On** (Единый вход) выберите **SAML**.

10. На hello **SAML** диалогового окна выполните следующие шаги hello:
   
    ![Диалоговое окно SAML в Bonusly](./media/active-directory-saas-bonus-tutorial/ic773687.png "Bonusly")
   
    а. В hello **URL-адрес назначения IdP SSO** текстовое значение hello вставить **SAML единого входа URL-адрес службы**, который вы скопировали из портала Azure.
   
    b. В hello **издатель IdP** текстовое значение hello вставить **SAML идентификатор сущности**, который вы скопировали из портала Azure. 

    c. В hello **URL-адрес входа поставщика удостоверений** текстовое значение hello вставить **SAML единого входа URL-адрес службы**, который вы скопировали из портала Azure.

    d. Вставить **отпечаток** значение копируется из портала Azure hello **отпечаток сертификата** текстового поля.
   
11. Щелкните **Сохранить**.

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello ** Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание тестового пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Кнопка Hello Azure Active Directory](./media/active-directory-saas-bonus-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Здравствуйте, «Пользователи и группы» и «Все пользователи» ссылки](./media/active-directory-saas-bonus-tutorial/create_aaduser_02.png) 

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".
 
    ![Кнопка "Добавить" Hello](./media/active-directory-saas-bonus-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![диалоговое окно приветствия пользователя](./media/active-directory-saas-bonus-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="create-a-bonusly-test-user"></a>Создание тестового пользователя приложения Bonusly

В порядке tooenable toolog пользователей Azure AD в tooBonusly их необходимо подготовить в Bonusly. В случае Bonusly hello Подготовка выполняется вручную.

>[!NOTE]
>Можно использовать любые другие Bonusly пользователя средства создания учетных записей или интерфейсы API, предоставляемые Bonusly tooprovision AAD учетных записей пользователей.
>  

**tooconfigure подготовки пользователей, выполните следующие шаги hello.**

1. В окне браузера войдите в tooyour Bonusly клиента.

2. Щелкните **Параметры**.
 
    ![Параметры](./media/active-directory-saas-bonus-tutorial/ic781041.png "Параметры")

3. Нажмите кнопку hello **пользователи и премии** вкладки.
   
    ![Пользователи и бонусы](./media/active-directory-saas-bonus-tutorial/ic781042.png "Пользователи и бонусы")

4. Выберите **Manage Users**(Управление пользователями).
   
    ![Управление пользователями](./media/active-directory-saas-bonus-tutorial/ic781043.png "Управление пользователями")

5. Нажмите кнопку **Add User**(Добавить пользователя).
   
    ![Добавление пользователя](./media/active-directory-saas-bonus-tutorial/ic781044.png "Добавление пользователя")

6. На hello **добавить пользователя** диалоговое окно, выполните следующие шаги hello:
   
    ![Добавление пользователя](./media/active-directory-saas-bonus-tutorial/ic781045.png "Добавление пользователя")  

    а. В hello **имя** текстовом поле введите имя пользователя, такие как hello **Britta**.

    b. В hello **Фамилия** текстовом поле введите фамилию пользователя как hello **Simon**.
 
    c. В hello **электронной почты** текстовом поле введите адрес электронной почты hello пользователя как ** brittasimon@contoso.com **.

    d. Щелкните **Сохранить**.
   
     >[!NOTE]
     >Владелец учетной записи Azure AD Hello получает сообщение электронной почты, который включает учетную запись hello tooconfirm ссылку, чтобы она стала активной.
     >  

### <a name="assign-hello-azure-ad-test-user"></a>Назначить hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooBonusly доступа.

![Назначение пользователям ролей hello][200] 

**tooassign tooBonusly Britta Simon выполните следующие шаги hello.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **Bonusly**.

    ![Hello Bonusly ссылку в списке приложений hello](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Hello ссылку «Пользователи и группы»][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![область назначения, добавьте Hello][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="test-single-sign-on"></a>Проверка единого входа

Цель этого раздела Hello является tootest настройки единого входа Azure AD с помощью панели доступа "hello".

При нажатии кнопки Bonusly плитки hello в Здравствуйте панели доступа, вы должны получить автоматически вошедшего tooyour Bonusly приложения.

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_203.png

