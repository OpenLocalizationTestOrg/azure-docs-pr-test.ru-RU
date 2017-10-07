---
title: "Руководство по интеграции Azure Active Directory с Adobe Sign | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Adobe знаком."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f9385723-8fe7-4340-8afb-1508dac3e92b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/24/2017
ms.author: jeedes
ms.openlocfilehash: b4b07907f30a0890003554a02a76d968400b43ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adobe-sign"></a>Руководство по интеграции Azure Active Directory с Adobe Sign

В этом учебнике вы узнаете, как Adobe toointegrate, войдите в Azure Active Directory (Azure AD).

Интеграция с Azure AD входа Adobe предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooAdobe входа
- Можно включить на пользователей tooautomatically get вошедшего tooAdobe входа (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с Adobe входа требуется hello следующих элементов:

- подписка Azure AD;
- подписка Adobe Sign с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление входа Adobe из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-adobe-sign-from-hello-gallery"></a>Добавление входа Adobe из галереи hello
tooconfigure hello интеграции Adobe входа в Azure AD, вы должны tooadd входа Adobe из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd входа Adobe из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Приложения][3]

4. Введите в поле поиска hello **входа Adobe**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_search.png)

5. В панели результатов hello выберите **входа Adobe**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в Adobe Sign с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Adobe входа является tooa в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в Adobe входа должен установить toobe.

В Adobe знака, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.

tooconfigure и теста Azure AD единого входа с Adobe входа, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя, прошедшего входа Adobe](#creating-an-adobe-sign-test-user)**  -toohave аналог Саймон Britta в Adobe знак, который является представлением связанного toohello Azure AD пользователя.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Adobe входа.

**Azure AD tooconfigure единого входа с входа Adobe выполните hello следующие шаги.**

1. В hello в hello портала Azure **входа Adobe** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_samlbase.png)

3. На hello **URL-адреса и домена входа Adobe** выполните следующие шаги hello:

    ![Настройка единого входа](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_url.png)

    а. В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<companyname>.echosign.com/`

    b. В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<companyname>.echosign.com`

    > [!NOTE] 
    > Эти значения приведены в качестве примера. Обновить значения hello фактический URL-адрес входа и идентификатор. Обратитесь к [группа поддержки клиента входа Adobe](https://helpx.adobe.com/in/contact/support.html) tooget эти значения. 
 
4. На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.

    ![Настройка единого входа](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_400.png)

6. На hello **конфигурации входа Adobe** щелкните **входа Adobe Настройка** tooopen **Настройка входа** окна. Копировать hello **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**

    ![Настройка единого входа](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_configure.png) 


7. В другом окне браузера Войдите на сайте компании tooyour входа Adobe в качестве администратора.

8. В меню в верхней части hello hello выберите **учетной записи**, hello hello левой панели навигации нажмите кнопку **параметры SAML** под **параметры учетной записи**.
   
   ![Учетная запись](./media/active-directory-saas-adobe-echosign-tutorial/ic789520.png "Учетная запись")

9. В hello в разделе "Параметры SAML" выполните следующие шаги hello.
   
   ![Параметры SAML](./media/active-directory-saas-adobe-echosign-tutorial/ic789521.png "Параметры SAML")
   
   а. В разделе **SAML Mode** (Режим SAML) выберите параметр **SAML Mandatory** (SAML обязательно).
   
   b. Выберите **toolog Разрешить администраторам учетных записей EchoSign с помощью учетных данных EchoSign**.
   
   c. В разделе **User Creation** (Создание пользователей) установите флажок **Automatically add users authenticated through SAML** (Автоматически добавлять пользователей, прошедших проверку подлинности с использованием SAML).

10. Продолжите и выполнении hello следующие шаги:

       ![Параметры SAML](./media/active-directory-saas-adobe-echosign-tutorial/ic789522.png "Параметры SAML")

    а. Вставить **SAML идентификатор сущности**, который вы скопировали из портала Azure в hello **идентификатор сущности поставщика удостоверений** текстового поля.
    
    b. Вставить **SAML единого входа URL-адрес службы**, который вы скопировали из портала Azure в hello **URL-адрес входа поставщика удостоверений** текстового поля.
   
    c. Вставить **URL-адрес выхода**, который вы скопировали из портала Azure в hello **URL-адрес выхода поставщика удостоверений** текстового поля.

    d. Откройте ваш загруженный **Certificate(Base64)** в блокноте, hello копирования содержимого его в буфер обмена, а затем вставьте его toohello **сертификат поставщика удостоверений** текстового поля

    д. Нажмите кнопку **Сохранить изменения**.

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_02.png) 

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-an-adobe-sign-test-user"></a>Создание тестового пользователя Adobe Sign

Пользователи toolog tooenable Azure AD в tooAdobe входа, их необходимо подготовить в Adobe входа. В случае hello входа Adobe Подготовка выполняется вручную.

>[!NOTE]
>Можно использовать любые другие Adobe входа пользователя средства создания учетных записей или интерфейсы API, предоставляемые tooprovision входа Adobe учетных записей пользователей AAD. 

**tooprovision учетной записи пользователя, выполните следующие шаги hello.**

1. Войдите в tooyour **входа Adobe** сайт компании от имени администратора.

2. В меню в верхней части hello hello выберите **учетной записи**, hello hello левой панели навигации нажмите кнопку **пользователи и группы**и нажмите кнопку **создать нового пользователя**.
   
   ![Учетная запись](./media/active-directory-saas-adobe-echosign-tutorial/ic789524.png "Учетная запись")
   
3. В hello **создать нового пользователя** выполните следующие шаги hello:
   
   ![Создание пользователя](./media/active-directory-saas-adobe-echosign-tutorial/ic789525.png "Создание пользователя")
   
   а. Тип hello **адрес электронной почты**, **имя**, и **Фамилия** из текстовых полей, связанных с действительной учетной записи AAD, которые должны tooprovision hello.
   
   b. Нажмите кнопку **Создать пользователя**.

>[!NOTE]
>Владелец учетной записи Azure Active Directory Hello получает сообщение электронной почты, который включает учетную запись hello tooconfirm ссылку, чтобы она стала активной. 

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooAdobe входа.

![Назначение пользователя][200] 

**tooassign tooAdobe Britta Simon входа, выполните следующие шаги hello.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **входа Adobe**.

    ![Настройка единого входа](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

При нажатии кнопки входа Adobe плитки в панели доступа hello приветствия, вы должны получить автоматически вошедшего tooyour входа Adobe приложения.
Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_203.png

