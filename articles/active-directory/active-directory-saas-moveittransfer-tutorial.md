---
title: "Руководство по интеграции Azure Active Directory с приложением MOVEit Transfer - Azure AD integration | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и передачи MOVEit - интеграция Azure AD."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 8ff7102d-be73-4888-ae81-d8e3d01dd534
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: 5bbe4f2d952bd45c4d58d55ffc3467b4eb871fd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-moveit-transfer---azure-ad-integration"></a>Руководство по интеграции Azure Active Directory с MOVEit Transfer - Azure AD integration

В этом учебнике вы узнаете, как toointegrate MOVEit передача — интеграция Azure AD с Azure Active Directory (Azure AD).

Интеграция MOVEit передача — интеграция Azure AD с Azure AD предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooMOVEit передача — интеграция Azure AD.
- Можно включить на пользователей tooautomatically get вошедшего tooMOVEit передача — интеграция Azure AD (Single Sign-On) с помощью своих учетных записей Azure AD.
- Вы можете управлять учетными записями в одном централизованном месте - hello портал Azure.

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

Интеграция Azure AD с MOVEit передача — интеграция Azure AD tooconfigure требуется hello следующих элементов:

- подписка Azure AD;
- подписка MOVEit Transfer с Azure AD integration с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление MOVEit передача — интеграция Azure AD из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-moveit-transfer---azure-ad-integration-from-hello-gallery"></a>Добавление MOVEit передача — интеграция Azure AD из галереи hello
Интеграция hello tooconfigure передачи MOVEit - интеграция Azure AD в Azure AD необходимо tooadd MOVEit передача — интеграция Azure AD из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd передача MOVEit — интеграция Azure AD из галереи hello выполните hello следующие шаги.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Кнопка Hello Azure Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Hello корпоративных приложений колонку][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Кнопка нового приложения Hello][3]

