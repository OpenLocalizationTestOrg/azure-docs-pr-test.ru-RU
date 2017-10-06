---
title: "Руководство по интеграции Azure Active Directory с SumoLogic | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и SumoLogic."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: fbb76765-92d7-4801-9833-573b11b4d910
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 2ef1bd329f5db8899f0b57744e4c0f6eed1c532f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sumologic"></a>Руководство. Интеграция Azure Active Directory с SumoLogic

В этом учебнике вы узнаете, как toointegrate SumoLogic с Azure Active Directory (Azure AD).

Интеграция SumoLogic с Azure AD предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooSumoLogic
- Можно включить на пользователей tooautomatically get вошедшего tooSumoLogic (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с SumoLogic требуется hello следующих элементов:

- подписка Azure AD;
- подписка с поддержкой единого входа SumoLogic.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление SumoLogic из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-sumologic-from-hello-gallery"></a>Добавление SumoLogic из галереи hello
tooconfigure hello интеграции SumoLogic в Azure AD, вы должны tooadd SumoLogic из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd SumoLogic из галереи hello, выполните следующие шаги hello.**

1. В hello ** [портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Приложения][3]

4. Введите в поле поиска hello **SumoLogic**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_search.png)

5. В панели результатов hello выберите **SumoLogic**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в SumoLogic с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в SumoLogic является tooa в Azure AD. Другими словами связи между пользователя Azure AD и hello связанных пользователей в SumoLogic должен установить toobe.

В SumoLogic, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.

tooconfigure и теста Azure AD единого входа с SumoLogic, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on) ** -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user) ** -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя SumoLogic](#creating-a-sumologic-test-user) ** -toohave аналог Саймон Britta в SumoLogic, который представляет связанный toohello Azure AD пользователя.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on) ** -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в SumoLogic приложения.

**Azure AD tooconfigure единого входа с SumoLogic, выполните следующие шаги hello.**

1. В hello в hello портала Azure **SumoLogic** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_samlbase.png)

3. На hello **URL-адреса и домена SumoLogic** выполните следующие шаги hello:

    ![Настройка единого входа](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_url.png)

    а. В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<tenantname>.SumoLogic.com`

    b. В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:
    | |
    |--|
    | `https://<tenantname>.us2.sumologic.com` |
    | `https://<tenantname>.sumologic.com` |
    | `https://<tenantname>.us4.sumologic.com` |
    | `https://<tenantname>.eu.sumologic.com` |
    | `https://<tenantname>.au.sumologic.com` |

    > [!NOTE] 
    > Эти значения приведены в качестве примера. Обновить значения hello фактический URL-адрес входа и идентификатор. Обратитесь к [группа поддержки клиент SumoLogic](https://www.sumologic.com/contact-us/) tooget эти значения. 
 
4. На hello **сертификат подписи SAML** щелкните **сертификата (Base64)** и затем сохраните файл сертификата hello на вашем компьютере.

    ![Настройка единого входа](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-sumologic-tutorial/tutorial_general_400.png)

6. На hello **конфигурации SumoLogic** щелкните **Настройка SumoLogic** tooopen **Настройка входа** окна. Копировать hello **идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**

    ![Настройка единого входа](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_configure.png) 

7. В другом окне браузера Войдите на сайте компании SumoLogic tooyour в качестве администратора.

8. Go слишком**управление \> безопасности**.
   
    ![Управление](./media/active-directory-saas-sumologic-tutorial/ic778556.png "Управление")

9. Нажмите кнопку **SAML**.
   
    ![Глобальные параметры безопасности](./media/active-directory-saas-sumologic-tutorial/ic778557.png "Глобальные параметры безопасности")

10. Из hello **выберите настройку или создайте новую** выберите **Azure AD**, а затем нажмите кнопку **Настройка**.
   
    ![Настройка SAML 2.0](./media/active-directory-saas-sumologic-tutorial/ic778558.png "Настройка SAML 2.0")

11. На hello **Настройка SAML 2.0** диалоговое окно, выполните следующие шаги hello:
   
    ![Настройка SAML 2.0](./media/active-directory-saas-sumologic-tutorial/ic778559.png "Настройка SAML 2.0")
   
    а. В hello **имя конфигурации** введите **Azure AD**. 

    b. Выберите **Режим отладки**.

    c. В hello **издателя** текстовое значение hello вставить **SAML идентификатор сущности**, который вы скопировали из портала Azure. 

    d. В hello **URL-адрес запроса Authn** текстовое значение hello вставить **SAML единого входа URL-адрес службы**, который вы скопировали из портала Azure.

    д. Откройте сертификат в кодировке base-64 в блокноте, hello копирования содержимого его в буфер обмена, а затем вставьте весь сертификат в hello **сертификат X.509** текстового поля.

    f. В поле **Email Attribute** (Атрибут электронной почты) задайте значение **Use SAML subject** (Использовать субъект SAML).  

    g. Выберите пункт **Конфигурация входа, инициируемая поставщиком услуг**.

    h. В hello **путь входа** введите **Azure** и нажмите кнопку **Сохранить**.

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello ** Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sumologic-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sumologic-tutorial/create_aaduser_02.png) 

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sumologic-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sumologic-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-a-sumologic-test-user"></a>Создание тестового пользователя SumoLogic

В порядке tooenable toolog пользователей Azure AD в tooSumoLogic они должны быть подготовленных tooSumoLogic.  

* В случае SumoLogic hello Подготовка выполняется вручную.

**tooprovision учетной записи пользователя, выполните следующие шаги hello.**

1. Войдите в tooyour **SumoLogic** клиента.

2. Go слишком**управление \> пользователей**.
   
    ![Пользователи](./media/active-directory-saas-sumologic-tutorial/ic778561.png "Пользователи")

3. Щелкните **Добавить**.
   
    ![Пользователи](./media/active-directory-saas-sumologic-tutorial/ic778562.png "Пользователи")

4. На hello **нового пользователя** диалоговое окно, выполните следующие шаги hello:
   
    ![Новый пользователь](./media/active-directory-saas-sumologic-tutorial/ic778563.png "Новый пользователь") 
 
    а. Тип hello связанные данные для учетной записи hello Azure AD, которые должны tooprovision hello **имя**, **Фамилия**, и **электронной почты** текстовые поля.
  
    b. Выберите роль.
  
    c. Для параметра **Status** (Состояние) выберите значение **Active** (Активно).
  
    d. Щелкните **Сохранить**.

>[!NOTE]
>Можно использовать любые другие SumoLogic пользователя средства создания учетных записей или API, предоставленные SumoLogic tooprovision учетных записей пользователей AAD. 
> 

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooSumoLogic доступа.

![Назначение пользователя][200] 

**tooassign tooSumoLogic Britta Simon выполните следующие шаги hello.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **SumoLogic**.

    ![Настройка единого входа](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

Цель этого раздела Hello является tootest настройки единого входа Azure AD с помощью панели доступа "hello".

При нажатии кнопки hello SumoLogic плитки в панели доступа hello, вы должны получить приложение автоматически вошедшего tooyour SumoLogic.

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_203.png

