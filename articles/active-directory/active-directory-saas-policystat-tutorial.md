---
title: "Руководство по интеграции Azure Active Directory с PolicyStat | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и PolicyStat."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: af5eb0f1-1c8e-4809-b0c4-8ccfb915ca42
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 868053cd0d37359fd9b4aeb93dba42cbbaa09845
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-policystat"></a>Руководство по интеграции Azure Active Directory с PolicyStat

В этом учебнике вы узнаете, как toointegrate PolicyStat с Azure Active Directory (Azure AD).

Интеграция с Azure AD PolicyStat предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooPolicyStat
- Можно включить на пользователей tooautomatically get вошедшего tooPolicyStat (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с PolicyStat требуется hello следующих элементов:

- подписка Azure AD;
- подписка PolicyStat с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление PolicyStat из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-policystat-from-hello-gallery"></a>Добавление PolicyStat из галереи hello
tooconfigure hello интеграции PolicyStat в Azure AD, вы должны tooadd PolicyStat из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd PolicyStat из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Приложения][3]

4. Введите в поле поиска hello **PolicyStat**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_search.png)

5. В панели результатов hello выберите **PolicyStat**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в PolicyStat с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в PolicyStat является tooa в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в PolicyStat должен установить toobe.

В PolicyStat, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.

tooconfigure и теста Azure AD единого входа с PolicyStat, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя PolicyStat](#creating-a-policystat-test-user)**  -toohave аналог Саймон Britta в PolicyStat, который представляет связанный toohello Azure AD пользователя.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении PolicyStat.

**tooconfigure Azure AD единого входа с PolicyStat, выполните следующие шаги hello.**

1. В hello в hello портала Azure **PolicyStat** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_samlbase.png)

3. На hello **URL-адреса и домена PolicyStat** выполните следующие шаги hello:

    ![Настройка единого входа](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_url.png)

    а. В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<companyname>.policystat.com`

    b. В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<companyname>.policystat.com/saml2/metadata/`

    > [!NOTE] 
    > Эти значения приведены в качестве примера. Обновить значения hello фактический URL-адрес входа и идентификатор. Обратитесь к [группа поддержки клиента PolicyStat](http://www.policystat.com/support/) tooget эти значения. 
 
4. На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.

    ![Настройка единого входа](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_certificate.png) 

5. Цель этого раздела Hello — toooutline как tooPolicyStat tooauthenticate tooenable пользователей с учетной записью в Azure AD, используя федерацию на основе hello SAML протокола.

    Hello PolicyStat приложения ожидает утверждения SAML hello в определенном формате, требующий tooadd настраиваемого атрибута сопоставления tooyour **атрибутов токена SAML** конфигурации.  

     Следующий снимок экрана приветствия показан пример этого.

     ![Атрибуты](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_attribute.png "Атрибуты")

6. сопоставления атрибутов hello необходимые tooadd, выполните hello следующие шаги.

    | Имя атрибута    |   Значение атрибута |
    |------------------- | -------------------- |
    | uid | ExtractMailPrefix([mail]) |
    
    а. Нажмите кнопку **добавить атрибут** tooopen hello **Добавление атрибута** диалогового окна.

    ![Настройка единого входа](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_04.png)

    ![Настройка единого входа](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_addatribute.png)
    
    b. В hello **имя атрибута** введите **uid**.

    c. В hello **значение атрибута** текстового поля, выберите **ExtractMailPrefix()**.    
   
    d. Из hello **Mail** выберите **User.mail**.
    
    д. Нажмите кнопку **ОК**.

7. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-policystat-tutorial/tutorial_general_400.png)

8. В другом окне веб-браузера войдите на сайт PolicyStat своей компании в качестве администратора.

9. Нажмите кнопку hello **администратора** , а затем щелкните **настройки единого входа** в левой области навигации.
   
    ![Меню администратора](./media/active-directory-saas-policystat-tutorial/ic808633.png "Меню администратора")

10. В hello **установки** выберите **Включение единого входа интеграции**.
   
    ![Конфигурация единого входа](./media/active-directory-saas-policystat-tutorial/ic808634.png "Конфигурация единого входа")

11. Нажмите кнопку **Настройка атрибутов**, а затем в hello **Настройка атрибутов** выполните следующие шаги hello:
   
    ![Конфигурация единого входа](./media/active-directory-saas-policystat-tutorial/ic808635.png "Конфигурация единого входа")
   
    а. В hello **атрибута Username** введите **uid**.

    b. В hello **атрибут имени** введите **firstname** пользователя **Britta**.

    c. В hello **атрибут фамилии** введите **lastname** пользователя **Simon**.

    d. В hello **атрибут адреса электронной почты** введите **emailaddress** пользователя  **BrittaSimon@contoso.com** .

    д. Нажмите кнопку **Сохранить изменения**.

12. Нажмите кнопку **свои метаданные поставщика Удостоверений**, а затем в hello **свои метаданные поставщика Удостоверений** выполните следующие шаги hello:
   
    ![Конфигурация единого входа](./media/active-directory-saas-policystat-tutorial/ic808636.png "Конфигурация единого входа")
   
    а. Откройте скачанный файл метаданных в hello копирования содержимого, а затем вставьте его в hello **свои метаданные поставщика удостоверений** текстового поля.

    b. Нажмите кнопку **Сохранить изменения**.

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-policystat-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-policystat-tutorial/create_aaduser_02.png) 

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-policystat-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-policystat-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-a-policystat-test-user"></a>Создание тестового пользователя PolicyStat

В порядке tooenable toolog пользователей Azure AD в PolicyStat их необходимо подготовить в PolicyStat.  

PolicyStat поддерживает подготовку пользователей «на лету». Это означает, что не требуется вручную пользователей hello tooadd tooPolicyStat. Hello пользователей будет автоматически добавляются при их первом входе с помощью единого входа.

>[!NOTE]
>Можно использовать любые другие PolicyStat пользователя средства создания учетных записей или интерфейсы API, предоставляемые PolicyStat tooprovision учетных записей пользователей Azure AD.
> 

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooPolicyStat доступа.

![Назначение пользователя][200] 

**tooassign tooPolicyStat Britta Simon выполните следующие шаги hello.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **PolicyStat**.

    ![Настройка единого входа](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.

При нажатии кнопки hello PolicyStat плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour PolicyStat приложения.
Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_203.png

