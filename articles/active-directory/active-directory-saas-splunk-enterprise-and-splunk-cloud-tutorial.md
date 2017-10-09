---
title: "Руководство. Интеграция Azure Active Directory с приложениями Splunk Enterprise и Splunk Cloud | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и корпоративный Splunk и Splunk облака."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b3e2b4a9-749c-4895-813d-db46f8dfdbf8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/09/2017
ms.author: jeedes
ms.openlocfilehash: 9bb6817cb31dce684cd9cc1c567fa3efc8906ad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-splunk-enterprise-and-splunk-cloud"></a>Руководство. Интеграция Azure Active Directory с приложениями Splunk Enterprise и Splunk Cloud

В этом учебнике вы узнаете, как toointegrate Splunk предприятия и Splunk в облаке в Azure Active Directory (Azure AD).

Интеграция с Azure AD Splunk предприятия и в облаке Splunk предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, который имеет доступ tooSplunk предприятия и Splunk в облаке
- Вы можете включить учетные записи Azure AD вашей пользователей tooautomatically get вошедшего tooSplunk предприятия и в облаке Splunk единого входа (SSO)
- Можно управлять учетными записями в одном централизованном месте - hello классический портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с Splunk предприятия и Splunk в облаке необходимо hello следующих элементов:

- подписка Azure AD;
- подписка Splunk Enterprise или Splunk Cloud с поддержкой единого входа.


>[!NOTE]
>в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.
>

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не следует использовать рабочую среду при отсутствии необходимости.
- Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).


## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.

Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление Splunk предприятия и в облаке Splunk из галереи hello
2. Настройка и проверка единого входа Azure AD.


## <a name="add-splunk-enterprise-and-splunk-cloud-from-hello-gallery"></a>Добавление Splunk предприятия и в облаке Splunk из коллекции hello
tooconfigure hello интеграции Splunk предприятия и Splunk в облаке в Azure AD, необходимо tooadd Splunk предприятия и Splunk облако из списка tooyour hello коллекции из управляемых приложений SaaS.

**tooadd Splunk предприятия и в облаке Splunk из галереи hello, выполните следующие шаги hello.**

1. В hello **классический портал Azure**, на левой панели навигации hello, нажмите кнопку **Active Directory**.

    ![Active Directory][1]

2. Из hello **каталога** список, выберите hello каталога, для которого требуется Интеграция каталогов tooenable.

3. Щелкните представление приложения hello tooopen в представлении каталога hello **приложений** в верхнем меню hello.

    ![Приложения][2]

4. Нажмите кнопку **добавить** hello нижней части страницы приветствия.

    ![Приложения][3]

5. На hello **что вам требуется toodo** диалоговое окно, нажмите кнопку **добавить приложение из коллекции hello**.

    ![Приложения][4]

6. Введите в поле поиска hello **Splunk Enterprise или облака Splunk**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_01.png)

7. В области результатов hello выберите **Splunk предприятия и в облаке Splunk**и нажмите кнопку **завершить** tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_02.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описывается настройка и проверка единого входа Azure AD в Splunk Enterprise и Splunk Cloud с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Splunk предприятия и в облаке Splunk является tooa в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в Splunk предприятия и в облаке Splunk должен установить toobe.

Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в Splunk предприятия и Splunk в облаке.

