---
title: "Руководство. Интеграция Azure Active Directory с FirmPlay — Employee Advocacy for Recruiting | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и FirmPlay - представительство найму сотрудников."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a6799629-7546-43f8-a966-956db32864b1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/15/2017
ms.author: jeedes
ms.openlocfilehash: f143e0bb8f2a42de880d77e5f033694ce3f09cdb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-firmplay---employee-advocacy-for-recruiting"></a>Руководство. Интеграция Azure Active Directory с FirmPlay — Employee Advocacy for Recruiting

В этом учебнике вы узнаете, как toointegrate FirmPlay - сотрудник представительство найму с Azure Active Directory (Azure AD).

Интеграция FirmPlay - сотрудник представительство найму с Azure AD предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooFirmPlay - сотрудник представительство найму
- Ваш пользователей tooautomatically get вошедшего tooFirmPlay - сотрудник представительство найму (Single Sign-On) можно включить с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал управления Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

Интеграция Azure AD с FirmPlay - сотрудник представительство найму, tooconfigure требуется hello следующих элементов:

- подписка Azure AD;
- подписка на FirmPlay — Employee Advocacy for Recruiting с поддержкой единого входа.


> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.


tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не следует использовать рабочую среду при отсутствии необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).


## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление FirmPlay - сотрудник представительство найму из галереи hello
2. Настройка и проверка единого входа в Azure AD


## <a name="adding-firmplay---employee-advocacy-for-recruiting-from-hello-gallery"></a>Добавление FirmPlay - сотрудник представительство найму из галереи hello
Интеграция hello tooconfigure FirmPlay - сотрудник представительство найму в Azure AD необходимо tooadd FirmPlay - сотрудник представительство найму из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd FirmPlay - сотрудник представительство найму из галереи hello, выполните следующие шаги hello.**

1. В hello ** [портала управления Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. Нажмите кнопку **добавить** кнопку в верхней части hello диалогового окна "hello".

    ![Приложения][3]

4. Введите в поле поиска hello **FirmPlay - сотрудник представительство найму**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_001.png)

5. В панели результатов hello выберите **FirmPlay - сотрудник представительство найму**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в FirmPlay — Employee Advocacy for Recruiting с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в FirmPlay - сотрудник представительство найму является tooa в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в FirmPlay - сотрудник представительство найму должен установить toobe.

Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **имя пользователя** в FirmPlay - представительство найму сотрудников.

tooconfigure и теста Azure AD единого входа с FirmPlay - сотрудник представительство найму, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on) ** -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user) ** -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание сотрудника представительство найму тестового пользователя FirmPlay -](#creating-a-firmplay---employee-advocacy-for-recruiting-test-user) ** -toohave аналог Саймон Britta в FirmPlay: операции Employee для сотрудников, то есть связанные представление ей toohello Azure AD.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on) ** -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал управления Azure hello и настройки единого входа в вашей FirmPlay - приложение по найму представительство сотрудника.

**tooconfigure Azure AD единого входа с FirmPlay - сотрудник представительство найму, выполните следующие шаги hello.**

1. На портале управления Azure hello на hello **FirmPlay - сотрудник представительство найму** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна, как **режим** выберите **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_01.png)

3. На hello **FirmPlay - представительство сотрудников о приеме на работу домена и URL-адреса** раздела hello **на URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<your-subdomain>.firmplay.com/`

    ![Настройка единого входа](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_02.png)

    > [!NOTE] 
    > Обратите внимание на то, что это не Вещественное значение hello. У вас есть tooupdate это значение с hello фактический URL-адрес входа. Обратитесь к [FirmPlay - сотрудник представительство группа поддержки по найму](mailto:engineering@firmplay.com) tooget это значение. 

4. На hello **сертификат подписи SAML** щелкните **Создание нового сертификата**.

    ![Настройка единого входа](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_03.png)   

5. На hello **создать новый сертификат** диалоговое окно, щелкните значок календаря hello и выберите **даты истечения срока действия**. Затем нажмите кнопку **Сохранить**.

    ![Настройка единого входа](./media/active-directory-saas-firmplay-tutorial/tutorial_general_300.png)

6. На hello **сертификат подписи SAML** выберите **активировать новый сертификат** и нажмите кнопку **Сохранить** кнопки.

    ![Настройка единого входа](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_04.png)

7. На всплывающее окно hello **сертификат продолжения** окно, нажмите кнопку **ОК**.

    ![Настройка единого входа](./media/active-directory-saas-firmplay-tutorial/tutorial_general_400.png)

8. На hello **сертификат подписи SAML** щелкните **сертификата (base64)** и затем сохраните файл сертификата hello на вашем компьютере. 

    ![Настройка единого входа](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_05.png) 

9. На hello **FirmPlay - представительство конфигурации о приеме на работу сотрудника** щелкните **FirmPlay Настройка - сотрудник представительство найму** tooopen **Настройкавхода**диалогового окна.

    ![Настройка единого входа](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_06.png) 

    ![Настройка единого входа](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_07.png)

10. tooget SSO настроен для вашего приложения, обратитесь в службу [FirmPlay - сотрудник представительство группа поддержки по найму](mailto:engineering@firmplay.com) и предоставить им hello следующее: 

    • hello загружены **файл сертификата**

    • hello **SAML единого входа URL-адрес службы**

    • hello **SAML идентификатор сущности**

    • hello **URL-адрес выхода**
  

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя на портале управления Azure hello, вызывается Саймон Britta.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал управления Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-firmplay-tutorial/create_aaduser_01.png) 

2. Go слишком**пользователей и групп** и нажмите кнопку **всех пользователей** toodisplay hello список пользователей.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-firmplay-tutorial/create_aaduser_02.png) 

3. Вверху hello диалоговое окно приветствия щелкните **добавить** tooopen hello **пользователя** диалогового окна.
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-firmplay-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-firmplay-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**. 



### <a name="creating-a-firmplay---employee-advocacy-for-recruiting-test-user"></a>Создание тестового пользователя FirmPlay — Employee Advocacy for Recruiting

В этом разделе вы создадите тестового пользователя FirmPlay — Employee Advocacy for Recruiting с именем Britta Simon. Обратитесь [FirmPlay - сотрудник представительство группа поддержки по найму](mailto:engineering@firmplay.com) tooadd пользователей hello в hello FirmPlay - сотрудник представительство найму платформы.


### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе Включить toouse Britta Simon Azure единого входа, предоставляя свой доступ tooFirmPlay - представительство найму сотрудников.

![Назначение пользователя][200] 

**tooassign tooFirmPlay Britta Simon - сотрудник представительство найму, выполните hello следующие шаги.**

1. На портале управления Azure hello, открыть представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **FirmPlay - сотрудник представительство найму**.

    ![Настройка единого входа](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_50.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    


### <a name="testing-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.

При нажатии кнопки hello FirmPlay - сотрудник представительство найму плитки в панели доступа hello следует получать автоматически вошедшего tooyour FirmPlay - приложение по найму представительство сотрудника.


## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_203.png