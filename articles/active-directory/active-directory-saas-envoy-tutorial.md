---
title: "Учебник. Интеграция Azure Active Directory с Envoy | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и делегатов."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 71f7afcc-1033-4098-9b7e-4f9f2b26f734
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: jeedes
ms.openlocfilehash: 93add7c1f3cf1fc163acc505f11e34bd696c571c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-envoy"></a>Руководство. Интеграция Azure Active Directory с Envoy

В этом учебнике вы узнаете, как toointegrate Envoy с Azure Active Directory (Azure AD).

Интеграция делегатов с Azure AD предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooEnvoy.
- Можно включить на пользователей tooautomatically get вошедшего tooEnvoy (Single Sign-On) с помощью своих учетных записей Azure AD.
- Вы можете управлять учетными записями в одном централизованном месте - hello портал Azure.

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с Envoy требуется hello следующих элементов:

- подписка Azure AD;
- подписка Envoy с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление делегатов из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-envoy-from-hello-gallery"></a>Добавление делегатов из галереи hello
tooconfigure hello интеграция делегатов в Azure AD, вы должны tooadd делегата из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd Envoy из галереи hello выполните следующие шаги hello.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Кнопка Hello Azure Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Hello корпоративных приложений колонку][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Кнопка нового приложения Hello][3]

4. Введите в поле поиска hello **Envoy**выберите **Envoy** из панели результатов щелкните **добавить** кнопку tooadd приложения hello.

    ![Envoy в списке результатов hello](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD

В этом разделе описана настройка и проверка единого входа Azure AD в приложение Envoy с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Envoy является tooa в Azure AD. Иными словами связи между пользователя Azure AD и hello связанных пользователей в Envoy требуется установить toobe.

В Envoy, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.

tooconfigure и теста Azure AD единого входа с Envoy, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя, прошедшего Envoy](#create-an-envoy-test-user)**  -toohave аналог Саймон Britta в Envoy, который представляет связанный toohello Azure AD пользователя.
4. **[Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#test-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configure-azure-ad-single-sign-on"></a>Настройка единого входа Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в Envoy приложения.

**tooconfigure Azure AD единого входа с Envoy, выполните следующие шаги hello.**

1. В hello в hello портала Azure **Envoy** странице интеграции приложения щелкните **единого входа**.

    ![Ссылка "Настройка единого входа"][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_samlbase.png)

3. На hello **URL-адреса и домена Envoy** выполните следующие шаги hello:

    ![Сведения о домене и URL-адресах единого входа приложения Envoy](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_url.png)

    В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<tenant-name>.Envoy.com`
    
    > [!NOTE] 
    > Это значение приведено для справки. Измените значение этого параметра hello фактический URL-адрес входа. Обратитесь к [группа поддержки клиент Envoy](https://envoy.com/contact/) tooget это значение.

4. На hello **сертификат подписи SAML** раздел, hello копирования **ОТПЕЧАТОК** значение сертификата...

    ![ссылку для скачивания сертификата Hello](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-envoy-tutorial/tutorial_general_400.png)

6. На hello **конфигурации Envoy** щелкните **Настройка Envoy** tooopen **Настройка входа** окна. Копировать hello **SAML единого входа URL-адрес службы** из hello **краткий справочник.**

    ![Конфигурация Envoy](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_configure.png)

7. В другом окне веб-браузера войдите на свой корпоративный веб-сайт Envoy в качестве администратора.

8. Щелкните hello панели инструментов в верхней части hello **параметры**.

    ![Envoy](./media/active-directory-saas-envoy-tutorial/ic776782.png "Envoy")

9. Нажмите **Компания**.

    ![Организация](./media/active-directory-saas-envoy-tutorial/ic776783.png "Организация")

10. Нажмите кнопку **SAML**.

    ![SAML](./media/active-directory-saas-envoy-tutorial/ic776784.png "SAML")

11. В hello **проверку подлинности SAML** конфигурации выполните следующие шаги hello:

    ![Аутентификация SAML](./media/active-directory-saas-envoy-tutorial/ic776785.png "Аутентификация SAML")
    
    >[!NOTE]
    >Hello для ИД расположения главного Офиса hello значение auto, созданном приложением hello.
    
    а. В **отпечатков пальцев** текстовое поле, вставить hello **отпечаток** значение сертификат, который вы скопировали из портала Azure.
    
    b. Вставить **SAML единого входа URL-адрес службы** значение, которое вы скопировали форме hello Azure портала в hello **URL-адрес HTTP ПОСТАВЩИКА SAML IDENTITY** текстового поля.
    
    c. Нажмите кнопку **Сохранить изменения**.

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD

Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

   ![Создание тестового пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello hello левой панели портала Azure щелкните hello **Azure Active Directory** кнопки.

    ![Кнопка Hello Azure Active Directory](./media/active-directory-saas-envoy-tutorial/create_aaduser_01.png)

2. слишком go toodisplay hello список пользователей,**пользователей и групп**, а затем нажмите кнопку **всех пользователей**.

    ![Здравствуйте, «Пользователи и группы» и «Все пользователи» ссылки](./media/active-directory-saas-envoy-tutorial/create_aaduser_02.png)

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** вверху hello hello **всех пользователей** диалоговое окно.

    ![Кнопка "Добавить" Hello](./media/active-directory-saas-envoy-tutorial/create_aaduser_03.png)

4. В hello **пользователя** диалогового окна выполните следующие шаги hello:

    ![диалоговое окно приветствия пользователя](./media/active-directory-saas-envoy-tutorial/create_aaduser_04.png)

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** поле типа hello адрес электронной почты пользователя Саймон Britta.

    c. Выберите hello **Показать пароль** флажок и запишите значение hello, отображаемый в hello **пароль** поле.

    d. Щелкните **Создать**.
 
### <a name="create-an-envoy-test-user"></a>Создание тестового пользователя Envoy

Нет элемента действия для вас tooconfigure подготовки пользователей tooEnvoy. Когда назначенный пользователь пытается toolog в Envoy с помощью панели доступа hello, Envoy проверяет, существует ли пользователь hello. Если учетная запись пользователя отсутствует, Envoy автоматически создает ее.

### <a name="assign-hello-azure-ad-test-user"></a>Назначить hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooEnvoy доступа.

![Назначение пользователям ролей hello][200] 

**tooassign tooEnvoy Britta Simon выполните следующие шаги hello.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **Envoy**.

    ![ссылка Envoy Hello в списке приложений hello](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_app.png)  

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Hello ссылку «Пользователи и группы»][202]

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![область назначения, добавьте Hello][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="test-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.

При нажатии кнопки hello Envoy плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour Envoy приложения.
Дополнительные сведения о панели доступа см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_203.png

