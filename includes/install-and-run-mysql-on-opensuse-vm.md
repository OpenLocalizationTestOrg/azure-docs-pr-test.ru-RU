
1. <span data-ttu-id="96f27-101">tooescalate права доступа, тип:</span><span class="sxs-lookup"><span data-stu-id="96f27-101">tooescalate privileges, type:</span></span>
   
        sudo -s
   
    <span data-ttu-id="96f27-102">Введите пароль.</span><span class="sxs-lookup"><span data-stu-id="96f27-102">Enter your password.</span></span>
2. <span data-ttu-id="96f27-103">tooinstall сервер MySQL Community edition, введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="96f27-103">tooinstall MySQL Community Server edition, type:</span></span>
   
        zypper install mysql-community-server
   
    <span data-ttu-id="96f27-104">Подождите, пока MySQL загрузится и установится.</span><span class="sxs-lookup"><span data-stu-id="96f27-104">Wait while MySQL downloads and installs.</span></span>
3. <span data-ttu-id="96f27-105">toostart MySQL tooset при загрузке системы hello, введите:</span><span class="sxs-lookup"><span data-stu-id="96f27-105">tooset MySQL toostart when hello system boots, type:</span></span>
   
        insserv mysql
4. <span data-ttu-id="96f27-106">Запустите управляющую программу MySQL hello (mysqld) вручную с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="96f27-106">Start hello MySQL daemon (mysqld) manually with this command:</span></span>
   
        rcmysql start
   
    <span data-ttu-id="96f27-107">состояние hello toocheck hello MySQL управляющей программы, введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="96f27-107">toocheck hello status of hello MySQL daemon, type:</span></span>
   
        rcmysql status
   
    <span data-ttu-id="96f27-108">hello toostop MySQL управляющей программы, введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="96f27-108">toostop hello MySQL daemon, type:</span></span>
   
        rcmysql stop
   
   > [!IMPORTANT]
   > <span data-ttu-id="96f27-109">После установки по умолчанию пусто пароль учетной записи root MySQL hello.</span><span class="sxs-lookup"><span data-stu-id="96f27-109">After installation, hello MySQL root password is empty by default.</span></span> <span data-ttu-id="96f27-110">Рекомендуем выполнить скрипт **mysql\_secure\_installation**, который помогает защитить MySQL.</span><span class="sxs-lookup"><span data-stu-id="96f27-110">We recommended that you run **mysql\_secure\_installation**, a script that helps secure MySQL.</span></span> <span data-ttu-id="96f27-111">Hello скрипт запрашивает пароль учетной записи root MySQL hello toochange анонимным пользователям, отключить имена входа удаленного корневого элемента, удалить тестовые базы данных и удаление перезагрузить hello привилегии таблицы.</span><span class="sxs-lookup"><span data-stu-id="96f27-111">hello script prompts you toochange hello MySQL root password, remove anonymous user accounts, disable remote root logins, remove test databases, and reload hello privileges table.</span></span> <span data-ttu-id="96f27-112">Рекомендуется, чтобы ответить на Да tooall из этих параметров и изменить пароль учетной записи root hello.</span><span class="sxs-lookup"><span data-stu-id="96f27-112">We recommended that you answer yes tooall of these options and change hello root password.</span></span>
   > 
   > 
5. <span data-ttu-id="96f27-113">Введите этот скрипт hello toorun сценарий установки MySQL:</span><span class="sxs-lookup"><span data-stu-id="96f27-113">Type this toorun hello script MySQL installation script:</span></span>
   
        mysql_secure_installation
6. <span data-ttu-id="96f27-114">Вход tooMySQL:</span><span class="sxs-lookup"><span data-stu-id="96f27-114">Log in tooMySQL:</span></span>
   
        mysql -u root -p
   
    <span data-ttu-id="96f27-115">Введите пароль пользователя root hello MySQL (который был изменен в предыдущем шаге hello) и будет выведен список с текстом приглашения, где может выдавать toointeract инструкций SQL с базой данных hello.</span><span class="sxs-lookup"><span data-stu-id="96f27-115">Enter hello MySQL root password (which you changed in hello previous step) and you'll be presented with a prompt where you can issue SQL statements toointeract with hello database.</span></span>
7. <span data-ttu-id="96f27-116">toocreate нового пользователя MySQL, выполните следующие hello в hello **mysql >** строки:</span><span class="sxs-lookup"><span data-stu-id="96f27-116">toocreate a new MySQL user, run hello following at hello **mysql>** prompt:</span></span>
   
        CREATE USER 'mysqluser'@'localhost' IDENTIFIED BY 'password';
   
    <span data-ttu-id="96f27-117">Следует отметить, что hello с запятой (;) в конце hello hello строки важны для конца команды hello.</span><span class="sxs-lookup"><span data-stu-id="96f27-117">Note, hello semi-colons (;) at hello end of hello lines are crucial for ending hello commands.</span></span>
