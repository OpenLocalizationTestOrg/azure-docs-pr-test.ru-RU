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
# <a name="create-a-php-mysql-web-app-in-azure-app-service-and-deploy-using-ftp"></a>Создание веб-приложения PHP-MySQL в службе приложений Azure и развертывание с помощью FTP
В этом учебнике показано, как toocreate PHP-MySQL веб-приложения и как toodeploy ее с помощью FTP. В этом учебнике предполагается, что на компьютере установлены компоненты [PHP][install-php], [MySQL][install-mysql], веб-сервер и FTP-клиент. Hello инструкциям этого учебника можно выполнять в любой операционной системе, включая Windows, Mac и Linux. По завершении работы с этим учебником у вас будет работающее в Azure веб-приложение PHP-MySQL.

Вы узнаете:

* Как toocreate веб-приложения и MySQL базы данных с помощью портала Azure hello. Так, как в веб-приложений PHP включена по умолчанию, никаких дополнительных действий не является обязательным toorun кода PHP.
* Как toopublish tooAzure приложения с помощью FTP.

Руководствуясь этим учебником, вы создадите на языке PHP простое веб-приложение для регистрации. в веб-приложение будет размещено приложение Hello. Снимок экрана приложения hello завершения используется следующим образом:

![Веб-сайт Azure на PHP][running-app]

