<span data-ttu-id="29fda-101">Выполните эти шаги tooinstall и запустите MongoDB на виртуальной машине под управлением Windows Server.</span><span class="sxs-lookup"><span data-stu-id="29fda-101">Follow these steps tooinstall and run MongoDB on a virtual machine running Windows Server.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="29fda-102">Функции безопасности MongoDB, такие как проверка подлинности и привязка IP-адреса, не включены по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="29fda-102">MongoDB security features, such as authentication and IP address binding, are not enabled by default.</span></span> <span data-ttu-id="29fda-103">Средства безопасности должна быть включена перед развертыванием MongoDB tooa рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="29fda-103">Security features should be enabled before deploying MongoDB tooa production environment.</span></span>  <span data-ttu-id="29fda-104">Дополнительные сведения см. в документе [Безопасность и проверка подлинности](http://www.mongodb.org/display/DOCS/Security+and+Authentication).</span><span class="sxs-lookup"><span data-stu-id="29fda-104">For more information, see [Security and Authentication](http://www.mongodb.org/display/DOCS/Security+and+Authentication).</span></span>
>
>

1. <span data-ttu-id="29fda-105">После подключения toohello виртуальной машины, с помощью удаленного рабочего стола, откройте Internet Explorer из hello **запустить** меню на виртуальной машине hello.</span><span class="sxs-lookup"><span data-stu-id="29fda-105">After you've connected toohello virtual machine using Remote Desktop, open Internet Explorer from hello **Start** menu on hello virtual machine.</span></span>
2. <span data-ttu-id="29fda-106">Выберите hello **средства** кнопку в правом верхнем углу hello.</span><span class="sxs-lookup"><span data-stu-id="29fda-106">Select hello **Tools** button in hello upper right corner.</span></span>  <span data-ttu-id="29fda-107">В **обозревателя**выберите hello **безопасности** , а затем выберите hello **надежных узлов** значок и выберите hello **узлы** кнопка.</span><span class="sxs-lookup"><span data-stu-id="29fda-107">In **Internet Options**, select hello **Security** tab, and then select hello **Trusted Sites** icon, and finally click hello **Sites** button.</span></span> <span data-ttu-id="29fda-108">Добавить *https://\*. mongodb.org* toohello список надежных сайтов.</span><span class="sxs-lookup"><span data-stu-id="29fda-108">Add *https://\*.mongodb.org* toohello list of trusted sites.</span></span>
3. <span data-ttu-id="29fda-109">Go слишком[загружает - MongoDB](https://www.mongodb.com/download-center#community).</span><span class="sxs-lookup"><span data-stu-id="29fda-109">Go too[Downloads - MongoDB](https://www.mongodb.com/download-center#community).</span></span>
4. <span data-ttu-id="29fda-110">Найти hello **текущей стабильной версии** из **сервер сообщества**выберите последнюю hello **64-разрядных** версии в столбце Windows hello.</span><span class="sxs-lookup"><span data-stu-id="29fda-110">Find hello **Current Stable Release** of **Community Server**, select hello latest **64-bit** version in hello Windows column.</span></span> <span data-ttu-id="29fda-111">Загрузить, а затем запустите установщик MSI hello.</span><span class="sxs-lookup"><span data-stu-id="29fda-111">Download, then run hello MSI installer.</span></span>
5. <span data-ttu-id="29fda-112">Приложение MongoDB обычно устанавливается в папку C:\Program Files\MongoDB.</span><span class="sxs-lookup"><span data-stu-id="29fda-112">MongoDB is typically installed in C:\Program Files\MongoDB.</span></span> <span data-ttu-id="29fda-113">Поиск переменные среды на рабочем столе hello и добавить hello MongoDB двоичные файлы путь toohello переменной PATH.</span><span class="sxs-lookup"><span data-stu-id="29fda-113">Search for Environment Variables on hello desktop and add hello MongoDB binaries path toohello PATH variable.</span></span> <span data-ttu-id="29fda-114">Например может оказаться hello двоичные файлы в C:\Program Files\MongoDB\Server\3.4\bin на компьютере.</span><span class="sxs-lookup"><span data-stu-id="29fda-114">For example, you might find hello binaries at C:\Program Files\MongoDB\Server\3.4\bin on your machine.</span></span>
6. <span data-ttu-id="29fda-115">Создание MongoDB каталоги данных и журналов в hello диск данных (например диск **F:**) созданный на предыдущих шагах hello.</span><span class="sxs-lookup"><span data-stu-id="29fda-115">Create MongoDB data and log directories in hello data disk (such as drive **F:**) you created in hello preceding steps.</span></span> <span data-ttu-id="29fda-116">Из **запустить**выберите **командной строки** tooopen окно командной строки.</span><span class="sxs-lookup"><span data-stu-id="29fda-116">From **Start**, select **Command Prompt** tooopen a command prompt window.</span></span>  <span data-ttu-id="29fda-117">Тип:</span><span class="sxs-lookup"><span data-stu-id="29fda-117">Type:</span></span>

        C:\> F:
        F:\> mkdir \MongoData
        F:\> mkdir \MongoLogs
7. <span data-ttu-id="29fda-118">базы данных toorun hello, выполните:</span><span class="sxs-lookup"><span data-stu-id="29fda-118">toorun hello database, run:</span></span>

        F:\> C:
        C:\> mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log

    <span data-ttu-id="29fda-119">Все сообщения журнала, направленной toohello *F:\MongoLogs\mongolog.log* файла, что и сервер mongod.exe начинается и предварительно размещает файлы журнала.</span><span class="sxs-lookup"><span data-stu-id="29fda-119">All log messages are directed toohello *F:\MongoLogs\mongolog.log* file as mongod.exe server starts and preallocates journal files.</span></span> <span data-ttu-id="29fda-120">Он может занять несколько минут для MongoDB toopreallocate hello файлов журнала и начать ожидать соединения.</span><span class="sxs-lookup"><span data-stu-id="29fda-120">It may take several minutes for MongoDB toopreallocate hello journal files and start listening for connections.</span></span> <span data-ttu-id="29fda-121">командную строку Hello остается ориентированы на эту задачу во время выполнения экземпляра MongoDB.</span><span class="sxs-lookup"><span data-stu-id="29fda-121">hello command prompt stays focused on this task while your MongoDB instance is running.</span></span>
8. <span data-ttu-id="29fda-122">hello toostart MongoDB административной оболочки, откройте другой командное окно от **запустить** и типа hello следующие команды:</span><span class="sxs-lookup"><span data-stu-id="29fda-122">toostart hello MongoDB administrative shell, open another command window from **Start** and type hello following commands:</span></span>

        C:\> cd \my_mongo_dir\bin  
        C:\my_mongo_dir\bin> mongo  
        >db  
        test
        > db.foo.insert( { a : 1 } )  
        > db.foo.find()  
        { _id : ..., a : 1 }  
        > show dbs  
        ...  
        > show collections  
        ...  
        > help  

    <span data-ttu-id="29fda-123">Hello база данных создается путем вставки hello.</span><span class="sxs-lookup"><span data-stu-id="29fda-123">hello database is created by hello insert.</span></span>
9. <span data-ttu-id="29fda-124">Кроме того, можно установить файл mongod.exe в качестве службы.</span><span class="sxs-lookup"><span data-stu-id="29fda-124">Alternatively, you can install mongod.exe as a service:</span></span>

        C:\> mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log --logappend  --install

    <span data-ttu-id="29fda-125">В этом случае будет установлена служба с именем MongoDB и описанием Mongo DB.</span><span class="sxs-lookup"><span data-stu-id="29fda-125">A service is installed named MongoDB with a description of "Mongo DB".</span></span> <span data-ttu-id="29fda-126">Hello `--logpath` должен указываться используется toospecify файл журнала, с момента hello запущена служба не имеет toodisplay вывода окна команд.</span><span class="sxs-lookup"><span data-stu-id="29fda-126">hello `--logpath` option must be used toospecify a log file, since hello running service does not have a command window toodisplay output.</span></span>  <span data-ttu-id="29fda-127">Hello `--logappend` параметр указывает на то, что перезапуск службы hello вызывает tooappend toohello существующего файла журнала.</span><span class="sxs-lookup"><span data-stu-id="29fda-127">hello `--logappend` option specifies that a restart of hello service causes output tooappend toohello existing log file.</span></span>  <span data-ttu-id="29fda-128">Hello `--dbpath` указывает расположение hello hello данных каталога.</span><span class="sxs-lookup"><span data-stu-id="29fda-128">hello `--dbpath` option specifies hello location of hello data directory.</span></span> <span data-ttu-id="29fda-129">Дополнительные сведения о параметрах командной строки, связанных со службами, см. [здесь][MongoWindowsSvcOptions].</span><span class="sxs-lookup"><span data-stu-id="29fda-129">For more service-related command-line options, see [Service-related command-line options][MongoWindowsSvcOptions].</span></span>

    <span data-ttu-id="29fda-130">toostart служба hello, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="29fda-130">toostart hello service, run this command:</span></span>

        C:\> net start MongoDB
10. <span data-ttu-id="29fda-131">Теперь, когда MongoDB установлена и запущена, вам требуется tooopen порт в брандмауэре Windows, вы можете удаленно подключиться tooMongoDB.</span><span class="sxs-lookup"><span data-stu-id="29fda-131">Now that MongoDB is installed and running, you need tooopen a port in Windows Firewall so you can remotely connect tooMongoDB.</span></span>  <span data-ttu-id="29fda-132">Из hello **запустить** последовательно выберите пункты **Администрирование** и затем **брандмауэр Windows в режиме повышенной безопасности**.</span><span class="sxs-lookup"><span data-stu-id="29fda-132">From hello **Start** menu, select **Administrative Tools** and then **Windows Firewall with Advanced Security**.</span></span>
11. <span data-ttu-id="29fda-133">) в левой области hello выберите **правила для входящих подключений**.</span><span class="sxs-lookup"><span data-stu-id="29fda-133">a) In hello left pane, select **Inbound Rules**.</span></span>  <span data-ttu-id="29fda-134">В hello **действия** на панели справа, hello выберите **новое правило...** .</span><span class="sxs-lookup"><span data-stu-id="29fda-134">In hello **Actions** pane on hello right, select **New Rule...**.</span></span>

    ![Брандмауэр Windows][Image1]

    <span data-ttu-id="29fda-136">(б) в hello **правило мастера**выберите **порт** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="29fda-136">b) In hello **New Inbound Rule Wizard**, select **Port** and then click **Next**.</span></span>

    ![Брандмауэр Windows][Image2]

    <span data-ttu-id="29fda-138">11.3. Выберите **TCP** и **Определенные локальные порты**.</span><span class="sxs-lookup"><span data-stu-id="29fda-138">c) Select **TCP** and then **Specific local ports**.</span></span>  <span data-ttu-id="29fda-139">Укажите порт «27017» (порт по умолчанию Здравствуй прослушивает MongoDB) и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="29fda-139">Specify a port of "27017" (hello default port MongoDB listens on) and click **Next**.</span></span>

    ![Брандмауэр Windows][Image3]

    <span data-ttu-id="29fda-141">d) выберите **разрешить подключение hello** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="29fda-141">d) Select **Allow hello connection** and click **Next**.</span></span>

    ![Брандмауэр Windows][Image4]

    <span data-ttu-id="29fda-143">11.5. Нажмите кнопку **Далее** еще раз.</span><span class="sxs-lookup"><span data-stu-id="29fda-143">e) Click **Next** again.</span></span>

    ![Брандмауэр Windows][Image5]

    <span data-ttu-id="29fda-145">f) укажите имя для правила hello, например «MongoPort» и нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="29fda-145">f) Specify a name for hello rule, such as "MongoPort", and click **Finish**.</span></span>

    ![Брандмауэр Windows][Image6]

