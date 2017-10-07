---
title: "Руководство по интеграции Azure Active Directory с SuccessFactors | Документация Майкрософт"
description: "Узнайте, как toouse SuccessFactors с Azure Active Directory tooenable единого входа, автоматизированной подготовки и многое другое!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 32bd8898-c2d2-4aa7-8c46-f1f5c2aa05f1
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/21/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 3f7895d7d5e26fda27f555ae2f14a1645b50dcba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-successfactors"></a>Руководство. Интеграция Azure Active Directory с SuccessFactors
Hello цель этого учебника — tooshow вы как toointegrate SuccessFactors с Azure Active Directory (Azure AD).

Интеграция SuccessFactors с Azure AD предоставляет hello следующие преимущества:

* Можно управлять в Azure AD, имеющего доступ tooSuccessFactors
* Можно включить на пользователей tooautomatically get вошедшего tooSuccessFactors (Single Sign-On) с помощью своих учетных записей Azure AD
* Можно управлять учетными записями в одном централизованном месте - hello классический портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования
tooconfigure интеграция Azure AD с SuccessFactors требуется hello следующих элементов:

* Действующая подписка на Azure
* клиент в SuccessFactors.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.
> 
> 

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

* Не следует использовать рабочую среду при отсутствии необходимости.
* Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
Hello цель этого учебника — tooenable tootest Azure AD единого входа в тестовой среде.

Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление SuccessFactors из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-successfactors-from-hello-gallery"></a>Добавление SuccessFactors из галереи hello
tooconfigure hello интеграции SuccessFactors в Azure AD, вы должны tooadd SuccessFactors из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd SuccessFactors из галереи hello, выполните следующие шаги hello.**

1. В классический портал Azure, на левой навигационной панели hello hello щелкните **Active Directory**.
   
    ![Настройка единого входа][1]
2. Из hello **каталога** список, выберите hello каталога, для которого требуется Интеграция каталогов tooenable.
3. Щелкните представление приложения hello tooopen в представлении каталога hello **приложений** в верхнем меню hello.
   
    ![Настройка единого входа][2]
4. Нажмите кнопку **добавить** hello нижней части страницы приветствия.
   
    ![Приложения][3]
5. На hello **что вам требуется toodo** диалоговое окно, нажмите кнопку **добавить приложение из коллекции hello**.
   
    ![Настройка единого входа][4]
6. В hello **поле поиска**, тип **SuccessFactors**.
   
    ![Настройка единого входа][5]
7. В панели результатов hello выберите **SuccessFactors**и нажмите кнопку **завершить** tooadd приложения hello.
   
    ![Настройка единого входа][6]

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
Цель этого раздела Hello является tooshow как tooconfigure и теста Azure AD единого входа с SuccessFactors на основе тестового пользователя с именем «Britta Simon».

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в SuccessFactors tooan пользователя в Azure AD. Другими словами связи между пользователя Azure AD и hello связанных пользователей в SuccessFactors должен установить toobe.

Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в SuccessFactors.

