---
title: "Учебник: Интеграция Azure Active Directory с @Task| Документы Microsoft"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и @Task."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: aab8bd2f-f9dd-42da-a18e-d707865687d7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 0840763622086a02a27cfafff3b741bc66cec498
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-task"></a>Учебник. Интеграция Azure Active Directory с @Task
Hello цель этого учебника — tooshow вы как toointegrate @Task с Azure Active Directory (Azure AD).  
Интеграция @Task с Azure AD предоставляет hello следующие преимущества: 

* Можно управлять в Azure AD, у которого есть доступtoo@Task
* Позволяет пользователям получить tooautomatically вошедшего too@Task (Single Sign-On) с помощью своих учетных записей Azure AD
* Можно управлять учетными записями в одном централизованном месте - hello классический портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования
Интеграция Azure AD tooconfigure с @Task, требуется hello следующих элементов:

* подписка Azure AD;
* подписка на @Task с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.
> 
> 

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

* Не следует использовать рабочую среду при отсутствии необходимости.
* Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/). 

## <a name="scenario-description"></a>Описание сценария
Hello цель этого учебника — tooenable tootest Azure AD единого входа в тестовой среде.  
Hello сценарий, описанный в этом учебнике состоит из трех основных компонентов:

1. Добавление @Task из галереи hello 
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-task-from-hello-gallery"></a>Добавление @Task из галереи hello
Интеграция hello tooconfigure @Task в Azure AD необходимо tooadd @Task из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd @Task из галереи hello выполнения hello следующие шаги:**

1. В hello **классический портал Azure**, на левой панели навигации hello, нажмите кнопку **Active Directory**. 
   
    ![Active Directory][1] 
2. Из hello **каталога** список, выберите hello каталога, для которого требуется Интеграция каталогов tooenable.
3. Щелкните представление приложения hello tooopen в представлении каталога hello **приложений** в верхнем меню hello.
   
    ![Приложения][2] 
4. Нажмите кнопку **добавить** hello нижней части страницы приветствия.
   
    ![Приложения][3] 
5. На hello **что вам требуется toodo** диалоговое окно, нажмите кнопку **добавить приложение из коллекции hello**.
   
    ![Приложения][4] 
6. Введите в поле поиска hello  **@Task** .
   
    ![Приложения][5] 
7. В области результатов hello выберите  **@Task** и нажмите кнопку **завершить** tooadd приложения hello.
   
    ![Приложения][30] 

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
Hello цель этого раздела — tooshow вы как tooconfigure и тестирования Azure AD single входа с @Task основании тестового пользователя с именем «Britta Simon».

Для единого входа toowork Azure AD необходима tooknow пользователя аналог hello в @Task tooan пользователя в Azure AD. Другими словами, связи между пользователя Azure AD и связанных пользователей hello в @Task должен установить toobe.   
Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в @Task.

tooconfigure и Azure AD тестирования единого входа с @Task, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание @Tasktest пользователя](#creating-a-halogen-software-test-user)**  -toohave a аналог Саймон Britta в @Taskthat является представлением ей связанного toohello Azure AD.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD
Цель этого раздела Hello является tooenable Azure AD единого входа в hello классический портал Azure и tooconfigure единый вход в ваш @Task приложения.

**tooconfigure Azure AD единого входа с @Task, выполните следующие шаги hello:**

1. В классический портал Azure, на hello hello  **@Task**  странице интеграции приложения щелкните **настроить единый вход** tooopen hello **настройки единого входа**  диалоговое окно.
   
    ![Настройка единого входа][6] 
2. На hello **как бы вы как toosign пользователей на too@Task**  выберите **Azure AD Single Sign-On**, а затем нажмите кнопку **Далее**.
   
    ![Единый вход в Azure AD][7] 
3. На hello **Настройка параметров приложения** диалогового окна выполните следующие шаги hello:
   
    ![Настройка параметров приложения][8] 
   
     а. В hello **на URL-адрес входа** textbox hello введите URL-адрес, используемые вашей пользователей на toosign tooyour @Task приложения (например:*https://<Tenant name>.attask ondemand.com*).
   
     b. Щелкните **Далее**.
4. На hello **настроить единый вход в @Task**  щелкните **загрузить метаданные**, сохраните файл метаданных hello на локальном компьютере и нажмите кнопку **Далее**.
   
    ![Что такое Azure AD Connect?][9] 
5. Tooyour входа @Task сайт компании от имени администратора.
6. Go слишком**единого входа на конфигурации**.
7. На hello **Single Sign-On** диалоговое окно, выполните следующие шаги hello
   
    ![Настройка единого входа][23]
   
    а. Для параметра **Тип** выберите значение **SAML 2.0**.
   
    b. Выберите **идентификатор поставщика службы**.
   
    c. На hello классического портала Azure скопируйте hello **URL-адрес удаленного входа**и вставьте его в hello **URL-адрес входа портала** текстового поля.
   
    d. На hello классического портала Azure скопируйте hello **URL-адрес службы единого выхода**, а затем вставьте его в hello **URL-адрес выхода** текстового поля.
   
    д. На hello классического портала Azure скопируйте hello **URL-адрес изменения пароля**и вставьте его в hello **URL-адрес изменения пароля** текстового поля.
   
    f. Щелкните **Сохранить**.
8. На hello классический портал Azure, выберите Подтверждение настройки единого входа hello и нажмите кнопку **Далее**. 
   
    ![Что такое Azure AD Connect?][10]
9. На hello **единого входа для подтверждения** щелкните **завершить**.  
   
    ![Что такое Azure AD Connect?][11]

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в классический портал Azure, вызывается Britta Simon hello.  

![Создание пользователя Azure AD][20]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **классический портал Azure**, на левой панели навигации hello, нажмите кнопку **Active Directory**.
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_02.png) 
2. Из hello **каталога** список, выберите hello каталога, для которого требуется Интеграция каталогов tooenable.
3. Щелкните toodisplay hello список пользователей, выберите в меню в верхней части экрана приветствия hello **пользователей**.
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_03.png) 
4. tooopen hello **добавить пользователя** щелкните диалоговое окно в нижней hello инструментов hello **добавить пользователя**. 
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_04.png) 
5. На hello **сообщите нам об этом пользователе** диалогового окна выполните следующие шаги hello: 
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_05.png) 
   
    а. В поле «Тип пользователя» выберите значение «Новый пользователь в вашей организации».
   
    b. В имени пользователя hello **textbox**, тип **BrittaSimon**.
   
    c. Щелкните **Далее**.
