---
title: "Руководство по интеграции Azure Active Directory с SugarCRM | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Sugar CRM."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3331b9fc-ebc0-4a3a-9f7b-bf20ee35d180
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: jeedes
ms.openlocfilehash: 108d2f8125e410743ee7bc48883a1d0b00602615
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sugar-crm"></a>Руководство по интеграции Azure Active Directory с SugarCRM

В этом учебнике вы узнаете, как toointegrate Sugar CRM с Azure Active Directory (Azure AD).

Интеграция Sugar CRM с Azure AD предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooSugar CRM
- Можно включить на пользователей tooautomatically get вошедшего tooSugar CRM (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с Sugar CRM требуется hello следующих элементов:

- подписка Azure AD;
- Подписка SugarCRM с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление Sugar CRM из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-sugar-crm-from-hello-gallery"></a>Добавление Sugar CRM из галереи hello
tooconfigure hello интеграции Sugar CRM в Azure AD, вы должны tooadd Sugar CRM из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd Sugar CRM из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Приложения][3]

4. Введите в поле поиска hello **Sugar CRM**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_search.png)

5. В панели результатов hello выберите **Sugar CRM**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в SugarCRM с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователя аналог hello в Sugar CRM — tooa пользователя в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в Sugar CRM должен установить toobe.

В Sugar CRM, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.

tooconfigure и теста Azure AD единого входа с Sugar CRM, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя Sugar CRM](#creating-a-sugar-crm-test-user)**  -toohave аналог Саймон Britta в Sugar CRM, представление связанных toohello Azure AD пользователя.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложение Sugar CRM.

**tooconfigure Azure AD единого входа с Sugar CRM, выполните следующие шаги hello.**

1. В hello в hello портала Azure **Sugar CRM** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_samlbase.png)

3. На hello **URL-адреса и домена Sugar CRM** выполните следующие шаги hello:

    ![Настройка единого входа](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_url.png)

    В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:
    | |
    |--|
    | `https://<companyname>.sugarondemand.com` |
    | `https://<companyname>.trial.sugarcrm` |

    > [!NOTE] 
    > значение Hello не является вещественным числом. Значение hello обновления с hello фактический URL-адрес входа. Обратитесь к [группа поддержки клиент Sugar CRM](https://support.sugarcrm.com/) tooget значение hello. 
 
4. На hello **сертификат подписи SAML** щелкните **сертификата (Base64)** и затем сохраните файл сертификата hello на вашем компьютере.

    ![Настройка единого входа](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_400.png)

6. На hello **конфигурации Sugar CRM** щелкните **Настройка Sugar CRM** tooopen **Настройка входа** окна. Копировать hello **URL-адрес выхода и SAML единого входа URL-адрес службы** из hello **краткий справочник.**

    ![Настройка единого входа](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_configure.png) 

7. В другом окне браузера Войдите на сайте компании Sugar CRM tooyour в качестве администратора.

8. Go слишком**администратора**.
   
    ![Администратор](./media/active-directory-saas-sugarcrm-tutorial/ic795888.png "Администратор")

9. В hello **администрирования** щелкните **управления паролями**.
   
    ![Администрирование](./media/active-directory-saas-sugarcrm-tutorial/ic795889.png "Администрирование")

10. Установите флажок **Включить проверку подлинности SAML**.
   
    ![Администрирование](./media/active-directory-saas-sugarcrm-tutorial/ic795890.png "Администрирование")

11. В hello **проверку подлинности SAML** выполните следующие шаги hello:
   
    ![Аутентификация SAML](./media/active-directory-saas-sugarcrm-tutorial/ic795891.png "Аутентификация SAML")  
 
    а. В hello **URL-адрес входа** текстовое значение hello вставить **SAML единого входа URL-адрес службы**, который вы скопировали из портала Azure.
  
    b. В hello **URL-адрес SLO** текстовое значение hello вставить **URL-адрес выхода**, который вы скопировали из портала Azure.
  
    c. Откройте сертификат в кодировке base-64 в блокноте, hello копирования содержимого его в буфер обмена, а затем вставьте весь сертификат в hello **сертификат X.509** текстового поля.
  
    d. Щелкните **Сохранить**.

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sugarcrm-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sugarcrm-tutorial/create_aaduser_02.png) 

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sugarcrm-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sugarcrm-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-a-sugar-crm-test-user"></a>Создание тестового пользователя SugarCRM

В порядке tooenable toolog пользователей Azure AD в tooSugar CRM они должны быть подготовленных tooSugar CRM.

В случае hello Sugar CRM Подготовка выполняется вручную.

**tooprovision учетной записи пользователя, выполните следующие шаги hello.**

1. Войдите в tooyour **Sugar CRM** сайт компании от имени администратора.

2. Go слишком**администратора**.
   
    ![Администратор](./media/active-directory-saas-sugarcrm-tutorial/ic795888.png "Администратор")

3. В hello **администрирования** щелкните **Управление пользователями**.
   
    ![Администрирование](./media/active-directory-saas-sugarcrm-tutorial/ic795893.png "Администрирование")

4. Go слишком**пользователей \> создать нового пользователя**.
   
    ![Создание пользователя](./media/active-directory-saas-sugarcrm-tutorial/ic795894.png "Создание пользователя")

5. На hello **профиля пользователя** выполните следующие шаги hello:
   
    ![Новый пользователь](./media/active-directory-saas-sugarcrm-tutorial/ic795895.png "Новый пользователь")

    а. Тип hello **имя пользователя**, **Фамилия**, и **адрес электронной почты** действительного пользователя Azure Active Directory в hello связанные текстовые поля.
  
6. Для параметра **Status** (Состояние) выберите значение **Active** (Активно).

7. На вкладку "пароль" hello выполните следующие шаги hello.
   
    ![Новый пользователь](./media/active-directory-saas-sugarcrm-tutorial/ic795896.png "Новый пользователь")

    а. Введите пароль hello в hello, связанные с текстового поля.

    b. Щелкните **Сохранить**.

>[!NOTE]
>Можно использовать любые другие Sugar CRM пользователя средства создания учетных записей или интерфейсы API, предоставляемые Sugar CRM tooprovision учетных записей пользователей AAD. 
> 

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooSugar CRM.

![Назначение пользователя][200] 

**tooassign tooSugar Britta Simon CRM, выполните hello следующие шаги.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **Sugar CRM**.

    ![Настройка единого входа](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

Цель этого раздела Hello является tootest настройки единого входа Azure AD с помощью панели доступа "hello".

При выборе плитки Sugar CRM hello в hello панели доступа, следует получать автоматически вошедшего tooyour приложение Sugar CRM.

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_203.png

