---
title: "Руководство. Интеграция Azure Active Directory с Absorb LMS | Документы Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и LMS запоминаются."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: ba9f1b3d-a4a0-4ff7-b0e7-428e0ed92142
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: a140a78a3a9474a6372a3ad4fb8251bd2452c990
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-absorb-lms"></a>Руководство. Интеграция Azure Active Directory с Absorb LMS

В этом учебнике вы узнаете, как toointegrate Absorb LMS с Azure Active Directory (Azure AD).

Интеграция LMS справиться с Azure AD предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooAbsorb LMS
- Можно включить на пользователей tooautomatically get вошедшего tooAbsorb LMS (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если необходимо, чтобы tooknow см. Дополнительные сведения об интеграции приложений SaaS в Azure AD. [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с запоминаются LMS требуется hello следующих элементов:

- подписка Azure AD;
- подписка Absorb LMS с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление запоминаются LMS из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-absorb-lms-from-hello-gallery"></a>Добавление запоминаются LMS из галереи hello
tooconfigure hello интеграции запоминаются LMS в tooAzure AD, вы должны tooadd Absorb LMS из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd Absorb LMS из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Кнопка Hello Azure Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Hello корпоративных приложений колонку][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Кнопка нового приложения Hello][3]

4. Введите в поле поиска hello **запоминаются LMS**выберите **запоминаются LMS** из панели результатов щелкните **добавить** кнопку tooadd приложения hello.

    ![Запоминаются LMS в списке результатов hello](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD

В этом разделе описана настройка и проверка единого входа Azure AD в Absorb LMS с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в запоминаются LMS является tooa в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в запоминаются LMS должен установить toobe.

Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в LMS запоминаются.

tooconfigure и теста Azure AD единого входа с запоминаются LMS, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя, прошедшего запоминаются LMS](#create-an-absorb-lms-test-user)**  -toohave аналог Саймон Britta в запоминаются LMS, представление связанных toohello Azure AD пользователя.
4. **[Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#test-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configure-azure-ad-single-sign-on"></a>Настройка единого входа Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении LMS запоминаются.

**tooconfigure Azure AD единого входа с запоминаются управления Обучением выполните следующие шаги hello.**

1. В hello в hello портала Azure **запоминаются LMS** странице интеграции приложения щелкните **единого входа**.

    ![Ссылка "Настройка единого входа"][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_samlbase.png)

3. На hello **URL-адреса и домена запоминаются LMS** выполните следующие шаги hello:

    ![Сведения о домене и URL-адресах единого входа для приложения Absorb LMS](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_url.png)

    а. В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<subdomain>.myabsorb.com/Account/SAML`

    b. В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<subdomain>.myabsorb.com/Account/SAML`
     
    > [!NOTE] 
    > Эти значения не являются реальными hello. Обновите эти значения с hello фактический идентификатор и ответ URL-адрес. Обратитесь к [группа поддержки запоминаются клиента LMS](https://www.absorblms.com/support) tooget эти значения. 

4. На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.

    ![ссылку для скачивания сертификата Hello](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_certificate.png) 

6. Нажмите кнопку **Сохранить** .

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-absorblms-tutorial/tutorial_general_400.png)
    
7. На hello **запоминаются конфигурации LMS** щелкните **Настройка запоминаются LMS** tooopen **Настройка входа** окна. Копировать hello **URL-адрес выхода и SAML единого входа URL-адрес службы** из hello **краткий справочник.**

    ![Конфигурация Absorb LMS](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_configure.png) 

8. В другом окне браузера Войдите на сайте компании запоминаются LMS tooyour в качестве администратора.

9. Нажмите кнопку hello **значок учетной записи** в интерфейсе администратора hello. 

    ![Настройка единого входа](./media/active-directory-saas-absorblms-tutorial/1.png)

10. Щелкните **Параметры портала**.

    ![Настройка единого входа](./media/active-directory-saas-absorblms-tutorial/2.png)
    
11. Нажмите кнопку hello **пользователей** вкладки.

    ![Настройка единого входа](./media/active-directory-saas-absorblms-tutorial/3.png)

12. Выполните следующие шаги tooaccess hello единым входом поля конфигурации hello.

    ![Настройка единого входа](./media/active-directory-saas-absorblms-tutorial/4.png)

    а. Выберите hello соответствующие **режим**.

    b. Привет открыть сертификат, загруженный из hello портал Azure в блокноте, удалите hello **---BEGIN CERTIFICATE---** и **---конечный СЕРТИФИКАТ---** тега, а затем вставьте hello оставшееся содержимое Hello **ключ** текстового поля.
    
    c. В hello **свойства Id**, Здравствуйте, выберите соответствующий атрибут, который вы настроили как hello идентификатор пользователя в hello Azure AD (например, при выборе hello userprinciplename в Azure AD, имя пользователя будет выбираться здесь.)

    d. В hello **URL-адрес входа**, вставьте hello **«SAML единого входа URL-адрес службы»** значением, скопированным из hello **Настройка входа** окно hello портал Azure.

    д. В hello **URL-адрес выхода**, вставьте hello **«URL-адрес выхода»** значением, скопированным из hello **Настройка входа** окно hello портал Azure.

13. Включите параметр **Only Allow SSO Login** (Разрешить только единый вход).

    ![Настройка единого входа](./media/active-directory-saas-absorblms-tutorial/5.png)

14. Нажмите кнопку **Сохранить**.

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD

Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание тестового пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Кнопка Hello Azure Active Directory](./media/active-directory-saas-absorblms-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Здравствуйте, «Пользователи и группы» и «Все пользователи» ссылки](./media/active-directory-saas-absorblms-tutorial/create_aaduser_02.png) 

3. Вверху hello диалоговое окно приветствия щелкните **добавить** tooopen hello **пользователя** диалогового окна.
 
    ![Кнопка "Добавить" Hello](./media/active-directory-saas-absorblms-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![диалоговое окно приветствия пользователя](./media/active-directory-saas-absorblms-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.

### <a name="create-an-absorb-lms-test-user"></a>Создание тестового пользователя Absorb LMS

Пользователи toolog tooenable Azure AD в tooAbsorb LMS, их необходимо подготовить в tooAbsorb управления Обучением.  
Эта подготовка для Absorb LMS выполняется вручную.

**tooprovision учетной записи пользователя, выполните следующие шаги hello.**

1. Войдите в систему tooyour запоминаются LMS сайт компании как администратор.

2. Откройте вкладку **Пользователи**.

    ![Приглашение пользователей](./media/active-directory-saas-absorblms-tutorial/absorblms_users.png)

3. Нажмите кнопку **пользователей** под hello **пользователей** вкладки.

    ![Приглашение пользователей](./media/active-directory-saas-absorblms-tutorial/absorblms_userssub.png)

4.  Выберите **Пользователя** в раскрывающемся списке **Добавить новый**.

    ![Приглашение пользователей](./media/active-directory-saas-absorblms-tutorial/absorblms_createuser.png)

5. На hello **добавить пользователя** выполните следующие шаги hello:

    ![Приглашение пользователей](./media/active-directory-saas-absorblms-tutorial/user.png)

    а. В hello **имя** текстовое поле, имя первого типа hello как Britta.

    b. В hello **Фамилия** текстовое поле, имя последнего типа hello как Simon.
    
    c. В hello **Username** текстовом поле введите имя пользователя hello как Саймон Britta.

    d. В hello **пароль** текстового поля, типа hello пароль Саймон Britta.

    д. В hello **подтверждение пароля** текстового поля, типа hello одинаковый пароль.
    
    f. Выберите значение **Активно**.   

6. Нажмите кнопку **Сохранить**.
 
### <a name="assign-hello-azure-ad-test-user"></a>Назначить hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooAbsorb LMS.

![Назначение пользователям ролей hello][200]

**tooassign tooAbsorb Britta Simon управления Обучением выполните hello следующие шаги.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **запоминаются LMS**.

    ![ссылка запоминаются LMS Hello в списке приложений hello](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Hello ссылку «Пользователи и группы»][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![область назначения, добавьте Hello][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="test-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.

Нажмите кнопку hello запоминаются LMS плитки в панели доступа hello вы получите tooyour автоматически вошедшего запоминаются LMS приложения. Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](https://msdn.microsoft.com/library/dn308586).

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_203.png

