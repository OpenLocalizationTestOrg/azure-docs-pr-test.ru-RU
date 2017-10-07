---
title: "Учебник. Интеграция Azure Active Directory с Freshservice | Документы Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Freshservice."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3dd22b1f-445d-45c6-8eda-30207eb9a1a8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: d73624b87d058f66885ae72fda69a0aacc89c1ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-freshservice"></a>Учебник. Интеграция Azure Active Directory с FreshService

В этом учебнике вы узнаете, как toointegrate Freshservice с Azure Active Directory (Azure AD).

Интеграция Freshservice с Azure AD предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooFreshservice
- Можно включить на пользователей tooautomatically get вошедшего tooFreshservice (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с Freshservice требуется hello следующих элементов:

- подписка Azure AD;
- подписка Freshservice с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление Freshservice из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-freshservice-from-hello-gallery"></a>Добавление Freshservice из галереи hello
tooconfigure hello интеграции Freshservice в Azure AD, вы должны tooadd Freshservice из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd Freshservice из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Приложения][3]

4. Введите в поле поиска hello **Freshservice**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_search.png)

5. В панели результатов hello выберите **Freshservice**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD во Freshservice с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Freshservice является tooa в Azure AD. Другими словами связи между пользователя Azure AD и hello связанных пользователей в Freshservice должен установить toobe.

В Freshservice, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.

tooconfigure и теста Azure AD единого входа с Freshservice, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя Freshservice](#creating-a-freshservice-test-user)**  -toohave аналог Саймон Britta в Freshservice, который представляет связанный toohello Azure AD пользователя.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в ваше приложение Freshservice.

**tooconfigure Azure AD единого входа с Freshservice, выполните следующие шаги hello.**

1. В hello в hello портала Azure **Freshservice** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_samlbase.png)

3. На hello **URL-адреса и домена Freshservice** выполните следующие шаги hello:

    ![Настройка единого входа](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_url.png)

    а. В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<democompany>.freshservice.com`

    b. В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<democompany>.freshservice.com`

    > [!NOTE] 
    > Эти значения приведены в качестве примера. Обновить значения hello фактический URL-адрес входа и идентификатор. Обратитесь к [группа поддержки клиента Freshservice](https://support.freshservice.com/) tooget эти значения. 
 
4. На hello **сертификат подписи SAML** скопируйте **ОТПЕЧАТОК** значение сертификата.

    ![Настройка единого входа](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-freshservice-tutorial/tutorial_general_400.png)

6. На hello **конфигурации Freshservice** щелкните **Настройка Freshservice** tooopen **Настройка входа** окна. Копировать hello **URL-адрес выхода и SAML единого входа URL-адрес службы** из hello **краткий справочник.**

    ![Настройка единого входа](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_configure.png) 

7. В другом окне браузера войти в корпоративный сайт Freshservice tooyour с правами администратора.

8. В меню в верхней части hello hello выберите **администратора**.
   
    ![Администратор](./media/active-directory-saas-freshservice-tutorial/ic790814.png "Администратор")

9. В hello **портал клиента**, нажмите кнопку **безопасности**.
   
    ![Безопасность](./media/active-directory-saas-freshservice-tutorial/ic790815.png "Безопасность")

10. В hello **безопасности** выполните следующие шаги hello:
   
    ![Единый вход](./media/active-directory-saas-freshservice-tutorial/ic790816.png "Единый вход")
   
    а. Включите **единый вход**.

    b. Выберите **Единый вход SAML**.

    c. В hello **URL-адрес входа SAML** текстовое значение hello вставить **SAML единого входа URL-адрес службы** скопирован из портала Azure.

    d. В hello **URL-адрес выхода** текстовое значение hello вставить **URL-адрес выхода** скопирован из портала Azure.

    д. В **отпечаток сертификата безопасности** текстовое поле, вставить hello **ОТПЕЧАТОК** значение сертификата, который вы скопировали из портала Azure.

    f. Нажмите кнопку **Сохранить**
   
> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-freshservice-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-freshservice-tutorial/create_aaduser_02.png) 

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-freshservice-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-freshservice-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-a-freshservice-test-user"></a>Создание тестового пользователя Freshservice

Пользователи toolog tooenable Azure AD в tooFreshService, их необходимо подготовить во FreshService. В случае FreshService hello Подготовка выполняется вручную.

**tooprovision учетной записи пользователя, выполните следующие шаги hello.**

1. Войдите в tooyour **FreshService** сайт компании от имени администратора.

2. В меню в верхней части hello hello выберите **администратора**.
   
    ![Администратор](./media/active-directory-saas-freshservice-tutorial/ic790814.png "Администратор")

3. В hello **Управление пользователями** щелкните **инициаторы запроса**.
   
    ![Инициатор запроса](./media/active-directory-saas-freshservice-tutorial/ic790818.png "Инициатор запроса")

4. Нажмите **Новый инициатор запроса**.
   
    ![Создание инициаторов запроса](./media/active-directory-saas-freshservice-tutorial/ic790819.png "Создание инициаторов запроса")

5. В hello **новый инициатор запроса** выполните следующие шаги hello:
   
    ![Создание инициатора запроса](./media/active-directory-saas-freshservice-tutorial/ic790820.png "Создание инициатора запроса")   

    а. Введите hello **имя** и **электронной почты** атрибуты действительной учетной записи Azure Active Directory, которые должны tooprovision hello связаны текстовые поля.

    b. Щелкните **Сохранить**.
   
    >[!NOTE]
    >Владелец учетной записи Azure Active Directory Hello получает сообщение электронной почты, включая учетную запись hello tooconfirm ссылку, чтобы она стала активной
    >  

>[!NOTE]
>Можно использовать любые другие FreshService пользователя средства создания учетных записей или интерфейсы API, предоставляемые FreshService tooprovision учетных записей пользователей AAD.
>  

![Назначение пользователя][200] 

**tooassign tooFreshservice Britta Simon выполните следующие шаги hello.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **Freshservice**.

    ![Настройка единого входа](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

Цель этого раздела Hello является tootest настройки единого входа Azure AD с помощью панели доступа "hello".

При нажатии кнопки hello Freshservice плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour Freshservice приложения.

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_203.png

