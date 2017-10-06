---
title: "Руководство по интеграции Azure Active Directory с xMatters OnDemand | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory с xMatters OnDemand."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ca0633db-4f95-432e-b3db-0168193b5ce9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 7cc8f9f0d8cefc8a60b9514027437ced50c66242
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-xmatters-ondemand"></a>Руководство по интеграции Azure Active Directory с xMatters OnDemand

В этом учебнике вы узнаете, как toointegrate xMatters OnDemand с Azure Active Directory (Azure AD).

Интеграция xMatters OnDemand с Azure AD предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooxMatters по запросу
- Можно включить на пользователей tooautomatically get вошедшего tooxMatters OnDemand (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с xMatters OnDemand требуется hello следующих элементов:

- подписка Azure AD;
- подписка xMatters OnDemand с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление xMatters OnDemand из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-xmatters-ondemand-from-hello-gallery"></a>Добавление xMatters OnDemand из галереи hello
tooconfigure hello интеграции xMatters OnDemand в Azure AD, вы должны tooadd xMatters OnDemand из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd xMatters OnDemand из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Приложения][3]

4. Введите в поле поиска hello **xMatters OnDemand**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_search.png)

5. В панели результатов hello выберите **xMatters OnDemand**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в xMatters OnDemand с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow какие hello пользователь аналога в xMatters OnDemand является tooa пользователем в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в xMatters OnDemand должен установить toobe.

В xMatters OnDemand, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.

tooconfigure и теста Azure AD единого входа с xMatters OnDemand, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя xMatters OnDemand](#creating-a-xmatters-ondemand-test-user)**  -toohave аналог Саймон Britta в xMatters OnDemand, представление связанных toohello Azure AD пользователя.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в вашей xMatters OnDemand приложения.

**tooconfigure Azure AD единого входа с xMatters OnDemand, выполните следующие шаги hello.**

1. В hello в hello портала Azure **xMatters OnDemand** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_samlbase.png)

3. На hello **xMatters OnDemand доменов и URL-адреса** выполните следующие шаги hello:

    ![Настройка единого входа](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_url.png)
    
    а. В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:   
    | |
    |--|
    | `https://<companyname>.au1.xmatters.com.au/`|
    | `https://<companyname>.cs1.xmatters.com/`|
    | `https://<companyname>.xmatters.com/`|
    | `https://www.xmatters.com`|
    | `https://<companyname>.xmatters.com.au/`|

    b. В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:
    | |
    |--|
    | `https://<companyname>.au1.xmatters.com.au`|
    | `https://<companyname>.xmatters.com/sp/<instancename>`|
    | `https://<companyname>.cs1.xmatters.com/sp/<instancename>`|
    | `https://<companyname>.au1.xmatters.com.au/<instancename>`|

    > [!NOTE] 
    > Эти значения приведены в качестве примера. Обновите эти значения с hello фактический идентификатор и ответ URL-адрес. Обратитесь к [поддержки xMatters OnDemand](https://www.xmatters.com/company/contact-us/) tooget эти значения.

4. На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и сохраните hello файл сертификата локально как **c:\\XMatters OnDemand.cer**.

    ![Настройка единого входа](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_certificate.png)
    
    > [!IMPORTANT]
    > Требуется сертификат toohello tooforward hello [поддержки xMatters OnDemand](https://www.xmatters.com/company/contact-us/). Hello сертификат должен toobe, загруженных с поддержки xmatters hello, чтобы вы могли завершить hello единого входа для конфигурации. 

5. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_400.png)

6. На hello **xMatters OnDemand конфигурации** щелкните **Настройка xMatters OnDemand** tooopen **Настройка входа** окна. Копировать hello **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**

    ![Настройка единого входа](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_configure.png) 

7. В другом окне браузера войдите в tooyour корпоративный сайт XMatters OnDemand с правами администратора.

8. Щелкните hello панели инструментов в верхней части hello **администратора**, а затем нажмите кнопку **сведения о компании** hello панели навигации слева hello.
   
    ![Администратор](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776795.png "Администратор")

9. На hello **конфигурация SAML** выполните следующие шаги hello:
   
    ![Настройка SAML](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776796.png "Настройка SAML")
   
    а. Выберите **Включить SAML**.
   
    b. Вставить **идентификатор сущности SAML**, которой копируются hello портал Azure в hello **идентификатор поставщика удостоверений** текстового поля.
   
    c. Вставить **SAML единого входа URL-адрес службы**, которого вы скопировали из портала Azure hello в hello **адрес единого входа** текстового поля.
   
    d. Вставить **URL-адрес выхода**, которого вы скопировали из портала Azure hello в hello **URL-адрес единого выхода** текстового поля.
   
    д. На странице hello сведения о компании в верхней части экрана приветствия щелкните **сохранить изменения**.
    
    ![Сведения о компании](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776797.png "Сведения о компании")

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-xmatters-ondemand-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-xmatters-ondemand-tutorial/create_aaduser_02.png) 

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-xmatters-ondemand-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-xmatters-ondemand-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-a-xmatters-ondemand-test-user"></a>Создание тестового пользователя xMatters OnDemand

В порядке tooenable toolog пользователей Azure AD в tooXMatters OnDemand их необходимо подготовить в XMatters OnDemand. В случае hello объекта XMatters OnDemand Подготовка выполняется вручную.

### <a name="tooprovision-a-user-accounts-perform-hello-following-steps"></a>tooprovision учетных записей пользователей, выполните следующие действия hello:
1. Войдите в tooyour **XMatters OnDemand** клиента.

2.  Нажмите кнопку **пользователей** вкладку и нажмите кнопку **добавить пользователя**.
  
    ![Пользователи](./media/active-directory-saas-xmatters-ondemand-tutorial/IC781048.png "Пользователи")

3. В hello **Добавление пользователя** выполните следующие шаги hello:
   
    ![Добавление пользователя](./media/active-directory-saas-xmatters-ondemand-tutorial/IC781049.png "Добавление пользователя")

    а. Установите флажок **Активно**.

    b. В hello **идентификатор пользователя** в текстовое поле типа hello идентификатор пользователя, например Brittasimon@contoso.com.
   
    c. В hello **имя** текстовое поле, имя первого типа hello пользователя как Britta.

    d. В hello **Фамилия** текстовое поле, тип фамилию пользователя hello как Simon.
    
    д. В hello **сайта** текстовое поле, ввод hello допустимым сайтом допустимым Azure AD счета, tooprovision.
    
    f. Щелкните **Сохранить**.

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooxMatters по запросу.

![Назначение пользователя][200] 

**tooassign tooxMatters Britta Simon OnDemand, выполните hello следующие шаги.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **xMatters OnDemand**.

    ![Настройка единого входа](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.

При нажатии кнопки hello xMatters OnDemand плитки в панели доступа hello, вы должны получить tooyour автоматически подписан в xMatters OnDemand приложения.
Дополнительные сведения о панели доступа см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_203.png

