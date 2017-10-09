---
title: "Руководство по интеграции Azure Active Directory с Soonr Workplace | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Soonr рабочей области."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
editor: na
ms.assetid: b75f5f00-ea8b-4850-ae2e-134e5d678d97
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: f950b45d0beceab2fa17b7690c9de81ec6603089
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-soonr-workplace"></a>Учебник. Интеграция Azure Active Directory с Soonr Workplace

Hello цель этого учебника — tooshow вы как toointegrate Soonr рабочему месту с Azure Active Directory (Azure AD).  
Интеграция с Azure AD Soonr рабочему месту предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего tooSoonr доступа к рабочему месту
- Можно включить на пользователей tooautomatically get вошедшего tooSoonr рабочему месту (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello классический портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD в рабочей области Soonr требуется hello следующих элементов:

- подписка Azure AD;
- подписка Soonr Workplace с поддержкой единого входа.


> [!NOTE] 
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.


tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не следует использовать рабочую среду при отсутствии необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).


## <a name="scenario-description"></a>Описание сценария
Hello цель этого учебника — tooenable tootest Azure AD единого входа в тестовой среде.  
Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление рабочей области Soonr из галереи hello
2. Настройка и проверка единого входа в Azure AD


## <a name="adding-soonr-workplace-from-hello-gallery"></a>Добавление рабочей области Soonr из галереи hello
tooconfigure hello интеграции Soonr рабочая область в Azure AD, вы должны tooadd Soonr рабочей области из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd Soonr рабочей области из галереи hello выполните следующие шаги hello.**

1. В hello **классический портал Azure**, на левой панели навигации hello, нажмите кнопку **Active Directory**. 

    ![Active Directory][1]

2. Из hello **каталога** список, выберите hello каталога, для которого требуется Интеграция каталогов tooenable.

3. Щелкните представление приложения hello tooopen в представлении каталога hello **приложений** в верхнем меню hello.

    ![Приложения][2]

4. Нажмите кнопку **добавить** hello нижней части страницы приветствия.

    ![Приложения][3]

5. На hello **что вам требуется toodo** диалоговое окно, нажмите кнопку **добавить приложение из коллекции hello**.
 
    ![Приложения][4]

6. Введите в поле поиска hello **рабочему месту Soonr**.
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_01.png)

7. В области результатов hello выберите **рабочему месту Soonr**и нажмите кнопку **завершить** tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_02.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
Цель этого раздела Hello является tooshow как tooconfigure и тестирования Azure AD единого входа в рабочей области Soonr на основе тестового пользователя с именем «Britta Simon».

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в рабочей области Soonr tooan пользователя в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в рабочей области Soonr должен установить toobe.  

Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** Soonr рабочем месте.

tooconfigure и тестирования Azure AD единого входа в рабочей области Soonr, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя рабочему месту Soonr](#creating-a-soonr-workplace-test-user)**  -toohave аналог Саймон Britta в рабочей области Soonr, представление связанных toohello Azure AD ей.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единого входа в классическом портале hello и настройки единого входа в приложении Soonr рабочей области.


**tooconfigure Azure AD единого входа в рабочей области Soonr, выполните следующие шаги hello.**

1. В классический портал Azure, на hello hello **рабочему месту Soonr** странице интеграции приложения щелкните **настроить единый вход** tooopen hello **настройки единого входа**  диалоговое окно.

    ![Настройка единого входа][6] 

2. На hello **предпочитаемый как toosign пользователей на рабочем месте tooSoonr** выберите **Azure AD Single Sign-On**, а затем нажмите кнопку **Далее**.

    ![Настройка единого входа](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_03.png) 

3. На hello **Настройка параметров приложения** диалогового окна выполните следующие шаги hello:.

    ![Настройка единого входа](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_04.png) 

    а. В hello **на URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello: `https://<server-name>.soonr.com/singlesignon/saml/SSO`.

    b. Щелкните **Далее**.

    > [!NOTE] 
    > Обратите внимание на то, что это не Вещественное значение hello. У вас есть tooupdate это значение с hello фактический URL-адрес входа. Обратитесь к рабочему месту Soonr поддержки команды tooget это значение.

4. На hello **настроить единый вход на рабочем месте Soonr** щелкните **загрузить метаданные** и затем сохраните файл hello на вашем компьютере:

    ![Настройка единого входа](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_05.png) 

5. tooget единого входа, настроенному для вашего приложения, обратитесь в службу поддержки Soonr рабочей области и предоставить им hello следующие: 

    • hello загружены **метаданные** файла

    • hello **URL-адрес издателя**

    • hello **URL-адрес единого входа SAML**

    • hello **URL-адрес службы единого выхода**

    >[!NOTE]
    >Это приложение заменяется <a href="https://azure.microsoft.com/en-us/marketplace/partners/autotask-corporataion/autotask/">Autotask рабочей области</a> и может указывать <a href="https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-autotaskworkplace-tutorial">это</a> учебника по настройке приложения hello в Azure AD.
   
6. В hello классический портал Azure, выберите Подтверждение настройки единого входа hello и нажмите кнопку **Далее**.

    ![Единый вход в Azure AD][10]

7. На hello **единого входа для подтверждения** щелкните **завершить**.  
  
    ![Единый вход в Azure AD][11]



### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в классический портал Azure, вызывается Britta Simon hello.  

![Создание пользователя Azure AD][20]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **классический портал Azure**, на левой панели навигации hello, нажмите кнопку **Active Directory**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_09.png) 

