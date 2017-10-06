---
title: "Руководство. Интеграция Azure Active Directory с Workstars | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Workstars."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 51a4a4e4-ff60-4971-b3f8-a0367b70d220
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: 86250d7538f058d2a821ded7dda0b2fc185d80df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workstars"></a>Учебник. Интеграция Azure Active Directory с Workstars

В этом учебнике вы узнаете, как toointegrate Workstars с Azure Active Directory (Azure AD).

Интеграция с Azure AD Workstars предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooWorkstars.
- Можно включить на пользователей tooautomatically get вошедшего tooWorkstars (Single Sign-On) с помощью своих учетных записей Azure AD.
- Вы можете управлять учетными записями в одном централизованном месте - hello портал Azure.

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с Workstars требуется hello следующих элементов:

- подписка Azure AD;
- подписка Workstars с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление Workstars из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-workstars-from-hello-gallery"></a>Добавление Workstars из галереи hello
tooconfigure hello интеграции Workstars в Azure AD, вы должны tooadd Workstars из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd Workstars из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Кнопка Hello Azure Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Hello корпоративных приложений колонку][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Кнопка нового приложения Hello][3]

4. Введите в поле поиска hello **Workstars**выберите **Workstars** из панели результатов щелкните **добавить** кнопку tooadd приложения hello.

    ![Workstars в списке результатов hello](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD

В этом разделе описана настройка и проверка единого входа Azure AD в Workstars с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Workstars является tooa в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в Workstars должен установить toobe.

В Workstars, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.

tooconfigure и теста Azure AD единого входа с Workstars, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя Workstars](#create-a-workstars-test-user)**  -toohave аналог Саймон Britta в Workstars, который представляет связанный toohello Azure AD пользователя.
4. **[Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#test-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configure-azure-ad-single-sign-on"></a>Настройка единого входа Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Workstars.

**tooconfigure Azure AD единого входа с Workstars, выполните следующие шаги hello.**

1. В hello в hello портала Azure **Workstars** странице интеграции приложения щелкните **единого входа**.

    ![Ссылка "Настройка единого входа"][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_samlbase.png)

3. На hello **URL-адреса и домена Workstars** выполните следующие шаги hello:

    ![Сведения о домене и URL-адресах единого входа приложения Workstars](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_url.png)

    а. В hello **идентификатор** текстовом поле введите URL-адрес hello:`https://workstars.com`

    b. В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<subdomain>.workstars.com/saml/login_check`

    > [!NOTE] 
    > значение Hello не является вещественным числом. Значение hello обновления с hello фактический URL-адрес ответа. Обратитесь к [Workstars поддержки](https://support.workstars.com) tooget значение hello.
 
4. На hello **сертификат подписи SAML** щелкните **сертификата (Base64)** и затем сохраните файл сертификата hello на вашем компьютере.

    ![ссылку для скачивания сертификата Hello](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-workstars-tutorial/tutorial_general_400.png)

6. На hello **конфигурации Workstars** щелкните **Настройка Workstars** tooopen **Настройка входа** окна. Копировать hello **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**

    ![Настройка Workstars](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_configure.png) 

7. В другом окне браузера Войдите на сайт компании Workstars tooyour с правами администратора.

8. На главной панели инструментов hello, щелкните **параметры**.

    ![Настройки Workstars](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_sett.png)

9. Go слишком**входа** > **параметры**.

    ![Workstars, раздел "Вход"](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_signon.png)

    ![Workstars, раздел "Настройки"](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_settings.png)

10. На hello **единого входа на (SAML) - параметры** выполните следующие шаги hello:
    
    ![Настройки SAML в Workstars](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_saml.png)

    а. В текстовом поле **Identity Provider Name** (Имя поставщика удостоверений) введите **Office 365**.

    b. В hello **идентификатор сущности поставщика удостоверений** текстовое значение hello вставить **идентификатор сущности SAML**, который вы скопировали из портала Azure.

    c. Скопируйте содержимое hello hello загруженный сертификат файл в Блокноте и вставьте его в hello **x509 сертификат** текстового поля. 

    d. В hello **URL-адрес единого входа SAML** текстовое значение hello вставить **SAML единого входа URL-адрес службы**, который вы скопировали из портала Azure.
    
    д. В hello **URL-адрес удаленного выхода** текстовое значение hello вставить **URL-адрес выхода**, который вы скопировали из портала Azure. 

    f. Для параметра **Name ID** (Идентификатор имени) выберите значение **Email (Default)** (Адрес электронной почты (по умолчанию)).

    g. Щелкните **Confirm** (Подтвердить).
    
> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD

Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

   ![Создание тестового пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello hello левой панели портала Azure щелкните hello **Azure Active Directory** кнопки.

    ![Кнопка Hello Azure Active Directory](./media/active-directory-saas-workstars-tutorial/create_aaduser_01.png)

2. слишком go toodisplay hello список пользователей,**пользователей и групп**, а затем нажмите кнопку **всех пользователей**.

    ![Здравствуйте, «Пользователи и группы» и «Все пользователи» ссылки](./media/active-directory-saas-workstars-tutorial/create_aaduser_02.png)

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** вверху hello hello **всех пользователей** диалоговое окно.

    ![Кнопка "Добавить" Hello](./media/active-directory-saas-workstars-tutorial/create_aaduser_03.png)

4. В hello **пользователя** диалогового окна выполните следующие шаги hello:

    ![диалоговое окно приветствия пользователя](./media/active-directory-saas-workstars-tutorial/create_aaduser_04.png)

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** поле типа hello адрес электронной почты пользователя Саймон Britta.

    c. Выберите hello **Показать пароль** флажок и запишите значение hello, отображаемый в hello **пароль** поле.

    d. Щелкните **Создать**.
  
### <a name="create-a-workstars-test-user"></a>Создание тестового пользователя Workstars

В этом разделе описано, как создать пользователя Britta Simon в приложении Workstars. Работать с [Workstars поддержки](https://support.workstars.com) tooadd hello пользователей на платформе Workstars hello.

### <a name="assign-hello-azure-ad-test-user"></a>Назначить hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooWorkstars доступа.

![Назначение пользователям ролей hello][200] 

**tooassign tooWorkstars Britta Simon выполните следующие шаги hello.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **Workstars**.

    ![ссылка Workstars Hello в списке приложений hello](./media/active-directory-saas-workstars-tutorial/tutorial_workstars_app.png)  

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Hello ссылку «Пользователи и группы»][202]

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![область назначения, добавьте Hello][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="test-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.

При нажатии кнопки Workstars плитки в панели доступа hello приветствия, вы должны получить автоматически вошедшего tooyour Workstars приложения.
Дополнительные сведения о панели доступа см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workstars-tutorial/tutorial_general_203.png

