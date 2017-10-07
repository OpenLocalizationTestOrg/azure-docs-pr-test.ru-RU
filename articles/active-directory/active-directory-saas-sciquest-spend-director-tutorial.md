---
title: "Руководство по интеграции Azure Active Directory с SciQuest Spend Director | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и SciQuest директор расходов."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 9fab641b-292e-4bef-91d1-8ccc4f3a0c1f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/17/2017
ms.author: jeedes
ms.openlocfilehash: 47c46f1297054fd96b86c1d8c66e1a55ec151497
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sciquest-spend-director"></a>Учебник. Интеграция Azure Active Directory с SciQuest Spend Director
Hello цель этого учебника — tooshow вы как toointegrate директор расходов SciQuest с Azure Active Directory (Azure AD).  
Интеграция с Azure AD директор расходов SciQuest предоставляет hello следующие преимущества: 

* Можно управлять в Azure AD, имеющего доступ tooSciQuest директор расходов 
* Можно включить на пользователей tooautomatically get вошедшего tooSciQuest директор расходов (Single Sign-On) с помощью своих учетных записей Azure AD
* Можно управлять учетными записями в одном централизованном месте - hello классический портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования
tooconfigure интеграция Azure AD с директор расходов SciQuest требуется hello следующих элементов:

* подписка Azure AD;
* подписка SciQuest Spend Director с включенным единым входом.

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

1. Добавление директор расходов SciQuest из галереи hello 
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-sciquest-spend-director-from-hello-gallery"></a>Добавление директор расходов SciQuest из галереи hello
tooconfigure hello интеграции SciQuest директор расходов в Azure AD, вы должны tooadd SciQuest директор расходов из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd директор расходов SciQuest из галереи hello выполните hello следующие шаги.**

1. В hello **классический портал Azure**, на левой панели навигации hello, нажмите кнопку **Active Directory**. 
   
    ![Active Directory][1]

2. Из hello **каталога** список, выберите hello каталога, для которого требуется Интеграция каталогов tooenable.

3. Щелкните представление приложения hello tooopen в представлении каталога hello **приложений** в верхнем меню hello.
   
    ![Приложения][2]

4. Нажмите кнопку **добавить** hello нижней части страницы приветствия.
   
    ![Приложения][3]

5. На hello **что вам требуется toodo** диалоговое окно, нажмите кнопку **добавить приложение из коллекции hello**.
   
    ![Приложения][4]

6. Введите в поле поиска hello **sciQuest тратить директора**.
   
    ![Приложения][5]

7. В области результатов hello выберите **директор расходов SciQuest**и нажмите кнопку **завершить** tooadd приложения hello.
   
    ![Приложения][6]

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
Цель этого раздела Hello является tooshow как tooconfigure и теста Azure AD единого входа с SciQuest директор расходов на основе тестового пользователя с именем «Britta Simon».

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в директор расходов SciQuest tooan пользователя в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в директор расходов SciQuest должен установить toobe.  
Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в SciQuest директор расходов.

