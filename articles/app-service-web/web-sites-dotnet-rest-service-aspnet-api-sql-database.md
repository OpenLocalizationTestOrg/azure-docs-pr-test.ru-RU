---
title: "Создание REST API в Azure с использованием ASP.NET и Базы данных SQL | Документация Майкрософт"
description: "Учебник, в котором показано развертывание приложения, использующего веб-API ASP.NET, в веб-приложении Azure с помощью Visual Studio."
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
ms.openlocfilehash: 64c18f2cfabbb7af6ffd89b4c2a9095fca1cf799
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-rest-service-using-aspnet-web-api-and-sql-database-in-azure-app-service"></a>Создание службы REST в службе приложений Azure с помощью веб-API ASP.NET и базы данных SQL
В этом учебнике показано, как развернуть веб-приложение ASP.NET в [службе приложений Azure](http://go.microsoft.com/fwlink/?LinkId=529714) с помощью мастера публикации веб-сайта в Visual Studio 2013 или Visual Studio 2013 Community Edition. 

Можно бесплатно создать учетную запись Azure, а если у вас еще нет Visual Studio 2013, то пакет SDK автоматически установит Visual Studio 2013 для Web Express. Таким образом, вы можете начинать разработку на Azure абсолютно бесплатно.

В данном учебнике предполагается, что у читателя нет опыта использования платформы Azure. После выполнения этого учебника вы получите простое веб-приложение, работающее в облаке.

Вы узнаете:

* Как подготовить компьютер к разработке для Azure путем установки пакета Azure SDK.
* Как создать проект Visual Studio ASP.NET MVC 5 и опубликовать его в приложении Azure.
* Как использовать веб-API ASP.NET для включения вызовов API Restful.
* Как использовать базу данных SQL для хранения данных в Azure.
* Как публиковать обновления приложений в Azure.

Вы создадите простое веб-приложение со списком контактов на платформе ASP.NET MVC 5 и использующее ADO.NET Entity Framework для доступа к базе данных. На следующем рисунке показано завершенное приложение:

![снимок экрана веб-сайта][intro001]

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

### <a name="create-the-project"></a>Создание проекта
1. Откройте Visual Studio 2013.
2. В меню **Файл** выберите **Новый проект**.
3. В диалоговом окне **Новый проект** разверните узел **Visual C#**, выберите **Веб**, а затем — **Веб-приложение ASP.NET**. Присвойте приложению имя **ContactManager** и нажмите кнопку **ОК**.
   
    ![Диалоговое окно "Новый проект"](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rr4.png)
4. В диалоговом окне **Новый проект ASP.NET** выберите шаблон **MVC**, установите флажок **Веб-API**, а затем щелкните **Изменить аутентификацию**.
5. В диалоговом окне **Изменить способ проверки подлинности** установите переключатель **Без проверки подлинности** и нажмите кнопку **ОК**.
   
    ![Без аутентификации](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/GS13noauth.png)
   
    В создаваемом образце приложения не будет функций, которые будут требовать от пользователя входа в систему. Для получения сведений об использовании функций аутентификации и авторизации см. раздел [Дальнейшие шаги](#nextsteps) в конце этого руководства. 
6. В диалоговом окне **Новый проект ASP.NET** убедитесь, что флажок **Разместить в облаке** установлен, и нажмите кнопку **ОК**.

Если вы еще не вошли в Azure, появится запрос на ввод учетных данных.

1. Мастер настройки предложит уникальное имя на основе *ContactManager* (см. рисунок ниже). Выберите ближайшую область. Поиск центра обработки данных с наименьшим временем задержки можно выполнить с помощью сайта [azurespeed.com](http://www.azurespeed.com/ "AzureSpeed.com"). 
2. Если вы еще не создали сервер базы данных, нажмите **Создать новый сервер**, а затем укажите имя пользователя и пароль для базы данных.
   
    ![Настройка веб-сайта Azure](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/configAz.PNG)

Если у вас есть сервер баз данных, используйте его для создания новой базы данных. Серверы баз данных являются ценным ресурсом, и обычно удобнее создать сразу несколько баз данных на одном сервере для тестирования и разработки, чем создавать по одному серверу на каждую базу данных. Убедитесь, что веб-сайт и базы данных находятся в одном регионе.

![Настройка веб-сайта Azure](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/configWithDB.PNG)

### <a name="set-the-page-header-and-footer"></a>Задание верхнего и нижнего колонтитула страницы
1. В **обозревателе решений** разверните папку *Views\Shared* и откройте файл *_Layout.cshtml*.
   
    ![_Layout.cshtml в обозревателе решений][newapp004]
2. Замените содержимое файла *Views\Shared_Layout.cshtml* кодом, приведенным ниже.

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

Приведенный выше код разметки позволяет изменить имя приложения с "Мое приложение ASP.NET" на "Диспетчер контактов" и удаляет ссылки на **главную** страницу, а также страницы **сведений** и **контактной информации**.

### <a name="run-the-application-locally"></a>Локальный запуск приложения
1. Для запуска приложения нажмите сочетание клавиш CTRL+F5.
   Главная страница приложения откроется в браузере, используемом по умолчанию.
    ![Главная страница списка дел](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rr5.png)

Это все, что требуется для создания приложения, которое будет развернуто в Azure. Далее вы добавите функции для работы с базой данных.

## <a name="deploy-the-application-to-azure"></a>Развертывание приложения в Azure
1. В Visual Studio щелкните правой кнопкой мыши проект в **обозревателе решений** и выберите **Опубликовать** в контекстном меню.
   
    !["Опубликовать" в контекстном меню проекта][PublishVSSolution]
   
    Откроется мастер **Публикация веб-сайта** .
2. Щелкните **Опубликовать**.

![Вкладка "Параметры"](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/pw.png)

Visual Studio начнет процесс копирования файлов в Azure. В окне **Вывод** указывается, какие действия по развертыванию были выполнены, а также сообщается об успешном завершении развертывания.

1. Браузер по умолчанию автоматически открывает URL-адрес развернутого сайта.
   
   Созданное вами приложение теперь выполняется в облаке.
   
   ![Главная страница списка дел на ресурсе Azure][rxz2]

## <a name="add-a-database-to-the-application"></a>Добавление базы данных в приложение
Далее вы обновите MVC-приложение, чтобы добавить отображение и изменение контактов, а также функции сохранения информации в базе данных. Это приложение для создания базы данных, чтения и обновления информации, содержащейся в ней, будет использовать платформу Entity Framework.

### <a name="add-data-model-classes-for-the-contacts"></a>Добавление классов модели данных для контактов
Начните с создания простой модели данных в коде.

1. В **обозревателе решений** щелкните правой кнопкой мыши папку "Модели" и выберите **Добавить**, а затем щелкните **Класс**.
   
    ![Контекстное меню добавления класса в папке "Модели"][adddb001]
2. В диалоговом окне **Добавление нового элемента** присвойте новому файлу класса имя *Contact.cs*, затем щелкните **Добавить**.
   
    ![Диалоговое окно "Добавление нового элемента"][adddb002]
3. Замените содержимое файла Contacts.cs на код, приведенный ниже.
   
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

Класс **Contact** определяет данные, которые будут храниться для каждого контакта, а также первичный ключ ContactID, необходимый для базы данных. Дополнительные сведения о моделях данных см. в разделе [Дальнейшие действия](#nextsteps) в конце этого руководства.

### <a name="create-web-pages-that-enable-app-users-to-work-with-the-contacts"></a>Создание веб-страниц, позволяющих пользователям приложений работать с контактами
Компонент формирования шаблонов в ASP.NET MVC может автоматически создавать код, выполняющий операции создания, чтения, обновления и удаления.

## <a name="add-a-controller-and-a-view-for-the-data"></a>Добавление контроллера и представления для данных
1. В **Обозревателе решений**разверните папку "Контроллеры".
2. Выполните сборку проекта**(Ctrl+Shift+B)**. Проект необходимо создать перед использованием механизма формирования шаблонов. 
3. Щелкните правой кнопкой мыши папку Controllers и выберите **Добавить**, а затем щелкните **Контроллер**.
   
    ![Контекстное меню добавления контроллера в папке "Контроллеры"][addcode001]
4. В диалоговом окне **Добавление шаблона** выберите **Контроллер MVC с представлениями, использующий Entity Framework** и щелкните **Добавить**.
   
   ![Добавление контролера](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rrAC.png)
5. Укажите имя контроллера **HomeController**. Выберите класс модели **Contact** . Нажмите кнопку **Новый контекст данных** и оставьте значение "ContactManager.Models.ContactManagerContext", предлагаемое по умолчанию в разделе **Новый тип контекста данных**. Щелкните **Добавить**.

    В диалоговом окне появится сообщение "Файл с именем HomeController уже существует. Вы хотите заменить его?». Щелкните **Да**. Контроллер Home, созданный для нового проекта, будет перезаписан. В списке контактов будет использоваться новый контроллер Home.

    Visual Studio создает методы и представления контроллера для операций создания, чтения, обновления и удаления в базе данных для объектов **Contact** .

## <a name="enable-migrations-create-the-database-add-sample-data-and-a-data-initializer"></a>Включение Migrations, создание базы данных, добавление примера данных и инициализатора данных
Следующая задача заключается в активации компонента [Code First Migrations](http://curah.microsoft.com/55220) для создания базы данных на основе созданной модели данных.

1. В меню **Сервис** выберите **Диспетчер пакетов библиотеки**, а затем — **Консоль диспетчера пакетов**.
   
    !["Консоль диспетчера пакетов" в меню "Сервис"][addcode008]
2. В окне **Консоль диспетчера пакетов** введите следующую команду:
   
        enable-migrations 
   
    Команда **enable-migrations** создает папку *Migrations* и размещает в этой папке файл *Configuration.cs*, который можно использовать для настройки миграций. 
3. В окне **Консоль диспетчера пакетов** введите следующую команду:
   
        add-migration Initial
   
    Команда **add-migration Initial** создает класс с именем **&lt;date_stampInitial&gt;**, который создает базу данных. Первый параметр ( *Initial* ) является произвольным и используется для создания имени файла. Новые файлы классов можно просмотреть в **обозревателе решений**.
   
    В классе **Initial** метод **Up** создает таблицу контактов, а метод **Down** (используется при возвращении к предыдущему состоянию) удаляет эту таблицу.
4. Откройте файл *Migrations\Configuration.cs*. 
5. Добавьте следующее пространства имен. 
   
         using ContactManager.Models;
6. Замените метод *Seed* следующим кодом:
   
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
   
    Код, приведенный выше, инициализирует базу данных контактной информацией. Дополнительные сведения об инициализации базы данных см. в разделе [Инициализация баз данных Entity Framework (EF)](http://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx).
7. В окне **Консоль диспетчера пакетов** введите команду:
   
        update-database
   
    ![Команды консоли диспетчера пакетов][addcode009]
   
    Команда **update-database** выполняет первую миграцию, при которой создается база данных. По умолчанию база данных создается как база данных LocalDB в SQL Server Express.
8. Для запуска приложения нажмите сочетание клавиш CTRL+F5. 

Приложение показывает начальные данные и предоставляет ссылки для изменения, удаления и просмотра подробных сведений.

![Представление MVC для данных][rxz3]

## <a name="edit-the-view"></a>Редактирование представления
1. Откройте файл *Views\Home\Index.cshtml*. На следующем шаге мы заменим созданную разметку кодом, в котором используются [jQuery](http://jquery.com/) и [Knockout.js](http://knockoutjs.com/). Новый код извлекает список контактов с помощью веб-интерфейса API и JSON, а затем привязывает данные контактов к пользовательскому интерфейсу с использованием knockout.js. Дополнительные сведения см. в разделе [Дальнейшие действия](#nextsteps) в конце этого руководства. 
2. Замените содержимое файла на код, приведенный ниже.
   
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
3. Щелкните правой кнопкой мыши папку Content и выберите **Добавить**, а затем щелкните **Новый элемент...**.
   
    ![Добавление таблицы стилей в контекстном меню папки Content][addcode005]
4. В диалоговом окне **Добавление нового элемента** введите **Стиль** в верхнем правом поле поиска, затем выберите **Список стилей**.
    ![Диалоговое окно "Добавление нового элемента"][rxStyle]
5. Присвойте файлу имя *Contacts.css* и выберите **Добавить**. Замените содержимое файла на код, приведенный ниже.
   
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
   
    Указанная таблица стилей будет определять макет, цвета и стили, используемые в приложении диспетчера контактов.
6. Откройте файл *App_Start\BundleConfig.cs*.
7. Добавьте следующий код для регистрации плагина [Knockout](http://knockoutjs.com/index.html "KO") .
   
        bundles.Add(new ScriptBundle("~/bundles/knockout").Include(
                    "~/Scripts/knockout-{version}.js"));
    В этом примере knockout используется для упрощения динамического кода JavaScript, который обрабатывает шаблоны экрана.
8. Измените запись contents/css для регистрации таблицы стилей *contacts.css* . Измените следующую строку:
   
                 bundles.Add(new StyleBundle("~/Content/css").Include(
                   "~/Content/bootstrap.css",
                   "~/Content/site.css"));
   на:
   
        bundles.Add(new StyleBundle("~/Content/css").Include(
                   "~/Content/bootstrap.css",
                   "~/Content/contacts.css",
                   "~/Content/site.css"));
9. В консоли диспетчера пакетов выполните следующую команду для установки подключаемого модуля Knockout.
   
        Install-Package knockoutjs

## <a name="add-a-controller-for-the-web-api-restful-interface"></a>Добавление контроллера для веб-интерфейса API Restful
1. В **обозревателе решений** щелкните правой кнопкой мыши папку Controllers и выберите **Добавить**, а затем щелкните **Контроллер...**. 
2. В диалоговом окне **Добавление шаблона** введите **Контроллер веб-интерфейса API 2 с действиями, использующий Entity Framework** и щелкните **Добавить**.
   
    ![Добавление контролера API](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rt1.png)
3. В диалоговом окне **Добавление контроллера** введите «ContactsController» в качестве имени контроллера. В раскрывающемся списке **Класс модели**выберите "Contact (ContactManager.Models)".  Оставьте значение по умолчанию для элемента **Класс контекста данных**. 
4. Щелкните **Добавить**.

### <a name="run-the-application-locally"></a>Локальный запуск приложения
1. Для запуска приложения нажмите сочетание клавиш CTRL+F5.
   
    ![Страница индексации][intro001]
2. Введите контакт и нажмите кнопку **Добавить**. Приложение возвращается на главную страницу и отображает введенный контакт.
   
    ![Страница индексации с элементами списка дел][addwebapi004]
3. В браузере добавьте к URL-адресу **/api/contacts** .
   
    Получившийся URL-адрес должен быть похож на этот: http://localhost:1234/api/contacts. Добавленный веб-интерфейс API RESTful возвращает сохраненные контакты. Браузеры Firefox и Chrome будут отображать данные в формате XML.
   
    ![Страница индексации с элементами списка дел][rxFFchrome]

    IE запрашивает открытие и сохранение контактов.

    ![Диалоговое окно сохранения веб-интерфейса API][addwebapi006]


    Возвращенные контакты можно открыть в блокноте или браузере.

    Эти выходные данные могут использоваться другим приложением, например мобильной веб-страницей или приложением.

    ![Диалоговое окно сохранения веб-интерфейса API][addwebapi007]

    **Предупреждение системы безопасности**. На этом этапе ваше приложение не защищено и уязвимо для атак с подделкой межсайтовых запросов (CSRF). Эта уязвимость будет удалена позднее в рамках этого учебника. Чтобы узнать больше, ознакомьтесь с [предотвращением атак с подделкой межсайтовых запросов (CSRF)][prevent-csrf-attacks].
## <a name="add-xsrf-protection"></a>Добавление защиты XSRF
Кросс-сайтовые атаки посредством ложных запросов (также известные как XSRF или CSRF) – это атаки, применяемые против приложений, размещенных в сети, когда вредоносный сайт может влиять на взаимодействие между клиентским браузером и веб-сайтом, которому доверяет браузер. Эти атаки становятся возможными, потому что браузеры отправляют маркеры аутентификации автоматически вместе с каждым запросом веб-сайта. Типичный пример – файл cookie для проверки подлинности, например билет проверки форм ASP.NET. Однако веб-сайты, использующие любой надежный способ проверки подлинности (например, Windows Authentication, Basic и т.п.), также могут стать целью таких атак.

Атака XSRF отличается от фишинговой атаки. При проведении фишинговой атаки требуется взаимодействие пользователя. В фишинговой атаке вредоносный веб-сайт практически идентичен целевому веб-сайту, поэтому жертва предоставляет атакующей стороне свои конфиденциальные данные. При атаке XSRF очень часто никаких действий со стороны жертвы не требуется. Злоумышленник больше полагается на то, что браузер автоматически отправляет все необходимые файлы cookie на целевой веб-сайт.

Дополнительную информацию см. на [веб-сайте открытого проекта безопасности веб-приложений](https://www.owasp.org/index.php/Main_Page) (OWASP)[ [XSRF]](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_\(CSRF\)).

1. В **обозревателе решений** щелкните правой кнопкой **ContactManager**, затем щелкните **Добавить** и **Класс**.
2. Назовите файл *ValidateHttpAntiForgeryTokenAttribute.cs* и добавьте следующий код:
   
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
3. Добавьте в контроллер контактов следующую инструкцию *using* , которая обеспечивает доступ к атрибуту **[ValidateHttpAntiForgeryToken]** .
   
        using ContactManager.Filters;
4. Добавьте атрибут **[ValidateHttpAntiForgeryToken]** в методы Post объекта **ContactsController**, чтобы защитить его от угроз XSRF. Этот атрибут необходимо добавить в методы действий "PutContact", "PostContact" и **DeleteContact**.
   
        [ValidateHttpAntiForgeryToken]
            public IHttpActionResult PutContact(int id, Contact contact)
            {
5. Обновите раздел *Scripts* файла *Views\Home\Index.cshtml*, включив в него код для получения токенов XSRF.
   
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

## <a name="publish-the-application-update-to-azure-and-sql-database"></a>Публикация обновления приложения в Azure и базе данных SQL
Чтобы опубликовать приложение, повторите процедуры, которые описаны выше.

1. Щелкните правой кнопкой мыши проект в **обозревателе решений** и выберите **Опубликовать**.
   
    ![Опубликовать][rxP]
2. Перейдите на вкладку **Параметры** .
3. В разделе **ContactsManagerContext(ContactsManagerContext)** щелкните значок **v**, чтобы изменить *строку удаленного подключения* на строку подключения для базы данных контактов. Щелкните **ContactDB**.
   
    ![Параметры](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rt5.png)
4. Установите флажок **Выполнить Code First Migrations (при запуске приложения)**.
5. Щелкните **Далее**, затем — **Предварительный просмотр**. В Visual Studio отображается список файлов, которые будут добавлены или обновлены.
6. Щелкните **Опубликовать**.
   После завершения развертывания в браузере открывается главная страница приложения.
   
    ![Страница индексации без контактов][intro001]
   
    Процесс публикации Visual Studio автоматически настроил строку подключения в развернутом файле *Web.config* для указания на базу данных SQL. Процесс также настроил Code First Migrations для автоматического обновления базы данных до последней версии при первом доступе приложения к базе данных после развертывания.
   
    В результате этой конфигурации Code First создает базу данных путем запуска кода в ранее созданном классе **Initial** . Это было сделано, когда приложение впервые попыталось получить доступ к базе данных после развертывания.
7. Введите контакт, как и при локальном запуске приложения, чтобы проверить успешность развертывания базы данных.

Когда вы увидите, что этот введенный элемент сохранен и показан на странице диспетчера контактов, вы будете знать, что он сохранен в базе данных.

![Страница индексации с контактами][addwebapi004]

Теперь приложение работает в облаке, используя базу данных SQL для хранения информации. После завершения тестирования приложения в Azure его необходимо удалить. Приложение является общедоступным и не имеет механизма ограничения доступа.

> [!NOTE]
> Чтобы приступить к работе со службой приложений Azure до создания учетной записи Azure, перейдите к разделу [Пробное использование службы приложений](https://azure.microsoft.com/try/app-service/), где вы можете быстро создать кратковременное веб-приложение начального уровня в службе приложений. Никаких кредитных карт и обязательств.
> 
> 

## <a name="next-steps"></a>Дальнейшие действия
Другой способ хранения данных в приложении Azure — использование хранилища Azure, обеспечивающего хранение нереляционных данных в виде BLOB-объектов и таблиц. Дополнительная информация о Web API, ASP.NET MVC и Window Azure содержится по ссылкам ниже.

* [Начало работы с Entity Framework 6 Code First с помощью MVC 5][EFCodeFirstMVCTutorial]
* [Введение в ASP.NET MVC 5](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started)
* [Первое приложение веб-интерфейса API ASP.NET](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api)
* [Отладка WAWS](web-sites-dotnet-troubleshoot-visual-studio.md)

Это руководство и пример приложения создал [Рик Андерсон (Rick Anderson)](http://blogs.msdn.com/b/rickandy/) (Twitter [@RickAndMSFT](https://twitter.com/RickAndMSFT)) при поддержке Тома Дийкстры (Tom Dykstra) и Барри Доррэнса (Barry Dorrans) (Twitter [@blowdart](https://twitter.com/blowdart)). 

Пожалуйста, оставьте отзыв о том, что вам понравилось или что вы хотели бы улучшить, не только о самом учебнике, но и о продуктах, которые он демонстрирует. Ваши отзывы помогут нам определить, какие улучшения наиболее приоритетные. Мы особенно заинтересованы узнать, насколько всем хочется получить дополнительные сведения об автоматизации процесса настройки и развертывании базы данных членства. 

## <a name="whats-changed"></a>Изменения
* Руководство по переходу от веб-сайтов к службе приложений см. в статье [Служба приложений Azure и существующие службы Azure](http://go.microsoft.com/fwlink/?LinkId=529714).

<!-- bookmarks -->
[Add an OAuth Provider]: #addOauth
[Add Roles to the Membership Database]:#mbrDB
[Create a Data Deployment Script]:#ppd
[Update the Membership Database]:#ppd2
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

