---
title: "Создание веб-приложения PHP-MySQL в службе приложений Azure и развертывание с помощью FTP"
description: "В этом учебнике показано, как создать веб-приложение PHP, которое хранит данные в MySQL и использует развертывание FTP в Azure."
services: app-service\web
documentationcenter: php
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 6d9d1de5-5868-48fd-8bad-decb4979cd65
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: d428dffc6b810a692be0ec39a5f9cca05f5439e3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-php-mysql-web-app-in-azure-app-service-and-deploy-using-ftp"></a><span data-ttu-id="a49ab-103">Создание веб-приложения PHP-MySQL в службе приложений Azure и развертывание с помощью FTP</span><span class="sxs-lookup"><span data-stu-id="a49ab-103">Create a PHP-MySQL web app in Azure App Service and deploy using FTP</span></span>
<span data-ttu-id="a49ab-104">В этом учебнике показано, как создать веб-приложение PHP-MySQL и развернуть его с помощью FTP.</span><span class="sxs-lookup"><span data-stu-id="a49ab-104">This tutorial shows you how to create a PHP-MySQL web app and how to deploy it using FTP.</span></span> <span data-ttu-id="a49ab-105">В этом учебнике предполагается, что на компьютере установлены компоненты [PHP][install-php], [MySQL][install-mysql], веб-сервер и FTP-клиент.</span><span class="sxs-lookup"><span data-stu-id="a49ab-105">This tutorial assumes you have [PHP][install-php], [MySQL][install-mysql], a web server, and an FTP client installed on your computer.</span></span> <span data-ttu-id="a49ab-106">Инструкции, приведенные в этом руководстве, применимы к любой операционной системе, включая Windows, Mac и Linux.</span><span class="sxs-lookup"><span data-stu-id="a49ab-106">The instructions in this tutorial can be followed on any operating system, including Windows, Mac, and  Linux.</span></span> <span data-ttu-id="a49ab-107">По завершении работы с этим учебником у вас будет работающее в Azure веб-приложение PHP-MySQL.</span><span class="sxs-lookup"><span data-stu-id="a49ab-107">Upon completing this guide, you will have a PHP/MySQL web app running in Azure.</span></span>

<span data-ttu-id="a49ab-108">Вы узнаете:</span><span class="sxs-lookup"><span data-stu-id="a49ab-108">You will learn:</span></span>

* <span data-ttu-id="a49ab-109">Как создать веб-приложение и базу данных MySQL с помощью портала Azure.</span><span class="sxs-lookup"><span data-stu-id="a49ab-109">How to create a web app and a MySQL database using the Azure Portal.</span></span> <span data-ttu-id="a49ab-110">Так как язык PHP включен в веб-приложениях по умолчанию, никаких дополнительных действий для выполнения вашего PHP-кода не требуется.</span><span class="sxs-lookup"><span data-stu-id="a49ab-110">Because PHP is enabled in Web Apps by default, nothing special is required to run your PHP code.</span></span>
* <span data-ttu-id="a49ab-111">Как опубликовать приложение в Azure с использованием FTP.</span><span class="sxs-lookup"><span data-stu-id="a49ab-111">How to publish your application to Azure using FTP.</span></span>

<span data-ttu-id="a49ab-112">Руководствуясь этим учебником, вы создадите на языке PHP простое веб-приложение для регистрации.</span><span class="sxs-lookup"><span data-stu-id="a49ab-112">By following this tutorial, you will build a simple registration web app in PHP.</span></span> <span data-ttu-id="a49ab-113">Приложение будет размещаться в веб-приложении.</span><span class="sxs-lookup"><span data-stu-id="a49ab-113">The application will be hosted in a Web App.</span></span> <span data-ttu-id="a49ab-114">Снимок экрана завершенного приложения приведен ниже:</span><span class="sxs-lookup"><span data-stu-id="a49ab-114">A screenshot of the completed application is below:</span></span>

![Веб-сайт Azure на PHP][running-app]

