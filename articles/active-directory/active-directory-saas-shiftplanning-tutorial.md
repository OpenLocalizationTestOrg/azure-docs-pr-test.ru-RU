---
title: "Учебник. Интеграция Azure Active Directory с Humanity | Документы Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и человечества."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6aa771e9-31c6-48d1-8dde-024bebc06943
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: jeedes
ms.openlocfilehash: 7d8a04a2eb3c997f86f1e199c47809fa3dad60e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-humanity"></a>Учебник. Интеграция Azure Active Directory с Humanity

В этом учебнике вы узнаете, как toointegrate человечества с Azure Active Directory (Azure AD).

Интеграция с Azure AD человечества предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooHumanity
- Можно включить на пользователей tooautomatically get вошедшего tooHumanity (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с человечества требуется hello следующих элементов:

- подписка Azure AD;
- подписка Humanity с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление человечества из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-humanity-from-hello-gallery"></a>Добавление человечества из галереи hello
интеграции hello tooconfigure человечества в Azure AD, вы должны tooadd человечества из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd человечества из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Приложения][3]

4. Введите в поле поиска hello **человечества**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_search.png)

5. В панели результатов hello, выберите **сознания**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в Humanity с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в человечества является tooa в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в человечества должен установить toobe.

В человечества, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.

tooconfigure и теста Azure AD единого входа с человечества, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя человечества](#creating-a-humanity-test-user)**  -toohave аналог Саймон Britta в человечества, представление связанных toohello Azure AD пользователя.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении человечества.

**tooconfigure Azure AD единого входа с человечества, выполните следующие шаги hello.**

1. В hello в hello портала Azure **сознания** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_samlbase.png)

3. На hello **URL-адреса и домена человечества** выполните следующие шаги hello:

    ![Настройка единого входа](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_url.png)

    а. В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://company.humanity.com/includes/saml/`

    b. В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://company.humanity.com/app/`

    > [!NOTE] 
    > Эти значения приведены в качестве примера. Обновить значения hello фактический URL-адрес входа и идентификатор. Обратитесь к [группа поддержки клиента человечества](https://www.humanity.com/support/) tooget эти значения. 
 
4. На hello **сертификат подписи SAML** щелкните **сертификата (Base64)** и затем сохраните файл сертификата hello на вашем компьютере.

    ![Настройка единого входа](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_400.png)

6. На hello **конфигурации человечества** щелкните **Настройка человечества** tooopen **Настройка входа** окна. Копировать hello **SAML единого входа URL-адрес службы и URL-адрес выхода** из hello **краткий справочник.**

    ![Настройка единого входа](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_configure.png) 

7. В другом окне браузера, войдите в tooyour **человечества** сайт компании от имени администратора.

8. В меню в верхней части hello hello выберите **администратора**.
   
    ![Администратор](./media/active-directory-saas-shiftplanning-tutorial/iC786619.png "Администратор")

9. В разделе **Integration** (Интеграция) щелкните **Single Sign-On** (Единый вход).
   
    ![Единый вход](./media/active-directory-saas-shiftplanning-tutorial/iC786620.png "Единый вход")

10. В hello **Single Sign-On** выполните следующие шаги hello:
   
    ![Единый вход](./media/active-directory-saas-shiftplanning-tutorial/iC786905.png "Единый вход")
   
    а. Установите флажок **SAML включен**.

    b. Установите флажок **Allow Password Login** (Разрешить вход с паролем).

    c. Вставить hello **SAML единого входа URL-адрес службы** значение в hello **URL-адрес издателя SAML** текстового поля.

    d. Вставить hello **URL-адрес выхода** значение в hello **URL-адрес удаленного выхода** текстового поля.
   
    д. Откройте сертификат в кодировке base-64 в блокноте, hello копирования содержимого его в буфер обмена, а затем вставьте его toohello **сертификат X.509** текстового поля.

11. Нажмите кнопку **Сохранить параметры**.

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-shiftplanning-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-shiftplanning-tutorial/create_aaduser_02.png) 

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-shiftplanning-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-shiftplanning-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-a-humanity-test-user"></a>Создание тестового пользователя Humanity

В порядке tooenable toolog пользователей Azure AD в tooHumanity их необходимо подготовить в человечества. В случае hello сознания Подготовка выполняется вручную.

**tooprovision учетной записи пользователя, выполните следующие шаги hello.**

1. Войдите в tooyour **человечества** сайт компании от имени администратора.

2. Щелкните **Администратор**.
   
    ![Администратор](./media/active-directory-saas-shiftplanning-tutorial/iC786619.png "Администратор")

3. Щелкните **Персонал**.
   
    ![Персонал](./media/active-directory-saas-shiftplanning-tutorial/ic786623.png "Персонал")

4. В разделе **Действия** щелкните **Добавление сотрудников**.
   
    ![Добавить сотрудников](./media/active-directory-saas-shiftplanning-tutorial/iC786624.png "Добавить сотрудников")

5. В hello **добавить сотрудника** выполните следующие шаги hello:
   
    ![Сохранить сотрудников](./media/active-directory-saas-shiftplanning-tutorial/iC786625.png "Сохранить сотрудников")
   
    а. Тип hello **имя**, **Фамилия**, и **электронной почты** из текстовых полей, связанных с действительной учетной записи AAD, которые должны tooprovision hello.

    b. Щелкните **Сохранить сотрудников**.

>[!NOTE]
>Можно использовать любые другие человечества пользователя средства создания учетных записей или интерфейсы API, предоставляемые человечества tooprovision учетных записей пользователей AAD.

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooHumanity доступа.

![Назначение пользователя][200] 

**tooassign tooHumanity Britta Simon выполните следующие шаги hello.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **человечества**.

    ![Настройка единого входа](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.

При выборе плитки человечества hello в hello панели доступа, следует получать автоматически вошедшего tooyour человечества приложения.
Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_203.png

