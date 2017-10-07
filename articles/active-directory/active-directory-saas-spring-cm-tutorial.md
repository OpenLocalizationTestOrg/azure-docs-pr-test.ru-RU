---
title: "Руководство по интеграции Azure Active Directory с SpringCM | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и SpringCM."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4a42f797-ac58-4aca-a8e6-53bfe5529083
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: jeedes
ms.openlocfilehash: 12c8ebe765e2c6e61115256e9343d90ec132e1f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-springcm"></a>Руководство. Интеграция Azure Active Directory с SpringCM

В этом учебнике вы узнаете, как toointegrate SpringCM с Azure Active Directory (Azure AD).

Интеграция SpringCM с Azure AD предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooSpringCM
- Можно включить на пользователей tooautomatically get вошедшего tooSpringCM (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с SpringCM требуется hello следующих элементов:

- подписка Azure AD;
- подписка SpringCM с активированной функцией единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление SpringCM из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-springcm-from-hello-gallery"></a>Добавление SpringCM из галереи hello
tooconfigure hello интеграции SpringCM в Azure AD, вы должны tooadd SpringCM из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd SpringCM из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Приложения][3]

4. Введите в поле поиска hello **SpringCM**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_search.png)

5. В панели результатов hello выберите **SpringCM**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в SpringCM с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в SpringCM является tooa в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в SpringCM должен установить toobe.

В SpringCM, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.

tooconfigure и теста Azure AD единого входа с SpringCM, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя SpringCM](#creating-a-springcm-test-user)**  -toohave аналог Саймон Britta в SpringCM, который представляет связанный toohello Azure AD пользователя.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложение SpringCM.

**tooconfigure Azure AD единого входа с SpringCM, выполните следующие шаги hello.**

1. В hello в hello портала Azure **SpringCM** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_samlbase.png)

3. На hello **URL-адреса и домена SpringCM** выполните следующие шаги hello:

    ![Настройка единого входа](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_url.png)

    В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://na11.springcm.com/atlas/SSO/SSOEndpoint.ashx?aid=<identifier>`

    > [!NOTE] 
    > Это значение приведено для справки. Измените значение этого параметра hello фактический URL-адрес входа. Обратитесь к [группа поддержки клиента SpringCM](https://knowledge.springcm.com/support) tooget это значение. 
 
4. На hello **сертификат подписи SAML** щелкните **Certificate(Raw)** и затем сохраните файл сертификата hello на вашем компьютере.

    ![Настройка единого входа](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-spring-cm-tutorial/tutorial_general_400.png)

6. На hello **конфигурации SpringCM** щелкните **Настройка SpringCM** tooopen **Настройка входа** окна. Копировать hello **идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**

    ![Настройка единого входа](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_configure.png)   

7. В другом окне браузера, войдите на tooyour **SpringCM** сайт компании от имени администратора.

8. В меню hello hello верхней части страницы, нажмите кнопку **перейти к**, нажмите кнопку **предпочтения**, а затем в hello **предпочтения учетной записи** щелкните **единого входа SAML**.
   
    ![Единый вход SAML](./media/active-directory-saas-spring-cm-tutorial/ic797051.png "Единый вход SAML")

9. В hello разделе Конфигурация поставщика удостоверений выполните следующие шаги hello.
   
    ![Конфигурация поставщика удостоверений](./media/active-directory-saas-spring-cm-tutorial/ic797052.png "Конфигурация поставщика удостоверений")
    
    а. tooupload Скачанный сертификат Azure Active Directory, нажмите кнопку **выбрать сертификат издателя** или **изменить сертификат издателя**.
    
    b. Вставить **идентификатор сущности SAML** значение, которое было скопировано из портала Azure в hello **издателя** текстового поля.
    
    c. Вставить **SAML единого входа URL-адрес службы** значение, которое было скопировано из hello портал Azure в hello **инициированная конечная точка Service Provider (SP)** текстового поля.
            
    d. Для параметра **SAML Enabled** (SAML включен) установите значение **Enabled** (Включено).

    д. Щелкните **Сохранить**.
 
> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-spring-cm-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-spring-cm-tutorial/create_aaduser_02.png) 

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-spring-cm-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-spring-cm-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-a-springcm-test-user"></a>Создание тестового пользователя SpringCM

toolog пользователей Azure Active Directory tooenable в tooSpringCM, их необходимо подготовить в SpringCM. В случае hello объекта SpringCM Подготовка выполняется вручную.

>[!NOTE]
>Дополнительные сведения см. в статье [Create and Edit a SpringCM User](http://knowledge.springcm.com/create-and-edit-a-springcm-user) (Создание и изменение пользователя SpringCM). 

**tooprovision tooSpringCM учетной записи пользователя, выполните следующие шаги hello.**

1. Войдите в tooyour **SpringCM** сайт компании от имени администратора.

2. Щелкните **GO TO** (Перейти), а затем — **ADDRESS BOOK** (Адресная книга).
   
    ![Создание пользователя](./media/active-directory-saas-spring-cm-tutorial/ic797054.png "Создание пользователя")

3. Щелкните **Создать пользователя**.

4. Выберите **роль пользователя**.

5. Установите флажок **Отправить сообщение для активации**.

6. Тип hello имя, фамилию и адрес электронной почты действующей учетной записи Azure Active Directory, требуется tooprovision в hello связанные текстовые поля.

7. Добавить пользователя tooa hello **группы безопасности**.

8. Щелкните **Сохранить**.

  >[!NOTE]
  >Можно использовать любые другие SpringCM пользователя средства создания учетных записей или интерфейсы API, предоставляемые SpringCM tooprovision учетных записей пользователей AAD.  
  > 

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooSpringCM доступа.

![Назначение пользователя][200] 

**tooassign tooSpringCM Britta Simon выполните следующие шаги hello.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **SpringCM**.

    ![Настройка единого входа](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.
 
При нажатии кнопки hello SpringCM плитки в панели доступа hello, вы должны получить tooyour автоматически подписан на SpringCM приложения.

Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_203.png