8. <span data-ttu-id="96f27-118">toocreate базе данных, а hello `mysqluser` разрешения пользователя на нем hello проблему, следующие команды:</span><span class="sxs-lookup"><span data-stu-id="96f27-118">toocreate a database and grant hello `mysqluser` user permissions on it, issue hello following commands:</span></span>
   
        CREATE DATABASE testdatabase;
        GRANT ALL ON testdatabase.* too'mysqluser'@'localhost' IDENTIFIED BY 'password';
   
    <span data-ttu-id="96f27-119">Обратите внимание, что базы данных имен пользователей и паролей только используются скриптами соединения toohello базы данных.</span><span class="sxs-lookup"><span data-stu-id="96f27-119">Note that database user names and passwords are only used by scripts connecting toohello database.</span></span>  <span data-ttu-id="96f27-120">Имена учетных записей пользователей базы данных не обязательно представляют действующие учетные записи пользователей в системе hello.</span><span class="sxs-lookup"><span data-stu-id="96f27-120">Database user account names do not necessarily represent actual user accounts on hello system.</span></span>
9. <span data-ttu-id="96f27-121">toolog в с другого компьютера, тип:</span><span class="sxs-lookup"><span data-stu-id="96f27-121">toolog in from another computer, type:</span></span>
   
        GRANT ALL ON testdatabase.* too'mysqluser'@'<ip-address>' IDENTIFIED BY 'password';
   
    <span data-ttu-id="96f27-122">где `ip-address` — IP-адрес компьютера hello, из которого можно подключиться tooMySQL hello.</span><span class="sxs-lookup"><span data-stu-id="96f27-122">where `ip-address` is hello IP address of hello computer from which you will connect tooMySQL.</span></span>
10. <span data-ttu-id="96f27-123">hello tooexit программа администрирования базы данных MySQL, введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="96f27-123">tooexit hello MySQL database administration utility, type:</span></span>
    
        quit

## <a name="add-an-endpoint"></a><span data-ttu-id="96f27-124">Добавление конечной точки</span><span class="sxs-lookup"><span data-stu-id="96f27-124">Add an endpoint</span></span>
1. <span data-ttu-id="96f27-125">После установки MySQL tooconfigure конечная точка tooaccess MySQL потребуется удаленно.</span><span class="sxs-lookup"><span data-stu-id="96f27-125">After MySQL is installed, you'll need tooconfigure an endpoint tooaccess MySQL remotely.</span></span> <span data-ttu-id="96f27-126">Войдите в toohello [классический портал Azure][AzurePortal].</span><span class="sxs-lookup"><span data-stu-id="96f27-126">Log in toohello [Azure  classic portal][AzurePortal].</span></span> <span data-ttu-id="96f27-127">Нажмите кнопку **виртуальные машины**, щелкните имя hello на новую виртуальную машину, затем щелкните **конечные точки**.</span><span class="sxs-lookup"><span data-stu-id="96f27-127">Click **Virtual Machines**, click hello name of your new virtual machine, and then click **Endpoints**.</span></span>
2. <span data-ttu-id="96f27-128">Нажмите кнопку **добавить** hello нижней части страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="96f27-128">Click **Add** at hello bottom of hello page.</span></span>
3. <span data-ttu-id="96f27-129">Добавить конечную точку с именем «MySQL» с протоколом **TCP**, и **открытый** и **закрытый** порты набор слишком «3306».</span><span class="sxs-lookup"><span data-stu-id="96f27-129">Add an endpoint named "MySQL" with protocol **TCP**, and **Public** and **Private** ports set too"3306".</span></span>
4. <span data-ttu-id="96f27-130">tooremotely подключения toohello виртуальной машины с компьютера, тип:</span><span class="sxs-lookup"><span data-stu-id="96f27-130">tooremotely connect toohello virtual machine from your computer, type:</span></span>
   
        mysql -u mysqluser -p -h <yourservicename>.cloudapp.net
   
    <span data-ttu-id="96f27-131">Например используя hello виртуальная машина, созданный в этом учебнике, введите эту команду:</span><span class="sxs-lookup"><span data-stu-id="96f27-131">For example, using hello virual machine we created in this tutorial, type this command:</span></span>
   
        mysql -u mysqluser -p -h testlinuxvm.cloudapp.net

[MySQLDocs]: http://dev.mysql.com/doc/
[AzurePortal]: http://manage.windowsazure.com

[Image9]: ./media/install-and-run-mysql-on-opensuse-vm/LinuxVmAddEndpointMySQL.png
