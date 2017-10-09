---
title: "Руководство по интеграции Azure Active Directory с Amazon Web Services (AWS) | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Amazon Web Services (AWS)."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7561c20b-2325-4d97-887f-693aa383c7be
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 1b79572ace63f6174ce4fa014c49bf44bd728228
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-amazon-web-services-aws"></a>Руководство по интеграции Azure Active Directory с Amazon Web Services

В этом учебнике вы узнаете, как toointegrate Amazon Web Services (AWS) с Azure Active Directory (Azure AD).

Интеграция с Azure AD Amazon Web Services (AWS) предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooAmazon Web Services (AWS)
- Ваш пользователей tooautomatically get вошедшего tooAmazon Web Services (AWS) (Single Sign-On) можно включить с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

<!--## Overview

tooenable single sign-on with Amazon Web Services (AWS), it must be configured toouse Azure Active Directory as an identity provider. This guide provides information and tips on how tooperform this configuration in Amazon Web Services (AWS).

>[!Note]: 
>This embedded guide is brand new in hello new Azure portal, and we’d love toohear your thoughts. Use hello Feedback ? button at hello top of hello portal tooprovide feedback. hello older guide for using hello [Azure classic portal](https://manage.windowsazure.com) tooconfigure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с Amazon Web Services (AWS) требуется hello следующих элементов:

- подписка Azure AD;
- Подписка с поддержкой единого входа в Amazon Web Services (AWS)

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не следует использовать рабочую среду при отсутствии необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление Amazon Web Services (AWS) из коллекции hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-amazon-web-services-aws-from-hello-gallery"></a>Добавление Amazon Web Services (AWS) из коллекции hello
tooconfigure hello интеграция Amazon Web Services (AWS) в Azure AD, вы должны tooadd Amazon Web Services (AWS) из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd Amazon Web Services (AWS) из коллекции hello, выполните следующие шаги hello.**

1. В hello  **[портала Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. Нажмите кнопку **добавить** кнопку в верхней части hello диалогового окна "hello".

    ![Приложения][3]

4. Введите в поле поиска hello **Amazon Web Services (AWS)**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_search.png)

5. В панели результатов hello выберите **Amazon Web Services (AWS)**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в Amazon Web Services (AWS) с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow какие пользователь аналог hello в Amazon Web Services (AWS) является tooa в Azure AD. Иными словами связи между пользователя Azure AD и связанных пользователей hello в Amazon Web Services (AWS) необходимо установить toobe.

Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в Amazon Web Services (AWS).

tooconfigure и тестирования Azure AD единого входа с Amazon Web Services (AWS), необходимы следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя, прошедшего Amazon Web Services](#creating-an-amazon-web-services-test-user)**  -toohave аналог Саймон Britta в Amazon Web Services (AWS), являющийся представлением ей связанного toohello Azure AD.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Amazon Web Services (AWS).

**tooconfigure Azure AD единого входа с Amazon Web Services (AWS), выполните следующие шаги hello.**

1. В hello портале Azure на hello **Amazon Web Services (AWS)** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна, как **режим** выберите **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_samlbase.png)

3. На hello **Amazon Web Services (AWS) доменов и URL-адреса** статьи, hello пользователь не имеет tooperform все меры как приложение hello уже заранее интегрировано с Azure.

    ![Настройка единого входа](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_url.png)

4. На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и сохраните hello XML-файл на компьютере.
    
    ![Настройка единого входа](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_certificate.png)

5. Hello Amazon Web Services (AWS) приложение ожидает утверждения SAML hello в определенном формате. Выполните настройку следующих утверждений для этого приложения hello. Вы можете управлять hello значения этих атрибутов из hello»**атрибуты пользователя**» на странице интеграции приложения. пример Hello следующий снимок экрана для этого.

    ![Настройка единого входа](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_attribute.png)

