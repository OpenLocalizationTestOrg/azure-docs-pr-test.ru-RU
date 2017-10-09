---
title: "Руководство по интеграции Azure Active Directory с ITRP | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и ITRP."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e09716a3-4200-4853-9414-2390e6c10d98
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: 35463a55fcfc1e55c90700737961c1ff2e58992a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-itrp"></a>Руководство по интеграции Azure Active Directory с ITRP

В этом учебнике вы узнаете, как toointegrate ITRP с Azure Active Directory (Azure AD).

Интеграция ITRP с Azure AD предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooITRP
- Можно включить на пользователей tooautomatically get вошедшего tooITRP (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с ITRP требуется hello следующих элементов:

- подписка Azure AD;
- подписка ITRP с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление ITRP из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-itrp-from-hello-gallery"></a>Добавление ITRP из галереи hello
tooconfigure hello интеграции ITRP в tooAzure AD, вы должны tooadd ITRP из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd ITRP из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Приложения][3]

4. Введите в поле поиска hello **ITRP**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_search.png)

5. В панели результатов hello выберите **ITRP**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD

В этом разделе описана настройка и проверка единого входа Azure AD в приложение ITRP с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в ITRP является tooa в Azure AD. Другими словами связи между пользователя Azure AD и hello связанных пользователей в ITRP требуется toobe установлено.

В ITRP, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.

tooconfigure и теста Azure AD единого входа с ITRP, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание ITRP тестовый пользователь](#creating-an-itrp-test-user)**  -toohave аналог Саймон Britta в ITRP, который представляет связанный toohello Azure AD пользователя.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе вы включите Azure AD единым входом в портал Azure hello и настройки единого входа в ITRP приложения.

**tooconfigure Azure AD единого входа с ITRP, выполните следующие шаги hello.**

1. В hello в hello портала Azure **ITRP** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_samlbase.png)

3. На hello **URL-адреса и домена ITRP** выполните следующие шаги hello:

    ![Настройка единого входа](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_url.png)

    а. В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<tenant-name>.itrp.com`

    b. В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<tenant-name>.itrp.com`

    > [!NOTE] 
    > Эти значения приведены в качестве примера. Обновить значения hello фактический URL-адрес входа и идентификатор. Обратитесь к [группа поддержки клиент ITRP](https://www.itrp.com/support) tooget эти значения. 
 
4. На hello **сертификат подписи SAML** раздел, hello копирования **ОТПЕЧАТОК** значение сертификата.

    ![Настройка единого входа](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-itrp-tutorial/tutorial_general_400.png)

6. На hello **конфигурации ITRP** щелкните **Настройка ITRP** tooopen **Настройка входа** окна. Копировать hello **SAML единого входа URL-адрес службы и URL-адрес выхода** из hello **краткий справочник.**

    ![Настройка единого входа](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_configure.png) 

7. В другом окне браузера войти в корпоративный сайт ITRP tooyour с правами администратора.

8. Щелкните hello панели инструментов в верхней части hello **параметры**.
   
    ![ITRP](./media/active-directory-saas-itrp-tutorial/ic775570.png "ITRP")

8. В области навигации слева hello выберите **Single Sign-On**.
   
    ![Единый вход](./media/active-directory-saas-itrp-tutorial/ic775571.png "Единый вход")

9. В hello единым входом раздел конфигурации выполните следующие шаги hello.
   
    ![Единый вход](./media/active-directory-saas-itrp-tutorial/ic775572.png "Единый вход")
    
    ![Единый вход](./media/active-directory-saas-itrp-tutorial/ic775573.png "Единый вход")   

    а. Нажмите **Включить**.

    b. В **журнала ожидания URL-адрес удаленного** текстовое значение hello вставить **URL-адрес выхода**, который вы скопировали из портала Azure.

    c. В **URL-адрес единого входа SAML** текстовое значение hello вставить **SAML единого входа URL-адрес службы**, который вы скопировали из портала Azure.

    d.In **отпечаток сертификата** текстовое поле, вставить hello **отпечаток** значение сертификат, который вы скопировали из портала Azure. 
      
10. Щелкните **Сохранить**.

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-itrp-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-itrp-tutorial/create_aaduser_02.png) 

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-itrp-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-itrp-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-an-itrp-test-user"></a>Создание тестового пользователя ITRP

Пользователи toolog tooenable Azure AD в tooITRP, их необходимо подготовить в tooITRP.  

В случае hello объекта ITRP Подготовка выполняется вручную.

**tooprovision учетной записи пользователя, выполните следующие шаги hello.**

1. Войдите в tooyour **ITRP** клиента.

2. Щелкните hello панели инструментов в верхней части hello **записи**.
   
    ![Администратор](./media/active-directory-saas-itrp-tutorial/ic775575.png "Администратор")

3. Hello всплывающего меню, выберите **людей**.
   
    ![Люди](./media/active-directory-saas-itrp-tutorial/ic775587.png "Люди")

4. Нажмите **Добавить пользователя** ("+").
   
    ![Администратор](./media/active-directory-saas-itrp-tutorial/ic775576.png "Администратор")

5. В диалоговом окне добавления человека hello выполните следующие шаги hello.
   
    ![Пользователь](./media/active-directory-saas-itrp-tutorial/ic775577.png "Пользователь") 
      
    а. Тип hello **имя**, **электронной почты** действительной учетной записи AAD, вы хотите tooprovision.

    b. Щелкните **Сохранить**.

>[!NOTE]
>Можно использовать любые другие ITRP пользователя средства создания учетных записей или интерфейсы API, предоставляемые ITRP tooprovision учетных записей пользователей AAD. 
> 

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooITRP доступа.

![Назначение пользователя][200] 

**tooassign tooITRP Britta Simon выполните следующие шаги hello.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **ITRP**.

    ![Настройка единого входа](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.

При нажатии кнопки ITRP плитки в панели доступа hello hello, вы должны получить автоматически вошедшего tooyour ITRP приложения.
Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_203.png

