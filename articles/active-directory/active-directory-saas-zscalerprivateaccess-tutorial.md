---
title: "Руководство по интеграции Azure Active Directory с Zscaler Private Access (ZPA) | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Zscaler закрытый доступ (ZPA)."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 83711115-1c4f-4dd7-907b-3da24b37c89e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: jeedes
ms.openlocfilehash: 0370cff60c8ac15bd1919acccc924da1e50dc45b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zscaler-private-access-zpa"></a>Руководство по интеграции Azure Active Directory с Zscaler Private Access (ZPA)

В этом учебнике вы узнаете, как toointegrate Zscaler закрытый доступ (ZPA) с Azure Active Directory (Azure AD).

Интеграция с Azure AD Zscaler закрытый доступ (ZPA) предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooZscaler закрытый доступ (ZPA)
- Ваш пользователей tooautomatically get вошедшего tooZscaler закрытый доступ (ZPA) (Single Sign-On) можно включить с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал управления Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с Zscaler закрытый доступ (ZPA) требуется hello следующих элементов:

- подписка Azure AD;
- подписка Zscaler Private Access (ZPA) с поддержкой единого входа.


> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.


tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не следует использовать рабочую среду при отсутствии необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).


## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление Zscaler закрытый доступ (ZPA) из коллекции hello
2. Настройка и проверка единого входа в Azure AD


## <a name="adding-zscaler-private-access-zpa-from-hello-gallery"></a>Добавление Zscaler закрытый доступ (ZPA) из коллекции hello
tooconfigure hello интеграция из Zscaler закрытый доступ (ZPA) в Azure AD, вы должны tooadd Zscaler закрытый доступ (ZPA) из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd Zscaler закрытый доступ (ZPA) из коллекции hello выполните следующие шаги hello.**

1. В hello  **[портала управления Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. Нажмите кнопку **добавить** кнопку в верхней части hello диалогового окна "hello".

    ![Приложения][3]

4. Введите в поле поиска hello **Zscaler закрытый доступ (ZPA)**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_001.png)

5. В панели результатов hello выберите **Zscaler закрытый доступ (ZPA)**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в Zscaler Private Access (ZPA) с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow какие пользователь аналог hello в Zscaler закрытый доступ (ZPA) является tooa в Azure AD. Иными словами связи между пользователя Azure AD и связанных пользователей hello в Zscaler закрытый доступ (ZPA) необходимо установить toobe.

Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в Zscaler закрытый доступ (ZPA).

tooconfigure и тестирования Azure AD единого входа с Zscaler закрытый доступ (ZPA), необходимы следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя Zscaler закрытый доступ (ZPA)](#creating-a-zscaler-private-access-(zpa)-test-user)**  -toohave аналог Саймон Britta в Zscaler закрытый доступ (ZPA), являющийся представлением ей связанного toohello Azure AD.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал управления Azure hello и настройки единого входа в приложение Zscaler закрытый доступ (ZPA).

**tooconfigure Azure AD единого входа с Zscaler закрытый доступ (ZPA), выполните следующие шаги hello.**

1. На портале управления Azure hello на hello **Zscaler закрытый доступ (ZPA)** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна, как **режим** выберите **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_300.png)
    
3. На hello **Zscaler закрытый доступ (ZPA) доменов и URL-адреса** выполните следующие шаги hello:
    
    ![Настройка единого входа](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_01.png)

    а. В hello **на URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://samlsp.private.zscaler.com/auth/login?domain=<your-domain-name>`

    b. В hello **идентификатор** введите:`https://samlsp.private.zscaler.com/auth/metadata`

    > [!NOTE] 
    > Обратите внимание на то, что они не hello реальные значения. У вас есть tooupdate входа эти значения с hello фактический URL-адрес и идентификатор. Здесь мы предлагаем вам toouse hello уникальное значение URL-адреса в hello идентификатор. Обратитесь к [группы поддержки Zscaler закрытый доступ (ZPA)](https://help.zscaler.com/zpa-submit-ticket) tooget эти значения.

4. На hello **сертификат подписи SAML** щелкните **Создание нового сертификата**.

    ![Настройка единого входа](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_400.png)   

5. На hello **создать новый сертификат** диалоговое окно, щелкните значок календаря hello и выберите **даты истечения срока действия**. Затем нажмите кнопку **Сохранить**.

    ![Настройка единого входа](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_500.png)

6. На hello **сертификат подписи SAML** выберите **активировать новый сертификат** и нажмите кнопку **Сохранить** кнопки.

    ![Настройка единого входа](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_02.png)

7. На всплывающее окно hello **сертификат продолжения** окно, нажмите кнопку **ОК**.

    ![Настройка единого входа](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_600.png)

8. На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.

    ![Настройка единого входа](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_03.png) 

9. В другом окне веб-браузера войдите на свой корпоративный сайт Zscaler Private Access (ZPA) в качестве администратора.

10. Перейдите в слишком**администратора** и нажмите кнопку **конфигурации поставщика удостоверений**.

    ![Настройка единого входа на стороне приложения](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_04.png)

11. В hello **конфигурации поставщика удостоверений** щелкните **Добавление новой конфигурации поставщика Удостоверений**.

    ![Настройка единого входа на стороне приложения](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_05.png)

12. В hello **новая конфигурация поставщика Удостоверений** выполните следующие шаги hello:

    ![Настройка единого входа на стороне приложения](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_06.png)

    а. Чтобы отправить скачанный файл метаданных, щелкните **Select File** (Выбрать файл).

    b. Нажмите кнопку **Сохранить** .
    


### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя на портале управления Azure hello, вызывается Саймон Britta.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал управления Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-zscalerprivateaccess-tutorial/create_aaduser_01.png) 

2. Go слишком**пользователей и групп** и нажмите кнопку **всех пользователей** toodisplay hello список пользователей.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-zscalerprivateaccess-tutorial/create_aaduser_02.png) 

3. Вверху hello диалоговое окно приветствия щелкните **добавить** tooopen hello **пользователя** диалогового окна.
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-zscalerprivateaccess-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-zscalerprivateaccess-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**. 



### <a name="creating-a-zscaler-private-access-zpa-test-user"></a>Создание тестового пользователя Zscaler Private Access (ZPA)

В этом разделе описано, как создать пользователя Britta Simon в приложении Zscaler Private Access (ZPA). Можно работать с [группы поддержки Zscaler закрытый доступ (ZPA)](https://help.zscaler.com/zpa-submit-ticket) tooadd hello пользователей на платформе hello Zscaler закрытый доступ (ZPA).


### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа, предоставляя свой доступ tooZscaler закрытый доступ (ZPA).

![Назначение пользователя][200] 

**tooassign tooZscaler Britta Simon закрытый доступ (ZPA), выполните следующие шаги hello.**

1. На портале управления Azure hello, открыть представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **Zscaler закрытый доступ (ZPA)**.

    ![Настройка единого входа](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_50.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    


### <a name="testing-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.

При нажатии кнопки hello Zscaler закрытый доступ (ZPA) плитки в панели доступа hello, вы должны получить приложения автоматически вошедшего tooyour Zscaler закрытый доступ (ZPA).


## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_203.png