
1. tooescalate права доступа, тип:
   
        sudo -s
   
    Введите пароль.
2. tooinstall сервер MySQL Community edition, введите следующую команду:
   
        zypper install mysql-community-server
   
    Подождите, пока MySQL загрузится и установится.
3. toostart MySQL tooset при загрузке системы hello, введите:
   
        insserv mysql
4. Запустите управляющую программу MySQL hello (mysqld) вручную с помощью следующей команды:
   
        rcmysql start
   
    состояние hello toocheck hello MySQL управляющей программы, введите следующую команду:
   
        rcmysql status
   
    hello toostop MySQL управляющей программы, введите следующую команду:
   
        rcmysql stop
   
   > [!IMPORTANT]
   > После установки по умолчанию пусто пароль учетной записи root MySQL hello. Рекомендуем выполнить скрипт **mysql\_secure\_installation**, который помогает защитить MySQL. Hello скрипт запрашивает пароль учетной записи root MySQL hello toochange анонимным пользователям, отключить имена входа удаленного корневого элемента, удалить тестовые базы данных и удаление перезагрузить hello привилегии таблицы. Рекомендуется, чтобы ответить на Да tooall из этих параметров и изменить пароль учетной записи root hello.
   > 
   > 
5. Введите этот скрипт hello toorun сценарий установки MySQL:
   
        mysql_secure_installation
6. Вход tooMySQL:
   
        mysql -u root -p
   
    Введите пароль пользователя root hello MySQL (который был изменен в предыдущем шаге hello) и будет выведен список с текстом приглашения, где может выдавать toointeract инструкций SQL с базой данных hello.
7. toocreate нового пользователя MySQL, выполните следующие hello в hello **mysql >** строки:
   
        CREATE USER 'mysqluser'@'localhost' IDENTIFIED BY 'password';
   
    Следует отметить, что hello с запятой (;) в конце hello hello строки важны для конца команды hello.
8. toocreate базе данных, а hello `mysqluser` разрешения пользователя на нем hello проблему, следующие команды:
   
        CREATE DATABASE testdatabase;
        GRANT ALL ON testdatabase.* too'mysqluser'@'localhost' IDENTIFIED BY 'password';
   
    Обратите внимание, что базы данных имен пользователей и паролей только используются скриптами соединения toohello базы данных.  Имена учетных записей пользователей базы данных не обязательно представляют действующие учетные записи пользователей в системе hello.
9. toolog в с другого компьютера, тип:
   
        GRANT ALL ON testdatabase.* too'mysqluser'@'<ip-address>' IDENTIFIED BY 'password';
   
    где `ip-address` — IP-адрес компьютера hello, из которого можно подключиться tooMySQL hello.
10. hello tooexit программа администрирования базы данных MySQL, введите следующую команду:
    
        quit

## <a name="add-an-endpoint"></a>Добавление конечной точки
1. После установки MySQL tooconfigure конечная точка tooaccess MySQL потребуется удаленно. Войдите в toohello [классический портал Azure][AzurePortal]. Нажмите кнопку **виртуальные машины**, щелкните имя hello на новую виртуальную машину, затем щелкните **конечные точки**.
2. Нажмите кнопку **добавить** hello нижней части страницы приветствия.
3. Добавить конечную точку с именем «MySQL» с протоколом **TCP**, и **открытый** и **закрытый** порты набор слишком «3306».
4. tooremotely подключения toohello виртуальной машины с компьютера, тип:
   
        mysql -u mysqluser -p -h <yourservicename>.cloudapp.net
   
    Например используя hello виртуальная машина, созданный в этом учебнике, введите эту команду:
   
        mysql -u mysqluser -p -h testlinuxvm.cloudapp.net

[MySQLDocs]: http://dev.mysql.com/doc/
[AzurePortal]: http://manage.windowsazure.com

[Image9]: ./media/install-and-run-mysql-on-opensuse-vm/LinuxVmAddEndpointMySQL.png
