---
title: "Руководство. Интеграция Azure Active Directory с приложением Bynder | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Bynder."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 4fb0ab26-b3b9-420a-8072-a0be80ea021e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/17/2017
ms.author: jeedes
ms.openlocfilehash: a2a8477580d28fe422f2836f483dff286bc71c93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bynder"></a>Руководство. Интеграция Azure Active Directory с Bynder
Hello цель этого учебника — tooshow вы как toointegrate Bynder с Azure Active Directory (Azure AD).

Интеграция с Azure AD Bynder предоставляет hello следующие преимущества:

* Можно управлять в Azure AD, имеющего доступ tooBynder
* Можно включить на пользователей tooautomatically get tooBynder вошедшего единого входа (SSO) с помощью своих учетных записей Azure AD
* Можно управлять учетными записями в одном централизованном месте - hello классический портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования
tooconfigure интеграция Azure AD с Bynder требуется hello следующих элементов:

* подписка Azure AD;
* подписка на Bynder с поддержкой единого входа.

>[!NOTE]
>в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде. 
> 

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

* Не следует использовать рабочую среду при отсутствии необходимости.
* Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
Hello цель этого учебника — tooenable вы tootest Microsoft Azure AD, единого входа в тестовой среде.

Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление Bynder из галереи hello
2. Настройка и проверка единого входа Microsoft Azure AD.

## <a name="add-bynder-from-hello-gallery"></a>Добавление Bynder из коллекции hello
tooconfigure hello интеграции Bynder в Azure AD, вы должны tooadd Bynder из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd Bynder из галереи hello, выполните следующие шаги hello.**

1. В hello **классический портал Azure**, на левой панели навигации hello, нажмите кнопку **Active Directory**. 
   
    ![Active Directory][1]
2. Из hello **каталога** список, выберите hello каталога, для которого требуется Интеграция каталогов tooenable.
3. Щелкните представление приложения hello tooopen в представлении каталога hello **приложений** в верхнем меню hello.
   
    ![Приложения][2]
4. Нажмите кнопку **добавить** hello нижней части страницы приветствия.
   
    ![Приложения][3]
5. На hello **что вам требуется toodo** диалоговое окно, нажмите кнопку **добавить приложение из коллекции hello**.
   
    ![Приложения][4]
6. Введите в поле поиска hello **Bynder**.
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_01.png)
7. В панели результатов hello выберите **Bynder**и нажмите кнопку **завершить** tooadd приложения hello.
   
    ![При выборе приложение hello в галерее hello](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_001.png)

## <a name="configure-and-test-microsoft-azure-ad-sso"></a>Настройка и проверка единого входа Microsoft Azure AD
Цель этого раздела Hello является tooshow как tooconfigure и тестирования единого входа Microsoft Azure AD, с Bynder на основе тестового пользователя с именем «Britta Simon».

Для toowork единого входа Azure AD необходима tooknow пользователь аналог какие hello в Bynder tooan пользователя в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в Bynder должен установить toobe.

Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в Bynder.

