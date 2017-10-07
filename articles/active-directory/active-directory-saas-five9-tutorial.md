---
title: "Руководство по интеграции Azure Active Directory с Five9 Plus Adapter (CTI, Contact Center Agents) | Документы Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и Five9 адаптера, а также (контакт Center агентов, CTI)."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 88dc82ab-be0b-4017-8335-c47d00775d7b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: jeedes
ms.openlocfilehash: 2e3ea8b5f2a6eaa8ad17d39e03fa490038b14561
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-five9-plus-adapter-cti-contact-center-agents"></a>Руководство по интеграции Azure Active Directory с Five9 Plus Adapter (CTI, Contact Center Agents)

В этом учебнике вы узнаете, как toointegrate Five9 Plus адаптера (CTI, агенты Center контактов) с Azure Active Directory (Azure AD).

Интеграция Five9 адаптера, а также (CTI, агенты Center контактов) с Azure AD предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooFive9 плюс адаптера (контакт Center агентов, CTI)
- Можно включить пользователя пользователей tooautomatically get вошедшего tooFive9 плюс адаптера (CTI, агенты Center контакт) (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

Интеграция tooconfigure Azure AD с Five9 плюс адаптером (CTI, агенты Center контакт), необходимо hello следующих элементов:

- подписка Azure AD;
- подписка Five9 Plus Adapter (CTI, Contact Center Agents) с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление Five9 адаптера, а также (CTI, агенты Center контакт) из коллекции hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-five9-plus-adapter-cti-contact-center-agents-from-hello-gallery"></a>Добавление Five9 адаптера, а также (CTI, агенты Center контакт) из коллекции hello
tooconfigure hello интеграция Five9 адаптера, а также (CTI, агенты Center контактов) в Azure AD, вы должны tooadd Five9 адаптера, а также (CTI, агенты Center контакт) из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd Five9 плюс адаптера (CTI, агенты Center контакт) из коллекции hello выполните hello следующие шаги.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Приложения][3]

4. Введите в поле поиска hello **Five9 адаптера, а также (CTI, агенты Center контакт)**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-five9-tutorial/tutorial_five9_search.png)

5. В панели результатов hello выберите **Five9 адаптера, а также (контакт Center агентов, CTI)**и нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-five9-tutorial/tutorial_five9_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в Five9 Plus Adapter (CTI, Contact Center Agents) для тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в Five9 адаптера, а также (CTI, агенты Center контакт) является tooa в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в Five9 адаптера, а также (CTI, агенты Center контакт) должен установить toobe.

В Five9 плюс адаптера (контакт Center агентов, CTI), присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.

tooconfigure и теста Azure AD единого входа с Five9 плюс адаптера (CTI, агенты Center контакт), требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя Five9 адаптера, а также (CTI, агенты Center контакт)](#creating-a-five9-plus-adapter-cti-contact-center-agents-test-user)**  -toohave аналог Саймон Britta в Five9, а также адаптер (контакт Center агентов, CTI), представление связанных toohello Azure AD пользователя.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении Five9 адаптера, а также (контакт Center агентов, CTI).

**tooconfigure Azure AD единого входа с Five9 адаптером, а также (CTI, обратитесь в службу центра агенты), выполните следующие шаги hello.**

1. В hello в hello портала Azure **Five9 адаптера, а также (CTI, агенты Center контакт)** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-five9-tutorial/tutorial_five9_samlbase.png)

3. На hello **Five9 адаптера, а также (CTI, агенты Center контакт) домена и URL-адреса** выполните следующие шаги hello:

    ![Настройка единого входа](./media/active-directory-saas-five9-tutorial/tutorial_five9_url.png)
    
    а. В hello **идентификатор** текстовое поле, введите URL-адрес, используя hello следующие шаблоны:

    |    Среда      |       URL-адрес      |
    | :-- | :-- |
    | Для "Five9 Plus Adapter for Microsoft Dynamics CRM" | `https://app.five9.com/appsvcs/saml/metadata/alias/msdc` |
    | Для "Five9 Plus Adapter for Zendesk" | `https://app.five9.com/appsvcs/saml/metadata/alias/zd` |
    | Для "Five9 Plus Adapter for Agent Desktop Toolkit" | `https://app.five9.com/appsvcs/saml/metadata/alias/adt` |

    b. В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:

    |      Среда     |      URL-адрес      |
    | :--                  | :--           |
    | Для "Five9 Plus Adapter for Microsoft Dynamics CRM" | `https://app.five9.com/appsvcs/saml/SSO/alias/msdc` |
    | Для "Five9 Plus Adapter for Zendesk" | `https://app.five9.com/appsvcs/saml/SSO/alias/zd` |
    | Для "Five9 Plus Adapter for Agent Desktop Toolkit" | `https://app.five9.com/appsvcs/saml/SSO/alias/adt` |

