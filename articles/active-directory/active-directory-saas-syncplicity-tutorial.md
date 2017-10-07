---
title: "Руководство. Интеграция Azure Active Directory с Syncplicity | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Syncplicity."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 896a3211-f368-46d7-95b8-e4768c23be08
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 6148112a959232ed24d76d1c7b8773f06568fee7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-syncplicity"></a>Учебник. Интеграция Azure Active Directory с Syncplicity

В этом учебнике вы узнаете, как toointegrate Syncplicity с Azure Active Directory (Azure AD).

Интеграция Syncplicity с Azure AD предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooSyncplicity
- Можно включить на пользователей tooautomatically get вошедшего tooSyncplicity (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с Syncplicity требуется hello следующих элементов:

- подписка Azure AD;
- подписка Syncplicity с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление Syncplicity из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-syncplicity-from-hello-gallery"></a>Добавление Syncplicity из галереи hello
tooconfigure hello интеграции Syncplicity в Azure AD, вы должны tooadd Syncplicity из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd Syncplicity из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Приложения][3]

4. Введите в поле поиска hello **Syncplicity**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_search.png)

5. В панели результатов hello выберите **Syncplicity**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в Syncplicity с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Syncplicity является tooa в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в Syncplicity должен установить toobe.

В Syncplicity, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.

tooconfigure и теста Azure AD единого входа с Syncplicity, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя Syncplicity](#creating-a-syncplicity-test-user)**  -toohave аналог Саймон Britta в Syncplicity, который представляет связанный toohello Azure AD пользователя.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложение Syncplicity.

**Azure AD tooconfigure единого входа с Syncplicity, выполните следующие шаги hello.**

1. В hello в hello портала Azure **Syncplicity** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_samlbase.png)

3. На hello **URL-адреса и домена Syncplicity** выполните следующие шаги hello:

    ![Настройка единого входа](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_url.png)

    а. В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<companyname>.syncplicity.com`

    b. В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<companyname>.syncplicity.com/sp`

    > [!NOTE] 
    > Эти значения приведены в качестве примера. Обновить значения hello фактический URL-адрес входа и идентификатор. Обратитесь к [группа поддержки клиента Syncplicity](https://www.syncplicity.com/contact-us) tooget эти значения. 
 

4. На hello **сертификат подписи SAML** щелкните **сертификата (Base64)** и затем сохраните файл сертификата hello на вашем компьютере.

    ![Настройка единого входа](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_certificate.png) 

  
5. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-syncplicity-tutorial/tutorial_general_400.png)

6. На hello **конфигурации Syncplicity** щелкните **Настройка Syncplicity** tooopen **Настройка входа** окна. Копировать hello **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**

    ![Настройка единого входа](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_configure.png) 

7. Войдите в tooyour **Syncplicity** клиента.

8. В меню в верхней части hello hello выберите **администратора**выберите **параметры**и нажмите кнопку **пользовательский домен и единый вход**.
   
    ![Syncplicity](./media/active-directory-saas-syncplicity-tutorial/ic769545.png "Syncplicity")

9. На hello **единый вход (SSO)** диалогового окна выполните следующие шаги hello:
   
    ![Единый вход\(Единый вход\)](./media/active-directory-saas-syncplicity-tutorial/ic769550.png "Single Sign-On \\\(SSO\\\)")   

    а. В hello **пользовательский домен** текстового поля, типа hello имя вашего домена.
  
    b. В поле **Состояния единого входа** задайте значение **Включено**.

    c. В hello **идентификатор сущности** текстовое значение hello вставить **идентификатор сущности SAML** скопирован из портала Azure.

    d. В hello **входа в URL-адрес страницы** текстовое поле, вставить hello **SAML единого входа URL-адрес службы** скопирован из портала Azure.

    д. В hello **URL-адрес страницы выхода** текстовое поле, вставить hello **URL-адрес выхода** скопирован из портала Azure.

    f. В **сертификат поставщика удостоверений**, нажмите кнопку **выбрать файл**, а затем отправьте hello сертификат, который вы скачали из hello портал Azure. 

    ж. Нажмите кнопку **Сохранить изменения**.

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_02.png) 

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-a-syncplicity-test-user"></a>Создание тестового пользователя Syncplicity
Для AAD пользователей toobe может toosign в они должны быть tooSyncplicity подготовленные приложения. В этом разделе описывается, как учетные записи пользователей toocreate AAD в Syncplicity.

**tooprovision tooSyncplicity учетной записи пользователя, выполните следующие шаги hello.**

1. Войдите в tooyour **Syncplicity** клиента (например: `https://company.Syncplicity.com`).

2. Щелкните **Администрирование** и выберите **Учетные записи пользователей**.

3. Нажмите кнопку **Добавить пользователя**.
   
    ![Управление пользователями](./media/active-directory-saas-syncplicity-tutorial/ic769764.png "Управление пользователями")

4. Тип hello **адресов электронной почты** учетной записи AAD, вы хотите tooprovision, выберите **пользователя** как **роли**и нажмите кнопку **Далее**.
   
    ![Сведения об учетной записи](./media/active-directory-saas-syncplicity-tutorial/ic769765.png "Сведения об учетной записи")
   
    >[!NOTE]
    >Держатель учетной записи AAD Hello получает сообщение электронной почты, tooconfirm ссылку и активации учетной записи hello. 
    > 

5. Выберите группу в организации, в которую будет входить новый пользователь, а затем нажмите кнопку **Далее**.
   
    ![Участие в группах](./media/active-directory-saas-syncplicity-tutorial/ic769772.png "Участие в группах")
   
    >[!NOTE]
    >Если список групп пуст, просто нажмите кнопку **Далее**. 
    > 

6. Выберите папки hello бы как tooplace под управлением Syncplicity на компьютере пользователя hello и нажмите кнопку **Далее**.
   
    ![Папки Syncplicity](./media/active-directory-saas-syncplicity-tutorial/ic769773.png "Папки Syncplicity")

>[!NOTE]
>Можно использовать любые другие Syncplicity пользователя средства создания учетных записей или интерфейсы API, предоставляемые Syncplicity tooprovision учетных записей пользователей AAD. 

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooSyncplicity доступа.

![Назначение пользователя][200] 

**tooassign tooSyncplicity Britta Simon выполните следующие шаги hello.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **Syncplicity**.

    ![Настройка единого входа](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

Цель этого раздела Hello является tootest настройки единого входа Azure AD с помощью панели доступа "hello".

При нажатии кнопки hello Syncplicity плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour Syncplicity приложения.
## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_203.png