6. В hello **атрибуты пользователя** раздела, посвященного hello **единого входа** диалогового окна, настроить атрибутов токена SAML, как показано в приведенном выше рисунке hello и выполнять hello следующие шаги:
    
    | Имя атрибута  | Значение атрибута | Пространство имен |
    | --------------- | --------------- | --------------- |
    | RoleSessionName | user.userprincipalname | https://aws.Amazon.com/SAML/Attributes |
    | Роль            | user.assignedroles |  https://aws.Amazon.com/SAML/Attributes |
    
    >[!TIP]
    >Необходимо tooconfigure hello Подготовка пользователя к Azure AD toofetch все роли hello из консоли AWS. См. шаги подготовки hello.

    а. Нажмите кнопку **добавить атрибут** tooopen hello **Добавление атрибута** диалогового окна.

    ![Настройка единого входа](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_attribute_04.png)

    b. В hello **имя** в текстовое поле имя атрибута типа hello, показанный для этой строки.

    ![Настройка единого входа](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_attribute_05.png)

    c. Из hello **значение** списка значение атрибута типа hello, показанный для этой строки. Добавьте значение пространства имен hello, как показано выше.
    
    d. Нажмите кнопку **ОК**.

7. Нажмите кнопку **Сохранить** кнопку Параметры toosave hello в Azure.

    ![Настройка единого входа](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_400.png)

8. В другом окне браузера, tooyour входа на сайт компании Amazon Web Services (AWS) от имени администратора.

9. Щелкните **Console Home**(Домашняя страница консоли).
   
    ![Настройка единого входа][11]

10. Щелкните **IAM** в службе **Security, Identity & Compliance** (Безопасность, удостоверения и соответствие требованиям).
   
    ![Настройка единого входа][12]

11. Щелкните **Identity Providers** (Поставщики удостоверений), затем щелкните **Create Provider** (Создать поставщик).
   
    ![Настройка единого входа][13]

12. На hello **настроить поставщик** диалогового окна выполните следующие шаги hello:
   
    ![Настройка единого входа][14]
 
    а. Выберите для параметра **Тип поставщика** значение **SAML**.

    b. В hello **имя поставщика** текстовом поле введите имя поставщика (например: *WAAD*).

    c. tooupload скачанный файл метаданных, щелкните **выбрать файл**.

    d. Щелкните **Следующий шаг**.

13. На hello **проверить сведения о поставщике** странице диалогового окна щелкните **создать**. 
    
    ![Настройка единого входа][15]

14. Щелкните **Roles** (Роли), а затем нажмите кнопку **Create New Role** (Создать новую роль). 
    
    ![Настройка единого входа][16]

15. На hello **задать имя роли** диалоговое окно, выполните следующие шаги hello: 
    
    ![Настройка единого входа][17] 

    а. В hello **имя роли** текстовом поле введите имя роли (например: *TestUser*). 

    b. Щелкните **Следующий шаг**.

16. На hello **выберите тип роли** диалоговое окно, выполните следующие шаги hello: 
    
    ![Настройка единого входа][18] 

    а. Выберите **Роль для доступа поставщика удостоверений**. 

    b. В hello **предоставление единого входа через Интернет (WebSSO) поставщики доступа к tooSAML** щелкните **выберите**.

17. На hello **установления доверия** диалоговое окно, выполните следующие шаги hello:  
    
    ![Настройка единого входа][19] 

    а. В качестве поставщика SAML выбрать поставщика SAML hello, вы создали ранее (например: *WAAD*)
  
    b. Щелкните **Следующий шаг**.

18. На hello **проверить доверие роли** диалоговое окно, нажмите кнопку **следующий шаг**.
    
    ![Настройка единого входа][32]

19. На hello **политики присоединения** диалоговое окно, нажмите кнопку **следующий шаг**.
    
    ![Настройка единого входа][33]

20. На hello **проверки** диалоговое окно, выполните следующие шаги hello:
    
    ![Настройка единого входа][34]
 
    а. Щелкните **Создать роль**.

    b. Создайте столько ролей и сопоставить их toohello поставщика удостоверений.