4. На hello **сертификат подписи SAML** щелкните **Certificate(Base64)** и затем сохраните файл сертификата hello на вашем компьютере.

    ![Настройка единого входа](./media/active-directory-saas-five9-tutorial/tutorial_five9_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-five9-tutorial/tutorial_general_400.png)

6. На hello **конфигурация Five9 адаптера, а также (CTI, агенты Center контакт)** щелкните **Настройка Five9 плюс адаптера (CTI, агенты Center контакт)** tooopen **Настройкавхода** окна. Копировать hello **URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** из hello **краткий справочник.**

    ![Настройка единого входа](./media/active-directory-saas-five9-tutorial/tutorial_five9_configure.png) 

7. tooconfigure единого входа на **Five9 адаптера, а также (CTI, агенты Center контакт)** стороны, необходимо загрузить hello toosend **Certificate(Base64), URL-адрес выхода, идентификатор сущности SAML и SAML единого входа URL-адрес службы** слишком[Five9 Plus (CTI, агенты Center контакт) поддержка адаптеров](https://www.five9.com/about/contact). Также Кроме того, для дальнейшей настройки единого входа выполните hello toohello адаптера в соответствии с шаги, описанные ниже.

    а. Руководство администратора "Five9 Plus Adapter for Agent Desktop Toolkit": [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/agent-desktop-toolkit/plus-agent-desktop-toolkit-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/agent-desktop-toolkit/plus-agent-desktop-toolkit-administrators-guide.pdf)
    
    b. Руководство администратора "Five9 Plus Adapter for Microsoft Dynamics CRM": [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/microsoft/microsoft-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/microsoft/microsoft-administrators-guide.pdf)
    
    c. Руководство администратора "Five9 Plus Adapter for Zendesk": [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/zendesk/zendesk-plus-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/zendesk/zendesk-plus-administrators-guide.pdf)


> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-five9-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-five9-tutorial/create_aaduser_02.png) 

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-five9-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-five9-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-a-five9-plus-adapter-cti-contact-center-agents-test-user"></a>Создание тестового пользователя Five9 Plus Adapter (CTI, Contact Center Agents)

В этом разделе вы создадите тестового пользователя по имени Britta Simon в Five9 Plus Adapter (CTI, Contact Center Agents). Работать с [Five9 Plus (CTI, агенты Center контакт) поддержка адаптеров](https://www.five9.com/about/contact) для добавления пользователей hello в платформе hello Five9 адаптера, а также (контакт Center агентов, CTI). Перед использованием единого входа необходимо создать и активировать пользователей.

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooFive9 плюс адаптера (контакт Center агентов, CTI).

![Назначение пользователя][200] 

**tooassign Britta Simon tooFive9 плюс адаптера (CTI, обратитесь в службу центра агенты), выполните следующие шаги hello.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **Five9 адаптера, а также (CTI, агенты Center контакт)**.

    ![Настройка единого входа](./media/active-directory-saas-five9-tutorial/tutorial_five9_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.

При нажатии кнопки hello Five9 адаптера, а также (контакт Center агентов, CTI) плитки в панели доступа hello, вы должны получить приложения автоматически вошедшего tooyour Five9 адаптера, а также (контакт Center агентов, CTI).
Дополнительные сведения о панели доступа см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-five9-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-five9-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-five9-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-five9-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-five9-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-five9-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-five9-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-five9-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-five9-tutorial/tutorial_general_203.png

