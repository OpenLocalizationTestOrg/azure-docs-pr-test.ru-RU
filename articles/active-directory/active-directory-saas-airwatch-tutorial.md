---
title: "Руководство. Интеграция Azure Active Directory с AirWatch | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и AirWatch."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 96a3bb1c-96c6-40dc-8ea0-060b0c2a62e5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: e5230d5a36824778a4d9804dadf9f13a0d11a68d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-airwatch"></a>Руководство. Интеграция Azure Active Directory с AirWatch

В этом учебнике вы узнаете, как toointegrate AirWatch с Azure Active Directory (Azure AD).

Интеграция AirWatch с Azure AD предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooAirWatch
- Можно включить на пользователей tooautomatically get вошедшего tooAirWatch (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с AirWatch требуется hello следующих элементов:

- подписка Azure AD;
- подписка AirWatch с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление AirWatch из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-airwatch-from-hello-gallery"></a>Добавление AirWatch из галереи hello
tooconfigure hello интеграции AirWatch в Azure AD, вы должны tooadd AirWatch от hello коллекции tooyour список управляемых приложений SaaS.

**tooadd AirWatch из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Приложения][3]

4. Введите в поле поиска hello **AirWatch**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_search.png)

5. В панели результатов hello выберите **AirWatch**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в приложение AirWatch с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в AirWatch является tooa в Azure AD. Другими словами связи между пользователя Azure AD и hello связанных пользователей в AirWatch должен установить toobe.

Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в AirWatch.

tooconfigure и теста Azure AD единого входа с AirWatch, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя AirWatch](#creating-a-airwatch-test-user)**  -toohave аналог Саймон Britta в AirWatch, который представляет связанный toohello Azure AD пользователя.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложение AirWatch.

**tooconfigure Azure AD единого входа с AirWatch, выполните следующие шаги hello.**

1. В hello в hello портала Azure **AirWatch** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_samlbase.png)

