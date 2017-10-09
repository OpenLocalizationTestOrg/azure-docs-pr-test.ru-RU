---
title: "Руководство по интеграции Azure Active Directory с решением SilkRoad Life Suite | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и SilkRoad жизни набора."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 3cd92319-7964-41eb-8712-444f5c8b4d15
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/10/2017
ms.author: jeedes
ms.openlocfilehash: 07367282ab42b7332f166d64743b4b447aec4935
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-silkroad-life-suite"></a>Руководство по интеграции Azure Active Directory с решением SilkRoad Life Suite
Hello цель этого учебника — tooshow вы как toointegrate SilkRoad жизни набора с Azure Active Directory (Azure AD). 

Интеграция с Azure AD SilkRoad жизни Suite предоставляет hello следующие преимущества: 

* Можно управлять в Azure AD, имеющего доступ tooSilkRoad жизни набора 
* Вы можете включить учетные записи Azure AD вашей пользователей tooautomatically get вошедшего tooSilkRoad жизни набора единого входа (SSO)

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования
tooconfigure интеграция Azure AD с SilkRoad жизни набора необходимо hello следующих элементов:

* подписка Azure AD;
* подписка SilkRoad Life Suite с поддержкой единого входа.

>[!NOTE]
>в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде. 
> 

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

* Не следует использовать рабочую среду при отсутствии необходимости.
* Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/). 

## <a name="scenario-description"></a>Описание сценария
Hello цель этого учебника — tooenable вы tootest единого входа Azure AD в тестовой среде.

Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление SilkRoad жизни набора из галереи hello 
2. Настройка и проверка единого входа Azure AD.

## <a name="add-silkroad-life-suite-from-hello-gallery"></a>Добавьте набор жизни SilkRoad из галереи hello
tooconfigure hello интеграция SilkRoad жизни набора в Azure AD, вы должны tooadd SilkRoad жизни набора из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd SilkRoad жизни набора из галереи hello, выполните следующие шаги hello.**

1. В hello **классический портал Azure**, на левой панели навигации hello, нажмите кнопку **Active Directory**. 
   
    ![Active Directory][1]

2. Из hello **каталога** список, выберите hello каталога, для которого требуется Интеграция каталогов tooenable.

3. Щелкните представление приложения hello tooopen в представлении каталога hello **приложений** в верхнем меню hello.
   
    ![Приложения][2]

4. Нажмите кнопку **добавить** hello нижней части страницы приветствия.
   
    ![Приложения][3]

5. На hello **что вам требуется toodo** диалоговое окно, нажмите кнопку **добавить приложение из коллекции hello**.
   
    ![Приложения][4]

6. Введите в поле поиска hello **SilkRoad жизни набора**.
   
    ![Приложения][5]

7. В области результатов hello выберите **SilkRoad жизни набора**и нажмите кнопку **завершить** tooadd приложения hello.
   
    ![Приложения][50]

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
Цель этого раздела Hello является tooshow как tooconfigure и Azure AD SSO с SilkRoad жизни набора тестов на основе тестового пользователя с именем «Britta Simon».

Для toowork единого входа Azure AD необходима tooknow пользователь аналог какие hello в жизни набора SilkRoad tooan пользователя в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в наборе SilkRoad жизни должен установить toobe.

Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** SilkRoad жизни набора.