12. <span data-ttu-id="29fda-147">Если не настроить конечную точку для MongoDB при создании виртуальной машины hello, можно сделать сейчас.</span><span class="sxs-lookup"><span data-stu-id="29fda-147">If you didn't configure an endpoint for MongoDB when you created hello virtual machine, you can do it now.</span></span> <span data-ttu-id="29fda-148">Необходимые правила брандмауэра hello и hello конечной точки toobe может tooconnect tooMongoDB удаленно.</span><span class="sxs-lookup"><span data-stu-id="29fda-148">You need both hello firewall rule and hello endpoint toobe able tooconnect tooMongoDB remotely.</span></span>

  <span data-ttu-id="29fda-149">В hello портал Azure, щелкните **виртуальные машины (классические)**, щелкните имя hello на новую виртуальную машину, затем щелкните **конечные точки**.</span><span class="sxs-lookup"><span data-stu-id="29fda-149">In hello Azure portal, click **Virtual Machines (classic)**, click hello name of your new virtual machine, and then click **Endpoints**.</span></span>

    ![Endpoints][Image7]

13. <span data-ttu-id="29fda-151">Щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="29fda-151">Click **Add**.</span></span>

14. <span data-ttu-id="29fda-152">Добавить конечную точку с именем «Mongo», протокол **TCP**и оба **открытый** и **закрытый** порты набор слишком «27017».</span><span class="sxs-lookup"><span data-stu-id="29fda-152">Add an endpoint with name "Mongo", protocol **TCP**, and both **Public** and **Private** ports set too"27017".</span></span> <span data-ttu-id="29fda-153">Открытие этого порта позволяет MongoDB toobe удаленного доступа.</span><span class="sxs-lookup"><span data-stu-id="29fda-153">Opening this port allows MongoDB toobe accessed remotely.</span></span>

    ![Endpoints][Image9]

