---
title: "aaaCreate PHP-MySQL веб-приложения в службе приложений Azure и развернуть с помощью FTP"
description: "Учебник, в котором показано, как toocreate PHP веб-приложение, которое сохраняет данные в MySQL и использование tooAzure FTP-развертывания."
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
ms.openlocfilehash: 4d3b56a8ac63d0eba0dc0aec1b62e6d12f601bf1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-php-mysql-web-app-in-azure-app-service-and-deploy-using-ftp"></a><span data-ttu-id="7888d-103">Создание веб-приложения PHP-MySQL в службе приложений Azure и развертывание с помощью FTP</span><span class="sxs-lookup"><span data-stu-id="7888d-103">Create a PHP-MySQL web app in Azure App Service and deploy using FTP</span></span>
<span data-ttu-id="7888d-104">В этом учебнике показано, как toocreate PHP-MySQL веб-приложения и как toodeploy ее с помощью FTP.</span><span class="sxs-lookup"><span data-stu-id="7888d-104">This tutorial shows you how toocreate a PHP-MySQL web app and how toodeploy it using FTP.</span></span> <span data-ttu-id="7888d-105">В этом учебнике предполагается, что на компьютере установлены компоненты [PHP][install-php], [MySQL][install-mysql], веб-сервер и FTP-клиент.</span><span class="sxs-lookup"><span data-stu-id="7888d-105">This tutorial assumes you have [PHP][install-php], [MySQL][install-mysql], a web server, and an FTP client installed on your computer.</span></span> <span data-ttu-id="7888d-106">Hello инструкциям этого учебника можно выполнять в любой операционной системе, включая Windows, Mac и Linux.</span><span class="sxs-lookup"><span data-stu-id="7888d-106">hello instructions in this tutorial can be followed on any operating system, including Windows, Mac, and  Linux.</span></span> <span data-ttu-id="7888d-107">По завершении работы с этим учебником у вас будет работающее в Azure веб-приложение PHP-MySQL.</span><span class="sxs-lookup"><span data-stu-id="7888d-107">Upon completing this guide, you will have a PHP/MySQL web app running in Azure.</span></span>

<span data-ttu-id="7888d-108">Вы узнаете:</span><span class="sxs-lookup"><span data-stu-id="7888d-108">You will learn:</span></span>

* <span data-ttu-id="7888d-109">Как toocreate веб-приложения и MySQL базы данных с помощью портала Azure hello.</span><span class="sxs-lookup"><span data-stu-id="7888d-109">How toocreate a web app and a MySQL database using hello Azure Portal.</span></span> <span data-ttu-id="7888d-110">Так, как в веб-приложений PHP включена по умолчанию, никаких дополнительных действий не является обязательным toorun кода PHP.</span><span class="sxs-lookup"><span data-stu-id="7888d-110">Because PHP is enabled in Web Apps by default, nothing special is required toorun your PHP code.</span></span>
* <span data-ttu-id="7888d-111">Как toopublish tooAzure приложения с помощью FTP.</span><span class="sxs-lookup"><span data-stu-id="7888d-111">How toopublish your application tooAzure using FTP.</span></span>

<span data-ttu-id="7888d-112">Руководствуясь этим учебником, вы создадите на языке PHP простое веб-приложение для регистрации.</span><span class="sxs-lookup"><span data-stu-id="7888d-112">By following this tutorial, you will build a simple registration web app in PHP.</span></span> <span data-ttu-id="7888d-113">в веб-приложение будет размещено приложение Hello.</span><span class="sxs-lookup"><span data-stu-id="7888d-113">hello application will be hosted in a Web App.</span></span> <span data-ttu-id="7888d-114">Снимок экрана приложения hello завершения используется следующим образом:</span><span class="sxs-lookup"><span data-stu-id="7888d-114">A screenshot of hello completed application is below:</span></span>

![Веб-сайт Azure на PHP][running-app]

