---
title: "Руководство по интеграции Azure Active Directory с PagerDuty | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и PagerDuty."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0410456a-76f7-42a7-9bb5-f767de75a0e0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: c3cfbedac3bf075e2d8cd833d5de7ca0bc9468b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-pagerduty"></a>Руководство по интеграции Azure Active Directory с PagerDuty

В этом учебнике вы узнаете, как toointegrate PagerDuty с Azure Active Directory (Azure AD).

Интеграция PagerDuty с Azure AD предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooPagerDuty
- Можно включить на пользователей tooautomatically get вошедшего tooPagerDuty (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с PagerDuty требуется hello следующих элементов:

- подписка Azure AD;
- подписка PagerDuty с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление PagerDuty из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-pagerduty-from-hello-gallery"></a>Добавление PagerDuty из галереи hello
tooconfigure hello интеграции PagerDuty в Azure AD, вы должны tooadd PagerDuty из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd PagerDuty из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Кнопка Hello Azure Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Hello корпоративных приложений колонку][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Кнопка нового приложения Hello][3]

4. Введите в поле поиска hello **PagerDuty**выберите **PagerDuty** из панели результатов щелкните **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD

В этом разделе описана настройка и проверка единого входа Azure AD в PagerDuty с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в PagerDuty является tooa в Azure AD. Другими словами связи между пользователя Azure AD и hello связанных пользователей в PagerDuty должен установить toobe.

В PagerDuty, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.

tooconfigure и теста Azure AD единого входа с PagerDuty, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя PagerDuty](#create-a-pagerduty-test-user)**  -toohave аналог Саймон Britta в PagerDuty, который представляет связанный toohello Azure AD пользователя.
4. **[Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#test-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configure-azure-ad-single-sign-on"></a>Настройка единого входа Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в PagerDuty приложения.

**Azure AD tooconfigure единого входа с PagerDuty, выполните следующие шаги hello.**

1. В hello в hello портала Azure **PagerDuty** странице интеграции приложения щелкните **единого входа**.

    ![Ссылка "Настройка единого входа"][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_samlbase.png)

3. На hello **URL-адреса и домена PagerDuty** выполните следующие шаги hello:

    ![Сведения о домене и URL-адресах единого входа для приложения PagerDuty](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_url.png)

    а. В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<tenant-name>.pagerduty.com`

    b. В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<tenant-name>.pagerduty.com`

    > [!NOTE] 
    > Эти значения приведены в качестве примера. Обновить значения hello фактический URL-адрес входа и идентификатор. Обратитесь к [группа поддержки клиент PagerDuty](https://www.pagerduty.com/support/) tooget эти значения. 

4. На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.

    ![ссылку для скачивания сертификата Hello](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-pagerduty-tutorial/tutorial_general_400.png)

6. На hello **конфигурации PagerDuty** щелкните **Настройка PagerDuty** tooopen **Настройка входа** окна. Копировать hello **URL-адрес выхода и SAML единого входа URL-адрес службы** из hello **краткий справочник.**

    ![Конфигурация PagerDuty](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_configure.png) 

7. В другом окне браузера войдите на свой сайт PagerDuty компании в качестве администратора.

8. В меню в верхней части hello hello выберите **параметры учетной записи**.
   
    ![Параметры учетной записи](./media/active-directory-saas-pagerduty-tutorial/ic778535.png "параметры учетной записи")

9. Щелкните **Single Sign-on**(Единый вход).
   
    ![Единый вход](./media/active-directory-saas-pagerduty-tutorial/ic778536.png "Единый вход")

10. На hello **Включение единого входа (SSO)** выполните следующие шаги hello:
   
    ![Разрешить единый вход](./media/active-directory-saas-pagerduty-tutorial/ic778537.png "Разрешить единый вход")
   
    а. Откройте сертификат кодировке base-64 загружен с портала Azure в блокноте, hello копирования содержимого его в буфер обмена, а затем вставьте его toohello **сертификат X.509** текстового поля
  
    b. В hello **URL-адрес входа** вставьте **SAML единого входа URL-адрес службы** скопирован из портала Azure.
  
    c. В hello **URL-адрес выхода** вставьте **URL-адрес выхода** скопирован из портала Azure.
 
    d. Установите флажок **Включить единый вход**.
 
    д. Нажмите кнопку **Сохранить изменения**.

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD

Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание тестового пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Кнопка Hello Azure Active Directory](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Здравствуйте, «Пользователи и группы» и «Все пользователи» ссылки](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_02.png) 

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".
 
    ![Кнопка "Добавить" Hello](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![диалоговое окно приветствия пользователя](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="create-a-pagerduty-test-user"></a>Создание тестового пользователя PagerDuty

Пользователи toolog tooenable Azure AD в tooPagerDuty, их необходимо подготовить в PagerDuty.  
В случае PagerDuty hello Подготовка выполняется вручную.

>[!NOTE]
>Можно использовать любые другие Pagerduty пользователя средства создания учетных записей или API, предоставленные Pagerduty tooprovision Azure Active Directory учетных записей пользователей.

**tooprovision учетной записи пользователя, выполните следующие шаги hello.**

1. Войдите в tooyour **Pagerduty** клиента.

2. В меню в верхней части hello hello выберите **пользователей**.

3. Щелкните **Добавить пользователей**.
   
    ![Добавление пользователей](./media/active-directory-saas-pagerduty-tutorial/ic778539.png "добавление пользователей")

4.  На hello **пригласить команду** диалоговое окно, выполните следующие шаги hello:
   
    ![Пригласить команду](./media/active-directory-saas-pagerduty-tutorial/ic778540.png "Пригласить команду")

    а. Тип hello **имя и фамилию** пользователя как **Britta Simon**. 
   
    b. Введите **Email** (Адрес электронной почты) для пользователя, например: **brittasimon@contoso.com**.
   
    c. Нажмите **Add** (Добавить), затем нажмите **Send Invites** (Отправить приглашения).
   
    >[!NOTE]
    >Все добавленные пользователи получат приглашение toocreate учетную запись PagerDuty.

### <a name="assign-hello-azure-ad-test-user"></a>Назначить hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooPagerDuty доступа.

![Назначение пользователям ролей hello][200]

**tooassign tooPagerDuty Britta Simon выполните следующие шаги hello.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **PagerDuty**.

    ![ссылка PagerDuty Hello в списке приложений hello](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Hello ссылку «Пользователи и группы»][202]

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![область назначения, добавьте Hello][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="test-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.

При нажатии кнопки hello PagerDuty плитки в hello Panelyou доступа следует получать автоматически вошедшего tooyour PagerDuty приложения.

Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_203.png

