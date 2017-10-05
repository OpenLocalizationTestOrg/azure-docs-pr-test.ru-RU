---
title: "Учебник. Интеграция Azure Active Directory с M-Files | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в M-Files."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4536fd49-3a65-4cff-9620-860904f726d0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 0f2682cf7cd3e11a5a7156938fbe9d4c7f541312
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-m-files"></a>Учебник. Интеграция Azure Active Directory с M-Files

В этом учебнике описано, как интегрировать приложение M-Files с Azure Active Directory (Azure AD).

Интеграция Azure AD с приложением M-Files обеспечивает следующие преимущества:

- С помощью Azure AD вы можете контролировать доступ к M-Files.
- Вы можете включить автоматический вход пользователей в M-Files (единый вход) с учетной записью Azure AD.
- Вы можете управлять учетными записями централизованно — через портал Azure.

Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

Чтобы настроить интеграцию Azure AD с M-Files, вам потребуется:

- подписка Azure AD;
- подписка M-Files с поддержкой единого входа.

> [!NOTE]
> Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.

При проверке действий в этом учебнике соблюдайте следующие рекомендации:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Сценарий, описанный в этом руководстве, состоит из двух стандартных блоков.

1. Добавление M-Files из коллекции
2. Настройка и проверка единого входа в Azure AD.

## <a name="adding-m-files-from-the-gallery"></a>Добавление M-Files из коллекции
Чтобы настроить интеграцию M-Files с Azure AD, необходимо добавить M-Files из коллекции в список управляемых приложений SaaS.

**Чтобы добавить M-Files из коллекции, выполните следующие действия:**

1. На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**. 

    ![Active Directory][1]

2. Перейдите к разделу **Корпоративные приложения**. Затем выберите **Все приложения**.

    ![Приложения][2]
    
3. Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.

    ![Приложения][3]

4. В поле поиска введите **M-Files**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_search.png)

5. На панели результатов выберите **M-Files** и нажмите кнопку **Добавить**, чтобы добавить это приложение.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в M-Files с использованием тестового пользователя Britta Simon.

Для работы единого входа Azure AD необходимо знать, какому пользователю в Azure AD соответствует пользователь в M-Files. Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в M-Files.

Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в M-Files.

Чтобы настроить и проверить единый вход Azure AD в M-Files, вам потребуется выполнить действия в следующих стандартных блоках:

1. **[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.
3. **[Создание тестового пользователя M-Files](#creating-a-m-files-test-user)** требуется для создания в M-Files пользователя Britta Simon, связанного с соответствующим представлением в Azure AD.
4. **[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.
5. **[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении M-Files.

**Чтобы настроить единый вход Azure AD в M-Files, выполните следующие действия:**

1. На портале Azure на странице интеграции с приложением **M-Files** щелкните **Единый вход**.

    ![Настройка единого входа][4]

2. В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_samlbase.png)

3. В разделе **Домены и URL-адреса приложения M-Files** выполните следующие действия:

    ![Настройка единого входа](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_url.png)

    а. В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<tenantname>.cloudvault.m-files.com/authentication/MFiles.AuthenticationProviders.Core/sso`

    b. В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://<tenantname>.cloudvault.m-files.com`

    > [!NOTE] 
    > Эти значения приведены в качестве примера. Замените эти значения фактическим URL-адресом для входа и идентификатором. Чтобы получить их, обратитесь в [службу поддержки клиентов M-Files](mailto:support@m-files.com). 
 
4. В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.

    ![Настройка единого входа](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-m-files-tutorial/tutorial_general_400.png)

6. Для настройки единого входа в вашем приложении обратитесь в [службу поддержки M-Files](mailto:support@m-files.com) и предоставьте скачанный файл метаданных.
   
    >[!NOTE]
    >Если вы хотите настроить единый вход для классического приложения M-Files, то выполните описанные ниже действия. Если единый вход настраивается только для веб-версии M-Files, то никакие дополнительные действия не требуются.  

7. Выполните описанные ниже действия, чтобы настроить в классическом приложении M-Files единый вход с помощью Azure AD. Для скачивания M-Files перейдите на страницу [M-Files download](https://www.m-files.com/en/download-latest-version) (Скачивание M-Files).

8. Откройте окно **M-Files Desktop Settings** (Параметры классического приложения M-Files). Нажмите кнопку **Добавить**.
   
    ![Настройка единого входа](./media/active-directory-saas-m-files-tutorial/tutorial_m_files_10.png)

9. В окне **Document Vault Connection Properties** (Свойства подключения хранилища документов) выполните указанные ниже действия.
   
    ![Настройка единого входа](./media/active-directory-saas-m-files-tutorial/tutorial_m_files_11.png)  

    В разделе Server (Сервер) введите следующие значения:  

    а. В поле **Name** (Имя) введите `<tenant-name>.cloudvault.m-files.com`. 
 
    b. В поле **Port Number** (Номер порта) введите **4466**. 

    c. Для параметра **Protocol** (Протокол) выберите **HTTPS**. 

    d. В поле **Authentication** (Аутентификация) выберите **Specific Windows user** (Определенный пользователь Windows). Затем отобразится страница подписи. Введите свои учетные данные Azure AD. 

    д. Для параметра **Vault on Server** (Хранилище на сервере) выберите соответствующее хранилище на сервере.
 
    Е. Нажмите кнопку **ОК**.

> [!TIP]
> Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.  После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы. Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).
> 

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.

![Создание пользователя Azure AD][100]

**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**

1. На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-m-files-tutorial/create_aaduser_01.png) 

2. Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-m-files-tutorial/create_aaduser_02.png) 

3. Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-m-files-tutorial/create_aaduser_03.png) 

4. На странице диалогового окна **Пользователь** выполните следующие действия.
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-m-files-tutorial/create_aaduser_04.png) 

    а. В текстовом поле **Имя** введите **BrittaSimon**.

    b. В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение поля **Пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-a-m-files-test-user"></a>Создание тестового пользователя M-Files

Цель этого раздела — создать пользователя с именем Britta Simon в приложении M-Files. Обратитесь в [службу поддержки M-Files](mailto:support@m-files.com), чтобы добавить пользователей в приложение M-Files.

### <a name="assigning-the-azure-ad-test-user"></a>Назначение тестового пользователя Azure AD

В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure путем предоставления доступа к M-Files.

![Назначение пользователя][200] 

**Чтобы назначить пользователя Britta Simon в M-Files, выполните следующие действия:**

1. На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений выберите **M-Files**.

    ![Настройка единого входа](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_app.png) 

3. В меню слева выберите **Пользователи и группы**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

Цель этого раздела — проверить конфигурацию единого входа Azure AD с помощью панели доступа.

Щелкнув элемент M-Files на панели доступа, вы автоматически войдете в приложение M-Files.

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по интеграции приложений SaaS с Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_203.png

