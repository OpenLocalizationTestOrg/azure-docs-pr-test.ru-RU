---
title: "Руководство по интеграции Azure Active Directory с ThirdLight | Документы Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и ThirdLight."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 168aae9a-54ee-4c2b-ab12-650a2c62b901
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: a510e514f6a8c4e89220b9a6f6db29668b451b61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-thirdlight"></a>Учебник. Интеграция Azure Active Directory с ThirdLight

В этом учебнике вы узнаете, как toointegrate ThirdLight с Azure Active Directory (Azure AD).

Интеграция с Azure AD ThirdLight предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooThirdLight
- Можно включить на пользователей tooautomatically get вошедшего tooThirdLight (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с ThirdLight требуется hello следующих элементов:

- подписка Azure AD;
- подписка ThirdLight с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление ThirdLight из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-thirdlight-from-hello-gallery"></a>Добавление ThirdLight из галереи hello
tooconfigure hello интеграции ThirdLight в Azure AD, вы должны tooadd ThirdLight из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd ThirdLight из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Приложения][3]

4. Введите в поле поиска hello **ThirdLight**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-thirdlight-tutorial/tutorial_thirdlight_search.png)

5. В панели результатов hello выберите **ThirdLight**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-thirdlight-tutorial/tutorial_thirdlight_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в ThirdLight с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в ThirdLight является tooa в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в ThirdLight должен установить toobe.

Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в ThirdLight.

tooconfigure и теста Azure AD единого входа с ThirdLight, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя ThirdLight](#creating-a-thirdlight-test-user)**  -toohave аналог Саймон Britta в ThirdLight, который представляет связанный toohello Azure AD пользователя.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении ThirdLight.

**tooconfigure Azure AD единого входа с ThirdLight, выполните следующие шаги hello.**

1. В hello в hello портала Azure **ThirdLight** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-thirdlight-tutorial/tutorial_thirdlight_samlbase.png)

3. На hello **URL-адреса и домена ThirdLight** выполните следующие шаги hello:

    ![Настройка единого входа](./media/active-directory-saas-thirdlight-tutorial/tutorial_thirdlight_url.png)

    а. В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<subdomain>.thirdlight.com/`

    b. В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<subdomain>.thirdlight.com/saml/sp`

    > [!NOTE] 
    > Эти значения приведены в качестве примера. Обновить значения hello фактический URL-адрес входа и Identiifer. Обратитесь к [группа поддержки клиента ThirdLight](https://www.thirdlight.com/support) tooget эти значения. 
 
4. На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и сохраните hello XML-файл на компьютере.

    ![Настройка единого входа](./media/active-directory-saas-thirdlight-tutorial/tutorial_thirdlight_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-thirdlight-tutorial/tutorial_general_400.png)

6. В другом окне браузера Войдите на сайте компании ThirdLight tooyour в качестве администратора.

7. Go слишком**конфигурации \> системное администрирование**, а затем нажмите кнопку **SAML2**.
   
    ![Администрирование системы](./media/active-directory-saas-thirdlight-tutorial/ic805843.png "Администрирование системы")

8. В разделе "Конфигурация" hello SAML2 выполните следующие шаги hello.
   
    ![Единый вход SAML](./media/active-directory-saas-thirdlight-tutorial/ic805844.png "Единый вход SAML")   

     а. Выберите параметр **Разрешить единый вход SAML2**.
 
     b. В качестве **источника для метаданных IdP** выберите **Load IdP Metadata from XML** (Загрузить метаданные IdP из XML).
 
     c. Откройте файл метаданных загружаются hello, скопируйте содержимое hello и вставьте его в hello **XML метаданных поставщика удостоверений** текстового поля. 
     
     d. Щелкните **Сохранить параметры SAML2**.

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-thirdlight-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-thirdlight-tutorial/create_aaduser_02.png) 

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-thirdlight-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-thirdlight-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из Саймон Britta.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-a-thirdlight-test-user"></a>Создание тестового пользователя ThirdLight

Пользователи toolog tooenable Azure AD в tooThirdLight, их необходимо подготовить в ThirdLight.  
В случае ThirdLight hello Подготовка выполняется вручную.

**tooprovision учетной записи пользователя, выполните следующие шаги hello.**

1. Войдите в tooyour **ThirdLight** сайт компании от имени администратора.

2. Go слишком**пользователей** вкладки.

3. Выберите пункт **Пользователи и группы**.

4. Щелкните **Добавить пользователя** .

5. Введите **hello имя пользователя, имя или описание, электронной почте, выберите стиль или группу новых членов** действительной учетной записи AAD, вы хотите tooprovision.

6. Щелкните **Создать**.

>[!NOTE]
>Можно использовать любые другие Thirdlight пользователя средства создания учетных записей или интерфейсы API, предоставляемые Thirdlight tooprovision учетных записей пользователей AAD. 

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooThirdLight доступа.

![Назначение пользователя][200] 

**tooassign tooThirdLight Britta Simon выполните следующие шаги hello.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **ThirdLight**.

    ![Настройка единого входа](./media/active-directory-saas-thirdlight-tutorial/tutorial_thirdlight_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.

При нажатии кнопки hello ThirdLight плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour ThirdLight приложения.
Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_203.png