tooconfigure и теста Azure AD единого входа с SuccessFactors, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя SuccessFactors](#creating-a-successfactors-test-user)**  -toohave аналог Саймон Britta в SuccessFactors, представление связанных toohello Azure AD ей.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD
В этом разделе включения Azure AD единого входа в классическом портале hello и настройки единого входа в приложение SuccessFactors.

**tooconfigure Azure AD единого входа с SuccessFactors, выполните следующие шаги hello.**

1. В классический портал Azure, на hello hello **SuccessFactors** странице интеграции приложения щелкните **настроить единый вход** tooopen hello **Настройка единого входа** диалоговое окно.
   
    ![Настройка единого входа][7]
2. На hello **предпочитаемый как toosign пользователей на tooSuccessFactors** выберите **Microsoft Azure AD Single Sign-On**, а затем нажмите кнопку **Далее**.
   
    ![Настройка единого входа][8]
3. На hello **настроить URL-адрес приложения** страницы, выполните следующие шаги hello и нажмите кнопку **Далее**.
   
    ![Настройка единого входа][9]
   
    а. В hello **на URL-адрес входа** текстовом поле введите URL-адрес, используя один из следующих шаблонов hello: 
   
    |  |
    | --- |
    | `https://<company name>.successfactors.com/<company name>` |
    | `https://<company name>.sapsf.com/<company name>` |
    | `https://<company name>.successfactors.eu/<company name>` |
    | `https://<company name>.sapsf.eu` |
   
    b. В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя один из следующих шаблонов hello: 
   
    |  |
    | --- |
    | `https://<company name>.successfactors.com/<company name>` |
    | `https://<company name>.sapsf.com/<company name>` |
    | `https://<company name>.successfactors.eu/<company name>` |
    | `https://<company name>.sapsf.eu` |
    | `https://<company name>.sapsf.eu/<company name>` |
   
    c. Щелкните **Далее**. 

    > [!NOTE]
    > Обратите внимание на то, что они не hello реальные значения. У вас tooupdate эти значения с hello фактический на URL-адрес входа и ответ URL-адрес. обратитесь в службу tooget эти значения [группы поддержки SuccessFactors](https://www.successfactors.com/en_us/support.html).

1. На hello **настройки единого входа в SuccessFactors** щелкните **загрузки сертификата**, а затем сохраните файл сертификата hello на локальном компьютере.
   
    ![Настройка единого входа][10]

2. В другом окне веб-браузера войдите на **портал администрирования SuccessFactors** с правами администратора.

3. Посетите **безопасности приложения** и собственные слишком**единого входа в компонент**. 

4. Установите любое значение в hello **сбросить токен** и нажмите кнопку **сохранить маркера** tooenable единого входа SAML.
   
    ![Настройка единого входа на стороне приложения][11]

    > [!NOTE] 
    > Это значение используется только в качестве hello выключатель. Если любое значение сохраняется, hello единого входа SAML — ON. Если пустое значение сохраняется hello единого входа SAML имеет значение OFF.

1. Снимок экрана собственного toobelow и выполните следующие действия hello.
   
    ![Настройка единого входа на стороне приложения][12]
   
    а. Выберите hello **единого входа SAML v2** переключатель
   
    b. Задайте hello Name(e.g. SAml issuer + company name) стороной утверждения SAML.
   
    c. В hello **издатель SAML** textbox помещение значения hello **URL-адрес издателя** из мастера настройки приложения Azure AD.
   
    d. Выберите значение **Response(Customer Generated/IdP/AP)** (Ответ (создается клиентом/IdP/AP)) для параметра **Require Mandatory Signature** (Требуется обязательная подпись).
   
    д. Выберите значение **Enabled** (Включено) для параметра **Enable SAML Flag** (Включить флаг SAML).
   
    Е. Выберите значение **No** (Нет) для параметра **Login Request Signature (SF Generated/SP/RP)** (Подпись запроса на вход (создается SF/SP/RP)).
   
    ж. Выберите значение **Browser/Post Profile** (Браузер/пост-профилирование) для параметра **SAML Profile** (Профиль SAML).
   
    h. Выберите значение **No** (Нет) для параметра **Enforce Certificate Valid Period** (Применять период действия сертификата).
   
    i. Скопируйте содержимое hello файла hello загруженного сертификата и вставьте его в hello **сертификата проверки SAML** текстового поля.

    > [!NOTE] 
    > Hello содержимого сертификата должен иметь начинаться сертификата и закрывающий теги сертификата.

1. Перейдите tooSAML V2, а затем выполните следующие шаги hello:
   
    ![Настройка единого входа на стороне приложения][13]
   
    а. Выберите значение **Yes** (Да) для параметра **Support SP-initiated Global Logout** (Поддержка глобального выхода, инициированного SP).
   
    b. В hello **URL-адрес (назначение LogoutRequest) глобального выхода служба** textbox помещение значения hello **URL-адрес удаленного выхода** из мастера настройки приложения Azure AD.
   
    c. Выберите значение **No** (Нет) для параметра **Require sp must encrypt all NameID element** (Требуется шифрование всех элементов NameID на стороне SP).
   
    d. Выберите значение **unspecified** (Не определено) для параметра **NameID Format** (Формат идентификатора имени).
   
    д. Выберите значение **Yes** (Да) для параметра **Enable sp initiated login (AuthnRequest)** (Включить вход по требованию SP).
   
    f. В hello **запрос на отправку в масштабе организации издателя** textbox помещение значения hello **URL-адрес удаленного входа** из мастера настройки приложения Azure AD.
2. Выполните следующие действия, если требуется, чтобы имена входа toomake hello без учета регистра,.
   
    а. Посетите **параметры компании**(нижней hello).
   
    b. Установите флажок **Enable Non-Case-Sensitive Username** (Имя пользователя без учета регистра).
   
    в) Щелкните **Save**(Сохранить).
   
    ![Настройка единого входа][29]

    > [!NOTE] 
    > При попытке tooenable это, hello система проверяет, если он создаст повторяющееся имя входа SAML. Например, если у клиента приветствия имен пользователей User1 и пользователь user1. Если отменить учет регистра, эти имена будут считаться одинаковыми. Hello система выдаст сообщение об ошибке и функция hello не будет разрешена. Hello клиента потребуется toochange один приветствия имен пользователей, фактически написано другой. 

1. На hello классический портал Azure, выберите Подтверждение настройки единого входа hello и нажмите кнопку **завершить** tooclose hello **Настройка единого входа** диалогового окна.
   
    ![Приложения][14]
2. На hello **единого входа для подтверждения** щелкните **завершить**.
   
    ![Приложения][15]

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Hello цель этого раздела — toocreate тестового пользователя вызывается Саймон Britta классическом портале hello.

![Создание пользователя Azure AD][16]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **классический портал Azure**, на левой панели навигации hello, нажмите кнопку **Active Directory**.
   
    ![Создание тестового пользователя Azure AD][17]
2. Из hello **каталога** список, выберите hello каталога, для которого требуется Интеграция каталогов tooenable.
3. Щелкните toodisplay hello список пользователей, выберите в меню в верхней части экрана приветствия hello **пользователей**.
   
    ![Создание тестового пользователя Azure AD][18]
4. tooopen hello **добавить пользователя** щелкните диалоговое окно в нижней hello инструментов hello **добавить пользователя**.
   
    ![Создание тестового пользователя Azure AD][19]
5. На hello **сообщите нам об этом пользователе** диалогового окна выполните следующие шаги hello:
   
    ![Создание тестового пользователя Azure AD][20]
   
    а. В поле «Тип пользователя» выберите значение «Новый пользователь в вашей организации».
   
    b. В имени пользователя hello **textbox**, тип **BrittaSimon**.
   
    c. Щелкните **Далее**.
6. На hello **профиля пользователя** диалогового окна выполните следующие шаги hello:
   
    ![Создание тестового пользователя Azure AD][21]
   
    а. В hello **имя** введите **Britta**.  
   
    b. В hello **Фамилия** текстовое поле, тип, **Simon**.
   
    c. В hello **отображаемое имя** введите **Britta Simon**.
   
    d. В hello **роли** выберите **пользователя**.
   
    д. Щелкните **Далее**.
7. На hello **получение временного пароля** странице диалогового окна щелкните **создания**.
   
    ![Создание тестового пользователя Azure AD][22]
8. На hello **получение временного пароля** диалогового окна выполните следующие шаги hello:
   
    ![Создание тестового пользователя Azure AD][23]
   
    а. Запишите значение hello hello **новый пароль**.
   
    b. Нажмите **Завершено**.  

### <a name="creating-a-successfactors-test-user"></a>Создание тестового пользователя SuccessFactors
В порядке tooenable toolog пользователей Azure AD в SuccessFactors их необходимо подготовить в SuccessFactors.  
В случае hello объекта SuccessFactors Подготовка выполняется вручную.

tooget создать пользователей в SuccessFactors, требуется toocontact hello [группы поддержки SuccessFactors](https://www.successfactors.com/en_us/support.html).

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя
Hello цель этого раздела — tooenabling toouse Britta Simon Azure единого входа путем предоставления ее tooSuccessFactors доступа.

![Назначение пользователя][24]

**tooassign tooSuccessFactors Britta Simon выполните следующие шаги hello.**

1. Hello классического портала щелкните представление приложения hello tooopen в представлении каталога hello **приложений** в верхнем меню hello.
   
    ![Назначение пользователя][25]
2. В списке приложений hello выберите **SuccessFactors**.
   
    ![Настройка единого входа][26]
3. В меню в верхней части hello hello выберите **пользователей**.
   
    ![Назначение пользователя][27]
4. В списке пользователей hello выберите **Britta Simon**.
5. В нижней hello hello инструментов, нажмите кнопку **назначить**.
   
    ![Назначение пользователя][28]

### <a name="testing-single-sign-on"></a>Проверка единого входа
Цель этого раздела Hello является tootest настройки единого входа Azure AD с помощью панели доступа "hello".

При нажатии кнопки SuccessFactors плитки в панели доступа hello приветствия, вы должны получить tooyour автоматически подписан в приложение SuccessFactors.

## <a name="additional-resources"></a>Дополнительные ресурсы
* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[0]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_00.png
[1]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_01.png
[6]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_02.png
[7]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_03.png
[8]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_04.png
[9]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_05.png
[10]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_06.png

[11]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_07.png
[12]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_08.png
[13]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_09.png
[14]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_05.png
[15]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_06.png

[16]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_00.png
[17]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_01.png
[18]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_02.png
[19]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_03.png
[20]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_04.png
[21]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_05.png
[22]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_06.png
[23]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_07.png

[24]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_07.png
[25]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_08.png
[26]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_11.png
[27]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_09.png
[28]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_10.png
[29]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_10.png