tooconfigure и теста Azure AD единого входа с SilkRoad жизни набора, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD единого входа](#configuring-azure-ad-single-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя Suite жизни SilkRoad](#creating-a-silkroad-life-suite-test-user)**  -toohave аналог Саймон Britta в наборе SilkRoad жизни, представление связанных toohello Azure AD ей.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configure-azure-ad-single-sign-on"></a>Настройка единого входа Azure AD
Цель этого раздела Hello — tooenable единого входа Azure AD в hello классический портал Azure и tooconfigure единого входа в приложении SilkRoad жизни набора.

**tooconfigure Azure AD единого входа с набором SilkRoad жизни, выполните следующие шаги hello.**

1. Корпоративный сайт SilkRoad tooyour входа от имени администратора. 

  >[!NOTE] 
  > toohello tooobtain доступа приложения проверки подлинности Suite жизни SilkRoad по настройке федерации с Microsoft Azure AD, обратитесь в службу поддержки SilkRoad либо с Вашим представителем службы SilkRoad.
  > 

2. Go слишком**поставщика услуг**и нажмите кнопку **сведения федерации**. 
   
    ![Единый вход в Azure AD][10] 

3. Нажмите кнопку **загрузить метаданные федерации**, а затем сохраните файл метаданных hello на вашем компьютере.
   
    ![Единый вход в Azure AD][11] 

4. В классический портал Azure, на hello hello **SilkRoad жизни набора** странице интеграции приложения щелкните **настроить единый вход** tooopen hello **настройки единого входа**  диалоговое окно.
   
    ![Настройка единого входа][6] 

5. На hello **предпочитаемый как toosign пользователей на tooSilkRoad жизни набора** выберите **Azure AD Single Sign-On**, а затем нажмите кнопку **Далее**.
   
    ![Единый вход в Azure AD][7] 

6. На hello **Настройка параметров приложения** диалогового окна выполните следующие шаги hello:
   
    ![Единый вход в Azure AD][8]   
 1. В hello **на URL-адрес входа** textbox hello введите URL-адрес, используемые на сайте SilkRoad жизни набора tooyour toosign на пользователей (например: *https://defcompanytest-test-redcarpet.silkroad-eng.com/Authentication/*).  
 2. Откройте hello загружены **Silkroad** файла метаданных. 
 3. Найдите hello **AssertionConsumerService** тега, а затем копировать hello **расположение** атрибута.         
   
    ![Единый вход в Azure AD][21] 
 4. Вставьте значение hello в hello **URL-адрес ответа** текстового поля.  
 5. Щелкните **Далее**.

6. На hello **настроить единый вход в жизни набора SilkRoad** выполните следующие шаги hello:
   
    ![Единый вход в Azure AD][9]  
 1. Нажмите кнопку загрузки сертификата, а затем сохраните файл hello на вашем компьютере.  
 2. Щелкните **Далее**.

7. В приложении **SilkRoad** щелкните **Authentication Sources** (Источники проверки подлинности).
   
    ![единого входа Azure AD][12] 

8. Щелкните **Add Authentication Source**(Добавить источник аутентификации). 
   
    ![Единый вход в Azure AD][13] 

9. В hello **добавить источник проверки подлинности** выполните следующие шаги hello: 
   
    ![Единый вход в Azure AD][14]  
 1. В разделе **вариант 2 - файл метаданных**, нажмите кнопку **Обзор** tooupload hello скачать файл метаданных.  
 2. Нажмите кнопку **Создать поставщик удостоверений с помощью данных из файла**.

10. В hello **источники проверки подлинности** щелкните **изменить**. 
    
     ![Единый вход в Azure AD][15] 

11. На hello **изменение проверки подлинности источника** диалоговое окно, выполните следующие шаги hello: 
    
     ![Единый вход в Azure AD][16] 
 1. В поле **Enabled** (Включено) выберите **Yes** (Да).   
 2. В hello **описание поставщика удостоверений** в текстовое поле введите описание для конфигурации (например: *единого входа Azure AD*).  
 3. В hello **имя поставщика удостоверений** текстовом поле введите имя, которое является tooyour определенной конфигурации (например: *Azure SP*).  
 4. Щелкните **Сохранить**.

12. Отключите все остальные источники аутентификации. 
    
     ![Единый вход в Azure AD][17]

13. В классический портал Azure, на hello hello **единого входа для подтверждения** щелкните **Далее**.  
    
     ![Единый вход в Azure AD][18]

14. На hello **единого входа для подтверждения** щелкните **завершить**.
    
     ![Единый вход в Azure AD][19]

### <a name="create-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в классический портал Azure, вызывается Britta Simon hello.

![Создание пользователя Azure AD][20]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **классический портал Azure**, на левой панели навигации hello, нажмите кнопку **Active Directory**.
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_09.png)  

2. Из hello **каталога** список, выберите hello каталога, для которого требуется Интеграция каталогов tooenable.

3. Щелкните toodisplay hello список пользователей, выберите в меню в верхней части экрана приветствия hello **пользователей**.
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_03.png) 