6. На hello **профиля пользователя** диалогового окна выполните следующие шаги hello: 
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_06.png) 
   
    а. В hello **имя** введите **Britta**.  
   
    b. В hello **Фамилия** текстовое поле, тип, **Simon**.
   
    c. В hello **отображаемое имя** введите **Britta Simon**.
   
    d. В hello **роли** выберите **пользователя**.

    д. Щелкните **Далее**.

7. На hello **получение временного пароля** странице диалогового окна щелкните **создания**.
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_07.png) 
8. На hello **получение временного пароля** диалогового окна выполните следующие шаги hello:
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_08.png) 
   
    а. Запишите значение hello hello **новый пароль**.
   
    b. Нажмите **Завершено**.   

### <a name="creating-an-task-test-user"></a>Создание тестового пользователя @Task
Hello цель этого раздела — toocreate пользователя с именем Саймон Britta @Task.

**toocreate пользователя с именем Саймон Britta @Task, выполните следующие шаги hello:**

1. Войдите на tooyour @Task сайт компании от имени администратора.
2. В меню в верхней части hello hello выберите **людей**.
3. Щелкните **Новый пользователь**. 
4. В диалоговом окне Новый пользователь hello выполните следующие шаги hello.
   
    ![Создание тестового пользователя @Task][21] 
   
    а. В hello **имя** текстовое поле, введите «Britta».
   
    b. В hello **Фамилия** текстовое поле, введите «Simon».
   
    c. В hello **адрес электронной почты** текстовом поле введите адрес электронной почты Britta Simon в Azure Active Directory.
   
    d. Нажмите кнопку **Добавить пользователя**.

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя
Hello цель этого раздела — tooenabling toouse Britta Simon Azure единого входа, предоставляя свой доступ too@Task.

![Назначение пользователя][200] 

**tooassign Britta Simon too@Task, выполните следующие шаги hello:**

1. Hello Azure представления приложения hello tooopen в представлении каталога hello классического портала щелкните **приложений** в верхнем меню hello.
   
    ![Назначение пользователя][201] 
2. В списке приложений hello выберите  **@Task** .
   
    ![Назначение пользователя][202] 
3. В меню в верхней части hello hello выберите **пользователей**.
   
    ![Назначение пользователя][203] 
4. В списке пользователей hello выберите **Britta Simon**.
5. В нижней hello hello инструментов, нажмите кнопку **назначить**.
   
    ![Назначение пользователя][205]

### <a name="testing-single-sign-on"></a>Проверка единого входа
Цель этого раздела Hello является tootest настройки единого входа Azure AD с помощью панели доступа "hello".  
При нажатии кнопки hello @Task плитки в Здравствуйте панели доступа, вы должны получить автоматически вошедшего tooyour @Task приложения.

## <a name="additional-resources"></a>Дополнительные ресурсы
* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-attask-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-attask-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-attask-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-attask-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_01.png
[30]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_02.png


[6]: ./media/active-directory-saas-attask-tutorial/tutorial_general_05.png
[7]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_03.png
[8]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_04.png
[9]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_05.png
[10]: ./media/active-directory-saas-attask-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-attask-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-attask-tutorial/tutorial_general_100.png
[21]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_08.png


[23]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_06.png

[200]: ./media/active-directory-saas-attask-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-attask-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_09.png
[203]: ./media/active-directory-saas-attask-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-attask-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-attask-tutorial/tutorial_general_205.png






