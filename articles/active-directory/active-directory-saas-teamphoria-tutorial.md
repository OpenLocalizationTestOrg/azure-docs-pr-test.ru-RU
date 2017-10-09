---
title: "Руководство по интеграции Azure Active Directory с Teamphoria | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Teamphoria."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d569c705-6f0f-4ec1-b485-ba82526b5d32
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/07/2017
ms.author: jeedes
ms.openlocfilehash: f32be9742b76f7fe464036dadc108c62e4a787a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-teamphoria"></a>Руководство по интеграции Azure Active Directory с Teamphoria

В этом учебнике вы узнаете, как toointegrate Teamphoria с Azure Active Directory (Azure AD).

Интеграция с Azure AD Teamphoria предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooTeamphoria
- Можно включить на пользователей tooautomatically get вошедшего tooTeamphoria (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал управления Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

<!--## Overview

tooenable single sign-on with Teamphoria, it must be configured toouse Azure Active Directory as an identity provider. This guide provides information and tips on how tooperform this configuration in Teamphoria.

>[!Note]: 
>This embedded guide is brand new in hello new Azure portal, and we’d love toohear your thoughts. Use hello Feedback ? button at hello top of hello portal tooprovide feedback. hello older guide for using hello [Azure classic portal](https://manage.windowsazure.com) tooconfigure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с Teamphoria требуется hello следующих элементов:

- подписка Azure AD;
- подписка Teamphoria с активированной функцией единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не следует использовать рабочую среду при отсутствии необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление Teamphoria из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-teamphoria-from-hello-gallery"></a>Добавление Teamphoria из галереи hello
tooconfigure hello интеграции Teamphoria в Azure AD, вы должны tooadd Teamphoria из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd Teamphoria из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портала управления Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. Нажмите кнопку **добавить** кнопку в верхней части hello диалогового окна "hello".

    ![Приложения][3]

4. Введите в поле поиска hello **Teamphoria**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_search.png)

5. В панели результатов hello выберите **Teamphoria**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в Teamphoria с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Teamphoria является tooa в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в Teamphoria должен установить toobe.

Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в Teamphoria.

tooconfigure и теста Azure AD единого входа с Teamphoria, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя Teamphoria](#creating-a-teamphoria-test-user)**  -toohave аналог Саймон Britta в Teamphoria, представление связанных toohello Azure AD ей.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал управления Azure hello и настройки единого входа в приложении Teamphoria.

**tooconfigure Azure AD единого входа с Teamphoria, выполните следующие шаги hello.**

1. На портале управления Azure hello на hello **Teamphoria** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна, как **режим** выберите **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_samlbase.png)

