---
title: "aaaGet к работе с API приложений и ASP.NET в службе приложений | Документы Microsoft"
description: "Узнайте, как toocreate, развертывать и использовать приложения ASP.NET API в службе приложений Azure, с помощью Visual Studio 2015."
services: app-service\api
documentationcenter: .net
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: ddc028b2-cde0-4567-a6ee-32cb264a830a
ms.service: app-service-api
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: hero-article
ms.date: 09/20/2016
ms.author: alkarche
ms.openlocfilehash: d3e90f1585907d183b0435c6cafc5585bc1e29ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-api-apps-aspnet-and-swagger-in-azure-app-service"></a>Приступая к работе с приложениями API, ASP.NET и Swagger в службе приложений Azure
[!INCLUDE [selector](../../includes/app-service-api-get-started-selector.md)]

— Hello сначала ряд учебники, которые показывают, как службы toouse возможности приложения Azure, полезны при разработке и хост-API RESTful.  В этом руководстве рассматривается обеспечение поддержки метаданных API в формате Swagger.

Вы узнаете:

* Как toocreate и развернуть [приложения API](app-service-api-apps-why-best-platform.md) в службе приложений Azure с помощью средств, встроенных в Visual Studio 2015.
* Как пакет Swashbuckle NuGet tooautomate API обнаружения с помощью hello toodynamically создания Swagger API метаданных.
* Как tooautomatically метаданных Swagger API toouse создания кода клиента для приложения API.

## <a name="sample-application-overview"></a>Обзор примеров приложений
В этом руководстве вы будете работать с простым примером приложения списка дел. приложение Hello имеет интерфейсную одностраничного приложения (SPA), средний уровень веб-API ASP.NET и веб-API ASP.NET уровня данных.

![Схема примера приложения приложений API](./media/app-service-api-dotnet-get-started/noauthdiagram.png)