tooconfigure и тестирования единого входа Microsoft Azure AD, с Bynder, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Microsoft Azure AD единого входа](#configuring-azure-ad-single-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Microsoft Azure AD Single Sign-On с Саймон Britta.
3. **[Создание тестового пользователя Bynder](#creating-a-bynder-test-user)**  -toohave аналог Саймон Britta в Bynder, представление связанных toohello Azure AD ей.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable toouse Britta Simon Microsoft Azure AD Single Sign-On.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-microsoft-azure-ad-sso"></a>Настройка единого входа Microsoft Azure AD
В этом разделе включить Microsoft Azure AD, единого входа в классическом портале hello и настройки единого входа в вашем приложении Bynder.

**tooconfigure Microsoft Azure AD и единого входа с Bynder, выполните следующие шаги hello.**

1. Классическом портале hello на hello **Bynder** странице интеграции приложения щелкните **настроить единый вход** tooopen hello **настройки единого входа** диалогового окна.
   
    ![Настройка единого входа][6] 
2. На hello **предпочитаемый как toosign пользователей на tooBynder** выберите **Microsoft Azure AD Single Sign-On**, а затем нажмите кнопку **Далее**.
   
    ![Настройка единого входа](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_03.png)
3. На hello **Настройка параметров приложения** странице диалогового окна, при желании tooconfigure приложения hello в **режиме, инициированный IDP**, выполните следующие шаги hello и нажмите кнопку **Далее**:
   
    ![Настройка единого входа](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_04.png)
  1. В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<company name>.getbynder.com/sso/SAML/authenticate/`
  2. Щелкните **Далее**.
4. При необходимости приложение hello tooconfigure в **режиме, инициируемая SP** на hello **Настройка параметров приложения** странице диалогового окна, а затем нажмите кнопку hello **«Дополнительные параметры (необязательно) Показать»**, а затем введите hello **на URL-адрес входа** и нажмите кнопку **Далее**.

    ![Настройка единого входа](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_10.png)
  1. В hello **на URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<company name>.getbynder.com/login/`
  2. Щелкните **Далее**.
  
   >[!NOTE]
   >Hello для hello на URL-адрес входа в этом учебнике значение просто placeholfer. Фактический vlaue tooget hello для вашей среды обратитесь к Bynder.
   >

5. На hello **настроить единый вход в Bynder** выполните следующие шаги hello и нажмите кнопку **Далее**:
   
    ![Настройка единого входа](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_05.png)  
  1. Нажмите кнопку **загрузить метаданные**, а затем сохраните файл hello на вашем компьютере.
  2. Щелкните **Далее**.
6. tooget единого входа, настроенному для вашего приложения, обратитесь в службу поддержки Bynder. Присоединение hello скачанный файл метаданных и предоставить Bynder tooset команды копирования единого входа с их стороны.
7. Hello классического портала выберите Подтверждение настройки единого входа hello и нажмите кнопку **Далее**.
   
    ![Единый вход в Azure AD][10]
8. На hello **единого входа для подтверждения** щелкните **завершить**.  
   
    ![Единый вход в Azure AD][11]

### <a name="create-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Hello цель этого раздела — toocreate тестового пользователя вызывается Саймон Britta классическом портале hello.

![Создание пользователя Azure AD][20]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **классический портал Azure**, на левой панели навигации hello, нажмите кнопку **Active Directory**.
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_09.png)
2. Из hello **каталога** список, выберите hello каталога, для которого требуется Интеграция каталогов tooenable.
3. Щелкните toodisplay hello список пользователей, выберите в меню в верхней части экрана приветствия hello **пользователей**.
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_03.png)
4. tooopen hello **добавить пользователя** щелкните диалоговое окно в нижней hello инструментов hello **добавить пользователя**.
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_04.png)
5. На hello **сообщите нам об этом пользователе** диалогового окна выполните следующие шаги hello:
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_05.png)
  1. В поле «Тип пользователя» выберите значение «Новый пользователь в вашей организации».
  2. В имени пользователя hello **textbox**, тип **BrittaSimon**.
  3. Щелкните **Далее**.
6. На hello **профиля пользователя** диалогового окна выполните следующие шаги hello:
   
   ![Создание тестового пользователя Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_06.png)
  1. В hello **имя** введите **Britta**.  
  2. В hello **Фамилия** текстовое поле, тип, **Simon**. 
  3. В hello **отображаемое имя** введите **Britta Simon**.
  4. В hello **роли** выберите **пользователя**.
  5. Щелкните **Далее**.
7. На hello **получение временного пароля** странице диалогового окна щелкните **создания**.
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_07.png)
8. На hello **получение временного пароля** диалогового окна выполните следующие шаги hello:
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_08.png)
   1. Запишите значение hello hello **новый пароль**.
   2. Нажмите **Завершено**.   

### <a name="create-a-bynder-test-user"></a>Создание тестового пользователя Bynder
Цель этого раздела Hello — toocreate пользователя с именем Саймон Britta в Bynder. Приложение Bynder поддерживает JIT-подготовку. Эта функция включена по умолчанию.

В этом разделе никакие действия с вашей стороны не требуются. Если он еще не существует во время попытки tooaccess Bynder создается новый пользователь.

>[!NOTE]
>Если вам требуется toocreate пользователя вручную, необходимо группа поддержки Bynder toocontact hello. 
> 

### <a name="assign-hello-azure-ad-test-user"></a>Назначить hello Azure AD тестового пользователя
Hello цель этого раздела — tooenabling toouse Britta Simon единого входа Azure, предоставляя свой tooBynder доступа.

   ![Назначение пользователя][200]

**tooassign tooBynder Britta Simon выполните следующие шаги hello.**

1. Hello классического портала щелкните представление приложения hello tooopen в представлении каталога hello **приложений** в верхнем меню hello.
   
    ![Назначение пользователя][201]
2. В списке приложений hello выберите **Bynder**.
   
    ![Настройка единого входа](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_50.png)
3. В меню в верхней части hello hello выберите **пользователей**.
   
    ![Назначение пользователя][203]
4. В списке пользователей hello выберите **Britta Simon**.
5. В нижней hello hello инструментов, нажмите кнопку **назначить**.
   
    ![Назначение пользователя][205]

### <a name="test-single-sign-on"></a>Проверка единого входа
Цель этого раздела Hello является tootest конфигурации Microsoft Azure AD, единого входа с помощью панели доступа "hello".

При нажатии кнопки hello Bynder плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour Bynder приложения.

## <a name="additional-resources"></a>Дополнительные ресурсы
* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_205.png
