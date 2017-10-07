---
title: "Руководство по интеграции Azure Active Directory с Sprinklr | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory с Sprinklr."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b33938a1-25a5-484c-8e75-7dc6de2d534d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: jeedes
ms.openlocfilehash: 14b467c72d4a453ed7ad248eadcdade710f105af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sprinklr"></a>Учебник. Интеграция Azure Active Directory с Sprinklr

В этом учебнике вы узнаете, как toointegrate Sprinklr с Azure Active Directory (Azure AD).

Интеграция Sprinklr с Azure AD предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooSprinklr
- Можно включить на пользователей tooautomatically get вошедшего tooSprinklr (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с Sprinklr требуется hello следующих элементов:

- подписка Azure AD;
- подписка Sprinklr с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление Sprinklr из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-sprinklr-from-hello-gallery"></a>Добавление Sprinklr из галереи hello
tooconfigure hello интеграции Sprinklr в Azure AD, вы должны tooadd Sprinklr из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd Sprinklr из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Приложения][3]

4. Введите в поле поиска hello **Sprinklr**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_search.png)

5. В панели результатов hello выберите **Sprinklr**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в Sprinklr для тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Sprinklr является tooa в Azure AD. Другими словами связи между пользователя Azure AD и hello связанных пользователей в Sprinklr должен установить toobe.

В Sprinklr, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.

tooconfigure и теста Azure AD единого входа с Sprinklr, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя Sprinklr](#creating-a-sprinklr-test-user)**  -toohave аналог Саймон Britta в Sprinklr, который представляет связанный toohello Azure AD пользователя.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Sprinklr.

**Azure AD tooconfigure единого входа с Sprinklr, выполните следующие шаги hello.**

1. В hello в hello портала Azure **Sprinklr** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_samlbase.png)

3. На hello **URL-адреса и домена Sprinklr** выполните следующие шаги hello:

    ![Настройка единого входа](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_url.png)

    а. В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<subdomain>.sprinklr.com`

    b. В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<subdomain>.sprinklr.com`

    > [!NOTE] 
    > Эти значения приведены в качестве примера. Обновите значение hello с hello фактический URL-адрес входа и идентификатор. Обратитесь к [группа поддержки клиент Sprinklr](https://www.sprinklr.com/contact-us/) tooget эти значения. 
 
4. На hello **сертификат подписи SAML** щелкните **сертификата (Base64)** и затем сохраните файл сертификата hello на вашем компьютере.

    ![Настройка единого входа](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-sprinklr-tutorial/tutorial_general_400.png)

6. На hello **конфигурации Sprinklr** щелкните **Настройка Sprinklr** tooopen **Настройка входа** окна. Копировать hello **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**

7. В другом окне браузера войти в корпоративный сайт Sprinklr tooyour с правами администратора.

8. Go слишком**администрирования \> параметры**.
   
    ![Администрирование](./media/active-directory-saas-sprinklr-tutorial/ic782907.png "Администрирование")

9. Go слишком**управление партнера \> единого входа** на левой панели щелкните hello.
   
    ![Управление партнером](./media/active-directory-saas-sprinklr-tutorial/ic782908.png "Управление партнером")

10. Щелкните **+ Добавить параметры единого входа**.
   
    ![Единый вход](./media/active-directory-saas-sprinklr-tutorial/ic782909.png "Единый вход")

11. На hello **единого входа в систему** выполните следующие шаги hello:
   
    ![Единый вход](./media/active-directory-saas-sprinklr-tutorial/ic782910.png "Единый вход")

    а. В hello **имя** текстовом поле введите имя для конфигурации (например: *WAADSSOTest*).

    b. Щелкните **Включено**.

    c. Установите флажок **Использовать новый сертификат единого входа**.
             
    д. Откройте сертификат в кодировке base-64 в блокноте, hello копирования содержимого его в буфер обмена, а затем вставьте его toohello **сертификат поставщика удостоверений** текстового поля.

    f. Вставить hello **идентификатор сущности SAML** значение, которое было скопировано из портала Azure в hello **идентификатор сущности** текстового поля.

    ж. Вставить hello **SAML единого входа URL-адрес службы** значение, которое было скопировано из портала Azure в hello **URL-адрес входа поставщика удостоверений** текстового поля.

    h. Вставить hello **URL-адрес выхода** значение, которое было скопировано из портала Azure в hello **URL-адрес выхода поставщика удостоверений** текстового поля.
     
    i. В поле **SAML User ID Type** (Тип идентификатора пользователя SAML) выберите значение **Assertion contains User”s sprinklr.com username** (Утверждение содержит имя пользователя sprinklr.com).

    j. Как **местоположение идентификатора пользователя SAML**выберите **идентификатор пользователя находится в элемент идентификатора имени hello hello оператора Subject**.

    k. Щелкните **Сохранить**.
       
    ![SAML](./media/active-directory-saas-sprinklr-tutorial/ic782911.png "SAML")

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_02.png) 

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sprinklr-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-a-sprinklr-test-user"></a>Создание тестового пользователя Skilljar

1. Войдите в tooyour корпоративный сайт Sprinklr с правами администратора.

2. Go слишком**администрирования \> параметры**.
   
    ![Администрирование](./media/active-directory-saas-sprinklr-tutorial/ic782907.png "Администрирование")

3. Go слишком**управление клиента \> пользователей** hello левой панели.
   
    ![Параметры](./media/active-directory-saas-sprinklr-tutorial/ic782914.png "Параметры")

4. Нажмите кнопку **Add User**(Добавить пользователя).
   
    ![Параметры](./media/active-directory-saas-sprinklr-tutorial/ic782915.png "Параметры")

5. На hello **пользователя изменить** диалоговое окно, выполните следующие шаги hello:
   
    ![Изменение пользователя](./media/active-directory-saas-sprinklr-tutorial/ic782916.png "Изменение пользователя") 

    а. В hello **электронной почты**, **имя** и **Фамилия** текстовые поля, типа hello сведения учетной записи пользователя в Azure AD, вы хотите tooprovision.

    b. Установите флажок **Пароль отключен**.

    c. Выберите **Язык**.

    г) Выберите **Тип пользователя**.

    д. Нажмите кнопку **Обновить**.
   
     >[!IMPORTANT]
     >**Пароль отключен** должен быть выбранного tooenable в toolog пользователя через поставщика удостоверений. 
     
6. Go слишком**роли**, а затем выполните следующие шаги hello:
   
    ![Роли партнера](./media/active-directory-saas-sprinklr-tutorial/ic782917.png "Роли партнера")

    а. Из hello **Global** выберите **все\_разрешений**.  

    b. Нажмите кнопку **Обновить**.

>[!NOTE]
>Можно использовать любые другие Sprinklr пользователя средства создания учетных записей или API, предоставленные Sprinklr tooprovision учетных записей пользователей Azure AD. 

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooSprinklr доступа.

![Назначение пользователя][200] 

**tooassign tooSprinklr Britta Simon выполните следующие шаги hello.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **Sprinklr**.

    ![Настройка единого входа](./media/active-directory-saas-sprinklr-tutorial/tutorial_sprinklr_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.

При нажатии кнопки hello Sprinklr плитки в панели доступа hello, вы должны получить tooyour автоматически подписью в приложении Sprinklr Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sprinklr-tutorial/tutorial_general_203.png

