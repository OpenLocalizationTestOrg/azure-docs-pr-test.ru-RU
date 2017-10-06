---
title: "Руководство по интеграции Azure Active Directory с Veracode | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Veracode."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 4fe78050-cb6d-4db9-96ec-58cc0779167f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: d17307b3864b7df8ee55f569d8f962e2e315b936
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-veracode"></a>Руководство. Интеграция Azure Active Directory с Veracode

В этом учебнике вы узнаете, как toointegrate Veracode с Azure Active Directory (Azure AD).

Интеграция с Azure AD Veracode предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooVeracode.
- Можно включить на пользователей tooautomatically get вошедшего tooVeracode (Single Sign-On) с помощью своих учетных записей Azure AD.
- Вы можете управлять учетными записями в одном централизованном месте - hello портал Azure.

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с Veracode требуется hello следующих элементов:

- подписка Azure AD;
- Подписка Veracode с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление Veracode из коллекции hello
2. Настройка и проверка единого входа в Azure AD

## <a name="add-veracode-from-hello-gallery"></a>Добавление Veracode из коллекции hello
tooconfigure hello интеграции Veracode в Azure AD, вы должны tooadd Veracode из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd Veracode из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Кнопка Hello Azure Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Hello корпоративных приложений колонку][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Кнопка нового приложения Hello][3]

