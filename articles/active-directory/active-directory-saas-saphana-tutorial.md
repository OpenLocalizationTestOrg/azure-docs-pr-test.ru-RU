---
title: "Руководство по интеграции Azure Active Directory с SAP HANA | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и SAP HANA."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: cef4a146-f4b0-4e94-82de-f5227a4b462c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 5ff6bfde0b1d7ab14025a4bc45199f9f826affd1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-hana"></a>Руководство по интеграции Azure Active Directory с SAP HANA

В этом учебнике вы узнаете, как toointegrate SAP HANA с Azure Active Directory (Azure AD).

Интеграция SAP HANA с Azure AD предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooSAP HANA
- Можно включить на пользователей tooautomatically get вошедшего tooSAP HANA (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с SAP HANA, требуется hello следующих элементов:

- подписка Azure AD;
- подписка SAP HANA с поддержкой единого входа;
- экземпляр HANA, выполняемый на любой общедоступной IaaS, локально, на виртуальной машине Azure или в решении "Крупные экземпляры SAP в Azure";
- Hello XSA администрирования веб-интерфейса, а также HANA Studio установлена на экземпляре HANA hello.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется использовать рабочей среде SAP HANA. Сначала протестируйте интеграцию hello в разработки или промежуточной среде приложения hello, а затем используйте hello рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление SAP HANA из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-sap-hana-from-hello-gallery"></a>Добавление SAP HANA из галереи hello
tooconfigure hello интеграции SAP HANA в Azure AD, вы должны tooadd SAP HANA из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd SAP HANA из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Кнопка Hello Azure Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Hello корпоративных приложений колонку][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Кнопка нового приложения Hello][3]

4. Введите в поле поиска hello **SAP HANA**выберите **SAP HANA** из панели результатов щелкните **добавить** кнопку tooadd приложения hello. 

    ![Новое приложение Hello](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в приложение SAP HANA с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в SAP HANA является tooa в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в SAP HANA должен установить toobe.

В SAP HANA, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.

tooconfigure и теста Azure AD единого входа с SAP HANA, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя SAP HANA](#creating-a-sap-hana-test-user)**  -toohave аналог Саймон Britta в SAP HANA, который представляет связанный toohello Azure AD пользователя.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении SAP HANA.

**tooconfigure Azure AD единого входа с SAP HANA, выполните следующие шаги hello.**

1. В hello в hello портала Azure **SAP HANA** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_samlbase.png)

