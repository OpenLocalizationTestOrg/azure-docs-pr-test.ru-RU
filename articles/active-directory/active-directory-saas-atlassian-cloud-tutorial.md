---
title: "Руководство по интеграции Azure Active Directory с Atlassian Cloud | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и облаком Atlassian."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 729b8eb6-efc4-47fb-9f34-8998ca2c9545
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: f679e8b3306bf0efb9373d8baa0cfe095b760aaf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-atlassian-cloud"></a>Руководство по интеграции Azure Active Directory с Atlassian Cloud

В этом учебнике вы узнаете, как toointegrate Atlassian облака в Azure Active Directory (Azure AD).

Интеграция с Azure AD облака Atlassian предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooAtlassian облака
- Можно включить на пользователей tooautomatically get вошедшего tooAtlassian облака (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с облаком Atlassian требуется hello следующих элементов:

- подписка Azure AD;
- подписка Atlassian Cloud с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление Atlassian облака из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-atlassian-cloud-from-hello-gallery"></a>Добавление Atlassian облака из галереи hello
tooconfigure hello интеграция Atlassian облака в Azure AD, вы должны tooadd Atlassian облако из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd Atlassian облака из галереи hello выполните hello следующие шаги.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Приложения][3]

4. Введите в поле поиска hello **Atlassian облака**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_search.png)

5. В панели результатов hello, выберите **облака Atlassian**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в Atlassian Cloud с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в облаке Atlassian является tooa в Azure AD. Другими словами связи между пользователя Azure AD и hello связанных пользователей в облаке Atlassian должен установить toobe.

Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в облаке Atlassian.

tooconfigure и тестирования Azure AD единого входа с облаком Atlassian, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя, прошедшего облака Atlassian](#creating-an-atlassian-cloud-test-user)**  -toohave аналог Саймон Britta в облаке Atlassian, представление связанных toohello Azure AD пользователя.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в Atlassian облачного приложения.

**tooconfigure Azure AD единого входа с облаком Atlassian выполните следующие шаги hello.**

1. В hello в hello портала Azure **облака Atlassian** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_samlbase.png)

3. На hello **Atlassian облака домена и URL-адреса** выполните hello, выполните действия, при желании tooconfigure приложения hello в **IDP** инициировал режим:

    ![Настройка единого входа](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_url.png)

    а. В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<instancename>.atlassian.net/admin/saml/edit`

    b. В hello **URL-адрес ответа** текстовом поле введите URL-адрес как:`https://id.atlassian.com/login/saml/acs`

4. Проверьте **Показывать дополнительные параметры URL-адреса** и выполните следующий шаг при желании tooconfigure приложения hello в hello **SP** инициировал режим:

    ![Настройка единого входа](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_url1.png)

    В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<instancename>.atlassian.net`

    > [!NOTE] 
    > Эти значения приведены в качестве примера. Обновить значения hello фактический идентификатор и URL-адрес входа. Hello точные значения можно получить из конфигурации SAML облака Atlassian экрана.
 
5. На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.

    ![Настройка единого входа](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_certificate.png) 

6. На hello **конфигурации облака Atlassian** щелкните **Настройка облака Atlassian** tooopen **Настройка входа** окна. Копировать hello **идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**

    ![Настройка единого входа](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_configure.png) 

7. tooget SSO настроен для вашего приложения, toohello входа Atlassian портал, используя права администратора hello.

8. В разделе проверки подлинности hello hello навигации слева щелкните **домены**.

    ![Настройка единого входа](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_06.png)

    а. В текстовом поле «hello» введите имя домена и нажмите кнопку **добавить домен**.
        
    ![Настройка единого входа](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_07.png)

    b. tooverify hello домена, нажмите кнопку **проверьте**. 

    ![Настройка единого входа](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_08.png)

    c. Загрузить файл html проверки домена hello, отправьте его в корневую папку toohello вашего домена веб-сайта и нажмите кнопку **Проверка домена**.
    
    ![Настройка единого входа](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_09.png)

    d. После проверки домена hello hello значение hello **состояние** поле является **проверено**.

    ![Настройка единого входа](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_10.png)

9. В левой навигационной панели hello, щелкните **SAML**.
 
    ![Настройка единого входа](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_11.png)

10. Создание конфигурации SAML и добавление hello конфигурация поставщика удостоверений.

    ![Настройка единого входа](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_12.png)

    а. В hello **поставщика удостоверений идентификатор сущности** текстовое поле, вставить значение hello **идентификатор сущности SAML** скопирован из портала Azure.

    b. В hello **поставщика удостоверений URL-адрес SSO** текстовое поле, вставить значение hello **SAML единого входа URL-адрес службы** скопирован из портала Azure.

    c. Откройте сертификат hello загружаются из Azure portal и скопировать значения hello без hello начало и конец строки и вставьте его в hello **X509 открытый сертификат** поле.
    
    d. Нажмите кнопку **сохранить конфигурацию** tooSave hello параметры.
     
11. Обновите hello Azure AD параметры toomake наличие установки hello исправьте идентификатор URL-адрес.
  
    а. Копировать hello **идентификатор удостоверений SP** hello SAML экране и вставьте его в Azure AD в качестве hello **идентификатор** значение.

    b. На URL-адрес входа — URL-адрес клиента hello Atlassian облака.     

     ![Настройка единого входа](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_13.png)
    
12. В hello портал Azure, щелкните **Сохранить** кнопки.

    ![Настройка единого входа](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_400.png)

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_02.png) 

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-an-atlassian-cloud-test-user"></a>Создание тестового пользователя Atlassian Cloud

Пользователи toolog tooenable Azure AD в tooAtlassian облака, их необходимо подготовить в облаке Atlassian.  
В случае Atlassian Cloud подготовка выполняется вручную.

**tooprovision учетной записи пользователя, выполните следующие шаги hello.**

1. В hello раздел администрирования сайта щелкните hello **пользователей** кнопки

    ![Создание пользователя Atlassian Cloud](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_14.png) 

2. Нажмите кнопку hello **Create User** кнопку toocreate пользователя в hello Atlassian облака

    ![Создание пользователя Atlassian Cloud](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_15.png) 

3. Введите пользователя hello **адрес электронной почты**, **Username**, и **полное имя** и назначить доступ приложения hello. 

    ![Создание пользователя Atlassian Cloud](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_16.png)
 
4. Нажмите кнопку **создать пользователя** кнопка, он отправляет приглашение toohello hello электронной почты пользователя и после принятия hello приглашения hello пользователя будет активным в системе hello. 

>[!NOTE] 
>Можно также создать hello массового пользователей, щелкнув hello **массового создания** кнопку в разделе "пользователи" hello.

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooAtlassian облака.

![Назначение пользователя][200] 

**tooassign tooAtlassian Britta Simon облака, выполните hello следующие шаги.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **Atlassian облака**.

    ![Настройка единого входа](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

В этом разделе Проверьте конфигурацию единого входа Azure AD с помощью панели доступа hello.

При нажатии кнопки hello облака Atlassian плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour Atlassian облачного приложения. Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_203.png

