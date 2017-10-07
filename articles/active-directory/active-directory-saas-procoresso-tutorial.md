---
title: "Руководство. Интеграция Azure Active Directory с Procore SSO | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Procore единого входа."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9818edd3-48c0-411d-b05a-3ec805eafb2e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/07/2017
ms.author: jeedes
ms.openlocfilehash: bb918617f18ba3f44ddde469e6fc411977752f15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-procore-sso"></a>Руководство. Интеграция Azure Active Directory с Procore SSO

В этом учебнике вы узнаете, как toointegrate Procore единого входа в Azure Active Directory (Azure AD).

Интеграция Procore единого входа с Azure AD предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooProcore единого входа
- Можно включить на пользователей tooautomatically get вошедшего tooProcore единого входа (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал управления Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

<!--## Overview

tooenable single sign-on with Procore SSO, it must be configured toouse Azure Active Directory as an identity provider. This guide provides information and tips on how tooperform this configuration in Procore SSO.

>[!Note]: 
>This embedded guide is brand new in hello new Azure portal, and we’d love toohear your thoughts. Use hello Feedback ? button at hello top of hello portal tooprovide feedback. hello older guide for using hello [Azure classic portal](https://manage.windowsazure.com) tooconfigure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с помощью Procore единого входа требуется hello следующих элементов:

- подписка Azure AD;
- подписка на Procore SSO с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не следует использовать рабочую среду при отсутствии необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление Procore единого входа из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-procore-sso-from-hello-gallery"></a>Добавление Procore единого входа из галереи hello
tooconfigure hello интеграции Procore единого входа в Azure AD, вы должны tooadd Procore единого входа из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd Procore единого входа из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портала управления Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. Нажмите кнопку **добавить** кнопку в верхней части hello диалогового окна "hello".

    ![Приложения][3]

4. Введите в поле поиска hello **Procore SSO**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_search.png)

5. В панели результатов hello выберите **Procore SSO**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в Procore SSO с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Procore единого входа является tooa в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в Procore единого входа должен установить toobe.

Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в Procore единого входа.

tooconfigure и теста Azure AD единого входа с помощью Procore единого входа, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя Procore SSO](#creating-a-procore-sso-test-user)**  -toohave аналог Саймон Britta в Procore единый вход, являющийся представлением ей связанного toohello Azure AD.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал управления Azure hello и настройки единого входа в приложении Procore единого входа.

**tooconfigure Azure AD единого входа с помощью Procore единого входа, выполните следующие шаги hello.**

1. На портале управления Azure hello на hello **Procore SSO** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_samlbase.png)

3. На hello **Procore домена единого входа и URL-адреса** статьи, hello пользователь не имеет tooperform все меры как приложение hello уже заранее интегрировано с Azure.

    ![Настройка единого входа](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_url.png)

4. На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и сохраните hello XML-файл на компьютере.

    ![Настройка единого входа](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-procoresso-tutorial/tutorial_general_400.png)

6. На hello **Procore Настройка единого входа** щелкните **Настройка Procore SSO** tooopen **Настройка входа** окна. Копировать hello **идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**

    ![Настройка единого входа](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_configure.png) 

7. tooconfigure единого входа на **Procore SSO** стороны, узел procore компании tooyour входа от имени администратора.

8. Элементов в раскрывающемся hello вниз, щелкните на **администратора** страницу параметров единого входа tooopen hello.

    ![Настройка единого входа](./media/active-directory-saas-procoresso-tutorial/procore_tool_admin.png)

9. Вставить hello значения в полях hello, как описано ниже-

    ![Настройка единого входа](./media/active-directory-saas-procoresso-tutorial/procore_setting_admin.png)    

    а. В hello **единого входа на URL-адрес издателя** вставьте hello, идентификатор сущности SAML копируются hello портал Azure.

    b. В hello **SAML на целевой URL-адрес входа** вставьте hello SAML единого входа URL-адрес службы копируются hello портал Azure.

    c. Теперь откройте hello **метаданные в формате XML** загружается выше с hello портал Azure и копирование сертификатов hello в тег hello **X509Certificate**. Вставить hello копируется значение hello **сертификат единого входа x509** поле.

