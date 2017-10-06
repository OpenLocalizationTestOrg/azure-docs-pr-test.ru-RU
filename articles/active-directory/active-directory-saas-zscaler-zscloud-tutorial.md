---
title: "Руководство по интеграции Azure Active Directory с Zscaler ZSCloud | Документы Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Zscaler ZSCloud."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 411d5684-a780-410a-9383-59f92cf569b5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: jeedes
ms.openlocfilehash: af6d5c1994e715cccf959cc9fd3ba998e5b9effa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zscaler-zscloud"></a>Руководство. Интеграция Azure Active Directory с Zscaler ZSCloud

В этом учебнике вы узнаете, как toointegrate Zscaler ZSCloud с Azure Active Directory (Azure AD).

Интеграция Zscaler ZSCloud с Azure AD предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooZscaler ZSCloud
- Можно включить на пользователей tooautomatically get вошедшего tooZscaler ZSCloud (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с Zscaler ZSCloud, требуется hello следующих элементов:

- подписка Azure AD;
- подписка с поддержкой единого входа Zscaler ZSCloud.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление Zscaler ZSCloud из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-zscaler-zscloud-from-hello-gallery"></a>Добавление Zscaler ZSCloud из галереи hello
tooconfigure hello интеграции Zscaler ZSCloud в Azure AD, вы должны tooadd Zscaler ZSCloud из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd Zscaler ZSCloud из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Приложения][3]

4. Введите в поле поиска hello **Zscaler ZSCloud**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_search.png)

5. В панели результатов hello выберите **Zscaler ZSCloud**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
Этот раздел описывает настройку и проверку единого входа Azure AD в Zscaler ZSCloud с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Zscaler ZSCloud является tooa в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в Zscaler ZSCloud должен установить toobe.

Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в Zscaler ZSCloud.

tooconfigure и теста Azure AD единого входа с Zscaler ZSCloud, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Настройка параметров прокси-сервера](#configuring-proxy-settings)**  -tooconfigure hello параметров прокси-сервера обозревателя Internet Explorer
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя Zscaler ZSCloud](#creating-a-zscaler-zscloud-test-user)**  -toohave аналог Саймон Britta в Zscaler ZSCloud, который представляет связанный toohello Azure AD пользователя.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложение Zscaler ZSCloud.

**tooconfigure Azure AD единого входа с Zscaler ZSCloud, выполните следующие шаги hello.**

1. В hello в hello портала Azure **Zscaler ZSCloud** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_samlbase.png)

