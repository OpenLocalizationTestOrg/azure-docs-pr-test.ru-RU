---
title: "Учебник. Интеграция Azure Active Directory с Rally Software | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Rally Software."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: ba25fade-e152-42dd-8377-a30bbc48c3ed
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: jeedes
ms.openlocfilehash: c75c8b98ce7fab19964c13de5ad7e19ef3ebd0e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rally-software"></a>Учебник. Интеграция Azure Active Directory с Rally Software

В этом учебнике вы узнаете, как toointegrate Rally Software с Azure Active Directory (Azure AD).

Интеграция Rally Software с Azure AD предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooRally программного обеспечения.
- Можно включить на пользователей tooautomatically get вошедшего tooRally программного обеспечения (Single Sign-On) с помощью своих учетных записей Azure AD.
- Вы можете управлять учетными записями в одном централизованном месте - hello портал Azure.

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с Rally Software, требуется hello следующих элементов:

- подписка Azure AD;
- подписка Rally Software с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление Rally Software из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-rally-software-from-hello-gallery"></a>Добавление Rally Software из галереи hello
tooconfigure hello интеграцией Rally Software с Azure AD, вы должны tooadd Rally Software из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd Rally Software из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Кнопка Hello Azure Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Hello корпоративных приложений колонку][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Кнопка нового приложения Hello][3]

