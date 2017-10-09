---
title: "Руководство по интеграции Azure Active Directory с ScreenSteps | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и ScreenSteps."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 4563fe94-a88f-4895-a07f-79df44889cf9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jeedes
ms.openlocfilehash: fd041e5fe4552727eeda2dabc1773d8043d410f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-screensteps"></a>Учебник. Интеграция Azure Active Directory с ScreenSteps

В этом учебнике вы узнаете, как toointegrate ScreenSteps с Azure Active Directory (Azure AD).

Интеграция ScreenSteps с Azure AD предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooScreenSteps.
- Можно включить на пользователей tooautomatically get вошедшего tooScreenSteps (Single Sign-On) с помощью своих учетных записей Azure AD.
- Вы можете управлять учетными записями в одном централизованном месте - hello портал Azure.

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с ScreenSteps требуется hello следующих элементов:

- подписка Azure AD;
- подписка ScreenSteps с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление ScreenSteps из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-screensteps-from-hello-gallery"></a>Добавление ScreenSteps из галереи hello
tooconfigure hello интеграции ScreenSteps в Azure AD, вы должны tooadd ScreenSteps из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd ScreenSteps из галереи hello, выполните следующие шаги hello.**

1. В hello ** [портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Кнопка Hello Azure Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Hello корпоративных приложений колонку][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Кнопка нового приложения Hello][3]

