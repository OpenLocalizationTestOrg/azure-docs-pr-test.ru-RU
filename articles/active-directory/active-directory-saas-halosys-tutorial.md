---
title: "Руководство по интеграции Azure Active Directory с Halosys | Документация Майкрософт"
description: "Узнайте, как toouse Halosys с Azure Active Directory tooenable единого входа, автоматизированной подготовки и многое другое!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 42a0eb7c-5cb7-44a9-b00b-b0e7df4b63e8
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 18043ed1b6f7ab45c59cfd36252bef1621618e51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-halosys"></a>Руководство по интеграции Azure Active Directory с Halosys

В этом учебнике вы узнаете, как toointegrate Halosys с Azure Active Directory (Azure AD).

Интеграция с Azure AD Halosys предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooHalosys
- Можно включить на пользователей tooautomatically get вошедшего tooHalosys (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello классический портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с Halosys требуется hello следующих элементов:

- подписка Azure AD;
- подписка Halosys с поддержкой единого входа.


> [!NOTE] 
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.


tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не следует использовать рабочую среду при отсутствии необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).


## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.

Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление Halosys из галереи hello
2. Настройка и проверка единого входа в Azure AD


## <a name="adding-halosys-from-hello-gallery"></a>Добавление Halosys из галереи hello
tooconfigure hello интеграции Halosys в Azure AD, вы должны tooadd Halosys из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd Halosys из галереи hello, выполните следующие шаги hello.**

1. В hello **классический портал Azure**, на левой панели навигации hello, нажмите кнопку **Active Directory**.

    ![Active Directory][1]
2. Из hello **каталога** список, выберите hello каталога, для которого требуется Интеграция каталогов tooenable.

3. Щелкните представление приложения hello tooopen в представлении каталога hello **приложений** в верхнем меню hello.

    ![Приложения][2]

4. Нажмите кнопку **добавить** hello нижней части страницы приветствия.

    ![Приложения][3]

5. На hello **что вам требуется toodo** диалоговое окно, нажмите кнопку **добавить приложение из коллекции hello**.

    ![Приложения][4]

6. Введите в поле поиска hello **Halosys**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_01.png)
    
7. В области результатов hello выберите **Halosys**и нажмите кнопку **завершить** tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_011.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в Halosys с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Halosys является tooa в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в Halosys должен установить toobe.

Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в Halosys.

tooconfigure и теста Azure AD единого входа с Halosys, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя Halosys](#creating-a-halosys-test-user)**  -toohave аналог Саймон Britta в Halosys, представление связанных toohello Azure AD ей.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единого входа в классическом портале hello и настройки единого входа в приложении Halosys.


**tooconfigure Azure AD единого входа с Halosys, выполните следующие шаги hello.**

1. Классическом портале hello на hello **Halosys** странице интеграции приложения щелкните **настроить единый вход** tooopen hello **настройки единого входа** диалогового окна.
     
    ![Настройка единого входа][6] 

2. На hello **предпочитаемый как toosign пользователей на tooHalosys** выберите **Azure AD Single Sign-On**, а затем нажмите кнопку **Далее**.

    ![Настройка единого входа](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_03.png) 

3. На hello **Настройка параметров приложения** диалогового окна выполните следующие шаги hello:

    ![Настройка единого входа](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_04.png) 

    а. В hello **на URL-адрес входа** текстовом поле введите URL-адрес hello, используемого приложением Halosys tooyour toosign на пользователей, используя следующий шаблон hello: `https://<company-name>.Halosys.com/client-api/api`.

    b.In hello **URL-адрес идентификатора** текстовом поле введите URL-адрес hello в hello следующий шаблон: `https://<company-name>.Halosys.com`. 
         
4. На hello **настроить единый вход в Halosys** щелкните **загрузить метаданные**, а затем сохраните файл hello на вашем компьютере:

    ![Настройка единого входа](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_05.png)
   
5. tooget единого входа, настроенному для вашего приложения, обратитесь в службу поддержки Halosys и предоставить им hello следующее:

    • hello загружены **файл метаданных**
    
    • hello **URL-адрес единого входа SAML**
    

6. Hello классического портала выберите Подтверждение настройки единого входа hello и нажмите кнопку **Далее**.
    
    ![Единый вход в Azure AD][10]

7. На hello **единого входа для подтверждения** щелкните **завершить**.  
 
    ![Единый вход в Azure AD][11]


### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
В этом разделе создайте тестового пользователя вызывается Саймон Britta классическом портале hello.


![Создание пользователя Azure AD][20]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **классический портал Azure**, на левой панели навигации hello, нажмите кнопку **Active Directory**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_09.png) 

2. Из hello **каталога** список, выберите hello каталога, для которого требуется Интеграция каталогов tooenable.

3. Щелкните toodisplay hello список пользователей, выберите в меню в верхней части экрана приветствия hello **пользователей**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_03.png) 

4. tooopen hello **добавить пользователя** щелкните диалоговое окно в нижней hello инструментов hello **добавить пользователя**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_04.png) 

5. На hello **сообщите нам об этом пользователе** диалогового окна выполните следующие шаги hello: ![Создание тестового пользователя Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_05.png) 

    а. В поле «Тип пользователя» выберите значение «Новый пользователь в вашей организации».

    b. В имени пользователя hello **textbox**, тип **BrittaSimon**.

    c. Щелкните **Далее**.

6.  На hello **профиля пользователя** диалогового окна выполните следующие шаги hello: ![Создание тестового пользователя Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_06.png) 

    а. В hello **имя** введите **Britta**.  

    b. В hello **Фамилия** текстовое поле, тип, **Simon**.

    c. В hello **отображаемое имя** введите **Britta Simon**.

    d. В hello **роли** выберите **пользователя**.

    д. Щелкните **Далее**.

7. На hello **получение временного пароля** странице диалогового окна щелкните **создания**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_07.png) 

8. На hello **получение временного пароля** диалогового окна выполните следующие шаги hello:

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_08.png) 

    а. Запишите значение hello hello **новый пароль**.

    b. Нажмите **Завершено**.   



### <a name="creating-a-halosys-test-user"></a>Создание тестового пользователя Halosys

В этом разделе описано, как создать пользователя Britta Simon в приложении Halosys. Обратитесь Halosys пользователи поддержки team tooadd hello в платформе Halosys hello.


### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления ее tooHalosys доступа.

![Назначение пользователя][200] 

**tooassign tooHalosys Britta Simon выполните следующие шаги hello.**

1. Hello классического портала щелкните представление приложения hello tooopen в представлении каталога hello **приложений** в верхнем меню hello.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **Halosys**.

    ![Настройка единого входа](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_50.png) 

3. В меню в верхней части hello hello выберите **пользователей**.

    ![Назначение пользователя][203]

4. В списке пользователей hello выберите **Britta Simon**.

5. В нижней hello hello инструментов, нажмите кнопку **назначить**.

    ![Назначение пользователя][205]


### <a name="testing-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.

При нажатии кнопки Halosys плитки в панели доступа hello приветствия, вы должны получить автоматически вошедшего tooyour Halosys приложения.


## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_205.png
