---
title: "Руководство по интеграции Azure Active Directory с Qlik Sense Enterprise | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и корпоративный Qlik смысле."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 8c27e340-2b25-47b6-bf1f-438be4c14f93
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: 153edb3f8cd41790d4e9a74f15cfb806e5e9e3b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-qlik-sense-enterprise"></a>Руководство. Интеграция Azure Active Directory с Qlik Sense Enterprise

В этом учебнике вы узнаете, как toointegrate Qlik смысле предприятия в Azure Active Directory (Azure AD).

Интеграция Qlik смысле предприятия с Azure AD предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooQlik смысле предприятия.
- Вы можете включить учетные записи Azure AD вашей пользователей tooautomatically get вошедшего tooQlik смысле предприятия (Single Sign-On).
- Вы можете управлять учетными записями в одном централизованном месте - hello портал Azure.

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с Qlik смысле предприятия необходимо hello следующих элементов:

- подписка Azure AD;
- подписка Qlik Sense Enterprise с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не используйте рабочую среду без необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление Qlik смысле Enterprise из коллекции hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-qlik-sense-enterprise-from-hello-gallery"></a>Добавление Qlik смысле Enterprise из коллекции hello
tooconfigure hello интеграции Qlik смысле предприятия в Azure AD, вы должны tooadd Enterprise смысле Qlik из списка tooyour коллекции hello управляемых приложений SaaS.