4. Введите в поле поиска hello **Veracode**выберите **Veracode** из панели результатов щелкните **добавить** кнопку tooadd приложения hello.

    ![Veracode в списке результатов hello](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD

В этом разделе описана настройка и проверка единого входа Azure AD в приложение Veracode с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Veracode является tooa в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в Veracode должен установить toobe.

В Veracode, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.

tooconfigure и теста Azure AD единого входа с Veracode, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя Veracode](#create-a-veracode-test-user)**  -toohave аналог Саймон Britta в Veracode, который представляет связанный toohello Azure AD пользователя.
4. **[Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#test-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configure-azure-ad-single-sign-on"></a>Настройка единого входа Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Veracode.

**Azure AD tooconfigure единого входа с Veracode, выполните следующие шаги hello.**

1. В hello в hello портала Azure **Veracode** странице интеграции приложения щелкните **единого входа**.

    ![Ссылка "Настройка единого входа"][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_samlbase.png)

3. На hello **URL-адреса и домена Veracode** раздела, пользователь не имеет tooperform все меры как приложение hello уже заранее интегрировано с Azure. 

    ![Настройка единого входа](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_url.png)

4. На hello **сертификат подписи SAML** щелкните **сертификата (Base64)** и затем сохраните файл сертификата hello на вашем компьютере.

    ![ссылку для скачивания сертификата Hello](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_certificate.png) 

5. Цель этого раздела Hello — toooutline как tooVeracode tooauthenticate tooenable пользователей с учетной записью в Azure AD, используя федерацию на основе hello SAML протокола.

    Приложение Veracode ожидает утверждения SAML hello в определенном формате, требующий tooadd настраиваемого атрибута сопоставления tooyour **атрибутов токена saml** конфигурации. пример Hello следующий снимок экрана для этого.
    
    ![Атрибуты](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_attr.png "Атрибуты")

6. сопоставления атрибутов hello необходимые tooadd, выполните hello следующие шаги.

    | Имя атрибута | Значение атрибута |
    |--- |--- |
    | firstname |User.givenname |
    | lastname |User.surname |
    | email |User.mail |
    
    а. Для каждой строки данных в таблице hello выше, щелкните **добавить атрибут пользователя**.
    
    ![Атрибуты](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addattr.png "Атрибуты")
    
    ![Атрибуты](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_addattr1.png "Атрибуты")
    
    b. В hello **имя атрибута** в текстовое поле имя атрибута типа hello, показанный для этой строки.
    
    c. В hello **значение атрибута** текстовое поле, значение атрибута выберите hello, показанный для этой строки.
    
    d. Нажмите кнопку **ОК**.

7. Нажмите кнопку **Сохранить** .

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-veracode-tutorial/tutorial_general_400.png)

8. На hello **конфигурации Veracode** щелкните **Настройка Veracode** tooopen **Настройка входа** окна. Копировать hello **идентификатор сущности SAML** из hello **краткий справочник.**

    ![Конфигурация Veracode](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_configure.png) 

9. В другом окне веб-браузера войдите на веб-сайт Veracode вашей компании в качестве администратора.

10. В меню в верхней части hello hello выберите **параметры**и нажмите кнопку **администратора**.
   
    ![Администрирование](./media/active-directory-saas-veracode-tutorial/ic802911.png "Администрирование")

11. Нажмите кнопку hello **SAML** вкладки.

12. В hello **параметры SAML организации** выполните следующие шаги hello:
   
    ![Администрирование](./media/active-directory-saas-veracode-tutorial/ic802912.png "Администрирование")
   
    а.  В **издателя** текстовое значение hello вставить **идентификатор сущности SAML** скопирован из портала Azure.
    
    b. щелкните загруженный сертификат из портала Azure tooupload **выбрать файл**.
   
    c. Выберите параметр **Включить саморегистрацию**.

13. В hello **параметры регистрации Self** статьи, выполните следующие шаги hello и нажмите кнопку **Сохранить**:
   
    ![Администрирование](./media/active-directory-saas-veracode-tutorial/ic802913.png "Администрирование")
   
    а. Для параметра **New User Activation** (Активация нового пользователя) выберите значение **No Activation Required** (Активация не требуется).
   
    b. Для параметра **User Data Updates** (Обновления пользовательских данных) выберите значение **Preference Veracode User Data** (Предпочтение пользовательских данных Veracode).
   
    c. Для **сведений об атрибутах SAML**, выберите hello следующее:
      * **роли пользователей;**
      * **администратор политики;**
      * **рецензент;**
      * **руководитель безопасности;**
      * **руководитель;**
      * **отправитель;**
      * **создатель;**
      * **все типы проверки;**
      * **участие в группе;**
      * **группа по умолчанию.**

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD

Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

   ![Создание тестового пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello hello левой панели портала Azure щелкните hello **Azure Active Directory** кнопки.

    ![Кнопка Hello Azure Active Directory](./media/active-directory-saas-veracode-tutorial/create_aaduser_01.png)

2. слишком go toodisplay hello список пользователей,**пользователей и групп**, а затем нажмите кнопку **всех пользователей**.

    ![Здравствуйте, «Пользователи и группы» и «Все пользователи» ссылки](./media/active-directory-saas-veracode-tutorial/create_aaduser_02.png)

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** вверху hello hello **всех пользователей** диалоговое окно.

    ![Кнопка "Добавить" Hello](./media/active-directory-saas-veracode-tutorial/create_aaduser_03.png)

4. В hello **пользователя** диалогового окна выполните следующие шаги hello:

    ![диалоговое окно приветствия пользователя](./media/active-directory-saas-veracode-tutorial/create_aaduser_04.png)

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** поле типа hello адрес электронной почты пользователя Саймон Britta.

    c. Выберите hello **Показать пароль** флажок и запишите значение hello, отображаемый в hello **пароль** поле.

    d. Щелкните **Создать**.
 
### <a name="create-a-veracode-test-user"></a>Создание тестового пользователя Veracode
В порядке tooenable toolog пользователей Azure AD в Veracode их необходимо подготовить в Veracode. В случае Veracode hello Подготовка — это автоматизированная задача. С вашей стороны никакие действия не требуются. Пользователи создаются автоматически при необходимости hello первой единого входа попытки.

> [!NOTE]
> Можно использовать любые другие Veracode пользователя средства создания учетных записей или интерфейсы API, предоставляемые Veracode tooprovision учетных записей пользователей Azure AD.
> 

### <a name="assign-hello-azure-ad-test-user"></a>Назначить hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooVeracode доступа.

![Назначение пользователям ролей hello][200] 

**tooassign tooVeracode Britta Simon выполните следующие шаги hello.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **Veracode**.

    ![ссылка Veracode Hello в списке приложений hello](./media/active-directory-saas-veracode-tutorial/tutorial_veracode_app.png)  

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Hello ссылку «Пользователи и группы»][202]

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![область назначения, добавьте Hello][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="test-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.

При нажатии кнопки hello Veracode плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour Veracode приложения.
Дополнительные сведения о панели доступа см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-veracode-tutorial/tutorial_general_203.png

