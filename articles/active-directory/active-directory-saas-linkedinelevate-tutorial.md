---
title: "Руководство по интеграции Azure Active Directory с LinkedIn Elevate | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и может повышать уровень LinkedIn."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2ad9941b-c574-42c3-bd0f-5d6ec68537ef
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: jeedes
ms.openlocfilehash: 189bd72c230be7dc0c0b934f94ea01e84af9ad23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-elevate"></a>Руководство по интеграции Azure Active Directory с LinkedIn Elevate

В этом учебнике вы узнаете, как повысить уровень LinkedIn toointegrate с Azure Active Directory (Azure AD).

Интеграция LinkedIn повышения прав с Azure AD предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooLinkedIn повышение
- Можно включить на пользователей tooautomatically get вошедшего tooLinkedIn повышение (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал управления Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с повышение LinkedIn требуется hello следующих элементов:

- подписка Azure AD;
- подписка LinkedIn Elevate с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не следует использовать рабочую среду при отсутствии необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление LinkedIn повысить уровень из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-linkedin-elevate-from-hello-gallery"></a>Добавление LinkedIn повысить уровень из галереи hello
tooconfigure hello интеграции LinkedIn повышение в Azure AD, вы должны tooadd LinkedIn повысить уровень из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd LinkedIn повысить уровень из галереи hello выполните hello следующие шаги.**

1. В hello  **[портала управления Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. Нажмите кнопку **добавить** кнопку в верхней части hello диалогового окна "hello".

    ![Приложения][3]

4. Введите в поле поиска hello **повысить LinkedIn**. На панели результатов щелкните **повысить LinkedIn** tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedinElevate_000.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в приложение LinkedIn Elevate с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в повышение LinkedIn является tooa в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в повышение LinkedIn должен установить toobe.

Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в повышение LinkedIn.

tooconfigure и теста Azure AD единого входа с LinkedIn повышать права, необходимые hello toocomplete следующие стандартные блоки.

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя повышение LinkedIn](#creating-a-linkedin-elevate-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал управления Azure hello и настройки единого входа в приложении LinkedIn повышения прав.

**tooconfigure Azure AD единого входа с LinkedIn повышения прав, выполните следующие шаги hello.**

1. На портале управления Azure hello на hello **LinkedIn повышение** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна, как **режим** выберите **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedin_01.png)

3. В другом окне браузера, клиент LinkedIn повышение tooyour входа от имени администратора.

4. В **Account Center** (Центр учетных записей) в разделе **Settings** (Параметры) щелкните **Global Settings** (Глобальные параметры). Кроме того, установите **повышение - повышение теста AAD** hello в раскрывающемся списке.

    ![Настройка единого входа](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_admin_01.png)

5. Щелкните **или щелкните здесь tooload и скопируйте отдельные поля из формы hello** и скопируйте **идентификатор сущности** и **URL-адрес утверждение потребителя доступа (ACS)**

    ![Настройка единого входа](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_admin_03.png)

6. На портале Azure в разделе **URL-адреса и домена повышение LinkedIn**, выполнять hello, выполнив действия, если требуется, чтобы tooconfigure единого входа в **инициированный IdP** режим

    ![Настройка единого входа](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_signon_01.png)

    а. В hello **идентификатор** текстовом поле введите hello **идентификатор сущности** копируются LinkedIn портала 

    b. В hello **URL-адрес ответа** текстовом поле введите hello **утверждение потребителя доступа (ACS) URL-адрес** копируются LinkedIn портала

7. Если требуется, чтобы tooconfigure единого входа в **, инициируемая SP**, затем щелкните URL-адрес Advanced Показать параметр в разделе конфигурации hello и настройка входа hello URL-адрес с hello следующий шаблон:

    `https://www.linkedin.com/checkpoint/enterprise/login/<AccountId>?application=elevate&applicationInstanceId=<InstanceId>` 
    
    ![Настройка единого входа](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_signon_02.png) 
    
8. Приложение LinkedIn повышение ожидает утверждения SAML hello в определенном формате, требующий вы tooadd настраиваемого атрибута сопоставления tooyour атрибутов токена конфигурация SAML. пример Hello следующий снимок экрана для этого. значение по умолчанию Hello **идентификатор пользователя** — **user.userprincipalname** , но повышение LinkedIn ожидает этот toobe, сопоставленный с адресом электронной почты пользователя hello. Для этого можно использовать **user.mail** атрибут из списка hello, или используйте hello соответствующее значение атрибута на основе конфигурации в организации. 

    ![Настройка единого входа](./media/active-directory-saas-linkedinElevate-tutorial/updateusermail.png)

9. В **атрибуты пользователя** щелкните **представление и редактировать все остальные атрибуты пользователя** и задавать атрибуты hello. Требуется tooadd с именем другого утверждения **отдел** и значение hello должен сопоставить слишком toobe**user.department**.

    | Имя атрибута | Значение атрибута |
    | --- | --- |    
    | department| user.department |

      ![Создание тестового пользователя Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/userattribute.png)

      а. Щелкните на странице добавить атрибут tooopen hello атрибут сведения о добавить атрибута отдела hello, как показано ниже-

      ![Создание тестового пользователя Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/adduserattribute.png)

      b. Щелкните **ОК** toosave hello атрибута.

      c. Изменение имени hello hello атрибута **emailaddress** слишком**электронной почты**.


10. На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и сохраните hello XML-файл на компьютере.

    ![Настройка единого входа](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedinElevate_certificate.png) 

11. Щелкните **Сохранить**.

    ![Настройка единого входа](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_400.png)

12. Go слишком**параметры администрирования LinkedIn** раздела. Отправьте hello XML-файл, только что загруженном из портала Azure hello, щелкнув hello параметр Отправить XML-файл.

    ![Настройка единого входа](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_metadata_03.png)

13. Нажмите кнопку **на** tooenable единого входа. SSO состояние изменится с **не подключены** слишком**подключено**

    ![Настройка единого входа](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_admin_05.png)

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя на портале управления Azure hello, вызывается Саймон Britta.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал управления Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_01.png) 

2. Go слишком**пользователей и групп** и нажмите кнопку **всех пользователей** toodisplay hello список пользователей.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_02.png) 

3. Вверху hello диалоговое окно приветствия щелкните **добавить** tooopen hello **пользователя** диалогового окна.
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**. 

### <a name="creating-a-linkedin-elevate-test-user"></a>Создание тестового пользователя LinkedIn Elevate

Связанное приложение повышение поддерживает только в подготовки пользователей время и после проверки подлинности пользователей в приложении hello автоматически создаются. На странице параметров администрирования hello на коммутаторе портала зеркало hello повышение LinkedIn hello **автоматически назначать лицензии** tooenable tooactive непосредственно в момент подготовки и это также назначить лицензию пользователя toohello.

   ![Создание тестового пользователя Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/LinkedinUserprovswitch.png)

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа, предоставляя свой доступ tooLinkedIn повышение.

![Назначение пользователя][200] 

**tooassign tooLinkedIn Britta Simon повышение, выполните hello следующие шаги.**

1. На портале управления Azure hello, открыть представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **повысить LinkedIn**.

    ![Настройка единого входа](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedinElevate_0001.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.

При нажатии кнопки hello повышение LinkedIn плитки в панели доступа hello, вы должны получить страницу hello Azure входа и на после успешного входа, должно появиться в приложение LinkedIn повышения прав.

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Руководство по настройке LinkedIn Elevate для автоматической подготовки пользователей с помощью Azure Active Directory](active-directory-saas-linkedinelevate-provisioning-tutorial.md)
* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_203.png