3. На hello **URL-адреса и домена Teamphoria** выполните следующие шаги hello:

    ![Настройка единого входа](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_url.png)

    а. В hello **URL-адрес входа** textbox hello введите URL-адрес, используя следующий шаблон hello:`https://<sub-domain>.teamphoria.com/login`  

    > [!NOTE] 
    > Обратите внимание на то, что они не hello реальные значения. Имеется tooupdate эти значения с hello фактический URL-адрес входа. Обратитесь к [группа поддержки клиента Teamphoria](https://www.teamphoria.com/) tooget hello входа URL-адрес. 

4. На hello **сертификат подписи SAML** щелкните **сертификата (Base64)** и сохраните hello сертификата на компьютере.

    ![Настройка единого входа](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-teamphoria-tutorial/tutorial_general_400.png)

6. На hello **конфигурации Teamphoria** щелкните **Настройка Teamphoria** tooopen **Настройка входа** окна. Копировать hello **SAML единого входа URL-адрес службы** из hello **краткий справочник.**

    ![Настройка единого входа](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_configure.png) 

7. tooconfigure единого входа на **Teamphoria** стороны, приложения Teamphoria tooyour входа в систему с правами администратора.

8. Go слишком**параметры АДМИНИСТРИРОВАНИЯ** параметр в левой панели инструментов hello и постоянно hello hello, настройте нажмите на **ЕДИНОГО входа** tooopen hello SSO конфигурации окна.

    ![Настройка единого входа](./media/active-directory-saas-teamphoria-tutorial/admin_sso_configure.png)

9. Щелкните **Добавление ПОСТАВЩИКА УДОСТОВЕРЕНИЙ** параметр в форме hello tooopen hello правом верхнем углу для добавления параметров hello для единого входа.

    ![Настройка единого входа](./media/active-directory-saas-teamphoria-tutorial/add_new_identity_provider.png)

10. Введите сведения о hello в полях hello, как описано ниже-

    ![Настройка единого входа](./media/active-directory-saas-teamphoria-tutorial/Teamphoria_sso_save.png)

    а. **ОТОБРАЖАЕМОЕ имя** : hello отображаемое имя подключаемого модуля hello на странице администрирования hello.

    b. **ИМЯ кнопки** : hello имя вкладки hello, которая будет отображаться на странице входа hello для ведения журнала во единого входа.

    c. **СЕРТИФИКАТ** : Привет открыть сертификата загружен ранее из hello портал Azure в блокноте, скопируйте содержимое hello hello же и вставьте его в поле hello.

    d. **ТОЧКА входа** : hello вставить **SAML единого входа URL-адрес службы** копируются ранней формы hello портал Azure.

    д. Переключение hello параметр слишком**ON** и выберите команду **Сохранить**. 

<!--### Next steps

tooensure users can sign-in tooTeamphoria after it has been configured toouse Azure Active Directory, review hello following tasks and topics:

- User accounts must be pre-provisioned into Teamphoria prior toosign-in. tooset this up, see Provisioning.
 
- Users must be assigned access tooTeamphoria in Azure AD toosign-in. tooassign users, see Users.
 
- tooconfigure access polices for Teamphoria users, see Access Policies.
 
- For additional information on deploying single sign-on toousers, see [this article](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя на портале управления Azure hello, вызывается Саймон Britta.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал управления Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_01.png) 

2. Go слишком**пользователей и групп** и нажмите кнопку **всех пользователей** toodisplay hello список пользователей.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_02.png) 

3. Вверху hello диалоговое окно приветствия щелкните **добавить** tooopen hello **пользователя** диалогового окна.
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-a-teamphoria-test-user"></a>Создание тестового пользователя Teamphoria

В порядке tooenable toolog пользователей Azure AD в Teamphoria их необходимо подготовить в Teamphoria. В случае Teamphoria hello Подготовка выполняется вручную.

**tooprovision учетных записей пользователей, выполните следующие действия hello:**

1. Войдите в систему tooyour Teamphoria сайт компании как администратор.

2. Щелкните **АДМИНИСТРАТОРА** параметры на левой панели инструментов hello и внутри hello **УПРАВЛЕНИЕ** вкладке щелкните на **пользователей** страницу администрирования hello tooopen для пользователей.

    ![Добавление сотрудника](./media/active-directory-saas-teamphoria-tutorial/admin_manage_users.png)

3. Щелкните hello **ПРИГЛАСИТЬ вручную** параметр.

    ![Приглашение пользователей](./media/active-directory-saas-teamphoria-tutorial/admin_manage_add_users.png)  

4. На этой странице сделайте следующее. 
    
    ![Приглашение пользователей](./media/active-directory-saas-teamphoria-tutorial/manual_user_invite.png)  

    а. В hello **адрес электронной почты** текстовом hello **адрес электронной почты** из BrittaSimon.

    b. В hello **имя** введите **Britta**.

    c. В hello **ФАМИЛИЯ** введите **Simon**.

    d. Нажмите кнопку **INVITE 1 USER** (Пригласить одного пользователя). Пользователь должен tooget приглашение hello tooaccept, созданные в системе hello.

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления ее tooTeamphoria доступа.

![Назначение пользователя][200] 

**tooassign tooTeamphoria Britta Simon выполните следующие шаги hello.**

1. На портале управления Azure hello, открыть представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **Teamphoria**.

    ![Настройка единого входа](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.

Если вы хотите проверить параметры единого входа, откройте панель доступа. Дополнительные сведения о панели доступа можно найти в статье [Общие сведения о панели доступа](https://msdn.microsoft.com/library/dn308586). 

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_203.png

