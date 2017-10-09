---
title: "Руководство по интеграции Azure Active Directory с Adaptive Suite | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и адаптивной Suite."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 13af9d00-116a-41b8-8ca0-4870b31e224c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: af309c27ab74098c1e229c80adb11c96dc2774fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adaptive-suite"></a>Руководство. Интеграция Azure Active Directory с Adaptive Suite

В этом учебнике вы узнаете, как toointegrate адаптивной Suite с Azure Active Directory (Azure AD).

Интеграция с Azure AD адаптивной Suite предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooAdaptive Suite
- Можно включить на пользователей tooautomatically get вошедшего tooAdaptive набора (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с адаптивной Suite необходимо hello следующих элементов:

- подписка Azure AD;
- подписка Adaptive Suite с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление адаптивной набор из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-adaptive-suite-from-hello-gallery"></a>Добавление адаптивной набор из галереи hello
tooconfigure hello интеграции адаптивной Suite в Azure AD, вы должны tooadd адаптивной набор из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd адаптивной набор из галереи hello выполните hello следующие шаги.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Приложения][3]

4. Введите в поле поиска hello **адаптивной Suite**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_search.png)

5. В панели результатов hello выберите **адаптивной Suite**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в приложение Adaptive Suite с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в адаптивной Suite является tooa в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в адаптивной Suite должен установить toobe.

Адаптивная пакета, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.

tooconfigure и теста Azure AD единого входа с адаптивной Suite, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя, прошедшего адаптивной Suite](#creating-an-adaptive-suite-test-user)**  -toohave аналог Саймон Britta адаптивной набора, представление связанных toohello Azure AD пользователя.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении адаптивной Suite.

**tooconfigure Azure AD единого входа с адаптивной Suite выполните следующие шаги hello.**

1. В hello в hello портала Azure **адаптивной Suite** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_samlbase.png)

3. На hello **URL-адреса и домена адаптивной Suite** выполните следующие шаги hello:

    ![Настройка единого входа](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_url.png)

    В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://login.adaptiveinsights.com:443/samlsso/<unique-id>`

    >[!NOTE]
    > Это значение можно получить из hello адаптивной Suite **настройки единого входа SAML** страницы.
    >  

4. На hello **сертификат подписи SAML** щелкните **сертификата (Base64)** и затем сохраните файл сертификата hello на вашем компьютере.

    ![Настройка единого входа](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_400.png)

6. На hello **адаптивной настройку пакета** щелкните **настройки адаптивной Suite** tooopen **Настройка входа** окна. Копировать hello **идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**

    ![Настройка единого входа](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_configure.png) 

7. В другом окне браузера Войдите на сайте компании tooyour адаптивной Suite в качестве администратора.

8. Go слишком**администратора**.
   
    ![Администратор](./media/active-directory-saas-adaptivesuite-tutorial/IC805644.png "Администратор")

9. В hello **пользователям и ролям** щелкните **Управление параметрами единого входа SAML**.
   
    ![Управление параметрами единого входа SAML](./media/active-directory-saas-adaptivesuite-tutorial/IC805645.png "Управление параметрами единого входа SAML")

10. На hello **настройки единого входа SAML** выполните следующие шаги hello:
   
    ![Параметры единого входа SAML](./media/active-directory-saas-adaptivesuite-tutorial/IC805646.png "Параметры единого входа SAML")

    а. В hello **имя поставщика удостоверений** текстовом поле введите имя для конфигурации.
    
    b. Вставить hello **идентификатор сущности SAML** значение копируется из портала Azure hello **поставщика удостоверений идентификатор сущности** текстового поля.
  
    c. Вставить hello **SAML единого входа URL-адрес службы** значение копируется из портала Azure hello **поставщика удостоверений URL-адрес SSO** текстового поля.
  
    d. Вставить hello **SAML единого входа URL-адрес службы** значение копируется из портала Azure hello **URL-адрес выхода Custom** текстового поля.
  
    д. tooupload загруженный сертификат, нажмите кнопку **выбрать файл**.
  
    f. Выберите следующие hello для:
    * Для параметра **SAML user id** (Идентификатор пользователя SAML) выберите значение **User’s Adaptive Insights user name** (Имя пользователя Adaptive Insights).
    * Для параметра **SAML user id location** (Расположение идентификатора пользователя SAML) выберите значение **User id in NameID of Subject** (Идентификатор пользователя из NameID в Subject).
    * Для параметра **SAML NameID format** (Формат NameID SAML) выберите значение **Адрес электронной почты**.
    * Для параметра **Включить SAML** выберите значение **Allow SAML SSO and direct Adaptive Insights login** (Разрешить единый вход SAML и прямой вход Adaptive Insights).
    
    g. Щелкните **Сохранить**.

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_02.png) 

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-an-adaptive-suite-test-user"></a>Создание тестового пользователя Adaptive Suite

Пользователи toolog tooenable Azure AD в tooAdaptive Suite, их необходимо подготовить в адаптивной набор.  

* В случае hello адаптивной набора Подготовка выполняется вручную.

**tooconfigure подготовки пользователей, выполните следующие шаги hello.** 

1. Войдите в tooyour **адаптивной Suite** сайт компании от имени администратора.
2. Go слишком**администратора**.
   
   ![Администратор](./media/active-directory-saas-adaptivesuite-tutorial/IC805644.png "Администратор")
3. В hello **пользователям и ролям** щелкните **добавить пользователя**.
   
   ![Добавление пользователя](./media/active-directory-saas-adaptivesuite-tutorial/IC805648.png "Добавление пользователя")
4. В hello **нового пользователя** выполните следующие шаги hello:
   
   ![Отправка](./media/active-directory-saas-adaptivesuite-tutorial/IC805649.png "Отправка")   

   а. Тип hello **имя**, **входа**, **электронной почты**, **пароль** действительного пользователя Azure Active Directory требуется tooprovision в связанных hello текстовые поля.
  
   b. Выберите **Роль**.
  
   c. Нажмите кнопку **Submit**(Отправить).

>[!NOTE]
>Можно использовать любые другие адаптивной Suite пользователя средства создания учетных записей или интерфейсы API, предоставляемые tooprovision адаптивной набора учетных записей пользователей AAD.
>  

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooAdaptive Suite.

![Назначение пользователя][200] 

**tooassign tooAdaptive Britta Simon Suite, выполните hello следующие шаги.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **адаптивной Suite**.

    ![Настройка единого входа](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

Цель этого раздела Hello является tootest к Microsoft Azure AD Single Sign-On конфигурации с помощью панели доступа "hello".

При выборе плитки адаптивной Suite hello в hello панели доступа, вы должны получить tooyour автоматически вошедшего адаптивной набора приложений.


## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_203.png

