---
title: "Руководство по интеграции Azure Active Directory с TargetProcess | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и TargetProcess."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 7cb91628-e758-480d-a233-7a3caaaff50d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 05c574e2c18d7f73edc6c094093a6e59d46b8e6b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-targetprocess"></a>Руководство. Интеграция Azure Active Directory с TargetProcess

В этом учебнике вы узнаете, как toointegrate TargetProcess с Azure Active Directory (Azure AD).

Интеграция с Azure AD TargetProcess предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooTargetProcess
- Можно включить на пользователей tooautomatically get вошедшего tooTargetProcess (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с TargetProcess требуется hello следующих элементов:

- подписка Azure AD;
- подписка TargetProcess с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление TargetProcess из коллекции hello
2. Настройка и проверка единого входа в Azure AD

## <a name="add-targetprocess-from-hello-gallery"></a>Добавление TargetProcess из коллекции hello
tooconfigure hello интеграции TargetProcess в Azure AD, вы должны tooadd TargetProcess из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd TargetProcess из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Приложения][3]

4. Введите в поле поиска hello **TargetProcess**выберите **TargetProcess** из панели результатов щелкните **добавить** кнопку tooadd приложения hello.

    ![Добавление TargetProcess из коллекции](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в TargetProcess с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в TargetProcess является tooa в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в TargetProcess должен установить toobe.

В TargetProcess, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.

tooconfigure и теста Azure AD единого входа с TargetProcess, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя TargetProcess](#create-a-targetprocess-test-user)**  -toohave аналог Саймон Britta в TargetProcess, который представляет связанный toohello Azure AD пользователя.
4. **[Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#test-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configure-azure-ad-single-sign-on"></a>Настройка единого входа Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении TargetProcess.

**tooconfigure Azure AD единого входа с TargetProcess, выполните следующие шаги hello.**

1. В hello в hello портала Azure **TargetProcess** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Параметр "Вход на основе SAML"](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_samlbase.png)

3. На hello **URL-адреса и домена TargetProcess** выполните следующие шаги hello:

    ![Раздел "Домены и URL-адреса приложения TargetProcess"](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_url.png)

    а. В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<subdomain>.tpondemand.com/`

    b. В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<subdomain>.tpondemand.com/`

    > [!NOTE] 
    > Эти значения приведены в качестве примера. Обновить значения hello фактический URL-адрес входа и идентификатор. Обратитесь к [группа поддержки клиента TargetProcess](mailto:support@targetprocess.com) tooget эти значения. 
 
4. На hello **сертификат подписи SAML** щелкните **сертификата (Base64)** и затем сохраните файл сертификата hello на вашем компьютере.

    ![Раздел "Сертификат подписи SAML"](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Кнопка "Сохранить"](./media/active-directory-saas-target-process-tutorial/tutorial_general_400.png)

6. На hello **конфигурации TargetProcess** щелкните **Настройка TargetProcess** tooopen **Настройка входа** окна. Копировать hello **SAML единого входа URL-адрес службы** из hello **краткий справочник.**

    ![Раздел "Конфигурация TargetProcess"](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_configure.png) 

7. Вход tooyour TargetProcess приложения от имени администратора.

8. В меню в верхней части hello hello выберите **установки**.
   
    ![Настройка](./media/active-directory-saas-target-process-tutorial/tutorial_target_process_05.png)

9. Щелкните **Параметры**.
   
    ![данных](./media/active-directory-saas-target-process-tutorial/tutorial_target_process_06.png) 

10. Щелкните **Single Sign-on**(Единый вход).
   
    ![Щелчок "Single Sign-on" (Единый вход)](./media/active-directory-saas-target-process-tutorial/tutorial_target_process_07.png) 

11. На hello единым входом параметры диалогового окна выполните следующие шаги hello.
   
    ![Настройка единого входа](./media/active-directory-saas-target-process-tutorial/tutorial_target_process_08.png)
    
    а. Щелкните **Enable Single Sign-on**(Включить единый вход).
    
    b. В **URL-адрес входа** текстовое значение hello вставить **SAML единого входа URL-адрес службы** скопирован из портала Azure.

    c. Откройте загруженный сертификат в блокноте, hello копирования содержимого, а затем вставьте его в hello **сертификат** текстового поля.
    
    d. Установите флажок **Enable JIT Provisioning**(Включить JIT-подготовку).

    д. Щелкните **Сохранить**.

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-target-process-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Список hello toodisplay пользователей](./media/active-directory-saas-target-process-tutorial/create_aaduser_02.png) 

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".
 
    ![Кнопка "Добавить"](./media/active-directory-saas-target-process-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Раздел "Пользователь"](./media/active-directory-saas-target-process-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="create-a-targetprocess-test-user"></a>Создание тестового пользователя TargetProcess

Цель этого раздела Hello — toocreate пользователя с именем Саймон Britta в TargetProcess.

Приложение TargetProcess поддерживает JIT-подготовку. Эта функция уже включена в ходе [настройки единого входа в Azure AD](#configuring-azure-ad-single-sign-on).

В этом разделе никакие действия с вашей стороны не требуются.

### <a name="assign-hello-azure-ad-test-user"></a>Назначить hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooTargetProcess доступа.

![Назначение пользователя][200] 

**tooassign tooTargetProcess Britta Simon выполните следующие шаги hello.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **TargetProcess**.

    ![TargetProcess в списке приложений](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="test-single-sign-on"></a>Проверка единого входа

Цель этого раздела Hello является tootest настройки единого входа Azure AD с помощью панели доступа "hello".

При нажатии кнопки TargetProcess плитки в панели доступа hello приветствия, вы должны получить автоматически вошедшего tooyour TargetProcess приложения. Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_203.png

