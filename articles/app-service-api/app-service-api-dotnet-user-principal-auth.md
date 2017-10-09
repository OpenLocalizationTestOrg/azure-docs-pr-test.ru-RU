---
title: "aaaUser проверки подлинности для приложений API в службе приложений Azure | Документы Microsoft"
description: "Узнайте, как tooprotect приложения API в службе приложений Azure, разрешив доступ к tooauthenticated только пользователей."
services: app-service\api
documentationcenter: .net
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: 3896760d-46ff-4b67-b98a-edd233f24758
ms.service: app-service-api
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 06/30/2016
ms.author: alkarche
ms.openlocfilehash: 4702fc77fcfe736405e22b033c35d22ae3c5a300
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="user-authentication-for-api-apps-in-azure-app-service"></a>Проверка подлинности пользователя для приложений API в службе приложений Azure
## <a name="overview"></a>Обзор
В этой статье показано, как tooprotect приложения Azure API, так что только прошедшие проверку пользователи могут вызвать его. Hello статьи предполагается, что вы прочитали hello [обзор проверки подлинности в службе приложений Azure](../app-service/app-service-authentication-overview.md).

Вы узнаете:

* Как tooconfigure поставщик проверки подлинности со сведениями для Azure Active Directory (Azure AD).
* Как hello tooconsume защищенного приложения API с помощью [Active Directory Authentication библиотеки (ADAL) для JavaScript](https://github.com/AzureAD/azure-activedirectory-library-for-js).

статья Hello содержит два раздела:

* Hello [как tooconfigure проверки подлинности пользователя в службе приложений Azure](#authconfig) разделе объясняется, как общие tooconfigure проверки подлинности пользователя для любого приложения API и tooall платформы, поддерживаемые службой приложений, включая .NET, в равной степени относится Node.js и Java.
* Начиная с hello [продолжением учебники по .NET API приложения hello](#tutorialstart) статьи, hello статьи руководства по настройке образца приложения с .NET резервное интерфейса и интерфейса AngularJS, чтобы он использовал Azure Active Directory для пользователя Проверка подлинности. 

## <a id="authconfig"></a>Способ проверки подлинности пользователя tooconfigure в службе приложений Azure
В этом разделе приведены общие инструкции, применимые tooany приложения API. TooDo toohello конкретного действия .NET списка образец приложения, см. слишком[продолжением учебники Приступая к работе hello .NET](#tutorialstart).

1. В hello [портал Azure](https://portal.azure.com/), перейдите toohello **параметры** колонке приложение hello API, которые должны tooprotect поиска hello **функции** , а затем выберите  **Проверка подлинности и авторизации**.
   
    ![Проверка подлинности и авторизация на портале Azure](./media/app-service-api-dotnet-user-principal-auth/features.png)
2. В hello **проверки подлинности и авторизации** колонка, щелкните **на**.
3. Выберите один из параметров hello hello **tootake действия, если запрос не прошел проверку подлинности** раскрывающегося списка.
   
   * Если требуется только проверенные на подлинность вызовы tooreach приложение API, выберите один из hello **входа в систему...**  параметры. Этот параметр позволяет вам tooprotect API приложение hello без написания кода, работающего в его.
   * Если требуется, чтобы все вызовы API приложения tooreach, выберите **разрешить запрос (никаких действий)**. Можно использовать этот выбор параметра toodirect не прошедшие проверку подлинности вызывающим объектам tooa поставщиков проверки подлинности. В этом случае у вас есть авторизации toohandle toowrite кода.
     
     Дополнительные сведения см. в статье [Проверка подлинности и авторизация для приложений API в службе приложений Azure](app-service-api-authentication.md#multiple-protection-options).
4. Выберите одну или несколько hello **поставщики проверки подлинности**.
   
    изображение Hello варианты выбора, требующих все вызывающие объекты toobe, проверку подлинности с помощью Azure AD.
   
    ![Колонка "Проверка подлинности и авторизация" на портале Azure](./media/app-service-api-dotnet-user-principal-auth/authblade.png)
   
    При выборе поставщика проверки подлинности портал hello отображает колонке конфигурации для данного поставщика. 
   
    Подробные инструкции, в которых объясняется, как tooconfigure hello колонках конфигурации поставщика проверки подлинности см. в разделе [как tooconfigure вход службы приложений toouse приложения Azure Active Directory](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md). (ссылка hello указывает tooan статьи об Azure AD, но самой статье hello содержит вкладки, которые связываются tooarticles для hello других поставщиков проверки подлинности).
5. После завершения работы с колонке конфигурации поставщика проверки подлинности hello, нажмите кнопку **ОК**.
6. В hello **проверки подлинности и авторизации** колонка, щелкните **Сохранить**.

После этого, приложение службы проверяет подлинность все вызовы API, прежде чем они достигнут приложения hello API. Работа служб проверки подлинности Hello hello одинаково для всех языков, поддерживаемых службы приложений, включая .NET, Node.js и Java. 

toomake проверкой подлинности вызовов API, вызывающий объект hello включает поставщика проверки подлинности hello токена носителя OAuth 2.0 в hello заголовок авторизации HTTP-запросов. токен Hello можно получить с помощью пакета SDK поставщика проверки подлинности hello.

## <a id="tutorialstart"></a>Продолжение учебники по .NET API приложения hello
Если вы следуете hello Node.js или Java учебники для приложений API, пропустить следующей статье toohello [основной проверки подлинности службы для приложений API](app-service-api-dotnet-service-principal-auth.md). 

Если следуете учебника ряда hello .NET для приложений API и уже развернули пример приложения hello, как указано в hello [первый](app-service-api-dotnet-get-started.md) и [второй](app-service-api-cors-consume-javascript.md) учебники, пропустить toohello [Настройка Проверка подлинности в службе приложений и Azure AD](#azureauth) раздела.

Следует toofollow этого учебника минуя hello первого и второго учебники hello следующие шаги, в которых объясняется, как tooget запущена с помощью образца приложения hello toodeploy автоматизированного процесса.

> [!NOTE]
> Hello следующее приступить toohello же начальной точки, как если бы hello первые два учебника, за одним исключением: Visual Studio уже могут не узнать, какие веб-приложения или приложения API, который разворачивается каждого проекта. Это означает, что вы не будете иметь точные инструкции этого учебника, в которых объясняется, как toodeploy toohello вправо цели. Если вы не освоите поняли как шаги развертывания hello toodo самостоятельно, это лучше toofollow hello учебника ряд hello [первом учебнике](app-service-api-dotnet-get-started.md) чем toostart с этим автоматизировать процесс развертывания.
> 
> 

1. Убедитесь, что есть все необходимые компоненты hello, перечисленные в hello [первом учебнике](app-service-api-dotnet-get-started.md). В добавление toohello предварительные условия эти учебники проверки подлинности предполагается работали с веб-приложений служб приложения и приложения API в Visual Studio и hello портал Azure.
2. Щелкните hello **развертывание tooAzure** кнопку в hello [файл readme репозитория образец списка tooDo](https://github.com/azure-samples/app-service-api-dotnet-todo-list/blob/master/readme.md) toodeploy hello API приложения и hello веб-приложения. Запишите hello группы ресурсов Azure, который создается, как можно использовать этот более поздней версии toolook веб-приложения и имена приложений API.
3. Загрузка или клон hello [репозитории примеров список tooDo](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list) tooget hello код, который вы будете работать с локально в Visual Studio.

## <a id="azureauth"></a> Настройка проверки подлинности в службе приложений и Azure AD
Теперь у вас есть приложение hello, запущенные в службе приложений Azure, не требуя проверки подлинности пользователей. В этом разделе добавьте проверки подлинности, выполнив следующие задачи hello:

* Настройка проверки подлинности Azure Active Directory (Azure AD) toorequire службы приложений для вызова приложения среднего уровня API hello.
* Создадим приложение Azure AD.
* После входа в систему toohello AngularJS внешнего интерфейса настройте токена носителя hello toosend приложения hello Azure AD. 

Если возникли проблемы при следующих инструкций учебника hello. в разделе hello [Устранение неполадок](#troubleshooting) раздел в конце hello hello учебника. 

### <a name="configure-authentication-for-hello-middle-tier-api-app"></a>Настройка проверки подлинности для hello среднего уровня приложения API
1. В hello [портал Azure](https://portal.azure.com/), перейдите toohello **параметры** колонке приложение hello API, созданный для проекта ToDoListAPI hello, найти hello **функции** раздела, а затем Нажмите кнопку **проверки подлинности и авторизации**.
   
    ![Проверка подлинности и авторизация на портале Azure](./media/app-service-api-dotnet-user-principal-auth/features.png)
2. В hello **проверки подлинности и авторизации** колонка, щелкните **на**.
3. В hello **tootake действия, если запрос не прошел проверку подлинности** раскрывающемся списке выберите **войти с использованием Azure Active Directory**.
   
    Этот параметр гарантирует, что запросы не unauathenticated достигнет API приложение hello. 
4. В разделе **Поставщики проверки подлинности** щелкните **Azure Active Directory**.
   
    ![Колонка "Проверка подлинности и авторизация" на портале Azure](./media/app-service-api-dotnet-user-principal-auth/authblade.png)
5. В hello **параметры Azure Active Directory** колонка, щелкните **Express**
   
    ![Параметр "Экспресс" для проверки подлинности и авторизации на портале Azure](./media/app-service-api-dotnet-user-principal-auth/aadsettings.png)
   
    С hello **Express** , службы приложений можно автоматически создавать приложения Azure AD в Azure AD [клиента](https://msdn.microsoft.com/en-us/library/azure/jj573650.aspx#BKMK_WhatIsAnAzureADTenant). 
   
    У вас нет toocreate клиента, так как каждая Azure учетная запись автоматически имеет один.
6. В разделе **режим управления**, нажмите кнопку **создать новое приложение AD** , если он еще не выбран и обратите внимание, значение hello в hello **Создание приложения** текстовое поле; будет искать этот AAD приложение в hello Azure классический портал позже.
   
    ![Параметры Azure AD на портале Azure](./media/app-service-api-dotnet-user-principal-auth/aadsettings2.png)
   
    Azure автоматически создаст приложения Azure AD с указанным именем hello в клиенте Azure AD. По умолчанию с именем hello приложения Azure AD Здравствуйте таким же, как приложение hello API. Вы можете ввести другое имя.
7. Нажмите кнопку **ОК**.
8. В hello **проверки подлинности и авторизации** колонка, щелкните **Сохранить**.
   
    ![Щелкните Сохранить](./media/app-service-api-dotnet-user-principal-auth/authsave.png)

Теперь только пользователи из вашего клиента Azure AD можно вызвать API приложение hello.

### <a name="optional-test-hello-api-app"></a>Необязательно: Протестировать приложение hello API
1. В браузере перейдите toohello URL-адрес приложения hello API: в hello **приложения API** колонки в hello портал Azure, щелкните ссылку hello под **URL-адрес**.  
   
    Перенаправленный tooa экран входа являются, так как не прошедшие проверку подлинности запросы запрещены приложение API tooreach hello.
   
    Если браузер переходит в «успешно создан» toohello страницу, браузер hello уже вошли--в этом случае откройте окно InPrivate или анонимный и перейти на URL-адрес приложения toohello API.
2. Войдите с помощью учетных данных, используемых в клиенте Azure AD.
   
    При входе странице «успешно создан» hello появится в браузере hello.
3. Hello закрыть браузер.

### <a name="configure-hello-azure-ad-application"></a>Настройка приложения hello Azure AD
При настройке проверки подлинности в Azure AD служба приложений автоматически создала приложение Azure AD. По умолчанию hello новый Azure AD приложению не настроенный tooprovide hello носителя токена toohello API приложения URL-адрес. В этом разделе Настройка hello Azure AD tooprovide hello носителя токена toohello AngularJS интерфейсом приложения вместо непосредственно toohello приложения среднего уровня API. Hello AngularJS переднего плана будет отправлять токен toohello API приложение hello, при вызове API приложение hello.

> [!NOTE]
> процесс hello tookeep как можно более простыми, в этом учебнике используется один Azure AD приложение hello переднего плана и приложение среднего уровня API hello. Другой вариант — toouse два приложения Azure AD. В этом случае имеется toogive hello переднего плана в Azure AD приложения разрешение toocall hello среднего уровня приложение Azure AD. Этот подход нескольких приложений предоставляют более детальный контроль над tooeach уровня разрешений.
> 
> 

1. В hello [классический портал Azure](https://manage.windowsazure.com/), перейдите в слишком**Azure Active Directory**.
   
   Поскольку некоторые параметры Azure Active Directory, которые необходимо получить доступ к tooare еще недоступна в текущем портале Azure hello имеется toouse hello классического портала.
2. На hello **каталога** щелкните клиенте AAD.
   
   ![Azure AD на классическом портале](./media/app-service-api-dotnet-user-principal-auth/selecttenant.png)
3. Нажмите кнопку **приложений > приложений, которыми владеет Моя компания**, а затем нажмите кнопку флажок hello.
   
   Также возможно toorefresh hello страницы toosee hello нового приложения.
4. В списке hello приложений щелкните имя hello hello, Azure создается при включении проверки подлинности для приложения API.
   
   ![Вкладка "Приложения Azure AD"](./media/app-service-api-dotnet-user-principal-auth/appstab.png)
5. Нажмите **Настроить**.
   
   ![Вкладка "Настройка Azure AD"](./media/app-service-api-dotnet-user-principal-auth/configure.png)
6. Задать **URL-адрес входа** toohello URL-адрес для веб-приложения AngularJS, без замыкающей косой черты.
   
   Например, https://todolistangular.azurewebsites.net.
   
   ![URL-адрес входа](./media/app-service-api-dotnet-user-principal-auth/signonurlazure.png)
7. Задать **URL-адрес ответа** toohello URL-адрес для веб-приложения без замыкающей косой черты.
   
   Например, https://todolistsangular.azurewebsites.net.
8. Щелкните **Сохранить**.
   
   ![URL-адрес ответа](./media/app-service-api-dotnet-user-principal-auth/replyurlazure.png)
9. Внизу hello страницы приветствия щелкните **управление манифест > загрузки манифеста**.
   
   ![Загрузить манифест](./media/app-service-api-dotnet-user-principal-auth/downloadmanifest.png)
10. Загрузите tooa hello местоположения, где его можно изменить.
11. В файле манифеста загружаются hello, поиск hello `oauth2AllowImplicitFlow` свойство. Измените значение этого свойства из hello `false` слишком`true`, а затем сохраните файл hello.
    
    Это нужно для того, чтобы был возможен доступ из одностраничного приложения JavaScript. Она позволяет hello Oauth 2.0 носителя токена toobe возвращается в hello фрагмент URL-адреса.
12. Нажмите кнопку **управление манифест > передачи манифест**и файл hello передачи, была обновлена в hello предыдущих шага.
    
    ![Отправить манифест](./media/app-service-api-dotnet-user-principal-auth/uploadmanifest.png)
13. Копировать hello **идентификатор клиента** значение и сохраните его где-то ее можно загрузить из более поздней версии.

## <a name="configure-hello-todolistangular-project-toouse-authentication"></a>Настройка проверки подлинности для toouse проекта ToDoListAngular hello
В этом разделе изменить hello AngularJS переднего плана, чтобы он использовал библиотеку проверки подлинности Active Directory (ADAL) для tooacquire JS токен носителя для hello вошедшего в систему пользователя из Azure AD. будет включить токен hello в HTTP-запросов, отправляемых toohello среднего уровня, кода Hello, как показано в hello следующие схемы. 

![Схема проверки подлинности пользователей](./media/app-service-api-dotnet-user-principal-auth/appdiagram.png)

Сделайте следующие изменения toofiles в проекте ToDoListAngular hello hello.

1. Откройте hello *index.cshtml* файла.
2. Раскомментируйте hello строк, которые ссылаются hello библиотеку проверки подлинности Active Directory (ADAL) для скриптов JS.
   
        <script src="app/scripts/adal.js"></script>
        <script src="app/scripts/adal-angular.js"></script>
3. Откройте hello *app/scripts/app.js* файла.
4. Закомментируйте hello блок кода, помеченные для «без проверки подлинности» и раскомментируйте hello блок кода, помеченные для «с» проверка подлинности.
   
    Это изменение ссылается на поставщика проверки подлинности ADAL JS hello и предоставляет tooit значения конфигурации. В следующие шаги hello задать hello значения конфигурации для приложения API и приложения Azure AD.
5. В коде hello, который задает hello `endpoints` hello переменной, задайте URL-адрес API toohello URL-адрес приложения hello API для hello ToDoListAPI проекта создан, и задайте hello Azure AD приложения идентификатор toohello идентификатор клиента, который был скопирован из hello классический портал Azure.
   
    Код Hello стал примерно toohello следующий пример.
   
        var endpoints = {
            "https://todolistapi0121.azurewebsites.net/": "1cf55bc9-9ed8-4df31cf55bc9-9ed8-4df3"
        };
6. В hello вызовите слишком`adalProvider.init`, задайте `tenant` tooyour имя клиента и `clientId` значение toosame, используемый в предыдущем шаге hello.
   
    Код Hello стал примерно toohello следующий пример.
   
        adalProvider.init(
            {
                instance: 'https://login.microsoftonline.com/', 
                tenant: 'contoso.onmicrosoft.com',
                clientId: '1cf55bc9-9ed8-4df31cf55bc9-9ed8-4df3',
                extraQueryParameter: 'nux=1',
                endpoints: endpoints
            },
            $httpProvider
            );
   
    Эти изменения слишком`app.js` указать, что вызывающий код hello и вызывается API hello в приложение hello же Azure AD.
7. Откройте hello *app/scripts/homeCtrl.js* файла.
8. Закомментируйте hello блок кода, помеченные для «без проверки подлинности» и раскомментируйте hello блок кода, помеченные для «с» проверка подлинности.
9. Откройте hello *app/scripts/indexCtrl.js* файла.
10. Закомментируйте hello блок кода, помеченные для «без проверки подлинности» и раскомментируйте hello блок кода, помеченные для «с» проверка подлинности.

### <a name="deploy-hello-todolistangular-project-tooazure"></a>Развертывание проекта tooAzure hello ToDoListAngular
1. В **обозревателе решений**, щелкните правой кнопкой мыши проект ToDoListAngular hello и нажмите кнопку **публикации**.
2. Щелкните **Опубликовать**.
   
    Visual Studio развертывает проект hello и открывает базовый URL-адрес браузера toohello веб-приложения. При этом будут отображены ошибка 403 страницы, которая является нормальным попытки toogo tooa веб-API базовый URL-адрес в браузере.
   
    У вас по-прежнему есть toomake изменение toohello средний уровень приложения API перед тестированием приложения hello.
3. Hello закрыть браузер.

## <a name="configure-hello-todolistapi-project-toouse-authentication"></a>Настройка проверки подлинности для toouse проекта ToDoListAPI hello
В настоящее время hello отправляет ToDoListAPI проекта «*» как hello `owner` tooToDoListDataAPI значение. В этом разделе изменить идентификатор hello toosend кода hello приветствия вошедшего пользователя.

Внесите следующие изменения в проекте ToDoListAPI hello hello.

1. Откройте hello *Controllers/ToDoListController.cs* файла и раскомментируйте строку hello в каждый метод действия, который задает `owner` toohello Azure AD `NameIdentifier` значение утверждения. Например:
   
        owner = ((ClaimsIdentity)User.Identity).FindFirst(ClaimTypes.NameIdentifier).Value;
   
    **Важные**: не раскомментируйте код в hello `ToDoListDataAPI` метода; вы выполните, далее в учебнике основной проверки подлинности службы hello.

### <a name="deploy-hello-todolistapi-project-tooazure"></a>Развертывание проекта tooAzure hello ToDoListAPI
1. В **обозревателе решений**, щелкните правой кнопкой мыши проект ToDoListAPI hello и нажмите кнопку **публикации**.
2. Щелкните **Опубликовать**.
   
    Visual Studio развертывает проект hello и открывает базовый URL-адрес приложения toohello обозреватель API.
3. Hello закрыть браузер.

### <a name="test-hello-application"></a>Тестирование приложения hello
1. Go toohello URL-адрес веб-приложения hello, **с использованием HTTPS, а не HTTP**.
2. Нажмите кнопку hello **tooDo списка** вкладки.
   
    Все запрашиваемые toolog в.
3. Войдите в систему с учетными данными пользователя в клиенте AAD hello.
4. Hello **tooDo списка** появится страница.
   
   ![Страница списка tooDo](./media/app-service-api-dotnet-user-principal-auth/webappindex.png)
   
   Элементы списка дел не отображаются, так как до этого момента все они принадлежали владельцу "*". Теперь запрашивает элементы для hello вошедшего пользователя hello среднего уровня и none пока не создано.
5. Добавьте новый tooverify элементов задачи, работа приложения hello.
6. В другом окне браузера перейдите toohello Swagger URL-адрес пользовательского интерфейса для приложения ToDoListDataAPI API hello и щелкните **ToDoList > получить**. Введите звездочку для hello `owner` параметр и нажмите кнопку **попробуйте**.
   
   Hello ответа показывает, что новые элементы задача hello быть hello Azure AD, фактический идентификатор пользователя в свойстве Owner hello.
   
   ![Идентификатор владельца в ответе JSON](./media/app-service-api-dotnet-user-principal-auth/todolistapiauth.png)

## <a name="building-hello-projects-from-scratch"></a>Построение проектов hello с нуля
Hello двух веб-API проекты были созданы с помощью hello **приложения API Azure** проекта шаблона и замена контроллера значения по умолчанию hello с ToDoList. 

Слишком сведения о создании приложения AngularJS одну страницу и серверной части веб-API 2, см. в разделе [руки на лаборатории: построение одной страницы приложений (SPA) с веб-API ASP.NET и Angular.js](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs). Сведения о том, как tooadd код проверки подлинности Azure AD, см. следующие ресурсы hello:

* [Защита одностраничных приложений AngularJS с помощью Azure AD](../active-directory/active-directory-devquickstarts-angular.md).
* [Introducing ADAL JS v1 (Введение в ADAL JS, версия 1)](http://www.cloudidentity.com/blog/2015/02/19/introducing-adal-js-v1/)

## <a name="troubleshooting"></a>Устранение неполадок
[!INCLUDE [troubleshooting](../../includes/app-service-api-auth-troubleshooting.md)]

* Убедитесь, что вы не путаете ToDoListAPI (средний уровень) и ToDoListDataAPI (уровень данных). Например у добавляемых проверки подлинности toohello среднего уровня API приложения hello уровня данных. 
* Убедитесь, что hello AngularJS исходного кода ссылок hello среднего уровня API URL-адрес приложения (ToDoListAPI, не ToDoListDataAPI) и hello правильными идентификатор клиента Azure AD. 

## <a name="next-steps"></a>Дальнейшие действия
В этом учебнике вы узнали, как toouse проверки подлинности службы приложений для приложения API и как toocall hello приложения API с помощью hello библиотеки ADAL JS. В следующем уроке hello вы узнаете, как слишком[приложения tooyour API безопасного доступа для service to service сценариев](app-service-api-dotnet-service-principal-auth.md).

