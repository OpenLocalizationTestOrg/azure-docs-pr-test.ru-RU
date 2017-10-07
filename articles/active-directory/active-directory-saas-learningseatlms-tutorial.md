---
title: "Руководство по интеграции Azure Active Directory с Learning Seat LMS | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и обучения LMS рабочих мест."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bb056fcf-4135-478e-85b1-5015d1f07b85
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: jeedes
ms.openlocfilehash: dc08aa444b85f35a4458768ac560ec663baa1c95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-learning-seat-lms"></a>Руководство по интеграции Azure Active Directory с Learning Seat LMS

В этом учебнике вы узнаете, как toointegrate LMS рабочее место обучения в Azure Active Directory (Azure AD).

Интеграция рабочих мест LMS обучения с Azure AD предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooLearning LMS рабочих мест
- Ваш пользователей tooautomatically get вошедшего tooLearning LMS рабочих мест (Single Sign-On) можно включить с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если необходимо, чтобы tooknow см. Дополнительные сведения об интеграции приложений SaaS в Azure AD. [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с LMS обучения рабочих мест необходимо hello следующих элементов:

- подписка Azure AD;
- подписка на Learning Seat LMS с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление рабочих мест LMS обучения из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-learning-seat-lms-from-hello-gallery"></a>Добавление рабочих мест LMS обучения из галереи hello
tooconfigure hello Интеграция рабочих мест LMS обучения в Azure AD, вы должны tooadd LMS рабочее место обучения из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd LMS рабочее место обучения из галереи hello выполните следующие шаги hello.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Приложения][3]

4. Введите в поле поиска hello **LMS рабочее место обучения**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-learnconnect-tutorial/tutorial_learnconnect_search.png)

5. В панели результатов hello выберите **LMS рабочее место обучения**и нажмите кнопку **добавить** кнопку tooadd приложения hello.


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описаны настройка и проверка единого входа Azure AD в Learning Seat LMS с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в рабочее место LMS обучения является tooa в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в рабочее место LMS обучения должен установить toobe.

Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в рабочее место LMS обучения.

tooconfigure и теста Azure AD единого входа с LMS рабочее место обучения, необходимые hello toocomplete следующие стандартные блоки.

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя LMS рабочее место обучения](#creating-a-learnconnect-test-user)**  -toohave аналог Саймон Britta в LMS рабочее место обучения, представление связанных toohello Azure AD пользователя.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении LMS обучения рабочих мест.

**tooconfigure Azure AD единого входа с LMS обучения рабочее место, выполните следующие шаги hello.**

1. В hello в hello портала Azure **LMS рабочее место обучения** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-learnconnect-tutorial/tutorial_learnconnect_samlbase.png)

3. На hello **URL-адреса и домена LMS обучения рабочее место** выполните hello, выполните действия, при желании tooconfigure приложения hello в **IDP** инициировал режим:

    ![Настройка единого входа](./media/active-directory-saas-learnconnect-tutorial/tutorial_learnconnect_url.png)

    а. В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<subdomain>.learningseatlms.com`

    b. В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<subdomain>.learningseatlms.com/Account/AssertionConsumerService`

4. Проверьте **Показывать дополнительные параметры URL-адреса**, если нужно, чтобы приложение hello tooconfigure в **SP** инициировал режим:

    ![Настройка единого входа](./media/active-directory-saas-learnconnect-tutorial/tutorial_learnconnect_url2.png)

    В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<subdomain>.learningseatlms.com`
     
    > [!NOTE] 
    > Эти значения не hello реальные значения. Обновить значения hello фактический идентификатор, URL-адрес ответа и URL-адрес входа. Обратитесь к [группа поддержки рабочее место обучения](http://help.learningseatlms.com/help) tooget эти значения. 

5. На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.

    ![Настройка единого входа](./media/active-directory-saas-learnconnect-tutorial/tutorial_learnconnect_certificate.png) 

6. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-learnconnect-tutorial/tutorial_general_400.png)

7. tooconfigure единого входа на **LMS рабочее место обучения** стороны, необходимо загрузить hello toosend **метаданные в формате XML** слишком[группа поддержки рабочее место обучения](http://help.learningseatlms.com/help).

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD](https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD

Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-learnconnect-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-learnconnect-tutorial/create_aaduser_02.png) 

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-learnconnect-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-learnconnect-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-a-learning-seat-lms-test-user"></a>Создание тестового пользователя Learning Seat LMS

В этом разделе описано, как создать пользователя Britta Simon в приложении Learning Seat LMS. Обратитесь к [группа поддержки рабочее место обучения](http://help.learningseatlms.com/help) со всеми hello пользователя сведения tooadd hello пользователями в hello LMS рабочее место обучения приложения.

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooLearning LMS рабочих мест.

![Назначение пользователя][200] 

**tooassign tooLearning Britta Simon LMS рабочее место выполнения hello следующие шаги:**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **LMS рабочее место обучения**.

    ![Настройка единого входа](./media/active-directory-saas-learnconnect-tutorial/tutorial_learnconnect_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello. 

Щелкните hello LMS рабочее место обучения плитку в hello панель доступа будет автоматически подписан на tooyour LMS рабочее место обучения приложения. Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](https://msdn.microsoft.com/library/dn308586).

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_203.png

