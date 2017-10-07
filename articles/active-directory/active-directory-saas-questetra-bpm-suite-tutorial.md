---
title: "Руководство по интеграции Azure Active Directory с Questetra BPM Suite | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Questetra BPM Suite."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: fb6d5b73-e491-4dd2-92d6-94e5aba21465
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/14/2017
ms.author: jeedes
ms.openlocfilehash: 4907e3b5751cd79f994fbd2ebcb7faec4eac34e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-questetra-bpm-suite"></a>Учебник. Интеграция Azure Active Directory с Questetra BPM Suite
Hello цель этого учебника — tooshow вы как toointegrate Questetra BPM Suite с Azure Active Directory (Azure AD).  
Интеграция с Azure AD Questetra BPM Suite предоставляет hello следующие преимущества: 

* Можно управлять в Azure AD, имеющего доступ tooQuestetra BPM Suite 
* Ваш пользователей tooautomatically get вошедшего tooQuestetra Suite BPM (Single Sign-On) можно включить с помощью своих учетных записей Azure AD
* Можно управлять учетными записями в одном централизованном месте - hello классический портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования
tooconfigure интеграция Azure AD с набором BPM Questetra требуется hello следующих элементов:

* подписка Azure AD;
* Подписка [Questetra BPM Suite](https://senbon-imadegawa-988.questetra.net/) с включенным единым входом.

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

1. Добавление набора BPM Questetra из галереи hello 
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-questetra-bpm-suite-from-hello-gallery"></a>Добавление набора BPM Questetra из галереи hello
tooconfigure hello интеграции Questetra BPM Suite в Azure AD, вы должны tooadd Questetra BPM набор из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd Questetra BPM набор из галереи hello выполните hello следующие шаги.**

1. В hello **классический портал Azure**, на левой панели навигации hello, нажмите кнопку **Active Directory**. 
   
    ![Active Directory][1]

2. Из hello **каталога** список, выберите hello каталога, для которого требуется Интеграция каталогов tooenable.

3. Щелкните представление приложения hello tooopen в представлении каталога hello **приложений** в верхнем меню hello.
   
    ![Приложения][2]

4. Нажмите кнопку **добавить** hello нижней части страницы приветствия.
   
    ![Приложения][3]

5. На hello **что вам требуется toodo** диалоговое окно, нажмите кнопку **добавить приложение из коллекции hello**.
   
    ![Приложения][4]

6. Введите в поле поиска hello **Questetra BPM Suite**.
   
    ![Приложения][5]

7. В области результатов hello выберите **Questetra BPM Suite**и нажмите кнопку **завершить** tooadd приложения hello.

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
Цель этого раздела Hello является tooshow как tooconfigure и тестирования Azure AD единого входа с набором BPM Questetra на основе тестового пользователя с именем «Britta Simon».

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в набор BPM Questetra tooan пользователя в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в наборе BPM Questetra должен установить toobe.  
Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** Questetra BPM набора.

tooconfigure и тестирования Azure AD единого входа с набором BPM Questetra, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя Questetra BPM Suite](#creating-a-questetra-bpm-suite-test-user)**  -toohave аналог Саймон Britta в наборе BPM Questetra, представление связанных toohello Azure AD ей.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD
Цель этого раздела Hello — tooenable Azure AD единого входа в hello классический портал Azure и tooconfigure единого входа в приложении Questetra BPM Suite.

**tooconfigure Azure AD единого входа с набором BPM Questetra, выполните следующие шаги hello.**

1. В классический портал Azure, на hello hello **Questetra BPM Suite** странице интеграции приложения щелкните **настроить единый вход** tooopen hello **настройки единого входа**  диалоговое окно.
   
    ![Настройка единого входа][8]

2. На hello **предпочитаемый как toosign пользователей на tooQuestetra BPM Suite** выберите **Azure AD Single Sign-On**, а затем нажмите кнопку **Далее**.
   
    ![Единый вход в Azure AD][9]

3. В другом окне веб-браузера войдите в свой корпоративный веб-сайт **Questetra BPM Suite** в качестве администратора.

4. В меню в верхней части hello hello выберите **параметры системы**. 
   
    ![Единый вход в Azure AD][10]

5. tooopen hello **SingleSignOnSAML** щелкните **единого входа (SAML)**. 
   
    ![Единый вход в Azure AD][11]

6. В классический портал Azure, на hello hello **Настройка параметров приложения** диалогового окна выполните следующие шаги hello: 
   
    ![Настройка параметров приложения][13]
   
    а. На вас **Questetra BPM Suite** корпоративный сайт в hello в разделе сведений SP, hello копирования **URL-адрес ACS**и вставьте его в hello **на URL-адрес входа** текстового поля.
   
    b. На вас **Questetra BPM Suite** корпоративный сайт в hello в разделе сведений SP, hello копирования **идентификатор сущности**и вставьте его в hello **URL-адрес издателя** текстового поля.
   
    c. На вас **Questetra BPM Suite** корпоративный сайт в hello в разделе сведений SP, hello копирования **URL-адрес ACS**и вставьте его в hello **URL-адрес ответа** текстового поля.
   
    d. Щелкните **Далее**.

7. На hello **настроить единый вход в набор BPM Questetra** нажмите кнопку **загрузки сертификата**, а затем сохраните файл сертификата hello на локальном компьютере.
   
    ![Настройка единого входа][14]

8. На вас **Questetra BPM Suite** компании сайта, выполните следующие шаги hello: 
   
    ![Настройка единого входа][15]
   
    а. Выберите пункт **Включить единый вход**.
   
    b. На hello классического портала Azure скопируйте hello **URL-адрес издателя** значение, а затем вставьте его в hello **идентификатор сущности** текстового поля.
   
    c. На hello классического портала Azure скопируйте hello **единого входа URL-адрес службы** значение, а затем вставьте его в hello **входа в URL-адрес страницы** текстового поля.
   
    d. На hello классического портала Azure скопируйте hello **URL-адрес службы единого выхода** значение, а затем вставьте его в hello **URL-адрес страницы выхода** текстового поля.
   
    д. В hello **формата идентификатора имени** введите **urn: oasis: имена: tc: SAML:1.1:nameid-format: emailAddress**.

    f. Создайте файл в кодировке Base-64 из загруженного сертификата. 

    >[!TIP] 
    >Дополнительные сведения см. в разделе [как tooconvert двоичные данные сертификата в текстовый файл](http://youtu.be/PlgrzUZ-Y1o).

    ж. Откройте сертификат в кодировке base-64 в блокноте, hello копирования содержимого его в буфер обмена, а затем вставьте его в hello **проверки сертификата** текстового поля. 

    h. Щелкните **Сохранить**.

1. На hello классический портал Azure, выберите Подтверждение настройки единого входа hello и нажмите кнопку **Далее**. 
   
    ![Что такое Azure AD Connect?][17]

2. На hello **единого входа для подтверждения** щелкните **завершить**.  
   
    ![Что такое Azure AD Connect?][18]


### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в классический портал Azure, вызывается Britta Simon hello.

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **классический портал Azure**, на левой панели навигации hello, нажмите кнопку **Active Directory**.
   
    ![Создание тестового пользователя Azure AD][100] 

2. Из hello **каталога** список, выберите hello каталога, для которого требуется Интеграция каталогов tooenable.

3. Щелкните toodisplay hello список пользователей, выберите в меню в верхней части экрана приветствия hello **пользователей**.
   
    ![Создание тестового пользователя Azure AD][101] 

4. tooopen hello **добавить пользователя** щелкните диалоговое окно в нижней hello инструментов hello **добавить пользователя**. 
   
    ![Создание тестового пользователя Azure AD][102] 

5. На hello **сообщите нам об этом пользователе** диалогового окна выполните следующие шаги hello:
   
    ![Создание тестового пользователя Azure AD][103]
   
    а. В поле **Тип пользователя** выберите значение **Новый пользователь в вашей организации**.
   
    b. В имени пользователя hello **textbox**, тип **BrittaSimon**.
   
    c. Нажмите кнопку Далее.

6. На hello **профиля пользователя** диалогового окна выполните следующие шаги hello: 
   
    ![Создание тестового пользователя Azure AD][104] 
   
    а. В hello **имя** введите **Britta**. 
   
    b. В hello **Фамилия** текстовое поле, тип, **Simon**.
   
    c. В hello **отображаемое имя** введите **Britta Simon**.
   
    d. В hello **роли** выберите **пользователя**.
   
    д. Щелкните **Далее**.

7. На hello **получение временного пароля** странице диалогового окна щелкните **создания**.
   
    ![Создание тестового пользователя Azure AD][105]  

8. На hello **получение временного пароля** диалогового окна выполните следующие шаги hello:
   
    ![Создание тестового пользователя Azure AD][106]   
   
    а. Запишите значение hello hello **новый пароль**.
   
    b. Нажмите **Завершено**.   

### <a name="creating-a-questetra-bpm-suite-test-user"></a>Создание тестового пользователя Questetra BPM Suite
Цель этого раздела Hello — toocreate пользователя с именем Britta Simon Questetra BPM набора.

**toocreate пользователя с именем Britta Simon Questetra BPM пакета, выполните следующие шаги hello.**

1. Корпоративный сайт Questetra BPM Suite tooyour входа от имени администратора.
2. Go слишком**параметры системы > список пользователей > нового пользователя**. 
3. В диалоговом окне Новый пользователь hello выполните следующие шаги hello. 
   
    ![Создание тестового пользователя][300] 
   
    а. В hello **имя** текстовом поле введите имя пользователя Britta в Azure AD.
   
    b. В hello **электронной почты** текстовом поле введите имя пользователя Britta в Azure AD.
   
    c. В hello **пароль** введите пароль.

4. Нажмите кнопку **Добавить нового пользователя**.

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя
Hello цель этого раздела — tooenabling toouse Britta Simon Azure единого входа, предоставляя свой доступ tooQuestetra BPM Suite.

![Что такое Azure AD Connect?][200]

**tooassign tooQuestetra Britta Simon BPM Suite выполните hello следующие шаги.**

1. Hello Azure представления приложения hello tooopen в представлении каталога hello классического портала щелкните **приложений** в верхнем меню hello.
   
    ![Что такое Azure AD Connect?][201]
2. В списке приложений hello выберите **Questetra BPM Suite**.
   
    ![Что такое Azure AD Connect?][205]
3. В меню в верхней части hello hello выберите **пользователей**.
   
    ![Что такое Azure AD Connect?][202]
4. В списке пользователей hello выберите **Britta Simon**.
   
    ![Что такое Azure AD Connect?][203]
5. В нижней hello hello инструментов, нажмите кнопку **назначить**.
   
    ![Что такое Azure AD Connect?][204]

### <a name="testing-single-sign-on"></a>Проверка единого входа
Цель этого раздела Hello является tootest настройки единого входа Azure AD с помощью панели доступа "hello".  
При выборе плитки Questetra BPM Suite hello в hello панели доступа, вы должны получить приложению автоматически вошедшего tooyour Questetra BPM Suite.

## <a name="additional-resources"></a>Дополнительные ресурсы
* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->
[1]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_01.png


[8]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_06.png
[9]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_02.png
[10]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_03.png
[11]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_04.png
[12]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_05.png
[13]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_06.png
[14]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_07.png
[15]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_08.png
[16]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_09.png
[17]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_10.png
[18]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_08.png


[100]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_09.png 
[101]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_10.png 
[102]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_11.png 
[103]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_12.png 
[104]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_13.png 
[105]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_14.png 
[106]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_15.png 


[200]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_16.png 
[201]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_17.png 
[202]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_18.png
[203]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_19.png
[204]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_20.png
[205]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_12.png

[300]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_11.png 