> [!NOTE]
> <span data-ttu-id="a49ab-116">Чтобы начать работу со службой приложений Azure до регистрации учетной записи Azure, перейдите в раздел [Пробная версия службы приложений](https://azure.microsoft.com/try/app-service/), где можно сразу создать кратковременное начальное мобильное веб-приложение в службе приложений.</span><span class="sxs-lookup"><span data-stu-id="a49ab-116">If you want to get started with Azure App Service before signing up for an account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="a49ab-117">Никаких кредитных карт и обязательств.</span><span class="sxs-lookup"><span data-stu-id="a49ab-117">No credit cards required, no commitments.</span></span> 
> 
> 

## <a name="create-a-web-app-and-set-up-ftp-publishing"></a><span data-ttu-id="a49ab-118">Создание веб-приложения и настройка публикации через FTP</span><span class="sxs-lookup"><span data-stu-id="a49ab-118">Create a web app and set up FTP publishing</span></span>
<span data-ttu-id="a49ab-119">Чтобы создать веб-приложение и базу данных MySQL, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="a49ab-119">Follow these steps to create a web app and a MySQL database:</span></span>

1. <span data-ttu-id="a49ab-120">Войдите на [портал Azure][management-portal].</span><span class="sxs-lookup"><span data-stu-id="a49ab-120">Login to the [Azure Portal][management-portal].</span></span>
2. <span data-ttu-id="a49ab-121">Щелкните значок **+ Создать** в верхнем левом углу портала Azure.</span><span class="sxs-lookup"><span data-stu-id="a49ab-121">Click the **+ New** icon on the top left of the Azure Portal.</span></span>
   
    ![Создание нового веб-сайта Azure][new-website]
3. <span data-ttu-id="a49ab-123">В поле поиска введите **Веб-приложение + MySQL** и щелкните элемент **Веб-приложение + MySQL**.</span><span class="sxs-lookup"><span data-stu-id="a49ab-123">In the search type **Web app + MySQL** and click on **Web app + MySQL**.</span></span>
   
    ![Настраиваемое создание нового веб-сайта][custom-create]
4. <span data-ttu-id="a49ab-125">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="a49ab-125">Click **Create**.</span></span> <span data-ttu-id="a49ab-126">Введите уникальное имя службы приложений, допустимое имя группы ресурсов и новый план обслуживания.</span><span class="sxs-lookup"><span data-stu-id="a49ab-126">Enter a unique app service name, a valid name for the resource group and a new service plan.</span></span>
   
    ![Задание имени группы ресурсов][resource-group]
5. <span data-ttu-id="a49ab-128">Введите значения для своей новой базы данных и примите условия.</span><span class="sxs-lookup"><span data-stu-id="a49ab-128">Enter values for your new database, including agreeing to the legal terms.</span></span>
   
    ![Создание новой базы данных MySQL][new-mysql-db]
6. <span data-ttu-id="a49ab-130">Когда веб-приложение будет создано, вы увидите колонку новой службы приложений.</span><span class="sxs-lookup"><span data-stu-id="a49ab-130">When the web app has been created, you will see the new app service blade.</span></span>
7. <span data-ttu-id="a49ab-131">Щелкните **Параметры** > **Учетные данные развертывания**.</span><span class="sxs-lookup"><span data-stu-id="a49ab-131">Click on **Settings** > **Deployment credentials**.</span></span> 
   
    ![Сброс учетных данных развертывания][set-deployment-credentials]
8. <span data-ttu-id="a49ab-133">Чтобы включить публикацию в FTP, необходимо указать имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="a49ab-133">To enable FTP publishing, you must provide a user name and password.</span></span> <span data-ttu-id="a49ab-134">Сохраните учетные данные и запишите имя пользователя и пароль, которые вы создали.</span><span class="sxs-lookup"><span data-stu-id="a49ab-134">Save the credentials and make a note of the user name and password you create.</span></span>
   
    ![Создание учетных данных для публикации][portal-ftp-username-password]

## <a name="build-and-test-your-app-locally"></a><span data-ttu-id="a49ab-136">Создание и тестирование приложения локально</span><span class="sxs-lookup"><span data-stu-id="a49ab-136">Build and test your app locally</span></span>
<span data-ttu-id="a49ab-137">Приложение регистрации представляет собой простое приложение PHP, которое позволяет регистрироваться на мероприятие, предоставляя свое имя и адрес электронной почты.</span><span class="sxs-lookup"><span data-stu-id="a49ab-137">The Registration application is a simple PHP application that allows you to register for an event by providing your name and email address.</span></span> <span data-ttu-id="a49ab-138">Сведения о ранее зарегистрировавшихся пользователях отображаются в таблице.</span><span class="sxs-lookup"><span data-stu-id="a49ab-138">Information about previous registrants is displayed in a table.</span></span> <span data-ttu-id="a49ab-139">Сведения о регистрации хранятся в базе данных MySQL.</span><span class="sxs-lookup"><span data-stu-id="a49ab-139">Registration information is stored in a MySQL database.</span></span> <span data-ttu-id="a49ab-140">Приложение состоит из двух файлов:</span><span class="sxs-lookup"><span data-stu-id="a49ab-140">The app consists of two files:</span></span>

* <span data-ttu-id="a49ab-141">**index.php**— вывод формы для регистрации и таблицы, содержащей сведения о зарегистрировавшихся пользователях.</span><span class="sxs-lookup"><span data-stu-id="a49ab-141">**index.php**: Displays a form for registration and a table containing registrant information.</span></span>
* <span data-ttu-id="a49ab-142">**createtable.php**— создание таблицы базы данных MySQL для приложения.</span><span class="sxs-lookup"><span data-stu-id="a49ab-142">**createtable.php**: Creates the MySQL table for the application.</span></span> <span data-ttu-id="a49ab-143">Этот файл будет использоваться только один раз.</span><span class="sxs-lookup"><span data-stu-id="a49ab-143">This file will only be used once.</span></span>

<span data-ttu-id="a49ab-144">Чтобы создать и запустить приложение локально, следуйте инструкциям.</span><span class="sxs-lookup"><span data-stu-id="a49ab-144">To build and run the app locally, follow the steps below.</span></span> <span data-ttu-id="a49ab-145">Обратите внимание, что предполагается наличие на локальном компьютере PHP, MySQL и веб-сервера, а также включение [расширения PDO для MySQL][pdo-mysql].</span><span class="sxs-lookup"><span data-stu-id="a49ab-145">Note that these steps assume you have PHP, MySQL, and a web server set up on your local machine, and that you have enabled the [PDO extension for MySQL][pdo-mysql].</span></span>

1. <span data-ttu-id="a49ab-146">Создание базы данных MySQL с именем `registration`.</span><span class="sxs-lookup"><span data-stu-id="a49ab-146">Create a MySQL database called `registration`.</span></span> <span data-ttu-id="a49ab-147">Это можно сделать в командной строке MySQL с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="a49ab-147">You can do this from the MySQL command prompt with this command:</span></span>
   
        mysql> create database registration;
2. <span data-ttu-id="a49ab-148">В корневом каталоге веб-сервера создайте папку с именем `registration`, а в ней два файла: один с именем `createtable.php`, а другой с именем `index.php`.</span><span class="sxs-lookup"><span data-stu-id="a49ab-148">In your web server's root directory, create a folder called `registration` and create two files in it - one called `createtable.php` and one called `index.php`.</span></span>
3. <span data-ttu-id="a49ab-149">Откройте файл `createtable.php` в текстовом редакторе или интегрированной среде разработки и добавьте приведенный ниже код.</span><span class="sxs-lookup"><span data-stu-id="a49ab-149">Open the `createtable.php` file in a text editor or IDE and add the code below.</span></span> <span data-ttu-id="a49ab-150">Этот код будет использоваться для создания таблицы `registration_tbl` в базе данных `registration`.</span><span class="sxs-lookup"><span data-stu-id="a49ab-150">This code will be used to create the `registration_tbl` table in the `registration` database.</span></span>
   
        <?php
        // DB connection info
        $host = "localhost";
        $user = "user name";
        $pwd = "password";
        $db = "registration";
        try{
            $conn = new PDO( "mysql:host=$host;dbname=$db", $user, $pwd);
            $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );
            $sql = "CREATE TABLE registration_tbl(
                        id INT NOT NULL AUTO_INCREMENT, 
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
   
   > [!NOTE]
   > <span data-ttu-id="a49ab-151">Вам потребуется обновить значения для <code>$user</code> и <code>$pwd</code> с локальным именем MySQL пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="a49ab-151">You will need to update the values for <code>$user</code> and <code>$pwd</code> with your local MySQL user name and password.</span></span>
   > 
   > 
4. <span data-ttu-id="a49ab-152">Откройте веб-браузер и перейдите по адресу [http://localhost/registration/createtable.php][localhost-createtable].</span><span class="sxs-lookup"><span data-stu-id="a49ab-152">Open a web browser and browse to [http://localhost/registration/createtable.php][localhost-createtable].</span></span> <span data-ttu-id="a49ab-153">В результате в базе данных будет создана таблица `registration_tbl` .</span><span class="sxs-lookup"><span data-stu-id="a49ab-153">This will create the `registration_tbl` table in the database.</span></span>
5. <span data-ttu-id="a49ab-154">Откройте файл **index.php** в текстовом редакторе или в интегрированной среде разработки и добавьте базовый HTML-код и CSS для страницы (PHP-код будет добавлен позднее).</span><span class="sxs-lookup"><span data-stu-id="a49ab-154">Open the **index.php** file in a text editor or IDE and add the basic HTML and CSS code for the page (the PHP code will be added in later steps).</span></span>
   
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
        <p>Fill in your name and email address, then click <strong>Submit</strong> to register.</p>
        <form method="post" action="index.php" enctype="multipart/form-data" >
              Name  <input type="text" name="name" id="name"/></br>
              Email <input type="text" name="email" id="email"/></br>
              <input type="submit" name="submit" value="Submit" />
        </form>
        <?php
   
        ?>
        </body>
        </html>
6. <span data-ttu-id="a49ab-155">Внутри тегов PHP добавьте PHP-код для подключения к базе данных.</span><span class="sxs-lookup"><span data-stu-id="a49ab-155">Within the PHP tags, add PHP code for connecting to the database.</span></span>
   
        // DB connection info
        $host = "localhost";
        $user = "user name";
        $pwd = "password";
        $db = "registration";
        // Connect to database.
        try {
            $conn = new PDO( "mysql:host=$host;dbname=$db", $user, $pwd);
            $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );
        }
        catch(Exception $e){
            die(var_dump($e));
        }
   
   > [!NOTE]
   > <span data-ttu-id="a49ab-156">Опять же, необходимо обновить значения для <code>$user</code> и <code>$pwd</code> с локальным именем MySQL пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="a49ab-156">Again, you will need to update the values for <code>$user</code> and <code>$pwd</code> with your local MySQL user name and password.</span></span>
   > 
   > 
7. <span data-ttu-id="a49ab-157">После кода подключения к базе данных добавьте код для вставки регистрационных данных в базу данных.</span><span class="sxs-lookup"><span data-stu-id="a49ab-157">Following the database connection code, add code for inserting registration information into the database.</span></span>
   
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
8. <span data-ttu-id="a49ab-158">Наконец, после вышеприведенного кода добавьте код для извлечения данных из базы данных.</span><span class="sxs-lookup"><span data-stu-id="a49ab-158">Finally, following the code above, add code for retrieving data from the database.</span></span>
   
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

<span data-ttu-id="a49ab-159">Теперь можно перейти по адресу [http://localhost/registration/index.php][localhost-index] для тестирования приложения.</span><span class="sxs-lookup"><span data-stu-id="a49ab-159">You can now browse to [http://localhost/registration/index.php][localhost-index] to test the app.</span></span>

## <a name="get-mysql-and-ftp-connection-information"></a><span data-ttu-id="a49ab-160">Получение сведений о подключении к MySQL и FTP</span><span class="sxs-lookup"><span data-stu-id="a49ab-160">Get MySQL and FTP connection information</span></span>
<span data-ttu-id="a49ab-161">Чтобы подключиться к базе данных MySQL, которая работает в веб-приложениях, вам потребуются сведения о подключении.</span><span class="sxs-lookup"><span data-stu-id="a49ab-161">To connect to the MySQL database that is running in Web Apps, your will need the connection information.</span></span> <span data-ttu-id="a49ab-162">Чтобы получить сведения о подключении к MySQL, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="a49ab-162">To get MySQL connection information, follow these steps:</span></span>

1. <span data-ttu-id="a49ab-163">В колонке веб-приложения службы приложений щелкните ссылку группы ресурсов:</span><span class="sxs-lookup"><span data-stu-id="a49ab-163">From the app service web app blade click on the resource group link:</span></span>
   
    ![Выбор группы ресурсов][select-resourcegroup]
2. <span data-ttu-id="a49ab-165">В группе ресурсов щелкните базу данных.</span><span class="sxs-lookup"><span data-stu-id="a49ab-165">From your resource group, click the database:</span></span>
   
    ![Выбор базы данных][select-database]
3. <span data-ttu-id="a49ab-167">В сводке базы данных щелкните **Параметры** > **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="a49ab-167">From the database summary, select **Settings** > **Properties**.</span></span>
   
    ![Выбор свойств][select-properties]
4. <span data-ttu-id="a49ab-169">Запишите значения `Database`, `Host`, `User Id` и `Password`.</span><span class="sxs-lookup"><span data-stu-id="a49ab-169">Make note of the values for `Database`, `Host`, `User Id`, and `Password`.</span></span>
   
    ![Запись свойств][note-properties]
5. <span data-ttu-id="a49ab-171">В веб-приложении в правом нижнем углу страницы щелкните ссылку **Загрузить профиль публикации** .</span><span class="sxs-lookup"><span data-stu-id="a49ab-171">From your web app, click the **Download publish profile** link at the bottom right corner of the page:</span></span>
   
    ![Загрузить профиль публикации][download-publish-profile]
6. <span data-ttu-id="a49ab-173">Откройте файл `.publishsettings` в редакторе XML.</span><span class="sxs-lookup"><span data-stu-id="a49ab-173">Open the `.publishsettings` file in an XML editor.</span></span> 
7. <span data-ttu-id="a49ab-174">Найдите элемент `<publishProfile >` с методом `publishMethod="FTP"` следующего вида:</span><span class="sxs-lookup"><span data-stu-id="a49ab-174">Find the `<publishProfile >` element with `publishMethod="FTP"` that looks similar to this:</span></span>
   
        <publishProfile publishMethod="FTP" publishUrl="ftp://[mysite].azurewebsites.net/site/wwwroot" ftpPassiveMode="True" userName="[username]" userPWD="[password]" destinationAppUrl="http://[name].antdf0.antares-test.windows-int.net" 
            ...
        </publishProfile>

<span data-ttu-id="a49ab-175">Обратите внимание на значения атрибутов `publishUrl`, `userName` и `userPWD`.</span><span class="sxs-lookup"><span data-stu-id="a49ab-175">Make note of the `publishUrl`, `userName`, and `userPWD` attributes.</span></span>

## <a name="publish-your-app"></a><span data-ttu-id="a49ab-176">Публикация приложения</span><span class="sxs-lookup"><span data-stu-id="a49ab-176">Publish your app</span></span>
<span data-ttu-id="a49ab-177">После локального тестирования приложения его можно опубликовать в веб-приложении с помощью FTP.</span><span class="sxs-lookup"><span data-stu-id="a49ab-177">After you have tested your app locally, you can publish it to your web app using FTP.</span></span> <span data-ttu-id="a49ab-178">Тем не менее, необходимо сначала обновить в приложении сведения подключения к базе данных.</span><span class="sxs-lookup"><span data-stu-id="a49ab-178">However, you first need to update the database connection information in the application.</span></span> <span data-ttu-id="a49ab-179">При помощи полученных ранее данных подключения к базе данных (ознакомьтесь с разделом **Получение сведений о подключении к базе данных MySQL и FTP**) измените приведенные ниже сведения в **обоих** файлах (`createdatabase.php` и `index.php`), используя соответствующие значения.</span><span class="sxs-lookup"><span data-stu-id="a49ab-179">Using the database connection information you obtained earlier (in the **Get MySQL and FTP connection information** section), update the following information in **both** the `createdatabase.php` and `index.php` files with the appropriate values:</span></span>

    // DB connection info
    $host = "value of Data Source";
    $user = "value of User Id";
    $pwd = "value of Password";
    $db = "value of Database";

<span data-ttu-id="a49ab-180">Теперь все готово для публикации приложения через FTP.</span><span class="sxs-lookup"><span data-stu-id="a49ab-180">Now you are ready to publish your app using FTP.</span></span>

1. <span data-ttu-id="a49ab-181">Откройте выбранный клиент FTP.</span><span class="sxs-lookup"><span data-stu-id="a49ab-181">Open your FTP client of choice.</span></span>
2. <span data-ttu-id="a49ab-182">Введите в FTP-клиент *имя узла* из атрибута `publishUrl`, записанное ранее.</span><span class="sxs-lookup"><span data-stu-id="a49ab-182">Enter the *host name portion* from the `publishUrl` attribute you noted above into your FTP client.</span></span>
3. <span data-ttu-id="a49ab-183">Введите в FTP-клиент атрибуты `userName` и `userPWD`, записанные ранее, без изменений.</span><span class="sxs-lookup"><span data-stu-id="a49ab-183">Enter the `userName` and `userPWD` attributes you noted above unchanged into your FTP client.</span></span>
4. <span data-ttu-id="a49ab-184">Установите подключение.</span><span class="sxs-lookup"><span data-stu-id="a49ab-184">Establish a connection.</span></span>

<span data-ttu-id="a49ab-185">После подключения можно будет отправлять и загружать файлы.</span><span class="sxs-lookup"><span data-stu-id="a49ab-185">After you have connected you will be able to upload and download files as needed.</span></span> <span data-ttu-id="a49ab-186">Убедитесь, что файлы передаются в корневой каталог, то есть в каталог `/site/wwwroot`.</span><span class="sxs-lookup"><span data-stu-id="a49ab-186">Be sure that you are uploading files to the root directory, which is `/site/wwwroot`.</span></span>

<span data-ttu-id="a49ab-187">После передачи файлов `index.php` и `createtable.php` перейдите по адресу **http://[имя_сайта].azurewebsites.net/createtable.php**, чтобы создать таблицу базы данных MySQL для приложения, а затем перейдите по адресу **http://[имя_сайта].azurewebsites.net/index.php**, чтобы приступить к работе с приложением.</span><span class="sxs-lookup"><span data-stu-id="a49ab-187">After uploading both `index.php` and `createtable.php`, browse to **http://[site name].azurewebsites.net/createtable.php** to create the MySQL table for the application, then browse to **http://[site name].azurewebsites.net/index.php** to begin using the application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a49ab-188">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a49ab-188">Next steps</span></span>
<span data-ttu-id="a49ab-189">Дополнительную информацию можно найти в [Центре разработчика PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="a49ab-189">For more information, see the [PHP Developer Center](/develop/php/).</span></span>

[install-php]: http://www.php.net/manual/en/install.php
[install-mysql]: http://dev.mysql.com/doc/refman/5.6/en/installing.html
[pdo-mysql]: http://www.php.net/manual/en/ref.pdo-mysql.php
[localhost-createtable]: http://localhost/tasklist/createtable.php
[localhost-index]: http://localhost/tasklist/index.php
[running-app]: ./media/web-sites-php-mysql-deploy-use-ftp/running_app_2.png
[new-website]: ./media/web-sites-php-mysql-deploy-use-ftp/new_website2.png
[custom-create]: ./media/web-sites-php-mysql-deploy-use-ftp/create_web_mysql.png
[website-details]: ./media/web-sites-php-web-site-mysql-deploy-use-ftp/website_details.jpg
[new-mysql-db]: ./media/web-sites-php-mysql-deploy-use-ftp/create_db.png
[go-to-webapp]: ./media/web-sites-php-mysql-deploy-use-ftp/select_webapp.png
[set-deployment-credentials]: ./media/web-sites-php-mysql-deploy-use-ftp/set_credentials.png
[portal-ftp-username-password]: ./media/web-sites-php-mysql-deploy-use-ftp/save_credentials.png
[resource-group]: ./media/web-sites-php-mysql-deploy-use-ftp/set_group.png
[new-web-app]: ./media/web-sites-php-mysql-deploy-use-ftp/create_wa.png
[select-database]: ./media/web-sites-php-mysql-deploy-use-ftp/select_database.png
[select-resourcegroup]: ./media/web-sites-php-mysql-deploy-use-ftp/select_resourcegroup.png
[select-properties]: ./media/web-sites-php-mysql-deploy-use-ftp/select_properties.png
[note-properties]: ./media/web-sites-php-mysql-deploy-use-ftp/note-properties.png

[connection-string-info]: ./media/web-sites-php-web-site-mysql-deploy-use-ftp/connection_string_info.png
[management-portal]: https://portal.azure.com
[download-publish-profile]: ./media/web-sites-php-mysql-deploy-use-ftp/download_publish_profile_3.png

