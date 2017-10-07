---
title: "Руководство по интеграции Azure Active Directory с облачной платформой SAP HANA | Документация Майкрософт"
description: "Узнайте, как toouse облачной платформы SAP HANA с Azure Active Directory tooenable единого входа, автоматизированной подготовки и многое другое!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: bd398225-8bd8-4697-9a44-af6e6679113a
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: cc6610969b1c7b08f776e6969a5977fc75eb9ab4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-hana-cloud-platform"></a>Учебник. Интеграция Azure Active Directory с облачной платформой SAP HANA
Цель этого учебника Hello — tooshow hello интеграцию Azure и облачная платформа SAP HANA.

Hello сценарий, описанный в этом руководстве предполагается, что уже hello следующих элементов:

* Действующая подписка на Azure
* Учетная запись облачной платформы SAP HANA.

После завершения этого учебника пользователи Azure AD, назначенные облачной платформы HANA будет tooSAP может toosingle входа в приложение hello hello Здравствуйте, [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).

>[!IMPORTANT]
>Необходима toodeploy собственное приложение или подписаться на один tootest учетной записи входа в вашей облачной платформы SAP HANA tooan приложения. В этом учебнике приложение развертывается в учетной записи hello.
> 
> 

Hello сценарий, описанный в этом руководстве состоит из hello следующие стандартные блоки.

1. Включение интеграции приложений hello для облачной платформы SAP HANA
2. Настройка единого входа.
3. Присвоение пользователю роли tooa
4. Назначение пользователей

![Сценарий](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790795.png "Сценарий")

## <a name="enabling-hello-application-integration-for-sap-hana-cloud-platform"></a>Включение интеграции приложений hello для облачной платформы SAP HANA
Hello цель этого раздела — toooutline как интеграции приложения hello tooenable для облачной платформы SAP HANA.

**Интеграция приложения hello tooenable для облачной платформы SAP HANA, выполните hello следующие шаги.**

1. В hello портала управления Azure, hello левой области навигации, выберите **Active Directory**.
   
    ![Active Directory](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700993.png "Active Directory")
2. Из hello **каталога** список, выберите hello каталога, для которого требуется Интеграция каталогов tooenable.
3. Щелкните представление приложения hello tooopen в представлении каталога hello **приложений** в верхнем меню hello.
   
    ![Приложения](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700994.png "Приложения")
4. Нажмите кнопку **добавить** hello нижней части страницы приветствия.
   
    ![Добавление приложения](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749321.png "Добавление приложения")
5. На hello **что вам требуется toodo** диалоговое окно, нажмите кнопку **добавить приложение из коллекции hello**.
   
    ![Добавление приложения из коллекции](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749322.png "Добавление приложения из коллекции")
6. В hello **поле поиска**, тип **облачной платформы SAP HANA**.
   
    ![Коллекция приложений](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790796.png "Коллекция приложений")
7. В области результатов hello выберите **облачной платформы SAP HANA**и нажмите кнопку **завершить** tooadd приложения hello.
   
    ![SAP HANA](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793929.png "SAP HANA")
   
## <a name="configure-single-sign-on"></a>Настройка единого входа

Цель этого раздела Hello — toooutline, каким образом пользователи tooenable tooauthenticate tooSAP HANA облачной платформы с помощью учетной записи в Azure AD, используя федерацию на основе hello SAML протокола.

В рамках этой процедуры, необходимые tooupload клиента tooyour облачной платформы SAP HANA сертификат в кодировке base-64.  

