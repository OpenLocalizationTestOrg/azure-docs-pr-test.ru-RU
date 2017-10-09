---
title: "Руководство. Интеграция Azure Active Directory с iLMS | Документация Майкрософт"
description: "Узнайте, как tooconfigure единый вход между Azure Active Directory и iLMS."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d6e11639-6cea-48c9-b008-246cf686e726
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/13/2017
ms.author: jeedes
ms.openlocfilehash: da0936de23afcd5a4213aa6f699165f9bfa82c35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ilms"></a>Руководство. Интеграция Azure Active Directory с iLMS

В этом учебнике вы узнаете, как iLMS toointegrate с Azure Active Directory (Azure AD).

Интеграция с Azure AD iLMS предоставляет hello следующие преимущества:

- Можно управлять в Azure AD, имеющего доступ tooiLMS
- Можно включить на пользователей tooautomatically get вошедшего tooiLMS (Single Sign-On) с помощью своих учетных записей Azure AD
- Можно управлять учетными записями в одном централизованном месте - hello портал Azure

Если tooknow Дополнительные сведения об интеграции приложений SaaS в Azure AD, см. [доступ к приложению и единый вход в Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Предварительные требования

tooconfigure интеграция Azure AD с iLMS требуется hello следующих элементов:

- подписка Azure AD;
- подписка iLMS с поддержкой единого входа.

> [!NOTE]
> в этом учебнике шаги tootest hello, не рекомендуется в рабочей среде.

tootest hello шаги в этом учебнике, необходимо следовать приведенным ниже рекомендациям:

- Не следует использовать рабочую среду при отсутствии необходимости.
- Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Описание сценария
В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде. Hello сценарий, описанный в этом учебнике состоит из двух основных компонентов:

1. Добавление iLMS из галереи hello
2. Настройка и проверка единого входа в Azure AD

## <a name="adding-ilms-from-hello-gallery"></a>Добавление iLMS из галереи hello
tooconfigure hello интеграции iLMS в Azure AD, вы должны iLMS tooadd из списка tooyour коллекции hello управляемых приложений SaaS.

**iLMS tooadd из галереи hello, выполните следующие шаги hello.**

1. В hello  **[портал Azure](https://portal.azure.com)**на левой навигационной панели hello, нажмите кнопку **Azure Active Directory** значок. 

    ![Active Directory][1]

2. Перейдите в слишком**корпоративных приложений**. Затем перейдите слишком**все приложения**.

    ![Приложения][2]
    
3. tooadd новое приложение, нажмите кнопку **новое приложение** кнопку в верхней части hello диалогового окна "hello".

    ![Приложения][3]

4. Введите в поле поиска hello **iLMS**.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_search.png)

5. В панели результатов hello выберите **iLMS**, нажмите кнопку **добавить** кнопку tooadd приложения hello.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Настройка и проверка единого входа в Azure AD
В этом разделе описана настройка и проверка единого входа Azure AD в iLMS с использованием тестового пользователя Britta Simon.

Для единого входа toowork Azure AD необходима tooknow пользователь аналог какие hello в iLMS является tooa в Azure AD. Другими словами связи между пользователя Azure AD и связанных пользователей hello в iLMS должен установить toobe.

Эта связь связь устанавливается путем назначения hello значение hello **имя пользователя** в Azure AD в качестве значения hello hello **Username** в iLMS.

tooconfigure и теста Azure AD единого входа с iLMS, требуются следующие стандартные блоки hello toocomplete:

1. **[Настройка Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable вашей toouse пользователи этой функции.
2. **[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD единого входа с Саймон Britta.
3. **[Создание тестового пользователя, прошедшего iLMS](#creating-an-ilms-test-user)**  -toohave аналог Саймон Britta в iLMS, представление связанных toohello Azure AD ей.
4. **[Назначение hello Azure AD тестового пользователя](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD единым входом.
5. **[Тестирование единого входа](#testing-single-sign-on)**  -tooverify ли hello works конфигурации.

### <a name="configuring-azure-ad-single-sign-on"></a>Настройка единого входа в Azure AD

В этом разделе включения Azure AD единым входом в портал Azure hello и настройки единого входа в приложении iLMS.

**tooconfigure Azure AD единого входа с iLMS, выполните следующие шаги hello.**

1. В hello в hello портала Azure **iLMS** странице интеграции приложения щелкните **единого входа**.

    ![Настройка единого входа][4]

2. На hello **единого входа** диалогового окна выберите **режим** как **входа на базе SAML** tooenable единого входа.
 
    ![Настройка единого входа](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_samlbase.png)

3. На hello **iLMS URL-адреса и домена** выполните hello, выполните действия, при желании tooconfigure приложения hello в **IDP** инициировал режим:

    ![Настройка единого входа](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_url.png)

    а. В hello **идентификатор** текстовое поле, вставить hello **идентификатор** значение Копировать из **поставщика услуг** раздел параметров SAML в портал администрирования iLMS.

    b. В hello **URL-адрес ответа** текстовое поле, вставить hello **конечной точки (URL)** значение Копировать из **поставщика услуг** раздел параметров SAML в портал администрирования iLMS наличие следующих hello шаблон`https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`

    >[!Note]
    >Значение "123456" указано в качестве примера идентификатора.

4. Проверьте **Показывать дополнительные параметры URL-адреса**, если нужно, чтобы приложение hello tooconfigure в **SP** инициировал режим:

    ![Настройка единого входа](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_url1.png)

    В hello **URL-адрес входа** текстовое поле, вставить hello **конечной точки (URL)** значение Копировать из **поставщика услуг** раздел параметров SAML в портал администрирования iLMS как`https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`     

5. tooenable JIT-компилятора подготовки iLMS приложение ожидает утверждения SAML hello в определенном формате. Настройка следующих утверждений для этого приложения hello. Вы можете управлять hello значения этих атрибутов из hello **атрибуты пользователя** раздел на странице интеграции приложений. пример Hello следующий снимок экрана для этого.
    
    ![Настройка единого входа](./media/active-directory-saas-ilms-tutorial/4.png)
    
    Создание **подразделение, регион** и **деления** атрибуты и добавьте имя hello этих атрибутов в iLMS. Все указанные выше атрибуты являются обязательными.    

    > [!NOTE] 
    > У вас есть tooenable **Создание учетной записи пользователя Un-recognized** в iLMS toomap этих атрибутов. Следуйте инструкциям hello [здесь](http://support.inspiredelearning.com/customer/portal/articles/2204526) tooget представление hello атрибуты конфигурации.

6. В hello **атрибуты пользователя** раздела, посвященного hello **единого входа** диалогового окна, настроить атрибутов токена SAML, как показано в приведенном выше рисунке hello и выполнять hello следующие шаги:
    
    | Имя атрибута | Значение атрибута |
    | ---------------| --------------- |    
    | division | user.department |
    | region | user.state |
    | department | user.jobtitle |

    а. Нажмите кнопку **добавить атрибут** tooopen hello **Добавление атрибута** диалогового окна.

    ![Настройка единого входа](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_04.png)

    ![Настройка единого входа](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_05.png)
    
    b. В hello **имя** в текстовое поле имя атрибута типа hello, показанный для этой строки.
    
    c. Из hello **значение** списка значение атрибута типа hello, показанный для этой строки.
    
    d. Нажмите кнопку **ОК**.

7. На hello **сертификат подписи SAML** щелкните **метаданные в формате XML** и сохраните hello XML-файл на компьютере.

    ![Настройка единого входа](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_certificate.png) 

8. Нажмите кнопку **Сохранить** .

    ![Настройка единого входа](./media/active-directory-saas-iLMS-tutorial/tutorial_general_400.png)

9. В другом окне браузера, войдите в tooyour **портал администрирования iLMS** с правами администратора.

10. Нажмите кнопку **SSO:SAML** под **параметры** tooopen SAML параметров вкладки и выполнять hello следующие шаги:
    
    ![Настройка единого входа](./media/active-directory-saas-ilms-tutorial/1.png) 

    а. Разверните hello **поставщика услуг** раздела и скопируйте hello **идентификатор** и **конечной точки (URL)** значение.

    ![Настройка единого входа](./media/active-directory-saas-ilms-tutorial/2.png) 

    b. В разделе **Identity Provider** (Поставщик удостоверений) установите переключатель **Import Metadata** (Импорт метаданных).
    
    c. Выберите hello **метаданные** файла, загруженного с портала Azure из **сертификат подписи SAML** раздела.

    ![Настройка единого входа](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_ssoconfig1.png) 

    d. Если требуется, чтобы tooenable JIT Подготовка toocreate iLMS учетных записей для отмены-распознавать пользователей, выполните следующие действия:
        
       - Установите флажок **Create Un-recognized User Account** (Создать учетную запись неопознанного пользователя) для сопоставления этих атрибутов.
       
       ![Настройка единого входа](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_ssoconfig2.png)

       -  Сопоставление атрибутов hello в Azure AD с атрибутами hello в iLMS. В столбце атрибутов hello укажите hello атрибуты имени или hello значение по умолчанию.

    д. Go слишком**бизнес-правила** вкладку и выполнять hello следующие шаги: 
        
       ![Настройка единого входа](./media/active-directory-saas-ilms-tutorial/5.png)

       - Проверьте **создания Un-recognized областей, подразделения и отделы** toocreate регионы, подразделения и отделы, которые еще не существуют во время hello единым входом.
        
       - Проверьте **обновление пользовательского профиля во время входа в** toospecify ли профиль пользователя hello обновляется каждый единого входа. 
        
       - Если hello **«Обновление пустые значения для не обязательные поля в профиль пользователя»** флажок, поля необязательно профиля, в которых не указаны при входе будет возникать hello iLMS профиля пользователя toocontain пустые значения для этих полей.
        
       - Проверьте **отправлять ошибки уведомления по электронной почте** и введите hello электронной почты пользователя hello, в котором требуется tooreceive hello Ошибка уведомления по электронной почте.

11. Нажмите кнопку **Сохранить** кнопку Параметры toosave hello.

    ![Настройка единого входа](./media/active-directory-saas-ilms-tutorial/save.png)

> [!TIP]
> Вы сможете прочитать четкими версии этих инструкций внутри hello [портал Azure](https://portal.azure.com), а вы настраиваете приложение hello!  После добавления этого приложения из hello **Active Directory > корпоративных приложений** просто щелкните hello **Single Sign-On** вкладку и доступа hello внедренных документации с помощью hello  **Конфигурация** раздела внизу hello. Вы можете прочитать больше о документации embedded функции hello здесь: [документации внедренных Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
    
### <a name="creating-an-azure-ad-test-user"></a>Создание тестового пользователя Azure AD
Цель этого раздела Hello — toocreate тестового пользователя в hello вызывается Саймон Britta портал Azure.

![Создание пользователя Azure AD][100]

**toocreate тестового пользователя в Azure AD, выполните следующие шаги hello.**

1. В hello **портал Azure**, на левой панели навигации hello, нажмите кнопку **Azure Active Directory** значок.

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-ilms-tutorial/create_aaduser_01.png) 

2. Go слишком**пользователей и групп** и нажмите кнопку **всех пользователей** toodisplay hello список пользователей.
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-ilms-tutorial/create_aaduser_02.png) 

3. Вверху hello диалоговое окно приветствия щелкните **добавить** tooopen hello **пользователя** диалогового окна.
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-ilms-tutorial/create_aaduser_03.png) 

4. На hello **пользователя** диалогового окна выполните следующие шаги hello:
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-ilms-tutorial/create_aaduser_04.png) 

    а. В hello **имя** введите **BrittaSimon**.

    b. В hello **имя пользователя** в текстовое поле типа hello **адрес электронной почты** из BrittaSimon.

    c. Выберите **Показать пароль** и запишите значение hello hello **пароль**.

    d. Щелкните **Создать**.
 
### <a name="creating-an-ilms-test-user"></a>Создание тестового пользователя iLMS

Приложение поддерживает только в подготовки пользователей время и после проверки подлинности пользователей автоматически создаются в приложении hello. JIT-компилятора будет работать, если щелкнуть hello **Создание учетной записи пользователя Un-recognized** флажок во время параметр конфигурации SAML на портале администрирования iLMS.

Toocreate пользователя вручную, затем выполните следующие действия:

1. Войдите на сайте компании iLMS tooyour в качестве администратора.

2. Нажмите кнопку **«Регистрация пользователя»** под **пользователей** вкладке tooopen **Регистрация пользователя** страницы. 
   
   ![Добавление сотрудника](./media/active-directory-saas-ilms-tutorial/3.png)

3. На hello **«Регистрация пользователя»** выполните следующие шаги hello.

    ![Добавление сотрудника](./media/active-directory-saas-ilms-tutorial/create_testuser_add.png)

    а. В hello **имя** в текстовое поле имя Britta типа hello.
   
    b. В hello **Фамилия** текстового поля, типа hello фамилии Simon.

    c. В hello **адрес электронной почты** текстовом поле введите адрес электронной почты hello Саймон Britta учетной записи.

    d. В hello **область** раскрывающийся список, выберите hello значение для области.

    д. В hello **деления** раскрывающийся список, выберите hello значение для раздела.

    f. В hello **отдел** раскрывающийся список, выберите hello значение для отдела.

    ж. Щелкните **Сохранить**.

    > [!NOTE] 
    > Можно отправить toouser почты регистрации, выбрав **Отправка почты регистрации** флажок.

### <a name="assigning-hello-azure-ad-test-user"></a>Назначение hello Azure AD тестового пользователя

В этом разделе включите toouse Britta Simon Azure единого входа путем предоставления ее tooiLMS доступа.

![Назначение пользователя][200] 

**tooassign tooiLMS Britta Simon выполните следующие шаги hello.**

1. В hello портал Azure, откройте представление приложения hello, а затем перейдите toohello представления каталога и перейти слишком**корпоративных приложений** щелкните **все приложения**.

    ![Назначение пользователя][201] 

2. В списке приложений hello выберите **iLMS**.

    ![Настройка единого входа](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_app.png) 

3. В меню слева hello hello выберите **пользователей и групп**.

    ![Назначение пользователя][202] 

4. Нажмите кнопку **Добавить**. Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.

    ![Назначение пользователя][203]

5. На **пользователей и групп** диалогового окна выберите **Britta Simon** в список пользователей hello.

6. В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.

7. В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.
    
### <a name="testing-single-sign-on"></a>Проверка единого входа

В этом разделе тестирования конфигурации Azure AD единого входа с помощью панели доступа hello.

При нажатии кнопки iLMS плитки в панели доступа hello приветствия, вы должны получить автоматически вошедшего tooyour iLMS приложения.

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Список учебников по tooIntegrate приложений SaaS в Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_203.png

