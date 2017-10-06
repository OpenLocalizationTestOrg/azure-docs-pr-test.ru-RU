---
title: "Руководство по интеграции Azure Active Directory с Perception United States (Non-UltiPro) | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и восприятия США (Non-UltiPro)."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: b4a8f026-cb5f-41eb-9680-68eddc33565e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 874b5da277b9c68504c4af2ac87ed90d2bbd93b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-perception-united-states-non-ultipro"></a>Руководство по интеграции Azure Active Directory с Perception United States (Non-UltiPro)

В этом учебнике вы узнаете, как toointegrate восприятии United States (Non-UltiPro) с Azure Active Directory (Azure AD).

Интеграция впечатление США (Non-UltiPro) с Azure AD предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooPerception США (Non-UltiPro).
- Можно включить на пользователей tooautomatically get вошедшего tooPerception США (Non-UltiPro) (Single Sign-On) с помощью своих учетных записей Azure AD.
- Вы можете управлять учетными записями в одном централизованном месте - hello портал Azure.

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с впечатление США (Non-UltiPro) требуется hello следующих элементов:

- подписка Azure AD;
- подписка Perception United States (Non-UltiPro) с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление впечатление США (Non-UltiPro) из коллекции hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-perception-united-states-non-ultipro-from-hello-gallery"></a>Добавление впечатление США (Non-UltiPro) из коллекции hello
tooconfigure hello интеграции для восприятия США (Non-UltiPro) в Azure AD, вы должны tooadd восприятии США (Non-UltiPro) из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd восприятии United States (Non-UltiPro) из коллекции hello выполните hello следующие шаги.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Кнопка Hello Azure Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Hello корпоративных приложений колонку][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Кнопка нового приложения Hello][3]

