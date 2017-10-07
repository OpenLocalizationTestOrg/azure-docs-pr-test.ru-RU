---
title: "Руководство. Интеграция Azure Active Directory с Zscaler | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Zscaler."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 68c453f7-aff1-4614-92d3-9b86f3ad99dc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: e2894534f5d6711fd6af618cd699fa5837b5bf26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zscaler"></a>Руководство. Интеграция Azure Active Directory с Zscaler

В этом учебнике вы узнаете, как toointegrate Zscaler с Azure Active Directory (Azure AD).

Интеграция Zscaler с Azure AD предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooZscaler
- Можно включить на пользователей tooautomatically get вошедшего tooZscaler (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с Zscaler требуется hello следующих элементов:

- подписка Azure AD;
- подписка Zscaler с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление Zscaler из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-zscaler-from-hello-gallery"></a>Добавление Zscaler из галереи hello
tooconfigure hello интеграции Zscaler в Azure AD, вы должны tooadd Zscaler из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd Zscaler из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Приложения][3]

4. Введите в поле поиска hello **Zscaler**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_search.png)

5. В панели результатов hello выберите **Zscaler**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в Zscaler с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Zscaler является tooa в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в Zscaler должен установить toobe.

В Zscaler, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.

tooconfigure и теста Azure AD единого входа с Zscaler, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Настройка параметров прокси-сервера](#configuring-proxy-settings)**  -tooconfigure hello параметров прокси-сервера обозревателя Internet Explorer
3. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
4. **[Создание тестового пользователя Zscaler](#creating-a-zscaler-test-user)**  -toohave аналог Саймон Britta в Zscaler, который представляет связанный toohello Azure AD пользователя.
5. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
6. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложение Zscaler.

**Azure AD tooconfigure единого входа с Zscaler, выполните следующие шаги hello.**

1. В hello в hello портала Azure **Zscaler** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_samlbase.png)

3. На hello **URL-адреса и домена Zscaler** выполните следующие шаги hello:

    ![Настройка единого входа](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_url.png)

    В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<companyname>.zsclaer.net`

    > [!NOTE] 
    > Это значение приведено для справки. Измените значение этого параметра hello фактический URL-адрес входа. Обратитесь к [группы поддержки Zscaler клиента](https://www.zscaler.com/company/contact) tooget это значение. 

4. На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.

    ![Настройка единого входа](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-zscaler-tutorial/tutorial_general_400.png)

6. На hello **конфигурации Zscaler** щелкните **Настройка Zscaler** tooopen **Настройка входа** окна. Копировать hello **SAML единого входа URL-адрес службы** из hello **краткий справочник.**

    ![Настройка единого входа](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_configure.png) 

7. В другом окне браузера войти в корпоративный сайт ZScaler tooyour с правами администратора.

8. В меню в верхней части hello hello выберите **администрирования**.
   
    ![Администрирование](./media/active-directory-saas-zscaler-tutorial/ic800206.png "Администрирование")

9. В разделе **Manage Administrators & Roles** (Управление администраторами и ролями) щелкните **Manage Users & Authentication** (Управление пользователями и проверкой подлинности).   
            
    ![Управление пользователями и проверкой подлинности](./media/active-directory-saas-zscaler-tutorial/ic800207.png "Управление пользователями и проверкой подлинности")

10. В hello **Выбор параметров проверки подлинности для вашей организации** выполните следующие шаги hello:   
                
    ![Аутентификация](./media/active-directory-saas-zscaler-tutorial/ic800208.png "Аутентификация")
   
    а. Выберите параметр **Проверка подлинности с помощью единого входа SAML**.

    b. Щелкните **Настроить параметры единого входа SAML**.

11. На hello **SAML единого входа параметры настройки** странице диалогового окна, выполните следующие шаги hello и нажмите кнопку **сделать**

    ![Единый вход](./media/active-directory-saas-zscaler-tutorial/ic800209.png "Единый вход")
    
    а. Вставить hello **SAML единого входа URL-адрес службы** значение, которое было скопировано из hello портал Azure в hello **URL-адрес hello портала SAML toowhich пользователей будет отправлено для проверки подлинности** текстового поля.
    
    b. В hello **атрибут, содержащий имя входа** введите **NameID**.
    
    c. tooupload загруженный сертификат, нажмите кнопку **PEM-файл Zscaler**.
    
    d. Выберите параметр **Включить автоматическую подготовку SAML**.

12. На hello **Настройка проверки подлинности пользователя** диалогового окна выполните следующие шаги hello:

    ![Администрирование](./media/active-directory-saas-zscaler-tutorial/ic800210.png "Администрирование")
    
    а. Щелкните **Сохранить**.

    b. Щелкните **Активировать сейчас**.

## <a name="configuring-proxy-settings"></a>Настройка параметров прокси-сервера
### <a name="tooconfigure-hello-proxy-settings-in-internet-explorer"></a>параметры прокси-сервера tooconfigure hello в Internet Explorer

1. Запустите **Internet Explorer**.

2. Выберите **обозревателя** из hello **средства** меню откройте hello **обозревателя** диалогового окна.   
    
     ![Свойства браузера](./media/active-directory-saas-zscaler-tutorial/ic769492.png "Свойства браузера")

3. Нажмите кнопку hello **подключений** вкладки.   
  
     ![Подключения](./media/active-directory-saas-zscaler-tutorial/ic769493.png "Подключения")

4. Нажмите кнопку **параметры локальной сети** tooopen hello **параметры локальной сети** диалогового окна.

5. В hello раздела прокси-сервера выполните следующие шаги hello.   
   
    ![Прокси-сервер](./media/active-directory-saas-zscaler-tutorial/ic769494.png "Прокси-сервер")

    а. Установите флажок **Использовать прокси-сервер для локальной сети**.

    b. Введите в текстовое поле адрес hello **gateway.zscaler.net**.

    c. Введите в текстовое поле hello порт **80**.

    d. Установите флаг **Не использовать прокси-сервер для локальных адресов**.

    д. Нажмите кнопку **ОК** tooclose hello **параметры локальной сети (LAN)** диалогового окна.

6. Нажмите кнопку **ОК** tooclose hello **обозревателя** диалогового окна.

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-zscaler-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-zscaler-tutorial/create_aaduser_02.png) 

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-zscaler-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-zscaler-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-a-zscaler-test-user"></a>Создание тестового пользователя Zscaler

Пользователи toolog tooenable Azure AD в tooZScaler, они должны быть подготовленных tooZScaler.  
В случае ZScaler hello Подготовка выполняется вручную.

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a>tooconfigure подготовки пользователей, выполните следующие шаги hello.

1. Войдите в tooyour **Zscaler** клиента.

2. Щелкните **Администрирование**.   
   
    ![Администрирование](./media/active-directory-saas-zscaler-tutorial/ic781035.png "Администрирование")

3. Щелкните **Управление пользователями**.   
        
     ![Добавление](./media/active-directory-saas-zscaler-tutorial/ic781036.png "Добавление")

4. В hello **пользователей** щелкните **добавить**.
      
    ![Добавление](./media/active-directory-saas-zscaler-tutorial/ic781037.png "Добавление")

5. В hello раздел добавить пользователя выполните hello следующие шаги.
        
    ![Добавление пользователя](./media/active-directory-saas-zscaler-tutorial/ic781038.png "Добавление пользователя")
   
    а. Hello тип **UserID**, **отображаемое имя пользователя**, **пароль**, **подтверждение пароля**, а затем выберите **группы**и hello **отдел** действительной учетной записи AAD, вы хотите tooprovision.

    b. Щелкните **Сохранить**.

> [!NOTE]
> Можно использовать любые другие ZScaler пользователя средства создания учетных записей или интерфейсы API, предоставляемые ZScaler tooprovision учетных записей пользователей AAD.

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooZscaler доступа.

![Назначение пользователя][200] 

**tooassign tooZscaler Britta Simon выполните следующие шаги hello.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **Zscaler**.

    ![Настройка единого входа](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.

При нажатии кнопки hello Zscaler плитки в панели доступа hello, вы должны получить tooyour автоматически подписан в приложение Zscaler.
Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_203.png

