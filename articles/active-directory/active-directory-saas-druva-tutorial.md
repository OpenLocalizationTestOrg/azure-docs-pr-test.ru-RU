---
title: "Руководство по интеграции Azure Active Directory с Druva | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Druva."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: ab92b600-1fea-4905-b1c7-ef8e4d8c495c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: a1c36c06d6d005e0aa363fbf34efe630e4cca1ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-druva"></a>Руководство по интеграции Azure Active Directory с Druva

В этом учебнике вы узнаете, как toointegrate Druva с Azure Active Directory (Azure AD).

Интеграция Druva с Azure AD предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooDruva.
- Можно включить на пользователей tooautomatically get вошедшего tooDruva (Single Sign-On) с помощью своих учетных записей Azure AD.
- Вы можете управлять учетными записями в одном централизованном месте - hello портал Azure.

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с Druva требуется hello следующих элементов:

- подписка Azure AD;
- Подписка с поддержкой единого входа Druva

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление Druva из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-druva-from-hello-gallery"></a>Добавление Druva из галереи hello
tooconfigure hello интеграции Druva в Azure AD, вы должны tooadd Druva из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd Druva из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Кнопка Hello Azure Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Hello корпоративных приложений колонку][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Кнопка нового приложения Hello][3]

4. Введите в поле поиска hello **Druva**выберите **Druva** из панели результатов щелкните **добавить** кнопку tooadd приложения hello.

    ![Druva в списке результатов hello](./media/active-directory-saas-druva-tutorial/tutorial_druva_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD

В этом разделе описана настройка и проверка единого входа Azure AD в приложение Druva с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Druva является tooa в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в Druva должен установить toobe.

В Druva, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.

tooconfigure и теста Azure AD единого входа с Druva, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя Druva](#create-a-druva-test-user)**  -toohave аналог Саймон Britta в Druva, который представляет связанный toohello Azure AD пользователя.
4. **[Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#test-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configure-azure-ad-single-sign-on"></a>Настройка единого входа Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в свое приложение Druva.

**tooconfigure Azure AD единого входа с Druva, выполните следующие шаги hello.**

1. В hello в hello портала Azure **Druva** странице интеграции приложения щелкните **единого входа**.

    ![Ссылка "Настройка единого входа"][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-druva-tutorial/tutorial_druva_samlbase.png)

3. На hello **URL-адреса и домена Druva** выполните следующие шаги hello:

    ![Настройка единого входа](./media/active-directory-saas-druva-tutorial/tutorial_druva_url.png)

    В hello **URL-адрес входа** текстовом поле введите URL-адрес hello:`https://cloud.druva.com/home`

4. На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.

    ![ссылку для скачивания сертификата Hello](./media/active-directory-saas-druva-tutorial/tutorial_druva_certificate.png) 

5. Приложение Druva ожидает утверждения SAML hello в определенном формате, поэтому требует сопоставления tooyour tooadd настраиваемого атрибута **атрибутов токена SAML** конфигурации. 

    ![Настройка единого входа](./media/active-directory-saas-druva-tutorial/tutorial_druva_attribute.png)

6. В hello **атрибуты пользователя** раздела, посвященного hello **единого входа** диалогового окна настройки атрибутов токена SAML, как показано в hello предшествующий образ и выполнить следующие шаги hello:

    | Имя атрибута      | Значение атрибута      |
    | ------------------- | -------------------- |
    | insync\_auth\_token |Введите значение маркера созданный hello |
    
    а. Нажмите кнопку **добавить атрибут** tooopen hello **Добавление атрибута** диалогового окна.
    
    ![Настройка единого входа](./media/active-directory-saas-druva-tutorial/tutorial_attribute_04.png)
    
    ![Настройка единого входа](./media/active-directory-saas-druva-tutorial/tutorial_attribute_05.png)
    
    b. В hello **имя** в текстовое поле имя атрибута типа hello, показанный для этой строки.

    c. Из hello **значение** списка значение атрибута типа hello, показанный для этой строки. значение маркера созданный Hello описан далее в учебнике.
    
    d. Нажмите кнопку **ОК**.    

7. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-druva-tutorial/tutorial_general_400.png)

8. На hello **конфигурации Druva** щелкните **Настройка Druva** tooopen **Настройка входа** окна. Копировать hello **URL-адрес выхода и SAML единого входа URL-адрес службы** из hello **краткий справочник.**

    ![Настройка единого входа](./media/active-directory-saas-druva-tutorial/tutorial_druva_configure.png) 

9. В другом окне браузера Войдите на сайте компании Druva tooyour в качестве администратора.

10. Go слишком**управление \> параметры**.

    ![Параметры](./media/active-directory-saas-druva-tutorial/ic795091.png "Параметры")

11. В диалоговом окне приветствия параметры единого входа выполните hello следующие шаги.

    ![Параметры единого входа](./media/active-directory-saas-druva-tutorial/ic795092.png "Параметры единого входа")
    
    а. Вставить **SAML единого входа URL-адрес службы** значение, которое было скопировано из hello портал Azure в hello **URL-адрес входа поставщика Идентификаторов** текстового поля.
    
    b. Вставить **URL-адрес выхода** значение, которое было скопировано из hello портал Azure в hello **URL-адрес выхода поставщика Идентификаторов** текстового поля.
    
     c. Откройте сертификат в кодировке base-64 в блокноте, hello копирования содержимого его в буфер обмена, а затем вставьте его toohello **сертификат поставщика Идентификаторов** текстового поля
     
     d. tooopen hello **параметры** щелкните **Сохранить**.

12. На hello **параметры** щелкните **создать токен единого входа**.

    ![Параметры](./media/active-directory-saas-druva-tutorial/ic795093.png "Параметры")

13. На hello **единого входа для проверки подлинности маркера** диалоговое окно, выполните следующие шаги hello:

    ![Маркер единого входа](./media/active-directory-saas-druva-tutorial/ic795094.png "Маркер единого входа")
    
    а. Нажмите кнопку **копирования**, Вставка скопированного значения в hello **значение** текстовое поле в hello **Добавление атрибута** раздела.
    
    b. Нажмите кнопку **Закрыть**

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD

Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

   ![Создание тестового пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello hello левой панели портала Azure щелкните hello **Azure Active Directory** кнопки.

    ![Кнопка Hello Azure Active Directory](./media/active-directory-saas-druva-tutorial/create_aaduser_01.png)

2. слишком go toodisplay hello список пользователей,**пользователей и групп**, а затем нажмите кнопку **всех пользователей**.

    ![Здравствуйте, «Пользователи и группы» и «Все пользователи» ссылки](./media/active-directory-saas-druva-tutorial/create_aaduser_02.png)

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** вверху hello hello **всех пользователей** диалоговое окно.

    ![Кнопка "Добавить" Hello](./media/active-directory-saas-druva-tutorial/create_aaduser_03.png)

4. В hello **пользователя** диалогового окна выполните следующие шаги hello:

    ![диалоговое окно приветствия пользователя](./media/active-directory-saas-druva-tutorial/create_aaduser_04.png)

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** поле типа hello адрес электронной почты пользователя Саймон Britta.

    c. Выберите hello **Показать пароль** флажок и запишите значение hello, отображаемый в hello **пароль** поле.

    d. Щелкните **Создать**.
 
### <a name="create-a-druva-test-user"></a>Создание тестового пользователя Druva

В порядке tooenable toolog пользователей Azure AD в tooDruva их необходимо подготовить в Druva. В случае hello объекта Druva Подготовка выполняется вручную.

**tooconfigure подготовки пользователей, выполните следующие шаги hello.**

1. Войдите в tooyour **Druva** сайт компании от имени администратора.

2. Go слишком**управление \> пользователей**.
   
   ![Управление пользователями](./media/active-directory-saas-druva-tutorial/ic795097.png "Управление пользователями")

3. Щелкните **Создать**.
   
   ![Управление пользователями](./media/active-directory-saas-druva-tutorial/ic795098.png "Управление пользователями")

4. В диалоговом окне Создать нового пользователя hello выполните следующие шаги hello.
   
   ![Создание пользователя](./media/active-directory-saas-druva-tutorial/ic795099.png "Создание пользователя")
   
   а. В hello **адрес электронной почты** текстовом поле введите адрес электронной почты hello пользователя как  **brittasimon@contoso.com** .
   
   b. В hello **имя** текстовом поле введите имя пользователя, такие как hello **BrittaSimon**.
   
   c. Нажмите кнопку **Создать пользователя**.

>[!NOTE]
>Можно использовать любые другие Druva пользователя средства создания учетных записей или интерфейсы API, предоставляемые Druva tooprovision учетных записей пользователей Azure AD.

### <a name="assign-hello-azure-ad-test-user"></a>Назначить hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooDruva доступа.

![Назначение пользователям ролей hello][200] 

**tooassign tooDruva Britta Simon выполните следующие шаги hello.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **Druva**.

    ![ссылка Druva Hello в списке приложений hello](./media/active-directory-saas-druva-tutorial/tutorial_druva_app.png)  

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Hello ссылку «Пользователи и группы»][202]

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![область назначения, добавьте Hello][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="test-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.

При нажатии кнопки hello Druva плитки в панели доступа hello, вы должны получить приложение автоматически вошедшего tooyour Druva.
Дополнительные сведения о панели доступа см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-druva-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-druva-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-druva-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-druva-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-druva-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-druva-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-druva-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-druva-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-druva-tutorial/tutorial_general_203.png