4. Введите в поле поиска hello **восприятия США (Non-UltiPro)**выберите **восприятия США (Non-UltiPro)** из панели результатов щелкните **добавить** tooadd кнопку приложение Hello.

    ![Впечатление United States (Non-UltiPro) в списке результатов hello](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD

В этом разделе описана настройка и проверка единого входа Azure AD в Perception United States (Non-UltiPro) с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow какие пользователь аналог hello в восприятии США (Non-UltiPro) является tooa в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в восприятии США (Non-UltiPro) должен установить toobe.

В восприятии США (Non-UltiPro), присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.

tooconfigure и тестирования Azure AD единого входа с впечатление США (Non-UltiPro), необходимы следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя впечатление США (Non-UltiPro)](#create-a-perception-united-states-non-ultipro-test-user)**  -toohave аналог Саймон Britta в восприятии США (Non-UltiPro), являющийся представлением связанного toohello Azure AD пользователя.
4. **[Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#test-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configure-azure-ad-single-sign-on"></a>Настройка единого входа Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении впечатление США (Non-UltiPro).

**tooconfigure Azure AD единого входа с впечатление США (Non-UltiPro), выполните следующие шаги hello.**

1. В hello в hello портала Azure **восприятии США (Non-UltiPro)** странице интеграции приложения щелкните **единого входа**.

    ![Ссылка "Настройка единого входа"][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_samlbase.png)

3. На hello **URL-адреса и домена впечатление США (Non-UltiPro)** выполните следующие шаги hello:

    ![Сведения о домене и URL-адресах единого входа для приложения Perception United States (Non-UltiPro)](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_url.png)

    а. В hello **идентификатор** текстовом поле введите URL-адрес hello:`https://perception.kanjoya.com/sp`

    b. В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://perception.kanjoya.com/sso?idp=<entity_id>`

    > [!NOTE] 
    > значение Hello не является вещественным числом. Значение hello будет обновляться hello фактический URL-адрес ответа, который описывается далее в учебнике hello.
 
4. На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.

    ![ссылку для скачивания сертификата Hello](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_400.png)

6. На hello **конфигурации впечатление США (Non-UltiPro)** щелкните **настройки восприятия США (Non-UltiPro)** tooopen **Настройка входа** окно. Копировать hello **идентификатор сущности SAML** из hello **краткий справочник.**

    а. Hello **восприятия США (Non-UltiPro)** приложению hello **идентификатор сущности SAML** закодированный toobe uri значение, которое вы скопировали. значения uri кодируются tooget hello, используйте hello следующей ссылке:**http://www.url-encode-decode.com/**.

    b. После получения hello uri закодированное значение совместно с hello **URL-адрес ответа** описанным ниже -

    `https://perception.kanjoya.com/sso?idp=<URI encooded entity_id>`
    
    c. Вставить hello выше значения в hello **URL-адрес ответа** текстовое поле в **URL-адреса и домена впечатление США (Non-UltiPro)** раздела.

    ![Настройка Perception United States (Non-UltiPro)](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_configure.png) 

7. В другом окне браузера Войдите на сайт компании tooyour восприятии США (Non-UltiPro) с правами администратора.

8. На главной панели инструментов hello, щелкните **параметры учетной записи**.

    ![Пользователь Perception United States (Non-UltiPro)](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_user.png)

9. На hello **параметры учетной записи** выполните следующие шаги hello:

    ![Пользователь Perception United States (Non-UltiPro)](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_account.png)

    а. В hello **название компании** в текстовое поле имя типа hello hello **компании**.
    
    b. В hello **имя учетной записи** в текстовое поле имя типа hello hello **учетной записи**.

    c. В **ответа по умолчанию-tooEmail** текстовое поле, тип hello допустимым **электронной почты**.

    d. Выберите для параметра **SSO Identity Provider** (Поставщик удостоверений единого входа) значение **SAML 2.0**.

10. На hello **Настройка единого входа** выполните следующие шаги hello:

    ![Настройка единого входа Perception United States (Non-UltiPro)](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_ssoconfig.png)

    а. Выберите для параметра **SAML NameID Type** (Тип NameID SAML) значение **EMAIL** (Электронная почта).

    b. В hello **имя конфигурации единого входа** в текстовое поле имя типа hello вашей **конфигурации**.
    
    c. В **имя поставщика удостоверений** текстовое значение hello вставить **идентификатор сущности SAML**, который вы скопировали из портала Azure. 

    d. В **текстовое поле для домена SAML**, введите домен hello как  **@contoso.com** .

    д. Щелкните **попытку отправить** tooupload hello **метаданные в формате XML** файла.

    f. Нажмите кнопку **Обновить**.


> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD

Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

   ![Создание тестового пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello hello левой панели портала Azure щелкните hello **Azure Active Directory** кнопки.

    ![Кнопка Hello Azure Active Directory](./media/active-directory-saas-perceptionunitedstates-tutorial/create_aaduser_01.png)

2. слишком go toodisplay hello список пользователей,**пользователей и групп**, а затем нажмите кнопку **всех пользователей**.

    ![Здравствуйте, «Пользователи и группы» и «Все пользователи» ссылки](./media/active-directory-saas-perceptionunitedstates-tutorial/create_aaduser_02.png)

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** вверху hello hello **всех пользователей** диалоговое окно.

    ![Кнопка "Добавить" Hello](./media/active-directory-saas-perceptionunitedstates-tutorial/create_aaduser_03.png)

4. В hello **пользователя** диалогового окна выполните следующие шаги hello:

    ![диалоговое окно приветствия пользователя](./media/active-directory-saas-perceptionunitedstates-tutorial/create_aaduser_04.png)

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** поле типа hello адрес электронной почты пользователя Саймон Britta.

    c. Выберите hello **Показать пароль** флажок и запишите значение hello, отображаемый в hello **пароль** поле.

    d. Щелкните **Создать**.
  
### <a name="create-a-perception-united-states-non-ultipro-test-user"></a>Создание тестового пользователя Perception United States (Non-UltiPro)

В этом разделе описано, как создать пользователя Britta Simon в приложении Perception United States (Non-UltiPro). Работать с [группа поддержки впечатление США (Non-UltiPro)](http://www.ultimatesoftware.com/Contact/ContactUs) tooadd hello пользователей на платформе hello впечатление США (Non-UltiPro).

### <a name="assign-hello-azure-ad-test-user"></a>Назначить hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooPerception США (Non-UltiPro).

![Назначение пользователям ролей hello][200] 

**tooassign Britta Simon tooPerception США (Non-UltiPro) выполните hello следующие шаги.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **восприятии США (Non-UltiPro)**.

    ![ссылка впечатление США (Non-UltiPro) Hello в списке приложений hello](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_app.png)  

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Hello ссылку «Пользователи и группы»][202]

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![область назначения, добавьте Hello][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="test-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.

При нажатии кнопки hello впечатление США (Non-UltiPro) плитки в панели доступа hello, вы должны получить tooyour автоматически подписан на восприятие США (Non-UltiPro) приложения.
Дополнительные сведения о панели доступа см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_203.png

