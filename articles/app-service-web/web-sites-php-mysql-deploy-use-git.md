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
# <a name="create-a-php-mysql-web-app-in-azure-app-service-and-deploy-using-git"></a>Создание веб-приложения PHP-MySQL в службе приложений Azure и развертывание с помощью Git
В этом учебнике показано, как toocreate PHP-MySQL веб-приложения и как toodeploy он слишком[службы приложений](http://go.microsoft.com/fwlink/?LinkId=529714) с помощью Git. Вы воспользуетесь [PHP][install-php], средство командной строки MySQL hello (частью [MySQL][install-mysql]), и [Git] [ install-git] установлены на компьютере. Hello инструкциям этого учебника можно выполнять в любой операционной системе, включая Windows, Mac и Linux. По завершении работы с этим учебником у вас будет работающее в Azure веб-приложение PHP-MySQL.

Вы узнаете:

* Как toocreate веб-приложения и MySQL базы данных с помощью hello [портала Azure][management-portal]. Из-за включения PHP в [веб-приложений служб приложений](http://go.microsoft.com/fwlink/?LinkId=529714) по умолчанию никаких дополнительных действий не является обязательным toorun кода PHP.
* Как toopublish и повторно опубликовать tooAzure вашего приложения, с помощью Git.
* Выполнение задач по tooenable hello Composer расширения tooautomate редактор в каждом `git push`.

Руководствуясь этим учебником, вы создадите на языке PHP простое веб-приложение для регистрации. приложение Hello будет размещено в веб-приложениях. Снимок экрана приложения hello завершения используется следующим образом:

![Веб-сайт Azure на PHP][running-app]

## <a name="set-up-hello-development-environment"></a>Настройка среды разработки hello
В этом учебнике предполагается, у вас есть [PHP][install-php], средство командной строки MySQL hello (частью [MySQL][install-mysql]), и [Git] [ install-git] установлены на компьютере.

<a id="create-web-site-and-set-up-git"></a>

## <a name="create-a-web-app-and-set-up-git-publishing"></a>Создание веб-приложения и настройка публикации через Git
Выполните эти шаги toocreate веб-приложения и базы данных MySQL.

1. Имя входа toohello [портала Azure][management-portal].
2. Нажмите кнопку hello **New** значок.
3. Нажмите кнопку **разделе все** Далее слишком**Marketplace**. 
4. Щелкните **Интернет + мобильные устройства**, а затем **Веб-приложение + MySQL**. Затем щелкните **Создать**.
5. Укажите действительное имя группы ресурсов.
   
    ![Задание имени группы ресурсов][resource-group]
6. Введите значения для нового веб-приложения.
   
    ![Создание веб-приложения][new-web-app]
7. Введите значения для новой базы данных, включая согласие toohello условия.
   
    ![Создание новой базы данных MySQL][new-mysql-db]
8. При создании веб-приложения hello вы увидите hello Новая колонка web app.
9. В колонке **Параметры** щелкните **Непрерывное развертывание**, а затем *Настроить необходимые параметры*.
   
    ![Настройка публикации Git][setup-publishing]
10. Выберите **локального репозитория Git** hello источника.
    
     ![Настройка репозитория Git][setup-repository]
11. tooenable публикации Git, необходимо указать имя пользователя и пароль. Запишите hello имя пользователя и пароль, который вы создаете. (Если ранее уже был настроен репозиторий Git, этот шаг будет пропущен.)
    
     ![Создание учетных данных для публикации][credentials]

## <a name="get-remote-mysql-connection-information"></a>Получение информации об удаленном подключении к MySQL
База данных MySQL tooconnect toohello, на котором выполняется в веб-приложениях, приведет к необходимости hello сведения о соединении. tooget сведения о соединении MySQL, выполните следующие действия.

1. В группе ресурсов выберите hello базы данных:
   
    ![Выбор базы данных][select-database]
2. Из базы данных hello **параметры**выберите **свойства**.
   
    ![Выбор свойств][select-properties]
3. Запишите значения hello для `Database`, `Host`, `User Id`, и `Password`.
   
    ![Запись свойств][note-properties]

## <a name="build-and-test-your-app-locally"></a>Локальное создание и тестирование приложения
Теперь, когда у вас есть созданное веб-приложение, вы можете разработать свое приложение локально и после тестирования развернуть его.

Регистрация приложения Hello представляет простое приложение PHP, позволяющий tooregister для события, предоставляя вашей имя и адрес электронной почты. Сведения о ранее зарегистрировавшихся пользователях отображаются в таблице. Сведения о регистрации хранятся в базе данных MySQL. приложение Hello состоит из одного файла (копирование и вставка кода ниже):

* **index.php**— вывод формы для регистрации и таблицы, содержащей сведения о зарегистрировавшихся пользователях.

toobuild и выполнения hello приложения локально, выполните следующие шаги hello. Обратите внимание, что эти шаги предполагают hello PHP и средство командной строки MySQL (часть MySQL) на локальном компьютере, а включены hello [расширение PDO для MySQL][pdo-mysql].

1. Подключение toohello с удаленным сервером MySQL, используя значение hello `Data Source`, `User Id`, `Password`, и `Database` , полученный ранее:
   
        mysql -h{Data Source] -u[User Id] -p[Password] -D[Database]
2. Появится Hello MySQL командной строки:
   
        mysql>
3. Вставить в hello ниже `CREATE TABLE` команда toocreate hello `registration_tbl` таблицы в базе данных:
   
        CREATE TABLE registration_tbl(id INT NOT NULL AUTO_INCREMENT, PRIMARY KEY(id), name VARCHAR(30), email VARCHAR(30), date DATE);
4. Создайте в корневой папке локального приложения hello **index.php** файла.
5. Откройте hello **index.php** в текстовом редакторе или в интегрированной среде разработки и добавьте hello после кода, и завершения hello необходимые изменения, отмеченные `//TODO:` комментарии.

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

1. В tooyour терминалов откройте приложение папку и введите hello следующую команду:
   
       php -S localhost:8000

Теперь можно выполнять поиск слишком**http://localhost: 8000 /** tootest приложения hello.

## <a name="publish-your-app"></a>Публикация приложения
После тестирования приложения локально, можно опубликовать его tooWeb приложений с помощью Git. Будет инициализировать ваш локальный репозиторий Git и публикации приложения hello.

> [!NOTE]
> Они являются hello же шаги, показанные на портале Azure в конце hello hello Создание веб-приложения и набора hello копию публикации Git раздела выше.
> 
> 

1. (Необязательно)  Если забыт или перемещено URL-адрес Git удаленного repostitory перейдите toohello веб-приложение свойств на портале Azure hello.
2. Откройте GitBash (или терминал, если Git находится в вашей `PATH`), измените каталоги toohello корневой каталог приложения и запустите hello, следующие команды:
   
        git init
        git add .
        git commit -m "initial commit"
        git remote add azure [URL for remote repository]
        git push azure master
   
    Появится для hello паролей, созданную ранее.
   
    ![Начальное tooAzure принудительной через Git][git-initial-push]
3. Обзор слишком**http://[site name].azurewebsites.net/index.php** toobegin, с помощью приложения hello (эти сведения будут храниться на панели мониторинга учетной записи):
   
    ![Веб-сайт Azure на PHP][running-app]

После публикации приложения можно начать создание tooit изменения и использовать Git toopublish их.

## <a name="publish-changes-tooyour-app"></a>Публикация приложения tooyour изменения
приложение tooyour toopublish изменения, выполните следующие действия:

1. Сделать приложение tooyour изменения локально.
2. Откройте GitBash (или терминал, ИТ Git находится в вашей `PATH`), измените каталоги toohello корневой каталог приложения и запустите hello, следующие команды:
   
        git add .
        git commit -m "comment describing changes"
        git push azure master
   
    Появится для hello паролей, созданную ранее.
   
    ![Помещает tooAzure изменения сайта через Git][git-change-push]
3. Обзор слишком**http://[site name].azurewebsites.net/index.php** toosee ваше приложение и все изменения, сделанные:
   
    ![Веб-сайт Azure на PHP][running-app]

> [!NOTE]
> Tooget работы в службе приложений Azure перед регистрацией учетную запись Azure, перейдите слишком[повторите служб приложений](https://azure.microsoft.com/try/app-service/), в котором можно немедленно создать кратковременных начальный веб-приложения в службе приложений. Никаких кредитных карт и обязательств.
> 
> 

<a name="composer"></a>

## <a name="enable-composer-automation-with-hello-composer-extension"></a>Включить редактор автоматизации с hello Composer расширения
По умолчанию hello процесс развертывания git в службе приложений не выполняет никаких действий с composer.json, если она есть в вашем проекте PHP. Можно включить во время обработки composer.json `git push` путем включения расширения Composer hello.

1. В вашей PHP веб-приложения колонки в hello [портал Azure][management-portal], нажмите кнопку **средства** > **расширения**.
   
    ![Параметры расширения Composer][composer-extension-settings]
2. Щелкните **Добавить**, а затем — **Composer**.
   
    ![Добавление расширения Composer][composer-extension-add]
3. Нажмите кнопку **ОК** tooaccept условия. Нажмите кнопку **ОК** снова tooadd hello расширения.
   
    Hello **установленные расширения** колонке теперь будет отображаться расширение Composer hello.  
    ![Просмотр расширения Composer][composer-extension-view]
4. Теперь выполните `git add`, `git commit`, и `git push` как и в предыдущем разделе hello. Вы увидите, что расширение Composer устанавливает зависимости, определенные в файле composer.json.
   
    ![Добавленное расширение Composer][composer-extension-success]

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения см. в разделе hello [Центр разработчика PHP](/develop/php/).

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
