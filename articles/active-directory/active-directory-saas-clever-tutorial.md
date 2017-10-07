---
title: "Учебник. Интеграция Azure Active Directory с Clever | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Clever."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 069ff13a-310e-4366-a147-d6ec5cca12a5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 24430e1e6c750efa5787561aa151201b1fe7d428
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-clever"></a>Руководство. Интеграция Azure Active Directory с Clever

В этом учебнике вы узнаете, как toointegrate Clever с Azure Active Directory (Azure AD).

Интеграция с Azure AD Clever предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooClever.
- Можно включить на пользователей tooautomatically get вошедшего tooClever (Single Sign-On) с помощью своих учетных записей Azure AD.
- Вы можете управлять учетными записями в одном централизованном месте - hello портал Azure.

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с Clever требуется hello следующих элементов:

- подписка Azure AD;
- подписка Clever с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление Clever из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-clever-from-hello-gallery"></a>Добавление Clever из галереи hello
tooconfigure hello интеграции Clever в Azure AD, вы должны tooadd Clever из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd Clever из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Кнопка Hello Azure Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Hello корпоративных приложений колонку][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Кнопка нового приложения Hello][3]

4. Введите в поле поиска hello **Clever**выберите **Clever** из панели результатов щелкните **добавить** кнопку tooadd приложения hello.

    ![В списке результатов hello некий](./media/active-directory-saas-clever-tutorial/tutorial_clever_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD

В этом разделе описана настройка и проверка единого входа Azure AD в Clever с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Clever является tooa в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в Clever должен установить toobe.

В Clever, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.

tooconfigure и теста Azure AD единого входа с Clever, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание некий тестового пользователя](#create-a-clever-test-user)**  -toohave аналог Саймон Britta в Clever, который представляет связанный toohello Azure AD пользователя.
4. **[Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#test-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configure-azure-ad-single-sign-on"></a>Настройка единого входа Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении некий.

**tooconfigure Azure AD единого входа с Clever, выполните следующие шаги hello.**

1. В hello в hello портала Azure **Clever** странице интеграции приложения щелкните **единого входа**.

    ![Ссылка "Настройка единого входа"][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-clever-tutorial/tutorial_clever_samlbase.png)

3. На hello **URL-адреса и домена некий** выполните следующие шаги hello:

    ![Сведения о домене и URL-адресах единого входа для приложения Clever](./media/active-directory-saas-clever-tutorial/tutorial_clever_url.png)

    а. В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://clever.com/in/<companyname>`

    b. В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://clever.com/<companyname>`

    > [!NOTE] 
    > Эти значения приведены в качестве примера. Обновить значения hello фактический URL-адрес входа и идентификатор. Обратитесь к [группа поддержки некий клиента](https://clever.com/about/contact/) tooget эти значения.

4. На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.

    ![ссылку для скачивания сертификата Hello](./media/active-directory-saas-clever-tutorial/tutorial_clever_certificate.png)

5. Hello некий приложения ожидает утверждения SAML hello в определенном формате, требующий tooadd настраиваемого атрибута сопоставления tooyour **атрибутов токена SAML** конфигурации.

    пример Hello следующий снимок экрана для этого.

    ![Настройка единого входа](./media/active-directory-saas-clever-tutorial/tutorial_clever_07.png) 

6. В hello **атрибуты пользователя** раздела, посвященного hello **единого входа** диалогового окна, настроить атрибутов токена SAML, как показано в приведенном выше рисунке hello и выполнять hello следующие шаги:
    
    | Имя атрибута  | Значение атрибута |
    | --------------- | -------------------- |    
    | clever.student.credentials.district\_username  | user.userprincipalname |
    | Firstname  | user.givenname |
    | Lastname  | user.surname |    

    а. Нажмите кнопку **добавить атрибут** tooopen hello **Добавление атрибута** диалогового окна.

    ![Настройка единого входа](./media/active-directory-saas-clever-tutorial/tutorial_attribute_04.png)
    
    ![Настройка единого входа](./media/active-directory-saas-clever-tutorial/tutorial_attribute_05.png)
    
    b. В hello **имя** в текстовое поле имя атрибута типа hello, показанный для этой строки.

    c. Из hello **значение** списка значение атрибута типа hello, показанный для этой строки.

    d. Оставьте hello **имен** пустое текстовое поле.
    
    d. Нажмите кнопку **ОК**.     

5. Нажмите кнопку **Сохранить** .

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-clever-tutorial/tutorial_general_400.png)

8. toogenerate hello **метаданные** URL-адрес, выполните следующие шаги hello:

    а. Щелкните **Регистрация приложений**.
    
    ![Настройка единого входа](./media/active-directory-saas-clever-tutorial/tutorial_clever_appregistrations.png)
   
    b. Нажмите кнопку **конечные точки** tooopen **конечные точки** диалоговое окно.  
    
    ![Настройка единого входа](./media/active-directory-saas-clever-tutorial/tutorial_clever_endpointicon.png)

    c. Нажмите кнопку toocopy hello копирования **документа МЕТАДАННЫХ ФЕДЕРАЦИИ** URL-адрес и вставьте его в Блокнот.
    
    ![Настройка единого входа](./media/active-directory-saas-clever-tutorial/tutorial_clever_endpoint.png)
     
    d. Теперь перейдите на странице свойств toohello **Clever** и копирования hello **идентификатор приложения** с помощью **копирования** кнопку и вставьте его в Блокнот.
 
    ![Настройка единого входа](./media/active-directory-saas-clever-tutorial/tutorial_clever_appid.png)

    д. Создать hello **URL-адрес метаданных** с помощью hello следующий шаблон:`<FEDERATION METADATA DOCUMENT url>?appid=<application id>`   

9. В другом окне браузера войдите в tooyour некий корпоративный сайт в качестве администратора.

10. Щелкните hello панели инструментов **мгновенный вход**.

    ![Мгновенный вход](./media/active-directory-saas-clever-tutorial/ic798984.png "Мгновенный вход")

11. На hello **мгновенный вход** выполните следующие шаги hello:
      
      ![Мгновенный вход](./media/active-directory-saas-clever-tutorial/ic798985.png "Мгновенный вход")
      
      а. Тип hello **URL-адрес входа**.
      
      >[!NOTE]
      >Hello **URL-адрес входа** является пользовательским значением. Обратитесь к [группа поддержки некий клиента](https://clever.com/about/contact/) tooget это значение.
      
      b. Для параметра **Identity System** (Система идентификации) выберите значение **ADFS**.

      c. Тип hello **URL-адрес метаданных** в hello **URL-адрес метаданных** текстового поля.
      
      d. Щелкните **Сохранить**.

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD

Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

   ![Создание тестового пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello hello левой панели портала Azure щелкните hello **Azure Active Directory** кнопки.

    ![Кнопка Hello Azure Active Directory](./media/active-directory-saas-clever-tutorial/create_aaduser_01.png)

2. слишком go toodisplay hello список пользователей,**пользователей и групп**, а затем нажмите кнопку **всех пользователей**.

    ![Здравствуйте, «Пользователи и группы» и «Все пользователи» ссылки](./media/active-directory-saas-clever-tutorial/create_aaduser_02.png)

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** вверху hello hello **всех пользователей** диалоговое окно.

    ![Кнопка "Добавить" Hello](./media/active-directory-saas-clever-tutorial/create_aaduser_03.png)

4. В hello **пользователя** диалогового окна выполните следующие шаги hello:

    ![диалоговое окно приветствия пользователя](./media/active-directory-saas-clever-tutorial/create_aaduser_04.png)

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** поле типа hello адрес электронной почты пользователя Саймон Britta.

    c. Выберите hello **Показать пароль** флажок и запишите значение hello, отображаемый в hello **пароль** поле.

    d. Щелкните **Создать**.
 
### <a name="create-a-clever-test-user"></a>Создание тестового пользователя Clever

Пользователи toolog tooenable Azure AD в tooClever, их необходимо подготовить в Clever.

В случае Clever, работать с [группа поддержки некий клиента](https://clever.com/about/contact/) для добавления пользователей hello hello некий платформы. Перед использованием единого входа необходимо создать и активировать пользователей. 

>[!NOTE]
>Можно использовать любые другие некий пользователя средства создания учетных записей или интерфейсы API, предоставляемые некий tooprovision учетных записей пользователей Azure AD.

### <a name="assign-hello-azure-ad-test-user"></a>Назначить hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooClever доступа.

![Назначение пользователям ролей hello][200] 

**tooassign tooClever Britta Simon выполните следующие шаги hello.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **Clever**.

    ![Hello Clever ссылку в списке приложений hello](./media/active-directory-saas-clever-tutorial/tutorial_clever_app.png)  

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Hello ссылку «Пользователи и группы»][202]

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![область назначения, добавьте Hello][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="test-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.

При нажатии кнопки hello некий плитки в Здравствуйте панели доступа, вы должны получить автоматически вошедшего tooyour некий приложения.
Дополнительные сведения о панели доступа см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-clever-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-clever-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-clever-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-clever-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-clever-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-clever-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-clever-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-clever-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-clever-tutorial/tutorial_general_203.png

