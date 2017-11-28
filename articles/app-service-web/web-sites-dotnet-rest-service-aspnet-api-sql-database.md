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
# <a name="create-a-rest-service-using-aspnet-web-api-and-sql-database-in-azure-app-service"></a><span data-ttu-id="03c71-103">Создание службы REST в службе приложений Azure с помощью веб-API ASP.NET и базы данных SQL</span><span class="sxs-lookup"><span data-stu-id="03c71-103">Create a REST service using ASP.NET Web API and SQL Database in Azure App Service</span></span>
<span data-ttu-id="03c71-104">В этом учебнике показано, как toodeploy ASP.NET веб-приложения tooan [службе приложений Azure](http://go.microsoft.com/fwlink/?LinkId=529714) с помощью мастера публикации веб-сайта hello в Visual Studio 2013 или Visual Studio 2013 Community Edition.</span><span class="sxs-lookup"><span data-stu-id="03c71-104">This tutorial shows how toodeploy an ASP.NET web app tooan [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) by using hello Publish Web wizard in Visual Studio 2013 or Visual Studio 2013 Community Edition.</span></span> 

<span data-ttu-id="03c71-105">Можно открыть учетную запись Azure бесплатно, и если у вас еще нет Visual Studio 2013, hello SDK автоматически устанавливает Visual Studio 2013 для Web Express.</span><span class="sxs-lookup"><span data-stu-id="03c71-105">You can open an Azure account for free, and if you don't already have Visual Studio 2013, hello SDK automatically installs Visual Studio 2013 for Web Express.</span></span> <span data-ttu-id="03c71-106">Таким образом, вы можете начинать разработку на Azure абсолютно бесплатно.</span><span class="sxs-lookup"><span data-stu-id="03c71-106">So you can start developing for Azure entirely for free.</span></span>

<span data-ttu-id="03c71-107">В данном учебнике предполагается, что у читателя нет опыта использования платформы Azure.</span><span class="sxs-lookup"><span data-stu-id="03c71-107">This tutorial assumes that you have no prior experience using Azure.</span></span> <span data-ttu-id="03c71-108">После завершения этого учебника, чтобы иметь простой веб-приложения вверх и работающих в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="03c71-108">On completing this tutorial, you'll have a simple web app up and running in hello cloud.</span></span>

<span data-ttu-id="03c71-109">Вы узнаете:</span><span class="sxs-lookup"><span data-stu-id="03c71-109">You'll learn:</span></span>

* <span data-ttu-id="03c71-110">Как tooenable компьютер для разработки Azure, установив hello Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="03c71-110">How tooenable your machine for Azure development by installing hello Azure SDK.</span></span>
* <span data-ttu-id="03c71-111">Как toocreate Visual Studio ASP.NET MVC 5 проекта и опубликуйте его tooan приложения Azure.</span><span class="sxs-lookup"><span data-stu-id="03c71-111">How toocreate a Visual Studio ASP.NET MVC 5 project and publish it tooan Azure app.</span></span>
* <span data-ttu-id="03c71-112">Каким образом вызывает toouse hello веб-API ASP.NET tooenable Restful API.</span><span class="sxs-lookup"><span data-stu-id="03c71-112">How toouse hello ASP.NET Web API tooenable Restful API calls.</span></span>
* <span data-ttu-id="03c71-113">Как toouse SQL базы данных toostore данные в Azure.</span><span class="sxs-lookup"><span data-stu-id="03c71-113">How toouse a SQL database toostore data in Azure.</span></span>
* <span data-ttu-id="03c71-114">Как приложение toopublish обновляет tooAzure.</span><span class="sxs-lookup"><span data-stu-id="03c71-114">How toopublish application updates tooAzure.</span></span>

<span data-ttu-id="03c71-115">Мы создадим простой список контактов веб-приложение, основанное на ASP.NET MVC 5 и использует hello ADO.NET Entity Framework для доступа к базе данных.</span><span class="sxs-lookup"><span data-stu-id="03c71-115">You'll build a simple contact list web application that is built on ASP.NET MVC 5 and uses hello ADO.NET Entity Framework for database access.</span></span> <span data-ttu-id="03c71-116">следующие иллюстрации показано hello Hello завершения приложения:</span><span class="sxs-lookup"><span data-stu-id="03c71-116">hello following illustration shows hello completed application:</span></span>

![снимок экрана веб-сайта][intro001]

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

### <a name="create-hello-project"></a><span data-ttu-id="03c71-118">Создание проекта hello</span><span class="sxs-lookup"><span data-stu-id="03c71-118">Create hello project</span></span>
1. <span data-ttu-id="03c71-119">Откройте Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="03c71-119">Start Visual Studio 2013.</span></span>
2. <span data-ttu-id="03c71-120">Из hello **файл** меню **новый проект**.</span><span class="sxs-lookup"><span data-stu-id="03c71-120">From hello **File** menu click **New Project**.</span></span>
3. <span data-ttu-id="03c71-121">В hello **новый проект** диалогового окна разверните **Visual C#** и выберите **Web** , а затем выберите **веб-приложение ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="03c71-121">In hello **New Project** dialog box, expand **Visual C#** and select **Web**  and then select **ASP.NET Web Application**.</span></span> <span data-ttu-id="03c71-122">Имя приложения hello **ContactManager** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="03c71-122">Name hello application **ContactManager** and click **OK**.</span></span>
   
    ![Диалоговое окно "Новый проект"](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rr4.png)
4. <span data-ttu-id="03c71-124">В hello **новый проект ASP.NET** диалоговое окно, выберите hello **MVC** шаблона, проверка **веб-API** и нажмите кнопку **изменить аутентификацию**.</span><span class="sxs-lookup"><span data-stu-id="03c71-124">In hello **New ASP.NET Project** dialog box, select hello **MVC** template, check **Web API** and then click **Change Authentication**.</span></span>
5. <span data-ttu-id="03c71-125">В hello **изменить аутентификацию** диалоговое окно, нажмите кнопку **без проверки подлинности**, а затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="03c71-125">In hello **Change Authentication** dialog box, click **No Authentication**, and then click **OK**.</span></span>
   
    ![Без аутентификации](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/GS13noauth.png)
   
    <span data-ttu-id="03c71-127">отсутствует функций, требующих toolog пользователей в пример приложения Hello, который вы создаете.</span><span class="sxs-lookup"><span data-stu-id="03c71-127">hello sample application you're creating won't have features that require users toolog in.</span></span> <span data-ttu-id="03c71-128">Сведения о функции tooimplement проверки подлинности и авторизации, в разделе hello [дальнейшие действия](#nextsteps) раздел в конце hello этого учебника.</span><span class="sxs-lookup"><span data-stu-id="03c71-128">For information about how tooimplement authentication and authorization features, see hello [Next Steps](#nextsteps) section at hello end of this tutorial.</span></span> 
6. <span data-ttu-id="03c71-129">В hello **новый проект ASP.NET** диалоговое окно, убедитесь, что hello **узлов в облаке hello** установлен флажок и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="03c71-129">In hello **New ASP.NET Project** dialog box, make sure hello **Host in hello Cloud** is checked and click **OK**.</span></span>

<span data-ttu-id="03c71-130">Если ранее вы не выполнялся в tooAzure, появится запрос toosign в.</span><span class="sxs-lookup"><span data-stu-id="03c71-130">If you have not previously signed in tooAzure, you will be prompted toosign in.</span></span>

1. <span data-ttu-id="03c71-131">Мастер настройки Hello предложит уникальным именем на основе *ContactManager* (см. ниже рисунке hello).</span><span class="sxs-lookup"><span data-stu-id="03c71-131">hello configuration wizard will suggest a unique name based on *ContactManager* (see hello image below).</span></span> <span data-ttu-id="03c71-132">Выберите ближайшую область.</span><span class="sxs-lookup"><span data-stu-id="03c71-132">Select a region near you.</span></span> <span data-ttu-id="03c71-133">Можно использовать [azurespeed.com](http://www.azurespeed.com/ "AzureSpeed.com") toofind hello наименьшее задержки ЦОД.</span><span class="sxs-lookup"><span data-stu-id="03c71-133">You can use [azurespeed.com](http://www.azurespeed.com/ "AzureSpeed.com") toofind hello lowest latency data center.</span></span> 
2. <span data-ttu-id="03c71-134">Если вы еще не создали сервер базы данных, нажмите **Создать новый сервер**, а затем укажите имя пользователя и пароль для базы данных.</span><span class="sxs-lookup"><span data-stu-id="03c71-134">If you haven't created a database server before, select **Create new server**, enter a database user name and password.</span></span>
   
    ![Настройка веб-сайта Azure](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/configAz.PNG)

<span data-ttu-id="03c71-136">Если сервер базы данных, используйте этот toocreate новую базу данных.</span><span class="sxs-lookup"><span data-stu-id="03c71-136">If you have a database server, use that toocreate a new database.</span></span> <span data-ttu-id="03c71-137">Серверы баз данных являются ценным ресурсом, и обычно требуется toocreate несколько баз данных на hello один сервер для тестирования и разработки, а не создание сервера базы данных на базу данных.</span><span class="sxs-lookup"><span data-stu-id="03c71-137">Database servers are a precious resource, and you generally want toocreate multiple databases on hello same server for testing and development rather than creating a database server per database.</span></span> <span data-ttu-id="03c71-138">Убедитесь, что веб-сайта и базы данных находятся в hello одного региона.</span><span class="sxs-lookup"><span data-stu-id="03c71-138">Make sure your web site and database are in hello same region.</span></span>

![Настройка веб-сайта Azure](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/configWithDB.PNG)

### <a name="set-hello-page-header-and-footer"></a><span data-ttu-id="03c71-140">Набор hello верхнего и нижнего колонтитула</span><span class="sxs-lookup"><span data-stu-id="03c71-140">Set hello page header and footer</span></span>
1. <span data-ttu-id="03c71-141">В **обозревателе решений**, разверните hello *представления\общие* папку и откройте hello *_Layout.cshtml* файла.</span><span class="sxs-lookup"><span data-stu-id="03c71-141">In **Solution Explorer**, expand hello *Views\Shared* folder and open hello *_Layout.cshtml* file.</span></span>
   
    ![_Layout.cshtml в обозревателе решений][newapp004]
2. <span data-ttu-id="03c71-143">Замените содержимое hello hello *Views\Shared_Layout.cshtml* файл с hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="03c71-143">Replace hello contents of hello *Views\Shared_Layout.cshtml* file with hello following code:</span></span>

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

<span data-ttu-id="03c71-144">Hello разметки выше имя приложения hello изменения из «Мое приложение ASP.NET» слишком «диспетчера контактов», который удаляет ссылки hello слишком**Главная**, **о** и **контакт**.</span><span class="sxs-lookup"><span data-stu-id="03c71-144">hello markup above changes hello app name from "My ASP.NET App" too"Contact Manager", and it removes hello links too**Home**, **About** and **Contact**.</span></span>

### <a name="run-hello-application-locally"></a><span data-ttu-id="03c71-145">Запустите приложение hello локально</span><span class="sxs-lookup"><span data-stu-id="03c71-145">Run hello application locally</span></span>
1. <span data-ttu-id="03c71-146">Нажмите клавиши CTRL + F5 toorun hello приложения.</span><span class="sxs-lookup"><span data-stu-id="03c71-146">Press CTRL+F5 toorun hello application.</span></span>
   <span data-ttu-id="03c71-147">Домашняя страница приложения Hello отображается в браузере по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="03c71-147">hello application home page appears in hello default browser.</span></span>
    <span data-ttu-id="03c71-148">![Домашняя страница tooDo списка](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rr5.png)</span><span class="sxs-lookup"><span data-stu-id="03c71-148">![tooDo List home page](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rr5.png)</span></span>

<span data-ttu-id="03c71-149">Это все, что нужно toodo для приложения hello toocreate сейчас, вы развернете tooAzure.</span><span class="sxs-lookup"><span data-stu-id="03c71-149">This is all you need toodo for now toocreate hello application that you'll deploy tooAzure.</span></span> <span data-ttu-id="03c71-150">Далее вы добавите функции для работы с базой данных.</span><span class="sxs-lookup"><span data-stu-id="03c71-150">Later you'll add database functionality.</span></span>

## <a name="deploy-hello-application-tooazure"></a><span data-ttu-id="03c71-151">Развертывание tooAzure приложения hello</span><span class="sxs-lookup"><span data-stu-id="03c71-151">Deploy hello application tooAzure</span></span>
1. <span data-ttu-id="03c71-152">В Visual Studio щелкните правой кнопкой мыши проект hello в **обозревателе решений** и выберите **публикации** hello контекстном меню.</span><span class="sxs-lookup"><span data-stu-id="03c71-152">In Visual Studio, right-click hello project in **Solution Explorer** and select **Publish** from hello context menu.</span></span>
   
    !["Опубликовать" в контекстном меню проекта][PublishVSSolution]
   
    <span data-ttu-id="03c71-154">Hello **веб-публикация** откроется мастер.</span><span class="sxs-lookup"><span data-stu-id="03c71-154">hello **Publish Web** wizard opens.</span></span>
2. <span data-ttu-id="03c71-155">Щелкните **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="03c71-155">Click **Publish**.</span></span>

![Вкладка "Параметры"](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/pw.png)

<span data-ttu-id="03c71-157">Visual Studio начинает процесс hello копирования файлов hello toohello сервера Azure.</span><span class="sxs-lookup"><span data-stu-id="03c71-157">Visual Studio begins hello process of copying hello files toohello Azure server.</span></span> <span data-ttu-id="03c71-158">Hello **вывода** окно показывает выполненные действия развертывания и сообщает успешного завершения развертывания hello.</span><span class="sxs-lookup"><span data-stu-id="03c71-158">hello **Output** window shows what deployment actions were taken and reports successful completion of hello deployment.</span></span>

1. <span data-ttu-id="03c71-159">toohello URL-адрес сайта hello развертывания автоматически откроется в браузере по умолчанию Hello.</span><span class="sxs-lookup"><span data-stu-id="03c71-159">hello default browser automatically opens toohello URL of hello deployed site.</span></span>
   
   <span data-ttu-id="03c71-160">созданное приложение Hello, теперь работает в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="03c71-160">hello application you created is now running in hello cloud.</span></span>
   
   ![Домашняя страница списка tooDo, работающие в Azure][rxz2]

## <a name="add-a-database-toohello-application"></a><span data-ttu-id="03c71-162">Добавить приложение toohello базы данных</span><span class="sxs-lookup"><span data-stu-id="03c71-162">Add a database toohello application</span></span>
<span data-ttu-id="03c71-163">Затем будет обновлять hello MVC приложения tooadd hello возможность toodisplay и обновить контакты и хранить в базе данных hello.</span><span class="sxs-lookup"><span data-stu-id="03c71-163">Next, you'll update hello MVC application tooadd hello ability toodisplay and update contacts and store hello data in a database.</span></span> <span data-ttu-id="03c71-164">приложение Hello использовать hello Entity Framework toocreate hello database и tooread и обновления данных в базе данных hello.</span><span class="sxs-lookup"><span data-stu-id="03c71-164">hello application will use hello Entity Framework toocreate hello database and tooread and update data in hello database.</span></span>

### <a name="add-data-model-classes-for-hello-contacts"></a><span data-ttu-id="03c71-165">Добавление классов модели данных для контактов, hello</span><span class="sxs-lookup"><span data-stu-id="03c71-165">Add data model classes for hello contacts</span></span>
<span data-ttu-id="03c71-166">Начните с создания простой модели данных в коде.</span><span class="sxs-lookup"><span data-stu-id="03c71-166">You begin by creating a simple data model in code.</span></span>

1. <span data-ttu-id="03c71-167">В **обозревателе решений**, щелкните правой кнопкой мыши папку Models hello, нажмите кнопку **добавить**, а затем **класса**.</span><span class="sxs-lookup"><span data-stu-id="03c71-167">In **Solution Explorer**, right-click hello Models folder, click **Add**, and then **Class**.</span></span>
   
    ![Контекстное меню добавления класса в папке "Модели"][adddb001]
2. <span data-ttu-id="03c71-169">В hello **Добавление нового элемента** диалоговое окно, новый файл класса имя hello *Contact.cs*, а затем нажмите кнопку **добавить**.</span><span class="sxs-lookup"><span data-stu-id="03c71-169">In hello **Add New Item** dialog box, name hello new class file *Contact.cs*, and then click **Add**.</span></span>
   
    ![Диалоговое окно "Добавление нового элемента"][adddb002]
3. <span data-ttu-id="03c71-171">Замените содержимое файла Contacts.cs hello hello hello, следующий код.</span><span class="sxs-lookup"><span data-stu-id="03c71-171">Replace hello contents of hello Contacts.cs file with hello following code.</span></span>
   
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

<span data-ttu-id="03c71-172">Hello **обратитесь к** класс определяет hello данных, в которой будут храниться для каждого контактного лица, а также первичный ключ ContactID, необходимые для hello базы данных.</span><span class="sxs-lookup"><span data-stu-id="03c71-172">hello **Contact** class defines hello data that you will store for each contact, plus a primary key, ContactID, that is needed by hello database.</span></span> <span data-ttu-id="03c71-173">Дополнительные сведения о моделях данных можно получить в hello [дальнейшие действия](#nextsteps) раздел в конце hello этого учебника.</span><span class="sxs-lookup"><span data-stu-id="03c71-173">You can get more information about data models in hello [Next Steps](#nextsteps) section at hello end of this tutorial.</span></span>

### <a name="create-web-pages-that-enable-app-users-toowork-with-hello-contacts"></a><span data-ttu-id="03c71-174">Создание веб-страницы, позволяющие toowork пользователей приложения с контактами hello</span><span class="sxs-lookup"><span data-stu-id="03c71-174">Create web pages that enable app users toowork with hello contacts</span></span>
<span data-ttu-id="03c71-175">Hello функции формирования шаблонов hello ASP.NET MVC можно автоматически создавать код, выполняющий создание, чтение, обновление и удаление (CRUD) действия.</span><span class="sxs-lookup"><span data-stu-id="03c71-175">hello ASP.NET MVC hello scaffolding feature can automatically generate code that performs create, read, update, and delete (CRUD) actions.</span></span>

## <a name="add-a-controller-and-a-view-for-hello-data"></a><span data-ttu-id="03c71-176">Добавление контроллера и представления для данных hello</span><span class="sxs-lookup"><span data-stu-id="03c71-176">Add a Controller and a view for hello data</span></span>
1. <span data-ttu-id="03c71-177">В **обозревателе решений**, разверните папку Controllers hello.</span><span class="sxs-lookup"><span data-stu-id="03c71-177">In **Solution Explorer**, expand hello Controllers folder.</span></span>
2. <span data-ttu-id="03c71-178">Построение проекта hello **(Ctrl + Shift + B)**.</span><span class="sxs-lookup"><span data-stu-id="03c71-178">Build hello project **(Ctrl+Shift+B)**.</span></span> <span data-ttu-id="03c71-179">(Перед использованием механизма формирования шаблонов необходимо построить проект hello.)</span><span class="sxs-lookup"><span data-stu-id="03c71-179">(You must build hello project before using scaffolding mechanism.)</span></span> 
3. <span data-ttu-id="03c71-180">Щелкните правой кнопкой мыши папку Controllers hello и нажмите кнопку **добавить**, а затем нажмите кнопку **контроллера**.</span><span class="sxs-lookup"><span data-stu-id="03c71-180">Right-click hello Controllers folder and click **Add**, and then click **Controller**.</span></span>
   
    ![Контекстное меню добавления контроллера в папке "Контроллеры"][addcode001]
4. <span data-ttu-id="03c71-182">В hello **Добавление формирования шаблонов** выберите **контроллер MVC с представлениями, использующий Entity Framework** и нажмите кнопку **добавить**.</span><span class="sxs-lookup"><span data-stu-id="03c71-182">In hello **Add Scaffold** dialog box, select **MVC Controller with views, using Entity Framework** and click **Add**.</span></span>
   
   ![Добавление контролера](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rrAC.png)
5. <span data-ttu-id="03c71-184">Задайте имя контроллера hello слишком**HomeController**.</span><span class="sxs-lookup"><span data-stu-id="03c71-184">Set hello controller name too**HomeController**.</span></span> <span data-ttu-id="03c71-185">Выберите класс модели **Contact** .</span><span class="sxs-lookup"><span data-stu-id="03c71-185">Select **Contact** as your model class.</span></span> <span data-ttu-id="03c71-186">Нажмите кнопку hello **новый контекст данных** кнопку и примите значение по умолчанию hello «ContactManager.Models.ContactManagerContext» для hello **новый тип контекста данных**.</span><span class="sxs-lookup"><span data-stu-id="03c71-186">Click hello **New data context** button and accept hello default "ContactManager.Models.ContactManagerContext" for hello **New data context type**.</span></span> <span data-ttu-id="03c71-187">Щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="03c71-187">Click **Add**.</span></span>

    <span data-ttu-id="03c71-188">Диалоговое окно предложит: «файл с именем hello HomeController уже существует.</span><span class="sxs-lookup"><span data-stu-id="03c71-188">A dialog box will prompt you: "A file with hello name HomeController already exits.</span></span> <span data-ttu-id="03c71-189">Вы хотите tooreplace его?».</span><span class="sxs-lookup"><span data-stu-id="03c71-189">Do you want tooreplace it?".</span></span> <span data-ttu-id="03c71-190">Щелкните **Да**.</span><span class="sxs-lookup"><span data-stu-id="03c71-190">Click **Yes**.</span></span> <span data-ttu-id="03c71-191">Мы — это перезапись hello Главная контроллера, который был создан с новым проектом hello.</span><span class="sxs-lookup"><span data-stu-id="03c71-191">We are overwriting hello Home Controller that was created with hello new project.</span></span> <span data-ttu-id="03c71-192">Мы будем использовать hello новый Главная контроллера списка контактов.</span><span class="sxs-lookup"><span data-stu-id="03c71-192">We will use hello new Home Controller for our contact list.</span></span>

    <span data-ttu-id="03c71-193">Visual Studio создает методы и представления контроллера для операций создания, чтения, обновления и удаления в базе данных для объектов **Contact** .</span><span class="sxs-lookup"><span data-stu-id="03c71-193">Visual Studio creates controller methods and views for CRUD database operations for **Contact** objects.</span></span>

## <a name="enable-migrations-create-hello-database-add-sample-data-and-a-data-initializer"></a><span data-ttu-id="03c71-194">Включить миграцию, создание hello базы данных, добавить образец данных и инициализаторов данных</span><span class="sxs-lookup"><span data-stu-id="03c71-194">Enable Migrations, create hello database, add sample data and a data initializer</span></span>
<span data-ttu-id="03c71-195">Следующая задача Hello — tooenable hello [Code First Migrations](http://curah.microsoft.com/55220) функции в базе данных hello toocreate заказа на основании созданная модель hello.</span><span class="sxs-lookup"><span data-stu-id="03c71-195">hello next task is tooenable hello [Code First Migrations](http://curah.microsoft.com/55220) feature in order toocreate hello database based on hello data model you created.</span></span>

1. <span data-ttu-id="03c71-196">В hello **средства** последовательно выберите пункты **диспетчер пакетов библиотеки** и затем **консоль диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="03c71-196">In hello **Tools** menu, select **Library Package Manager** and then **Package Manager Console**.</span></span>
   
    !["Консоль диспетчера пакетов" в меню "Сервис"][addcode008]
2. <span data-ttu-id="03c71-198">В hello **консоль диспетчера пакетов** окно, введите следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="03c71-198">In hello **Package Manager Console** window, enter hello following command:</span></span>
   
        enable-migrations 
   
    <span data-ttu-id="03c71-199">Hello **enable-migrations** команда создает *миграций* папке и ее помещает в этой папке *Configuration.cs* tooconfigure миграции можно редактировать файл.</span><span class="sxs-lookup"><span data-stu-id="03c71-199">hello **enable-migrations** command creates a *Migrations* folder and it puts in that folder a *Configuration.cs* file that you can edit tooconfigure Migrations.</span></span> 
3. <span data-ttu-id="03c71-200">В hello **консоль диспетчера пакетов** окно, введите следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="03c71-200">In hello **Package Manager Console** window, enter hello following command:</span></span>
   
        add-migration Initial
   
    <span data-ttu-id="03c71-201">Hello **добавьте миграции исходного** команда создает класс с именем  **&lt;date_stamp&gt;начальной** , создает базу данных hello.</span><span class="sxs-lookup"><span data-stu-id="03c71-201">hello **add-migration Initial** command generates a class named **&lt;date_stamp&gt;Initial** that creates hello database.</span></span> <span data-ttu-id="03c71-202">Здравствуйте, первый параметр ( *начальной* ) — имя hello toocreate произвольный и используемого файла hello.</span><span class="sxs-lookup"><span data-stu-id="03c71-202">hello first parameter ( *Initial* ) is arbitrary and used toocreate hello name of hello file.</span></span> <span data-ttu-id="03c71-203">Для просмотра файлов новый класс hello в **обозревателе решений**.</span><span class="sxs-lookup"><span data-stu-id="03c71-203">You can see hello new class files in **Solution Explorer**.</span></span>
   
    <span data-ttu-id="03c71-204">В hello **начальной** класса hello **копирование** метод создает таблицы Contacts hello и hello **работу** метод (используется, если предыдущее состояние toohello tooreturn) удаляется.</span><span class="sxs-lookup"><span data-stu-id="03c71-204">In hello **Initial** class, hello **Up** method creates hello Contacts table, and hello **Down** method (used when you want tooreturn toohello previous state) drops it.</span></span>
4. <span data-ttu-id="03c71-205">Откройте hello *Migrations\Configuration.cs* файла.</span><span class="sxs-lookup"><span data-stu-id="03c71-205">Open hello *Migrations\Configuration.cs* file.</span></span> 
5. <span data-ttu-id="03c71-206">Добавьте следующие пространства имен hello.</span><span class="sxs-lookup"><span data-stu-id="03c71-206">Add hello following namespaces.</span></span> 
   
         using ContactManager.Models;
6. <span data-ttu-id="03c71-207">Замените hello *начальное значение* метод с hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="03c71-207">Replace hello *Seed* method with hello following code:</span></span>
   
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
   
    <span data-ttu-id="03c71-208">Приведенный выше код инициализирует hello базы данных с hello контактные данные.</span><span class="sxs-lookup"><span data-stu-id="03c71-208">This code above will initialize hello database with hello contact information.</span></span> <span data-ttu-id="03c71-209">Дополнительные сведения о заполнения hello базы данных см. в разделе [отладки Entity Framework (EF) баз данных SQL Server](http://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx).</span><span class="sxs-lookup"><span data-stu-id="03c71-209">For more information on seeding hello database, see [Debugging Entity Framework (EF) DBs](http://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx).</span></span>
7. <span data-ttu-id="03c71-210">В hello **консоль диспетчера пакетов** введите команду hello:</span><span class="sxs-lookup"><span data-stu-id="03c71-210">In hello **Package Manager Console** enter hello command:</span></span>
   
        update-database
   
    ![Команды консоли диспетчера пакетов][addcode009]
   
    <span data-ttu-id="03c71-212">Hello **базы данных обновления** запусков hello первый миграции, который создает базу данных hello.</span><span class="sxs-lookup"><span data-stu-id="03c71-212">hello **update-database** runs hello first migration which creates hello database.</span></span> <span data-ttu-id="03c71-213">По умолчанию hello базы данных создается как база данных SQL Server Express LocalDB.</span><span class="sxs-lookup"><span data-stu-id="03c71-213">By default, hello database is created as a SQL Server Express LocalDB database.</span></span>
8. <span data-ttu-id="03c71-214">Нажмите клавиши CTRL + F5 toorun hello приложения.</span><span class="sxs-lookup"><span data-stu-id="03c71-214">Press CTRL+F5 toorun hello application.</span></span> 

<span data-ttu-id="03c71-215">приложение Hello hello начальное значение данных и поле редактирования, сведения и ссылки для удаления.</span><span class="sxs-lookup"><span data-stu-id="03c71-215">hello application shows hello seed data and provides edit, details and delete links.</span></span>

![Представление MVC для данных][rxz3]

## <a name="edit-hello-view"></a><span data-ttu-id="03c71-217">Изменить представление hello</span><span class="sxs-lookup"><span data-stu-id="03c71-217">Edit hello View</span></span>
1. <span data-ttu-id="03c71-218">Откройте hello *Views\Home\Index.cshtml* файла.</span><span class="sxs-lookup"><span data-stu-id="03c71-218">Open hello *Views\Home\Index.cshtml* file.</span></span> <span data-ttu-id="03c71-219">В следующем шаге hello мы заменит разметки hello созданный код, использующий [jQuery](http://jquery.com/) и [Knockout.js](http://knockoutjs.com/).</span><span class="sxs-lookup"><span data-stu-id="03c71-219">In hello next step, we will replace hello generated markup with code that uses [jQuery](http://jquery.com/) and [Knockout.js](http://knockoutjs.com/).</span></span> <span data-ttu-id="03c71-220">Этот новый код извлекает список контактов, hello с помощью веб-API и JSON, а затем привязывает hello обратитесь в службу данных toohello пользовательского интерфейса с помощью knockout.js.</span><span class="sxs-lookup"><span data-stu-id="03c71-220">This new code retrieves hello list of contacts from using web API and JSON and then binds hello contact data toohello UI using knockout.js.</span></span> <span data-ttu-id="03c71-221">Дополнительные сведения см. в разделе hello [дальнейшие действия](#nextsteps) раздел в конце hello этого учебника.</span><span class="sxs-lookup"><span data-stu-id="03c71-221">For more information, see hello [Next Steps](#nextsteps) section at hello end of this tutorial.</span></span> 
2. <span data-ttu-id="03c71-222">Замените содержимое файла hello hello hello, следующий код.</span><span class="sxs-lookup"><span data-stu-id="03c71-222">Replace hello contents of hello file with hello following code.</span></span>
   
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
3. <span data-ttu-id="03c71-223">Щелкните правой кнопкой мыши папку содержимого hello и нажмите кнопку **добавить**, а затем нажмите кнопку **новый элемент...** .</span><span class="sxs-lookup"><span data-stu-id="03c71-223">Right-click hello Content folder and click **Add**, and then click **New Item...**.</span></span>
   
    ![Добавление таблицы стилей в контекстном меню папки Content][addcode005]
4. <span data-ttu-id="03c71-225">В hello **Добавление нового элемента** диалогового окна введите **стиль** в hello поле верхнего правого поиска, а затем выберите **стилей**.</span><span class="sxs-lookup"><span data-stu-id="03c71-225">In hello **Add New Item** dialog box, enter **Style** in hello upper right search box and then select **Style Sheet**.</span></span>
    <span data-ttu-id="03c71-226">![Диалоговое окно "Добавление нового элемента"][rxStyle]</span><span class="sxs-lookup"><span data-stu-id="03c71-226">![Add New Item dialog box][rxStyle]</span></span>
5. <span data-ttu-id="03c71-227">Имя файла hello *Contacts.css* и нажмите кнопку **добавить**.</span><span class="sxs-lookup"><span data-stu-id="03c71-227">Name hello file *Contacts.css* and click **Add**.</span></span> <span data-ttu-id="03c71-228">Замените содержимое файла hello hello hello, следующий код.</span><span class="sxs-lookup"><span data-stu-id="03c71-228">Replace hello contents of hello file with hello following code.</span></span>
   
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
   
    <span data-ttu-id="03c71-229">Мы будем использовать данную таблицу стилей для hello макета, цветов и стилей, используемых в приложение диспетчера контактов hello.</span><span class="sxs-lookup"><span data-stu-id="03c71-229">We will use this style sheet for hello layout, colors and styles used in hello contact manager app.</span></span>
6. <span data-ttu-id="03c71-230">Откройте hello *App_Start\BundleConfig.cs* файла.</span><span class="sxs-lookup"><span data-stu-id="03c71-230">Open hello *App_Start\BundleConfig.cs* file.</span></span>
7. <span data-ttu-id="03c71-231">Добавьте следующий код tooregister hello hello [Knockout](http://knockoutjs.com/index.html "KO") подключаемого модуля.</span><span class="sxs-lookup"><span data-stu-id="03c71-231">Add hello following code tooregister hello [Knockout](http://knockoutjs.com/index.html "KO") plugin.</span></span>
   
        bundles.Add(new ScriptBundle("~/bundles/knockout").Include(
                    "~/Scripts/knockout-{version}.js"));
    <span data-ttu-id="03c71-232">В этом примере с помощью knockout toosimplify динамический код JavaScript, который обрабатывает шаблоны экран приветствия.</span><span class="sxs-lookup"><span data-stu-id="03c71-232">This sample using knockout toosimplify dynamic JavaScript code that handles hello screen templates.</span></span>
8. <span data-ttu-id="03c71-233">Изменить запись tooregister hello содержимое/css hello *contacts.css* таблицы стилей.</span><span class="sxs-lookup"><span data-stu-id="03c71-233">Modify hello contents/css entry tooregister hello *contacts.css* style sheet.</span></span> <span data-ttu-id="03c71-234">Изменить hello, следующей строкой:</span><span class="sxs-lookup"><span data-stu-id="03c71-234">Change hello following line:</span></span>
   
                 bundles.Add(new StyleBundle("~/Content/css").Include(
                   "~/Content/bootstrap.css",
                   "~/Content/site.css"));
   <span data-ttu-id="03c71-235">на:</span><span class="sxs-lookup"><span data-stu-id="03c71-235">To:</span></span>
   
        bundles.Add(new StyleBundle("~/Content/css").Include(
                   "~/Content/bootstrap.css",
                   "~/Content/contacts.css",
                   "~/Content/site.css"));
9. <span data-ttu-id="03c71-236">В hello консоль диспетчера пакетов выполните следующие команды tooinstall маскирования hello.</span><span class="sxs-lookup"><span data-stu-id="03c71-236">In hello Package Manager Console, run hello following command tooinstall Knockout.</span></span>
   
        Install-Package knockoutjs

## <a name="add-a-controller-for-hello-web-api-restful-interface"></a><span data-ttu-id="03c71-237">Добавить контроллер Web API Restful интерфейса hello</span><span class="sxs-lookup"><span data-stu-id="03c71-237">Add a controller for hello Web API Restful interface</span></span>
1. <span data-ttu-id="03c71-238">В **обозревателе решений** щелкните правой кнопкой мыши папку Controllers и выберите **Добавить**, а затем щелкните **Контроллер...**.</span><span class="sxs-lookup"><span data-stu-id="03c71-238">In **Solution Explorer**, right-click Controllers and click **Add** and then **Controller....**</span></span> 
2. <span data-ttu-id="03c71-239">В hello **Добавление формирования шаблонов** диалогового окна введите **Web API 2 контроллер с действиями, использующий Entity Framework** и нажмите кнопку **добавить**.</span><span class="sxs-lookup"><span data-stu-id="03c71-239">In hello **Add Scaffold** dialog box, enter **Web API 2 Controller with actions, using Entity Framework** and then click **Add**.</span></span>
   
    ![Добавление контролера API](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rt1.png)
3. <span data-ttu-id="03c71-241">В hello **добавить контроллер** диалогового окна введите «ContactsController» в качестве имени контроллера.</span><span class="sxs-lookup"><span data-stu-id="03c71-241">In hello **Add Controller** dialog box, enter "ContactsController" as your controller name.</span></span> <span data-ttu-id="03c71-242">Выберите «Contact (ContactManager.Models)» для hello **класс модели**.</span><span class="sxs-lookup"><span data-stu-id="03c71-242">Select "Contact (ContactManager.Models)" for hello **Model class**.</span></span>  <span data-ttu-id="03c71-243">Оставьте значение по умолчанию hello hello **класс контекста данных**.</span><span class="sxs-lookup"><span data-stu-id="03c71-243">Keep hello default value for hello **Data context class**.</span></span> 
4. <span data-ttu-id="03c71-244">Щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="03c71-244">Click **Add**.</span></span>

### <a name="run-hello-application-locally"></a><span data-ttu-id="03c71-245">Запустите приложение hello локально</span><span class="sxs-lookup"><span data-stu-id="03c71-245">Run hello application locally</span></span>
1. <span data-ttu-id="03c71-246">Нажмите клавиши CTRL + F5 toorun hello приложения.</span><span class="sxs-lookup"><span data-stu-id="03c71-246">Press CTRL+F5 toorun hello application.</span></span>
   
    ![Страница индексации][intro001]
2. <span data-ttu-id="03c71-248">Введите контакт и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="03c71-248">Enter a contact and click **Add**.</span></span> <span data-ttu-id="03c71-249">приложение Hello возвращает toohello домашней страницы и отображает hello контакт введенный.</span><span class="sxs-lookup"><span data-stu-id="03c71-249">hello app returns toohello home page and displays hello contact you entered.</span></span>
   
    ![Страница индексации с элементами списка дел][addwebapi004]
3. <span data-ttu-id="03c71-251">В браузере hello append **контактов/api/** toohello URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="03c71-251">In hello browser, append **/api/contacts** toohello URL.</span></span>
   
    <span data-ttu-id="03c71-252">Полученный Hello URL-адрес будет похоже на http://localhost:1234/api/контактов.</span><span class="sxs-lookup"><span data-stu-id="03c71-252">hello resulting URL will resemble http://localhost:1234/api/contacts.</span></span> <span data-ttu-id="03c71-253">веб-RESTful Hello API, которые вы добавили возвращает контакты хранятся hello.</span><span class="sxs-lookup"><span data-stu-id="03c71-253">hello RESTful web API you added returns hello stored contacts.</span></span> <span data-ttu-id="03c71-254">Hello данные будут отображаться Firefox и Chrome в формате XML.</span><span class="sxs-lookup"><span data-stu-id="03c71-254">Firefox and Chrome will display hello data in XML format.</span></span>
   
    ![Страница индексации с элементами списка дел][rxFFchrome]

    <span data-ttu-id="03c71-256">IE будет предложен tooopen или сохранять контакты hello.</span><span class="sxs-lookup"><span data-stu-id="03c71-256">IE will prompt you tooopen or save hello contacts.</span></span>

    ![Диалоговое окно сохранения веб-интерфейса API][addwebapi006]


    <span data-ttu-id="03c71-258">Вы можете открыть hello возвращается контактов в блокноте или в браузере.</span><span class="sxs-lookup"><span data-stu-id="03c71-258">You can open hello returned contacts in notepad or a browser.</span></span>

    <span data-ttu-id="03c71-259">Эти выходные данные могут использоваться другим приложением, например мобильной веб-страницей или приложением.</span><span class="sxs-lookup"><span data-stu-id="03c71-259">This output can be consumed by another application such as mobile web page or application.</span></span>

    ![Диалоговое окно сохранения веб-интерфейса API][addwebapi007]

    <span data-ttu-id="03c71-261">**Предупреждение системы безопасности**: на этом этапе приложение является небезопасной и уязвимым tooCSRF атаки.</span><span class="sxs-lookup"><span data-stu-id="03c71-261">**Security Warning**: At this point, your application is insecure and vulnerable tooCSRF attack.</span></span> <span data-ttu-id="03c71-262">Далее в учебнике hello удалит эту уязвимость.</span><span class="sxs-lookup"><span data-stu-id="03c71-262">Later in hello tutorial we will remove this vulnerability.</span></span> <span data-ttu-id="03c71-263">Чтобы узнать больше, ознакомьтесь с [предотвращением атак с подделкой межсайтовых запросов (CSRF)][prevent-csrf-attacks].</span><span class="sxs-lookup"><span data-stu-id="03c71-263">For more information see [Preventing Cross-Site Request Forgery (CSRF) Attacks][prevent-csrf-attacks].</span></span>
## <a name="add-xsrf-protection"></a><span data-ttu-id="03c71-264">Добавление защиты XSRF</span><span class="sxs-lookup"><span data-stu-id="03c71-264">Add XSRF Protection</span></span>
<span data-ttu-id="03c71-265">Подделки межсайтовых запросов (также известный как XSRF или CSRF) — это атака, для приложений веб сервере, при котором вредоносный веб-сайт может повлиять на взаимодействие hello браузер клиента и веб-сайта, которым доверяет этот браузер.</span><span class="sxs-lookup"><span data-stu-id="03c71-265">Cross-site request forgery (also known as XSRF or CSRF) is an attack against web-hosted applications whereby a malicious website can influence hello interaction between a client browser and a website trusted by that browser.</span></span> <span data-ttu-id="03c71-266">Такие атаки становится возможным, так как веб-браузеры будет отправлять маркеры проверки подлинности автоматически с каждым веб-сайтом tooa запроса.</span><span class="sxs-lookup"><span data-stu-id="03c71-266">These attacks are made possible because web browsers will send authentication tokens automatically with every request tooa website.</span></span> <span data-ttu-id="03c71-267">Типичный пример Hello — файл cookie проверки подлинности, например ASP. Билет проверки подлинности форм в NET.</span><span class="sxs-lookup"><span data-stu-id="03c71-267">hello canonical example is an authentication cookie, such as ASP.NET's Forms Authentication ticket.</span></span> <span data-ttu-id="03c71-268">Однако веб-сайты, использующие любой надежный способ проверки подлинности (например, Windows Authentication, Basic и т.п.), также могут стать целью таких атак.</span><span class="sxs-lookup"><span data-stu-id="03c71-268">However, websites which use any persistent authentication mechanism (such as Windows Authentication, Basic, and so forth) can be targeted by these attacks.</span></span>

<span data-ttu-id="03c71-269">Атака XSRF отличается от фишинговой атаки.</span><span class="sxs-lookup"><span data-stu-id="03c71-269">An XSRF attack is distinct from a phishing attack.</span></span> <span data-ttu-id="03c71-270">Фишинг-атаках требуют взаимодействия из hello жертвы.</span><span class="sxs-lookup"><span data-stu-id="03c71-270">Phishing attacks require interaction from hello victim.</span></span> <span data-ttu-id="03c71-271">В фишинга вредоносный веб-сайт будет имитировать hello целевой веб-сайт и жертвы hello верьте обеспечить злоумышленник toohello конфиденциальные сведения.</span><span class="sxs-lookup"><span data-stu-id="03c71-271">In a phishing attack, a malicious website will mimic hello target website, and hello victim is fooled into providing sensitive information toohello attacker.</span></span> <span data-ttu-id="03c71-272">При атаке XSRF обычно имеется без участия необходимые из hello жертвы.</span><span class="sxs-lookup"><span data-stu-id="03c71-272">In an XSRF attack, there is often no interaction necessary from hello victim.</span></span> <span data-ttu-id="03c71-273">Вместо этого он hello полагается на автоматическую отправку веб-сайта назначения toohello все соответствующие файлы cookie браузера hello.</span><span class="sxs-lookup"><span data-stu-id="03c71-273">Rather, hello attacker is relying on hello browser automatically sending all relevant cookies toohello destination website.</span></span>

<span data-ttu-id="03c71-274">Дополнительные сведения см. в разделе hello [откройте проект безопасности веб-приложения](https://www.owasp.org/index.php/Main_Page) (OWASP) [XSRF](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_\(CSRF\)).</span><span class="sxs-lookup"><span data-stu-id="03c71-274">For more information, see hello [Open Web Application Security Project](https://www.owasp.org/index.php/Main_Page) (OWASP) [XSRF](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_\(CSRF\)).</span></span>

1. <span data-ttu-id="03c71-275">В **обозревателе решений** щелкните правой кнопкой **ContactManager**, затем щелкните **Добавить** и **Класс**.</span><span class="sxs-lookup"><span data-stu-id="03c71-275">In **Solution Explorer**, right **ContactManager** project and click **Add** and then click **Class**.</span></span>
2. <span data-ttu-id="03c71-276">Имя файла hello *ValidateHttpAntiForgeryTokenAttribute.cs* и добавить hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="03c71-276">Name hello file *ValidateHttpAntiForgeryTokenAttribute.cs* and add hello following code:</span></span>
   
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
3. <span data-ttu-id="03c71-277">Добавьте следующее hello *с помощью* toohello инструкции контракты контроллера, у вас есть доступ toohello **[ValidateHttpAntiForgeryToken]** атрибута.</span><span class="sxs-lookup"><span data-stu-id="03c71-277">Add hello following *using* statement toohello contracts controller so you have access toohello **[ValidateHttpAntiForgeryToken]** attribute.</span></span>
   
        using ContactManager.Filters;
4. <span data-ttu-id="03c71-278">Добавить hello **[ValidateHttpAntiForgeryToken]** атрибута toohello методы Post hello **ContactsController** tooprotect его от XSRF угроз.</span><span class="sxs-lookup"><span data-stu-id="03c71-278">Add hello **[ValidateHttpAntiForgeryToken]** attribute toohello Post methods of hello **ContactsController** tooprotect it from XSRF threats.</span></span> <span data-ttu-id="03c71-279">Вы добавите toohello «PutContact», «PostContact» и **DeleteContact** методы действий.</span><span class="sxs-lookup"><span data-stu-id="03c71-279">You will add it toohello "PutContact",  "PostContact" and **DeleteContact** action methods.</span></span>
   
        [ValidateHttpAntiForgeryToken]
            public IHttpActionResult PutContact(int id, Contact contact)
            {
5. <span data-ttu-id="03c71-280">Обновление hello *сценариев* раздел hello *Views\Home\Index.cshtml* файл tooinclude кода tooget hello XSRF маркеры.</span><span class="sxs-lookup"><span data-stu-id="03c71-280">Update hello *Scripts* section of hello *Views\Home\Index.cshtml* file tooinclude code tooget hello XSRF tokens.</span></span>
   
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

## <a name="publish-hello-application-update-tooazure-and-sql-database"></a><span data-ttu-id="03c71-281">Опубликовать tooAzure обновление приложения hello и базы данных SQL</span><span class="sxs-lookup"><span data-stu-id="03c71-281">Publish hello application update tooAzure and SQL Database</span></span>
<span data-ttu-id="03c71-282">приложение hello toopublish, повторите hello процедуры, которые описаны выше.</span><span class="sxs-lookup"><span data-stu-id="03c71-282">toopublish hello application, you repeat hello procedure you followed earlier.</span></span>

1. <span data-ttu-id="03c71-283">В **обозревателе решений**, щелкните правой кнопкой мыши проект hello и выберите **публикации**.</span><span class="sxs-lookup"><span data-stu-id="03c71-283">In **Solution Explorer**, right click hello project and select **Publish**.</span></span>
   
    ![Опубликовать][rxP]
2. <span data-ttu-id="03c71-285">Нажмите кнопку hello **параметры** вкладки.</span><span class="sxs-lookup"><span data-stu-id="03c71-285">Click hello **Settings** tab.</span></span>
3. <span data-ttu-id="03c71-286">В разделе **ContactsManagerContext(ContactsManagerContext)**, щелкните hello **v** toochange значок *строку подключения к удаленному* toohello строку подключения для контактов, hello База данных.</span><span class="sxs-lookup"><span data-stu-id="03c71-286">Under **ContactsManagerContext(ContactsManagerContext)**, click hello **v** icon toochange *Remote connection string* toohello connection string for hello contact database.</span></span> <span data-ttu-id="03c71-287">Щелкните **ContactDB**.</span><span class="sxs-lookup"><span data-stu-id="03c71-287">Click **ContactDB**.</span></span>
   
    ![данных](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rt5.png)
4. <span data-ttu-id="03c71-289">Установите флажок "hello" для **выполнять миграции Code First (запускается при запуске приложения)**.</span><span class="sxs-lookup"><span data-stu-id="03c71-289">Check hello box for **Execute Code First Migrations (runs on application start)**.</span></span>
5. <span data-ttu-id="03c71-290">Щелкните **Далее**, затем — **Предварительный просмотр**.</span><span class="sxs-lookup"><span data-stu-id="03c71-290">Click **Next** and then click **Preview**.</span></span> <span data-ttu-id="03c71-291">Visual Studio отображает список файлов hello, которые будут добавлены или обновлены.</span><span class="sxs-lookup"><span data-stu-id="03c71-291">Visual Studio displays a list of hello files that will be added or updated.</span></span>
6. <span data-ttu-id="03c71-292">Щелкните **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="03c71-292">Click **Publish**.</span></span>
   <span data-ttu-id="03c71-293">После завершения развертывания hello hello браузера откроется toohello Домашняя страница приложения hello.</span><span class="sxs-lookup"><span data-stu-id="03c71-293">After hello deployment completes, hello browser opens toohello home page of hello application.</span></span>
   
    ![Страница индексации без контактов][intro001]
   
    <span data-ttu-id="03c71-295">Hello Visual Studio опубликовать строки подключения автоматически настроить процесс hello в развертывании hello *Web.config* toopoint toohello файл SQL-базы данных.</span><span class="sxs-lookup"><span data-stu-id="03c71-295">hello Visual Studio publish process automatically configured hello connection string in hello deployed *Web.config* file toopoint toohello SQL database.</span></span> <span data-ttu-id="03c71-296">Он также настроен Code First Migrations tooautomatically hello обновления базы данных toohello последней версии hello первое время hello приложение обращается к hello базы данных после развертывания.</span><span class="sxs-lookup"><span data-stu-id="03c71-296">It also configured Code First Migrations tooautomatically upgrade hello database toohello latest version hello first time hello application accesses hello database after deployment.</span></span>
   
    <span data-ttu-id="03c71-297">В результате этой конфигурации Code First hello база данных создана путем выполнения кода hello в hello **начальной** класса, которое было создано ранее.</span><span class="sxs-lookup"><span data-stu-id="03c71-297">As a result of this configuration, Code First created hello database by running hello code in hello **Initial** class that you created earlier.</span></span> <span data-ttu-id="03c71-298">После развертывания было этой hello первый раз hello пытался tooaccess hello базы данных приложения.</span><span class="sxs-lookup"><span data-stu-id="03c71-298">It did this hello first time hello application tried tooaccess hello database after deployment.</span></span>
7. <span data-ttu-id="03c71-299">Ввести контакт, как при запуске локально, приложение hello tooverify об успешном выполнении развертывания базы данных.</span><span class="sxs-lookup"><span data-stu-id="03c71-299">Enter a contact as you did when you ran hello app locally, tooverify that database deployment succeeded.</span></span>

<span data-ttu-id="03c71-300">При появлении этого элемента Привет вводимых вами сохраняется и отображается на странице приветствия диспетчера контактов, вы знаете, хранящихся в базе данных hello.</span><span class="sxs-lookup"><span data-stu-id="03c71-300">When you see that hello item you enter is saved and appears on hello contact manager page, you know that it has been stored in hello database.</span></span>

![Страница индексации с контактами][addwebapi004]

<span data-ttu-id="03c71-302">приложение Hello теперь работает в облаке hello toostore базы данных SQL с использованием его данных.</span><span class="sxs-lookup"><span data-stu-id="03c71-302">hello application is now running in hello cloud, using SQL Database toostore its data.</span></span> <span data-ttu-id="03c71-303">После завершения тестирования приложения hello в Azure, удалите его.</span><span class="sxs-lookup"><span data-stu-id="03c71-303">After you finish testing hello application in Azure, delete it.</span></span> <span data-ttu-id="03c71-304">приложение Hello является открытым и не имеет доступа toolimit механизм.</span><span class="sxs-lookup"><span data-stu-id="03c71-304">hello application is public and doesn't have a mechanism toolimit access.</span></span>

> [!NOTE]
> <span data-ttu-id="03c71-305">Tooget работы в службе приложений Azure перед регистрацией учетную запись Azure, перейдите слишком[повторите служб приложений](https://azure.microsoft.com/try/app-service/), в котором можно немедленно создать кратковременных начальный веб-приложения в службе приложений.</span><span class="sxs-lookup"><span data-stu-id="03c71-305">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="03c71-306">Никаких кредитных карт и обязательств.</span><span class="sxs-lookup"><span data-stu-id="03c71-306">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="03c71-307">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="03c71-307">Next Steps</span></span>
<span data-ttu-id="03c71-308">Другой как toostore данные в приложении Azure — toouse хранилища Azure, предоставляемый хранения нереляционных данных в форме hello больших двоичных объектов и таблиц.</span><span class="sxs-lookup"><span data-stu-id="03c71-308">Another way toostore data in an Azure application is toouse Azure storage, which provide non-relational data storage in hello form of blobs and tables.</span></span> <span data-ttu-id="03c71-309">Привет, следующие ссылки предоставляют дополнительные сведения по веб-API, ASP.NET MVC и Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="03c71-309">hello following links provide more information on Web API, ASP.NET MVC and Window Azure.</span></span>

* <span data-ttu-id="03c71-310">[Начало работы с Entity Framework 6 Code First с помощью MVC 5][EFCodeFirstMVCTutorial]</span><span class="sxs-lookup"><span data-stu-id="03c71-310">[Getting Started with Entity Framework using MVC][EFCodeFirstMVCTutorial]</span></span>
* [<span data-ttu-id="03c71-311">Начальный tooASP.NET MVC 5</span><span class="sxs-lookup"><span data-stu-id="03c71-311">Intro tooASP.NET MVC 5</span></span>](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started)
* [<span data-ttu-id="03c71-312">Первое приложение веб-интерфейса API ASP.NET</span><span class="sxs-lookup"><span data-stu-id="03c71-312">Your First ASP.NET Web API</span></span>](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api)
* [<span data-ttu-id="03c71-313">Отладка WAWS</span><span class="sxs-lookup"><span data-stu-id="03c71-313">Debugging WAWS</span></span>](web-sites-dotnet-troubleshoot-visual-studio.md)

<span data-ttu-id="03c71-314">В этом образце приложения hello и учебных было написано с [Рик Андерсон](http://blogs.msdn.com/b/rickandy/) (Twitter [ @RickAndMSFT ](https://twitter.com/RickAndMSFT)) с помощью Tom Dykstra и Барри Dorrans (Twitter [ @blowdart ](https://twitter.com/blowdart)).</span><span class="sxs-lookup"><span data-stu-id="03c71-314">This tutorial and hello sample application was written by [Rick Anderson](http://blogs.msdn.com/b/rickandy/) (Twitter [@RickAndMSFT](https://twitter.com/RickAndMSFT)) with assistance from Tom Dykstra and Barry Dorrans (Twitter [@blowdart](https://twitter.com/blowdart)).</span></span> 

<span data-ttu-id="03c71-315">Оставьте отзыв на что вам понравилось или что хотелось бы toosee улучшены, не только о учебника hello сам, но также и о продуктах hello, он демонстрирует.</span><span class="sxs-lookup"><span data-stu-id="03c71-315">Please leave feedback on what you liked or what you would like toosee improved, not only about hello tutorial itself but also about hello products that it demonstrates.</span></span> <span data-ttu-id="03c71-316">Ваши отзывы помогут нам определить, какие улучшения наиболее приоритетные.</span><span class="sxs-lookup"><span data-stu-id="03c71-316">Your feedback will help us prioritize improvements.</span></span> <span data-ttu-id="03c71-317">Нас интересуют особенно узнать о том, сколько процентная существует находится в большей автоматизации процесса hello, настройки и развертывания базы данных членства hello.</span><span class="sxs-lookup"><span data-stu-id="03c71-317">We are especially interested in finding out how much interest there is in more automation for hello process of configuring and deploying hello membership database.</span></span> 

## <a name="whats-changed"></a><span data-ttu-id="03c71-318">Изменения</span><span class="sxs-lookup"><span data-stu-id="03c71-318">What's changed</span></span>
* <span data-ttu-id="03c71-319">Toohello руководство изменений из tooApp веб-сайтов службы. в разделе: [службе приложений Azure и ее влияние на существующие службы Azure](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="03c71-319">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

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

