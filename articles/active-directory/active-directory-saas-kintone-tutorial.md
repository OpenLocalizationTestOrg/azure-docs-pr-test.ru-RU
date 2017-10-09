---
title: "Руководство по интеграции Azure Active Directory с Kintone | Документы Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Kintone."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c2b947dc-e1a8-4f5f-b40e-2c5180648e4f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jeedes
ms.openlocfilehash: 4f61fb95c643743504699b175beeff06e01c95c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kintone"></a>Руководство по интеграции Azure Active Directory с Kintone

В этом учебнике вы узнаете, как toointegrate Kintone с Azure Active Directory (Azure AD).

Интеграция Kintone с Azure AD предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooKintone
- Можно включить на пользователей tooautomatically get вошедшего tooKintone (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с Kintone, необходимо hello следующих элементов:

- подписка Azure AD;
- Подписка с поддержкой единого входа Kintone

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление Kintone из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-kintone-from-hello-gallery"></a>Добавление Kintone из галереи hello
tooconfigure hello интеграции Kintone в Azure AD, вы должны tooadd Kintone из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd Kintone из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Приложения][3]

4. Введите в поле поиска hello **Kintone**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_search.png)

5. В панели результатов hello выберите **Kintone**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в Kintone для тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Kintone является tooa в Azure AD. Другими словами связи между пользователя Azure AD и hello связанных пользователей в Kintone должен установить toobe.

В Kintone, присвоить значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.

tooconfigure и теста Azure AD единого входа с Kintone, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя Kintone](#creating-a-kintone-test-user)**  -toohave аналог Саймон Britta в Kintone, который представляет связанный toohello Azure AD пользователя.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении-Kintone.

**tooconfigure Azure AD единого входа с Kintone, выполните следующие шаги hello.**

1. В hello в hello портала Azure **Kintone** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_samlbase.png)

3. На hello **URL-адреса и домена Kintone** выполните следующие шаги hello:

    ![Настройка единого входа](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_url.png)

    а. В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<companyname>.kintone.com`

    b. В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:
    | |
    |--|
    | `https://<companyname>.cybozu.com`|
    | `https://<companyname>.kintone.com`|

    > [!NOTE] 
    > Эти значения приведены в качестве примера. Обновить значения hello фактический URL-адрес входа и идентификатор. Обратитесь к [группа поддержки клиента Kintone](https://www.kintone.com/contact/) tooget эти значения. 
 
4. На hello **сертификат подписи SAML** щелкните **сертификата (Base64)** и затем сохраните файл сертификата hello на вашем компьютере.

    ![Настройка единого входа](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-kintone-tutorial/tutorial_general_400.png)

6. На hello **конфигурации Kintone** щелкните **Настройка Kintone** tooopen **Настройка входа** окна. Копировать hello **URL-адрес выхода и SAML единого входа URL-адрес службы** из hello **краткий справочник.**

    ![Настройка единого входа](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_configure.png) 

7. В другом окне веб-браузера войдите на веб-сайт **Kintone** компании в качестве администратора.

8. Щелкните **Параметры**.
   
    ![Параметры](./media/active-directory-saas-kintone-tutorial/ic785879.png "Параметры")

9. Щелкните **Users & System Administration** (Администрирование пользователей и системы).
   
    ![Users & System Administration](./media/active-directory-saas-kintone-tutorial/ic785880.png "Users & System Administration") (Администрирование пользователей и системы)

10. Перейдите в раздел **System Administration \> Security** (Системное администрирование > Безопасность) и щелкните **Login** (Вход).
   
    ![Login](./media/active-directory-saas-kintone-tutorial/ic785881.png "Login") (Вход)

11. Установите флажок **Включить проверку подлинности SAML**.
   
    ![Аутентификация SAML](./media/active-directory-saas-kintone-tutorial/ic785882.png "Аутентификация SAML")

12. В hello раздел проверки подлинности SAML выполните следующие шаги hello.
    
    ![Аутентификация SAML](./media/active-directory-saas-kintone-tutorial/ic785883.png "Аутентификация SAML")
    
    а. В hello **URL-адрес входа** текстовое значение hello вставить **SAML единого входа URL-адрес службы** скопирован из портала Azure.
   
    b. В hello **URL-адрес выхода** текстовое значение hello вставить **URL-адрес выхода** скопирован из портала Azure.
    
    c. Нажмите кнопку **Обзор** tooupload загруженный сертификат.
    
    d. Щелкните **Сохранить**.

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-kintone-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-kintone-tutorial/create_aaduser_02.png) 

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-kintone-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-kintone-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-a-kintone-test-user"></a>Создание тестового пользователя Kintone

Пользователи toolog tooenable Azure AD в tooKintone, их необходимо подготовить в Kintone.  
В случае hello объекта Kintone Подготовка осуществляется вручную.

### <a name="tooprovision-a-user-account-perform-hello-following-steps"></a>tooprovision учетной записи пользователя, выполните следующие шаги hello.

1. Войдите в tooyour **Kintone** сайт компании от имени администратора.

2. Щелкните **Параметр**.
   
    ![Параметры](./media/active-directory-saas-kintone-tutorial/ic785879.png "Параметры")

3. Щелкните **Users & System Administration** (Администрирование пользователей и системы).
   
    ![Users & System Administration](./media/active-directory-saas-kintone-tutorial/ic785880.png "Users & System Administration") (Администрирование пользователей и системы)

4. В разделе **User Administration** (Администрирование пользователей) щелкните **Departments & Users** (Отделы и пользователи).
   
    ![Department & Users](./media/active-directory-saas-kintone-tutorial/ic785888.png "Department & Users") (Отделы и пользователи)

5. Щелкните **Новый пользователь**.
   
    ![Новые пользователи](./media/active-directory-saas-kintone-tutorial/ic785889.png "Новые пользователи")

6. В hello **нового пользователя** выполните следующие шаги hello:
   
    ![Новые пользователи](./media/active-directory-saas-kintone-tutorial/ic785890.png "Новые пользователи")
   
    а. Введите значение **отображаемое имя**, **имя входа**, **новый пароль**, **подтверждение пароля**, **адрес электронной почты**, и другие сведения о действительной учетной записи AAD, требуется tooprovision в hello связаны текстовые поля.
 
    b. Щелкните **Сохранить**.

> [!NOTE]
> Можно использовать любые другие Kintone пользователя средства создания учетных записей или интерфейсы API, предоставляемые Kintone tooprovision учетных записей пользователей AAD.

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooKintone доступа.

![Назначение пользователя][200] 

**tooassign tooKintone Britta Simon выполните следующие шаги hello.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **Kintone**.

    ![Настройка единого входа](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

Цель этого раздела Hello является tootest настройки единого входа Azure AD с помощью панели доступа "hello".

При нажатии кнопки hello Kintone плитки в панели доступа hello, вы должны получить приложение автоматически вошедшего tooyour Kintone.

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_203.png