4. tooopen hello **добавить пользователя** щелкните диалоговое окно в нижней hello инструментов hello **добавить пользователя**. 
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_04.png) 

5. На hello **сообщите нам об этом пользователе** диалогового окна выполните следующие шаги hello: 
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_05.png)  
 1. В поле «Тип пользователя» выберите значение «Новый пользователь в вашей организации».  
 2. В имени пользователя hello **textbox**, тип **BrittaSimon**. 
 3. Щелкните **Далее**.

6. На hello **профиля пользователя** диалогового окна выполните следующие шаги hello: 
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_06.png)  
 1. В hello **имя** введите **Britta**.    
 2. В hello **Фамилия** текстовое поле, тип, **Simon**. 
 3. В hello **отображаемое имя** введите **Britta Simon**. 
 4. В hello **роли** выберите **пользователя**.
 5. Щелкните **Далее**.

7. На hello **получение временного пароля** странице диалогового окна щелкните **создания**.
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_07.png) 

8. На hello **получение временного пароля** диалогового окна выполните следующие шаги hello:
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_08.png)  
 1. Запишите значение hello hello **новый пароль**. 
 2. Нажмите **Завершено**.   

### <a name="create-a-silkroad-life-suite-test-user"></a>Создание тестового пользователя SilkRoad Life Suite
Цель этого раздела Hello — toocreate пользователя с именем Britta Simon SilkRoad жизни набора. Britta должен иметь идентификатор единого входа (иногда называется tooas *AuthParam*), соответствующий элемента Britta **emailaddress** в Azure AD.

**toocreate пользователя с именем Britta Simon SilkRoad жизни пакета, выполните следующие шаги hello.**

- Попросите пользователя с теми, что вашей toocreate team Suite жизни SilkRoad поддержки **код SSO** hello атрибута совпадает со значением в hello **emailaddress** из Britta Simon в Azure AD.

### <a name="assign-hello-azure-ad-test-user"></a>Назначить hello Azure AD тестового пользователя
Hello цель этого раздела — tooenable toouse Britta Simon единого входа в Azure, предоставляя свой доступ tooSilkRoad жизни набора.

![Назначение пользователя][200] 

**tooassign tooSilkRoad Britta Simon Suite жизни выполните hello следующие шаги.**

1. Hello Azure представления приложения hello tooopen в представлении каталога hello классического портала щелкните **приложений** в верхнем меню hello.
   
    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **SilkRoad жизни набора**.
   
    ![Назначение пользователя][202] 

3. В меню в верхней части hello hello выберите **пользователей**.
   
    ![Назначение пользователя][203] 

4. В списке пользователей hello выберите **Britta Simon**.

5. В нижней hello hello инструментов, нажмите кнопку **назначить**.
   
    ![Назначение пользователя][205]

### <a name="test-single-sign-on"></a>Проверка единого входа
Цель этого раздела Hello является tootest конфигурации единого входа Azure AD с помощью панели доступа "hello".  

При выборе плитки SilkRoad жизни набора hello в hello панели доступа, вы должны получить tooyour автоматически вошедшего Suite SilkRoad жизни приложения.

## <a name="additional-resources"></a>Дополнительные ресурсы
* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_01.png
[50]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_02.png

[6]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_05.png
[7]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_03.png
[8]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_04.png
[9]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_05.png
[10]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_06.png
[11]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_07.png
[12]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_08.png
[13]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_09.png
[14]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_10.png
[15]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_11.png
[16]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_12.png
[17]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_13.png
[18]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_06.png
[19]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_07.png


[20]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_100.png
[21]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_15.png


[200]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_14.png
[203]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_205.png





