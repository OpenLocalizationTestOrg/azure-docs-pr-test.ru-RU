---
title: "Руководство по интеграции Azure Active Directory с песочницей Salesforce | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и песочницы Salesforce."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ee54c39e-ce20-42a4-8531-da7b5f40f57c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 7539f08356568a17ebfcee2764bbbefa129b0553
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-salesforce-sandbox"></a>Учебник. Интеграция Azure Active Directory с песочницей Salesforce

В этом учебнике вы узнаете, как toointegrate песочницы Salesforce с Azure Active Directory (Azure AD).

Интеграция песочницы Salesforce с Azure AD предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooSalesforce "песочницы"
- Можно включить на пользователей tooautomatically get вошедшего tooSalesforce "песочницы" (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с песочницей Salesforce требуется hello следующих элементов:

- подписка Azure AD;
- подписка Salesforce Sandbox с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление из галереи hello песочницы Salesforce
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-salesforce-sandbox-from-hello-gallery"></a>Добавление из галереи hello песочницы Salesforce
tooconfigure hello интеграцией песочницы Salesforce с Azure AD, вы должны tooadd песочницы Salesforce из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd песочницы Salesforce из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. Нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна "hello".

    ![Приложения][3]

4. Введите в поле поиска hello **песочницы Salesforce**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_search.png)

5. В панели результатов hello выберите **песочницы Salesforce**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в Salesforce Sandbox с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в песочницу Salesforce является tooa в Azure AD. Другими словами связи между пользователя Azure AD и hello связанных пользователей в песочницу Salesforce должен установить toobe.

Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в песочницу Salesforce.

tooconfigure и тестирования Azure AD единого входа с песочницей Salesforce, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя песочницы Salesforce](#creating-a-salesforce-sandbox-test-user)**  -toohave аналог Саймон Britta в песочницу Salesforce, который представляет связанный toohello Azure AD пользователя.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложение песочницы Salesforce.

**tooconfigure Azure AD единого входа с песочницей Salesforce, выполните следующие шаги hello.**

1. В hello в hello портала Azure **песочницы Salesforce** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_samlbase.png)

3. На hello **URL-адреса и домен песочницы Salesforce** выполните следующие шаги hello:

    ![Настройка единого входа](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_url.png)

     В hello **URL-адрес входа** текстовое значение hello типа, используя следующий шаблон hello:`https://<subdomain>.my.salesforce.com`

    > [!NOTE] 
    > Это значение не реальными hello. Измените значение этого параметра hello фактический URL-адрес входа. Обратитесь к [группа поддержки клиента песочницы Salesforce](https://help.salesforce.com/support) tooget это значение.


4. Если вы уже настроили единого входа для другого экземпляра песочницы Salesforce в вашем каталоге, то необходимо также настроить hello **идентификатор** toohave hello совпадает со значением hello **URL-адрес входа**. 
    
    >[!Note]
    >Hello **идентификатор** поле можно найти путем проверки hello **Показывать дополнительные параметры** флажок на hello **настроить URL-адрес приложения** hello диалогового окна 


5. На hello **сертификат подписи SAML** щелкните **сертификат** и затем сохраните файл сертификата hello на вашем компьютере.

    ![Настройка единого входа](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_certificate.png) 

6. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_400.png)

7. На hello **конфигурации песочницы Salesforce** щелкните **настроить песочницу Salesforce** tooopen **Настройка входа** окна. Копировать hello **идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**

    ![Настройка единого входа](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_configure.png) 
<CS>
8. Откройте новую вкладку в браузере и войдите в учетную запись администратора песочницы Salesforce tooyour.

9. В меню в верхней части hello hello выберите **установки**.

    ![Настройка единого входа](./media/active-directory-saas-salesforcesandbox-tutorial/IC781024.png)
10. Hello hello левой панели навигации щелкните **управления безопасностью**, а затем нажмите кнопку **параметры единого входа**.

    ![Настройка единого входа](./media/active-directory-saas-salesforcesandbox-tutorial/IC781025.png)
