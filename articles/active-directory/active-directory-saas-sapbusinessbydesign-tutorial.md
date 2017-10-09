---
title: "Руководство по интеграции Azure Active Directory с SAP Business ByDesign | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и SAP Business ByDesign."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 82938920-33ba-47cb-b141-511b46d19e66
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: c14714fd27f8d7fc555f25c7be83fad2b0d7f333
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-business-bydesign"></a>Руководство по интеграции Azure Active Directory с SAP Business ByDesign

В этом учебнике вы узнаете, как toointegrate SAP Business ByDesign с Azure Active Directory (Azure AD).

Интеграция SAP Business ByDesign с Azure AD предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooSAP ByDesign бизнеса.
- Вы можете включить учетные записи Azure AD вашей пользователей tooautomatically get вошедшего tooSAP ByDesign бизнеса (Single Sign-On).
- Вы можете управлять учетными записями в одном централизованном месте - hello портал Azure.

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с SAP Business ByDesign требуется hello следующих элементов:

- подписка Azure AD;
- подписка SAP Business ByDesign с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление SAP Business ByDesign из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-sap-business-bydesign-from-hello-gallery"></a>Добавление SAP Business ByDesign из галереи hello
tooconfigure hello интеграции SAP Business ByDesign в Azure AD, вы должны tooadd SAP Business ByDesign из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd SAP Business ByDesign из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Кнопка Hello Azure Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Hello корпоративных приложений колонку][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Кнопка нового приложения Hello][3]

