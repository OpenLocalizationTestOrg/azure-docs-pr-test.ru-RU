---
title: "Руководство по интеграции Azure Active Directory с Wizergos Productivity Software | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Wizergos производительном программном обеспечении."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: acc04396-13c5-4c24-ab9a-30fbc9234ebd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/20/2017
ms.author: jeedes
ms.openlocfilehash: cdd186c38c426dde404ed8bb84700faf9c8c1a46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-wizergos-productivity-software"></a>Руководство. Интеграция Azure Active Directory с Wizergos Productivity Software
Hello цель этого учебника — tooshow вы как toointegrate Wizergos офисного программного обеспечения в Azure Active Directory (Azure AD).

Интеграция программного обеспечения производительности Wizergos с Azure AD предоставляет hello следующие преимущества:

* Можно управлять в Azure AD, имеющего доступ tooWizergos производительном программном обеспечении
* Вы можете включить учетные записи Azure AD вашей пользователей tooautomatically get вошедшего tooWizergos производительности программного обеспечения единого входа (SSO)
* Можно управлять учетными записями в одном централизованном месте - hello классический портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования
tooconfigure интеграция Azure AD с программным обеспечением для повышения производительности Wizergos требуется hello следующих элементов:

* подписка Azure AD;
* подписка на Wizergos Productivity Software с поддержкой единого входа.

>[!NOTE]
>в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде. 
> 

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

* Не следует использовать рабочую среду при отсутствии необходимости.
* Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
Hello цель этого учебника — tooenable вы tootest единого входа Azure AD в тестовой среде.

Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление программного обеспечения производительности Wizergos из галереи hello
2. Настройка и проверка единого входа Azure AD.

## <a name="adding-wizergos-productivity-software-from-hello-gallery"></a>Добавление программного обеспечения производительности Wizergos из галереи hello
tooconfigure hello интеграция Wizergos производительности программного обеспечения в Azure AD, вы должны tooadd Wizergos производительном программном обеспечении из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd Wizergos производительном программном обеспечении из библиотеки hello, выполните следующие шаги hello.**

1. В hello **классический портал Azure**, на левой панели навигации hello, нажмите кнопку **Active Directory**. 
   
    ![Active Directory][1]
2. Из hello **каталога** список, выберите hello каталога, для которого требуется Интеграция каталогов tooenable.
3. Щелкните представление приложения hello tooopen в представлении каталога hello **приложений** в верхнем меню hello.
   
    ![Приложения][2]
4. Нажмите кнопку **добавить** hello нижней части страницы приветствия.
   
    ![Приложения][3]
5. На hello **что вам требуется toodo** диалоговое окно, нажмите кнопку **добавить приложение из коллекции hello**.
   
    ![Приложения][4]
6. Введите в поле поиска hello **Wizergos производительном программном обеспечении**.
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_01.png)
7. В панели результатов hello выберите **Wizergos производительном программном обеспечении**и нажмите кнопку **завершить** tooadd приложения hello.
   
    ![При выборе приложение hello в галерее hello](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_001.png)

## <a name="configure-and-test-azure-ad-sso"></a>Настройка и проверка единого входа Azure AD
Цель этого раздела Hello является tooshow как tooconfigure и тестирования единого входа Azure AD, с программным обеспечением Wizergos производительности на основе тестового пользователя с именем «Britta Simon».

Для toowork единого входа Azure AD необходима tooknow пользователь аналог какие hello в Wizergos производительном программном обеспечении tooan пользователя в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в программном обеспечении производительности Wizergos должен установить toobe.

Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в Wizergos производительном программном обеспечении.