tooconfigure и теста Azure AD единого входа с SciQuest директор расходов, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD один Single Sign-On](#configuring-azure-ad-single-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя директор расходов SciQuest](#creating-a-halogen-software-test-user)**  -toohave аналог Саймон Britta в SciQuest тратить директора, представление связанных toohello Azure AD ей.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-single-sign-on"></a>Настройка единого входа в Azure AD
Цель этого раздела Hello — tooenable Azure AD единого входа в hello классический портал Azure и tooconfigure единого входа в приложении SciQuest директор расходов.

**tooconfigure Azure AD единого входа с SciQuest директор расходов, выполните следующие шаги hello.**

1. В классический портал Azure, на hello hello **директор расходов SciQuest** странице интеграции приложения щелкните **настроить единый вход** tooopen hello **настройки единого входа**диалогового окна.
   
    ![Настройка единого входа][8]

2. На hello **предпочитаемый как toosign пользователей на tooSciQuest директор расходов** выберите **Azure AD Single Sign-On**, а затем нажмите кнопку **Далее**.
   
    ![Единый вход в Azure AD][9]

3. На hello **Настройка параметров приложения** диалогового окна выполните следующие шаги hello: 
   
    ![Настройка параметров приложения][10]
   
     а. В hello **на URL-адрес входа** текстовом поле введите URL-адрес, используемый вашей toosign пользователей в приложении директор расходов SciQuest tooyour, используя следующий шаблон hello: *https://.* sciquest.com/.**
   
     b. В hello **URL-адрес ответа** текстового поля, типа hello же значение, которое вы ввели в hello **на URL-адрес входа** текстового поля. 
   
     c. Щелкните **Далее**.

4. На hello **настроить единый вход в директор расходов SciQuest** нажмите кнопку **загрузить метаданные**, а затем сохраните файл метаданных hello на локальном компьютере.
   
    ![Что такое Azure AD Connect?][11]

5. Обратитесь в службу поддержки tooenable SciQuest этот метод проверки подлинности с использованием hello выше загрузки метаданных.

6. На hello классический портал Azure, выберите Подтверждение настройки единого входа hello и нажмите кнопку **завершить** tooclose hello **Настройка единого входа** диалогового окна. 
   
    ![Что такое Azure AD Connect?][15]

7. На hello **единого входа для подтверждения** щелкните **завершить**.  

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в классический портал Azure, вызывается Britta Simon hello.

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **классический портал Azure**, на левой панели навигации hello, нажмите кнопку **Active Directory**.
   
    ![Что такое Azure AD Connect?][100] 

2. Из hello **каталога** список, выберите hello каталога, для которого требуется Интеграция каталогов tooenable.

3. Щелкните toodisplay hello список пользователей, выберите в меню в верхней части экрана приветствия hello **пользователей**.
   
    ![Что такое Azure AD Connect?][101] 

4. tooopen hello **добавить пользователя** щелкните диалоговое окно в нижней hello инструментов hello **добавить пользователя**. 
   
    ![Что такое Azure AD Connect?][102] 

5. На hello **сообщите нам об этом пользователе** диалогового окна выполните следующие шаги hello:
   
    ![Что такое Azure AD Connect?][103] 
   
    а. В поле **Тип пользователя** выберите значение **Новый пользователь в вашей организации**.
   
    b. В имени пользователя hello **textbox**, тип **BrittaSimon**.
   
    c. Щелкните **Далее**.

6. На hello **профиля пользователя** диалогового окна выполните следующие шаги hello: 
   
    ![Что такое Azure AD Connect?][104] 
   
    а. В hello **имя** введите **Britta**.  
   
    b. В hello **Фамилия** txtbox, тип, **Simon**.
   
    c. В hello **отображаемое имя** введите **Britta Simon**.
   
    d. В hello **роли** выберите **пользователя**.
   
    д. Щелкните **Далее**.

7. На hello **получение временного пароля** странице диалогового окна щелкните **создания**.
   
    ![Что такое Azure AD Connect?][105]  

8. На hello **получение временного пароля** диалогового окна выполните следующие шаги hello:
   
    ![Что такое Azure AD Connect?][106]   
   
    а. Запишите значение hello hello **новый пароль**.
   
    b. Нажмите **Завершено**.   

### <a name="creating-a-sciquest-spend-director-test-user"></a>Создание тестового пользователя SciQuest Spend Director
Цель этого раздела Hello — toocreate пользователя с именем Саймон Britta в SciQuest директор расходов.

Требуется toocontact сотрудники службы поддержки SciQuest директор расходов и предоставить им hello сведения о вашей учетной записи tooget тестирования, она создана.

Вы также можете использовать JIT-подготовку — функцию единого входа, поддерживаемую SciQuest Spend Director.  
Если функция JIT-подготовки включена, SciQuest Spend Director автоматически создает пользователей при попытке единого входа, если они еще не созданы. Эта возможность устраняет необходимость hello toomanually создать аналог-пользователей.

Подготовка just-in-time tooget включен, необходимо toocontact вы сотрудники службы поддержки SciQuest директор расходов.

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя
Hello цель этого раздела — tooenabling toouse Britta Simon Azure единого входа, предоставляя свой доступ tooSciQuest директор расходов.

![Что такое Azure AD Connect?][200]

**tooassign tooSciQuest Britta Simon директор расходов, выполните hello следующие шаги.**

1. Hello Azure представления приложения hello tooopen в представлении каталога hello классического портала щелкните **приложений** в верхнем меню hello.
   
    ![Что такое Azure AD Connect?][201]

2. В списке приложений hello выберите **директор расходов SciQuest**.
   
    ![Что такое Azure AD Connect?][202]

3. В меню в верхней части hello hello выберите **пользователей**.
   
    ![Что такое Azure AD Connect?][203]

4. В списке пользователей hello выберите **Britta Simon**.
   
    ![Что такое Azure AD Connect?][204]

5. В нижней hello hello инструментов, нажмите кнопку **назначить**.
   
    ![Что такое Azure AD Connect?][205]

### <a name="testing-single-sign-on"></a>Проверка единого входа
Цель этого раздела Hello является tootest настройки единого входа Azure AD с помощью панели доступа "hello".  
При нажатии кнопки hello директор расходов SciQuest плитки в панели доступа hello, вы должны получить tooyour автоматически вошедшего директор расходов SciQuest приложения.

## <a name="additional-resources"></a>Дополнительные ресурсы
* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->
[1]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_01.png
[6]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_05.png
[8]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_06.png
[9]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_07.png
[10]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_08.png
[11]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_03.png
[15]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_04.png

[100]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_09.png 
[101]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_10.png 
[102]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_11.png 
[103]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_12.png 
[104]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_13.png 
[105]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_14.png 
[106]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_15.png 
[200]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_16.png 
[201]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_17.png 
[202]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_06.png
[203]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_18.png
[204]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_19.png
[205]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_20.png