> [!NOTE]
> <span data-ttu-id="7888d-116">Tooget работы в службе приложений Azure перед регистрацией для учетной записи, перейдите слишком[повторите служб приложений](https://azure.microsoft.com/try/app-service/), в котором можно немедленно создать кратковременных начальный веб-приложения в службе приложений.</span><span class="sxs-lookup"><span data-stu-id="7888d-116">If you want tooget started with Azure App Service before signing up for an account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="7888d-117">Никаких кредитных карт и обязательств.</span><span class="sxs-lookup"><span data-stu-id="7888d-117">No credit cards required, no commitments.</span></span> 
> 
> 

## <a name="create-a-web-app-and-set-up-ftp-publishing"></a><span data-ttu-id="7888d-118">Создание веб-приложения и настройка публикации через FTP</span><span class="sxs-lookup"><span data-stu-id="7888d-118">Create a web app and set up FTP publishing</span></span>
<span data-ttu-id="7888d-119">Выполните эти шаги toocreate веб-приложения и базы данных MySQL.</span><span class="sxs-lookup"><span data-stu-id="7888d-119">Follow these steps toocreate a web app and a MySQL database:</span></span>

1. <span data-ttu-id="7888d-120">Имя входа toohello [портала Azure][management-portal].</span><span class="sxs-lookup"><span data-stu-id="7888d-120">Login toohello [Azure Portal][management-portal].</span></span>
2. <span data-ttu-id="7888d-121">Нажмите кнопку hello **+ создать** значок hello сверху слева от hello портала Azure.</span><span class="sxs-lookup"><span data-stu-id="7888d-121">Click hello **+ New** icon on hello top left of hello Azure Portal.</span></span>
   
    ![Создание нового веб-сайта Azure][new-website]
3. <span data-ttu-id="7888d-123">В типе поиска hello **веб-приложение + MySQL** и выберите команду **веб-приложение + MySQL**.</span><span class="sxs-lookup"><span data-stu-id="7888d-123">In hello search type **Web app + MySQL** and click on **Web app + MySQL**.</span></span>
   
    ![Настраиваемое создание нового веб-сайта][custom-create]
4. <span data-ttu-id="7888d-125">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="7888d-125">Click **Create**.</span></span> <span data-ttu-id="7888d-126">Введите имя уникальным приложения службы, допустимое имя для группы ресурсов hello и новый план служб.</span><span class="sxs-lookup"><span data-stu-id="7888d-126">Enter a unique app service name, a valid name for hello resource group and a new service plan.</span></span>
   
    ![Задание имени группы ресурсов][resource-group]
5. <span data-ttu-id="7888d-128">Введите значения для новой базы данных, включая согласие toohello условия.</span><span class="sxs-lookup"><span data-stu-id="7888d-128">Enter values for your new database, including agreeing toohello legal terms.</span></span>
   
    ![Создание новой базы данных MySQL][new-mysql-db]
6. <span data-ttu-id="7888d-130">При создании веб-приложения hello вы увидите hello Новая колонка приложения службы.</span><span class="sxs-lookup"><span data-stu-id="7888d-130">When hello web app has been created, you will see hello new app service blade.</span></span>
7. <span data-ttu-id="7888d-131">Щелкните **Параметры** > **Учетные данные развертывания**.</span><span class="sxs-lookup"><span data-stu-id="7888d-131">Click on **Settings** > **Deployment credentials**.</span></span> 
   
    ![Сброс учетных данных развертывания][set-deployment-credentials]
8. <span data-ttu-id="7888d-133">tooenable публикации FTP, необходимо указать имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="7888d-133">tooenable FTP publishing, you must provide a user name and password.</span></span> <span data-ttu-id="7888d-134">Сохранить учетные данные hello и запишите hello имя пользователя и пароль, который вы создаете.</span><span class="sxs-lookup"><span data-stu-id="7888d-134">Save hello credentials and make a note of hello user name and password you create.</span></span>
   
    ![Создание учетных данных для публикации][portal-ftp-username-password]

## <a name="build-and-test-your-app-locally"></a><span data-ttu-id="7888d-136">Создание и тестирование приложения локально</span><span class="sxs-lookup"><span data-stu-id="7888d-136">Build and test your app locally</span></span>
<span data-ttu-id="7888d-137">Регистрация приложения Hello представляет простое приложение PHP, позволяющий tooregister для события, предоставляя вашей имя и адрес электронной почты.</span><span class="sxs-lookup"><span data-stu-id="7888d-137">hello Registration application is a simple PHP application that allows you tooregister for an event by providing your name and email address.</span></span> <span data-ttu-id="7888d-138">Сведения о ранее зарегистрировавшихся пользователях отображаются в таблице.</span><span class="sxs-lookup"><span data-stu-id="7888d-138">Information about previous registrants is displayed in a table.</span></span> <span data-ttu-id="7888d-139">Сведения о регистрации хранятся в базе данных MySQL.</span><span class="sxs-lookup"><span data-stu-id="7888d-139">Registration information is stored in a MySQL database.</span></span> <span data-ttu-id="7888d-140">приложение Hello состоит из двух файлов:</span><span class="sxs-lookup"><span data-stu-id="7888d-140">hello app consists of two files:</span></span>

* <span data-ttu-id="7888d-141">**index.php**— вывод формы для регистрации и таблицы, содержащей сведения о зарегистрировавшихся пользователях.</span><span class="sxs-lookup"><span data-stu-id="7888d-141">**index.php**: Displays a form for registration and a table containing registrant information.</span></span>
* <span data-ttu-id="7888d-142">**CreateTable.PHP**: создает таблицу hello MySQL для приложения hello.</span><span class="sxs-lookup"><span data-stu-id="7888d-142">**createtable.php**: Creates hello MySQL table for hello application.</span></span> <span data-ttu-id="7888d-143">Этот файл будет использоваться только один раз.</span><span class="sxs-lookup"><span data-stu-id="7888d-143">This file will only be used once.</span></span>

<span data-ttu-id="7888d-144">toobuild и выполнения hello приложения локально, выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="7888d-144">toobuild and run hello app locally, follow hello steps below.</span></span> <span data-ttu-id="7888d-145">Обратите внимание, что эти шаги предполагают, что у вас есть PHP, MySQL и веб-сервер на локальном компьютере и что включена hello [расширение PDO для MySQL][pdo-mysql].</span><span class="sxs-lookup"><span data-stu-id="7888d-145">Note that these steps assume you have PHP, MySQL, and a web server set up on your local machine, and that you have enabled hello [PDO extension for MySQL][pdo-mysql].</span></span>

1. <span data-ttu-id="7888d-146">Создание базы данных MySQL с именем `registration`.</span><span class="sxs-lookup"><span data-stu-id="7888d-146">Create a MySQL database called `registration`.</span></span> <span data-ttu-id="7888d-147">Это можно сделать из hello MySQL командной строки с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="7888d-147">You can do this from hello MySQL command prompt with this command:</span></span>
   
        mysql> create database registration;
2. <span data-ttu-id="7888d-148">В корневом каталоге веб-сервера создайте папку с именем `registration`, а в ней два файла: один с именем `createtable.php`, а другой с именем `index.php`.</span><span class="sxs-lookup"><span data-stu-id="7888d-148">In your web server's root directory, create a folder called `registration` and create two files in it - one called `createtable.php` and one called `index.php`.</span></span>
3. <span data-ttu-id="7888d-149">Откройте hello `createtable.php` и добавьте приведенный ниже код hello файла в текстовом редакторе или в интегрированной среде разработки.</span><span class="sxs-lookup"><span data-stu-id="7888d-149">Open hello `createtable.php` file in a text editor or IDE and add hello code below.</span></span> <span data-ttu-id="7888d-150">Этот код будет использоваться toocreate hello `registration_tbl` таблицы в hello `registration` базы данных.</span><span class="sxs-lookup"><span data-stu-id="7888d-150">This code will be used toocreate hello `registration_tbl` table in hello `registration` database.</span></span>
   
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
   > <span data-ttu-id="7888d-151">Вам потребуются значения hello tooupdate для <code>$user</code> и <code>$pwd</code> с локальным именем MySQL пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="7888d-151">You will need tooupdate hello values for <code>$user</code> and <code>$pwd</code> with your local MySQL user name and password.</span></span>
   > 
   > 
4. <span data-ttu-id="7888d-152">Откройте веб-браузер и перейдите в слишком[http://localhost/registration/createtable.php][localhost-createtable].</span><span class="sxs-lookup"><span data-stu-id="7888d-152">Open a web browser and browse too[http://localhost/registration/createtable.php][localhost-createtable].</span></span> <span data-ttu-id="7888d-153">Это создаст hello `registration_tbl` таблицы в базе данных hello.</span><span class="sxs-lookup"><span data-stu-id="7888d-153">This will create hello `registration_tbl` table in hello database.</span></span>
5. <span data-ttu-id="7888d-154">Откройте hello **index.php** и добавьте hello базовый код HTML и CSS для страницы приветствия файла в текстовом редакторе или в интегрированной среде разработки (hello код PHP будут добавляться на последующих этапах).</span><span class="sxs-lookup"><span data-stu-id="7888d-154">Open hello **index.php** file in a text editor or IDE and add hello basic HTML and CSS code for hello page (hello PHP code will be added in later steps).</span></span>
   
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
6. <span data-ttu-id="7888d-155">В тегах PHP hello добавьте код PHP для соединения toohello базы данных.</span><span class="sxs-lookup"><span data-stu-id="7888d-155">Within hello PHP tags, add PHP code for connecting toohello database.</span></span>
   
        // DB connection info
        $host = "localhost";
        $user = "user name";
        $pwd = "password";
        $db = "registration";
        // Connect toodatabase.
        try {
            $conn = new PDO( "mysql:host=$host;dbname=$db", $user, $pwd);
            $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );
        }
        catch(Exception $e){
            die(var_dump($e));
        }
   
   > [!NOTE]
   > <span data-ttu-id="7888d-156">Опять же, необходимо будет tooupdate hello значения для <code>$user</code> и <code>$pwd</code> с локальным именем MySQL пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="7888d-156">Again, you will need tooupdate hello values for <code>$user</code> and <code>$pwd</code> with your local MySQL user name and password.</span></span>
   > 
   > 
7. <span data-ttu-id="7888d-157">Следующий код подключения hello базы данных добавьте код для ввода сведений о регистрации в базу данных hello.</span><span class="sxs-lookup"><span data-stu-id="7888d-157">Following hello database connection code, add code for inserting registration information into hello database.</span></span>
   
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
8. <span data-ttu-id="7888d-158">Наконец следующий код hello выше, добавьте код для извлечения данных из базы данных hello.</span><span class="sxs-lookup"><span data-stu-id="7888d-158">Finally, following hello code above, add code for retrieving data from hello database.</span></span>
   
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

<span data-ttu-id="7888d-159">Теперь можно выполнять поиск слишком[http://localhost/registration/index.php] [ localhost-index] tootest приложение hello.</span><span class="sxs-lookup"><span data-stu-id="7888d-159">You can now browse too[http://localhost/registration/index.php][localhost-index] tootest hello app.</span></span>

## <a name="get-mysql-and-ftp-connection-information"></a><span data-ttu-id="7888d-160">Получение сведений о подключении к MySQL и FTP</span><span class="sxs-lookup"><span data-stu-id="7888d-160">Get MySQL and FTP connection information</span></span>
<span data-ttu-id="7888d-161">База данных MySQL tooconnect toohello, на котором выполняется в веб-приложениях, приведет к необходимости hello сведения о соединении.</span><span class="sxs-lookup"><span data-stu-id="7888d-161">tooconnect toohello MySQL database that is running in Web Apps, your will need hello connection information.</span></span> <span data-ttu-id="7888d-162">tooget сведения о соединении MySQL, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="7888d-162">tooget MySQL connection information, follow these steps:</span></span>

1. <span data-ttu-id="7888d-163">Из службы приложения hello колонки веб-приложения щелкните ссылку группы ресурсов hello:</span><span class="sxs-lookup"><span data-stu-id="7888d-163">From hello app service web app blade click on hello resource group link:</span></span>
   
    ![Выбор группы ресурсов][select-resourcegroup]
2. <span data-ttu-id="7888d-165">В группе ресурсов выберите hello базы данных:</span><span class="sxs-lookup"><span data-stu-id="7888d-165">From your resource group, click hello database:</span></span>
   
    ![Выбор базы данных][select-database]
3. <span data-ttu-id="7888d-167">Сводка базы данных hello, выберите **параметры** > **свойства**.</span><span class="sxs-lookup"><span data-stu-id="7888d-167">From hello database summary, select **Settings** > **Properties**.</span></span>
   
    ![Выбор свойств][select-properties]
4. <span data-ttu-id="7888d-169">Запишите значения hello для `Database`, `Host`, `User Id`, и `Password`.</span><span class="sxs-lookup"><span data-stu-id="7888d-169">Make note of hello values for `Database`, `Host`, `User Id`, and `Password`.</span></span>
   
    ![Запись свойств][note-properties]
5. <span data-ttu-id="7888d-171">Выберите веб-приложения hello **загрузить профиль публикации** ссылку в hello нижнем правом углу страницы приветствия:</span><span class="sxs-lookup"><span data-stu-id="7888d-171">From your web app, click hello **Download publish profile** link at hello bottom right corner of hello page:</span></span>
   
    ![Загрузить профиль публикации][download-publish-profile]
6. <span data-ttu-id="7888d-173">Откройте hello `.publishsettings` файл в редакторе XML.</span><span class="sxs-lookup"><span data-stu-id="7888d-173">Open hello `.publishsettings` file in an XML editor.</span></span> 
7. <span data-ttu-id="7888d-174">Найти hello `<publishProfile >` элемент с `publishMethod="FTP"` это выглядит как toothis:</span><span class="sxs-lookup"><span data-stu-id="7888d-174">Find hello `<publishProfile >` element with `publishMethod="FTP"` that looks similar toothis:</span></span>
   
        <publishProfile publishMethod="FTP" publishUrl="ftp://[mysite].azurewebsites.net/site/wwwroot" ftpPassiveMode="True" userName="[username]" userPWD="[password]" destinationAppUrl="http://[name].antdf0.antares-test.windows-int.net" 
            ...
        </publishProfile>

<span data-ttu-id="7888d-175">Запишите hello `publishUrl`, `userName`, и `userPWD` атрибуты.</span><span class="sxs-lookup"><span data-stu-id="7888d-175">Make note of hello `publishUrl`, `userName`, and `userPWD` attributes.</span></span>

## <a name="publish-your-app"></a><span data-ttu-id="7888d-176">Публикация приложения</span><span class="sxs-lookup"><span data-stu-id="7888d-176">Publish your app</span></span>
<span data-ttu-id="7888d-177">После тестирования приложения локально, его можно опубликовать tooyour веб-приложения с помощью протокола FTP.</span><span class="sxs-lookup"><span data-stu-id="7888d-177">After you have tested your app locally, you can publish it tooyour web app using FTP.</span></span> <span data-ttu-id="7888d-178">Тем не менее необходимо сначала tooupdate hello сведений о соединении в приложении hello.</span><span class="sxs-lookup"><span data-stu-id="7888d-178">However, you first need tooupdate hello database connection information in hello application.</span></span> <span data-ttu-id="7888d-179">С помощью hello сведений о соединении полученного ранее (в hello **получить MySQL и FTP-сведения о соединении** раздел), обновления hello следующую информацию в **оба** hello `createdatabase.php` и `index.php` файлы с hello соответствующие значения:</span><span class="sxs-lookup"><span data-stu-id="7888d-179">Using hello database connection information you obtained earlier (in hello **Get MySQL and FTP connection information** section), update hello following information in **both** hello `createdatabase.php` and `index.php` files with hello appropriate values:</span></span>

    // DB connection info
    $host = "value of Data Source";
    $user = "value of User Id";
    $pwd = "value of Password";
    $db = "value of Database";

<span data-ttu-id="7888d-180">Теперь вы готовы toopublish приложения с помощью протокола FTP.</span><span class="sxs-lookup"><span data-stu-id="7888d-180">Now you are ready toopublish your app using FTP.</span></span>

1. <span data-ttu-id="7888d-181">Откройте выбранный клиент FTP.</span><span class="sxs-lookup"><span data-stu-id="7888d-181">Open your FTP client of choice.</span></span>
2. <span data-ttu-id="7888d-182">Введите hello *имя узла в составе* из hello `publishUrl` атрибутов, указанных выше в ваш FTP-клиента.</span><span class="sxs-lookup"><span data-stu-id="7888d-182">Enter hello *host name portion* from hello `publishUrl` attribute you noted above into your FTP client.</span></span>
3. <span data-ttu-id="7888d-183">Введите hello `userName` и `userPWD` атрибутов, указанных выше без изменений в вашей FTP-клиента.</span><span class="sxs-lookup"><span data-stu-id="7888d-183">Enter hello `userName` and `userPWD` attributes you noted above unchanged into your FTP client.</span></span>
4. <span data-ttu-id="7888d-184">Установите подключение.</span><span class="sxs-lookup"><span data-stu-id="7888d-184">Establish a connection.</span></span>

<span data-ttu-id="7888d-185">После подключения вы будет может tooupload и при необходимости загрузить файлы.</span><span class="sxs-lookup"><span data-stu-id="7888d-185">After you have connected you will be able tooupload and download files as needed.</span></span> <span data-ttu-id="7888d-186">Убедитесь, что вы отправляете файлы toohello корневой каталог, который является `/site/wwwroot`.</span><span class="sxs-lookup"><span data-stu-id="7888d-186">Be sure that you are uploading files toohello root directory, which is `/site/wwwroot`.</span></span>

<span data-ttu-id="7888d-187">После отправки оба `index.php` и `createtable.php`, Обзор слишком**http://[site name].azurewebsites.net/createtable.php** toocreate hello MySQL для приложения hello, а затем найдите слишком**http://[site имя ].azurewebsites.net/index.php** toobegin, с помощью приложения hello.</span><span class="sxs-lookup"><span data-stu-id="7888d-187">After uploading both `index.php` and `createtable.php`, browse too**http://[site name].azurewebsites.net/createtable.php** toocreate hello MySQL table for hello application, then browse too**http://[site name].azurewebsites.net/index.php** toobegin using hello application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7888d-188">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7888d-188">Next steps</span></span>
<span data-ttu-id="7888d-189">Дополнительные сведения см. в разделе hello [Центр разработчика PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="7888d-189">For more information, see hello [PHP Developer Center](/develop/php/).</span></span>

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

