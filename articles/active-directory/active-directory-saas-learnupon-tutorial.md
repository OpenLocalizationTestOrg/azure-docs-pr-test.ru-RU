---
title: "Руководство по интеграции Azure Active Directory с LearnUpon | Документы Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и LearnUpon."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b11c6315-c79d-4f34-9610-bd17070ab7c7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: fdb9c62172327a539f0459c98aa20e63fa441e4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-learnupon"></a>Руководство. Интеграция Azure Active Directory с LearnUpon

В этом учебнике вы узнаете, как toointegrate LearnUpon с Azure Active Directory (Azure AD).

Интеграция с Azure AD LearnUpon предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooLearnUpon
- Можно включить на пользователей tooautomatically get вошедшего tooLearnUpon (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с LearnUpon требуется hello следующих элементов:

- подписка Azure AD;
- подписка LearnUpon с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление LearnUpon из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-learnupon-from-hello-gallery"></a>Добавление LearnUpon из галереи hello
tooconfigure hello интеграции LearnUpon в Azure AD, вы должны tooadd LearnUpon из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd LearnUpon из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Приложения][3]

4. Введите в поле поиска hello **LearnUpon**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_search.png)

5. В панели результатов hello выберите **LearnUpon**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в LearnUpon для тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в LearnUpon является tooa в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в LearnUpon должен установить toobe.

В LearnUpon, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.

tooconfigure и теста Azure AD единого входа с LearnUpon, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя LearnUpon](#creating-a-learnupon-test-user)**  -toohave аналог Саймон Britta в LearnUpon, который представляет связанный toohello Azure AD пользователя.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении LearnUpon.

**tooconfigure Azure AD единого входа с LearnUpon, выполните следующие шаги hello.**

1. В hello в hello портала Azure **LearnUpon** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_samlbase.png)

3. На hello **URL-адреса и домена LearnUpon** выполните следующие шаги hello:

    ![Настройка единого входа](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_url.png)

    В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<companyname>.learnupon.com/saml/consumer`

    > [!NOTE] 
    > Обратите внимание на то, что это не Вещественное значение hello. у вас есть tooupdate это значение с hello фактический URL-адрес ответа. обратитесь в службу tooget это значение [LearnUpon поддержки](https://www.learnupon.com/features/support/).



4. На hello **сертификат подписи SAML** щелкните **сертификата (Raw)** и затем сохраните файл сертификата hello на вашем компьютере.

    ![Настройка единого входа](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-learnupon-tutorial/tutorial_general_400.png)

6. На hello **конфигурации LearnUpon** щелкните **Настройка LearnUpon** tooopen **Настройка входа** окна. Копировать hello **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**

    ![Настройка единого входа](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_configure.png) 

7. Откройте другую страницу браузера и войдите в LearnUpon с учетной записью администратора. 

8. Нажмите кнопку hello **параметры** вкладки.
   
    ![Настройка единого входа](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_06.png)

9. Нажмите кнопку **Single Sign On - SAML**, а затем нажмите кнопку **Общие параметры** tooconfigure параметры SAML.
   
    ![Настройка единого входа](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_07.png) 

10. В hello **Общие параметры** выполните следующие шаги hello:
   
    ![Настройка единого входа](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_08.png)  
  
    а. Щелкните **Включено**.

    b. Для параметра **Версия** установите значение **2.0**.

    c. Для параметра **Пропустить условия** установите значение **Нет**.

    d. В hello **имя маркера блога SAML param** в текстовое поле имя типа hello запрос post параметр toohello вышеуказанных SAML потребителя URL-адрес, содержащий toobe утверждения SAML hello проверены и проверка подлинности — например  **SAMLResponse**.

    д. В hello **формат идентификатора имени** текстовое значение hello типа, указывающее, где в пользователи hello утверждения SAML идентификатор (адрес электронной почты) находится — например **urn: oasis: имена: tc: SAML:1.1:nameid-формат: emailAddress**.
  
    f. В hello **определить расположение поставщика** текстового поля, типа hello значение, указывающее, где hello отправляются tooif пользователи они щелкнуть значок данного загруженного на экране входа Azure портала.
  
    ж. В hello **выход URL-адрес** текстовое поле, вставить hello **URL-адрес выхода** скопирован из hello портал Azure.
    
    h. Нажмите кнопку **управление отпечатков пальцев**и затем передать отпечаток пальца hello загруженного сертификата.

11. Нажмите кнопку **параметры пользователя**, а затем выполните следующие шаги hello:
   
     ![Настройка единого входа](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_11.png)  
 
    а. В hello **формат идентификатора имени** в текстовое поле типа hello, сообщающего нам в вашей firstname пользователей hello утверждения SAML находится значение — например: **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.
  
    b. В hello **последний формат идентификатора имени** в текстовое поле типа hello, сообщающего нам в вашей lastname пользователей hello утверждения SAML находится значение — например: **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**.

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-learnupon-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-learnupon-tutorial/create_aaduser_02.png) 

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-learnupon-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-learnupon-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-a-learnupon-test-user"></a>Создание тестового пользователя LearnUpon

Цель этого раздела Hello — toocreate пользователя с именем Саймон Britta в LearnUpon. Приложение LearnUpon поддерживает JIT-подготовку. Эта функция включена по умолчанию.

В этом разделе никакие действия с вашей стороны не требуются. Если он еще не существует во время попытки tooaccess LearnUpon создается новый пользователь. [Настройка единого входа в Azure AD](#configuring-azure-ad-single-single-sign-on).

>[!NOTE]
>Если требуется toocreate пользователя вручную, необходимо toocontact [LearnUpon поддержки](https://www.learnupon.com/features/support/). 

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooLearnUpon доступа.

![Назначение пользователя][200] 

**tooassign tooLearnUpon Britta Simon выполните следующие шаги hello.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **LearnUpon**.

    ![Настройка единого входа](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.

При нажатии кнопки hello LearnUpon плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour LearnUpon приложения.
Дополнительные сведения о панели доступа см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_203.png

