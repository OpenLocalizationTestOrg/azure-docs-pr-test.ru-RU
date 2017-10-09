---
title: "aaaBuild приложения ASP.NET в Azure с базой данных SQL | Документы Microsoft"
description: "Узнайте, как tooget ASP.NET приложения работают в Azure, с tooa подключения базы данных SQL."
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: 03c584f1-a93c-4e3d-ac1b-c82b50c75d3e
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: csharp
ms.topic: tutorial
ms.date: 06/09/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: d21c2bc404bfe038608c17e5a94d96847153002c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="build-an-aspnet-app-in-azure-with-sql-database"></a>Создание приложения ASP.NET в Azure с подключением к базе данных SQL

[Веб-приложения Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) — это служба веб-размещения с самостоятельной установкой исправлений и высоким уровнем масштабируемости. В этом учебнике показано, как toodeploy ASP.NET, управляемые данными веб-приложения в Azure и подключите его слишком[базы данных SQL Azure](../sql-database/sql-database-technical-overview.md). Когда закончите, у вас есть приложения ASP.NET, работающего в [службе приложений Azure](../app-service/app-service-value-prop-what-is.md) и подключен tooSQL базы данных.

![Опубликованное приложение ASP.NET в веб-приложении Azure](./media/app-service-web-tutorial-dotnet-sqldatabase/azure-app-in-browser.png)

Из этого руководства вы узнаете, как выполнять такие задачи:

> [!div class="checklist"]
> * Создание базы данных SQL в Azure.
> * Подключение tooSQL приложения ASP.NET базы данных
> * Развертывание tooAzure приложения hello
> * Обновить модель данных hello и повторно развернуть приложение hello
> * Журналы Azure tooyour терминалов потока
> * Управление приложение hello в hello портал Azure

## <a name="prerequisites"></a>Предварительные требования

toocomplete этого учебника:

* Установка [2017 г. Visual Studio](https://www.visualstudio.com/downloads/) с hello следующие рабочие нагрузки:
  - **ASP.NET и веб-разработка;**
  - **разработка Azure.**

  ![ASP.NET и веб-разработка, разработка Azure (в разделе Web & Cloud (Сеть и облако))](media/app-service-web-tutorial-dotnet-sqldatabase/workloads.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="download-hello-sample"></a>Загрузить образец hello

[Загрузите образец проекта hello](https://github.com/Azure-Samples/dotnet-sqldb-tutorial/archive/master.zip).

Извлечение (Распакуйте) hello *dotnet sqldb учебника master.zip* файл.

Образец Hello проекта содержит базовый [ASP.NET MVC](https://www.asp.net/mvc) CRUD (Создание чтение обновления и удаления) приложения с использованием [Entity Framework Code First](/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application).

### <a name="run-hello-app"></a>Выполните приложение hello

Откройте hello *dotnet-sqldb учебник master/DotNetAppSqlDb.sln* файл в Visual Studio. 

Тип `Ctrl+F5` toorun приложение hello без отладки. приложение Hello отображается в браузере по умолчанию. Выберите hello **создать новый** связь и создать несколько *задачи* элементов. 

![Диалоговое окно "Новый проект ASP.NET"](media/app-service-web-tutorial-dotnet-sqldatabase/local-app-in-browser.png)

Тест hello **изменить**, **сведения**, и **удалить** ссылки.

приложение Hello использует tooconnect контекст базы данных с базой данных hello. В этом образце hello контекст базы данных использует строку подключения с именем `MyDbConnection`. задана строка соединения Hello в hello *Web.config* файл и на которую ссылается hello *Models/MyDatabaseContext.cs* файла. Имя строки соединения Hello используется далее в tooan hello учебника tooconnect hello Azure web app базы данных SQL Azure. 

## <a name="publish-tooazure-with-sql-database"></a>Публикация tooAzure с базой данных SQL

В hello **обозревателе решений**, щелкните правой кнопкой мыши ваш **DotNetAppSqlDb** проект и выберите **публикации**.

![Публикация в обозревателе решений](./media/app-service-web-tutorial-dotnet-sqldatabase/solution-explorer-publish.png)

Выберите **Служба приложений Microsoft Azure** и нажмите кнопку **Опубликовать**.

![Публикация с помощью страницы обзора проекта](./media/app-service-web-tutorial-dotnet-sqldatabase/publish-to-app-service.png)

Публикация открывает hello **Создание приложения службы** диалоговое окно, в которых служит для создания всех hello Azure ресурсы, необходимые toorun веб-приложения ASP.NET в Azure.

### <a name="sign-in-tooazure"></a>Войдите в tooAzure

В hello **Создание приложения службы** диалоговое окно, нажмите кнопку **добавить учетную запись**, а затем войдите в tooyour подписки Azure. Если вы уже вошли в учетную запись Майкрософт, проверьте, содержит ли она подписку Azure. Если hello вход в учетную запись Майкрософт нет подписки Azure, щелкните его правильную учетную запись hello tooadd.
   
![Войдите в tooAzure](./media/app-service-web-tutorial-dotnet-sqldatabase/sign-in-azure.png)

После входа вы готовы toocreate Здравствуйте, все ресурсы, необходимые для вашего веб-приложение Azure в этом диалоговом окне.

### <a name="configure-hello-web-app-name"></a>Настройте имя веб-приложения hello

Можно сохранить имя веб-приложения создается hello, или изменить его уникальное имя tooanother (допустимые символы — `a-z`, `0-9`, и `-`). Имя веб-приложения Hello используется как часть URL-адрес по умолчанию hello в приложении (`<app_name>.azurewebsites.net`, где `<app_name>` является имя вашего веб-приложения). Имя веб-приложения Hello должен toobe уникальным для всех приложений в Azure. 

![Диалоговое окно "Создание службы приложений"](media/app-service-web-tutorial-dotnet-sqldatabase/wan.png)

### <a name="create-a-resource-group"></a>Создание группы ресурсов

[!INCLUDE [resource-group](../../includes/resource-group.md)]

Далее слишком**группы ресурсов**, нажмите кнопку **New**.

![Далее tooResource группы, нажмите кнопку Создать.](media/app-service-web-tutorial-dotnet-sqldatabase/new_rg2.png)

Имя группы ресурсов hello **myResourceGroup**.

> [!NOTE]
> Не нажимайте кнопку **Создать**. Необходимо сначала tooset копии базы данных SQL на более позднем этапе.

### <a name="create-an-app-service-plan"></a>Создание плана службы приложений

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

Далее слишком**план служб приложений**, нажмите кнопку **New**. 

В hello **настройте план обслуживания приложений** диалогового окна, Настройка hello новый план служб приложений с hello следующие параметры:

![Создание плана службы приложений](./media/app-service-web-tutorial-dotnet-sqldatabase/configure-app-service-plan.png)

| Настройка  | Рекомендуемое значение | Дополнительные сведения |
| ----------------- | ------------ | ----|
|**План службы приложений**| myAppServicePlan | [Планы службы приложений](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) |
|**Расположение**| Западная Европа | [Регионы Azure](https://azure.microsoft.com/regions/) |
|**Размер**| Free | [Ценовые категории](https://azure.microsoft.com/pricing/details/app-service/)|

### <a name="create-a-sql-server-instance"></a>Создание экземпляра SQL Server

Перед созданием базы данных необходимо сначала создать [логический сервер базы данных SQL Azure](../sql-database/sql-database-features.md). Логический сервер содержит группу баз данных, которыми можно управлять как группой.

Выберите **Обзор дополнительных служб Azure**.

![Настройка имени веб-приложения](media/app-service-web-tutorial-dotnet-sqldatabase/web-app-name.png)

В hello **службы** щелкните hello  **+**  значок Далее слишком**базы данных SQL**. 

![На вкладке службы hello, щелкните значок + hello Далее tooSQL базы данных.](media/app-service-web-tutorial-dotnet-sqldatabase/sql.png)

В hello **Настройка базы данных SQL** диалоговое окно, нажмите кнопку **New** Далее слишком**SQL Server**. 

Создается уникальное имя сервера. Это имя используется как часть URL-адрес по умолчанию hello для логического сервера, `<server_name>.database.windows.net`. Оно должно быть уникальным для всех экземпляров логических серверов в Azure. Можно изменить имя сервера hello, но для этого учебника оставьте значение hello создан.

Добавьте имя пользователя и пароль администратора, а затем нажмите кнопку **ОК**. Требования к сложности пароля см. в статье [Политика паролей](/sql/relational-databases/security/password-policy).

Запомните это имя пользователя и пароль. Они необходимы toomanage hello логического сервера экземпляр более поздней версии.

![Создание экземпляра SQL Server](media/app-service-web-tutorial-dotnet-sqldatabase/configure-sql-database-server.png)

### <a name="create-a-sql-database"></a>Создание базы данных SQL

В hello **Настройка базы данных SQL** диалогового окна: 

* Сохранить создаются по умолчанию hello **имя базы данных**.
* В поле **Имя строки подключения** введите *MyDbConnection*. Это имя должно соответствовать hello строку подключения, которая ссылается на *Models/MyDatabaseContext.cs*.
* Нажмите кнопку **ОК**.

![Настройка базы данных SQL](media/app-service-web-tutorial-dotnet-sqldatabase/configure-sql-database.png)

Hello **Создание приложения службы** диалоговое окно показывает hello ресурсов, вы создали. Щелкните **Создать**. 

![Hello ресурсы, которые вы создали](media/app-service-web-tutorial-dotnet-sqldatabase/app_svc_plan_done.png)

После завершения выполнения мастера hello, создание hello ресурсы Azure, он публикует вашей tooAzure приложения ASP.NET. Браузер по умолчанию запускается с toohello развернуть приложение hello URL-адрес. 

Добавьте несколько элементов списка дел.

![Опубликованное приложение ASP.NET в веб-приложении Azure](./media/app-service-web-tutorial-dotnet-sqldatabase/azure-app-in-browser.png)

Поздравляем! Вы запустили управляемое данными приложение ASP.NET в службе приложений Azure.

## <a name="access-hello-sql-database-locally"></a>Доступ к локально hello базы данных SQL

Visual Studio позволяет просматривать и управлять ими новой базы данных SQL в hello **обозреватель объектов SQL Server**.

### <a name="create-a-database-connection"></a>Создание подключения к базе данных

Из hello **представление** последовательно выберите пункты **обозреватель объектов SQL Server**.

Вверху hello **обозреватель объектов SQL Server**, нажмите кнопку hello **добавить SQL Server** кнопку.

### <a name="configure-hello-database-connection"></a>Подключение к базе данных hello

В hello **Connect** диалогового окна разверните hello **Azure** узла. Здесь перечислены все экземпляры базы данных SQL в Azure.

Выберите hello `DotNetAppSqlDb` базы данных SQL. внизу hello автоматически заполняется Hello подключение, которое было создано ранее.

Введите пароль администратора hello базы данных, созданной ранее и нажмите кнопку **Connect**.

![Настройка подключения к базе данных из Visual Studio](./media/app-service-web-tutorial-dotnet-sqldatabase/connect-to-sql-database.png)

### <a name="allow-client-connection-from-your-computer"></a>Разрешение клиентских подключений с вашего компьютера

Hello **Создание нового правила брандмауэра** открыть диалоговое окно. По умолчанию к экземпляру базы данных SQL могут подключаться только службы Azure, такие как ваше веб-приложение Azure. tooconnect tooyour базы данных, необходимо создать правила брандмауэра в экземпляр базы данных SQL hello. правило брандмауэра Hello допускает hello общедоступный IP-адрес локального компьютера.

диалоговое окно приветствия, уже заполненный общедоступный IP-адрес вашего компьютера.

Убедитесь, что флажок **Добавить IP-адрес моего клиента** установлен, и щелкните **ОК**. 

![Задание правила брандмауэра для экземпляра базы данных SQL](./media/app-service-web-tutorial-dotnet-sqldatabase/sql-set-firewall.png)

После завершения выполнения Visual Studio, создав hello параметр брандмауэра для экземпляра базы данных SQL, подключение отображается в **обозреватель объектов SQL Server**.

Здесь можно выполнять создание hello наиболее распространенные базы данных операций, например выполнения запросов, представлений и хранимых процедур и многое другое. 

Щелкните правой кнопкой мыши на hello `Todoes` таблицы и выберите **данные представления**. 

![Просмотр объектов базы данных SQL](./media/app-service-web-tutorial-dotnet-sqldatabase/explore-sql-database.png)

## <a name="update-app-with-code-first-migrations"></a>Изменение приложения с помощью Code First Migrations

Можно использовать знакомые средства hello в Visual Studio tooupdate базы данных и веб-приложения, в Azure. На этом шаге можно использовать миграции Code First в Entity Framework toomake изменение tooyour схемы базы данных, а также опубликовать tooAzure.

Дополнительные сведения об использовании Entity Framework Code First Migrations см. в статье [Getting Started with Entity Framework 6 Code First using MVC 5](https://docs.microsoft.com/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application) (Начало работы с Entity Framework 6 Code First с помощью MVC 5).

### <a name="update-your-data-model"></a>Обновление модели данных

Откройте _Models\Todo.cs_ в редакторе кода hello. Добавьте следующие свойства toohello hello `ToDo` класса:

```csharp
public bool Done { get; set; }
```

### <a name="run-code-first-migrations-locally"></a>Локальный запуск Code First Migrations

Запустите несколько команд toomake обновления tooyour локальной базы данных. 

Из hello **средства** меню, нажмите кнопку **диспетчера пакетов NuGet** > **консоль диспетчера пакетов**.

В hello в окне консоли диспетчера пакетов включите Code First Migrations:

```PowerShell
Enable-Migrations
```

Добавьте миграцию:

```PowerShell
Add-Migration AddProperty
```

Обновление hello локальной базы данных:

```PowerShell
Update-Database
```

Тип `Ctrl+F5` toorun приложение hello. Тест hello, редактирования и создать связи.

Если приложение hello загружается без ошибок, Code First Migrations завершилась успешно. Тем не менее содержатся в электронной таблице страницы по-прежнему hello таким же, так как логика приложения еще не использует это новое свойство. 

### <a name="use-hello-new-property"></a>Использовать новое свойство hello

Внести некоторые изменения в ваш код toouse hello `Done` свойство. Для простоты в этом учебнике только ты toochange hello `Index` и `Create` представления hello свойство toosee в действие.

Откройте файл _Controllers\TodosController.cs_.

Найти hello `Create()` метода и добавьте `Done` toohello список свойств в hello `Bind` атрибута. Когда закончите, ваш `Create()` сигнатура метода выглядит hello, следующий код:

```csharp
public ActionResult Create([Bind(Include = "id,Description,CreatedDate,Done")] Todo todo)
```

Откройте файл _Views\Todos\Create.cshtml_.

В hello кода Razor, вы увидите `<div class="form-group">` элемент, который использует `model.Description`и еще один `<div class="form-group">` элемент, который использует `model.CreatedDate`. Сразу после этих двух элементов добавьте еще один элемент `<div class="form-group">`, который использует `model.Done`:

```csharp
<div class="form-group">
    @Html.LabelFor(model => model.Done, htmlAttributes: new { @class = "control-label col-md-2" })
    <div class="col-md-10">
        <div class="checkbox">
            @Html.EditorFor(model => model.Done)
            @Html.ValidationMessageFor(model => model.Done, "", new { @class = "text-danger" })
        </div>
    </div>
</div>
```

Откройте файл _Views\Todos\Index.cshtml_.

Поиск hello пустой `<th></th>` элемента. Только что выше этого элемента добавьте после кода Razor hello:

```csharp
<th>
    @Html.DisplayNameFor(model => model.Done)
</th>
```

Найти hello `<td>` элемент, содержащий hello `Html.ActionLink()` вспомогательные методы. Только что выше этого элемента добавьте после кода Razor hello:

```csharp
<td>
    @Html.DisplayFor(modelItem => item.Done)
</td>
```

Вот и все необходимые изменения toosee hello в hello `Index` и `Create` представления. 

Тип `Ctrl+F5` toorun приложение hello.

Теперь вы сможете добавить элемент списка дел и установить флажок **Готово**. После этого задание должно появиться на главной странице как выполненное. Помните, что hello `Edit` представления не показывает hello `Done` поле, так как не были изменены hello `Edit` представления.

### <a name="enable-code-first-migrations-in-azure"></a>Включение Code First Migrations в Azure

Теперь, когда код работает, включая перенос базы данных изменений публикации его tooyour Azure веб-приложения и обновления базы данных SQL с помощью Code First Migrations слишком.

Как и прежде, щелкните правой кнопкой мыши свой проект и выберите **Опубликовать**.

Нажмите кнопку **параметры** tooopen hello мастер публикации.

![Открытие параметров публикации](./media/app-service-web-tutorial-dotnet-sqldatabase/publish-settings.png)

В мастере приветствия щелкните **Далее**.

Убедитесь, что эта строка подключения hello для заполнения базы данных SQL в **MyDatabaseContext (MyDbConnection)**. Может потребоваться tooselect hello **myToDoAppDb** базы данных из раскрывающегося списка hello. 

Установите флажок **Выполнять Code First Migrations (при запуске приложения)** и нажмите кнопку **Сохранить**.

![Включение Code First Migrations в веб-приложении Azure](./media/app-service-web-tutorial-dotnet-sqldatabase/enable-migrations.png)

### <a name="publish-your-changes"></a>Публикация изменений

Включив Code First Migrations в веб-приложении Azure, опубликуйте изменения кода.

Страница "Публикация" hello, щелкните **публикации**.

Попробуйте добавить новые задачи, устанавливая флажок **Готово**. Эти задачи должны появляться на главной странице как выполненные.

![Веб-приложение Azure после включения Code First Migrations](./media/app-service-web-tutorial-dotnet-sqldatabase/this-one-is-done.png)

Все имеющиеся элементы списка дел по-прежнему отображаются. При повторной публикации приложения ASP.NET существующие данные в базе данных SQL не теряются. Кроме того, Code First Migrations только изменения схемы данных hello и оставляет без изменений существующих данных.


## <a name="stream-application-logs"></a>Потоковая передача журналов приложений

Можно осуществлять потоковую передачу сообщений трассировки непосредственно из вашего Azure web app tooVisual Studio.

Откройте файл _Controllers\TodosController.cs_.

Каждое действие начинается с метода `Trace.WriteLine()`. Этот код добавляется tooshow вы способ трассировки tooadd сообщений tooyour веб-приложение Azure.

### <a name="open-server-explorer"></a>Откройте обозреватель сервера

Из hello **представление** последовательно выберите пункты **обозревателя серверов**. Ведение журнала для веб-приложения Azure можно включить в **обозревателе сервера**. 

### <a name="enable-log-streaming"></a>Включение потоковой передачи журналов

В **обозревателе сервера** выберите **Azure** > **Служба приложений**.

Разверните hello **myResourceGroup** группы ресурсов, созданный при первом создании hello Azure веб-приложения.

Щелкните веб-приложение правой кнопкой мыши и выберите **Просмотреть журналы потоковой передачи**.

![Включение потоковой передачи журналов](./media/app-service-web-tutorial-dotnet-sqldatabase/stream-logs.png)

Hello журналы теперь потока можно добиться hello **вывода** окна. 

![Потоковая передача журналов в окне "Выходные данные"](./media/app-service-web-tutorial-dotnet-sqldatabase/log-streaming-pane.png)

Тем не менее вы не видите сообщения трассировки hello еще. Который так, как при первом обращении **Просмотр журналов потоковой передачи**, Azure веб-приложение задает уровень трассировки hello слишком`Error`, какие только журналы событий ошибок (с hello `Trace.TraceError()` метода).

### <a name="change-trace-levels"></a>Изменение уровней трассировки

трассировки hello toochange уровни toooutput другие сообщения трассировки, перейдите назад слишком**обозревателя серверов**.

Снова щелкните веб-приложение правой кнопкой мыши и выберите **Параметры**.

В hello **ведение журнала приложения (файловая система)** раскрывающийся список, выберите **Verbose**. Щелкните **Сохранить**.

![Изменение уровня tooVerbose трассировки](./media/app-service-web-tutorial-dotnet-sqldatabase/trace-level-verbose.png)

> [!TIP]
> Можно поэкспериментировать с toosee уровни трассировки разные каких типов сообщений отображаются для каждого уровня. Здравствуйте, например, **сведения** уровень включает все журналы, созданные `Trace.TraceInformation()`, `Trace.TraceWarning()`, и `Trace.TraceError()`, но не журналы, созданные `Trace.WriteLine()`.
>
>

В браузере щелкните правой кнопкой мыши вокруг приложения список дел hello в Azure. сообщения трассировки Hello теперь потоком toohello **выходной** в Visual Studio.

```
Application: 2017-04-06T23:30:41  PID[8132] Verbose     GET /Todos/Index
Application: 2017-04-06T23:30:43  PID[8132] Verbose     GET /Todos/Create
Application: 2017-04-06T23:30:53  PID[8132] Verbose     POST /Todos/Create
Application: 2017-04-06T23:30:54  PID[8132] Verbose     GET /Todos/Index
```



### <a name="stop-log-streaming"></a>Выключение потоковой передачи журналов

toostop Здравствуйте потоковой передачи журнала службы, нажмите кнопку hello **Остановить наблюдение** кнопку в hello **вывода** окна.

![Выключение потоковой передачи журналов](./media/app-service-web-tutorial-dotnet-sqldatabase/stop-streaming.png)

## <a name="manage-your-azure-web-app"></a>Управление веб-приложением Azure

Go toohello [портал Azure](https://portal.azure.com) toosee hello веб-приложения был создан. 



Hello в левом меню, щелкните **службы приложений**, затем щелкните имя hello Azure веб-приложения.

![Веб-приложения портала навигации tooAzure](./media/app-service-web-tutorial-dotnet-sqldatabase/access-portal.png)

Вы попадете на страницу веб-приложения. 

По умолчанию hello портал отображает hello **Обзор** страницы. Здесь вы можете наблюдать за работой приложения. Вы также можете выполнять базовые задачи управления: обзор, завершение, запуск, перезагрузку и удаление. Hello вкладках hello левой части страницы приветствия отображаются страницы hello другой конфигурации, которые можно открыть. 

![Страница службы приложений на портале Azure](./media/app-service-web-tutorial-dotnet-sqldatabase/web-app-blade.png)

[!INCLUDE [Clean up section](../../includes/clean-up-section-portal-web-app.md)]

<a name="next"></a>

## <a name="next-steps"></a>Дальнейшие действия

Из этого руководства вы узнали, как выполнять такие задачи:

> [!div class="checklist"]
> * Создание базы данных SQL в Azure.
> * Подключение tooSQL приложения ASP.NET базы данных
> * Развертывание tooAzure приложения hello
> * Обновить модель данных hello и повторно развернуть приложение hello
> * Журналы Azure tooyour терминалов потока
> * Управление приложение hello в hello портал Azure

Переместить следующий учебник toolearn toohello как toomap пользовательские DNS имя toohello веб-приложения.

> [!div class="nextstepaction"]
> [Сопоставьте существующий пользовательский DNS имя tooAzure веб-приложений](app-service-web-tutorial-custom-domain.md)