4. Введите в поле поиска hello **SAP Business ByDesign**выберите **SAP Business ByDesign** из панели результатов щелкните **добавить** кнопку tooadd приложения hello.

    ![SAP Business ByDesign в списке результатов hello](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD

В этом разделе описана настройка и проверка единого входа Azure AD в SAP Business ByDesign с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в SAP Business ByDesign является tooa в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в SAP Business ByDesign должен установить toobe.

В SAP Business ByDesign, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.

tooconfigure и теста Azure AD единого входа с SAP Business ByDesign, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя, прошедшего SAP Business ByDesign](#create-an-sap-business-bydesign-test-user)**  -toohave аналог Саймон Britta в SAP Business ByDesign, представление связанных toohello Azure AD пользователя.
4. **[Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#test-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configure-azure-ad-single-sign-on"></a>Настройка единого входа Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении SAP Business ByDesign.

**tooconfigure Azure AD единого входа с SAP Business ByDesign, выполните следующие шаги hello.**

1. В hello в hello портала Azure **SAP Business ByDesign** странице интеграции приложения щелкните **единого входа**.

    ![Ссылка "Настройка единого входа"][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_samlbase.png)

3. На hello **URL-адреса и домена ByDesign SAP Business** выполните следующие шаги hello:

    ![Сведения о домене и URL-адресах единого входа для приложения SAP Business ByDesign](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_url.png)

    а. В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<servername>.sapbydesign.com`

    b. В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<servername>.sapbydesign.com`

    > [!NOTE] 
    > Эти значения приведены в качестве примера. Обновить значения hello фактический URL-адрес входа и идентификатор. Обратитесь к [группа поддержки SAP Business ByDesign клиента](https://www.sap.com/products/cloud-analytics.support.html) tooget эти значения.

4. На hello **атрибуты пользователя** выполните следующие шаги hello:

    ![Раздел атрибутов SAP Business ByDesign](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_attribute.png)
    
    а. В **идентификатор пользователя** список, выберите hello **ExtractMailPrefix()** функции.
    
    b. Из hello **Mail** список, атрибут пользователя выберите hello требуется toouse вашей реализации. Например если требуется toouse hello EmployeeID как уникальный идентификатор пользователя и хранящимся в hello ExtensionAttribute2 значение атрибута hello, выберите user.extensionattribute2.   

5. На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.

    ![ссылку для скачивания сертификата Hello](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_certificate.png) 

6. Нажмите кнопку **Сохранить** .

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_400.png)

7. На hello **ByDesign конфигурации SAP Business** щелкните **Настройка SAP Business ByDesign** tooopen **Настройка входа** окна. Копировать hello **SAML единого входа URL-адрес службы** из hello **краткий справочник.**

    ![Настройка SAP Business ByDesign](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_configure.png) 

8. tooget единого входа, настроенному для вашего приложения, выполните следующие шаги hello.
   
    а. Войдите на портал SAP Business ByDesign tooyour с правами администратора.
   
    b. Перейдите в слишком**приложения и общие задачи управления пользователя** и нажмите кнопку hello **поставщика удостоверений** вкладки.
   
    c. Нажмите кнопку **нового поставщика удостоверений** и выберите hello метаданных XML-файл, загруженный с портала Azure hello. Путем импорта метаданных hello, hello системы автоматически отправляет сертификат подписи требуется указать hello и сертификат шифрования.
   
    ![Настройка единого входа](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_54.png)
   
    d. tooinclude hello **URL-адрес службы утверждения потребителя** в запросе SAML hello, выберите **включает утверждение потребителя URL-адрес службы**.
   
    д. Щелкните **Activate Single Sign-On**(Активировать единый вход).
   
    Е. Сохраните изменения.
   
    ж. Нажмите кнопку hello **Мои системы** вкладки.
   
    ![Настройка единого входа](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_52.png)
   
    h. Вставить **SAML единого входа URL-адрес службы**, который вы скопировали из портала Azure hello его в hello **URL-адрес входа AD Azure** текстового поля.
   
    ![Настройка единого входа](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_53.png)
   
    i. Указать ли hello сотрудника можно вручную выбрать между войти с помощью идентификатора пользователя и пароль или единого входа, выбрав **Выбор поставщика удостоверений вручную**.
   
    j. В hello **URL-адрес SSO** статьи, укажите hello URL-адрес, который должен использоваться системой toohello toologon сотрудника hello. 
    Hello URL-адрес отправки tooEmployee раскрывающемся списке можно выбрать hello следующие параметры:
   
    **Non-SSO URL**
   
    Hello система отправляет только hello нормальная URL-адрес toohello сотрудника. Сотрудник Hello не может войти в систему с помощью единого входа и должны использовать пароль или сертификат вместо.
   
    **SSO URL** 
   
    Hello система отправляет только hello сотрудник toohello URL-адрес единого входа. Сотрудник Hello можно войти в систему с помощью единого входа. Перенаправляет запрос проверки подлинности через hello поставщика удостоверений.
   
    **Automatic Selection**
   
    Если единый вход не активен, hello система отправляет hello нормальная URL-адрес toohello сотрудника. Если активен единого входа, hello система проверяет, содержит ли сотрудника hello пароль. Если пароль, URL-адрес единого входа и URL-адрес единого входа не отправляются toohello сотрудника. Тем не менее если сотрудник hello не имеет пароля, toohello сотрудника отправляется только hello URL-адрес единого входа.
   
    k. Сохраните изменения.

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD

Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

   ![Создание тестового пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello hello левой панели портала Azure щелкните hello **Azure Active Directory** кнопки.

    ![Кнопка Hello Azure Active Directory](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_01.png)

2. слишком go toodisplay hello список пользователей,**пользователей и групп**, а затем нажмите кнопку **всех пользователей**.

    ![Здравствуйте, «Пользователи и группы» и «Все пользователи» ссылки](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_02.png)

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** вверху hello hello **всех пользователей** диалоговое окно.

    ![Кнопка "Добавить" Hello](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_03.png)

4. В hello **пользователя** диалогового окна выполните следующие шаги hello:

    ![диалоговое окно приветствия пользователя](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_04.png)

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** поле типа hello адрес электронной почты пользователя Саймон Britta.

    c. Выберите hello **Показать пароль** флажок и запишите значение hello, отображаемый в hello **пароль** поле.

    d. Щелкните **Создать**.
 
### <a name="create-an-sap-business-bydesign-test-user"></a>Создание тестового пользователя SAP Business ByDesign

В этом разделе мы создадим пользователя Britta Simon в приложении SAP Business ByDesign. Можно работать с [группа поддержки SAP Business ByDesign клиента](https://www.sap.com/products/cloud-analytics.support.html) tooadd hello пользователей на платформе SAP Business ByDesign hello. 

> [!NOTE]
> Убедитесь, что значение идентификатора имени должен совпадать с hello поле имени пользователя на платформе SAP Business ByDesign hello.

### <a name="assign-hello-azure-ad-test-user"></a>Назначить hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooSAP ByDesign бизнеса.

![Назначение пользователям ролей hello][200] 

**tooassign tooSAP Britta Simon ByDesign бизнеса выполните hello следующие шаги.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **SAP Business ByDesign**.

    ![ссылка SAP Business ByDesign Hello в списке приложений hello](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_app.png)  

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Hello ссылку «Пользователи и группы»][202]

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![область назначения, добавьте Hello][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="test-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.

Если щелкнуть плитку SAP Business ByDesign hello в hello панели доступа, следует получать приложения SAP Business ByDesign tooyour автоматически вошедшего.

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_203.png

