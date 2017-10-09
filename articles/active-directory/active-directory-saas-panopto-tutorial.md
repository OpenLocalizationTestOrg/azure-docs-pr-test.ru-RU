---
title: "Руководство по интеграции Azure Active Directory с Panopto | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory с Panopto."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 89c88e23-93ce-4970-9baa-1104c4e8fe4a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 76b30e1cd2782bb5fba3d229378b8f82652b6503
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-panopto"></a>Учебник. Интеграция Azure Active Directory с Panopto

В этом учебнике вы узнаете, как toointegrate Panopto с Azure Active Directory (Azure AD).

Интеграция Panopto с Azure AD предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooPanopto
- Можно включить на пользователей tooautomatically get вошедшего tooPanopto (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с Panopto требуется hello следующих элементов:

- подписка Azure AD;
- подписка Panopto с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление Panopto из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-panopto-from-hello-gallery"></a>Добавление Panopto из галереи hello
tooconfigure hello интеграции Panopto в Azure AD, вы должны tooadd Panopto из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd Panopto из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Приложения][3]

4. Введите в поле поиска hello **Panopto**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_search.png)

5. В панели результатов hello выберите **Panopto**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD

В этом разделе описана настройка и проверка единого входа Azure AD в Panopto с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Panopto является tooa в Azure AD. Другими словами связи между пользователя Azure AD и hello связанных пользователей в Panopto должен установить toobe.

В Panopto, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.

tooconfigure и теста Azure AD единого входа с Panopto, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя Panopto](#creating-a-panopto-test-user)**  -toohave аналог Саймон Britta в Panopto, который представляет связанный toohello Azure AD пользователя.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в Panopto приложения.

**Azure AD tooconfigure единого входа с Panopto, выполните следующие шаги hello.**

1. В hello в hello портала Azure **Panopto** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_samlbase.png)

3. На hello **URL-адреса и домена Panopto** выполните следующие шаги hello:

    ![Настройка единого входа](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_url.png)

    В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<tenant-name>.panopto.com`

    > [!NOTE] 
    > Это значение приведено для справки. Измените значение этого параметра hello фактический URL-адрес входа. Обратитесь к [группа поддержки клиент Panopto](mailto:support@panopto.com‎) tooget это значение. 
 
4. На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.

    ![Настройка единого входа](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-panopto-tutorial/tutorial_general_400.png)

6. На hello **конфигурации Panopto** щелкните **Настройка Panopto** tooopen **Настройка входа** окна. Копировать hello **идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**

    ![Настройка единого входа](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_configure.png) 

7. В другом окне браузера войти в корпоративный сайт Panopto tooyour с правами администратора.

8. Щелкните hello панели инструментов слева hello **системы**и нажмите кнопку **Поставщики удостоверений**.
   
   ![Система](./media/active-directory-saas-panopto-tutorial/ic777670.png "Система")
9. Щелкните **Добавить поставщик**.
   
   ![Поставщики удостоверений](./media/active-directory-saas-panopto-tutorial/ic777671.png "Поставщики удостоверений")
   
10. В hello разделе поставщика SAML выполните следующие шаги hello.
   
    ![Конфигурация SaaS](./media/active-directory-saas-panopto-tutorial/ic777672.png "Конфигурация SaaS")
    
    а. Из hello **тип поставщика** выберите **SAML20**.    
    
    b. В hello **имя экземпляра** в текстовое поле введите имя для экземпляра hello.

    c. В hello **понятное описание** текстовом поле введите понятное описание.
    
    d. В **URL-адрес страницы возврата** текстовое значение hello вставить **SAML единого входа URL-адрес службы**, который вы скопировали из портала Azure.

    д. В hello **издателя** текстовое значение hello вставить **SAML идентификатор сущности**, который вы скопировали из портала Azure.

    f. Откройте base-64 сертификат в кодировке, который вы скачали из содержимого его в буфер обмена tooyour Azure hello портала, копировать, а затем вставьте его toohello **открытый ключ** текстового поля.

11. Щелкните **Сохранить**.

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD

Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-panopto-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-panopto-tutorial/create_aaduser_02.png) 

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-panopto-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-panopto-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-a-panopto-test-user"></a>Создание тестового пользователя приложения Panopto

Нет элемента действия для вас tooconfigure подготовки пользователей tooPanopto.  
Когда назначенный пользователь пытается toolog в tooPanopto, с помощью панели доступа hello, Panopto проверяет, существует ли пользователь hello.  

Если учетная запись пользователя отсутствует, Panopto автоматически создает ее.

>[!NOTE]
>Можно использовать любые другие Panopto пользователя средства создания учетных записей или API, предоставленные Panopto tooprovision учетных записей пользователей Azure AD.
>
>

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooPanopto доступа.

![Назначение пользователя][200] 

**tooassign tooPanopto Britta Simon выполните следующие шаги hello.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **Panopto**.

    ![Настройка единого входа](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.

Если щелкнуть плитку Panopto hello в hello панели доступа, следует получать автоматически страницы входа в Panopto приложения.
Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_203.png

