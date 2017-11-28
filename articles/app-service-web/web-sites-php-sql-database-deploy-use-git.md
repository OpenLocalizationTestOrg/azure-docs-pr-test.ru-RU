---
title: "aaaCreate PHP SQL, веб-приложения и развертывания tooAzure службы приложений с помощью Git"
description: "Учебник, в котором показано, как toocreate PHP веб-приложение, которое сохраняет данные в базе данных SQL Azure и использовать tooAzure Git развертывания служб приложений."
services: app-service\web, sql-database
documentationcenter: php
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 6b090bf6-31d8-4b74-81eb-050ef95929ca
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: aaacb2fe0787bbcdafa72871912e8d08792be29d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-php-sql-web-app-and-deploy-tooazure-app-service-using-git"></a><span data-ttu-id="1caed-103">Создание веб-приложения PHP SQL и развертывание tooAzure службы приложений с помощью Git</span><span class="sxs-lookup"><span data-stu-id="1caed-103">Create a PHP-SQL web app and deploy tooAzure App Service using Git</span></span>
<span data-ttu-id="1caed-104">В этом учебнике показано, как приложение в веб-toocreate PHP [службе приложений Azure](http://go.microsoft.com/fwlink/?LinkId=529714) , при подключении tooAzure базы данных SQL и как toodeploy его с помощью Git.</span><span class="sxs-lookup"><span data-stu-id="1caed-104">This tutorial shows you how toocreate a PHP web app in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) that connects tooAzure SQL Database and how toodeploy it using Git.</span></span> <span data-ttu-id="1caed-105">В этом учебнике предполагается, у вас есть [PHP][install-php], [SQL Server Express][install-SQLExpress], hello [драйверы Майкрософт для SQL Server для PHP ](http://www.microsoft.com/download/en/details.aspx?id=20098), и [Git] [ install-git] установлены на компьютере.</span><span class="sxs-lookup"><span data-stu-id="1caed-105">This tutorial assumes you have [PHP][install-php], [SQL Server Express][install-SQLExpress], hello [Microsoft Drivers for SQL Server for PHP](http://www.microsoft.com/download/en/details.aspx?id=20098), and [Git][install-git] installed on your computer.</span></span> <span data-ttu-id="1caed-106">После завершения работы с этим учебником у вас будет работающее в Azure веб-приложение PHP-SQL.</span><span class="sxs-lookup"><span data-stu-id="1caed-106">Upon completing this guide, you will have a PHP-SQL web app running in Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="1caed-107">Можно установить и настроить PHP, SQL Server Express и hello драйверы Майкрософт для SQL Server для PHP с помощью hello [Microsoft Web Platform Installer](http://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="1caed-107">You can install and configure PHP, SQL Server Express, and hello Microsoft Drivers for SQL Server for PHP using hello [Microsoft Web Platform Installer](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
> 
> 

<span data-ttu-id="1caed-108">Вы узнаете:</span><span class="sxs-lookup"><span data-stu-id="1caed-108">You will learn:</span></span>

* <span data-ttu-id="1caed-109">Как toocreate Azure веб-приложения и базы данных SQL с помощью hello [портала Azure](http://go.microsoft.com/fwlink/?LinkId=529715).</span><span class="sxs-lookup"><span data-stu-id="1caed-109">How toocreate an Azure web app and a SQL Database using hello [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715).</span></span> <span data-ttu-id="1caed-110">Так, как PHP в веб-приложений приложения служб включена по умолчанию, никаких дополнительных действий не является обязательным toorun кода PHP.</span><span class="sxs-lookup"><span data-stu-id="1caed-110">Because PHP is enabled in App Service Web Apps by default, nothing special is required toorun your PHP code.</span></span>
* <span data-ttu-id="1caed-111">Как toopublish и повторно опубликовать tooAzure вашего приложения, с помощью Git.</span><span class="sxs-lookup"><span data-stu-id="1caed-111">How toopublish and re-publish your application tooAzure using Git.</span></span>

<span data-ttu-id="1caed-112">Руководствуясь этим учебником, вы создадите в PHP простое веб-приложение регистрации.</span><span class="sxs-lookup"><span data-stu-id="1caed-112">By following this tutorial, you will build a simple registration web application in PHP.</span></span> <span data-ttu-id="1caed-113">в веб-сайт Azure будет размещаться приложение Hello.</span><span class="sxs-lookup"><span data-stu-id="1caed-113">hello application will be hosted in an Azure Website.</span></span> <span data-ttu-id="1caed-114">Снимок экрана приложения hello завершения используется следующим образом:</span><span class="sxs-lookup"><span data-stu-id="1caed-114">A screenshot of hello completed application is below:</span></span>

![Веб-сайт Azure на PHP](./media/web-sites-php-sql-database-deploy-use-git/running_app_3.png)

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="1caed-116">Tooget работы в службе приложений Azure перед регистрацией учетную запись Azure, перейдите слишком[повторите служб приложений](https://azure.microsoft.com/try/app-service/), в котором можно немедленно создать кратковременных начальный веб-приложения в службе приложений.</span><span class="sxs-lookup"><span data-stu-id="1caed-116">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="1caed-117">Никаких кредитных карт и обязательств.</span><span class="sxs-lookup"><span data-stu-id="1caed-117">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="create-an-azure-web-app-and-set-up-git-publishing"></a><span data-ttu-id="1caed-118">Создание веб-приложения Azure и настройка публикации в Git</span><span class="sxs-lookup"><span data-stu-id="1caed-118">Create an Azure web app and set up Git publishing</span></span>
<span data-ttu-id="1caed-119">Выполните эти шаги toocreate Azure веб-приложение и база данных SQL.</span><span class="sxs-lookup"><span data-stu-id="1caed-119">Follow these steps toocreate an Azure web app and a SQL Database:</span></span>

1. <span data-ttu-id="1caed-120">Войдите в toohello [портала Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="1caed-120">Log in toohello [Azure Portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="1caed-121">Откройте hello Azure Marketplace, щелкнув hello **New** можно, щелкнув значок в верхней части hello левой части панели мониторинга hello **выделить все** Далее tooMarketplace и выбрав **Интернет + мобильные устройства**.</span><span class="sxs-lookup"><span data-stu-id="1caed-121">Open hello Azure Marketplace by clicking hello **New** icon on hello top left of hello dashboard, click on **Select All** next tooMarketplace and selecting **Web + Mobile**.</span></span>
3. <span data-ttu-id="1caed-122">В hello Marketplace, выберите **Интернет + мобильные устройства**.</span><span class="sxs-lookup"><span data-stu-id="1caed-122">In hello Marketplace, select **Web + Mobile**.</span></span>
4. <span data-ttu-id="1caed-123">Нажмите кнопку hello **веб-приложение + SQL** значок.</span><span class="sxs-lookup"><span data-stu-id="1caed-123">Click hello **Web app + SQL** icon.</span></span>
5. <span data-ttu-id="1caed-124">После прочтения hello описание веб-приложения hello + SQL приложения, выберите **создать**.</span><span class="sxs-lookup"><span data-stu-id="1caed-124">After reading hello description of hello Web app + SQL app, select **Create**.</span></span>
6. <span data-ttu-id="1caed-125">Нажмите кнопку с каждой стороны (**группы ресурсов**, **веб-приложения**, **базы данных**, и **подписки**) и введите или выберите значения для необходимых hello поля:</span><span class="sxs-lookup"><span data-stu-id="1caed-125">Click on each part (**Resource Group**, **Web App**, **Database**, and **Subscription**) and enter or select values for hello required fields:</span></span>
   
   * <span data-ttu-id="1caed-126">Введите URL-адрес по своему выбору.</span><span class="sxs-lookup"><span data-stu-id="1caed-126">Enter a URL name of your choice</span></span>    
   * <span data-ttu-id="1caed-127">Настройте учетные данные для сервера базы данных.</span><span class="sxs-lookup"><span data-stu-id="1caed-127">Configure database server credentials</span></span>
   * <span data-ttu-id="1caed-128">Выберите tooyou ближайший регион hello</span><span class="sxs-lookup"><span data-stu-id="1caed-128">Select hello region closest tooyou</span></span>
     
     ![настройка приложения](./media/web-sites-php-sql-database-deploy-use-git/configure-db-settings.png)
7. <span data-ttu-id="1caed-130">Когда мы определим hello веб-приложение, нажмите кнопку **создать**.</span><span class="sxs-lookup"><span data-stu-id="1caed-130">When finished defining hello web app, click **Create**.</span></span>
   
    <span data-ttu-id="1caed-131">При создании веб-приложения hello hello **уведомления** кнопка будет мигать зеленым **успех** и hello обоих hello web app и hello база данных SQL в группе hello tooshow откройте колонку группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="1caed-131">When hello web app has been created, hello **Notifications** button will flash a green **SUCCESS** and hello resource group blade open tooshow both hello web app and hello SQL database in hello group.</span></span>
8. <span data-ttu-id="1caed-132">Щелкните значок веб-приложения hello в колонке hello ресурсов группы колонке tooopen hello веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="1caed-132">Click hello web app's icon in hello resource group blade tooopen hello web app's blade.</span></span>
   
    ![группа ресурсов веб-приложений](./media/web-sites-php-sql-database-deploy-use-git/resource-group-blade.png)
9. <span data-ttu-id="1caed-134">В колонке **Параметры** щелкните **Непрерывное развертывание** > **Настроить необходимые параметры**.</span><span class="sxs-lookup"><span data-stu-id="1caed-134">In **Settings** click **Continuous deployment** > **Configure required settings**.</span></span> <span data-ttu-id="1caed-135">Выберите **Локальный репозиторий Git** и щелкните **ОК**.</span><span class="sxs-lookup"><span data-stu-id="1caed-135">Select **Local Git Repository** and click **OK**.</span></span>
   
    ![где находится исходный код](./media/web-sites-php-sql-database-deploy-use-git/setup-local-git.png)
   
    <span data-ttu-id="1caed-137">Если репозиторий Git не был настроен предварительно, необходимо указать имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="1caed-137">If you have not set up a Git repository before, you must provide a user name and password.</span></span> <span data-ttu-id="1caed-138">toodo, нажмите кнопку **параметры** > **учетные данные развертывания** в колонке hello веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="1caed-138">toodo this, click **Settings** > **Deployment credentials** in hello web app's blade.</span></span>
   
    ![](./media/web-sites-php-sql-database-deploy-use-git/deployment-credentials.png)
10. <span data-ttu-id="1caed-139">В **параметры** щелкните **свойства** toosee hello Git URL-адрес удаленного понадобятся toouse toodeploy приложения PHP позднее.</span><span class="sxs-lookup"><span data-stu-id="1caed-139">In **Settings** click on **Properties** toosee hello Git remote URL you need toouse toodeploy your PHP app later.</span></span>

## <a name="get-sql-database-connection-information"></a><span data-ttu-id="1caed-140">Получение сведений о подключении к базе данных SQL</span><span class="sxs-lookup"><span data-stu-id="1caed-140">Get SQL Database connection information</span></span>
<span data-ttu-id="1caed-141">экземпляр базы данных SQL toohello tooconnect, связанных tooyour веб-приложения, приведет к необходимости hello сведения о соединении, указанные при создании базы данных hello.</span><span class="sxs-lookup"><span data-stu-id="1caed-141">tooconnect toohello SQL Database instance that is linked tooyour web app, your will need hello connection information, which you specified when you created hello database.</span></span> <span data-ttu-id="1caed-142">hello tooget сведения о подключении базы данных SQL, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="1caed-142">tooget hello SQL Database connection information, follow these steps:</span></span>

1. <span data-ttu-id="1caed-143">В колонке группы ресурсов hello щелкните значок базы данных SQL hello.</span><span class="sxs-lookup"><span data-stu-id="1caed-143">Back in hello resource group's blade, click hello SQL database's icon.</span></span>
2. <span data-ttu-id="1caed-144">В колонке базы данных SQL hello щелкните **параметры** > **свойства**, нажмите кнопку **Показать строки подключения базы данных**.</span><span class="sxs-lookup"><span data-stu-id="1caed-144">In hello SQL database's blade, click **Settings** > **Properties**, then click **Show database connection strings**.</span></span> 
   
    ![Просмотр свойств базы данных](./media/web-sites-php-sql-database-deploy-use-git/view-database-properties.png)
3. <span data-ttu-id="1caed-146">Из hello **PHP** раздел hello полученный диалогового окна, запишите значения hello для `Server`, `SQL Database`, и `User Name`.</span><span class="sxs-lookup"><span data-stu-id="1caed-146">From hello **PHP** section of hello resulting dialog, make note of hello values for `Server`, `SQL Database`, and `User Name`.</span></span> <span data-ttu-id="1caed-147">Будет использовать эти значения позже при публикации вашей tooAzure web приложения PHP службы приложений.</span><span class="sxs-lookup"><span data-stu-id="1caed-147">You will use these values later when publishing your PHP web app tooAzure App Service.</span></span>

## <a name="build-and-test-your-application-locally"></a><span data-ttu-id="1caed-148">Построение и тестирование приложения на локальном ресурсе</span><span class="sxs-lookup"><span data-stu-id="1caed-148">Build and test your application locally</span></span>
<span data-ttu-id="1caed-149">Регистрация приложения Hello представляет простое приложение PHP, позволяющий tooregister для события, предоставляя вашей имя и адрес электронной почты.</span><span class="sxs-lookup"><span data-stu-id="1caed-149">hello Registration application is a simple PHP application that allows you tooregister for an event by providing your name and email address.</span></span> <span data-ttu-id="1caed-150">Сведения о ранее зарегистрировавшихся пользователях отображаются в таблице.</span><span class="sxs-lookup"><span data-stu-id="1caed-150">Information about previous registrants is displayed in a table.</span></span> <span data-ttu-id="1caed-151">Сведения о регистрации хранятся в экземпляре базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="1caed-151">Registration information is stored in a SQL Database instance.</span></span> <span data-ttu-id="1caed-152">приложение Hello состоит из двух файлов (копирование и вставка кода ниже):</span><span class="sxs-lookup"><span data-stu-id="1caed-152">hello application consists of two files (copy/paste code available below):</span></span>

* <span data-ttu-id="1caed-153">**index.php**— вывод формы для регистрации и таблицы, содержащей сведения о зарегистрировавшихся пользователях.</span><span class="sxs-lookup"><span data-stu-id="1caed-153">**index.php**: Displays a form for registration and a table containing registrant information.</span></span>
* <span data-ttu-id="1caed-154">**CreateTable.PHP**: создает таблицу базы данных SQL hello для приложения hello.</span><span class="sxs-lookup"><span data-stu-id="1caed-154">**createtable.php**: Creates hello SQL Database table for hello application.</span></span> <span data-ttu-id="1caed-155">Этот файл будет использоваться только один раз.</span><span class="sxs-lookup"><span data-stu-id="1caed-155">This file will only be used once.</span></span>

<span data-ttu-id="1caed-156">приложения hello toorun локально, выполните шаги hello.</span><span class="sxs-lookup"><span data-stu-id="1caed-156">toorun hello application locally, follow hello steps below.</span></span> <span data-ttu-id="1caed-157">Обратите внимание, что эти предполагается, что у вас есть PHP и SQL Server Express установить на локальном компьютере, а также включены hello [расширение PDO для SQL Server][pdo-sqlsrv].</span><span class="sxs-lookup"><span data-stu-id="1caed-157">Note that these steps assume you have PHP and SQL Server Express set up on your local machine, and that you have enabled hello [PDO extension for SQL Server][pdo-sqlsrv].</span></span>

1. <span data-ttu-id="1caed-158">Создайте базу данных SQL Server под названием `registration`.</span><span class="sxs-lookup"><span data-stu-id="1caed-158">Create a SQL Server database called `registration`.</span></span> <span data-ttu-id="1caed-159">Это можно сделать из hello `sqlcmd` командной строки с помощью следующих команд:</span><span class="sxs-lookup"><span data-stu-id="1caed-159">You can do this from hello `sqlcmd` command prompt with these commands:</span></span>
   
        >sqlcmd -S localhost\sqlexpress -U <local user name> -P <local password>
        1> create database registration
        2> GO    
2. <span data-ttu-id="1caed-160">В корневом каталоге приложения создайте два файла — один с именем `createtable.php`, а другой с именем `index.php`.</span><span class="sxs-lookup"><span data-stu-id="1caed-160">In your application root directory, create two files in it - one called `createtable.php` and one called `index.php`.</span></span>
3. <span data-ttu-id="1caed-161">Откройте hello `createtable.php` и добавьте приведенный ниже код hello файла в текстовом редакторе или в интегрированной среде разработки.</span><span class="sxs-lookup"><span data-stu-id="1caed-161">Open hello `createtable.php` file in a text editor or IDE and add hello code below.</span></span> <span data-ttu-id="1caed-162">Этот код будет использоваться toocreate hello `registration_tbl` таблицы в hello `registration` базы данных.</span><span class="sxs-lookup"><span data-stu-id="1caed-162">This code will be used toocreate hello `registration_tbl` table in hello `registration` database.</span></span>
   
        <?php
        // DB connection info
        $host = "localhost\sqlexpress";
        $user = "user name";
        $pwd = "password";
        $db = "registration";
        try{
            $conn = new PDO( "sqlsrv:Server= $host ; Database = $db ", $user, $pwd);
            $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );
            $sql = "CREATE TABLE registration_tbl(
            id INT NOT NULL IDENTITY(1,1) 
            PRIMARY KEY(id),
            name VARCHAR(30),
            email VARCHAR(30),
            date DATE)";
            $conn->query($sql);
        }
        catch(Exception $e){
            die(print_r($e));
        }
        echo "<h3>Table created.</h3>";
        ?>
   
    <span data-ttu-id="1caed-163">Обратите внимание, что вам потребуется tooupdate hello значения для <code>$user</code> и <code>$pwd</code> локальное имя пользователя SQL Server и пароль.</span><span class="sxs-lookup"><span data-stu-id="1caed-163">Note that you will need tooupdate hello values for <code>$user</code> and <code>$pwd</code> with your local SQL Server user name and password.</span></span>
4. <span data-ttu-id="1caed-164">В конечном в корневом каталоге hello hello тип приложения hello, следующую команду:</span><span class="sxs-lookup"><span data-stu-id="1caed-164">In a terminal at hello root directory of hello application type hello following command:</span></span>
   
        php -S localhost:8000
5. <span data-ttu-id="1caed-165">Откройте веб-браузер и перейдите в слишком**http://localhost:8000/createtable.php**.</span><span class="sxs-lookup"><span data-stu-id="1caed-165">Open a web browser and browse too**http://localhost:8000/createtable.php**.</span></span> <span data-ttu-id="1caed-166">Это создаст hello `registration_tbl` таблицы в базе данных hello.</span><span class="sxs-lookup"><span data-stu-id="1caed-166">This will create hello `registration_tbl` table in hello database.</span></span>
6. <span data-ttu-id="1caed-167">Откройте hello **index.php** и добавьте hello базовый код HTML и CSS для страницы приветствия файла в текстовом редакторе или в интегрированной среде разработки (hello код PHP будут добавляться на последующих этапах).</span><span class="sxs-lookup"><span data-stu-id="1caed-167">Open hello **index.php** file in a text editor or IDE and add hello basic HTML and CSS code for hello page (hello PHP code will be added in later steps).</span></span>
   
        <html>
        <head>
        <Title>Registration Form</Title>
        <style type="text/css">
            body { background-color: #fff; border-top: solid 10px #000;
                color: #333; font-size: .85em; margin: 20; padding: 20;
                font-family: "Segoe UI", Verdana, Helvetica, Sans-Serif;
            }
            h1, h2, h3,{ color: #000; margin-bottom: 0; padding-bottom: 0; }
            h1 { font-size: 2em; }
            h2 { font-size: 1.75em; }
            h3 { font-size: 1.2em; }
            table { margin-top: 0.75em; }
            th { font-size: 1.2em; text-align: left; border: none; padding-left: 0; }
            td { padding: 0.25em 2em 0.25em 0em; border: 0 none; }
        </style>
        </head>
        <body>
        <h1>Register here!</h1>
        <p>Fill in your name and email address, then click <strong>Submit</strong> tooregister.</p>
        <form method="post" action="index.php" enctype="multipart/form-data" >
              Name  <input type="text" name="name" id="name"/></br>
              Email <input type="text" name="email" id="email"/></br>
              <input type="submit" name="submit" value="Submit" />
        </form>
        <?php
   
        ?>
        </body>
        </html>
7. <span data-ttu-id="1caed-168">В тегах PHP hello добавьте код PHP для соединения toohello базы данных.</span><span class="sxs-lookup"><span data-stu-id="1caed-168">Within hello PHP tags, add PHP code for connecting toohello database.</span></span>
   
        // DB connection info
        $host = "localhost\sqlexpress";
        $user = "user name";
        $pwd = "password";
        $db = "registration";
        // Connect toodatabase.
        try {
            $conn = new PDO( "sqlsrv:Server= $host ; Database = $db ", $user, $pwd);
            $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );
        }
        catch(Exception $e){
            die(var_dump($e));
        }
   
    <span data-ttu-id="1caed-169">Опять же, необходимо будет tooupdate hello значения для <code>$user</code> и <code>$pwd</code> с локальным именем MySQL пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="1caed-169">Again, you will need tooupdate hello values for <code>$user</code> and <code>$pwd</code> with your local MySQL user name and password.</span></span>
8. <span data-ttu-id="1caed-170">Следующий код подключения hello базы данных добавьте код для ввода сведений о регистрации в базу данных hello.</span><span class="sxs-lookup"><span data-stu-id="1caed-170">Following hello database connection code, add code for inserting registration information into hello database.</span></span>
   
        if(!empty($_POST)) {
        try {
            $name = $_POST['name'];
            $email = $_POST['email'];
            $date = date("Y-m-d");
            // Insert data
            $sql_insert = "INSERT INTO registration_tbl (name, email, date) 
                           VALUES (?,?,?)";
            $stmt = $conn->prepare($sql_insert);
            $stmt->bindValue(1, $name);
            $stmt->bindValue(2, $email);
            $stmt->bindValue(3, $date);
            $stmt->execute();
        }
        catch(Exception $e) {
            die(var_dump($e));
        }
        echo "<h3>Your're registered!</h3>";
        }
9. <span data-ttu-id="1caed-171">Наконец следующий код hello выше, добавьте код для извлечения данных из базы данных hello.</span><span class="sxs-lookup"><span data-stu-id="1caed-171">Finally, following hello code above, add code for retrieving data from hello database.</span></span>
   
        $sql_select = "SELECT * FROM registration_tbl";
        $stmt = $conn->query($sql_select);
        $registrants = $stmt->fetchAll(); 
        if(count($registrants) > 0) {
            echo "<h2>People who are registered:</h2>";
            echo "<table>";
            echo "<tr><th>Name</th>";
            echo "<th>Email</th>";
            echo "<th>Date</th></tr>";
            foreach($registrants as $registrant) {
                echo "<tr><td>".$registrant['name']."</td>";
                echo "<td>".$registrant['email']."</td>";
                echo "<td>".$registrant['date']."</td></tr>";
            }
             echo "</table>";
        } else {
            echo "<h3>No one is currently registered.</h3>";
        }

<span data-ttu-id="1caed-172">Теперь можно выполнять поиск слишком**http://localhost:8000/index.php** tootest приложения hello.</span><span class="sxs-lookup"><span data-stu-id="1caed-172">You can now browse too**http://localhost:8000/index.php** tootest hello application.</span></span>

## <a name="publish-your-application"></a><span data-ttu-id="1caed-173">Публикация приложения</span><span class="sxs-lookup"><span data-stu-id="1caed-173">Publish your application</span></span>
<span data-ttu-id="1caed-174">После тестирования приложения локально, его можно опубликовать tooApp службы веб-приложений с помощью Git.</span><span class="sxs-lookup"><span data-stu-id="1caed-174">After you have tested your application locally, you can publish it tooApp Service Web Apps using Git.</span></span> <span data-ttu-id="1caed-175">Тем не менее необходимо сначала tooupdate hello сведений о соединении в приложении hello.</span><span class="sxs-lookup"><span data-stu-id="1caed-175">However, you first need tooupdate hello database connection information in hello application.</span></span> <span data-ttu-id="1caed-176">С помощью hello сведений о соединении полученного ранее (в hello **сведения о соединении получить базу данных SQL** раздела), обновление hello следующую информацию в **оба** hello `createdatabase.php` и `index.php` файлы с hello соответствующие значения:</span><span class="sxs-lookup"><span data-stu-id="1caed-176">Using hello database connection information you obtained earlier (in hello **Get SQL Database connection information** section), update hello following information in **both** hello `createdatabase.php` and `index.php` files with hello appropriate values:</span></span>

    // DB connection info
    $host = "tcp:<value of Server>";
    $user = "<value of User Name>";
    $pwd = "<your password>";
    $db = "<value of SQL Database>";

> [!NOTE]
> <span data-ttu-id="1caed-177">В hello <code>$host</code>, значение hello Server должен указываться с <code>tcp:</code>.</span><span class="sxs-lookup"><span data-stu-id="1caed-177">In hello <code>$host</code>, hello value of Server must be prepended with <code>tcp:</code>.</span></span>
> 
> 

<span data-ttu-id="1caed-178">Теперь вы готовы tooset вверх публикации через Git и публикации приложения hello.</span><span class="sxs-lookup"><span data-stu-id="1caed-178">Now, you are ready tooset up Git publishing and publish hello application.</span></span>

> [!NOTE]
> <span data-ttu-id="1caed-179">Это же шаги, перечисленные в конец hello hello hello **создать веб-приложение Azure и настройте публикацию Git** выше.</span><span class="sxs-lookup"><span data-stu-id="1caed-179">These are hello same steps noted at hello end of hello **Create an Azure web app and set up Git publishing** section above.</span></span>
> 
> 

1. <span data-ttu-id="1caed-180">Откройте GitBash (или терминал, если Git находится в вашей `PATH`), измените каталоги toohello корневой каталог приложения (hello **регистрации** каталог), и выполнения hello следующие команды:</span><span class="sxs-lookup"><span data-stu-id="1caed-180">Open GitBash (or a terminal, if Git is in your `PATH`), change directories toohello root directory of your application (hello **registration** directory), and run hello following commands:</span></span>
   
        git init
        git add .
        git commit -m "initial commit"
        git remote add azure [URL for remote repository]
        git push azure master
   
    <span data-ttu-id="1caed-181">Появится для hello паролей, созданную ранее.</span><span class="sxs-lookup"><span data-stu-id="1caed-181">You will be prompted for hello password you created earlier.</span></span>
2. <span data-ttu-id="1caed-182">Обзор слишком**name].azurewebsites.net/createtable.php приложения http://[web** toocreate hello база данных SQL для приложения hello.</span><span class="sxs-lookup"><span data-stu-id="1caed-182">Browse too**http://[web app name].azurewebsites.net/createtable.php** toocreate hello SQL database table for hello application.</span></span>
3. <span data-ttu-id="1caed-183">Обзор слишком**name].azurewebsites.net/index.php приложения http://[web** toobegin, с помощью приложения hello.</span><span class="sxs-lookup"><span data-stu-id="1caed-183">Browse too**http://[web app name].azurewebsites.net/index.php** toobegin using hello application.</span></span>

<span data-ttu-id="1caed-184">После публикации приложения можно начать создание tooit изменения и использовать Git toopublish их.</span><span class="sxs-lookup"><span data-stu-id="1caed-184">After you have published your application, you can begin making changes tooit and use Git toopublish them.</span></span> 

## <a name="publish-changes-tooyour-application"></a><span data-ttu-id="1caed-185">Публикация приложения tooyour изменения</span><span class="sxs-lookup"><span data-stu-id="1caed-185">Publish changes tooyour application</span></span>
<span data-ttu-id="1caed-186">toopublish изменяет tooapplication, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="1caed-186">toopublish changes tooapplication, follow these steps:</span></span>

1. <span data-ttu-id="1caed-187">Внесите изменения tooyour приложения локально.</span><span class="sxs-lookup"><span data-stu-id="1caed-187">Make changes tooyour application locally.</span></span>
2. <span data-ttu-id="1caed-188">Откройте GitBash (или терминал, ИТ Git находится в вашей `PATH`), измените каталоги toohello корневой каталог приложения и запустите hello, следующие команды:</span><span class="sxs-lookup"><span data-stu-id="1caed-188">Open GitBash (or a terminal, it Git is in your `PATH`), change directories toohello root directory of your application, and run hello following commands:</span></span>
   
        git add .
        git commit -m "comment describing changes"
        git push azure master
   
    <span data-ttu-id="1caed-189">Появится для hello паролей, созданную ранее.</span><span class="sxs-lookup"><span data-stu-id="1caed-189">You will be prompted for hello password you created earlier.</span></span>
3. <span data-ttu-id="1caed-190">Обзор слишком**name].azurewebsites.net/index.php приложения http://[web** toosee изменений.</span><span class="sxs-lookup"><span data-stu-id="1caed-190">Browse too**http://[web app name].azurewebsites.net/index.php** toosee your changes.</span></span>

## <a name="whats-changed"></a><span data-ttu-id="1caed-191">Изменения</span><span class="sxs-lookup"><span data-stu-id="1caed-191">What's changed</span></span>
* <span data-ttu-id="1caed-192">Toohello руководство изменений из tooApp веб-сайтов службы. в разделе: [службе приложений Azure и ее влияние на существующие службы Azure](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="1caed-192">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

[install-php]: http://www.php.net/manual/en/install.php
[install-SQLExpress]: http://www.microsoft.com/download/details.aspx?id=29062
[install-Drivers]: http://www.microsoft.com/download/details.aspx?id=20098
[install-git]: http://git-scm.com/
[pdo-sqlsrv]: http://php.net/pdo_sqlsrv

