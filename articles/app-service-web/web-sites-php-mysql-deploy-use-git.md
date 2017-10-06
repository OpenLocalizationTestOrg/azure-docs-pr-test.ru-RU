---
title: "aaaCreate PHP-MySQL веб-приложения в службе приложений Azure и развертывание с помощью Git"
description: "Учебник, в котором показано, как веб-приложение, которое сохраняет данные в MySQL toocreate PHP и использовать tooAzure развертывания Git."
services: app-service\web
documentationcenter: php
author: rmcmurray
manager: erikre
editor: 
tags: mysql
ms.assetid: 7454475f-e275-4bc7-9f09-1ef07382e5da
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 9c22946777598cc973cd9dfc8d2a258bd08cc39a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-php-mysql-web-app-in-azure-app-service-and-deploy-using-git"></a><span data-ttu-id="5ceae-103">Создание веб-приложения PHP-MySQL в службе приложений Azure и развертывание с помощью Git</span><span class="sxs-lookup"><span data-stu-id="5ceae-103">Create a PHP-MySQL web app in Azure App Service and deploy using Git</span></span>
<span data-ttu-id="5ceae-104">В этом учебнике показано, как toocreate PHP-MySQL веб-приложения и как toodeploy он слишком[службы приложений](http://go.microsoft.com/fwlink/?LinkId=529714) с помощью Git.</span><span class="sxs-lookup"><span data-stu-id="5ceae-104">This tutorial shows you how toocreate a PHP-MySQL web app and how toodeploy it too[App Service](http://go.microsoft.com/fwlink/?LinkId=529714) using Git.</span></span> <span data-ttu-id="5ceae-105">Вы воспользуетесь [PHP][install-php], средство командной строки MySQL hello (частью [MySQL][install-mysql]), и [Git] [ install-git] установлены на компьютере.</span><span class="sxs-lookup"><span data-stu-id="5ceae-105">You will use [PHP][install-php], hello MySQL Command-Line Tool (part of [MySQL][install-mysql]), and [Git][install-git] installed on your computer.</span></span> <span data-ttu-id="5ceae-106">Hello инструкциям этого учебника можно выполнять в любой операционной системе, включая Windows, Mac и Linux.</span><span class="sxs-lookup"><span data-stu-id="5ceae-106">hello instructions in this tutorial can be followed on any operating system, including Windows, Mac, and  Linux.</span></span> <span data-ttu-id="5ceae-107">По завершении работы с этим учебником у вас будет работающее в Azure веб-приложение PHP-MySQL.</span><span class="sxs-lookup"><span data-stu-id="5ceae-107">Upon completing this guide, you will have a PHP/MySQL web app running in Azure.</span></span>

<span data-ttu-id="5ceae-108">Вы узнаете:</span><span class="sxs-lookup"><span data-stu-id="5ceae-108">You will learn:</span></span>

* <span data-ttu-id="5ceae-109">Как toocreate веб-приложения и MySQL базы данных с помощью hello [портала Azure][management-portal].</span><span class="sxs-lookup"><span data-stu-id="5ceae-109">How toocreate a web app and a MySQL database using hello [Azure Portal][management-portal].</span></span> <span data-ttu-id="5ceae-110">Из-за включения PHP в [веб-приложений служб приложений](http://go.microsoft.com/fwlink/?LinkId=529714) по умолчанию никаких дополнительных действий не является обязательным toorun кода PHP.</span><span class="sxs-lookup"><span data-stu-id="5ceae-110">Because PHP is enabled in [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) by default, nothing special is required toorun your PHP code.</span></span>
* <span data-ttu-id="5ceae-111">Как toopublish и повторно опубликовать tooAzure вашего приложения, с помощью Git.</span><span class="sxs-lookup"><span data-stu-id="5ceae-111">How toopublish and re-publish your application tooAzure using Git.</span></span>
* <span data-ttu-id="5ceae-112">Выполнение задач по tooenable hello Composer расширения tooautomate редактор в каждом `git push`.</span><span class="sxs-lookup"><span data-stu-id="5ceae-112">How tooenable hello Composer extension tooautomate Composer tasks at every `git push`.</span></span>

<span data-ttu-id="5ceae-113">Руководствуясь этим учебником, вы создадите на языке PHP простое веб-приложение для регистрации.</span><span class="sxs-lookup"><span data-stu-id="5ceae-113">By following this tutorial, you will build a simple registration web app in PHP.</span></span> <span data-ttu-id="5ceae-114">приложение Hello будет размещено в веб-приложениях.</span><span class="sxs-lookup"><span data-stu-id="5ceae-114">hello application will be hosted in Web Apps.</span></span> <span data-ttu-id="5ceae-115">Снимок экрана приложения hello завершения используется следующим образом:</span><span class="sxs-lookup"><span data-stu-id="5ceae-115">A screenshot of hello completed application is below:</span></span>

![Веб-сайт Azure на PHP][running-app]

## <a name="set-up-hello-development-environment"></a><span data-ttu-id="5ceae-117">Настройка среды разработки hello</span><span class="sxs-lookup"><span data-stu-id="5ceae-117">Set up hello development environment</span></span>
<span data-ttu-id="5ceae-118">В этом учебнике предполагается, у вас есть [PHP][install-php], средство командной строки MySQL hello (частью [MySQL][install-mysql]), и [Git] [ install-git] установлены на компьютере.</span><span class="sxs-lookup"><span data-stu-id="5ceae-118">This tutorial assumes you have [PHP][install-php], hello MySQL Command-Line Tool (part of [MySQL][install-mysql]), and [Git][install-git] installed on your computer.</span></span>

<a id="create-web-site-and-set-up-git"></a>

## <a name="create-a-web-app-and-set-up-git-publishing"></a><span data-ttu-id="5ceae-119">Создание веб-приложения и настройка публикации через Git</span><span class="sxs-lookup"><span data-stu-id="5ceae-119">Create a web app and set up Git publishing</span></span>
<span data-ttu-id="5ceae-120">Выполните эти шаги toocreate веб-приложения и базы данных MySQL.</span><span class="sxs-lookup"><span data-stu-id="5ceae-120">Follow these steps toocreate a web app and a MySQL database:</span></span>

1. <span data-ttu-id="5ceae-121">Имя входа toohello [портала Azure][management-portal].</span><span class="sxs-lookup"><span data-stu-id="5ceae-121">Login toohello [Azure Portal][management-portal].</span></span>
2. <span data-ttu-id="5ceae-122">Нажмите кнопку hello **New** значок.</span><span class="sxs-lookup"><span data-stu-id="5ceae-122">Click hello **New** icon.</span></span>
3. <span data-ttu-id="5ceae-123">Нажмите кнопку **разделе все** Далее слишком**Marketplace**.</span><span class="sxs-lookup"><span data-stu-id="5ceae-123">Click **See All** next too**Marketplace**.</span></span> 
4. <span data-ttu-id="5ceae-124">Щелкните **Интернет + мобильные устройства**, а затем **Веб-приложение + MySQL**.</span><span class="sxs-lookup"><span data-stu-id="5ceae-124">Click **Web + Mobile**, then **Web app + MySQL**.</span></span> <span data-ttu-id="5ceae-125">Затем щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="5ceae-125">Then, click **Create**.</span></span>
5. <span data-ttu-id="5ceae-126">Укажите действительное имя группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="5ceae-126">Enter a valid name for your resource group.</span></span>
   
    ![Задание имени группы ресурсов][resource-group]
6. <span data-ttu-id="5ceae-128">Введите значения для нового веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="5ceae-128">Enter values for your new web app.</span></span>
   
    ![Создание веб-приложения][new-web-app]
7. <span data-ttu-id="5ceae-130">Введите значения для новой базы данных, включая согласие toohello условия.</span><span class="sxs-lookup"><span data-stu-id="5ceae-130">Enter values for your new database, including agreeing toohello legal terms.</span></span>
   
    ![Создание новой базы данных MySQL][new-mysql-db]
8. <span data-ttu-id="5ceae-132">При создании веб-приложения hello вы увидите hello Новая колонка web app.</span><span class="sxs-lookup"><span data-stu-id="5ceae-132">When hello web app has been created, you will see hello new web app blade.</span></span>
9. <span data-ttu-id="5ceae-133">В колонке **Параметры** щелкните **Непрерывное развертывание**, а затем *Настроить необходимые параметры*.</span><span class="sxs-lookup"><span data-stu-id="5ceae-133">In **Settings** click on **Continuous Deployment**, then click on *Configure required settings*.</span></span>
   
    ![Настройка публикации Git][setup-publishing]
10. <span data-ttu-id="5ceae-135">Выберите **локального репозитория Git** hello источника.</span><span class="sxs-lookup"><span data-stu-id="5ceae-135">Select **Local Git Repository** for hello source.</span></span>
    
     ![Настройка репозитория Git][setup-repository]
11. <span data-ttu-id="5ceae-137">tooenable публикации Git, необходимо указать имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="5ceae-137">tooenable Git publishing, you must provide a user name and password.</span></span> <span data-ttu-id="5ceae-138">Запишите hello имя пользователя и пароль, который вы создаете.</span><span class="sxs-lookup"><span data-stu-id="5ceae-138">Make a note of hello user name and password you create.</span></span> <span data-ttu-id="5ceae-139">(Если ранее уже был настроен репозиторий Git, этот шаг будет пропущен.)</span><span class="sxs-lookup"><span data-stu-id="5ceae-139">(If you have set up a Git repository before, this step will be skipped.)</span></span>
    
     ![Создание учетных данных для публикации][credentials]

## <a name="get-remote-mysql-connection-information"></a><span data-ttu-id="5ceae-141">Получение информации об удаленном подключении к MySQL</span><span class="sxs-lookup"><span data-stu-id="5ceae-141">Get remote MySQL connection information</span></span>
<span data-ttu-id="5ceae-142">База данных MySQL tooconnect toohello, на котором выполняется в веб-приложениях, приведет к необходимости hello сведения о соединении.</span><span class="sxs-lookup"><span data-stu-id="5ceae-142">tooconnect toohello MySQL database that is running in Web Apps, your will need hello connection information.</span></span> <span data-ttu-id="5ceae-143">tooget сведения о соединении MySQL, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="5ceae-143">tooget MySQL connection information, follow these steps:</span></span>

1. <span data-ttu-id="5ceae-144">В группе ресурсов выберите hello базы данных:</span><span class="sxs-lookup"><span data-stu-id="5ceae-144">From your resource group, click hello database:</span></span>
   
    ![Выбор базы данных][select-database]
2. <span data-ttu-id="5ceae-146">Из базы данных hello **параметры**выберите **свойства**.</span><span class="sxs-lookup"><span data-stu-id="5ceae-146">From hello database **Settings**, select **Properties**.</span></span>
   
    ![Выбор свойств][select-properties]
3. <span data-ttu-id="5ceae-148">Запишите значения hello для `Database`, `Host`, `User Id`, и `Password`.</span><span class="sxs-lookup"><span data-stu-id="5ceae-148">Make note of hello values for `Database`, `Host`, `User Id`, and `Password`.</span></span>
   
    ![Запись свойств][note-properties]

## <a name="build-and-test-your-app-locally"></a><span data-ttu-id="5ceae-150">Локальное создание и тестирование приложения</span><span class="sxs-lookup"><span data-stu-id="5ceae-150">Build and test your app locally</span></span>
<span data-ttu-id="5ceae-151">Теперь, когда у вас есть созданное веб-приложение, вы можете разработать свое приложение локально и после тестирования развернуть его.</span><span class="sxs-lookup"><span data-stu-id="5ceae-151">Now that you have created a web app, you can develop your application locally, then deploy it after testing.</span></span>

<span data-ttu-id="5ceae-152">Регистрация приложения Hello представляет простое приложение PHP, позволяющий tooregister для события, предоставляя вашей имя и адрес электронной почты.</span><span class="sxs-lookup"><span data-stu-id="5ceae-152">hello Registration application is a simple PHP application that allows you tooregister for an event by providing your name and email address.</span></span> <span data-ttu-id="5ceae-153">Сведения о ранее зарегистрировавшихся пользователях отображаются в таблице.</span><span class="sxs-lookup"><span data-stu-id="5ceae-153">Information about previous registrants is displayed in a table.</span></span> <span data-ttu-id="5ceae-154">Сведения о регистрации хранятся в базе данных MySQL.</span><span class="sxs-lookup"><span data-stu-id="5ceae-154">Registration information is stored in a MySQL database.</span></span> <span data-ttu-id="5ceae-155">приложение Hello состоит из одного файла (копирование и вставка кода ниже):</span><span class="sxs-lookup"><span data-stu-id="5ceae-155">hello application consists of one file (copy/paste code available below):</span></span>

* <span data-ttu-id="5ceae-156">**index.php**— вывод формы для регистрации и таблицы, содержащей сведения о зарегистрировавшихся пользователях.</span><span class="sxs-lookup"><span data-stu-id="5ceae-156">**index.php**: Displays a form for registration and a table containing registrant information.</span></span>

<span data-ttu-id="5ceae-157">toobuild и выполнения hello приложения локально, выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="5ceae-157">toobuild and run hello application locally, follow hello steps below.</span></span> <span data-ttu-id="5ceae-158">Обратите внимание, что эти шаги предполагают hello PHP и средство командной строки MySQL (часть MySQL) на локальном компьютере, а включены hello [расширение PDO для MySQL][pdo-mysql].</span><span class="sxs-lookup"><span data-stu-id="5ceae-158">Note that these steps assume you have hello PHP and MySQL Command-Line Tool (part of MySQL) set up on your local machine, and that you have enabled hello [PDO extension for MySQL][pdo-mysql].</span></span>

1. <span data-ttu-id="5ceae-159">Подключение toohello с удаленным сервером MySQL, используя значение hello `Data Source`, `User Id`, `Password`, и `Database` , полученный ранее:</span><span class="sxs-lookup"><span data-stu-id="5ceae-159">Connect toohello remote MySQL server, using hello value for `Data Source`, `User Id`, `Password`, and `Database` that you retrieved earlier:</span></span>
   
        mysql -h{Data Source] -u[User Id] -p[Password] -D[Database]
2. <span data-ttu-id="5ceae-160">Появится Hello MySQL командной строки:</span><span class="sxs-lookup"><span data-stu-id="5ceae-160">hello MySQL command prompt will appear:</span></span>
   
        mysql>
3. <span data-ttu-id="5ceae-161">Вставить в hello ниже `CREATE TABLE` команда toocreate hello `registration_tbl` таблицы в базе данных:</span><span class="sxs-lookup"><span data-stu-id="5ceae-161">Paste in hello following `CREATE TABLE` command toocreate hello `registration_tbl` table in your database:</span></span>
   
        CREATE TABLE registration_tbl(id INT NOT NULL AUTO_INCREMENT, PRIMARY KEY(id), name VARCHAR(30), email VARCHAR(30), date DATE);
4. <span data-ttu-id="5ceae-162">Создайте в корневой папке локального приложения hello **index.php** файла.</span><span class="sxs-lookup"><span data-stu-id="5ceae-162">In hello root of your local application folder create **index.php** file.</span></span>
5. <span data-ttu-id="5ceae-163">Откройте hello **index.php** в текстовом редакторе или в интегрированной среде разработки и добавьте hello после кода, и завершения hello необходимые изменения, отмеченные `//TODO:` комментарии.</span><span class="sxs-lookup"><span data-stu-id="5ceae-163">Open hello **index.php** file in a text editor or IDE and add hello following code, and complete hello necessary changes marked with `//TODO:` comments.</span></span>

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
            // DB connection info
            //TODO: Update hello values for $host, $user, $pwd, and $db
            //using hello values you retrieved earlier from hello Azure Portal.
            $host = "value of Data Source";
            $user = "value of User Id";
            $pwd = "value of Password";
            $db = "value of Database";
            // Connect toodatabase.
            try {
                $conn = new PDO( "mysql:host=$host;dbname=$db", $user, $pwd);
                $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );
            }
            catch(Exception $e){
                die(var_dump($e));
            }
            // Insert registration info
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
            // Retrieve data
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
        ?>
        </body>
        </html>

1. <span data-ttu-id="5ceae-164">В tooyour терминалов откройте приложение папку и введите hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="5ceae-164">In a terminal go tooyour application folder and type hello following command:</span></span>
   
       php -S localhost:8000

<span data-ttu-id="5ceae-165">Теперь можно выполнять поиск слишком**http://localhost: 8000 /** tootest приложения hello.</span><span class="sxs-lookup"><span data-stu-id="5ceae-165">You can now browse too**http://localhost:8000/** tootest hello application.</span></span>

## <a name="publish-your-app"></a><span data-ttu-id="5ceae-166">Публикация приложения</span><span class="sxs-lookup"><span data-stu-id="5ceae-166">Publish your app</span></span>
<span data-ttu-id="5ceae-167">После тестирования приложения локально, можно опубликовать его tooWeb приложений с помощью Git.</span><span class="sxs-lookup"><span data-stu-id="5ceae-167">After you have tested your app locally, you can publish it tooWeb Apps using Git.</span></span> <span data-ttu-id="5ceae-168">Будет инициализировать ваш локальный репозиторий Git и публикации приложения hello.</span><span class="sxs-lookup"><span data-stu-id="5ceae-168">You will initialize your local Git repository and publish hello application.</span></span>

> [!NOTE]
> <span data-ttu-id="5ceae-169">Они являются hello же шаги, показанные на портале Azure в конце hello hello Создание веб-приложения и набора hello копию публикации Git раздела выше.</span><span class="sxs-lookup"><span data-stu-id="5ceae-169">These are hello same steps shown in hello Azure Portal at hello end of hello Create a web app and Set up Git Publishing section above.</span></span>
> 
> 

1. <span data-ttu-id="5ceae-170">(Необязательно)  Если забыт или перемещено URL-адрес Git удаленного repostitory перейдите toohello веб-приложение свойств на портале Azure hello.</span><span class="sxs-lookup"><span data-stu-id="5ceae-170">(Optional)  If you've forgotten or misplaced your Git remote repostitory URL, navigate toohello web app properties on hello Azure Portal.</span></span>
2. <span data-ttu-id="5ceae-171">Откройте GitBash (или терминал, если Git находится в вашей `PATH`), измените каталоги toohello корневой каталог приложения и запустите hello, следующие команды:</span><span class="sxs-lookup"><span data-stu-id="5ceae-171">Open GitBash (or a terminal, if Git is in your `PATH`), change directories toohello root directory of your application, and run hello following commands:</span></span>
   
        git init
        git add .
        git commit -m "initial commit"
        git remote add azure [URL for remote repository]
        git push azure master
   
    <span data-ttu-id="5ceae-172">Появится для hello паролей, созданную ранее.</span><span class="sxs-lookup"><span data-stu-id="5ceae-172">You will be prompted for hello password you created earlier.</span></span>
   
    ![Начальное tooAzure принудительной через Git][git-initial-push]
3. <span data-ttu-id="5ceae-174">Обзор слишком**http://[site name].azurewebsites.net/index.php** toobegin, с помощью приложения hello (эти сведения будут храниться на панели мониторинга учетной записи):</span><span class="sxs-lookup"><span data-stu-id="5ceae-174">Browse too**http://[site name].azurewebsites.net/index.php** toobegin using hello application (this information will be stored on your account dashboard):</span></span>
   
    ![Веб-сайт Azure на PHP][running-app]

<span data-ttu-id="5ceae-176">После публикации приложения можно начать создание tooit изменения и использовать Git toopublish их.</span><span class="sxs-lookup"><span data-stu-id="5ceae-176">After you have published your app, you can begin making changes tooit and use Git toopublish them.</span></span>

## <a name="publish-changes-tooyour-app"></a><span data-ttu-id="5ceae-177">Публикация приложения tooyour изменения</span><span class="sxs-lookup"><span data-stu-id="5ceae-177">Publish changes tooyour app</span></span>
<span data-ttu-id="5ceae-178">приложение tooyour toopublish изменения, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="5ceae-178">toopublish changes tooyour app, follow these steps:</span></span>

1. <span data-ttu-id="5ceae-179">Сделать приложение tooyour изменения локально.</span><span class="sxs-lookup"><span data-stu-id="5ceae-179">Make changes tooyour app locally.</span></span>
2. <span data-ttu-id="5ceae-180">Откройте GitBash (или терминал, ИТ Git находится в вашей `PATH`), измените каталоги toohello корневой каталог приложения и запустите hello, следующие команды:</span><span class="sxs-lookup"><span data-stu-id="5ceae-180">Open GitBash (or a terminal, it Git is in your `PATH`), change directories toohello root directory of your app, and run hello following commands:</span></span>
   
        git add .
        git commit -m "comment describing changes"
        git push azure master
   
    <span data-ttu-id="5ceae-181">Появится для hello паролей, созданную ранее.</span><span class="sxs-lookup"><span data-stu-id="5ceae-181">You will be prompted for hello password you created earlier.</span></span>
   
    ![Помещает tooAzure изменения сайта через Git][git-change-push]
3. <span data-ttu-id="5ceae-183">Обзор слишком**http://[site name].azurewebsites.net/index.php** toosee ваше приложение и все изменения, сделанные:</span><span class="sxs-lookup"><span data-stu-id="5ceae-183">Browse too**http://[site name].azurewebsites.net/index.php** toosee your app and any changes you may have made:</span></span>
   
    ![Веб-сайт Azure на PHP][running-app]

> [!NOTE]
> <span data-ttu-id="5ceae-185">Tooget работы в службе приложений Azure перед регистрацией учетную запись Azure, перейдите слишком[повторите служб приложений](https://azure.microsoft.com/try/app-service/), в котором можно немедленно создать кратковременных начальный веб-приложения в службе приложений.</span><span class="sxs-lookup"><span data-stu-id="5ceae-185">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="5ceae-186">Никаких кредитных карт и обязательств.</span><span class="sxs-lookup"><span data-stu-id="5ceae-186">No credit cards required; no commitments.</span></span>
> 
> 

<a name="composer"></a>

## <a name="enable-composer-automation-with-hello-composer-extension"></a><span data-ttu-id="5ceae-187">Включить редактор автоматизации с hello Composer расширения</span><span class="sxs-lookup"><span data-stu-id="5ceae-187">Enable Composer automation with hello Composer extension</span></span>
<span data-ttu-id="5ceae-188">По умолчанию hello процесс развертывания git в службе приложений не выполняет никаких действий с composer.json, если она есть в вашем проекте PHP.</span><span class="sxs-lookup"><span data-stu-id="5ceae-188">By default, hello git deployment process in App Service doesn't do anything with composer.json, if you have one in your PHP project.</span></span> <span data-ttu-id="5ceae-189">Можно включить во время обработки composer.json `git push` путем включения расширения Composer hello.</span><span class="sxs-lookup"><span data-stu-id="5ceae-189">You can enable composer.json processing during `git push` by enabling hello Composer extension.</span></span>

1. <span data-ttu-id="5ceae-190">В вашей PHP веб-приложения колонки в hello [портал Azure][management-portal], нажмите кнопку **средства** > **расширения**.</span><span class="sxs-lookup"><span data-stu-id="5ceae-190">In your PHP web app's blade in hello [Azure portal][management-portal], click **Tools** > **Extensions**.</span></span>
   
    ![Параметры расширения Composer][composer-extension-settings]
2. <span data-ttu-id="5ceae-192">Щелкните **Добавить**, а затем — **Composer**.</span><span class="sxs-lookup"><span data-stu-id="5ceae-192">Click **Add**, then click **Composer**.</span></span>
   
    ![Добавление расширения Composer][composer-extension-add]
3. <span data-ttu-id="5ceae-194">Нажмите кнопку **ОК** tooaccept условия.</span><span class="sxs-lookup"><span data-stu-id="5ceae-194">Click **OK** tooaccept legal terms.</span></span> <span data-ttu-id="5ceae-195">Нажмите кнопку **ОК** снова tooadd hello расширения.</span><span class="sxs-lookup"><span data-stu-id="5ceae-195">Click **OK** again tooadd hello extension.</span></span>
   
    <span data-ttu-id="5ceae-196">Hello **установленные расширения** колонке теперь будет отображаться расширение Composer hello.</span><span class="sxs-lookup"><span data-stu-id="5ceae-196">hello **Installed extensions** blade will now show hello Composer extension.</span></span>  
    <span data-ttu-id="5ceae-197">![Просмотр расширения Composer][composer-extension-view]</span><span class="sxs-lookup"><span data-stu-id="5ceae-197">![Composer Extension View][composer-extension-view]</span></span>
4. <span data-ttu-id="5ceae-198">Теперь выполните `git add`, `git commit`, и `git push` как и в предыдущем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="5ceae-198">Now, perform `git add`, `git commit`, and `git push` like in hello previous section.</span></span> <span data-ttu-id="5ceae-199">Вы увидите, что расширение Composer устанавливает зависимости, определенные в файле composer.json.</span><span class="sxs-lookup"><span data-stu-id="5ceae-199">You'll now see that Composer is installing dependencies defined in composer.json.</span></span>
   
    ![Добавленное расширение Composer][composer-extension-success]

## <a name="next-steps"></a><span data-ttu-id="5ceae-201">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5ceae-201">Next steps</span></span>
<span data-ttu-id="5ceae-202">Дополнительные сведения см. в разделе hello [Центр разработчика PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="5ceae-202">For more information, see hello [PHP Developer Center](/develop/php/).</span></span>

<!-- URL List -->

[install-php]: http://www.php.net/manual/en/install.php
[install-SQLExpress]: http://www.microsoft.com/download/details.aspx?id=29062
[install-Drivers]: http://www.microsoft.com/download/details.aspx?id=20098
[install-git]: http://git-scm.com/
[install-mysql]: http://dev.mysql.com/downloads/mysql/
[pdo-mysql]: http://www.php.net/manual/en/ref.pdo-mysql.php
[management-portal]: https://portal.azure.com
[sql-database-editions]: http://msdn.microsoft.com/library/windowsazure/ee621788.aspx

<!-- IMG List -->

[running-app]: ./media/web-sites-php-mysql-deploy-use-git/running_app_2.png
[new-website]: ./media/web-sites-php-mysql-deploy-use-git/new_website2.png
[custom-create]: ./media/web-sites-php-mysql-deploy-use-git/create_web_mysql.png
[new-mysql-db]: ./media/web-sites-php-mysql-deploy-use-git/create_db.png
[go-to-webapp]: ./media/web-sites-php-mysql-deploy-use-git/select_webapp.png
[setup-git-publishing]: ./media/web-sites-php-mysql-deploy-use-git/setup_git_publishing.png
[credentials]: ./media/web-sites-php-mysql-deploy-use-git/save_credentials.png
[resource-group]: ./media/web-sites-php-mysql-deploy-use-git/set_group.png
[new-web-app]: ./media/web-sites-php-mysql-deploy-use-git/create_wa.png
[setup-publishing]: ./media/web-sites-php-mysql-deploy-use-git/setup_deploy.png
[setup-repository]: ./media/web-sites-php-mysql-deploy-use-git/select_local_git.png
[select-database]: ./media/web-sites-php-mysql-deploy-use-git/select_database.png
[select-properties]: ./media/web-sites-php-mysql-deploy-use-git/select_properties.png
[note-properties]: ./media/web-sites-php-mysql-deploy-use-git/note-properties.png

[git-instructions]: ./media/web-sites-php-mysql-deploy-use-git/git-instructions.png
[git-change-push]: ./media/web-sites-php-mysql-deploy-use-git/php-git-change-push.png
[git-initial-push]: ./media/web-sites-php-mysql-deploy-use-git/php-git-initial-push.png

[composer-extension-settings]: ./media/web-sites-php-mysql-deploy-use-git/composer-extension-settings.png
[composer-extension-add]: ./media/web-sites-php-mysql-deploy-use-git/composer-extension-add.png
[composer-extension-view]: ./media/web-sites-php-mysql-deploy-use-git/composer-extension-view.png
[composer-extension-success]: ./media/web-sites-php-mysql-deploy-use-git/composer-extension-success.png
