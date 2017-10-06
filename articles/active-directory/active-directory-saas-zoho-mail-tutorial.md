---
title: "Руководство по интеграции Azure Active Directory с Zoho | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Zoho."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 9874e1f3-ade5-42e7-a700-e08b3731236a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: jeedes
ms.openlocfilehash: 5d1c196d3b97babab196f509ea68e7d61523a7e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zoho"></a>Руководство по интеграции Azure Active Directory с Zoho

В этом учебнике вы узнаете, как toointegrate Zoho с Azure Active Directory (Azure AD).

Интеграция с Azure AD Zoho предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooZoho.
- Можно включить на пользователей tooautomatically get вошедшего tooZoho (Single Sign-On) с помощью своих учетных записей Azure AD.
- Вы можете управлять учетными записями в одном централизованном месте - hello портал Azure.

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с Zoho требуется hello следующих элементов:

- подписка Azure AD;
- подписка Zoho с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление Zoho из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-zoho-from-hello-gallery"></a>Добавление Zoho из галереи hello
tooconfigure hello интеграции Zoho в Azure AD, вы должны tooadd Zoho из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd Zoho из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Кнопка Hello Azure Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Hello корпоративных приложений колонку][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Кнопка нового приложения Hello][3]

4. Введите в поле поиска hello **Zoho**выберите **Zoho** из панели результатов щелкните **добавить** кнопку tooadd приложения hello.

    ![Zoho в списке результатов hello](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD

В этом разделе описана настройка и проверка единого входа Azure AD в приложение Zoho с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Zoho является tooa в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в Zoho должен установить toobe.

В Zoho, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.

tooconfigure и теста Azure AD единого входа с Zoho, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя Zoho](#create-a-zoho-test-user)**  -toohave аналог Саймон Britta в Zoho, который представляет связанный toohello Azure AD пользователя.
4. **[Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#test-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configure-azure-ad-single-sign-on"></a>Настройка единого входа Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Zoho.

**Azure AD tooconfigure единого входа с Zoho, выполните следующие шаги hello.**

1. В hello в hello портала Azure **Zoho** странице интеграции приложения щелкните **единого входа**.

    ![Ссылка "Настройка единого входа"][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_samlbase.png)

3. На hello **URL-адреса и домена Zoho** выполните следующие шаги hello:

    ![Сведения о домене и URL-адресах единого входа для приложения Zoho](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_url.png)

    а. В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<company name>.zohomail.com`

    > [!NOTE] 
    > Это значение приведено для справки. Измените значение этого параметра hello фактический URL-адрес входа. Обратитесь к [группа поддержки клиент Zoho](https://www.zoho.com/mail/contact.html) tooget это значение. 
 
4. На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.

    ![ссылку для скачивания сертификата Hello](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_400.png)

6. На hello **конфигурации Zoho** щелкните **Настройка Zoho** tooopen **Настройка входа** окна. Копировать hello **URL-адрес выхода, URL-адрес изменения пароля и SAML единого входа URL-адрес службы** из hello **краткий справочник.**

    ![Настройка Zoho](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_configure.png) 

7. В другом окне браузера войдите на свой корпоративный сайт Zoho Mail в качестве администратора.

8. Go toohello **панели управления**.
   
    ![Панель управления](./media/active-directory-saas-zoho-mail-tutorial/ic789607.png "Панель управления")

9. Нажмите кнопку hello **проверку подлинности SAML** вкладки.
   
    ![Аутентификация SAML](./media/active-directory-saas-zoho-mail-tutorial/ic789608.png "Аутентификация SAML")

10. В hello **информация об аутентификации SAML** выполните следующие шаги hello:
   
    ![Параметры аутентификации SAML](./media/active-directory-saas-zoho-mail-tutorial/ic789609.png "Параметры аутентификации SAML")
   
    а. В hello **URL-адрес входа** вставьте **SAML единого входа URL-адрес службы** скопирован из портала Azure.
   
    b. В hello **URL-адрес выхода** вставьте **URL-адрес выхода** скопирован из портала Azure.
   
    c. В hello **URL-адрес изменения пароля** вставьте **URL-адрес изменения пароля** скопирован из портала Azure.
       
    d. Откройте сертификат кодировке base-64 загружен с портала Azure в блокноте, hello копирования содержимого его в буфер обмена, а затем вставьте его toohello **PublicKey** текстового поля.
   
    д. В поле **Algorithm** (Алгоритм) задайте значение **RSA**.
   
    f. Нажмите кнопку **ОК**.

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD

Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

   ![Создание тестового пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello hello левой панели портала Azure щелкните hello **Azure Active Directory** кнопки.

    ![Кнопка Hello Azure Active Directory](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_01.png)

2. слишком go toodisplay hello список пользователей,**пользователей и групп**, а затем нажмите кнопку **всех пользователей**.

    ![Здравствуйте, «Пользователи и группы» и «Все пользователи» ссылки](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_02.png)

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** вверху hello hello **всех пользователей** диалоговое окно.

    ![Кнопка "Добавить" Hello](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_03.png)

4. В hello **пользователя** диалогового окна выполните следующие шаги hello:

    ![диалоговое окно приветствия пользователя](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_04.png)

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** поле типа hello адрес электронной почты пользователя Саймон Britta.

    c. Выберите hello **Показать пароль** флажок и запишите значение hello, отображаемый в hello **пароль** поле.

    d. Щелкните **Создать**.
 
### <a name="create-a-zoho-test-user"></a>Создание тестового пользователя Zoho

В порядке tooenable toolog пользователей Azure AD в Zoho Mail их необходимо подготовить в Zoho Mail. В случае hello объекта Zoho Mail Подготовка выполняется вручную.

> [!NOTE]
> Можно использовать любые другие Zoho Mail пользователя средства создания учетных записей или интерфейсы API, предоставляемые Zoho Mail tooprovision учетных записей пользователей AAD.

### <a name="tooprovision-a-user-account-perform-hello-following-steps"></a>tooprovision учетной записи пользователя, выполните следующие шаги hello.

1. Войдите в tooyour **Zoho Mail** сайт компании от имени администратора.

2. Go слишком**панели управления \> почта и документы**.

3. Go слишком**сведения о пользователе \> добавить пользователя**.
   
    ![Добавление пользователя](./media/active-directory-saas-zoho-mail-tutorial/ic789611.png "Добавление пользователя")

4. На hello **Добавление пользователей** диалоговое окно, выполните следующие шаги hello:
   
    ![Добавление пользователя](./media/active-directory-saas-zoho-mail-tutorial/ic789612.png "Добавление пользователя")
   
    а. В hello **имя** в текстовое поле типа hello имя пользователя как **Britta**.

    b. В hello **Фамилия** в текстовое поле типа hello фамилию пользователя как **Simon**.

    c. В hello **адрес электронной почты** текстовое поле, идентификатор типа hello электронной почты пользователя, таких как  **brittasimon@contoso.com** .

    d. В hello **пароль** текстовом поле введите пароль пользователя.
   
    д. Нажмите кнопку **ОК**.  
      
    > [!NOTE]
    > Hello владельцем учетной записи Azure Active Directory получит сообщение электронной почты с учетной записью hello tooconfirm ссылку, чтобы она стала активной.

### <a name="assign-hello-azure-ad-test-user"></a>Назначить hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooZoho доступа.

![Назначение пользователям ролей hello][200] 

**tooassign tooZoho Britta Simon выполните следующие шаги hello.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **Zoho**.

    ![ссылка Zoho Hello в списке приложений hello](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_app.png)  

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Hello ссылку «Пользователи и группы»][202]

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![область назначения, добавьте Hello][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="test-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.

При нажатии кнопки hello Zoho плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour Zoho приложения.
Дополнительные сведения о панели доступа см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_203.png