**tooadd Enterprise смысле Qlik из галереи hello выполните hello следующие шаги.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Кнопка Hello Azure Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Hello корпоративных приложений колонку][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна.

    ![Кнопка нового приложения Hello][3]

4. Введите в поле поиска hello **Enterprise смысле Qlik**выберите **Qlik смысле Enterprise** из панели результатов щелкните **добавить** кнопку tooadd приложения hello.

    ![Enterprise смысле Qlik в списке результатов hello](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD

В этом разделе описана настройка и проверка единого входа Azure AD в Qlik Sense Enterprise с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в смысле Enterprise Qlik является tooa в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в смысле Enterprise Qlik должен установить toobe.

В Enterprise смысле Qlik, присвойте значение hello hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** tooestablish hello связи.

tooconfigure и теста Azure AD единого входа с Qlik смысле Enterprise, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя Enterprise смысле Qlik](#create-a-qlik-sense-enterprise-test-user)**  -toohave аналог Саймон Britta Qlik смысле предприятии, которая является представлением связанного toohello Azure AD пользователя.
4. **[Назначить hello Azure AD тестового пользователя](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#test-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configure-azure-ad-single-sign-on"></a>Настройка единого входа Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении предприятия Qlik смысле.

**tooconfigure Azure AD единого входа с Qlik смысле Enterprise, выполните следующие шаги hello.**

1. В hello в hello портала Azure **Enterprise смысле Qlik** странице интеграции приложения щелкните **единого входа**.

    ![Ссылка "Настройка единого входа"][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_samlbase.png)

3. На hello **URL-адреса и домена предприятия смысле Qlik** выполните следующие шаги hello:

    ![Сведения о домене и URL-адресах в приложении Qlik Sense Enterprise](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_url.png)

    а. В hello **URL-адрес входа** текстовом поле введите URL-адрес, используя следующий шаблон hello:`https://<Qlik Sense Fully Qualifed Hostname>:443//samlauthn/`
    
    > [!NOTE]
    > Обратите внимание, hello завершающей косой чертой в конце hello данного универсального кода ресурса. Она обязательная.
    
    b. В hello **идентификатор** текстовом поле введите URL-адрес, используя следующий шаблон hello:
    | |
    |--|
    | `https://<Qlik Sense Fully Qualifed Hostname>.qlikpoc.com`|
    | `https://<Qlik Sense Fully Qualifed Hostname>.qliksense.com`|

    > [!NOTE] 
    > Эти значения приведены в качестве примера. Обновление, эти значения с hello фактический URL-адрес входа и идентификатора, которые рассматриваются далее в этот учебник или обратитесь к [Qlik смысле корпоративный клиент поддержки](https://www.qlik.com/us/services/support) tooget эти значения. 

4. На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и затем сохраните файл метаданных hello на вашем компьютере.

    ![ссылку для скачивания сертификата Hello](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_certificate.png) 

5. Нажмите кнопку **Сохранить** .

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_400.png)

6. Подготовьте файл hello XML метаданных федерации можно передать этот сервер tooQlik смысле.
   
    > [!NOTE]
    > Перед отправкой toohello метаданных поставщика удостоверений hello смысле Qlik сервера, необходимо изменить toobe tooremove сведения tooensure правильную работу между Azure AD файл hello и смысле Qlik сервера.
    
    ![QlikSense][qs24]
   
    а. Откройте файл FederationMetaData.xml hello, который вы скачали из портала Azure в текстовом редакторе.
   
    b. Найдите значение hello **RoleDescriptor**.  Вы найдете четыре записи (две пары открывающих и закрывающих тегов для элементов).
   
    c. Удалите теги RoleDescriptor hello и все данные из файла hello между ними.
   
    d. Сохраните файл hello и сохранить его ближайших для дальнейшего использования в этом документе.

7. Перейдите toohello Qlik управления Qlik смысле консоли (QMC) от пользователя, который можно создать конфигурации виртуального прокси-сервера.

8. Hello QMC щелкнуть hello **виртуальные учетные записи-посредники** элемента меню.
   
    ![QlikSense][qs6] 

9. Hello нижней части экрана приветствия, щелкните hello **создать новый** кнопки.
   
    ![QlikSense][qs7]

10. Появится экран Редактирование Hello виртуальной прокси-сервера.  На hello в правой части экрана приветствия — это меню для отображения параметров конфигурации.
   
    ![QlikSense][qs9]

11. Параметр меню идентификации hello этот флажок установлен введите hello идентифицирующие сведения для настройки прокси-сервера Azure виртуальных hello.
    
    ![QlikSense][qs8]  
    
    а. Hello **описание** поля — это понятное имя для конфигурации виртуального прокси hello.  Введите значение в поле Description (Описание).
    
    b. Hello **префикса** поле определяет конечную hello виртуального прокси для соединения с Azure AD Single Sign-On tooQlik смысле.  Введите уникальное имя префикса для этого виртуального прокси-сервера.
    
    c. **Время ожидания сеанса простоя (в минутах)** hello время ожидания для подключения через этот виртуальный прокси-сервер.
    
    d. Hello **имя заголовка файла cookie сеанса** является хранение имя файла cookie hello hello идентификатор сеанса для hello смысле Qlik сеанса пользователь получает после успешной проверки подлинности.  Это имя должно быть уникальным.

12. Щелкните меню параметр hello проверки подлинности toomake его видимым.  Появится экран приветствия проверки подлинности.
    
    ![QlikSense][qs10]
    
    а. Hello **режим анонимного доступа** определяет раскрывающийся список, если анонимные пользователи могут обращаться к Qlik смысле через виртуальный hello прокси-сервера.  анонимный пользователь не параметр по умолчанию Hello.
    
    b. Hello **метод проверки подлинности** раскрывающийся список определяет, будет использоваться виртуальный прокси схемы проверки подлинности hello hello.  Выберите SAML из раскрывающегося списка hello.  После этого появятся дополнительные параметры.
    
    c. В hello **поле URI узла SAML**, входной hello hostname пользователи вводят tooaccess Qlik смысле через этот прокси виртуального SAML.  Имя узла Hello представляет uri hello hello server Qlik смысле.
    
    d. В hello **идентификатор сущности SAML**, введите hello того же значения, указанного для узла URI hello SAML поля.
    
    д. Hello **метаданные поставщика удостоверений SAML** — файл hello изменить ранее в hello **редактирование метаданных федерации из конфигурации Azure AD** раздела.  **Перед отправкой hello метаданные поставщика удостоверений, необходимо изменить toobe файл hello** tooremove сведения tooensure правильную работу между Azure AD и смысле Qlik сервера.  **Если файл hello имеет еще toobe изменить см. выше toohello инструкций.**  Если hello файл был изменен нажмите кнопку обзора hello и выберите hello измененные метаданные файла tooupload его toohello Конфигурация виртуальных прокси-сервера.
    
    f. Введите имя или схема ссылку hello атрибут для hello атрибут SAML, представляющий hello **UserID** Azure AD отправляет toohello смысле Qlik сервера.  Схемы справочная информация доступна в конфигурации записи экраны hello приложения Azure.  атрибут имени toouse hello, введите `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.
    
    ж. Введите значение hello hello **каталог пользователя** , которые будут вложенного toousers при проверке подлинности сервера смысле tooQlik через Azure AD.  Жестко заданные значения нужно заключить в **квадратные скобки []**.  toouse атрибут, отправляемый в hello утверждения Azure AD SAML, введите имя hello hello атрибута в этом текстовом поле **без** квадратные скобки.
    
    h. Hello **алгоритм подписи SAML** наборов hello подписи для конфигурации виртуального прокси hello сертификата службы поставщика (в этого обращения Qlik смысле сервера).  Если сервер смысле Qlik использует доверенный сертификат, созданный с помощью Microsoft Enhanced RSA и AES Cryptographic Provider, измените алгоритм подписи SAML hello слишком**SHA-256**.
    
    i. для дополнительных атрибутов, таких как группы toobe отправлено tooQlik смысле для использования в правилах безопасности позволяет Hello разделе сопоставление атрибута SAML.

13. Щелкните hello **БАЛАНСИРОВКИ НАГРУЗКИ** toomake параметр меню его видимым.  Появится экран балансировки нагрузки Hello.
    
    ![QlikSense][qs11]

14. Щелкните hello **добавить новый узел сервера** кнопку engine выберите узел или узлы Qlik смысле отправки в целях балансировки нагрузки toofor сеансы и щелкните hello **добавить** кнопки.
    
    ![QlikSense][qs12]

15. Щелкните toomake параметр меню "Дополнительно" hello его видимым. Появится экран дополнительных Hello.
    
    ![QlikSense][qs13]
    
    список разрешенных Hello узла определяет имена узлов, которые принимаются при подключении toohello смысле Qlik сервера.  **Введите имя узла hello, которую пользователи будут указывать при подключении сервера tooQlik смысле.** Имя узла Hello — hello одинаковое значение как hello SAML uri узла без hello https://.

16. Нажмите кнопку hello **применить** кнопки.
    
    ![QlikSense][qs14]

17. Нажмите кнопку ОК tooaccept hello предупредительное сообщение, указывающее прокси-серверы виртуальных toohello связанный прокси-сервер будет перезапущен.
    
    ![QlikSense][qs15]

18. Hello правой части экрана приветствия появится hello связанные элементы меню.  Щелкните hello **учетные записи-посредники** пункт меню.
    
    ![QlikSense][qs16]

19. Появится экран приветствия прокси-сервера.  Нажмите кнопку hello **ссылку** , расположенную в нижней toolink hello виртуального прокси toohello прокси-сервера.
    
    ![QlikSense][qs17]

20. Узел прокси-сервера выберите hello, который будет поддерживать этот виртуальный прокси-подключения и нажмите кнопку hello **ссылку** кнопки.  После связывания, hello прокси-сервера будут перечислены под ними прокси-серверы.
    
    ![QlikSense][qs18]
  
    ![QlikSense][qs19]

21. После будут отображаться пять секунд tooten, обновите QMC сообщение hello.  Нажмите кнопку hello **QMC обновление** кнопки.
    
    ![QlikSense][qs20]

22. После обновления hello QMC щелкните hello **виртуальные учетные записи-посредники** элемента меню. Hello новая запись SAML виртуального прокси-сервера перечислены в таблице hello на экране приветствия.  Одним щелчком на запись hello виртуального прокси-сервера.
    
    ![QlikSense][qs51]

23. Hello нижней части экрана приветствия активируется кнопка метаданные SP загрузить hello.  Щелкните hello **метаданные SP загрузить** файл tooa метаданных hello toosave кнопки.
    
    ![QlikSense][qs52]

24. Файл метаданных Привет открыть пакет.  Наблюдать за hello **entityID** входа и hello **AssertionConsumerService** входа.  Эти значения имеют эквивалентные toohello **идентификатор** и hello **URL-адрес входа** в конфигурации приложения hello Azure AD. Вставьте эти значения в hello **URL-адреса и домена предприятия смысле Qlik** раздела конфигурации приложения hello Azure AD, если они не совпадают, то их следует заменить приветствия мастера настройки приложения Azure AD.
    
    ![QlikSense][qs53]

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание тестового пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello hello левой панели портала Azure щелкните hello **Azure Active Directory** кнопки.

   ![Кнопка Hello Azure Active Directory](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_01.png)

2. слишком go toodisplay hello список пользователей,**пользователей и групп**, а затем нажмите кнопку **всех пользователей**.

   ![Здравствуйте, «Пользователи и группы» и «Все пользователи» ссылки](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_02.png)

3. tooopen hello **пользователя** диалоговое окно, нажмите кнопку **добавить** вверху hello hello **всех пользователей** диалоговое окно.

   ![Кнопка "Добавить" Hello](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_03.png)

4. В hello **пользователя** диалогового окна выполните следующие шаги hello:

   ![диалоговое окно приветствия пользователя](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_04.png)

   а. В hello **имя** введите **BrittaSimon**.

   b. В hello **имя пользователя** поле типа hello адрес электронной почты пользователя Саймон Britta.

   c. Выберите hello **Показать пароль** флажок и запишите значение hello, отображаемый в hello **пароль** поле.

   d. Щелкните **Создать**.
 
### <a name="create-a-qlik-sense-enterprise-test-user"></a>Создание тестового пользователя Qlik Sense Enterprise

В этом разделе описано, как создать пользователя Britta Simon в приложении Sense Enterprise. Работать с [Qlik смысле корпоративный клиент поддержки](https://www.qlik.com/us/services/support) для добавления пользователей hello в hello Qlik смысле корпоративной платформы. Перед использованием единого входа необходимо создать и активировать пользователей. 

### <a name="assign-hello-azure-ad-test-user"></a>Назначить hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления доступа tooQlik смысле предприятия.

![Назначение пользователям ролей hello][200] 

**tooassign tooQlik Britta Simon смысле Enterprise, выполните hello следующие шаги.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **Qlik смысле Enterprise**.

    ![ссылка на корпоративный смысле Qlik Hello в списке приложений hello](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_app.png)  

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Hello ссылку «Пользователи и группы»][202]

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![область назначения, добавьте Hello][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="test-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.

Если щелкнуть плитку Enterprise смысле Qlik hello в hello панели доступа, следует получать автоматически вошедшего tooyour Qlik смысле корпоративного приложения. 

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_203.png

[qs6]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_06.png
[qs7]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_07.png
[qs8]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_08.png
[qs9]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_09.png
[qs10]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_10.png
[qs11]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_11.png
[qs12]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_12.png
[qs13]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_13.png
[qs14]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_14.png
[qs15]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_15.png
[qs16]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_16.png
[qs17]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_17.png
[qs18]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_18.png
[qs19]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_19.png
[qs20]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_20.png
[qs24]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_24.png
[qs51]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_51.png
[qs52]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_52.png
[qs53]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_53.png

