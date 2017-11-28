---
title: "aaaInstall MongoDB на виртуальной Машине Windows в Azure | Документы Microsoft"
description: "Дополнительные сведения, способ создания tooinstall MongoDB на ВМ Azure с ОС Windows Server 2012 R2 с моделью развертывания диспетчера ресурсов hello."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 53faf630-8da5-4955-8d0b-6e829bf30cba
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: becd2c607d098e2bc806139e03f2c42f1f01f6f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-mongodb-on-a-windows-vm-in-azure"></a><span data-ttu-id="dc034-103">Установка и настройка базы данных MongoDB на виртуальной машине Windows в Azure</span><span class="sxs-lookup"><span data-stu-id="dc034-103">Install and configure MongoDB on a Windows VM in Azure</span></span>
<span data-ttu-id="dc034-104">[MongoDB](http://www.mongodb.org) — это популярная высокопроизводительная база данных NoSQL с открытым кодом.</span><span class="sxs-lookup"><span data-stu-id="dc034-104">[MongoDB](http://www.mongodb.org) is a popular open-source, high-performance NoSQL database.</span></span> <span data-ttu-id="dc034-105">В этой статье приведены инструкции по установке и настройке MongoDB на виртуальной машине Windows Server 2012 R2 в Azure.</span><span class="sxs-lookup"><span data-stu-id="dc034-105">This article guides you through installing and configuring MongoDB on a Windows Server 2012 R2 virtual machine (VM) in Azure.</span></span> <span data-ttu-id="dc034-106">[MongoDB можно также установить на виртуальной машине Linux в Azure](../linux/install-mongodb.md).</span><span class="sxs-lookup"><span data-stu-id="dc034-106">You can also [install MongoDB on a Linux VM in Azure](../linux/install-mongodb.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dc034-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="dc034-107">Prerequisites</span></span>
<span data-ttu-id="dc034-108">Прежде чем установить и настроить MongoDB, toocreate виртуальной Машины и, в идеальном случае добавьте tooit диска данных.</span><span class="sxs-lookup"><span data-stu-id="dc034-108">Before you install and configure MongoDB, you need toocreate a VM and, ideally, add a data disk tooit.</span></span> <span data-ttu-id="dc034-109">См. следующие статьи toocreate ВМ hello и добавьте диск данных.</span><span class="sxs-lookup"><span data-stu-id="dc034-109">See hello following articles toocreate a VM and add a data disk:</span></span>

* <span data-ttu-id="dc034-110">Создание виртуальной Машины Windows Server с помощью [hello портал Azure](quick-create-portal.md) или [Azure PowerShell](quick-create-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="dc034-110">Create a Windows Server VM using [hello Azure portal](quick-create-portal.md) or [Azure PowerShell](quick-create-powershell.md).</span></span>
* <span data-ttu-id="dc034-111">Присоединение данных диска tooa виртуальной Машины Windows Server с помощью [hello портал Azure](attach-managed-disk-portal.md) или [Azure PowerShell](attach-disk-ps.md).</span><span class="sxs-lookup"><span data-stu-id="dc034-111">Attach a data disk tooa Windows Server VM using [hello Azure portal](attach-managed-disk-portal.md) or [Azure PowerShell](attach-disk-ps.md).</span></span>

<span data-ttu-id="dc034-112">toobegin Установка и настройка MongoDB, [войти в систему виртуальной Машины Windows Server tooyour](connect-logon.md) с помощью удаленного рабочего стола.</span><span class="sxs-lookup"><span data-stu-id="dc034-112">toobegin installing and configuring MongoDB, [log on tooyour Windows Server VM](connect-logon.md) by using Remote Desktop.</span></span>

## <a name="install-mongodb"></a><span data-ttu-id="dc034-113">Установка MongoDB</span><span class="sxs-lookup"><span data-stu-id="dc034-113">Install MongoDB</span></span>
> [!IMPORTANT]
> <span data-ttu-id="dc034-114">Функции безопасности MongoDB, такие как проверка подлинности и привязка IP-адреса, не включены по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="dc034-114">MongoDB security features, such as authentication and IP address binding, are not enabled by default.</span></span> <span data-ttu-id="dc034-115">Средства безопасности должна быть включена перед развертыванием MongoDB tooa рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="dc034-115">Security features should be enabled before deploying MongoDB tooa production environment.</span></span> <span data-ttu-id="dc034-116">Чтобы узнать больше, ознакомьтесь с [системой безопасности и аутентификацией MongoDB](http://www.mongodb.org/display/DOCS/Security+and+Authentication).</span><span class="sxs-lookup"><span data-stu-id="dc034-116">For more information, see [MongoDB Security and Authentication](http://www.mongodb.org/display/DOCS/Security+and+Authentication).</span></span>


1. <span data-ttu-id="dc034-117">После подключения tooyour виртуальную Машину с помощью удаленного рабочего стола, откройте Internet Explorer из hello **запустить** меню hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="dc034-117">After you've connected tooyour VM using Remote Desktop, open Internet Explorer from hello **Start** menu on hello VM.</span></span>
2. <span data-ttu-id="dc034-118">При первом запуске Internet Explorer выберите **Использовать рекомендуемые параметры безопасности, конфиденциальности и совместимости** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="dc034-118">Select **Use recommended security, privacy, and compatibility settings** when Internet Explorer first opens, and click **OK**.</span></span>
3. <span data-ttu-id="dc034-119">Конфигурация усиленной безопасности Internet Explorer включена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="dc034-119">Internet Explorer enhanced security configuration is enabled by default.</span></span> <span data-ttu-id="dc034-120">Добавьте hello MongoDB веб-сайт toohello списка разрешенных сайтов:</span><span class="sxs-lookup"><span data-stu-id="dc034-120">Add hello MongoDB website toohello list of allowed sites:</span></span>
   
   * <span data-ttu-id="dc034-121">Выберите hello **средства** значок в правом верхнем углу hello.</span><span class="sxs-lookup"><span data-stu-id="dc034-121">Select hello **Tools** icon in hello upper-right corner.</span></span>
   * <span data-ttu-id="dc034-122">В **обозревателя**выберите hello **безопасности** , а затем выберите hello **надежных узлов** значок.</span><span class="sxs-lookup"><span data-stu-id="dc034-122">In **Internet Options**, select hello **Security** tab, and then select hello **Trusted Sites** icon.</span></span>
   * <span data-ttu-id="dc034-123">Нажмите кнопку hello **сайтов** кнопки.</span><span class="sxs-lookup"><span data-stu-id="dc034-123">Click hello **Sites** button.</span></span> <span data-ttu-id="dc034-124">Добавить *https://\*. mongodb.org* toohello список надежных сайтов и затем закройте окно hello-диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="dc034-124">Add *https://\*.mongodb.org* toohello list of trusted sites, and then close hello dialog box.</span></span>
     
     ![Настройка параметров безопасности Internet Explorer](./media/install-mongodb/configure-internet-explorer-security.png)
4. <span data-ttu-id="dc034-126">Обзор toohello [загружает MongoDB -](http://www.mongodb.org/downloads) страницы (http://www.mongodb.org/downloads).</span><span class="sxs-lookup"><span data-stu-id="dc034-126">Browse toohello [MongoDB - Downloads](http://www.mongodb.org/downloads) page (http://www.mongodb.org/downloads).</span></span>
5. <span data-ttu-id="dc034-127">При необходимости выберите hello **сервер сообщества** выпуска и hello, а затем выберите последний текущей стабильной выпуск для Windows Server 2008 R2 64-разрядных систем и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="dc034-127">If needed, select hello **Community Server** edition and then select hello latest current stable release for Windows Server 2008 R2 64-bit and later.</span></span> <span data-ttu-id="dc034-128">toodownload Здравствуйте установщика, нажмите кнопку **загрузки (msi)**.</span><span class="sxs-lookup"><span data-stu-id="dc034-128">toodownload hello installer, click **DOWNLOAD (msi)**.</span></span>
   
    ![Скачивание установщика MongoDB](./media/install-mongodb/download-mongodb.png)
   
    <span data-ttu-id="dc034-130">Запустите установщик hello, после завершения загрузки hello.</span><span class="sxs-lookup"><span data-stu-id="dc034-130">Run hello installer after hello download is complete.</span></span>
6. <span data-ttu-id="dc034-131">Прочтите и примите лицензионное соглашение hello.</span><span class="sxs-lookup"><span data-stu-id="dc034-131">Read and accept hello license agreement.</span></span> <span data-ttu-id="dc034-132">Когда появится запрос, выберите **Complete** (Завершить).</span><span class="sxs-lookup"><span data-stu-id="dc034-132">When you're prompted, select **Complete** install.</span></span>
7. <span data-ttu-id="dc034-133">На последнем экране приветствия, нажмите кнопку **установить**.</span><span class="sxs-lookup"><span data-stu-id="dc034-133">On hello final screen, click **Install**.</span></span>

## <a name="configure-hello-vm-and-mongodb"></a><span data-ttu-id="dc034-134">Настройка виртуальной Машины hello и MongoDB</span><span class="sxs-lookup"><span data-stu-id="dc034-134">Configure hello VM and MongoDB</span></span>
1. <span data-ttu-id="dc034-135">переменные пути Hello не обновляются с помощью установщика MongoDB hello.</span><span class="sxs-lookup"><span data-stu-id="dc034-135">hello path variables are not updated by hello MongoDB installer.</span></span> <span data-ttu-id="dc034-136">Без hello MongoDB `bin` расположения в переменной путь требуется полный путь hello toospecify каждый раз при использовании исполняемый объект MongoDB.</span><span class="sxs-lookup"><span data-stu-id="dc034-136">Without hello MongoDB `bin` location in your path variable, you need toospecify hello full path each time you use a MongoDB executable.</span></span> <span data-ttu-id="dc034-137">переменная path tooyour расположение hello tooadd:</span><span class="sxs-lookup"><span data-stu-id="dc034-137">tooadd hello location tooyour path variable:</span></span>
   
   * <span data-ttu-id="dc034-138">Щелкните правой кнопкой мыши hello **запустить** и выбрать пункт **системы**.</span><span class="sxs-lookup"><span data-stu-id="dc034-138">Right-click hello **Start** menu, and select **System**.</span></span>
   * <span data-ttu-id="dc034-139">Выберите **Дополнительные параметры системы**, а затем щелкните **Переменные среды**.</span><span class="sxs-lookup"><span data-stu-id="dc034-139">Click **Advanced system settings**, and then click **Environment Variables**.</span></span>
   * <span data-ttu-id="dc034-140">В разделе **Системные переменные** выберите **Путь** и нажмите кнопку **Изменить**.</span><span class="sxs-lookup"><span data-stu-id="dc034-140">Under **System variables**, select **Path**, and then click **Edit**.</span></span>
     
     ![Настройка переменных PATH](./media/install-mongodb/configure-path-variables.png)
     
     <span data-ttu-id="dc034-142">Добавить путь hello tooyour MongoDB `bin` папки.</span><span class="sxs-lookup"><span data-stu-id="dc034-142">Add hello path tooyour MongoDB `bin` folder.</span></span> <span data-ttu-id="dc034-143">Приложение MongoDB обычно устанавливается в папку *C:\Program Files\MongoDB*.</span><span class="sxs-lookup"><span data-stu-id="dc034-143">MongoDB is typically installed in *C:\Program Files\MongoDB*.</span></span> <span data-ttu-id="dc034-144">Проверьте путь установки hello на ВМ.</span><span class="sxs-lookup"><span data-stu-id="dc034-144">Verify hello installation path on your VM.</span></span> <span data-ttu-id="dc034-145">Hello следующий пример добавляет hello по умолчанию MongoDB установки расположение toohello `PATH` переменной:</span><span class="sxs-lookup"><span data-stu-id="dc034-145">hello following example adds hello default MongoDB install location toohello `PATH` variable:</span></span>
     
     ```
     ;C:\Program Files\MongoDB\Server\3.2\bin
     ```
     
     > [!NOTE]
     > <span data-ttu-id="dc034-146">Быть убедиться, что tooadd hello начальные точки с запятой (`;`) tooindicate, что вы добавляете tooyour расположение `PATH` переменной.</span><span class="sxs-lookup"><span data-stu-id="dc034-146">Be sure tooadd hello leading semicolon (`;`) tooindicate that you are adding a location tooyour `PATH` variable.</span></span>

2. <span data-ttu-id="dc034-147">Создайте каталоги данных и журналов MongoDB на диске данных.</span><span class="sxs-lookup"><span data-stu-id="dc034-147">Create MongoDB data and log directories on your data disk.</span></span> <span data-ttu-id="dc034-148">Из hello **запустить** последовательно выберите пункты **командной строки**.</span><span class="sxs-lookup"><span data-stu-id="dc034-148">From hello **Start** menu, select **Command Prompt**.</span></span> <span data-ttu-id="dc034-149">Следующие примеры Hello создать hello каталоги на диске «f:»</span><span class="sxs-lookup"><span data-stu-id="dc034-149">hello following examples create hello directories on drive F:</span></span>
   
    ```
    mkdir F:\MongoData
    mkdir F:\MongoLogs
    ```
3. <span data-ttu-id="dc034-150">Запуск экземпляра MongoDB с hello следующую команду, настройки hello путь tooyour данных и журналов каталоги соответствующим образом:</span><span class="sxs-lookup"><span data-stu-id="dc034-150">Start a MongoDB instance with hello following command, adjusting hello path tooyour data and log directories accordingly:</span></span>
   
    ```
    mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log
    ```
   
    <span data-ttu-id="dc034-151">Он может занять несколько минут для MongoDB tooallocate hello файлов журнала и начать ожидать соединения.</span><span class="sxs-lookup"><span data-stu-id="dc034-151">It may take several minutes for MongoDB tooallocate hello journal files and start listening for connections.</span></span> <span data-ttu-id="dc034-152">Все сообщения журнала, направленной toohello *F:\MongoLogs\mongolog.log* файл с именем `mongod.exe` server запущен и выделяет файлы журнала.</span><span class="sxs-lookup"><span data-stu-id="dc034-152">All log messages are directed toohello *F:\MongoLogs\mongolog.log* file as `mongod.exe` server starts and allocates journal files.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="dc034-153">командную строку Hello остается ориентированы на эту задачу во время выполнения экземпляра MongoDB.</span><span class="sxs-lookup"><span data-stu-id="dc034-153">hello command prompt stays focused on this task while your MongoDB instance is running.</span></span> <span data-ttu-id="dc034-154">Оставьте hello командной строки окна откройте toocontinue под управлением MongoDB.</span><span class="sxs-lookup"><span data-stu-id="dc034-154">Leave hello command prompt window open toocontinue running MongoDB.</span></span> <span data-ttu-id="dc034-155">Кроме того, можно установить MongoDB как служба, как описано в следующем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="dc034-155">Or, install MongoDB as service, as detailed in hello next step.</span></span>

4. <span data-ttu-id="dc034-156">Для более надежной работы MongoDB, установить hello `mongod.exe` как служба.</span><span class="sxs-lookup"><span data-stu-id="dc034-156">For a more robust MongoDB experience, install hello `mongod.exe` as a service.</span></span> <span data-ttu-id="dc034-157">Создание службы означает, что не требуется tooleave командной строки необходимо toouse MongoDB каждый раз.</span><span class="sxs-lookup"><span data-stu-id="dc034-157">Creating a service means you don't need tooleave a command prompt running each time you want toouse MongoDB.</span></span> <span data-ttu-id="dc034-158">Создайте hello службы следующим образом, Настройка hello путь tooyour каталоги данных и журнала соответственно:</span><span class="sxs-lookup"><span data-stu-id="dc034-158">Create hello service as follows, adjusting hello path tooyour data and log directories accordingly:</span></span>
   
    ```
    mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log `
        --logappend  --install
    ```
   
    <span data-ttu-id="dc034-159">Hello предыдущая команда создает службу с именем MongoDB, с описанием «Mongo DB».</span><span class="sxs-lookup"><span data-stu-id="dc034-159">hello preceding command creates a service named MongoDB, with a description of "Mongo DB".</span></span> <span data-ttu-id="dc034-160">также указываются Hello следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="dc034-160">hello following parameters are also specified:</span></span>
   
   * <span data-ttu-id="dc034-161">Hello `--dbpath` указывает расположение hello hello данных каталога.</span><span class="sxs-lookup"><span data-stu-id="dc034-161">hello `--dbpath` option specifies hello location of hello data directory.</span></span>
   * <span data-ttu-id="dc034-162">Hello `--logpath` должен указываться используется toospecify файла журнала, поскольку работающую службу hello не имеет toodisplay вывода окна команд.</span><span class="sxs-lookup"><span data-stu-id="dc034-162">hello `--logpath` option must be used toospecify a log file, because hello running service does not have a command window toodisplay output.</span></span>
   * <span data-ttu-id="dc034-163">Hello `--logappend` параметр указывает на то, что перезапуск службы hello вызывает tooappend toohello существующего файла журнала.</span><span class="sxs-lookup"><span data-stu-id="dc034-163">hello `--logappend` option specifies that a restart of hello service causes output tooappend toohello existing log file.</span></span>
   
   <span data-ttu-id="dc034-164">hello MongoDB toostart службе, выполните следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="dc034-164">toostart hello MongoDB service, run hello following command:</span></span>
   
    ```
    net start MongoDB
    ```
   
    <span data-ttu-id="dc034-165">Дополнительные сведения о создании службы MongoDB hello см. в разделе [Настройка службы Windows для MongoDB](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-windows/#mongodb-as-a-windows-service).</span><span class="sxs-lookup"><span data-stu-id="dc034-165">For more information about creating hello MongoDB service, see [Configure a Windows Service for MongoDB](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-windows/#mongodb-as-a-windows-service).</span></span>

## <a name="test-hello-mongodb-instance"></a><span data-ttu-id="dc034-166">Экземпляр MongoDB hello теста</span><span class="sxs-lookup"><span data-stu-id="dc034-166">Test hello MongoDB instance</span></span>
<span data-ttu-id="dc034-167">Теперь, когда компонент MongoDB выполняется как один экземпляр или установлен в качестве службы, можно приступить к созданию и использованию баз данных.</span><span class="sxs-lookup"><span data-stu-id="dc034-167">With MongoDB running as a single instance or installed as a service, you can now start creating and using your databases.</span></span> <span data-ttu-id="dc034-168">hello toostart MongoDB административной оболочки, открыть другое окно командной строки от hello **запустить** меню и введите следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="dc034-168">toostart hello MongoDB administrative shell, open another command prompt window from hello **Start** menu, and enter hello following command:</span></span>

```
mongo  
```

<span data-ttu-id="dc034-169">Можно получить список баз данных hello с hello `db` команды.</span><span class="sxs-lookup"><span data-stu-id="dc034-169">You can list hello databases with hello `db` command.</span></span> <span data-ttu-id="dc034-170">Вставьте некоторые данные следующим образом.</span><span class="sxs-lookup"><span data-stu-id="dc034-170">Insert some data as follows:</span></span>

```
db.foo.insert( { a : 1 } )
```

<span data-ttu-id="dc034-171">Выполните поиск данных следующим образом.</span><span class="sxs-lookup"><span data-stu-id="dc034-171">Search for data as follows:</span></span>

```
db.foo.find()
```

<span data-ttu-id="dc034-172">Hello вывода будет примерно toohello следующий пример:</span><span class="sxs-lookup"><span data-stu-id="dc034-172">hello output is similar toohello following example:</span></span>

```
{ "_id" : "ObjectId("57f6a86cee873a6232d74842"), "a" : 1 }
```

<span data-ttu-id="dc034-173">Выход hello `mongo` консоли следующим образом:</span><span class="sxs-lookup"><span data-stu-id="dc034-173">Exit hello `mongo` console as follows:</span></span>

```
exit
```

## <a name="configure-firewall-and-network-security-group-rules"></a><span data-ttu-id="dc034-174">Настройка брандмауэра и правил группы безопасности сети</span><span class="sxs-lookup"><span data-stu-id="dc034-174">Configure firewall and Network Security Group rules</span></span>
<span data-ttu-id="dc034-175">Теперь, когда MongoDB установлены и запущены, откройте порт в брандмауэре Windows, чтобы удаленно подключиться tooMongoDB.</span><span class="sxs-lookup"><span data-stu-id="dc034-175">Now that MongoDB is installed and running, open a port in Windows Firewall so you can remotely connect tooMongoDB.</span></span> <span data-ttu-id="dc034-176">toocreate новое правило для входящего трафика tooallow TCP-порт 27017, откройте командной строке PowerShell с правами администратора и введите hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="dc034-176">toocreate a new inbound rule tooallow TCP port 27017, open an administrative PowerShell prompt and enter hello following command:</span></span>

```powerahell
New-NetFirewallRule `
    -DisplayName "Allow MongoDB" `
    -Direction Inbound `
    -Protocol TCP `
    -LocalPort 27017 `
    -Action Allow
```

<span data-ttu-id="dc034-177">Можно также создать правило hello с помощью hello **брандмауэр Windows в режиме повышенной безопасности** графическое средство управления.</span><span class="sxs-lookup"><span data-stu-id="dc034-177">You can also create hello rule by using hello **Windows Firewall with Advanced Security** graphical management tool.</span></span> <span data-ttu-id="dc034-178">Создайте новое правило для входящего трафика tooallow TCP-порт 27017.</span><span class="sxs-lookup"><span data-stu-id="dc034-178">Create a new inbound rule tooallow TCP port 27017.</span></span>

<span data-ttu-id="dc034-179">При необходимости создайте группы безопасности сети правило tooallow доступа tooMongoDB из вне hello существующей подсети виртуальной сети Azure.</span><span class="sxs-lookup"><span data-stu-id="dc034-179">If needed, create a Network Security Group rule tooallow access tooMongoDB from outside of hello existing Azure virtual network subnet.</span></span> <span data-ttu-id="dc034-180">Hello можно создать правила группы безопасности сети с помощью hello [портал Azure](nsg-quickstart-portal.md) или [Azure PowerShell](nsg-quickstart-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="dc034-180">You can create hello Network Security Group rules by using hello [Azure portal](nsg-quickstart-portal.md) or [Azure PowerShell](nsg-quickstart-powershell.md).</span></span> <span data-ttu-id="dc034-181">С помощью правил брандмауэра Windows hello, разрешить TCP toohello 27017 порта виртуального сетевого интерфейса виртуальной Машины MongoDB.</span><span class="sxs-lookup"><span data-stu-id="dc034-181">As with hello Windows Firewall rules, allow TCP port 27017 toohello virtual network interface of your MongoDB VM.</span></span>

> [!NOTE]
> <span data-ttu-id="dc034-182">TCP-порт 27017 — hello по умолчанию порт MongoDB.</span><span class="sxs-lookup"><span data-stu-id="dc034-182">TCP port 27017 is hello default port used by MongoDB.</span></span> <span data-ttu-id="dc034-183">Этот порт можно изменить с помощью hello `--port` параметра при запуске `mongod.exe` вручную или из службы.</span><span class="sxs-lookup"><span data-stu-id="dc034-183">You can change this port by using hello `--port` parameter when starting `mongod.exe` manually or from a service.</span></span> <span data-ttu-id="dc034-184">Если вы измените порт hello, делает убедиться, что tooupdate hello брандмауэра Windows и группы безопасности сети правила в предыдущих шагах hello.</span><span class="sxs-lookup"><span data-stu-id="dc034-184">If you change hello port, make sure tooupdate hello Windows Firewall and Network Security Group rules in hello preceding steps.</span></span>


## <a name="next-steps"></a><span data-ttu-id="dc034-185">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="dc034-185">Next steps</span></span>
<span data-ttu-id="dc034-186">В этом учебнике вы узнали, как tooinstall и настройте MongoDB на виртуальной Машине Windows.</span><span class="sxs-lookup"><span data-stu-id="dc034-186">In this tutorial, you learned how tooinstall and configure MongoDB on your Windows VM.</span></span> <span data-ttu-id="dc034-187">Теперь вы можете просматривать MongoDB на виртуальной Машине Windows, по следующие дополнительные разделы в hello hello [документацию MongoDB](https://docs.mongodb.com/manual/).</span><span class="sxs-lookup"><span data-stu-id="dc034-187">You can now access MongoDB on your Windows VM, by following hello advanced topics in hello [MongoDB documentation](https://docs.mongodb.com/manual/).</span></span>