> [!NOTE]
> Tooget работы в службе приложений Azure перед регистрацией для учетной записи, перейдите слишком[повторите служб приложений](https://azure.microsoft.com/try/app-service/), в котором можно немедленно создать кратковременных начальный веб-приложения в службе приложений. Никаких кредитных карт и обязательств. 
> 
> 

## <a name="create-a-web-app-and-set-up-ftp-publishing"></a>Создание веб-приложения и настройка публикации через FTP
Выполните эти шаги toocreate веб-приложения и базы данных MySQL.

1. Имя входа toohello [портала Azure][management-portal].
2. Нажмите кнопку hello **+ создать** значок hello сверху слева от hello портала Azure.
   
    ![Создание нового веб-сайта Azure][new-website]
3. В типе поиска hello **веб-приложение + MySQL** и выберите команду **веб-приложение + MySQL**.
   
    ![Настраиваемое создание нового веб-сайта][custom-create]
4. Щелкните **Создать**. Введите имя уникальным приложения службы, допустимое имя для группы ресурсов hello и новый план служб.
   
    ![Задание имени группы ресурсов][resource-group]
5. Введите значения для новой базы данных, включая согласие toohello условия.
   
    ![Создание новой базы данных MySQL][new-mysql-db]
6. При создании веб-приложения hello вы увидите hello Новая колонка приложения службы.
7. Щелкните **Параметры** > **Учетные данные развертывания**. 
   
    ![Сброс учетных данных развертывания][set-deployment-credentials]
8. tooenable публикации FTP, необходимо указать имя пользователя и пароль. Сохранить учетные данные hello и запишите hello имя пользователя и пароль, который вы создаете.
   
    ![Создание учетных данных для публикации][portal-ftp-username-password]

## <a name="build-and-test-your-app-locally"></a>Создание и тестирование приложения локально
Регистрация приложения Hello представляет простое приложение PHP, позволяющий tooregister для события, предоставляя вашей имя и адрес электронной почты. Сведения о ранее зарегистрировавшихся пользователях отображаются в таблице. Сведения о регистрации хранятся в базе данных MySQL. приложение Hello состоит из двух файлов:

* **index.php**— вывод формы для регистрации и таблицы, содержащей сведения о зарегистрировавшихся пользователях.
* **CreateTable.PHP**: создает таблицу hello MySQL для приложения hello. Этот файл будет использоваться только один раз.

toobuild и выполнения hello приложения локально, выполните следующие шаги hello. Обратите внимание, что эти шаги предполагают, что у вас есть PHP, MySQL и веб-сервер на локальном компьютере и что включена hello [расширение PDO для MySQL][pdo-mysql].

1. Создание базы данных MySQL с именем `registration`. Это можно сделать из hello MySQL командной строки с помощью следующей команды:
   
        mysql> create database registration;
2. В корневом каталоге веб-сервера создайте папку с именем `registration`, а в ней два файла: один с именем `createtable.php`, а другой с именем `index.php`.
3. Откройте hello `createtable.php` и добавьте приведенный ниже код hello файла в текстовом редакторе или в интегрированной среде разработки. Этот код будет использоваться toocreate hello `registration_tbl` таблицы в hello `registration` базы данных.
   
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
   > Вам потребуются значения hello tooupdate для <code>$user</code> и <code>$pwd</code> с локальным именем MySQL пользователя и пароль.
   > 
   > 
4. Откройте веб-браузер и перейдите в слишком[http://localhost/registration/createtable.php][localhost-createtable]. Это создаст hello `registration_tbl` таблицы в базе данных hello.
5. Откройте hello **index.php** и добавьте hello базовый код HTML и CSS для страницы приветствия файла в текстовом редакторе или в интегрированной среде разработки (hello код PHP будут добавляться на последующих этапах).
   
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
6. В тегах PHP hello добавьте код PHP для соединения toohello базы данных.
   
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
   > Опять же, необходимо будет tooupdate hello значения для <code>$user</code> и <code>$pwd</code> с локальным именем MySQL пользователя и пароль.
   > 
   > 
7. Следующий код подключения hello базы данных добавьте код для ввода сведений о регистрации в базу данных hello.
   
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
8. Наконец следующий код hello выше, добавьте код для извлечения данных из базы данных hello.
   
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

Теперь можно выполнять поиск слишком[http://localhost/registration/index.php] [ localhost-index] tootest приложение hello.

## <a name="get-mysql-and-ftp-connection-information"></a>Получение сведений о подключении к MySQL и FTP
База данных MySQL tooconnect toohello, на котором выполняется в веб-приложениях, приведет к необходимости hello сведения о соединении. tooget сведения о соединении MySQL, выполните следующие действия.

1. Из службы приложения hello колонки веб-приложения щелкните ссылку группы ресурсов hello:
   
    ![Выбор группы ресурсов][select-resourcegroup]
2. В группе ресурсов выберите hello базы данных:
   
    ![Выбор базы данных][select-database]
3. Сводка базы данных hello, выберите **параметры** > **свойства**.
   
    ![Выбор свойств][select-properties]
4. Запишите значения hello для `Database`, `Host`, `User Id`, и `Password`.
   
    ![Запись свойств][note-properties]
5. Выберите веб-приложения hello **загрузить профиль публикации** ссылку в hello нижнем правом углу страницы приветствия:
   
    ![Загрузить профиль публикации][download-publish-profile]
6. Откройте hello `.publishsettings` файл в редакторе XML. 
7. Найти hello `<publishProfile >` элемент с `publishMethod="FTP"` это выглядит как toothis:
   
        <publishProfile publishMethod="FTP" publishUrl="ftp://[mysite].azurewebsites.net/site/wwwroot" ftpPassiveMode="True" userName="[username]" userPWD="[password]" destinationAppUrl="http://[name].antdf0.antares-test.windows-int.net" 
            ...
        </publishProfile>

Запишите hello `publishUrl`, `userName`, и `userPWD` атрибуты.

## <a name="publish-your-app"></a>Публикация приложения
После тестирования приложения локально, его можно опубликовать tooyour веб-приложения с помощью протокола FTP. Тем не менее необходимо сначала tooupdate hello сведений о соединении в приложении hello. С помощью hello сведений о соединении полученного ранее (в hello **получить MySQL и FTP-сведения о соединении** раздел), обновления hello следующую информацию в **оба** hello `createdatabase.php` и `index.php` файлы с hello соответствующие значения:

    // DB connection info
    $host = "value of Data Source";
    $user = "value of User Id";
    $pwd = "value of Password";
    $db = "value of Database";

Теперь вы готовы toopublish приложения с помощью протокола FTP.

1. Откройте выбранный клиент FTP.
2. Введите hello *имя узла в составе* из hello `publishUrl` атрибутов, указанных выше в ваш FTP-клиента.
3. Введите hello `userName` и `userPWD` атрибутов, указанных выше без изменений в вашей FTP-клиента.
4. Установите подключение.

После подключения вы будет может tooupload и при необходимости загрузить файлы. Убедитесь, что вы отправляете файлы toohello корневой каталог, который является `/site/wwwroot`.

После отправки оба `index.php` и `createtable.php`, Обзор слишком**http://[site name].azurewebsites.net/createtable.php** toocreate hello MySQL для приложения hello, а затем найдите слишком**http://[site имя ].azurewebsites.net/index.php** toobegin, с помощью приложения hello.

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения см. в разделе hello [Центр разработчика PHP](/develop/php/).

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