11. На hello раздел параметров единого входа, выполните следующие шаги hello: ![настройки единого входа](./media/active-directory-saas-salesforcesandbox-tutorial/IC781026.png)
     
     а.  Установите флажок **SAML включен**. 

     b.  Нажмите кнопку **Создать**.

12. На hello SAML единого входа «параметры» выполните следующие шаги hello.

    ![Настройка единого входа](./media/active-directory-saas-salesforcesandbox-tutorial/IC781027.png)

    a.In hello в текстовое поле имя, имя типа hello hello конфигурации (например: *SPSSOWAAD\_тест*). 

    b. Вставить **идентификатор сущности SMAL** значение в hello **издателя** текстового поля.

    c. В hello **идентификатор сущности** введите **https://test.salesforce.com** при hello первый экземпляр песочницы Salesforce, добавляется tooyour каталога. При добавлении экземпляра песочницы Salesforce, а затем для hello **идентификатор сущности** типа в hello **на URL-адрес входа**, которые должны быть в следующем формате:`http://company.my.salesforce.com`  
 
    d. Нажмите кнопку **Обзор** tooupload hello загрузить сертификат.  

    д. Как **типа удостоверения SAML**выберите **утверждение, содержащее hello идентификатор федерации из объекта пользователя hello**.
 
    f. Как **расположения удостоверения SAML**выберите **удостоверение находится в элемент hello NameIdentifier оператора Subject hello**.

    ж. Вставить **единого входа URL-адрес службы** в hello **URL-адрес входа поставщика удостоверений** текстового поля. 

    h. SFDC не поддерживает выход SAML.  Чтобы избежать этого, вставьте «https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0» в hello **URL-адрес выхода поставщика удостоверений** текстового поля.

    i. В поле **Service Provider Initiated Request Binding** (Связывание запросов, инициированных поставщиком услуг) выберите значение **HTTP POST**. 

    j. Щелкните **Сохранить**.

### <a name="enable-your-domain"></a>Включение домена
В этом разделе предполагается, что вы уже создали домен.  Дополнительные сведения см. в разделе [Define Your Domain Name](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US) (Определение доменного имени).

**tooenable к домену, выполните следующие шаги hello:**

1. Hello панели навигации слева щелкните **Управление доменами**, а затем нажмите кнопку **Мой домен.**
   
     ![Настройка единого входа](./media/active-directory-saas-salesforcesandbox-tutorial/IC781029.png)
   
   >[!NOTE]
   >Убедитесь в правильности настройки домена. 

2. В hello **параметры страницы входа** щелкните **изменить**, затем, по мере **службы проверки подлинности**, выберите имя hello hello SAML единого входа параметр из предыдущего hello статьи, а затем щелкните **Сохранить**.
   
   ![Настройка единого входа](./media/active-directory-saas-salesforcesandbox-tutorial/IC781030.png)

Как только домен настроен, пользователям следует использовать hello домена URL-адрес toologin toohello песочницы Salesforce.  

значение hello tooget hello URL-адреса, щелкните профиль единого входа hello, созданный в предыдущем разделе hello.    

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)


### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей перейти слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_02.png) 

3. Вверху hello hello диалоговое окно, нажмите кнопку **добавить** tooopen hello **пользователя** диалогового окна.
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-a-salesforce-sandbox-test-user"></a>Создание тестового пользователя Salesforce Sandbox

В этом разделе вы создадите в Salesforce Sandbox пользователя с именем Britta Simon. Salesforce Sandbox поддерживает JIT-подготовку. Эта функция включена по умолчанию.
В этом разделе никакие действия с вашей стороны не требуются. Если пользователь еще не существует в песочницу Salesforce, создается новый, при попытке tooaccess песочницы Salesforce.

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooSalesforce "песочницы".

![Назначение пользователя][200] 

**tooassign tooSalesforce Britta Simon "песочницы", выполните следующие шаги hello.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **песочницы Salesforce**.

    ![Настройка единого входа](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

Tootest параметры единого входа, откройте панель доступа hello. Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Руководство по настройке Google Apps для автоматической подготовки пользователей](active-directory-saas-salesforce-sandbox-provisioning-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_203.png

