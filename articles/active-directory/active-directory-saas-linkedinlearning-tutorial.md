---
title: "Руководство по интеграции Azure Active Directory с LinkedIn Learning | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и LinkedIn обучения."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d5857070-bf79-4bd3-9a2a-4c1919a74946
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: jeedes
ms.openlocfilehash: 14610a25132ed0ccf5892cad6ccc4e1ef03ff280
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-learning"></a>Руководство по интеграции Azure Active Directory с LinkedIn Learning

В этом учебнике вы узнаете, как toointegrate обучения LinkedIn с Azure Active Directory (Azure AD).

Интеграция обучения LinkedIn с Azure AD предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooLinkedIn обучения
- Можно включить на пользователей tooautomatically get вошедшего tooLinkedIn обучения (Single Sign-On) с использованием их учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с LinkedIn обучения необходимо hello следующих элементов:

- подписка Azure AD;
- подписка LinkedIn Learning с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление LinkedIn обучения из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-linkedin-learning-from-hello-gallery"></a>Добавление LinkedIn обучения из галереи hello
tooconfigure hello интеграции LinkedIn обучения в Azure AD, вы должны tooadd LinkedIn обучения из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd LinkedIn обучения из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. Нажмите кнопку **добавить** кнопку в верхней части hello диалогового окна "hello".

    ![Приложения][3]

4. Введите в поле поиска hello **обучения LinkedIn**. На панели результатов щелкните **обучения LinkedIn** tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedinlearning_000.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в приложение LinkedIn Learning с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в обучении LinkedIn является tooa в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в обучении LinkedIn должен установить toobe.

Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в обучении LinkedIn.

tooconfigure и теста Azure AD единого входа с LinkedIn обучения, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя LinkedIn обучения](#creating-a-linkedin-learning-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении LinkedIn обучения.

**tooconfigure Azure AD единого входа с помощью LinkedIn обучения, выполните следующие шаги hello.**

1. В hello в hello портала Azure **обучения LinkedIn** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedin_01.png)

3. В другом окне браузера, клиент LinkedIn обучения tooyour входа от имени администратора.

4. В **Account Center** (Центр учетных записей) в разделе **Settings** (Параметры) щелкните **Global Settings** (Глобальные параметры). Кроме того, установите **обучения - по умолчанию** hello в раскрывающемся списке.

    ![Настройка единого входа](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_admin_01.png)

5. Нажмите кнопку **или щелкните здесь tooload и скопируйте отдельные поля из формы hello** и скопируйте **идентификатор сущности** и **URL-адрес утверждение потребителя доступа (ACS)**

    ![Настройка единого входа](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_admin_03.png)

6. На портале Azure в разделе **URL-адреса и домена обучения LinkedIn**, выполнять hello, выполнив действия, если требуется, чтобы tooconfigure единого входа в **инициированный IdP** режим

    ![Настройка единого входа](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_signon_01.png)

    а. В hello **идентификатор** текстовом поле введите hello **идентификатор сущности** копируются LinkedIn портала 

    b. В hello **URL-адрес ответа** текстовом поле введите hello **утверждение потребителя доступа (ACS) URL-адрес** копируются LinkedIn портала

7. Если требуется, чтобы tooconfigure единого входа в **, инициируемая SP**, затем щелкните URL-адрес Advanced Показать параметр в разделе конфигурации hello и настройте hello URL-адрес входа с hello следующий шаблон:

    `https://www.linkedin.com/checkpoint/enterprise/login/<AccountId>?application=learning&applicationInstanceId=<InstanceId>`

    ![Настройка единого входа](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_signon_02.png)   
    
8. Приложение обучения LinkedIn ожидает утверждения SAML hello в определенном формате, требующий вы tooadd настраиваемого атрибута сопоставления tooyour атрибутов токена конфигурация SAML. пример Hello следующий снимок экрана для этого. значение по умолчанию Hello **идентификатор пользователя** — **user.userprincipalname** , но это toobe, сопоставленный с адресом электронной почты пользователя hello ожидает LinkedIn обучения. Для этого можно использовать **user.mail** атрибут из списка hello, или используйте hello соответствующее значение атрибута на основе конфигурации в организации. 

    ![Настройка единого входа](./media/active-directory-saas-linkedinlearning-tutorial/updateusermail.png)
    
9. В **атрибуты пользователя** щелкните **представление и редактировать все остальные атрибуты пользователя** и задавать атрибуты hello. Hello пользователь должен tooadd четыре утверждения с именем **электронной почты**, **отдел**, **firstname**, и **lastname** и hello значение — toobe сопоставлено с **user.mail**, **user.department**, **user.givenname**, и **user.surname** соответственно

    | Имя атрибута | Значение атрибута |
    | --- | --- |
    | email| user.mail |    
    | department| user.department |
    | firstname| user.givenname |
    | lastname| user.surname |
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-linkedinlearning-tutorial/userattribute.png)
    
    а. Нажмите кнопку **Добавление атрибута** tooopen hello атрибута, диалоговое окно.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-linkedinLearning-tutorial/tutorial_attribute_04.png)

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-linkedinLearning-tutorial/tutorial_attribute_05.png)
    
    b. В hello **имя** в текстовое поле имя атрибута типа hello, показанный для этой строки.
    
    c. Из hello **значение** списка значение атрибута типа hello, показанный для этой строки.
    
    d. Нажмите кнопку **ОК**.

10. Выполните следующие действия на hello hello **имя** атрибута -

    а. Щелкните hello атрибут tooopen hello **изменение атрибута** окна.

    ![Настройка единого входа](./media/active-directory-saas-linkedinLearning-tutorial/url_update.png)

    b. Удалить значение URL-адрес hello из hello **пространства имен**.
    
    c. Нажмите кнопку **ОК** toosave приветствия.

11. На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и сохраните hello XML-файл на компьютере.

    ![Настройка единого входа](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedinlearning_certificate.png) 

12. Щелкните **Сохранить**.

    ![Настройка единого входа](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_400.png)

13. Go слишком**параметры администрирования LinkedIn** раздела. Отправьте hello XML-файл, загруженный с портала Azure hello, щелкнув hello отправить файл в формат XML.

    ![Настройка единого входа](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_metadata_03.png)

14. Нажмите кнопку **на** tooenable единого входа. Изменение состояния единого входа с **не подключены** слишком**подключено**

    ![Настройка единого входа](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_admin_05.png)

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_02.png) 

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**. 

### <a name="creating-a-linkedin-learning-test-user"></a>Создание тестового пользователя LinkedIn Learning

Приложение Linked Learning поддерживает Только время подготовки пользователей и после проверки подлинности пользователей автоматически создаются в приложение hello. На странице параметров администрирования hello на коммутаторе портала зеркало hello обучения LinkedIn hello **автоматически назначать лицензии** tooenable tooactive непосредственно в момент подготовки и это также назначить лицензию пользователя toohello.
   
   ![Создание тестового пользователя Azure AD](./media/active-directory-saas-linkedinLearning-tutorial/LinkedinUserprovswitch.png)

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooLinkedIn обучения.

![Назначение пользователя][200] 

**tooassign tooLinkedIn Britta Simon обучения, выполните следующие шаги hello:**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **обучения LinkedIn**.

    ![Настройка единого входа](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedinlearning_0001.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.

При выборе плитки обучения LinkedIn hello в hello панели доступа, вы должны получить страницу hello Azure входа и на после успешного входа, должно появиться в приложение LinkedIn обучения.

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_203.png