Если вы не знакомы с этой процедурой, см. раздел [как tooconvert двоичные данные сертификата в текстовый файл](http://youtu.be/PlgrzUZ-Y1o)

**tooconfigure единого входа, выполните следующие шаги hello:**

1. В классический портал Azure, на hello hello **облачной платформы SAP HANA** странице интеграции приложения щелкните **настроить единый вход** tooopen hello **Настройка единого входа**диалогового окна.
   
    ![Настройка единого входа](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC778552.png "Настройка единого входа")
2. На hello **предпочитаемый как toosign пользователей на tooSAP облачной платформы HANA** выберите **Microsoft Azure AD Single Sign-On**, а затем нажмите кнопку **Далее**.
   
    ![Настройка единого входа](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790797.png "Настройка единого входа")
3. В другом окне браузера Войдите на toohello облачной платформы SAP HANA панелей в https://account. \<узла Альбомная\>.ondemand.com/cockpit (например: *https://account.hanatrial.ondemand.com/cockpit*).
4. Нажмите кнопку hello **доверия** вкладки.
   
    ![Доверие](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790800.png "Доверие")
5. В раздел управления доверием выполните следующие шаги hello.
   
    ![Получение метаданных](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793930.png "Получение метаданных")
   
   1. Нажмите кнопку hello **локальный поставщик службы** вкладки.
   2. Щелкните toodownload hello файл метаданных облачной платформы SAP HANA, **получить метаданные**.
6. Hello Azure Active классического портала на hello **настроить URL-адрес приложения** страницы, выполните следующие шаги hello и нажмите кнопку **Далее**.
   
    ![Настройка URL-адреса приложения](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790798.png "Настройка URL-адреса приложения")
   
   1. В hello **на URL-адрес входа** textbox hello введите URL-адрес, используемый вашей toosign пользователей в вашей **облачной платформы SAP HANA** приложения. Это URL-адрес защищенного ресурса в приложении облачной платформы SAP HANA для конкретной учетной записи hello. Hello URL-адрес основан на hello следующий шаблон: *https://\<applicationName\>\<accountName\>.\< Альбомная узла\>.ondemand.com/\<путь\_для\_защищенных\_ресурсов\>*  (например: *https://xleavep1941203872trial.hanatrial.ondemand.com/xleave*)
      
     >[!NOTE]
     >Это URL-адрес hello в приложении облачной платформы SAP HANA, требующий hello tooauthenticate пользователя.
     > 

   2. Откройте файл метаданных облачной платформы SAP HANA hello загружены, а затем найдите hello **NS3: assertionconsumerservice** тег.
   3. Скопируйте значение hello hello **расположение** атрибута, а затем вставьте его в hello **URL-адрес SAP HANA облачной платформы ответа** текстового поля.

7. На hello **настроить единый вход в облачную платформу SAP HANA** страницы, toodownload метаданные, нажмите кнопку **загрузить метаданные**, а затем сохраните файл hello на вашем компьютере.
   
    ![Настройка единого входа](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790799.png "Настройка единого входа")
8. На hello панель для облачной платформы SAP HANA, в hello **локальный поставщик службы** выполните следующие шаги hello:
   
    ![Управление доверием](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793931.png "Управление доверием")
   
  1. Нажмите кнопку **Изменить**.
  2. Для параметра **Configuration Type** (Тип конфигурации) выберите значение **Custom** (Настраиваемая).
  3. Как **локальное имя поставщика**, оставьте значение по умолчанию hello.
  4. toogenerate **ключа подписи** и **сертификат подписи** пары ключей, нажмите кнопку **создать пару ключей**.
  5. Для параметра **Principal Propagation** (Распространение субъектов) выберите значение **Disabled** (Отключено).
  6. Для параметра **Force Authentication** (Принудительная аутентификация) выберите значение **Disabled** (Отключено).
  7. Щелкните **Сохранить**.

9. Нажмите кнопку hello **доверенного поставщика удостоверений** , а затем щелкните **добавить доверенного поставщика удостоверений**.
   
    ![Управление доверием](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790802.png "Управление доверием")
   
    >[!NOTE]
    >toomanage hello список доверенных поставщиков удостоверений, необходимо toohave выбранным hello конфигурации пользовательского типа в hello раздел локальный поставщик службы. Для типа конфигурации по умолчанию у вас есть toohello нередактируемые неявное доверие SAP ID Service. Для значения «Нет» параметры доверия отсутствуют.
    > 
    > 

10. Нажмите кнопку hello **Общие** , а затем щелкните **Обзор** tooupload hello скачать файл метаданных.
    
    ![Управление доверием](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793932.png "Управление доверием")
    
    >[!NOTE]
    >После передачи файла метаданных hello hello значения для **-URL**, **URL-адрес единого выхода** и **сертификат подписи** заполняются автоматически.
    > 
    > 

11. Нажмите кнопку hello **атрибуты** вкладки.
12. На hello **атрибуты** выполните следующий шаг hello:
    
    ![Атрибуты](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790804.png "Атрибуты") 
  * Нажмите кнопку **добавить атрибут**, а затем добавьте следующие атрибуты на основе утверждений hello:
       
    | Атрибут утверждения | Атрибут субъекта |
    | --- | --- |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname |firstname |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname |Lastname |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress |email 
   
     >[!NOTE]
     >Конфигурация Hello hello атрибутов зависит от того, как приложения hello в HCP разрабатываются, т. е. какие атрибуты предполагается использовать в hello ответ SAML и какое имя (атрибут субъекта) их доступа к этому атрибуту в коде hello.
     > 
     >  

    1.  Hello **атрибут по умолчанию** в hello экрана — только для примера. Это не требуется toomake hello сценарии работы.   
    2.  Здравствуйте, имена и значения для **атрибут субъекта** показано hello экрана зависят от способа разработки приложения hello. Возможно, приложению требуются другие сопоставления.
     
13. В классический портал Azure, на hello hello **настроить единый вход в облачную платформу SAP HANA** странице диалогового окна, выберите Подтверждение настройки единого входа hello и нажмите кнопку **завершить**.
    
    ![Настройка единого входа](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC796933.png "Настройка единого входа")

###<a name="assertion-based-groups"></a>Группы на основе утверждений
При необходимости для поставщика удостоверений Azure Active Directory можно настроить группы на основе утверждений.

С помощью групп на облачной платформы SAP HANA позволяет назначить toodynamically один или несколько tooone пользователей или несколько ролей в приложениях облачной платформы SAP HANA, определяются значения атрибутов в hello SAML 2.0 утверждение. 

Например, если hello утверждение, содержащее атрибут hello»*контракта = temporary*«, вы можете все затронутые пользователи toobe toohello добавлена группа»*ВРЕМЕННЫЕ*». Группа Hello»*ВРЕМЕННЫЕ*» может содержать одну или несколько ролей из одного или нескольких приложений, развернутых в вашей учетной записи облачной платформы SAP HANA.
 
Используйте группы на основе утверждений, при необходимости назначьте toosimultaneously tooone много пользователей или несколько ролей приложений в вашей учетной записи облачной платформы SAP HANA. Следует tooassign только одного или небольшое число пользователей toospecific ролей рекомендуется назначить их непосредственно в hello»**авторизаций**» вкладки панелей облачной платформы SAP HANA hello.

## <a name="assign-a-role-tooa-user"></a>Назначить пользователя роли tooa
В порядке tooenable toolog пользователей Azure AD в облачную платформу SAP HANA необходимо назначить роли в облачной платформы SAP HANA toothem hello.

**tooassign tooa роли пользователя, выполните следующие шаги hello.**

1. Войдите в tooyour **облачной платформы SAP HANA** панель.
2. Выполните следующие hello.
   
   ![Авторизации](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790805.png "Авторизации")
   
  1. Щелкните **Авторизация**.
  2. Нажмите кнопку hello **пользователей** вкладки.
  3. В hello **пользователя** в текстовое поле адрес электронной почты пользователя типа hello.
  4. Нажмите кнопку **назначить** tooa tooassign hello обязанности.
  5. Щелкните **Сохранить**.

## <a name="assign-users"></a>Назначить пользователей
tootest конфигурацию, необходимо toogrant hello Azure AD пользователей с помощью tooit доступ вашего приложения путем назначения им tooallow.

**Пользователи tooassign tooSAP HANA Cloud Platform выполните hello следующие шаги.**

1. В hello классический портал Azure создайте тестовую учетную запись.
2. На hello **облачной платформы SAP HANA** странице интеграции приложения щелкните **назначить пользователей**.
   
   ![Назначение пользователей](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790806.png "Назначение пользователей")
3. Выберите тестового пользователя, нажмите кнопку **назначить**, а затем нажмите кнопку **Да** tooconfirm назначения.
   
   ![Да](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC767830.png "Да")

Tootest параметры единого входа, откройте панель доступа hello. Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).

