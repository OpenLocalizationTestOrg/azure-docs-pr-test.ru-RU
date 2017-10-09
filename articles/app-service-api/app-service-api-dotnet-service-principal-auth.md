---
title: "aaaService основной проверки подлинности для приложений API в службе приложений Azure | Документы Microsoft"
description: "Узнайте, как tooprotect API приложения в службе приложений Azure для сценариев служба служба."
services: app-service\api
documentationcenter: .net
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: 7ca0bab2-1d29-4d51-b779-dce0edd34f8b
ms.service: app-service-api
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 06/30/2016
ms.author: alkarche
ms.openlocfilehash: 94d9ee11f38293df4a2fd815ef02c59cc6defed4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="service-principal-authentication-for-api-apps-in-azure-app-service"></a>Проверка подлинности с использованием субъекта-службы для приложений API в службе приложений Azure
## <a name="overview"></a>Обзор
В этой статье объясняется способ проверки подлинности службы приложения toouse для *внутренней* доступа к приложениям tooAPI. Внутренний сценарий вас есть приложение API, что требуется toobe использоваться только в коде приложения. Hello рекомендуется tooimplement способом этот сценарий в службе приложений Azure AD toouse tooprotect hello называется приложения API. Вызов приложения hello защищенный API с токен носителя, получаемые из Azure AD, предоставляя удостоверение приложения учетные данные (субъекта-службы). Альтернативные варианты toousing Azure AD, в разделе hello **проверки подлинности службы для службы** раздел hello [обзор проверки подлинности в службе приложений Azure](../app-service/app-service-authentication-overview.md#service-to-service-authentication).

Из этой статьи вы узнаете следующее.

* Как приложения Azure Active Directory (Azure AD) tooprotect API toouse доступ без проверки подлинности.
* Как tooconsume защищенный API приложения из приложения API, веб-приложения или мобильные приложения с помощью учетных данных участника (удостоверение приложения) службы Azure AD. Сведения о том, как tooconsume из логики приложения, в разделе [с помощью настраиваемого API, размещенных в службе приложений с приложениями логики](../logic-apps/logic-apps-custom-hosted-api.md).
* Как toomake, убедитесь, что этот hello защищен приложения API не может вызываться из браузера, в системе работают пользователи.
* Как убедиться, что hello защищенные приложения API toomake только может вызываться с конкретного участника-службы Azure AD.

статья Hello содержит два раздела:

* Hello [как tooconfigure службы основной проверки подлинности в службе приложений Azure](#authconfig) разделе объясняется, как общие tooconfigure проверки подлинности для любого приложения API и защищать приложения API tooconsume hello. В этом разделе, одинаково применимо tooall платформы, поддерживаемые службой приложений, включая .NET, Node.js и Java.
* Начиная с hello [продолжением учебники Приступая к работе .NET hello](#tutorialstart) разделе hello учебник поможет настроить сценарий «внутренний доступ» для образца приложения .NET, запущенные в службе приложений. 

## <a id="authconfig"></a>Как tooconfigure службы основной проверки подлинности в службе приложений Azure
В этом разделе приведены общие инструкции, применимые tooany приложения API. TooDo toohello конкретного действия .NET списка образец приложения, см. слишком[продолжением учебника ряда приложений .NET API hello](#tutorialstart).

1. В hello [портал Azure](https://portal.azure.com/), перейдите toohello **параметры** колонке приложение hello API требуется tooprotect и затем найти hello **функции** и нажмите кнопку **Проверки подлинности и авторизации**.
   
    ![Проверка подлинности и авторизация на портале Azure](./media/app-service-api-dotnet-user-principal-auth/features.png)
2. В hello **проверки подлинности и авторизации** колонка, щелкните **на**.
3. В hello **tootake действия, если запрос не прошел проверку подлинности** раскрывающемся списке выберите **войти с использованием Azure Active Directory** .
4. В разделе **Поставщики проверки подлинности** выберите **Azure Active Directory**.
   
    ![Колонка "Проверка подлинности и авторизация" на портале Azure](./media/app-service-api-dotnet-user-principal-auth/authblade.png)
5. Настройка hello **параметры Azure Active Directory** колонке toocreate новый Azure AD приложения или использование существующего приложения Azure AD, если она уже есть, которые должны toouse.
   
    Во внутренних сценариях обычно участвует приложение API, которое вызывает приложение API. Вы можете использовать отдельные приложения Azure AD для каждого приложения API или только одно приложение Azure AD.
   
    Подробные инструкции по этой колонке см. в разделе [как tooconfigure вход службы приложений toouse приложения Azure Active Directory](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).
6. После завершения работы с колонке конфигурации поставщика проверки подлинности hello, нажмите кнопку **ОК**.
7. В hello **проверки подлинности и авторизации** колонка, щелкните **Сохранить**.
   
    ![Щелкните Сохранить](./media/app-service-api-dotnet-service-principal-auth/authsave.png)

После этого, службы приложений позволяет только запросы от вызывающих объектов в клиенте Azure AD настроена hello. Без проверки подлинности или авторизации кода является обязательным в hello защищенные приложения API. Hello токена носителя передается toohello API приложения вместе с часто используемые утверждений в заголовках HTTP, и можно прочитать эту информацию в toovalidate кода, которые запросов от определенного вызывающего объекта, например субъекта-службы.

Эта функция проверки подлинности может применяться hello одинаково для всех языков этой службы приложения поддерживает, включая .NET, Node.js и Java. 

#### <a name="how-tooconsume-hello-protected-api-app"></a>Защищать приложения API tooconsume hello
вызывающий объект Hello необходимо предоставить токена носителя Azure AD с вызовами API. tooget токен носителя, с помощью учетных данных участника службы, вызывающий объект hello использует библиотеку аутентификации Active Directory (ADAL для [.NET](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory), [Node.js](https://github.com/AzureAD/azure-activedirectory-library-for-nodejs), или [Java](https://github.com/AzureAD/azure-activedirectory-library-for-java)). tooget маркер hello код, который вызывает ADAL предоставляет hello tooADAL следующую информацию:

* Hello имя вашего клиента Azure AD.
* Hello клиента идентификатор и секрет клиента (ключ приложения) приложения hello Azure AD, связанные с hello вызывающего объекта.
* Идентификатор клиента приложения Azure AD, связанного с hello hello Hello защищенного приложения API. (Если используется только одно приложение Azure AD, это является hello же идентификатор клиента как Здравствуйте, один для вызывающего объекта hello.)

Эти значения доступны на страницах hello Azure AD hello [классический портал Azure](https://manage.windowsazure.com/).

После получил токен hello hello вызывающего объекта содержит это HTTP-запросов в заголовке авторизации hello.  Службы приложений проверяет токен hello и позволяет приложения API, защищенный hello tooreach hello запросов.

#### <a name="how-tooprotect-hello-api-app-from-access-by-users-in-hello-same-tenant"></a>Как приложение hello API tooprotect от доступа пользователей в hello же клиента
Токены носителя для пользователей в одном клиенте считаются допустимыми для hello hello защищенного приложения API.  Если требуется, можно вызвать только субъект-служба tooensure Здравствуйте защищенного приложения API, добавьте код в hello защищенные API приложения toovalidate hello после утверждения из токена hello:

* `appid`должно быть hello идентификатор клиента приложения Azure AD hello, связанный с вызывающим объектом hello. 
* `oid`(`objectidentifier`) должен быть идентификатор участника службы hello hello вызывающего метода. 

Служба приложения также предоставляет hello `objectidentifier` утверждений в заголовке X-MS-CLIENT-УЧАСТНИК-ID hello.

### <a name="how-tooprotect-hello-api-app-from-browser-access"></a>Как tooprotect hello приложение API из доступ в браузере
Если не проверить утверждения в код в приложение hello защищенный API и использовать отдельный приложения Azure AD для hello защищенного приложения API убедитесь в том, что hello, URL-адрес ответа приложения Azure AD не hello так же, как hello базовый URL-адрес приложения API. Если hello URL-адрес ответа указывает непосредственно toohello защищенные приложения API, пользователь в клиенте hello же Azure AD может Обзор toohello приложения API, войти в систему и успешного вызова hello API.

## <a id="tutorialstart"></a>Продолжение ряда учебного приложения API .NET hello
Если вы следуете hello Node.js или Java учебника рядов для приложений API, пропустите toohello [дальнейшие действия](#next-steps) раздела. 

Hello оставшейся части этой статьи продолжает учебник ряда приложений .NET API hello и предполагается, что вы выполнили hello [учебника проверки подлинности пользователя](app-service-api-dotnet-user-principal-auth.md) и иметь пример приложения hello, запущенных в Azure с проверкой подлинности пользователя включена.

## <a name="set-up-authentication-in-azure"></a>Настройка проверки подлинности в Azure
В этом разделе Настройка приложения службы, таким образом, что hello только HTTP-запросы, она позволяет tooreach hello данных уровня API приложения будут hello те, которые имеют допустимые Azure AD токены носителя. 

В следующем разделе hello настройте tooAzure приложения учетных данных для среднего уровня API приложения hello toosend AD, вернемся токен носителя и отправить hello носителя токена toohello данных уровня API приложение. Этот процесс показан на диаграмме hello.

![Схема проверки подлинности службы](./media/app-service-api-dotnet-service-principal-auth/appdiagram.png)

Если возникли проблемы при следующих инструкций учебника hello. в разделе hello [Устранение неполадок](#troubleshooting) раздел в конце hello hello учебника. 

1. В hello [портал Azure](https://portal.azure.com/), перейдите toohello **параметры** колонке hello API приложения, созданного для приложения API hello ToDoListDataAPI (уровень данных) и нажмите кнопку **параметры**.
2. В hello **параметры** колонки, найти hello **функции** , а затем выберите **проверки подлинности и авторизации**.
   
    ![Проверка подлинности и авторизация на портале Azure](./media/app-service-api-dotnet-user-principal-auth/features.png)
3. В hello **проверки подлинности и авторизации** колонка, щелкните **на**.
4. В hello **tootake действия, если запрос не прошел проверку подлинности** раскрывающемся списке выберите **войти с использованием Azure Active Directory**.
   
    Это параметр hello, вызывающая tooensure приложения службы, проверку подлинности только приложение API hello reach запросов. Для запросов, имеющих маркеров допустимым носителя, службы приложений, передает токены hello вдоль toohello API приложения и заполняет заголовки HTTP с toomake часто используемые утверждений этих сведений легко доступны tooyour кода.
5. В разделе **Поставщики проверки подлинности** щелкните **Azure Active Directory**.
   
    ![Колонка "Проверка подлинности и авторизация" на портале Azure](./media/app-service-api-dotnet-user-principal-auth/authblade.png)
6. В hello **параметры Azure Active Directory** колонка, щелкните **Express**.
   
    С hello **Express** параметр Azure можно автоматически создать приложение AAD в Azure AD [клиента](https://msdn.microsoft.com/en-us/library/azure/jj573650.aspx#BKMK_WhatIsAnAzureADTenant). 
   
    У вас нет toocreate клиента, так как каждая Azure учетная запись автоматически имеет один.
7. В разделе **Режим управления** щелкните **Создать новое приложение AD**, если этот параметр еще не выбран.
   
    портал Hello подключается hello **Создание приложения** поля ввода и значение по умолчанию. По умолчанию с именем hello приложения Azure AD Здравствуйте таким же, как приложение hello API. Вы можете ввести другое имя.
   
    ![параметры Azure AD](./media/app-service-api-dotnet-service-principal-auth/aadsettings.png)
   
    **Примечание**: в качестве альтернативы можно использовать один Azure AD приложения для обоих hello вызывающего приложения API и hello защищенные приложения API. Если выбран этот вариант не потребуются hello **создать новое приложение AD** параметр здесь, так как приложения Azure AD уже созданы ранее в учебнике проверки подлинности пользователя hello. В этом учебнике будет использоваться разделения приложения Azure AD для вызова API приложения и hello hello защищенного приложения API.
8. Запишите значение hello в hello **Создание приложения** поле ввода; позволяет просмотреть в этом приложении AAD в hello классический портал Azure позже.
9. Нажмите кнопку **ОК**.
10. В hello **проверки подлинности и авторизации** колонка, щелкните **Сохранить**.
    
    ![Щелкните Сохранить](./media/app-service-api-dotnet-service-principal-auth/saveauth.png)
    
    Приложение службы создается приложение Azure Active Directory с **URL-адрес входа** и **URL-адрес ответа** автоматически устанавливается toohello URL-адрес приложения API. Последнее значение Hello позволяет пользователям в вашей toolog клиента AAD в и приложения API hello доступа.

### <a name="verify-that-hello-api-app-is-protected"></a>Убедитесь, что приложение hello API защищен
1. В браузере перейдите toohello URL-адрес приложения hello API: в hello **приложения API** колонки в hello портал Azure, щелкните ссылку hello под **URL-адрес**. 
   
    Перенаправленный tooa экран входа являются, так как не прошедшие проверку подлинности запросы запрещены приложение API tooreach hello. 
   
    Если браузер перехода toohello Swagger пользовательского интерфейса, браузер уже вошел — в этом случае откройте окно InPrivate или анонимный и перейдите toohello Swagger URL-адрес пользовательского интерфейса.
2. Войдите с помощью учетных данных, используемых в клиенте AAD.
   
   При входе странице «успешно создан» hello появится в браузере hello.

## <a name="configure-hello-todolistapi-project-tooacquire-and-send-hello-azure-ad-token"></a>Настройка проекта tooacquire hello ToDoListAPI и отправлять hello маркера Azure AD
В этом разделе hello следующие задания:

* Добавьте код в приложении API hello среднего уровня, которое использует tooacquire учетные данные приложения Azure AD токен и отправьте HTTP-запросов приложения API уровня toohello данных.
* Hello учетные данные, которые необходимо получите из Azure AD.
* Введите учетные данные hello в службе приложений Azure параметры среды выполнения в hello среднего уровня приложения API. 

### <a name="configure-hello-todolistapi-project-tooacquire-and-send-hello-azure-ad-token"></a>Настройка проекта tooacquire hello ToDoListAPI и отправлять hello маркера Azure AD
Внесите следующие изменения в проекте ToDoListAPI hello в Visual Studio hello.

1. Раскомментируйте весь код hello в hello *ServicePrincipal.cs* файла.
   
    Это hello код, который использует ADAL для токена носителя .NET tooacquire hello Azure AD.  Она использует несколько значений конфигурации, которые можно задать в среде выполнения Azure hello позже. Ниже приведен код hello. 
   
        public static class ServicePrincipal
        {
            static string authority = ConfigurationManager.AppSettings["ida:Authority"];
            static string clientId = ConfigurationManager.AppSettings["ida:ClientId"];
            static string clientSecret = ConfigurationManager.AppSettings["ida:ClientSecret"];
            static string resource = ConfigurationManager.AppSettings["ida:Resource"];
   
            public static AuthenticationResult GetS2SAccessTokenForProdMSA()
            {
                return GetS2SAccessToken(authority, resource, clientId, clientSecret);
            }
   
            static AuthenticationResult GetS2SAccessToken(string authority, string resource, string clientId, string clientSecret)
            {
                var clientCredential = new ClientCredential(clientId, clientSecret);
                AuthenticationContext context = new AuthenticationContext(authority, false);
                AuthenticationResult authenticationResult = context.AcquireToken(
                    resource,
                    clientCredential);
                return authenticationResult;
            }
        }
   
    **Примечание:** этого примера кода требуются hello ADAL для пакета .NET NuGet (Microsoft.IdentityModel.Clients.ActiveDirectory), который еще не установлен в проекте hello. Если этот проект был создан с нуля, будет иметь tooinstall этого пакета. Этот пакет не устанавливается автоматически с шаблона новый проект приложения hello API.
2. В *контроллеров или ToDoListController*, раскомментируйте код hello в hello `NewDataAPIClient` метод, который добавляет запросы маркера tooHTTP hello в заголовке авторизации hello.
   
        client.HttpClient.DefaultRequestHeaders.Authorization =
            new AuthenticationHeaderValue("Bearer", ServicePrincipal.GetS2SAccessTokenForProdMSA().AccessToken);
3. Разверните проект ToDoListAPI hello. (Щелкните правой кнопкой мыши проект hello, а затем нажмите кнопку **публикации > публикации**.)
   
    Visual Studio развертывает проект hello и открывает базовый URL-адрес браузера toohello веб-приложения. При этом будут отображены ошибка 403 страницы, которая является нормальным попытки toogo tooa веб-API базовый URL-адрес в браузере.
4. Hello закрыть браузер.

### <a name="get-azure-ad-configuration-values"></a>Получение значений конфигурации Azure AD
1. В hello [классический портал Azure](https://manage.windowsazure.com/), перейдите в слишком**Azure Active Directory**.
2. На hello **каталога** щелкните клиенте AAD.
3. Нажмите кнопку **приложений > приложений, которыми владеет Моя компания**, а затем нажмите кнопку флажок hello.
4. В списке hello приложений щелкните имя hello hello, Azure создается при включении проверки подлинности для приложения API hello ToDoListDataAPI (уровень данных).
5. Нажмите кнопку hello **Настройка** вкладки.
6. Копировать hello **идентификатор клиента** значение и сохраните его где-то ее можно загрузить из более поздней версии. 
7. На классический портал Azure hello вернитесь toohello список **приложений, которыми владеет Моя компания**, а затем выберите приложение hello AAD, созданный для приложения ToDoListAPI API hello среднего уровня (hello один, созданный в предыдущем учебнике hello не Здравствуйте, где создается в этом учебнике).
8. Нажмите кнопку hello **Настройка** вкладки.
9. Копировать hello **идентификатор клиента** значение и сохраните его где-то ее можно загрузить из более поздней версии.
10. В разделе **ключей**выберите **1 год** из hello **выберите длительность** раскрывающегося списка.
11. Щелкните **Сохранить**.
    
     ![Создать ключ приложения](./media/app-service-api-dotnet-service-principal-auth/genkey.png)
12. Скопируйте значение ключа hello и сохраните где-то, которые можно получить его из более поздней версии.
    
     ![Скопировать новый ключ приложения](./media/app-service-api-dotnet-service-principal-auth/genkeycopy.png)

### <a name="configure-azure-ad-settings-in-hello-middle-tier-api-apps-runtime-environment"></a>Настройте параметры Azure AD в приложение hello среднего уровня API среды выполнения
1. Go toohello [портал Azure](https://portal.azure.com/)и перейдите toohello **приложения API** колонке приложение hello API, которая содержит проект hello TodoListAPI (средний уровень).
2. Щелкните элементы **Параметры > Параметры приложения**.
3. В hello **параметры приложения** добавьте следующие hello ключам и значениям:
   
   | **Ключ** | ida:Authority |
   | --- | --- |
   | **Значение** |https://login.microsoftonline.com/{имя клиента Azure AD} |
   | **Пример** |https://login.microsoftonline.com/contoso.onmicrosoft.com |
   
   | **Ключ** | ida:ClientId |
   | --- | --- |
   | **Значение** |Идентификатор клиента для вызова приложения (средний уровень - ToDoListAPI) hello |
   | **Пример** |960adec2-b74a-484a-960adec2-b74a-484a |
   
   | **Ключ** | ida:ClientSecret |
   | --- | --- |
   | **Значение** |Ключ приложения hello вызов приложения (средний уровень - ToDoListAPI) |
   | **Пример** |e65e8fc9-5f6b-48e8-e65e8fc9-5f6b-48e8 |
   
   | **Ключ** | ida:Resource |
   | --- | --- |
   | **Значение** |Идентификатор клиента приложения вызывается hello (уровень данных — ToDoListDataAPI) |
   | **Пример** |e65e8fc9-5f6b-48e8-e65e8fc9-5f6b-48e8 |
   
    **Примечание**: для `ida:Resource`, убедитесь, что используют вызывается приложения hello **идентификатор клиента** и не его **URI идентификатора приложения**.
   
    `ida:ClientId`и `ida:Resource` отличаются значения для этого учебника, так как вы используете разделения applicaations Azure AD для hello средний уровень и уровень данных. Если вы использовали один приложения Azure AD для вызова API приложения и hello hello защищенные приложения API, может использовать одинаковое значение в обоих hello `ida:ClientId` и `ida:Resource`.
   
    Hello код использует ConfigurationManager tooget эти значения, поэтому они могут храниться в файле Web.config hello проекта или в среде выполнения Azure hello. Пока приложение ASP.NET работает в службе приложений Azure, параметры среды автоматически переопределяют параметры в файле Web.config. Параметры среды являются обычно [более безопасный способ toostore конфиденциальной информации по сравнению файл Web.config tooa](http://www.asp.net/identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure).
4. Щелкните **Сохранить**.
   
    ![Щелкните Сохранить](./media/app-service-api-dotnet-service-principal-auth/appsettings.png)

### <a name="test-hello-application"></a>Тестирование приложения hello
1. В браузере перейдите toohello URL-адреса HTTPS hello AngularJS внешнего интерфейса веб-приложения.
2. Нажмите кнопку hello **tooDo списка** вкладку и войти в систему с учетными данными пользователя в клиенте Azure AD. 
3. Добавьте tooverify элементов задачи, работа приложения hello.
   
    ![Страница списка tooDo](./media/app-service-api-dotnet-service-principal-auth/mvchome.png)
   
    Если приложение hello не работает должным образом, повторно проверьте все параметры hello, введенное на портал Azure hello. Если все параметры hello отображаются правильные toobe, см. раздел hello [Устранение неполадок](#troubleshooting) далее в этом учебнике.

## <a name="protect-hello-api-app-from-browser-access"></a>Приложение hello API предотвратить доступ в браузере
В этом учебнике вы создали отдельный приложения Azure AD для приложения hello API ToDoListDataAPI (уровень данных). Как вы уже видели, когда службы приложений создает приложение AAD настраивает hello AAD приложения, что позволяет пользователю toogo toohello API приложения URL-адрес в браузере и войдите на. Это означает, что возможно для конечного пользователя в клиенте Azure AD не только участника-службы, tooaccess hello API. 

Если требуется доступ через браузер tooprevent без написания кода в hello защищенные приложения API, можно изменить hello **URL-адрес ответа** в AAD приложения hello, чтобы оно отличается от приложения hello API базовый URL-адрес. 

### <a name="disable-browser-access"></a>Отключение доступа через браузер
1. В классическом портале hello **Настройка** для hello AAD приложений, созданных для hello TodoListService, измените значение hello в hello **URL-адрес ответа** таким образом, чтобы он является допустимым URL-адресом, но не hello API приложения URL-АДРЕС.
2. Щелкните **Сохранить**.

### <a name="verify-browser-access-no-longer-works"></a>Проверка отсутствия доступа через браузер
Ранее вы проверили, можно перейти URL-адрес приложения API toohello из браузера войдя в систему с учетными данными для отдельного пользователя. В этом разделе вы убедитесь, что это больше нельзя сделать. 

1. В новом окне браузера перейдите снова toohello URL-адрес приложения hello API.
2. Если вход запрос toodo таким образом.
3. Имя входа выполняется успешно, но ведет tooan страницы ошибки.
   
    Вы настроили приложение hello AAD, чтобы пользователи в клиенте AAD hello не может войти и получить доступ к hello API из браузера. Можно по-прежнему получить доступ к API приложение hello с помощью токена участника службы, это можно проверить URL-адрес веб-приложения toohello и добавлять дополнительные элементы задачи.

## <a name="restrict-access-tooa-particular-service-principal"></a>Ограничить участник определенной службы доступа к tooa
В данный момент, любой вызывающий объект, который может получить маркер для пользователя или субъекта-службы в клиенте Azure AD может вызывать приложение hello API TodoListDataAPI (уровень данных). Может потребоваться toomake том, что приложение hello уровня данных API-Интерфейс только принимает вызовы из приложения API hello TodoListAPI (средний уровень) и только с участником определенной службы. 

Эти ограничения можно добавлять путем добавления кода hello toovalidate `appid` и `objectidentifier` утверждений от входящих вызовов.

В этом учебнике поместите hello код, который проверяет идентификатор приложения и идентификатор участника службы непосредственно в ваши действия контроллера.  Существуют варианты toouse пользовательского `Authorize` атрибута или toodo проверки в последовательностях запуска (например по промежуточного слоя OWIN). Пример hello в последнем разделе [в этом образце приложения](https://github.com/mohitsriv/EasyAuthMultiTierSample/blob/master/MyDashDataAPI/Startup.cs). 

Сделайте следующие изменения toohello TodoListDataAPI проекта hello.

1. Откройте hello *Controllers/TodoListController.cs* файла.
2. Раскомментируйте строки hello заданных `trustedCallerClientId` и `trustedCallerServicePrincipalId`.
   
        private static string trustedCallerClientId = ConfigurationManager.AppSettings["todo:TrustedCallerClientId"];
        private static string trustedCallerServicePrincipalId = ConfigurationManager.AppSettings["todo:TrustedCallerServicePrincipalId"];
3. Раскомментируйте hello код в метод CheckCallerId hello. Этот метод вызывается в начале каждого метода действия в контроллере hello hello. 
   
        private static void CheckCallerId()
        {
            string currentCallerClientId = ClaimsPrincipal.Current.FindFirst("appid").Value;
            string currentCallerServicePrincipalId = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier").Value;
            if (currentCallerClientId != trustedCallerClientId || currentCallerServicePrincipalId != trustedCallerServicePrincipalId)
            {
                throw new HttpResponseException(new HttpResponseMessage { StatusCode = HttpStatusCode.Unauthorized, ReasonPhrase = "hello appID or service principal ID is not hello expected value." });
            }
        }
4. Повторное развертывание hello ToDoListDataAPI проекта tooAzure службы приложений.
5. В браузере перейдите на URL-адрес внешнего интерфейса веб-toohello AngularJS приложения HTTPS, а на главной странице приветствия нажмите кнопку hello **tooDo списка** вкладки.
   
    приложение Hello не работает из-за ошибки при выполнении вызовов завершить toohello обратно. Hello новый код проверки, фактический appid и objectidentifier, но он еще не определен toocheck hello правильные значения для них. браузер Hello консоль средств разработчика сообщает, hello сервер вернул ошибку HTTP 401.
   
    ![Ошибка в консоли инструментов для разработчиков](./media/app-service-api-dotnet-service-principal-auth/webapperror.png)
   
    В hello следующие шаги настройки hello ожидаемые значения.
6. С помощью Azure AD PowerShell, получите значение hello hello службы участника для приложения Azure AD, созданный для проекта TodoListWebApp hello hello.
   
    а. Дополнительные сведения о tooinstall Azure PowerShell и tooyour подписки, обратитесь к подразделу [с помощью Azure PowerShell с помощью диспетчера ресурсов Azure](../powershell-azure-resource-manager.md).
   
    b. список участников, tooget выполнение hello `Login-AzureRmAccount` команды и затем hello `Get-AzureRmADServicePrincipal` команды.
   
    c. Найдите hello objectid hello участника-службы приложения hello TodoListAPI и сохраните его в расположение, которое можно скопировать из более поздней версии.
7. В hello портал Azure перейдите toohello колонка приложения API для приложения hello API, который был развернут проект ToDoListDataAPI hello.
8. Щелкните элементы **Параметры > Параметры приложения**.
9. В hello **параметры приложения** добавьте следующие hello ключам и значениям:
   
   | **Ключ** | todo:TrustedCallerServicePrincipalId |
   | --- | --- |
   | **Значение** |Идентификатор субъекта-службы вызывающего приложения |
   | **Пример** |4f4a94a4-6f0d-4072-4f4a94a4-6f0d-4072 |
   
   | **Ключ** | todo:TrustedCallerClientId |
   | --- | --- |
   | **Значение** |Идентификатор клиента для вызова приложения - скопированы из приложения hello TodoListAPI Azure AD |
   | **Пример** |960adec2-b74a-484a-960adec2-b74a-484a |
10. Щелкните **Сохранить**.
    
     ![Щелкните Сохранить](./media/app-service-api-dotnet-service-principal-auth/trustedcaller.png)
11. В браузере URL-адрес веб-приложения toohello возврата, а на главной странице приветствия нажмите кнопку hello **tooDo списка** вкладки.
    
     Это приложение hello времени работает как ожидается, поскольку приложение hello доверенного вызывающего объекта, идентификатор и идентификатор участника службы, hello ожидаемые значения.
    
     ![Страница списка tooDo](./media/app-service-api-dotnet-service-principal-auth/mvchome.png)

## <a name="building-hello-projects-from-scratch"></a>Построение проектов hello с нуля
Hello двух веб-API проекты были созданы с помощью hello **приложения API Azure** проекта шаблона и замена контроллера значения по умолчанию hello с ToDoList. Для получения токенов основной службы Azure AD в проекте ToDoListAPI hello, hello [Active Directory Authentication библиотеки (ADAL) для .NET](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) был установлен пакет NuGet.

Слишком сведения о создании одностраничного приложения AngularJS с серверную часть веб-API как ToDoListAngular, см. в разделе [руки на лаборатории: построение одной страницы приложений (SPA) с веб-API ASP.NET и Angular.js](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs). Сведения о том, как tooadd код проверки подлинности Azure AD, в разделе [защита AngularJS одной страницы приложений с Azure AD](../active-directory/active-directory-devquickstarts-angular.md).

## <a name="troubleshooting"></a>Устранение неполадок
[!INCLUDE [troubleshooting](../../includes/app-service-api-auth-troubleshooting.md)]

* Убедитесь, что вы не путаете ToDoListAPI (средний уровень) и ToDoListDataAPI (уровень данных). Например, в этом учебнике вы добавить приложения API уровня данных toohello проверки подлинности, **, но ключ приложения hello должны поступать из приложения Azure AD, созданный для приложения среднего уровня API hello hello**.

## <a name="next-steps"></a>Дальнейшие действия
Это последний учебник hello в hello ряда приложений API. 

Дополнительные сведения о Azure Active Directory см. следующие ресурсы hello.

* [Руководство разработчика по Azure Active Directory](http://aka.ms/aaddev)
* [Сценарии проверки подлинности в Azure AD](http://aka.ms/aadscenarios)
* [Azure Samples (Примеры для Azure)](http://aka.ms/aadsamples)
  
    Hello [WebApp-WebAPI-OAuth2-AppIdentity-DotNet](http://github.com/AzureADSamples/WebApp-WebAPI-OAuth2-AppIdentity-DotNet) пример аналогичен toowhat отображается в этом учебнике, но без использования проверки подлинности службы приложений.

Сведения о других способах toodeploy Visual Studio проектов tooAPI приложений с помощью Visual Studio или [автоматизации развертывания](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery) из [система управления версиями](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control), в разделе [как toodeploy Приложение службы приложений Azure](../app-service-web/web-sites-deploy.md).