3. На hello **URL-адреса и домена AirWatch** выполните следующие шаги hello:

    ![Настройка единого входа](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_url.png)

    а. В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<subdomain>.awmdm.com/AirWatch/Login?gid=companycode`

    b. В hello **идентификатор** текстовое поле, значение типа hello как`AirWatch`

    > [!NOTE] 
    > Это значение не реальными hello. Измените значение этого параметра hello фактический URL-адрес входа. Обратитесь к [группа поддержки клиента AirWatch](http://www.air-watch.com/company/contact-us/) tooget это значение. 
 
4. На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и сохраните hello XML-файл на компьютере.

    ![Настройка единого входа](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_certificate.png) 

5. На hello **конфигурации AirWatch** щелкните **Настройка AirWatch** tooopen **Настройка входа** окна. Копировать hello **SAML единого входа URL-адрес службы** из hello **краткий справочник.**

    ![Настройка единого входа](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_configure.png) 

6. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-airwatch-tutorial/tutorial_general_400.png)
<CS>
7. В другом окне браузера Войдите на сайте компании AirWatch tooyour в качестве администратора.

8. Hello панели навигации слева щелкните **учетные записи**, а затем нажмите кнопку **Администраторы**.
   
   ![Администраторы](./media/active-directory-saas-airwatch-tutorial/ic791920.png "Администраторы")

9. Разверните hello **параметры** меню, а затем нажмите **службы каталогов**.
   
   ![Параметры](./media/active-directory-saas-airwatch-tutorial/ic791921.png "Параметры")

10. Нажмите кнопку hello **пользователя** hello на вкладке **базовое DN** текстовом поле введите имя домена и нажмите кнопку **Сохранить**.
   
   ![Пользователь](./media/active-directory-saas-airwatch-tutorial/ic791922.png "Пользователь")

11. Нажмите кнопку hello **сервера** вкладки.
   
   ![Сервер](./media/active-directory-saas-airwatch-tutorial/ic791923.png "Сервер")

12. Выполните следующие шаги hello.
    
    ![Передача](./media/active-directory-saas-airwatch-tutorial/ic791924.png "Передача")   
    
    а. Для параметра **Directory Type** (Тип каталога) выберите значение **None** (Нет).

    b. Установите флажок **Use SAML For Authentication**(Использовать SAML для проверки подлинности).

    c. tooupload Здравствуйте Скачанный сертификат, нажмите кнопку **отправить**.

13. В hello **запроса** выполните следующие шаги hello:
    
    ![Запрос](./media/active-directory-saas-airwatch-tutorial/ic791925.png "Запрос")  

    а. Для параметра **Request Binding Type** (Тип привязки запроса) выберите значение **POST**.

    b. В hello в hello портала Azure **настройки единого входа в Airwatch** странице диалогового окна, hello копирования **SAML единого входа URL-адрес службы** значение, а затем вставьте его в hello **поставщика удостоверений Один на URL-адрес входа** текстового поля.

    c. Для параметра **NameID Format** (Формат идентификатора имени) выберите значение **Email Address** (Адрес электронной почты).

    г) Щелкните **Сохранить**.

14. Нажмите кнопку hello **пользователя** вкладку еще раз.
    
    ![Пользователь](./media/active-directory-saas-airwatch-tutorial/ic791926.png "Пользователь")

15. В hello **атрибута** выполните следующие шаги hello:
    
    ![Атрибут](./media/active-directory-saas-airwatch-tutorial/ic791927.png "Атрибут")

    а. В hello **идентификатор объекта** введите **http://schemas.microsoft.com/identity/claims/objectidentifier**.

    b. В hello **Username** введите **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.

    c. В hello **отображаемое имя** введите **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.

    d. В hello **имя** введите **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.

    д. В hello **Фамилия** введите **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**.

    f. В hello **электронной почты** введите **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.

    ж. Щелкните **Сохранить**.

<CE>

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-airwatch-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-airwatch-tutorial/create_aaduser_02.png) 

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-airwatch-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-airwatch-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из Саймон Britta.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-a-airwatch-test-user"></a>Создание тестового пользователя AirWatch

Пользователи toolog tooenable Azure AD в tooAirWatch, их необходимо подготовить в tooAirWatch.

* Подготовка в AirWatch выполняется вручную.

**tooprovision учетной записи пользователя, выполните следующие шаги hello.**

1. Войдите в tooyour **AirWatch** сайт компании от имени администратора.
2. Hello hello левой панели навигации щелкните **учетные записи**, а затем нажмите кнопку **пользователей**.
   
   ![Пользователи](./media/active-directory-saas-airwatch-tutorial/ic791929.png "Пользователи")
3. В hello **пользователей** меню, нажмите кнопку **представление списка**, а затем нажмите кнопку **добавить \> добавить пользователя**.
   
   ![Добавление пользователя](./media/active-directory-saas-airwatch-tutorial/ic791930.png "Добавление пользователя")
4. На hello **Добавление и изменение пользователей** диалоговое окно, выполните следующие шаги hello:

   ![Добавление пользователя](./media/active-directory-saas-airwatch-tutorial/ic791931.png "Добавление пользователя")   
   1. Тип hello **Username**, **пароль**, **подтверждение пароля**, **имя**, **Фамилия**,  **Адрес электронной почты** из допустимых Azure связанные с учетной записью Active Directory требуется tooprovision в hello текстовые поля.
   2. Щелкните **Сохранить**.

>[!NOTE]
>Можно использовать любые другие AirWatch пользователя средства создания учетных записей или интерфейсы API, предоставляемые AirWatch tooprovision учетных записей пользователей AAD.
>  

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooAirWatch доступа.

![Назначение пользователя][200] 

**tooassign tooAirWatch Britta Simon выполните следующие шаги hello.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **AirWatch**.

    ![Настройка единого входа](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.

Tootest параметры единого входа, откройте панель доступа hello. Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).


## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_203.png