3. На hello **Zscaler ZSCloud доменов и URL-адреса** выполните следующие шаги hello:

    ![Настройка единого входа](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_url.png)

     В hello **URL-адрес входа** textbox hello введите URL-адрес, используемый вашей пользователей на toosign tooyour ZScaler ZSCloud приложения.
    
    > [!NOTE] 
    > Имеется tooupdate это значение с hello фактический URL-адрес входа. Обратитесь к [группы поддержки Zscaler ZSCloud клиента](https://support.zscaler.com/hc/articles/210172606-Zscaler-is-Expanding-Its-Zscloud-Global-Footprint) tooget это значение. 
 
4. На hello **сертификат подписи SAML** щелкните **сертификата (Base64)** и затем сохраните файл сертификата hello на вашем компьютере.

    ![Настройка единого входа](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_400.png)

6. На hello **Zscaler ZSCloud конфигурации** щелкните **Настройка Zscaler ZSCloud** tooopen **Настройка входа** окна. Копировать hello **SAML единого входа URL-адрес службы** из hello **краткий справочник.**

    ![Настройка единого входа](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_configure.png) 

7. В другом окне браузера войдите в tooyour сайт ZScaler ZSCloud компании от имени администратора.

8. В меню в верхней части hello hello выберите **администрирования**.
   
    ![Администрирование](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800206.png "Администрирование")

9. В разделе **Manage Administrators & Roles** (Управление администраторами и ролями) щелкните **Manage Users & Authentication** (Управление пользователями и проверкой подлинности).   
            
    ![Управление пользователями и проверкой подлинности](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800207.png "Управление пользователями и проверкой подлинности")

10. В hello **Выбор параметров проверки подлинности для вашей организации** выполните следующие шаги hello:   
                
    ![Аутентификация](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800208.png "Аутентификация")
   
    а. Выберите параметр **Проверка подлинности с помощью единого входа SAML**.

    b. Щелкните **Настроить параметры единого входа SAML**.

11. На hello **SAML единого входа параметры настройки** странице диалогового окна, выполните следующие шаги hello и нажмите кнопку **сделать**

    ![Единый вход](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800209.png "Единый вход")
    
    а. Вставить hello **SAML единого входа URL-адрес службы** значение в hello **URL-адрес hello портала SAML toowhich пользователей будет отправлено для проверки подлинности** текстового поля.
    
    b. В hello **атрибут, содержащий имя входа** введите **NameID**.
    
    c. tooupload загруженный сертификат, нажмите кнопку **PEM-файл Zscaler**.
    
    d. Выберите параметр **Включить автоматическую подготовку SAML**.

12. На hello **Настройка проверки подлинности пользователя** диалогового окна выполните следующие шаги hello:

    ![Администрирование](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800210.png "Администрирование")
    
    а. Щелкните **Сохранить**.

    b. Щелкните **Активировать сейчас**.

## <a name="configuring-proxy-settings"></a>Настройка параметров прокси-сервера
### <a name="tooconfigure-hello-proxy-settings-in-internet-explorer"></a>параметры прокси-сервера tooconfigure hello в Internet Explorer

1. Запустите **Internet Explorer**.

2. Выберите **обозревателя** из hello **средства** меню откройте hello **обозревателя** диалогового окна.   
    
     ![Свойства браузера](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769492.png "Свойства браузера")

3. Нажмите кнопку hello **подключений** вкладки.   
  
     ![Подключения](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769493.png "Подключения")

4. Нажмите кнопку **параметры локальной сети** tooopen hello **параметры локальной сети** диалогового окна.

5. В hello раздела прокси-сервера выполните следующие шаги hello.   
   
    ![Прокси-сервер](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769494.png "Прокси-сервер")

    а. Установите флажок **Использовать прокси-сервер для локальной сети**.

    b. Введите в текстовое поле адрес hello **gateway.zscalerone.net**.

    c. Введите в текстовое поле hello порт **80**.

    d. Установите флаг **Не использовать прокси-сервер для локальных адресов**.

    д. Нажмите кнопку **ОК** tooclose hello **параметры локальной сети (LAN)** диалогового окна.

6. Нажмите кнопку **ОК** tooclose hello **обозревателя** диалогового окна.

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-zscaler-zscloud-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-zscaler-zscloud-tutorial/create_aaduser_02.png) 

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-zscaler-zscloud-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-zscaler-zscloud-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.

### <a name="creating-a-zscaler-zscloud-test-user"></a>Создание тестового пользователя Zscaler ZSCloud

Пользователи toolog tooenable Azure AD в tooZScaler ZSCloud, они должны быть подготовленных tooZScaler ZSCloud.  
В случае ZScaler ZSCloud hello Подготовка выполняется вручную.

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a>tooconfigure подготовки пользователей, выполните следующие шаги hello.

1. Войдите в tooyour **Zscaler** клиента.

2. Щелкните **Администрирование**.   
   
    ![Администрирование](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781035.png "Администрирование")

3. Щелкните **Управление пользователями**.   
        
     ![Добавление](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781037.png "Добавление")

4. В hello **пользователей** щелкните **добавить**.
      
    ![Добавление](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781037.png "Добавление")

5. В hello раздел добавить пользователя выполните hello следующие шаги.
        
    ![Добавление пользователя](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781038.png "Добавление пользователя")
   
    а. Hello тип **UserID**, **отображаемое имя пользователя**, **пароль**, **подтверждение пароля**, а затем выберите **группы**и hello **отдел** действительной учетной записи AAD, вы хотите tooprovision.

    b. Щелкните **Сохранить**.

> [!NOTE]
> Можно использовать любые другие ZScaler ZSCloud пользователя средства создания учетных записей или интерфейсы API, предоставляемые ZScaler ZSCloud tooprovision учетных записей пользователей AAD.

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooZscaler ZSCloud.

![Назначение пользователя][200] 

**tooassign Britta Simon tooZscaler ZSCloud, выполните следующие шаги hello.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **Zscaler ZSCloud**.

    ![Настройка единого входа](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

Tootest параметры единого входа, откройте панель доступа hello.

При нажатии кнопки Zscaler ZSCloud плитки в панели доступа hello hello, вы должны получить tooyour автоматически подписан в приложение Zscaler ZSCloud.

Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_203.png