10. Щелкните **Save Changes** (Сохранить изменения).

11. После этих параметров должен toosend hello **доменное имя** (например **contoso.com**), по которой вход Procore toohello [Procore поддержки](https://support.procore.com/) и они будут Активируйте федеративный единый вход для этого домена.

<!--### Next steps

tooensure users can sign-in tooProcore SSO after it has been configured toouse Azure Active Directory, review hello following tasks and topics:

- User accounts must be pre-provisioned into Procore SSO prior toosign-in. tooset this up, see Provisioning.
 
- Users must be assigned access tooProcore SSO in Azure AD toosign-in. tooassign users, see Users.
 
- tooconfigure access polices for Procore SSO users, see Access Policies.
 
- For additional information on deploying single sign-on toousers, see [this article](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя на портале управления Azure hello, вызывается Саймон Britta.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал управления Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-procoresso-tutorial/create_aaduser_01.png) 

2. Go слишком**пользователей и групп** и нажмите кнопку **всех пользователей** toodisplay hello список пользователей.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-procoresso-tutorial/create_aaduser_02.png) 

3. Вверху hello диалоговое окно приветствия щелкните **добавить** tooopen hello **пользователя** диалогового окна.
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-procoresso-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-procoresso-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-a-procore-sso-test-user"></a>Создание тестового пользователя Procore SSO

Следуйте hello ниже шаги toocreate Procore тестового пользователя с их стороны.

1. Узел procore компании tooyour входа от имени администратора.  

2. Элементов в раскрывающемся hello вниз, щелкните на **каталога** страница directory компании tooopen hello.

    ![Настройка единого входа](./media/active-directory-saas-procoresso-tutorial/Procore_sso_directory.png)

3. Щелкните **добавления пользователя** tooopen hello формы и введите выполнять следующие параметра:

    ![Настройка единого входа](./media/active-directory-saas-procoresso-tutorial/Procore_user_add.png)

    а. В hello **имя** в текстовое поле имя пользователя тип как **Britta**.

    b. В hello **Фамилия** текстовое поле, Фамилия пользователя тип как **Simon**.

    c. В hello **адрес электронной почты** в текстовое поле, например адрес электронной почты пользователя типа  **BrittaSimon@contoso.com** .

    d. Для параметра **Permission Template** (Шаблон разрешений) выберите значение **Apply Permission Template Later** (Применить шаблон разрешений позже).

    д. Щелкните **Создать**.

4. Проверьте и обновите hello сведения для hello вновь добавленного контакта.

    ![Настройка единого входа](./media/active-directory-saas-procoresso-tutorial/Procore_user_check.png)

5. Щелкните **сохранения и отправки Invitiation** (Если приглашение по почте требуется) или **Сохранить** (сохранить непосредственно) регистрация пользователя toocomplete hello.
    
    ![Настройка единого входа](./media/active-directory-saas-procoresso-tutorial/Procore_user_save.png)    

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа, предоставляя свой доступ tooProcore единого входа.

![Назначение пользователя][200] 

**tooassign tooProcore Britta Simon единого входа, выполните hello следующие шаги.**

1. На портале управления Azure hello, открыть представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **Procore SSO**.

    ![Настройка единого входа](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.

Если вы хотите проверить параметры единого входа, откройте панель доступа. Дополнительные сведения о панели доступа можно найти в статье [Общие сведения о панели доступа](https://msdn.microsoft.com/library/dn308586). Если щелкнуть плитку hello Procore единого входа в панель доступа hello, вы должны получить приложение автоматически вошедшего tooyour Procore единого входа.

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_203.png