Ниже приведен снимок экрана приветствия [AngularJS](https://angularjs.org/) переднего плана.

![API образец приложения toodo список приложений](./media/app-service-api-dotnet-get-started/todospa.png)

Hello решения Visual Studio включает в себя три проекта:

![](./media/app-service-api-dotnet-get-started/projectsinse.png)

* **ToDoListAngular** -hello переднего плана: SPA AngularJS, который вызывает hello среднего уровня.
* **ToDoListAPI** -hello среднего уровня: это проект веб-API ASP.NET, который вызывает hello уровень данных операции CRUD tooperform заданий для выполнения.
* **ToDoListDataAPI** -уровень данных hello: проект веб-API ASP.NET, выполняющей заданий для выполнения операций CRUD.

Трехуровневая архитектура Hello является одним из многих архитектур, которые можно реализовать с помощью API приложения и используется только для демонстрационных целей. Hello код на каждом уровне сводится функций API приложений возможных toodemonstrate; Например уровень данных hello использует памяти сервера, а не базы данных как механизма сохраняемости.

После завершения этого учебника, вы получите два проекта веб-API hello вверх и запуск в облаке hello в приложение API службы приложений.

Далее учебнике Hello серии hello развертывает hello SPA внешнего интерфейса toohello облака.

## <a name="prerequisites"></a>Предварительные требования
* Веб-API ASP.NET - hello учебника инструкции предполагают, у вас есть базовых знаний о том, как toowork с ASP.NET [веб-API 2](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api) в Visual Studio.
* Учетная запись Azure. [Создайте бесплатную учетную запись Azure](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) или [активируйте преимущества для подписчиков Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).
  
    Tooget к работе со службой приложения Azure, прежде чем выполнить вход для учетной записи Azure, перейдите слишком[повторите служб приложений](https://azure.microsoft.com/try/app-service/). Там можно быстро создать кратковременное приложение начального уровня в службе приложений. Это не потребует **ни кредитной карты**, ни каких-либо обязательств.
* Visual Studio 2015 с hello [Azure SDK для .NET](https://azure.microsoft.com/downloads/archive-net-downloads/) -hello SDK устанавливает Visual Studio 2015 автоматически, если вы его еще нет.
  
  * В Visual Studio щелкните "Справка -> О Microsoft Visual Studio" и убедитесь, что у вас установлены средства службы приложений Azure версии 2.9.1 или более поздней.
    
    ![Версия средств приложений Azure](./media/app-service-api-dotnet-get-started/apiversion.png)
    
    > [!NOTE]
    > В зависимости от того, сколько зависимостей SDK hello уже имеется на компьютере установка hello SDK может занять много времени, от нескольких минут tooa полчаса или несколько.
    > 
    > 

## <a name="download-hello-sample-application"></a>Загрузите пример приложения hello
1. Загрузите hello [Azure-Samples/app-service-api-dotnet-to-do-list](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list) репозитория.
   
    Можно щелкнуть hello **загрузить ZIP** кнопки или клонирования репозитория hello на локальном компьютере.
2. Откройте решение ToDoList hello в Visual Studio 2015 или 2013.
   
   1. Вам потребуется tootrust каждого решения.
         ![Предупреждение системы безопасности](./media/app-service-api-dotnet-get-started/securitywarning.png)
3. Построение решений (CTRL + SHIFT + B) toorestore hello hello-пакеты NuGet.
   
    Перед развертыванием следует toosee приложения hello в операции можно выполнять локально. Убедитесь, что ToDoListDataAPI запускаемого проекта и решения выполнения hello. Ошибки HTTP 403 toosee следует ожидать в браузере.

## <a name="use-swagger-api-metadata-and-ui"></a>Использование метаданных и пользовательского интерфейса API Swagger
Поддержка метаданных API [Swagger 2.0](http://swagger.io/) встроена в службу приложений Azure. Каждое приложение API можно указать URL-адрес конечной точки, которая возвращает метаданные для hello API в формате Swagger JSON. Hello метаданные, возвращенные этой конечной точки можно использовать toogenerate клиентский код.

Проект веб-API ASP.NET можно создать динамически метаданных Swagger с помощью hello [Swashbuckle](https://www.nuget.org/packages/Swashbuckle) пакет NuGet. в проектах ToDoListDataAPI и ToDoListAPI hello, которые загружаются Hello пакет Swashbuckle NuGet уже установлена.

В этом разделе учебника hello просмотрите созданные hello метаданных Swagger 2.0, и повторите тестирования пользовательского интерфейса, основанный на метаданных Swagger hello.

1. Установите проект ToDoListDataAPI hello (**не** проекта ToDoListAPI hello) hello запускаемым проектом.
   
    ![Назначить ToDoDataAPI в качестве запускаемого проекта](./media/app-service-api-dotnet-get-started/startupproject.png)
2. Нажмите клавишу F5 или выберите **Отладка > Начать отладку** toorun hello проекта в режиме отладки.
   
    Hello браузера открывается и отображается страница ошибки HTTP 403 hello.
3. В адресной строки браузера, добавьте `swagger/docs/v1` toohello конец строки hello и нажмите клавишу Return. (URL-адрес является hello `http://localhost:45914/swagger/docs/v1`.)
   
    Это значение по умолчанию hello URL-адрес, используемый метаданных Swagger 2.0 JSON tooreturn Swashbuckle для hello API.
   
    При использовании Internet Explorer hello браузер предложит toodownload *v1.json* файла.
   
    ![Скачивание метаданных JSON в Internet Explorer](./media/app-service-api-dotnet-get-started/iev1json.png)
   
    При использовании Chrome, Firefox или край hello браузер отображает hello JSON в окне браузера hello. По-разному обрабатывать JSON в различных браузерах и окна браузера может выглядеть так же, как и пример hello.
   
    ![Метаданные JSON в Chrome](./media/app-service-api-dotnet-get-started/chromev1json.png)
   
    Hello ниже приведен пример hello первый раздел метаданных Swagger hello для hello API, с определением hello для hello метод Get. Эти метаданные являются, какие диски hello Swagger пользовательского интерфейса, используйте в hello, выполнив действия, которое используется в следующем разделе учебника tooautomatically hello создания кода клиента.
   
        {
          "swagger": "2.0",
          "info": {
            "version": "v1",
            "title": "ToDoListDataAPI"
          },
          "host": "localhost:45914",
          "schemes": [ "http" ],
          "paths": {
            "/api/ToDoList": {
              "get": {
                "tags": [ "ToDoList" ],
                "operationId": "ToDoList_GetByOwner",
                "consumes": [ ],
                "produces": [ "application/json", "text/json", "application/xml", "text/xml" ],
                "parameters": [
                  {
                    "name": "owner",
                    "in": "query",
                    "required": true,
                    "type": "string"
                  }
                ],
                "responses": {
                  "200": {
                    "description": "OK",
                    "schema": {
                      "type": "array",
                      "items": { "$ref": "#/definitions/ToDoItem" }
                    }
                  }
                },
                "deprecated": false
              },
4. Закройте браузер hello и остановка отладки в Visual Studio.
5. В hello ToDoListDataAPI проектов в **обозревателе решений**откройте hello *App_Start\SwaggerConfig.cs* файла, а затем прокрутите список вниз tooline 174 и раскомментируйте следующий код hello.
   
        /*
            })
        .EnableSwaggerUi(c =>
            {
        */
   
    Hello *SwaggerConfig.cs* файл создается при установке пакета Swashbuckle hello в проекте. файл Hello предоставляет ряд способов tooconfigure Swashbuckle.
   
    Hello код Раскомментировать приветствия включает Swagger пользовательского интерфейса, используемого в hello следующие шаги. При создании проекта веб-API с помощью шаблона проекта приложения hello API, этот код закомментирована по умолчанию в качестве меры безопасности.
6. Снова запустите проект hello.
7. В адресной строки браузера, добавьте `swagger` toohello конец строки hello и нажмите клавишу Return. (URL-адрес является hello `http://localhost:45914/swagger`.)
8. Когда откроется страница приветствия Swagger пользовательского интерфейса, нажмите кнопку **ToDoList** toosee hello доступные методы.
   
    ![Пользовательский интерфейс Swagger — доступные методы](./media/app-service-api-dotnet-get-started/methods.png)
9. Сначала щелкните hello **получить** кнопку в списке hello.
10. В hello **параметры** введите звездочку в качестве значения hello hello `owner` параметр и нажмите кнопку **попробуйте**.
    
    При добавлении проверки подлинности на следующих занятиях рассматривается среднего уровня hello предоставит уровень hello действительного пользовательского идентификатора toohello данных. Пока все задачи имеют звездочку как их идентификатор владельца во время выполнения приложения hello не включена проверка подлинности.
    
    ![Пользовательский интерфейс Swagger — кнопка Try it out](./media/app-service-api-dotnet-get-started/gettryitout1.png)
    
    Hello Swagger пользовательского интерфейса вызывает метод ToDoList Get hello и отображает код ответа hello и результаты JSON.
    
    ![Пользовательский интерфейс Swagger — результаты нажатия кнопки Try it out](./media/app-service-api-dotnet-get-started/gettryitout.png)
11. Нажмите кнопку **Post**и щелкните поле hello **схему модели**.
    
    Щелкнув hello модели схемы prefills hello поле ввода где можно указать значение параметра hello hello метода Post. (Если это не сработает в Internet Explorer, используйте другой браузер или вручную ввести значение параметра hello в hello следующий шаг).  
    
    ![Пользовательский интерфейс Swagger — нажатие кнопки Try it out при выборе метода Post](./media/app-service-api-dotnet-get-started/post.png)
12. Изменение hello JSON в hello `todo` входной параметр, чтобы он выглядит как следующий пример hello или замените текст описания:
    
        {
          "ID": 2,
          "Description": "buy hello dog a toy",
          "Owner": "*"
        }
13. Щелкните **Попробовать**.
    
    Hello ToDoList API возвращает код ответа HTTP 204 означает успешное выполнение.
14. Сначала щелкните hello **получить** , а затем в этом разделе страницы приветствия нажмите hello **попробуйте** кнопки.
    
    метод ответа на получение Hello теперь включает новый элемент toodo hello.
15. Необязательно: Hello Put, Delete, попробуйте также и получить идентификатор методами.
16. Закройте браузер hello и остановка отладки в Visual Studio.

Swashbuckle можно использовать с любыми проектами веб-API ASP.NET. Если вы хотите tooadd Swagger метаданных поколения tooan существующий проект, просто установите hello Swashbuckle пакета.

> [!NOTE]
> В метаданных Swagger есть уникальный идентификатор для каждой операции API. По умолчанию пакет Swashbuckle может создавать дублирующиеся идентификаторы операций Swagger для методов контроллера веб-API. Это происходит, если перегружены методы HTTP контроллера, например `Get()` и `Get(id)`. Сведения о как overloads toohandle разделе [определения интерфейсов API настройки Swashbuckle создан](app-service-api-dotnet-swashbuckle-customize.md). При создании проекта веб-API в Visual Studio с помощью шаблона приложения API Azure hello toohello автоматически добавляется код, который приводит к возникновению ошибки операции уникальные идентификаторы *SwaggerConfig.cs* файла.  
> 
> 

## <a id="createapiapp"></a>Создание приложения API в Azure и развертывание кода tooit
В этом разделе, используйте инструменты Azure, интегрированные в Visual Studio hello **веб-публикация** мастер toocreate новый API приложения в Azure. Затем развертывание ToDoListDataAPI проекта toohello новый API приложение hello и вызвать hello API, запустив hello Swagger пользовательского интерфейса.

1. В **обозревателе решений**, щелкните правой кнопкой мыши проект ToDoListDataAPI hello и нажмите кнопку **публикации**.
   
    ![Нажмите кнопку "Опубликовать" в Visual Studio](./media/app-service-api-dotnet-get-started/pubinmenu.png)
2. В hello **профиль** шага hello **веб-публикация** мастера, нажмите кнопку **службу приложений Microsoft Azure**.
   
   ![Выберите "Служба приложений Azure" в мастере веб-публикации](./media/app-service-api-dotnet-get-started/selectappservice.png)
3. Вход tooyour учетная запись Azure, если вы еще не выполнена или обновите учетные данные, если вы истечении срока.
4. В диалоговое окно службы приложения hello, выберите hello Azure **подписки** toouse и нажмите кнопку **New**.
   
    ![Нажмите кнопку "Создать" в диалоговом окне службы приложений](./media/app-service-api-dotnet-get-started/clicknew.png)
   
    Hello **размещения** вкладка hello **Создание приложения службы** откроется диалоговое окно.
   
    Так как вы развертываете проект веб-API, который содержит Swashbuckle установлена, Visual Studio подразумевает toocreate приложения API. Это обозначается hello **имя приложения API** title и по hello фактов, hello **изменение типа** раскрывающегося списка задано слишком**приложения API**.
   
    ![Тип приложения в диалоговом окне службы приложений](./media/app-service-api-dotnet-get-started/apptype.png)
5. Введите **имя приложения API** является уникальным в hello *azurewebsites.net* домена. Можно принять имя по умолчанию hello, предлагаемых программой Visual Studio.
   
    Если ввести имя, которое уже использован другим пользователем, можно увидеть право toohello красный восклицательный знак.
   
    Hello URL-адрес приложения hello API будет `{API app name}.azurewebsites.net`.
6. В hello **группы ресурсов** раскрывающийся список, щелкните **New**, а затем введите «ToDoListGroup» или другое имя, если вы предпочитаете.
   
    Группы ресурсов — это совокупность ресурсов Azure, таких как приложения API, базы данных, виртуальные машины и т. д.    В этом учебнике это лучший toocreate новую группу ресурсов, так как это позволяет легко toodelete за один шаг, все hello Azure ресурсов, созданных для учебника hello.
   
    В этом поле можно выбрать существующую [группу ресурсов](../azure-resource-manager/resource-group-overview.md) или создать отдельную, введя имя, которое отличается от имени любой существующей группы ресурсов в подписке.
7. Нажмите кнопку hello **New** кнопку Далее toohello **план служб приложений** раскрывающегося списка.
   
    Hello снимке экрана показаны примеры значений **имя приложения API**, **подписки**, и **группы ресурсов** --значения будут отличаться.
   
    ![Диалоговое окно "Создание службы приложений"](./media/app-service-api-dotnet-get-started/createas.png)
   
    В следующие шаги hello создается план служб приложений для новой группы ресурсов hello. План служб приложений указывает hello вычислительные ресурсы, которые ваше приложение API запускается. Например при выборе hello бесплатный уровень API приложения выполняется на общих виртуальных машин, выполняющегося на выделенных виртуальных машин для некоторых платных уровней. Дополнительные сведения см. в статье [Подробный обзор планов службы приложений Azure](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).
8. В hello **настроить план служб приложений** диалоговое окно, введите «ToDoListPlan» или другое имя, если вы предпочитаете.
9. В hello **расположение** раскрывающегося списка выберите ближайший tooyou расположение hello.
   
    Этот параметр определяет, в каком центре обработки данных Azure будет выполняться приложение. Выберите расположение закрыть tooyou toominimize [задержки](http://www.bing.com/search?q=web%20latency%20introduction&qs=n&form=QBRE&pq=web%20latency%20introduction&sc=1-24&sp=-1&sk=&cvid=eefff99dfc864d25a75a83740f1e0090).
10. В hello **размер** раскрывающийся список, щелкните **Free**.
    
    В этом учебнике hello бесплатной ценовой категории предоставит достаточно производительности.
11. В hello **настроить план служб приложений** диалоговое окно, нажмите кнопку **ОК**.
    
    ![Нажмите кнопку "ОК" в диалоговом окне "Настройка плана службы приложений"](./media/app-service-api-dotnet-get-started/configasp.png)
12. В hello **Создание приложения службы** диалоговое окно, нажмите кнопку **создать**.
    
    ![Нажмите кнопку "Создать" в диалоговом окне"Создание службы приложений"](./media/app-service-api-dotnet-get-started/clickcreate.png)
    
    Visual Studio создает приложение hello API и профиль публикации, которая имеет все hello необходимые параметры для приложения hello API. Затем он открывает hello **веб-публикация** мастер, который будет использоваться toodeploy hello проекта.
    
    Hello **веб-публикация** откроется мастер на hello **подключения** вкладка (см. ниже).
    
    На hello **подключения** вкладке hello **сервера** и **имя сайта** параметры приложения API tooyour точки. Hello **имя пользователя** и **пароль** учетные данные развертывания, которые создает Azure. После развертывания Visual Studio открывает toohello браузера **URL-адрес назначения** (это hello единственной целью **URL-адрес назначения**).  
13. Щелкните **Далее**.
    
    ![Нажмите кнопку "Далее" на вкладке "Подключение" мастера веб-публикации](./media/app-service-api-dotnet-get-started/connnext.png)
    
    Следующая вкладка Hello — hello **параметры** вкладке (см. ниже). Здесь можно изменить toodeploy вкладка конфигурации сборки hello отладочного построения [удаленной отладки](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug). Hello вкладка также предлагает несколько вариантов **параметры публикации файлов**:
    
    * "Удалить дополнительные файлы в месте назначения";
    * "Предварительно компилировать при публикации";
    * Исключить файлы из папки App_Data hello
    
    В данном руководстве эти параметры не используются. Подробное описание этих параметров см. в статье [How to: Deploy a Web Project Using One-Click Publish in Visual Studio](https://msdn.microsoft.com/library/dd465337.aspx) (Развертывание веб-проекта с помощью публикации одним щелчком в Visual Studio).
14. Щелкните **Далее**.
    
    ![Нажмите кнопку "Далее" на вкладке "Параметры" мастера веб-публикации](./media/app-service-api-dotnet-get-started/settingsnext.png)
    
    Далее следует hello **предварительного просмотра** вкладки (показано ниже), предоставляющей возможности toosee, какие файлы будут скопированы из проекта приложения toohello API toobe. При развертывании приложения tooan API проекта, уже развернут tooearlier копируются только измененные файлы. Если требуется toosee список какие будут скопированы, можно щелкнуть hello **начать просмотр** кнопки.
15. Щелкните **Опубликовать**.
    
    ![Нажмите кнопку "Опубликовать" на вкладке "Предварительный просмотр" мастера веб-публикации](./media/app-service-api-dotnet-get-started/clickpublish.png)
    
    Visual Studio развертывает hello ToDoListDataAPI проекта toohello нового приложения API. Hello **вывода** окно входит успешному развертыванию, и в URL-toohello открытое окно браузера приложение hello API появится страница «создан».
    
    ![Окно вывода с информацией об успешном развертывании](./media/app-service-api-dotnet-get-started/deploymentoutput.png)
    
    ![Страница "Приложение API успешно создано"](./media/app-service-api-dotnet-get-started/appcreated.png)
16. Добавить URL-адрес toohello «swagger» в адресной строке браузера hello и нажмите клавишу ВВОД. (URL-адрес является hello `http://{apiappname}.azurewebsites.net/swagger`.)
    
    Hello браузер отображает hello же Swagger пользовательский Интерфейс, который вы видели ранее, но теперь он работает в облаке hello. Опробуйте hello метод Get и вы увидите, что вы будете toohello назад по умолчанию 2 заданий для выполнения. Hello изменения, сделанные ранее были сохранены в памяти на локальном компьютере hello.
17. Откройте hello [портал Azure](https://portal.azure.com/).
    
    Hello портал Azure является веб-интерфейс для управления ресурсами Azure, таких как приложения API.
18. Щелкните **Больше служб > Службы приложений**.
    
    ![Обзор служб приложений](./media/app-service-api-dotnet-get-started/browseas.png)
19. В hello **службы приложений** колонки, найдите и выберите новый API приложения. (В hello портал Azure, называются окнах, открывающихся справа toohello *колонок*.)
    
    ![Колонка "Службы приложений"](./media/app-service-api-dotnet-get-started/choosenewapiappinportal.png)
    
    Откроются две колонки: Обзор API приложение hello имеет один колонки и один длинный список параметров, которые можно просматривать и изменять.
20. В hello **параметры** колонки, найти hello **API** и нажмите кнопку **определения API**.
    
    ![Определение API в колонке "Параметры"](./media/app-service-api-dotnet-get-started/apidefinsettings.png)
    
    Hello **определения API** колонке позволяет указать URL-адрес hello, возвращающий метаданные Swagger 2.0 в формате JSON. Когда Visual Studio создает приложение hello API, задает значение по умолчанию toohello URL-адрес определения hello API для созданных Swashbuckle метаданные, вы уже видели раньше, приложение hello API базовый URL-адрес плюс `/swagger/docs/v1`.
    
    ![URL-адрес определения API](./media/app-service-api-dotnet-get-started/apidefurl.png)
    
    При выборе кода клиента toogenerate приложения API для него Visual Studio извлекает метаданные hello из этого URL-адреса.

## <a id="codegen"></a>Создание клиентского кода для hello уровня данных
Одним из преимуществ hello интеграцию Swagger в приложения Azure API является автоматическое создание кода. Созданные классы клиентских стала проще toowrite код, который вызывает приложение API.

Hello ToDoListAPI проект уже содержит hello созданный код клиента, но в hello, выполнив действия будет удалить его и создать его заново, как создание кода toodo hello toosee.

1. В Visual Studio **обозревателе решений**, в hello ToDoListAPI проектов, удалите hello *ToDoListDataAPI* папки. **Предупреждение: Удалите только hello папки, не hello ToDoListDataAPI проекта.**
   
    ![Удаление кода, созданного клиентом](./media/app-service-api-dotnet-get-started/deletecodegen.png)
   
    Эта папка была создана с помощью процесса создания кода hello, скоро будет toogo через.
2. Щелкните правой кнопкой мыши проект ToDoListAPI hello и нажмите кнопку **Добавить > клиента REST API**.
   
    ![Добавление клиента REST API в Visual Studio](./media/app-service-api-dotnet-get-started/codegenmenu.png)
3. В hello **Добавление клиента REST API** диалоговое окно, нажмите кнопку **URL-адрес Swagger**, а затем нажмите кнопку **активов Azure выберите**.
   
    ![Select Azure Asset](./media/app-service-api-dotnet-get-started/codegenbrowse.png)
4. В hello **службы приложений** диалоговое окно, разверните группу ресурсов hello, вы используете для этого учебника выберите API приложения и нажмите кнопку **ОК**.
   
    ![Выбор приложения API для создания кода](./media/app-service-api-dotnet-get-started/codegenselect.png)
   
    Обратите внимание, что при возврате toohello **Добавление клиента REST API** диалоговом hello текстовое поле автоматически вводится определение hello API значение URL-адреса, который рассматривался выше hello портала.
   
    ![URL-адрес определения API](./media/app-service-api-dotnet-get-started/codegenurlplugged.png)
   
   > [!TIP]
   > Метаданные tooget альтернативный способ создания кода — это URL-адрес hello tooenter напрямую, а не через диалоговое окно обзора hello. Или следует toogenerate клиентский код перед развертыванием tooAzure можно запустить проект веб-API hello локально, go toohello URL-адрес, предоставляющий hello Swagger JSON-файл, сохраните файл hello и использовать hello **выберите существующий файл метаданных Swagger**параметр.
   > 
   > 
5. В hello **Добавление клиента REST API** диалоговое окно, нажмите кнопку **ОК**.
   
    Visual Studio создает папку с именем приложение hello API и создает клиентские классы.
   
    ![Файлы кода для созданного клиента](./media/app-service-api-dotnet-get-started/codegenfiles.png)
6. В проекте ToDoListAPI hello откройте *Controllers\ToDoListController.cs* toosee hello код вызывает hello API с помощью клиента создается hello строки 40.
   
    Hello, следующий фрагмент кода показывает, как hello код создает экземпляр объекта клиента hello и вызовы hello метода Get.
   
        private static ToDoListDataAPI NewDataAPIClient()
        {
            var client = new ToDoListDataAPI(new Uri(ConfigurationManager.AppSettings["toDoListDataAPIURL"]));
            return client;
        }
   
        public async Task<IEnumerable<ToDoItem>> Get()
        {
            using (var client = NewDataAPIClient())
            {
                var results = await client.ToDoList.GetByOwnerAsync(owner);
                return results.Select(m => new ToDoItem
                {
                    Description = m.Description,
                    ID = (int)m.ID,
                    Owner = m.Owner
                });
            }
        }
   
    параметр Hello конструктор получает URL-адрес конечной точки hello от hello `toDoListDataAPIURL` параметра приложения. В файле Web.config hello это значение является toohello набор локальных IIS Express URL-адрес hello API проекта, чтобы можно было запускать приложения hello локально. При отсутствии параметра конструктора hello конечную точку по умолчанию hello — hello URL-адрес, созданный код hello.
7. Будет создан класс вашего клиента с другим именем на основе имени приложения API; Изменение кода hello в *Controllers\ToDoListController.cs* , чтобы hello имя типа соответствует что был создан в своем проекте. Например, если вы назвали приложение API ToDoListDataAPI071316, необходимо изменить код
   
        private static ToDoListDataAPI NewDataAPIClient()
        {
            var client = new ToDoListDataAPI(new Uri(ConfigurationManager.AppSettings["toDoListDataAPIURL"]));

toothis:

        private static ToDoListDataAPI071316 NewDataAPIClient()
        {
            var client = new ToDoListDataAPI071316(new Uri(ConfigurationManager.AppSettings["toDoListDataAPIURL"]));


## <a name="create-an-api-app-toohost-hello-middle-tier"></a>Создать API приложения toohost hello среднего уровня
Ранее вы [приложения hello данных уровня API создания и развертывания кода tooit](#createapiapp).  Теперь выполните hello же процедуру для среднего уровня API приложение hello.

1. В **обозревателе решений**, щелкните правой кнопкой мыши hello среднего уровня ToDoListAPI проекта (не hello уровень данных ToDoListDataAPI) и нажмите кнопку **публикации**.
   
    ![Нажмите кнопку "Опубликовать" в Visual Studio](./media/app-service-api-dotnet-get-started/pubinmenu2.png)
2. В hello **профиль** вкладка hello **веб-публикация** мастера, нажмите кнопку **службу приложений Microsoft Azure**.
3. В hello **службы приложений** диалоговое окно, нажмите кнопку **New**.
4. В hello **размещения** вкладка hello **Создание приложения службы** диалогового окна поле, примите значение по умолчанию hello **имя приложения API** или введите имя, которое является уникальным в hello  *azurewebsites.NET* домена.
5. Выберите hello Azure **подписки** вы используете.
6. В hello **группы ресурсов** раскрывающийся список, выберите hello одну группу ресурсов, созданного ранее.
7. В hello **план обслуживания приложений** раскрывающийся список, выберите hello одного плана, созданного ранее. По умолчанию значение toothat.
8. Щелкните **Создать**.
   
    Visual Studio создает приложение hello API, создает профиль публикации для него и отображает hello **подключения** шага hello **веб-публикация** мастера.
9. В hello **подключения** шага hello **веб-публикация** мастера, нажмите кнопку **публикации**.
   
   Visual Studio развертывает ToDoListAPI проекта toohello новый API приложение hello и открывает обозреватель toohello URL-адрес приложения hello API. Откроется страница приветствия «успешно создан».

## <a name="configure-hello-middle-tier-toocall-hello-data-tier"></a>Настроить уровень данных hello toocall среднего уровня hello
При вызове API приложение hello среднего уровня теперь он предпримет попытку уровень данных hello toocall, с помощью hello localhost URL-адрес, по-прежнему в файле Web.config hello. В этом разделе введите URL-адрес hello данных уровня API приложения в параметры среды в API приложение hello среднего уровня. Если hello кода в приложении API hello среднего уровня получает URL-адрес уровня данных приветствия, параметр среды hello перезаписывает в файл Web.config hello.

1. Go toohello [портал Azure](https://portal.azure.com/)и перейдите toohello **приложения API** колонке приложение hello API, созданного проекта TodoListAPI (средний уровень) toohost hello.
2. В hello приложения API **параметры** колонка, щелкните **параметры приложения**.
3. Здравствуйте, приложения API в **параметры приложения** колонки, прокрутите вниз toohello **параметры приложения** статьи и добавьте следующее hello ключ и значение. URL-адрес hello hello первый API приложения, опубликованные в этом учебнике будет иметь значение Hello.
   
   | **Ключ** | toDoListDataAPIURL |
   | --- | --- |
   | **Значение** |https://{имя приложения API уровня данных}.azurewebsites.net |
   | **Пример** |https://todolistdataapi.azurewebsites.net |
4. Щелкните **Сохранить**.
   
    ![Нажмите кнопку "Сохранить" в колонке "Параметры приложения"](./media/app-service-api-dotnet-get-started/asinportal.png)
   
    Когда код hello работает в Azure, это значение теперь переопределит hello localhost URL-адрес, в файле Web.config hello.

## <a name="test"></a>Тест
1. В окне браузера перейдите toohello URL-адрес нового hello среднего уровня приложения API, который вы только что создали ToDoListAPI. Существует можно получить, щелкнув URL-адрес hello в главной колонке приложение hello API на портале hello.
2. Добавить URL-адрес toohello «swagger» в адресной строке браузера hello и нажмите клавишу ВВОД. (URL-адрес является hello `http://{apiappname}.azurewebsites.net/swagger`.)
   
    Hello браузер отображает hello же Swagger пользовательский Интерфейс, который вы видели ранее для ToDoListDataAPI, но теперь `owner` не поле является обязательным для операции Get hello, так как приложение среднего уровня API hello отправляет этого API приложения уровня данных значение toohello для вас. (Hello учебники проверки подлинности, средний уровень hello отправляют идентификаторы пользователя для hello `owner` параметр; теперь он жестко запрограммированного звездочку.)
3. Опробуйте hello метод Get и hello других toovalidate методы, hello приложения среднего уровня API успешно вызывает hello данных уровня приложения API.
   
    ![Метод Get пользовательского интерфейса Swagger](./media/app-service-api-dotnet-get-started/midtierget.png)

## <a name="troubleshooting"></a>Устранение неполадок
Если в ходе выполнения инструкций этого руководства возникнут проблемы, можно воспользоваться рекомендациями по устранению неполадок ниже:

* Убедитесь, что вы используете последнюю версию hello hello [Azure SDK для .NET](http://go.microsoft.com/fwlink/?linkid=518003).
* Два приветствия имен проекта являются аналогичные (ToDoListAPI, ToDoListDataAPI). Если не выглядит как описано в инструкциях hello при работе с проектом, убедитесь, что вы открыли hello нужный проект.
* Если вы в корпоративной сети и пытаетесь tooAzure toodeploy службы приложений через брандмауэр, убедитесь, что открыты порты 443 и 8172 для веб-развертывания. Если не удается открыть эти порты, можно использовать другие способы развертывания.  В разделе [развертывание вашего приложения tooAzure службы приложений](../app-service-web/web-sites-deploy.md).
* Ошибки «имена маршрутов должны быть уникальными»--можно получить их, если случайно развернуть приложение tooan API неправильный проекта hello и впоследствии развернуты правильно один tooit hello. toocorrect, повторного развертывания нужный проект toohello API приложение hello и на hello **параметры** вкладка hello **веб-публикация** мастера щелкните **удалить дополнительные файлы в месте назначения**.

После того как вы приложении ASP.NET API, запущенные в службе приложений Azure, вы можете toolearn Дополнительные сведения о функциональных возможностях Visual Studio, которые упрощают устранение неполадок. Сведения о ведении журналов, удаленной отладке и другую информацию см. в статье [Устранение неполадок веб-приложения в службе приложений Azure с помощью Visual Studio](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).

## <a name="next-steps"></a>Дальнейшие действия
Вы знаете, как toodeploy существующие веб-API проекты tooAPI приложения, создания кода клиента для приложения API и использовать API приложения от клиентов .NET. Hello далее в этой серии мы увидели, как слишком[использовать приложения tooconsume API CORS из клиентов JavaScript](app-service-api-cors-consume-javascript.md).

Дополнительные сведения о создании кода клиента см. в разделе hello [Azure/AutoRest](https://github.com/azure/autorest) репозитория в GitHub.com. Помощь по вопросам, с помощью клиента создается hello откройте [проблему в репозитории hello AutoRest](https://github.com/azure/autorest/issues).

Новые проекты приложения API toocreate с нуля, используйте hello **приложения API Azure** шаблона.

![Шаблон приложения API в Visual Studio](./media/app-service-api-dotnet-get-started/apiapptemplate.png)

Hello **приложения API Azure** шаблон проекта — hello эквивалентные toochoosing **пустой** ASP.NET 4.5.2 шаблона, щелкнув поддержки веб-API tooadd флажок hello и установка пакета Swashbuckle NuGet hello. Кроме того шаблон hello добавляет некоторые Создание Swashbuckle конфигурации код, предназначенный tooprevent hello повторяющиеся операции Swagger идентификаторы. После создания проекта приложения API, его можно развернуть приложение hello tooan API так же, как показано в данном учебнике.

