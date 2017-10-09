---
title: "Руководство по интеграции Azure Active Directory с Namely | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и т."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9541d5c4-4c82-4b5b-b01a-6a3f75a2b7a1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: b0477ca6fa52a21abea7de458f8a99a01e8c25c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-namely"></a>Руководство по интеграции Azure Active Directory с Namely

В этом учебнике вы узнаете, как toointegrate, а именно с Azure Active Directory (Azure AD).

А именно: интеграция с Azure AD предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooNamely
- Можно включить на пользователей tooautomatically get вошедшего tooNamely (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

Интеграция tooconfigure Azure AD, вам требуется hello следующих элементов:

- подписка Azure AD;
- подписка Namely с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. А именно: Добавление из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-namely-from-hello-gallery"></a>А именно: Добавление из галереи hello
tooconfigure hello интеграции а именно в Azure AD, вы должны tooadd, а именно из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd, а именно из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Приложения][3]

4. Введите в поле поиска hello **а именно**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-namely-tutorial/tutorial_namely_search.png)

5. В панели результатов hello выберите **а именно**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-namely-tutorial/tutorial_namely_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описаны настройка и проверка единого входа Azure AD в приложение Namely с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow какие hello аналога в а именно он tooa пользователя в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в а именно должен установить toobe.

В а именно, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.

tooconfigure и тестирования Azure AD единого входа, а именно, вам требуется hello toocomplete следующие компоненты:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание а именно тестовый пользователь](#creating-a-namely-test-user)**  -toohave квантор Саймон Britta, в т. то есть связанного toohello представление пользователя Azure AD.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в а именно приложение.

**tooconfigure Azure AD единого входа с а именно, выполните следующие шаги hello.**

1. В hello в hello портала Azure **а именно** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-namely-tutorial/tutorial_namely_samlbase.png)

3. На hello **URL-адреса и домена а именно** выполните следующие шаги hello:

    ![Настройка единого входа](./media/active-directory-saas-namely-tutorial/tutorial_namely_url.png)

    а. В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<subdomain>.namely.com`

    b. В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<subdomain>.namely.com/saml/metadata`

    > [!NOTE] 
    > Эти значения приведены в качестве примера. Обновить значения hello фактический URL-адрес входа и идентификатор. Обратитесь к [группа поддержки а именно клиент](https://www.namely.com/contact/) tooget эти значения. 
 
4. На hello **сертификат подписи SAML** щелкните **сертификата (Base64)** и затем сохраните файл сертификата hello на вашем компьютере.

    ![Настройка единого входа](./media/active-directory-saas-namely-tutorial/tutorial_namely_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-namely-tutorial/tutorial_general_400.png)

6. На hello **а именно конфигурации** щелкните **Настройка а именно** tooopen **Настройка входа** окна. Копировать hello **SAML единого входа URL-адрес службы** из hello **краткий справочник.**

    ![Настройка единого входа](./media/active-directory-saas-namely-tutorial/tutorial_namely_configure.png) 

7. В другом окне браузера Войдите на tooyour а именно на сайт компании от имени администратора.

8. Щелкните hello панели инструментов в верхней части hello **компании**.
   
    ![Настройка единого входа](./media/active-directory-saas-namely-tutorial/tutorial_namely_06.png) 

9. Нажмите кнопку hello **параметры** вкладки.
   
    ![Настройка единого входа](./media/active-directory-saas-namely-tutorial/tutorial_namely_07.png) 

10. Нажмите кнопку **SAML**.
   
    ![Настройка единого входа](./media/active-directory-saas-namely-tutorial/tutorial_namely_08.png) 

11. На hello **параметры SAML** выполните следующие шаги hello:
   
    ![Настройка единого входа](./media/active-directory-saas-namely-tutorial/tutorial_namely_09.png)
 
    а. Выберите команду **Enable SAML**(Включить SAML). 

    b. В hello **URL-адрес единого входа поставщика удостоверений** текстовое значение hello вставить **SAML единого входа URL-адрес службы**, который вы скопировали из портала Azure.
    
    c. Откройте загруженный сертификат в блокноте, hello копирования содержимого, а затем вставьте его в hello **сертификат поставщика удостоверений** текстового поля.
     
    d. Щелкните **Сохранить**.

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-namely-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-namely-tutorial/create_aaduser_02.png) 

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-namely-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-namely-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-a-namely-test-user"></a>Создание тестового пользователя Namely

Цель этого раздела Hello — toocreate пользователя с именем Britta Simon, а именно.

**toocreate пользователя с именем Britta Simon, а именно, выполните следующие шаги hello.**

1. А именно tooyour входа компании сайта от имени администратора.

2. Щелкните hello панели инструментов в верхней части hello **людей**.
   
    ![Настройка единого входа](./media/active-directory-saas-namely-tutorial/tutorial_namely_10.png) 

3. Нажмите кнопку hello **каталога** вкладки.
   
    ![Настройка единого входа](./media/active-directory-saas-namely-tutorial/tutorial_namely_11.png) 

4. Щелкните **Add New Person**(Добавить нового пользователя).

    ![Настройка единого входа](./media/active-directory-saas-namely-tutorial/tutorial_namely_12.png)

5. На hello **Добавление нового человека** диалоговое окно, выполните следующие шаги hello:

    а. В hello **имя** введите **Britta**.

    b. В hello **Фамилия** введите **Simon**.

    c. В hello **электронной почты** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    d. Щелкните **Сохранить**.

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooNamely доступа.

![Назначение пользователя][200] 

**tooassign tooNamely Britta Simon выполните следующие шаги hello.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **а именно**.

    ![Настройка единого входа](./media/active-directory-saas-namely-tutorial/tutorial_namely_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

Цель этого раздела Hello является tootest конфигурации единого входа Azure AD с помощью панели доступа "hello".

При нажатии кнопки hello а именно плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour а именно приложение

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-namely-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-namely-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-namely-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-namely-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-namely-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-namely-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-namely-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-namely-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-namely-tutorial/tutorial_general_203.png

