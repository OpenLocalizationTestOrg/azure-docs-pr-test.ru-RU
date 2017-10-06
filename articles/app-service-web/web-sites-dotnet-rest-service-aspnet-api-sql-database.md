---
title: "aaaCreate REST API в Azure с помощью ASP.NET и баз данных SQL Server | Документы Microsoft"
description: "Учебник, объясняется, как toodeploy приложения, использующего hello tooan ASP.NET Web API веб-приложение Azure с помощью Visual Studio."
services: app-service\web
documentationcenter: .net
author: Rick-Anderson
writer: Rick-Anderson
manager: erikre
editor: 
ms.assetid: f4916fc0-ea08-41f7-846b-73e41bc88149
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 02/29/2016
ms.author: riande
ms.openlocfilehash: 1ef45dd1582bfda367e53c39f863164422ad678b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-rest-service-using-aspnet-web-api-and-sql-database-in-azure-app-service"></a>Создание службы REST в службе приложений Azure с помощью веб-API ASP.NET и базы данных SQL
В этом учебнике показано, как toodeploy ASP.NET веб-приложения tooan [службе приложений Azure](http://go.microsoft.com/fwlink/?LinkId=529714) с помощью мастера публикации веб-сайта hello в Visual Studio 2013 или Visual Studio 2013 Community Edition. 

Можно открыть учетную запись Azure бесплатно, и если у вас еще нет Visual Studio 2013, hello SDK автоматически устанавливает Visual Studio 2013 для Web Express. Таким образом, вы можете начинать разработку на Azure абсолютно бесплатно.

В данном учебнике предполагается, что у читателя нет опыта использования платформы Azure. После завершения этого учебника, чтобы иметь простой веб-приложения вверх и работающих в облаке hello.

Вы узнаете:

* Как tooenable компьютер для разработки Azure, установив hello Azure SDK.
* Как toocreate Visual Studio ASP.NET MVC 5 проекта и опубликуйте его tooan приложения Azure.
* Каким образом вызывает toouse hello веб-API ASP.NET tooenable Restful API.
* Как toouse SQL базы данных toostore данные в Azure.
* Как приложение toopublish обновляет tooAzure.

Мы создадим простой список контактов веб-приложение, основанное на ASP.NET MVC 5 и использует hello ADO.NET Entity Framework для доступа к базе данных. следующие иллюстрации показано hello Hello завершения приложения:

![снимок экрана веб-сайта][intro001]

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

### <a name="create-hello-project"></a>Создание проекта hello
1. Откройте Visual Studio 2013.
2. Из hello **файл** меню **новый проект**.
3. В hello **новый проект** диалогового окна разверните **Visual C#** и выберите **Web** , а затем выберите **веб-приложение ASP.NET**. Имя приложения hello **ContactManager** и нажмите кнопку **ОК**.
   
    ![Диалоговое окно "Новый проект"](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rr4.png)
4. В hello **новый проект ASP.NET** диалоговое окно, выберите hello **MVC** шаблона, проверка **веб-API** и нажмите кнопку **изменить аутентификацию**.
5. В hello **изменить аутентификацию** диалоговое окно, нажмите кнопку **без проверки подлинности**, а затем нажмите кнопку **ОК**.
   
    ![Без аутентификации](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/GS13noauth.png)
   
    отсутствует функций, требующих toolog пользователей в пример приложения Hello, который вы создаете. Сведения о функции tooimplement проверки подлинности и авторизации, в разделе hello [дальнейшие действия](#nextsteps) раздел в конце hello этого учебника. 
6. В hello **новый проект ASP.NET** диалоговое окно, убедитесь, что hello **узлов в облаке hello** установлен флажок и нажмите кнопку **ОК**.

Если ранее вы не выполнялся в tooAzure, появится запрос toosign в.

1. Мастер настройки Hello предложит уникальным именем на основе *ContactManager* (см. ниже рисунке hello). Выберите ближайшую область. Можно использовать [azurespeed.com](http://www.azurespeed.com/ "AzureSpeed.com") toofind hello наименьшее задержки ЦОД. 
2. Если вы еще не создали сервер базы данных, нажмите **Создать новый сервер**, а затем укажите имя пользователя и пароль для базы данных.
   
    ![Настройка веб-сайта Azure](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/configAz.PNG)

Если сервер базы данных, используйте этот toocreate новую базу данных. Серверы баз данных являются ценным ресурсом, и обычно требуется toocreate несколько баз данных на hello один сервер для тестирования и разработки, а не создание сервера базы данных на базу данных. Убедитесь, что веб-сайта и базы данных находятся в hello одного региона.

![Настройка веб-сайта Azure](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/configWithDB.PNG)

### <a name="set-hello-page-header-and-footer"></a>Набор hello верхнего и нижнего колонтитула
1. В **обозревателе решений**, разверните hello *представления\общие* папку и откройте hello *_Layout.cshtml* файла.
   
    ![_Layout.cshtml в обозревателе решений][newapp004]
2. Замените содержимое hello hello *Views\Shared_Layout.cshtml* файл с hello, следующий код:

        <!DOCTYPE html>
        <html lang="en">
        <head>
            <meta charset="utf-8" />
            <title>@ViewBag.Title - Contact Manager</title>
            <link href="~/favicon.ico" rel="shortcut icon" type="image/x-icon" />
            <meta name="viewport" content="width=device-width" />
            @Styles.Render("~/Content/css")
            @Scripts.Render("~/bundles/modernizr")
        </head>
        <body>
            <header>
                <div class="content-wrapper">
                    <div class="float-left">
                        <p class="site-title">@Html.ActionLink("Contact Manager", "Index", "Home")</p>
                    </div>
                </div>
            </header>
            <div id="body">
                @RenderSection("featured", required: false)
                <section class="content-wrapper main-content clear-fix">
                    @RenderBody()
                </section>
            </div>
            <footer>
                <div class="content-wrapper">
                    <div class="float-left">
                        <p>&copy; @DateTime.Now.Year - Contact Manager</p>
                    </div>
                </div>
            </footer>
            @Scripts.Render("~/bundles/jquery")
            @RenderSection("scripts", required: false)
        </body>
        </html>

Hello разметки выше имя приложения hello изменения из «Мое приложение ASP.NET» слишком «диспетчера контактов», который удаляет ссылки hello слишком**Главная**, **о** и **контакт**.

### <a name="run-hello-application-locally"></a>Запустите приложение hello локально
1. Нажмите клавиши CTRL + F5 toorun hello приложения.
   Домашняя страница приложения Hello отображается в браузере по умолчанию hello.
    ![Домашняя страница tooDo списка](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rr5.png)

Это все, что нужно toodo для приложения hello toocreate сейчас, вы развернете tooAzure. Далее вы добавите функции для работы с базой данных.

## <a name="deploy-hello-application-tooazure"></a>Развертывание tooAzure приложения hello
1. В Visual Studio щелкните правой кнопкой мыши проект hello в **обозревателе решений** и выберите **публикации** hello контекстном меню.
   
    !["Опубликовать" в контекстном меню проекта][PublishVSSolution]
   
    Hello **веб-публикация** откроется мастер.
2. Щелкните **Опубликовать**.

![Вкладка "Параметры"](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/pw.png)

Visual Studio начинает процесс hello копирования файлов hello toohello сервера Azure. Hello **вывода** окно показывает выполненные действия развертывания и сообщает успешного завершения развертывания hello.

1. toohello URL-адрес сайта hello развертывания автоматически откроется в браузере по умолчанию Hello.
   
   созданное приложение Hello, теперь работает в облаке hello.
   
   ![Домашняя страница списка tooDo, работающие в Azure][rxz2]

## <a name="add-a-database-toohello-application"></a>Добавить приложение toohello базы данных
Затем будет обновлять hello MVC приложения tooadd hello возможность toodisplay и обновить контакты и хранить в базе данных hello. приложение Hello использовать hello Entity Framework toocreate hello database и tooread и обновления данных в базе данных hello.

### <a name="add-data-model-classes-for-hello-contacts"></a>Добавление классов модели данных для контактов, hello
Начните с создания простой модели данных в коде.

1. В **обозревателе решений**, щелкните правой кнопкой мыши папку Models hello, нажмите кнопку **добавить**, а затем **класса**.
   
    ![Контекстное меню добавления класса в папке "Модели"][adddb001]
2. В hello **Добавление нового элемента** диалоговое окно, новый файл класса имя hello *Contact.cs*, а затем нажмите кнопку **добавить**.
   
    ![Диалоговое окно "Добавление нового элемента"][adddb002]
3. Замените содержимое файла Contacts.cs hello hello hello, следующий код.
   
        using System.Globalization;
        namespace ContactManager.Models
        {
            public class Contact
               {
                public int ContactId { get; set; }
                public string Name { get; set; }
                public string Address { get; set; }
                public string City { get; set; }
                public string State { get; set; }
                public string Zip { get; set; }
                public string Email { get; set; }
                public string Twitter { get; set; }
                public string Self
                {
                    get { return string.Format(CultureInfo.CurrentCulture,
                         "api/contacts/{0}", this.ContactId); }
                    set { }
                }
            }
        }

Hello **обратитесь к** класс определяет hello данных, в которой будут храниться для каждого контактного лица, а также первичный ключ ContactID, необходимые для hello базы данных. Дополнительные сведения о моделях данных можно получить в hello [дальнейшие действия](#nextsteps) раздел в конце hello этого учебника.

### <a name="create-web-pages-that-enable-app-users-toowork-with-hello-contacts"></a>Создание веб-страницы, позволяющие toowork пользователей приложения с контактами hello
Hello функции формирования шаблонов hello ASP.NET MVC можно автоматически создавать код, выполняющий создание, чтение, обновление и удаление (CRUD) действия.

## <a name="add-a-controller-and-a-view-for-hello-data"></a>Добавление контроллера и представления для данных hello
1. В **обозревателе решений**, разверните папку Controllers hello.
2. Построение проекта hello **(Ctrl + Shift + B)**. (Перед использованием механизма формирования шаблонов необходимо построить проект hello.) 
3. Щелкните правой кнопкой мыши папку Controllers hello и нажмите кнопку **добавить**, а затем нажмите кнопку **контроллера**.
   
    ![Контекстное меню добавления контроллера в папке "Контроллеры"][addcode001]
4. В hello **Добавление формирования шаблонов** выберите **контроллер MVC с представлениями, использующий Entity Framework** и нажмите кнопку **добавить**.
   
   ![Добавление контролера](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rrAC.png)
5. Задайте имя контроллера hello слишком**HomeController**. Выберите класс модели **Contact** . Нажмите кнопку hello **новый контекст данных** кнопку и примите значение по умолчанию hello «ContactManager.Models.ContactManagerContext» для hello **новый тип контекста данных**. Щелкните **Добавить**.

    Диалоговое окно предложит: «файл с именем hello HomeController уже существует. Вы хотите tooreplace его?». Щелкните **Да**. Мы — это перезапись hello Главная контроллера, который был создан с новым проектом hello. Мы будем использовать hello новый Главная контроллера списка контактов.

    Visual Studio создает методы и представления контроллера для операций создания, чтения, обновления и удаления в базе данных для объектов **Contact** .

## <a name="enable-migrations-create-hello-database-add-sample-data-and-a-data-initializer"></a>Включить миграцию, создание hello базы данных, добавить образец данных и инициализаторов данных
Следующая задача Hello — tooenable hello [Code First Migrations](http://curah.microsoft.com/55220) функции в базе данных hello toocreate заказа на основании созданная модель hello.

1. В hello **средства** последовательно выберите пункты **диспетчер пакетов библиотеки** и затем **консоль диспетчера пакетов**.
   
    !["Консоль диспетчера пакетов" в меню "Сервис"][addcode008]
2. В hello **консоль диспетчера пакетов** окно, введите следующую команду hello:
   
        enable-migrations 
   
    Hello **enable-migrations** команда создает *миграций* папке и ее помещает в этой папке *Configuration.cs* tooconfigure миграции можно редактировать файл. 
3. В hello **консоль диспетчера пакетов** окно, введите следующую команду hello:
   
        add-migration Initial
   
    Hello **добавьте миграции исходного** команда создает класс с именем  **&lt;date_stamp&gt;начальной** , создает базу данных hello. Здравствуйте, первый параметр ( *начальной* ) — имя hello toocreate произвольный и используемого файла hello. Для просмотра файлов новый класс hello в **обозревателе решений**.
   
    В hello **начальной** класса hello **копирование** метод создает таблицы Contacts hello и hello **работу** метод (используется, если предыдущее состояние toohello tooreturn) удаляется.
4. Откройте hello *Migrations\Configuration.cs* файла. 
5. Добавьте следующие пространства имен hello. 
   
         using ContactManager.Models;
6. Замените hello *начальное значение* метод с hello, следующий код:
   
        protected override void Seed(ContactManager.Models.ContactManagerContext context)
        {
            context.Contacts.AddOrUpdate(p => p.Name,
               new Contact
               {
                   Name = "Debra Garcia",
                   Address = "1234 Main St",
                   City = "Redmond",
                   State = "WA",
                   Zip = "10999",
                   Email = "debra@example.com",
                   Twitter = "debra_example"
               },
                new Contact
                {
                    Name = "Thorsten Weinrich",
                    Address = "5678 1st Ave W",
                    City = "Redmond",
                    State = "WA",
                    Zip = "10999",
                    Email = "thorsten@example.com",
                    Twitter = "thorsten_example"
                },
                new Contact
                {
                    Name = "Yuhong Li",
                    Address = "9012 State st",
                    City = "Redmond",
                    State = "WA",
                    Zip = "10999",
                    Email = "yuhong@example.com",
                    Twitter = "yuhong_example"
                },
                new Contact
                {
                    Name = "Jon Orton",
                    Address = "3456 Maple St",
                    City = "Redmond",
                    State = "WA",
                    Zip = "10999",
                    Email = "jon@example.com",
                    Twitter = "jon_example"
                },
                new Contact
                {
                    Name = "Diliana Alexieva-Bosseva",
                    Address = "7890 2nd Ave E",
                    City = "Redmond",
                    State = "WA",
                    Zip = "10999",
                    Email = "diliana@example.com",
                    Twitter = "diliana_example"
                }
                );
        }
   
    Приведенный выше код инициализирует hello базы данных с hello контактные данные. Дополнительные сведения о заполнения hello базы данных см. в разделе [отладки Entity Framework (EF) баз данных SQL Server](http://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx).
7. В hello **консоль диспетчера пакетов** введите команду hello:
   
        update-database
   
    ![Команды консоли диспетчера пакетов][addcode009]
   
    Hello **базы данных обновления** запусков hello первый миграции, который создает базу данных hello. По умолчанию hello базы данных создается как база данных SQL Server Express LocalDB.
8. Нажмите клавиши CTRL + F5 toorun hello приложения. 

приложение Hello hello начальное значение данных и поле редактирования, сведения и ссылки для удаления.

![Представление MVC для данных][rxz3]

## <a name="edit-hello-view"></a>Изменить представление hello
1. Откройте hello *Views\Home\Index.cshtml* файла. В следующем шаге hello мы заменит разметки hello созданный код, использующий [jQuery](http://jquery.com/) и [Knockout.js](http://knockoutjs.com/). Этот новый код извлекает список контактов, hello с помощью веб-API и JSON, а затем привязывает hello обратитесь в службу данных toohello пользовательского интерфейса с помощью knockout.js. Дополнительные сведения см. в разделе hello [дальнейшие действия](#nextsteps) раздел в конце hello этого учебника. 
2. Замените содержимое файла hello hello hello, следующий код.
   
        @model IEnumerable<ContactManager.Models.Contact>
        @{
            ViewBag.Title = "Home";
        }
        @section Scripts {
            @Scripts.Render("~/bundles/knockout")
            <script type="text/javascript">
                function ContactsViewModel() {
                    var self = this;
                    self.contacts = ko.observableArray([]);
                    self.addContact = function () {
                        $.post("api/contacts",
                            $("#addContact").serialize(),
                            function (value) {
                                self.contacts.push(value);
                            },
                            "json");
                    }
                    self.removeContact = function (contact) {
                        $.ajax({
                            type: "DELETE",
                            url: contact.Self,
                            success: function () {
                                self.contacts.remove(contact);
                            }
                        });
                    }
   
                    $.getJSON("api/contacts", function (data) {
                        self.contacts(data);
                    });
                }
                ko.applyBindings(new ContactsViewModel());    
        </script>
        }
        <ul id="contacts" data-bind="foreach: contacts">
            <li class="ui-widget-content ui-corner-all">
                <h1 data-bind="text: Name" class="ui-widget-header"></h1>
                <div><span data-bind="text: $data.Address || 'Address?'"></span></div>
                <div>
                    <span data-bind="text: $data.City || 'City?'"></span>,
                    <span data-bind="text: $data.State || 'State?'"></span>
                    <span data-bind="text: $data.Zip || 'Zip?'"></span>
                </div>
                <div data-bind="if: $data.Email"><a data-bind="attr: { href: 'mailto:' + Email }, text: Email"></a></div>
                <div data-bind="ifnot: $data.Email"><span>Email?</span></div>
                <div data-bind="if: $data.Twitter"><a data-bind="attr: { href: 'http://twitter.com/' + Twitter }, text: '@@' + Twitter"></a></div>
                <div data-bind="ifnot: $data.Twitter"><span>Twitter?</span></div>
                <p><a data-bind="attr: { href: Self }, click: $root.removeContact" class="removeContact ui-state-default ui-corner-all">Remove</a></p>
            </li>
        </ul>
        <form id="addContact" data-bind="submit: addContact">
            <fieldset>
                <legend>Add New Contact</legend>
                <ol>
                    <li>
                        <label for="Name">Name</label>
                        <input type="text" name="Name" />
                    </li>
                    <li>
                        <label for="Address">Address</label>
                        <input type="text" name="Address" >
                    </li>
                    <li>
                        <label for="City">City</label>
                        <input type="text" name="City" />
                    </li>
                    <li>
                        <label for="State">State</label>
                        <input type="text" name="State" />
                    </li>
                    <li>
                        <label for="Zip">Zip</label>
                        <input type="text" name="Zip" />
                    </li>
                    <li>
                        <label for="Email">E-mail</label>
                        <input type="text" name="Email" />
                    </li>
                    <li>
                        <label for="Twitter">Twitter</label>
                        <input type="text" name="Twitter" />
                    </li>
                </ol>
                <input type="submit" value="Add" />
            </fieldset>
        </form>
3. Щелкните правой кнопкой мыши папку содержимого hello и нажмите кнопку **добавить**, а затем нажмите кнопку **новый элемент...** .
   
    ![Добавление таблицы стилей в контекстном меню папки Content][addcode005]
4. В hello **Добавление нового элемента** диалогового окна введите **стиль** в hello поле верхнего правого поиска, а затем выберите **стилей**.
    ![Диалоговое окно "Добавление нового элемента"][rxStyle]
5. Имя файла hello *Contacts.css* и нажмите кнопку **добавить**. Замените содержимое файла hello hello hello, следующий код.
   
        .column {
            float: left;
            width: 50%;
            padding: 0;
            margin: 5px 0;
        }
        form ol {
            list-style-type: none;
            padding: 0;
            margin: 0;
        }
        form li {
            padding: 1px;
            margin: 3px;
        }
        form input[type="text"] {
            width: 100%;
        }
        #addContact {
            width: 300px;
            float: left;
            width:30%;
        }
        #contacts {
            list-style-type: none;
            margin: 0;
            padding: 0;
            float:left;
            width: 70%;
        }
        #contacts li {
            margin: 3px 3px 3px 0;
            padding: 1px;
            float: left;
            width: 300px;
            text-align: center;
            background-image: none;
            background-color: #F5F5F5;
        }
        #contacts li h1
        {
            padding: 0;
            margin: 0;
            background-image: none;
            background-color: Orange;
            color: White;
            font-family: Trebuchet MS, Tahoma, Verdana, Arial, sans-serif;
        }
        .removeContact, .viewImage
        {
            padding: 3px;
            text-decoration: none;
        }
   
    Мы будем использовать данную таблицу стилей для hello макета, цветов и стилей, используемых в приложение диспетчера контактов hello.
6. Откройте hello *App_Start\BundleConfig.cs* файла.
7. Добавьте следующий код tooregister hello hello [Knockout](http://knockoutjs.com/index.html "KO") подключаемого модуля.
   
        bundles.Add(new ScriptBundle("~/bundles/knockout").Include(
                    "~/Scripts/knockout-{version}.js"));
    В этом примере с помощью knockout toosimplify динамический код JavaScript, который обрабатывает шаблоны экран приветствия.
8. Изменить запись tooregister hello содержимое/css hello *contacts.css* таблицы стилей. Изменить hello, следующей строкой:
   
                 bundles.Add(new StyleBundle("~/Content/css").Include(
                   "~/Content/bootstrap.css",
                   "~/Content/site.css"));
   на:
   
        bundles.Add(new StyleBundle("~/Content/css").Include(
                   "~/Content/bootstrap.css",
                   "~/Content/contacts.css",
                   "~/Content/site.css"));
9. В hello консоль диспетчера пакетов выполните следующие команды tooinstall маскирования hello.
   
        Install-Package knockoutjs

## <a name="add-a-controller-for-hello-web-api-restful-interface"></a>Добавить контроллер Web API Restful интерфейса hello
1. В **обозревателе решений** щелкните правой кнопкой мыши папку Controllers и выберите **Добавить**, а затем щелкните **Контроллер...**. 
2. В hello **Добавление формирования шаблонов** диалогового окна введите **Web API 2 контроллер с действиями, использующий Entity Framework** и нажмите кнопку **добавить**.
   
    ![Добавление контролера API](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rt1.png)
3. В hello **добавить контроллер** диалогового окна введите «ContactsController» в качестве имени контроллера. Выберите «Contact (ContactManager.Models)» для hello **класс модели**.  Оставьте значение по умолчанию hello hello **класс контекста данных**. 
4. Щелкните **Добавить**.

### <a name="run-hello-application-locally"></a>Запустите приложение hello локально
1. Нажмите клавиши CTRL + F5 toorun hello приложения.
   
    ![Страница индексации][intro001]
2. Введите контакт и нажмите кнопку **Добавить**. приложение Hello возвращает toohello домашней страницы и отображает hello контакт введенный.
   
    ![Страница индексации с элементами списка дел][addwebapi004]
3. В браузере hello append **контактов/api/** toohello URL-адрес.
   
    Полученный Hello URL-адрес будет похоже на http://localhost:1234/api/контактов. веб-RESTful Hello API, которые вы добавили возвращает контакты хранятся hello. Hello данные будут отображаться Firefox и Chrome в формате XML.
   
    ![Страница индексации с элементами списка дел][rxFFchrome]

    IE будет предложен tooopen или сохранять контакты hello.

    ![Диалоговое окно сохранения веб-интерфейса API][addwebapi006]


    Вы можете открыть hello возвращается контактов в блокноте или в браузере.

    Эти выходные данные могут использоваться другим приложением, например мобильной веб-страницей или приложением.

    ![Диалоговое окно сохранения веб-интерфейса API][addwebapi007]

    **Предупреждение системы безопасности**: на этом этапе приложение является небезопасной и уязвимым tooCSRF атаки. Далее в учебнике hello удалит эту уязвимость. Чтобы узнать больше, ознакомьтесь с [предотвращением атак с подделкой межсайтовых запросов (CSRF)][prevent-csrf-attacks].
## <a name="add-xsrf-protection"></a>Добавление защиты XSRF
Подделки межсайтовых запросов (также известный как XSRF или CSRF) — это атака, для приложений веб сервере, при котором вредоносный веб-сайт может повлиять на взаимодействие hello браузер клиента и веб-сайта, которым доверяет этот браузер. Такие атаки становится возможным, так как веб-браузеры будет отправлять маркеры проверки подлинности автоматически с каждым веб-сайтом tooa запроса. Типичный пример Hello — файл cookie проверки подлинности, например ASP. Билет проверки подлинности форм в NET. Однако веб-сайты, использующие любой надежный способ проверки подлинности (например, Windows Authentication, Basic и т.п.), также могут стать целью таких атак.

Атака XSRF отличается от фишинговой атаки. Фишинг-атаках требуют взаимодействия из hello жертвы. В фишинга вредоносный веб-сайт будет имитировать hello целевой веб-сайт и жертвы hello верьте обеспечить злоумышленник toohello конфиденциальные сведения. При атаке XSRF обычно имеется без участия необходимые из hello жертвы. Вместо этого он hello полагается на автоматическую отправку веб-сайта назначения toohello все соответствующие файлы cookie браузера hello.

Дополнительные сведения см. в разделе hello [откройте проект безопасности веб-приложения](https://www.owasp.org/index.php/Main_Page) (OWASP) [XSRF](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_\(CSRF\)).

1. В **обозревателе решений** щелкните правой кнопкой **ContactManager**, затем щелкните **Добавить** и **Класс**.
2. Имя файла hello *ValidateHttpAntiForgeryTokenAttribute.cs* и добавить hello, следующий код:
   
        using System;
        using System.Collections.Generic;
        using System.Linq;
        using System.Net;
        using System.Net.Http;
        using System.Web.Helpers;
        using System.Web.Http.Controllers;
        using System.Web.Http.Filters;
        using System.Web.Mvc;
        namespace ContactManager.Filters
        {
            public class ValidateHttpAntiForgeryTokenAttribute : AuthorizationFilterAttribute
            {
                public override void OnAuthorization(HttpActionContext actionContext)
                {
                    HttpRequestMessage request = actionContext.ControllerContext.Request;
                    try
                    {
                        if (IsAjaxRequest(request))
                        {
                            ValidateRequestHeader(request);
                        }
                        else
                        {
                            AntiForgery.Validate();
                        }
                    }
                    catch (HttpAntiForgeryException e)
                    {
                        actionContext.Response = request.CreateErrorResponse(HttpStatusCode.Forbidden, e);
                    }
                }
                private bool IsAjaxRequest(HttpRequestMessage request)
                {
                    IEnumerable<string> xRequestedWithHeaders;
                    if (request.Headers.TryGetValues("X-Requested-With", out xRequestedWithHeaders))
                    {
                        string headerValue = xRequestedWithHeaders.FirstOrDefault();
                        if (!String.IsNullOrEmpty(headerValue))
                        {
                            return String.Equals(headerValue, "XMLHttpRequest", StringComparison.OrdinalIgnoreCase);
                        }
                    }
                    return false;
                }
                private void ValidateRequestHeader(HttpRequestMessage request)
                {
                    string cookieToken = String.Empty;
                    string formToken = String.Empty;
                    IEnumerable<string> tokenHeaders;
                    if (request.Headers.TryGetValues("RequestVerificationToken", out tokenHeaders))
                    {
                        string tokenValue = tokenHeaders.FirstOrDefault();
                        if (!String.IsNullOrEmpty(tokenValue))
                        {
                            string[] tokens = tokenValue.Split(':');
                            if (tokens.Length == 2)
                            {
                                cookieToken = tokens[0].Trim();
                                formToken = tokens[1].Trim();
                            }
                        }
                    }
                    AntiForgery.Validate(cookieToken, formToken);
                }
            }
        }
3. Добавьте следующее hello *с помощью* toohello инструкции контракты контроллера, у вас есть доступ toohello **[ValidateHttpAntiForgeryToken]** атрибута.
   
        using ContactManager.Filters;
4. Добавить hello **[ValidateHttpAntiForgeryToken]** атрибута toohello методы Post hello **ContactsController** tooprotect его от XSRF угроз. Вы добавите toohello «PutContact», «PostContact» и **DeleteContact** методы действий.
   
        [ValidateHttpAntiForgeryToken]
            public IHttpActionResult PutContact(int id, Contact contact)
            {
5. Обновление hello *сценариев* раздел hello *Views\Home\Index.cshtml* файл tooinclude кода tooget hello XSRF маркеры.
   
         @section Scripts {
            @Scripts.Render("~/bundles/knockout")
            <script type="text/javascript">
                @functions{
                   public string TokenHeaderValue()
                   {
                      string cookieToken, formToken;
                      AntiForgery.GetTokens(null, out cookieToken, out formToken);
                      return cookieToken + ":" + formToken;                
                   }
                }
   
               function ContactsViewModel() {
                  var self = this;
                  self.contacts = ko.observableArray([]);
                  self.addContact = function () {
   
                     $.ajax({
                        type: "post",
                        url: "api/contacts",
                        data: $("#addContact").serialize(),
                        dataType: "json",
                        success: function (value) {
                           self.contacts.push(value);
                        },
                        headers: {
                           'RequestVerificationToken': '@TokenHeaderValue()'
                        }
                     });
   
                  }
                  self.removeContact = function (contact) {
                     $.ajax({
                        type: "DELETE",
                        url: contact.Self,
                        success: function () {
                           self.contacts.remove(contact);
                        },
                        headers: {
                           'RequestVerificationToken': '@TokenHeaderValue()'
                        }
   
                     });
                  }
   
                  $.getJSON("api/contacts", function (data) {
                     self.contacts(data);
                  });
               }
               ko.applyBindings(new ContactsViewModel());
            </script>
         }

## <a name="publish-hello-application-update-tooazure-and-sql-database"></a>Опубликовать tooAzure обновление приложения hello и базы данных SQL
приложение hello toopublish, повторите hello процедуры, которые описаны выше.

1. В **обозревателе решений**, щелкните правой кнопкой мыши проект hello и выберите **публикации**.
   
    ![Опубликовать][rxP]
2. Нажмите кнопку hello **параметры** вкладки.
3. В разделе **ContactsManagerContext(ContactsManagerContext)**, щелкните hello **v** toochange значок *строку подключения к удаленному* toohello строку подключения для контактов, hello База данных. Щелкните **ContactDB**.
   
    ![данных](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rt5.png)
4. Установите флажок "hello" для **выполнять миграции Code First (запускается при запуске приложения)**.
5. Щелкните **Далее**, затем — **Предварительный просмотр**. Visual Studio отображает список файлов hello, которые будут добавлены или обновлены.
6. Щелкните **Опубликовать**.
   После завершения развертывания hello hello браузера откроется toohello Домашняя страница приложения hello.
   
    ![Страница индексации без контактов][intro001]
   
    Hello Visual Studio опубликовать строки подключения автоматически настроить процесс hello в развертывании hello *Web.config* toopoint toohello файл SQL-базы данных. Он также настроен Code First Migrations tooautomatically hello обновления базы данных toohello последней версии hello первое время hello приложение обращается к hello базы данных после развертывания.
   
    В результате этой конфигурации Code First hello база данных создана путем выполнения кода hello в hello **начальной** класса, которое было создано ранее. После развертывания было этой hello первый раз hello пытался tooaccess hello базы данных приложения.
7. Ввести контакт, как при запуске локально, приложение hello tooverify об успешном выполнении развертывания базы данных.

При появлении этого элемента Привет вводимых вами сохраняется и отображается на странице приветствия диспетчера контактов, вы знаете, хранящихся в базе данных hello.

![Страница индексации с контактами][addwebapi004]

приложение Hello теперь работает в облаке hello toostore базы данных SQL с использованием его данных. После завершения тестирования приложения hello в Azure, удалите его. приложение Hello является открытым и не имеет доступа toolimit механизм.

> [!NOTE]
> Tooget работы в службе приложений Azure перед регистрацией учетную запись Azure, перейдите слишком[повторите служб приложений](https://azure.microsoft.com/try/app-service/), в котором можно немедленно создать кратковременных начальный веб-приложения в службе приложений. Никаких кредитных карт и обязательств.
> 
> 

## <a name="next-steps"></a>Дальнейшие действия
Другой как toostore данные в приложении Azure — toouse хранилища Azure, предоставляемый хранения нереляционных данных в форме hello больших двоичных объектов и таблиц. Привет, следующие ссылки предоставляют дополнительные сведения по веб-API, ASP.NET MVC и Windows Azure.

* [Начало работы с Entity Framework 6 Code First с помощью MVC 5][EFCodeFirstMVCTutorial]
* [Начальный tooASP.NET MVC 5](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started)
* [Первое приложение веб-интерфейса API ASP.NET](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api)
* [Отладка WAWS](web-sites-dotnet-troubleshoot-visual-studio.md)

В этом образце приложения hello и учебных было написано с [Рик Андерсон](http://blogs.msdn.com/b/rickandy/) (Twitter [ @RickAndMSFT ](https://twitter.com/RickAndMSFT)) с помощью Tom Dykstra и Барри Dorrans (Twitter [ @blowdart ](https://twitter.com/blowdart)). 

Оставьте отзыв на что вам понравилось или что хотелось бы toosee улучшены, не только о учебника hello сам, но также и о продуктах hello, он демонстрирует. Ваши отзывы помогут нам определить, какие улучшения наиболее приоритетные. Нас интересуют особенно узнать о том, сколько процентная существует находится в большей автоматизации процесса hello, настройки и развертывания базы данных членства hello. 

## <a name="whats-changed"></a>Изменения
* Toohello руководство изменений из tooApp веб-сайтов службы. в разделе: [службе приложений Azure и ее влияние на существующие службы Azure](http://go.microsoft.com/fwlink/?LinkId=529714)

<!-- bookmarks -->
[Add an OAuth Provider]: #addOauth
[Add Roles toohello Membership Database]:#mbrDB
[Create a Data Deployment Script]:#ppd
[Update hello Membership Database]:#ppd2
[setupdbenv]: #bkmk_setupdevenv
[setupwindowsazureenv]: #bkmk_setupwindowsazure
[createapplication]: #bkmk_createmvc4app
[deployapp1]: #bkmk_deploytowindowsazure1
[adddb]: #bkmk_addadatabase
[addcontroller]: #bkmk_addcontroller
[addwebapi]: #bkmk_addwebapi
[deploy2]: #bkmk_deploydatabaseupdate

<!-- links -->
[EFCodeFirstMVCTutorial]: http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application
[dbcontext-link]: http://msdn.microsoft.com/library/system.data.entity.dbcontext(v=VS.103).aspx


<!-- images-->
[rxE]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxE.png
[rxP]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxP.png
[rx22]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/
[rxb2]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxb2.png
[rxz]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxz.png
[rxzz]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxzz.png
[rxz2]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxz2.png
[rxz3]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxz3.png
[rxStyle]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxStyle.png
[rxz4]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxz4.png
[rxz44]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxz44.png
[rxNewCtx]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxNewCtx.png
[rxPrevDB]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxPrevDB.png
[rxOverwrite]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxOverwrite.png
[rxPWS]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxPWS.png
[rxNewCtx]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxNewCtx.png
[rxAddApiController]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxAddApiController.png
[rxFFchrome]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxFFchrome.png
[intro001]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobil-intro-finished-web-app.png
[rxCreateWSwithDB]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxCreateWSwithDB.png
[setup007]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-setup-azure-site-004.png
[setup009]: ../Media/dntutmobile-setup-azure-site-006.png
[newapp002]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-createapp-002.png
[newapp004]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-createapp-004.png
[firsdeploy007]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-deploy1-publish-005.png
[firsdeploy009]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-deploy1-publish-007.png
[adddb001]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-adddatabase-001.png
[adddb002]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-adddatabase-002.png
[addcode001]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-controller-add-context-menu.png
[addcode002]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-controller-add-controller-dialog.png
[addcode004]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-controller-modify-index-context.png
[addcode005]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-controller-add-contents-context-menu.png
[addcode007]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-controller-modify-bundleconfig-context.png
[addcode008]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-migrations-package-manager-menu.png
[addcode009]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-migrations-package-manager-console.png
[addwebapi004]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-webapi-added-contact.png
[addwebapi006]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-webapi-save-returned-contacts.png
[addwebapi007]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-webapi-contacts-in-notepad.png
[Add XSRF Protection]: #xsrf
[WebPIAzureSdk20NetVS12]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/WebPIAzureSdk20NetVS12.png
[Add XSRF Protection]: #xsrf
[ImportPublishSettings]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/ImportPublishSettings.png
[ImportPublishProfile]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/ImportPublishProfile.png
[PublishVSSolution]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/PublishVSSolution.png
[ValidateConnection]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/ValidateConnection.png
[WebPIAzureSdk20NetVS12]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/WebPIAzureSdk20NetVS12.png
[prevent-csrf-attacks]: http://www.asp.net/web-api/overview/security/preventing-cross-site-request-forgery-(csrf)-attacks

