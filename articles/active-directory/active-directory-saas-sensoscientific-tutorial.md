---
title: "Руководство по интеграции Azure Active Directory с беспроводной системой мониторинга температуры SensoScientific | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и системы мониторинга температуры SensoScientific беспроводной связи."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ee9a924d-ccde-45b0-ab40-877f82f5dfa2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: jeedes
ms.openlocfilehash: 4eabf7fc6457c217fd5c0c2539ab88c8110055e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sensoscientific-wireless-temperature-monitoring-system"></a>Руководство по интеграции Azure Active Directory с беспроводной системой мониторинга температуры SensoScientific

В этом учебнике вы узнаете, как toointegrate SensoScientific беспроводной температуры системы мониторинга в Azure Active Directory (Azure AD).

Интеграция системы мониторинга температуры SensoScientific беспроводной связи с Azure AD предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooSensoScientific системы мониторинга температуры беспроводной связи
- Ваш пользователей tooautomatically get вошедшего tooSensoScientific системы мониторинга беспроводной температуры (Single Sign-On) можно включить с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с помощью системы мониторинга температуры SensoScientific беспроводной связи, необходимо hello следующих элементов:

- подписка Azure AD;
- подписка на беспроводную систему мониторинга температуры SensoScientific с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление системы мониторинга температуры SensoScientific беспроводной сети из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-sensoscientific-wireless-temperature-monitoring-system-from-hello-gallery"></a>Добавление системы мониторинга температуры SensoScientific беспроводной сети из галереи hello
tooconfigure hello интеграции системы мониторинга температуры SensoScientific беспроводной сети в Azure AD, вы должны tooadd системы мониторинга температуры SensoScientific беспроводной сети из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd SensoScientific беспроводной температуры системы мониторинга из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Приложения][3]

4. Введите в поле поиска hello **системы мониторинга температуры SensoScientific беспроводной**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_search.png)

5. В панели результатов hello выберите **системы мониторинга температуры SensoScientific беспроводной**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описывается настройка и проверка единого входа Azure AD в беспроводную систему мониторинга температуры SensoScientific с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в системе наблюдения за SensoScientific беспроводной температуры является tooa в Azure AD. Другими словами связи между пользователя Azure AD и hello связанных пользователей в системе наблюдения за SensoScientific беспроводной температуры должен установить toobe.

Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **имя пользователя** в системе наблюдения за температуры SensoScientific беспроводной связи.

tooconfigure и теста Azure AD единого входа с системой мониторинга температуры SensoScientific беспроводной связи, необходимые hello toocomplete следующие стандартные блоки.

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя системы мониторинга температуры SensoScientific беспроводной](#creating-a-sensoscientific-wireless-temperature-monitoring-system-test-user)**  -toohave аналог Саймон Britta в SensoScientific беспроводной температуры мониторинг системы, связанные представление toohello Azure AD пользователь.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении системы мониторинга температуры SensoScientific беспроводной связи.

**tooconfigure Azure AD единого входа с SensoScientific беспроводной температуры системы мониторинга, выполните следующие шаги hello.**

1. В hello в hello портала Azure **системы мониторинга температуры SensoScientific беспроводной** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_samlbase.png)

3. На hello **SensoScientific беспроводной температуры мониторинга системных доменов и URL-адреса** статьи, нет необходимости tooperform, все действия приложение hello уже заранее интегрировано с Azure:

    ![Настройка единого входа](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_url.png)

4. На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.

    ![Настройка единого входа](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_400.png)

6. На hello **SensoScientific беспроводной температуры системы конфигурации мониторинга** щелкните **Настройка SensoScientific беспроводной температуры мониторинг системы** tooopen  **Настройка единого входа** окна. Копировать hello **URL-адрес выхода, идентификатор сущности SAML** и **SAML единого входа URL-адрес службы** из hello **краткий справочник.**

    ![Настройка единого входа](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_configure.png) 

7. Войдите на tooyour системы мониторинга температуры SensoScientific беспроводной приложения от имени администратора.

8. В меню навигации hello hello верхней части страницы, нажмите кнопку **конфигурации** и перейти к **Настройка** под **Single Sign On** tooopen hello настройки единого входа.

    ![Настройка единого входа](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_admin.png) 

9. В **настройки единого входа** формы выполнения hello следующие шаги:
 
    а. В качестве **имени издателя** выберите Azure AD.
    
    b. Вставить hello **идентификатор сущности SAML** скопирован из портала Azure в текстовое поле URL-адрес издателя.
    
    c. Вставить hello **SAML единого входа URL-адрес службы** скопирован из портала Azure в текстовое поле единого входа URL-адрес службы.

    d. Вставить hello **URL-адрес выхода** скопирован из портала Azure в текстовое поле URL-адрес службы единого выхода.

    д. Обзор hello сертификат, который вы загрузили с портала Azure и отправлять здесь.
    
    f. Щелкните **Сохранить**.
  
> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD](https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sensoscientific-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sensoscientific-tutorial/create_aaduser_02.png) 

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sensoscientific-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sensoscientific-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-a-sensoscientific-wireless-temperature-monitoring-system-test-user"></a>Создание текстового пользователя беспроводной системы мониторинга температуры SensoScientific

Пользователи toolog tooenable Azure AD в tooSensoScientific системы мониторинга температуры беспроводной связи, их необходимо подготовить в систему мониторинга температуры SensoScientific беспроводной связи. Работать с [группа поддержки системы мониторинга температуры SensoScientific беспроводной](https://www.sensoscientific.com/contact-us/) для добавления пользователей hello на платформе системы мониторинга температуры SensoScientific беспроводной hello. Перед использованием единого входа необходимо создать и активировать пользователей. 

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooSensoScientific системы мониторинга температуры беспроводной связи.

![Назначение пользователя][200] 

**tooassign tooSensoScientific Britta Simon системы мониторинга температуры беспроводной выполните hello следующие шаги.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **системы мониторинга температуры SensoScientific беспроводной**.

    ![Настройка единого входа](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello. Щелкните плитку системы мониторинга температуры SensoScientific беспроводной hello в hello панели доступа, будут автоматически вошедшего tooyour системы мониторинга температуры SensoScientific беспроводной приложения. Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](https://msdn.microsoft.com/library/dn308586).

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_203.png