tooconfigure и теста Azure AD единого входа с Softwareder BynWizergos производительность, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD единого входа](#configuring-azure-ad-single-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя производительном программном обеспечении Wizergos](#creating-a-wizergos-productivity-software-test-user)**  -toohave аналог Саймон Britta в Wizergos производительном программном обеспечении, представление связанных toohello Azure AD ей.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-sso"></a>Настройка единого входа Azure AD
В этом разделе включения Azure AD единого входа в классическом портале hello и настройки единого входа в приложении Wizergos производительном программном обеспечении.

**tooconfigure Azure AD единого входа с Wizergos производительном программном обеспечении, выполните следующие шаги hello.**

1. Классическом портале hello на hello **Wizergos производительном программном обеспечении** странице интеграции приложения щелкните **настроить единый вход** tooopen hello **настройки единого входа**диалогового окна.
   
    ![Настройка единого входа][6] 
2. На hello **предпочитаемый как toosign пользователей на tooWizergos производительном программном обеспечении** выберите **Azure AD Single Sign-On**, а затем нажмите кнопку **Далее**:
   
    ![Настройка единого входа](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_03.png)
3. На hello **Настройка параметров приложения** странице диалогового окна щелкните **Далее**:
   
    ![Настройка единого входа](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_04.png)
4. На hello **настроить единый вход в Wizergos производительном программном обеспечении** щелкните **загрузки сертификата**, а затем сохраните файл hello на компьютере:
   
    ![Настройка единого входа](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_05.png)
5. В другом окне браузера, клиент производительном программном обеспечении Wizergos tooyour входа от имени администратора.
6. Меню "гамбургер" hello выберите **администратора**.
   
    ![Настройка единого входа на стороне приложения](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_000.png)
7. На странице администрирования в меню слева выберите **Проверка подлинности** и нажмите кнопку **Azure AD**.
   
    ![Настройка единого входа на стороне приложения](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_002.png)
8. Выполнить hello, выполните действия **проверки ПОДЛИННОСТИ** раздела.
   
    ![Настройка единого входа на стороне приложения](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_003.png)
  1. Нажмите кнопку **отправить** hello tooupload кнопку Загрузить сертификат из Azure AD. 
  2. В hello **URL-адрес издателя** textbox помещение значения hello **URL-адрес издателя** из мастера настройки приложения Azure AD.
  3. В hello **-URL** textbox помещение значения hello **входа адрес службы единого** из мастера настройки приложения Azure AD.
  4. В hello **URL-адрес единого выхода** textbox помещение значения hello **URL-адрес службы единого выхода** из мастера настройки приложения Azure AD.
  5. Нажмите кнопку **Сохранить** .
9. Hello классического портала выберите Подтверждение настройки единого входа hello и нажмите кнопку **Далее**.
   
    ![Единый вход в Azure AD][10]
10. На hello **единого входа для подтверждения** щелкните **завершить**.  
    
    ![Единый вход в Azure AD][11]

### <a name="create-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Hello цель этого раздела — toocreate тестового пользователя вызывается Саймон Britta классическом портале hello.

![Создание пользователя Azure AD][20]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **классический портал Azure**, на левой панели навигации hello, нажмите кнопку **Active Directory**.
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_09.png)
2. Из hello **каталога** список, выберите hello каталога, для которого требуется Интеграция каталогов tooenable.
3. Щелкните toodisplay hello список пользователей, выберите в меню в верхней части экрана приветствия hello **пользователей**.
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_03.png)
4. tooopen hello **добавить пользователя** щелкните диалоговое окно в нижней hello инструментов hello **добавить пользователя**.
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_04.png)
5. На hello **сообщите нам об этом пользователе** диалогового окна выполните следующие шаги hello:
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_05.png) 
  1. В поле «Тип пользователя» выберите значение «Новый пользователь в вашей организации».
  2. В имени пользователя hello **textbox**, тип **BrittaSimon**.
  3. Щелкните **Далее**.
6. На hello **профиля пользователя** диалогового окна выполните следующие шаги hello:
   
   ![Создание тестового пользователя Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_06.png)
  1. В hello **имя** введите **Britta**.  
  2. В hello **Фамилия** текстовое поле, тип, **Simon**.
  3. В hello **отображаемое имя** введите **Britta Simon**.
  4. В hello **роли** выберите **пользователя**.
  5. Щелкните **Далее**.
7. На hello **получение временного пароля** странице диалогового окна щелкните **создания**.
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_07.png)
8. На hello **получение временного пароля** диалогового окна выполните следующие шаги hello:
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_08.png)
  1. Запишите значение hello hello **новый пароль**.
  2. Нажмите **Завершено**.   

### <a name="create-a-wizergos-productivity-software-test-user"></a>Создание тестового пользователя Wizergos Productivity Software
В этом разделе описано, как создать пользователя Britta Simon в приложении Wizergos Productivity Software. Следует работать с группой поддержки Wizergos производительном программном обеспечении через [ support@wizergos.com ](emailTo:support@wizergos.com) tooadd hello пользователей на платформе Wizergos офисные приложения hello.

### <a name="assign-hello-azure-ad-test-user"></a>Назначить hello Azure AD тестового пользователя
Hello цель этого раздела — tooenabling toouse Britta Simon единого входа в Azure, предоставляя свой доступ tooWizergos производительности программного обеспечения.

  ![Назначение пользователя][200]

**tooassign tooWizergos Britta Simon производительном программном обеспечении выполните hello следующие шаги.**

1. Hello классического портала щелкните представление приложения hello tooopen в представлении каталога hello **приложений** в верхнем меню hello.
   
    ![Назначение пользователя][201]
2. В списке приложений hello выберите **Wizergos производительном программном обеспечении**.
   
    ![Настройка единого входа](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_50.png)
3. В меню в верхней части hello hello выберите **пользователей**.
   
    ![Назначение пользователя][203]
4. В списке пользователей hello выберите **Britta Simon**.
5. В нижней hello hello инструментов, нажмите кнопку **назначить**.
   
    ![Назначение пользователя][205]

### <a name="test-single-sign-on"></a>Проверка единого входа
Цель этого раздела Hello является tootest конфигурации единого входа Azure AD с помощью панели доступа "hello".

Если щелкнуть плитку Wizergos офисные приложения hello в hello панели доступа, следует получать автоматически вошедшего tooyour Wizergos производительность приложения.

## <a name="additional-resources"></a>Дополнительные ресурсы
* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_205.png
