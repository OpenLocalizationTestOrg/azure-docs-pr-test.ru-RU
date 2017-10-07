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
# <a name="create-a-php-sql-web-app-and-deploy-tooazure-app-service-using-git"></a>Создание веб-приложения PHP SQL и развертывание tooAzure службы приложений с помощью Git
В этом учебнике показано, как приложение в веб-toocreate PHP [службе приложений Azure](http://go.microsoft.com/fwlink/?LinkId=529714) , при подключении tooAzure базы данных SQL и как toodeploy его с помощью Git. В этом учебнике предполагается, у вас есть [PHP][install-php], [SQL Server Express][install-SQLExpress], hello [драйверы Майкрософт для SQL Server для PHP ](http://www.microsoft.com/download/en/details.aspx?id=20098), и [Git] [ install-git] установлены на компьютере. После завершения работы с этим учебником у вас будет работающее в Azure веб-приложение PHP-SQL.

> [!NOTE]
> Можно установить и настроить PHP, SQL Server Express и hello драйверы Майкрософт для SQL Server для PHP с помощью hello [Microsoft Web Platform Installer](http://www.microsoft.com/web/downloads/platform.aspx).
> 
> 

Вы узнаете:

* Как toocreate Azure веб-приложения и базы данных SQL с помощью hello [портала Azure](http://go.microsoft.com/fwlink/?LinkId=529715). Так, как PHP в веб-приложений приложения служб включена по умолчанию, никаких дополнительных действий не является обязательным toorun кода PHP.
* Как toopublish и повторно опубликовать tooAzure вашего приложения, с помощью Git.

Руководствуясь этим учебником, вы создадите в PHP простое веб-приложение регистрации. в веб-сайт Azure будет размещаться приложение Hello. Снимок экрана приложения hello завершения используется следующим образом:

![Веб-сайт Azure на PHP](./media/web-sites-php-sql-database-deploy-use-git/running_app_3.png)

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> Tooget работы в службе приложений Azure перед регистрацией учетную запись Azure, перейдите слишком[повторите служб приложений](https://azure.microsoft.com/try/app-service/), в котором можно немедленно создать кратковременных начальный веб-приложения в службе приложений. Никаких кредитных карт и обязательств.
> 
> 

## <a name="create-an-azure-web-app-and-set-up-git-publishing"></a>Создание веб-приложения Azure и настройка публикации в Git
Выполните эти шаги toocreate Azure веб-приложение и база данных SQL.

1. Войдите в toohello [портала Azure](https://portal.azure.com/).
2. Откройте hello Azure Marketplace, щелкнув hello **New** можно, щелкнув значок в верхней части hello левой части панели мониторинга hello **выделить все** Далее tooMarketplace и выбрав **Интернет + мобильные устройства**.
3. В hello Marketplace, выберите **Интернет + мобильные устройства**.
4. Нажмите кнопку hello **веб-приложение + SQL** значок.
5. После прочтения hello описание веб-приложения hello + SQL приложения, выберите **создать**.
6. Нажмите кнопку с каждой стороны (**группы ресурсов**, **веб-приложения**, **базы данных**, и **подписки**) и введите или выберите значения для необходимых hello поля:
   
   * Введите URL-адрес по своему выбору.    
   * Настройте учетные данные для сервера базы данных.
   * Выберите tooyou ближайший регион hello
     
     ![настройка приложения](./media/web-sites-php-sql-database-deploy-use-git/configure-db-settings.png)
7. Когда мы определим hello веб-приложение, нажмите кнопку **создать**.
   
    При создании веб-приложения hello hello **уведомления** кнопка будет мигать зеленым **успех** и hello обоих hello web app и hello база данных SQL в группе hello tooshow откройте колонку группы ресурсов.
8. Щелкните значок веб-приложения hello в колонке hello ресурсов группы колонке tooopen hello веб-приложения.
   
    ![группа ресурсов веб-приложений](./media/web-sites-php-sql-database-deploy-use-git/resource-group-blade.png)
9. В колонке **Параметры** щелкните **Непрерывное развертывание** > **Настроить необходимые параметры**. Выберите **Локальный репозиторий Git** и щелкните **ОК**.
   
    ![где находится исходный код](./media/web-sites-php-sql-database-deploy-use-git/setup-local-git.png)
   
    Если репозиторий Git не был настроен предварительно, необходимо указать имя пользователя и пароль. toodo, нажмите кнопку **параметры** > **учетные данные развертывания** в колонке hello веб-приложения.
   
    ![](./media/web-sites-php-sql-database-deploy-use-git/deployment-credentials.png)
10. В **параметры** щелкните **свойства** toosee hello Git URL-адрес удаленного понадобятся toouse toodeploy приложения PHP позднее.

## <a name="get-sql-database-connection-information"></a>Получение сведений о подключении к базе данных SQL
экземпляр базы данных SQL toohello tooconnect, связанных tooyour веб-приложения, приведет к необходимости hello сведения о соединении, указанные при создании базы данных hello. hello tooget сведения о подключении базы данных SQL, выполните следующие действия.

1. В колонке группы ресурсов hello щелкните значок базы данных SQL hello.
2. В колонке базы данных SQL hello щелкните **параметры** > **свойства**, нажмите кнопку **Показать строки подключения базы данных**. 
   
    ![Просмотр свойств базы данных](./media/web-sites-php-sql-database-deploy-use-git/view-database-properties.png)
3. Из hello **PHP** раздел hello полученный диалогового окна, запишите значения hello для `Server`, `SQL Database`, и `User Name`. Будет использовать эти значения позже при публикации вашей tooAzure web приложения PHP службы приложений.

## <a name="build-and-test-your-application-locally"></a>Построение и тестирование приложения на локальном ресурсе
Регистрация приложения Hello представляет простое приложение PHP, позволяющий tooregister для события, предоставляя вашей имя и адрес электронной почты. Сведения о ранее зарегистрировавшихся пользователях отображаются в таблице. Сведения о регистрации хранятся в экземпляре базы данных SQL. приложение Hello состоит из двух файлов (копирование и вставка кода ниже):

* **index.php**— вывод формы для регистрации и таблицы, содержащей сведения о зарегистрировавшихся пользователях.
* **CreateTable.PHP**: создает таблицу базы данных SQL hello для приложения hello. Этот файл будет использоваться только один раз.

приложения hello toorun локально, выполните шаги hello. Обратите внимание, что эти предполагается, что у вас есть PHP и SQL Server Express установить на локальном компьютере, а также включены hello [расширение PDO для SQL Server][pdo-sqlsrv].

1. Создайте базу данных SQL Server под названием `registration`. Это можно сделать из hello `sqlcmd` командной строки с помощью следующих команд:
   
        >sqlcmd -S localhost\sqlexpress -U <local user name> -P <local password>
        1> create database registration
        2> GO    
2. В корневом каталоге приложения создайте два файла — один с именем `createtable.php`, а другой с именем `index.php`.
3. Откройте hello `createtable.php` и добавьте приведенный ниже код hello файла в текстовом редакторе или в интегрированной среде разработки. Этот код будет использоваться toocreate hello `registration_tbl` таблицы в hello `registration` базы данных.
   
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
   
    Обратите внимание, что вам потребуется tooupdate hello значения для <code>$user</code> и <code>$pwd</code> локальное имя пользователя SQL Server и пароль.
4. В конечном в корневом каталоге hello hello тип приложения hello, следующую команду:
   
        php -S localhost:8000
5. Откройте веб-браузер и перейдите в слишком**http://localhost:8000/createtable.php**. Это создаст hello `registration_tbl` таблицы в базе данных hello.
6. Откройте hello **index.php** и добавьте hello базовый код HTML и CSS для страницы приветствия файла в текстовом редакторе или в интегрированной среде разработки (hello код PHP будут добавляться на последующих этапах).
   
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
7. В тегах PHP hello добавьте код PHP для соединения toohello базы данных.
   
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
   
    Опять же, необходимо будет tooupdate hello значения для <code>$user</code> и <code>$pwd</code> с локальным именем MySQL пользователя и пароль.
8. Следующий код подключения hello базы данных добавьте код для ввода сведений о регистрации в базу данных hello.
   
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
9. Наконец следующий код hello выше, добавьте код для извлечения данных из базы данных hello.
   
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

Теперь можно выполнять поиск слишком**http://localhost:8000/index.php** tootest приложения hello.

## <a name="publish-your-application"></a>Публикация приложения
После тестирования приложения локально, его можно опубликовать tooApp службы веб-приложений с помощью Git. Тем не менее необходимо сначала tooupdate hello сведений о соединении в приложении hello. С помощью hello сведений о соединении полученного ранее (в hello **сведения о соединении получить базу данных SQL** раздела), обновление hello следующую информацию в **оба** hello `createdatabase.php` и `index.php` файлы с hello соответствующие значения:

    // DB connection info
    $host = "tcp:<value of Server>";
    $user = "<value of User Name>";
    $pwd = "<your password>";
    $db = "<value of SQL Database>";

> [!NOTE]
> В hello <code>$host</code>, значение hello Server должен указываться с <code>tcp:</code>.
> 
> 

Теперь вы готовы tooset вверх публикации через Git и публикации приложения hello.

> [!NOTE]
> Это же шаги, перечисленные в конец hello hello hello **создать веб-приложение Azure и настройте публикацию Git** выше.
> 
> 

1. Откройте GitBash (или терминал, если Git находится в вашей `PATH`), измените каталоги toohello корневой каталог приложения (hello **регистрации** каталог), и выполнения hello следующие команды:
   
        git init
        git add .
        git commit -m "initial commit"
        git remote add azure [URL for remote repository]
        git push azure master
   
    Появится для hello паролей, созданную ранее.
2. Обзор слишком**name].azurewebsites.net/createtable.php приложения http://[web** toocreate hello база данных SQL для приложения hello.
3. Обзор слишком**name].azurewebsites.net/index.php приложения http://[web** toobegin, с помощью приложения hello.

После публикации приложения можно начать создание tooit изменения и использовать Git toopublish их. 

## <a name="publish-changes-tooyour-application"></a>Публикация приложения tooyour изменения
toopublish изменяет tooapplication, выполните следующие действия:

1. Внесите изменения tooyour приложения локально.
2. Откройте GitBash (или терминал, ИТ Git находится в вашей `PATH`), измените каталоги toohello корневой каталог приложения и запустите hello, следующие команды:
   
        git add .
        git commit -m "comment describing changes"
        git push azure master
   
    Появится для hello паролей, созданную ранее.
3. Обзор слишком**name].azurewebsites.net/index.php приложения http://[web** toosee изменений.

## <a name="whats-changed"></a>Изменения
* Toohello руководство изменений из tooApp веб-сайтов службы. в разделе: [службе приложений Azure и ее влияние на существующие службы Azure](http://go.microsoft.com/fwlink/?LinkId=529714)

[install-php]: http://www.php.net/manual/en/install.php
[install-SQLExpress]: http://www.microsoft.com/download/details.aspx?id=29062
[install-Drivers]: http://www.microsoft.com/download/details.aspx?id=20098
[install-git]: http://git-scm.com/
[pdo-sqlsrv]: http://php.net/pdo_sqlsrv