tooconfigure и теста Azure AD единого входа с Splunk предприятия и Splunk в облаке, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD единого входа](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя Splunk предприятия и в облаке Splunk](#creating-a-splunk-enterprise-and-splunk-cloud-test-user)**  -toohave аналог Саймон Britta Splunk предприятия и Splunk облако, которое является представлением ей связанного toohello Azure AD.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configure-azure-ad-single-sign-on"></a>Настройка единого входа Azure AD

В этом разделе Включить единый вход Azure AD в классическом портале hello и Настройка единого входа в приложении предприятия Splunk и Splunk в облаке.


**tooconfigure Azure AD единого входа с Splunk предприятия и Splunk в облаке, выполните следующие шаги hello.**

1. Классическом портале hello на hello **Splunk предприятия и в облаке Splunk** странице интеграции приложения щелкните **настроить единый вход** tooopen hello **настройки единого входа** диалогового окна.
     
    ![Настройка единого входа][6] 

2. На hello **как toosign пользователей на tooSplunk предприятия и облако Splunk** выберите **Azure AD Single Sign-On**, а затем нажмите кнопку **Далее**.

    ![Настройка единого входа](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_03.png) 

3. На hello **Настройка параметров приложения** диалогового окна выполните следующие шаги hello:

    ![Настройка единого входа](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_04.png) 
  1. В hello **на URL-адрес входа** текстовом поле введите URL-адрес hello используется вашим пользователям на toosign tooyour Splunk предприятия и Splunk облачного приложения, используя следующий шаблон hello:`https://<splunkserverUrl>/en-US/app/launcher/home`
  2. В hello **идентификатор** текстовом поле введите URL-адрес hello Splunk сервера.
  3. В hello **URL-адрес ответа** текстовом поле введите URL-адрес hello с hello следующий шаблон:`https://<splunkserver>/saml/acs`
  4. Щелкните **Далее**.
 
4. На hello **настроить единый вход в Splunk предприятия и в облаке Splunk** выполните следующие шаги hello:

    ![Настройка единого входа](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_05.png)
  1. Нажмите кнопку **загрузить метаданные**, а затем сохраните файл hello на вашем компьютере.
  2. Щелкните **Далее**.

5. tooget единого входа, настроенному для вашего приложения, обратитесь к Splunk Enterprise и группа поддержки Splunk облака и укажите их hello следующее:

    * загружаются Hello **federaton метаданных**
6. Hello классического портала выберите Подтверждение настройки единого входа hello и нажмите кнопку **Далее**.
    
    ![Единый вход в Azure AD][10]

7. На hello **единого входа для подтверждения** щелкните **завершить**.  
 
    ![Единый вход в Azure AD][11]

### <a name="create-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
В этом разделе создайте тестового пользователя вызывается Саймон Britta классическом портале hello.

![Создание пользователя Azure AD][20]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **классический портал Azure**, на левой панели навигации hello, нажмите кнопку **Active Directory**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_09.png) 

2. Из hello **каталога** список, выберите hello каталога, для которого требуется Интеграция каталогов tooenable.

3. Щелкните toodisplay hello список пользователей, выберите в меню в верхней части экрана приветствия hello **пользователей**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_03.png) 

4. tooopen hello **добавить пользователя** щелкните диалоговое окно в нижней hello инструментов hello **добавить пользователя**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_04.png) 

5. На hello **сообщите нам об этом пользователе** диалогового окна выполните следующие шаги hello:

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_05.png) 
  1. В поле «Тип пользователя» выберите значение «Новый пользователь в вашей организации».
  2. В имени пользователя hello **textbox**, тип **BrittaSimon**.
  3. Щелкните **Далее**.

6.  На hello **профиля пользователя** диалогового окна выполните следующие шаги hello:
  
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_06.png) 
  1. В hello **имя** введите **Britta**.  
  2. В hello **Фамилия** текстовое поле, тип, **Simon**.
  3. В hello **отображаемое имя** введите **Britta Simon**.
  4. В hello **роли** выберите **пользователя**.
  5. Щелкните **Далее**.

7. На hello **получение временного пароля** странице диалогового окна щелкните **создания**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_07.png) 

8. На hello **получение временного пароля** диалогового окна выполните следующие шаги hello:

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_08.png) 
  1. Запишите значение hello hello **новый пароль**.
  2. Нажмите **Завершено**.   

### <a name="create-a-splunk-enterprise-and-splunk-cloud-test-user"></a>Создание тестового пользователя Splunk Enterprise и Splunk Cloud

В этом разделе описано, как создать пользователя Britta Simon в Splunk Enterprise и Splunk Cloud. Обратитесь Splunk предприятия и в облаке Splunk поддержки команды tooadd hello пользователей hello Splunk предприятия и Splunk облачной платформы.


### <a name="assign-hello-azure-ad-test-user"></a>Назначить hello Azure AD тестового пользователя

В этом разделе включите Саймон Britta toouse SSOy Azure предоставление своего предприятия tooSplunk доступа и Splunk в облаке.

![Назначение пользователя][200] 

**tooassign Britta Simon tooSplunk предприятия и облака Splunk выполняют hello следующие шаги:**

1. Hello классического портала щелкните представление приложения hello tooopen в представлении каталога hello **приложений** в верхнем меню hello.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **Splunk предприятия и в облаке Splunk**.

    ![Настройка единого входа](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_50.png) 

3. В меню в верхней части hello hello выберите **пользователей**.

    ![Назначение пользователя][203]

4. В списке пользователей hello выберите **Britta Simon**.

5. В нижней hello hello инструментов, нажмите кнопку **назначить**.

    ![Назначение пользователя][205]

### <a name="test-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования вашей SSOonfiguration Azure AD, с помощью панели доступа hello.

При нажатии кнопки hello Splunk предприятия и облака Splunk плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour Splunk предприятия и Splunk облачных приложений.


## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_205.png