2. Из hello **каталога** список, выберите hello каталога, для которого требуется Интеграция каталогов tooenable.

3. Щелкните toodisplay hello список пользователей, выберите в меню в верхней части экрана приветствия hello **пользователей**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_03.png) 

4. tooopen hello **добавить пользователя** щелкните диалоговое окно в нижней hello инструментов hello **добавить пользователя**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_04.png) 

5. На hello **сообщите нам об этом пользователе** диалогового окна выполните следующие шаги hello:

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_05.png) 

    а. В поле «Тип пользователя» выберите значение «Новый пользователь в вашей организации».

    b. В имени пользователя hello **textbox**, тип **BrittaSimon**.

    c. Щелкните **Далее**.

6.  На hello **профиля пользователя** диалогового окна выполните следующие шаги hello:

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_06.png) 

    а. В hello **имя** введите **Britta**.  

    b. В hello **Фамилия** текстовое поле, тип, **Simon**.

    c. В hello **отображаемое имя** введите **Britta Simon**.

    d. В hello **роли** выберите **пользователя**.

    д. Щелкните **Далее**.

7. На hello **получение временного пароля** странице диалогового окна щелкните **создания**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_07.png) 

8. На hello **получение временного пароля** диалогового окна выполните следующие шаги hello:

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_08.png) 

    а. Запишите значение hello hello **новый пароль**.

    b. Нажмите **Завершено**.   



### <a name="creating-a-soonr-workplace-test-user"></a>Создание тестового пользователя Soonr Workplace

Цель этого раздела Hello — toocreate пользователя с именем Britta Simon Soonr рабочем месте. Обратитесь toocreate группы поддержки Soonr рабочее место пользователя на платформе hello. Может вызывать службу поддержки hello Soonr из <a href="https://na01.safelinks.protection.outlook.com/?url=http%3A%2F%2Fsoonr.com%2FAWPHelp%2FContent%2F0_HOME%2FSupport_for_End_Clients.htm&data=01%7C01%7Cv-saikra%40microsoft.com%7Ccbb4367ab09b4dacaac408d3eebe3f42%7C72f988bf86f141af91ab2d7cd011db47%7C1&sdata=FB92qtE6m%2Fd8yox7AnL2f1h%2FGXwSkma9x9H8Pz0955M%3D&reserved=0/">здесь</a>.


### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

Hello цель этого раздела — tooenabling toouse Britta Simon Azure единого входа путем предоставления ее tooSoonr доступа к рабочему месту.

![Назначение пользователя][200] 

**tooassign tooSoonr Britta Simon рабочему месту, выполните hello следующие шаги.**

1. Hello Azure представления приложения hello tooopen в представлении каталога hello классического портала щелкните **приложений** в верхнем меню hello.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **рабочему месту Soonr**.

    ![Настройка единого входа](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_50.png) 

1. В меню в верхней части hello hello выберите **пользователей**.

    ![Назначение пользователя][203] 

1. В списке пользователей hello выберите **Britta Simon**.

2. В нижней hello hello инструментов, нажмите кнопку **назначить**.

    ![Назначение пользователя][205]



### <a name="testing-single-sign-on"></a>Проверка единого входа

Цель этого раздела Hello является tootest настройки единого входа Azure AD с помощью панели доступа "hello".  
При нажатии кнопки hello рабочему месту Soonr плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour Soonr рабочей области приложения.


## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_205.png