4. Введите в поле поиска hello **Rally Software**выберите **Rally Software** из панели результатов щелкните **добавить** кнопку tooadd приложения hello.

    ![Программное обеспечение Rally в списке результатов hello](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD

В этом разделе описана настройка и проверка единого входа Azure AD в Rally Software для тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Rally Software является tooa в Azure AD. Другими словами связи между пользователя Azure AD и hello связанных пользователей в Rally Software должен установить toobe.

В Rally Software, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.

tooconfigure и теста Azure AD единого входа с Rally Software, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя Rally Software](#create-a-rally-software-test-user)**  -toohave аналог Саймон Britta в Rally Software, представление связанных toohello Azure AD пользователя.
4. **[Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#test-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configure-azure-ad-single-sign-on"></a>Настройка единого входа Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Rally Software.

**tooconfigure Azure AD единого входа с Rally Software, выполните следующие шаги hello.**

1. В hello в hello портала Azure **Rally Software** странице интеграции приложения щелкните **единого входа**.

    ![Ссылка "Настройка единого входа"][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_samlbase.png)

3. На hello **URL-адреса и домена программное обеспечение Rally** выполните следующие шаги hello:

    ![Сведения о домене и URL-адресах единого входа приложения Rally Software](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_url.png)

    а. В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<tenant-name>.rally.com`

    b. В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<tenant-name>.rally.com`

    > [!NOTE] 
    > Эти значения приведены в качестве примера. Обновить значения hello фактический URL-адрес входа и идентификатор. Обратитесь к [Rally клиентское программное обеспечение поддержки](https://help.rallydev.com/) tooget эти значения. 
 


4. На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.

    ![ссылку для скачивания сертификата Hello](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-rally-software-tutorial/tutorial_general_400.png)

6. На hello **Rally конфигурации программного обеспечения** щелкните **Настройка Rally Software** tooopen **Настройка входа** окна. Копировать hello **URL-адрес выхода и идентификатор сущности SAML** из hello **краткий справочник.**

    ![Настройка Rally Software](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_configure.png) 

7. Войдите в tooyour **Rally Software** клиента.

8. Щелкните hello панели инструментов в верхней части hello **установки**, а затем выберите **подписки**.
   
    ![Подписка](./media/active-directory-saas-rally-software-tutorial/ic769531.png "Подписка")

9. Нажмите кнопку hello **действия** кнопки. Выберите **изменение подписки** в hello верхней правой части панели инструментов hello.

10. На hello **подписки** странице диалогового окна, выполните следующие шаги hello и нажмите кнопку **сохранить и закрыть**:
   
    ![Аутентификация](./media/active-directory-saas-rally-software-tutorial/ic769542.png "Аутентификация")
   
    а. Из раскрывающегося списка "Аутентификация" выберите пункт **Rally or SSO authentication** (Аутентификация Rally или путем единого входа).

    b. В hello **URL-адрес поставщика удостоверений** текстовое значение hello вставить **идентификатор сущности SAML**, который вы скопировали из портала Azure. 

    c. В hello **выхода SSO** текстовое значение hello вставить **URL-адрес выхода**, который вы скопировали из портала Azure.

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD

Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

   ![Создание тестового пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello hello левой панели портала Azure щелкните hello **Azure Active Directory** кнопки.

    ![Кнопка Hello Azure Active Directory](./media/active-directory-saas-rally-software-tutorial/create_aaduser_01.png)

2. слишком go toodisplay hello список пользователей,**пользователей и групп**, а затем нажмите кнопку **всех пользователей**.

    ![Здравствуйте, «Пользователи и группы» и «Все пользователи» ссылки](./media/active-directory-saas-rally-software-tutorial/create_aaduser_02.png)

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** вверху hello hello **всех пользователей** диалоговое окно.

    ![Кнопка "Добавить" Hello](./media/active-directory-saas-rally-software-tutorial/create_aaduser_03.png)

4. В hello **пользователя** диалогового окна выполните следующие шаги hello:

    ![диалоговое окно приветствия пользователя](./media/active-directory-saas-rally-software-tutorial/create_aaduser_04.png)

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** поле типа hello адрес электронной почты пользователя Саймон Britta.

    c. Выберите hello **Показать пароль** флажок и запишите значение hello, отображаемый в hello **пароль** поле.

    d. Щелкните **Создать**.
 
### <a name="create-a-rally-software-test-user"></a>Создание тестового пользователя Rally Software

Для Azure AD пользователи toobe может toosign в они должны быть подготовленных toohello приложении Rally Software с использованием своих имен пользователей Azure Active Directory.

**tooconfigure подготовки пользователей, выполните следующие шаги hello.**

1. Войдите в систему tooyour клиент Rally Software.

2. Go слишком**установки \> пользователей**и нажмите кнопку **+ добавить New**.
   
    ![Пользователи](./media/active-directory-saas-rally-software-tutorial/ic781039.png "Пользователи")

3. Введите имя hello в текстовом поле hello нового пользователя и нажмите кнопку **добавить с подробностями**.

4. В hello **Create User** выполните следующие шаги hello:
   
    ![Создание пользователя](./media/active-directory-saas-rally-software-tutorial/ic781040.png "Создание пользователя")

    а. В hello **имя пользователя** в текстовое поле имя пользователя как типа hello **Brittsimon**.
   
    b. В **адрес электронной почты** текстовом поле введите адрес электронной почты hello пользователя как  **brittasimon@contoso.com** .

    c. В **имя** текста введите имя пользователя, такие как hello **Britta**.

    d. В **Фамилия** текста введите hello фамилию пользователя как **Simon**.

    д. Щелкните **Save & Close** (Сохранить и закрыть).

   >[!NOTE]
   >Можно использовать любые другие Rally Software пользователя средства создания учетных записей или интерфейсы API, предоставляемые Rally Software tooprovision учетных записей пользователей Azure AD.

### <a name="assign-hello-azure-ad-test-user"></a>Назначить hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooRally программного обеспечения.

![Назначение пользователям ролей hello][200] 

**tooassign tooRally Britta Simon программное обеспечение, выполните hello следующие шаги.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **Rally Software**.

    ![ссылка Rally Software Hello в списке приложений hello](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_app.png)  

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Hello ссылку «Пользователи и группы»][202]

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![область назначения, добавьте Hello][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="test-single-sign-on"></a>Проверка единого входа

Цель этого раздела Hello является tootest настройки единого входа Azure AD с помощью панели доступа "hello".

Если щелкнуть плитку Rally Software hello в hello панели доступа, вы должны получить tooyour автоматически подписью в приложении Rally Software.

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_203.png