4. Введите в поле поиска hello **ScreenSteps**выберите **ScreenSteps** из панели результатов щелкните **добавить** кнопку tooadd приложения hello.

    ![ScreenSteps в списке результатов hello](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD

В этом разделе описана настройка и проверка единого входа Azure AD в ScreenSteps с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в ScreenSteps является tooa в Azure AD. Другими словами связи между пользователя Azure AD и hello связанных пользователей в ScreenSteps должен установить toobe.

В ScreenSteps, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.

tooconfigure и теста Azure AD единого входа с ScreenSteps, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configure-azure-ad-single-sign-on) ** -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user) ** -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя ScreenSteps](#create-a-screensteps-test-user) ** -toohave аналог Саймон Britta в ScreenSteps, который представляет связанный toohello Azure AD пользователя.
4. **[Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#test-single-sign-on) ** -tooverify ли hello works конфигурации.

### <a name="configure-azure-ad-single-sign-on"></a>Настройка единого входа Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в ScreenSteps приложения.

**tooconfigure Azure AD единого входа с ScreenSteps, выполните следующие шаги hello.**

1. В hello в hello портала Azure **ScreenSteps** странице интеграции приложения щелкните **единого входа**.

    ![Ссылка "Настройка единого входа"][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_samlbase.png)

3. На hello **URL-адреса и домена ScreenSteps** выполните следующие шаги hello:

    ![Сведения о домене и URL-адресах единого входа приложения ScreenSteps](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_url.png)

    В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<tenantname>.ScreenSteps.com`

    > [!NOTE] 
    > Это значение приведено для справки. Измените значение этого параметра hello фактический URL-адрес входа, который описывается далее в этом учебнике. 

4. На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.

    ![ссылку для скачивания сертификата Hello](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-screensteps-tutorial/tutorial_general_400.png)

6. На hello **конфигурации ScreenSteps** щелкните **Настройка ScreenSteps** tooopen **Настройка входа** окна. Копировать hello **URL-адрес выхода и SAML единого входа URL-адрес службы** из hello **краткий справочник.**

    ![Конфигурация ScreenSteps](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_configure.png) 

7. В другом окне веб-браузера войдите на сайт ScreenSteps своей компании в качестве администратора.

8. Щелкните **Параметры учетной записи**.

    ![Управление учетными записями](./media/active-directory-saas-screensteps-tutorial/ic778523.png "Управление учетными записями")

9. Щелкните **Single Sign-on**(Единый вход).

    ![Удаленная аутентификация](./media/active-directory-saas-screensteps-tutorial/ic778524.png "Удаленная аутентификация")

10. Щелкните **Create Single Sign-on Endpoint** (Создать конечную точку единого входа).

    ![Удаленная аутентификация](./media/active-directory-saas-screensteps-tutorial/ic778525.png "Удаленная аутентификация")

11. В hello **создать единую конечную точку входа** выполните следующие шаги hello:

    ![Создание конечной точки аутентификации](./media/active-directory-saas-screensteps-tutorial/ic778526.png "Создание конечной точки аутентификации")
    
    а. В hello **заголовок** текстовом поле введите заголовок.
    
    b. Из hello **режим** выберите **SAML**.
    
    c. Щелкните **Создать**.

12. **Изменить** hello новой конечной точки.

    ![Изменение конечной точки](./media/active-directory-saas-screensteps-tutorial/ic778528.png "Edit endpoint")

13. В hello **изменить одну конечную точку входа** выполните следующие шаги hello:

    ![Конечная точка удаленной аутентификации](./media/active-directory-saas-screensteps-tutorial/ic778527.png "Конечная точка удаленной аутентификации")

    а. Нажмите кнопку **передачи новый файл сертификата SAML**, а затем передачи hello сертификат, который вы скачали из портала Azure.
    
    b. Вставить **SAML единого входа URL-адрес службы** значение, которое было скопировано из hello портал Azure в hello **URL-адрес удаленного входа** текстового поля.
    
    c. Вставить **URL-адрес выхода** значение, которое было скопировано из hello портал Azure в hello **URL-адрес выхода** текстового поля.
    
    d. Выберите **группы** toowhen tooassign пользователей, их инициализации.
    
    д. Нажмите кнопку **Обновить**.

    f. Hello копирования **URL-адрес потребителя SAML** toohello буфер обмена и вставьте в toohello **URL-адрес входа** текстовое поле в **URL-адреса и домена ScreenSteps** раздела.
    
    ж. Вернуть toohello **изменить одну конечную точку входа**.
    
    h. Нажмите кнопку hello **сделать по умолчанию для учетной записи** кнопку toouse эту конечную точку для всех пользователей, входящих в ScreenSteps. Кроме того, можно щелкнуть hello **добавить tooSite** кнопку toouse эту конечную точку для определенных сайтов в **ScreenSteps**.

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello ** Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD

Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

   ![Создание тестового пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello hello левой панели портала Azure щелкните hello **Azure Active Directory** кнопки.

    ![Кнопка Hello Azure Active Directory](./media/active-directory-saas-screensteps-tutorial/create_aaduser_01.png)

2. слишком go toodisplay hello список пользователей,**пользователей и групп**, а затем нажмите кнопку **всех пользователей**.

    ![Здравствуйте, «Пользователи и группы» и «Все пользователи» ссылки](./media/active-directory-saas-screensteps-tutorial/create_aaduser_02.png)

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** вверху hello hello **всех пользователей** диалоговое окно.

    ![Кнопка "Добавить" Hello](./media/active-directory-saas-screensteps-tutorial/create_aaduser_03.png)

4. В hello **пользователя** диалогового окна выполните следующие шаги hello:

    ![диалоговое окно приветствия пользователя](./media/active-directory-saas-screensteps-tutorial/create_aaduser_04.png)

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** поле типа hello адрес электронной почты пользователя Саймон Britta.

    c. Выберите hello **Показать пароль** флажок и запишите значение hello, отображаемый в hello **пароль** поле.

    d. Щелкните **Создать**.
 
### <a name="create-a-screensteps-test-user"></a>Создание тестового пользователя ScreenSteps

В этом разделе описано, как создать пользователя Britta Simon в ScreenSteps. Работать с [группа поддержки клиент ScreenSteps](https://www.screensteps.com/contact) для добавления пользователей hello в платформе ScreenSteps hello. Перед использованием единого входа необходимо создать и активировать пользователей. 

### <a name="assign-hello-azure-ad-test-user"></a>Назначить hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooScreenSteps доступа.

![Назначение пользователям ролей hello][200] 

**tooassign tooScreenSteps Britta Simon выполните следующие шаги hello.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **ScreenSteps**.

    ![ссылка ScreenSteps Hello в списке приложений hello](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_app.png)  

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Hello ссылку «Пользователи и группы»][202]

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![область назначения, добавьте Hello][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="test-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.

При нажатии кнопки ScreenSteps плитки в панели доступа hello приветствия, вы должны получить автоматически вошедшего tooyour ScreenSteps приложения.
Дополнительные сведения о панели доступа см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_203.png