4. Введите в поле поиска hello **MOVEit передача — интеграция Azure AD**выберите **MOVEit передача — интеграция Azure AD** из панели результатов щелкните **добавить** hello tooadd кнопку приложение.

    ![Передача MOVEit — интеграция Azure AD в списке результатов hello](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD

В этом разделе показано, как настроить и проверить единый вход Azure AD в приложение MOVEit Transfer - Azure AD integration с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow hello аналог пользователя во время передачи MOVEit - интеграция Azure AD tooa пользователя в Azure AD. Другими словами связи между пользователя Azure AD и hello связанных пользователей во время передачи MOVEit - интеграция Azure AD должен установить toobe.

Во время передачи MOVEit - интеграция Azure AD, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.

tooconfigure и тестирования Azure AD единого входа для передачи MOVEit - интеграция Azure AD, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя Azure AD интеграции переноса MOVEit -](#create-a-moveit-transfer---azure-ad-integration-test-user)**  - toohave аналог Саймон Britta во время передачи MOVEit - интеграция Azure AD, представление связанных toohello Azure AD пользователя.
4. **[Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#test-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configure-azure-ad-single-sign-on"></a>Настройка единого входа Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в MOVEit передачи - интеграция приложения Azure AD.

**tooconfigure Azure AD единого входа для передачи MOVEit - интеграция Azure AD, выполните следующие шаги hello.**

1. В hello в hello портала Azure **MOVEit передача — интеграция Azure AD** странице интеграции приложения щелкните **единого входа**.

    ![Ссылка "Настройка единого входа"][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_samlbase.png)

3. На hello **MOVEit передача — интеграция Azure AD доменов и URL-адреса** выполните следующие шаги hello:

    ![Настройка единого входа](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_url.png)

    а. В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://contoso.com`

    b. В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://contoso.com/<tenatid>`

    c. В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://contoso.com/<tenatid>/SAML/SSO/HTTP-Post`    
     
    > [!NOTE] 
    > Эти значения приведены в качестве примера. Обновить значения hello фактический идентификатор, URL-адрес ответа и URL-адрес входа. Можно ссылаться эти значения позже в **URL-адрес метаданных службы поставщика** разделу или обратитесь в службу [MOVEit передача — группа поддержки клиента Azure AD интеграции](https://community.ipswitch.com/s/support) tooget эти значения.

4. На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.

    ![ссылку для скачивания сертификата Hello](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_400.png)
    
6. Войдите на tooyour MOVEit передачи клиента с правами администратора.

7. На панели навигации слева hello, нажмите кнопку **параметры**.

    ![Раздел Settings (Параметры) на стороне приложения](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_000.png)

8. Щелкните ссылку **Single Signon** (Единый вход), которая расположена в разделе **Security Policies -> User Auth** (Политики безопасности -> Проверка подлинности пользователя).

    ![Политики безопасности на стороне приложения](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_001.png)

9. Щелкните hello hello URL-адрес метаданных ссылки toodownload документа метаданных.

    ![URL-адрес метаданных поставщика службы](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_002.png)
    
    * Проверьте **entityID** соответствует **идентификатор** в hello **MOVEit передача — интеграция Azure AD доменов и URL-адреса** раздела.
    * Проверьте **AssertionConsumerService** соответствует URL-адрес расположения **URL-адрес ОТВЕТА** в hello **MOVEit передача — интеграция Azure AD доменов и URL-адреса** раздела.
    
    ![Настройка единого входа на стороне приложения](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_007.png)

10. Нажмите кнопку **Добавление поставщика удостоверений** кнопку tooadd новый поставщик федеративных удостоверений.

    ![Добавление поставщика удостоверений](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_003.png)

11. Нажмите кнопку **Обзор...**  tooselect hello файл метаданных, который был загружен с портала Azure, а затем щелкните **Добавление поставщика удостоверений** tooupload hello загрузили файл.

    ![Поставщик удостоверений SAML](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_004.png)

12. Выберите «**Да**» как **включено** в hello **изменить параметры поставщика федеративных удостоверений...**  и нажмите кнопку **Сохранить**.

    ![Параметры федеративного поставщика удостоверений](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_005.png)

13. В hello **изменение федеративного удостоверения пользователя параметры поставщика** выполните hello, следующие действия:
    
    ![Изменение параметров федеративного поставщика удостоверений](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_006.png)
    
    а. Выберите значение **SAML NameID** для параметра **Login name** (Имя для входа).
    
    b. Выберите **других** как **полное имя** и в hello **имя атрибута** текстовое поле поместить значение hello: `http://schemas.microsoft.com/identity/claims/displayname`.
    
    c. Выберите **других** как **электронной почты** и в hello **имя атрибута** текстовое поле поместить значение hello: `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.
    
    d. Выберите значение **Yes** (Да) для параметра **Auto-create account on signon** (Автоматическое создание учетной записи при первом входе).
    
    д. Нажмите кнопку **Сохранить** .

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD

Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

   ![Создание тестового пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello hello левой панели портала Azure щелкните hello **Azure Active Directory** кнопки.

    ![Кнопка Hello Azure Active Directory](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_01.png)

2. слишком go toodisplay hello список пользователей,**пользователей и групп**, а затем нажмите кнопку **всех пользователей**.

    ![Здравствуйте, «Пользователи и группы» и «Все пользователи» ссылки](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_02.png)

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** вверху hello hello **всех пользователей** диалоговое окно.

    ![Кнопка "Добавить" Hello](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_03.png)

4. В hello **пользователя** диалогового окна выполните следующие шаги hello:

    ![диалоговое окно приветствия пользователя](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_04.png)

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** поле типа hello адрес электронной почты пользователя Саймон Britta.

    c. Выберите hello **Показать пароль** флажок и запишите значение hello, отображаемый в hello **пароль** поле.

    d. Щелкните **Создать**.
 
### <a name="create-a-moveit-transfer---azure-ad-integration-test-user"></a>Создание тестового пользователя MOVEit Transfer - Azure AD integration

Цель этого раздела Hello — toocreate пользователя с именем Britta Simon во время передачи MOVEit - интеграция Azure AD. Приложение MOVEit Transfer - Azure AD integration поддерживает JIT-подготовку, и вы уже включили ее. В этом разделе никакие действия с вашей стороны не требуются. Новый пользователь создается во время попытки tooaccess MOVEit передача — интеграция Azure AD, если он еще не существует.

>[!NOTE]
>Если требуется toocreate пользователя вручную, необходимо toocontact hello [MOVEit передача — группа поддержки клиента Azure AD интеграции](https://community.ipswitch.com/s/support).

### <a name="assign-hello-azure-ad-test-user"></a>Назначить hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooMOVEit передача — интеграция Azure AD.

![Назначение пользователям ролей hello][200] 

**tooassign tooMOVEit Britta Simon передача — интеграция Azure AD, выполните hello следующие шаги.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **MOVEit передача — интеграция Azure AD**.

    ![Hello MOVEit передача — интеграция Azure AD ссылку в список приложений hello](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_app.png)  

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Hello ссылку «Пользователи и группы»][202]

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![область назначения, добавьте Hello][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="test-single-sign-on"></a>Проверка единого входа

Цель этого раздела Hello является tootest конфигурации единого входа Azure AD с помощью панели доступа "hello".

При нажатии кнопки hello передача MOVEit — Azure AD интеграции плитки в hello панели доступа, вы должны получить автоматически вошедшего tooyour передачи MOVEit - интеграция приложения Azure AD. 

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_203.png