> [!NOTE]
> <span data-ttu-id="29fda-155">порт Hello 27017 — hello по умолчанию порт MongoDB.</span><span class="sxs-lookup"><span data-stu-id="29fda-155">hello port 27017 is hello default port used by MongoDB.</span></span> <span data-ttu-id="29fda-156">Этот порт по умолчанию можно изменить, указав hello `--port` параметра при запуске сервера mongod.exe hello.</span><span class="sxs-lookup"><span data-stu-id="29fda-156">You can change this default port by specifying hello `--port` parameter when starting hello mongod.exe server.</span></span> <span data-ttu-id="29fda-157">Убедитесь, что toogive hello одинаковый номер порта в брандмауэре hello и hello конечной точки «Mongo» в hello предшествующие инструкции.</span><span class="sxs-lookup"><span data-stu-id="29fda-157">Make sure toogive hello same port number in hello firewall and hello "Mongo" endpoint in hello preceding instructions.</span></span>
>
>

[MongoDownloads]: http://www.mongodb.org/downloads

[MongoWindowsSvcOptions]: http://www.mongodb.org/display/DOCS/Windows+Service


[Image1]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall1.png
[Image2]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall2.png
[Image3]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall3.png
[Image4]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall4.png
[Image5]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall5.png
[Image6]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall6.png
[Image7]: ./media/install-and-run-mongo-on-win2k8-vm/menusendpointadd.png
<!-- Removed 03/08/2017. Not in new portal. -->
<!-- [Image8]: ./media/install-and-run-mongo-on-win2k8-vm/WinVmAddEndpoint2.png
-->
[Image9]: ./media/install-and-run-mongo-on-win2k8-vm/newendpointdetails.png