21. Теперь настройки hello подготовки пользователей toofetch все роли hello из AWS

    а. В имени входа консоли AWS hello с вашей учетной записи root

    b. В hello правом верхнем углу щелкните свое имя и нажмите кнопку hello **мои учетные данные безопасности** параметр. Откроется экран с предупреждением. Нажмите кнопку "hello" **учетные данные безопасности** toopass кнопку hello экрана.
        
       ![Настройка единого входа][36]

       ![Настройка единого входа][37]

    c. В hello ключи доступа нажмите кнопку hello **создать новый ключ доступа** кнопки. Это приводит к возникновению ошибки hello кода доступа и значение маркера.
    
       ![Настройка единого входа][38]

    d. Скопируйте оба эти значения, а также скачайте их, чтобы не потерять.

    д. В hello портале Azure на странице интеграции приложения hello Amazon Web Services (AWS), щелкните **Provisioning**.
        
       ![Настройка единого входа][35]

    f. Установить режим подготовки hello слишком**автоматический**
        
       ![Настройка единого входа][39]

    ж. Теперь в hello **clientsecret** и **секрет маркера** вставьте hello соответствующего значения, которые вы скопировали из консоли AWS.
    
    h. Можно щелкнуть hello **проверить подключение** кнопку tootest hello подключения. После успешной можно запустить hello подготовки соединителя.
       
       ![Настройка единого входа][40]

    i. Теперь включить hello состояние подготовки слишком**на**. Запустится выборка hello ролей из приложения hello.

       ![Настройка единого входа][41]

    > [!NOTE]
    > Запускается служба Azure AD подготовки каждой после некоторых ролей hello время toosync из AWS. Вы увидите все hello поставщика удостоверений присоединенного AWS роли в Azure AD, и их можно использовать при назначении toousers приложения hello или группы.

<!--### Next steps

tooensure users can sign-in tooAmazon Web Services (AWS) after it has been configured toouse Azure Active Directory, review hello following tasks and topics:

- User accounts must be pre-provisioned into Amazon Web Services (AWS) prior toosign-in. tooset this up, see Provisioning.
 
- Users must be assigned access tooAmazon Web Services (AWS) in Azure AD toosign-in. tooassign users, see Users.
 
- tooconfigure access polices for Amazon Web Services (AWS) users, see Access Policies.
 
- For additional information on deploying single sign-on toousers, see [this article](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_01.png) 

2. Go слишком**пользователей и групп** и нажмите кнопку **всех пользователей** toodisplay hello список пользователей.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_02.png) 

3. Вверху hello диалоговое окно приветствия щелкните **добавить** tooopen hello **пользователя** диалогового окна.
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-an-amazon-web-services-test-user"></a>Создание тестового пользователя Amazon Web Services

В порядке tooenable toolog пользователей Azure AD в tooAmazon Web Services (AWS) их необходимо подготовить в Amazon Web Services (AWS). В случае hello Amazon Web Services (AWS) Подготовка выполняется вручную.

**tooprovision учетной записи пользователя, выполните следующие шаги hello.**

1. Войдите в tooyour **Amazon Web Services (AWS)** сайт компании от имени администратора.

2. Нажмите кнопку hello **Главная страница консоли** значок. 
   
    ![Настройка единого входа][11]

3. Щелкните Identity and Access Management (Управление удостоверениями и доступом). 
   
    ![Настройка единого входа][28]

4. Hello панели мониторинга, щелкните **пользователей**, а затем нажмите кнопку **создания новых пользователей**. 
   
    ![Настройка единого входа][29]

5. В диалоговом окне приветствия создать пользователя выполните hello следующие шаги. 
   
    ![Настройка единого входа][30]   
    
    а. В hello **введите имена пользователей** текстовые поля, введите имя пользователя Саймон Brita (userprincipalname) в Azure AD.

    b. Щелкните **Создать**.
        
### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа, предоставляя свой доступ tooAmazon Web Services (AWS).

![Назначение пользователя][200] 

**tooassign tooAmazon Britta Simon Web Services (AWS) выполните hello следующие шаги.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **Amazon Web Services (AWS)**.

    ![Настройка единого входа](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. На **выберите роль** вкладке, выберите hello соответствующую роль для пользователя hello. Эти роли обозначаются hello имя роли и имя поставщика удостоверений. Таким образом, можно легко определить роли hello из AWS.

8. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.

При нажатии кнопки приветствия Amazon Web Services (AWS) плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour приложения Amazon Web Services (AWS). 

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_203.png
[11]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795031.png
[12]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795032.png
[13]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795033.png
[14]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795034.png
[15]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795035.png
[16]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795022.png
[17]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795023.png
[18]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795024.png
[19]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795025.png
[20]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950351.png
[21]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_80.png
[22]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950352.png
[23]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_81.png
[24]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950353.png
[25]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_15.png

[28]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950321.png
[29]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795037.png
[30]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795038.png
[32]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950251.png
[33]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950252.png
[34]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950253.png
[35]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning.png
[36]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_securitycredentials.png
[37]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_securitycredentials_continue.png
[38]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_createnewaccesskey.png
[39]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning_automatic.png
[40]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning_testconnection.png
[41]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning_on.png
