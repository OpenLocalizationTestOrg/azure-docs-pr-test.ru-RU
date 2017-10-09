---
title: "Руководство по интеграции Azure Active Directory с Workplace by Facebook | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и рабочей области с Facebook."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 30f2ee64-95d3-44ef-b832-8a0a27e2967c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: f71a59527394730757d501a973251dc293fd3683
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workplace-by-facebook"></a>Руководство по интеграции Azure Active Directory с Workplace by Facebook

В этом учебнике вы узнаете, как toointegrate рабочему месту с Facebook с Azure Active Directory (Azure AD).

Интеграция рабочему месту с Facebook с Azure AD предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooWorkplace с Facebook
- Можно включить на пользователей tooautomatically get вошедшего tooWorkplace с Facebook (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD в рабочей области с Facebook, требуется hello следующих элементов:

- подписка Azure AD;
- подписка Workplace by Facebook с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление рабочей области с Facebook из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-workplace-by-facebook-from-hello-gallery"></a>Добавление рабочей области с Facebook из галереи hello
tooconfigure hello интеграции рабочему месту с Facebook в Azure AD, вы должны tooadd рабочему месту с Facebook из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd рабочему месту с Facebook из галереи hello выполните следующие шаги hello.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Приложения][3]

4. Введите в поле поиска hello **рабочему месту с Facebook**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_search.png)

5. В панели результатов hello выберите **рабочему месту с Facebook**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в Workplace by Facebook с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в рабочей области с Facebook является tooa в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в рабочей области с Facebook должен установить toobe.

Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в рабочей области с Facebook.

tooconfigure и тестирования Azure AD единого входа в рабочей области с Facebook, необходимы следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Настройка частоты повторная проверка подлинности](#configuring-reauthentication-frequency)**  -tooconfigure tooprompt рабочему месту для проверки SAML.
3. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
4. **[Создание рабочей области с Facebook тестового пользователя](#creating-a-workplace-by-facebook-test-user)**  -toohave аналог Саймон Britta в рабочей области с Facebook, который представляет связанный toohello Azure AD пользователя.
5. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
6. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в рабочую область приложения Facebook.

**tooconfigure Azure AD единого входа в рабочей области с Facebook, выполните следующие шаги hello.**

1. В hello в hello портала Azure **рабочему месту с Facebook** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_samlbase.png)

3. На hello **рабочему месту с URL-адреса и домена Facebook** выполните следующие шаги hello:

    ![Настройка единого входа](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_url.png)

    а. В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<instancename>.facebook.com`

    b. В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://www.facebook.com/company/<instancename>`

    > [!NOTE] 
    > Эти значения не являются реальными hello. Обновить значения hello фактический URL-адрес входа и идентификатор. Обратитесь к [рабочей группой поддержки клиент Facebook](https://workplace.fb.com/faq/) tooget эти значения. 

4. На hello **сертификат подписи SAML** щелкните **сертификата (Base64)** и затем сохраните файл сертификата hello на вашем компьютере.

    ![Настройка единого входа](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_400.png)

6. На hello **рабочему месту конфигурацией Facebook** щелкните **Настройка рабочей области с Facebook** tooopen **Настройка входа** окна. Копировать hello **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**

    ![Настройка единого входа](./media/active-directory-saas-workplacebyfacebook-tutorial/config.png) 

7. В другом окне браузера, tooyour входа рабочему месту с Facebook сайт компании от имени администратора.
  
   > [!NOTE] 
   > Как часть процесса проверки подлинности SAML hello рабочее место может использовать строки запроса из копии too2.5 килобайт в размер в порядке toopass параметры tooAzure AD.

8. В hello **панели мониторинга компании**, go toohello **проверки подлинности** вкладки.

9. В разделе **проверку подлинности SAML**выберите **SSO только** из раскрывающегося списка hello.

10. Hello входные значения, скопированные из **рабочему месту конфигурацией Facebook** раздел hello портал Azure в соответствующие поля hello:

    *   В **SAML URL-адрес** текстовое значение hello вставить **единого входа URL-адрес службы**, который вы скопировали из портала Azure.
    *   В **текстовое поле URL-адрес издателя SAML**, вставьте значение hello **идентификатор сущности SAML**, который вы скопировали из портала Azure.
    *   В **перенаправление выхода SAML** (необязательно) вставьте значение hello **URL-адрес выхода**, который вы скопировали из портала Azure.
    *   Откройте ваш **сертификат в кодировке base-64** в блокноте, Скачанный с портала Azure скопируйте hello содержимое в буфер обмена, а затем вставьте его toothe **сертификат SAML** текстового поля.

11. Может потребоваться tooenter hello аудитории URL-адрес, URL-адрес получателя, и URL-адрес ACS (службы обработчика утверждений), перечисленные в папке hello **конфигурация SAML** раздела.

12. Прокрутите toohello нижней части раздела hello и щелкните hello **тестирования единого входа** кнопки. Появится всплывающее окно со страницей входа в Azure AD. Введите свои учетные данные в виде обычных tooauthenticate. 

    **Устранение неполадок:** Здравствуйте убедитесь, что адрес электронной почты на hello возвращается обратно из Azure AD, так же, как hello рабочей учетной записи, на который выполнен вход в систему.

13. После успешного выполнения теста hello, прокрутите toohello внизу страницы приветствия и нажмите кнопку hello **Сохранить** кнопки.

14. Теперь для аутентификации всех пользователей Workplace будет отображаться страница входа в Azure AD.

15. **Перенаправление для выхода SAML (необязательно)** - 

    Вы можете toooptionally настроить URL-адрес выхода SAML, которой может быть toopoint, используемые в Azure AD страницы выхода. Если этот параметр включен и настроен, hello пользователь больше не будет страницы выхода направленной toohello рабочей области. Вместо этого пользователь hello будет перенаправленный toohello URL-адрес, которое было добавлено в приветствия перенаправление выхода SAML.


> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="configuring-reauthentication-frequency"></a>Настройка частоты повторной проверки подлинности

Можно настроить tooprompt рабочему месту для проверки SAML каждый день, три дня недели, в две недели, месяц или никогда.

> [!NOTE] 
>Hello минимальное значение для проверки SAML hello мобильных приложений имеет значение tooone недели.

Можно также принудительно выполнить сброс для всех пользователей с помощью кнопки hello SAML: требуется проверка подлинности SAML для всех пользователей сейчас.


### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_02.png) 

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-workplacebyfacebook-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-a-workplace-by-facebook-test-user"></a>Создание тестового пользователя Workplace by Facebook

В этом разделе вы создадите в Workplace by Facebook пользователя с именем Britta Simon. Workplace by Facebook поддерживает JIT-подготовку. Эта функция включена по умолчанию.

В этом разделе никакие действия с вашей стороны не требуются. Если пользователь не существует в рабочей области с Facebook, новый созданный при попытке tooaccess рабочему месту Facebook.

>[!Note]
>При необходимости пользователь вручную, обратитесь в службу toocreate [рабочей группой поддержки клиент Facebook](https://workplace.fb.com/faq/)

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooWorkplace с Facebook.

![Назначение пользователя][200] 

**tooassign tooWorkplace Britta Simon с Facebook, выполните hello следующие шаги.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **рабочему месту с Facebook**.

    ![Настройка единого входа](./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

Tootest параметры единого входа, откройте панель доступа hello.
Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).


## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Руководство по настройке Google Apps для автоматической подготовки пользователей](active-directory-saas-workplacebyfacebook-provisioning-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workplacebyfacebook-tutorial/tutorial_general_203.png

