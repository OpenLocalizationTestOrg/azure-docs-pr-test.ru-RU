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
# <a name="create-a-rest-service-using-aspnet-web-api-and-sql-database-in-azure-app-service"></a><span data-ttu-id="1c4e6-103">Создание службы REST в службе приложений Azure с помощью веб-API ASP.NET и базы данных SQL</span><span class="sxs-lookup"><span data-stu-id="1c4e6-103">Create a REST service using ASP.NET Web API and SQL Database in Azure App Service</span></span>
<span data-ttu-id="1c4e6-104">В этом учебнике показано, как развернуть веб-приложение ASP.NET в [службе приложений Azure](http://go.microsoft.com/fwlink/?LinkId=529714) с помощью мастера публикации веб-сайта в Visual Studio 2013 или Visual Studio 2013 Community Edition.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-104">This tutorial shows how to deploy an ASP.NET web app to an [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) by using the Publish Web wizard in Visual Studio 2013 or Visual Studio 2013 Community Edition.</span></span> 

<span data-ttu-id="1c4e6-105">Можно бесплатно создать учетную запись Azure, а если у вас еще нет Visual Studio 2013, то пакет SDK автоматически установит Visual Studio 2013 для Web Express.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-105">You can open an Azure account for free, and if you don't already have Visual Studio 2013, the SDK automatically installs Visual Studio 2013 for Web Express.</span></span> <span data-ttu-id="1c4e6-106">Таким образом, вы можете начинать разработку на Azure абсолютно бесплатно.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-106">So you can start developing for Azure entirely for free.</span></span>

<span data-ttu-id="1c4e6-107">В данном учебнике предполагается, что у читателя нет опыта использования платформы Azure.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-107">This tutorial assumes that you have no prior experience using Azure.</span></span> <span data-ttu-id="1c4e6-108">После выполнения этого учебника вы получите простое веб-приложение, работающее в облаке.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-108">On completing this tutorial, you'll have a simple web app up and running in the cloud.</span></span>

<span data-ttu-id="1c4e6-109">Вы узнаете:</span><span class="sxs-lookup"><span data-stu-id="1c4e6-109">You'll learn:</span></span>

* <span data-ttu-id="1c4e6-110">Как подготовить компьютер к разработке для Azure путем установки пакета Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-110">How to enable your machine for Azure development by installing the Azure SDK.</span></span>
* <span data-ttu-id="1c4e6-111">Как создать проект Visual Studio ASP.NET MVC 5 и опубликовать его в приложении Azure.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-111">How to create a Visual Studio ASP.NET MVC 5 project and publish it to an Azure app.</span></span>
* <span data-ttu-id="1c4e6-112">Как использовать веб-API ASP.NET для включения вызовов API Restful.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-112">How to use the ASP.NET Web API to enable Restful API calls.</span></span>
* <span data-ttu-id="1c4e6-113">Как использовать базу данных SQL для хранения данных в Azure.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-113">How to use a SQL database to store data in Azure.</span></span>
* <span data-ttu-id="1c4e6-114">Как публиковать обновления приложений в Azure.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-114">How to publish application updates to Azure.</span></span>

<span data-ttu-id="1c4e6-115">Вы создадите простое веб-приложение со списком контактов на платформе ASP.NET MVC 5 и использующее ADO.NET Entity Framework для доступа к базе данных.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-115">You'll build a simple contact list web application that is built on ASP.NET MVC 5 and uses the ADO.NET Entity Framework for database access.</span></span> <span data-ttu-id="1c4e6-116">На следующем рисунке показано завершенное приложение:</span><span class="sxs-lookup"><span data-stu-id="1c4e6-116">The following illustration shows the completed application:</span></span>

![снимок экрана веб-сайта][intro001]

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

### <a name="create-the-project"></a><span data-ttu-id="1c4e6-118">Создание проекта</span><span class="sxs-lookup"><span data-stu-id="1c4e6-118">Create the project</span></span>
1. <span data-ttu-id="1c4e6-119">Откройте Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-119">Start Visual Studio 2013.</span></span>
2. <span data-ttu-id="1c4e6-120">В меню **Файл** выберите **Новый проект**.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-120">From the **File** menu click **New Project**.</span></span>
3. <span data-ttu-id="1c4e6-121">В диалоговом окне **Новый проект** разверните узел **Visual C#**, выберите **Веб**, а затем — **Веб-приложение ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-121">In the **New Project** dialog box, expand **Visual C#** and select **Web**  and then select **ASP.NET Web Application**.</span></span> <span data-ttu-id="1c4e6-122">Присвойте приложению имя **ContactManager** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-122">Name the application **ContactManager** and click **OK**.</span></span>
   
    ![Диалоговое окно "Новый проект"](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rr4.png)
4. <span data-ttu-id="1c4e6-124">В диалоговом окне **Новый проект ASP.NET** выберите шаблон **MVC**, установите флажок **Веб-API**, а затем щелкните **Изменить аутентификацию**.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-124">In the **New ASP.NET Project** dialog box, select the **MVC** template, check **Web API** and then click **Change Authentication**.</span></span>
5. <span data-ttu-id="1c4e6-125">В диалоговом окне **Изменить способ проверки подлинности** установите переключатель **Без проверки подлинности** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-125">In the **Change Authentication** dialog box, click **No Authentication**, and then click **OK**.</span></span>
   
    ![Без аутентификации](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/GS13noauth.png)
   
    <span data-ttu-id="1c4e6-127">В создаваемом образце приложения не будет функций, которые будут требовать от пользователя входа в систему.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-127">The sample application you're creating won't have features that require users to log in.</span></span> <span data-ttu-id="1c4e6-128">Для получения сведений об использовании функций аутентификации и авторизации см. раздел [Дальнейшие шаги](#nextsteps) в конце этого руководства.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-128">For information about how to implement authentication and authorization features, see the [Next Steps](#nextsteps) section at the end of this tutorial.</span></span> 
6. <span data-ttu-id="1c4e6-129">В диалоговом окне **Новый проект ASP.NET** убедитесь, что флажок **Разместить в облаке** установлен, и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-129">In the **New ASP.NET Project** dialog box, make sure the **Host in the Cloud** is checked and click **OK**.</span></span>

<span data-ttu-id="1c4e6-130">Если вы еще не вошли в Azure, появится запрос на ввод учетных данных.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-130">If you have not previously signed in to Azure, you will be prompted to sign in.</span></span>

1. <span data-ttu-id="1c4e6-131">Мастер настройки предложит уникальное имя на основе *ContactManager* (см. рисунок ниже).</span><span class="sxs-lookup"><span data-stu-id="1c4e6-131">The configuration wizard will suggest a unique name based on *ContactManager* (see the image below).</span></span> <span data-ttu-id="1c4e6-132">Выберите ближайшую область.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-132">Select a region near you.</span></span> <span data-ttu-id="1c4e6-133">Поиск центра обработки данных с наименьшим временем задержки можно выполнить с помощью сайта [azurespeed.com](http://www.azurespeed.com/ "AzureSpeed.com").</span><span class="sxs-lookup"><span data-stu-id="1c4e6-133">You can use [azurespeed.com](http://www.azurespeed.com/ "AzureSpeed.com") to find the lowest latency data center.</span></span> 
2. <span data-ttu-id="1c4e6-134">Если вы еще не создали сервер базы данных, нажмите **Создать новый сервер**, а затем укажите имя пользователя и пароль для базы данных.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-134">If you haven't created a database server before, select **Create new server**, enter a database user name and password.</span></span>
   
    ![Настройка веб-сайта Azure](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/configAz.PNG)

<span data-ttu-id="1c4e6-136">Если у вас есть сервер баз данных, используйте его для создания новой базы данных.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-136">If you have a database server, use that to create a new database.</span></span> <span data-ttu-id="1c4e6-137">Серверы баз данных являются ценным ресурсом, и обычно удобнее создать сразу несколько баз данных на одном сервере для тестирования и разработки, чем создавать по одному серверу на каждую базу данных.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-137">Database servers are a precious resource, and you generally want to create multiple databases on the same server for testing and development rather than creating a database server per database.</span></span> <span data-ttu-id="1c4e6-138">Убедитесь, что веб-сайт и базы данных находятся в одном регионе.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-138">Make sure your web site and database are in the same region.</span></span>

![Настройка веб-сайта Azure](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/configWithDB.PNG)

### <a name="set-the-page-header-and-footer"></a><span data-ttu-id="1c4e6-140">Задание верхнего и нижнего колонтитула страницы</span><span class="sxs-lookup"><span data-stu-id="1c4e6-140">Set the page header and footer</span></span>
1. <span data-ttu-id="1c4e6-141">В **обозревателе решений** разверните папку *Views\Shared* и откройте файл *_Layout.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-141">In **Solution Explorer**, expand the *Views\Shared* folder and open the *_Layout.cshtml* file.</span></span>
   
    ![_Layout.cshtml в обозревателе решений][newapp004]
2. <span data-ttu-id="1c4e6-143">Замените содержимое файла *Views\Shared_Layout.cshtml* кодом, приведенным ниже.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-143">Replace the contents of the *Views\Shared_Layout.cshtml* file with the following code:</span></span>

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

<span data-ttu-id="1c4e6-144">Приведенный выше код разметки позволяет изменить имя приложения с "Мое приложение ASP.NET" на "Диспетчер контактов" и удаляет ссылки на **главную** страницу, а также страницы **сведений** и **контактной информации**.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-144">The markup above changes the app name from "My ASP.NET App" to "Contact Manager", and it removes the links to **Home**, **About** and **Contact**.</span></span>

### <a name="run-the-application-locally"></a><span data-ttu-id="1c4e6-145">Локальный запуск приложения</span><span class="sxs-lookup"><span data-stu-id="1c4e6-145">Run the application locally</span></span>
1. <span data-ttu-id="1c4e6-146">Для запуска приложения нажмите сочетание клавиш CTRL+F5.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-146">Press CTRL+F5 to run the application.</span></span>
   <span data-ttu-id="1c4e6-147">Главная страница приложения откроется в браузере, используемом по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-147">The application home page appears in the default browser.</span></span>
    <span data-ttu-id="1c4e6-148">![Главная страница списка дел](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rr5.png)</span><span class="sxs-lookup"><span data-stu-id="1c4e6-148">![To Do List home page](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rr5.png)</span></span>

<span data-ttu-id="1c4e6-149">Это все, что требуется для создания приложения, которое будет развернуто в Azure.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-149">This is all you need to do for now to create the application that you'll deploy to Azure.</span></span> <span data-ttu-id="1c4e6-150">Далее вы добавите функции для работы с базой данных.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-150">Later you'll add database functionality.</span></span>

## <a name="deploy-the-application-to-azure"></a><span data-ttu-id="1c4e6-151">Развертывание приложения в Azure</span><span class="sxs-lookup"><span data-stu-id="1c4e6-151">Deploy the application to Azure</span></span>
1. <span data-ttu-id="1c4e6-152">В Visual Studio щелкните правой кнопкой мыши проект в **обозревателе решений** и выберите **Опубликовать** в контекстном меню.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-152">In Visual Studio, right-click the project in **Solution Explorer** and select **Publish** from the context menu.</span></span>
   
    !["Опубликовать" в контекстном меню проекта][PublishVSSolution]
   
    <span data-ttu-id="1c4e6-154">Откроется мастер **Публикация веб-сайта** .</span><span class="sxs-lookup"><span data-stu-id="1c4e6-154">The **Publish Web** wizard opens.</span></span>
2. <span data-ttu-id="1c4e6-155">Щелкните **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-155">Click **Publish**.</span></span>

![Вкладка "Параметры"](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/pw.png)

<span data-ttu-id="1c4e6-157">Visual Studio начнет процесс копирования файлов в Azure.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-157">Visual Studio begins the process of copying the files to the Azure server.</span></span> <span data-ttu-id="1c4e6-158">В окне **Вывод** указывается, какие действия по развертыванию были выполнены, а также сообщается об успешном завершении развертывания.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-158">The **Output** window shows what deployment actions were taken and reports successful completion of the deployment.</span></span>

1. <span data-ttu-id="1c4e6-159">Браузер по умолчанию автоматически открывает URL-адрес развернутого сайта.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-159">The default browser automatically opens to the URL of the deployed site.</span></span>
   
   <span data-ttu-id="1c4e6-160">Созданное вами приложение теперь выполняется в облаке.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-160">The application you created is now running in the cloud.</span></span>
   
   ![Главная страница списка дел на ресурсе Azure][rxz2]

## <a name="add-a-database-to-the-application"></a><span data-ttu-id="1c4e6-162">Добавление базы данных в приложение</span><span class="sxs-lookup"><span data-stu-id="1c4e6-162">Add a database to the application</span></span>
<span data-ttu-id="1c4e6-163">Далее вы обновите MVC-приложение, чтобы добавить отображение и изменение контактов, а также функции сохранения информации в базе данных.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-163">Next, you'll update the MVC application to add the ability to display and update contacts and store the data in a database.</span></span> <span data-ttu-id="1c4e6-164">Это приложение для создания базы данных, чтения и обновления информации, содержащейся в ней, будет использовать платформу Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-164">The application will use the Entity Framework to create the database and to read and update data in the database.</span></span>

### <a name="add-data-model-classes-for-the-contacts"></a><span data-ttu-id="1c4e6-165">Добавление классов модели данных для контактов</span><span class="sxs-lookup"><span data-stu-id="1c4e6-165">Add data model classes for the contacts</span></span>
<span data-ttu-id="1c4e6-166">Начните с создания простой модели данных в коде.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-166">You begin by creating a simple data model in code.</span></span>

1. <span data-ttu-id="1c4e6-167">В **обозревателе решений** щелкните правой кнопкой мыши папку "Модели" и выберите **Добавить**, а затем щелкните **Класс**.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-167">In **Solution Explorer**, right-click the Models folder, click **Add**, and then **Class**.</span></span>
   
    ![Контекстное меню добавления класса в папке "Модели"][adddb001]
2. <span data-ttu-id="1c4e6-169">В диалоговом окне **Добавление нового элемента** присвойте новому файлу класса имя *Contact.cs*, затем щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-169">In the **Add New Item** dialog box, name the new class file *Contact.cs*, and then click **Add**.</span></span>
   
    ![Диалоговое окно "Добавление нового элемента"][adddb002]
3. <span data-ttu-id="1c4e6-171">Замените содержимое файла Contacts.cs на код, приведенный ниже.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-171">Replace the contents of the Contacts.cs file with the following code.</span></span>
   
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

<span data-ttu-id="1c4e6-172">Класс **Contact** определяет данные, которые будут храниться для каждого контакта, а также первичный ключ ContactID, необходимый для базы данных.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-172">The **Contact** class defines the data that you will store for each contact, plus a primary key, ContactID, that is needed by the database.</span></span> <span data-ttu-id="1c4e6-173">Дополнительные сведения о моделях данных см. в разделе [Дальнейшие действия](#nextsteps) в конце этого руководства.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-173">You can get more information about data models in the [Next Steps](#nextsteps) section at the end of this tutorial.</span></span>

### <a name="create-web-pages-that-enable-app-users-to-work-with-the-contacts"></a><span data-ttu-id="1c4e6-174">Создание веб-страниц, позволяющих пользователям приложений работать с контактами</span><span class="sxs-lookup"><span data-stu-id="1c4e6-174">Create web pages that enable app users to work with the contacts</span></span>
<span data-ttu-id="1c4e6-175">Компонент формирования шаблонов в ASP.NET MVC может автоматически создавать код, выполняющий операции создания, чтения, обновления и удаления.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-175">The ASP.NET MVC the scaffolding feature can automatically generate code that performs create, read, update, and delete (CRUD) actions.</span></span>

## <a name="add-a-controller-and-a-view-for-the-data"></a><span data-ttu-id="1c4e6-176">Добавление контроллера и представления для данных</span><span class="sxs-lookup"><span data-stu-id="1c4e6-176">Add a Controller and a view for the data</span></span>
1. <span data-ttu-id="1c4e6-177">В **Обозревателе решений**разверните папку "Контроллеры".</span><span class="sxs-lookup"><span data-stu-id="1c4e6-177">In **Solution Explorer**, expand the Controllers folder.</span></span>
2. <span data-ttu-id="1c4e6-178">Выполните сборку проекта**(Ctrl+Shift+B)**.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-178">Build the project **(Ctrl+Shift+B)**.</span></span> <span data-ttu-id="1c4e6-179">Проект необходимо создать перед использованием механизма формирования шаблонов.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-179">(You must build the project before using scaffolding mechanism.)</span></span> 
3. <span data-ttu-id="1c4e6-180">Щелкните правой кнопкой мыши папку Controllers и выберите **Добавить**, а затем щелкните **Контроллер**.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-180">Right-click the Controllers folder and click **Add**, and then click **Controller**.</span></span>
   
    ![Контекстное меню добавления контроллера в папке "Контроллеры"][addcode001]
4. <span data-ttu-id="1c4e6-182">В диалоговом окне **Добавление шаблона** выберите **Контроллер MVC с представлениями, использующий Entity Framework** и щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-182">In the **Add Scaffold** dialog box, select **MVC Controller with views, using Entity Framework** and click **Add**.</span></span>
   
   ![Добавление контролера](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rrAC.png)
5. <span data-ttu-id="1c4e6-184">Укажите имя контроллера **HomeController**.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-184">Set the controller name to **HomeController**.</span></span> <span data-ttu-id="1c4e6-185">Выберите класс модели **Contact** .</span><span class="sxs-lookup"><span data-stu-id="1c4e6-185">Select **Contact** as your model class.</span></span> <span data-ttu-id="1c4e6-186">Нажмите кнопку **Новый контекст данных** и оставьте значение "ContactManager.Models.ContactManagerContext", предлагаемое по умолчанию в разделе **Новый тип контекста данных**.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-186">Click the **New data context** button and accept the default "ContactManager.Models.ContactManagerContext" for the **New data context type**.</span></span> <span data-ttu-id="1c4e6-187">Щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-187">Click **Add**.</span></span>

    <span data-ttu-id="1c4e6-188">В диалоговом окне появится сообщение "Файл с именем HomeController уже существует.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-188">A dialog box will prompt you: "A file with the name HomeController already exits.</span></span> <span data-ttu-id="1c4e6-189">Вы хотите заменить его?».</span><span class="sxs-lookup"><span data-stu-id="1c4e6-189">Do you want to replace it?".</span></span> <span data-ttu-id="1c4e6-190">Щелкните **Да**.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-190">Click **Yes**.</span></span> <span data-ttu-id="1c4e6-191">Контроллер Home, созданный для нового проекта, будет перезаписан.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-191">We are overwriting the Home Controller that was created with the new project.</span></span> <span data-ttu-id="1c4e6-192">В списке контактов будет использоваться новый контроллер Home.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-192">We will use the new Home Controller for our contact list.</span></span>

    <span data-ttu-id="1c4e6-193">Visual Studio создает методы и представления контроллера для операций создания, чтения, обновления и удаления в базе данных для объектов **Contact** .</span><span class="sxs-lookup"><span data-stu-id="1c4e6-193">Visual Studio creates controller methods and views for CRUD database operations for **Contact** objects.</span></span>

## <a name="enable-migrations-create-the-database-add-sample-data-and-a-data-initializer"></a><span data-ttu-id="1c4e6-194">Включение Migrations, создание базы данных, добавление примера данных и инициализатора данных</span><span class="sxs-lookup"><span data-stu-id="1c4e6-194">Enable Migrations, create the database, add sample data and a data initializer</span></span>
<span data-ttu-id="1c4e6-195">Следующая задача заключается в активации компонента [Code First Migrations](http://curah.microsoft.com/55220) для создания базы данных на основе созданной модели данных.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-195">The next task is to enable the [Code First Migrations](http://curah.microsoft.com/55220) feature in order to create the database based on the data model you created.</span></span>

1. <span data-ttu-id="1c4e6-196">В меню **Сервис** выберите **Диспетчер пакетов библиотеки**, а затем — **Консоль диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-196">In the **Tools** menu, select **Library Package Manager** and then **Package Manager Console**.</span></span>
   
    !["Консоль диспетчера пакетов" в меню "Сервис"][addcode008]
2. <span data-ttu-id="1c4e6-198">В окне **Консоль диспетчера пакетов** введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="1c4e6-198">In the **Package Manager Console** window, enter the following command:</span></span>
   
        enable-migrations 
   
    <span data-ttu-id="1c4e6-199">Команда **enable-migrations** создает папку *Migrations* и размещает в этой папке файл *Configuration.cs*, который можно использовать для настройки миграций.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-199">The **enable-migrations** command creates a *Migrations* folder and it puts in that folder a *Configuration.cs* file that you can edit to configure Migrations.</span></span> 
3. <span data-ttu-id="1c4e6-200">В окне **Консоль диспетчера пакетов** введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="1c4e6-200">In the **Package Manager Console** window, enter the following command:</span></span>
   
        add-migration Initial
   
    <span data-ttu-id="1c4e6-201">Команда **add-migration Initial** создает класс с именем **&lt;date_stampInitial&gt;**, который создает базу данных.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-201">The **add-migration Initial** command generates a class named **&lt;date_stamp&gt;Initial** that creates the database.</span></span> <span data-ttu-id="1c4e6-202">Первый параметр ( *Initial* ) является произвольным и используется для создания имени файла.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-202">The first parameter ( *Initial* ) is arbitrary and used to create the name of the file.</span></span> <span data-ttu-id="1c4e6-203">Новые файлы классов можно просмотреть в **обозревателе решений**.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-203">You can see the new class files in **Solution Explorer**.</span></span>
   
    <span data-ttu-id="1c4e6-204">В классе **Initial** метод **Up** создает таблицу контактов, а метод **Down** (используется при возвращении к предыдущему состоянию) удаляет эту таблицу.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-204">In the **Initial** class, the **Up** method creates the Contacts table, and the **Down** method (used when you want to return to the previous state) drops it.</span></span>
4. <span data-ttu-id="1c4e6-205">Откройте файл *Migrations\Configuration.cs*.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-205">Open the *Migrations\Configuration.cs* file.</span></span> 
5. <span data-ttu-id="1c4e6-206">Добавьте следующее пространства имен.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-206">Add the following namespaces.</span></span> 
   
         using ContactManager.Models;
6. <span data-ttu-id="1c4e6-207">Замените метод *Seed* следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="1c4e6-207">Replace the *Seed* method with the following code:</span></span>
   
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
   
    <span data-ttu-id="1c4e6-208">Код, приведенный выше, инициализирует базу данных контактной информацией.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-208">This code above will initialize the database with the contact information.</span></span> <span data-ttu-id="1c4e6-209">Дополнительные сведения об инициализации базы данных см. в разделе [Инициализация баз данных Entity Framework (EF)](http://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx).</span><span class="sxs-lookup"><span data-stu-id="1c4e6-209">For more information on seeding the database, see [Debugging Entity Framework (EF) DBs](http://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx).</span></span>
7. <span data-ttu-id="1c4e6-210">В окне **Консоль диспетчера пакетов** введите команду:</span><span class="sxs-lookup"><span data-stu-id="1c4e6-210">In the **Package Manager Console** enter the command:</span></span>
   
        update-database
   
    ![Команды консоли диспетчера пакетов][addcode009]
   
    <span data-ttu-id="1c4e6-212">Команда **update-database** выполняет первую миграцию, при которой создается база данных.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-212">The **update-database** runs the first migration which creates the database.</span></span> <span data-ttu-id="1c4e6-213">По умолчанию база данных создается как база данных LocalDB в SQL Server Express.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-213">By default, the database is created as a SQL Server Express LocalDB database.</span></span>
8. <span data-ttu-id="1c4e6-214">Для запуска приложения нажмите сочетание клавиш CTRL+F5.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-214">Press CTRL+F5 to run the application.</span></span> 

<span data-ttu-id="1c4e6-215">Приложение показывает начальные данные и предоставляет ссылки для изменения, удаления и просмотра подробных сведений.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-215">The application shows the seed data and provides edit, details and delete links.</span></span>

![Представление MVC для данных][rxz3]

## <a name="edit-the-view"></a><span data-ttu-id="1c4e6-217">Редактирование представления</span><span class="sxs-lookup"><span data-stu-id="1c4e6-217">Edit the View</span></span>
1. <span data-ttu-id="1c4e6-218">Откройте файл *Views\Home\Index.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-218">Open the *Views\Home\Index.cshtml* file.</span></span> <span data-ttu-id="1c4e6-219">На следующем шаге мы заменим созданную разметку кодом, в котором используются [jQuery](http://jquery.com/) и [Knockout.js](http://knockoutjs.com/).</span><span class="sxs-lookup"><span data-stu-id="1c4e6-219">In the next step, we will replace the generated markup with code that uses [jQuery](http://jquery.com/) and [Knockout.js](http://knockoutjs.com/).</span></span> <span data-ttu-id="1c4e6-220">Новый код извлекает список контактов с помощью веб-интерфейса API и JSON, а затем привязывает данные контактов к пользовательскому интерфейсу с использованием knockout.js.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-220">This new code retrieves the list of contacts from using web API and JSON and then binds the contact data to the UI using knockout.js.</span></span> <span data-ttu-id="1c4e6-221">Дополнительные сведения см. в разделе [Дальнейшие действия](#nextsteps) в конце этого руководства.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-221">For more information, see the [Next Steps](#nextsteps) section at the end of this tutorial.</span></span> 
2. <span data-ttu-id="1c4e6-222">Замените содержимое файла на код, приведенный ниже.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-222">Replace the contents of the file with the following code.</span></span>
   
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
3. <span data-ttu-id="1c4e6-223">Щелкните правой кнопкой мыши папку Content и выберите **Добавить**, а затем щелкните **Новый элемент...**.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-223">Right-click the Content folder and click **Add**, and then click **New Item...**.</span></span>
   
    ![Добавление таблицы стилей в контекстном меню папки Content][addcode005]
4. <span data-ttu-id="1c4e6-225">В диалоговом окне **Добавление нового элемента** введите **Стиль** в верхнем правом поле поиска, затем выберите **Список стилей**.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-225">In the **Add New Item** dialog box, enter **Style** in the upper right search box and then select **Style Sheet**.</span></span>
    <span data-ttu-id="1c4e6-226">![Диалоговое окно "Добавление нового элемента"][rxStyle]</span><span class="sxs-lookup"><span data-stu-id="1c4e6-226">![Add New Item dialog box][rxStyle]</span></span>
5. <span data-ttu-id="1c4e6-227">Присвойте файлу имя *Contacts.css* и выберите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-227">Name the file *Contacts.css* and click **Add**.</span></span> <span data-ttu-id="1c4e6-228">Замените содержимое файла на код, приведенный ниже.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-228">Replace the contents of the file with the following code.</span></span>
   
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
   
    <span data-ttu-id="1c4e6-229">Указанная таблица стилей будет определять макет, цвета и стили, используемые в приложении диспетчера контактов.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-229">We will use this style sheet for the layout, colors and styles used in the contact manager app.</span></span>
6. <span data-ttu-id="1c4e6-230">Откройте файл *App_Start\BundleConfig.cs*.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-230">Open the *App_Start\BundleConfig.cs* file.</span></span>
7. <span data-ttu-id="1c4e6-231">Добавьте следующий код для регистрации плагина [Knockout](http://knockoutjs.com/index.html "KO") .</span><span class="sxs-lookup"><span data-stu-id="1c4e6-231">Add the following code to register the [Knockout](http://knockoutjs.com/index.html "KO") plugin.</span></span>
   
        bundles.Add(new ScriptBundle("~/bundles/knockout").Include(
                    "~/Scripts/knockout-{version}.js"));
    <span data-ttu-id="1c4e6-232">В этом примере knockout используется для упрощения динамического кода JavaScript, который обрабатывает шаблоны экрана.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-232">This sample using knockout to simplify dynamic JavaScript code that handles the screen templates.</span></span>
8. <span data-ttu-id="1c4e6-233">Измените запись contents/css для регистрации таблицы стилей *contacts.css* .</span><span class="sxs-lookup"><span data-stu-id="1c4e6-233">Modify the contents/css entry to register the *contacts.css* style sheet.</span></span> <span data-ttu-id="1c4e6-234">Измените следующую строку:</span><span class="sxs-lookup"><span data-stu-id="1c4e6-234">Change the following line:</span></span>
   
                 bundles.Add(new StyleBundle("~/Content/css").Include(
                   "~/Content/bootstrap.css",
                   "~/Content/site.css"));
   <span data-ttu-id="1c4e6-235">на:</span><span class="sxs-lookup"><span data-stu-id="1c4e6-235">To:</span></span>
   
        bundles.Add(new StyleBundle("~/Content/css").Include(
                   "~/Content/bootstrap.css",
                   "~/Content/contacts.css",
                   "~/Content/site.css"));
9. <span data-ttu-id="1c4e6-236">В консоли диспетчера пакетов выполните следующую команду для установки подключаемого модуля Knockout.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-236">In the Package Manager Console, run the following command to install Knockout.</span></span>
   
        Install-Package knockoutjs

## <a name="add-a-controller-for-the-web-api-restful-interface"></a><span data-ttu-id="1c4e6-237">Добавление контроллера для веб-интерфейса API Restful</span><span class="sxs-lookup"><span data-stu-id="1c4e6-237">Add a controller for the Web API Restful interface</span></span>
1. <span data-ttu-id="1c4e6-238">В **обозревателе решений** щелкните правой кнопкой мыши папку Controllers и выберите **Добавить**, а затем щелкните **Контроллер...**.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-238">In **Solution Explorer**, right-click Controllers and click **Add** and then **Controller....**</span></span> 
2. <span data-ttu-id="1c4e6-239">В диалоговом окне **Добавление шаблона** введите **Контроллер веб-интерфейса API 2 с действиями, использующий Entity Framework** и щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-239">In the **Add Scaffold** dialog box, enter **Web API 2 Controller with actions, using Entity Framework** and then click **Add**.</span></span>
   
    ![Добавление контролера API](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rt1.png)
3. <span data-ttu-id="1c4e6-241">В диалоговом окне **Добавление контроллера** введите «ContactsController» в качестве имени контроллера.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-241">In the **Add Controller** dialog box, enter "ContactsController" as your controller name.</span></span> <span data-ttu-id="1c4e6-242">В раскрывающемся списке **Класс модели**выберите "Contact (ContactManager.Models)".</span><span class="sxs-lookup"><span data-stu-id="1c4e6-242">Select "Contact (ContactManager.Models)" for the **Model class**.</span></span>  <span data-ttu-id="1c4e6-243">Оставьте значение по умолчанию для элемента **Класс контекста данных**.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-243">Keep the default value for the **Data context class**.</span></span> 
4. <span data-ttu-id="1c4e6-244">Щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-244">Click **Add**.</span></span>

### <a name="run-the-application-locally"></a><span data-ttu-id="1c4e6-245">Локальный запуск приложения</span><span class="sxs-lookup"><span data-stu-id="1c4e6-245">Run the application locally</span></span>
1. <span data-ttu-id="1c4e6-246">Для запуска приложения нажмите сочетание клавиш CTRL+F5.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-246">Press CTRL+F5 to run the application.</span></span>
   
    ![Страница индексации][intro001]
2. <span data-ttu-id="1c4e6-248">Введите контакт и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-248">Enter a contact and click **Add**.</span></span> <span data-ttu-id="1c4e6-249">Приложение возвращается на главную страницу и отображает введенный контакт.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-249">The app returns to the home page and displays the contact you entered.</span></span>
   
    ![Страница индексации с элементами списка дел][addwebapi004]
3. <span data-ttu-id="1c4e6-251">В браузере добавьте к URL-адресу **/api/contacts** .</span><span class="sxs-lookup"><span data-stu-id="1c4e6-251">In the browser, append **/api/contacts** to the URL.</span></span>
   
    <span data-ttu-id="1c4e6-252">Получившийся URL-адрес должен быть похож на этот: http://localhost:1234/api/contacts.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-252">The resulting URL will resemble http://localhost:1234/api/contacts.</span></span> <span data-ttu-id="1c4e6-253">Добавленный веб-интерфейс API RESTful возвращает сохраненные контакты.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-253">The RESTful web API you added returns the stored contacts.</span></span> <span data-ttu-id="1c4e6-254">Браузеры Firefox и Chrome будут отображать данные в формате XML.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-254">Firefox and Chrome will display the data in XML format.</span></span>
   
    ![Страница индексации с элементами списка дел][rxFFchrome]

    <span data-ttu-id="1c4e6-256">IE запрашивает открытие и сохранение контактов.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-256">IE will prompt you to open or save the contacts.</span></span>

    ![Диалоговое окно сохранения веб-интерфейса API][addwebapi006]


    <span data-ttu-id="1c4e6-258">Возвращенные контакты можно открыть в блокноте или браузере.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-258">You can open the returned contacts in notepad or a browser.</span></span>

    <span data-ttu-id="1c4e6-259">Эти выходные данные могут использоваться другим приложением, например мобильной веб-страницей или приложением.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-259">This output can be consumed by another application such as mobile web page or application.</span></span>

    ![Диалоговое окно сохранения веб-интерфейса API][addwebapi007]

    <span data-ttu-id="1c4e6-261">**Предупреждение системы безопасности**. На этом этапе ваше приложение не защищено и уязвимо для атак с подделкой межсайтовых запросов (CSRF).</span><span class="sxs-lookup"><span data-stu-id="1c4e6-261">**Security Warning**: At this point, your application is insecure and vulnerable to CSRF attack.</span></span> <span data-ttu-id="1c4e6-262">Эта уязвимость будет удалена позднее в рамках этого учебника.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-262">Later in the tutorial we will remove this vulnerability.</span></span> <span data-ttu-id="1c4e6-263">Чтобы узнать больше, ознакомьтесь с [предотвращением атак с подделкой межсайтовых запросов (CSRF)][prevent-csrf-attacks].</span><span class="sxs-lookup"><span data-stu-id="1c4e6-263">For more information see [Preventing Cross-Site Request Forgery (CSRF) Attacks][prevent-csrf-attacks].</span></span>
## <a name="add-xsrf-protection"></a><span data-ttu-id="1c4e6-264">Добавление защиты XSRF</span><span class="sxs-lookup"><span data-stu-id="1c4e6-264">Add XSRF Protection</span></span>
<span data-ttu-id="1c4e6-265">Кросс-сайтовые атаки посредством ложных запросов (также известные как XSRF или CSRF) – это атаки, применяемые против приложений, размещенных в сети, когда вредоносный сайт может влиять на взаимодействие между клиентским браузером и веб-сайтом, которому доверяет браузер.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-265">Cross-site request forgery (also known as XSRF or CSRF) is an attack against web-hosted applications whereby a malicious website can influence the interaction between a client browser and a website trusted by that browser.</span></span> <span data-ttu-id="1c4e6-266">Эти атаки становятся возможными, потому что браузеры отправляют маркеры аутентификации автоматически вместе с каждым запросом веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-266">These attacks are made possible because web browsers will send authentication tokens automatically with every request to a website.</span></span> <span data-ttu-id="1c4e6-267">Типичный пример – файл cookie для проверки подлинности, например билет проверки форм ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-267">The canonical example is an authentication cookie, such as ASP.NET's Forms Authentication ticket.</span></span> <span data-ttu-id="1c4e6-268">Однако веб-сайты, использующие любой надежный способ проверки подлинности (например, Windows Authentication, Basic и т.п.), также могут стать целью таких атак.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-268">However, websites which use any persistent authentication mechanism (such as Windows Authentication, Basic, and so forth) can be targeted by these attacks.</span></span>

<span data-ttu-id="1c4e6-269">Атака XSRF отличается от фишинговой атаки.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-269">An XSRF attack is distinct from a phishing attack.</span></span> <span data-ttu-id="1c4e6-270">При проведении фишинговой атаки требуется взаимодействие пользователя.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-270">Phishing attacks require interaction from the victim.</span></span> <span data-ttu-id="1c4e6-271">В фишинговой атаке вредоносный веб-сайт практически идентичен целевому веб-сайту, поэтому жертва предоставляет атакующей стороне свои конфиденциальные данные.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-271">In a phishing attack, a malicious website will mimic the target website, and the victim is fooled into providing sensitive information to the attacker.</span></span> <span data-ttu-id="1c4e6-272">При атаке XSRF очень часто никаких действий со стороны жертвы не требуется.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-272">In an XSRF attack, there is often no interaction necessary from the victim.</span></span> <span data-ttu-id="1c4e6-273">Злоумышленник больше полагается на то, что браузер автоматически отправляет все необходимые файлы cookie на целевой веб-сайт.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-273">Rather, the attacker is relying on the browser automatically sending all relevant cookies to the destination website.</span></span>

<span data-ttu-id="1c4e6-274">Дополнительную информацию см. на [веб-сайте открытого проекта безопасности веб-приложений](https://www.owasp.org/index.php/Main_Page) (OWASP)[ [XSRF]](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_\(CSRF\)).</span><span class="sxs-lookup"><span data-stu-id="1c4e6-274">For more information, see the [Open Web Application Security Project](https://www.owasp.org/index.php/Main_Page) (OWASP) [XSRF](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_\(CSRF\)).</span></span>

1. <span data-ttu-id="1c4e6-275">В **обозревателе решений** щелкните правой кнопкой **ContactManager**, затем щелкните **Добавить** и **Класс**.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-275">In **Solution Explorer**, right **ContactManager** project and click **Add** and then click **Class**.</span></span>
2. <span data-ttu-id="1c4e6-276">Назовите файл *ValidateHttpAntiForgeryTokenAttribute.cs* и добавьте следующий код:</span><span class="sxs-lookup"><span data-stu-id="1c4e6-276">Name the file *ValidateHttpAntiForgeryTokenAttribute.cs* and add the following code:</span></span>
   
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
3. <span data-ttu-id="1c4e6-277">Добавьте в контроллер контактов следующую инструкцию *using* , которая обеспечивает доступ к атрибуту **[ValidateHttpAntiForgeryToken]** .</span><span class="sxs-lookup"><span data-stu-id="1c4e6-277">Add the following *using* statement to the contracts controller so you have access to the **[ValidateHttpAntiForgeryToken]** attribute.</span></span>
   
        using ContactManager.Filters;
4. <span data-ttu-id="1c4e6-278">Добавьте атрибут **[ValidateHttpAntiForgeryToken]** в методы Post объекта **ContactsController**, чтобы защитить его от угроз XSRF.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-278">Add the **[ValidateHttpAntiForgeryToken]** attribute to the Post methods of the **ContactsController** to protect it from XSRF threats.</span></span> <span data-ttu-id="1c4e6-279">Этот атрибут необходимо добавить в методы действий "PutContact", "PostContact" и **DeleteContact**.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-279">You will add it to the "PutContact",  "PostContact" and **DeleteContact** action methods.</span></span>
   
        [ValidateHttpAntiForgeryToken]
            public IHttpActionResult PutContact(int id, Contact contact)
            {
5. <span data-ttu-id="1c4e6-280">Обновите раздел *Scripts* файла *Views\Home\Index.cshtml*, включив в него код для получения токенов XSRF.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-280">Update the *Scripts* section of the *Views\Home\Index.cshtml* file to include code to get the XSRF tokens.</span></span>
   
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

## <a name="publish-the-application-update-to-azure-and-sql-database"></a><span data-ttu-id="1c4e6-281">Публикация обновления приложения в Azure и базе данных SQL</span><span class="sxs-lookup"><span data-stu-id="1c4e6-281">Publish the application update to Azure and SQL Database</span></span>
<span data-ttu-id="1c4e6-282">Чтобы опубликовать приложение, повторите процедуры, которые описаны выше.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-282">To publish the application, you repeat the procedure you followed earlier.</span></span>

1. <span data-ttu-id="1c4e6-283">Щелкните правой кнопкой мыши проект в **обозревателе решений** и выберите **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-283">In **Solution Explorer**, right click the project and select **Publish**.</span></span>
   
    ![Опубликовать][rxP]
2. <span data-ttu-id="1c4e6-285">Перейдите на вкладку **Параметры** .</span><span class="sxs-lookup"><span data-stu-id="1c4e6-285">Click the **Settings** tab.</span></span>
3. <span data-ttu-id="1c4e6-286">В разделе **ContactsManagerContext(ContactsManagerContext)** щелкните значок **v**, чтобы изменить *строку удаленного подключения* на строку подключения для базы данных контактов.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-286">Under **ContactsManagerContext(ContactsManagerContext)**, click the **v** icon to change *Remote connection string* to the connection string for the contact database.</span></span> <span data-ttu-id="1c4e6-287">Щелкните **ContactDB**.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-287">Click **ContactDB**.</span></span>
   
    ![Параметры](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rt5.png)
4. <span data-ttu-id="1c4e6-289">Установите флажок **Выполнить Code First Migrations (при запуске приложения)**.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-289">Check the box for **Execute Code First Migrations (runs on application start)**.</span></span>
5. <span data-ttu-id="1c4e6-290">Щелкните **Далее**, затем — **Предварительный просмотр**.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-290">Click **Next** and then click **Preview**.</span></span> <span data-ttu-id="1c4e6-291">В Visual Studio отображается список файлов, которые будут добавлены или обновлены.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-291">Visual Studio displays a list of the files that will be added or updated.</span></span>
6. <span data-ttu-id="1c4e6-292">Щелкните **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-292">Click **Publish**.</span></span>
   <span data-ttu-id="1c4e6-293">После завершения развертывания в браузере открывается главная страница приложения.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-293">After the deployment completes, the browser opens to the home page of the application.</span></span>
   
    ![Страница индексации без контактов][intro001]
   
    <span data-ttu-id="1c4e6-295">Процесс публикации Visual Studio автоматически настроил строку подключения в развернутом файле *Web.config* для указания на базу данных SQL.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-295">The Visual Studio publish process automatically configured the connection string in the deployed *Web.config* file to point to the SQL database.</span></span> <span data-ttu-id="1c4e6-296">Процесс также настроил Code First Migrations для автоматического обновления базы данных до последней версии при первом доступе приложения к базе данных после развертывания.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-296">It also configured Code First Migrations to automatically upgrade the database to the latest version the first time the application accesses the database after deployment.</span></span>
   
    <span data-ttu-id="1c4e6-297">В результате этой конфигурации Code First создает базу данных путем запуска кода в ранее созданном классе **Initial** .</span><span class="sxs-lookup"><span data-stu-id="1c4e6-297">As a result of this configuration, Code First created the database by running the code in the **Initial** class that you created earlier.</span></span> <span data-ttu-id="1c4e6-298">Это было сделано, когда приложение впервые попыталось получить доступ к базе данных после развертывания.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-298">It did this the first time the application tried to access the database after deployment.</span></span>
7. <span data-ttu-id="1c4e6-299">Введите контакт, как и при локальном запуске приложения, чтобы проверить успешность развертывания базы данных.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-299">Enter a contact as you did when you ran the app locally, to verify that database deployment succeeded.</span></span>

<span data-ttu-id="1c4e6-300">Когда вы увидите, что этот введенный элемент сохранен и показан на странице диспетчера контактов, вы будете знать, что он сохранен в базе данных.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-300">When you see that the item you enter is saved and appears on the contact manager page, you know that it has been stored in the database.</span></span>

![Страница индексации с контактами][addwebapi004]

<span data-ttu-id="1c4e6-302">Теперь приложение работает в облаке, используя базу данных SQL для хранения информации.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-302">The application is now running in the cloud, using SQL Database to store its data.</span></span> <span data-ttu-id="1c4e6-303">После завершения тестирования приложения в Azure его необходимо удалить.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-303">After you finish testing the application in Azure, delete it.</span></span> <span data-ttu-id="1c4e6-304">Приложение является общедоступным и не имеет механизма ограничения доступа.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-304">The application is public and doesn't have a mechanism to limit access.</span></span>

> [!NOTE]
> <span data-ttu-id="1c4e6-305">Чтобы приступить к работе со службой приложений Azure до создания учетной записи Azure, перейдите к разделу [Пробное использование службы приложений](https://azure.microsoft.com/try/app-service/), где вы можете быстро создать кратковременное веб-приложение начального уровня в службе приложений.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-305">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="1c4e6-306">Никаких кредитных карт и обязательств.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-306">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="1c4e6-307">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1c4e6-307">Next Steps</span></span>
<span data-ttu-id="1c4e6-308">Другой способ хранения данных в приложении Azure — использование хранилища Azure, обеспечивающего хранение нереляционных данных в виде BLOB-объектов и таблиц.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-308">Another way to store data in an Azure application is to use Azure storage, which provide non-relational data storage in the form of blobs and tables.</span></span> <span data-ttu-id="1c4e6-309">Дополнительная информация о Web API, ASP.NET MVC и Window Azure содержится по ссылкам ниже.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-309">The following links provide more information on Web API, ASP.NET MVC and Window Azure.</span></span>

* <span data-ttu-id="1c4e6-310">[Начало работы с Entity Framework 6 Code First с помощью MVC 5][EFCodeFirstMVCTutorial]</span><span class="sxs-lookup"><span data-stu-id="1c4e6-310">[Getting Started with Entity Framework using MVC][EFCodeFirstMVCTutorial]</span></span>
* [<span data-ttu-id="1c4e6-311">Введение в ASP.NET MVC 5</span><span class="sxs-lookup"><span data-stu-id="1c4e6-311">Intro to ASP.NET MVC 5</span></span>](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started)
* [<span data-ttu-id="1c4e6-312">Первое приложение веб-интерфейса API ASP.NET</span><span class="sxs-lookup"><span data-stu-id="1c4e6-312">Your First ASP.NET Web API</span></span>](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api)
* [<span data-ttu-id="1c4e6-313">Отладка WAWS</span><span class="sxs-lookup"><span data-stu-id="1c4e6-313">Debugging WAWS</span></span>](web-sites-dotnet-troubleshoot-visual-studio.md)

<span data-ttu-id="1c4e6-314">Это руководство и пример приложения создал [Рик Андерсон (Rick Anderson)](http://blogs.msdn.com/b/rickandy/) (Twitter [@RickAndMSFT](https://twitter.com/RickAndMSFT)) при поддержке Тома Дийкстры (Tom Dykstra) и Барри Доррэнса (Barry Dorrans) (Twitter [@blowdart](https://twitter.com/blowdart)).</span><span class="sxs-lookup"><span data-stu-id="1c4e6-314">This tutorial and the sample application was written by [Rick Anderson](http://blogs.msdn.com/b/rickandy/) (Twitter [@RickAndMSFT](https://twitter.com/RickAndMSFT)) with assistance from Tom Dykstra and Barry Dorrans (Twitter [@blowdart](https://twitter.com/blowdart)).</span></span> 

<span data-ttu-id="1c4e6-315">Пожалуйста, оставьте отзыв о том, что вам понравилось или что вы хотели бы улучшить, не только о самом учебнике, но и о продуктах, которые он демонстрирует.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-315">Please leave feedback on what you liked or what you would like to see improved, not only about the tutorial itself but also about the products that it demonstrates.</span></span> <span data-ttu-id="1c4e6-316">Ваши отзывы помогут нам определить, какие улучшения наиболее приоритетные.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-316">Your feedback will help us prioritize improvements.</span></span> <span data-ttu-id="1c4e6-317">Мы особенно заинтересованы узнать, насколько всем хочется получить дополнительные сведения об автоматизации процесса настройки и развертывании базы данных членства.</span><span class="sxs-lookup"><span data-stu-id="1c4e6-317">We are especially interested in finding out how much interest there is in more automation for the process of configuring and deploying the membership database.</span></span> 

## <a name="whats-changed"></a><span data-ttu-id="1c4e6-318">Изменения</span><span class="sxs-lookup"><span data-stu-id="1c4e6-318">What's changed</span></span>
* <span data-ttu-id="1c4e6-319">Руководство по переходу от веб-сайтов к службе приложений см. в статье [Служба приложений Azure и существующие службы Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="1c4e6-319">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

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

