---
title: "Руководство по интеграции Azure Active Directory с Zendesk | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Zendesk."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9d7c91e5-78f5-4016-862f-0f3242b00680
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 46ccd57a4adeb810af459caaa1e592cf2b62cb8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zendesk"></a>Руководство. Интеграция Azure Active Directory с Zendesk

В этом учебнике вы узнаете, как toointegrate Zendesk с Azure Active Directory (Azure AD).

Интеграция Zendesk с Azure AD предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooZendesk
- Можно включить на пользователей tooautomatically get вошедшего tooZendesk (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с Zendesk требуется hello следующих элементов:

- подписка Azure AD;
- подписка Zendesk с поддержкой единого входа.


> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.


tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).


## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление Zendesk из галереи hello
2. Настройка и проверка единого входа в Azure AD


## <a name="adding-zendesk-from-hello-gallery"></a>Добавление Zendesk из галереи hello
tooconfigure hello интеграции Zendesk в Azure AD, вы должны tooadd Zendesk из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd Zendesk из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портала Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. Нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна "hello".

    ![Приложения][3]

4. Введите в поле поиска hello **Zendesk**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_search.png)

5. В панели результатов hello выберите **Zendesk**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в приложение Zendesk с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователя аналог hello в Zendesk — tooa пользователя в Azure AD. Другими словами связи между пользователя Azure AD и hello связанных пользователей в Zendesk должен установить toobe.

Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в Zendesk.

tooconfigure и теста Azure AD единого входа с Zendesk, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя Zendesk](#creating-a-zendesk-test-user)**  -toohave аналог Саймон Britta в Zendesk, который представляет связанный toohello Azure AD пользователя.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Zendesk.

**tooconfigure Azure AD единого входа с помощью Zendesk, выполните следующие шаги hello.**

1. В hello в hello портала Azure **Zendesk** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_samlbase.png)

3. На hello **URL-адреса и домена Zendesk** выполните следующие шаги hello:

    ![Настройка единого входа](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_url.png)

    а. В hello **URL-адрес входа** текстовое значение hello типа, используя следующий шаблон hello:`https://<subdomain>.zendesk.com`

    b. В hello **идентификатор** текстовое значение hello типа, используя следующий шаблон hello:`https://<subdomain>.zendesk.com`

    > [!NOTE] 
    > Эти значения приведены в качестве примера. Обновите эти значения с hello фактический URL-адрес входа и URL-адрес идентификатора. Обратитесь к [группа поддержки Zendesk](https://support.zendesk.com/hc/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise) tooget эти значения. 

4. Zendesk ожидает утверждения SAML hello в определенном формате. Отсутствуют обязательные атрибуты SAML, но при необходимости можно добавить атрибут из **атрибуты пользователя** раздел по hello следующие шаги, описанные ниже: 

     ![Настройка единого входа](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_attributes1.png)

    а. Нажмите кнопку hello **Просмотр и изменение hello другие атрибуты** флажок.
     
    ![Настройка единого входа](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_attributes2.png)
   
    b. Нажмите кнопку hello **Добавление атрибута** tooopen **добавить атрибут** диалогового окна.
    
    ![Настройка единого входа](./media/active-directory-saas-zendesk-tutorial/tutorial_attribute_05.png)

    c. В hello **имя** в текстовое поле имя атрибута типа hello (например **emailaddress**).
    
    d. Из hello **значение** списка значение атрибута выберите hello (как **user.mail**).
    
    д. Нажмите кнопку **ОК**.
 
    > [!NOTE] 
    > Расширения атрибутов tooadd атрибуты, которые не находятся в Azure AD по умолчанию использовать. Нажмите кнопку [атрибутов пользователей, которые могут быть установлены в SAML](https://support.zendesk.com/hc/en-us/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise-) tooget hello SAML в полный список атрибутов, **Zendesk** принимает. 

5. На hello **сертификат подписи SAML** раздел, hello копирования **ОТПЕЧАТОК** значение сертификата.

    ![Настройка единого входа](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_certificate.png) 

6. На hello **конфигурации Zendesk** щелкните **Настройка Zendesk** tooopen **Настройка входа** окна. Копировать hello **URL-адрес выхода и SAML единого входа URL-адрес службы** из hello **краткий справочник.**

    ![Настройка единого входа](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_configure.png) 

7. В другом окне браузера войдите на свой корпоративный сайт Zendesk в качестве администратора.

8. Щелкните **Администратор**.

9. Hello панели навигации слева щелкните **параметры**, а затем нажмите кнопку **безопасности**.

10. На hello **безопасности** выполните следующие шаги hello: 
   
     ![Безопасность](./media/active-directory-saas-zendesk-tutorial/ic773089.png "Безопасность")

    ![Единый вход](./media/active-directory-saas-zendesk-tutorial/ic773090.png "Единый вход")

     а. Нажмите кнопку hello **Admin & агенты** вкладки.

     b. Выберите **Single sign-on (SSO) and SAML** (Единый вход и SAML), а затем щелкните **SAML**.

     c. В **URL-адрес единого входа SAML** текстовое значение hello вставить **SAML единого входа URL-адрес службы** скопирован из портала Azure. 

     d. В **URL-адрес удаленного выхода** текстовое значение hello вставить **URL-адрес выхода** скопирован из портала Azure.
        
     д. В **отпечаток сертификата** текстовое поле, вставить hello **отпечаток** значение сертификата, который вы скопировали из портала Azure.
     
     f. Щелкните **Сохранить**.

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-zendesk-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей перейти слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-zendesk-tutorial/create_aaduser_02.png) 

3. Вверху hello hello диалоговое окно, нажмите кнопку **добавить** tooopen hello **пользователя** диалогового окна.
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-zendesk-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-zendesk-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**. 

### <a name="creating-a-zendesk-test-user"></a>Создание тестового пользователя Zendesk

toolog tooenable Azure AD пользователи в **Zendesk**, их необходимо подготовить в **Zendesk**.  
В зависимости от роли hello, назначенные в приложения hello его hello ожидаемое поведение:

 1. Учетные записи с ролью **Конечный пользователь** подготавливаются автоматически при входе.
 2. **Агент** и **администратора** учетные записи должны вручную подготовить в toobe **Zendesk** перед входом в.
 
**tooprovision учетной записи пользователя, выполните следующие шаги hello.**

1. Войдите в tooyour **Zendesk** клиента.

2. Выберите hello **список клиентов** вкладки.

3. Выберите hello **пользователя** и нажмите кнопку **добавить**.
   
    ![Добавление пользователя](./media/active-directory-saas-zendesk-tutorial/ic773632.png "Добавление пользователя")
4. Введите адрес электронной почты hello существующей учетной записи Azure AD tooprovision и нажмите кнопку **Сохранить**.
   
    ![Новый пользователь](./media/active-directory-saas-zendesk-tutorial/ic773633.png "Новый пользователь")

> [!NOTE]
> Можно использовать любые другие Zendesk пользователя средства создания учетных записей или интерфейсы API, предоставляемые Zendesk tooprovision учетных записей пользователей AAD.


### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooZendesk доступа.

![Назначение пользователя][200] 

**tooassign tooZendesk Britta Simon выполните следующие шаги hello.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **Zendesk**.

    ![Настройка единого входа](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.

При нажатии кнопки hello Zendesk плитки в панели доступа hello, вы должны получить tooyour автоматически подписан на Zendesk приложения.
Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_203.png
