---
title: "Учебник. Интеграция Azure Active Directory с Skillport | Документы Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Skillport."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4df349b2-a73f-4b88-a077-ec0fbfc26527
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: jeedes
ms.openlocfilehash: ba504c3cae5f92767eb90d8453887904690fe0c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-skillport"></a>Руководство по интеграции Azure Active Directory с Skillport

В этом учебнике вы узнаете, как toointegrate Skillport с Azure Active Directory (Azure AD).

Интеграция с Azure AD Skillport предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooSkillport
- Можно включить на пользователей tooautomatically get вошедшего tooSkillport (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с Skillport требуется hello следующих элементов:

- подписка Azure AD;
- подписка на Skillport с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление Skillport из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-skillport-from-hello-gallery"></a>Добавление Skillport из галереи hello
tooconfigure hello интеграции Skillport в Azure AD, вы должны tooadd Skillport из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd Skillport из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. Нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна "hello".

    ![Приложения][3]

4. Введите в поле поиска hello **Skillport**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_search.png)

5. В панели результатов hello выберите **Skillport**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в Skillport с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Skillport является tooa в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в Skillport должен установить toobe.

Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в Skillport.

tooconfigure и теста Azure AD единого входа с Skillport, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя Skillport](#creating-a-skillport-test-user)**  -toohave аналог Саймон Britta в Skillport, который представляет связанный toohello Azure AD пользователя.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Skillport.

**tooconfigure Azure AD единого входа с Skillport, выполните следующие шаги hello.**

1. В hello в hello портала Azure **Skillport** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_samlbase.png)

3. На hello **URL-адреса и домена Skillport** выполните следующие шаги hello:

    ![Настройка единого входа](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_url.png)

    а. В hello **URL-адрес входа** текстовое поле, введите URL-адрес, используя hello следующие шаблоны:
      
      Центр обработки данных в ЕС: `https://<subdomain>.skillport.eu`
   
      Центр обработки данных в США: `https://<subdomain>.skillport.com`
   
    b. В hello **URL-адрес ответа** текстовое поле, введите URL-адрес, используя hello следующие шаблоны:
    
      Центр обработки данных в ЕС: `https://<subdomain>.skillport.eu/adfs/ls/`
    
      Центр обработки данных в США: `https://<subdomain>.skillport.com/sp/ACS.saml2`

    > [!NOTE] 
    > Эти значения не являются реальными hello. Обновите эти значения с hello фактический URL-адрес ответа и URL-адрес входа. Обратитесь к [группа поддержки клиента Skillport](https://www.skillsoft.com/contact.asp) tooget эти значения.
 
4. На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и сохраните hello XML-файл на компьютере.

    ![Настройка единого входа](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-skillport-tutorial/tutorial_general_400.png)

6. tooconfigure единого входа на **Skillport** стороны, необходимо загрузить hello toosend **метаданные в формате XML** слишком[Skillport поддержки](https://www.skillsoft.com/contact.asp). Они устанавливаются его toohave hello правильно настроенной на обеих сторонах соединения единого входа SAML.

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-skillport-tutorial/create_aaduser_01.png) 

2. Go слишком**пользователей и групп** и нажмите кнопку **всех пользователей** toodisplay hello список пользователей.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-skillport-tutorial/create_aaduser_02.png) 

3. Вверху hello hello диалоговое окно, нажмите кнопку **добавить** tooopen hello **пользователя** диалогового окна.
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-skillport-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-skillport-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-a-skillport-test-user"></a>Создание тестового пользователя Skillport

Порядок toocreate Skillport тестового пользователя нужен toocontact [Skillport поддержки](https://www.skillsoft.com/contact.asp) они имеют несколько бизнес-сценариев, в соответствии с требованием toohello конечного пользователя. Компания будет настраивать после обсуждения с пользователями hello.  

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooSkillport доступа.

![Назначение пользователя][200] 

**tooassign tooSkillport Britta Simon выполните следующие шаги hello.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **Skillport**.

    ![Настройка единого входа](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.

При нажатии кнопки hello Skillport плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour Skillport приложения.
Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](https://msdn.microsoft.com/library/dn308586). 

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_203.png