3. На hello **URL-адреса и SAP HANA домена** выполните следующие шаги hello:

    ![Сведения о домене и URL-адресах единого входа](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_url.png)

    а. В hello **идентификатор** текстовое поле, тип, что:`HA100` 

    b. В hello **URL-адрес ответа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<Customer-SAP-instance-url>/sap/hana/xs/saml/login.xscfunc`

    > [!NOTE] 
    > Эти значения приведены в качестве примера. Обновите эти значения с hello фактический идентификатор и ответ URL-адрес. Обратитесь к [группа поддержки клиента SAP HANA](https://cloudplatform.sap.com/contact.html) tooget эти значения. 

4. На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.

    ![ссылку для скачивания сертификата Hello](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_certificate.png) 

    >[!Note]
    >Если сертификат не используется затем сделайте его активным, щелкнув hello флажок «Сделать новый сертификат active» в hello Azure AD. 

5. SAP HANA приложение ожидает утверждения SAML hello в определенном формате. пример Hello следующий снимок экрана для этого. Здесь мы сопоставленной hello **идентификатор пользователя** с **ExtractMailPrefix()** функция **user.mail**. Это дает значение hello префикс адреса электронной почты пользователя hello, что является hello уникальный ИД пользователя. Это число отправляется toohello приложения SAP HANA в каждом успешного ответа.

    ![Настройка единого входа](./media/active-directory-saas-saphana-tutorial/attribute.png)

6. В hello **атрибуты пользователя** раздела, посвященного hello **единого входа** диалогового окна:

    а. В hello **идентификатор пользователя** раскрывающегося списка выберите **ExtractMailPrefix**.
    
    b. В hello **Mail** раскрывающегося списка выберите **user.mail**.

7. Нажмите кнопку **Сохранить** .

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-saphana-tutorial/tutorial_general_400.png)
    
8. tooconfigure единого входа на **SAP HANA** стороны, tooyour входа **HANA XSA веб-консоли** путем просмотра toohello соответствующей конечной точки HTTPS.

    > [!Note]
    > В конфигурации по умолчанию hello URL-адрес hello перенаправляет hello запроса tooa входа в систему, что требует учетные данные hello прошедшего проверку подлинности SAP HANA базы данных toocomplete hello процесса входа пользователя. Hello пользователь, вошедший должен иметь задач администрирования SAML tooperform необходимые привилегии hello.

9. Hello XSA веб-интерфейса, перейдите слишком**поставщика удостоверений SAML** и после этого нажмите кнопку hello **«+»** -кнопку внизу hello hello экрана toodisplay hello добавить сведения о поставщике удостоверений области и выполнение Здравствуйте, следующие шаги:

    ![Добавление поставщика удостоверений](./media/active-directory-saas-saphana-tutorial/sap1.png)

    а. В hello **добавить сведения о поставщике удостоверений** область, содержимое hello вставить hello метаданных XML-код, загруженный с портала Azure в hello **метаданные** текстового поля.

    ![Добавление параметров поставщика удостоверений](./media/active-directory-saas-saphana-tutorial/sap2.png)

    b. Если содержимое hello hello XML-документа являются допустимыми, hello синтаксического анализа процесса извлекает сведения, необходимые tooinsert hello в hello **тему, идентификатор сущности и издателя** поля в общие данные hello область экрана и hello URL-адрес поля в hello Области экрана назначения, например,  **базовый URL-адрес и URL-адрес единого входа (*)**.

    ![Добавление параметров поставщика удостоверений](./media/active-directory-saas-saphana-tutorial/sap3.png)

    c. В поле имя hello hello общие данные область экрана, введите имя для нового поставщика удостоверений единого входа SAML hello.

    > [!Note]
    > Имя Hello hello Удостоверений SAML является обязательным и должно быть уникальным; оно появляется в список доступных IDPs SAML, который отображается, hello выборе SAML как hello метод проверки подлинности для toouse приложений SAP HANA XS, например, в области экрана приветствия проверки подлинности средства администрирования артефакта XS hello.

10. Сохраните сведения о hello hello нового поставщика удостоверений SAML. Выберите **Сохранить** toosave hello сведений поставщика удостоверений SAML hello и добавьте hello нового поставщика Удостоверений SAML toohello список известных IDPs SAML.

    ![Кнопка "Сохранить"](./media/active-directory-saas-saphana-tutorial/sap4.png)

11. В в системных свойств hello hello Studio HANA **конфигурации** вкладки, просто фильтрации настроек по **saml** и настроить hello **assertion_timeout** из **10 сек** слишком**120 сек**.

    ![Параметр assertion_timeout](./media/active-directory-saas-saphana-tutorial/sap7.png)

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Кнопка Hello Azure Active Directory](./media/active-directory-saas-saphana-tutorial/create_aaduser_01.png) 

2. hello toodisplay список пользователей, перейдите в слишком**пользователей и групп** и нажмите кнопку **всех пользователей**.
    
    ![Здравствуйте, «Пользователи и группы» и «Все пользователи» ссылки](./media/active-directory-saas-saphana-tutorial/create_aaduser_02.png) 

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** в верхней части hello диалогового окна "hello".
 
    ![Кнопка "Добавить" Hello](./media/active-directory-saas-saphana-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![диалоговое окно приветствия пользователя](./media/active-directory-saas-saphana-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-a-sap-hana-test-user"></a>Создание тестового пользователя SAP HANA

Пользователи toolog tooenable Azure AD в tooSAP HANA, их необходимо подготовить в SAP HANA.
SAP HANA поддерживает JIT-подготовку. Эта функция включена по умолчанию.

При необходимости toocreate пользователя вручную, выполните следующие шаги hello.

>[!Note]
>Вы можете изменить hello внешней проверки подлинности, используемый пользователем hello.
Внешние пользователи проходят проверку подлинности с помощью внешней системы, например системы Kerberos. Чтобы получить дополнительные сведения о внешних удостоверениях, свяжитесь со своим [администратором домена](https://cloudplatform.sap.com/contact.html).

1. Откройте hello [SAP HANA Studio](https://help.sap.com/viewer/a2a49126a5c546a9864aae22c05c3d0e/2.0.01/en-us) как администратор и включить hello DB пользователя для единого входа SAML.

    ![создать пользователя](./media/active-directory-saas-saphana-tutorial/sap5.png)

2. Деления hello невидимой флажок toohello слева от **SAML** и настройка hello по ссылке.

3. Нажмите кнопку **добавить** tooadd hello Удостоверений SAML и нажмите кнопку **ОК** при выборе соответствующего поставщика Удостоверений SAML "hello".

4. Добавить hello **внешнего идентификатора** (например) Britta Simon) или выберите **Any** (Любой) и нажмите кнопку **ОК**.

    >[!Note]
    >Если не установлен флажок «ANY», то имя пользователя hello в HANA должно tooexactly соответствия hello имя пользователя hello в hello UPN перед суффикс домена hello (т. е. BrittaSimon@contoso.com стал бы BrittaSimon в HANA).

5. Для целей тестирования, назначьте все **«XS»** toohello пользователя роли.

    ![Назначение ролей](./media/active-directory-saas-saphana-tutorial/sap6.png)

    > [!TIP]
    > Следует предоставить разрешения, которые подходят только для вашего варианта использования.

6. Сохраните hello пользователя.

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooSAP HANA.

![Назначение пользователям ролей hello][200] 

**tooassign Britta Simon tooSAP HANA, выполните следующие шаги hello.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **SAP HANA**.

    ![Назначение пользователя](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Hello ссылку «Пользователи и группы»][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![область назначения, добавьте Hello][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.

При нажатии кнопки hello SAP HANA плитки в панели доступа hello, вы должны получить автоматически вошедшего tooyour приложения SAP HANA.
Дополнительные сведения о панели доступа см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_203.png

