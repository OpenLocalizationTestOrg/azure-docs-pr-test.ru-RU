---
title: "Учебник. Интеграция Azure Active Directory с Front | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и передней панели."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 88270b6d-2571-434a-b139-b6ccc3a2b19f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: 4be363a3d338ec9268f3324daab4a80346ec3131
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-front"></a>Учебник. Интеграция Azure Active Directory с Front

В этом учебнике вы узнаете, как toointegrate передней панели с Azure Active Directory (Azure AD).

Интеграция с Azure AD передней предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooFront.
- Можно включить на пользователей tooautomatically get вошедшего tooFront (Single Sign-On) с помощью своих учетных записей Azure AD.
- Вы можете управлять учетными записями в одном централизованном месте - hello портал Azure.

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

Интеграция tooconfigure Azure AD с частотой, требуется hello следующих элементов:

- подписка Azure AD;
- подписка с поддержкой единого входа Front.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление передней из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-front-from-hello-gallery"></a>Добавление передней из галереи hello
tooconfigure hello интеграции передней панели в Azure AD, вы должны tooadd передний план из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd передней из галереи hello выполните hello следующие шаги.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Кнопка Hello Azure Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Hello корпоративных приложений колонку][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Кнопка нового приложения Hello][3]

4. Введите в поле поиска hello **передней**выберите **передней** из панели результатов щелкните **добавить** кнопку tooadd приложения hello.

    ![Передний план в списке результатов hello](./media/active-directory-saas-front-tutorial/tutorial_front_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD

В этом разделе описана настройка и проверка единого входа Azure AD в приложение Front с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow какие hello аналог пользователь на переднем плане является tooa пользователем в Azure AD. Другими словами связи между пользователя Azure AD и hello связанных пользователей на переднем плане должен установить toobe.

На переднем плане, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.

tooconfigure и теста Azure AD единого входа с частотой, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя передней](#create-a-front-test-user)**  -toohave аналог Саймон Britta на переднем плане, представление связанных toohello Azure AD пользователя.
4. **[Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#test-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configure-azure-ad-single-sign-on"></a>Настройка единого входа Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении передней панели.

**tooconfigure Azure AD единого входа с помощью передней панели, выполните следующие шаги hello.**

1. В hello в hello портала Azure **передней** странице интеграции приложения щелкните **единого входа**.

    ![Ссылка "Настройка единого входа"][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-front-tutorial/tutorial_front_samlbase.png)

3. На hello **внешнего домена и URL-адреса** статьи, при желании tooconfigure приложения hello в **IDP** инициировал режим:

    ![Настройка единого входа](./media/active-directory-saas-front-tutorial/tutorial_front_url1.png)

    а. В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<companyname>.frontapp.com`

    b. В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<companyname>.frontapp.com/sso/saml/callback`

4. Проверьте **Показывать дополнительные параметры URL-адреса**, если нужно, чтобы приложение hello tooconfigure в **SP** инициировал режим:

    ![Настройка единого входа](./media/active-directory-saas-front-tutorial/tutorial_front_url2.png)

    В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<companyname>.frontapp.com`
     
    > [!NOTE] 
    > Эти значения приведены в качестве примера. Обновление, эти значения с hello фактический идентификатор, URL-адрес ответа и URL-адрес входа которых приведены далее в учебнике или контакт [группа поддержки внешнего клиента](mailto:support@frontapp.com) tooget эти значения. 

5. На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.

    ![Настройка единого входа](./media/active-directory-saas-front-tutorial/tutorial_front_certificate.png) 

6. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-front-tutorial/tutorial_general_400.png)
    
7. На hello **передней конфигурации** щелкните **Настройка передней** tooopen **Настройка входа** окна. Копировать hello **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**

    ![Настройка единого входа](./media/active-directory-saas-front-tutorial/tutorial_front_configure.png) 

8. Клиент передней tooyour входа от имени администратора.

9. Go слишком**параметры (значок шестеренки hello нижней части левой боковой панели hello) > Параметры**.
   
    ![Настройка единого входа на стороне приложения](./media/active-directory-saas-front-tutorial/tutorial_front_000.png)

10. Щелкните ссылку **Single Sign On** (Единый вход).
   
    ![Настройка единого входа на стороне приложения](./media/active-directory-saas-front-tutorial/tutorial_front_001.png)

11. Выберите **SAML** в раскрывающемся списке hello **Single Sign On**.
   
    ![Настройка единого входа на стороне приложения](./media/active-directory-saas-front-tutorial/tutorial_front_002.png)

12. В hello **точки входа** textbox помещение значения hello **входа адрес службы единого** из мастера настройки приложения Azure AD.
    
    ![Настройка единого входа на стороне приложения](./media/active-directory-saas-front-tutorial/tutorial_front_003.png)

13. Откройте ваш загруженный **Certificate(Base64)** в блокноте, hello копирования содержимого его в буфер обмена, а затем вставьте его toohello **сертификат подписи** текстового поля.
    
    ![Настройка единого входа на стороне приложения](./media/active-directory-saas-front-tutorial/tutorial_front_004.png)

14. На hello **параметры поставщика службы** выполните следующие шаги hello:

    ![Настройка единого входа на стороне приложения](./media/active-directory-saas-front-tutorial/tutorial_front_005.png)

    а. Скопируйте значение hello **идентификатор сущности** и вставьте его в hello **идентификатор** текстовое поле в **внешнего домена и URL-адреса** раздела на портале Azure.

    b. Скопируйте значение hello **URL-адрес ACS** и вставьте его в hello **URL-адрес входа** текстовое поле в **внешнего домена и URL-адреса** раздела на портале Azure.
    
15. Нажмите кнопку **Сохранить** .

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD

Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

   ![Создание тестового пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello hello левой панели портала Azure щелкните hello **Azure Active Directory** кнопки.

    ![Кнопка Hello Azure Active Directory](./media/active-directory-saas-front-tutorial/create_aaduser_01.png)

2. слишком go toodisplay hello список пользователей,**пользователей и групп**, а затем нажмите кнопку **всех пользователей**.

    ![Здравствуйте, «Пользователи и группы» и «Все пользователи» ссылки](./media/active-directory-saas-front-tutorial/create_aaduser_02.png)

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** вверху hello hello **всех пользователей** диалоговое окно.

    ![Кнопка "Добавить" Hello](./media/active-directory-saas-front-tutorial/create_aaduser_03.png)

4. В hello **пользователя** диалогового окна выполните следующие шаги hello:

    ![диалоговое окно приветствия пользователя](./media/active-directory-saas-front-tutorial/create_aaduser_04.png)

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** поле типа hello адрес электронной почты пользователя Саймон Britta.

    c. Выберите hello **Показать пароль** флажок и запишите значение hello, отображаемый в hello **пароль** поле.

    d. Щелкните **Создать**.
 
### <a name="create-a-front-test-user"></a>Создание тестового пользователя Front

В этом разделе описано, как создать пользователя Britta Simon в приложении Front. Работать с [группа поддержки внешнего клиента](mailto:support@frontapp.com) для добавления пользователей hello в платформе передней hello. Перед использованием единого входа необходимо создать и активировать пользователей.

### <a name="assign-hello-azure-ad-test-user"></a>Назначить hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления tooFront доступа.

![Назначение пользователям ролей hello][200] 

**tooassign tooFront Britta Simon выполните следующие шаги hello.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **передней**.

    ![ссылка передней Hello в списке приложений hello](./media/active-directory-saas-front-tutorial/tutorial_front_app.png)  

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Hello ссылку «Пользователи и группы»][202]

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![область назначения, добавьте Hello][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="test-single-sign-on"></a>Проверка единого входа

Цель этого раздела Hello — tootest Azure AD SSOconfiguration с помощью панели доступа "hello".

Если щелкнуть плитку передней hello в hello панели доступа, вы должны получить tooyour автоматически подписан на передней панели приложения. 

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-front-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-front-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-front-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-front-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-front-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-front-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-front-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-front-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-front-tutorial/tutorial_general_203.png

